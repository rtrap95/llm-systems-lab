# Learning log

Append one entry after each substantial study or build session. Keep notes factual: what was studied, what was produced, and what remains unclear. Link to code, experiment reports, or result files where possible.

Record only user-reported time spent; use `Not recorded` if the duration is unknown. Update the current snapshot in [`STUDY_STATE.md`](STUDY_STATE.md) when closing the session.

## Entry template

Copy this block for a new session:

```markdown
### YYYY-MM-DD — Phase N: short topic

- Session ID:
- Planned / actual time:
- Focus blocks: (topic, activity, minutes)
- Studied:
- Built or measured:
- Evidence: (file, commit, run, or experiment link)
- What I learned:
- User's own formulation of the vocabulary point: the vocabulary takes a fixed amount of memory (given its size), which weighs more on models with few parameters and less on models with many.
- Open questions / next session:
- Energy / motivation / confidence (optional, 1–5):
```

## Entries

### 2026-09-30 — Phase 1: number formats, prefill/decode, batch and KV cache

- Session ID: 20260930-01
- Planned / actual time: Not stated / 45 minutes (user-reported: 30 during the main session plus 15 added at close; no per-topic breakdown)
- Focus blocks: 01 — `unallocated`, study, 45 minutes. Topics covered, without a time split: matmul, batch size, floating-point formats (FP32/FP16/BF16), weight memory, brief INT8 discussion, autoregressive generation loop, prefill vs decode, batching, KV cache, written note, then follow-up questions on frontier model sizes, FP32-to-BF16 casting, tokenizer/vocabulary, fine-tuning, MoE active vs total parameters, MLP, arithmetic intensity.
- Studied: what matmul and batch size are; FP32/FP16/BF16 layout (sign/exponent/mantissa); weight memory per parameter; why INT8 is not simply used everywhere (rounding error, activation outliers, training stability, calibration); end-to-end generation (tokenizer, embedding, layers, output token, repeat); prefill (compute-bound) vs decode (memory-bound); why batching amortizes weight reads; what the KV cache stores (K and V per token, per layer) and why it limits batch size. Follow-up questions: parameter and layer counts of open-weight models (Llama 3 70B and 405B, DeepSeek-V3; closed frontier models do not publish them); casting FP32 to BF16 after training (one-way); the vocabulary comes from the tokenizer (BPE on a corpus) and is fixed before training; fine-tuning updates weights (full vs LoRA); MoE total vs active parameters; what the MLP is and that it holds most of a layer's parameters; arithmetic intensity (operations per byte read).
- Built or measured: Hand calculations only. 1B parameters = 3.725 GiB in FP32 and 1.863 GiB in FP16/BF16; 7B in FP16 is about 13 GiB and tight on a 16 GB GPU. KV cache estimate for a 7B-style model (32 layers, hidden size 4096, FP16): about 0.5 MiB per token; 64 layers doubles it, INT8 halves it. Traced a 100-token prompt generating 50 tokens: 1 prefill step plus 49 decode steps. Embedding table for a 100,000-token vocabulary and 4096-dim vectors: about 410M parameters, 0.76 GiB in BF16; about 5.9% of a 7B model (about 11.7% with a separate output matrix). MoE example, 100B total and 10B active in BF16: 200 GB of weights, 20 GB read per token at batch 1. No code or benchmarks were run.
- Evidence: the written note below; no code or experiment files.
- What I learned (user's note, dictated, with corrections from review):
  - Weights can be stored as FP32 (4 bytes; 8 exponent and 23 mantissa bits), FP16 (2 bytes; 5 and 10) or BF16 (2 bytes; 8 and 7). Fewer bytes per weight cost memory less but reduce precision; BF16 keeps FP32's range.
  - Prefill processes the whole prompt in one step (large matmuls, compute-bound) and yields the first token. Decode takes one token per step, reuses cached Keys/Values, and rereads all weights each step (memory-bound).
  - Batching serves several sequences per weight read, but each sequence has its own KV cache, so memory is the limit.
  - Corrections from review: memory depends on bytes per parameter, not per token; "28" in the dictation was likely INT8; the KV cache holds Keys and Values, not "all previous calculations"; batch size is the number of sequences processed together, not a fill level. Generation does not restart from zero when memory runs low. It stops at an end token or length limit. Recomputing a prefill after dropping a request's cache (preemption) is a server-side exception, to be studied in Phase 5.
- Consolidated note (user's content, with the ending rewritten after review):
  > **Weights and memory.** Weights can be stored as FP32 (4 bytes), FP16 (2) or BF16 (2). Fewer bytes per weight means less memory and less data to read, at the cost of precision. BF16 keeps FP32's exponent range (8 bits) with a shorter mantissa (7 bits). **Inference.** Prefill processes the whole prompt in one step (large matmuls, compute-bound) and produces the first token. Decode then takes only the last generated token per step, reuses the Keys and Values of earlier tokens from the KV cache, and rereads all weights each step (memory-bound). **Batch and KV cache.** Batch size is the number of sequences processed together. One read of the weights serves all of them, so throughput rises. Each sequence has its own KV cache, which grows with its length and with the number of layers, so memory bounds how many sequences fit and how long they can be. Generation does not restart from zero: a sequence ends at an end token or a length limit, and its cache is kept until then. If a server runs out of memory, it may drop a request's cache and recompute the prefill later; that is an exception, covered in Phase 5.
- User's own formulation of the vocabulary point: the vocabulary takes a fixed amount of memory (given its size), which weighs more on models with few parameters and less on models with many.
- Open questions / next session:
  - Re-explain in own words how batch size and KV cache memory interact, since the last part of the dictated note was the weakest.
  - No local GPU; decide how to run the first benchmark (CPU with a small model, optionally a short cloud GPU run later).
- Energy / motivation / confidence (optional, 1–5): Not provided

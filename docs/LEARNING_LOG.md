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
- Open questions / next session:
- Energy / motivation / confidence (optional, 1–5):
```

## Entries

### 2026-09-30 — Phase 1: number formats, prefill/decode, batch and KV cache

- Session ID: 20260930-01
- Planned / actual time: Not stated / Not recorded
- Focus blocks:
  - 01 — `llm_fundamentals`, study: matmul, batch size, floating-point formats (FP32/FP16/BF16), weight memory, brief INT8 discussion (minutes not recorded)
  - 02 — `inference`, study: autoregressive generation loop, prefill vs decode, batch size, KV cache, written note (minutes not recorded)
- Studied: what matmul and batch size are; FP32/FP16/BF16 layout (sign/exponent/mantissa); weight memory per parameter; why INT8 is not simply used everywhere (rounding error, activation outliers, training stability, calibration); end-to-end generation (tokenizer, embedding, layers, output token, repeat); prefill (compute-bound) vs decode (memory-bound); why batching amortizes weight reads; what the KV cache stores (K and V per token, per layer) and why it limits batch size.
- Built or measured: Hand calculations only. 1B parameters = 3.725 GiB in FP32 and 1.863 GiB in FP16/BF16; 7B in FP16 is about 13 GiB and tight on a 16 GB GPU. KV cache estimate for a 7B-style model (32 layers, hidden size 4096, FP16): about 0.5 MiB per token; 64 layers doubles it, INT8 halves it. Traced a 100-token prompt generating 50 tokens: 1 prefill step plus 49 decode steps. No code or benchmarks were run.
- Evidence: the written note below; no code or experiment files.
- What I learned (user's note, dictated, with corrections from review):
  - Weights can be stored as FP32 (4 bytes; 8 exponent and 23 mantissa bits), FP16 (2 bytes; 5 and 10) or BF16 (2 bytes; 8 and 7). Fewer bytes per weight cost memory less but reduce precision; BF16 keeps FP32's range.
  - Prefill processes the whole prompt in one step (large matmuls, compute-bound) and yields the first token. Decode takes one token per step, reuses cached Keys/Values, and rereads all weights each step (memory-bound).
  - Batching serves several sequences per weight read, but each sequence has its own KV cache, so memory is the limit.
  - Corrections from review: memory depends on bytes per parameter, not per token; "28" in the dictation was likely INT8; the KV cache holds Keys and Values, not "all previous calculations"; batch size is the number of sequences processed together, not a fill level. Generation does not restart from zero when memory runs low. It stops at an end token or length limit. Recomputing a prefill after dropping a request's cache (preemption) is a server-side exception, to be studied in Phase 5.
- Open questions / next session:
  - Re-explain in own words how batch size and KV cache memory interact, since the last part of the note was the weakest.
  - No local GPU; decide how to run the first benchmark (CPU with a small model, optionally a short cloud GPU run later).
- Energy / motivation / confidence (optional, 1–5): Not provided

# Study state

This is the concise source of truth for where to resume. Update it at the end of each study session under the rules in the repository's `AGENTS.md`. Structured time and activity records live in [`data/`](../data/README.md).

**Last updated:** 2026-09-30  
**Current phase:** Phase 1 — Foundations  
**Phase status:** In progress  
**Latest session:** 2026-09-30 (`20260930-01`), 30 minutes logged — see [learning log](LEARNING_LOG.md)

## Phase status

- [ ] Phase 1 — ML, PyTorch, Transformer, and inference fundamentals (in progress)
- [ ] Phase 2 — Semantic search and RAG
- [ ] Phase 3 — CUDA fundamentals
- [ ] Phase 4 — GPU performance and Triton
- [ ] Phase 5 — LLM inference and serving
- [ ] Phase 6 — Quantization and capstone

## Progress and evidence

- Session 1 covered number formats (FP32/FP16/BF16), weight memory, the generation loop, prefill vs decode, batching, and KV cache. Evidence: a written note and hand calculations in the [learning log](LEARNING_LOG.md); no code or benchmark yet.
- Not yet covered in Phase 1: neural network basics, attention and tokenization in more detail, PyTorch, and GPU memory in practice.
- Phase 1 exit evidence (a reproducible benchmark report) does not exist yet.
- Logged time so far: 30 minutes (one session, no topic breakdown). A single session is too little data for a trend against the 10–12 hours/week target.

## Next recommended activity

Phase 1, planning (about 45 minutes): define the first benchmark on CPU. Start by rewriting the last part of the note (batch size vs KV cache memory) in your own words, then choose a small model, the variables (dtype FP32 vs BF16, batch size, sequence length), and the metrics (prefill latency, decode tokens/sec, memory) in `docs/EXPERIMENTS.md`. Expected result: a written benchmark plan before any setup.

## Open questions / blockers

- No local GPU. Plan fundamentals on CPU and decide later whether a short cloud GPU run is needed.
None other recorded.

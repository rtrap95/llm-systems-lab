# Learning roadmap

## Outcome

Over six months, build on senior software engineering experience to gain practical depth across LLM applications and the systems underneath them. The path moves from ML and inference fundamentals through retrieval, GPU programming, serving, and quantization. The target specialization remains open until there is hands-on evidence to choose among AI Engineering, AI Systems / Infrastructure, inference performance, and adjacent paths.

**Planned pace:** 10–12 hours per week.  
**Current status:** Tracked in [`STUDY_STATE.md`](STUDY_STATE.md). Begin Phase 1 when the first study session is logged; do not infer dates from this sequence.

## Phases

| Phase | Focus | Study and build | Exit artifact / evidence |
| --- | --- | --- | --- |
| 1 — Foundations | ML, PyTorch, Transformer, and inference basics | Tensors and matrix multiplication; neural networks; attention and tokenization; autoregressive generation; FP32/FP16/BF16; GPU memory. Build a small-model benchmark and vary batch size, sequence length, and dtype where hardware permits. | A reproducible benchmark report with latency, tokens/sec, memory, workload, device, and software versions. Explain at least one observed performance change. |
| 2 — Retrieval | Embeddings, semantic search, and RAG | Chunking; vector and hybrid search; reranking; retrieval evaluation; answer grounding. Build an editorial-document RAG pipeline and a 30–50 question evaluation set. | Pipeline plus evaluation report covering retrieval quality, answer quality, latency, and token usage. Record how the evaluation set was assembled. |
| 3 — CUDA fundamentals | GPU execution and memory | Threads, blocks, grids, warps, SMs, global/shared memory, registers, synchronization, and memory coalescing. Implement vector addition, element-wise operations, reduction, softmax, and matrix multiplication. | Correctness checks and PyTorch-versus-CUDA measurements, with an explanation of bottlenecks and hardware limits. |
| 4 — GPU performance and Triton | Profiling and kernel optimization | Occupancy, register pressure, bandwidth, compute- versus memory-bound work, cache, warp utilization, launch overhead, Nsight, and Triton. Implement vector addition, softmax, layer norm, matmul, and attention as feasible. | A comparison of PyTorch, Triton, and CUDA implementations with profiler evidence for selected cases. |
| 5 — LLM inference | Serving, batching, and KV cache | KV cache; batching and continuous batching; PagedAttention; prefix caching; memory management; throughput and latency. Benchmark a serving stack across sequence length and concurrency. | Report TTFT, end-to-end latency, throughput, tokens/sec, memory, and GPU utilization where available. State the serving configuration and workload. |
| 6 — Quantization and capstone | Quality/performance trade-offs | FP32, FP16, BF16, INT8, INT4; weight-only and activation quantization; PTQ/QAT; GPTQ/AWQ concepts. Compare supported formats on one documented workload. | Capstone report comparing memory, latency, throughput, and output quality, including limitations and a next-step recommendation. |

## Checkpoints

### After Phase 2

Review the learning log and ask:

- Did retrieval, evaluation, and product-facing LLM work hold my interest?
- Did I prefer implementation, measurement, or operating the system?
- What part of CUDA/GPU work do I still want to test before drawing conclusions?

Keep going into GPU work even if RAG was enjoyable; the plan is designed to provide evidence across both layers.

### After Phase 4

Review whether kernel programming and profiling are engaging enough to justify deeper inference optimization. Check whether the time and cloud hardware used have produced interpretable evidence, rather than chasing a particular speedup.

### After Phase 6

Write a short direction note in `docs/DECISIONS.md`: strongest interest, strongest evidence, remaining uncertainty, and a 90-day follow-up plan. Possible outcomes include AI Engineering, AI Systems / Infrastructure, inference optimization, Research Engineering, or a pivot toward distributed systems/performance or cybersecurity plus AI.

## Initial resource list

Start with the resources already selected for this plan; add or replace resources only when a concrete gap appears.

- [PyTorch Tutorials](https://pytorch.org/tutorials/)
- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course)
- [NVIDIA CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/)
- [GPU MODE lectures](https://github.com/gpu-mode/lectures)
- [GPU Puzzles](https://github.com/srush/GPU-Puzzles)
- [NVIDIA CUDA C++ Best Practices Guide](https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/)
- [Triton tutorials](https://triton-lang.org/main/getting-started/tutorials/)
- [vLLM documentation](https://docs.vllm.ai/)
- DeepLearning.AI: *Fast and Efficient LLM Inference with vLLM* (course named in the initial plan; add the exact course link when starting Phase 5).

## Adjusting the roadmap

This is a hypothesis about a useful learning order, not a promise to finish every kernel or tool. Log material changes in `docs/DECISIONS.md`. Keep the phase exit artifact focused on what was learned and measured; if hardware or time blocks an implementation, record the limitation and complete an alternative that tests the same concept.

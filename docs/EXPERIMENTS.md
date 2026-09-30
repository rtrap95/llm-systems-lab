# Experiment and benchmark protocol

Use this protocol for performance comparisons and evaluation runs. The aim is to make a result understandable and repeatable, including when a future run disagrees with it.

## Before implementation

1. State the problem and a testable hypothesis.
2. Define the workload: model and revision, input/output lengths, batch or concurrency, dtype, and relevant settings.
3. Decide how correctness or output quality will be checked.
4. Identify the baseline and which factor is changing in the comparison.
5. Record device and software versions before collecting results.

## Measurement

- Run a correctness check before timing.
- Separate startup, compilation, and warm-up from steady-state measurements; state what is included.
- Use repeated runs and report the summary statistic (at minimum median; include p95 when useful) and sample count.
- Keep workload and environment fixed for a direct comparison. If more than one factor changes, call that out.
- Capture profiler evidence only when it helps explain the measured result.
- Record failures and inconvenient results; do not silently discard them.

## Metrics by experiment type

| Type | Useful measurements |
| --- | --- |
| Model inference | Time to first token (TTFT), inter-token latency or end-to-end latency, tokens/sec, peak GPU memory, batch and sequence lengths |
| Serving | TTFT, request latency (including p50/p95), throughput, concurrency, queueing behavior, peak memory, GPU utilization if available |
| Kernel | Correctness/error tolerance, latency, effective bandwidth or throughput when meaningful, launch configuration, profiler observations |
| Retrieval / RAG | Recall@k or another named retrieval metric, reranker impact, grounded answer quality, latency by stage, token usage, evaluation set size and method |
| Quantization | Quality metric or fixed evaluation procedure, model memory, latency, throughput, dtype/format, workload |

Define each metric precisely in the experiment report when its meaning could be ambiguous. Do not compare numbers produced with different workload definitions as if they were directly comparable.

## Report and results

Start from [`experiments/template/README.md`](../experiments/template/README.md). Store per-experiment code and narrative under `experiments/<id>-<slug>/`; store compact measurements and environment metadata under `results/<id>-<slug>/`. Link the two in both directions.

Commit small CSV/JSON summaries and plots when they help reproduce or understand the conclusion. Do not commit model weights, raw datasets, or bulky profiler captures. See [results guidance](../results/README.md).

## Conclusion format

Separate these statements in the report:

- **Observed:** what the measurements show.
- **Explanation:** the mechanism that best fits the evidence.
- **Uncertainty:** what was not controlled or measured.
- **Next experiment:** the smallest follow-up that could disprove the explanation.

# LLM Systems Lab

A hands-on learning lab for building on senior software engineering experience and exploring AI engineering, AI systems, and inference infrastructure.

The goal is to learn by measuring real systems. Each substantial exercise should connect a problem to a hypothesis, an implementation, a benchmark, profiling evidence, and a conclusion. This repository is a learning and portfolio project; it does not claim that every experiment generalizes beyond its recorded hardware and workload.

## Start here

1. Check the [current study state](docs/STUDY_STATE.md), then read the [learning roadmap](docs/LEARNING_ROADMAP.md).
2. Copy the [learning log entry](docs/LEARNING_LOG.md) when you finish a study session.
3. Copy the [experiment template](experiments/template/README.md) before starting a benchmark.
4. Follow the [experiment protocol](docs/EXPERIMENTS.md) and keep small, reproducible result artifacts in `results/`.

No local GPU or Python environment is required for this documentation scaffold. Set up tools when an experiment needs them; use cloud GPU time selectively during the early exploration.

## Repository map

| Path | Purpose |
| --- | --- |
| `docs/LEARNING_ROADMAP.md` | Six-month sequence, deliverables, and review points |
| `docs/STUDY_STATE.md` | Current phase, progress evidence, blockers, and next activity |
| `docs/LEARNING_LOG.md` | Session notes and evidence of progress |
| `data/` | Structured session and focus-block records for later analysis |
| `docs/DECISIONS.md` | Current constraints and decisions to revisit |
| `docs/EXPERIMENTS.md` | Repeatable benchmark and reporting protocol |
| `experiments/` | Experiment briefs, code, and per-experiment notes |
| `benchmarks/` | Shared benchmark harnesses and metric definitions |
| `pytorch/` | Tensor, model, and inference fundamentals |
| `cuda/` | CUDA concepts and kernels |
| `triton/` | Triton kernels and comparisons |
| `vllm/` | LLM serving and inference experiments |
| `results/` | Compact measurements, environment metadata, and plots |

The module directories are intentionally lightweight. Add code and environment files alongside the first exercise that needs them, rather than installing every tool up front.

## Learning cadence

Planned effort is about 10–12 hours per week. A useful starting split is 4–5 hours of study, 4–5 hours of implementation and measurement, and 1–2 hours to document findings. Adjust it to the week; preserve the evidence and conclusions even when the schedule slips.

## Working principles

- Build small artifacts that answer a question; do not stop at reproducing a tutorial.
- Record the device, software versions, workload, and measurement method with each result.
- Establish correctness and a baseline before tuning.
- Separate observed measurements from explanations and hypotheses.
- Revisit the specialization choice at the roadmap checkpoints; it is deliberately undecided.
- Use the tutor check-ins to calibrate pace; the weekly hours are a planning target, not a judgment.
- Keep large model weights, datasets, and profiler captures out of Git. See `.gitignore` and [results guidance](results/README.md).

## Current status

See [`docs/STUDY_STATE.md`](docs/STUDY_STATE.md) for the current phase and next recommended activity. The roadmap is a sequence of learning phases, not calendar commitments.

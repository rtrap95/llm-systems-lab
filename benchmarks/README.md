# Benchmarks

Put reusable benchmark runners and shared metric definitions here. Keep experiment-specific hypotheses, workload decisions, and conclusions in the corresponding `experiments/` report.

## Guidelines

- Verify correctness before collecting performance numbers.
- Make warm-up, compilation, synchronization, and timed regions explicit.
- Keep the workload configurable and record its full configuration with every run.
- Prefer machine-readable output for measurements, with units and enough metadata to interpret it.
- Avoid a single generic benchmark that hides model, kernel, or serving-specific assumptions.

No benchmark harness has been added yet. Add one with the first Phase 1 experiment and document its invocation here.

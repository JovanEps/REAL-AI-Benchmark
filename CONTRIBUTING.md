# Contributing to REAL-AI-Benchmark

Contributions are welcome if they improve reproducibility, evaluation clarity, benchmark coverage, implementation quality, or documentation.

## Accepted contribution types

- new model run logs,
- verified reference solutions,
- corrected benchmark implementations,
- reproducible Zig/C/Python tooling,
- scoring-rubric improvements,
- charts and result tables,
- hardware-profile reports,
- documentation fixes.

## Submission rules

1. Preserve the original model output whenever possible.
2. Include model name, version/provider, quantization, context length, inference settings, runtime, output speed, and hardware profile.
3. Include whether code compiled and, if it failed, the exact compiler/runtime error.
4. Do not silently repair model answers. Corrected versions must be marked as corrected and kept separate from raw outputs.
5. Use the component-based scoring methodology from `docs/scoring-rubric.md`.
6. For GO-6 multimodal runs, explicitly state whether the five instrument images were attached and visible to the model.
7. For text-only GO-6 runs, label the benchmark as `GO-6-old-simple-no-VI`.

## Suggested log naming

```text
results/raw-logs/GO-4_ModelName_Quantization_Run01.md
results/raw-logs/GO-5_ModelName_API_Run01.md
results/raw-logs/GO-6_ModelName_Multimodal_Run01.json
```

## Review principle

The benchmark is not a popularity contest between model vendors. Scores should be based on visible task achievements, reproducibility, and the published rubric.

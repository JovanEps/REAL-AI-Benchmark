# Evaluation Methodology

REAL-AI-Benchmark uses a component-based score from **0 to 10**.

The evaluator does not assign a score by general impression alone. Each benchmark has required elements, and each element contributes a defined portion of the total score. The final score is the weighted sum of visible achievements.

## General scoring dimensions

| Dimension | Typical weight | Description |
|---|---:|---|
| Final correctness | 2.0–3.0 | Correct final answer, exact values, no contradiction |
| Reasoning procedure | 2.0–2.5 | Step-by-step derivation, traceability, mathematical discipline |
| Completeness | 1.0–1.5 | Covers all required sections and edge cases |
| Proof / validation | 0.5–1.5 | Minimality proof, uniqueness proof, inverse check, physical validation |
| Code quality | 1.0–2.0 | Clean implementation, correctness, maintainability |
| Code execution | 0.5–1.5 | Compiles/runs when code is required |
| Reporting format | 0.5–1.0 | Tables, JSON, reproducible output, clarity |

Exact weights may differ by benchmark.

## Important rule

A bad code section should not automatically collapse the whole score if the benchmark gives limited weight to code. Conversely, if a benchmark is explicitly code-heavy, compilation and runtime behavior may carry higher weight.

The same rule must be applied consistently across all models. A model should not be penalized or protected because of vendor name, local/cloud status, parameter count, or prior expectation.

## GO-6 multimodal extension

GO-6 adds a visual-physical layer:

- analog instrument reading,
- nominal values plus measurement intervals,
- fuzzy inference,
- dynamic simulation,
- final action choice,
- executable verification.

The text-only `GO-6-old-simple-no-VI` variant should be scored separately from the multimodal GO-6 run because it does not test visual instrument reading.

## Reproducibility

A run should include:

- model version/name,
- local/API provider,
- quantization,
- context size,
- hardware,
- runtime,
- output speed,
- exact prompt,
- exact response,
- compile/run result if applicable,
- score and evaluator notes.

# Scoring Rubric

This file defines the default 10-point structure. Individual GO benchmarks may refine it.

## Default 10-point score

| Component | Points |
|---|---:|
| Correct final result | 2.5 |
| Correct intermediate reasoning | 2.0 |
| Completeness of required sections | 1.5 |
| Proof / validation / inverse check | 1.0 |
| Code implementation quality | 1.5 |
| Code compilation and executable behavior | 1.0 |
| Structured final output / JSON / readability | 0.5 |

## Score interpretation

| Score | Interpretation |
|---:|---|
| 9.0–10.0 | Reference-level or near-reference solution |
| 8.0–8.9 | Strong solution with limited defects |
| 7.0–7.9 | Good but incomplete, fragile, or with code/reporting defects |
| 5.0–6.9 | Partially correct but unreliable or substantially incomplete |
| 3.0–4.9 | Major reasoning/code failure but useful fragments exist |
| 0.0–2.9 | Mostly invalid or unusable result |

## GO-6 recommended 100-point decomposition

| Section | Element | Points |
|---|---|---:|
| A | Reading five analog instruments, nominal values, intervals, short justification | 15 |
| B | Physical consistency and understanding of system-channel conflict | 10 |
| C | Fuzzy memberships, rule activations, aggregated risk, initial fuzzy decision | 20 |
| D | Three-step simulation of all four actions and outcome classification | 20 |
| E | Final decision, A2 selection, uniqueness proof, explanation why fuzzy decision is not final | 15 |
| F | Zig implementation quality, algorithmic completeness, result reproduction | 15 |
| G | Required format, `RESULTS_JSON`, `<END>` marker, clarity | 5 |

The 100-point GO-6 score can be divided by 10 for the standard 0–10 score.

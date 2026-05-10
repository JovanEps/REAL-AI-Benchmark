# REAL-AI-Benchmark

**REAL-AI-Benchmark** is an independent practical benchmark suite for evaluating AI/LLM/LMM systems on tasks that resemble real technical work rather than synthetic leaderboard exercises.

The project evaluates what a model actually produces: reasoning traceability, numerical correctness, formal proof discipline, executable code, reproducible output, structured reporting, and physical/multimodal perception from analog instruments.

> Real tasks. Real models. Real results.

## What this repository contains

The suite currently contains seven GO benchmark tasks and related methodology documents.

| Benchmark | Short purpose | Main evaluated capability |
|---|---|---|
| **GO-1** | Minimal correction of an RBAC/DSS policy | logical consistency, constraint checking, minimality proof |
| **GO-2** | Discrete LIF neuron with exact arithmetic | exact fractional computation, invariant proof, Python verification |
| **GO-3** | 2D valid convolution in C99 | manual numerical derivation, matrix reasoning, C implementation |
| **GO-4** | 4x4 Latin-square solver in Zig | combinatorial search, bitmasks, uniqueness proof, executable Zig |
| **GO-5** | Seeded Mealy transducer and one-symbol forensic correction | formal generation, simulation, Hamming analysis, uniqueness proof, Zig verification |
| **GO-6** | Physical-causal fuzzy dynamics with analog instruments | multimodal sensor reading, measurement intervals, fuzzy inference, short-horizon dynamics, decision proof, Zig verification |
| **GO-6+** | Robust physical-AI decision benchmark with decoy instruments | analog perception, decoy filtering, calibration, nonlinear dynamics, pessimistic simulation, robust action selection, Zig verifier |

GO-6 also has a text-only control version named **GO-6-old-simple-no-VI**, intended for models that cannot process images. The main GO-6 benchmark is the multimodal version using `PIC1.png`–`PIC5.png`.

GO-6+ is a separate and harder extension of GO-6 Rev. 1.1. It uses `Fig-1.png`–`Fig-9.png` images inside `Figure_set2/`, requires hidden instrument mapping, raw/corrected reading handling, decoy rejection, nominal and pessimistic simulation, and robust-best action selection.

## Repository layout

```text
REAL-AI-Benchmark/
├── README.md
├── CONTRIBUTING.md
├── SPONSORSHIP.md
├── LICENSE
├── LICENSE.txt
├── NOTICE.md
├── CITATION.cff
├── CHANGELOG.md
├── REAL-AI-Bench-Linkedin-promo.png
├── zenodo.json
├── assets/
│   ├── logo.png
│   └── social-preview.png
├── docs/
│   ├── benchmark-integrity.md
│   ├── evaluation-methodology.md
│   ├── license-and-citation.md
│   ├── reproducibility.md
│   └── scoring-rubric.md
├── GO-1/
│   └── GO-1.txt
├── GO-2/
│   └── GO-2.txt
├── GO-3/
│   └── GO-3.txt
├── GO-4/
│   └── GO-4.txt
├── GO-5/
│   └── GO-5.txt
├── GO-6 Ultimate reality/
│   ├── GO-6.txt
│   ├── GO-6-old-simple-no-VI.txt
│   └── PIC1.png ... PIC5.png
├── GO-6+ Next Ultimate reality/
│   ├── GO-6+.txt
│   ├── README.md
│   └── Figure_set2/
│       ├── Fig-1.png
│       ├── Fig-2.png
│       ├── Fig-3.png
│       ├── Fig-4.png
│       ├── Fig-5.png
│       ├── Fig-6.png
│       ├── Fig-7.png
│       ├── Fig-8.png
│       └── Fig-9.png
├── Methodology/
│   └── methodology papers and draft reports
└── results/
    └── tables/
```

## GO-6+ Next Ultimate reality

`GO-6+ Next Ultimate reality` is the extended robust physical-AI benchmark in the GO-6 family.

It expands GO-6 Rev. 1.1 with a more demanding multimodal and engineering-oriented task structure:

- hidden `Fig-*` analog instrument mapping;
- nine analog instrument images;
- six relevant physical variables;
- three decoy instruments;
- raw and corrected readings;
- calibration handling;
- fuzzy inference;
- nonlinear physical dynamics;
- nominal and pessimistic simulations;
- robust action selection;
- executable Zig verifier;
- strict `RESULTS_JSON` audit output.

The GO-6+ benchmark is designed to test not only whether a model can compute a nominal answer, but whether it can robustly reason from imperfect analog measurements under uncertainty.

Folder:

```text
GO-6+ Next Ultimate reality/
├── GO-6+.txt
├── README.md
└── Figure_set2/
    ├── Fig-1.png
    ├── Fig-2.png
    ├── Fig-3.png
    ├── Fig-4.png
    ├── Fig-5.png
    ├── Fig-6.png
    ├── Fig-7.png
    ├── Fig-8.png
    └── Fig-9.png
```

Related methodology documents are available in:

```text
Methodology/
├── GO-6+_Next_Ultimate_reality_metodologija_SR.pdf
└── GO-6+_Next_Ultimate_reality_Methodology_EN.pdf
```

GO-6+ should be treated as a separate benchmark from GO-6 Rev. 1.1. Scores from GO-6 and GO-6+ should not be directly compared without explicitly stating the test version.

## Evaluation principle

Each model run is scored using a **component-based 0–10 methodology**. The score is not assigned by general impression and no component is arbitrarily made “fatal” unless the benchmark definition explicitly gives it high weight.

The evaluator adds what the model demonstrably achieved:

1. correct final result,
2. correct intermediate reasoning,
3. completeness of required sections,
4. proof, validation, or inverse check,
5. code implementation quality,
6. compilation/execution behavior where code is required,
7. structured final output and machine-readable reporting,
8. multimodal input interpretation where images are part of the task,
9. robustness analysis where the benchmark requires nominal and pessimistic scenarios.

This makes comparisons auditable and prevents inconsistent scoring across model families.

## Benchmark versioning

Results must always identify the exact benchmark version:

| Label | Meaning |
|---|---|
| `GO-1`–`GO-5` | Formal, numerical, combinatorial, and code-grounded text benchmarks |
| `GO-6 Rev. 1.1` | Multimodal physical-AI benchmark with anti-leak analog instrument mapping |
| `GO-6-old-simple-no-VI` | Text-only control version for models without visual input |
| `GO-6+ Next Ultimate reality` | Extended robust physical-AI benchmark with decoys, calibration, nonlinear dynamics and pessimistic simulation |

Do not mix GO-6, GO-6-old-simple-no-VI and GO-6+ results without clearly marking the tested variant.

## Minimal result schema

Every measured run should provide at least:

```json
{
  "model": "model-name",
  "benchmark": "GO-4 / GO-6 Rev. 1.1 / GO-6+",
  "platform": "PC1 / PC2 / Online / Other",
  "quantization": "Q4_K_M / Q6_K / BF16 / API / other",
  "tokens_per_second": 0.0,
  "thinking_time_sec": 0,
  "output_tokens": 0,
  "score": 0.0,
  "code_compiles": false,
  "unique": null,
  "notes": ""
}
```

For GO-6 and GO-6+ runs, also record:

```json
{
  "images_attached": true,
  "visual_reading_claimed": true,
  "zig_runtime": "Zig version / compiler note",
  "results_json_valid": true,
  "nominal_best_action": "optional",
  "robust_best_action": "optional for GO-6+"
}
```

## Reproducibility and raw logs

For every evaluated model, preserve:

- full raw model answer;
- exact benchmark prompt used;
- image set used for multimodal tasks;
- model/runtime identifier;
- quantization or API model version;
- generation parameters where available;
- wall-clock time and tokens/s where measurable;
- whether generated code compiled;
- whether generated code output matched the textual answer;
- final score and scoring breakdown.

The repository is intended to evolve toward fully auditable tables with raw logs, normalized results, and charts.

## Citation

Please cite this repository and the methodology documents when using the benchmark tasks, prompts, results, or evaluation approach. A `CITATION.cff` file is included so GitHub can display citation metadata.

Suggested citation:

```text
Ivković, J. (2026). REAL-AI-Benchmark: Practical GO-1 to GO-6+ benchmark suite for real-task AI evaluation. GitHub repository.
```

For GO-6+ specifically:

```text
Ivković, J. (2026). GO-6+ Next Ultimate reality: Analog Physical Fuzzy-Dynamic Robust Decision Benchmark. REAL-AI-Benchmark project.
```

For a persistent academic identifier, the recommended next step is to create a GitHub release and archive it through Zenodo, which can issue a DOI for the repository release.

## Sponsorship and support

This project requires time, high-RAM local inference hardware, GPU/accelerator testing, storage, electricity, paid model access, repeated runs, manual verification, charting, and public documentation.

Sponsors help expand model coverage, maintain public result tables, rerun benchmarks, and improve reproducibility tooling.

See [`SPONSORSHIP.md`](SPONSORSHIP.md).

## Status

Public research draft. Benchmark definitions and methodology documents are included; raw logs, charts, reference solutions, and normalized result tables will be expanded progressively.

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**, unless explicitly stated otherwise.

You are free to share, copy, redistribute, remix, transform, and build upon the material for any purpose, including commercial use, provided that appropriate credit is given.

Recommended attribution:

> Jovan Ivković, REAL-AI-Benchmark: Real-World Reasoning and Physical-AI Benchmark Suite, GitHub repository, CC BY 4.0.

See [`LICENSE.txt`](LICENSE.txt) and [`NOTICE.md`](NOTICE.md) for details.

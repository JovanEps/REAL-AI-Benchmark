# REAL-AI-Benchmark

**REAL-AI-Benchmark** is an independent practical benchmark suite for evaluating AI/LLM/LMM systems on tasks that resemble real technical work rather than synthetic leaderboard exercises.

The project evaluates what a model actually produces: reasoning traceability, numerical correctness, formal proof discipline, executable code, reproducible output, structured reporting, and—in GO-6—physical perception from analog instruments.

> Real tasks. Real models. Real results.

## What this repository contains

The suite currently contains six GO benchmark tasks:

| Benchmark | Short purpose | Main evaluated capability |
|---|---|---|
| **GO-1** | Minimal correction of an RBAC/DSS policy | logical consistency, constraint checking, minimality proof |
| **GO-2** | Discrete LIF neuron with exact arithmetic | exact fractional computation, invariant proof, Python verification |
| **GO-3** | 2D valid convolution in C99 | manual numerical derivation, matrix reasoning, C implementation |
| **GO-4** | 4x4 Latin-square solver in Zig | combinatorial search, bitmasks, uniqueness proof, executable Zig |
| **GO-5** | Seeded Mealy transducer and one-symbol forensic correction | formal generation, simulation, Hamming analysis, uniqueness proof, Zig verification |
| **GO-6** | Physical-causal fuzzy dynamics with analog instruments | multimodal sensor reading, measurement intervals, fuzzy inference, short-horizon dynamics, decision proof, Zig verification |

GO-6 also has a text-only control version named **GO-6-old-simple-no-VI**, intended for models that cannot process images. The main GO-6 benchmark is the multimodal version using `PIC1.png`–`PIC5.png`.

## Repository layout

```text
REAL-AI-Benchmark/
├── README.md
├── CONTRIBUTING.md
├── SPONSORSHIP.md
├── LICENSE
├── CITATION.cff
├── assets/
│   ├── logo.png
│   └── social-preview.png
├── docs/
│   ├── evaluation-methodology.md
│   ├── scoring-rubric.md
│   └── reproducibility.md
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
│   ├── PIC1.png ... PIC5.png
│   └── GO-6_Physical_AI_Benchmark_Methodology_EN.pdf
├── Methodology/
│   └── methodology papers and draft reports
└── results/
    └── tables/
```

## Evaluation principle

Each model run is scored using a **component-based 0–10 methodology**. The score is not assigned by general impression and no component is arbitrarily made “fatal” unless the benchmark definition explicitly gives it high weight.

The evaluator adds what the model demonstrably achieved:

1. correct final result,
2. correct intermediate reasoning,
3. completeness of required sections,
4. proof, validation, or inverse check,
5. code implementation quality,
6. compilation/execution behavior where code is required,
7. structured final output and machine-readable reporting.

This makes comparisons auditable and prevents inconsistent scoring across model families.

## Minimal result schema

Every measured run should provide at least:

```json
{
  "model": "model-name",
  "benchmark": "GO-4",
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

## Citation

Please cite this repository and the methodology documents when using the benchmark tasks, prompts, results, or evaluation approach. A `CITATION.cff` file is included so GitHub can display citation metadata.

Suggested citation:

```text
Ivković, J. (2026). REAL-AI-Benchmark: Practical GO-1 to GO-6 benchmark suite for real-task AI evaluation. GitHub repository.
```

For a persistent academic identifier, the recommended next step is to create a GitHub release and archive it through Zenodo, which can issue a DOI for the repository release.

## Sponsorship and support

This project requires time, high-RAM local inference hardware, GPU/accelerator testing, storage, electricity, paid model access, repeated runs, manual verification, charting, and public documentation.

Sponsors help expand model coverage, maintain public result tables, rerun benchmarks, and improve reproducibility tooling.

See [`SPONSORSHIP.md`](SPONSORSHIP.md).

## Status

Public research draft. Benchmark definitions and methodology documents are included; raw logs, charts, reference solutions, and normalized result tables will be expanded progressively.

## License

This repository is licensed under the **Creative Commons Attribution 4.0
International License (CC BY 4.0)**, unless explicitly stated otherwise.

You are free to share, copy, redistribute, remix, transform, and build upon
the material for any purpose, including commercial use, provided that
appropriate credit is given.

Recommended attribution:

> Jovan Ivković, REAL-AI-Benchmark: Real-World Reasoning and Physical-AI Benchmark Suite, GitHub repository, CC BY 4.0.

See [`LICENSE.txt`](LICENSE.txt) and [`NOTICE.md`](NOTICE.md) for details.

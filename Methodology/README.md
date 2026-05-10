# Methodology Documents

This folder contains methodology documents for the **REAL-AI-Benchmark** project.

The methodology documents define the evaluation logic, scoring rubrics, benchmark interpretation rules, failure-mode taxonomies, and recommended result reporting structure for GO-series tests.

## Folder structure

```text
Methodology/
├── archive/
├── README.md
├── GO-6+_Next_Ultimate_reality_metodologija_SR.pdf
├── GO-6+_Next_Ultimate_reality_Methodology_EN.pdf
├── GO-6_rev1.1_methodology_scoring_SR.md
├── GO-6_Physical_AI_Benchmark_Methodology_EN_rev1.1_anti-leak.pdf
├── GO-6_fizicki_AI_benchmark_metodologija_rev1.1_anti-leak.pdf
├── GO_benchmark_standardization_methodology_GO5_extended_EN.pdf
└── GO_benchmark_standardization_methodology_GO5_extended.pdf
```

## Active methodology documents

### GO-1 to GO-5 methodology

```text
GO_benchmark_standardization_methodology_GO5_extended.pdf
GO_benchmark_standardization_methodology_GO5_extended_EN.pdf
```

These documents describe the general GO-1 to GO-5 benchmark methodology, scoring principles, standardized answer structures, common failure modes, and recommended reporting practices.

GO-1 to GO-5 cover:

- formal policy correction;
- exact numerical reasoning;
- manual convolution and C implementation;
- combinatorial search and Zig implementation;
- deterministic transducer generation and forensic correction.

### GO-6 Rev. 1.1 anti-leak methodology

```text
GO-6_fizicki_AI_benchmark_metodologija_rev1.1_anti-leak.pdf
GO-6_Physical_AI_Benchmark_Methodology_EN_rev1.1_anti-leak.pdf
GO-6_rev1.1_methodology_scoring_SR.md
```

These documents define the methodology for **GO-6 Rev. 1.1**, the anti-leak multimodal physical-AI benchmark.

GO-6 Rev. 1.1 evaluates:

- analog instrument reading;
- anti-leak image-to-variable mapping;
- reading intervals;
- fuzzy inference;
- short-horizon dynamic simulation;
- action classification;
- uniqueness proof;
- Zig verifier;
- `RESULTS_JSON` formal output.

GO-6 Rev. 1.1 is the active baseline physical-AI benchmark.

### GO-6+ Next Ultimate reality methodology

```text
GO-6+_Next_Ultimate_reality_metodologija_SR.pdf
GO-6+_Next_Ultimate_reality_Methodology_EN.pdf
```

These documents define the methodology for **GO-6+ Next Ultimate reality**, the extended robust physical-AI benchmark.

GO-6+ extends GO-6 Rev. 1.1 with:

- nine analog instrument images;
- six relevant physical variables;
- three decoy instruments;
- raw and corrected readings;
- calibration handling;
- control-voltage channel;
- nonlinear vibration dynamics;
- physical flow clamping;
- nominal and pessimistic simulations;
- robust action selection;
- stricter Zig verification;
- stricter JSON audit trace.

GO-6+ should be treated as a separate and harder benchmark than GO-6 Rev. 1.1.

## Recommended methodology by benchmark

| Benchmark | Recommended methodology document |
|---|---|
| GO-1 to GO-5 | `GO_benchmark_standardization_methodology_GO5_extended.pdf` |
| GO-1 to GO-5 English | `GO_benchmark_standardization_methodology_GO5_extended_EN.pdf` |
| GO-6 Rev. 1.1 Serbian | `GO-6_fizicki_AI_benchmark_metodologija_rev1.1_anti-leak.pdf` |
| GO-6 Rev. 1.1 English | `GO-6_Physical_AI_Benchmark_Methodology_EN_rev1.1_anti-leak.pdf` |
| GO-6 Rev. 1.1 scoring summary | `GO-6_rev1.1_methodology_scoring_SR.md` |
| GO-6+ Serbian | `GO-6+_Next_Ultimate_reality_metodologija_SR.pdf` |
| GO-6+ English | `GO-6+_Next_Ultimate_reality_Methodology_EN.pdf` |

## Versioning principle

Each benchmark version must be evaluated against its matching methodology document.

Do not evaluate GO-6+ with the GO-6 Rev. 1.1 methodology.  
Do not evaluate GO-6 Rev. 1.1 with the GO-6+ methodology.  
Do not mix GO-6-old-simple-no-VI results with multimodal GO-6 results without explicitly marking the no-visual-input variant.

The GO-6+ benchmark introduces additional requirements that are not present in GO-6 Rev. 1.1, especially:

- decoy filtering;
- raw/corrected reading separation;
- calibration handling;
- pessimistic simulation;
- both-end `U_ctrl` interval checking;
- robust-best action selection.

## Archive

The `archive/` folder is intended for superseded, deprecated, or historical methodology drafts.

Documents in `archive/` are preserved for transparency and historical traceability, but should not be used for new evaluations unless explicitly stated.

## Citation note

These are public research drafts. When using or discussing the benchmark methodology, cite the repository and the relevant methodology document.

A repository-level `CITATION.cff` file is included for GitHub citation metadata.

When citing benchmark results, always specify:

- benchmark name;
- benchmark version;
- methodology document;
- model name;
- quantization/runtime environment if applicable;
- whether images were attached for multimodal tasks;
- whether Zig code compiled and executed;
- final score and scoring breakdown.

Example:

```text
REAL-AI-Benchmark, GO-6+ Next Ultimate reality,
evaluated using GO-6+_Next_Ultimate_reality_Methodology_EN.pdf.
```

## Recommended result reporting

For transparent reporting, each result should include at least:

```json
{
  "model": "model-name",
  "benchmark": "GO-6+ Next Ultimate reality",
  "methodology": "GO-6+_Next_Ultimate_reality_Methodology_EN.pdf",
  "platform": "PC1 / PC2 / Online / Other",
  "quantization": "Q4_K_M / Q6_K / BF16 / API / other",
  "images_attached": true,
  "zig_compiles": true,
  "results_json_valid": true,
  "score": 0.0,
  "notes": ""
}
```

For GO-6+ also record:

```json
{
  "instrument_mapping_correct": true,
  "decoys_correctly_ignored": true,
  "calibration_applied": true,
  "nominal_simulation_complete": true,
  "pessimistic_simulation_complete": true,
  "robust_best_action": "action-name"
}
```

## Maintenance note

If a benchmark prompt changes, its methodology document should be updated or versioned.  
If a methodology document changes, previously scored results should not be silently reinterpreted without recording the scoring version used at the time of evaluation.

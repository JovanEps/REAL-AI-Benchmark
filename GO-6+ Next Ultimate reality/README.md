# GO-6+ Next Ultimate reality

**GO-6+ Next Ultimate reality** is an extended multimodal physical-AI benchmark for robust decision-making from analog instrumentation.

It is a more demanding successor to GO-6 Rev. 1.1 and is intended to test visual interpretation, physical reasoning, fuzzy inference, nonlinear dynamic simulation, robust decision-making, and executable software verification.

## Folder structure

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

## Main benchmark file

```text
GO-6+.txt
```

This file contains the full GO-6+ task prompt.

It defines:

- required answer structure;
- image-reading and anti-leakage rules;
- relevant physical variables;
- decoy instrument policy;
- raw/corrected reading requirements;
- calibration handling;
- fuzzy rules;
- dynamic model;
- action set;
- nominal simulation requirements;
- pessimistic simulation requirements;
- robust decision protocol;
- Zig verifier requirements;
- `RESULTS_JSON` output contract.

## Figure set

The active image set is stored in:

```text
Figure_set2/
```

It contains nine analog instrument images:

```text
Fig-1.png
Fig-2.png
Fig-3.png
Fig-4.png
Fig-5.png
Fig-6.png
Fig-7.png
Fig-8.png
Fig-9.png
```

The order of the images must not be interpreted as a solution key.

A tested model must identify, read, and classify the instruments from their visible content. Some instruments are relevant to the physical model, while others are decoy instruments.

## Relevant physical variables

The physical model uses six relevant variables:

| Variable | Meaning | Unit |
|---|---|---|
| `T` | process temperature | °C |
| `P` | process pressure | kPa |
| `F` | coolant flow | L/min |
| `V` | vibration | mm/s |
| `D` | pressure trend `dP/dt` | kPa/min |
| `U_ctrl` | regulator control voltage | V |

The model must map exactly six images to these six variables and must identify exactly three images as decoy/ignored instruments.

## Anti-leakage policy

This benchmark is designed to avoid direct answer leakage.

The prompt and supporting files must not provide:

- direct `Fig-n → variable` mapping;
- digital readouts that print the exact analog needle value;
- metadata with hidden answers;
- file names that encode the solution;
- JSON templates that expose ready-made sensor fields such as `T_C`, `P_kPa`, `F_L_min`, `V_mm_s`, `dPdt_kPa_min` or `U_ctrl_V`.

The model must infer all input bindings from the visible instrument content.

If a model reports a direct digital value printed on the instrument face as the basis of the reading, the evaluator should check whether this is a leakage artefact rather than a legitimate analog reading.

## Required answer sections

The answer must follow this section order:

```text
A-IDENTIFIKACIJA_I_OCITAVANJE_ANALOGNIH_INSTRUMENATA
B-FIZICKA_KONZISTENTNOST_I_KALIBRACIJA_ULAZA
C-FUZZY_INFERENCIJA
D-NOMINALNA_DINAMICKA_SIMULACIJA
E-PESSIMISTIC_SIMULACIJA_I_ROBUSTNOST
F-ODLUKA_I_DOKAZ_JEDINSTVENOSTI
G-ZIG_KOD
RESULTS_JSON
<END>
```

Each section contains control points. Missing control points should reduce the score.

## Key extensions over GO-6 Rev. 1.1

GO-6 Rev. 1.1 evaluates:

- analog instrument reading;
- anti-leak mapping;
- fuzzy inference;
- dynamic simulation;
- decision proof;
- Zig verifier;
- formal JSON output.

GO-6+ adds:

- more analog instruments;
- decoy instruments;
- raw and corrected readings;
- calibration handling;
- a control-voltage channel;
- nonlinear vibration dynamics;
- physical clamping of flow;
- nominal and pessimistic simulations;
- robust action selection;
- stricter Zig verifier requirements;
- stricter JSON audit trace.

## Evaluation focus

GO-6+ is not only a numerical problem. It is a complete perception-to-decision pipeline.

The evaluated model must:

1. read analog gauges;
2. infer what each instrument measures;
3. reject decoy instruments;
4. identify units and scales;
5. distinguish raw from corrected readings;
6. propagate measurement intervals;
7. compute fuzzy memberships and rules;
8. simulate all actions in the nominal scenario;
9. simulate all actions in the pessimistic scenario;
10. evaluate both ends of the `U_ctrl` interval;
11. select a robust action;
12. prove uniqueness or correctly report non-uniqueness;
13. write executable Zig code;
14. provide valid `RESULTS_JSON`.

## Methodology

The scoring methodology is documented in:

```text
../Methodology/GO-6+_Next_Ultimate_reality_metodologija_SR.pdf
../Methodology/GO-6+_Next_Ultimate_reality_Methodology_EN.pdf
```

The GO-6+ methodology should be used for GO-6+ evaluations only.

Do not score GO-6+ with the GO-6 Rev. 1.1 methodology, because GO-6+ contains additional required components: decoy filtering, calibration, pessimistic simulation, robust-best action selection, and stricter verification requirements.

## Scoring note

GO-6+ is intentionally harder than GO-6 Rev. 1.1.

Scores from GO-6 and GO-6+ should not be directly compared without explicitly stating the benchmark version.

The expected scoring scale is stricter because the model must solve a combined perception, instrumentation, calibration, fuzzy logic, dynamic simulation, robust decision, and code-verification task.

## Recommended execution protocol

For each tested model:

1. attach the complete `Figure_set2/` image set;
2. use the exact `GO-6+.txt` prompt;
3. preserve the full raw answer;
4. record model name and runtime environment;
5. record whether the model actually used visual input;
6. compile and run generated Zig code where possible;
7. validate the final `RESULTS_JSON`;
8. score using the GO-6+ methodology documents.

## Recommended citation

```text
Ivković, J. (2026). GO-6+ Next Ultimate reality:
Analog Physical Fuzzy-Dynamic Robust Decision Benchmark.
REAL-AI-Benchmark project.
```

## Status

This folder contains the active GO-6+ benchmark definition and the active `Figure_set2` image set.

Older experimental figure sets should not be used for scoring unless explicitly marked as legacy or illustrative.

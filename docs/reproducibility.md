# Reproducibility Notes

For each benchmark run, store the original prompt and raw model output. Do not replace raw outputs with corrected versions.

## Required run metadata

```text
model:
provider:
local/runtime:
quantization:
hardware_profile:
RAM:
VRAM:
context:
temperature:
top_p:
top_k:
repeat_penalty:
time_to_first_token:
generation_time:
tokens_per_second:
output_tokens:
code_compilation_result:
score:
evaluator_notes:
```

## GO-6-specific metadata

```text
go6_variant: multimodal | old-simple-no-VI
images_attached: true | false
image_files: PIC1.png, PIC2.png, PIC3.png, PIC4.png, PIC5.png
instrument_reading_error_notes:
```

## Raw vs corrected outputs

Raw outputs should be kept unchanged. Any corrected code, evaluator commentary, or reference solution should be stored separately and clearly marked.

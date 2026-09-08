# CamillaNode documentation mirror — source and rules

This directory mirrors the technical documentation from:

- repository: `flashmoc/camillaNode-EStack`
- source branch: `feature/estack-dsp-product`
- sync date: `2026-09-08`

The mirrored files are intentionally kept under `docs/camillanode/` so they do not overwrite the E-Stack SoundSystem's own calibration/system documentation.

## Mirrored source documents

| Source path | Source blob SHA |
| --- | --- |
| `docs/README.md` | `23bb6ef2979f7d791b928ec51959d6c72ff2e6da` |
| `docs/architecture.md` | `a0fb0f19d92b04b0faa9a37e10ec7333ae91dd4b` |
| `docs/dsp-safety.md` | `02bf1113202fd940639267724dd6add98d79f631` |
| `docs/estack-dsp-architecture.md` | `d463dda5cdae9965ed28f5e2784534abec7136a7` |
| `docs/estack-dsp-product.md` | `ba4226ab409303c412fdafb945e99b999504e62a` |
| `docs/measurement-batch.md` | `d52a1dc2f4fff8b67d969f6cf46d5054e62e2ba8` |
| `docs/persistence.md` | `b17a0a33ac19db96260da105a4c7232fb3a0b93a` |
| `docs/raspberry.md` | `07dead708752b0182c5794bf6631707d178136e9` |
| `docs/runtime-contracts.md` | `73e3ab622b84c313d54ef32e2d700fa565ebda73` |
| `docs/ui-architecture.md` | `25dec31e2e17d64e1f0f446a9e5268e48a917666` |
| `docs/pages/control.md` | `e5c8e42f0434a59d22b7aa920907fcd2ff8a7536` |

Supporting Measurement Batch examples were also copied to `measurements/batch-examples/`.

## Authority / update rule

- `camillaNode-EStack` remains the implementation source for CamillaNode code and its runtime/API contracts.
- `e-stack-soundsystem` is the central project/system/calibration source of truth and contains a mirrored copy of the CamillaNode documentation so a new assistant can work from one repository.
- If CamillaNode code or its docs change, re-sync this mirror and update the source SHAs above.
- Never silently edit a mirrored file to make it match the current hardware. Put E-Stack-specific differences in the system repo's own documentation instead.

## Current E-Stack measurement-input override

The mirrored Measurement Batch documentation uses `measurementInput: 4` as an example for **physical IN4**. The current E-Stack system documentation records the REW path as:

`physical IN5 → ALSA CH4 → Camilla logical IN4`

Because Measurement Batch physical input numbering is one-based, batches generated for the current system should therefore use:

```json
"measurementInput": 5
```

unless the hardware routing is changed and documented later.

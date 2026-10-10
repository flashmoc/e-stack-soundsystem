# CamillaNode documentation mirror — source and rules

This directory mirrors the technical documentation from:

- repository: `flashmoc/camillaNode-EStack`
- source branch: `feature/estack-dsp-product`
- sync date: `2026-09-08`

The mirrored files are intentionally kept under `docs/camillanode/` so they do not overwrite the E-Stack SoundSystem's own calibration/system documentation.

## Mirrored source documents

| Source path | Destination | Source blob SHA |
| --- | --- | --- |
| `README.md` | `docs/camillanode/repository-README.md` | `c40916b22abfc8b86e39939d8cbc1ce7a9b7d99f` |
| `AGENTS.md` | `docs/camillanode/AGENTS.md` | `7045df4e4e758acc9a8295a329f72978958182bf` |
| `docs/README.md` | `docs/camillanode/README.md` | `23bb6ef2979f7d791b928ec51959d6c72ff2e6da` |
| `docs/architecture.md` | `docs/camillanode/architecture.md` | `a0fb0f19d92b04b0faa9a37e10ec7333ae91dd4b` |
| `docs/dsp-safety.md` | `docs/camillanode/dsp-safety.md` | `02bf1113202fd940639267724dd6add98d79f631` |
| `docs/estack-dsp-architecture.md` | `docs/camillanode/estack-dsp-architecture.md` | `d463dda5cdae9965ed28f5e2784534abec7136a7` |
| `docs/estack-dsp-product.md` | `docs/camillanode/estack-dsp-product.md` | `ba4226ab409303c412fdafb945e99b999504e62a` |
| `docs/measurement-batch.md` (**resynchronisé depuis `flashmoc/e-stack-dsp`, branche `main`, 2026-10-10**) | `docs/camillanode/measurement-batch.md` | `917dbd78d60d818e71c24c788ce405fe4a450f61` |
| `docs/persistence.md` | `docs/camillanode/persistence.md` | `b17a0a33ac19db96260da105a4c7232fb3a0b93a` |
| `docs/raspberry.md` | `docs/camillanode/raspberry.md` | `07dead708752b0182c5794bf6631707d178136e9` |
| `docs/runtime-contracts.md` | `docs/camillanode/runtime-contracts.md` | `73e3ab622b84c313d54ef32e2d700fa565ebda73` |
| `docs/ui-architecture.md` | `docs/camillanode/ui-architecture.md` | `25dec31e2e17d64e1f0f446a9e5268e48a917666` |
| `docs/pages/control.md` | `docs/camillanode/pages/control.md` | `e5c8e42f0434a59d22b7aa920907fcd2ff8a7536` |

Supporting Measurement Batch examples were also copied from the CamillaNode repository to `measurements/batch-examples/`.

## Authority / update rule

- `camillaNode-EStack` remains the historical source for the other mirrored CamillaNode documentation and runtime/API contracts.
- **Exception explicite (2026-10-10):** `docs/camillanode/measurement-batch.md` is now synchronized from `flashmoc/e-stack-dsp` at `docs/measurement-batch.md` (source blob SHA in the table), with a separate top-of-file E-Stack SoundSystem cabling note. The `e-stack-dsp` repository contains the currently verified dual-mode Measurement Batch implementation. The original 2026-09-08 mirror source/branch metadata continues to describe the **other** files in this directory.
- `e-stack-soundsystem` is the central project/system/calibration source of truth and contains a mirrored copy of the CamillaNode documentation so a new assistant can work from one repository.
- If CamillaNode code or its docs change, re-sync this mirror and update the source SHAs above.
- Never silently edit a mirrored file to make it match the current hardware. Put E-Stack-specific differences in the system repo's own documentation instead.

## E-Stack measurement inputs: distinguish the modes

- **Measure current system / live snapshot:** the server always routes **physical IN3** to OUT1…OUT6 at 0 dB mixer-source gain. This is independent of `defaults.measurementInput` in any saved JSON. The REW interface must actually feed physical IN3 for this shortcut to produce a valid sweep.
- **Imported JSON campaign / calibration:** optional `defaults.measurementInput` chooses the physical input. The last documented E-Stack REW connection for these campaigns was **physical IN5 → ALSA CH4 (zero-based) → Camilla logical IN4**, requiring `"measurementInput": 5`. This old hardware connection must be verified if the interface cable was moved.
- **No unconditional global input number:** physical IN3 is fixed by current-system mode; physical IN5 is a recorded campaign wiring choice, not the fixed input of every mode.
- **Baseline policies differ:** the calibration campaign forces Loudness and Input Trim off; current-system mode preserves both, along with the selected ways' existing gains/mutes.

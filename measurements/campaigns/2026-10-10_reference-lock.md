# Calibration reference lock — 2026-10-10

## Authoritative pair

From this point forward, calibration work must use this pair as its starting reference unless the user supplies a newer live export:
This was the lock **on 2026-10-10**, not a live read on every later date. The complete JSON and `.mdat` named below are not checked into this repository; obtain them before attempting exact reproduction or a new numerical fit.

- DSP export timestamp: **2026-10-10T18:58:49.858Z**
- DSP title: `Stereo-LR-balanced-L-PAD`
- config revision: `3b3d5f8e04576343db5a63b3a549f19dd92db640ee3955145d99aaed9e16631f`
- REW acoustic reference uploaded in the same handoff: `oct. 10 20_57_36.mdat`

Earlier same-day system exports and earlier full-system REW curves are superseded when they differ.

## Locked starting values

| Parameter | Value |
|---|---:|
| Master | -9.0 dB |
| SUB gain | -7.3 dB |
| KICK gain | -18.4 dB |
| MID L/R gain | 0.0 / 0.0 dB |
| HIGH L/R gain | -4.0 / -4.0 dB |
| SUB delay | 0.000 ms |
| KICK delay | 1.300 ms |
| MID L/R delay | 2.760 ms |
| HIGH L/R delay | 2.720 ms |
| SUB polarity | NORMAL |
| KICK polarity | INVERTED |
| MID L/R polarity | NORMAL |
| HIGH L/R polarity | NORMAL |

Crossovers, per-way PEQ and protection are those summarized in `CURRENT_REFERENCE.md`.

## Measurement rule

The next six-way level-matching campaign must be started with this DSP state unchanged. Its JSON is:
`measurements/batches/2026-10-10_stereo-level-match-6solos.json`

Do not manually pre-correct way gains before acquiring the six solo responses.

The exact physical REW input cable must still be verified before starting an imported JSON campaign; the DSP export cannot prove physical cabling.

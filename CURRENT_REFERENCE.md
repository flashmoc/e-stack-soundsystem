# E-Stack — Current Reference

## Status

**WORKING / LIVE BASELINE — not yet final calibration.**

Source: live system export supplied on **2026-10-10**, title `Stereo-LR-balanced-L-PAD`.

This live export supersedes older manually transcribed gain/delay values when they differ.

## Master and way gains

- MASTER: **-9.0 dB**
- SUB: **-7.3 dB**
- KICK: **-18.4 dB**
- MID L: **-0.6 dB**
- MID R: **+0.6 dB**
- HIGH L: **-3.5 dB**
- HIGH R: **-1.8 dB**

Current L/R offsets:
- MID R is **+1.2 dB** relative to MID L
- HIGH R is **+1.7 dB** relative to HIGH L

These are the current deployment gains, not yet the final level-match result.

## Polarities

- SUB: **NORMAL**
- KICK: **INVERTED**
- MID L/R: **NORMAL**
- HIGH L/R: **NORMAL**

## Delays

- SUB: **0.000 ms**, subsample enabled
- KICK: **1.300 ms**
- MID L/R: **2.760 ms**
- HIGH L/R: **2.720 ms**

Relative baseline:
- MID is **+0.040 ms** later than HIGH
- MID is **+1.460 ms** later than KICK
- HIGH is **+1.420 ms** later than KICK
- KICK is **+1.300 ms** later than SUB

These values are current working values; final delay/phase optimisation is still pending.

## Crossovers

- SUB: HPF **40 Hz Butterworth order 4 / 24 dB/oct**, LPF **130 Hz LR24**
- KICK: HPF **130 Hz LR24**, LPF **300 Hz LR24**
- MID L/R: HPF **300 Hz LR24**, LPF **2000 Hz LR24**
- HIGH L/R: HPF **2000 Hz LR24**

## Per-way PEQ

MID L/R:
- PK **1350 Hz / -5.0 dB / Q 1.02**

HIGH L:
- PK **2850 Hz / -2.5 dB / Q 1.96**
- PK **4600 Hz / -4.0 dB / Q 1.03**
- High-shelf **7763 Hz / +5.7 dB / Q 1**

HIGH R:
- PK **2850 Hz / -2.5 dB / Q 1.96**
- PK **4600 Hz / -4.0 dB / Q 0.70**
- High-shelf **7763 Hz / +5.7 dB / Q 1**

## Input / Global EQ state

The current live export contains Global PEQ/GEQ filter definitions, but the stored `ESTACK_INPUT_EQ_STATE` reports:

- GEQ: **disabled**
- PEQ: **disabled**

The live pipeline starts at mixer `estack_preview`; no Global EQ or Loudness filter stage is active before the mixer in this export.

Therefore calibration batches must not assume `ESTACK_LOUDNESS` exists in the live baseline.

## Routing

Mixer `estack_preview`:

- OUT0 SUB: IN0 + IN1, each **-6.0206 dB**
- OUT1 KICK: IN0 + IN1, each **-6.0206 dB**
- OUT2 MID L: IN0 at 0 dB
- OUT3 MID R: IN1 at 0 dB
- OUT4 HIGH L: IN0 at 0 dB
- OUT5 HIGH R: IN1 at 0 dB
- OUT6/7 spare

Measurement source currently documented:
- physical **IN5**
- ALSA zero-based **CH4**
- Camilla logical **IN4**
- Measurement Batch: `measurementInput: 5`

## Protection

Hard limiters:
- SUB: **-12.6 dBFS**
- KICK: **-15.8 dBFS**
- MID L/R: **-5.1 dBFS**
- HIGH L/R: **-5.1 dBFS**

Compressors:
- SUB: **-13.6 dB**, 10 ms / 500 ms / 20:1
- KICK: **-16.8 dB**, 5 ms / 300 ms / 20:1
- MID L/R: **-6.1 dB**, 2 ms / 200 ms / 20:1
- HIGH L/R: **-6.1 dB**, 1 ms / 150 ms / 20:1

Protection thresholds are present in the live export, but amplifier calibration comments still mark some assumptions/provisional validation requirements.

## Calibration status

Known live baseline:
- current gains and L/R balance captured
- absolute SUB/KICK delays captured
- all current polarities captured
- crossover/PEQ/protection topology captured

To finish:
- six-way solo level match at C0
- final MID/HIGH phase/delay optimisation L and R
- final KICK ↔ stereo TOP compromise
- final SUB ↔ KICK optimisation
- physical SUM/REV verification
- spatial robustness
- final room/system target EQ
- directivity / distortion / headroom checks
- final reference export

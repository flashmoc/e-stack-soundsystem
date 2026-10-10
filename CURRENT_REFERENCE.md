# E-Stack — Current Reference

## Status

**WORKING / LOCKED BASELINE FOR NEXT CALIBRATION PASSES — not yet final calibration.**

Authoritative source from now on:
- live export timestamp: **2026-10-10T18:58:49.858Z**
- title: `Stereo-LR-balanced-L-PAD`
- config revision: `3b3d5f8e04576343db5a63b3a549f19dd92db640ee3955145d99aaed9e16631f`
- acoustic reference supplied in the same handoff: `oct. 10 20_57_36.mdat`

This pair supersedes all earlier gain/delay/level references when they differ.

## Master and way gains

- MASTER: **-9.0 dB**
- SUB: **-7.3 dB**
- KICK: **-18.4 dB**
- MID L: **0.0 dB**
- MID R: **0.0 dB**
- HIGH L: **-4.0 dB**
- HIGH R: **-4.0 dB**

There is therefore **no current DSP L/R gain offset** on MID or HIGH in this locked baseline.

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

These are the locked starting values for optimisation, not yet the final phase-optimal solution.

## Crossovers

- SUB: HPF **40 Hz Butterworth order 4 / 24 dB/oct**, LPF **130 Hz LR24**
- KICK: HPF **130 Hz LR24**, LPF **300 Hz LR24**
- MID L/R: HPF **300 Hz LR24**, LPF **2000 Hz LR24**
- HIGH L/R: HPF **2000 Hz LR24**

## Per-way PEQ

SUB:
- no per-way PEQ in the active output stage

KICK:
- no per-way PEQ in the active output stage

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

Important: HIGH L/R are not filter-identical because the 4600 Hz Q differs.

## Input / Global EQ state

The live export contains Global PEQ/GEQ filter definitions, but `ESTACK_INPUT_EQ_STATE` reports:
- GEQ: **disabled**
- PEQ: **disabled**

The active pipeline begins at mixer `estack_preview`; no Global EQ or Loudness filter stage is active before the mixer in this export.

## Routing

Mixer `estack_preview`:
- OUT0 SUB: IN0 + IN1, each **-6.0206 dB**
- OUT1 KICK: IN0 + IN1, each **-6.0206 dB**
- OUT2 MID L: IN0 at 0 dB
- OUT3 MID R: IN1 at 0 dB
- OUT4 HIGH L: IN0 at 0 dB
- OUT5 HIGH R: IN1 at 0 dB
- OUT6/7 spare

Measurement-input note:
- imported JSON campaigns still use the project wiring convention recorded in their JSON (currently `measurementInput: 5`);
- the DSP export itself does not prove the physical REW cable location;
- verify actual hardware cabling before starting a campaign.

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

## Calibration sequence from this baseline

1. six-way solo level match at C0;
2. MID/HIGH phase/delay optimisation L and R;
3. KICK ↔ stereo TOP compromise;
4. SUB ↔ KICK optimisation;
5. physical SUM/REV verification;
6. multi-position robustness;
7. final room/system target EQ;
8. final reference export.

Do not use an older chat value or older repo snapshot in place of this locked baseline unless the user explicitly changes the live system again.

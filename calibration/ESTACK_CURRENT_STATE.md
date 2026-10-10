# E-Stack — Current State

## Authoritative baseline

Latest live DSP export supplied **2026-10-10**:
- exportedAt: **2026-10-10T18:58:49.858Z**
- config revision: `3b3d5f8e04576343db5a63b3a549f19dd92db640ee3955145d99aaed9e16631f`
- title: `Stereo-LR-balanced-L-PAD`
- associated acoustic reference: `oct. 10 20_57_36.mdat`
- status: **WORKING / LOCKED BASELINE**, not final calibration

This state supersedes earlier 2026-10-10 exports if values differ.

## Architecture

- Raspberry Pi 5
- RASPIAUDIO 8×IN / 8×OUT
- CamillaDSP / CamillaNode
- REW with hardware timing loopback
- Komplete Audio 1
- ECM8000
- sample rate: **48 kHz**

## Mapping

- OUT0 = SUB
- OUT1 = KICK
- OUT2 = MID L
- OUT3 = MID R
- OUT4 = HIGH L
- OUT5 = HIGH R
- OUT6/7 = spare

## Current master / gains

- MASTER = **-9.0 dB**
- SUB = **-7.3 dB**
- KICK = **-18.4 dB**
- MID L = **0.0 dB**
- MID R = **0.0 dB**
- HIGH L = **-4.0 dB**
- HIGH R = **-4.0 dB**

No current DSP L/R level offset on MID/HIGH.

## Current polarity

- SUB = NORMAL
- KICK = INVERTED
- MID L/R = NORMAL
- HIGH L/R = NORMAL

## Current delays

- SUB = **0.000 ms**, subsample true
- KICK = **1.300 ms**
- MID L/R = **2.760 ms**
- HIGH L/R = **2.720 ms**

These remain optimisation starting points.

## Current crossovers

SUB:
- HPF 40 Hz Butterworth order 4
- LPF 130 Hz LR24

KICK:
- HPF 130 Hz LR24
- LPF 300 Hz LR24

MID L/R:
- HPF 300 Hz LR24
- LPF 2000 Hz LR24

HIGH L/R:
- HPF 2000 Hz LR24

## Per-way EQ

SUB:
- none in active output stage

KICK:
- none in active output stage

MID L/R:
- 1350 Hz / -5 dB / Q 1.02

HIGH L:
- 2850 Hz / -2.5 dB / Q 1.96
- 4600 Hz / -4 dB / Q 1.03
- high-shelf 7763 Hz / +5.7 dB / Q 1

HIGH R:
- 2850 Hz / -2.5 dB / Q 1.96
- 4600 Hz / -4 dB / Q 0.70
- high-shelf 7763 Hz / +5.7 dB / Q 1

## Input / Global EQ

The live configuration contains Global PEQ and fitted GEQ filter definitions, but `ESTACK_INPUT_EQ_STATE` reports both sections disabled.

Active pipeline begins directly with:
`Mixer estack_preview → per-way processing → protection → hard limiters`

No active pre-mixer Loudness stage is present in the supplied export.

## Mixer

Programme IN0/IN1:
- SUB/KICK mono sum: each source -6.0206 dB
- MID/HIGH stereo at 0 dB

## Measurement input

The preset export does not encode which physical socket currently carries the REW cable.

Imported batch JSONs now specify `measurementInput: 3`, matching physical IN3 / Camilla zero-based IN2.

## Protection

Hard limits:
- SUB -12.6 dBFS
- KICK -15.8 dBFS
- MID L/R -5.1 dBFS
- HIGH L/R -5.1 dBFS

Compression:
- SUB -13.6 dB / 10 ms / 500 ms / 20:1
- KICK -16.8 dB / 5 ms / 300 ms / 20:1
- MID L/R -6.1 dB / 2 ms / 200 ms / 20:1
- HIGH L/R -6.1 dB / 1 ms / 150 ms / 20:1

## Current calibration work

Immediate sequence:
1. six solo ways at C0 with this baseline unchanged;
2. derive level balance;
3. finish delay / phase optimisation;
4. validate SUM/REV physically;
5. optimise room/system EQ only afterwards.

Any future recommendation must be referenced back to config revision `3b3d5f8e...` unless a newer live export is supplied.

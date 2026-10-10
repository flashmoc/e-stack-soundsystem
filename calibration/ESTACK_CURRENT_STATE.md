# E-Stack — Current State

## Source

Latest live DSP export supplied **2026-10-10**:
- title: `Stereo-LR-balanced-L-PAD`
- sample rate: **48 kHz**
- current status: **WORKING / live baseline**, not final calibration

## Architecture

- Raspberry Pi 5
- RASPIAUDIO 8×IN / 8×OUT
- CamillaDSP / CamillaNode
- REW with hardware timing loopback
- Komplete Audio 1
- ECM8000

## Mapping

- OUT0 = SUB
- OUT1 = KICK
- OUT2 = MID L
- OUT3 = MID R
- OUT4 = HIGH L
- OUT5 = HIGH R
- OUT6/7 = spare

## REW measurement source

- physical input: IN5
- ALSA zero-based: CH4
- Camilla logical: IN4
- for an **imported calibration JSON**, the last recorded wiring corresponds to `measurementInput: 5`

**Separate current-system shortcut:** `MEASURE NOW` always routes **physical IN3** (CamillaDSP source channel 2), keeps selected ways' current gain/mute, Input Trim/Loudness and all existing filters/protections, and captures a new baseline on each start. The earlier physical IN5 record remains a *historical campaign wiring note*, not the hardcoded input of current-system mode. Verify the real audio cable/channel map before a measurement; do not treat the physical input currently used as independently verified by the preset export.

## Current master / gains

- MASTER = **-9.0 dB**
- SUB = **-7.3 dB**
- KICK = **-18.4 dB**
- MID L = **-0.6 dB**
- MID R = **+0.6 dB**
- HIGH L = **-3.5 dB**
- HIGH R = **-1.8 dB**

The stereo deployment currently contains deliberate L/R gain offsets. Do not collapse L/R to a common gain before analysing the six solo measurements.

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

These are not yet considered phase-optimal.

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

The live configuration contains definitions for Global PEQ and fitted GEQ filters, but `ESTACK_INPUT_EQ_STATE` reports both sections disabled.

The active pipeline begins directly with:
`Mixer estack_preview → per-way processing → protection → hard limiters`

No active pre-mixer Loudness stage is present in this live export.

## Mixer

Programme IN0/IN1:
- SUB/KICK mono sum: each source -6.0206 dB
- MID/HIGH stereo at 0 dB

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
1. measure six solo ways at C0 without changing current gains;
2. derive true level balance and L/R offsets;
3. finish delay / phase optimisation;
4. verify SUM/REV physically;
5. only then optimise room/system EQ and target.

Do not use an old reference gain table in place of this live export.

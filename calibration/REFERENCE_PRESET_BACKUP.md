# E-Stack — Reference Preset Backup

## Status

This file now records the **2026-10-10 live working baseline** `Stereo-LR-balanced-L-PAD`.

It is reconstructible at the parameter level but is **not yet the final calibrated REFERENCE**.

## 1. Master / Gains

- MASTER: -9.0 dB
- SUB: -7.3 dB
- KICK: -18.4 dB
- MID L: -0.6 dB
- MID R: +0.6 dB
- HIGH L: -3.5 dB
- HIGH R: -1.8 dB

## 2. Polarities

- SUB: NORMAL
- KICK: INVERTED
- MID L: NORMAL
- MID R: NORMAL
- HIGH L: NORMAL
- HIGH R: NORMAL

## 3. Delays

- SUB: 0.000 ms, subsample true
- KICK: 1.300 ms
- MID L: 2.760 ms
- MID R: 2.760 ms
- HIGH L: 2.720 ms
- HIGH R: 2.720 ms

## 4. Crossovers

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

## 5. Per-way EQ

MID L/R:
- PK 1350 Hz
- -5.0 dB
- Q 1.02

HIGH L:
- PK 2850 Hz / -2.5 dB / Q 1.96
- PK 4600 Hz / -4.0 dB / Q 1.03
- HS 7763 Hz / +5.7 dB / Q 1

HIGH R:
- PK 2850 Hz / -2.5 dB / Q 1.96
- PK 4600 Hz / -4.0 dB / Q 0.70
- HS 7763 Hz / +5.7 dB / Q 1

## 6. Global/Input EQ active state

The live export keeps Global EQ/GEQ filter definitions but the E-Stack state marker reports:
- GEQ disabled
- PEQ disabled

No active pre-mixer Global EQ/Loudness stage appears in the supplied live pipeline.

## 7. Routing

Outputs:
- 0 SUB
- 1 KICK
- 2 MID L
- 3 MID R
- 4 HIGH L
- 5 HIGH R
- 6/7 spare

Normal programme:
- IN0/IN1
- SUB/KICK L+R sum, each source -6.0206 dB
- MID/HIGH stereo

REW:
- physical IN5
- ALSA CH4
- Camilla logical IN4
- Measurement Batch input 5

## 8. Measurement reference

- sample rate: 48 kHz
- native NI ASIO
- hardware timing loopback
- ECM8000
- Komplete Audio 1

## 9. Amplifiers and protection

| Way | Hard limiter | Compressor | Attack | Release | Ratio |
|---|---:|---:|---:|---:|---:|
| SUB | -12.6 dBFS | -13.6 dB | 10 ms | 500 ms | 20:1 |
| KICK | -15.8 dBFS | -16.8 dB | 5 ms | 300 ms | 20:1 |
| MID L/R | -5.1 dBFS | -6.1 dB | 2 ms | 200 ms | 20:1 |
| HIGH L/R | -5.1 dBFS | -6.1 dB | 1 ms | 150 ms | 20:1 |

Amplifier calibration reference remains documented in `docs/limiters-and-amplifiers.md`.

## 10. Remaining calibration

- six-way level match at C0
- MID/HIGH final delay/phase
- KICK/TOP final delay/phase
- SUB/KICK final delay/phase
- SUM/REV final validation
- room/system target EQ
- spatial validation
- final reference export

# Stereo room reference — Pass 1 acquisition

## Purpose

This is a **historical acquisition plan**, not evidence that its 42 steps were run. It was prepared for the then-current Stereo preset; it does not describe the later locked 2026-10-10 baseline.

Batch:
`measurements/batches/2026-09-30_stereo-room-reference-pass1.json`

Expected baseline:
- saved preset: `Stereo`
- Measurement Batch source in the **current JSON file**: intended physical IN3 (`measurementInput: 3`). The original IN5 plan is superseded; verify the actual socket/ALSA mapping before running.
- sample rate: 48 kHz
- REW loopback timing reference enabled
- master and per-way settings are captured live at `START BATCH`, so the result depends on the DSP state at that time, not on this plan's original Stereo assumptions

The batch disables `ESTACK_LOUDNESS` for the whole campaign so the dynamic listening curve does not contaminate calibration measurements. Output crossovers, PEQ, gains, delays, compressors and hard limiters remain active.

## Why this batch does not sweep dozens of delay values

Pass 1 is an acquisition campaign, not a blind parameter search.

The timed solo responses let the analysis stage model:
- polarity changes;
- arbitrary delay changes;
- relative level changes;
- phase tracking;
- complex summation;
- robustness over several listening positions.

The physical SUM/REV measurements are included as validation anchors.

After the resulting REW `.mdat` is analysed, create a short Pass 2 batch containing only the best candidate settings and nearby verification points.

## Microphone positions

Keep capsule height and orientation unchanged.

- `C0`: main listening position.
- `L20`: 20 cm left of C0.
- `R20`: 20 cm right of C0.
- `F20`: 20 cm forward of C0.
- `B20`: 20 cm behind C0.

At C0, do not move the microphone between M01 and M22.

## Stereo-specific logic

SUB and KICK are mono ways while MID/HIGH are stereo.

For `SYSTEM L EMU` and `SYSTEM R EMU`, SUB and KICK are attenuated by exactly **-6.0206 dB**. This reproduces the contribution of one programme channel to the normal L+R mono summation while leaving the selected MID/HIGH side at its normal baseline level.

`SYSTEM MONO C0` sends the same correlated measurement signal to both stereo heads and the mono low section. It is useful for phantom-centre verification, but it must not be the sole basis for room EQ above the bass because L/R acoustic summation creates comb filtering.

## Required REW practice

- Native NI ASIO.
- 48 kHz.
- Hardware loopback timing reference.
- Use the exact measurement names shown by the batch.
- Start at the requested -20 dBFS only if the previously validated measurement chain is unchanged and meters show safe headroom; otherwise start lower and repeat the affected step at a documented level.
- Do not change CamillaDSP manually during the batch.
- Save all 42 traces in one `.mdat`.

## Analysis after Pass 1

Analyse, in this order:

1. measurement integrity / timing repeatability;
2. MID/HIGH L and R independently;
3. KICK/MID against both stereo sides;
4. SUB/KICK over C0/L20/R20/F20/B20;
5. left/right balance;
6. spatial-average target / room EQ;
7. candidate crossover and delay simulation;
8. short physical verification batch.

Do not commit new calibration values to `CURRENT_REFERENCE.md` until Pass 2 confirms them physically.

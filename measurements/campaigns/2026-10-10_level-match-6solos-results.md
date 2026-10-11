# 2026-10-10 — Six-way level-match results at C0

## Source

REW file supplied by user:
- `FULL_measuremennt.mdat`

The raw `.mdat` is not committed here. The numbers below are the dated analysis record; reproducing the complex calculation requires the source file and the complete live DSP export.

Locked DSP starting reference:
- title: `Stereo-LR-balanced-L-PAD`
- export timestamp: `2026-10-10T18:58:49.858Z`
- config revision: `3b3d5f8e04576343db5a63b3a549f19dd92db640ee3955145d99aaed9e16631f`
- Measurement Batch input: physical IN3 = CamillaDSP zero-based IN2/channel 2 = `measurementInput: 3`

Measurements found:
- `FULL`
- `L01_SUB_SOLO_C0`
- `L02_KICK_SOLO_C0`
- `L03_MID_L_SOLO_C0`
- `L04_HIGH_L_SOLO_C0`
- `L05_MID_R_SOLO_C0`
- `L06_HIGH_R_SOLO_C0`

All sweeps use the REW loopback timing reference.

## Integrity

The complex sum reconstructed from the six SOLO traces reproduces the measured FULL trace closely enough to treat the campaign as valid.

Median absolute reconstruction error:
- 40–120 Hz: ~0.16 dB
- 120–350 Hz: ~0.27 dB
- 350–1800 Hz: ~0.85 dB
- 1.8–16 kHz: ~0.97 dB

This confirms that routing and solo-way acquisition are coherent.

## Current solo levels — useful bands

Values below use the saved REW smoothed SPL data and log-frequency-equal weighting.

| Way | Evaluation band | Approx. median SPL |
|---|---:|---:|
| SUB | 55–105 Hz | 85.4 dB |
| KICK | 170–260 Hz | 76.1 dB |
| MID L | 700–1600 Hz | 81.7 dB |
| MID R | 700–1600 Hz | 81.9 dB |
| HIGH L | 3–6.5 kHz | 75.8 dB |
| HIGH R | 3–6.5 kHz | 76.4 dB |
| HIGH L | 8–14 kHz | 82.7 dB |
| HIGH R | 8–14 kHz | 83.1 dB |

These broad-band values are **not** direct gain instructions because C0 contains room effects and the HIGH response contains deliberate per-way EQ.

## L/R balance

At C0:
- MID L/R are effectively balanced in their core band; median difference ~0.2 dB.
- HIGH R is only ~0.6–0.7 dB above HIGH L in 3–6.5 kHz.
- Do not create new L/R gain offsets from this single room position.

Keep for now:
- MID L/R = 0.0 / 0.0 dB
- HIGH L/R = -4.0 / -4.0 dB

## Crossover-level observations

### SUB ↔ KICK

Around 120–150 Hz:
- SUB is roughly 2.5–3 dB above KICK around 125–140 Hz.
- A **temporary calibration candidate** is SUB -2.5 dB relative to the locked baseline, i.e. approximately -9.8 dB instead of -7.3 dB, if the goal is equal-magnitude crossover alignment before adding the final house-curve bass lift.

Do not commit this as final listening gain until SUM/REV and target validation.

### KICK ↔ MID

Across roughly 380–480 Hz:
- KICK median ~75.6 dB
- MID L median ~74.5 dB
- MID R median ~75.6 dB

The existing KICK gain is therefore already close to the MID acoustic overlap. Do **not** raise KICK by 6–8 dB merely to fill the broad 200–800 Hz room depression.

Keep KICK = -18.4 dB for the next phase/delay pass.

### MID ↔ HIGH

Across roughly 1.9–2.1 kHz:
- MID L ~73.1 dB, HIGH L ~73.6 dB
- MID R ~72.3 dB, HIGH R ~70.8 dB

The current -4 dB HIGH gains are close enough for phase work. The right-side difference is too small / position-dependent to justify a permanent one-point L/R correction yet.

## HIGH tonal-shape issue

The HIGH way is not a simple gain problem:
- 3–6.5 kHz is around 76 dB;
- 8–14 kHz is around 83 dB.

Therefore increasing HIGH gain to fix 3–6 kHz would make the upper treble substantially too high.

Current HIGH processing includes:
- 2850 Hz / -2.5 dB
- 4600 Hz / -4 dB
- 7763 Hz high-shelf / +5.7 dB

The next tonal-EQ pass must treat these filters separately from way gain. Do not solve this shape with output gain alone.

## Timing observations

REW-reported loopback-relative delays:
- SUB ~51.917 ms
- KICK ~51.979 ms
- MID L ~46.479 ms
- HIGH L ~46.187 ms
- MID R ~46.146 ms
- HIGH R ~45.833 ms

The stereo deployment therefore requires a fresh phase/delay optimisation. Do not copy the old stack-layout alignment directly.

These delay readings are diagnostic arrival information, not direct DSP delay commands. Final DSP delays must be found from complex phase / summation across each crossover.

## Decision

Validated now:
- campaign is usable;
- keep KICK, MID L/R and HIGH L/R gains unchanged for phase work;
- no L/R gain correction is justified from C0 alone;
- HIGH tonal imbalance is EQ-shape, not output-gain only.

Candidate to test, not yet final:
- SUB approximately -2.5 dB relative to baseline for equal-magnitude SUB/KICK alignment.

Next step:
- phase/delay optimisation using the same locked reference, followed by physical SUM/REV verification and only then final room/house-curve gains/EQ.

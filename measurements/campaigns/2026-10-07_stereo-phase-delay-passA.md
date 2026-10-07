# Stereo phase/delay optimisation — Pass A

## Purpose

This campaign is the **first calibration pass** to run before room-target optimisation.

It exists because the current Stereo preset still contains provisional timing choices. The campaign acquires the six DSP ways independently at five listening-area positions with the REW hardware loopback timing reference, so relative delay, polarity and optional first-order all-pass phase trims can be optimised numerically before making more room-EQ decisions.

Batch:
`measurements/batches/2026-10-07_stereo-phase-delay-passA.json`

## Baseline assumptions from the current Stereo export

Current saved-preset values supplied on 2026-09-30 include:

- SUB delay: 0.000 ms
- KICK delay: 1.300 ms
- MID L/R delay: 2.760 ms
- HIGH L/R delay: 2.720 ms
- KICK polarity: inverted
- SUB/MID/HIGH polarities: normal
- XO: 130 Hz, 300 Hz, 2000 Hz
- per-way PEQ and protection active

These values are the **starting baseline**, not the final answer.

The batch disables `ESTACK_LOUDNESS` because a master-dependent curve must not alter calibration data. It keeps the current crossovers, per-way PEQ, gain structure, compressors and hard limiters.

## Why no physical delay grid in Pass A

Delay and AllpassFO are linear deterministic transfer functions. Once each source is measured with a stable hardware timing reference, candidate delay/polarity/phase settings can be applied to the measured complex transfer functions offline.

Therefore Pass A measures information, not guesses.

The five physical SUM/REV pairs at C0 validate that the complex solo responses reconstruct the real acoustic sums before the optimiser is trusted.

## Measurements

### C0

P01-P06:
- SUB
- KICK
- MID L
- HIGH L
- MID R
- HIGH R

P07-P16:
- MID/HIGH L SUM/REV
- MID/HIGH R SUM/REV
- KICK/MID L SUM/REV
- KICK/MID R SUM/REV
- SUB/KICK SUM/REV

P17-P18:
- program-left emulation
- program-right emulation

### Spatial positions

At each position all six sources are measured independently:

- L20
- R20
- F20
- B20

This is essential for the current deployment because one mono KICK and one mono SUB DSP way must integrate with **two spatially separated stereo tops**. A setting that is perfect only at C0 is not automatically the best listening-area solution.

## REW settings

- 48 kHz
- native NI ASIO
- hardware loopback timing reference
- same microphone orientation throughout
- full-range 20 Hz–20 kHz sweep for every trace
- requested level: -30 dBFS

The full-range sweep is intentional. The existing electrical crossovers/protection limit the signal delivered to each driver, while using one sweep range makes comparison and complex-response processing easier.

If -30 dBFS gives inadequate SNR in a crossover region, repeat only the affected trace at a safely verified higher level and document it.

## Optimisation sequence after the .mdat is returned

### 1. Measurement integrity

First prove that the measured SUM traces match complex sums reconstructed from their SOLO traces.

If reconstruction is inconsistent, do not optimise from that pair until the bad trace is identified.

### 2. MID/HIGH internal alignment

Optimise left and right independently first.

Search:
- relative delay;
- polarity;
- optional AllpassFO phase trim;
- phase tracking across the full 2 kHz acoustic overlap, not one frequency point.

The same-side MID/HIGH solution should maximise broad SUM and reverse-null quality without degrading nearby positions.

### 3. KICK ↔ TOP integration

Once each MID/HIGH pair is internally aligned, preserve that relation.

Optimise the **common top timing relative to KICK** jointly against MID L and MID R. Because KICK is mono while the tops are spatially separated, the objective is a best joint solution, not an impossible independent perfect delay to both sides.

Any common timing move of a top must move MID and HIGH together.

### 4. SUB ↔ KICK

After KICK/TOP is fixed, align SUB to the already aligned system above it.

Prefer moving SUB timing/polarity so the KICK/TOP relationship stays intact.

If multiple physical sub cabinets share the single SUB DSP output, they are acoustically one controllable source for timing purposes. Individual sub-to-sub alignment would require independent DSP outputs.

### 5. Optional phase trim

Only after the correct delay branch is found, test first-order AllpassFO trims around the relevant crossover if they improve:
- complex summation;
- reverse null;
- spatial robustness;
- group delay.

Do not use an all-pass to hide a wrong delay branch.

### 6. Numerical search

Use fine numerical resolution offline rather than physical sweeps.

Suggested search spaces:
- MID/HIGH relative delay: baseline ±0.30 ms, then refine around the optimum to ~5–10 µs;
- common TOP ↔ KICK timing: broad enough to include the current 1.46 ms MID-vs-KICK offset, then refine;
- SUB ↔ KICK timing: search several milliseconds in both directions via an equivalent non-negative Camilla delay solution;
- both polarity states where physically meaningful;
- AllpassFO: 0 to -179 degrees only after delay selection.

Score C0 strongly but include L20/R20/F20/B20 so the result remains useful over the listening area.

### 7. Pass B

After numerical ranking, generate a **short physical verification batch** containing only:
- current baseline;
- best candidate;
- one nearby candidate;
- SUM/REV validation for each crossover;
- final left/right program checks.

Only after Pass B should validated delay/phase values replace the current reference.

# E-Stack — Reference Preset Backup

Ce document est le snapshot de reconstruction du preset actuellement utilisé comme base de calibration.

## 1. Gains

- MASTER: -12.0 dB
- SUB: -9.5 dB
- KICK: -19.3 dB
- MID L: -14.0 dB
- MID R: -14.0 dB
- HIGH L: -7.6 dB
- HIGH R: -7.6 dB

## 2. Polarités

- SUB: NORMAL
- KICK: INVERTED
- MID L: NORMAL
- MID R: NORMAL
- HIGH L: NORMAL
- HIGH R: NORMAL

## 3. Delays

- MID L: 2.760 ms
- MID R: 2.760 ms
- HIGH L: 2.720 ms
- HIGH R: 2.720 ms

À compléter :
- SUB delay absolu
- KICK delay absolu

Ne pas inventer ces deux valeurs.

## 4. Crossovers

SUB:
- HPF 40 Hz BW24
- LPF 130 Hz LR24

KICK:
- HPF 130 Hz LR24
- LPF 300 Hz LR24

MID L/R:
- HPF 300 Hz LR24
- LPF 2000 Hz LR24

HIGH L/R:
- HPF 2000 Hz LR24

## 5. PEQ de voie

MID L/R:
- PK 1350 Hz
- -5.0 dB
- Q 1.0

HIGH L/R:
- PK 2850 Hz
- -2.5 dB
- Q 2.0

HIGH L/R:
- PK 4600 Hz
- -4.0 dB
- Q 1.0

## 6. System EQ

État actuel observé :
- PK/BELL 162 Hz
- -4.0 dB
- Q 0.70

Placement observé :
- Input Processing
- shared Input L/R
- pre-routing

Action prévue :
- déplacer le System EQ après `estack_preview`
- avant les crossovers/per-way processing
- afin que musique et REW traversent la même correction

## 7. Routing

Outputs:
- 0 SUB
- 1 KICK
- 2 MID L
- 3 MID R
- 4 HIGH L
- 5 HIGH R
- 6/7 spare

REW:
- logical IN4
- 0 dB vers les voies mesurées

Normal source:
- IN0/IN1
- SUB/KICK mono sum avec -6.0206 dB par source
- MID/HIGH stéréo

## 8. Mesure

- sample rate: 48 kHz
- REW timing reference: loopback
- Komplete Audio 1
- ECM8000
- source REW actuelle: IN4 Camilla

## 9. État normal actuel

Quand aucune mesure reverse n'est en cours :
- SUB NORMAL
- KICK INVERTED
- MID NORMAL
- HIGH NORMAL

## 10. Amplificateurs et limiteurs

Source utilisateur datée du 30/08/2026.

| Voie | Ampli | Réglage ampli | Gain mesuré | Limite HP | Équiv. puissance | Hard Limiter Camilla | Compresseur | Attack | Release | Ratio |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| SUB | t.amp E1200 | Potard max | 40.1 dB | 50.0 Vrms | 625 W @ 4 Ω total | -12.6 dBFS | -13.6 dB | 10 ms | 500 ms | 20:1 |
| KICK | t.amp E1200 | Potard max | 40.1 dB | 34.6 Vrms | 300 W @ 4 Ω | -15.8 dBFS | -16.8 dB | 5 ms | 300 ms | 20:1 |
| MID L | t.amp E400 | 26 dB, potard max | 26.7 dB | 25.3 Vrms | 80 W @ 8 Ω | -5.1 dBFS | -6.1 dB | 2 ms | 200 ms | 20:1 |
| MID R | t.amp E400 | 26 dB, potard max | 26.7 dB | 25.3 Vrms | 80 W @ 8 Ω | -5.1 dBFS | -6.1 dB | 2 ms | 200 ms | 20:1 |
| HIGH L | ampli HIGH/Fosi | Potard réduit | 19.9 dB | 11.5 Vrms | ≈16.5 W @ 8 Ω | -5.1 dBFS | -6.1 dB | 1 ms | 150 ms | 20:1 |
| HIGH R | ampli HIGH/Fosi | même position | ≈19.9 dB* | 11.5 Vrms | ≈16.5 W @ 8 Ω | -5.1 dBFS | non documenté | 1 ms | 150 ms | 20:1 |

Voir aussi `docs/limiters-and-amplifiers.md` pour les remarques de traçabilité.

## 11. Éléments encore à sauvegarder

Avant de considérer ce backup comme définitif :
- valeur absolue delay SUB
- valeur absolue delay KICK
- comparer les hard limiters et compresseurs ci-dessus avec le YAML réellement chargé
- confirmer le seuil Compresseur HIGH R (cellule vide dans la capture source)
- autres protections / hard limits éventuellement présentes dans la pipeline
- YAML final exporté

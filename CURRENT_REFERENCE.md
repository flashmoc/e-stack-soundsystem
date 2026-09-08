# E-Stack — Current Reference

Dernier état de référence connu pour la calibration actuelle.

## Gains

- MASTER: **-12.0 dB**
- SUB: **-9.5 dB**
- KICK: **-19.3 dB**
- MID L/R: **-14.0 dB**
- HIGH L/R: **-7.6 dB**

## Polarités

- SUB: **NORMAL**
- KICK: **INVERTED**
- MID L/R: **NORMAL**
- HIGH L/R: **NORMAL**

## Delays connus

- MID L/R: **2.760 ms**
- HIGH L/R: **2.720 ms**
- Différence MID/HIGH: **MID +0.040 ms** par rapport au HIGH
- SUB/KICK: valeurs absolues encore à capturer depuis la config DSP avant de considérer le backup comme complet

## Crossovers

- SUB: HPF **40 Hz BW24**, LPF **130 Hz LR24**
- KICK: HPF **130 Hz LR24**, LPF **300 Hz LR24**
- MID L/R: HPF **300 Hz LR24**, LPF **2000 Hz LR24**
- HIGH L/R: HPF **2000 Hz LR24**

## PEQ de voie

MID L/R:
- PK **1350 Hz / -5.0 dB / Q 1.0**

HIGH L/R:
- PK **2850 Hz / -2.5 dB / Q 2.0**
- PK **4600 Hz / -4.0 dB / Q 1.0**

## System EQ actuel

- PK/BELL **162 Hz / -4.0 dB / Q 0.70**

Placement observé actuellement:
- Input Processing
- `shared Input L/R - pre-routing`

Point à corriger/valider:
- la source REW arrive sur IN4 et bypass probablement ce filtre ; le System EQ doit idéalement être placé après le mixer `estack_preview` et avant les traitements de voie pour que musique et REW traversent la même correction.

## Routing

- OUT0 SUB
- OUT1 KICK
- OUT2 MID L
- OUT3 MID R
- OUT4 HIGH L
- OUT5 HIGH R
- OUT6/7 libres

Source REW:
- Camilla logical IN4
- ALSA zero-based CH4
- physical/human IN5

## Statut

Déjà fortement validé:
- polarités SUB/KICK
- calage relatif MID/HIGH
- retard commun du TOP par rapport au KICK
- PEQ MID/HIGH actuels

À terminer avant REFERENCE final:
- déplacer/valider le System EQ commun
- recheck final SUM/REV MID-HIGH après PEQ
- recheck final KICK-MID
- capturer delays absolus SUB/KICK
- limiteurs
- directivité
- distorsion/headroom
- export YAML final

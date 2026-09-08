# E-Stack — Current State

Dernière base de travail connue pour la calibration actuelle.

## Architecture

Chaîne :
- Raspberry Pi 5
- RASPIAUDIO 8×IN / 8×OUT
- CamillaDSP / CamillaNode
- REW avec timing loopback
- Komplete Audio 1
- ECM8000

## Mapping sorties

- OUT0 = SUB
- OUT1 = KICK
- OUT2 = MID L
- OUT3 = MID R
- OUT4 = HIGH L
- OUT5 = HIGH R
- OUT6/7 = libres

## Source de mesure REW

- entrée logique Camilla : IN4
- ALSA zero-based : CH4
- entrée physique/humaine : IN5

Le signal REW est routé à 0 dB vers la/les voies mesurées.

## État normal actuel

Polarités :
- SUB = NORMAL
- KICK = INVERTED
- MID L/R = NORMAL
- HIGH L/R = NORMAL

Delays connus :
- MID L/R = 2.760 ms
- HIGH L/R = 2.720 ms
- différence MID/HIGH = MID +0.040 ms par rapport au HIGH

Valeurs absolues SUB/KICK :
- à extraire de la config DSP actuelle avant de considérer le backup comme totalement complet

## Crossovers actuels

SUB :
- HPF 40 Hz Butterworth 24 dB/oct
- LPF 130 Hz Linkwitz-Riley 24 dB/oct

KICK :
- HPF 130 Hz Linkwitz-Riley 24 dB/oct
- LPF 300 Hz Linkwitz-Riley 24 dB/oct

MID L/R :
- HPF 300 Hz Linkwitz-Riley 24 dB/oct
- LPF 2000 Hz Linkwitz-Riley 24 dB/oct

HIGH L/R :
- HPF 2000 Hz Linkwitz-Riley 24 dB/oct

## Gains actuels

- MASTER = -12.0 dB
- SUB = -9.5 dB
- KICK = -19.3 dB
- MID L = -14.0 dB
- MID R = -14.0 dB
- HIGH L = -7.6 dB
- HIGH R = -7.6 dB

## PEQ de voie

MID L/R :
- PK 1350 Hz
- Gain -5.0 dB
- Q 1.0

HIGH L/R :
- PK 2850 Hz
- Gain -2.5 dB
- Q 2.0

HIGH L/R :
- PK 4600 Hz
- Gain -4.0 dB
- Q 1.0

## System / Input EQ actuel

Filtre actuellement présent :
- PK/BELL 162 Hz
- Gain -4.0 dB
- Q 0.70

Important :
- actuellement vu dans Input Processing comme `shared Input L/R - pre-routing`
- la source REW IN4 le bypass probablement
- architecture cible : placer le System EQ après `estack_preview` et avant les traitements de voie

## Mixer

Musique IN0/IN1 :
- SUB/KICK : sommation L+R à -6.0206 dB par source
- MID/HIGH : stéréo

REW IN4 :
- source unique
- mappings REW à 0 dB
- pas de -6.02 dB lié à la sommation L/R

## État de calibration

Validé / fortement retenu :
- SUB normal
- KICK inversé
- MID/HIGH normal
- TOP commun retardé par rapport au KICK
- différence MID/HIGH ~0.040 ms
- PEQ MID 1350/-5/Q1
- PEQ HIGH 2850/-2.5/Q2
- PEQ HIGH 4600/-4/Q1
- target globale descendante légère dans l'aigu
- grave légèrement relevé

À revalider avant de déclarer REFERENCE final :
- System EQ après mixer
- effet réel du 162 Hz sur REW
- dernier recheck MID/HIGH après PEQ
- dernier recheck KICK/MID
- valeurs absolues delay SUB/KICK
- limiteurs
- directivité
- distorsion/headroom

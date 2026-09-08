# E-Stack — System Architecture

## Signal chain

Source musicale :

`IN0/IN1 → traitement entrée → mixer estack_preview → traitements système communs → crossovers / PEQ / gains / delays / polarités / protections → OUT0..OUT5`

Source REW actuelle :

`REW → RASPIAUDIO physical IN5 → ALSA CH4 → Camilla IN4 → mixer estack_preview → traitements de sortie`

## Point d’architecture à corriger

Le Global/System EQ à 162 Hz est actuellement observé en `shared Input L/R - pre-routing`.

Comme REW arrive sur IN4, il bypass probablement ce filtre.

Architecture cible :

`toutes sources → estack_preview → SYSTEM EQ commun → traitements de voies`

Ainsi :
- musique et REW traversent la même target globale,
- un EQ commun n’altère pas la phase relative entre les voies d’un crossover,
- les PEQ intrinsèques restent séparés par voie.

## Outputs

- OUT0 SUB
- OUT1 KICK
- OUT2 MID L
- OUT3 MID R
- OUT4 HIGH L
- OUT5 HIGH R
- OUT6/7 libres

## Normal routing

IN0/IN1 :
- SUB/KICK sommés L+R à -6.0206 dB par source,
- MID/HIGH stéréo.

REW IN4 :
- routage mono de mesure à 0 dB vers les voies sélectionnées,
- une seule source, donc pas de compensation -6.02 dB liée à la sommation L/R.

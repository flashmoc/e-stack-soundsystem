# E-Stack — System Architecture

## Signal chain

Source musicale :

`IN0/IN1 → traitement entrée → mixer estack_preview → traitements système communs → crossovers / PEQ / gains / delays / polarités / protections → OUT0..OUT5`

## Mesures REW — deux chemins selon le mode

**1. Measure current system (état actuel)**

`REW → RASPIAUDIO physical IN3 → CamillaDSP source CH2 (zéro-based) → shared Input L/R filters mirrored to IN3 → mixer (source 0 dB) → traitements de voies OUT0..OUT5`

- Le bouton **MEASURE NOW** force temporairement **IN3** sur les six destinations logiques du mixer, sans toucher aux réglages matériels `devices`.
- Les gains de voies Control, leurs états MUTE (pour les voies choisies), Input Trim, Loudness, EQ, crossovers, délais, polarités et protections sont conservés depuis la capture au démarrage.
- Les voies non choisies sont mutées temporairement. `−60 dB` sur une voie est une atténuation, **pas un mute**.
- Pour mesurer via ce mode, vérifier que la **sortie de l'interface REW est réellement câblée à physical IN3** ; le dernier schéma historique mentionne IN5 pour les anciennes campagnes.
- Garder le volume WiiM constant pendant le sweep si Loudness est actif.

**2. Campagne JSON importée (calibration)**

Dernier chemin matériel noté dans le projet (historique à vérifier si le câble a changé) :

`REW → RASPIAUDIO physical IN5 → ALSA CH4 (zéro-based) → Camilla logical IN4 → mixer (source 0 dB si measurementInput: 5) → traitements de voies`

- `defaults.measurementInput: 5` vaut pour cette entrée physique **uniquement si le câble est encore sur IN5**. Dans le cas contraire, adapter `measurementInput` au numéro physique réellement raccordé.
- Si aucun `measurementInput` n'est défini, le routage du mixer capturé est préservé.
- Les EQ d'entrée communs à L/R sont recopiés temporairement sur l'entrée de mesure choisie ; ils ne sont pas contournés quand le mode Measurement Batch est actif.
- Les voies choisies sont démûtées ; les autres mutées par défaut. Les gains peuvent recevoir des **offsets négatifs relatifs** à la baseline.
- Loudness et Input Trim sont forcés OFF pendant la campagne.

**Règle commune :** le Master est abaissé à au plus −60 dB pour une transition de graphe, puis restauré. Fin/annulation rétablit la configuration et le mixer capturés. Aucun changement permanent au hardware `devices`.

**À vérifier sur le Raspberry :** après les évolutions de câblage, confirmer l'entrée physique effectivement alimentée par la Komplete Audio 1 et sa correspondance ALSA/CamillaDSP, puis mettre à jour l'état courant. Ne pas déduire cette correspondance du seul numéro de source logique.

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

## Routing des mesures

- Mode **état actuel** : IN3 physique, une seule source mono à 0 dB dans les six destinations de mixer ; les gains de sortie capturés restent en place.
- Mode **campagne importée** : entrée choisie via `measurementInput`, historiquement IN5 pour le câblage REW documenté ; 0 dB ne concerne que le gain de source du mixer, pas les gains de sortie.
- Les voies exclues sont mutées par leur filtre de gain, sans désactiver les protections.

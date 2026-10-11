# E-Stack — System Architecture

## Signal chain

Source musicale :

`IN0/IN1 → traitement d'entrée partagé s'il est actif → mixer estack_preview → crossovers / PEQ de voie / gains / délais / polarités / protections → destinations logiques 0..5`

Dans l'export daté du 10 octobre, les définitions GEQ/PEQ d'entrée existent mais sont **désactivées** ; aucune étape Global EQ ou Loudness active n'apparaît avant le mixer. Le logiciel place les traitements d'entrée actifs **avant** le mixer. Un « System EQ » commun après le mixer est une proposition d'architecture distincte, pas le graphe observé. CamillaDSP expose 8 canaux matériels playback ; les six voies logiques ne prouvent pas quelles prises physiques du DAC8x leur correspondent.

## Mesures REW — deux chemins selon le mode

**1. Measure current system (état actuel)**

`REW → prise IN3 rapportée → CamillaDSP source CH2 (index zéro) → filtres Input L/R partagés recopiés sur CH2 s'ils sont actifs → mixer (gain source 0 dB) → six voies logiques`

- Le bouton **MEASURE NOW** force temporairement **IN3** sur les six destinations logiques du mixer, sans toucher aux réglages matériels `devices`.
- Les gains de voies Control, leurs états MUTE (pour les voies choisies), Input Trim, Loudness, EQ, crossovers, délais, polarités et protections sont conservés depuis la capture au démarrage.
- Les voies non choisies sont mutées temporairement. `−60 dB` sur une voie est une atténuation, **pas un mute**.
- Pour mesurer via ce mode, vérifier que la **sortie de l'interface REW est réellement câblée à physical IN3** et que l'ordre ALSA des entrées le confirme ; le dernier schéma historique mentionne IN5 pour d'anciennes campagnes.
- Garder le volume WiiM constant pendant le sweep si Loudness est actif.

**2. Campagne JSON importée (calibration)**

Chemin visé par les JSON actuels, sous réserve de vérification physique :

`REW → RASPIAUDIO physical IN3 → CamillaDSP zero-based IN2 / channel 2 → mixer (source 0 dB avec measurementInput: 3) → traitements de voies`

- `defaults.measurementInput: 3` correspond à **physical IN3**, car le champ JSON utilise une numérotation physique one-based.
- Si aucun `measurementInput` n'est défini, le routage du mixer capturé est préservé.
- Les EQ d'entrée communs à L/R sont recopiés temporairement sur l'entrée de mesure choisie ; ils ne sont pas contournés quand le mode Measurement Batch est actif.
- Les voies choisies sont démûtées ; les autres mutées par défaut. Les gains peuvent recevoir des **offsets négatifs relatifs** à la baseline.
- Loudness et Input Trim sont forcés OFF pendant la campagne.

**Règle commune :** le Master est abaissé à au plus −60 dB pour une transition de graphe, puis restauré. Fin/annulation rétablit la configuration et le mixer capturés. Aucun changement permanent au hardware `devices`.

**À vérifier sur le Raspberry :** confirmer l'entrée physique alimentée par la Komplete Audio 1, sa correspondance ALSA/CamillaDSP et les prises des huit sorties. Ne pas déduire ce mapping physique du seul numéro de source ou de destination logique.

## Outputs

- OUT0 SUB
- OUT1 KICK
- OUT2 MID L
- OUT3 MID R
- OUT4 HIGH L
- OUT5 HIGH R
- destinations logiques 6/7 sans voie E-Stack dans l'export daté ; prises physiques à vérifier

## Normal routing

IN0/IN1 :
- SUB/KICK sommés L+R à -6.0206 dB par source,
- MID/HIGH stéréo.

## Routing des mesures

- Mode **état actuel** : IN3 physique, une seule source mono à 0 dB dans les six destinations de mixer ; les gains de sortie capturés restent en place.
- Mode **campagne importée** : entrée actuelle **physical IN3 / measurementInput: 3** ; 0 dB ne concerne que le gain de source du mixer, pas les gains de sortie.
- Les voies exclues sont mutées par leur filtre de gain, sans désactiver les protections.

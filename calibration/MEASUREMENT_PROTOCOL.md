# E-Stack — Measurement Protocol

## Choisir le bon mode Measurement Batch avant toute mesure

**Deux modes, deux comportements de capture différents.**

| Propriété | Mesure « état actuel » (MEASURE NOW) | Campagne JSON importée (START BATCH) |
| --- | --- | --- |
| Source REW | **Physical IN3**, imposée par le serveur | `defaults.measurementInput` = numéro physique IN1…IN8, sinon routing capturé |
| Capture de référence | **Nouvelle** capture à chaque clic | **Une seule** capture au démarrage de la campagne |
| Mixer | IN3 vers six destinations à **0 dB gain source** | Entrée sélectionnée vers six destinations à **0 dB gain source** si configurée |
| Voies sélectionnées | Gain **et MUTE** de Control inchangés | Démûtées ; gain baseline + offsets négatifs éventuels |
| Voies exclues | Mutées temporairement | Mutées par défaut |
| Input Trim et Loudness | **Conservés** | **Forcés OFF** |
| Autres filtres / protections | Capturés et conservés | Capturés, sauf ajustements de calibration explicitement demandés |
| Fin / annulation | Restore config + routing capturés | Restore config + routing capturés |

**Pour une mesure rapide avec le preset courant**, connecter effectivement la sortie de la carte son REW à **physical IN3**, choisir les voies dans **Measure current system**, puis cliquer **MEASURE NOW**. Le fait de régler une voie à **−60 dB n'est pas un mute** : la désélectionner, ou la muter **avant** la capture, pour l'exclure complètement. Un nouveau clic après FINISH/ABORT capture les modifications faites entre-temps dans Control.

**For imported E-Stack JSON campaigns, set `"measurementInput": 3`.** The user reports the REW interface on physical IN3 for both measurement modes. `Measure current system` always selects CamillaDSP channel 2 automatically; calibration campaigns do so through the JSON field. Previous IN5 / `measurementInput: 5` notes are superseded. Verify the physical socket and ALSA correspondence by signal test before relying on this route.

Dans les deux modes, les paramètres matériels `devices` restent inchangés. Lors de chaque modification temporaire de graphe, le Master passe au plus à **−60 dB**, puis revient au niveau précédent. Vérifier le panneau **ACTUAL DSP** et le statut de conformité à la configuration attendue avant d'interpréter la mesure ; FINISH/ABORT rétablit le DSP et le mixer de début de session.

**Attention Loudness en « état actuel » :** le traitement est conservé et peut varier avec le volume WiiM pendant le sweep. Conserver le volume source constant pour des comparaisons ; pour une mesure de référence statique, désactiver le Loudness **avant** MEASURE NOW. Ne pas utiliser l'outil Signal Generator interne en même temps qu'un Measurement Batch.

Pour les détails du traitement et des endpoints, voir `docs/camillanode/measurement-batch.md`.

## A. Avant de mesurer

Vérifier :
- 48 kHz partout
- driver natif/ASIO de la Komplete Audio 1 (ou du périphérique REW effectivement employé)
- loopback actif
- aucune saturation
- protections actives
- routing Camilla correct **pour le mode choisi** (IN3 fixe en état actuel / INx configurable en JSON)
- aucune voie inattendue dans les meters
- micro immobile pendant une série
- gains fixes
- master fixe
- sweep fixe
- configuration DSP sauvegardée

Si le routing semble incohérent :
- arrêter immédiatement
- baisser/couper les amplis
- vérifier Camilla
- redémarrer si nécessaire
- reprendre à très bas niveau

## B. Série de base pour un crossover A/B

1. `A_SOLO`
2. `B_SOLO`
3. `AB_SUM`
4. `AB_REV`

Pour `REV`, inverser une seule voie.

Après la mesure REV :
- remettre immédiatement la polarité normale de fonctionnement.

## C. Crossover MID/HIGH

Exemple :
- SUB MUTE
- KICK MUTE
- MID L ON
- HIGH L ON
- droite mutée si une seule tête est étudiée

Mesures :
- MID solo
- HIGH solo
- MID+HIGH normal
- MID+HIGH avec HIGH inversé

## D. Crossover KICK/MID

Mesures :
- KICK solo
- MID solo
- KICK+MID normal
- KICK inversé + MID

Si le TOP est déjà aligné :
- tout offset de delay appliqué au TOP doit être commun au MID et HIGH.

## E. Crossover SUB/KICK

Mesures :
- SUB solo
- KICK solo
- SUB+KICK
- SUB+KICK avec une seule voie inversée

Ne pas modifier simultanément polarité et delay entre deux mesures comparées.

## F. Spatial average

Pour la target :
- Centre
- +20 cm gauche
- +20 cm droite
- éventuellement avant
- éventuellement arrière

Même système, même gain, même sweep.

## G. Directivité

Pour optimisation d'architecture :
- 0°
- +10°
- -10°
- +20°
- -20°
- +30°
- -30°

Conserver distance et hauteur constantes.

## H. Mesure outdoor / speaker preset

Idéalement :
- un seul stack
- espace dégagé
- distance documentée
- hauteur documentée
- ground-plane pour le grave si pertinent
- gating pour médium/aigu
- protections conservées

Objectif :
- réponse intrinsèque
- phase
- directivité
- THD
- crossover acoustique

## I. Nommage

Toujours coder la condition réelle dans le nom.

Exemples :
- `KM_T22_KINV`
- `MH_P040_REV`
- `TARGET3_C`
- `SYSTEM_EQ_ON`

Éviter les noms génériques du type `mesure1`.

## J. Critères d'arrêt

Arrêter si :
- clipping
- crack numérique
- sortie dans le mauvais caisson
- niveau anormal
- timing loopback incohérent
- mesure impossible physiquement
- Camilla a changé de routing

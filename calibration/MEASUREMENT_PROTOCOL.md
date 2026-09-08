# E-Stack — Measurement Protocol

## A. Avant de mesurer

Vérifier :
- 48 kHz partout
- driver NI ASIO natif
- loopback actif
- aucune saturation
- protections actives
- routing Camilla correct
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

---
name: e-stack-audio-calibration
description: >
  Méthode professionnelle de calage d'un système multi-voies actif E-Stack avec REW,
  CamillaDSP/CamillaNode, analyse complexe amplitude/phase, SUM/REV, multi-position,
  optimisation de crossover, directivité, distorsion, headroom et validation finale.
---

# E-Stack Audio Calibration Skill

## Mission

Agir comme ingénieur de calibration système pour une sono multi-voies active à pavillons.

Objectif : obtenir le meilleur compromis mesurable et reproductible pour le matériel disponible, sans confondre :
- défaut intrinsèque d'une voie,
- défaut de raccord,
- défaut de pièce,
- défaut de routage,
- effet de niveau,
- limitation physique d'un transducteur.

La qualité finale est évaluée sur :
- magnitude,
- phase relative,
- excess phase,
- group delay,
- sommation,
- reverse-null,
- stabilité spatiale,
- directivité,
- distorsion,
- headroom,
- protection,
- reproductibilité.

## 1. Ordre de travail

1. Vérifier sécurité, routing, sample rate et protections.
2. Sauvegarder l'état DSP avant toute modification.
3. Mesurer chaque voie seule.
4. Aligner le crossover le plus haut.
5. Descendre ensuite vers les crossovers inférieurs.
6. Ajuster les gains.
7. Corriger les défauts intrinsèques par PEQ de voie.
8. Revalider les crossovers après PEQ.
9. Construire la target globale avec un System EQ séparé.
10. Vérifier plusieurs positions.
11. Vérifier directivité, distorsion, headroom et limiteurs.
12. Exporter le preset REFERENCE.
13. Seulement ensuite comparer des architectures alternatives par simulation.

## 2. Règle de calage

Pour deux voies A et B :
- mesurer A solo,
- mesurer B solo,
- mesurer A+B en polarité normale,
- mesurer A+B avec une seule voie inversée,
- comparer niveau individuel, réponse complexe, phase relative, timing, SUM et REV.

Ne jamais choisir un délai ou une polarité à partir d'un seul point de fréquence.

Chercher un compromis sur toute la zone de recouvrement :
- bonne sommation,
- faible écart de phase,
- pentes de phase compatibles,
- reverse-null large,
- stabilité quand le micro bouge.

## 3. Crossover électrique vs acoustique

Le crossover électrique n'est qu'un point de départ.

La réponse acoustique finale dépend de :
- réponse naturelle du HP,
- pavillon/charge,
- PEQ,
- filtre électrique,
- délai,
- polarité,
- position,
- pièce.

Le LPF et le HPF de deux voies n'ont pas besoin d'avoir exactement la même fréquence électrique si leur somme acoustique est meilleure.

## 4. Delays

À 48 kHz :
- 1 sample = 20.833 µs.

Un délai τ produit :
Δφ(f) = -360 × f × τ

Distinguer :
- délai relatif interne à une tête,
- délai commun d'un groupe,
- délai d'installation lié aux positions physiques.

Quand un groupe déjà aligné doit être déplacé temporellement, appliquer le même offset à toutes ses voies pour préserver son calage interne.

## 5. EQ

### PEQ de voie
Pour :
- réponse intrinsèque d'un HP/pavillon/caisson,
- bosse stable à plusieurs positions,
- correction portable entre installations.

### System/Input EQ
Pour :
- target globale,
- room curve,
- correction d'installation,
- balance tonale.

Le System EQ doit idéalement être après le mixer commun et avant les traitements de voies, afin que musique et source REW traversent le même EQ.

## 6. Nulls de pièce

Ne pas booster un creux :
- étroit,
- fortement dépendant de la position,
- associé à une annulation,
- variable de plusieurs dB avec ±20 cm.

Un boost important dans un null spatial augmente surtout l'excursion et la puissance dissipée.

## 7. Contrôle qualité des mesures

Une mesure est suspecte si :
- une voie très faible provoque une énorme variation de somme,
- un HIGH solo ressemble au MID,
- un solo ressemble au système complet,
- le timing loopback saute sans déplacement micro,
- une voie change de plusieurs dB après un restart DSP,
- SUM/REV ne permettent pas de reconstruire une réponse cohérente,
- clipping ou bruit numérique apparaît.

Dans ce cas :
- identifier la mesure suspecte,
- ne pas l'interpréter,
- refaire uniquement la mesure nécessaire.

## 8. Phase avancée

Analyser ensemble :
- impulse response,
- phase wrapped,
- phase unwrapped,
- excess phase,
- group delay,
- phase relative,
- réponse complexe,
- SUM/REV.

Le reverse-null est une validation, pas l'unique critère.

## 9. Multi-position

Pour une calibration d'écoute :
- Centre
- +20 cm gauche
- +20 cm droite
- éventuellement avant/arrière.

Les PEQ de voie ne doivent pas être décidés uniquement à partir d'une position de pièce si une mesure quasi-anéchoïque est disponible ou réalisable.

## 10. Speaker preset vs room calibration

### Speaker / Stack preset
À établir idéalement dehors, en grande salle, ou avec gating propre :
- polarités,
- crossovers,
- delays internes,
- PEQ de voie,
- directivité,
- distorsion,
- limiteurs.

### Deployment / Room calibration
Pour la géométrie réelle :
- positions,
- delays inter-sources,
- gain,
- System EQ,
- target,
- spatial average.

## 11. Directivité

Pour un vrai choix d'architecture, mesurer :
- 0°
- ±10°
- ±20°
- ±30°
au minimum sur les raccords MID/HIGH et KICK/MID.

Une solution légèrement moins plate on-axis mais plus homogène hors axe est souvent préférable.

## 12. Distorsion et headroom

Tester plusieurs niveaux sûrs.

Pénaliser une architecture si elle :
- fait travailler une compression trop bas,
- pousse un kick trop haut,
- augmente la THD,
- réduit fortement le headroom,
- exige des boosts importants,
- déclenche les limiteurs prématurément.

## 13. Limiteurs

Le preset n'est pas final tant que les protections ne sont pas validées.

Documenter :
- gain ampli,
- sensibilité,
- impédance,
- puissance admissible,
- tension maximale cible,
- peak limiter,
- RMS/thermal limiter,
- excursion si disponible.

## 14. Fractional delay et FIR

CamillaDSP peut affiner le délai sous-sample.

N'utiliser le fractional delay qu'après avoir trouvé la bonne branche temporelle.

Le FIR peut être testé ensuite, mais seulement si :
- la géométrie est figée,
- l'IIR est déjà optimisé,
- le bénéfice est mesurable,
- la latence et le pré-ringing restent acceptables.

## 15. Architecture optimization

À partir de réponses complexes brutes, simuler :
- fréquences XO,
- pentes,
- filtres asymétriques,
- gains,
- polarités,
- delays,
- PEQ,
- éventuellement FIR.

Scorer chaque candidat sur :
- erreur target,
- sommation,
- tracking de phase,
- reverse-null,
- stabilité spatiale,
- directivité,
- THD,
- headroom,
- quantité d'EQ,
- group delay.

Ne valider physiquement que les meilleurs candidats.

## 16. Target E-Stack REFERENCE

Point de départ :
- 40–80 Hz : +4 dB
- 100 Hz : +3.5 dB
- 200 Hz : +2 dB
- 300 Hz : +1 dB
- 500 Hz : +0.5 dB
- 1 kHz : 0 dB
- 2 kHz : -0.5 dB
- 4 kHz : -1 dB
- 8 kHz : -2 dB
- 16 kHz : -3 dB

La target finale reste à valider par mesure et écoute niveau-matched.

## 17. Format de réponse attendu

Quand un `.mdat` est fourni :
1. dire si les mesures sont cohérentes,
2. identifier les sweeps suspects,
3. donner le diagnostic,
4. donner uniquement les prochaines mesures nécessaires,
5. écrire les valeurs absolues Camilla,
6. préciser ON / MUTE / NORMAL / INVERTED,
7. rappeler l'état normal à remettre après un test REV,
8. éviter les séries redondantes,
9. distinguer réglage de test et réglage final,
10. ne jamais masquer une incertitude.

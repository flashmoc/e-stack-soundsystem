# E-Stack — Missing Data / To Verify

Ce fichier liste ce qui manque encore pour qu'une nouvelle conversation ou un autre compte puisse reconstruire et poursuivre le projet sans aucune information extérieure.

## CRITICAL — requis pour reconstruction DSP exacte

- [ ] Ajouter le **YAML CamillaDSP réellement chargé** sur la Raspberry dans `camilladsp/reference/`.
- [ ] Capturer et documenter le **delay absolu SUB**.
- [ ] Capturer et documenter le **delay absolu KICK**.
- [ ] Documenter tous les **limiteurs / hard limits / protections** réellement actifs, avec seuils et paramètres complets.
- [ ] Vérifier et documenter l'ordre exact de tous les blocs de la pipeline CamillaDSP.
- [ ] Déplacer ou confirmer le placement du **System EQ 162 Hz** après `estack_preview`, puis sauvegarder le YAML correspondant.

## HIGH — requis pour reprise technique fiable

- [ ] Sauvegarder les paramètres complets des amplificateurs utiles au calage/protection : gain/sensibilité réellement utilisée, positions de potentiomètres si pertinentes, impédances des charges.
- [ ] Documenter les modèles exacts de tous les transducteurs/caissons et leur affectation par voie.
- [ ] Documenter les paramètres complets REW utilisés pour les campagnes de référence : sweep range, level, length, timing reference, calibration mic utilisée ou non.
- [ ] Ajouter un compte-rendu de la dernière validation SUM/REV de chaque crossover avec les noms de `.mdat` correspondants.
- [ ] Ajouter les courbes finales magnitude/phase/group delay quand la calibration REFERENCE sera terminée.

## MEDIUM — requis pour audit / optimisation avancée

- [ ] Ajouter mesures de directivité 0° / ±10° / ±20° / ±30°.
- [ ] Ajouter mesures de distorsion à plusieurs niveaux.
- [ ] Ajouter validation headroom / compression thermique.
- [ ] Ajouter validation des limiteurs par tension/puissance.
- [ ] Créer le preset `ARCHITECTURE_RAW` pour les futures simulations de crossover.
- [ ] Versionner les scripts de simulation et de scoring.

## État actuel connu

Le repo contient déjà :
- mapping sorties ;
- source REW IN4 ;
- gains actuels ;
- polarités actuelles ;
- delays MID/HIGH ;
- crossovers ;
- PEQ MID/HIGH ;
- System EQ actuellement observé ;
- protocole de mesure ;
- méthode de calage ;
- architecture logique du signal.

## Règle

Tant qu'un élément critique ci-dessus n'est pas rempli, tout assistant doit le signaler explicitement avant de prétendre restaurer ou reproduire le système à l'identique.

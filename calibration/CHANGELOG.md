# Changelog

## 2026-10-11 — audit documentaire (sans modification DSP)

- Synchronisation **octet pour octet** de toute la documentation Markdown de `flashmoc/e-stack-dsp` branche `main` au commit `642ede541e282ce9329390698bdbad5075577808` dans `docs/camillanode/`, avec provenance par blob dans `SOURCE.md`. Les anciennes instructions de déploiement `camillaNode-EStack` ne décrivent plus le logiciel produit.
- Ajout de `docs/estack-dsp-software-status.md` pour distinguer code source, version réellement déployée et état DSP/acoustique. La fonction d'import JSON des System Presets est signalée comme **branche locale non fusionnée**, pas comme fonction disponible sur `main`.
- Correction du protocole et du compte rendu historiques : la campagne du 30 septembre vise désormais `measurementInput: 3` dans son JSON ; son texte indiquait encore IN5. Les plans des 30 septembre et 7 octobre restent historiques et ne sont pas des preuves d'exécution.
- Les délais SUB/KICK et paramètres de protection déjà transcrits ne sont plus présentés comme inconnus ; restent manquants le JSON complet, le YAML de démarrage et la vérification physique. Les références du 10 octobre sont explicitement **datées**, non garanties live le 11 octobre.
- Clarification : dans le code actuel, GEQ/PEQ d'entrée actifs sont **pré-mixer** ; les déplacer après le mixer reste une proposition non implémentée. Aucune valeur audio, campagne JSON ou configuration Raspberry n'a été modifiée par cet audit.

## 2026-10-10

Locked calibration baseline superseding earlier same-day exports:
- authoritative live export: `2026-10-10T18:58:49.858Z`;
- title: `Stereo-LR-balanced-L-PAD`;
- config revision: `3b3d5f8e04576343db5a63b3a549f19dd92db640ee3955145d99aaed9e16631f`;
- associated acoustic reference supplied by user: `oct. 10 20_57_36.mdat`;
- MASTER -9.0 dB;
- SUB -7.3 dB;
- KICK -18.4 dB, inverted;
- MID L/R 0.0 dB;
- HIGH L/R -4.0 dB;
- delays: SUB 0.000 ms, KICK 1.300 ms, MID 2.760 ms, HIGH 2.720 ms;
- per-way PEQ and protection topology retained as documented;
- Global GEQ and Global PEQ state disabled;
- `CURRENT_REFERENCE.md`, `ESTACK_CURRENT_STATE.md`, `REFERENCE_PRESET_BACKUP.md` updated;
- six-solo level-match batch pinned to this config revision.

Measurement Batch documentation sync (no DSP/audio preset changes):
- synchronized `docs/camillanode/measurement-batch.md` with the dual-mode behavior verified in `flashmoc/e-stack-dsp`;
- recorded **Measure current system** using physical **IN3**, new live capture each run, mixer source at 0 dB, preserved output gains/mutes, input processing and Loudness;
- recorded **imported calibration JSON** as a single baseline for multiple steps, relative negative gain offsets, selected ways unmuted, Loudness/Input Trim forced off, optional measurement input (historical E-Stack campaign path IN5);
- documented the −60 dB Master transition, actual-DSP diagnostics, automatic restore and the difference between an output gain of −60 dB and true mute;
- corrected current REW routing: **CamillaDSP zero-based IN2/channel 2 = physical IN3**;
- corrected all active project Measurement Batch JSONs to **`measurementInput: 3`**;
- the older physical IN5 / logical IN4 campaign note is superseded.

## 2026-09-08

Création de la structure projet :
- séparation méthode / état / protocole / backup,
- intégration des pratiques de calage multi-voies,
- ajout directivité, distorsion, headroom, limiteurs,
- séparation Speaker Preset / Room Calibration,
- intégration du routing REW IN4,
- intégration des réglages E-Stack actuels,
- signalement explicite des delays SUB/KICK encore à sauvegarder.

Centralisation documentaire CamillaNode :
- miroir de toute la documentation technique de `flashmoc/camillaNode-EStack` branche `feature/estack-dsp-product` dans `docs/camillanode/`,
- ajout du README repo et du guide `AGENTS.md`,
- ajout des contrats runtime/API, du modèle de sécurité DSP, de la persistence, du déploiement Raspberry, de l’architecture frontend et de la documentation Control,
- ajout de la documentation complète `Measurement Batch`,
- copie des exemples JSON Measurement Batch dans `measurements/batch-examples/`,
- ajout de `docs/camillanode/SOURCE.md` avec provenance, SHAs source et règle de resynchronisation,
- ajout à cette date de la différence locale : REW sur **physical IN5**, donc `measurementInput: 5` pour les batchs de septembre (**note historique, remplacée depuis par IN3**),
- mise à jour de `START_HERE.md`, `README.md` et `measurements/README.md` pour qu’un nouvel assistant puisse reprendre depuis ce repo seul.

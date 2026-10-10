# Changelog

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
- physical REW cabling remains a hardware fact to verify before campaigns.

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
- ajout explicite de la différence locale : système actuel REW sur **physical IN5**, donc `measurementInput: 5` pour les nouveaux batchs,
- mise à jour de `START_HERE.md`, `README.md` et `measurements/README.md` pour qu’un nouvel assistant puisse reprendre depuis ce repo seul.

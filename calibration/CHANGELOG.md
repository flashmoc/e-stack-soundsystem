# Changelog

## 2026-10-10

Measurement Batch documentation sync (no DSP/audio preset changes):
- synchronized `docs/camillanode/measurement-batch.md` with the dual-mode behavior verified in `flashmoc/e-stack-dsp`;
- recorded **Measure current system** using physical **IN3**, new live capture each run, mixer source at 0 dB, preserved output gains/mutes, input processing and Loudness;
- recorded **imported calibration JSON** as a single baseline for multiple steps, relative negative gain offsets, selected ways unmuted, Loudness/Input Trim forced off, optional measurement input (historical E-Stack campaign path IN5);
- documented the −60 dB Master transition, actual-DSP diagnostics, automatic restore and the difference between an output gain of −60 dB and true mute;
- flagged physical REW cabling IN3 versus historical IN5 for verification; updated central protocol, reference notes, system architecture and documentation provenance.

Live baseline sync from user export `Stereo-LR-balanced-L-PAD`:
- MASTER -9.0 dB;
- SUB -7.3 dB;
- KICK -18.4 dB, inverted;
- MID L -0.6 dB / MID R +0.6 dB;
- HIGH L -3.5 dB / HIGH R -1.8 dB;
- absolute delays captured: SUB 0.000 ms, KICK 1.300 ms, MID 2.760 ms, HIGH 2.720 ms;
- current Global GEQ and Global PEQ state recorded as disabled;
- current protection thresholds verified from the live export;
- `CURRENT_REFERENCE.md`, `ESTACK_CURRENT_STATE.md` and `REFERENCE_PRESET_BACKUP.md` updated to the live working baseline;
- six-solo level-match batch corrected so it no longer tries to disable a missing `ESTACK_LOUDNESS` filter.

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

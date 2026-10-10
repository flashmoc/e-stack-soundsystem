# E-Stack SoundSystem

Référentiel technique central du projet **E-Stack SoundSystem** : calibration REW/CamillaDSP, état courant du système, sauvegarde du preset de référence, protocoles de mesure, documentation CamillaNode et futures simulations d’architecture.

## Source de vérité

- `START_HERE.md` : ordre de lecture obligatoire pour toute nouvelle conversation / nouvel assistant.
- `CURRENT_REFERENCE.md` : état validé à consulter en premier.
- `calibration/SKILL.md` : méthode de calage et règles d’ingénierie.
- `calibration/ESTACK_CURRENT_STATE.md` : état de travail courant.
- `calibration/MEASUREMENT_PROTOCOL.md` : protocole pratique REW/Camilla, avec choix entre campagne JSON et mesure du système actuel (**IN3**).
- `calibration/REFERENCE_PRESET_BACKUP.md` : snapshot de reconstruction du preset.
- `calibration/CHANGELOG.md` : historique des évolutions.
- `camilladsp/` : configurations DSP de référence et de mesure.
- `measurements/` : index, exemples de Measurement Batch et comptes-rendus des campagnes de mesures.
- `simulations/` : optimisation numérique des crossovers, phase et directivité.
- `docs/system-architecture.md` : chaîne de signal du système réel.
- `docs/limiters-and-amplifiers.md` : gains ampli, limites HP et protections connues.
- `docs/camillanode/` : documentation miroir, historiquement issue de `flashmoc/camillaNode-EStack` ; la référence **Measurement Batch** a été resynchronisée depuis l'implémentation actuelle `flashmoc/e-stack-dsp` (provenance dans `SOURCE.md`).

## Documentation CamillaNode centralisée

Le repo CamillaNode reste la source d’implémentation du logiciel, mais sa documentation nécessaire à l’exploitation du système est recopiée ici pour qu’un nouvel assistant puisse travailler depuis **un seul repo**.

Commencer par :

1. `docs/camillanode/README.md`
2. `docs/camillanode/runtime-contracts.md`
3. `docs/camillanode/dsp-safety.md`
4. `docs/camillanode/measurement-batch.md`
5. `docs/camillanode/SOURCE.md`

Les exemples JSON du runner sont dans `measurements/batch-examples/`.

## Règle de versioning

La branche `main` doit représenter uniquement l’état **validé** ou explicitement documenté comme état de travail courant. Les essais d’architecture importants doivent être isolés dans des branches dédiées avant fusion.

Les fichiers sous `docs/camillanode/` sont des miroirs à provenance tracée : toute resynchronisation doit mettre à jour `docs/camillanode/SOURCE.md`. **Le câblage REW actuel est physical IN3 dans les DEUX modes.** `Measure current system` route IN3 automatiquement ; les campagnes JSON E-Stack utilisent `defaults.measurementInput: 3` pour cette même prise. L'ancien IN5 est obsolète. Les deux modes diffèrent dans la capture, les gains, les mutes, Loudness et Input Trim.

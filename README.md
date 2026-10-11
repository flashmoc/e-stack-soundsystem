# E-Stack SoundSystem

Référentiel technique central du projet **E-Stack SoundSystem** : calibration REW/CamillaDSP, référence datée du système, campagnes de mesure et documentation du logiciel E-Stack DSP. Le code de l'application reste dans [flashmoc/e-stack-dsp](https://github.com/flashmoc/e-stack-dsp).

**À lire avant de reprendre un réglage :** les gains et filtres de `CURRENT_REFERENCE.md` décrivent le dernier export documenté ici (10 octobre 2026), pas une lecture en direct du Raspberry. Le JSON complet de cet export et les fichiers REW `.mdat` cités ne sont pas versionnés ici. Vérifier un nouvel export live avant d'appliquer ou de calculer des changements à partir de ces valeurs.

## Source de vérité

- `START_HERE.md` : ordre de lecture obligatoire pour toute nouvelle conversation / nouvel assistant.
- `CURRENT_REFERENCE.md` : dernière référence de travail datée, à consulter en premier.
- `calibration/SKILL.md` : méthode de calage et règles d’ingénierie.
- `calibration/ESTACK_CURRENT_STATE.md` : état de travail courant.
- `calibration/MEASUREMENT_PROTOCOL.md` : protocole pratique REW/Camilla, avec choix entre campagne JSON et mesure du système actuel (**IN3**).
- `calibration/REFERENCE_PRESET_BACKUP.md` : transcription des paramètres connus, **pas** un export JSON/YAML restaurable.
- `calibration/CHANGELOG.md` : historique des évolutions.
- `camilladsp/` : configurations DSP de référence et de mesure.
- `measurements/` : index, exemples de Measurement Batch et comptes-rendus des campagnes de mesures.
- `simulations/` : optimisation numérique des crossovers, phase et directivité.
- `docs/system-architecture.md` : chaîne de signal du système réel.
- `docs/limiters-and-amplifiers.md` : gains ampli, limites HP et protections connues.
- `docs/camillanode/` : miroir documentaire du commit logiciel indiqué dans `docs/camillanode/SOURCE.md`.
- `docs/estack-dsp-software-status.md` : état logiciel, déploiement et fonctions à distinguer de la calibration.

## Documentation E-Stack DSP centralisée

`flashmoc/e-stack-dsp` est la source d'implémentation. Ce dépôt recopie sa documentation à un commit précis pour qu'un nouvel assistant puisse l'étudier sans confondre documentation de code et état physique du système.

Commencer par :

1. `docs/camillanode/README.md`
2. `docs/camillanode/runtime-contracts.md`
3. `docs/camillanode/dsp-safety.md`
4. `docs/camillanode/measurement-batch.md`
5. `docs/camillanode/SOURCE.md`

Les exemples JSON du runner sont dans `measurements/batch-examples/`. Les trois campagnes propres à l'installation sont dans `measurements/batches/` ; elles ne doivent pas être confondues avec ces exemples.

## Règle de versioning

La branche `main` doit représenter uniquement l’état **validé** ou explicitement documenté comme état de travail courant. Les essais d’architecture importants doivent être isolés dans des branches dédiées avant fusion.

Les fichiers sous `docs/camillanode/` sont des miroirs à provenance tracée : toute resynchronisation doit mettre à jour `docs/camillanode/SOURCE.md`. Le câblage REW **rapporté pour l'installation** est physical IN3 dans les deux modes : `Measure current system` route IN3 automatiquement et les campagnes JSON E-Stack utilisent `defaults.measurementInput: 3`. L'ancien IN5 est obsolète dans les campagnes actuelles ; sa mention dans un historique reste datée. Un test matériel reste nécessaire pour démontrer la correspondance prise/ALSA.

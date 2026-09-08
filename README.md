# E-Stack SoundSystem

Référentiel technique du projet **E-Stack SoundSystem** : calibration REW/CamillaDSP, état courant du système, sauvegarde du preset de référence, protocoles de mesure et futures simulations d’architecture.

## Source de vérité

- `CURRENT_REFERENCE.md` : état validé à consulter en premier.
- `calibration/SKILL.md` : méthode de calage et règles d’ingénierie.
- `calibration/ESTACK_CURRENT_STATE.md` : état de travail courant.
- `calibration/MEASUREMENT_PROTOCOL.md` : protocole pratique REW/Camilla.
- `calibration/REFERENCE_PRESET_BACKUP.md` : snapshot de reconstruction du preset.
- `calibration/CHANGELOG.md` : historique des évolutions.
- `camilladsp/` : configurations DSP de référence et de mesure.
- `measurements/` : index et comptes-rendus des campagnes de mesures.
- `simulations/` : optimisation numérique des crossovers, phase et directivité.
- `docs/` : architecture système et documentation technique.

## Règle de versioning

La branche `main` doit représenter uniquement l’état **validé** ou explicitement documenté comme état de travail courant. Les essais d’architecture importants doivent être isolés dans des branches dédiées avant fusion.

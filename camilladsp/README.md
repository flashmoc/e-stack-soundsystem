# CamillaDSP

Ce dossier **ne contient actuellement aucun JSON live ni YAML matériel** réellement utilisé : ses sous-dossiers sont une structure prévue. Les valeurs de `../CURRENT_REFERENCE.md` sont une transcription partielle de l'export daté du 10 octobre 2026, pas une configuration à charger directement dans CamillaDSP.

Structure prévue :

- `reference/` : presets validés.
- `measurement/` : presets dédiés aux mesures/architecture raw.
- `archive/` : anciennes versions conservées pour traçabilité.

Règle : ne jamais remplacer un preset de référence validé sans conserver un historique Git clair.
Avant d'ajouter un export, noter sa date, sa révision, la machine d'origine et le statut « live », « saved preset » ou « hardware YAML ». L'export sauvegardé du système contient traitement + Master, pas les périphériques ou mixers ; le YAML est nécessaire pour restaurer la couche matérielle. Vérifier les noms de périphériques et chemins privés avant publication.

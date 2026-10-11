# E-Stack — Start Here

Ce dépôt doit permettre à un nouvel assistant, une nouvelle conversation ou un autre compte de reprendre le projet sans dépendre de l'historique de chat.

## Ordre de lecture obligatoire

1. `CURRENT_REFERENCE.md` — dernière référence de travail datée ; vérifier un export plus récent avant tout changement.
2. `calibration/SKILL.md` — méthode et règles de calage.
3. `calibration/ESTACK_CURRENT_STATE.md` — état détaillé en cours.
4. `calibration/REFERENCE_PRESET_BACKUP.md` — transcription de secours des paramètres connus, non restaurable telle quelle.
5. `docs/system-architecture.md` — chaîne de signal et routing du système réel.
6. `calibration/MEASUREMENT_PROTOCOL.md` — protocole REW/Camilla.
7. `docs/estack-dsp-software-status.md` — frontière entre code, déploiement et validation physique.
8. `docs/camillanode/README.md` — documentation E-Stack DSP à lire avant toute action sur le frontend, les API ou les workflows serveur.
9. `docs/camillanode/runtime-contracts.md` — contrats WebSocket/HTTP à préserver.
10. `docs/camillanode/dsp-safety.md` — invariants de sécurité et transactions DSP.
11. `docs/camillanode/measurement-batch.md` — schéma JSON Measurement Batch et comportement du runner.
12. `docs/camillanode/SOURCE.md` — provenance du miroir logiciel.
13. `MISSING_DATA.md` — éléments encore non documentés ou non validés.
14. `calibration/CHANGELOG.md` — historique des évolutions.

## Règles pour tout nouvel assistant

- Considérer ce repo comme la source de vérité **des décisions de calibration datées** ; le code et les contrats logiciels sont dans `flashmoc/e-stack-dsp`, et l'état DSP live se vérifie sur le Raspberry.
- Ne jamais inventer une valeur absente du repo.
- Distinguer clairement : `VALIDATED`, `WORKING`, `TO VERIFY`, `MISSING`.
- Avant toute recommandation de changement, lire `CURRENT_REFERENCE.md` et `MISSING_DATA.md`.
- Avant toute modification ou recommandation concernant CamillaNode, lire `docs/camillanode/README.md`, `runtime-contracts.md` et `dsp-safety.md`.
- Avant de générer un JSON Measurement Batch, lire `docs/camillanode/measurement-batch.md` et `docs/camillanode/SOURCE.md`.
- **Entrée REW rapportée par l'utilisateur : physical IN3, dans les DEUX modes.** `Measure current system` / `MEASURE NOW` sélectionne le canal CamillaDSP 2 (index zéro). Pour chaque campagne JSON importée E-Stack, définir `defaults.measurementInput: 3` pour viser cette entrée. Ne pas reprendre l'ancienne note IN5. Le 0 dB est le gain de source du mixer, pas le gain des sorties. Vérifier physiquement la prise et le mapping ALSA avant une nouvelle campagne.
- Quand un réglage est validé, mettre à jour `CURRENT_REFERENCE.md`, `ESTACK_CURRENT_STATE.md`, `REFERENCE_PRESET_BACKUP.md` et le `CHANGELOG.md`.
- Ne pas modifier le preset de référence sans conserver l'ancien état dans Git.
- Les mesures `.mdat` envoyées dans le chat servent à l'analyse ; leurs conclusions validées doivent être résumées dans le repo.
- Le nouvel export live doit être comparé à la référence datée ; le YAML CamillaDSP réellement chargé, lorsqu'il sera ajouté, documentera le démarrage matériel mais ne remplace pas à lui seul les changements live non sauvegardés.
- Les fichiers sous `docs/camillanode/` sont des copies du commit **`flashmoc/e-stack-dsp`** indiqué dans `docs/camillanode/SOURCE.md`. Ne pas les modifier silencieusement pour décrire le matériel local : utiliser `docs/system-architecture.md` et les documents de calibration.

## Objectif de reproductibilité

Le dépôt est considéré autonome seulement lorsqu'il contient :

- le YAML CamillaDSP de démarrage réellement utilisé et un export live JSON complet daté ;
- le mapping matériel complet ;
- gains, delays, polarités, XO, PEQ ;
- System EQ ;
- protections/limiteurs ;
- paramètres matériel/amplificateurs indispensables ;
- protocole REW ;
- documentation CamillaNode/API/Measurement Batch nécessaire à l'exploitation ;
- dernière validation de phase/SUM/REV ;
- état des éléments encore à vérifier.

Tant que `MISSING_DATA.md` contient des éléments critiques, ne pas prétendre que le système peut être reconstruit à 100 % depuis ce repo seul.

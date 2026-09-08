# E-Stack — Start Here

Ce dépôt doit permettre à un nouvel assistant, une nouvelle conversation ou un autre compte de reprendre le projet sans dépendre de l'historique de chat.

## Ordre de lecture obligatoire

1. `CURRENT_REFERENCE.md` — état validé / état de travail actuel.
2. `calibration/SKILL.md` — méthode et règles de calage.
3. `calibration/ESTACK_CURRENT_STATE.md` — état détaillé en cours.
4. `calibration/REFERENCE_PRESET_BACKUP.md` — snapshot reconstructible du preset.
5. `docs/system-architecture.md` — chaîne de signal et routing du système réel.
6. `calibration/MEASUREMENT_PROTOCOL.md` — protocole REW/Camilla.
7. `docs/camillanode/README.md` — documentation CamillaNode/E-Stack DSP à lire avant toute action sur le frontend, les API ou les workflows serveur.
8. `docs/camillanode/runtime-contracts.md` — contrats WebSocket/HTTP à préserver.
9. `docs/camillanode/dsp-safety.md` — invariants de sécurité et transactions DSP.
10. `docs/camillanode/measurement-batch.md` — schéma JSON Measurement Batch et comportement du runner.
11. `docs/camillanode/SOURCE.md` — provenance du miroir et différences locales E-Stack.
12. `MISSING_DATA.md` — éléments encore non documentés ou non validés.
13. `calibration/CHANGELOG.md` — historique des évolutions.

## Règles pour tout nouvel assistant

- Considérer ce repo comme la source de vérité projet, pas l'historique de conversation.
- Ne jamais inventer une valeur absente du repo.
- Distinguer clairement : `VALIDATED`, `WORKING`, `TO VERIFY`, `MISSING`.
- Avant toute recommandation de changement, lire `CURRENT_REFERENCE.md` et `MISSING_DATA.md`.
- Avant toute modification ou recommandation concernant CamillaNode, lire `docs/camillanode/README.md`, `runtime-contracts.md` et `dsp-safety.md`.
- Avant de générer un JSON Measurement Batch, lire `docs/camillanode/measurement-batch.md` et `docs/camillanode/SOURCE.md`.
- Pour le système actuel, `measurementInput` est **5** tant que `docs/system-architecture.md` documente `physical IN5 → ALSA CH4 → Camilla logical IN4`. Ne pas recopier automatiquement le `4` des exemples historiques.
- Quand un réglage est validé, mettre à jour `CURRENT_REFERENCE.md`, `ESTACK_CURRENT_STATE.md`, `REFERENCE_PRESET_BACKUP.md` et le `CHANGELOG.md`.
- Ne pas modifier le preset de référence sans conserver l'ancien état dans Git.
- Les mesures `.mdat` envoyées dans le chat servent à l'analyse ; leurs conclusions validées doivent être résumées dans le repo.
- Le fichier YAML CamillaDSP réellement chargé sur la Raspberry, lorsqu'il sera ajouté, prime sur une transcription manuelle si les deux divergent.
- Les fichiers sous `docs/camillanode/` sont un miroir documentaire du repo `flashmoc/camillaNode-EStack`; les différences propres au système réel doivent être documentées séparément, pas modifiées silencieusement dans le miroir.

## Objectif de reproductibilité

Le dépôt est considéré autonome seulement lorsqu'il contient :

- le YAML CamillaDSP de référence réellement utilisé ;
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

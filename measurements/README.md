# Measurements

Index des campagnes REW, des JSON Measurement Batch et de leurs conclusions.

## Measurement Batch

La documentation de référence du runner est :

- `docs/camillanode/measurement-batch.md`
- `docs/camillanode/SOURCE.md`

Exemples génériques recopiés depuis le logiciel, **non adaptés automatiquement au câblage E-Stack** :

- `batch-examples/measurement-batch-kick-mid.example.json`
- `batch-examples/measurement-batch-smoke-test-v1.json`

**Deux modes distincts (2026-10-10) :**

- **Measure current system / MEASURE NOW :** n'utilise **pas** ces JSON ; il capture le DSP au clic, route **physical IN3** aux six destinations du mixer à 0 dB de gain source et garde les gains, MUTE, EQ, crossovers, Input Trim, Loudness, délais et protections de l'état capturé. Pour l'utiliser, brancher réellement la sortie REW sur **physical IN3** ; arrêter le générateur interne et maintenir le WiiM stable si Loudness est actif.
- **Campagne JSON importée :** `START BATCH` capture une fois la baseline, puis construit chaque étape à partir de cette même capture. Les voies choisies sont démûtées, les autres mutées ; `gainOffsetDb` est une **atténuation relative**. En version 3, `gainDb` permet un gain absolu borné et `inputEq` des candidats GEQ/PEQ d'entrée ; `ways.<voie>.peq` permet des candidats PEQ de sortie. Input Trim et Loudness sont forcés OFF et ne sont pas réglables par étape. `measurementInput` est le numéro **physique IN1–IN8** si une source de mesure dédiée est configurée.
- Les exemples génériques peuvent utiliser d'autres entrées (notamment IN4) : ne pas les lancer tels quels sur l'installation. **Le câblage rapporté** est physical IN3 = CamillaDSP zero-based IN2/channel 2 ; les trois JSON de campagne E-Stack utilisent **`measurementInput: 3`**. Le chemin IN5 est supersédé, mais le mapping prise/ALSA reste à vérifier physiquement.
- Les deux modes restaurent le DSP et le routage de référence à la fin/annulation, préservent les paramètres `devices`, et baissent temporairement Master à **au plus −60 dB** lors des changements de configuration.

Voir `docs/camillanode/measurement-batch.md` pour le détail et les diagnostics `/api/measurement-batch/effective`.

Pour préparer une campagne de comparaison EQ/gain, utiliser `version: 3` et définir explicitement les valeurs candidates dans chaque étape. Une valeur omise conserve celle de la baseline capturée ; les changements d'une étape ne s'additionnent pas à la suivante. `inputEq.geq.targets` contient les dix gains cibles du GEQ ; `inputEq.peq.bands` cible les slots PEQ globaux ; `ways.<voie>.peq` cible les slots PEQ de chaque sortie. Un candidat peut modifier l'état `enabled` et le type des PEQ. Le serveur borne le gain d'une voie à au plus +3 dB au-dessus de sa baseline et vérifie également la hausse de réponse **combinée** EQ d'entrée + EQ de sortie + gain de voie à 20 Hz–20 kHz. Il refuse les filtres partagés ou ambigus et préserve les protections, limiteurs, mixer hors routage temporaire et `devices`. Vérifier la version déployée du serveur et l'écran **ACTUAL DSP** avant le premier sweep ; l'import JSON seul ne prouve pas que la configuration candidate est appliquée. Les candidats ne sont pas enregistrés comme preset : appliquer ensuite manuellement un résultat validé dans les pages de tuning.

Les campagnes datées du 30 septembre et du 7 octobre sont des **plans historiques** préparés avec un preset Stereo antérieur. Leur JSON a été corrigé pour viser IN3, mais le reste du plan n'a pas été recalé sur la baseline du 10 octobre. Elles ne sont pas une preuve de mesures réellement exécutées. Vérifier le preset live, les gains, le Master et le câblage avant tout nouveau lancement. Le compte rendu du 10 octobre se rapporte à une mesure déjà fournie par l'utilisateur et à la baseline citée dans `CURRENT_REFERENCE.md`.

## Comptes-rendus de campagne

Pour chaque campagne, documenter au minimum :
- date,
- fichier `.mdat` associé,
- fichier JSON batch associé si utilisé,
- baseline/preset DSP,
- baseline ID Measurement Batch si disponible,
- position micro,
- sample rate,
- niveau sweep,
- routing,
- mesures contenues,
- anomalies éventuelles,
- conclusion,
- réglages validés ou rejetés.

Les `.mdat` sont la matière première ; les conclusions et paramètres validés doivent rester lisibles en Markdown/CSV pour pouvoir être relus rapidement depuis GitHub.

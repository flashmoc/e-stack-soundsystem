# Measurements

Index des campagnes REW, des JSON Measurement Batch et de leurs conclusions.

## Measurement Batch

La documentation de référence du runner est :

- `docs/camillanode/measurement-batch.md`
- `docs/camillanode/SOURCE.md`

Exemples copiés depuis CamillaNode :

- `batch-examples/measurement-batch-kick-mid.example.json`
- `batch-examples/measurement-batch-smoke-test-v1.json`

**Deux modes distincts (2026-10-10) :**

- **Measure current system / MEASURE NOW :** n'utilise **pas** ces JSON ; il capture le DSP au clic, route **physical IN3** aux six destinations du mixer à 0 dB de gain source et garde les gains, MUTE, EQ, crossovers, Input Trim, Loudness, délais et protections de l'état capturé. Pour l'utiliser, brancher réellement la sortie REW sur **physical IN3** ; arrêter le générateur interne et maintenir le WiiM stable si Loudness est actif.
- **Campagne JSON importée :** `START BATCH` capture une fois la baseline, puis applique des étapes relatives. Les voies choisies sont démûtées, les autres mutées ; `gainOffsetDb` est une **atténuation relative**. Input Trim et Loudness sont forcés OFF. `measurementInput` est le numéro **physique IN1–IN8** si une source de mesure dédiée est configurée.
- Les exemples historiques peuvent utiliser `measurementInput: 4`. Le dernier câblage des campagnes du projet est noté **physical IN5 → `measurementInput: 5`**. Vérifier le câblage actuel avant de réutiliser les JSON de `batches/`. **IN3 est fixe uniquement pour le mode état actuel.**
- Les deux modes restaurent le DSP et le routage de référence à la fin/annulation, préservent les paramètres `devices`, et baissent temporairement Master à **au plus −60 dB** lors des changements de configuration.

Voir `docs/camillanode/measurement-batch.md` pour le détail et les diagnostics `/api/measurement-batch/effective`.

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

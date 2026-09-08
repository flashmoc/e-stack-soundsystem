# Measurements

Index des campagnes REW, des JSON Measurement Batch et de leurs conclusions.

## Measurement Batch

La documentation de référence du runner est :

- `docs/camillanode/measurement-batch.md`
- `docs/camillanode/SOURCE.md`

Exemples copiés depuis CamillaNode :

- `batch-examples/measurement-batch-kick-mid.example.json`
- `batch-examples/measurement-batch-smoke-test-v1.json`

Attention : les exemples historiques peuvent utiliser `measurementInput: 4`. Pour le système E-Stack actuellement documenté, REW arrive sur **physical IN5**, donc les nouveaux batchs doivent utiliser `measurementInput: 5` tant que le routing n’a pas changé.

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

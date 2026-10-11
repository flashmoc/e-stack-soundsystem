# Source du miroir E-Stack DSP

Les fichiers de ce répertoire proviennent des documents de [flashmoc/e-stack-dsp](https://github.com/flashmoc/e-stack-dsp) au commit [`0fd2acf8eacf4abe3bfe337b020465f7e13ec7b8`](https://github.com/flashmoc/e-stack-dsp/tree/0fd2acf8eacf4abe3bfe337b020465f7e13ec7b8) (branche `main`, consultée le 2026-10-11). Ils décrivent le logiciel à ce commit, **pas** l'état acoustique actuel ni la version nécessairement installée sur le Raspberry. Tous sont copiés **octet pour octet**, sauf les liens relatifs corrigés dans `AGENTS.md` et `repository-README.md` pour fonctionner depuis ce répertoire. Le tableau conserve les empreintes des blobs **source**, avant ces corrections de liens.

L'ancien miroir provenait de `flashmoc/camillaNode-EStack` en septembre 2026. Cette provenance est historique et ne décrit plus les copies ci-dessous. Le logiciel produit est désormais le dépôt autonome `e-stack-dsp`. Pour modifier le comportement, changer ce dépôt source ; pour décrire le câblage, les mesures et la calibration E-Stack, modifier les documents propres à `e-stack-soundsystem`.

| Source | Copie ici | Blob Git source |
| --- | --- | --- |
| `docs/README.md` | `README.md` | `cff93224958a4b93d5add47e0cf47b75b33286b4` |
| `docs/architecture.md` | `architecture.md` | `a0fb0f19d92b04b0faa9a37e10ec7333ae91dd4b` |
| `docs/development.md` | `development.md` | `620ab1d0b1b27ccb43425aafbd360f8168cbd877` |
| `docs/dsp-safety.md` | `dsp-safety.md` | `290ff21e8a99f193ab68173fe0fdb577d5e025fa` |
| `docs/estack-dsp-architecture.md` | `estack-dsp-architecture.md` | `3f116069643e0e495ba260c01aa8b059b1fd22ba` |
| `docs/estack-dsp-product.md` | `estack-dsp-product.md` | `40323288103f717fff98636b7085c211d1aeafba` |
| `docs/input-dual-eq-delivery.md` | `input-dual-eq-delivery.md` | `49eb76ee527134d8c985fec91fa8f7ee58cafe03` |
| `docs/live-mock-audit.md` | `live-mock-audit.md` | `4f9e1c58216eb7a014ed158b913876ee8991dd7b` |
| `docs/measurement-batch.md` | `measurement-batch.md` | `e42c0607c4fb8a55273b27655f0afc2608d36ae1` |
| `docs/operational-ownership.md` | `operational-ownership.md` | `f2c29e4ce7582a49c3cce80c7d89f774bbbcc71e` |
| `docs/pages/advanced.md` | `pages/advanced.md` | `401e4ba173ab3aa1b9cdc32f15cbdd55c9be603a` |
| `docs/pages/connections.md` | `pages/connections.md` | `5cd59ca897c9cbf8662e09ff3b4c8c265b1da499` |
| `docs/pages/control.md` | `pages/control.md` | `ef1ad0c9d2650bf37e5ec54e1a0ba8eb3a46b2df` |
| `docs/pages/input-processing.md` | `pages/input-processing.md` | `5ebf00e381c49f99e07abcfa1e72395eda6e45d3` |
| `docs/pages/loudness.md` | `pages/loudness.md` | `374e4e0c04e162426b5847abeac43673106e371a` |
| `docs/pages/measurement-batch.md` | `pages/measurement-batch.md` | `d084a4b805eb4e94d9012ead3563553333bd551d` |
| `docs/pages/output-processing.md` | `pages/output-processing.md` | `91a0893b2c4a060e2b5639c4edabde12d55adbf1` |
| `docs/pages/preferences.md` | `pages/preferences.md` | `468dbf1353d65a038ed0b761ebf49746d8fbbf0a` |
| `docs/pages/signal-generator.md` | `pages/signal-generator.md` | `3a3e712ef9ebd8a276204ded7aea9096da605f97` |
| `docs/pages/system-presets.md` | `pages/system-presets.md` | `81e11cfabe0f1fac62d7e2a20a0f6f56ffeb1c61` |
| `docs/persistence.md` | `persistence.md` | `181daf233b5457864e54d7e7a2f197c6a638358a` |
| `docs/raspberry-rc1.md` | `raspberry-rc1.md` | `3c34f959b23a89d8b9f7bef86f27e7fea425125c` |
| `docs/raspberry.md` | `raspberry.md` | `d58abbeb993b72dfa52d611a7d21fdd70e16c6f1` |
| `docs/runtime-contracts.md` | `runtime-contracts.md` | `bbfba32c0c75bdf04b5c8c386f0161c505caec4a` |
| `docs/software-release-audit.md` | `software-release-audit.md` | `dcf196e5e299c29ddbd4deba5ad0e59652cebb0e` |
| `docs/standalone-runtime.md` | `standalone-runtime.md` | `e7e4450f34ed23d6c4cae28de2ab28b19fae1089` |
| `docs/ui-architecture.md` | `ui-architecture.md` | `25dec31e2e17d64e1f0f446a9e5268e48a917666` |
| `AGENTS.md` | `AGENTS.md` | `5bea3c9fdfdc754ebc3909f429d2ae2c1dd76276` |
| `README.md` | `repository-README.md` | `1402f1a43efe0efe523af9e213397f1f807d243f` |

## Règle de mise à jour

1. Choisir un commit précis de `flashmoc/e-stack-dsp` et recopier les documents sans modification locale silencieuse.
2. Actualiser ce commit et les empreintes de blobs ci-dessus.
3. Signaler séparément les fonctionnalités non fusionnées sur `main` et les différences entre code, déploiement Raspberry et validation physique.
4. Vérifier les liens Markdown internes et les exemples JSON après synchronisation.

La correspondance **IN3 physique ↔ canal CamillaDSP 2 (index zéro)** est une information de câblage rapportée pour l'installation E-Stack ; le code ne peut pas la prouver à lui seul. Les deux modes de Measurement Batch, leurs gains, leurs mutes et la restauration sont décrits dans [measurement-batch.md](measurement-batch.md). Les paramètres et résultats acoustiques datés restent dans les documents de calibration du présent dépôt.

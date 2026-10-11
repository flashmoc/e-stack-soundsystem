# E-Stack DSP — état logiciel et frontières de preuve

Référence documentaire : [flashmoc/e-stack-dsp](https://github.com/flashmoc/e-stack-dsp), branche `main`, commit `0fd2acf8eacf4abe3bfe337b020465f7e13ec7b8` (11 octobre 2026). Le miroir exact est dans `docs/camillanode/` ; son inventaire de blobs est dans [`SOURCE.md`](camillanode/SOURCE.md). Ce document résume ce **commit logiciel**, sans prétendre connaître le commit actuellement installé sur le Raspberry.

## Installation et architecture

- L'interface produit est `/estack-dsp/` dans l'application E-Stack DSP autonome, servie normalement sur le port 8080 ; l'ancienne interface CamillaNode n'est qu'une référence historique. Le service visé est `estack-dsp.service`, avec CamillaDSP comme moteur audio et les API de sécurité côté serveur. Voir [`standalone-runtime.md`](camillanode/standalone-runtime.md) et [`raspberry.md`](camillanode/raspberry.md).
- L'utilisateur a indiqué qu'E-Stack DSP est installé sur son Raspberry Pi 5. **Aucun inventaire live n'a été effectué lors de cette mise à jour documentaire** : ne pas déduire du commit source le commit déployé, le YAML actif, le preset chargé ou l'état du câblage.
- Le matériel déclaré est RASPIAUDIO/HiFiBerry DAC8xADC8x, 8 entrées et 8 sorties à 48 kHz S32_LE. Les voies **logiques** E-Stack sont six : SUB, KICK, MID L/R, HIGH L/R. Les deux autres canaux hardware existent sans voie logique E-Stack ; la correspondance des prises physiques doit être testée sur le Raspberry.

## Fonctions documentées dans `main`

| Surface | Comportement utile | Document source |
| --- | --- | --- |
| Control | Master, mute, gains et mutes par voie ; liens MID et HIGH indépendants ; Input Trim et calcul de headroom lié aux niveaux observés | [`control.md`](camillanode/pages/control.md) |
| Input Processing | GEQ et PEQ d'entrée indépendants, import/presets adaptés à l'éditeur visible, état ON/OFF enregistré dans la configuration DSP | [`input-processing.md`](camillanode/pages/input-processing.md) |
| Output Processing | EQ, crossover, gain, délai, phase, polarité et mute ; lien MID/HIGH pour les réglages de paire, PEQ par voie avec copie explicite de l'autre côté | [`output-processing.md`](camillanode/pages/output-processing.md) |
| Loudness | Presets, état ON/OFF explicite, courbes maximum et courante lorsque WiiM transmet une télémétrie fraîche ; niveau WiiM en pourcentage, pas un niveau dBFS mesuré | [`loudness.md`](camillanode/pages/loudness.md) |
| Measurement Batch | Campagne JSON relative à une baseline capturée une fois **ou** mesure ponctuelle du système à l'instant T via IN3 ; v3 permet des candidats temporaires GEQ/PEQ d'entrée et gain/PEQ des voies, sous limites serveur ; état DSP appliqué vérifiable, restauration en fin/annulation | [`measurement-batch.md`](camillanode/measurement-batch.md) |
| System Presets | Capture et rappel du traitement + Master, choix de démarrage, import et export JSON live ou sauvegardé ; un preset ne remplace ni `devices` ni `mixers` | [`system-presets.md`](camillanode/pages/system-presets.md) |
| Preferences | Présentation locale, page d'accueil, diagnostics Connections, changement live du chunksize avec estimation `chunksize / samplerate` et validation serveur | [`preferences.md`](camillanode/pages/preferences.md) |

L'import JSON de System Presets et les candidats Measurement Batch v3 sont présents dans le **code source** du commit cité. Leur disponibilité sur le Raspberry dépend de la version effectivement déployée et doit être vérifiée avant utilisation. L'import crée un nouveau preset de traitement + Master sans l'appliquer ni modifier le hardware ; une campagne v3 n'enregistre pas ses candidats comme preset.

## Trois états à ne pas confondre

1. **Code/source :** contrat attesté par un commit, tests logiciels et miroir documentaire.
2. **Déploiement :** version réellement exécutée par `estack-dsp.service` sur le Raspberry ; à confirmer avec le commit local et `/api/runtime`.
3. **Audio :** configuration CamillaDSP live, choix de démarrage, câblage des prises, gains d'amplificateur et résultat REW ; à confirmer par export live et essais matériels.

Le statut « hardware acceptance pending » de certains documents du code signifie que leurs tests logiciels ne valident pas à eux seuls le dispositif physique. Ce n'est ni une preuve d'absence d'installation ni une preuve de calibration finale. `CURRENT_REFERENCE.md` reste la dernière **référence de travail datée** conservée ici ; voir `MISSING_DATA.md` pour les pièces nécessaires à une restauration exacte.

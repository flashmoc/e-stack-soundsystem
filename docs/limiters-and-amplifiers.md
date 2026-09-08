# E-Stack — Amplificateurs et limiteurs

Source : tableau utilisateur daté du **30/08/2026**, recopié depuis la note de calibration. Les valeurs ci-dessous sont considérées comme la référence connue tant qu'une mesure ou la configuration CamillaDSP réelle ne les remplace pas.

## Amplificateurs, gains mesurés et limites HP

| Voie | Ampli | Réglage ampli | Gain mesuré | Limite HP retenue | Équiv. puissance | Hard Limiter Camilla | Compresseur |
|---|---|---|---:|---:|---:|---:|---:|
| SUB | t.amp E1200 | Potard max | 40.1 dB | 50.0 Vrms | 625 W @ 4 Ω total | -12.6 dBFS | -13.6 dB |
| KICK | t.amp E1200 | Potard max | 40.1 dB | 34.6 Vrms | 300 W @ 4 Ω | -15.8 dBFS | -16.8 dB |
| MID L | t.amp E400 | 26 dB, potard max | 26.7 dB | 25.3 Vrms | 80 W @ 8 Ω | -5.1 dBFS | -6.1 dB |
| MID R | t.amp E400 | 26 dB, potard max | 26.7 dB | 25.3 Vrms | 80 W @ 8 Ω | -5.1 dBFS | -6.1 dB |
| HIGH L | ampli HIGH / Fosi | Potard réduit | 19.9 dB | 11.5 Vrms | ≈16.5 W @ 8 Ω | -5.1 dBFS | -6.1 dB |
| HIGH R | ampli HIGH / Fosi | même position | ≈19.9 dB* | 11.5 Vrms | ≈16.5 W @ 8 Ω | -5.1 dBFS | non documenté sur la capture |

`*` Le gain HIGH R est noté approximatif dans la source utilisateur.

## Paramètres dynamiques du limiteur

| Voie | Attack | Release | Ratio |
|---|---:|---:|---:|
| SUB | 10 ms | 500 ms | 20:1 |
| KICK | 5 ms | 300 ms | 20:1 |
| MID L/R | 2 ms | 200 ms | 20:1 |
| HIGH L/R | 1 ms | 150 ms | 20:1 |

## Remarques de traçabilité

- La seconde capture rend lisible la colonne `Compresseur` : SUB -13.6 dB, KICK -16.8 dB, MID L/R -6.1 dB, HIGH L -6.1 dB.
- La cellule `Compresseur` de HIGH R est vide dans la source. Ne pas supposer automatiquement qu'elle vaut -6.1 dB, même si HIGH L/R partagent les mêmes paramètres Attack/Release/Ratio.
- Les seuils ci-dessus devront être comparés avec la configuration CamillaDSP/YAML réellement chargée sur le Raspberry avant de déclarer la sauvegarde de protection complète.
- Les valeurs de tension/puissance doivent être conservées avec les réglages physiques des amplificateurs ; changer la position des potentiomètres modifie la validité des seuils dBFS calculés.

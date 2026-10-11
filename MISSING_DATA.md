# E-Stack — données manquantes et vérifications

Ce dépôt conserve une **transcription** de l'export live du 10 octobre 2026 (`CURRENT_REFERENCE.md`) et des conclusions REW. Il ne prouve pas que ce preset tourne encore sur le Raspberry le 11 octobre. Distinguer valeur documentée, fichier source disponible, et vérification physique.

## Critique pour une restauration exacte

- [ ] Versionner le **JSON complet de l'export live** cité (`2026-10-10T18:58:49.858Z`, révision `3b3d5f8e…`) dans `camilladsp/reference/`, après vérification des noms de périphériques/chemins éventuellement sensibles. Sa transcription Markdown ne conserve pas tous les filtres, étapes, processors, propriétés et mutes.
- [ ] Versionner séparément le **YAML matériel réellement chargé au démarrage** du Raspberry, avec la version CamillaDSP, les 8 canaux capture/playback, la taille du mixer et le chunksize. Un System Preset sauvegardé ne contient volontairement pas `devices` ni `mixers`.
- [ ] Comparer un **nouvel export live** et les choix de démarrage (YAML / preset précis / dernier preset) à la référence datée, puis consigner la révision et toute divergence. La présence du logiciel sur le Raspberry ne valide pas le dernier état DSP.
- [ ] Vérifier physiquement, sortie par sortie, la correspondance entre les destinations logiques 0…5 et les prises du DAC8x, ainsi que le sort des canaux matériels 6/7. Le mapping logiciel 8×8 ne démontre pas le câblage.
- [ ] Vérifier par signal de test la prise REW **IN3** rapportée par l'utilisateur et sa correspondance avec le canal CamillaDSP 2 (index zéro) avant une nouvelle campagne.
- [ ] Comparer protections, gains analogiques, positions des potentiomètres et tensions réellement mesurées avec les seuils du DSP. Les paramètres des compresseurs et hard limiters sont **transcrits** dans la référence du 10 octobre, mais leur efficacité matérielle n'est pas encore acceptée.
- [ ] Conserver les fichiers REW `.mdat` cités (`oct. 10 20_57_36.mdat`, `FULL_measuremennt.mdat`) ou indiquer un emplacement stable et leurs empreintes. Les conclusions seules ne permettent pas de refaire l'analyse complexe.

## Connu dans la transcription du 10 octobre, mais pas confirmé live aujourd'hui

- Délais absolus enregistrés : SUB **0,000 ms**, KICK **1,300 ms**, MID L/R **2,760 ms**, HIGH L/R **2,720 ms**.
- Seuils et temps de protection, ordre partiel des étapes et traitements actifs sont décrits dans `CURRENT_REFERENCE.md` et `calibration/REFERENCE_PRESET_BACKUP.md`. Le **graphe exact** nécessite le JSON original.
- PEQ/GEQ d'entrée : définitions présentes, sections **désactivées** dans l'export cité ; ne pas déduire qu'un « System EQ 162 Hz » est actuellement actif ni déplacer un filtre dans le graphe sans analyse/validation.
- REW : les trois campagnes projet utilisent `defaults.measurementInput: 3` ; cela exprime l'intention de router IN3, pas une preuve du câblage physique.

## Calibration encore à compléter

- [ ] Documenter les modèles et charges exacts par voie, ainsi que les réglages complets des amplificateurs utiles au calage.
- [ ] Documenter sweep range, niveau, longueur, timing reference et fichier de calibration micro de chaque série de référence.
- [ ] Ajouter les validations physiques SUM/REV de chaque crossover et les noms des traces `.mdat` associées.
- [ ] Ajouter les courbes finales magnitude, phase et group delay lorsque le preset REFERENCE sera terminé.
- [ ] Vérifier robustesse multi-position, directivité, distorsion et headroom/limitation thermique.
- [ ] Versionner les simulations et le scoring avant d'en déduire des réglages live.

**Règle :** ne pas présenter le dépôt comme une sauvegarde reconstructible à 100 % tant que ces sources et vérifications manquent. Ne pas remplacer les valeurs historiques par des suppositions.

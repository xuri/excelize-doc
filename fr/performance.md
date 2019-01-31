# Performance

Les performances indiquées ci-dessous indiquent le temps d'exécution et l'utilisation de la mémoire pour les feuilles de calcul de taille `N` lignes x `50` colonnes avec un mélange 50/50 de chaînes et de nombres. Les chiffres proviennent d'une machine de milieu de gamme arbitraire (OS: macOS High Sierra version 10.13.4, CPU: 1.8GHz Intel Core i5, RAM: 8 GB 1600 MHz DDR3, SSD: 120GB, Golang Version: `go1.10.2 darwin/amd64`, Commit: [`d96440e`](https://github.com/360EntSecGroup-Skylar/excelize/tree/d96440edc480976e3ec48958c68e67f7a506ad32)). Les chiffres spécifiques varient d'une machine à l'autre, mais les tendances devraient être les mêmes.

Lignes|Colonnes|Temps (s) - Préférentiellement Insérer des lignes|Temps (s) - Préférentiellement Insérer des colonnes|Mémoire (MB)
---|---|---|---|---
200|50|0.05|0.05|10.0
400|50|0.09|0.09|11.0
800|50|0.15|0.18|20.7
1600|50|0.37|0.42|36.1
3200|50|0.68|1.01|46.1
6400|50|1.34|3.36|136.9
12800|50|2.64|11.76|305.1

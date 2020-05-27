# Performance

Les performances indiquées ci-dessous indiquent le temps d'exécution et l'utilisation de la mémoire pour les feuilles de calcul de taille `N` lignes x `50` colonnes avec un mélange 50/50 de chaînes et de nombres. Les chiffres proviennent d'une machine de milieu de gamme arbitraire (OS: macOS Mojave version 10.14.4, CPU: 3.4 GHz Intel Core i5, RAM: 16 GB 2400 MHz DDR4, HDD: 1 TB, Go Version: `go1.12.4 darwin/amd64`, Commit: [`0660f30`](https://github.com/360EntSecGroup-Skylar/excelize/tree/0660f30cddc06de7883d40eb4f8e4945c18a0252)). Les chiffres spécifiques varient d'une machine à l'autre, mais les tendances devraient être les mêmes.

<table>
    <tr>
        <th>Type</th>
        <th>Lignes</th>
        <th>Colonnes</th>
        <th>Temps (s)</th>
        <th>Mémoire (MB)</th>
    </tr>
    <tr>
        <td rowspan="10">Set Cell Value</td>
        <td>200</td>
        <td>50</td>
        <td>0.03</td>
        <td>4</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>0.07</td>
        <td>5</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>0.12</td>
        <td>9</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>0.25</td>
        <td>15</td>
    </tr>
    <tr>
        <td>3200</td>
        <td>50</td>
        <td>0.49</td>
        <td>53</td>
    </tr>
    <tr>
        <td>6400</td>
        <td>50</td>
        <td>1.01</td>
        <td>101</td>
    </tr>
    <tr>
        <td>12800</td>
        <td>50</td>
        <td>2.06</td>
        <td>137</td>
    </tr>
    <tr>
        <td>25600</td>
        <td>50</td>
        <td>4.10</td>
        <td>237</td>
    </tr>
    <tr>
        <td>52100</td>
        <td>50</td>
        <td>8.44</td>
        <td>437</td>
    </tr>
    <tr>
        <td>102400</td>
        <td>50</td>
        <td>16.78</td>
        <td>1643</td>
    </tr>
    <tr>
        <td rowspan="1">Add Chart</td>
        <td>200</td>
        <td>50</td>
        <td>10.6</td>
        <td>171</td>
    </tr>
    <tr>
        <td rowspan="7">Set HyperLink</td>
        <td>200</td>
        <td>50</td>
        <td>0.08</td>
        <td>9</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>0.15</td>
        <td>16</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>0.31</td>
        <td>41</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>0.59</td>
        <td>63</td>
    </tr>
    <tr>
        <td>3200</td>
        <td>50</td>
        <td>1.16</td>
        <td>132</td>
    </tr>
    <tr>
        <td>6400</td>
        <td>50</td>
        <td>2.40</td>
        <td>253</td>
    </tr>
    <tr>
        <td>12800</td>
        <td>50</td>
        <td>4.94</td>
        <td>748</td>
    </tr>
    <tr>
        <td rowspan="7">Insert Picture</td>
        <td>200</td>
        <td>50</td>
        <td>0.86</td>
        <td>40</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>1.83</td>
        <td>79</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>4.11</td>
        <td>158</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>10.07</td>
        <td>316</td>
    </tr>
    <tr>
        <td>3200</td>
        <td>50</td>
        <td>28.17</td>
        <td>632</td>
    </tr>
    <tr>
        <td>6400</td>
        <td>50</td>
        <td>87.90</td>
        <td>1263</td>
    </tr>
    <tr>
        <td>12800</td>
        <td>50</td>
        <td>299.32</td>
        <td>2535</td>
    </tr>
</table>

## Comparaison des performances de bibliothèques similaires

Le graphique ci-dessous compare les performances de la matrice en texte brut de la génération `102400*50` avec les principales bibliothèques Excel open source sous un ordinateur personnel (OS: macOS Catalina version 10.15.4, CPU: 3.4 GHz Intel Core i5, RAM: 16 GB 2400 MHz DDR4, HDD: 1 TB), including Go, Python, Java, PHP and NodeJS.
) y compris Go, Python, Java, PHP et NodeJS.

<p align="center"><img width="688" src="https://xuri.me/wp-content/uploads/2016/08/excelize-golang-library-for-reading-and-writing-xlsx-files-3.png" alt="Comparaison des performances de bibliothèques similaires"></p>

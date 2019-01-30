# Utilitaire

## Table {#AddTable}

```go
func (f *File) AddTable(sheet, hcell, vcell, format string) error
```

AddTable fournit la méthode pour ajouter une table dans une feuille de calcul par nom de feuille de calcul donné, zone de coordonnées et jeu de formats.

- Exemple 1, créer une table de `A1:D5` sur `Sheet1`:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="Créer une table"></p>

```go
xlsx.AddTable("Sheet1", "A1", "D5", ``)
```

- Exemple 2, créer une table de `F2: H6` sur `Sheet2` avec le jeu de format:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="Ajouter une table avec le jeu de formats"></p>

```go
xlsx.AddTable("Sheet2", "F2", "H6", `{"table_name":"table","table_style":"TableStyleMedium2", "show_first_column":true,"show_last_column":true,"show_row_stripes":false,"show_column_stripes":true}`)
```

Notez que la table au moins deux lignes incluent l'en-tête de type chaîne. Les zones de coordonnées de plusieurs tables ne peuvent pas avoir d'intersection.

`table_name`: Le nom de la table, dans le même nom de feuille de calcul de la table, doit être unique.

`table_style`: Les noms de style de table intégrés:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

## Filtre autor {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, hcell, vcell, format string) error
```

AutoFilter fournit la méthode pour ajouter un filtre automatique dans une feuille de calcul en fonction du nom de la feuille de calcul, de la zone de coordonnées et des paramètres. Un filtre automatique dans Excel est un moyen de filtrer une plage de données 2D en fonction de critères simples.

Exemple 1, application d'un autofiltre à une plage de cellules `A1:D4` dans `Sheet1`:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="Ajouter un filtre automatique"></p>

```go
err = xlsx.AutoFilter("Sheet1", "A1", "D4", "")
```

Exemple 2, filtrez les données dans un autofiltre:

```go
err = xlsx.AutoFilter("Sheet1", "A1", "D4", `{"column":"B","expression":"x != blanks"}`)
```

`column` définit les colonnes de filtre dans une gamme de filtre automatique basée sur des critères simples

Il ne suffit pas de spécifier simplement la condition de filtre. Vous devez également masquer les lignes qui ne correspondent pas à la condition de filtre. Les lignes sont masquées à l'aide de la méthode [`SetRowVisible()`](sheet.md#SetRowVisible). Excelize ne peut pas filtrer les lignes automatiquement car cela ne fait pas partie du format de fichier.

SDéfinition d'un critère de filtre pour une colonne:

`expression` définit les conditions, les opérateurs suivants sont disponibles pour définir les critères de filtrage:

```text
==
!=
>
<
>=
<=
and
or
```

Une expression peut comprendre une seule instruction ou deux instructions séparées par les opérateurs `and` et `or`. Par exemple:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

Le filtrage des données vierges ou non peut être réalisé en utilisant une valeur de Blanks ou NonBlanks dans l'expression:

```text
x == Blanks
x == NonBlanks
```

Office Excel permet également certaines opérations de correspondance de chaînes simples:

```text
x == b*      // begins with b
x != b*      // doesn't begin with b
x == *b      // ends with b
x != *b      // doesn't end with b
x == *b*     // contains b
x != *b*     // doesn't contains b
```

Vous pouvez également utiliser `*` pour faire correspondre un caractère ou un nombre et `?` Pour correspondre à un seul caractère ou chiffre. Aucun autre quantificateur d'expressions régulières n'est pris en charge par les filtres d'Excel. Les caractères d'expression régulière d'Excel peuvent être échappés en utilisant `~`.

La variable d'espace réservé `x` dans les exemples ci-dessus peut être remplacée par n'importe quelle chaîne simple. Le nom de l'espace réservé réel est ignoré en interne de sorte que les éléments suivants sont tous équivalents:

```text
x     < 2000
col   < 2000
Price < 2000
```

## Mettre à jour la valeur liée {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue()
```

Les valeurs liées au correctif UpdateLinkedValue dans une feuille de calcul ne sont pas mises à jour dans Office Excel 2007 et 2010. Cette fonction supprime la balise de valeur lorsqu'une cellule est associée à une valeur liée. Référence[https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating?forum=excel](https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating?forum=excel) Avis: après ouverture du fichier XLSX, Excel mettra à jour la valeur liée et génèrera une nouvelle valeur et demandera l'enregistrement du fichier ou non.

L'effet de l'effacement du cache de cellules sur le classeur apparaît sous la forme d'une modification de la balise `<v>`, par exemple, le cache de la cellule avant l'effacement:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

Après avoir effacé le cache de la cellule:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## Convertir la colonne en index {#TitleToNumber}

```go
func TitleToNumber(s string) int
```

TitleToNumber fournit une fonction permettant de convertir le titre d'une colonne Excel en int (cette fonction ne vérifie pas la valeur actuellement). Par exemple, convertissez `AK` et `ak` dans le titre de colonne `36`:

```go
excelize.TitleToNumber("AK")
excelize.TitleToNumber("ak")
```

## Convertir l'index en colonne {#ToAlphaString}

```go
func ToAlphaString(value int) string
```

ToAlphaString fournit une fonction permettant de convertir un nombre entier en titre de colonne de feuille Excel. Par exemple, convertir `36` dans le titre de la colonne `AK`

```go
excelize.ToAlphaString(36)
```

## Style de condition {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style string) (int, error)
```

NewConditionalStyle fournit une fonction pour créer un style pour le format conditionnel par format de style donné. Les paramètres sont les mêmes que la fonction [`NewStyle()`](style.md#NewStyle). Notez que le champ de couleur utilise le code de couleur RGB et uniquement le support pour définir la police, les remplissages, l'alignement et les bordures actuellement.

## Format de condition {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, area, formatSet string) error
```

SetConditionalFormat fournit une fonction pour créer une règle de mise en forme conditionnelle pour la valeur de la cellule. La mise en forme conditionnelle est une fonctionnalité d'Office Excel qui vous permet d'appliquer un format à une cellule ou à une plage de cellules en fonction de certains critères.

L'option `type` est un paramètre obligatoire et n'a pas de valeur par défaut. Les valeurs de type autorisées et leurs paramètres associés sont:

<table>
    <thead>
        <tr>
            <th>Type</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td rowspan=4>date</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>duplicate</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>unique</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=2>top</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=6>2_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>mid_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>mid_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>mid_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=5>data_bar</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>bar_color</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>criteria</td>
        </tr>
    </tbody>
</table>

Le paramètre `criteria` est utilisé pour définir les critères selon lesquels les données de la cellule seront évaluées. Il n'a pas de valeur par défaut. Les critères les plus communs appliqués à `{"type"："cell"}` sont:

Caractère de description de texte|Représentation symbolique
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

Vous pouvez utiliser les chaînes de description textuelles d'Excel, dans la première colonne ci-dessus ou les alternatives symboliques les plus courantes.

Des critères supplémentaires spécifiques aux autres types de formats conditionnels sont présentés dans les sections pertinentes ci-dessous.

`value`: La valeur est généralement utilisée avec le paramètre `criteria` pour définir la règle selon laquelle les données de la cellule seront évaluées:

```go
xlsx.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[{"type":"cell","criteria":">","format":%d,"value":"6"}]`, format))
```

La propriété `value` peut également être une référence de cellule:

```go
xlsx.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[{"type":"cell","criteria":">","format":%d,"value":"$C$1"}]`, format))
```

type: `format` - Le paramètre `format` est utilisé pour spécifier le format qui sera appliqué à la cellule lorsque le critère de mise en forme conditionnelle est satisfait. Le format est créé en utilisant [`NewConditionalStyle()`](utils.md#NewConditionalStyle) une méthode de la même manière que les formats de cellule:

```go
format, err = xlsx.NewConditionalStyle(`{"font":{"color":"#9A0511"},"fill":{"type":"pattern","color":["#FEC7CE"],"pattern":1}}`)
if err != nil {
    fmt.Println(err)
}
xlsx.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[{"type":"cell","criteria":">","format":%d,"value":"6"}]`, format))
```

Remarque: Dans Excel, un format conditionnel est superposé au format de cellule existant et toutes les propriétés de format de cellule ne peuvent pas être modifiées. Les propriétés qui ne peuvent pas être modifiées dans un format conditionnel sont le nom de la police, la taille de la police, l'exposant et l'indice, les bordures diagonales, toutes les propriétés d'alignement et toutes les propriétés de protection.

Excel spécifie certains formats par défaut à utiliser avec la mise en forme conditionnelle. Ceux-ci peuvent être répliqués en utilisant les formats excelize suivants:

```go
// Format rose pour mauvais conditionnel.
format1, err = xlsx.NewConditionalStyle(`{"font":{"color":"#9A0511"},"fill":{"type":"pattern","color":["#FEC7CE"],"pattern":1}}`)

// Format jaune clair pour neutre conditionnel.
format2, err = xlsx.NewConditionalStyle(`{"font":{"color":"#9B5713"},"fill":{"type":"pattern","color":["#FEEAA0"],"pattern":1}}`)

// Le format vert clair pour le bon conditionnel.
format3, err = xlsx.NewConditionalStyle(`{"font":{"color":"#09600B"},"fill":{"type":"pattern","color":["#C7EECF"],"pattern":1}}`)
```

type: `minimum` - Le paramètre minimum est utilisé pour définir la valeur limite inférieure lorsque le `critère` est entre `between` ou `not between`.

```go
// Highlight cells rules: between...
xlsx.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[{"type":"cell","criteria":"between","format":%d,"minimum":"6","maximum":"8"}]`, format))
```

type: `maximum` - Le paramètre `maximum` est utilisé pour définir la valeur limite supérieure lorsque les critères sont entre `between` ou `not between`. Voir l'exemple précédent.

type: `average` - Le type `average` est utilisé pour spécifier le format conditionnel de style "Moyenne" d'Office Excel:

```go
// Haut/Bas règles: Au-dessus de la moyenne ...
xlsx.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[{"type":"average","criteria":"=","format":%d, "above_average": true}]`, format1))

// THaut/Bas règles: Au-dessous de la moyenne ...
xlsx.SetConditionalFormat("Sheet1", "B1:B10", fmt.Sprintf(`[{"type":"average","criteria":"=","format":%d, "above_average": false}]`, format2))
```

type: `duplicate` - The `duplicate` type is used to highlight duplicate cells in a range:

```go
// Mettez en surbrillance les règles relatives aux cellules: Valeurs en double ...
xlsx.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[{"type":"duplicate","criteria":"=","format":%d}]`, format))
```

type: `unique` - Le type unique est utilisé pour mettre en évidence des cellules individuelles dans une gamme:

```go
// Mettez en surbrillance les règles des cellules: pas égal à ...
xlsx.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[{"type":"unique","criteria":"=","format":%d}]`, format))
```

type: `top` - Le type `top` est utilisé pour spécifier les n premières valeurs en nombre ou en pourcentage dans une plage:

```go
// THaut/Bas règles: Top 10.
xlsx.SetConditionalFormat("Sheet1", "H1:H10", fmt.Sprintf(`[{"type":"top","criteria":"=","format":%d,"value":"6"}]`, format))
```

Les critères peuvent être utilisés pour indiquer qu'une condition de pourcentage est requise:

```go
xlsx.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[{"type":"top","criteria":"=","format":%d,"value":"6","percent":true}]`, format))
```

type: `2_color_scale` - Le type `2_color_scale` est utilisé pour spécifier le format conditionnel de style Excel "2 Color Scale":

```go
// Échelles de couleurs: 2 couleurs.
xlsx.SetConditionalFormat("Sheet1", "A1:A10", `[{"type":"2_color_scale","criteria":"=","min_type":"min","max_type":"max","min_color":"#F8696B","max_color":"#63BE7B"}]`)
```

Ce type conditionnel peut être modifié avec `min_type`, `max_type`, `min_value`, `max_value`, `min_color` et `max_color`, voir ci-dessous.

type: `3_color_scale` - Le type `3_color_scale` est utilisé pour spécifier le format conditionnel de style "3 Color Scale" d'Excel:

```go
// Échelles de couleurs: 3 couleurs.
xlsx.SetConditionalFormat("Sheet1", "A1:A10", `[{"type":"3_color_scale","criteria":"=","min_type":"min","mid_type":"percentile","max_type":"max","min_color":"#F8696B","mid_color":"#FFEB84","max_color":"#63BE7B"}]`)
```

Ce type conditionnel peut être modifié avec `min_type`, `mid_type`, `max_type`, `min_value`, `mid_value`, `max_value`, `min_color`, `mid_color` et `max_color`, voir ci-dessous.

type: `data_bar` - Le type `data_bar` est utilisé pour spécifier le format conditionnel du style "Data Bar" d'Excel.

`min_type` - Les propriétés `min_type` et `max_type` sont disponibles lorsque le type de formatage conditionnel est `2_color_scale`, `3_color_scale` ou `data_bar`. Le `mid_type` est disponible pour `3_color_scale`. Les propriétés sont utilisées comme suit:

```go
// Barres de données: Remplissage dégradé.
xlsx.SetConditionalFormat("Sheet1", "K1:K10", `[{"type":"data_bar", "criteria":"=", "min_type":"min","max_type":"max","bar_color":"#638EC6"}]`)
```

Les types `min/mid/max` disponibles sont:

Paramètre|Explication
---|---
min|Minimum value (for `min_type` only)
num|Numeric
percent|Percentage
percentile|Percentile
formula|Formula
max|Maximum (for `max_type` only)

`mid_type` - Utilisé pour `3_color_scale`. Pareil que `min_type`, voir au dessus.

`max_type` - Pareil que `min_type`, voir au dessus.

`min_value` - Les propriétés `min_value` et `max_value` sont disponibles lorsque le type de formatage conditionnel est `2_color_scale`, `3_color_scale` ou `data_bar`. La valeur `mid_value` est disponible pour `3_color_scale`.

`mid_value` - Utilisé pour `3_color_scale`. Pareil que `min_value`, voir au dessus.

`max_value` - Pareil que `min_value`, voir au dessus.

`min_color` - Les propriétés `min_color` et `max_color` sont disponibles lorsque le type de formatage conditionnel est `2_color_scale`, `3_color_scale` ou `data_bar`. Le `mid_color` est disponible pour `3_color_scale`. Les propriétés sont utilisées comme suit:

```go
// Échelles de couleurs: 3 couleurs.
xlsx.SetConditionalFormat("Sheet1", "B1:B10", `[{"type":"3_color_scale","criteria":"=","min_type":"min","mid_type":"percentile","max_type":"max","min_color":"#F8696B","mid_color":"#FFEB84","max_color":"#63BE7B"}]`)
```

`mid_color` - Utilisé pour `3_color_scale`. Pareil que `min_color`, voir au dessus.

`max_color` - Pareil que `min_color`, voir au dessus.

`bar_color` - Utilisé pour `data_bar`. Pareil que `min_color`, voir au dessus.

## Panes {#SetPanes}

```go
func (f *File) SetPanes(sheet, panes string)
```

SetPanes fournit une fonction permettant de créer et de supprimer des fenêtres de gel et des panneaux de division en fonction d'un ensemble de formats de nom de feuille de calcul et de volets donnés.

`activePane` définit le volet actif. Les valeurs possibles pour cet attribut sont définies dans le tableau suivant:

Valeur d'énumération|Description
---|---
bottomLeft (Bottom Left Pane) |Panneau inférieur gauche, lorsque des divisions verticales et horizontales sont appliquées.<br><br>Cette valeur est également utilisée lorsque seule une division horizontale a été appliquée, divisant le volet en régions supérieure et inférieure. Dans ce cas, cette valeur spécifie le volet inférieur.
bottomRight (Bottom Right Pane) |Volet inférieur droit, lorsque des divisions verticales et horizontales sont appliquées.
topLeft (Top Left Pane)|Volet supérieur gauche, lorsque des divisions verticales et horizontales sont appliquées.<br><br>Cette valeur est également utilisée lorsque seule une division horizontale a été appliquée, divisant le volet en régions supérieure et inférieure. Dans ce cas, cette valeur spécifie le volet supérieur.<br><br>Cette valeur est également utilisée lorsque seule une division verticale a été appliquée, divisant le volet en régions droite et gauche. Dans ce cas, cette valeur spécifie le volet de gauche.
topRight (Top Right Pane)|Volet supérieur droit, lorsque des divisions verticales et horizontales sont appliquées.<br><br>Cette valeur est également utilisée lorsque seule une division verticale a été appliquée, divisant le volet en régions droite et gauche. Dans ce cas, cette valeur spécifie le volet droit.

Le type d'état du volet est limité aux valeurs prises en charge actuellement répertoriées dans le tableau suivant:

Valeur d'énumération|Description
---|---
frozen (Frozen)|Les panneaux sont gelés, mais n'ont pas été divisés. Dans cet état, lorsque les volets sont à nouveau décongelés, un seul volet est généré, sans division.<br><br>Dans cet état, les barres de fractionnement ne sont pas réglables.
split (Split)|Les volets sont divisés, mais pas gelés. Dans cet état, les barres de fractionnement sont réglables par l'utilisateur.

`x_split` - Position horizontale de la fente, en 1/20ème de point; 0 (zéro) si aucun. Si le volet est figé, cette valeur indique le nombre de colonnes visibles dans le volet supérieur.

`y_split` - Position verticale de la fente, en 1/20ème de pointe; 0 (zéro) si aucun. Si le volet est figé, cette valeur indique le nombre de lignes visibles dans le volet de gauche. Les valeurs possibles pour cet attribut sont définies par le double type de données W3C XML Schema.

`top_left_cell` - L'emplacement du haut à gauche de la cellule visible dans le volet inférieur droit (en mode Gauche-Droite).

`sqref` - La plage de la sélection Peut être un ensemble de plages non contiguës.

Example 1: freeze column `A` in the `Sheet1` and set the active cell on `Sheet1!K16`:

!["Colonne gelée"](./images/setpans_01.png "Colonne gelée")

```go
xlsx.SetPanes("Sheet1", `{"freeze":true,"split":false,"x_split":1,"y_split":0,"top_left_cell":"B1","active_pane":"topRight","panes":[{"sqref":"K16","active_cell":"K16","pane":"topRight"}]}`)
```

Exemple 2: geler les lignes 1 à 9 dans la feuille Sheet1 et définir les plages de cellules actives sur `Sheet1!A11:XFD11`:

!["Geler les colonnes et définir les plages de cellules actives"](./images/setpans_02.png "Geler les colonnes et définir les plages de cellules actives")

```go
xlsx.SetPanes("Sheet1", `{"freeze":true,"split":false,"x_split":0,"y_split":9,"top_left_cell":"A34","active_pane":"bottomLeft","panes":[{"sqref":"A11:XFD11","active_cell":"A11","pane":"bottomLeft"}]}`)
```

Exemple 3: créer des volets fractionnés dans `Sheet1` et définir la cellule active sur  `Sheet1!J60`:

!["Créer des volets divisés"](./images/setpans_03.png "Créer des volets divisés")

```go
xlsx.SetPanes("Sheet1", `{"freeze":false,"split":true,"x_split":3270,"y_split":1800,"top_left_cell":"N57","active_pane":"bottomLeft","panes":[{"sqref":"I36","active_cell":"I36"},{"sqref":"G33","active_cell":"G33","pane":"topRight"},{"sqref":"J60","active_cell":"J60","pane":"bottomLeft"},{"sqref":"O60","active_cell":"O60","pane":"bottomRight"}]}`)
```

Exemple 4, dégeler et supprimer tous les volets sur `Sheet1`:

```go
xlsx.SetPanes("Sheet1", `{"freeze":false,"split":false}`)
```

## Couleur {#ThemeColor}

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor a appliqué la couleur avec la valeur de teinte:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx, _ := excelize.OpenFile("Book1.xlsx")
    fmt.Println(getCellBgColor(xlsx, "Sheet1", "C1"))
}

func getCellBgColor(xlsx *excelize.File, sheet, axix string) string {
    styleID := xlsx.GetCellStyle(sheet, axix)
    fillID := xlsx.Styles.CellXfs.Xf[styleID].FillID
    fgColor := xlsx.Styles.Fills.Fill[fillID].PatternFill.FgColor
    if fgColor.Theme != nil {
        srgbClr := xlsx.Theme.ThemeElements.ClrScheme.Children[*fgColor.Theme].SrgbClr.Val
        return excelize.ThemeColor(srgbClr, fgColor.Tint)
    }
    return fgColor.RGB
}
```

## Convertir RGB en HSL {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL convertit un triplet RGB en triplet HSL.

## Convertir HSL en RGB {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB convertit un triple HSL en un triple RGB.

## Writer Fichier {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer) error
```

Write fournit une fonction pour écrire dans un `io.Writer`.

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer) (int64, error)
```

WriteTo implémente `io.WriterTo` pour écrire le fichier.

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer fournit une fonction pour obtenir `*bytes.Buffer` à partir du fichier enregistré.

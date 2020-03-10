# Cellule

## Définir la valeur de la cellule {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{}) error
```

SetCellValue fournit une fonction pour définir la valeur d'une cellule. Les coordonnées spécifiées ne doivent pas figurer dans la première ligne du tableau. Voici les types de données pris en charge:

|Types de données pris en charge|
|---|
|int|
|int8|
|int16|
|int32|
|int64|
|uint|
|uint8|
|uint16|
|uint32|
|uint64|
|float32|
|float64|
|string|
|[]byte|
|time.Duration|
|time.Time|
|bool|
|nil|

## Définir la valeur booléenne {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool) error
```

SetCellBool fournit une fonction pour définir la valeur du type booléen d'une cellule par nom de feuille de calcul donné, coordonnées de cellule et valeur de cellule.

## Définir la valeur RAW {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string) error
```

SetCellDefault fournit une fonction pour définir la valeur de type chaîne d'une cellule comme format par défaut sans échapper à la cellule.

## Définir la valeur entière {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int) error
```

SetCellInt fournit une fonction pour définir la valeur de type int d'une cellule par nom de feuille de calcul donné, coordonnées de cellule et valeur de cellule.

## Définir la valeur de chaîne {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string) error
```

SetCellStr fournit une fonction pour définir la valeur du type de chaîne d'une cellule. Nombre total de caractères qu'une cellule peut contenir `32767`.

## Définir le style de cellule {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hcell, vcell string, styleID int) error
```

SetCellStyle fournit la fonction pour ajouter l'attribut de style pour les cellules par nom de feuille de calcul donné, zone de coordonnées et ID de style. Les index de style peuvent être obtenus avec la fonction [`NewStyle`](style.md#NewStyle). Notez que les bordures de type `diagonalDown` et` diagonalUp` doivent utiliser la même couleur dans la même zone de coordonnées.

- Exemple 1, créez une bordure de la cellule `D7` sur `Sheet1`:

```go
style, err := f.NewStyle(`{"border":[{"type":"left","color":"0000FF","style":3},{"type":"top","color":"00FF00","style":4},{"type":"bottom","color":"FFFF00","style":5},{"type":"right","color":"FF0000","style":6},{"type":"diagonalDown","color":"A020F0","style":7},{"type":"diagonalUp","color":"A020F0","style":8}]}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="Définir un style de bordure pour une cellule"></p>

Les quatre bordures de la cellule `D7` sont définies avec des styles et des couleurs différents. Ceci est lié aux paramètres lors de l'appel de la fonction [`NewStyle`](style.md#NewStyle). Vous devez définir différents styles pour faire référence à la documentation de ce chapitre.

- Exemple 2, définition du style de dégradé pour la cellule `D7` de la feuille de calcul nommée `Sheet1`:

```go
style, err := f.NewStyle(`{"fill":{"type":"gradient","color":["#FFFFFF","#E0EBF5"],"shading":1}}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="Définir un style de dégradé pour la cellule"></p>

La cellule `D7` est définie avec le remplissage de couleur de l'effet de dégradé. L'effet de remplissage de dégradé est lié au paramètre lorsque la fonction [`NewStyle`](style.md#NewStyle) est appelée. Vous devez définir différents styles pour vous référer à la documentation de ce chapitre.

- Exemple 3, définissez un remplissage solide pour la cellule `D7` nommée `Sheet1`:

```go
style, err := f.NewStyle(`{"fill":{"type":"pattern","color":["#E0EBF5"],"pattern":1}}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="Définir un remplissage solide pour la cellule"></p>

La cellule `D7` est définie avec un remplissage solide.

- Exemple 4, définissez l'espacement des caractères et l'angle de rotation pour la cellule `D7` nommée `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Style")
style, err := f.NewStyle(`{"alignment":{"horizontal":"center","ident":1,"justify_last_line":true,"reading_order":0,"relative_indent":1,"shrink_to_fit":true,"text_rotation":45,"vertical":"","wrap_text":true}}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="Définir l'espacement des caractères et l'angle de rotation"></p>

- Exemple 5, la date et l'heure dans Excel sont représentées par des nombres réels, par exemple, `2017/7/4 12:00:00 PM` peut être représenté par le nombre `42920.5`. Définissez le format d'heure pour la cellule `D7` de la feuille de calcul nommée `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(`{"number_format": 22}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="Définir le format de l'heure pour la cellule"></p>

La cellule `D7` est définie sur le format de l'heure. Notez que lorsque la largeur de la cellule avec le format d'heure appliqué est trop étroite pour être entièrement affichée, elle sera affichée comme `####`, vous pouvez faire glisser et déposer la largeur de colonne ou définir la taille appropriée de la colonne en appelant le Fonction `SetColWidth` pour le rendre normal. afficher.

- Exemple 6, définition de la police, de la taille de police, de la couleur et du style de décalage pour la cellule de la feuille de calcul `D7` nommée `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Excel")
style, err := f.NewStyle(`{"font":{"bold":true,"italic":true,"family":"Times New Roman","size":36,"color":"#777777"}}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="Définir la police, la taille de la police, la couleur et le style de biais pour les cellules"></p>

- Exemple 7, verrouillage et masquage de la cellule `D7` de la feuille de calcul nommée `Sheet1`:

```go
style, err := f.NewStyle(`{"protection":{"hidden":true, "locked":true}}`)
if err != nil {
    println(err.Error())
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

Pour verrouiller une cellule ou masquer une formule, protégez la feuille de calcul. Dans l'onglet "La revue", cliquez sur "Protéger la feuille de travail".

## Définir un lien hypertexte {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string) error
```

SetCellHyperLink fournit une fonction pour définir le lien hypertexte de cellule par nom de feuille de calcul donné et adresse URL de lien. LinkType définit deux types d'hyperliens `External` pour site Web ou `Location` pour passer à l'une des cellules de ce classeur. Le nombre maximal d’hyperliens de limite dans une feuille de calcul est `65530`. Ce qui suit est un exemple de lien externe.

- Exemple 1, ajout d'un lien externe à la cellule `A3` de la feuille de calcul nommée `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "https://github.com/360EntSecGroup-Skylar/excelize", "External")
// Définir le style de police et de soulignement pour la cellule
style, err := f.NewStyle(`{"font":{"color":"#1265BE","underline":"single"}}`)
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- Exemple 2, ajout d'un lien d'emplacement interne à la cellule `A3` nommée `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## Obtenir la valeur de la cellule {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string) (string, error)
```

La valeur de la cellule est récupérée en fonction de la feuille de calcul et des coordonnées de la cellule, et la valeur de retour est convertie en type `string`. Si le format de cellule peut être appliqué à la valeur d'une cellule, la valeur appliquée sera renvoyée, sinon la valeur d'origine sera renvoyée.

## Obtenir toute la valeur de la cellule {#GetRows}

```go
func (f *File) GetRows(sheet string) ([][]string, error)
```

Obtient la valeur de toutes les cellules de la feuille de calcul en fonction du nom de feuille de calcul donné (sensible à la casse), renvoyé sous la forme d'un tableau à deux dimensions, où la valeur de la cellule est convertie en type chaîne. Si le format de cellule peut être appliqué à la valeur de la cellule, la valeur appliquée sera utilisée, sinon la valeur d'origine sera utilisée.

Par exemple, obtenez et parcourez la valeur de toutes les cellules d'une feuille de calcul appelée `Sheet1`:

```go
rows, err := f.GetRows("Sheet1")
for _, row := range rows {
    for _, colCell := range row {
        print(colCell, "\t")
    }
    println()
}
```

## Obtenir un lien hypertexte {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string, error)
```

Obtient un lien hypertexte de cellule basé sur le nom de feuille de calcul donné (sensible à la casse) et les coordonnées de cellule. Si la cellule a un lien hypertexte, elle retournera `true` et l'adresse du lien, sinon elle retournera `false` et une adresse de lien vide.

Par exemple, obtenez un lien hypertexte vers une cellule `H6` sur une feuille de calcul nommée `Sheet1`:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## Obtenir l'index de style {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) (int, error)
```

L'index de style de cellule est obtenu à partir du nom de feuille de calcul donné (sensible à la casse) et des coordonnées de cellule, et l'index obtenu peut être utilisé comme paramètre pour appeler la fonction `SetCellValue` lors de la copie du style de cellule.

## Fusionner les cellules {#MergeCell}

```go
func (f *File) MergeCell(sheet, hcell, vcell string) error
```

Fusionner des cellules en fonction du nom de feuille de calcul donné (sensible à la casse) et des régions de coordonnées de cellule. Par exemple, fusionner des cellules dans la zone `D3:E9` sur une feuille de calcul nommée `Sheet1`:

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

Si la zone de coordonnées de cellule donnée chevauche d'autres cellules fusionnées existantes, les cellules fusionnées existantes seront supprimées.

## Dissocier les cellules {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hcell, vcell string) error
```

UnmergeCell fournit une fonction pour annuler la fusion d'une zone de coordonnées donnée. Par exemple, annuler la fusion de la zone `D3:E9` sur `Sheet1`:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

Attention: les zones qui se chevauchent seront également non fusionnées.

## Obtenir les cellules fusionnées {#GetMergeCells}

GetMergeCells fournit une fonction pour obtenir toutes les cellules fusionnées à partir d'une feuille de calcul.

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

## Ajouter un commentaire {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

AddComment fournit la méthode pour ajouter un commentaire dans une feuille par index de feuille de calcul, cellule et ensemble de formats donnés (tels que l'auteur et le texte). Notez que la longueur maximale de l'auteur est 255 et la longueur maximale du texte est 32512. Par exemple, ajoutez un commentaire dans `Sheet1!$A$3`:

!["Ajouter un commentaire à un document Excel"](./images/comment.png "Ajouter un commentaire à un document Excel")

```go
err := f.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"This is a comment."}`)
```

## Obtenir un commentaire {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

GetComments récupère tous les commentaires et renvoie une carte de nom de feuille de calcul dans les commentaires de feuille de calcul.

## Formule de définition de cellule {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string, opts ...FormulaOpts) error
```

La formule sur la cellule est prise en fonction du nom de feuille de calcul donné (sensible à la casse) et des paramètres de formule de cellule. Le résultat de la formule est calculé lorsque la feuille de calcul est ouverte par l'application Office Excel et que Excelize ne fournit pas actuellement de moteur de calcul de formule. Les résultats de formule ne peuvent donc pas être calculés.

## Obtenir la formule cellulaire {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, axis string) (string, error)
```

Obtenez la formule sur la cellule en fonction du nom de feuille de calcul donné (sensible à la casse) et des coordonnées de cellule.

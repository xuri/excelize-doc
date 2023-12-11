# Cellule

`RichTextRun` mappe directement les paramètres de l'exécution de texte riche.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

`HyperlinkOpts` peut être transmis à [`SetCellHyperlink`](cell.md#SetCellHyperlink) pour définir des attributs de lien hypertexte facultatifs (par exemple, le texte à afficher et le texte de l'info-bulle à l'écran).

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

`FormulaOpts` peut être transmis à [`SetCellFormula`](cell.md#SetCellFormula) pour utiliser d'autres types de formules.

```go
type FormulaOpts struct {
    Type *string // Type de formule
    Ref  *string // Référence de formule partagée
}
```

## Définir la valeur de la cellule {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, cell string, value interface{}) error
```

SetCellValue fournit une fonction pour définir la valeur d'une cellule. Cette fonction est sécurisée pour la concurrence. Les coordonnées spécifiées ne doivent pas figurer dans la première ligne du tableau. Voici les types de données pris en charge:

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

Notez que le format de date par défaut est `m/d/yy h:mm` de la valeur de type `time.Time`. Vous pouvez définir le format des nombres par la méthode [`SetCellStyle`](cell.md#SetCellStyle). Si vous devez définir la date spécialisée dans Excel comme le 0 janvier 1900 ou le 29 février 1900, ces heures ne peuvent pas être représentées dans le type de données `time.Time` du langage Go. Veuillez définir la valeur de la cellule sur le nombre 0 ou 60, puis créez et liez le style de format de nombre date-heure pour la cellule.

## Définir la valeur booléenne {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, cell string, value bool) error
```

SetCellBool fournit une fonction pour définir la valeur du type booléen d'une cellule par nom de feuille de calcul donné, coordonnées de cellule et valeur de cellule.

## Définir la valeur RAW {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, cell, value string) error
```

SetCellDefault fournit une fonction pour définir la valeur de type chaîne d'une cellule comme format par défaut sans échapper à la cellule.

## Définir la valeur entière {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, cell string, value int) error
```

SetCellInt fournit une fonction pour définir la valeur de type int d'une cellule par nom de feuille de calcul donné, coordonnées de cellule et valeur de cellule.

## Définir une valeur entière non signée {#SetCellUint}

```go
func (f *File) SetCellUint(sheet, cell string, value uint64) error
```

SetCellUint fournit une fonction permettant de définir la valeur de type de données entier non signé d'une cellule par nom de feuille de calcul, référence de cellule et valeur de cellule donnés.

## Définir la valeur en virgule flottante {#SetCellFloat}

```go
func (f *File) SetCellFloat(sheet, cell string, value float64, precision, bitSize int) error
```

SetCellFloat définit une valeur à virgule flottante dans une cellule. Le paramètre `precision` spécifie combien de décimales après la virgule seront affichées tandis que `-1` est une valeur spéciale qui utilisera autant de décimales que nécessaire pour représenter le nombre. `bitSize` est `32` ou `64` selon qu'un `float32` ou `float64` a été utilisé à l'origine pour la valeur.

## Définir la valeur de chaîne {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, cell, value string) error
```

SetCellStr fournit une fonction pour définir la valeur du type de chaîne d'une cellule. Nombre total de caractères qu'une cellule peut contenir `32767`.

## Définir le style de cellule {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

SetCellStyle fournit la fonction pour ajouter l'attribut de style pour les cellules par nom de feuille de calcul donné, zone de coordonnées et ID de style. Cette fonction est sécurisée pour la concurrence. Les index de style peuvent être obtenus avec la fonction [`NewStyle`](style.md#NewStyle). Notez que les bordures de type `diagonalDown` et `diagonalUp` doivent utiliser la même couleur dans la même zone de coordonnées. SetCellStyle écrasera les styles existants pour la cellule, il n'ajoutera ni ne fusionnera le style avec les styles existants.

- Exemple 1, créez une bordure de la cellule `D7` sur `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Border: []excelize.Border{
        {Type: "left", Color: "0000FF", Style: 3},
        {Type: "top", Color: "00FF00", Style: 4},
        {Type: "bottom", Color: "FFFF00", Style: 5},
        {Type: "right", Color: "FF0000", Style: 6},
        {Type: "diagonalDown", Color: "A020F0", Style: 8},
        {Type: "diagonalUp", Color: "A020F0", Style: 8},
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="Définir un style de bordure pour une cellule"></p>

Les quatre bordures de la cellule `D7` sont définies avec des styles et des couleurs différents. Ceci est lié aux paramètres lors de l'appel de la fonction [`NewStyle`](style.md#NewStyle). Vous devez définir différents styles pour faire référence à la documentation de ce chapitre.

- Exemple 2, définition du style de dégradé pour la cellule `D7` de la feuille de calcul nommée `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"FFFFFF", "E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="Définir un style de dégradé pour la cellule"></p>

La cellule `D7` est définie avec le remplissage de couleur de l'effet de dégradé. L'effet de remplissage de dégradé est lié au paramètre lorsque la fonction [`NewStyle`](style.md#NewStyle) est appelée. Vous devez définir différents styles pour vous référer à la documentation de ce chapitre.

- Exemple 3, définissez un remplissage solide pour la cellule `D7` nommée `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="Définir un remplissage solide pour la cellule"></p>

La cellule `D7` est définie avec un remplissage solide.

- Exemple 4, définissez l'espacement des caractères et l'angle de rotation pour la cellule `D7` nommée `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Style")
style, err := f.NewStyle(&excelize.Style{
    Alignment: &excelize.Alignment{
        Horizontal:      "center",
        Indent:          1,
        JustifyLastLine: true,
        ReadingOrder:    0,
        RelativeIndent:  1,
        ShrinkToFit:     true,
        TextRotation:    45,
        Vertical:        "",
        WrapText:        true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="Définir l'espacement des caractères et l'angle de rotation"></p>

- Exemple 5, la date et l'heure dans Excel sont représentées par des nombres réels, par exemple, `2017/7/4 12:00:00 PM` peut être représenté par le nombre `42920.5`. Définissez le format d'heure pour la cellule `D7` de la feuille de calcul nommée `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="Définir le format de l'heure pour la cellule"></p>

La cellule `D7` est définie sur le format de l'heure. Notez que lorsque la largeur de la cellule avec le format d'heure appliqué est trop étroite pour être entièrement affichée, elle sera affichée comme `####`, vous pouvez faire glisser et déposer la largeur de colonne ou définir la taille appropriée de la colonne en appelant le Fonction `SetColWidth` pour le rendre normal. afficher.

- Exemple 6, définition de la police, de la taille de police, de la couleur et du style de décalage pour la cellule de la feuille de calcul `D7` nommée `Sheet1`:

```go
f.SetCellValue("Sheet1", "D7", "Excel")
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{
        Bold:   true,
        Italic: true,
        Family: "Times New Roman",
        Size:   36,
        Color:  "777777",
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="Définir la police, la taille de la police, la couleur et le style de biais pour les cellules"></p>

- Exemple 7, verrouillage et masquage de la cellule `D7` de la feuille de calcul nommée `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Protection: &excelize.Protection{
        Hidden: true,
        Locked: true,
    },
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

Pour verrouiller une cellule ou masquer une formule, protégez la feuille de calcul. Dans l'onglet "La revue", cliquez sur "Protéger la feuille de travail".

## Définir un lien hypertexte {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, cell, link, linkType string, opts ...HyperlinkOpts) error
```

SetCellHyperLink fournit une fonction pour définir le lien hypertexte de cellule par nom de feuille de calcul donné et adresse URL de lien. LinkType définit deux types d'hyperliens `External` pour site Web ou `Location` pour passer à l'une des cellules de ce classeur. Le nombre maximal d'hyperliens de limite dans une feuille de calcul est `65530`. Cette fonction est uniquement utilisée pour définir le lien hypertexte de la cellule et n'affecte pas la valeur de la cellule. Si vous devez définir la valeur de la cellule, veuillez utiliser les autres fonctions telles que [`SetCellStyle`](cell.md#SetCellStyle) ou [`SetSheetRow`](sheet.md#SetSheetRow). Ce qui suit est un exemple de lien externe.

- Exemple 1, ajout d'un lien externe à la cellule `A3` de la feuille de calcul nommée `Sheet1`:

```go
display, tooltip := "https://github.com/xuri/excelize", "Excelize on GitHub"
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External", excelize.HyperlinkOpts{
        Display: &display,
        Tooltip: &tooltip,
    }); err != nil {
    fmt.Println(err)
}
// Définir le style de police et de soulignement pour la cellule
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- Exemple 2, ajout d'un lien d'emplacement interne à la cellule `A3` nommée `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## Définir le texte riche pour la cellule {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

SetCellRichText fournit une fonction pour définir une cellule avec du texte riche par feuille de calcul donnée.

Par exemple, définissez du texte enrichi dans la cellule `A1` de la feuille de calcul nommée `Sheet1`:

<p align="center"><img width="612" src="./images/rich_text.png" alt="Définir le texte riche pour la cellule"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    if err := f.SetRowHeight("Sheet1", 1, 35); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetColWidth("Sheet1", "A", "A", 44); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellRichText("Sheet1", "A1", []excelize.RichTextRun{
        {
            Text: "bold",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354E8",
                Family: "Times New Roman",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Family: "Times New Roman",
            },
        },
        {
            Text: "italic ",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "E83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354E8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "AD23E8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "E89923",
                Strike: true,
            },
        },
        {
            Text: " superscript",
            Font: &excelize.Font{
                Color:     "DBC21F",
                VertAlign: "superscript",
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:      14,
                Color:     "AD23E8",
                VertAlign: "baseline",
            },
        },
        {
            Text: "underline",
            Font: &excelize.Font{
                Color:     "23E833",
                Underline: "single",
            },
        },
        {
            Text: " subscript.",
            Font: &excelize.Font{
                Color:     "017505",
                VertAlign: "subscript",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    style, err := f.NewStyle(&excelize.Style{
        Alignment: &excelize.Alignment{
            WrapText: true,
        },
    })
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetCellStyle("Sheet1", "A1", "A1", style); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtenir le texte enrichi de la cellule {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) ([]RichTextRun, error)
```

GetCellRichText fournit une fonction pour obtenir le texte enrichi des cellules par feuille de calcul donnée.

## Obtenir la valeur de la cellule {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, cell string, opts ...Options) (string, error)
```

La valeur de la cellule est récupérée en fonction de la feuille de calcul et des coordonnées de la cellule, et la valeur de retour est convertie en type `string`. Cette fonction est sécurisée pour la concurrence. Si le format de cellule peut être appliqué à la valeur d'une cellule, la valeur appliquée sera renvoyée, sinon la valeur d'origine sera renvoyée. Les valeurs de toutes les cellules seront les mêmes dans une plage fusionnée.

## Obtenir le type de cellule {#GetCellType}

```go
func (f *File) GetCellType(sheet, cell string) (CellType, error)
```

GetCellType fournit une fonction pour obtenir le type de données de la cellule par nom de feuille de calcul et axe donnés dans un fichier de feuille de calcul.

## Obtenir toutes les valeurs des cellules par colonnes {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

GetCols obtient la valeur de toutes les cellules par colonnes de la feuille de calcul en fonction du nom de feuille de calcul donné, renvoyé sous la forme d'un tableau à deux dimensions, où la valeur de la cellule est convertie en type `string`. Si le format de cellule peut être appliqué à la valeur de la cellule, la valeur appliquée sera utilisée, sinon la valeur d'origine sera utilisée.

Par exemple, obtenez et parcourez la valeur de toutes les cellules par colonnes dans une feuille de calcul nommée `Feuil1`:

```go
cols, err := f.GetCols("Feuil1")
if err != nil {
    fmt.Println(err)
    return
}
for _, col := range cols {
    for _, rowCell := range col {
        fmt.Print(rowCell, "\t")
    }
    fmt.Println()
}
```

## Obtenir toutes les valeurs de la cellule par des lignes {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

GetRows renvoie toutes les lignes d'une feuille par nom de feuille de calcul donné, renvoyé sous la forme d'un tableau à deux dimensions, où la valeur de la cellule est convertie en type `string`. Si le format de cellule peut être appliqué à la valeur de la cellule, la valeur appliquée sera utilisée, sinon la valeur d'origine sera utilisée. GetRows a récupéré les lignes avec des cellules de valeur ou de formule, les cellules continuellement vides à la fin de chaque ligne seront ignorées, de sorte que la longueur de chaque ligne peut être incohérente.

Par exemple, obtenez et parcourez la valeur de toutes les cellules par lignes sur une feuille de calcul nommée `Feuil1`:

```go
rows, err := f.GetRows("Feuil1")
if err != nil {
    fmt.Println(err)
    return
}
for _, row := range rows {
    for _, colCell := range row {
        fmt.Print(colCell, "\t")
    }
    fmt.Println()
}
```

## Obtenir un lien hypertexte {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, cell string) (bool, string, error)
```

Obtient un lien hypertexte de cellule basé sur le nom de feuille de calcul donné et les coordonnées de cellule. Si la cellule a un lien hypertexte, elle retournera `true` et l'adresse du lien, sinon elle retournera `false` et une adresse de lien vide.

Par exemple, obtenez un lien hypertexte vers une cellule `H6` sur une feuille de calcul nommée `Feuil1`:

```go
link, target, err := f.GetCellHyperLink("Feuil1", "H6")
```

## Obtenir l'index de style {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, cell string) (int, error)
```

L'index de style de cellule est obtenu à partir du nom de feuille de calcul donné et des coordonnées de cellule, et l'index obtenu peut être utilisé comme paramètre pour appeler la fonction `SetCellStyle` lors de la copie du style de cellule.

## Fusionner les cellules {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

Fusionner des cellules en fonction du nom de feuille de calcul donné et des régions de coordonnées de cellule. La fusion de cellules ne conserve que la valeur de la cellule supérieure gauche et ignore les autres valeurs. Par exemple, fusionner des cellules dans la zone `D3:E9` sur une feuille de calcul nommée `Feuil1`:

```go
err := f.MergeCell("Feuil1", "D3", "E9")
```

Si la zone de coordonnées de cellule donnée chevauche d'autres cellules fusionnées existantes, les cellules fusionnées existantes seront supprimées.

## Dissocier les cellules {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

UnmergeCell fournit une fonction pour annuler la fusion d'une zone de coordonnées donnée. Par exemple, annuler la fusion de la zone `D3:E9` sur `Feuil1`:

```go
err := f.UnmergeCell("Feuil1", "D3", "E9")
```

Attention: les zones qui se chevauchent seront également non fusionnées.

## Obtenir les cellules fusionnées {#GetMergeCells}

GetMergeCells fournit une fonction pour obtenir toutes les cellules fusionnées à partir d'une feuille de calcul.

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### Obtenir la valeur de cellule fusionnée

```go
func (m *MergeCell) GetCellValue() string
```

GetCellValue renvoie la valeur de cellule fusionnée.

### Obtenez les coordonnées de la cellule en haut à gauche de la plage fusionnée

```go
func (m *MergeCell) GetStartAxis() string
```

GetStartAxis renvoie les coordonnées de la cellule supérieure gauche de la plage fusionnée, par exemple: `C2`.

### Obtenez les coordonnées de la cellule en bas à droite de la plage fusionnée

```go
func (m *MergeCell) GetEndAxis() string
```

GetEndAxis renvoie les coordonnées de la cellule en bas à droite de la plage fusionnée, par exemple: `D4`.

## Obtenir des cellules d'image {#GetPictureCells}

```go
func (f *File) GetPictureCells(sheet string) ([]string, error)
```

GetPictureCells renvoie toutes les références de cellules d'image dans une feuille de calcul par un nom de feuille de calcul spécifique.

## Ajouter un commentaire {#AddComment}

```go
func (f *File) AddComment(sheet string, comment Comment) error
```

AddComment fournit la méthode pour ajouter un commentaire dans une feuille par index de feuille de calcul, cellule et ensemble de formats donnés (tels que l'auteur et le texte). Notez que la longueur maximale de l'auteur est 255 et la longueur maximale du texte est 32512. Par exemple, ajoutez un commentaire dans `Sheet1!A3`:

<p align="center"><img width="612" src="./images/comment.png" alt="Ajouter un commentaire à un document Excel"></p>

```go
err := f.AddComment("Sheet1", excelize.Comment{
    Cell:   "A3",
    Author: "Excelize",
    Paragraph: []excelize.RichTextRun{
        {Text: "Excelize: ", Font: &excelize.Font{Bold: true}},
        {Text: "Il s'agit d'un commentaire."},
    },
})
```

## Obtenir un commentaire {#GetComments}

```go
func (f *File) GetComments(sheet string) ([]Comment, error)
```

GetComments récupère tous les commentaires d'une feuille de calcul par nom de feuille de calcul donné.

## Supprimer le commentaire {#DeleteComment}

```go
func (f *File) DeleteComment(sheet, cell string) error
```

DeleteComment fournit la méthode pour supprimer un commentaire dans une feuille par feuille de calcul donnée. Par exemple, supprimez le commentaire dans `Feuil1!A30`:

```go
err := f.DeleteComment("Feuil1", "A30")
```

## Formule de définition de cellule {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, cell, formula string, opts ...FormulaOpts) error
```

SetCellFormula fournit une fonction pour définir la formule sur la cellule en fonction du nom de feuille de calcul donné et des paramètres de formule de cellule. Le résultat de la cellule de formule peut être calculé lorsque la feuille de travail est ouverte par l'application Office Excel ou peut utiliser la fonction [CalcCellValue](cell.md#CalcCellValue) peut également obtenir la valeur cellulaire calculée. Si l'application Excel ne calcule pas la formule automatiquement lorsque le classeur a été ouvert, veuillez appeler [UpdateLinkedValue](utils.md#UpdateLinkedValue) après avoir défini les fonctions de formule de cellule.

- Exemple 1, définissez la formule normale `=SUM(A1,B1)` pour la cellule `A3` sur `Feuil1`:

```go
err := f.SetCellFormula("Feuil1", "A3", "=SUM(A1,B1)")
```

- Exemple 2, définissez la formule de tableau de constantes verticales unidimensionnelles (tableau de colonnes) `1;2;3` pour la cellule `A3` sur `Feuil1`:

```go
err := f.SetCellFormula("Feuil1", "A3", "={1;2;3}")
```

- Exemple 3, définissez la formule de tableau constant horizontal unidimensionnel (tableau de lignes) `"a","b","c"` pour la cellule `A3` sur `Feuil1`:

```go
err := f.SetCellFormula("Feuil1", "A3", "={\"a\",\"b\",\"c\"}")
```

- Exemple 4, définissez la formule matricielle constante à deux dimensions `{1,2;"a","b"}` pour la cellule `A3` sur `Feuil1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Feuil1", "A3", "={1,2;\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Exemple 5, définissez la formule matricielle de plage `A1:A2` pour la cellule `A3` sur `Feuil1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Feuil1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Exemple 6, définissez la formule partagée `=A1+B1` pour les cellules `C1:C5` sur `Feuil1`, `C1` est la cellule maître:

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Feuil1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Exemple 7, définissez la formule de table `=SUM(Table1[[A]:[B]])` pour la cellule `C2` sur `Feuil1`:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    if err := f.SetSheetName("Sheet1", "Feuil1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Feuil1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Feuil1",
        &excelize.Table{
            Range:     "A1:C2",
            Name:      "Table1",
            StyleName: "TableStyleMedium2",
        }); err != nil {
        fmt.Println(err)
        return
    }
    formulaType := excelize.STCellFormulaTypeDataTable
    if err := f.SetCellFormula("Feuil1", "C2", "=SUM(Table1[[A]:[B]])",
        excelize.FormulaOpts{Type: &formulaType}); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Classeur1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtenir la formule cellulaire {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, cell string) (string, error)
```

Obtenez la formule sur la cellule en fonction du nom de feuille de calcul donné et des coordonnées de cellule.

## Calculer la valeur de la cellule {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string, opts ...Options) (string, error)
```

CalcCellValue fournit une fonction pour obtenir la valeur de cellule calculée. Cette fonctionnalité est actuellement en cours de traitement. Le calcul itératif, l'intersection implicite, l'intersection explicite, la formule matricielle, la formule de tableau et certaines autres formules ne sont pas pris en charge actuellement.

Formules prises en charge:

Nom de la fonction | Type et description
---|---
ABS                          | Renvoie la valeur absolue d'un nombre
ACCRINT                      | Renvoie l'intérêt couru non échu d'un titre dont l'intérêt est perçu périodiquement
INTERET.ACC.MAT              | Renvoie l'intérêt couru non échu d'un titre dont l'intérêt est perçu à l'échéance
ACOS                         | Renvoie l'arccosinus d'un nombre
ACOSH                        | Renvoie le cosinus hyperbolique inverse d'un nombre
ACOT                         | Renvoie l'arccotangente d'un nombre
ACOTH                        | Renvoie l'arccotangente hyperbolique d'un nombre
AGREGAT                      | Renvoie un agrégat dans une liste ou une base de données
ADRESSE                      | Renvoie une référence sous forme de texte à une seule cellule d'une feuille de calcul
AMORDEGRC                    | Renvoie l'amortissement correspondant à chaque période comptable en utilisant un coefficient d'amortissement
AMORLINC                     | Renvoie l'amortissement correspondant à chaque période comptable
AND                          | Renvoie TRUE si tous les arguments ont la valeur TRUE
ARABIC                       | Convertit un nombre romain en chiffre arabe
TABLEAU.EN.TEXTE             | Renvoie un tableau de valeurs de texte dans une plage spécifiée.
ASIN                         | Renvoie l'arcsinus d'un nombre
ASINH                        | Renvoie le sinus hyperbolique inverse d'un nombre
ATAN                         | Renvoie l'arctangente d'un nombre
ATAN2                        | Renvoie l'arctangente des coordonnées x et y
ATANH                        | Renvoie la tangente hyperbolique inverse d'un nombre
AVEDEV                       | Renvoie la moyenne des écarts absolus des points de données par rapport à leur moyenne
MOYENNE                      | Renvoie la moyenne de ses arguments
AVERAGEA                     | Renvoie la moyenne de ses arguments, y compris les nombres, le texte et les valeurs logiques
MOYENNE.SI                   | Renvoie la moyenne (arithmétique) de toutes les cellules d'une plage respectant un critère donné
AVERAGEIFS                   | Renvoie la moyenne (arithmétique) de toutes les cellules qui répondent à plusieurs critères
BASE                         | Convertit un nombre en représentation textuelle avec la base spécifiée
BESSELI                      | Renvoie la fonction de Bessel modifiée In(x)
BESSELJ                      | Renvoie la fonction de Bessel Jn(x)
BESSELK                      | Renvoie la fonction de Bessel modifiée Kn(x)
BESSELY                      | Renvoie la fonction de Bessel Yn(x)
LOI.BETA                     | Renvoie la fonction de distribution cumulée suivant une loi Bêta. Dans Excel 2007, il s'agit d'une fonction statistique
BETA.DIST                    | Renvoie la fonction de distribution cumulée suivant une loi Bêta
BETA.INVERSE                 | Renvoie l'inverse de la fonction de distribution cumulée pour une distribution bêta spécifiée. Dans Excel 2007, il s'agit d'une fonction statistique
BETA.INV                     | Renvoie l'inverse de la fonction de distribution cumulée pour une distribution bêta spécifiée
BIN2DEC                      | Convertit un nombre binaire en nombre décimal
BINHEX                       | Convertit un nombre binaire en nombre hexadécimal
BINOCT                       | Convertit un nombre binaire en nombre octal
LOI.BINOMIALE                | Renvoie la probabilité d'une variable aléatoire discrète suivant la loi binomiale. Dans Excel 2007, il s'agit d'une fonction statistique
BINOM.DIST                   | Renvoie la probabilité d'une variable aléatoire discrète suivant la loi binomiale
BINOM.DIST.RANGE             | Renvoie la probabilité d'un résultat de tirage en suivant une distribution binomiale
BINOM.INV                    | Renvoie la plus petite valeur pour laquelle la distribution binomiale cumulée est inférieure ou égale à une valeur critère
BITAND                       | Renvoie une opération AND au niveau du bit de deux nombres
BITLSHIFT                    | Renvoie un nombre décalé vers la gauche de total_décalage bits
BITOR                        | Renvoie une opération OR au niveau du bit de deux nombres
BITRSHIFT                    | Renvoie un nombre décalé vers la droite de total_décalage bits
BITXOR                       | Renvoie une opération 'Exclusive Or' de deux nombres
PLAFOND                      | Arrondit un nombre au nombre entier le plus proche ou au multiple le plus proche de l'argument précision en s'éloignant de zéro
CEILING.MATH                 | Arrondit un nombre à l'entier ou au multiple supérieur le plus proche de l'argument de précision
PLAFOND.PRECIS               | Arrondit un nombre à l'entier ou au multiple le plus proche de l'argument de précision. Quel que soit le signe du nombre, le nombre est arrondi à l'unité supérieure
CHAR                         | Renvoie le caractère spécifié par le code numérique
LOI.KHIDEUX                  | Renvoie la probabilité d'une variable aléatoire continue suivant une loi unilatérale du Khi-deux. Dans Excel 2007, il s'agit d'une fonction statistique
KHIDEUX.INVERSE              | Renvoie l'inverse de la probabilité d'une variable aléatoire continue suivant une loi unilatérale du Khi-deux. Dans Excel 2007, il s'agit d'une fonction statistique
TEST.KHIDEUX                 | Renvoie le test d'indépendance.. Dans Excel 2007, il s'agit d'une fonction statistique
CHISQ.DIST                   | Renvoie la fonction de densité de probabilité bêta cumulative
CHISQ.DIST.RT                | Renvoie la probabilité d'une variable aléatoire continue suivant une loi unilatérale du Khi-deux
CHISQ.INV                    | Renvoie la fonction de densité de probabilité bêta cumulative
CHISQ.INV.RT                 | Renvoie l'inverse de la probabilité d'une variable aléatoire continue suivant une loi unilatérale du Khi-deux
CHISQ.TEST                   | Renvoie le test d'indépendance
CHOOSE                       | Choisit une valeur dans une liste de valeurs
CLEAN                        | Supprime tous les caractères non imprimables du texte
CODE                         | Renvoie le code numérique du premier caractère d'une chaîne de texte
COLONNE                      | Renvoie le numéro de colonne d'une référence
COLONNES                     | Renvoie le nombre de colonnes dans une référence
COMBIN                       | Renvoie le nombre de combinaisons pour un nombre d'objets donné
COMBINA                      | Renvoie le nombre de combinaisons avec répétitions pour un nombre d'éléments donné
COMPLEX                      | Convertit des coefficients réels et imaginaires en nombre complexe
CONCAT                       | Combine le texte de plusieurs plages et/ou chaînes, mais ne fournit pas le délimiteur ou les arguments IgnoreEmpty
CONCATENER                   | Regroupe plusieurs éléments textuels en un élément textuel
INTERVALLE.CONFIANCE         | Renvoie l'intervalle de confiance pour la moyenne d'une population. Dans Excel 2007, il s'agit d'une fonction statistique
CONFIDENCE.NORM              | Renvoie l'intervalle de confiance pour la moyenne d'une population
CONFIDENCE.T                 | Renvoie l'intervalle de confiance pour la moyenne d'une population, à l'aide de la probabilité d'une variable aléatoire suivant une loi T de Student
CONVERT                      | Convertit un nombre d'un système de mesure à un autre
COEFFICIENT.CORRELATION      | Renvoie le coefficient de corrélation entre deux séries de données
COS                          | Renvoie le cosinus d'un nombre
COSH                         | Renvoie le cosinus hyperbolique d'un nombre
COT                          | Renvoie le cosinus hyperbolique d'un nombre
COTH                         | Renvoie la cotangente d'un angle
COUNT                        | Compte le nombre de chiffres compris dans la liste d'arguments
NBVAL                        | Compte le nombre de valeurs comprises dans la liste d'arguments
NB.VIDE                      | Compte le nombre de cellules vides dans une plage
NB.SI                        | Compte le nombre de cellules à l'intérieur d'une plage qui répondent aux critères donnés
COUNTIFS                     | Compte le nombre de cellules à l'intérieur d'une plage qui répondent à plusieurs critères
COUPDAYBS                    | Renvoie le nombre de jours entre le début de la période du coupon et la date d'escompte
NB.JOURS.COUPONS             | Renvoie le nombre de jours dans la période du coupon contenant la date d'escompte
NB.JOURS.COUPON.SUIV         | Renvoie le nombre de jours séparant la date d'escompte de la date du prochain coupon
DATE.COUPON.SUIV             | Renvoie la date du prochain coupon suivant la date d'escompte
NB.COUPONS                   | Renvoie le nombre de coupons à régler entre la date d'escompte et la date d'échéance
DATE.COUPON.PREC             | Renvoie la date du coupon antérieur précédant la date d'escompte
COVARIANCE                   | Renvoie la covariance, moyenne des produits des écarts pour chaque série d'observations.. Dans Excel 2007, il s'agit d'une fonction statistique
COVARIANCE.PEARSON           | Renvoie la covariance, moyenne des produits des écarts pour chaque série d'observations
COVARIANCE.STANDARD          | Renvoie la covariance d'échantillon, moyenne des produits des écarts pour chaque paire de points de deux jeux de données
CRITERE.LOI.BINOMIALE        | Renvoie la plus petite valeur pour laquelle la distribution binomiale cumulée est inférieure ou égale à une valeur critère. Dans Excel 2007, il s'agit d'une fonction statistique
CSC                          | Renvoie la cosécante d'un angle
CSCH                         | Renvoie la cosécante hyperbolique d'un angle
CUMUL.INTER                  | Renvoie les intérêts cumulés réglés entre deux périodes
CUMUL.PRINCPER               | Renvoie le montant cumulé du remboursement du capital réglé entre deux périodes
DATE                         | Renvoie le numéro de série d'une date précise
DATEDIF                      | Calcule le nombre de jours, de mois ou d'années qui séparent deux dates. Cette fonction est utile dans les formules où vous devez calculer un âge
DATEVAL                      | Convertit une date au format texte en numéro de série
DAVERAGE                     | Renvoie la moyenne des entrées d'une base de données sélectionnée
DAY                          | Convertit un numéro de série en jour du mois
DAYS                         | Renvoie le nombre de jours entre deux dates
JOURS360                     | Calcule le nombre de jours entre deux dates sur la base d'une année de 360 jours
DB                           | Renvoie l'amortissement d'un bien durant une période spécifiée en utilisant la méthode de l'amortissement dégressif à taux fixe
DCOUNT                       | Compte les cellules qui contiennent des nombres dans une base de données
BDNBVAL                      | Compte les cellules non vides d'une base de données
DDB                          | Renvoie l'amortissement d'un bien durant une période spécifiée suivant la méthode de l'amortissement dégressif à taux double ou selon un coefficient à spécifier
DEC2BIN                      | Convertit un nombre décimal en nombre binaire
DECHEX                       | Convertit un nombre décimal en nombre hexadécimal
DECOCT                       | Convertit un nombre décimal en nombre octal
DECIMAL                      | Convertit une représentation textuelle d'un nombre dans une base donnée en nombre décimal
DEGRES                       | Convertit des radians en degrés
DELTA                        | Vérifie si deux valeurs sont égales
DEVSQ                        | Renvoie la somme des carrés des écarts
DGET                         | Extrait d'une base de données un seul enregistrement correspondant aux critères spécifiés
DISC                         | Renvoie le taux d'escompte d'un titre
DMAX                         | Renvoie la valeur maximale des entrées de base de données sélectionnées
BDMIN                        | Renvoie la valeur minimale des entrées de base de données sélectionnées
DOLLAR                       | Convertit un nombre en texte en utilisant le format monétaire $ (dollar)
DOLLARDE                     | Convertit un prix en dollars, exprimé sous forme de fraction, en un prix en dollars exprimé sous forme de nombre décimal
DPRODUCT                     | Multiplie les valeurs d'un champ particulier dans des enregistrements correspondant aux critères d'une base de données
DSTDEV                       | Calcule l'écart type en fonction d'un échantillon d'entrées de base de données sélectionnées
BDECARTYPEP                  | Calcule l'écart type en fonction de l'ensemble des entrées de base de données sélectionnées
BDSOMME                      | Ajoute les nombres dans la colonne Champ des enregistrements de la base de données correspondant aux critères
DURATION                     | Renvoie la durée annuelle d'un titre dont les intérêts sont perçus périodiquement
DVAR                         | Estime la variance en fonction d'un échantillon d'entrées de base de données sélectionnées
BDVARP                       | Calcule la variance en fonction de l'ensemble des entrées de base de données sélectionnées
EDATE                        | Renvoie le numéro de série de la date qui représente le nombre indiqué de mois précédant ou suivant la date de début
EFFECT                       | Renvoie le taux d'intérêt annuel effectif
URLENCODAGE                  | Renvoie une chaîne codée au format URL. Cette fonction n'est pas disponible dans Excel pour le web
EOMONTH                      | Renvoie le numéro de série du dernier jour du mois précédant ou suivant un nombre de mois spécifié
ERF                          | Renvoie la valeur de la fonction d'erreur
ERF.PRECISE                  | Renvoie la valeur de la fonction d'erreur
ERFC                         | Renvoie la valeur de la fonction d'erreur complémentaire
ERFC.PRECISE                 | Renvoie la valeur de la fonction d'erreur complémentaire comprise entre x et l'infini
ERROR.TYPE                   | Renvoie un nombre correspondant à un type d'erreur
EUROCONVERT                  | convertit un nombre en euros, convertit un nombre en euros en une devise de la zone européenne ou convertit un nombre exprimé en une devise de la zone européenne en une autre, en utilisant l'euro comme intermédiaire (triangulation)
EVEN                         | Arrondit un nombre au nombre entier pair supérieur
EXACT                        | Vérifie si deux valeurs textuelles sont identiques
EXP                          | Renvoie e élevé à la puissance d'un nombre donné
EXPON.DIST                   | Renvoie la distribution exponentielle
LOI.EXPONENTIELLE            | Renvoie la distribution exponentielle. Dans Excel 2007, il s'agit d'une fonction statistique
FACT                         | Renvoie la factorielle d'un nombre
FACTDOUBLE                   | Renvoie la factorielle double d'un nombre
FALSE                        | Renvoie la valeur logique FALSE
F.DIST                       | Renvoie la distribution de probabilité F
LOI.F                        | Renvoie la distribution de probabilité F. Dans Excel 2007, il s'agit d'une fonction statistique
F.DIST.RT                    | Renvoie la distribution de probabilité F
FIND                         | Cherche une valeur textuelle dans une autre (en respectant la casse)
FINDB                        | Cherche une valeur textuelle dans une autre (en respectant la casse)
F.INV                        | Renvoie l'inverse de la distribution de probabilité F
F.INVERT.RT                  | Renvoie l'inverse de la distribution de probabilité F
INVERSE.LOI.F                | Renvoie l'inverse de la distribution de probabilité F. Dans Excel 2007, il s'agit d'une fonction statistique
FISHER                       | Renvoie la transformation de Fisher
FISHER.INVERSE               | Renvoie l'inverse de la transformation de Fisher
FIXED                        | Convertit un nombre en texte avec un nombre de décimales fixe
FLOOR                        | Arrondit un nombre à la valeur d'arrondi la plus proche de zéro. Dans Excel 2007 et Excel 2010, il s'agit d'une fonction mathématique et trigonométrique
FLOOR.MATH                   | Arrondit un nombre à l'entier ou au multiple inférieur le plus proche de l'argument de précision
FLOOR.PRECISE                | Arrondit un nombre à l'entier ou au multiple le plus proche de l'argument de précision. Quel que soit le signe du nombre, le nombre est arrondi à l'unité supérieure
PREVISION                    | Renvoie une valeur par rapport à une tendance linéaire
PREVISION.LINEAIRE           | Renvoie une valeur par rapport à une tendance linéaire
FORMULETEXTE                 | Renvoie la formule à la référence donnée sous forme de texte
FREQUENCE                    | Calcule la fréquence d'apparition des valeurs dans une plage de valeurs, puis renvoie des nombres sous forme de matrice verticale
F.TEST                       | Renvoie le résultat d'un test F
TEST.F                       | Renvoie le résultat d'un test F.. Dans Excel 2007, il s'agit d'une fonction statistique
FV                           | Renvoie la valeur future d'un investissement
VC.PAIEMENTS                 | Renvoie la valeur future d'un investissement en appliquant une série de taux d'intérêt composites
GAMMA                        | Renvoie la valeur de la fonction Gamma
GAMMA.DIST                   | Renvoie la distribution suivant une loi Gamma
LOI.GAMMA                    | Renvoie la distribution suivant une loi Gamma. Dans Excel 2007, il s'agit d'une fonction statistique
GAMMA.INV                    | Renvoie l'inverse de la distribution cumulée suivant une loi Gamma
LOI.GAMMA.INVERSE            | Renvoie l'inverse de la distribution cumulée suivant une loi Gamma. Dans Excel 2007, il s'agit d'une fonction statistique
GAMMALN                      | Renvoie le logarithme népérien de la fonction gamma, Γ(x)
GAMMALN.PRECISE              | Renvoie le logarithme népérien de la fonction gamma, Γ(x)
GAUSS                        | Renvoie 0,5 de moins que la distribution cumulée suivant une loi normale centrée réduite
GCD                          | Renvoie le plus grand diviseur commun
GEOMEAN                      | Renvoie la moyenne géométrique
GESTEP                       | Vérifie si un nombre est supérieur à une valeur seuil
CROISSANCE                   | Calcule des valeurs par rapport à une tendance exponentielle
MOYENNE.HARMONIQUE           | Renvoie la moyenne harmonique
HEX2BIN                      | Convertit un nombre hexadécimal en nombre binaire
HEXDEC                       | Convertit un nombre hexadécimal en nombre décimal
HEXOCT                       | Convertit un nombre hexadécimal en nombre octal
HLOOKUP                      | Cherche dans la première ligne d'un tableau et renvoie la valeur de la cellule indiquée
HOUR                         | Convertit un numéro de série en heure
HYPERLINK                    | Crée un raccourci ou un renvoi qui ouvre un document stocké sur un serveur réseau, un intranet ou Internet
HYPGEOM.DIST                 | Renvoie la distribution suivant une loi hypergéométrique
LOI.HYPERGEOMETRIQUE         | Renvoie la distribution suivant une loi hypergéométrique. Dans Excel 2007, il s'agit d'une fonction statistique
SI                           | Indique un test logique à effectuer
SIERREUR                     | Renvoie une valeur que vous spécifiez si une formule génère une erreur ; sinon, elle renvoie le résultat de la formule
SI.NON.DISP                  | Renvoie la valeur que vous spécifiez si l'expression est résolue à #N/A ; autrement, renvoie le résultat de l'expression
SI.CONDITIONS                | Vérifie si une ou plusieurs conditions sont remplies et renvoie une valeur correspondant à la première condition VRAI
COMPLEXE.MODULE              | Renvoie la valeur absolue (module) d'un nombre complexe
COMPLEXE.IMAGINAIRE          | Renvoie le coefficient imaginaire d'un nombre complexe
COMPLEXE.ARGUMENT            | Renvoie l'argument thêta, un angle exprimé en radians
COMPLEXE.CONJUGUE            | Renvoie le conjugué complexe d'un nombre complexe
COMPLEXE.COS                 | Renvoie le cosinus d'un nombre complexe
IMCOSH                       | Renvoie le cosinus hyperbolique d'un nombre complexe
IMCOT                        | Renvoie la cotangente d'un nombre complexe
IMCSC                        | Renvoie la cosécante d'un nombre complexe
IMCSCH                       | Renvoie la cosécante hyperbolique d'un nombre complexe
COMPLEXE.DIV                 | Renvoie le quotient de deux nombres complexes
COMPLEXE.EXP                 | Renvoie la fonction exponentielle d'un nombre complexe
COMPLEXE.LN                  | Renvoie le logarithme népérien d'un nombre complexe
COMPLEXE.LOG10               | Calcule le logarithme d'un nombre complexe en base 10
COMPLEXE.LOG2                | Calcule le logarithme d'un nombre complexe en base 2
COMPLEXE.PUISSANCE           | Renvoie un nombre complexe élevé à une puissance entière
IMPRODUCT                    | renvoie le produit de plusieurs nombres complexes
IMREAL                       | Renvoie le coefficient réel d'un nombre complexe
IMSEC                        | Renvoie la sécante d'un nombre complexe
IMSECH                       | Renvoie la sécante hyperbolique d'un nombre complexe
COMPLEXE.SIN                 | Renvoie le sinus d'un nombre complexe
IMSINH                       | Renvoie le sinus hyperbolique d'un nombre complexe
COMPLEXE.RACINE              | Renvoie la racine carrée d'un nombre complexe
COMPLEXE.DIFFERENCE          | Renvoie la différence entre deux nombres complexes
COMPLEXE.SOMME               | Renvoie la somme de plusieurs nombres complexes
IMTAN                        | Renvoie la tangente d'un nombre complexe
INDEX                        | Utilise un index pour choisir une valeur provenant d'une référence ou d'une matrice
INDIRECT                     | Renvoie une référence indiquée par une valeur de texte
INFORMATIONS                 | Renvoie des informations sur l'environnement d'exploitation actuel. Cette fonction n'est pas disponible dans Excel pour le web
INT                          | Arrondit un nombre à l'entier inférieur le plus proche
INTRATE                      | Renvoie le taux d'intérêt pour un titre totalement investi
INTPER                       | Renvoie le montant des intérêts d'un investissement pour une période donnée
TRI                          | Renvoie le taux de rendement interne pour une série de mouvements de trésorerie
ESTVIDE                      | Renvoie VRAI si l'argument valeur est vide
ESTERR                       | Renvoie TRUE si la valeur est une valeur d'erreur, sauf #N/A
ESTERREUR                    | Renvoie TRUE si la valeur est une valeur d'erreur
EST.PAIR                     | Renvoie TRUE si le nombre est pair
ISFORMULA                    | Renvoie TRUE s'il existe une référence à une cellule qui contient une formule
ESTLOGIQUE                   | Renvoie TRUE si la valeur est une valeur logique
ESTNA                        | Renvoie TRUE si la valeur est la valeur d'erreur #N/A
ESTNONTEXTE                  | Renvoie TRUE si la valeur n'est pas textuelle
ESTNUM                       | Renvoie TRUE si la valeur est un nombre
EST.IMPAIR                   | Renvoie TRUE si le nombre est impair
ESTREF                       | Renvoie TRUE si la valeur est une référence
ESTTEXTE                     | Renvoie TRUE si la valeur est textuelle
ISO.CEILING                  | Renvoie un nombre arrondi à l'entier ou au multiple supérieur le plus proche de l'argument de précision
ISOWEEKNUM                   | Renvoie le numéro de la semaine ISO de l'année pour une date donnée
ISPMT                        | Calcule le montant des intérêts payés au cours d'une période spécifique d'un investissement
KURT                         | Renvoie le kurtosis d'un jeu de données
GRANDE.VALEUR                | Renvoie la k-ième plus grande valeur d'un jeu de données
LCM                          | Renvoie le plus petit dénominateur commun
LEFT                         | Renvoie les caractères les plus à gauche d'une valeur textuelle
LEFTB                        | Renvoie les caractères les plus à gauche d'une valeur textuelle
NBCAR                        | Renvoie le nombre de caractères dans une chaîne de texte
LENB                         | Renvoie le nombre de caractères dans une chaîne de texte
LN                           | Renvoie le logarithme népérien d'un nombre
LOG                          | Renvoie le logarithme d'un nombre selon la base spécifiée
LOG10                        | Renvoie le logarithme d'un nombre en base 10
LOI.LOGNORMALE.INVERSE       | Renvoie l'inverse de la distribution cumulée suivant une loi lognormale
LOGNORM.DIST                 | Renvoie la distribution suivant une loi lognormale cumulée
LOI.LOGNORMALE               | Renvoie la distribution suivant une loi lognormale cumulée
LOGNORM.INV                  | Renvoie l'inverse de la distribution cumulée suivant une loi lognormale
LOOKUP                       | Cherche des valeurs dans un vecteur ou un tableau
LOWER                        | Convertit le texte en minuscules
EQUIV                        | Cherche des valeurs dans une référence ou un tableau
MAX                          | Renvoie la valeur maximale contenue dans une liste d'arguments
MAXA                         | Renvoie la valeur maximale contenue dans une liste d'arguments, y compris les nombres, le texte et les valeurs logiques
MAX.SI.ENS                   | Renvoie la valeur maximale parmi les cellules spécifiées par un ensemble de conditions ou critères
DETERMAT                     | Renvoie le déterminant d'une matrice
MDURATION                    | Renvoie la durée modifiée de Macauley pour un titre avec une valeur estimée à 100 dollars
MEDIAN                       | Renvoie la valeur médiane des nombres donnés
MID                          | Renvoie un nombre déterminé de caractères d'une chaîne de texte en commençant à la position indiquée
MIDB                         | Renvoie un nombre déterminé de caractères d'une chaîne de texte en commençant à la position indiquée
MIN                          | Renvoie la valeur minimale contenue dans une liste d'arguments
MIN.SI                       | Renvoie la valeur minimale parmi les cellules spécifiées par un ensemble de conditions ou critères
MINA                         | Renvoie la plus petite valeur contenue dans une liste d'arguments, y compris les nombres, le texte et les valeurs logiques
MINUTE                       | Convertit un numéro de série en minute
INVERSEMAT                   | Renvoie la matrice inverse d'une matrice
MIRR                         | Renvoie le taux de rendement interne lorsque des mouvements de trésorerie positifs et négatifs sont financés à des taux différents
PRODUITMAT                   | Renvoie le produit de deux matrices
MOD                          | Renvoie le reste d'une division
MODE                         | Renvoie la valeur la plus courante d'une série de données.. Dans Excel 2007, il s'agit d'une fonction statistique
MODE.MULTIPLE                | Renvoie une matrice verticale des valeurs les plus fréquentes ou répétitives dans une matrice ou une plage de données
MODE.SIMPLE                  | Renvoie la valeur la plus courante d'une série de données
MONTH                        | Convertit un numéro de série en mois
MROUND                       | Renvoie un nombre arrondi au dénominateur souhaité
MULTINOMIALE                 | Calcule la multinomiale d'un ensemble de nombres
MATRICE.UNITAIRE             | Renvoie la matrice unitaire ou la dimension spécifiée
N                            | Renvoie une valeur convertie en nombre
NA                           | Renvoie la valeur d'erreur #N/A
NEGBINOM.DIST                | Renvoie la distribution négative binomiale
LOI.BINOMIALE.NEG            | Renvoie la distribution négative binomiale. Dans Excel 2007, il s'agit d'une fonction statistique
NETWORKDAYS                  | Renvoie le nombre de jours ouvrés entiers entre deux dates
NETWORKDAYS.INTL             | Renvoie le nombre de jours ouvrés entiers compris entre deux dates à l'aide de paramètres indiquant le nombre de jours compris dans un week-end
NOMINAL                      | Renvoie le taux d'intérêt nominal annuel
NORM.DIST                    | Renvoie la distribution cumulée suivant une loi normale
LOI.NORMALE                  | Renvoie la distribution cumulée suivant une loi normale. Dans Excel 2007, il s'agit d'une fonction statistique
LOI.NORMALE.INVERSE          | Renvoie l'inverse de la distribution cumulée suivant une loi normale
NORM.INV                     | Renvoie l'inverse de la distribution cumulée suivant une loi normale. Dans Excel 2007, il s'agit d'une fonction statistique
NORM.S.DIST                  | Renvoie la distribution cumulée suivant une loi normale centrée réduite
LOI.NORMALE.STANDARD         | Renvoie la distribution cumulée suivant une loi normale centrée réduite. Dans Excel 2007, il s'agit d'une fonction statistique
NORM.S.INV                   | Renvoie l'inverse de la distribution cumulée suivant une loi normale centrée réduite
LOI.NORMALE.STANDARD.INVERSE | Renvoie l'inverse de la distribution cumulée suivant une loi normale centrée réduite. Dans Excel 2007, il s'agit d'une fonction statistique
NOT                          | Inverse la logique de son argument
NOW                          | Renvoie le numéro de série de la date et de l'heure actuelles
NPM                          | Renvoie le nombre de paiements d'un investissement
VAN                          | Renvoie la valeur nette actuelle d'un investissement, en fonction d'une série de flux de trésorerie périodiques et d'un taux d'escompte
OCT2BIN                      | Convertit un nombre octal en nombre binaire
OCTDEC                       | Convertit un nombre octal en nombre décimal
OCTHEX                       | Convertit un nombre octal en nombre hexadécimal
IMPAIR                       | Arrondit un nombre à l'entier impair supérieur le plus proche
PRIX.PCOUPON.IRREG           | Renvoie le prix par valeur faciale de 100 dollars d'un titre dont la première période est irrégulière
REND.PCOUPON.IRREG           | Renvoie le rendement d'un titre dont la première période est irrégulière
PRIX.DCOUPON.IRREG           | Renvoie le prix par valeur faciale de 100 dollars d'un titre dont la dernière période est irrégulière
REND.DCOUPON.IRREG           | Renvoie le rendement d'un titre dont la dernière période est irrégulière
OU                           | Renvoie TRUE si un argument a la valeur TRUE
PDURATION                    | Renvoie le nombre de périodes requises par un investissement pour atteindre une valeur spécifiée
PEARSON                      | Renvoie le coefficient de corrélation d'échantillonnage de Pearson
PERCENTILE.EXC               | Renvoie le k-ième centile de valeur d'une plage, où k se trouve dans la plage de 0 à 1 exclus
PERCENTILE.INC               | Renvoie le k-ième centile des valeurs d'une plage
CENTILE                      | Renvoie le k-ième centile des valeurs d'une plage. Dans Excel 2007, il s'agit d'une fonction statistique
PERCENTRANK.EXC              | Renvoie le rang d'une valeur dans un ensemble de données défini comme pourcentage (0..1, exclus) de cet ensemble
PERCENTRANK.INC              | Renvoie le rang en pourcentage d'une valeur dans un jeu de données
RANG.POURCENTAGE             | Renvoie le rang en pourcentage d'une valeur dans un jeu de données. Dans Excel 2007, il s'agit d'une fonction statistique
PERMUT                       | Renvoie le nombre de permutations pour un nombre d'objets donné
PERMUTATIONA                 | Renvoie le nombre de permutations pour un nombre d'objets donné (avec répétitions) pouvant être sélectionnés à partir du nombre total d'objets
PHI                          | Renvoie la valeur de la fonction de densité pour une distribution suivant une loi normale centrée réduite
PI                           | Renvoie la valeur de pi
PMT                          | Renvoie le montant périodique d'une annuité
POISSON.DIST                 | Renvoie la distribution suivant une loi de Poisson
LOI.POISSON                  | Renvoie la distribution suivant une loi de Poisson. Dans Excel 2007, il s'agit d'une fonction statistique
POWER                        | Renvoie le résultat d'un nombre élevé à une puissance
PPMT                         | Renvoie la part de remboursement du principal d'un emprunt pour une période donnée
PRIX.TITRE                   | Renvoie le prix par valeur faciale de 100 dollars d'un titre dont les intérêts sont payés périodiquement
VALEUR.ENCAISSEMENT          | Renvoie le prix par valeur faciale de 100 dollars pour un titre escompté
PRIX.TITRE.ECHEANCE          | Renvoie le prix par valeur faciale de 100 dollars d'un titre dont les intérêts sont payés à échéance
PROBABILITE                  | Renvoie la probabilité que des valeurs dans une plage soient comprises entre deux limites
PRODUIT                      | Multiplie ses arguments
NOMPROPRE                    | Met en majuscule la première lettre de chaque mot d'une valeur textuelle
VA                           | Renvoie la valeur actuelle d'un investissement
QUARTILE                     | Renvoie le quartile d'un jeu de données. Dans Excel 2007, il s'agit d'une fonction statistique
QUARTILE.EXCLURE             | Renvoie le quartile de l'ensemble de données d'après des valeurs de centile comprises entre 0 et 1, exclus
QUARTILE.INCLURE             | Renvoie le quartile d'un jeu de données
QUOTIENT                     | Renvoie la partie entière d'une division
RADIANS                      | Convertit des degrés en radians
ALEA                         | Renvoie un nombre aléatoire compris entre 0 et 1
ALEA.ENTRE.BORNES            | Renvoie un nombre aléatoire entre les nombres que vous spécifiez
RANK.EQ                      | Renvoie le rang d'un nombre dans une liste de nombres
RANG                         | Renvoie le rang d'un nombre dans une liste de nombres. Dans Excel 2007, il s'agit d'une fonction statistique
RATE                         | Renvoie le taux d'intérêt par période pour une annuité
VALEUR.NOMINALE              | Renvoie le montant reçu lorsqu'un titre totalement investi arrive à échéance
REPLACE                      | Remplace des caractères dans un texte
REPLACEB                     | Remplace des caractères dans un texte
REPT                         | Répète un texte un certain nombre de fois
DROITE                       | Renvoie les caractères les plus à droite d'une valeur textuelle
DROITEB                      | Renvoie les caractères les plus à droite d'une valeur textuelle
ROMAN                        | convertit des chiffres arabes en chiffres romains, sous forme de texte
ROUND                        | Arrondit un nombre à un nombre de chiffres spécifié
ARRONDI.INF                  | Arrondit un nombre à la valeur d'arrondi la plus proche de zéro
ARRONDI.SUP                  | Arrondit un nombre à la valeur d'arrondi la plus éloignée de zéro
LIGNE                        | Renvoie le numéro de ligne d'une référence
LIGNES                       | Renvoie le nombre de lignes dans une référence
RRI                          | Renvoie un taux d'intérêt équivalent pour la croissance d'un investissement
COEFFICIENT.DETERMINATION    | Renvoie la valeur du coefficient de détermination R^2 d'une régression linéaire
CHERCHE                      | Trouve un texte dans un autre texte (sans respecter la casse)
CHERCHERB                    | Trouve un texte dans un autre texte (sans respecter la casse)
SEC                          | Renvoie la sécante d'un angle
SECH                         | Renvoie la sécante hyperbolique d'un angle
SECOND                       | Convertit un numéro de série en seconde
SERIESSUM                    | Renvoie le total d'une série de puissance basé sur la formule
SHEET                        | Renvoie le numéro de la feuille référencée
SHEETS                       | Renvoie le nombre de feuilles dans une référence
SIGN                         | Renvoie le signe d'un nombre
SIN                          | Renvoie le sinus d'un angle donné
SINH                         | Renvoie le sinus hyperbolique d'un nombre
SKEW                         | Renvoie l'asymétrie d'une distribution
SKEW.P                       | Renvoie l'asymétrie d'une distribution en fonction d'une population : la caractérisation du degré d'asymétrie d'une distribution par rapport à sa moyenne
SLN                          | Renvoie l'amortissement linéaire d'une immobilisation pour une période
PENTE                        | Renvoie la pente d'une droite de régression linéaire
PETITE.VALEUR                | Renvoie la k-ième plus petite valeur d'un jeu de données
SQRT                         | Renvoie une racine carrée positive
RACINE.PI                    | Renvoie la racine carrée de (nombre \* pi)
STANDARDIZE                  | Renvoie une valeur normalisée
ECARTYPE                     | Évalue l'écart type en fonction d'un échantillon
ECARTYPE.PEARSON             | Calcule l'écart type en fonction de la population entière
ECARTYPE.STANDARD            | Évalue l'écart type en fonction d'un échantillon
STDEVA                       | Évalue l'écart type en fonction d'un échantillon, y compris les nombres, le texte et les valeurs logiques
ECARTYPEP                    | Calcule l'écart type en fonction de la population entière. Dans Excel 2007, il s'agit d'une fonction statistique
STDEVPA                      | Calcule l'écart type en fonction de la population entière, y compris les nombres, le texte et les valeurs logiques
ERREUR.TYPE.XY               | Renvoie l'erreur type de la valeur y prévue pour chaque x de la régression
SUBSTITUTE                   | Remplace le nouveau texte par l'ancien texte d'une chaîne de texte
SUBTOTAL                     | Renvoie un sous-total dans une liste ou une base de données
SOMME                        | Ajoute ses arguments
SOMME.SI                     | Ajoute les cellules spécifiées par un critère donné
SUMIFS                       | Ajoute les cellules d'une plage répondant à plusieurs critères
SOMMEPROD                    | Multiplie les valeurs correspondantes des matrices spécifiées et calcule la somme de ces produits
SOMME.CARRES                 | Renvoie le total des carrés des arguments
SOMME.X2MY2                  | Renvoie la somme de la différence des carrés des valeurs correspondantes de deux matrices
SOMME.X2PY2                  | Renvoie la somme de la somme des carrés des valeurs correspondantes de deux matrices
SOMME.XMY2                   | Renvoie la somme des carrés des différences entre les valeurs correspondantes de deux matrices
SI.MULTIPLE                  | Évalue une expression par rapport à une liste de valeurs et renvoie le résultat correspondant à la première valeur correspondante. S'il n'y a pas de correspondance, une valeur par défaut facultative peut être renvoyée
SYD                          | Renvoie l'amortissement des chiffres cumulés sur l'année d'une immobilisation pour une période spécifique
T                            | Convertit ses arguments en texte
TAN                          | Renvoie la tangente d'un nombre
TANH                         | Renvoie la tangente hyperbolique d'un nombre
TAUX.ESCOMPTE.R              | Renvoie un nombre spécifié de lignes ou de colonnes contiguës à partir du début ou de la fin du tableau
PRIX.BON.TRESOR              | Renvoie le prix par valeur faciale de 100 dollars pour un bon du Trésor
RENDEMENT.BON.TRESOR         | Renvoie le rapport pour un bon du Trésor
T.DIST                       | Renvoie les points de pourcentage (probabilité) pour la distribution suivant la loi T de Student
T.DIST.2T                    | Renvoie les points de pourcentage (probabilité) pour la distribution suivant la loi T de Student
T.DIST.RT                    | Renvoie la distribution suivant la loi T de Student
LOI.STUDENT                  | Renvoie la distribution suivant la loi T de Student
TEXTE                        | Met en forme un nombre et le convertit en texte
TEXTEAPRES                   | Retourne le texte qui se trouve après le caractère ou la chaîne de caractères donnés
TEXTEAVANT                   | Retourne le texte qui se trouve avant un caractère ou une chaîne de caractères donnés
JOINDRE.TEXTE                | Combiner le texte de plusieurs plages et/ou chaînes
TEMPS                        | Renvoie le numéro de série d'une heure précise
TEMPSVAL                     | Convertit une heure au format texte en numéro de série
T.INV                        | Renvoie la valeur t de la distribution suivant la loi T de Student sous forme de fonction de probabilité et de degrés de liberté
T.INV.2T                     | Renvoie l'inverse de la distribution suivant la loi T de Student
LOI.STUDENT.INVERSE          | Renvoie l'inverse de la distribution suivant la loi T de Student
AUJOURDHUI                   | Renvoie le numéro de série de la date du jour
TRANSPOSE                    | Renvoie la transposition d'une matrice
TENDANCE                     | Renvoie des valeurs par rapport à une tendance linéaire
TRIM                         | Supprime les espaces du texte
TRIMMEAN                     | Renvoie la moyenne de la partie intérieure d'un jeu de données
TRUE                         | Renvoie la valeur logique TRUE
TRUNC                        | Tronque un nombre en entier
T.TEST                       | Renvoie la probabilité associée à un test T de Student
TEST.STUDENT                 | Renvoie la probabilité associée à un test T de Student.. Dans Excel 2007, il s'agit d'une fonction statistique
TYPE                         | Renvoie un nombre indiquant le type de données d'une valeur
UNICHAR                      | Renvoie le caractère unicode référencé par la valeur numérique donnée
UNICODE                      | Renvoie le nombre (point de code) qui correspond au premier caractère du texte
UPPER                        | Convertit le texte en majuscules
CNUM                         | Convertit un argument textuel en nombre
VALEUR.EN.TEXTE              | Renvoie le texte de toute valeur spécifiée
VAR                          | Fournit une estimation de l'écart à partir d'un échantillon. Dans Excel 2007, il s'agit d'une fonction statistique
VAR.P                        | Calcule l'écart en fonction de la population entière
VAR.S                        | Fournit une estimation de l'écart à partir d'un échantillon
VARA                         | Évalue la varianceen fonction d'un échantillon, y compris les nombres, le texte et les valeurs logiques
VAR.P                        | Calcule l'écart en fonction de la population entière. Dans Excel 2007, il s'agit d'une fonction statistique
VARPA                        | Calcule la variance en fonction de la population entière, y compris les nombres, le texte et les valeurs logiques
VDB                          | Renvoie l'amortissement d'un bien durant une période spécifiée ou partielle en utilisant une méthode d'amortissement dégressif
VLOOKUP                      | Cherche dans la première colonne d'un tableau et se déplace horizontalement pour renvoyer la valeur d'une cellule
JOURSEM                      | Ajoute des tableaux verticalement et en séquence pour renvoyer un tableau plus grand
NO.SEMAINE                   | Convertit un numéro de série en un numéro de semaine correspondant à l'année
LOI.WEIBULL                  | Calcule la variance en fonction de la population entière, y compris les nombres, le texte et les valeurs logiques. Dans Excel 2007, il s'agit d'une fonction statistique
WEIBULL.DIST                 | Renvoie la distribution suivant la loi de Weibull
SERIE.JOUR.OUVRE             | Renvoie le numéro de série de la date précédant ou suivant un nombre de jours ouvrés spécifié
WORKDAY.INTL                 | Renvoie le numéro de série de la date précédant ou suivant un nombre spécifié de jours ouvrés à l'aide de paramètres indiquant le nombre de jours compris dans un week-end
TRI.PAIEMENTS                | Renvoie le taux de rendement interne d'une planification de flux financiers qui n'est pas nécessairement périodique
RECHERCHEX                   | Recherche une plage ou une matrice et renvoie un élément correspondant à la première correspondance qu'elle trouve. Si une correspondance n'existe pas, la recherche X peut renvoyer la correspondance la plus proche (approximative)
VAN.PAIEMENTS                | Renvoie la valeur actuelle nette d'une planification de flux financiers qui n'est pas nécessairement périodique
XOR                          | Renvoie une valeur logique exclusive OR de tous les arguments
ANNEE                        | Convertit un numéro de série en année
FRACTION.ANNEE               | Renvoie la fraction de l'année représentant le nombre de jours entiers compris entre start_date et end_date
YIELD                        | Renvoie le rendement d'un titre rapportant des intérêts périodiquement
RENDEMENT.SIMPLE             | Renvoie le rendement annuel d'un titre escompté, par exemple, un bon du Trésor
RENDEMENT.TITRE.ECHEANCE     | Renvoie le rendement annuel d'un titre pour lequel des intérêts sont payés à l'échéance
Z.TEST                       | Renvoie la valeur de probabilité unilatérale du test Z
TEST.Z                       | Renvoie la valeur de probabilité unilatérale du test Z. Dans Excel 2007, il s'agit d'une fonction statistique

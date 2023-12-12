# Graphique

## Ajouter un graphique {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChart fournit la méthode pour ajouter un graphique dans une feuille en fonction d'un ensemble de formats de graphique donné (tel que le décalage, l'échelle, le paramètre de rapport d'aspect et les paramètres d'impression) et le jeu de propriétés.

Voici le `Type` de graphique supporté par excelize:

ID|Énumération|Graphique
---|---|---
0  | Area                        | 2D graphique à aires
1  | AreaStacked                 | 2D graphique à aires empilées
2  | AreaPercentStacked          | 2D 100% graphique à aires empilées
3  | Area3D                      | 3D graphique à aires
4  | Area3DStacked               | 3D graphique à aires empilées
5  | Area3DPercentStacked        | 3D 100% graphique à aires empilées
6  | Bar                         | 2D graphique à barres en cluster
7  | BarStacked                  | 2D graphique à barres empilées
8  | BarPercentStacked           | 2D 100% graphique à barres empilées
9  | Bar3DClustered              | 3D graphique à barres en cluster
10 | Bar3DStacked                | 3D graphique à barres empilées
11 | Bar3DPercentStacked         | 3D 100% graphique à barres empilées
12 | Bar3DConeClustered          | 3D graphique à barres groupée de cône
13 | Bar3DConeStacked            | 3D graphique à barres empilés de cône
14 | Bar3DConePercentStacked     | 3D graphique à barres cône
15 | Bar3DPyramidClustered       | 3D graphique à barres groupée pyramide
16 | Bar3DPyramidStacked         | 3D graphique de barre empilé de pyramide
17 | Bar3DPyramidPercentStacked  | 3D 100% graphique à barres empilées pyramide
18 | Bar3DCylinderClustered      | 3D graphique à barres groupée de cylindres
19 | Bar3DCylinderStacked        | 3D graphique à barres empilés de cylindre
20 | Bar3DCylinderPercentStacked | 3D 100% graphique à barres cylindre empilées
21 | Col                         | 2D tableau à colonnes groupées
22 | ColStacked                  | 2D graphique à colonnes empilées
23 | ColPercentStacked           | 2D 100% graphique à colonnes empilées
24 | Col3D                       | 3D graphique à colonnes
25 | Col3DClustered              | 3D tableau à colonnes groupées
26 | Col3DStacked                | 3D graphique à colonnes empilées
27 | Col3DPercentStacked         | 3D 100% graphique à colonnes empilées
28 | Col3DCone                   | 3D graphique de colonne de cône
29 | Col3DConeClustered          | 3D graphique de colonne groupé de cône
30 | Col3DConeStacked            | 3D graphique de colonne empilé de cône
31 | Col3DConePercentStacked     | 3D 100% graphique de colonne empilé cône empilé
32 | Col3DPyramid                | 3D graphique de colonne de pyramide
33 | Col3DPyramidClustered       | 3D graphique de colonne groupé de pyramide
34 | Col3DPyramidStacked         | 3D graphique de colonne empilé de pyramide
35 | Col3DPyramidPercentStacked  | 3D 100% graphique de colonne empilée pyramide
36 | Col3DCylinder               | 3D graphique de colonne de cylindre
37 | Col3DCylinderClustered      | 3D graphique de colonne groupé de cylindre
38 | Col3DCylinderStacked        | 3D graphique de colonne empilé de cylindre
39 | Col3DCylinderPercentStacked | 3D 100 graphique de colonne cylindre empilé
40 | Doughnut                    | tableau de donut
41 | Line                        | graphique en ligne
42 | Line3D                      | 3D graphique en ligne
43 | Pie                         | graphique tarte
44 | Pie3D                       | 3D graphique tarte
45 | PieOfPie                    | double du camembert
46 | BarOfPie                    | barre de camembert
47 | Radar                       | graphique radar
48 | Scatter                     | graphique de dispersion
49 | Surface3D                   | 3D graphique de surface
50 | WireframeSurface3D          | 3D graphique de surface de fil
51 | Contour                     | graphique de contour
52 | WireframeContour            | graphique de contour de trame de fil
53 | Bubble                      | graphique à bulles
54 | Bubble3D                    | 3D graphique à bulles

Dans la zone de données de graphique Office Excel `Series` spécifie l'ensemble des informations pour lesquelles les données doivent être dessinées, l'élément de légende (série) et l'étiquette d'axe horizontal (catégorie).

Les options `Series` qui peuvent être définies sont:

Paramètre|Explication
---|---
Name|Élément de légende (série), affiché dans la légende du graphique et la barre de formule. Le paramètre `Name` est facultatif. Si vous ne spécifiez pas cette valeur, la valeur par défaut sera `Series 1 .. n`. Support `Name` pour la représentation de la formule, par exemple: `Sheet1!$A$1`.
Categories|Etiquette d'axe horizontal (catégorie). Le paramètre `Categories` est facultatif dans la plupart des types de graphiques, la valeur par défaut est une séquence contiguë de la forme `1..n`.
Values|La zone de données de graphique, qui est le paramètre le plus important dans `Series`, est également le seul paramètre requis lors de la création d'un graphique. Cette option lie le graphique aux données de la feuille de calcul qu'il affiche.
Line|Ceci définit le format de ligne du graphique en courbes. La propriété `Line` est facultative et si elle n'est pas fournie, le style par défaut. Les options pouvant être définies sont `Width`. La plage de `Width` est comprise entre 0.25 et 999 pt. Si la valeur de width est en dehors de la plage, la largeur par défaut de la ligne est de 2 pt.
Marker|Ceci définit le marqueur du graphique linéaire et du nuage de points. La plage du champ facultatif `Size` est comprise entre 2 et 72 (la valeur par défaut est `5`). La valeur d'énumération du champ facultatif `Symbol` est (la valeur par défaut est `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

Définir les propriétés de la légende du graphique. Les options qui peuvent être définies sont:

Paramètre|Type|Explication
---|---|---
Position        | `string` | La position de la légende du graphique
ShowLegendKey   | `bool`   | Définir les clés de légende doivent être affichées dans les étiquettes de données

Définissez la `Position` de la légende du graphique. La position par défaut de la légende est `right`. Les postes disponibles sont:

Paramètre|Explication
---|---
none|Désactiver la légende
top|En haut
bottom|Au fond
left|Sur la gauche
right|Sur la droite
top_right|En haut à droite

Le paramètre `ShowLegendKey`  défini les clés de légende doit être affiché dans les étiquettes de données. La valeur par défaut est `false`.

Le titre du graphique est défini en sélectionnant le paramètre `Name` de l'objet `Title` et le titre sera affiché au-dessus du graphique. Le paramètre `Name` prend en charge l'utilisation de représentations de formules, telles que `Sheet1!$A$1`, si vous ne spécifiez pas de titre d'icône, la valeur par défaut est null.

Le paramètre `ShowBlanksAs` fournit le paramètre "Hide and empty cells". La valeur par défaut est: `gap`. Dans l'application Excel "cellule vide est affiché comme": "espace". Les valeurs suivantes sont des valeurs facultatives pour ce paramètre:

Paramètre|Explication
---|---
gap|espace
span|Connecter des points de données avec des lignes droites
zero|zvaleur zéro

Spécifie que chaque marqueur de données de la série a une couleur différente par `VaryColors`. La valeur par défaut est `true`.

Le paramètre `Format` fournit des paramètres pour des paramètres tels que le décalage de diagramme, l'échelle, les paramètres de format et les propriétés d'impression, ainsi que ceux utilisés dans la fonction [`AddPicture`](image.md#AddPicture).

Définissez la position de la zone de tracé de graphique par plotarea. Les propriétés qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
ShowBubbleSize  | `bool` | `false` | Spécifie que la taille de la bulle doit apparaître dans une étiquette de données.
ShowCatName     | `bool` | `false` | Nom de catégorie
ShowLeaderLines | `bool` | `false` | Indique que le nom de la catégorie doit apparaître dans l'étiquette de données.
ShowPercent     | `bool` | `false` | Indique que le pourcentage doit être indiqué dans une étiquette de données.
ShowSerName     | `bool` | `false` | Indique que le nom de la série doit apparaître dans une étiquette de données.
ShowVal         | `bool` | `false` | Indique que la valeur doit apparaître dans une étiquette de données.

Définissez les options de l'axe horizontal et vertical principal par `XAxis` et `YAxis`.

Les propriétés de `XAxis` qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
None           | `bool`          | `false` | Désactiver les axes.
MajorGridLines | `bool`          | `false` | Spécifie les lignes de grille principales.
MinorGridLines | `bool`          | `false` | Spécifie les lignes de grille mineures.
TickLabelSkip  | `int`           | `1`     | Spécifie le nombre d'étiquettes de graduation à ignorer entre les étiquettes dessinées. La propriété `TickLabelSkip` est facultative. La valeur par défaut est auto.
ReverseOrder   | `bool`          | `false` | Spécifie que les catégories ou valeurs dans l'ordre inverse (orientation du graphique). La propriété `ReverseOrder` est facultative.
Maximum        | `*float64`      | `0`     | Indique que le maximum fixé, 0 est auto. La propriété maximum est facultative.
Minimum        | `*float64`      | `0`     | Spécifie que le minimum fixé, 0 est auto. La propriété minimum est facultative. La valeur par défaut est auto.
Font           | `Font`          | N/A     | Spécifie que la police de l'axe horizontal.
NumFmt         | `ChartNumFmt`   | N/A     | Spécifie que s'il est lié à la source et définit le code de format de nombre personnalisé pour l'axe.
Title          | `[]RichTextRun` | N/A     | Spécifie que le titre de l'axe horizontal principal et le graphique de redimensionnement.

Les propriétés de `YAxis` qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
None           | `bool`          | `false` | Désactiver les axes.
MajorGridLines | `bool`          | `false` | Spécifie les lignes de grille principales.
MinorGridLines | `bool`          | `false` | Spécifie les lignes de grille mineures.
MajorUnit      | `float64`       | `0`     | Spécifie la distance entre les graduations principales. Doit contenir un nombre à virgule flottante positif. La propriété `MajorUnit` est facultative. La valeur par défaut est auto.
ReverseOrder   | `bool`          | `false` | Spécifie que les catégories ou valeurs dans l'ordre inverse (orientation du graphique). La propriété `ReverseOrder` est facultative.
Maximum        | `*float64`      | `0`     | Indique que le maximum fixé, 0 est auto. La propriété maximum est facultative.
Minimum        | `*float64`      | `0`     | Spécifie que le minimum fixé, 0 est auto. La propriété minimum est facultative. La valeur par défaut est auto.
Font           | `Font`          | N/A     | Spécifie que la police de l'axe vertical.
LogBase        | `float64`       | N/A     | Spécifie le numéro de base de l'échelle logarithmique de l'axe vertical.
NumFmt         | `ChartNumFmt`   | N/A     | Spécifie que s'il est lié à la source et définit le code de format de nombre personnalisé pour l'axe.
Title          | `[]RichTextRun` | N/A     | Spécifie que le titre de l'axe vertical principal et le graphique de redimensionnement.

Définissez la taille du graphique par la propriété `Dimension`. La propriété dimension est facultative. Les propriétés qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
Height | `uint` | 260 | Hauteur
Width  | `uint` | 480 | Largeur

Le paramètre `combo` spécifie la création d'un graphique qui combine deux ou plusieurs types de graphiques dans un seul graphique. Par exemple, créez un graphique à colonnes groupées avec des données `Sheet1!$E$1:$L$15`:

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
    for idx, row := range [][]interface{}{
        {nil, "Apple", "Orange", "Pear"},
        {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Large", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Feuil1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Feuil1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Feuil1!$A$2",
                Categories: "Feuil1!$B$1:$D$1",
                Values:     "Feuil1!$B$2:$D$2",
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Title: []excelize.RichTextRun{
            {
                Text: "2D tableau à colonnes groupées - graphique en ligne",
            },
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }, &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Feuil1!$A$4",
                Categories: "Feuil1!$B$1:$D$1",
                Values:     "Feuil1!$B$4:$D$4",
                Marker: excelize.ChartMarker{
                    Symbol: "none", Size: 10,
                },
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Legend: excelize.ChartLegend{
            Position: "right",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Enregistrer le classeur
    if err := f.SaveAs("Classeur1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Créer une feuille de graphique {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChartSheet fournit la méthode pour créer une feuille de graphique en fonction d'un ensemble de formats de graphique donné (tels que l'offset, l'échelle, le paramètre de rapport hauteur / largeur et les paramètres d'impression) et d'un ensemble de propriétés. Dans Excel, une feuille de graphique est une feuille de calcul qui contient uniquement un graphique.

## Supprimer le graphique {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart fournit une fonction pour supprimer le graphique dans XLSX par feuille de calcul et nom de cellule donnés.

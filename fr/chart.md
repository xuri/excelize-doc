# Graphique

## Ajouter un graphique

```go
func (f *File) AddChart(sheet, cell, format string) error
```

AddChart fournit la méthode pour ajouter un graphique dans une feuille en fonction d'un ensemble de formats de graphique donné (tel que le décalage, l'échelle, le paramètre de rapport d'aspect et les paramètres d'impression) et le jeu de propriétés.

Par exemple, ajoutez un graphique qui ressemble à ceci:

!["Créer un graphique dans un document Excel"](./images/chart.png "Créer un graphique dans un document Excel")

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    categories := map[string]string{"A2": "Small", "A3": "Normal", "A4": "Large", "B1": "Apple", "C1": "Orange", "D1": "Pear"}
    values := map[string]int{"B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    xlsx := excelize.NewFile()
    for k, v := range categories {
        xlsx.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        xlsx.SetCellValue("Sheet1", k, v)
    }
    err := xlsx.AddChart("Sheet1", "E1", `{"type":"col3DClustered","series":[{"name":"Sheet1!$A$2","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$2:$D$2"},{"name":"Sheet1!$A$3","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$3:$D$3"},{"name":"Sheet1!$A$4","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$4:$D$4"}],"format":{"x_scale":1.0,"y_scale":1.0,"x_offset":15,"y_offset":10,"print_obj":true,"lock_aspect_ratio":false,"locked":false},"legend":{"position":"bottom","show_legend_key":false},"title":{"name":"Fruit 3D Clustered Column Chart"},"plotarea":{"show_bubble_size":true,"show_cat_name":false,"show_leader_lines":false,"show_percent":true,"show_series_name":true,"show_val":true},"show_blanks_as":"zero","x_axis":{"reverse_order":true},"y_axis":{"maximum":7.5,"minimum":0.5}}`)
    if err != nil {
        fmt.Println(err)
    }
    // Enregistrer le classeur
    err = xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

Voici le `type` de graphique supporté par excelize:

Type|Graphique
---|---
bar                 | 2D graphique à barres en cluster
barStacked          | 2D graphique à barres empilées
barPercentStacked   | 2D 100% graphique à barres empilées
bar3DClustered      | 3D graphique à barres en cluster
bar3DStacked        | 3D graphique à barres empilées
bar3DPercentStacked | 3D 100% graphique à barres empilées
col                 | 2D tableau à colonnes groupées
colStacked          | 2D graphique à colonnes empilées
colPercentStacked   | 2D 100% graphique à colonnes empilées
col3DClustered      | 3D tableau à colonnes groupées
col3D               | 3D graphique à colonnes
col3DStacked        | 3D graphique à colonnes empilées
col3DPercentStacked | 3D 100% graphique à colonnes empilées
doughnut            | tableau de donut
line                | graphique en ligne
pie                 | graphique tarte
pie3D               | 3D graphique tarte
radar               | graphique radar
scatter             | graphique de dispersion

Dans la zone de données de graphique Office Excel `series` spécifie l'ensemble des informations pour lesquelles les données doivent être dessinées, l'élément de légende (série) et l'étiquette d'axe horizontal (catégorie).

Les options `series` qui peuvent être définies sont:

Paramètre|Explication
---|---
name|Élément de légende (série), affiché dans la légende du graphique et la barre de formule. Le paramètre `name` est facultatif. Si vous ne spécifiez pas cette valeur, la valeur par défaut sera `Series 1 .. n`. Support `name` pour la représentation de la formule, par exemple: `Sheet1!$A$1`.
categories|Etiquette d'axe horizontal (catégorie). Le paramètre `categories` est facultatif dans la plupart des types de graphiques, la valeur par défaut est une séquence contiguë de la forme `1..n`.
values|La zone de données de graphique, qui est le paramètre le plus important dans `series`, est également le seul paramètre requis lors de la création d'un graphique. Cette option lie le graphique aux données de la feuille de calcul qu'il affiche.

Définir les propriétés de la légende du graphique. Les options qui peuvent être définies sont:

Paramètre|Type|Explication
---|---|---
position|string|La position de la légende du graphique
show_legend_key|bool|Afficher la légende sans chevauchement avec le graphique

Définissez la `position` de la légende du graphique. La position de la légende par défaut est `right`. Les postes disponibles sont:

Paramètre|Explication
---|---
top|En haut
bottom|Au fond
left|Sur la gauche
right|Sur la droite
top_right|En haut à droite

Le paramètre `show_legend_key` défini les clés de légende doit être affiché dans les étiquettes de données. La valeur par défaut est `false`.

Le titre du graphique est défini en sélectionnant le paramètre `name` de l'objet `title` et le titre sera affiché au-dessus du graphique. Le paramètre `name` prend en charge l'utilisation de représentations de formules, telles que `Sheet1!$A$1`, si vous ne spécifiez pas de titre d'icône, la valeur par défaut est null.

Le paramètre `show_blanks_as` fournit le paramètre "Hide and empty cells". La valeur par défaut est: `gap`. Dans l'application Excel "cellule vide est affiché comme": "espace". Les valeurs suivantes sont des valeurs facultatives pour ce paramètre:


Paramètre|Explication
---|---
gap|espace
span|Connecter des points de données avec des lignes droites
zero|zvaleur zéro

Le paramètre `format` fournit des paramètres pour des paramètres tels que le décalage de diagramme, l'échelle, les paramètres de format et les propriétés d'impression, ainsi que ceux utilisés dans la fonction [`AddPicture()`](image.md#AddPicture).

Définissez la position de la zone de tracé de graphique par plotarea. Les propriétés qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
show_bubble_size|bool|`false`|Spécifie que la taille de la bulle doit apparaître dans une étiquette de données.
show_cat_name|bool|`true`|Nom de catégorie
show_leader_lines|bool|`false`|Indique que le nom de la catégorie doit apparaître dans l'étiquette de données.
show_percent|bool|`false`|Indique que le pourcentage doit être indiqué dans une étiquette de données.
show_series_name|bool|`false`|Indique que le nom de la série doit apparaître dans une étiquette de données.
show_val|bool|`false`|Indique que la valeur doit apparaître dans une étiquette de données.

Définissez les options de l'axe horizontal et vertical principal par `x_axis` et `y_axis`. Les propriétés qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
reverse_order|bool|`false`|Spécifie que les catégories ou valeurs dans l'ordre inverse (orientation du graphique). La propriété `reverse_order` est facultative.
maximum|int|`0`|Indique que le maximum fixé, 0 est auto. La propriété maximum est facultative.
minimum|int|`0`|Spécifie que le minimum fixé, 0 est auto. La propriété minimum est facultative. La valeur par défaut est auto.

Définissez la taille du graphique par la propriété `dimension`. La propriété dimension est facultative. Les propriétés qui peuvent être définies sont:

Paramètre|Type|Défaut|Explication
---|---|---|---
height|int|290|Hauteur
width|int|480|Largeur

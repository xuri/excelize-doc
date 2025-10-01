# Utilisation basique

## Installation {#install}

Le tableau suivant indique les exigences minimales du langage Go avec chaque version publiée d'Excelize:

Version Excelize | Configuration minimale requise pour la version de la langue Go
---|---
v2.10.0 ~ master | 1.24.0
v2.9.1 | 1.23.0
v2.8.1 ~ v2.9.0 | 1.18
v2.7.0 ~ v2.8.0 | 1.16
v2.4.0 ~ v2.6.1 | 1.15
v2.0.2 ~ v2.3.2 | 1.10
v1.0.0 ~ v2.0.1 | 1.6

L'utilisation de la dernière version de la bibliothèque Excelize nécessite Go version 1.23.0 ou ultérieure. Notez qu'il y a des [modifications incompatibles](https://github.com/golang/go/issues/61881) dans Go 1.21.0, cette bibliothèque ne peut pas fonctionner avec cette version, si vous utilisez Go 1.21.x, veuillez passer à Go 1.21.1 et version ultérieure.

- Installation

```bash
go get github.com/xuri/excelize
```

- Si votre gestion de package avec des [Go Modules](https://go.dev/blog/using-go-modules), veuillez installer avec la commande suivante.

```bash
go get github.com/xuri/excelize/v2
```

## Mise à niveau {#update}

- Mise à niveau vers la dernière version stable publiée

```bash
go get -u github.com/xuri/excelize/v2
```

- Mise à niveau vers le dernier code de la branche de développement

```bash
go get -u github.com/xuri/excelize/v2@master
```

## Créer un document Excel {#NewFile}

Voici un exemple d'utilisation minimale qui créera le fichier XLSX:

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
    // Créer une nouvelle feuille.
    index, err := f.NewSheet("Sheet2")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Définir la valeur d'une cellule.
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // Définir la feuille active du classeur.
    f.SetActiveSheet(index)
    // Enregistrer le fichier xlsx par le chemin donné.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Lire un document Excel {#read}

Ce qui suit constitue le seul à lire un document XLSX:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Obtenir la valeur de la cellule par nom de feuille de calcul donné et axe.
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Obtenez toutes les lignes de la feuille Sheet1.
    rows, err := f.GetRows("Sheet1")
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
}
```

## Ajouter un graphique au document Excel {#chart}

Avec Excelize, la génération et la gestion des graphiques est aussi simple que quelques lignes de code. Vous pouvez créer des graphiques basés sur des données dans votre feuille de calcul ou générer des graphiques sans aucune donnée dans votre feuille de calcul.

<p align="center"><img width="770" src="../images/base.png" alt="Ajouter un graphique au document Excel"></p>

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
    for idx, row := range [][]interface{}{
        {nil, "Apple", "Orange", "Pear"}, {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4}, {"Large", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        f.SetSheetRow("Sheet1", cell, &row)
    }
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: excelize.Col3DClustered,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
            },
            {
                Name:       "Sheet1!$A$3",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$3:$D$3",
            },
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
            }},
        Title: []excelize.RichTextRun{
            {
                Text: "Fruit 3D Clustered Column Chart",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Enregistrez le fichier xlsx par le chemin donné.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Ajouter l'image au document Excel {#image}

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Insérer une image.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Insérer une image dans une feuille de calcul avec mise à l'échelle.
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{ScaleX: 0.5, ScaleY: 0.5}); err != nil {
        fmt.Println(err)
        return
    }
    // Insérer un décalage d'image dans la cellule avec support d'impression.
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            PrintObject:     &enable,
            LockAspectRatio: false,
            OffsetX:         15,
            OffsetY:         10,
            Locked:          &disable,
        }); err != nil {
        fmt.Println(err)
        return
    }
    // Enregistrez le fichier xlsx avec le chemin d'origine.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

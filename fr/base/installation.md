# Utilisation basique

## Installation {#install}

Utiliser la bibliothèque Excelize nécessite Go version 1.8 ou ultérieure.

- Installation

```bash
go get github.com/360EntSecGroup-Skylar/excelize
```

## Mise à niveau {#update}

- Mise à niveau

```bash
go get -u github.com/360EntSecGroup-Skylar/excelize
```

## Créer un document Excel {#NewFile}

Voici un exemple d'utilisation minimale qui créera le fichier XLSX:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx := excelize.NewFile()
    // Créer une nouvelle feuille.
    index := xlsx.NewSheet("Sheet2")
    // Définir la valeur d'une cellule.
    xlsx.SetCellValue("Sheet2", "A2", "Hello world.")
    xlsx.SetCellValue("Sheet1", "B2", 100)
    // Définir la feuille active du classeur.
    xlsx.SetActiveSheet(index)
    // Enregistrer le fichier xlsx par le chemin donné.
    err := xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
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

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx, err := excelize.OpenFile("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Obtenir la valeur de la cellule par nom de feuille de calcul donné et axe.
    cell := xlsx.GetCellValue("Sheet1", "B2")
    fmt.Println(cell)
    // Obtenez toutes les lignes de la feuille Sheet1.
    rows := xlsx.GetRows("Sheet1")
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
    xlsx.AddChart("Sheet1", "E1", `{"type":"col3DClustered","series":[{"name":"Sheet1!$A$2","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$2:$D$2"},{"name":"Sheet1!$A$3","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$3:$D$3"},{"name":"Sheet1!$A$4","categories":"Sheet1!$B$1:$D$1","values":"Sheet1!$B$4:$D$4"}],"title":{"name":"Fruit 3D Clustered Column Chart"}}`)
    // Enregistrez le fichier xlsx par le chemin donné.
    err := xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
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

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx, err := excelize.OpenFile("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Insérer une image.
    err = xlsx.AddPicture("Sheet1", "A2", "./image1.png", "")
    if err != nil {
        fmt.Println(err)
    }
    // Insérer une image dans une feuille de calcul avec mise à l'échelle.
    err = xlsx.AddPicture("Sheet1", "D2", "./image2.jpg", `{"x_scale": 0.5, "y_scale": 0.5}`)
    if err != nil {
        fmt.Println(err)
    }
    // Insérer un décalage d'image dans la cellule avec support d'impression.
    err = xlsx.AddPicture("Sheet1", "H2", "./image3.gif", `{"x_offset": 15, "y_offset": 10, "print_obj": true, "lock_aspect_ratio": false, "locked": false}`)
    if err != nil {
        fmt.Println(err)
    }
    // Enregistrez le fichier xlsx avec le chemin d'origine.
    err = xlsx.Save()
    if err != nil {
        fmt.Println(err)
    }
}
```
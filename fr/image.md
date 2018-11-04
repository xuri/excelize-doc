# Picture

## Ajouter une image {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture fournit la méthode pour ajouter une image dans une feuille en fonction d'un format d'image donné (tel que le décalage, l'échelle, le paramètre de format d'image et les paramètres d'impression) et le chemin du fichier.

Par exemple:

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
    xlsx := excelize.NewFile()
    // Ajouter une image.
    err := xlsx.AddPicture("Sheet1", "A2", "./image1.jpg", "")
    if err != nil {
        fmt.Println(err)
    }
    // Insérer une mise à l'échelle de l'image dans la cellule avec un lien hypertexte.
    err = xlsx.AddPicture("Sheet1", "D2", "./image1.png", `{"x_scale": 0.5, "y_scale": 0.5, "hyperlink": "#Sheet2!D8", "hyperlink_type": "Location"}`)
    if err != nil {
        fmt.Println(err)
    }
    // Insérer un décalage d'image dans la cellule avec un lien hypertexte externe, un support d'impression et de positionnement.
    err = xlsx.AddPicture("Sheet1", "H2", "./image3.gif", `{"x_offset": 15, "y_offset": 10, "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize", "hyperlink_type": "External", "print_obj": true, "lock_aspect_ratio": false, "locked": false, "positioning": "oneCell"}`)
    if err != nil {
        fmt.Println(err)
    }
    err = xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

LinkType définit deux types d'hyperliens `External` pour un site Web ou `Location` pour passer à l'une des cellules de ce classeur. Lorsque le `hyperlink_type` est `Location`, les coordonnées doivent commencer par `#`.

Le positionnement définit deux types de position d'une image dans une feuille de calcul Excel, `oneCell` (Déplacer mais pas dimensionner avec des cellules) ou "absolu" (Ne pas déplacer ou dimensionner avec des cellules). Si vous ne définissez pas ce paramètre, le `positioning` par défaut est le déplacement et la taille avec les cellules.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

AddPictureFromBytes fournit la méthode pour ajouter une image dans une feuille selon le format d'image défini (décalage, échelle, paramètres de format et paramètres d'impression), la description textuelle, le nom de l'extension et le contenu du fichier dans le type `[]byte`.

Par exemple:

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    xlsx := excelize.NewFile()

    file, err := ioutil.ReadFile("./image1.jpg")
    if err != nil {
        fmt.Println(err)
    }
    err = xlsx.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file)
    if err != nil {
        fmt.Println(err)
    }
    err = xlsx.SaveAs("./Book1.xlsx")
    if err != nil {
        fmt.Println(err)
    }
}
```

## Obtenir une image {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte)
```

GetPicture fournit une fonction permettant d'incorporer le nom de la base de l'image et le contenu brut dans XLSX en fonction de la feuille de calcul et du nom de la cellule. Cette fonction renvoie le nom du fichier dans XLSX et le contenu des fichiers sous la forme de types de données `[]byte`.

Par exemple:

```go
xlsx, err := excelize.OpenFile("./Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw := xlsx.GetPicture("Sheet1", "A2")
if file == "" {
    return
}
err := ioutil.WriteFile(file, raw, 0644)
if err != nil {
    fmt.Println(err)
}
```
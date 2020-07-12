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
    f := excelize.NewFile()
    // Ajouter une image.
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        fmt.Println(err)
    }
    // Insérer une mise à l'échelle de l'image dans la cellule avec un lien hypertexte.
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{
        "x_scale": 0.5,
        "y_scale": 0.5,
        "hyperlink": "#Sheet2!D8",
        "hyperlink_type": "Location"
    }`); err != nil {
        fmt.Println(err)
    }
    // Insérer un décalage d'image dans la cellule avec un lien hypertexte externe, un support d'impression et de positionnement.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize",
        "hyperlink_type": "External",
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false,
        "positioning": "oneCell"
    }`); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
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
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()

    file, err := ioutil.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtenir une image {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture fournit une fonction permettant d'incorporer le nom de la base de l'image et le contenu brut dans XLSX en fonction de la feuille de calcul et du nom de la cellule. Cette fonction renvoie le nom du fichier dans XLSX et le contenu des fichiers sous la forme de types de données `[]byte`.

Par exemple:

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := ioutil.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## Supprimer l'image {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture fournit une fonction pour supprimer des graphiques dans XLSX par feuille de calcul et nom de cellule donnés. Notez que le fichier image ne sera pas supprimé du document actuellement.

# Image

## Ajouter une image {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture fournit la méthode pour ajouter une image dans une feuille en fonction d'un format d'image donné (tel que le décalage, l'échelle, le paramètre de format d'image et les paramètres d'impression) et le chemin du fichier. Cette fonction est sécurisée pour la concurrence.

Par exemple:

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
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // Ajouter une image.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Insérer une mise à l'échelle de l'image dans la cellule avec un lien hypertexte.
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Sheet2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // Insérer un décalage d'image dans la cellule avec un lien hypertexte externe, un support d'impression et de positionnement.
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            OffsetX:         15,
            OffsetY:         10,
            Hyperlink:       "https://github.com/xuri/excelize",
            HyperlinkType:   "External",
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
            Positioning:     "oneCell",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

Le paramètre optionnel `AltText` est utilisé pour ajouter un texte alternatif à un objet graphique.

Le paramètre facultatif `PrintObject` indique si l'image est imprimée lors de l'impression de la feuille de calcul, la valeur par défaut est `true`.

Le paramètre optionnel `Locked` indique si verrouiller l'image. Le verrouillage d'un objet n'a d'effet que si la feuille est protégée.

Le paramètre optionnel `LockAspectRatio` indique si verrouiller le rapport hauteur/largeur de l'image, la valeur par défaut de celui-ci est `false`.

Le paramètre facultatif `AutoFit` spécifie si make image size auto s'adapte à la cellule, la valeur par défaut est `false`.

Le paramètre facultatif `OffsetX` spécifie le décalage horizontal de l'image avec la cellule, la valeur par défaut est 0.

Le paramètre facultatif `OffsetY` spécifie le décalage vertical de l'image avec la cellule, la valeur par défaut est 0.

Le paramètre facultatif `ScaleX` spécifie l'échelle horizontale des images, la valeur par défaut de celle-ci est 1.0 qui présente 100%.

Le paramètre facultatif `ScaleY` spécifie l'échelle verticale des images, la valeur par défaut de celle-ci est 1.0 qui présente 100%.

Le paramètre facultatif `Hyperlink` spécifie le lien hypertexte de l'image.

Le paramètre facultatif `HyperlinkType` définit deux types de lien hypertexte `External` pour le site Web ou `Location` pour se déplacer vers l'une des cellules de ce classeur. Lorsque le `HyperlinkType` est `Location`, les coordonnées doivent commencer par `#`.

Le paramètre optionnel `Positioning` définit 3 types de position d'un objet graphique dans une feuille de calcul: `oneCell` (déplacer mais ne pas redimensionner avec les cellules), `twoCell` (déplacer et redimensionner avec les cellules) et `absolute` (Ne pas déplacer ou dimensionner avec les cellules). Si vous ne définissez pas ce paramètre, le positionnement par défaut consiste à déplacer et dimensionner avec les cellules.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

AddPictureFromBytes fournit la méthode pour ajouter une image dans une feuille selon le format d'image défini (décalage, échelle, paramètres de format et paramètres d'impression), la description textuelle, le nom de l'extension et le contenu du fichier dans le type `[]byte`.

Par exemple:

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    file, err := os.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Excel Logo"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Obtenir une image {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

GetPicture fournit une fonction permettant d'incorporer le nom de la base de l'image et le contenu brut dans XLSX en fonction de la feuille de calcul et du nom de la cellule. Cette fonction est sécurisée pour la concurrence. Cette fonction renvoie le nom du fichier dans XLSX et le contenu des fichiers sous la forme de types de données `[]byte`.

Par exemple:

```go
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
pics, err := f.GetPictures("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("image%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## Supprimer l'image {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture fournit une fonction pour supprimer des graphiques dans XLSX par feuille de calcul et nom de cellule donnés. Notez que le fichier image ne sera pas supprimé du document actuellement.

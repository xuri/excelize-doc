# Bild

## Bild hinzufügen {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture bietet die Methode zum Hinzufügen eines Bilds zu einem Arbeitsblatt anhand eines bestimmten Bildformatsatzes (z. B. Versatz, Skalierung, Seitenverhältniseinstellung und Druckeinstellungen) und des Dateipfads.

Zum Beispiel:

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
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    // Fügen Sie ein Bild ein.
    if err := f.AddPicture("Sheet1", "A2", "image.png", ""); err != nil {
        fmt.Println(err)
    }
    // Fügen Sie ein Bild mit Skalierung in ein Arbeitsblatt ein.
    if err := f.AddPicture("Sheet1", "D2", "image.jpg", `{
        "x_scale": 0.5,
        "y_scale": 0.5
    }`); err != nil {
        fmt.Println(err)
    }
    // Fügen Sie mit Druckunterstützung einen Bildversatz in die Zelle ein.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false
    }`); err != nil {
        fmt.Println(err)
    }
    // Speichern Sie die Tabellenkalkulationsdatei mit dem Ursprungspfad.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

LinkType definiert zwei Arten von Hyperlinks: `External` für eine Website oder `Location` für das Verschieben in eine der Zellen in dieser Arbeitsmappe. Wenn der `hyperlink_type` `Location` ist, müssen die Koordinaten mit `#` beginnen.

Die Positionierung definiert zwei Arten der Position eines Bildes in einer Excel-Tabelle: `oneCell` (Verschieben, aber keine Größe mit Zellen) oder "absolut" (Nicht verschieben oder Größe mit Zellen). Wenn Sie diesen Parameter nicht einstellen, ist die Standardeinstellung `positioning` Verschieben und Größe mit Zellen.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

AddPictureFromBytes bietet die Methode zum Hinzufügen eines Bilds zu einem Blatt anhand eines bestimmten Bildformatsatzes (z. B. Versatz, Skalierung, Seitenverhältniseinstellung und Druckeinstellungen), einer alternativen Textbeschreibung, eines Erweiterungsnamens und eines Dateiinhalts im Typ `[]byte`.

Zum Beispiel:

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

## Holen Sie sich ein Bild {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture bietet eine Funktion, mit der der Name der Bildbasis und der Rohinhalt anhand des Arbeitsblatts und des Zellennamens in eine Tabelle eingebettet werden können. Diese Funktion gibt den Dateinamen in der Tabelle und den Dateiinhalt als Datentypen `[]byte` zurück.

Zum Beispiel:

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

## Bild löschen {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture bietet eine Funktion zum Löschen von Diagrammen in einer Tabelle anhand des angegebenen Arbeitsblatts und des Zellennamens. Beachten Sie, dass die Bilddatei derzeit nicht aus dem Dokument gelöscht wird.

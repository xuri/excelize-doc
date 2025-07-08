# Bild

## Bild hinzufügen {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture ermöglicht das Hinzufügen eines Bildes zu einem Arbeitsblatt anhand des vorgegebenen Bildformats (z. B. Offset, Skalierung, Seitenverhältnis und Druckeinstellungen) und Dateipfads. Unterstützte Bildtypen: BMP, EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF und WMZ. Diese Funktion ist parallelitätssicher. Beachten Sie, dass diese Funktion nur das Hinzufügen von Bildern über den aktuell platzierten Zellen unterstützt. Das Hinzufügen von Bildern in Zellen oder das Erstellen eingebetteter Kingsoft WPS Office-Bildzellen ist nicht möglich.

Zum Beispiel:

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
    // Fügen Sie ein Bild ein.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // Fügen Sie ein Bild mit Skalierung in ein Arbeitsblatt ein.
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
    // Fügen Sie mit Druckunterstützung einen Bildversatz in die Zelle ein.
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
    // Speichern Sie die Tabellenkalkulationsdatei mit dem Ursprungspfad.
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

Der optionale Parameter `AltText` wird verwendet, um alternativen Text zu einem Diagrammobjekt hinzuzufügen.

Der optionale Parameter `PrintObject` gibt an, ob das Bild gedruckt wird, wenn das Arbeitsblatt gedruckt wird, der Standardwert dafür ist `true`.

Der optionale Parameter `Locked` gibt an, ob das Bild gesperrt ist. Das Sperren eines Objekts hat keine Auswirkung, es sei denn, das Blatt ist geschützt.

Der optionale Parameter `LockAspectRatio` gibt an, ob das Seitenverhältnis für das Bild gesperrt ist, der Standardwert dafür ist `false`.

Der optionale Parameter `AutoFit` gibt an, ob die Bildgröße automatisch in die Zelle passt, der Standardwert dafür ist `false`.

Der optionale Parameter `OffsetX` gibt den horizontalen Versatz des Bildes mit der Zelle an, der Standardwert davon ist 0.

Der optionale Parameter `OffsetY` gibt den vertikalen Versatz des Bildes mit der Zelle an, der Standardwert davon ist 0.

Der optionale Parameter `ScaleX` spezifiziert die horizontale Skalierung von Bildern, der Standardwert davon ist 1.0, was 100% darstellt.

Der optionale Parameter `ScaleY` spezifiziert die vertikale Skalierung von Bildern, der Standardwert davon ist 1.0, was 100% darstellt.

Der optionale Parameter `Hyperlink` spezifiziert den Hyperlink des Bildes.

Der optionale Parameter `HyperlinkType` definiert zwei Arten von Hyperlinks `External` für die Website oder `Location` zum Verschieben in eine der Zellen in dieser Arbeitsmappe. Wenn der `HyperlinkType` `Location` ist, müssen die Koordinaten mit `#` beginnen.

Der optionale Parameter `Positioning` definiert drei Arten der Position eines Diagrammobjekts in einer Tabellenkalkulation: `oneCell` (Verschieben, aber Größe nicht mit Zellen anpassen), `twoCell` (Verschieben und Größe mit Zellen anpassen) und `absolute` ( Zellen nicht verschieben oder vergrößern). Wenn Sie diesen Parameter nicht festlegen, erfolgt die Standardpositionierung durch Verschieben und Größe mit Zellen.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

AddPictureFromBytes bietet die Methode zum Hinzufügen eines Bilds zu einem Blatt anhand eines bestimmten Bildformatsatzes (z. B. Versatz, Skalierung, Seitenverhältniseinstellung und Druckeinstellungen), einer alternativen Textbeschreibung, eines Erweiterungsnamens und eines Dateiinhalts im Typ `[]byte`. Unterstützte Bildtypen: EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF und WMZ. Beachten Sie, dass diese Funktion nur das Hinzufügen von Bildern über den aktuellen Zellen unterstützt. Das Hinzufügen von Bildern in Zellen oder das Erstellen der in Kingsoft WPS Office eingebetteten Bildzellen ist nicht möglich.

Zum Beispiel:

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

## Holen Sie sich ein Bild {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

GetPicture bietet eine Funktion, mit der der Name der Bildbasis und der Rohinhalt anhand des Arbeitsblatts und des Zellennamens in eine Tabelle eingebettet werden können. Diese Funktion wird für die gleichzeitige Verwendung unterstützt. Diese Funktion gibt den Dateinamen in der Tabelle und den Dateiinhalt als Datentypen `[]byte` zurück.

Zum Beispiel:

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

## Bild löschen {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture bietet eine Funktion zum Löschen von Diagrammen in einer Tabelle anhand des angegebenen Arbeitsblatts und des Zellennamens. Beachten Sie, dass die Bilddatei derzeit nicht aus dem Dokument gelöscht wird.

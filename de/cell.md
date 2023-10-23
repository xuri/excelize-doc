# Zelle

`RichTextRun` ordnet die Einstellungen des Rich-Text-Laufs direkt zu.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

`HyperlinkOpts` können an [`SetCellHyperlink`](cell.md#SetCellHyperlink) übergeben werden, um optionale Hyperlink-Attribute festzulegen (z. B. anzugebender Text und Text mit Bildschirmtipps).

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

`FormulaOpts` können an [`SetCellFormula`](cell.md#SetCellFormula) übergeben werden, um andere Formeltypen zu verwenden.

```go
type FormulaOpts struct {
    Type *string // Formeltyp
    Ref  *string // Gemeinsame Formelreferenz
}
```

## Festlegen des Zellenwerts {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, cell string, value interface{}) error
```

SetCellValue bietet eine Funktion zum Festlegen des Werts einer Zelle. Diese Funktion wird für die gleichzeitige Verwendung unterstützt. Die angegebenen Koordinaten sollten sich nicht in der ersten Zeile der Tabelle befinden. Im Folgenden werden die unterstützten Datentypen angezeigt:

|Unterstützte Datentypen|
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

Beachten Sie, dass das standardmäßige Datumsformat `m/d/yy h:mm` mit dem Wert `time.Time` ist. Sie können das Zahlenformat mit der Methode [`SetCellStyle`](cell.md#SetCellStyle) festlegen. Wenn Sie das spezielle Datum in Excel wie den 0. Januar 1900 oder den 29. Februar 1900 festlegen müssen, können diese Zeiten nicht im Datentyp `time.Time` der Go-Sprache dargestellt werden. Bitte legen Sie den Zellenwert als Zahl 0 oder 60 fest, erstellen und binden Sie dann den Datum-Uhrzeit-Zahlenformatstil für die Zelle.

## Festlegen eines booleschen Werts {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, cell string, value bool) error
```

SetCellBool bietet eine Funktion zum Festlegen des Bool-Typwerts einer Zelle anhand des angegebenen Arbeitsblattnamens, der Zellkoordinaten und des Zellenwerts.

## Festlegen des RAW-Werts {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, cell, value string) error
```

SetCellDefault bietet eine Funktion zum Festlegen des Zeichenfolgentypwerts einer Zelle als Standardformat, ohne die Zelle zu verlassen.

## Ganzzahlwert festlegen {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, cell string, value int) error
```

SetCellInt bietet eine Funktion zum Festlegen des Int-Typ-Werts einer Zelle anhand des angegebenen Arbeitsblattnamens, der Zellkoordinaten und des Zellenwerts.

## Gleitkommawert festlegen {#SetCellFloat}

```go
func (f *File) SetCellFloat(sheet, cell string, value float64, precision, bitSize int) error
```

SetCellFloat setzt einen Fließkommawert in eine Zelle. Der Parameter `precision` gibt an, wie viele Nachkommastellen angezeigt werden, während `-1` ein spezieller Wert ist, der so viele Dezimalstellen wie nötig verwendet, um die Zahl darzustellen. `bitSize` ist `32` oder `64`, je nachdem, ob `float32` oder `float64` ursprünglich für den Wert verwendet wurde.

## Festlegen des Zeichenfolgenwerts {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, cell, value string) error
```

SetCellStr bietet eine Funktion zum Festlegen des Zeichenfolgentypwerts einer Zelle. Die Gesamtzahl der Zeichen, die eine Zelle `32767` Zeichen enthalten kann.

## Festlegen des Zellstils {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hCell, vCell string, styleID int) error
```

SetCellStyle bietet eine Funktion zum Hinzufügen von Stilattributen für Zellen anhand des angegebenen Arbeitsblattnamens, des Koordinatenbereichs und der Stil-ID. Diese Funktion wird für die gleichzeitige Verwendung unterstützt. Stilindizes können mit der Funktion [`NewStyle`](style.md#NewStyle) abgerufen werden. Beachten Sie, dass die Rahmen vom Typ `diagonalDown` und `diagonalUp` dieselbe Farbe im selben Koordinatenbereich verwenden sollten. SetCellStyle überschreibt die vorhandenen Stile für die Zelle, fügt Stile nicht an oder führt sie mit vorhandenen Stilen zusammen.

- Beispiel 1: Erstellen Sie Ränder der Zelle `D7` auf `Sheet1`:

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

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="Legen Sie einen Rahmenstil für eine Zelle fest"></p>

Die vier Ränder der Zelle `D7` sind mit unterschiedlichen Stilen und Farben festgelegt. Dies hängt mit den Parametern beim Aufrufen der Funktion [`NewStyle`](style.md#NewStyle) zusammen. Sie müssen verschiedene Stile festlegen, um auf die Dokumentation zu diesem Kapitel zu verweisen.

- Beispiel 2: Festlegen des Verlaufsstils für die Arbeitsblattzelle `D7` mit dem Namen `Sheet1`:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "gradient", Color: []string{"FFFFFF", "E0EBF5"}, Shading: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="Legen Sie einen Verlaufsstil für die Zelle fest"></p>

Die Zelle `D7` wird mit der Farbfüllung des Verlaufseffekts eingestellt. Der Gradientenfüllungseffekt hängt mit dem Parameter zusammen, wenn die Funktion [`NewStyle`](style.md#NewStyle) aufgerufen wird. Sie müssen verschiedene Stile festlegen, um auf die Dokumentation dieses Kapitels zu verweisen.

- Beispiel 3: Legen Sie eine feste Füllung für die `D7`-Zelle mit dem Namen `Sheet1` fest:

```go
style, err := f.NewStyle(&excelize.Style{
    Fill: excelize.Fill{Type: "pattern", Color: []string{"E0EBF5"}, Pattern: 1},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_03.png" alt="Stellen Sie eine feste Füllung für die Zelle ein"></p>

Die Zelle `D7` wird mit einer festen Füllung gesetzt.

- Beispiel 4: Legen Sie den Zeichenabstand und den Drehwinkel für die `D7`-Zelle mit dem Namen `Sheet1` fest:

```go
f.SetCellValue("Sheet1", "D7", "Stil")
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

<p align="center"><img width="612" src="./images/SetCellStyle_04.png" alt="Stellen Sie den Zeichenabstand und den Drehwinkel ein"></p>

- In Beispiel 5 werden Datum und Uhrzeit in Excel durch reelle Zahlen dargestellt. Beispiel: "2017/7/4 12:00:00 PM" kann durch die Zahl `42920.5` dargestellt werden. Legen Sie das Zeitformat für die Arbeitsblattzelle `D7` mit dem Namen `Sheet1` fest:

```go
f.SetCellValue("Sheet1", "D7", 42920.5)
f.SetColWidth("Sheet1", "D", "D", 13)
style, err := f.NewStyle(&excelize.Style{NumFmt: 22})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_05.png" alt="Legen Sie das Zeitformat für die Zelle fest"></p>

Die Zelle `D7` ist auf das Zeitformat eingestellt. Beachten Sie, dass wenn die Zellenbreite mit dem angewendeten Zeitformat zu schmal ist, um vollständig angezeigt zu werden, sie als `####` angezeigt wird. Sie können die Spaltenbreite ziehen und ablegen oder die Spalte durch Aufrufen von auf die entsprechende Größe einstellen `SetColWidth` Funktion zur normalen Anzeige.

- Beispiel 6: Festlegen von Schriftart, Schriftgröße, Farbe und Versatzstil für die Arbeitsblattzelle `D7` mit dem Namen `Sheet1`:

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

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="Legen Sie Schriftart, Schriftgröße, Farbe und Versatzstil für Zellen fest"></p>

- Beispiel 7: Sperren und Ausblenden der `D7`-Zelle des Arbeitsblatts mit dem Namen `Sheet1`:

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

Schützen Sie das Arbeitsblatt, um eine Zelle zu sperren oder eine Formel auszublenden. Klicken Sie auf der Registerkarte "Überprüfen" auf "Arbeitsblatt schützen".

## Festlegen eines Hyperlinks {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, cell, link, linkType string, opts ...HyperlinkOpts) error
```

SetCellHyperLink bietet eine Funktion zum Festlegen von Zellen-Hyperlinks anhand des angegebenen Arbeitsblattnamens und der Link-URL-Adresse. LinkType definiert zwei Arten von Hyperlinks: `External` für die Website oder `Location` für das Verschieben in eine der Zellen in dieser Arbeitsmappe. Die maximale Anzahl von Hyperlinks in einem Arbeitsblatt beträgt `65530`. Diese Funktion wird nur verwendet, um den Hyperlink der Zelle festzulegen und hat keinen Einfluss auf den Wert der Zelle. Wenn Sie den Wert der Zelle setzen müssen, verwenden Sie bitte die anderen Funktionen wie [`SetCellStyle`](cell.md#SetCellStyle) oder [`SetSheetRow`](sheet.md#SetSheetRow). Unten finden Sie ein Beispiel für einen externen Link.

- Beispiel 1: Hinzufügen eines externen Links zur `A3`-Zelle des Arbeitsblatts mit dem Namen `Sheet1`:

```go
display, tooltip := "https://github.com/xuri/excelize", "Excelize on GitHub"
if err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External", excelize.HyperlinkOpts{
        Display: &display,
        Tooltip: &tooltip,
    }); err != nil {
    fmt.Println(err)
}
// Legen Sie die Schriftart und den Unterstreichungsstil für die Zelle fest
style, err := f.NewStyle(&excelize.Style{
    Font: &excelize.Font{Color: "1265BE", Underline: "single"},
})
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "A3", "A3", style)
```

- Beispiel 2: Hinzufügen einer internen Standortverknüpfung zur `A3`-Zelle mit dem Namen `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3", "Sheet1!A40", "Location")
```

## Festlegen von Zell-Richtext {#SetCellRichText}

```go
func (f *File) SetCellRichText(sheet, cell string, runs []RichTextRun) error
```

SetCellRichText bietet eine Funktion zum Festlegen einer Zelle mit Rich Text anhand eines bestimmten Arbeitsblatts.

Legen Sie beispielsweise Rich Text in der Zelle `A1` des Arbeitsblatts mit dem Namen `Sheet1` fest:

<p align="center"><img width="612" src="./images/rich_text.png" alt="Stellen Sie den Zellen-Rich-Text ein"></p>

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

## Holen Sie sich zellreichen Text {#GetCellRichText}

```go
func (f *File) GetCellRichText(sheet, cell string) ([]RichTextRun, error)
```

GetCellRichText bietet eine Funktion zum Abrufen des Rich-Textes von Zellen anhand eines bestimmten Arbeitsblatts.

## Abrufen des Zellenwerts {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, cell string, opts ...Options) (string, error)
```

Der Wert der Zelle wird gemäß dem angegebenen Arbeitsblatt und den angegebenen Zellkoordinaten abgerufen, und der Rückgabewert wird in den Typ `string` konvertiert. Diese Funktion wird für die gleichzeitige Verwendung unterstützt. Wenn das Zellenformat auf den Wert einer Zelle angewendet werden kann, wird der angewendete Wert zurückgegeben, andernfalls wird der ursprüngliche Wert zurückgegeben. Die Werte aller Zellen sind in einem zusammengeführten Bereich gleich.

## Holen Sie sich den Zellendatentyp {#GetCellType}

```go
func (f *File) GetCellType(sheet, cell string) (CellType, error)
```

GetCellType bietet eine Funktion zum Abrufen des Datentyps der Zelle anhand des angegebenen Arbeitsblattnamens und der Achse in der Tabellenkalkulationsdatei.

## Abrufen des gesamten Zellenwerts nach Spalten {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

GetCols ruft den Wert aller Zellen nach Spalten auf dem Arbeitsblatt basierend auf dem angegebenen Arbeitsblattnamen ab und wird als zweidimensionales Array zurückgegeben, wobei der Wert der Zelle in den Typ `string` konvertiert wird. Wenn das Zellenformat auf den Wert der Zelle angewendet werden kann, wird der angewendete Wert verwendet, andernfalls wird der ursprüngliche Wert verwendet. Zum Beispiel:

Abrufen und Durchlaufen des Werts aller Zellen durch Spalten in einem Arbeitsblatt mit dem Namen `Sheet1`:

```go
cols, err := f.GetCols("Sheet1")
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

## Abrufen des gesamten Zellenwerts nach Zeilen {#GetRows}

```go
func (f *File) GetRows(sheet string, opts ...Options) ([][]string, error)
```

GetRows gibt alle Zeilen in einem Blatt mit dem angegebenen Arbeitsblattnamen zurück, der als zweidimensionales Array zurückgegeben wird, wobei der Wert der Zelle in den Typ `string` konvertiert wird. Wenn das Zellenformat auf den Wert der Zelle angewendet werden kann, wird der angewendete Wert verwendet, andernfalls wird der ursprüngliche Wert verwendet. GetRows die Zeilen mit Wert- oder Formelzellen abgerufen hat, werden die ständig leeren Zellen am Ende jeder Zeile übersprungen, sodass die Länge jeder Zeile möglicherweise inkonsistent ist.

Abrufen und Durchlaufen des Werts aller Zellen in Zeilen in einem Arbeitsblatt mit dem Namen `Sheet1`:

```go
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
```

## Abrufen von Hyperlinks {#GetCellHyperLink}

```go
func (f *File) GetCellHyperLink(sheet, cell string) (bool, string, error)
```

GetCellHyperLink ruft einen Zell-Hyperlink basierend auf dem angegebenen Arbeitsblattnamen und Zellkoordinaten ab. Wenn die Zelle einen Hyperlink hat, gibt sie `true` und die Linkadresse zurück, andernfalls gibt sie `false` und eine leere Linkadresse zurück.

Holen Sie sich beispielsweise einen Hyperlink zu einer `H6`-Zelle in einem Arbeitsblatt mit dem Namen `Sheet1`:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## Stilindex abrufen {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, cell string) (int, error)
```

Der Zellenstilindex wird aus dem angegebenen Arbeitsblattnamen und den Zellkoordinaten abgerufen, und der erhaltene Index kann als Parameter zum Aufrufen der Funktion `SetCellStyle` beim Kopieren des Zellenstils verwendet werden.

## Zusammenführen von Zellen {#MergeCell}

```go
func (f *File) MergeCell(sheet, hCell, vCell string) error
```

Führen Sie Zellen basierend auf dem angegebenen Arbeitsblattnamen und den Zellkoordinatenbereichen zusammen. Beim Zusammenführen von Zellen wird nur der obere linke Zellenwert beibehalten und die anderen Werte verworfen. Führen Sie beispielsweise Zellen im Bereich `D3:E9` in einem Arbeitsblatt mit dem Namen `Sheet1` zusammen:

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

Wenn sich der angegebene Zellkoordinatenbereich mit anderen vorhandenen zusammengeführten Zellen überschneidet, werden die vorhandenen zusammengeführten Zellen gelöscht.

## Unmerge-Zellen {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hCell, vCell string) error
```

UnmergeCell bietet eine Funktion zum Aufheben der Zusammenführung eines bestimmten Koordinatenbereichs. Zum Beispiel den Bereich `D3:E9` auf `Sheet1` entfernen:

```go
err := f.UnmergeCell("Sheet1", "D3", "E9")
```

Achtung: Überlappende Bereiche werden ebenfalls nicht zusammengeführt.

## Abrufen von Zusammenführungszellen {#GetMergeCells}

GetMergeCells bietet eine Funktion zum Abrufen aller zusammengeführten Zellen aus einem aktuellen Arbeitsblatt.

```go
func (f *File) GetMergeCells(sheet string) ([]MergeCell, error)
```

### Wert der zusammengeführten Zelle abrufen

```go
func (m *MergeCell) GetCellValue() string
```

GetCellValue gibt den zusammengeführten Zellenwert zurück.

### Holen Sie sich die Zellenkoordinaten oben links des zusammengeführten Bereichs

```go
func (m *MergeCell) GetStartAxis() string
```

GetStartAxis gibt die oberen linken Zellenkoordinaten des zusammengeführten Bereichs zurück, zum Beispiel: `C2`.

### Holen Sie sich die unteren rechten Zellenkoordinaten des zusammengeführten Bereichs

```go
func (m *MergeCell) GetEndAxis() string
```

GetEndAxis gibt die unteren rechten Zellenkoordinaten des zusammengeführten Bereichs zurück, zum Beispiel: `D4`.

## Kommentar hinzufügen {#AddComment}

```go
func (f *File) AddComment(sheet string, comment Comment) error
```

AddComment bietet die Methode zum Hinzufügen von Kommentaren zu einem Blatt anhand eines bestimmten Arbeitsblattindex, einer bestimmten Zelle und eines bestimmten Formatsatzes (z. B. Autor und Text). Beachten Sie, dass die maximale Autorenlänge 255 und die maximale Textlänge 32512 beträgt. Fügen Sie beispielsweise einen Kommentar in `Sheet1!$A$3` hinzu:

<p align="center"><img width="612" src="./images/comment.png" alt="Fügen Sie einem Excel-Dokument einen Kommentar hinzu"></p>

```go
err := f.AddComment("Sheet1", excelize.Comment{
    Cell:   "A3",
    Author: "Excelize",
    Paragraph: []excelize.RichTextRun{
        {Text: "Excelize: ", Font: &excelize.Font{Bold: true}},
        {Text: "Dies ist ein Kommentar."},
    },
})
```

## Kommentar abrufen {#GetComments}

```go
func (f *File) GetComments(sheet string) ([]Comment, error)
```

GetComments ruft alle Kommentare in einem Arbeitsblatt nach dem angegebenen Arbeitsblattnamen ab.

## Kommentar löschen {#DeleteComment}

```go
func (f *File) DeleteComment(sheet, cell string) error
```

DeleteComment bietet die Methode zum Löschen von Kommentaren in einem Blatt nach gegebenem Arbeitsblatt. Löschen Sie beispielsweise den Kommentar in `Sheet1!$A$30`:

```go
err := f.DeleteComment("Sheet1", "A30")
```

## Festlegen der Zellenformel {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, cell, formula string, opts ...FormulaOpts) error
```

SetCellFormula bietet eine Funktion zum Festlegen der Formel für die Zelle, die gemäß dem angegebenen Arbeitsblattnamen und den Zellformeleinstellungen verwendet wird. Das Ergebnis der Formelzelle kann berechnet werden, wenn das Arbeitsblatt von der Office Excel-Anwendung geöffnet wird, oder kann die [CalcCellValue](cell.md#CalcCellValue) Funktion auch den berechneten Zellenwert abrufen. Wenn die Excel-Anwendung die Formel beim Öffnen der Arbeitsmappe nicht automatisch berechnet, rufen Sie nach dem Einstellen der Zellenformelfunktionen [UpdateLinkedValue](utils.md#UpdateLinkedValue) auf.

- Beispiel 1, setzen Sie die normale Formel `=SUM(A1,B1)` für die Zelle `A3` auf `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- Beispiel 2, setze eindimensionale vertikale Konstantenarray (Spaltenarray) Formel `1;2;3` für die Zelle `A3` auf `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={1;2;3}")
```

- Beispiel 3, setze eindimensionales horizontales konstantes Array (Zeilenarray) Formel `"a","b","c"` für die Zelle `A3` auf `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- Beispiel 4, setze die zweidimensionale konstante Arrayformel `{1,2;"a","b"}` für die Zelle `A3` auf `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2;\"a\",\"b\"}",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Beispiel 5, setze die Range-Array-Formel `A1:A2` für die Zelle `A3` auf `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "=A1:A2",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Beispiel 6, setze die gemeinsame Formel `=A1+B1` für die Zellen `C1:C5` auf `Sheet1`, `C1` ist die Masterzelle:

```go
formulaType, ref := excelize.STCellFormulaTypeShared, "C1:C5"
err := f.SetCellFormula("Sheet1", "C1", "=A1+B1",
    excelize.FormulaOpts{Ref: &ref, Type: &formulaType})
```

- Beispiel 7, setze die Tabellenformel `=SUM(Table1[[A]:[B]])` für die Zelle `C2` auf `Sheet1`:

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
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1",
        &excelize.Table{
            Range:     "A1:C2",
            Name:      "Table1",
            StyleName: "TableStyleMedium2",
        }); err != nil {
        fmt.Println(err)
        return
    }
    formulaType := excelize.STCellFormulaTypeDataTable
    if err := f.SetCellFormula("Sheet1", "C2", "=SUM(Table1[[A]:[B]])",
        excelize.FormulaOpts{Type: &formulaType}); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Abrufen der Zellenformel {#GetCellFormula}

```go
func (f *File) GetCellFormula(sheet, cell string) (string, error)
```

Rufen Sie die Formel für die Zelle basierend auf dem angegebenen Arbeitsblattnamen und den Zellkoordinaten ab.

## Zellenwert berechnen {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string, opts ...Options) (string, error)
```

CalcCellValue bietet eine Funktion zum Abrufen des berechneten Zellenwerts. Diese Funktion befindet sich derzeit in Bearbeitung. Iterative Berechnung, implizite Schnittmenge, explizite Schnittmenge, Matrixformel, Tabellenformel und einige andere Formeln werden derzeit nicht unterstützt.

Unterstützte Formeln:

Funktionsname | Typ und Beschreibung
---|---
ABS                       | Gibt den absoluten Wert einer Zahl zurück
AUFGELZINS                | Gibt die aufgelaufenen Zinsen für ein Wertpapier zurück, das regelmäßig Zinsen abwirft
AUFGELZINSF               | Gibt die aufgelaufenen Zinsen für ein Wertpapier zurück, das bei Fälligkeit Zinsen abwirft
ARCCOS                    | Gibt den Arkuskosinus einer Zahl zurück
ARCCOSHYP                 | Gibt den umgekehrten hyperbolischen Kosinus einer Zahl zurück
ARCCOT                    | Gibt den Arkuskotangens einer Zahl zurück
ARCCOTHYP                 | Gibt den hyperbolischen Arkuskotangens einer Zahl zurück
AGGREGAT                  | Gibt ein Aggregat in einer Liste oder Datenbank zurück
ADRESS                    | Gibt einen Bezug auf eine einzelne Zelle in einem Tabellenblatt als Text zurück
AMORDEGRK                 | Gibt die Abschreibung für die einzelnen Abschreibungszeiträume mithilfe eines Abschreibungskoeffizienten zurück
AMORLINEARK               | Gibt die Abschreibung für die einzelnen Abschreibungszeiträume zurück
UND                       | Gibt WAHR zurück, wenn alle Argumente WAHR sind
ARABISCH                  | Konvertiert eine römische Zahl in eine arabische (als Zahl)
ARRAYTOTEXT               | Gibt ein Array von Textwerten aus einem beliebigen angegebenen Range zurück
ARCSIN                    | Gibt den Arkussinus einer Zahl zurück
ARCSINHYP                 | Gibt den umgekehrten hyperbolischen Sinus einer Zahl zurück
ARCTAN                    | Gibt den Arkustangens einer Zahl zurück
ARCTAN2                   | Gibt den Arkustangens von x- und y-Koordinaten zurück
ARCTANHYP                 | Gibt den umgekehrten hyperbolischen Tangens einer Zahl zurück
MITTELABW                 | Gibt die durchschnittliche absolute Abweichung von Datenpunkten von ihrem Mittelwert zurück
MITTELWERT                | Gibt den Mittelwert der Argumente zurück
MITTELWERTA               | Gibt den Mittelwert der Argumente zurück, die Zahlen, Text und Wahrheitswerte enthalten können
MITTELWERTWENN            | Gibt den Mittelwert (arithmetisches Mittel) aller Zellen in einem Bereich zurück, die ein bestimmtes Kriterium erfüllen
MITTELWERTWENNS           | Gibt den Mittelwert (arithmetisches Mittel) aller Zellen zurück, die mehrere Kriterien erfüllen
BASIS                     | Konvertiert eine Zahl in eine Textdarstellung mit der angegebenen Basis
BESSELI                   | Gibt die modifizierte Bessel-Funktion ln(x) zurück
BESSELJ                   | Gibt die Bessel-Funktion Jn(x) zurück
BESSELK                   | Gibt die modifizierte Bessel-Funktion Kn(x) zurück
BESSELY                   | Gibt die Bessel-Funktion Yn(x) zurück
BETADIST                  | Gibt die kumulierte Beta-Verteilungsfunktion zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
BETA.VERT                 | Gibt die kumulierte Beta-Verteilungsfunktion zurück
BETAINV                   | Gibt die Umkehrung der kumulierten Verteilungsfunktion für eine angegebene Beta-Verteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
BETA.INV                  | Gibt die Umkehrung der kumulierten Verteilungsfunktion für eine angegebene Beta-Verteilung zurück
BININDEZ                  | Konvertiert eine binäre Zahl in eine Dezimalzahl
BININHEX                  | Konvertiert eine binäre Zahl in eine Hexadezimalzahl
BININOKT                  | Konvertiert eine binäre Zahl in eine oktale Zahl
BINOMDIST                 | Gibt Wahrscheinlichkeiten einer binomialverteilten Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
BINOM.VERT                | Gibt Wahrscheinlichkeiten einer binomialverteilten Zufallsvariablen zurück
BINOM.VERT.BEREICH        | Gibt die Erfolgswahrscheinlichkeit eines Versuchsergebnisses als Binomialverteilung zurück
BINOM.INV                 | Gibt den kleinsten Wert zurück, für den die kumulierten Wahrscheinlichkeiten der Binomialverteilung kleiner oder gleich einer Grenzwahrscheinlichkeit sind
BITUND                    | Gibt ein bitweises UND zweier Zahlen zurück
BITLVERSCHIEB             | Gibt einen Zahlenwert um eine angegebene Anzahl von Bits nach links verschoben zurück
BITODER                   | Gibt ein bitweises ODER von zwei Zahlen zurück
BITRVERSCHIEB             | Gibt einen Zahlenwert um eine angegebene Anzahl Bits nach rechts verschoben zurück
BITXODER                  | Gibt ein bitweises exklusives ODER zweier Zahlen zurück
CEILING                   | Rundet eine Zahl auf die nächste Ganzzahl oder auf das kleinste Vielfache des angegebenen Schritts
OBERGRENZE.MATHEMATIK     | Rundet eine Zahl auf die nächste ganze Zahl oder auf das kleinste Vielfache des angegebenen Schritts auf
OBERGRENZE.GENAU          | Rundet eine Zahl auf die nächste ganze Zahl oder auf das kleinste Vielfache des angegebenen Schritts. Die Zahl wird Unabhängig vom ihrem Vorzeichen aufgerundet
ZEICHEN                   | Gibt das durch die Codenummer angegebene Zeichen zurück
CHIDIST                   | Gibt Werte der Verteilungsfunktion (1-Alpha) einer Chi-Quadrat-verteilten Zufallsgröße zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
CHIINV                    | Gibt Perzentile der Verteilungsfunktion einer Chi-Quadrat-verteilten Zufallsgröße zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
CHITEST                   | Gibt die Teststatistik eines Unabhängigkeitstests zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
CHIQU.VERT                | Gibt die kumulative Beta-Wahrscheinlichkeitsdichtefunktion zurück
CHIQU.VERT.RE             | Gibt Werte der Verteilungsfunktion (1-Alpha) einer Chi-Quadrat-verteilten Zufallsgröße zurück
CHIQU.INV                 | Gibt die kumulative Beta-Wahrscheinlichkeitsdichtefunktion zurück
CHIQU.INV.RE              | Gibt Perzentile der Verteilungsfunktion einer Chi-Quadrat-verteilten Zufallsgröße zurück
CHIQU.TEST                | Gibt die Teststatistik eines Unabhängigkeitstests zurück
WAHL                      | Wählt einen Wert aus einer Liste mit Werten aus
SÄUBERN                   | Entfernt alle nicht druckbaren Zeichen aus Text
CODE                      | Gibt einen numerischen Code für das erste Zeichen in einer Textzeichenfolge zurück
COLUMN                    | Gibt die Spaltennummer eines Bezugs zurück
SPALTEN                   | Gibt die Anzahl von Spalten in einem Bezug zurück
KOMBINATIONEN             | Gibt die Anzahl der Kombinationen für eine bestimmte Anzahl von Objekten zurück
KOMBINATIONEN2            | Gibt die Anzahl der Kombinationen mit Wiederholung für eine angegebene Anzahl von Elementen zurück
KOMPLEXE                  | Konvertiert den Realteil und Imaginärteil in eine komplexe Zahl
TEXTKETTE                 | Kombiniert den Text aus mehreren Bereichen und/oder Zeichenfolgen, gibt aber keine Trennzeichen oder IgnoreEmpty-Argumente an
VERKETTEN                 | Verknüpft mehrere Textelemente zu einem Textelement
KONFIDENZ                 | Gibt das Konfidenzintervall für den Erwartungswert einer Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
KONFIDENZ.NORM            | Gibt das Konfidenzintervall für den Erwartungswert einer Zufallsvariablen zurück
KONFIDENZ.T               | Gibt das Konfidenzintervall für den Erwartungswert einer (Student) t-verteilten Zufallsvariablen zurück
UMWANDELN                 | Wandelt eine Zahl von einem Maßsystem in ein anderes um
KORREL                    | Gibt den Korrelationskoeffizienten zweier Reihen von Merkmalsausprägungen zurück
COS                       | Gibt den Kosinus einer Zahl zurück
COSHYP                    | Gibt den hyperbolischen Kosinus einer Zahl zurück
COT                       | Gibt den hyperbolischen Kosinus einer Zahl zurück
COTHYP                    | Gibt den Kotangens eines Winkels zurück
ANZAHL                    | Zählt, wie viele Zahlen in der Liste mit Argumenten enthalten sind
ANZAHL2                   | Zählt, wie viele Werte in der Liste mit Argumenten enthalten sind
ANZAHLLEEREZELLEN         | Zählt die leeren Zellen in einem Bereich
ZÄHLENWENN                | Ermittelt die Anzahl der Zellen in einem Bereich, die den angegebenen Kriterien entsprechen
ZÄHLENWENNS               | Ermittelt die Anzahl der Zellen in einem Bereich, die mehreren Kriterien entsprechen
ZINSTERMTAGVA             | Gibt die Anzahl der Tage vom Anfang des Zinstermins bis zum Abrechnungstermin zurück
ZINSTERMTAGE              | Gibt die Anzahl der Tage der Zinsperiode zurück, die das Abrechnungsdatum einschließt
ZINSTERMTAGNZ             | Gibt die Anzahl der Tage vom Abrechnungstermin bis zum nächsten Zinstermin zurück
ZINSTERMNZ                | Gibt den nächsten Zinstermin nach dem Abrechnungstermin zurück
ZINSTERMZAHL              | Gibt die Anzahl der Zinstermine zwischen Abrechnungs- und Fälligkeitsdatum zurück
ZINSTERMVZ                | Gibt den letzten Zinstermin vor dem Abrechnungstermin zurück
COVAR                     | Gibt die Kovarianz zurück, den Mittelwert der für alle Datenpunktpaare gebildeten Produkte der Abweichungen In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
COVARIANCE.P              | Gibt die Kovarianz zurück, den Mittelwert der für alle Datenpunktpaare gebildeten Produkte der Abweichungen
COVARIANCE.S              | Gibt die Kovarianz einer Stichprobe zurück, d. h. den Mittelwert der für alle Datenpunktpaare gebildeten Produkte der Abweichungen
CRITBINOM                 | Gibt den kleinsten Wert zurück, für den die kumulierten Wahrscheinlichkeiten der Binomialverteilung kleiner oder gleich einer Grenzwahrscheinlichkeit sind. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
COSEC                     | Gibt den Kosekans eines Winkels zurück
COSECHYP                  | Gibt den hyperbolischen Kosekans eines Winkels zurück
KUMZINSZ                  | Berechnet die kumulierten Zinsen, die zwischen zwei Perioden zu zahlen sind
KUMKAPITAL                | Gibt die aufgelaufene Tilgung eines Darlehens zurück, die zwischen zwei Perioden zu zahlen ist
DATUM                     | Gibt die fortlaufende Zahl eines bestimmten Datums zurück
DATEDIF                   | Berechnet die Anzahl der Tage, Monate oder Jahre zwischen zwei Datumsangaben. Diese Funktion ist in Formeln nützlich, in denen Sie ein Alter berechnen müssen
DATWERT                   | Wandelt ein Datum in Form von Text in eine fortlaufende Zahl um
DBMITTELWERT              | Gibt den Mittelwert der ausgewählten Datenbankeinträge zurück
TAG                       | Wandelt eine fortlaufende Zahl in den Tag des Monats um
TAGE                      | Gibt die Anzahl der Tage zwischen zwei Datumswerten zurück
TAGE360                   | Berechnet die Anzahl der Tage zwischen zwei Datumsangaben ausgehend von einem Jahr mit 360 Tagen
GDA2                      | Gibt die geometrisch-degressive Abschreibung eines Vermögenswerts für eine bestimmte Periode zurück
DBANZAHL                  | Zählt die Zellen mit Zahlen in einer Datenbank
DBANZAHL2                 | Zählt nicht leere Zellen in einer Datenbank
GDA                       | Gibt die degressive Doppelratenabschreibung eines Vermögenswerts oder eine mit einer anderen angegebenen Methode berechnete Abschreibung für eine bestimmte Periode zurück
DEZINBIN                  | Konvertiert eine Dezimalzahl in eine binäre Zahl
DEZINHEX                  | Konvertiert eine dezimale Zahl in eine Hexadezimalzahl
DEZINOKT                  | Konvertiert eine Dezimalzahl in eine Oktalzahl
DEZIMAL                   | Konvertiert eine Textdarstellung einer Zahl mit einer angegebenen Basis in eine Dezimalzahl
GRAD                      | Wandelt Bogenmaß (Radiant) in Grad um
DELTA                     | Überprüft, ob zwei Werte gleich sind
SUMQUADABW                | Gibt die Summe der quadrierten Abweichungen zurück
DBAUSZUG                  | Extrahiert aus einer Datenbank einen einzelnen Datensatz, der den angegebenen Kriterien entspricht
DISAGIO                   | Gibt den Abschlag (Disagio) eines Wertpapiers zurück
DBMAX                     | Gibt den größten Wert aus ausgewählten Datenbankeinträgen zurück
DBMIN                     | Gibt den kleinsten Wert aus ausgewählten Datenbankeinträgen zurück
NOTIERUNGDEZ              | Konvertiert eine Notierung, die als Dezimalbruch ausgedrückt wurde, in eine Dezimalzahl
NOTIERUNGBRU              | Konvertiert eine Notierung in dezimaler Schreibweise in einen gemischten Dezimalbruch
DBPRODUKT                 | Multipliziert die Werte in einem bestimmten Feld von Datensätzen, die den Kriterien in einer Datenbank entsprechen
DBSTDABW                  | Schätzt die Standardabweichung basierend auf einer Stichprobe aus ausgewählten Datenbankeinträgen
DBSTDABWN                 | Berechnet die Standardabweichung basierend auf der Grundgesamtheit ausgewählter Datenbankeinträge
DBSUMME                   | Addiert die Zahlen in der Feldspalte von Datensätzen in der Datenbank, die den Kriterien entsprechen
DURATION                  | Gibt die jährliche Duration eines Wertpapiers mit periodischen Zinszahlungen zurück
DBVARIANZ                 | Schätzt die Varianz basierend auf einer Stichprobe aus ausgewählten Datenbankeinträgen
DBVARIANZEN               | Berechnet die Varianz basierend auf der Grundgesamtheit ausgewählter Datenbankeinträge
EDATUM                    | Gibt die fortlaufende Zahl des Datums zurück, das die angegebene Anzahl von Monaten vor oder nach dem Ausgangsdatum liegt
EFFEKTIV                  | Gibt die jährliche Effektivverzinsung zurück
ENCODEURL                 | Gibt eine URL-codierte Zeichenfolge zurück Diese Funktion steht in Excel für das Web nicht zur Verfügung
MONATSENDE                | Gibt die fortlaufende Zahl des letzten Tags des Monats vor oder nach einer bestimmten Anzahl von Monaten zurück
GAUSSFEHLER               | Gibt die Fehlerfunktion zurück
GAUSSFEHLER.GENAU         | Gibt die Fehlerfunktion zurück
GAUSSFKOMPL               | Gibt die komplementäre Fehlerfunktion zurück
GAUSSFKOMPL.GENAU         | Gibt die komplementäre Fehlerfunktion zwischen X und Unendlich integriert zurück
FEHLER.TYP                | Gibt eine Zahl zurück, die einem Fehlertyp entspricht
EUROCONVERT               | Wandelt eine Zahl in Euro oder von Euro in die Währung eines Mitgliedsstaats oder von der Währung eines Euro-Mitgliedsstaats in die Währung eines anderen Mitgliedsstaats um, indem der Euro als Zwischenwert verwendet wird (Triangulieren)
GERADE                    | Rundet eine Zahl auf die nächste gerade ganze Zahl auf
IDENTISCH                 | Überprüft, ob zwei Textwerte identisch sind
EXP                       | Potenziert die Basis e mit der angegebenen Zahl
EXPON.VERT                | Gibt die exponentielle Verteilung zurück
EXPONDIST                 | Gibt die exponentielle Verteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
FAKULTÄT                  | Gibt die Fakultät zu einer Zahl zurück
ZWEIFAKULTÄT              | Gibt die Fakultät zu einer Zahl mit der Schrittlänge 2 zurück
FALSCH                    | Gibt den Wahrheitswert FALSCH zurück
F.VERT                    | Gibt die F-Wahrscheinlichkeitsverteilung zurück
FDIST                     | Gibt die F-Wahrscheinlichkeitsverteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
F.VERT.RE                 | Gibt die F-Wahrscheinlichkeitsverteilung zurück
FINDEN                    | Sucht einen Textwert in einem anderen (Groß-/Kleinschreibung wird berücksichtigt)
FINDENB                   | Sucht einen Textwert in einem anderen (Groß-/Kleinschreibung wird berücksichtigt)
F.INV                     | Gibt Perzentile der F-Verteilung zurück
F.INV.RE                  | Gibt Perzentile der F-Verteilung zurück
FINV                      | Gibt Perzentile der F-Verteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
FISHER                    | Gibt die Fisher-Transformation zurück
FISHERINV                 | Gibt die Umkehrung der Fisher-Transformation zurück
FEST                      | Formatiert eine Zahl als Text mit einer festen Anzahl von Dezimalstellen
UNTERGRENZE               | Rundet eine Zahl in Richtung Null ab In Excel 2007 und Excel 2010 ist dies eine Funktion aus dem Bereich Mathematik und Trigonometrie
UNTERGRENZE.MATHEMATIK    | Rundet eine Zahl auf die nächste ganze Zahl oder auf das kleinste Vielfache des angegebenen Schritts ab
UNTERGRENZE.GENAU         | Rundet eine Zahl auf die nächste ganze Zahl oder auf das kleinste Vielfache des angegebenen Schritts. Die Zahl wird Unabhängig vom ihrem Vorzeichen aufgerundet
PROGNOSE                  | Gibt einen zukünftigen Wert basierend auf vorhandenen Werten zurück
PROGNOSE.LINEAR           | Gibt einen zukünftigen Wert basierend auf vorhandenen Werten zurück
FORMULATEXT               | Gibt die Formel am angegebenen Bezug als Text zurück
HÄUFIGKEIT                | Gibt eine Häufigkeitsverteilung als einspaltige Matrix zurück
F.TEST                    | Gibt die Teststatistik eines F-Tests zurück
FTEST                     | Gibt die Teststatistik eines F-Tests zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
ZW                        | Gibt den zukünftigen Wert einer Investition zurück
ZW2                       | Gibt den aufgezinsten Wert des Anfangskapitals für eine Reihe periodisch unterschiedlicher Zinssätze zurück
GAMMA                     | Gibt den Wert der Gamma-Funktion zurück
GAMMA.VERT                | Gibt Wahrscheinlichkeiten einer gammaverteilten Zufallsvariablen zurück
GAMMADIST                 | Gibt Wahrscheinlichkeiten einer gammaverteilten Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
GAMMA.INV                 | Gibt den Kehrwert der kumulierten Gamma-Verteilung zurück
GAMMAINV                  | Gibt den Kehrwert der kumulierten Gamma-Verteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
GAMMALN                   | Gibt den natürlichen Logarithmus der Gamma-Funktion zurück, Γ(x)
GAMMALN.GENAU             | Gibt den natürlichen Logarithmus der Gamma-Funktion zurück, Γ(x)
GAUSS                     | Gibt 0,5 weniger als die kumulierte Normalverteilung zurück
GGT                       | Gibt den größten gemeinsamen Teiler zurück
GEOMITTEL                 | Gibt das geometrische Mittel zurück
GGANZZAHL                 | Überprüft, ob eine Zahl größer als ein gegebener Schwellenwert ist
GROWTH                    | Gibt Werte zurück, die sich aus einem exponentiellen Trend ergeben
HARMITTEL                 | Gibt das harmonische Mittel zurück
HEXINBIN                  | Wandelt eine hexadezimale Zahl in eine binäre Zahl um
HEXINDEZ                  | Wandelt eine hexadezimale Zahl in eine Dezimalzahl um
HEXINOKT                  | Wandelt eine hexadezimale Zahl in eine Oktalzahl um
WVERWEIS                  | Sucht in der obersten Zeile einer Matrix und gibt den Wert der angegebenen Zelle zurück
STUNDE                    | Wandelt eine fortlaufende Zahl in eine Stunde um
HYPERLINK                 | Erstellt eine Verknüpfung oder einen Sprung, über den ein auf einem Netzwerkserver, in einem Intranet oder im Internet gespeichertes Dokument geöffnet wird
HYPGEOM.VERT              | Gibt Wahrscheinlichkeiten einer hypergeometrisch verteilten Zufallsvariablen zurück
HYPGEOMDIST               | Gibt Wahrscheinlichkeiten einer hypergeometrisch verteilten Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
WENN                      | Gibt einen auszuführenden logischen Test an
WENNFEHLER                | Wenn eine Formel mit einem Fehler ausgewertet wird, wird ein angegebener Wert zurückgegeben; andernfalls wird das Ergebnis der Formel zurückgegeben
WENNNV                    | Gibt den Wert zurück, den Sie angeben, wenn der Ausdruck zu #N/V ausgewertet wird; gibt andernfalls das Ergebnis des Ausdrucks zurück
WENNS                     | Hiermit wird geprüft, ob eine oder mehrere Bedingungen zutreffen, und es wird der Wert zurückgegeben, der der ersten auf WAHR lautenden Bedingung entspricht
IMABS                     | Gibt den Absolutbetrag (Modul) einer komplexen Zahl zurück
IMAGINÄRE                 | Gibt den Imaginärteil einer komplexen Zahl zurück
IMARGUMENT                | Gibt das Argument Theta zurück, einen Winkel, der als Bogenmaß ausgedrückt wird
IMKONJUGIERTE             | Gibt die konjugierte komplexe Zahl zu einer komplexen Zahl zurück
IMCOS                     | Gibt den Kosinus einer komplexen Zahl zurück
IMCOSHYP                  | Gibt den hyperbolischen Kosinus einer komplexen Zahl zurück
IMCOT                     | Gibt den Kotangens einer komplexen Zahl zurück
IMCOSEC                   | Gibt den Kosekans einer komplexen Zahl zurück
IMCOSECHYP                | Gibt den hyperbolischen Kosekans einer komplexen Zahl zurück
IMDIV                     | Gibt den Quotienten zweier komplexer Zahlen zurück
IMEXP                     | Gibt die algebraische Form einer in exponentieller Schreibweise vorliegenden komplexen Zahl zurück
IMLN                      | Gibt den natürlichen Logarithmus einer komplexen Zahl zurück
IMLOG10                   | Gibt den Logarithmus einer komplexen Zahl zur Basis 10 zurück
IMLOG2                    | Gibt den Logarithmus einer komplexen Zahl zur Basis 2 zurück
IMAPOTENZ                 | Gibt eine mit einer ganzen Zahl potenzierte komplexe Zahl zurück
IMPRODUKT                 | Gibt das Produkt von komplexen Zahlen zurück
IMREALTEIL                | Gibt den Realteil einer komplexen Zahl zurück
IMSEC                     | Gibt den Sekans einer komplexen Zahl zurück
IMSECHYP                  | Gibt den hyperbolischen Sekans einer komplexen Zahl zurück
IMSIN                     | Gibt den Sinus einer komplexen Zahl zurück
IMSINHYP                  | Gibt den hyperbolischen Sinus einer komplexen Zahl zurück
IMWURZEL                  | Gibt die Quadratwurzel einer komplexen Zahl zurück
IMSUB                     | Gibt die Differenz zwischen zwei komplexen Zahlen zurück
IMSUMME                   | Gibt die Summe von komplexen Zahlen zurück
IMTAN                     | Gibt den Tangens einer komplexen Zahl zurück
INDEX                     | Verwendet einen Index, um einen Wert aus einem Bezug oder einem Array auszuwählen
INDIREKT                  | Gibt einen Bezug zurück, der von einem Textwert angegeben wird
GANZZAHL                  | Rundet eine Zahl auf die nächste ganze Zahl ab
INTERCEPT                 | Gibt den Schnittpunkt der linearen Regressionsgeraden zurück
ZINSSATZ                  | Gibt den Zinssatz eines voll investierten Wertpapiers zurück
ZINSZ                     | Gibt die Zinszahlung einer Investition für eine angegebene Periode zurück
IKV                       | Gibt den internen Zinsfuß für eine Reihe von Zahlungen zurück
ISTLEER                   | Gibt WAHR zurück, wenn der Wert leer ist
ISTFEHL                   | Gibt WAHR zurück, wenn der Wert ein beliebiger Fehlerwert außer #NV ist
ISTFEHLER                 | Gibt WAHR zurück, wenn der Wert ein beliebiger Fehlerwert ist
ISTGERADE                 | Gibt WAHR zurück, wenn die Zahl gerade ist
ISTFORMEL                 | Gibt WAHR zurück, wenn ein Bezug auf eine Zelle vorhanden ist, die eine Formel enthält
ISTLOG                    | Gibt WAHR zurück, wenn der Wert ein Wahrheitswert ist
ISTNV                     | Gibt WAHR zurück, wenn der Wert der Fehlerwert #NV ist
ISTKTEXT                  | Gibt WAHR zurück, wenn der Wert kein Text ist
ISTZAHL                   | Gibt WAHR zurück, wenn der Wert eine Zahl ist
ISTUNGERADE               | Gibt WAHR zurück, wenn die Zahl ungerade ist
ISTBEZUG                  | Gibt WAHR zurück, wenn der Wert ein Bezug ist
ISTTEXT                   | Gibt WAHR zurück, wenn der Wert ein Text ist
ISO.OBERGRENZE            | Gibt eine Zahl zurück, die auf die nächste ganze Zahl oder auf das kleinste Vielfache des angegebenen Schritts aufgerundet ist
ISOKALENDERWOCHE          | Gibt die Zahl der ISO-Kalenderwoche des Jahres für ein angegebenes Datum zurück
ISPMT                     | Berechnet die während eines bestimmten Zeitraums für eine Investition gezahlten Zinsen
KURT                      | Gibt die Kurtosis (Exzess) einer Datengruppe zurück
KGRÖSSTE                  | Gibt den k-größten Wert innerhalb einer Datengruppe zurück
KGV                       | Gibt das kleinste gemeinsame Vielfache zurück
LINKS                     | Gibt die Zeichen ganz links aus einem Textwert zurück
LINKSB                    | Gibt die Zeichen ganz links aus einem Textwert zurück
LÄNGE                     | Gibt die Anzahl der Zeichen in einer Textzeichenfolge zurück
LÄNGEB                    | Gibt die Anzahl der Zeichen in einer Textzeichenfolge zurück
LN                        | Gibt den natürlichen Logarithmus einer Zahl zurück
LOG                       | Gibt den Logarithmus einer Zahl zur angegebenen Basis zurück
LOG10                     | Gibt den Logarithmus einer Zahl zur Basis 10 zurück
LOGEST                    | Gibt die Parameter eines exponentiellen Trends zurück
LOGINV                    | Gibt Perzentile der Lognormalverteilung zurück
LOGNORM.VERT              | Gibt die Werte der Verteilungsfunktion einer lognormalverteilten Zufallsvariablen zurück
LOGNORMDIST               | Gibt die Werte der Verteilungsfunktion einer lognormalverteilten Zufallsvariablen zurück
LOGNORM.INV               | Gibt Perzentile der Lognormalverteilung zurück
KLEIN                     | Wandelt Text in Kleinbuchstaben um
VERGLEICH                 | Sucht Werte in einem Bezug oder in einer Matrix
MAX                       | Gibt den größten Wert in einer Liste mit Argumenten zurück
MAXA                      | Gibt den größten Wert in einer Liste mit Argumenten zurück. Dazu zählen Zahlen, Text und Wahrheitswerte
MAXWENNS                  | Gibt den Maximalwert aus Zellen zurück, die mit einem bestimmten Satz Bedingungen oder Kriterien angegeben wurden
MDET                      | Gibt die Determinante einer Matrix zurück
MDURATION                 | Gibt die modifizierte Macauley-Dauer eines Wertpapiers mit einem angenommenen Nennwert von 100 $ zurück
MEDIAN                    | Gibt den Median der angegebenen Zahlen zurück
TEIL                      | Gibt eine bestimmte Anzahl Zeichen aus einer Textzeichenfolge zurück, die den angegebenen Stelle beginnt
TEILB                     | Gibt eine bestimmte Anzahl Zeichen aus einer Textzeichenfolge zurück, die den angegebenen Stelle beginnt
MIN                       | Gibt den kleinsten Wert in einer Liste mit Argumenten zurück
MINWENNS                  | Gibt den Minimalwert aus Zellen zurück, die mit einem bestimmten Satz Bedingungen oder Kriterien angegeben wurden
MINA                      | Gibt den kleinsten Wert in einer Liste mit Argumenten zurück. Dazu zählen Zahlen, Text und Wahrheitswerte
MINUTE                    | Wandelt eine fortlaufende Zahl in eine Minute um
MINVERSE                  | Gibt die Inverse einer Matrix zurück
QIKV                      | Gibt den internen Zinsfuß zurück, wobei positive und negative Zahlungen zu unterschiedlichen Sätzen finanziert werden
MMULT                     | Gibt das Produkt zweier Matrizen zurück
REST                      | Gibt den Rest einer Division zurück
MODE                      | Gibt den am häufigsten vorkommenden Wert in einer Datengruppe zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
MODE.MULT                 | Gibt ein vertikales Array der am häufigsten vorkommenden oder wiederholten Werte in einem Array oder Datenbereich zurück
MODE.SNGL                 | Gibt den am häufigsten vorkommenden Wert in einer Datengruppe zurück
MONAT                     | Wandelt eine fortlaufende Zahl in einen Monat um
VRUNDEN                   | Gibt eine auf das gewünschte Vielfache gerundete Zahl zurück
POLYNOMIAL                | Gibt den Polynomialkoeffizienten einer Gruppe von Zahlen zurück
MEINHEIT                  | Gibt die Einheitsmatrix für die angegebene Größe zurück
N                         | Gibt einen Wert zurück, der in eine Zahl umgewandelt wurde
NV                        | Gibt den Fehlerwert #NV zurück
NEGBINOM.VERT             | Gibt Wahrscheinlichkeiten einer negativ binomialverteilten Zufallsvariablen zurück
NEGBINOMDIST              | Gibt Wahrscheinlichkeiten einer negativ binomialverteilten Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
NETTOARBEITSTAGE          | Gibt die Anzahl der vollen Arbeitstage zwischen zwei Datumswerten zurück
NETTOARBEITSTAGE.INTL     | ExceGibt die Anzahl der vollen Arbeitstage zwischen zwei Datumsangaben zurück. Dabei werden Parameter verwendet, um anzugeben, welche und wie viele Tage auf Wochenenden fallen
NOMINAL                   | Gibt die jährliche Nominalverzinsung zurück
NORM.VERT                 | Gibt Wahrscheinlichkeiten einer normalverteilten Zufallsvariablen zurück
NORMDIST                  | Gibt Wahrscheinlichkeiten einer normalverteilten Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
NORMINV                   | Gibt Perzentile der Normalverteilung zurück
NORM.INV                  | Gibt Perzentile der Normalverteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
NORM.S.VERT               | Gibt die Standardnormalverteilung zurück
NORMSDIST                 | Gibt die Standardnormalverteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
NORM.S.INV                | Gibt Perzentile der Standardnormalverteilung zurück
NORMSINV                  | Gibt Perzentile der Standardnormalverteilung zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
NICHT                     | Kehrt die Logik der Argumente um
JETZT                     | Gibt die fortlaufende Zahl des aktuellen Datums und der aktuellen Uhrzeit zurück
ZZR                       | Gibt die Anzahl der Zahlungsperioden einer Investition zurück
NBW                       | Gibt den Nettobarwert einer Investition auf Basis periodisch anfallender Zahlungen und eines Abzinsungssatzes zurück
OKTINBIN                  | Wandelt eine oktale Zahl in eine binäre Zahl (Dualzahl) um
OKTINDEZ                  | Wandelt eine oktale Zahl in eine dezimale Zahl um
OKTINHEX                  | Wandelt eine oktale Zahl in eine hexadezimale Zahl um
UNGERADE                  | Rundet eine Zahl auf die nächste ungerade ganze Zahl auf
UNREGER.KURS              | Gibt den Kurs pro 100 $ Nennwert eines Wertpapiers mit einem unregelmäßigen ersten Zinstermin zurück
UNREGER.REND              | Gibt die Rendite eines Wertpapiers mit einem unregelmäßigen ersten Zinstermin zurück
UNREGLE.KURS              | Gibt den Kurs pro 100 $ Nennwert eines Wertpapiers mit einem unregelmäßigen letzten Zinstermin zurück
UNREGLE.REND              | Gibt die Rendite eines Wertpapiers mit einem unregelmäßigen letzten Zinstermin zurück
ODER                      | Gibt WAHR zurück, wenn ein Argument WAHR ist
PDURATION                 | Gibt die Anzahl der Zahlungsperioden zurück, die eine Investition zum Erreichen eines angegebenen Werts benötigt
PEARSON                   | Gibt den Pearsonschen Korrelationskoeffizienten zurück
QUANTIL.EXKL              | Gibt das k-Quantil von Werten in einem Bereich zurück, wobei k im Bereich von 0..1 ausschließlich liegt
QUANTIL.INKL              | Gibt das k-Quantil von Werten in einem Bereich zurück
PERCENTILE                | Gibt das k-Quantil von Werten in einem Bereich zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
QUANTILSRANG.EXKL         | Gibt den prozentualen Rang eines Werts in einem Dataset als Prozentsatz des Datasets (0..1 ausschließlich) zurück
QUANTILSRANG.INKL         | Gibt den prozentualen Rang eines Werts in einer Datengruppe zurück
PERCENTRANK               | Gibt den prozentualen Rang eines Werts in einer Datengruppe zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
VARIATIONEN               | Gibt die Anzahl der Permutationen für eine bestimmte Anzahl von Objekten zurück
VARIATIONEN2              | Gibt die Anzahl der Permutationen für eine angegebene Anzahl von Objekten zurück (mit Wiederholungen), die aus der Gesamtmenge der Objekte ausgewählt werden können
PHI                       | Gibt den Wert der Dichtefunktion für eine Standardnormalverteilung zurück
PI                        | Gibt den Wert von Pi zurück
RMZ                       | Gibt die periodische Zahlung für eine Annuität zurück
POISSON.VERT              | Gibt Wahrscheinlichkeiten einer poissonverteilten Zufallsvariablen zurück
POISSON                   | Gibt Wahrscheinlichkeiten einer poissonverteilten Zufallsvariablen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
POTENZ                    | Gibt als Ergebnis eine potenzierte Zahl zurück
KAPZ                      | Gibt die Kapitalrückzahlung einer Investition für eine angegebene Periode zurück
KURS                      | Gibt den Kurs pro 100 $ Nennwert eines Wertpapiers zurück, das periodisch Zinsen auszahlt
KURSDISAGIO               | Gibt den Kurs pro 100 $ Nennwert eines unverzinslichen Wertpapiers zurück
KURSFÄLLIG                | Gibt den Kurs pro 100 $ Nennwert eines Wertpapiers zurück, das Zinsen am Fälligkeitsdatum auszahlt
WAHRSCHBEREICH            | Gibt die Wahrscheinlichkeit zurück, dass die Werte in einem Bereich zwischen zwei Grenzwerten liegen
PRODUKT                   | Multipliziert die Argumente
GROSS2                    | Schreibt den ersten Buchstaben jedes Worts in einem Textwert groß
BW                        | Gibt den Barwert einer Investition zurück
QUARTILE                  | Gibt die Quartile einer Datengruppe zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
QUARTILE.EXKL             | Gibt die Quartile eines Datasets zurück, basierend auf Perzentilwerten von 0..1 ausschließlich
QUARTILE.INKL             | Gibt die Quartile einer Datengruppe zurück
QUOTIENT                  | Gibt den ganzzahligen Teil einer Division zurück
BOGENMASS                 | Rechnet Grad in Bogenmaß um
ZUFALLSZAHL               | Gibt eine Zufallszahl zwischen 0 und 1 zurück
ZUFALLSBEREICH            | Gibt eine Zufallszahl zwischen den angegebenen Zahlen zurück
RANG.GLEICH               | Gibt den Rang einer Zahl in einer Liste von Zahlen zurück
RANK                      | Gibt den Rang einer Zahl in einer Liste von Zahlen zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
ZINS                      | Gibt den Zinssatz pro Zeitraum einer Annuität zurück
AUSZAHLUNG                | Gibt den bei Fälligkeit für ein vollständig angelegtes Wertpapier erhaltenen Betrag zurück
ERSETZEN                  | Ersetzt Zeichen in Text
ERSETZENB                 | Ersetzt Zeichen in Text
WIEDERHOLEN               | Wiederholt einen Text so oft wie angegeben
RECHTS                    | Gibt die Zeichen ganz rechts aus einem Textwert zurück
RECHTSB                   | Gibt die Zeichen ganz rechts aus einem Textwert zurück
RÖMISCH                   | Wandelt eine arabische Zahl in eine römische Zahl als Text um
RUNDEN                    | Rundet eine Zahl auf eine angegebene Anzahl von Stellen
ABRUNDEN                  | Rundet eine Zahl in Richtung Null ab
AUFRUNDEN                 | Rundet eine Zahl von Null aus auf
ROW                       | Gibt die Zeilennummer eines Bezugs zurück
ZEILEN                    | Gibt die Anzahl von Zeilen in einem Bezug zurück
ZSATZINVEST               | Gibt den effektiven Jahreszins für den Wertzuwachs einer Investition zurück
RSQ                       | Gibt das Quadrat des Pearsonschen Korrelationskoeffizienten zurück
SUCHEN                    | Sucht einen in einem anderen Textwert enthaltenen Textwert (Groß-/Kleinschreibung wird nicht beachtet)
SUCHENB                   | Sucht einen in einem anderen Textwert enthaltenen Textwert (Groß-/Kleinschreibung wird nicht beachtet)
SEC                       | Gibt den Sekans eines Winkels zurück
SECHYP                    | Gibt den hyperbolischen Sekans eines Winkels zurück
SEKUNDE                   | Wandelt eine fortlaufende Zahl in eine Sekunde um
POTENZREIHE               | Gibt die Summe einer Potenzreihe auf der Grundlage der Formel zurück
BLATT                     | Gibt die Blattnummer des Blatts zurück, auf das verwiesen wird
BLÄTTER                   | Gibt die Anzahl von Blättern in einem Bezug zurück
VORZEICHEN                | Gibt das Vorzeichen einer Zahl zurück
SIN                       | Gibt den Sinus des angegebenen Winkels zurück
SINHYP                    | Gibt den hyperbolischen Sinus einer Zahl zurück
SCHIEFE                   | Gibt die Schiefe einer Verteilung zurück
SCHIEFE.P                 | Gibt die Schiefe einer Verteilung auf der Basis einer Grundgesamtheit zurück: eine Charakterisierung des Asymmetriegrads einer Verteilung um ihren Mittelwert
LIA                       | Gibt die lineare Abschreibung eines Vermögenswerts für einen Zeitraum zurück
SLOPE                     | Gibt die Steigung der linearen Regressionsgeraden zurück
KKLEINSTE                 | Gibt den k-kleinsten Wert innerhalb einer Datengruppe zurück
WURZEL                    | Gibt die Quadratwurzel einer Zahl zurück
WURZELPI                  | Gibt die Quadratwurzel von (Zahl \* Pi) zurück
STANDARDISIERUNG          | Gibt einen standardisierten Wert zurück
STDEV                     | Schätzt die Standardabweichung auf der Grundlage einer Stichprobe
STABW.P                   | Berechnet die Standardabweichung anhand der Grundgesamtheit
STABW.S                   | Schätzt die Standardabweichung auf der Grundlage einer Stichprobe
STABWA                    | Schätzt die Standardabweichung ausgehend von einer Stichprobe, die Zahlen, Text und Wahrheitswerte enthält
STDEVP                    | Berechnet die Standardabweichung anhand der Grundgesamtheit In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
STABWNA                   | Berechnet die Standardabweichung auf der Grundlage der Grundgesamtheit, die Zahlen, Text und Wahrheitswerte enthält
STFEHLERYX                | Gibt den Standardfehler der geschätzten y-Werte für alle x-Werte der Regression zurück
WECHSELN                  | Ersetzt alten Text in einer Textzeichenfolge durch neuen Text
TEILERGEBNIS              | Gibt ein Teilergebnis in einer Liste oder Datenbank zurück
SUMME                     | Addiert die zugehörigen Argumente
SUMMEWENN                 | Addiert die nach einem bestimmten Kriterium angegebenen Zellen
SUMMEWENNS                | Addiert die Zellen in einem Bereich, die mehreren Kriterien entsprechen
SUMMENPRODUKT             | Gibt die Summe der Produkte entsprechender Matrixkomponenten zurück
QUADRATESUMME             | Gibt die Summe der Quadrate der Argumente zurück
SUMMEX2MY2                | Gibt die Summe der Differenz von Quadraten entsprechender Werte in zwei Matrizen zurück
SUMMEX2PY2                | Gibt die Summe der Summe von Quadraten entsprechender Werte in zwei Matrizen zurück
SUMMEXMY2                 | Gibt die Summe der Quadrate von Differenzen entsprechender Werte in zwei Matrizen zurück
SWITCH                    | Wertet einen Ausdruck anhand einer Liste mit Werten aus. Als Ergebnis wird der erste übereinstimmende Wert zurückgegeben. Wenn es keine Übereinstimmung gibt, kann ein optionaler Standardwert zurückgegeben werden
DIA                       | Gibt die Abschreibung eines Vermögenswerts im Hinblick auf die Zahlen der Jahressumme für einen bestimmten Zeitraum zurück
T                         | Wandelt die eigenen Argumente in Text um
TAN                       | Gibt den Tangens einer Zahl zurück
TANHYP                    | Gibt den hyperbolischen Tangens einer Zahl zurück
TBILLÄQUIV                | Gibt die Rendite eines Schatzwechsels zurück
TBILLKURS                 | Gibt den Kurs pro 100 $ Nennwert für einen Schatzwechsel zurück
TBILLRENDITE              | Gibt die Rendite für einen Schatzwechsel zurück
T.VERT                    | Gibt die Prozentpunkte (Wahrscheinlichkeit) entsprechend der Student-t-Verteilung zurück
T.VERT.2S                 | Gibt die Prozentpunkte (Wahrscheinlichkeit) entsprechend der Student-t-Verteilung zurück
T.VERT.RE                 | Gibt Werte der (Student) t-Verteilung zurück
TDIST                     | Gibt Werte der (Student) t-Verteilung zurück
TEXT                      | Formatiert eine Zahl und wandelt sie in Text um
TEXTVERKETTEN             | Kombiniert den Text aus mehreren Bereichen und/oder Zeichenfolgen
ZEIT                      | Gibt die fortlaufende Zahl einer bestimmten Uhrzeit zurück
ZEITWERT                  | Wandelt eine Uhrzeit in Form von Text in eine fortlaufende Zahl um
T.INV                     | Gibt den t-Wert der (Student) t-Verteilung als Funktion der Wahrscheinlichkeit und der Freiheitsgrade zurück
T.INV.2S                  | Gibt Perzentile der (Student) t-Verteilung zurück
TINV                      | Gibt Perzentile der (Student) t-Verteilung zurück
HEUTE                     | Gibt die fortlaufende Zahl des heutigen Datums zurück
MTRANS                    | Gibt die Transponierte einer Matrix zurück
TREND                     | Gibt Werte zurück, die sich aus einem linearen Trend ergeben
GLÄTTEN                   | Entfernt Leerzeichen aus Text
GESTUTZTMITTEL            | Gibt den Mittelwert des inneren Teils einer Datengruppe zurück
WAHR                      | Gibt den Wahrheitswert WAHR zurück
KÜRZEN                    | Kürzt eine Zahl auf eine ganze Zahl
T.TEST                    | Gibt die Teststatistik eines (Student) t-Tests zurück
TTEST                     | Gibt die Teststatistik eines (Student) t-Tests zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
TYP                       | Gibt eine Zahl zurück, die den Datentyp eines Werts angibt
UNIZEICHEN                | Gibt das Unicode-Zeichen zurück, auf das durch den angegebenen Zahlenwert verwiesen wird
UNICODE                   | Gibt die Zahl (Codepoint) zurück, die dem ersten Zeichen des Texts entspricht
GROSS                     | Wandelt Text in Großbuchstaben um
WERT                      | Wandelt ein Textargument in eine Zahl um
WERTZUTEXT                | Gibt Text aus einem beliebigen angegebenen Wert zurück
VARIANZ                   | Schätzt die Varianz anhand einer Stichprobe. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
VAR.P                     | Berechnet die Varianz anhand der Grundgesamtheit
VAR.S                     | Schätzt die Varianz anhand einer Stichprobe
VARIANZA                  | Schätzt die Varianz ausgehend von einer Stichprobe, die Zahlen, Text und Wahrheitswerte enthält
VARP                      | Berechnet die Varianz anhand der Grundgesamtheit. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
VARIANZENA                | Berechnet die Varianz auf der Grundlage der Grundgesamtheit, die Zahlen, Text und Wahrheitswerte enthält
VDB                       | Gibt die degressive Abschreibung eines Vermögenswerts für eine bestimmte Periode oder Teilperiode zurück
SVERWEIS                  | Sucht in der ersten Spalte einer Matrix und dann zeilenweise, um den Wert einer Zelle zurückzugeben
WOCHENTAG                 | Wandelt eine fortlaufende Zahl in den Tag der Woche um
KALENDERWOCHE             | Wandelt eine fortlaufende Zahl in eine Zahl um, die angibt, in welche Woche eines Jahres das angegebene Datum fällt
WEIBULL                   | Berechnet die Varianz auf der Grundlage der Grundgesamtheit, die Zahlen, Text und Wahrheitswerte enthält In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik
WEIBULL.VERT              | Gibt Wahrscheinlichkeiten einer Weibull-verteilten Zufallsvariablen zurück
ARBEITSTAG                | Gibt die fortlaufende Zahl des Datums vor oder nach einer bestimmten Anzahl von Arbeitstagen zurück
ARBEITSTAG.INTL           | Gibt die fortlaufende Zahl des Datums zurück, das vor oder nach einer bestimmten Anzahl von Arbeitstagen liegt. Dabei werden Parameter verwendet, um anzugeben, welche und wie viele Tage auf Wochenenden fallen
XINTZINSFUSS              | Gibt den internen Zinsfuß für eine Reihe nicht unbedingt periodisch anfallender Zahlungen zurück
XLOOKUP                   | Die XVERWEIS-Funktion sucht nach einem Bereich oder einer Matrix und gibt ein Element zurück, das zur ersten gefundenen Übereinstimmung passt. Wenn es keine Übereinstimmung gibt, kann XVERWEIS die beste (ungefähre) Übereinstimmung zurückgeben
XKAPITALWERT              | Gibt den Nettobarwert für eine Reihe nicht unbedingt periodisch anfallender Zahlungen zurück
XODER                     | Gibt ein logisches exklusives ODER aller Argumente zurück
JAHR                      | Wandelt eine fortlaufende Zahl in ein Jahr um
BRTEILJAHRE               | Gibt die Anzahl der ganzen Tage zwischen Ausgangsdatum und Enddatum in Bruchteilen von Jahren zurück
RENDITE                   | Gibt die Rendite eines Wertpapiers zurück, das regelmäßig Zinsen abwirft
RENDITEDIS                | Gibt die jährliche Rendite eines diskontierten Wertpapiers zurück, zum Beispiel eines Schatzwechsels
RENDITEFÄLL               | Gibt die Jahresrendite für ein Wertpapier zurück, für das Zinsen bei Fälligkeit gezahlt werden
G.TEST                    | Gibt den einseitigen Wahrscheinlichkeitswert für einen Gauß-Test (Normalverteilung) zurück
GTEST                     | Gibt den einseitigen Wahrscheinlichkeitswert für einen Gauß-Test (Normalverteilung) zurück. In Excel 2007 ist dies ist eine Funktion aus dem Bereich Statistik

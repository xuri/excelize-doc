# Zelle

RichTextRun ordnet die Einstellungen des Rich-Text-Laufs direkt zu.

```go
type RichTextRun struct {
    Font *Font
    Text string
}
```

HyperlinkOpts können an [`SetCellHyperlink`](cell.md#SetCellHyperlink) übergeben werden, um optionale Hyperlink-Attribute festzulegen (z. B. anzugebender Text und Text mit Bildschirmtipps).

```go
type HyperlinkOpts struct {
    Display *string
    Tooltip *string
}
```

FormulaOpts können an [`SetCellFormula`](cell.md#SetCellFormula) übergeben werden, um andere Formeltypen zu verwenden.

```go
type FormulaOpts struct {
    Type *string // Formeltyp
    Ref  *string // Gemeinsame Formelreferenz
}
```

## Festlegen des Zellenwerts {#SetCellValue}

```go
func (f *File) SetCellValue(sheet, axis string, value interface{}) error
```

SetCellValue bietet eine Funktion zum Festlegen des Werts einer Zelle. Die angegebenen Koordinaten sollten sich nicht in der ersten Zeile der Tabelle befinden. Im Folgenden werden die unterstützten Datentypen angezeigt:

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

## Festlegen eines booleschen Werts {#SetCellBool}

```go
func (f *File) SetCellBool(sheet, axis string, value bool) error
```

SetCellBool bietet eine Funktion zum Festlegen des Bool-Typwerts einer Zelle anhand des angegebenen Arbeitsblattnamens, der Zellkoordinaten und des Zellenwerts.

## Festlegen des RAW-Werts {#SetCellDefault}

```go
func (f *File) SetCellDefault(sheet, axis, value string) error
```

SetCellDefault bietet eine Funktion zum Festlegen des Zeichenfolgentypwerts einer Zelle als Standardformat, ohne die Zelle zu verlassen.

## Ganzzahlwert festlegen {#SetCellInt}

```go
func (f *File) SetCellInt(sheet, axis string, value int) error
```

SetCellInt bietet eine Funktion zum Festlegen des Int-Typ-Werts einer Zelle anhand des angegebenen Arbeitsblattnamens, der Zellkoordinaten und des Zellenwerts.

## Festlegen des Zeichenfolgenwerts {#SetCellStr}

```go
func (f *File) SetCellStr(sheet, axis, value string) error
```

SetCellStr bietet eine Funktion zum Festlegen des Zeichenfolgentypwerts einer Zelle. Die Gesamtzahl der Zeichen, die eine Zelle `32767` Zeichen enthalten kann.

## Festlegen des Zellstils {#SetCellStyle}

```go
func (f *File) SetCellStyle(sheet, hcell, vcell string, styleID int) error
```

SetCellStyle bietet eine Funktion zum Hinzufügen von Stilattributen für Zellen anhand des angegebenen Arbeitsblattnamens, des Koordinatenbereichs und der Stil-ID. Stilindizes können mit der Funktion [`NewStyle`](style.md#NewStyle) abgerufen werden. Beachten Sie, dass die Rahmen vom Typ `diagonalDown` und `diagonalUp` dieselbe Farbe im selben Koordinatenbereich verwenden sollten. SetCellStyle überschreibt die vorhandenen Stile für die Zelle, fügt Stile nicht an oder führt sie mit vorhandenen Stilen zusammen.

- Beispiel 1: Erstellen Sie Ränder der Zelle `D7` auf `Sheet1`:

```go
style, err := f.NewStyle(`{
    "border": [
    {
        "type": "left",
        "color": "0000FF",
        "style": 3
    },
    {
        "type": "top",
        "color": "00FF00",
        "style": 4
    },
    {
        "type": "bottom",
        "color": "FFFF00",
        "style": 5
    },
    {
        "type": "right",
        "color": "FF0000",
        "style": 6
    },
    {
        "type": "diagonalDown",
        "color": "A020F0",
        "style": 7
    },
    {
        "type": "diagonalUp",
        "color": "A020F0",
        "style": 8
    }]
}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_01.png" alt="Legen Sie einen Rahmenstil für eine Zelle fest"></p>

Die vier Ränder der Zelle `D7` sind mit unterschiedlichen Stilen und Farben festgelegt. Dies hängt mit den Parametern beim Aufrufen der Funktion [`NewStyle`](style.md#NewStyle) zusammen. Sie müssen verschiedene Stile festlegen, um auf die Dokumentation zu diesem Kapitel zu verweisen.

- Beispiel 2: Festlegen des Verlaufsstils für die Arbeitsblattzelle `D7` mit dem Namen `Sheet1`:

```go
style, err := f.NewStyle(`{"fill":{"type":"gradient","color":["#FFFFFF","#E0EBF5"],"shading":1}}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_02.png" alt="Legen Sie einen Verlaufsstil für die Zelle fest"></p>

Die Zelle `D7` wird mit der Farbfüllung des Verlaufseffekts eingestellt. Der Gradientenfüllungseffekt hängt mit dem Parameter zusammen, wenn die Funktion [`NewStyle`](style.md#NewStyle) aufgerufen wird. Sie müssen verschiedene Stile festlegen, um auf die Dokumentation dieses Kapitels zu verweisen.

- Beispiel 3: Legen Sie eine feste Füllung für die `D7`-Zelle mit dem Namen `Sheet1` fest:

```go
style, err := f.NewStyle(`{"fill":{"type":"pattern","color":["#E0EBF5"],"pattern":1}}`)
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
style, err := f.NewStyle(`{
    "alignment":
    {
        "horizontal": "center",
        "ident": 1,
        "justify_last_line": true,
        "reading_order": 0,
        "relative_indent": 1,
        "shrink_to_fit": true,
        "text_rotation": 45,
        "vertical": "",
        "wrap_text": true
    }
}`)
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
style, err := f.NewStyle(`{"number_format": 22}`)
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
style, err := f.NewStyle(`{
    "font":
    {
        "bold": true,
        "italic": true,
        "family": "Times New Roman",
        "size": 36,
        "color": "#777777"
    }
}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

<p align="center"><img width="612" src="./images/SetCellStyle_06.png" alt="Legen Sie Schriftart, Schriftgröße, Farbe und Versatzstil für Zellen fest"></p>

- Beispiel 7: Sperren und Ausblenden der `D7`-Zelle des Arbeitsblatts mit dem Namen `Sheet1`:

```go
style, err := f.NewStyle(`{"protection":{"hidden":true, "locked":true}}`)
if err != nil {
    fmt.Println(err)
}
err = f.SetCellStyle("Sheet1", "D7", "D7", style)
```

Schützen Sie das Arbeitsblatt, um eine Zelle zu sperren oder eine Formel auszublenden. Klicken Sie auf der Registerkarte "Überprüfen" auf "Arbeitsblatt schützen".

## Festlegen eines Hyperlinks {#SetCellHyperLink}

```go
func (f *File) SetCellHyperLink(sheet, axis, link, linkType string) error
```

SetCellHyperLink bietet eine Funktion zum Festlegen von Zellen-Hyperlinks anhand des angegebenen Arbeitsblattnamens und der Link-URL-Adresse. LinkType definiert zwei Arten von Hyperlinks: `External` für die Website oder `Location` für das Verschieben in eine der Zellen in dieser Arbeitsmappe. Die maximale Anzahl von Hyperlinks in einem Arbeitsblatt beträgt `65530`. Unten finden Sie ein Beispiel für einen externen Link.

- Beispiel 1: Hinzufügen eines externen Links zur `A3`-Zelle des Arbeitsblatts mit dem Namen `Sheet1`:

```go
err := f.SetCellHyperLink("Sheet1", "A3",
    "https://github.com/xuri/excelize", "External")
// Legen Sie die Schriftart und den Unterstreichungsstil für die Zelle fest
style, err := f.NewStyle(`{"font":{"color":"#1265BE","underline":"single"}}`)
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
                Color:  "2354e8",
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
            Text: "italic",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "e83723",
                Italic: true,
                Family: "Times New Roman",
            },
        },
        {
            Text: "text with color and font-family,",
            Font: &excelize.Font{
                Bold:   true,
                Color:  "2354e8",
                Family: "Times New Roman",
            },
        },
        {
            Text: "\r\nlarge text with ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "strike",
            Font: &excelize.Font{
                Color:  "e89923",
                Strike: true,
            },
        },
        {
            Text: " and ",
            Font: &excelize.Font{
                Size:  14,
                Color: "ad23e8",
            },
        },
        {
            Text: "underline.",
            Font: &excelize.Font{
                Color:     "23e833",
                Underline: "single",
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
func (f *File) GetCellRichText(sheet, cell string) (runs []RichTextRun, err error)
```

GetCellRichText bietet eine Funktion zum Abrufen des Rich-Textes von Zellen anhand eines bestimmten Arbeitsblatts.

## Abrufen des Zellenwerts {#GetCellValue}

```go
func (f *File) GetCellValue(sheet, axis string, opts ...Options) (string, error)
```

Der Wert der Zelle wird gemäß dem angegebenen Arbeitsblatt und den angegebenen Zellkoordinaten abgerufen, und der Rückgabewert wird in den Typ `string` konvertiert. Wenn das Zellenformat auf den Wert einer Zelle angewendet werden kann, wird der angewendete Wert zurückgegeben, andernfalls wird der ursprüngliche Wert zurückgegeben. Die Werte aller Zellen sind in einem zusammengeführten Bereich gleich.

## Abrufen des gesamten Zellenwerts nach Spalten {#GetCols}

```go
func (f *File) GetCols(sheet string, opts ...Options) ([][]string, error)
```

Ruft den Wert aller Zellen nach Spalten im Arbeitsblatt ab, basierend auf dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten), der als zweidimensionales Array zurückgegeben wird, wobei der Wert der Zelle in den Typ `string` konvertiert wird. Wenn das Zellenformat auf den Wert der Zelle angewendet werden kann, wird der angewendete Wert verwendet, andernfalls wird der ursprüngliche Wert verwendet.

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

Ruft den Wert aller Zellen nach Zeilen im Arbeitsblatt ab, basierend auf dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten), der als zweidimensionales Array zurückgegeben wird, wobei der Wert der Zelle in den Typ `string` konvertiert wird. Wenn das Zellenformat auf den Wert der Zelle angewendet werden kann, wird der angewendete Wert verwendet, andernfalls wird der ursprüngliche Wert verwendet. GetRows holte die Zeilen mit Wert- oder Formelzellen, die am Ende ständig leere Zelle wird übersprungen.

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
func (f *File) GetCellHyperLink(sheet, axis string) (bool, string, error)
```

Ruft einen Zellen-Hyperlink ab, der auf dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten) und den Zellkoordinaten basiert. Wenn die Zelle einen Hyperlink hat, gibt sie `true` und die Linkadresse zurück, andernfalls `false` und eine leere Linkadresse.

Holen Sie sich beispielsweise einen Hyperlink zu einer `H6`-Zelle in einem Arbeitsblatt mit dem Namen `Sheet1`:

```go
link, target, err := f.GetCellHyperLink("Sheet1", "H6")
```

## Stilindex abrufen {#GetCellStyle}

```go
func (f *File) GetCellStyle(sheet, axis string) (int, error)
```

Der Zellenstilindex wird aus dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten) und den Zellkoordinaten abgerufen, und der erhaltene Index kann als Parameter zum Aufrufen der Funktion `SetCellValue` beim Kopieren des Zellenstils verwendet werden.

## Zusammenführen von Zellen {#MergeCell}

```go
func (f *File) MergeCell(sheet, hcell, vcell string) error
```

Führen Sie Zellen basierend auf dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten) und den Zellkoordinatenbereichen zusammen. Beim Zusammenführen von Zellen wird nur der obere linke Zellenwert beibehalten und die anderen Werte verworfen. Führen Sie beispielsweise Zellen im Bereich `D3:E9` in einem Arbeitsblatt mit dem Namen `Sheet1` zusammen:

```go
err := f.MergeCell("Sheet1", "D3", "E9")
```

Wenn sich der angegebene Zellkoordinatenbereich mit anderen vorhandenen zusammengeführten Zellen überschneidet, werden die vorhandenen zusammengeführten Zellen gelöscht.

## Unmerge-Zellen {#UnmergeCell}

```go
func (f *File) UnmergeCell(sheet string, hcell, vcell string) error
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

## Kommentar hinzufügen {#AddComment}

```go
func (f *File) AddComment(sheet, cell, format string) error
```

AddComment bietet die Methode zum Hinzufügen von Kommentaren zu einem Blatt anhand eines bestimmten Arbeitsblattindex, einer bestimmten Zelle und eines bestimmten Formatsatzes (z. B. Autor und Text). Beachten Sie, dass die maximale Autorenlänge 255 und die maximale Textlänge 32512 beträgt. Fügen Sie beispielsweise einen Kommentar in `Sheet1!$A$3` hinzu:

<p align="center"><img width="612" src="./images/comment.png" alt="Fügen Sie einem Excel-Dokument einen Kommentar hinzu"></p>

```go
err := f.AddComment("Sheet1", "A3", `{"author":"Excelize: ","text":"Dies ist ein Kommentar."}`)
```

## Kommentar abrufen {#GetComments}

```go
func (f *File) GetComments() (comments map[string][]Comment)
```

GetComments ruft alle Kommentare ab und gibt eine Karte des Arbeitsblattnamens an die Arbeitsblattkommentare zurück.

## Festlegen der Zellenformel {#SetCellFormula}

```go
func (f *File) SetCellFormula(sheet, axis, formula string, opts ...FormulaOpts) error
```

Die Formel in der Zelle wird gemäß dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten) und den Einstellungen für die Zellformel verwendet. Das Ergebnis der Formelzelle kann berechnet werden, wenn das Arbeitsblatt von der Office Excel-Anwendung geöffnet wird, oder kann die [CalcCellValue](cell.md#CalcCellValue) Funktion auch den berechneten Zellenwert abrufen. Wenn die Excel-Anwendung die Formel beim Öffnen der Arbeitsmappe nicht automatisch berechnet, rufen Sie nach dem Einstellen der Zellenformelfunktionen [UpdateLinkedValue](utils.md#UpdateLinkedValue) auf.

- Beispiel 1, setzen Sie die normale Formel `=SUM(A1,B1)` für die Zelle `A3` auf `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "=SUM(A1,B1)")
```

- Beispiel 2, setze eindimensionale vertikale Konstantenarray (Zeilenarray) Formel `1,2,3` für die Zelle `A3` auf `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={1,2,3}")
```

- Beispiel 3, setze eindimensionales horizontales konstantes Array (Spaltenarray) Formel `"a","b","c"` für die Zelle `A3` auf `Sheet1`:

```go
err := f.SetCellFormula("Sheet1", "A3", "={\"a\",\"b\",\"c\"}")
```

- Beispiel 4, setze die zweidimensionale konstante Arrayformel `{1,2,"a","b"}` für die Zelle `A3` auf `Sheet1`:

```go
formulaType, ref := excelize.STCellFormulaTypeArray, "A3:A3"
err := f.SetCellFormula("Sheet1", "A3", "={1,2,\"a\",\"b\"}",
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
    for idx, row := range [][]interface{}{{"A", "B", "C"}, {1, 2}} {
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", idx+1), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    if err := f.AddTable("Sheet1", "A1", "C2",
        `{"table_name":"Table1","table_style":"TableStyleMedium2"}`); err != nil {
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
func (f *File) GetCellFormula(sheet, axis string) (string, error)
```

Rufen Sie die Formel für die Zelle basierend auf dem angegebenen Arbeitsblattnamen (Groß- und Kleinschreibung beachten) und den Zellkoordinaten ab.

## Zellenwert berechnen {#CalcCellValue}

```go
func (f *File) CalcCellValue(sheet, cell string) (result string, err error)
```

CalcCellValue bietet eine Funktion zum Abrufen des berechneten Zellenwerts. Diese Funktion wird derzeit bearbeitet. Array-Formel, Tabellenformel und einige andere Formeln werden derzeit nicht unterstützt.

Unterstützte Formeln:

```text
ABS
ACOS
ACOSH
ACOT
ACOTH
AND
ARABIC
ASIN
ASINH
ATAN
ATAN2
ATANH
AVERAGE
AVERAGEA
BASE
BESSELI
BESSELJ
BESSELK
BESSELY
BIN2DEC
BIN2HEX
BIN2OCT
BITAND
BITLSHIFT
BITOR
BITRSHIFT
BITXOR
CEILING
CEILING.MATH
CEILING.PRECISE
CHAR
CHOOSE
CLEAN
CODE
COLUMN
COLUMNS
COMBIN
COMBINA
COMPLEX
CONCAT
CONCATENATE
COS
COSH
COT
COTH
COUNT
COUNTA
COUNTBLANK
CSC
CSCH
CUMIPMT
CUMPRINC
DATE
DATEDIF
DAY
DB
DDB
DEC2BIN
DEC2HEX
DEC2OCT
DECIMAL
DEGREES
DOLLARDE
DOLLARFR
EFFECT
ENCODEURL
EVEN
EXACT
EXP
FACT
FACTDOUBLE
FALSE
FIND
FINDB
FISHER
FISHERINV
FIXED
FLOOR
FLOOR.MATH
FLOOR.PRECISE
FV
FVSCHEDULE
GAMMA
GAMMALN
GCD
HARMEAN
HEX2BIN
HEX2DEC
HEX2OCT
HLOOKUP
IF
IFERROR
IMABS
IMAGINARY
IMARGUMENT
IMCONJUGATE
IMCOS
IMCOSH
IMCOT
IMCSC
IMCSCH
IMDIV
IMEXP
IMLN
IMLOG10
IMLOG2
IMPOWER
IMPRODUCT
IMREAL
IMSEC
IMSECH
IMSIN
IMSINH
IMSQRT
IMSUB
IMSUM
IMTAN
INT
IPMT
IRR
ISBLANK
ISERR
ISERROR
ISEVEN
ISNA
ISNONTEXT
ISNUMBER
ISODD
ISTEXT
ISO.CEILING
ISPMT
KURT
LARGE
LCM
LEFT
LEFTB
LEN
LENB
LN
LOG
LOG10
LOOKUP
LOWER
MATCH
MAX
MDETERM
MEDIAN
MID
MIDB
MIN
MINA
MIRR
MOD
MONTH
MROUND
MULTINOMIAL
MUNIT
N
NA
NOMINAL
NORM.DIST
NORMDIST
NORM.INV
NORMINV
NORM.S.DIST
NORMSDIST
NORM.S.INV
NORMSINV
NOT
NOW
NPER
NPV
OCT2BIN
OCT2DEC
OCT2HEX
ODD
OR
PDURATION
PERCENTILE.INC
PERCENTILE
PERMUT
PERMUTATIONA
PI
PMT
POISSON.DIST
POISSON
POWER
PPMT
PRODUCT
PROPER
QUARTILE
QUARTILE.INC
QUOTIENT
RADIANS
RAND
RANDBETWEEN
REPLACE
REPLACEB
REPT
RIGHT
RIGHTB
ROMAN
ROUND
ROUNDDOWN
ROUNDUP
ROW
ROWS
SEC
SECH
SHEET
SIGN
SIN
SINH
SKEW
SMALL
SQRT
SQRTPI
STDEV
STDEV.S
STDEVA
SUBSTITUTE
SUM
SUMIF
SUMSQ
T
TAN
TANH
TODAY
TRIM
TRUE
TRUNC
UNICHAR
UNICODE
UPPER
VAR.P
VARP
VLOOKUP
XOR
YEAR
```

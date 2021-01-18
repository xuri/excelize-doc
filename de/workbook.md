# Arbeitsmappe

Optionen definieren die Optionen für eine offene Kalkulationstabelle.

```go
type Options struct {
    Password string
}
```

## Erstellen einer Kalkulationstabelle {#NewFile}

```go
func NewFile() *File
```

NewFile bietet eine Funktion zum Erstellen einer neuen Datei als Standardvorlage. Die neu erstellte Arbeitsmappe enthält standardmäßig ein Arbeitsblatt mit dem Namen `Sheet1`. Zum Beispiel:

## Öffnen {#OpenFile}

```go
func OpenFile(filename string, opt ...Options) (*File, error)
```

OpenFile nimmt den Namen einer Tabellenkalkulationsdatei an und gibt dafür eine aufgefüllte Tabellenkalkulationsdateistruktur zurück. Öffnen Sie beispielsweise eine Kalkulationstabelle mit Kennwortschutz:

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

Beachten Sie, dass die excelize nur unterstützt entschlüsseln und nicht unterstützen Verschlüsselung derzeit, die Tabelle von [`Save()`](workbook.md#Save) und [`SaveAs()`](workbook.md#SaveAs) gespeichert wird ohne Passwort ungeschützt sein.

## Offener Datenstrom {#OpenReader}

```go
func OpenReader(r io.Reader, opt ...Options) (*File, error)
```

OpenReader liest Datenstrom von `io.Reader` und gibt eine gefüllte Tabellenkalkulationsdatei zurück.

Erstellen Sie beispielsweise http-Server, um die Upload-Vorlage zu verarbeiten, und senden Sie dann eine Antwortdownloaddatei mit einem neuen Arbeitsblatt:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprintf(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprintf(w, err.Error())
        return
    }
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", "attachment; filename=Book1.xlsx")
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if _, err := f.WriteTo(w); err != nil {
        fmt.Fprintf(w, err.Error())
    }
    return
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

Test mit cURL:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xlsx' -O -J
curl: Saved to filename 'Book1.xlsx'
```

## Speichern {#Save}

```go
func (f *File) Save() error
```

Save bietet eine Funktion zum Überschreiben der Tabellenkalkulationsdatei mit dem Ursprungspfad.

## Speichern als {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

SaveAs bietet eine Funktion zum Erstellen oder Aktualisieren einer Tabellenkalkulationsdatei unter dem angegebenen Pfad.

## Arbeitsblatt erstellen {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

NewSheet bietet die Funktion zum Erstellen eines neuen Blatts, indem ein Arbeitsblattname angegeben wird, und gibt den Index der Blätter in der Arbeitsmappe (Spreadsheet) zurück, nachdem es angehängt wurde. Beachten Sie, dass beim Erstellen einer neuen Tabellenkalkulationsdatei das Standardarbeitsblatt mit dem Namen `Sheet1` erstellt wird.

## Arbeitsblatt löschen {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

DeleteSheet bietet eine Funktion zum Löschen von Arbeitsblättern in einer Arbeitsmappe nach einem bestimmten Arbeitsblattnamen. Verwenden Sie diese Methode mit Vorsicht, die sich auf Änderungen in Verweisen wie Formeln, Diagrammen usw. auswirkt. Wenn auf einen Referenzwert des gelöschten Arbeitsblatts verwiesen wird, wird beim Öffnen ein Dateifehler verursacht. Diese Funktion ist ungültig, wenn nur noch ein Arbeitsblatt übrig ist.

## Arbeitsblatt kopieren {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

CopySheet bietet eine Funktion zum Duplizieren eines Arbeitsblatts nach dem gegebenen Quell- und Zielarbeitsblattindex. Beachten Sie, dass derzeit keine doppelten Arbeitsmappen unterstützt werden, die Tabellen, Diagramme oder Bilder enthalten. Zum Beispiel:

```go
// Sheet1 ist bereits vorhanden...
index := f.NewSheet("Sheet2")
err := f.CopySheet(1, index)
return err
```

## Festlegen des Arbeitsblatthintergrunds {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground bietet eine Funktion zum Festlegen eines Hintergrundbilds anhand des angegebenen Arbeitsblattnamens.

## Festlegen eines Standardarbeitsblatts {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet bietet eine Funktion zum Festlegen des aktiven Standardblatts der Arbeitsmappe durch einen bestimmten Index. Beachten Sie, dass sich der aktive Index von der ID unterscheidet, die von der Funktion [`GetSheetMap`](sheet.md#GetSheetMap) zurückgegeben wird. Sie sollte größer oder gleich 0 und kleiner als die Gesamten der Arbeitsblattnummern sein.

## Aktives Blattindex abrufen {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

GetActiveSheetIndex bietet eine Funktion zum Abrufen eines aktiven Arbeitsblatts der Arbeitsmappe. Wenn das aktive Blatt nicht gefunden wurde, wird die ganze Zahl `0` zurückgegeben.

## Set-Arbeitsblatt sichtbar {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(name string, visible bool) error
```

SetSheetVisible bietet eine Funktion zum Festlegen eines Arbeitsblatts, das durch den angegebenen Arbeitsblattnamen sichtbar ist. Eine Arbeitsmappe muss mindestens ein sichtbares Arbeitsblatt enthalten. Wenn das angegebene Arbeitsblatt aktiviert wurde, wird diese Einstellung ungültig. Blattzustandswerte, wie in [SheetStateValues Enum](https://docs.microsoft.com/de-de/dotnet/api/documentformat.openxml.spreadsheet.sheetstatevalues?view=openxml-2.8.1) definiert:

|Arbeitsblattstatuswerte|
|---|
|visible|
|hidden|
|veryHidden|

Geben Sie beispielsweise `Sheet1` aus:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## Arbeitsblatt sichtbar machen {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(name string) bool
```

GetSheetVisible bietet eine Funktion, mit der das Arbeitsblatt unter dem angegebenen Arbeitsblattnamen sichtbar gemacht wird. Erhalten Sie beispielsweise den sichtbaren Status von `Sheet1`:

```go
f.GetSheetVisible("Sheet1")
```

## Festlegen von Eigenschaften des Arbeitsblattformats {#SetSheetFormatPr}

```go
func (f *File) SetSheetFormatPr(sheet string, opts ...SheetFormatPrOptions) error
```

SetSheetFormatPr bietet eine Funktion zum Festlegen von Formatierungseigenschaften von Arbeitsblättern.

Verfügbare Optionen:

Optionaler Formatparameter |Typ
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

Legen Sie beispielsweise fest, dass Arbeitsblattzeilen standardmäßig ausgeblendet sind:

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="Festlegen der Eigenschaften des Arbeitsblattformats"></p>

```go
f := excelize.NewFile()
const sheet = "Sheet1"
if err := f.SetSheetFormatPr("Sheet1", excelize.ZeroHeight(true)); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("Book1.xlsx")
```

## Abrufen von Eigenschaften des Arbeitsblattformats {#GetSheetFormatPr}

```go
func (f *File) GetSheetFormatPr(sheet string, opts ...SheetFormatPrOptionsPtr) error
```

GetSheetFormatPr bietet eine Funktion zum Abrufen der Eigenschaften der Arbeitsblattformatierung.

Verfügbare Optionen:

Optionaler Formatparameter |Typ
---|---
BaseColWidth | uint8
DefaultColWidth | float64
DefaultRowHeight | float64
CustomHeight | bool
ZeroHeight | bool
ThickTop | bool
ThickBottom | bool

Zum Beispiel:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    baseColWidth     excelize.BaseColWidth
    defaultColWidth  excelize.DefaultColWidth
    defaultRowHeight excelize.DefaultRowHeight
    customHeight     excelize.CustomHeight
    zeroHeight       excelize.ZeroHeight
    thickTop         excelize.ThickTop
    thickBottom      excelize.ThickBottom
)

if err := f.GetSheetFormatPr(sheet,
    &baseColWidth,
    &defaultColWidth,
    &defaultRowHeight,
    &customHeight,
    &zeroHeight,
    &thickTop,
    &thickBottom,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- baseColWidth:", baseColWidth)
fmt.Println("- defaultColWidth:", defaultColWidth)
fmt.Println("- defaultRowHeight:", defaultRowHeight)
fmt.Println("- customHeight:", customHeight)
fmt.Println("- zeroHeight:", zeroHeight)
fmt.Println("- thickTop:", thickTop)
fmt.Println("- thickBottom:", thickBottom)
```

Ausgabe abrufen:

```text
Defaults:
- baseColWidth: 0
- defaultColWidth: 0
- defaultRowHeight: 15
- customHeight: false
- zeroHeight: false
- thickTop: false
- thickBottom: false
```

## Festlegen von Arbeitsblattansichtseigenschaften {#SetSheetViewOptions}

```go
func (f *File) SetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOption) error
```

SetSheetViewOptions legt Optionen für die Blattansicht fest. Der `viewIndex` kann negativ sein und wird in diesem Fall rückwärts gezählt (` -1` ist die letzte Ansicht).

Verfügbare Optionen:

Optional view parameter |Typ
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string

- Beispiel 1:

```go
err = f.SetSheetViewOptions("Sheet1", -1, ShowGridLines(false))
```

- Beispiel 2:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetSheetViewOptions(sheet, 0,
    excelize.DefaultGridColor(false),
    excelize.RightToLeft(false),
    excelize.ShowFormulas(true),
    excelize.ShowGridLines(true),
    excelize.ShowRowColHeaders(true),
    excelize.ZoomScale(80),
    excelize.TopLeftCell("C3"),
); err != nil {
    fmt.Println(err)
}

var zoomScale excelize.ZoomScale
fmt.Println("Default:")
fmt.Println("- zoomScale: 80")

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(500)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used out of range value:")
fmt.Println("- zoomScale:", zoomScale)

if err := f.SetSheetViewOptions(sheet, 0, excelize.ZoomScale(123)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &zoomScale); err != nil {
    fmt.Println(err)
}

fmt.Println("Used correct value:")
fmt.Println("- zoomScale:", zoomScale)
```

Ausgabe abrufen:

```text
Default:
- zoomScale: 80
Used out of range value:
- zoomScale: 80
Used correct value:
- zoomScale: 123
```

## Abrufen von Arbeitsblattansichtseigenschaften {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

GetSheetViewOptions ruft den Wert der Optionen für die Blattansicht ab. Der `viewIndex` kann negativ sein und wird in diesem Fall rückwärts gezählt (`-1` ist die letzte Ansicht). Verfügbare Optionen:

Optional view parameter |Typ
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool
ZoomScale|float64
TopLeftCell|string

- Beispiel 1, um die Eigenschaften der Gitterlinieneigenschaft für die letzte Ansicht im Arbeitsblatt mit dem Namen `Sheet1` abzurufen:

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- Beispiel 2:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    rightToLeft       excelize.RightToLeft
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showZeros         excelize.ShowZeros
    showRowColHeaders excelize.ShowRowColHeaders
    zoomScale         excelize.ZoomScale
    topLeftCell       excelize.TopLeftCell
)

if err := f.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
    &showZeros,
    &showRowColHeaders,
    &zoomScale,
    &topLeftCell,
); err != nil {
    fmt.Println(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- zoomScale:", zoomScale)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)

if err := f.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    fmt.Println(err)
}

if err := f.SetSheetViewOptions(sheet, 0, excelize.ShowZeros(false)); err != nil {
    fmt.Println(err)
}

if err := f.GetSheetViewOptions(sheet, 0, &showZeros); err != nil {
    fmt.Println(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showZeros:", showZeros)
fmt.Println("- topLeftCell:", topLeftCell)
```

Ausgabe abrufen:

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showZeros: true
- showRowColHeaders: true
- zoomScale: 0
- topLeftCell: ""
After change:
- showGridLines: false
- showZeros: false
- topLeftCell: B2
```

## Festlegen des Layouts der Arbeitsblattseite {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

SetPageLayout bietet eine Funktion zum Festlegen des Seitenlayouts von Arbeitsblättern. Verfügbare Optionen:

- `BlackAndWhite` spezifizierter Druck Schwarzweiß.

- `FirstPageNumber` hat die erste gedruckte Seitenzahl angegeben. Wenn kein Wert angegeben ist, wird "automatisch" angenommen.

- `PageLayoutOrientation` bietet eine Methode zum Festlegen der Arbeitsblattausrichtung. Die Standardausrichtung ist "porträt". Im Folgenden werden die von der Excelize-Indexnummer unterstützten Orientierungsparameter angezeigt:

Parameter|Orientierung
---|---
OrientationPortrait|porträt
OrientationLandscape|landschaft

- `PageLayoutPaperSize` bietet eine Methode zum Festlegen der Arbeitsblattpapiergröße. Die Standardpapiergröße des Arbeitsblatts lautet "Briefpapier (8,5 Zoll x 11 Zoll)". Im Folgenden wird das nach Excelize-Indexnummer sortierte Papierformat angezeigt:

Index|Papiergröße
---|---
1   | Briefpapier (8.5 in. × 11 in.)
2   | Brief kleines Papier (8.5 in. × 11 in.)
3   | Tabloidpapier (11 in. × 17 in.)
4   | Hauptbuchpapier (17 in. × 11 in.)
5   | Rechtsdokument (8.5 in. × 14 in.)
6   | Statement Papier (5.5 in. × 8.5 in.)
7   | Executive Papier (7.25 in. × 10.5 in.)
8   | A3 Papier (297 mm × 420 mm)
9   | A4 Papier (210 mm × 297 mm)
10  | A4 kleines Papier (210 mm × 297 mm)
11  | A5 Papier (148 mm × 210 mm)
12  | B4 Papier (250 mm × 353 mm)
13  | B5 Papier (176 mm × 250 mm)
14  | Foliopapier (8.5 in. × 13 in.)
15  | Quartopapier (215 mm × 275 mm)
16  | Standardpapier (10 in. × 14 in.)
17  | Standardpapier (11 in. × 17 in.)
18  | Notizpapier (8.5 in. × 11 in.)
19  | Umschlag Nr. 9 (3.875 in. × 8.875 in.)
20  | Umschlag Nr. 10 (4.125 in. × 9.5 in.)
21  | Umschlag Nr. 11 (4.5 in. × 10.375 in.)
22  | Umschlag Nr. 12 (4.75 in. × 11 in.)
23  | Umschlag Nr. 14 (5 in. × 11.5 in.)
24  | C Papier (17 in. × 22 in.)
25  | D Papier (22 in. × 34 in.)
26  | E Papier (34 in. × 44 in.)
27  | DL-Umschlag (110 mm × 220 mm)
28  | C5-Umschlag (162 mm × 229 mm)
29  | C3-Umschlag (324 mm × 458 mm)
30  | C4-Umschlag (229 mm × 324 mm)
31  | C6-Umschlag (114 mm × 162 mm)
32  | C65-Umschlag (114 mm × 229 mm)
33  | B4-Umschlag (250 mm × 353 mm)
34  | B5-Umschlag (176 mm × 250 mm)
35  | B6-Umschlag (176 mm × 125 mm)
36  | Italien Umschlag (110 mm × 230 mm)
37  | Monarch Umschlag (3.875 in. × 7.5 in.).
38  | 6¾ Umschlag (3.625 in. × 6.5 in.)
39  | US Standard-Lüfterfalte (14.875 in. × 11 in.)
40  | Deutsche Standard-Lüfterfalte (8.5 in. × 12 in.)
41  | Deutsche Rechtsfanfalte (8.5 in. × 13 in.)
42  | ISO B4 (250 mm × 353 mm)
43  | Japanische Postkarte (100 mm × 148 mm)
44  | Standardpapier (9 in. × 11 in.)
45  | Standardpapier (10 in. × 11 in.)
46  | Standardpapier (15 in. × 11 in.)
47  | Umschlag einladen (220 mm × 220 mm)
50  | Brief extra Papier (9.275 in. × 12 in.)
51  | Legal zusätzliches Papier (9.275 in. × 15 in.)
52  | Tabloid zusätzliches Papier (11.69 in. × 18 in.)
53  | A4 zusätzliches Papier (236 mm × 322 mm)
54  | Brief Querpapier (8.275 in. × 11 in.)
55  | A4 Querpapier (210 mm × 297 mm)
56  | Brief extra Querpapier (9.275 in. × 12 in.)
57  | SuperA/SuperA/A4 papier (227 mm × 356 mm)
58  | SuperB/SuperB/A3 papier (305 mm × 487 mm)
59  | Brief plus Papier (8.5 in. × 12.69 in.)
60  | A4 plus Papier (210 mm × 330 mm)
61  | A5 Querpapier (148 mm × 210 mm)
62  | JIS B5 Querpapier (182 mm × 257 mm)
63  | A3 zusätzliches Papier (322 mm × 445 mm)
64  | A5 zusätzliches Papier (174 mm × 235 mm)
65  | ISO B5 zusätzliches Papier (201 mm × 276 mm)
66  | A2 papier (420 mm × 594 mm)
67  | A3 Querpapier (297 mm × 420 mm)
68  | A3 zusätzliches Querpapier (322 mm × 445 mm)
69  | Japanische Doppelpostkarte (200 mm × 148 mm)
70  | A6 (105 mm × 148 mm)
71  | Japanischer Umschlag Kaku # 2
72  | Japanischer Umschlag Kaku # 3
73  | Japanischer Umschlag Chou # 3
74  | Japanischer Umschlag Chou # 4
75  | Buchstabe gedreht (11 × 8½ in.)
76  | A3 gedreht (420 mm × 297 mm)
77  | A4 gedreht (297 mm × 210 mm)
78  | A5 gedreht (210 mm × 148 mm)
79  | B4 (JIS) gedreht (364 mm × 257 mm)
80  | B5 (JIS) gedreht (257 mm × 182 mm)
81  | Japanische Postkarte gedreht (148 mm × 100 mm)
82  | Doppelte japanische Postkarte gedreht (148 mm × 200 mm)
83  | A6 gedreht (148 mm × 105 mm)
84  | Japanischer Umschlag Kaku # 2 gedreht
85  | Japanischer Umschlag Kaku # 3 gedreht
86  | Japanischer Umschlag Chou # 3 gedreht
87  | Japanischer Umschlag Chou # 4 gedreht
88  | B6 (JIS) (128 mm × 182 mm)
89  | B6 (JIS) gedreht (182 mm × 128 mm)
90  | (12 in × 11 in)
91  | Japanischer Umschlag Sie # 4
92  | Japanischer Umschlag Sie # 4 gedreht
93  | PRC 16K (146 mm × 215 mm)
94  | PRC 32K (97 mm × 151 mm)
95  | PRC 32K(Big) (97 mm × 151 mm)
96  | PRC-Umschlag Nr. #1 (102 mm × 165 mm)
97  | PRC-Umschlag Nr. #2 (102 mm × 176 mm)
98  | PRC-Umschlag Nr. #3 (125 mm × 176 mm)
99  | PRC-Umschlag Nr. #4 (110 mm × 208 mm)
100 | PRC-Umschlag Nr. #5 (110 mm × 220 mm)
101 | PRC-Umschlag Nr. #6 (120 mm × 230 mm)
102 | PRC-Umschlag Nr. #7 (160 mm × 230 mm)
103 | PRC-Umschlag Nr. #8 (120 mm × 309 mm)
104 | PRC-Umschlag Nr. #9 (229 mm × 324 mm)
105 | PRC-Umschlag Nr. #10 (324 mm × 458 mm)
106 | PRC 16K gedreht
107 | PRC 32K gedreht
108 | PRC 32K (groß) gedreht
109 | PRC-Umschlag Nr. 1 gedreht (165 mm × 102 mm)
110 | PRC-Umschlag Nr. 2 gedreht (176 mm × 102 mm)
111 | PRC-Umschlag Nr. 3 gedreht (176 mm × 125 mm)
112 | PRC-Umschlag Nr. 4 gedreht (208 mm × 110 mm)
113 | PRC-Umschlag Nr. 5 gedreht (220 mm × 110 mm)
114 | PRC-Umschlag Nr. 6 gedreht (230 mm × 120 mm)
115 | PRC-Umschlag Nr. 7 gedreht (230 mm × 160 mm)
116 | PRC-Umschlag Nr. 8 gedreht (309 mm × 120 mm)
117 | PRC-Umschlag Nr. 9 gedreht (324 mm × 229 mm)
118 | PRC-Umschlag Nr. 10 gedreht (458 mm × 324 mm)

- `FitToHeight` hat die Anzahl der vertikalen Seiten angegeben, auf die gepasst werden soll.

- `FitToWidth` hat die Anzahl der horizontalen Seiten angegeben, auf die gepasst werden soll.

- `PageLayoutScale` definiert die Druckskalierung. Dieses Attribut ist auf Werte zwischen 10 (10%) und 400 (400%) beschränkt. Diese Einstellung wird überschrieben, wenn "FitToWidth" und / oder "FitToHeight" verwendet werden.

- Legen Sie beispielsweise das Seitenlayout für `Sheet1` mit Schwarzweißdruck, erste gedruckte Seitenzahl von `2`, kleines A4-Querformatpapier (210 mm x 297 mm), 2 vertikale Seiten zum Anpassen und 2 horizontale Seiten zum Anpassen fest Ein und 50% Druckskalierung:

```go
f := excelize.NewFile()
if err := f.SetPageLayout(
    "Sheet1",
    excelize.BlackAndWhite(true),
    excelize.FirstPageNumber(2),
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
    excelize.PageLayoutPaperSize(10),
    excelize.FitToHeight(2),
    excelize.FitToWidth(2),
    excelize.PageLayoutScale(50),
); err != nil {
    fmt.Println(err)
}
```

## Abrufen des Layouts der Arbeitsblattseite {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

GetPageLayout bietet eine Funktion zum Abrufen des Seitenlayouts des Arbeitsblatts. Verfügbare Optionen:

- `PageLayoutOrientation` bietet eine Methode zum Abrufen der Arbeitsblattorientierung
- `PageLayoutPaperSize` bietet eine Methode zum Abrufen der Arbeitsblattpapiergröße

- Zum Beispiel, seitenlayout von `Sheet1` abrufen:

```go
f := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := f.GetPageLayout("Sheet1", &orientation); err != nil {
    fmt.Println(err)
}
if err := f.GetPageLayout("Sheet1", &paperSize); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
```

Ausgabe:

```text
Defaults:
- orientation: "portrait"
- paper size: 1
```

## Festlegen von Arbeitsblattseitenrändern {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts ...PageMarginsOptions) error
```

SetPageMargins bietet eine Funktion zum Festlegen der Seitenränder von Arbeitsblättern. Verfügbare Optionen:

Options|Typ
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- Zum Beispiel, seitenränder von `Sheet1` einstellen:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

if err := f.SetPageMargins(sheet,
    excelize.PageMarginBottom(1.0),
    excelize.PageMarginFooter(1.0),
    excelize.PageMarginHeader(1.0),
    excelize.PageMarginLeft(1.0),
    excelize.PageMarginRight(1.0),
    excelize.PageMarginTop(1.0),
); err != nil {
    fmt.Println(err)
}
```

## Abrufen von Arbeitsblattseitenrändern {#GetPageMargins}

GetPageMargins bietet eine Funktion zum Abrufen von Arbeitsblattseitenrändern. Verfügbare Optionen:

Options|Typ
---|---
PageMarginBotom|float64
PageMarginFooter|float64
PageMarginHeader|float64
PageMarginLeft|float64
PageMarginRight|float64
PageMarginTop|float64

- Zum Beispiel, seitenränder von `Sheet1` abrufen:

```go
f := excelize.NewFile()
const sheet = "Sheet1"

var (
    marginBottom excelize.PageMarginBottom
    marginFooter excelize.PageMarginFooter
    marginHeader excelize.PageMarginHeader
    marginLeft   excelize.PageMarginLeft
    marginRight  excelize.PageMarginRight
    marginTop    excelize.PageMarginTop
)

if err := f.GetPageMargins(sheet,
    &marginBottom,
    &marginFooter,
    &marginHeader,
    &marginLeft,
    &marginRight,
    &marginTop,
); err != nil {
    fmt.Println(err)
}
fmt.Println("Defaults:")
fmt.Println("- marginBottom:", marginBottom)
fmt.Println("- marginFooter:", marginFooter)
fmt.Println("- marginHeader:", marginHeader)
fmt.Println("- marginLeft:", marginLeft)
fmt.Println("- marginRight:", marginRight)
fmt.Println("- marginTop:", marginTop)
```

Ausgabe:

```text
Defaults:
- marginBottom: 0.75
- marginFooter: 0.3
- marginHeader: 0.3
- marginLeft: 0.7
- marginRight: 0.7
- marginTop: 0.75
```

## Kopf- und Fußzeile einstellen {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, settings *FormatHeaderFooter) error
```

SetHeaderFooter bietet eine Funktion zum Festlegen von Kopf- und Fußzeilen anhand des angegebenen Arbeitsblattnamens und der Steuerzeichen.

Kopf- und Fußzeilen werden in den folgenden Einstellungsfeldern angegeben:

Felder           | Beschreibung
---|---
AlignWithMargins | Richten Sie die Fußzeilenränder der Kopfzeilen an den Seitenrändern aus
DifferentFirst   | Unterschiedliche Kopf- und Fußzeile der ersten Seite
DifferentOddEven | Unterschiedliche ungerade und gerade Seitenkopf- und Fußzeilenanzeige
ScaleWithDoc     | Skalieren Sie Kopf- und Fußzeile mit Dokumentenskalierung
OddFooter        | Ungerader Seitenfußzeile
OddHeader        | Ungerader Seitenkopf
EvenFooter       | Sogar Seitenfußzeile
EvenHeader       | Sogar Seitenüberschriften
FirstFooter      | Fußzeile der ersten Seite
FirstHeader      | Kopfzeile der ersten Seite

Die folgenden Formatierungscodes können in Feldern mit 6 Zeichenfolgentypen verwendet werden: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>Code formatieren</th>
            <th>Beschreibung</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>Der Charakter &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>Größe der Textschrift, wobei die Schriftgröße eine dezimale Schriftgröße in Punkten ist</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>Eine Textschriftartennamenzeichenfolge, ein Schriftartname und eine Textschriftartenzeichenfolge, ein Schrifttyp</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>Normales Textformat. Schaltet den Fett- und Kursivmodus aus</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>Name der Registerkarte des aktuellen Arbeitsblatts</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>Fettgedrucktes Textformat von Aus nach Ein oder umgekehrt. Der Standardmodus ist ausgeschaltet</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>Aktuelles Datum</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>Mittelteil</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>Textformat mit doppelter Unterstreichung</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>Dateiname der aktuellen Arbeitsmappe</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>Objekt als Hintergrund zeichnen</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>Schattentextformat</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>Kursives Textformat</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>Textschriftfarbe<br>Eine RGB-Farbe wird als RRGGBB angegeben<br>Eine Themenfarbe wird als TTSNNN angegeben, wobei TT die Themenfarben-ID ist, S ist entweder &quot;+&quot; oder &quot;-&quot; des Farbton- / Farbtonwerts und NNN ist der Farbton- / Farbtonwert</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>Linker Abschnitt</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>Gesamtzahl der Seiten</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>Gliederungstextformat</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>Ohne das optionale Suffix wird die aktuelle Seitenzahl dezimal angegeben</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>Rechter Abschnitt</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>Durchgestrichenes Textformat</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>Aktuelle Uhrzeit</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>Textformat mit einer Unterstreichung. Wenn der Doppelunterstreichungsmodus aktiviert ist, schaltet das nächste Vorkommen in einem Abschnittsspezifizierer den Doppelunterstreichungsmodus aus. Andernfalls wird der Einzelunterstreichungsmodus von Aus auf Ein oder umgekehrt umgeschaltet. Der Standardmodus ist ausgeschaltet</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>Hochgestelltes Textformat</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>Tiefgestelltes Textformat</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>Aktueller Pfad der Arbeitsmappendatei</td>
        </tr>
    </tbody>
</table>

Zum Beispiel:

```go
err := f.SetHeaderFooter("Sheet1", &excelize.FormatHeaderFooter{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

Dieses Beispiel zeigt:

- Die erste Seite hat eine eigene Kopf- und Fußzeile
- Ungerade und gerade nummerierte Seiten haben unterschiedliche Kopf- und Fußzeilen
- Aktuelle Seitenzahl im rechten Bereich der Überschriften für ungerade Seiten
- Der Dateiname der aktuellen Arbeitsmappe im mittleren Bereich der Fußzeilen für ungerade Seiten
- Aktuelle Seitenzahl im linken Bereich der Überschriften mit geraden Seiten
- Aktuelles Datum im linken Bereich und aktuelle Uhrzeit im rechten Bereich der Fußzeilen mit geraden Seiten
- Der Text "Center Bold Header" in der ersten Zeile des mittleren Abschnitts der ersten Seite und das Datum in der zweiten Zeile des mittleren Abschnitts derselben Seite
- Keine Fußzeile auf der ersten Seite

## Definierter Name festlegen {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

SetDefinedName bietet eine Funktion zum Festlegen der definierten Namen der Arbeitsmappe oder des Arbeitsblatts. Wenn kein Bereich angegeben ist, ist der Standardbereich die Arbeitsmappe.

Zum Beispiel:

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

Einstellungen für Druckbereich und Drucktitel für das Arbeitsblatt:

<p align="center"><img width="703" src="./images/page_setup_01.png" alt="Einstellungen für Druckbereich und Drucktitel für das Arbeitsblatt"></p>

```go
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
})
f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
})
```

## Definierten Namen abrufen {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

GetDefinedName bietet eine Funktion zum Abrufen der definierten Namen der Arbeitsmappe oder des Arbeitsblatts.

## Definierter Name löschen {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

DeleteDefinedName bietet eine Funktion zum Löschen der definierten Namen der Arbeitsmappe oder des Arbeitsblatts. Wenn kein Bereich angegeben ist, ist der Standardbereich die Arbeitsmappe. Zum Beispiel:

```go
f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## Festlegen von Dokumenteigenschaften {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

SetDocProps bietet eine Funktion zum Festlegen der Eigenschaften des Dokumentkerns. Folgende Eigenschaften können festgelegt werden:

Eigentum       | Beschreibung
---|---
Title          | Der Name wurde der Ressource gegeben.
Subject        | Das Thema des Inhalts der Ressource.
Creator        | Eine Entität, die hauptsächlich für die Erstellung des Inhalts der Ressource verantwortlich ist.
Keywords       | Eine begrenzte Anzahl von Schlüsselwörtern zur Unterstützung der Suche und Indizierung. Dies ist normalerweise eine Liste von Begriffen, die an keiner anderen Stelle in den Eigenschaften verfügbar sind.
Description    | Eine Erläuterung des Inhalts der Ressource.
LastModifiedBy | Der Benutzer, der die letzte Änderung vorgenommen hat. Die Identifizierung ist umgebungsspezifisch.
Language       | Die Sprache des intellektuellen Inhalts der Ressource.
Identifier     | Ein eindeutiger Verweis auf die Ressource in einem bestimmten Kontext.
Revision       | Das Thema des Inhalts der Ressource.
ContentStatus  | Der Status des Inhalts. Zum Beispiel: Zu den Werten gehören Draft", "Reviewed" und "Final"
Category       | Eine Kategorisierung des Inhalts dieses Pakets.
Version        | Die Versionsnummer. Dieser Wert wird vom Benutzer oder von der Anwendung festgelegt.

Zum Beispiel:

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## Abrufen von Dokumenteigenschaften {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

GetDocProps bietet eine Funktion zum Abrufen der Eigenschaften des Dokumentkerns.

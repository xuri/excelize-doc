# Diagramm

## Diagramm hinzufügen {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChart bietet die Methode zum Hinzufügen eines Diagramms zu einem Arbeitsblatt anhand eines bestimmten Diagrammformatsatzes (z. B. Versatz, Skalierung, Seitenverhältniseinstellung und Druckeinstellungen) und festgelegter Eigenschaften.

Das Folgende zeigt den `Type` des Diagramms, das von Excelize unterstützt wird:

ID|Aufzählung|Diagramm
---|---|---
0  | Area                        | 2D Flächendiagramm
1  | AreaStacked                 | 2D gestapeltes Flächendiagramm
2  | AreaPercentStacked          | 2D 100% gestapeltes Flächendiagramm
3  | Area3D                      | 3D Flächendiagramm
4  | Area3DStacked               | 3D gestapeltes Flächendiagramm
5  | Area3DPercentStacked        | 3D 100% gestapeltes Flächendiagramm
6  | Bar                         | 2D Clusterbalkendiagramm
7  | BarStacked                  | 2D gestapeltes Balkendiagramm
8  | BarPercentStacked           | 2D 100% gestapeltes Balkendiagramm
9  | Bar3DClustered              | 3D Clusterbalkendiagramm
10 | Bar3DStacked                | 3D gestapeltes Balkendiagramm
11 | Bar3DPercentStacked         | 3D 100% gestapeltes Balkendiagramm
12 | Bar3DConeClustered          | 3D Kegel-Cluster-Balkendiagramm
13 | Bar3DConeStacked            | 3D Kegel gestapelte Balkendiagramm
14 | Bar3DConePercentStacked     | 3D 100% Kegelbalkendiagramm
15 | Bar3DPyramidClustered       | 3D Pyramiden-Cluster-Balkendiagramm
16 | Bar3DPyramidStacked         | 3D Pyramide gestapelt Balkendiagramm
17 | Bar3DPyramidPercentStacked  | 3D 100% Pyramide gestapelt Balkendiagramm
18 | Bar3DCylinderClustered      | 3D Zylinder-Clusterbalkendiagramm
19 | Bar3DCylinderStacked        | 3D Zylinder gestapeltes Balkendiagramm
20 | Bar3DCylinderPercentStacked | 3D 100% Zylinder gestapelte Balkendiagramm
21 | Col                         | 2D Cluster-Säulendiagramm
22 | ColStacked                  | 2D gestapeltes Säulendiagramm
23 | ColPercentStacked           | 2D 100% gestapeltes Säulendiagramm
24 | Col3DClustered              | 3D Cluster-Säulendiagramm
25 | Col3D                       | 3D Säulendiagramm
26 | Col3DStacked                | 3D gestapeltes Säulendiagramm
27 | Col3DPercentStacked         | 3D 100% gestapeltes Säulendiagramm
28 | Col3DCone                   | 3D Kegel-Säulendiagramm
29 | Col3DConeClustered          | 3D Kegel-Cluster-Säulendiagramm
30 | Col3DConeStacked            | 3D Kegel gestapeltes Säulendiagramm
31 | Col3DConePercentStacked     | 3D 100% Kegel gestapeltes Säulendiagramm
32 | Col3DPyramid                | 3D Pyramidensäulendiagramm
33 | Col3DPyramidClustered       | 3D Pyramiden-Pyramiden-Säulendiagramm
34 | Col3DPyramidStacked         | 3D Pyramidenstapelsäulendiagramm
35 | Col3DPyramidPercentStacked  | 3D 100% Pyramide gestapelt Säulendiagramm
36 | Col3DCylinder               | 3D Zylinder-Säulendiagramm
37 | Col3DCylinderClustered      | 3D Zylinder-Cluster-Säulendiagramm
38 | Col3DCylinderStacked        | 3D Zylinder gestapeltes Säulendiagramm
39 | Col3DCylinderPercentStacked | 3D 100% Zylinder gestapeltsäulendiagramm
40 | Doughnut                    | donut-Diagramm
41 | Line                        | liniendiagramm
42 | Line3D                      | 3D Liniendiagramm
43 | Pie                         | kreisdiagramm
44 | Pie3D                       | 3D Kreisdiagramm
45 | PieOfPie                    | Doppeltes Tortendiagramm
46 | BarOfPie                    | Balken eines Kreisdiagramms
47 | Radar                       | netzdiagramm
48 | Scatter                     | streudiagramm
49 | Surface3D                   | 3D Oberflächendiagramm
50 | WireframeSurface3D          | 3D Drahtmodell-Oberflächendiagramm
51 | Contour                     | konturdiagramm
52 | WireframeContour            | wireframe-Konturdiagramm
53 | Bubble                      | blasendiagramm
54 | Bubble3D                    | 3D Blasendiagramm

Im Office Excel-Diagrammdatenbereich gibt `Series` den Informationssatz an, für den Daten gezeichnet werden sollen, das Legendenelement (Serie) und die horizontale (Kategorie) Achsenbeschriftung.

Folgende Optionen können für die `Series` eingestellt werden:

Parameter|Erläuterung
---|---
Name|Legendenelement (Serie), angezeigt in der Diagrammlegende und in der Formelleiste. Der Parameter `Name` ist optional. Wenn Sie diesen Wert nicht angeben, lautet der Standardwert `Serie 1 .. n`. `Name` Unterstützung für die Darstellung von Formeln, zum Beispiel: `Sheet1!$A$1`.
Categories|Beschriftung der horizontalen Achse (Kategorie). Der Parameter `Categories` ist in den meisten Diagrammtypen optional. Der Standardwert ist eine zusammenhängende Folge der Form `1..n`.
Values|Der Diagrammdatenbereich, der der wichtigste Parameter in `Series` ist, ist auch der einzige erforderliche Parameter beim Erstellen eines Diagramms. Diese Option verknüpft das Diagramm mit den angezeigten Arbeitsblattdaten.
Line|Hiermit wird das Linienformat des Liniendiagramms festgelegt. Die Eigenschaft `Line` ist optional. Wenn sie nicht angegeben wird, wird der Standardstil verwendet. Die Optionen, die eingestellt werden können, sind `Width`. Der Bereich von `Width` beträgt 0.25pt - 999pt. Wenn der Wert für width außerhalb des Bereichs liegt, beträgt die Standardbreite der Linie 2pt.
Marker|Dies setzt die Markierung des Liniendiagramms und des Streudiagramms. Der Bereich des optionalen Feldes `Size` liegt zwischen 2 und 72 (Standardwert ist `5`). Der Aufzählungswert des optionalen Felds `Symbol` ist (Standardwert ist `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x`, `auto`.

Legen Sie die Eigenschaften der Diagrammlegende fest. Folgende Optionen können eingestellt werden:

Parameter|Typ|Erläuterung
---|---|---
Position        | `string` | Die Position der Diagrammlegende
ShowLegendKey   | `bool`   | Stellen Sie die Legendenschlüssel ein, die in Datenbezeichnungen angezeigt werden sollen

Stellen Sie die `Position` der Diagrammlegende ein. Die Standard-Legendenposition ist `right`. Die verfügbaren Positionen sind:

Parameter|Erläuterung
---|---
none|Legende deaktivieren
top|Oben drauf
bottom|Am Boden
left|Links
right|Rechts
top_right|Oben rechts

Der Parametersatz `ShowLegendKey`  der Legendenschlüssel soll in Datenbeschriftungen angezeigt werden. Der Standardwert ist `false`.

Der Diagrammtitel wird durch Auswahl des Parameters `Name` des Objekts `Title` festgelegt. Der Titel wird über dem Diagramm angezeigt. Der Parameter `Name` unterstützt die Verwendung von Formeldarstellungen wie `Sheet1!$A$1`. Wenn Sie keinen Symboltitel angeben, ist der Standardwert null.

Der Parameter `ShowBlanksAs` liefert die Einstellung "Zellen ausblenden und leeren". Der Standardwert ist: `gap`. In der Excel-Anwendung wird "leere Zelle als" angezeigt: "Leerzeichen". Die folgenden Werte sind für diesen Parameter optional:

Parameter|Erläuterung
---|---
gap|Leerzeichen
span|Verbinden Sie Datenpunkte mit geraden Linien
zero|Nullwert

Gibt an, dass jede Datenpunktmarkierung in der Reihe eine andere Farbe durch `VaryColors` hat. Der Standardwert ist `true`.

Der Parameter `Format` bietet Einstellungen für Parameter wie Diagrammversatz, Skalierung, Seitenverhältniseinstellungen und Druckeigenschaften sowie für die in der Funktion [`AddPicture`](image.md#AddPicture) verwendeten.

Legen Sie die Position des Diagrammplotbereichs nach Plotbereich fest. Folgende Eigenschaften können festgelegt werden:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
ShowBubbleSize  | `bool` | `false` | Gibt an, dass die Blasengröße auf einem Datenetikett angegeben werden soll.
ShowCatName     | `bool` | `false` | Kategoriename.
ShowLeaderLines | `bool` | `false` | Gibt an, dass der Kategoriename auf dem Datenetikett angezeigt werden soll.
ShowPercent     | `bool` | `false` | Gibt an, dass der Prozentsatz auf einem Datenetikett angegeben werden soll.
ShowSerName     | `bool` | `false` | Gibt an, dass der Serienname auf einem Datenetikett angezeigt werden soll.
ShowVal         | `bool` | `false` | Gibt an, dass der Wert auf einem Datenetikett angezeigt werden soll.

Stellen Sie die primären Optionen für die horizontale und vertikale Achse auf `XAxis` und `YAxis` ein.

Die Eigenschaften von `XAxis`, die eingestellt werden können, sind:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
None           | `bool`          | `false` | Achsen deaktivieren.
MajorGridLines | `bool`          | `false` | Gibt die Hauptgitterlinien an.
MinorGridLines | `bool`          | `false` | Gibt kleinere Gitterlinien an.
TickLabelSkip  | `int`           | `1`     | Gibt an, wie viele Häkchen zwischen einem gezeichneten Etikett übersprungen werden sollen. Die Eigenschaft `TickLabelSkip` ist optional. Der Standardwert ist auto.
ReverseOrder   | `bool`          | `false` | Gibt an, dass die Kategorien oder Werte in umgekehrter Reihenfolge (Ausrichtung des Diagramms) sind. Die Eigenschaft `ReverseOrder` ist optional.
Maximum        | `*float64`      | `0`     | Gibt an, dass das feste Maximum 0 automatisch ist. Die maximale Eigenschaft ist optional.
Minimum        | `*float64`      | `0`     | Gibt an, dass das feste Minimum 0 automatisch ist. Die minimale Eigenschaft ist optional. Der Standardwert ist auto.
Font           | `Font`          | N/A     | Gibt die Schriftart der horizontalen Achse an.
NumFmt         | `ChartNumFmt`   | N/A     | Gibt an, dass bei Verknüpfung mit der Quelle ein benutzerdefinierter Zahlenformatcode für die Achse festgelegt wird.
Title          | `[]RichTextRun` | N/A     | Gibt den Titel der primären horizontalen Achse und die Größenänderung des Diagramms an.

Die Eigenschaften von `YAxis`, die eingestellt werden können, sind:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
None           | `bool`          | `false` | Achsen deaktivieren.
MajorGridLines | `bool`          | `false` | Gibt die Hauptgitterlinien an.
MinorGridLines | `bool`          | `false` | Gibt kleinere Gitterlinien an.
MajorUnit      | `float64`       | `0`     | Gibt den Abstand zwischen den Hauptstrichen an. Muss eine positive Gleitkommazahl enthalten. Die Eigenschaft `MajorUnit` ist optional. Der Standardwert ist auto.
ReverseOrder   | `bool`          | `false` | Gibt an, dass die Kategorien oder Werte in umgekehrter Reihenfolge (Ausrichtung des Diagramms) sind. Die Eigenschaft `ReverseOrder` ist optional.
Maximum        | `*float64`      | `0`     | Gibt an, dass das feste Maximum 0 automatisch ist. Die maximale Eigenschaft ist optional.
Minimum        | `*float64`      | `0`     | Gibt an, dass das feste Minimum 0 automatisch ist. Die minimale Eigenschaft ist optional. Der Standardwert ist auto.
Font           | `Font`          | N/A     | Gibt die Schriftart der vertikalen Achse an.
LogBase        | `float64`       | N/A     | Gibt die Basiszahl der logarithmischen Skala der vertikalen Achse an.
NumFmt         | `ChartNumFmt`   | N/A     | Gibt an, dass bei Verknüpfung mit der Quelle ein benutzerdefinierter Zahlenformatcode für die Achse festgelegt wird.
Title          | `[]RichTextRun` | N/A     | Gibt den Titel der primären vertikalen Achse und die Größenänderung des Diagramms an.

Legen Sie die Diagrammgröße anhand der Eigenschaft `Dimension` fest. Die Dimensionseigenschaft ist optional. Folgende Eigenschaften können festgelegt werden:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
Height | `uint` | 260 | Height
Width  | `uint` | 480 | Width

Der Parameter `combo` gibt an, dass ein Diagramm erstellt wird, das zwei oder mehr Diagrammtypen in einem einzelnen Diagramm kombiniert. Erstellen Sie beispielsweise ein gruppiertes Spalten-Liniendiagramm mit den Daten `Sheet1!$E$1:$L$15`:

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
    if err := f.SetSheetName("Sheet1", "Tabelle1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Apfel", "Orange", "Birne"},
        {"Klein", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Groß", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Tabelle1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Tabelle1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Tabelle1!$A$2",
                Categories: "Tabelle1!$B$1:$D$1",
                Values:     "Tabelle1!$B$2:$D$2",
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Title: []excelize.RichTextRun{
            {
                Text: "Clustered Column - Liniendiagramm",
            },
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }, &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Tabelle1!$A$4",
                Categories: "Tabelle1!$B$1:$D$1",
                Values:     "Tabelle1!$B$4:$D$4",
                Marker: excelize.ChartMarker{
                    Symbol: "none", Size: 10,
                },
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Legend: excelize.ChartLegend{
            Position: "right",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Speichern Sie die Tabelle unter dem angegebenen Pfad.
    if err := f.SaveAs("Mappe1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Diagrammblatt hinzufügen {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChartSheet bietet die Methode zum Erstellen eines Diagrammblatts anhand eines bestimmten Diagrammformatsatzes (z. B. Versatz, Skalierung, Einstellung des Seitenverhältnisses und Druckeinstellungen) und festgelegter Eigenschaften. In Excel ist ein Diagrammblatt ein Arbeitsblatt, das nur ein Diagramm enthält.

## Diagramm löschen {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart bietet eine Funktion zum Löschen von Diagrammen in einer Tabelle anhand des angegebenen Arbeitsblatts und des Zellennamens.

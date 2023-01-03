# Diagramm

## Diagramm hinzufügen {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChart bietet die Methode zum Hinzufügen eines Diagramms zu einem Arbeitsblatt anhand eines bestimmten Diagrammformatsatzes (z. B. Versatz, Skalierung, Seitenverhältniseinstellung und Druckeinstellungen) und festgelegter Eigenschaften.

Das Folgende zeigt den `Type` des Diagramms, das von Excelize unterstützt wird:

Typ|Diagramm
---|---
area                        | 2D Flächendiagramm
areaStacked                 | 2D gestapeltes Flächendiagramm
areaPercentStacked          | 2D 100% gestapeltes Flächendiagramm
area3D                      | 3D Flächendiagramm
area3DStacked               | 3D gestapeltes Flächendiagramm
area3DPercentStacked        | 3D 100% gestapeltes Flächendiagramm
bar                         | 2D Clusterbalkendiagramm
barStacked                  | 2D gestapeltes Balkendiagramm
barPercentStacked           | 2D 100% gestapeltes Balkendiagramm
bar3DClustered              | 3D Clusterbalkendiagramm
bar3DStacked                | 3D gestapeltes Balkendiagramm
bar3DPercentStacked         | 3D 100% gestapeltes Balkendiagramm
bar3DConeClustered          | 3D Kegel-Cluster-Balkendiagramm
bar3DConeStacked            | 3D Kegel gestapelte Balkendiagramm
bar3DConePercentStacked     | 3D 100% Kegelbalkendiagramm
bar3DPyramidClustered       | 3D Pyramiden-Cluster-Balkendiagramm
bar3DPyramidStacked         | 3D Pyramide gestapelt Balkendiagramm
bar3DPyramidPercentStacked  | 3D 100% Pyramide gestapelt Balkendiagramm
bar3DCylinderClustered      | 3D Zylinder-Clusterbalkendiagramm
bar3DCylinderStacked        | 3D Zylinder gestapeltes Balkendiagramm
bar3DCylinderPercentStacked | 3D 100% Zylinder gestapelte Balkendiagramm
col                         | 2D Cluster-Säulendiagramm
colStacked                  | 2D gestapeltes Säulendiagramm
colPercentStacked           | 2D 100% gestapeltes Säulendiagramm
col3DClustered              | 3D Cluster-Säulendiagramm
col3D                       | 3D Säulendiagramm
col3DStacked                | 3D gestapeltes Säulendiagramm
col3DPercentStacked         | 3D 100% gestapeltes Säulendiagramm
col3DCone                   | 3D Kegel-Säulendiagramm
col3DConeClustered          | 3D Kegel-Cluster-Säulendiagramm
col3DConeStacked            | 3D Kegel gestapeltes Säulendiagramm
col3DConePercentStacked     | 3D 100% Kegel gestapeltes Säulendiagramm
col3DPyramid                | 3D Pyramidensäulendiagramm
col3DPyramidClustered       | 3D Pyramiden-Pyramiden-Säulendiagramm
col3DPyramidStacked         | 3D Pyramidenstapelsäulendiagramm
col3DPyramidPercentStacked  | 3D 100% Pyramide gestapelt Säulendiagramm
col3DCylinder               | 3D Zylinder-Säulendiagramm
col3DCylinderClustered      | 3D Zylinder-Cluster-Säulendiagramm
col3DCylinderStacked        | 3D Zylinder gestapeltes Säulendiagramm
col3DCylinderPercentStacked | 3D 100% Zylinder gestapeltsäulendiagramm
doughnut                    | donut-Diagramm
line                        | liniendiagramm
pie                         | kreisdiagramm
pie3D                       | 3D Kreisdiagramm
radar                       | netzdiagramm
scatter                     | streudiagramm
surface3D                   | 3D Oberflächendiagramm
wireframeSurface3D          | 3D Drahtmodell-Oberflächendiagramm
contour                     | konturdiagramm
wireframeContour            | wireframe-Konturdiagramm
bubble                      | blasendiagramm
bubble3D                    | 3D Blasendiagramm

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

Der Parameter `format` bietet Einstellungen für Parameter wie Diagrammversatz, Skalierung, Seitenverhältniseinstellungen und Druckeigenschaften sowie für die in der Funktion [`AddPicture`](image.md#AddPicture) verwendeten.

Legen Sie die Position des Diagrammplotbereichs nach Plotbereich fest. Folgende Eigenschaften können festgelegt werden:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
ShowBubbleSize  | `bool` | `false` | Gibt an, dass die Blasengröße auf einem Datenetikett angegeben werden soll.
ShowCatName     | `bool` | `true`  | Kategoriename.
ShowLeaderLines | `bool` | `false` | Gibt an, dass der Kategoriename auf dem Datenetikett angezeigt werden soll.
ShowPercent     | `bool` | `false` | Gibt an, dass der Prozentsatz auf einem Datenetikett angegeben werden soll.
ShowSerName     | `bool` | `false` | Gibt an, dass der Serienname auf einem Datenetikett angezeigt werden soll.
ShowVal         | `bool` | `false` | Gibt an, dass der Wert auf einem Datenetikett angezeigt werden soll.

Stellen Sie die primären Optionen für die horizontale und vertikale Achse auf `XAxis` und `YAxis` ein.

Die Eigenschaften von `XAxis`, die eingestellt werden können, sind:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
None           | `bool`     | `false` | Achsen deaktivieren.
MajorGridLines | `bool`     | `false` | Gibt die Hauptgitterlinien an.
MinorGridLines | `bool`     | `false` | Gibt kleinere Gitterlinien an.
TickLabelSkip  | `int`      | `1`     | Gibt an, wie viele Häkchen zwischen einem gezeichneten Etikett übersprungen werden sollen. Die Eigenschaft `TickLabelSkip` ist optional. Der Standardwert ist auto.
ReverseOrder   | `bool`     | `false` | Gibt an, dass die Kategorien oder Werte in umgekehrter Reihenfolge (Ausrichtung des Diagramms) sind. Die Eigenschaft `ReverseOrder` ist optional.
Maximum        | `*float64` | `0`     | Gibt an, dass das feste Maximum 0 automatisch ist. Die maximale Eigenschaft ist optional.
Minimum        | `*float64` | `0`     | Gibt an, dass das feste Minimum 0 automatisch ist. Die minimale Eigenschaft ist optional. Der Standardwert ist auto.

Die Eigenschaften von `YAxis`, die eingestellt werden können, sind:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
None           | `bool`     | `false` | Achsen deaktivieren.
MajorGridLines | `bool`     | `false` | Gibt die Hauptgitterlinien an.
MinorGridLines | `bool`     | `false` | Gibt kleinere Gitterlinien an.
MajorUnit      | `float64`  | `0`     | Gibt den Abstand zwischen den Hauptstrichen an. Muss eine positive Gleitkommazahl enthalten. Die Eigenschaft `MajorUnit` ist optional. Der Standardwert ist auto.
ReverseOrder   | `bool`     | `false` | Gibt an, dass die Kategorien oder Werte in umgekehrter Reihenfolge (Ausrichtung des Diagramms) sind. Die Eigenschaft `ReverseOrder` ist optional.
Maximum        | `*float64` | `0`     | Gibt an, dass das feste Maximum 0 automatisch ist. Die maximale Eigenschaft ist optional.
Minimum        | `*float64` | `0`     | Gibt an, dass das feste Minimum 0 automatisch ist. Die minimale Eigenschaft ist optional. Der Standardwert ist auto.

Legen Sie die Diagrammgröße anhand der Eigenschaft `Dimension` fest. Die Dimensionseigenschaft ist optional. Folgende Eigenschaften können festgelegt werden:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
height | `int` | 290 | Height
width  | `int` | 480 | Width

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
        if err := f.SetSheetRow("Sheet1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: "col",
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
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
        Title: excelize.ChartTitle{
            Name: "Clustered Column - Liniendiagramm",
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
        Type: "line",
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
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
    if err := f.SaveAs("Book1.xlsx"); err != nil {
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

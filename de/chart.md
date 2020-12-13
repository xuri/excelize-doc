# Diagramm

## Diagramm hinzufügen {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
```

AddChart bietet die Methode zum Hinzufügen eines Diagramms zu einem Arbeitsblatt anhand eines bestimmten Diagrammformatsatzes (z. B. Versatz, Skalierung, Seitenverhältniseinstellung und Druckeinstellungen) und festgelegter Eigenschaften.

Das Folgende zeigt den `type` des Diagramms, das von Excelize unterstützt wird:

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

Im Office Excel-Diagrammdatenbereich gibt `series` den Informationssatz an, für den Daten gezeichnet werden sollen, das Legendenelement (Serie) und die horizontale (Kategorie) Achsenbeschriftung.

Folgende Optionen können für die `series` eingestellt werden:

Parameter|Erläuterung
---|---
name|Legendenelement (Serie), angezeigt in der Diagrammlegende und in der Formelleiste. Der Parameter `name` ist optional. Wenn Sie diesen Wert nicht angeben, lautet der Standardwert `Serie 1 .. n`. `name` Unterstützung für die Darstellung von Formeln, zum Beispiel: `Sheet1!$A$1`.
categories|Beschriftung der horizontalen Achse (Kategorie). Der Parameter `categories` ist in den meisten Diagrammtypen optional. Der Standardwert ist eine zusammenhängende Folge der Form `1..n`.
values|Der Diagrammdatenbereich, der der wichtigste Parameter in `series` ist, ist auch der einzige erforderliche Parameter beim Erstellen eines Diagramms. Diese Option verknüpft das Diagramm mit den angezeigten Arbeitsblattdaten.
line|Hiermit wird das Linienformat des Liniendiagramms festgelegt. Die Eigenschaft `line` ist optional. Wenn sie nicht angegeben wird, wird der Standardstil verwendet. Die Optionen, die eingestellt werden können, sind `width`. Der Bereich von `width` beträgt 0.25pt - 999pt. Wenn der Wert für width außerhalb des Bereichs liegt, beträgt die Standardbreite der Linie 2pt.

Legen Sie die Eigenschaften der Diagrammlegende fest. Folgende Optionen können eingestellt werden:

Parameter|Typ|Erläuterung
---|---|---
position|string|Die Position der Diagrammlegende
show_legend_key|bool|Legende anzeigen, aber nicht mit Diagramm überlappen

Stellen Sie den `position` der Diagrammlegende ein. Die Standard-Legendenposition ist `right`. Die verfügbaren Positionen sind:

Parameter|Erläuterung
---|---
top|Oben drauf
bottom|Am Boden
left|Links
right|Rechts
top_right|Oben rechts

Der Parametersatz `show_legend_key` der Legendenschlüssel soll in Datenbeschriftungen angezeigt werden. Der Standardwert ist `false`.

Der Diagrammtitel wird durch Auswahl des Parameters `name` des Objekts `title` festgelegt. Der Titel wird über dem Diagramm angezeigt. Der Parameter `name` unterstützt die Verwendung von Formeldarstellungen wie `Sheet1!$A$1`. Wenn Sie keinen Symboltitel angeben, ist der Standardwert null.

Der Parameter `show_blanks_as` liefert die Einstellung "Zellen ausblenden und leeren". Der Standardwert ist: `gap`. In der Excel-Anwendung wird "leere Zelle als" angezeigt: "Leerzeichen". Die folgenden Werte sind für diesen Parameter optional:

Parameter|Erläuterung
---|---
gap|Leerzeichen
span|Verbinden Sie Datenpunkte mit geraden Linien
zero|Nullwert

Der Parameter `format` bietet Einstellungen für Parameter wie Diagrammversatz, Skalierung, Seitenverhältniseinstellungen und Druckeigenschaften sowie für die in der Funktion [`AddPicture()`](image.md#AddPicture) verwendeten.

Legen Sie die Position des Diagrammplotbereichs nach Plotbereich fest. Folgende Eigenschaften können festgelegt werden:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
show_bubble_size|bool|`false`|Gibt an, dass die Blasengröße auf einem Datenetikett angegeben werden soll.
show_cat_name|bool|`true`|Kategoriename.
show_leader_lines|bool|`false`|Gibt an, dass der Kategoriename auf dem Datenetikett angezeigt werden soll.
show_percent|bool|`false`|Gibt an, dass der Prozentsatz auf einem Datenetikett angegeben werden soll.
show_series_name|bool|`false`|Gibt an, dass der Serienname auf einem Datenetikett angezeigt werden soll.
show_val|bool|`false`|Gibt an, dass der Wert auf einem Datenetikett angezeigt werden soll.

Stellen Sie die primären Optionen für die horizontale und vertikale Achse auf `x_axis` und `y_axis` ein.

Die Eigenschaften von `x_axis`, die eingestellt werden können, sind:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
major_grid_lines|bool|`false`|Gibt die Hauptgitterlinien an.
minor_grid_lines|bool|`false`|Gibt kleinere Gitterlinien an.
tick_label_skip|int|`1`|Gibt an, wie viele Häkchen zwischen einem gezeichneten Etikett übersprungen werden sollen. Die Eigenschaft `tick_label_skip` ist optional. Der Standardwert ist auto.
reverse_order|bool|`false`|Gibt an, dass die Kategorien oder Werte in umgekehrter Reihenfolge (Ausrichtung des Diagramms) sind. Die Eigenschaft `reverse_order` ist optional.
maximum|int|`0`|Gibt an, dass das feste Maximum 0 automatisch ist. Die maximale Eigenschaft ist optional.
minimum|int|`0`|Gibt an, dass das feste Minimum 0 automatisch ist. Die minimale Eigenschaft ist optional. Der Standardwert ist auto.

Die Eigenschaften von `y_axis`, die eingestellt werden können, sind:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
major_grid_lines|bool|`false`|Gibt die Hauptgitterlinien an.
minor_grid_lines|bool|`false`|Gibt kleinere Gitterlinien an.
major_unit|float64|`0`|Gibt den Abstand zwischen den Hauptstrichen an. Muss eine positive Gleitkommazahl enthalten. Die Eigenschaft `major_unit` ist optional. Der Standardwert ist auto.
reverse_order|bool|`false`|Gibt an, dass die Kategorien oder Werte in umgekehrter Reihenfolge (Ausrichtung des Diagramms) sind. Die Eigenschaft `reverse_order` ist optional.
maximum|int|`0`|Gibt an, dass das feste Maximum 0 automatisch ist. Die maximale Eigenschaft ist optional.
minimum|int|`0`|Gibt an, dass das feste Minimum 0 automatisch ist. Die minimale Eigenschaft ist optional. Der Standardwert ist auto.

Legen Sie die Diagrammgröße anhand der Eigenschaft `dimension` fest. Die Dimensionseigenschaft ist optional. Folgende Eigenschaften können festgelegt werden:

Parameter|Typ|Standard|Erläuterung
---|---|---|---
height|int|290|Height
width|int|480|Width

Der Parameter `combo` gibt an, dass ein Diagramm erstellt wird, das zwei oder mehr Diagrammtypen in einem einzelnen Diagramm kombiniert. Erstellen Sie beispielsweise ein gruppiertes Spalten-Liniendiagramm mit den Daten `Sheet1!$E$1:$L$15`:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Klein", "A3": "Normal", "A4": "Groß", "B1": "Apfel", "C1": "Orange", "D1": "Birne"}
    values := map[string]int{
        "B2": 2, "C2": 3, "D2": 3, "B3": 5, "C3": 2, "D3": 4, "B4": 6, "C4": 7, "D4": 8}
    f := excelize.NewFile()
    for k, v := range categories {
        f.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Sheet1", k, v)
    }
    if err := f.AddChart("Sheet1", "E1", `{
        "type": "col",
        "series": [
        {
            "name": "Sheet1!$A$2",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$2:$D$2"
        },
        {
            "name": "Sheet1!$A$3",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$3:$D$3"
        }],
        "format":
        {
            "x_scale": 1.0,
            "y_scale": 1.0,
            "x_offset": 15,
            "y_offset": 10,
            "print_obj": true,
            "lock_aspect_ratio": false,
            "locked": false
        },
        "legend":
        {
            "position": "left",
            "show_legend_key": false
        },
        "title":
        {
            "name": "Clustered Column - Liniendiagramm"
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": true,
            "show_val": true
        }
    }`, `{
        "type": "line",
        "series": [
        {
            "name": "Sheet1!$A$4",
            "categories": "Sheet1!$B$1:$D$1",
            "values": "Sheet1!$B$4:$D$4"
        }],
        "format":
        {
            "x_scale": 1.0,
            "y_scale": 1.0,
            "x_offset": 15,
            "y_offset": 10,
            "print_obj": true,
            "lock_aspect_ratio": false,
            "locked": false
        },
        "legend":
        {
            "position": "left",
            "show_legend_key": false
        },
        "plotarea":
        {
            "show_bubble_size": true,
            "show_cat_name": false,
            "show_leader_lines": false,
            "show_percent": true,
            "show_series_name": true,
            "show_val": true
        }
    }`); err != nil {
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
func (f *File) AddChartSheet(sheet, format string, combo ...string) error
```

AddChartSheet bietet die Methode zum Erstellen eines Diagrammblatts anhand eines bestimmten Diagrammformatsatzes (z. B. Versatz, Skalierung, Einstellung des Seitenverhältnisses und Druckeinstellungen) und festgelegter Eigenschaften. In Excel ist ein Diagrammblatt ein Arbeitsblatt, das nur ein Diagramm enthält.

## Diagramm löschen {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) (err error)
```

DeleteChart bietet eine Funktion zum Löschen von Diagrammen in einer Tabelle anhand des angegebenen Arbeitsblatts und des Zellennamens.

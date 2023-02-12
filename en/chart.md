# Chart

## Add chart {#AddChart}

```go
func (f *File) AddChart(sheet, cell, opts string, combo ...string) error
```

AddChart provides the method to add a chart in a worksheet by given chart format set (such as offset, scale, aspect ratio setting, and print settings) and properties set.

The following shows the `type` of chart supported by excelize:

Type|Chart
---|---
area                        | 2D area chart
areaStacked                 | 2D stacked area chart
areaPercentStacked          | 2D 100% stacked area chart
area3D                      | 3D area chart
area3DStacked               | 3D stacked area chart
area3DPercentStacked        | 3D 100% stacked area chart
bar                         | 2D clustered bar chart
barStacked                  | 2D stacked bar chart
barPercentStacked           | 2D 100% stacked bar chart
bar3DClustered              | 3D clustered bar chart
bar3DStacked                | 3D stacked bar chart
bar3DPercentStacked         | 3D 100% stacked bar chart
bar3DConeClustered          | 3D cone clustered bar chart
bar3DConeStacked            | 3D cone stacked bar chart
bar3DConePercentStacked     | 3D 100% cone bar chart
bar3DPyramidClustered       | 3D pyramid clustered bar chart
bar3DPyramidStacked         | 3D pyramid stacked bar chart
bar3DPyramidPercentStacked  | 3D 100% pyramid stacked bar chart
bar3DCylinderClustered      | 3D cylinder clustered bar chart
bar3DCylinderStacked        | 3D cylinder stacked bar chart
bar3DCylinderPercentStacked | 3D 100% cylinder stacked bar chart
col                         | 2D clustered column chart
colStacked                  | 2D stacked column chart
colPercentStacked           | 2D 100% stacked column chart
col3DClustered              | 3D clustered column chart
col3D                       | 3D column chart
col3DStacked                | 3D stacked column chart
col3DPercentStacked         | 3D 100% stacked column chart
col3DCone                   | 3D cone column chart
col3DConeClustered          | 3D cone clustered column chart
col3DConeStacked            | 3D cone stacked column chart
col3DConePercentStacked     | 3D 100% cone stacked column chart
col3DPyramid                | 3D pyramid column chart
col3DPyramidClustered       | 3D pyramid clustered column chart
col3DPyramidStacked         | 3D pyramid stacked column chart
col3DPyramidPercentStacked  | 3D 100% pyramid stacked column chart
col3DCylinder               | 3D cylinder column chart
col3DCylinderClustered      | 3D cylinder clustered column chart
col3DCylinderStacked        | 3D cylinder stacked column chart
col3DCylinderPercentStacked | 3D 100% cylinder stacked column chart
doughnut                    | doughnut chart
line                        | line chart
pie                         | pie chart
pie3D                       | 3D pie chart
pieOfPie                    | pie of pie chart
barOfPie                    | bar of pie chart
radar                       | radar chart
scatter                     | scatter chart
surface3D                   | 3D surface chart
wireframeSurface3D          | 3D wireframe surface chart
contour                     | contour chart
wireframeContour            | wireframe contour chart
bubble                      | bubble chart
bubble3D                    | 3D bubble chart

In the Office Excel chart data range, `Series` specifies the set of information for which data to draw, the legend item (series), and the horizontal (category) axis label.

The `Series` options that can be set are:

Parameter|Explanation
---|---
Name|Legend item (series), displayed in the chart legend and formula bar. The `Name` parameter is optional. If you don't specify this value, the default will be `Series 1 .. n`. `name` support for formula representation, for example: `Sheet1!$A$1`.
Categories|Horizontal (category) axis label. The `Categories` parameter is optional in most chart types, the default is a contiguous sequence of the form `1..n`.
Values|The chart data area, which is the most important parameter in `Series`, is also the only required parameter when creating a chart. This option links the chart to the worksheet data it displays.
Line|This sets the line format of the line chart. The `Line` property is optional and if it isn't supplied it will default style. The options that can be set is `Width`. The range of `Width` is 0.25pt - 999pt. If the value of width is outside the range, the default width of the line is 2pt.
Marker|This sets the marker of the line chart and scatter chart. The range of the optional field `Size` is 2-72 (default value is `5`). The enumeration value of optional field `Symbol` are (default value is `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` and `auto`.

Set properties of the chart legend. The options that can be set are:

Parameter|Type|Explanation
---|---|---
None          | `bool`   | Specify if show the legend without overlapping the chart. The default value is `false`
Position      | `string` | The position of the chart legend
ShowLegendKey | `bool`   | Set the legend keys shall be shown in data labels

Set the `Position` of the chart legend. The default legend position is `right`. This parameter only takes effect when `none` is `false`. The available positions are:

Parameter|Explanation
---|---
top|On top
bottom|On bottom
left|On left
right|On right
top_right|On top right

The `ShowLegendKey` parameter set the legend keys shall be shown in data labels. The default value is `false`.

The chart title is set by selecting the `Name` parameter of the `Title` object, and the title will be displayed above the chart. The parameter `Name` supports the use of formula representations, such as `Sheet1!$A$1`, if you do not specify an icon title, the default value is null.

The parameter `ShowBlanksAs` provides the "Hide and empty cells" setting. The default value is: `gap`. In the Excel application "empty cell is displayed as": "space". The following are optional values for this parameter:

Parameter|Explanation
---|---
gap|space
span|Connect data points with straight lines
zero|zero value

Specifies that each data marker in the series has a different color by `VaryColors`. The default value is `true`.

The parameter `Format` provides settings for parameters such as chart offset, scale, aspect ratio settings, and print properties, as well as those used in the [`AddPicture`](image.md#AddPicture) function.

Set the position of the chart plot area by plot area. The properties that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
ShowBubbleSize  | `bool` | `false` | Specifies the bubble size shall be shown in a data label.
ShowCatName     | `bool` | `true`  | Category name.
ShowLeaderLines | `bool` | `false` | Specifies that the category name shall be shown in the data label.
ShowPercent     | `bool` | `false` | Specifies that the percentage shall be shown in a data label.
ShowSerName     | `bool` | `false` | Specifies that the series name shall be shown in a data label.
ShowVal         | `bool` | `false` | Specifies that the value shall be shown in a data label.

Set the primary horizontal and vertical axis options by `XAxis` and `YAxis`.

The properties of `XAxis` that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
None           | `bool` | `false` | Disable axes.
MajorGridLines | `bool` | `false` | Specifies major grid lines.
MinorGridLines | `bool` | `false` | Specifies minor grid lines.
TickLabelSkip  | `int`  | `1`     | Specifies how many tick labels to skip between label that is drawn. The `TickLabelSkip` property is optional. The default value is auto.
ReverseOrder   | `bool` | `false` | Specifies that the categories or values in reverse order (orientation of the chart). The `ReverseOrder` property is optional.
Maximum        | `int`  | `0`     | Specifies that the fixed maximum, 0 is auto. The maximum property is optional.
Minimum        | `int`  | `0`     | Specifies that the fixed minimum, 0 is auto. The minimum property is optional. The default value is auto.

The properties of `YAxis` that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
None           | `bool`    | `false` | Disable axes.
MajorGridLines | `bool`    | `false` | Specifies major grid lines.
MinorGridLines | `bool`    | `false` | Specifies minor grid lines.
MajorUnit      | `float64` | `0`     | Specifies the distance between major ticks. Shall contain a positive floating-point number. The `MajorUnit` property is optional. The default value is auto.
ReverseOrder   | `bool`    | `false` | Specifies that the categories or values in reverse order (orientation of the chart). The `ReverseOrder` property is optional.
Maximum        | `int`     | `0`     | Specifies that the fixed maximum, 0 is auto. The maximum property is optional.
Minimum        | `int`     | `0`     | Specifies that the fixed minimum, 0 is auto. The minimum property is optional. The default value is auto.

Set the chart size by `Dimension` property. The dimension property is optional. The properties that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
Height | `int` | 290 | Height
Width  | `int` | 480 | Width

The parameter `combo` specifies the create a chart that combines two or more chart types in a single chart. For example, create a clustered column - line chart with data `Sheet1!$E$1:$L$15`:

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
        {nil, "Apple", "Orange", "Pear"},
        {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Large", 6, 7, 8},
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
            Name: "Clustered Column - Line Chart",
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
    // Save the spreadsheet by the given path.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Add chart sheet {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, opts string, combo ...string) error
```

AddChartSheet provides the method to create a chartsheet by given chart format set (such as offset, scale, aspect ratio setting and print settings) and properties set. In Excel a chartsheet is a worksheet that only contains a chart.

## Delete chart {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart provides a function to delete chart in spreadsheet by given worksheet name and cell reference.

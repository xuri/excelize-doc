# Chart

## Add chart {#AddChart}

```go
func (f *File) AddChart(sheet, cell, opts string, combo ...string) error
```

AddChart provides the method to add a chart in a worksheet by given chart format set (such as offset, scale, aspect ratio setting, and print settings) and properties set.

The following shows the `Type` of chart supported by excelize:

ID|Enumeration|Chart
---|---|---
0  | Area                        | 2D area chart
1  | AreaStacked                 | 2D stacked area chart
2  | AreaPercentStacked          | 2D 100% stacked area chart
3  | Area3D                      | 3D area chart
4  | Area3DStacked               | 3D stacked area chart
5  | Area3DPercentStacked        | 3D 100% stacked area chart
6  | Bar                         | 2D clustered bar chart
7  | BarStacked                  | 2D stacked bar chart
8  | BarPercentStacked           | 2D 100% stacked bar chart
9  | Bar3DClustered              | 3D clustered bar chart
10 | Bar3DStacked                | 3D stacked bar chart
11 | Bar3DPercentStacked         | 3D 100% stacked bar chart
12 | Bar3DConeClustered          | 3D cone clustered bar chart
13 | Bar3DConeStacked            | 3D cone stacked bar chart
14 | Bar3DConePercentStacked     | 3D 100% cone bar chart
15 | Bar3DPyramidClustered       | 3D pyramid clustered bar chart
16 | Bar3DPyramidStacked         | 3D pyramid stacked bar chart
17 | Bar3DPyramidPercentStacked  | 3D 100% pyramid stacked bar chart
18 | Bar3DCylinderClustered      | 3D cylinder clustered bar chart
19 | Bar3DCylinderStacked        | 3D cylinder stacked bar chart
20 | Bar3DCylinderPercentStacked | 3D 100% cylinder stacked bar chart
21 | Col                         | 2D clustered column chart
22 | ColStacked                  | 2D stacked column chart
23 | ColPercentStacked           | 2D 100% stacked column chart
24 | Col3DClustered              | 3D clustered column chart
25 | Col3D                       | 3D column chart
26 | Col3DStacked                | 3D stacked column chart
27 | Col3DPercentStacked         | 3D 100% stacked column chart
28 | Col3DCone                   | 3D cone column chart
29 | Col3DConeClustered          | 3D cone clustered column chart
30 | Col3DConeStacked            | 3D cone stacked column chart
31 | Col3DConePercentStacked     | 3D 100% cone stacked column chart
32 | Col3DPyramid                | 3D pyramid column chart
33 | Col3DPyramidClustered       | 3D pyramid clustered column chart
34 | Col3DPyramidStacked         | 3D pyramid stacked column chart
35 | Col3DPyramidPercentStacked  | 3D 100% pyramid stacked column chart
36 | Col3DCylinder               | 3D cylinder column chart
37 | Col3DCylinderClustered      | 3D cylinder clustered column chart
38 | Col3DCylinderStacked        | 3D cylinder stacked column chart
39 | Col3DCylinderPercentStacked | 3D 100% cylinder stacked column chart
40 | Doughnut                    | doughnut chart
41 | Line                        | line chart
42 | Line3D                      | 3D line chart
43 | Pie                         | pie chart
44 | Pie3D                       | 3D pie chart
45 | PieOfPie                    | pie of pie chart
46 | BarOfPie                    | bar of pie chart
47 | Radar                       | radar chart
48 | Scatter                     | scatter chart
49 | Surface3D                   | 3D surface chart
50 | WireframeSurface3D          | 3D wireframe surface chart
51 | Contour                     | contour chart
52 | WireframeContour            | wireframe contour chart
53 | Bubble                      | bubble chart
54 | Bubble3D                    | 3D bubble chart
55 | StockHighLowClose           | High-Low-Close stock chart
56 | StockOpenHighLowClose       | Open-High-Low-Close stock chart

In the Office Excel chart data range, `Series` specifies the set of information for which data to draw, the legend item (series), and the horizontal (category) axis label.

The `Series` options that can be set are:

Parameter|Explanation
---|---
Name              | Legend item (series), displayed in the chart legend and formula bar. The `Name` parameter is optional. If you don't specify this value, the default will be `Series 1 .. n`. `Name` support for formula representation, for example: `Sheet1!$A$1`.
Categories        | Horizontal (category) axis label. The `Categories` parameter is optional in most chart types, the default is a contiguous sequence of the form `1..n`.
Values            | The chart data area, which is the most important parameter in `Series`, is also the only required parameter when creating a chart. This option links the chart to the worksheet data it displays.
Fill              | This sets the format for the data series fill.
Legend            | This set the font of legend text for a data series. The `Legend` property is optional.
Line              | This sets the line format of the line chart. The `Line` property is optional and if it isn't supplied it will default style. The options that can be set is `Width`. The range of `Width` is 0.25pt - 999pt. If the value of width is outside the range, the default width of the line is 2pt.
Marker            | This sets the marker of the line chart and scatter chart. The range of the optional field `Size` is 2-72 (default value is `5`). The enumeration value of optional field `Symbol` are (default value is `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` and `auto`.
DataLabelPosition | This sets the position of the chart series data label.

Set properties of the chart legend. The options that can be set are:

Parameter|Type|Explanation
---|---|---
Position      | `string` | The position of the chart legend
ShowLegendKey | `bool`   | Set the legend keys shall be shown in data labels
Font          | `Font`   | Set the font properties of the chart legend text. The properties that can be set are the same as the font object that is used for cell formatting. The font family, size, color, bold, italic, underline, and strike properties can be set

Set the `Position` of the chart legend. The default legend position is `right`. This parameter only takes effect when `none` is `false`. The available positions are:

Parameter|Explanation
---|---
none      | Disable legend
top       | On top
bottom    | On bottom
left      | On left
right     | On right
top_right | On top right

The `ShowLegendKey` parameter set the legend keys shall be shown in data labels. The default value is `false`.

The chart title is set by selecting the `Name` parameter of the `Title` object, and the title will be displayed above the chart. The parameter `Name` supports the use of formula representations, such as `Sheet1!$A$1`, if you do not specify an icon title, the default value is null.

The parameter `ShowBlanksAs` provides the "Hide and empty cells" setting. The default value is: `gap`. In the Excel application "empty cell is displayed as": "space". The following are optional values for this parameter:

Parameter|Explanation
---|---
gap  | Space
span | Connect data points with straight lines
zero | Zero value

Set chart legend for all data series by `Legend` property. The `Legend` property is optional.

Set the bubble size in all data series for the bubble chart or 3D bubble chart by `BubbleSizes` property. The `BubbleSizes` property is optional. The default width is `100`, and the value should be great than 0 and less or equal than 300.

Set the doughnut hole size in all data series for the doughnut chart by `HoleSize` property. The `HoleSize` property is optional. The default width is `75`, and the value should be great than 0 and less or equal than 90.

Specifies that each data marker in the series has a different color by `VaryColors`. The default value is `true`.

The parameter `Format` provides settings for parameters such as chart offset, scale, aspect ratio settings, and print properties, as well as those used in the [`AddPicture`](image.md#AddPicture) function.

Set the position of the chart plot area by plot area. The properties that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
SecondPlotValues  | `int`            | `0`     | Specifies the values in second plot for the `PieOfPie` and `BarOfPie` chart.
ShowBubbleSize    | `bool`           | `false` | Specifies the bubble size shall be shown in a data label.
ShowCatName       | `bool`           | `true`  | Specifies that the category name shall be shown in the data label. The `ShowCatName` property is optional.
ShowDataTable     | `bool`           | `false` | Used for add data table under chart, depending on the chart type, only available for area, bar, column and line series type charts.
ShowDataTableKeys | `bool`           | `false` | Used for add legend key in data table, only works on `ShowDataTable` is enabled. The `ShowDataTableKeys` property is optional.
ShowLeaderLines   | `bool`           | `false` | Specifies leader lines shall be shown for data labels. The `ShowLeaderLines` property is optional.
ShowPercent       | `bool`           | `false` | Specifies that the percentage shall be shown in a data label.
ShowSerName       | `bool`           | `false` | Specifies that the series name shall be shown in a data label.
ShowVal           | `bool`           | `false` | Specifies that the value shall be shown in a data label.
Fill              | `Fill`           | N/A     | Set fill color of the chart.
UpBars            | `ChartUpDownBar` | N/A     | Specifies the format for stock chart up bars. The `UpBars` property is optional.
DownBars          | `ChartUpDownBar` | N/A     | Specifies the format for stock chart down bars. The `DownBars` property is optional.
NumFmt            | `ChartNumFmt`    | N/A     | Specifies that if linked to source and set custom number format code for data labels. The `NumFmt` property is optional. The default format code is `General`.

Set the primary horizontal and vertical axis options by `XAxis` and `YAxis`.

The properties of `XAxis` that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
None           | `bool`          | `false` | Disable axes.
MajorGridLines | `bool`          | `false` | Specifies major grid lines.
MinorGridLines | `bool`          | `false` | Specifies minor grid lines.
TickLabelSkip  | `int`           | `1`     | Specifies how many tick labels to skip between label that is drawn. The `TickLabelSkip` property is optional. The default value is auto.
ReverseOrder   | `bool`          | `false` | Specifies that the categories or values in reverse order (orientation of the chart). The `ReverseOrder` property is optional.
Maximum        | `*float64`      | `0`     | Specifies that the fixed maximum, 0 is auto. The maximum property is optional.
Minimum        | `*float64`      | `0`     | Specifies that the fixed minimum, 0 is auto. The minimum property is optional. The default value is auto.
Alignment      | `Alignment`     | N/A     | Specifies that the alignment of the horizontal and vertical axis. The properties of font that can be set are: `TextRotation` and `Vertical`
Font           | `Font`          | N/A     | Specifies that the font of the horizontal axis.
NumFmt         | `ChartNumFmt`   | N/A     | Specifies that if linked to source and set custom number format code for axis.
Title          | `[]RichTextRun` | N/A     | Specifies that the primary horizontal axis title and resize chart.

The properties of `YAxis` that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
None           | `bool`          | `false` | Disable axes.
MajorGridLines | `bool`          | `false` | Specifies major grid lines.
MinorGridLines | `bool`          | `false` | Specifies minor grid lines.
MajorUnit      | `float64`       | `0`     | Specifies the distance between major ticks. Shall contain a positive floating-point number. The `MajorUnit` property is optional. The default value is auto.
ReverseOrder   | `bool`          | `false` | Specifies that the categories or values in reverse order (orientation of the chart). The `ReverseOrder` property is optional.
Maximum        | `*float64`      | `0`     | Specifies that the fixed maximum, 0 is auto. The maximum property is optional.
Minimum        | `*float64`      | `0`     | Specifies that the fixed minimum, 0 is auto. The minimum property is optional. The default value is auto.
Alignment      | `Alignment`     | N/A     | Specifies that the alignment of the horizontal and vertical axis. The properties of font that can be set are: `TextRotation` and `Vertical`
Font           | `Font`          | N/A     | Specifies that the font of the vertical axis.
LogBase        | `float64`       | N/A     | Specifies logarithmic scale base number of the vertical axis.
NumFmt         | `ChartNumFmt`   | N/A     | Specifies that if linked to source and set custom number format code for axis.
Title          | `[]RichTextRun` | N/A     | Specifies that the primary vertical axis title and resize chart.

The value of `TextRotation` that can be set from -90 to 90.

The value of `Vertical` that can be set are: `horz`, `vert`, `vert270`, `wordArtVert`, `eaVert`, `mongolianVert` and `wordArtVertRtl`.

Set the chart size by `Dimension` property. The dimension property is optional. The properties that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
Height | `uint` | 260 | Height
Width  | `uint` | 480 | Width

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
        Type: excelize.Col,
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
        Title: []excelize.RichTextRun{
            {
                Text: "Clustered Column - Line Chart",
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

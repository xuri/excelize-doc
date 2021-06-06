# Chart

## Add chart {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
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
radar                       | radar chart
scatter                     | scatter chart
surface3D                   | 3D surface chart
wireframeSurface3D          | 3D wireframe surface chart
contour                     | contour chart
wireframeContour            | wireframe contour chart
bubble                      | bubble chart
bubble3D                    | 3D bubble chart

In the Office Excel chart data range, `series` specifies the set of information for which data to draw, the legend item (series), and the horizontal (category) axis label.

The `series` options that can be set are:

Parameter|Explanation
---|---
name|Legend item (series), displayed in the chart legend and formula bar. The `name` parameter is optional. If you don't specify this value, the default will be `Series 1 .. n`. `name` support for formula representation, for example: `Sheet1!$A$1`.
categories|Horizontal (category) axis label. The `categories` parameter is optional in most chart types, the default is a contiguous sequence of the form `1..n`.
values|The chart data area, which is the most important parameter in `series`, is also the only required parameter when creating a chart. This option links the chart to the worksheet data it displays.
line|This sets the line format of the line chart. The `line` property is optional and if it isn't supplied it will default style. The options that can be set is `width`. The range of `width` is 0.25pt - 999pt. If the value of width is outside the range, the default width of the line is 2pt.
marker|This sets the marker of the line chart and scatter chart. The range of the optional field `size` is 2-72 (default value is `5`). The enumeration value of optional field `symbol` are (default value is `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` and `auto`.

Set properties of the chart legend. The options that can be set are:

Parameter|Type|Explanation
---|---|---
none|bool|Specify if show the legend without overlapping the chart. The default value is `false`
position|string|The position of the chart legend
show_legend_key|bool|Set the legend keys shall be shown in data labels

Set the `position` of the chart legend. The default legend position is `right`. This parameter only takes effect when `none` is `false`. The available positions are:

Parameter|Explanation
---|---
top|On top
bottom|On bottom
left|On left
right|On right
top_right|On top right

The `show_legend_key` parameter set the legend keys shall be shown in data labels. The default value is `false`.

The chart title is set by selecting the `name` parameter of the `title` object, and the title will be displayed above the chart. The parameter `name` supports the use of formula representations, such as `Sheet1!$A$1`, if you do not specify an icon title, the default value is null.

The parameter `show_blanks_as` provides the "Hide and empty cells" setting. The default value is: `gap`. In the Excel application "empty cell is displayed as": "space". The following are optional values for this parameter:

Parameter|Explanation
---|---
gap|space
span|Connect data points with straight lines
zero|zero value

Specifies that each data marker in the series has a different color by `vary_colors`. The default value is `true`.

The parameter `format` provides settings for parameters such as chart offset, scale, aspect ratio settings, and print properties, as well as those used in the [`AddPicture()`](image.md#AddPicture) function.

Set the position of the chart plot area by plot area. The properties that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
show_bubble_size|bool|`false`|Specifies the bubble size shall be shown in a data label.
show_cat_name|bool|`true`|Category name.
show_leader_lines|bool|`false`|Specifies that the category name shall be shown in the data label.
show_percent|bool|`false`|Specifies that the percentage shall be shown in a data label.
show_series_name|bool|`false`|Specifies that the series name shall be shown in a data label.
show_val|bool|`false`|Specifies that the value shall be shown in a data label.

Set the primary horizontal and vertical axis options by `x_axis` and `y_axis`.

The properties of `x_axis` that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
none|bool|`false`|Disable axes.
major_grid_lines|bool|`false`|Specifies major gridlines.
minor_grid_lines|bool|`false`|Specifies minor gridlines.
tick_label_skip|int|`1`|Specifies how many tick labels to skip between label that is drawn. The `tick_label_skip` property is optional. The default value is auto.
reverse_order|bool|`false`|Specifies that the categories or values in reverse order (orientation of the chart). The `reverse_order` property is optional.
maximum|int|`0`|Specifies that the fixed maximum, 0 is auto. The maximum property is optional.
minimum|int|`0`|Specifies that the fixed minimum, 0 is auto. The minimum property is optional. The default value is auto.

The properties of `y_axis` that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
none|bool|`false`|Disable axes.
major_grid_lines|bool|`false`|Specifies major gridlines.
minor_grid_lines|bool|`false`|Specifies minor gridlines.
major_unit|float64|`0`|Specifies the distance between major ticks. Shall contain a positive floating-point number. The `major_unit` property is optional. The default value is auto.
reverse_order|bool|`false`|Specifies that the categories or values in reverse order (orientation of the chart). The `reverse_order` property is optional.
maximum|int|`0`|Specifies that the fixed maximum, 0 is auto. The maximum property is optional.
minimum|int|`0`|Specifies that the fixed minimum, 0 is auto. The minimum property is optional. The default value is auto.

Set the chart size by `dimension` property. The dimension property is optional. The properties that can be set are:

Parameter|Type|Default|Explanation
---|---|---|---
height|int|290|Height
width|int|480|Width

The parameter `combo` specifies the create a chart that combines two or more chart types in a single chart. For example, create a clustered column - line chart with data `Sheet1!$E$1:$L$15`:

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Small", "A3": "Normal", "A4": "Large",
        "B1": "Apple", "C1": "Orange", "D1": "Pear"}
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
            "name": "Clustered Column - Line Chart"
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
            "position": "right",
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
    // Save the spreadsheet by the given path.
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Add chart sheet {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, format string, combo ...string) error
```

AddChartSheet provides the method to create a chartsheet by given chart format set (such as offset, scale, aspect ratio setting and print settings) and properties set. In Excel a chartsheet is a worksheet that only contains a chart.

## Delete chart {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) (err error)
```

DeleteChart provides a function to delete charts in a spreadsheet by given worksheet and cell name.

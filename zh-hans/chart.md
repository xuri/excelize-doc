# 图表

## 添加图表 {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
```

根据给定的工作表名称、单元格坐标和图表样式属性插入图表。

下面是 Excelize 支持创建的图表类型 `type`：

名称|图表类型
---|---
area                        | 二维面积图
areaStacked                 | 二维堆积面积图
areaPercentStacked          | 二维百分比堆积面积图
area3D                      | 三维面积图
area3DStacked               | 三维堆积面积图
area3DPercentStacked        | 三维百分比堆积面积图
bar                         | 二维簇状条形图
barStacked                  | 二维堆积条形图
barPercentStacked           | 二维百分比堆积条形图
bar3DClustered              | 三维簇状条形图
bar3DStacked                | 三维堆积条形图
bar3DPercentStacked         | 三维百分比堆积条形图
bar3DConeClustered          | 三维簇状水平圆锥图
bar3DConeStacked            | 三维堆积水平圆锥图
bar3DConePercentStacked     | 三维堆积百分比水平圆锥图
bar3DPyramidClustered       | 三维簇状水平棱锥图
bar3DPyramidStacked         | 三维堆积水平棱锥图
bar3DPyramidPercentStacked  | 三维堆积百分比水平棱锥图
bar3DCylinderClustered      | 三维簇状水平圆柱图
bar3DCylinderStacked        | 三维堆积水平圆柱图
bar3DCylinderPercentStacked | 三维堆积百分比水平圆柱图
col                         | 二维簇状柱形图
colStacked                  | 二维堆积柱形图
colPercentStacked           | 二维百分比堆积柱形图
col3D                       | 三维柱形图
col3DClustered              | 三维簇状柱形图
col3DStacked                | 三维堆积柱形图
col3DPercentStacked         | 三维百分比堆积柱形图
col3DCone                   | 三维圆锥图
col3DConeClustered          | 三维簇状圆锥图
col3DConeStacked            | 三维堆积圆锥图
col3DConePercentStacked     | 三维百分比堆积圆锥图
col3DPyramid                | 三维棱锥图
col3DPyramidClustered       | 三维簇状棱锥图
col3DPyramidStacked         | 三维堆积棱锥图
col3DPyramidPercentStacked  | 三维百分比堆积棱锥图
col3DCylinder               | 三维圆柱图
col3DCylinderClustered      | 三维簇状圆柱图
col3DCylinderStacked        | 三维堆积圆柱图
col3DCylinderPercentStacked | 三维百分比堆积圆柱图
doughnut                    | 圆环图
line                        | 折线图
pie                         | 饼图
pie3D                       | 三维饼图
radar                       | 雷达图
scatter                     | 散点图
surface3D                   | 三维曲面图
wireframeSurface3D          | 三维曲面图（框架图）
contour                     | 曲面图
wireframeContour            | 曲面图（俯视框架图）
bubble                      | 气泡图
bubble3D                    | 三维气泡图

在 Office Excel 中图表数据区域 `series` 指定了绘制哪些数据的信息集合、图例项（系列）和水平（分类）轴标签。

下面是 Excelize 中 `series` 的可选参数：

参数|含义
---|---
name|图例项（系列），在图表图例和公式栏中显示。`name` 参数是可选的，如果不指定该值默认将会使用 `Series 1 .. n` 表示。`name` 支持使用公式表示，例如：`Sheet1!$A$1`。
categories|水平（分类）轴标签。在大多数图表类型中，`categories` 属性是可选的，默认为形如 `1..n` 的连续序列。
values|图表数据区域，是 `series` 中最重要的参数，也是创建图表时唯一的必选参数。该选项将图表与其显示的工作表数据链接起来。
line |设置折线图的折线格式。`line` 属性是可选的，如果未指定该属性，则为默认样式。可以设置的选项是 `width`，宽度范围是 0.25pt 至 999pt。如果 `width` 的值超出范围，则线的默认宽度为 2pt。
marker|设置折线图和散点图数据系列线型宽度和线端类型。可选参数 `size` 指定线型宽度，其取值范围是 2-72 (默认缺省值为 `5`)。线端类型可选参数 `symbol` 的枚举值为 (默认缺省值为 `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` 和 `auto`.

参数 `legend` 提供对图例项的属性设置方法，下面是 Excelize 中 `legend` 的可选参数：

参数|类型|含义
---|---|---
none|bool|指定是否关闭不与图表重叠的图例。默认值为 `false`
position|string|图例位置
show_legend_key|bool|指定是否在数据标签中显示图例项标示

其中参数 `position` 默认值为 `right`，该参数仅在当显示图例（即 `none` 的值为 `false`）时生效。下面是该参数的可选值：

可选值|含义
---|---
top|靠上
bottom|靠下
left|靠左
right|靠右
top_right|右上

其中参数 `show_legend_key` 默认值为 `false`。

通过可选 `title` 对象的 `name` 参数设置图表标题，标题将会在图表上方显示。参数 `name` 支持使用公式表示，例如 `Sheet1!$A$1`，图表标题的默认值为空。

参数 `show_blanks_as` 提供“隐藏和清空单元格”设置，默认值为：`gap` 即“空单元格显示为”：“空距”。下面是该参数的可选值：

值|含义
---|---
gap|空距
span|用直线连接数据点
zero|零值

通过参数 `vary_colors` 指定是否设置图表数据系列格式为自动填充颜色，默认值为 `true`。

参数 `format` 提供对图表偏移、缩放、高宽比设置和打印属性等参数的设置，其参数与在 [`AddPicture`](image.md#AddPicture) 函数中所使用的相同。

通过可选 `plotarea` 对象设置数据标签格式，可选参数如下：

参数|类型|默认值|含义
---|---|---|---
show_bubble_size|bool|`false`|气泡大小
show_cat_name|bool|`true`|类别名称
show_leader_lines|bool|`false`|显示引导线
show_percent|bool|`false`|百分比
show_series_name|bool|`false`|系列名称
show_val|bool|`false`|值

通过参数 `x_axis` 和 `y_axis` 参数设置坐标轴选项。

下面是 `x_axis` 参数的可选值：

参数|类型|默认值|含义
---|---|---|---
none|bool|`false`|隐藏坐标轴
major_grid_lines|bool|`false`|主要网格线
minor_grid_lines|bool|`false`|次要网格线
tick_label_skip|int|`1`|指定标签间隔单位
reverse_order|bool|`false`|逆序刻度值
maximum|int|`0`|最大值，`0` 代表自动
minimum|int|`0`|最小值，`0` 代表自动

下面是 `y_axis` 参数的可选值：

参数|类型|默认值|含义
---|---|---|---
none|bool|`false`|隐藏坐标轴
major_grid_lines|bool|`false`|主要网格线
minor_grid_lines|bool|`false`|次要网格线
major_unit|float64|`0`|坐标轴主要刻度单位
reverse_order|bool|`false`|逆序刻度值
maximum|int|`0`|最大值，`0` 代表自动
minimum|int|`0`|最小值，`0` 代表自动

通过可选 `dimension` 对象设置图表的大小，可选参数如下：

参数|类型|默认值|含义
---|---|---|---
height|int|290|高度
width|int|480|宽度

参数 `combo` 用来指定创建组合图表，该图表将两个或多个图表类型组合在一个图表中。例如，在 `Sheet1!$E$1:$L$15` 区域创建一个 簇状柱形图 - 折线图：

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
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
            "name": "簇状柱形图 - 折线图"
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
    // 保存工作簿
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 创建图表工作表 {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, format string, combo ...string) error
```

根据给定的工作表名称和图表样式属性创建图表工作表，图表样式属性的定义与 [AddChart](chart.md#AddChart) 函数相同。Excel 中的图表工作表是仅包含图表的工作表。

## 删除图表 {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) (err error)
```

根据给定的工作表名称和单元格坐标删除图表。

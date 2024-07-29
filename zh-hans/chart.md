# 图表

{{ book.info }}

## 添加图表 {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

根据给定的工作表名称、单元格坐标和图表样式属性插入图表。

下面是 Excelize 支持创建的图表类型 `Type`：

ID|枚举|图表类型
---|---|---
0  | Area                        | 二维面积图
1  | AreaStacked                 | 二维堆积面积图
2  | AreaPercentStacked          | 二维百分比堆积面积图
3  | Area3D                      | 三维面积图
4  | Area3DStacked               | 三维堆积面积图
5  | Area3DPercentStacked        | 三维百分比堆积面积图
6  | Bar                         | 二维簇状条形图
7  | BarStacked                  | 二维堆积条形图
8  | BarPercentStacked           | 二维百分比堆积条形图
9  | Bar3DClustered              | 三维簇状条形图
10 | Bar3DStacked                | 三维堆积条形图
11 | Bar3DPercentStacked         | 三维百分比堆积条形图
12 | Bar3DConeClustered          | 三维簇状水平圆锥图
13 | Bar3DConeStacked            | 三维堆积水平圆锥图
14 | Bar3DConePercentStacked     | 三维堆积百分比水平圆锥图
15 | Bar3DPyramidClustered       | 三维簇状水平棱锥图
16 | Bar3DPyramidStacked         | 三维堆积水平棱锥图
17 | Bar3DPyramidPercentStacked  | 三维堆积百分比水平棱锥图
18 | Bar3DCylinderClustered      | 三维簇状水平圆柱图
19 | Bar3DCylinderStacked        | 三维堆积水平圆柱图
20 | Bar3DCylinderPercentStacked | 三维堆积百分比水平圆柱图
21 | Col                         | 二维簇状柱形图
22 | ColStacked                  | 二维堆积柱形图
23 | ColPercentStacked           | 二维百分比堆积柱形图
24 | Col3D                       | 三维柱形图
25 | Col3DClustered              | 三维簇状柱形图
26 | Col3DStacked                | 三维堆积柱形图
27 | Col3DPercentStacked         | 三维百分比堆积柱形图
28 | Col3DCone                   | 三维圆锥图
29 | Col3DConeClustered          | 三维簇状圆锥图
30 | Col3DConeStacked            | 三维堆积圆锥图
31 | Col3DConePercentStacked     | 三维百分比堆积圆锥图
32 | Col3DPyramid                | 三维棱锥图
33 | Col3DPyramidClustered       | 三维簇状棱锥图
34 | Col3DPyramidStacked         | 三维堆积棱锥图
35 | Col3DPyramidPercentStacked  | 三维百分比堆积棱锥图
36 | Col3DCylinder               | 三维圆柱图
37 | Col3DCylinderClustered      | 三维簇状圆柱图
38 | Col3DCylinderStacked        | 三维堆积圆柱图
39 | Col3DCylinderPercentStacked | 三维百分比堆积圆柱图
40 | Doughnut                    | 圆环图
41 | Line                        | 折线图
42 | Line3D                      | 三维折线图
43 | Pie                         | 饼图
44 | Pie3D                       | 三维饼图
45 | PieOfPie                    | 子母饼图
46 | BarOfPie                    | 复合条饼图
47 | Radar                       | 雷达图
48 | Scatter                     | 散点图
49 | Surface3D                   | 三维曲面图
50 | WireframeSurface3D          | 三维曲面图（框架图）
51 | Contour                     | 曲面图
52 | WireframeContour            | 曲面图（俯视框架图）
53 | Bubble                      | 气泡图
54 | Bubble3D                    | 三维气泡图

在 Office Excel 中图表数据区域 `Series` 指定了绘制哪些数据的信息集合、图例项（系列）和水平（分类）轴标签。

下面是 Excelize 中 `Series` 的可选参数：

参数|含义
---|---
Name              | 图例项（系列），在图表图例和公式栏中显示。`Name` 参数是可选的，如果不指定该值默认将会使用 `Series 1 .. n` 表示。`Name` 支持使用公式表示，例如：`Sheet1!$A$1`。
Categories        | 水平（分类）轴标签。在大多数图表类型中，`Categories` 属性是可选的，默认为形如 `1..n` 的连续序列。
Values            | 图表数据区域，是 `Series` 中最重要的参数，也是创建图表时唯一的必选参数。该选项将图表与其显示的工作表数据链接起来。
Fill              | 设置图表中每个数据系列的填充格式。
Line              | 设置折线图的折线格式。`Line` 属性是可选的，如果未指定该属性，则为默认样式。可以设置的选项是 `Width`，宽度范围是 0.25pt 至 999pt。如果 `Width` 的值超出范围，则线的默认宽度为 2pt。
Marker            | 设置折线图和散点图的数据点标记格式。可选参数 `Size` 内置数据标记图形的大小，其取值范围是 2-72 (默认缺省值为 `5`)。线端类型可选参数 `Symbol` 的枚举值为 (默认缺省值为 `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` 和 `auto`.
DataLabelPosition | 设置图表中每个数据系列数据标签的位置。

参数 `Legend` 提供对图例项的属性设置方法，下面是 Excelize 中 `Legend` 的可选参数：

参数|类型|含义
---|---|---
Position        | `string` | 图例位置
ShowLegendKey   | `bool`   | 指定是否在数据标签中显示图例项标示

其中参数 `Position` 默认值为 `right`。下面是该参数的可选值：

可选值|含义
---|---
none      | 关闭图例
top       | 靠上
bottom    | 靠下
left      | 靠左
right     | 靠右
top_right | 右上

其中参数 `ShowLegendKey`  默认值为 `false`。

通过可选 `Title` 对象的 `Name` 参数设置图表标题，标题将会在图表上方显示。参数 `Name` 支持使用公式表示，例如 `Sheet1!$A$1`，图表标题的默认值为空。

参数 `ShowBlanksAs` 提供“隐藏和清空单元格”设置，默认值为：`gap` 即“空单元格显示为”：“空距”。下面是该参数的可选值：

值|含义
---|---
gap  | 空距
span | 用直线连接数据点
zero | 零值

参数 `BubbleSize` 用于设置气泡图和三维气泡图的气泡大小。该参数是可选的，其取值范围是 1-300 (默认缺省值为 `100`)

参数 `HoleSize` 用于设置圆环图的圆环内径大小。该参数是可选的，其取值范围是 1-90 (默认缺省值为 `75`)

参数 `VaryColors` 用于指定是否设置图表数据系列格式为自动填充颜色，默认值为 `true`。

参数 `Format` 提供对图表偏移、缩放、高宽比设置和打印属性等参数的设置，其参数与在 [`AddPicture`](image.md#AddPicture) 函数中所使用的相同。

通过可选 `PlotArea` 对象设置绘图区域格式，可选参数如下：

参数|类型|默认值|含义
---|---|---|---
SecondPlotValues | `int`         | `0`     | 子母饼图和复合条饼图中第二绘图区域中的数据系列数量
ShowBubbleSize   | `bool`        | `false` | 气泡大小
ShowCatName      | `bool`        | `false` | 类别名称
ShowLeaderLines  | `bool`        | `false` | 显示引导线
ShowPercent      | `bool`        | `false` | 百分比
ShowSerName      | `bool`        | `false` | 系列名称
ShowVal          | `bool`        | `false` | 值
NumFmt           | `ChartNumFmt` | N/A     | 设置数据标签的数字格式和链接到源

通过参数 `XAxis` 和 `YAxis` 参数设置坐标轴选项。

下面是 `XAxis` 参数的可选值：

参数|类型|默认值|含义
---|---|---|---
None           | `bool`          | `false` | 隐藏坐标轴
MajorGridLines | `bool`          | `false` | 主要网格线
MinorGridLines | `bool`          | `false` | 次要网格线
TickLabelSkip  | `int`           | `1`     | 指定标签间隔单位
ReverseOrder   | `bool`          | `false` | 逆序刻度值
Maximum        | `*float64`      | `0`     | 最大值，`0` 代表自动
Minimum        | `*float64`      | `0`     | 最小值，`0` 代表自动
Font           | `Font`          | N/A     | 设置水平坐标轴刻度字体格式
NumFmt         | `ChartNumFmt`   | N/A     | 设置水平坐标轴数字格式和链接到源
Title          | `[]RichTextRun` | N/A     | 设置位于坐标轴下方的主要横坐标轴标题，并调整图表大小

下面是 `YAxis` 参数的可选值：

参数|类型|默认值|含义
---|---|---|---
None           | `bool`          | `false` | 隐藏坐标轴
MajorGridLines | `bool`          | `false` | 主要网格线
MinorGridLines | `bool`          | `false` | 次要网格线
MajorUnit      | `float64`       | `0`     | 坐标轴主要刻度单位，`MajorUnit` 参数为可选参数，默认值 `0` 代表为自动
ReverseOrder   | `bool`          | `false` | 逆序刻度值
Maximum        | `*float64`      | `0`     | 最大值，`0` 代表自动
Minimum        | `*float64`      | `0`     | 最小值，`0` 代表自动
Font           | `Font`          | N/A     | 设置垂直坐标轴刻度字体格式
LogBase        | `float64`       | N/A     | 设置垂直坐标轴对数刻度的基数
NumFmt         | `ChartNumFmt`   | N/A     | 设置垂直坐标轴数字格式和链接到源
Title          | `[]RichTextRun` | N/A     | 设置旋转过的主要纵坐标轴标题，并调整图表大小

通过可选 `Dimension` 对象设置图表的大小，可选参数如下：

参数|类型|默认值|含义
---|---|---|---
Height | `uint` | 260 | 高度
Width  | `uint` | 480 | 宽度

参数 `combo` 用来指定创建组合图表，该图表将两个或多个图表类型组合在一个图表中。例如，在 `Sheet1!$E$1:$L$15` 区域创建一个 簇状柱形图 - 折线图：

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
                Text: "簇状柱形图 - 折线图",
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
    // 保存工作簿
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 创建图表工作表 {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

根据给定的工作表名称和图表样式属性创建图表工作表，图表样式属性的定义与 [AddChart](chart.md#AddChart) 函数相同。Excel 中的图表工作表是仅包含图表的工作表。

## 删除图表 {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

根据给定的工作表名称和单元格坐标删除图表。

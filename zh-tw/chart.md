# 圖表

## 添加圖表 {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

根據給定的工作表名稱、儲存格坐標和圖表樣式屬性插入圖表。

下面是 Excelize 支持創建的圖表類別 `Type`：

ID|列舉|圖表類別
---|---|---
0  | Area                        | 二維區域圖
1  | AreaStacked                 | 二維堆疊區域圖
2  | AreaPercentStacked          | 二維百分比堆疊區域圖
3  | Area3D                      | 立體區域圖
4  | Area3DStacked               | 立體堆疊區域圖
5  | Area3DPercentStacked        | 立體百分比堆疊區域圖
6  | Bar                         | 二維群組條形圖
7  | BarStacked                  | 二維堆疊條形圖
8  | BarPercentStacked           | 二維百分比堆疊條形圖
9  | Bar3DClustered              | 立體群組條形圖
10 | Bar3DStacked                | 立體堆疊條形圖
11 | Bar3DPercentStacked         | 立體百分比堆疊條形圖
12 | Bar3DConeClustered          | 立體群組水平圓錐圖
13 | Bar3DConeStacked            | 立體堆疊水平圓錐圖
14 | Bar3DConePercentStacked     | 立體堆疊百分比水平圓錐圖
15 | Bar3DPyramidClustered       | 立體群組水平稜錐圖
16 | Bar3DPyramidStacked         | 立體堆疊水平稜錐圖
17 | Bar3DPyramidPercentStacked  | 立體堆疊百分比水平稜錐圖
18 | Bar3DCylinderClustered      | 立體群組水平圓柱圖
19 | Bar3DCylinderStacked        | 立體堆疊水平圓柱圖
20 | Bar3DCylinderPercentStacked | 立體堆疊百分比水平圓柱圖
21 | Col                         | 二維群組柱形圖
22 | ColStacked                  | 二維堆疊柱形圖
23 | ColPercentStacked           | 二維百分比堆疊柱形圖
24 | Col3D                       | 立體柱形圖
25 | Col3DClustered              | 立體群組柱形圖
26 | Col3DStacked                | 立體堆疊柱形圖
27 | Col3DPercentStacked         | 立體百分比堆疊柱形圖
28 | Col3DCone                   | 立體圓錐圖
29 | Col3DConeClustered          | 立體群組圓錐圖
30 | Col3DConeStacked            | 立體堆疊圓錐圖
31 | Col3DConePercentStacked     | 立體百分比堆疊圓錐圖
32 | Col3DPyramid                | 立體稜錐圖
33 | Col3DPyramidClustered       | 立體群組稜錐圖
34 | Col3DPyramidStacked         | 立體堆疊稜錐圖
35 | Col3DPyramidPercentStacked  | 立體百分比堆疊稜錐圖
36 | Col3DCylinder               | 立體圓柱圖
37 | Col3DCylinderClustered      | 立體群組圓柱圖
38 | Col3DCylinderStacked        | 立體堆疊圓柱圖
39 | Col3DCylinderPercentStacked | 立體百分比堆疊圓柱圖
40 | Doughnut                    | 環圈圖
41 | Line                        | 折線圖
42 | Line3D                      | 立體折線圖
43 | Pie                         | 圓形圖
44 | Pie3D                       | 立體圓形圖
45 | PieOfPie                    | 子母圓形圖
46 | BarOfPie                    | 圓形圖帶有子橫條圖
47 | Radar                       | 雷達圖
48 | Scatter                     | 散佈圖
49 | Surface3D                   | 立體曲面圖
50 | WireframeSurface3D          | 立體曲面圖（只顯示線條）
51 | Contour                     | 曲面圖
52 | WireframeContour            | 曲面圖（俯視、只顯示線條）
53 | Bubble                      | 泡泡圖
54 | Bubble3D                    | 立體泡泡圖

在 Office Excel 中圖表資料區域 `Series` 指定了繪制哪些資料的信息集合、圖例項（系列）和水平（類別）軸標籤。

下面是 Excelize 中 `Series` 的可選參數：

參數|含義
---|---
Name|圖例項（系列），在圖表圖例和公式欄中顯示。`Name` 參數是可選的，如果不指定該值默認將會使用 `Series 1 .. n` 表示。`Name` 支持使用公式表示，例如：`Sheet1!$A$1`。
Categories|水平（類別）軸標籤。在大多數圖表類別中，`Categories` 屬性是可選的，默認為形如 `1..n` 的連續序列。
Values|圖表資料區域，是 `Series` 中最重要的參數，也是創建圖表時唯一的必選參數。該選項將圖表與其顯示的工作表資料鏈接起來。
Line|設定折線圖的折線格式。`Line` 屬性是可選的，如果未指定該屬性，則為默認樣式。可以設定的選項是 `Width`，寬度範圍是 0.25pt 至 999pt。如果 `Width` 的值超出範圍，則線的默認寬度為 2pt。
Marker|設定折線圖和散點圖的數據點標記格式。可選參數 `Size` 內置數據標記圖形的大小，其取值範圍是 2-72 (默認缺省值為 `5`)。線端類型可選參數 `Symbol` 的列舉值為(默認缺省值為 `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` 和 `auto`。

參數 `legend` 提供對圖例項的屬性設定方法，下面是 Excelize 中 `legend` 的可選參數：

參數|類別|含義
---|---|---
Position        | `string` | 圖例位置
ShowLegendKey   | `bool`   | 指定是否在數據標籤中顯示圖例項標示

其中參數 `Position` 默認值為 `right`。下面是該參數的可選值：

可選值|含義
---|---
none|關閉圖例
top|靠上
bottom|靠下
left|靠左
right|靠右
top_right|右上

其中參數 `ShowLegendKey`  默認值為 `false`。

通過可選 `Title` 對象的 `Name` 參數設定圖表標題，標題將會在圖表上方顯示。參數 `Name` 支持使用公式表示，例如 `Sheet1!$A$1`，圖表標題的默認值為空。

參數 `ShowBlanksAs` 提供「隱藏和清空儲存格」設定，默認值為：`gap` 即「空儲存格顯示為」：「空距」。下面是該參數的可選值：

值|含義
---|---
gap|空距
span|用直線連接資料點
zero|零值

通過參數 `VaryColors` 指定是否設定圖表數據系列格式為自動填滿色彩，默認值為 `true`。

參數 `Format` 提供對圖表偏移、縮放、高寬比設定和列印屬性等參數的設定，其參數與在 [`AddPicture`](image.md#AddPicture) 函數中所使用的相同。

通過可選 `PlotArea` 對象設定資料標籤格式，可選參數如下：

參數|類別|默認值|含義
---|---|---|---
ShowBubbleSize  | `bool` | `false` | 泡泡大小
ShowCatName     | `bool` | `false` | 類別名稱
ShowLeaderLines | `bool` | `false` | 顯示引導線
ShowPercent     | `bool` | `false` | 百分比
ShowSerName     | `bool` | `false` | 系列名稱
ShowVal         | `bool` | `false` | 值

通過參數 `XAxis` 和 `YAxis` 參數設定坐標軸選項。

下面是 `XAxis` 參數的可選值：

參數|類別|默認值|含義
---|---|---|---
None           | `bool`     | `false` | 隱藏坐標軸
MajorGridLines | `bool`     | `false` | 主要網格線
MinorGridLines | `bool`     | `false` | 次要網格線
TickLabelSkip  | `int`      | `1`     | 指定標籤間隔單位
ReverseOrder   | `bool`     | `false` | 逆序刻度值
Maximum        | `*float64` | `0`     | 最大值，`0` 代表自動
Minimum        | `*float64` | `0`     | 最小值，`0` 代表自動

下面是 `YAxis` 參數的可選值：

參數|類別|默認值|含義
---|---|---|---
None           | `bool`     | `false` | 隱藏坐標軸
MajorGridLines | `bool`     | `false` | 主要網格線
MinorGridLines | `bool`     | `false` | 次要網格線
MajorUnit      | `float64`  | `0`     | 坐標軸主要刻度單位，`MajorUnit` 參數為可選參數，默認值 `0` 代表為自動
ReverseOrder   | `bool`     | `false` | 逆序刻度值
Maximum        | `*float64` | `0`     | 最大值，`0` 代表自動
Minimum        | `*float64` | `0`     | 最小值，`0` 代表自動

通過可選 `Dimension` 對象設定圖表的大小，可選參數如下：

參數|類別|默認值|含義
---|---|---|---
Height | `int` | 290 | 高度
Width  | `int` | 480 | 寬度

參數 `combo` 用來指定創建組合圖表，該圖表將兩個或多個圖表類別組合在一個圖表中。例如，在 `Sheet1!$E$1:$L$15` 區域創建一個 群組柱形圖 - 折線圖：

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
        Title: excelize.ChartTitle{
            Name: "群組柱形圖 - 折線圖",
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
    // 儲存活頁簿
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 創建圖表工作表 {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

根據給定的工作表名稱和圖表樣式屬性創建圖表工作表，圖表樣式屬性的定義與 [AddChart](chart.md#AddChart) 函數相同。Excel 中的圖表工作表是僅包含圖表的工作表。

## 刪除圖表 {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

根據給定的工作表名稱和儲存格坐標刪除圖表。

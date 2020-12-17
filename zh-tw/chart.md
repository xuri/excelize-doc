# 圖表

## 添加圖表 {#AddChart}

```go
func (f *File) AddChart(sheet, cell, format string, combo ...string) error
```

根據給定的工作表名稱、儲存格坐標和圖表樣式屬性插入圖表。

下面是 Excelize 支持創建的圖表類別 `type`：

名稱|圖表類別
---|---
area                        | 二維區域圖
areaStacked                 | 二維堆疊區域圖
areaPercentStacked          | 二維百分比堆疊區域圖
area3D                      | 立體區域圖
area3DStacked               | 立體堆疊區域圖
area3DPercentStacked        | 立體百分比堆疊區域圖
bar                         | 二維群組條形圖
barStacked                  | 二維堆疊條形圖
barPercentStacked           | 二維百分比堆疊條形圖
bar3DClustered              | 立體群組條形圖
bar3DStacked                | 立體堆疊條形圖
bar3DPercentStacked         | 立體百分比堆疊條形圖
bar3DConeClustered          | 立體群組水平圓錐圖
bar3DConeStacked            | 立體堆疊水平圓錐圖
bar3DConePercentStacked     | 立體堆疊百分比水平圓錐圖
bar3DPyramidClustered       | 立體群組水平稜錐圖
bar3DPyramidStacked         | 立體堆疊水平稜錐圖
bar3DPyramidPercentStacked  | 立體堆疊百分比水平稜錐圖
bar3DCylinderClustered      | 立體群組水平圓柱圖
bar3DCylinderStacked        | 立體堆疊水平圓柱圖
bar3DCylinderPercentStacked | 立體堆疊百分比水平圓柱圖
col                         | 二維群組柱形圖
colStacked                  | 二維堆疊柱形圖
colPercentStacked           | 二維百分比堆疊柱形圖
col3D                       | 立體柱形圖
col3DClustered              | 立體群組柱形圖
col3DStacked                | 立體堆疊柱形圖
col3DPercentStacked         | 立體百分比堆疊柱形圖
col3DCone                   | 立體圓錐圖
col3DConeClustered          | 立體群組圓錐圖
col3DConeStacked            | 立體堆疊圓錐圖
col3DConePercentStacked     | 立體百分比堆疊圓錐圖
col3DPyramid                | 立體稜錐圖
col3DPyramidClustered       | 立體群組稜錐圖
col3DPyramidStacked         | 立體堆疊稜錐圖
col3DPyramidPercentStacked  | 立體百分比堆疊稜錐圖
col3DCylinder               | 立體圓柱圖
col3DCylinderClustered      | 立體群組圓柱圖
col3DCylinderStacked        | 立體堆疊圓柱圖
col3DCylinderPercentStacked | 立體百分比堆疊圓柱圖
doughnut                    | 環圈圖
line                        | 折線圖
pie                         | 圓形圖
pie3D                       | 立體圓形圖
radar                       | 雷達圖
scatter                     | 散佈圖
surface3D                   | 立體曲面圖
wireframeSurface3D          | 立體曲面圖（只顯示線條）
contour                     | 曲面圖
wireframeContour            | 曲面圖（俯視、只顯示線條）
bubble                      | 泡泡圖
bubble3D                    | 立體泡泡圖

在 Office Excel 中圖表資料區域 `series` 指定了繪制哪些資料的信息集合、圖例項（系列）和水平（分類）軸標籤。

下面是 Excelize 中 `series` 的可選參數：

參數|含義
---|---
name|圖例項（系列），在圖表圖例和公式欄中顯示。`name` 參數是可選的，如果不指定該值默認將會使用 `Series 1 .. n` 表示。`name` 支持使用公式表示，例如：`Sheet1!$A$1`。
categories|水平（分類）軸標籤。在大多數圖表類別中，`categories` 屬性是可選的，默認為形如 `1..n` 的連續序列。
values|圖表資料區域，是 `series` 中最重要的參數，也是創建圖表時唯一的必選參數。該選項將圖表與其顯示的工作表資料鏈接起來。
line|設定折線圖的折線格式。`line` 屬性是可選的，如果未指定該屬性，則為默認樣式。可以設定的選項是 `width`，寬度範圍是 0.25pt 至 999pt。如果 `width` 的值超出範圍，則線的默認寬度為 2pt。
marker|設定折線圖和散點圖數據系列線型寬度和線端類型。可選參數 `size` 指定線型寬度，其取值範圍是 2-72 (默認缺省值為 `5`)。線端類型可選參數 `symbol` 的列舉值為(默認缺省值為 `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` 和 `auto`。

參數 `legend` 提供對圖例項的屬性設定方法，下面是 Excelize 中 `legend` 的可選參數：

參數|類別|含義
---|---|---
position|string|圖例位置
show_legend_key|bool|顯示圖例，但不與圖表重疊

其中參數 `position` 默認值為 `right`，下面是可選值：

可選值|含義
---|---
top|靠上
bottom|靠下
left|靠左
right|靠右
top_right|右上

其中參數 `show_legend_key` 默認值為 `false`。

通過可選 `title` 對象的 `name` 參數設定圖表標題，標題將會在圖表上方顯示。參數 `name` 支持使用公式表示，例如 `Sheet1!$A$1`，圖表標題的默認值為空。

參數 `show_blanks_as` 提供「隱藏和清空儲存格」設定，默認值為：`gap` 即「空儲存格顯示為」：「空距」。下面是該參數的可選值：

值|含義
---|---
gap|空距
span|用直線連接資料點
zero|零值

參數 `format` 提供對圖表偏移、縮放、高寬比設定和打印屬性等參數的設定，其參數與在 [`AddPicture()`](image.md#AddPicture) 函數中所使用的相同。

通過可選 `plotarea` 對象設定資料標籤格式，可選參數如下：

參數|類別|默認值|含義
---|---|---|---
show_bubble_size|bool|`false`|泡泡大小
show_cat_name|bool|`true`|類別名稱
show_leader_lines|bool|`false`|顯示引導線
show_percent|bool|`false`|百分比
show_series_name|bool|`false`|系列名稱
show_val|bool|`false`|值

通過參數 `x_axis` 和 `y_axis` 參數設定坐標軸選項。

下面是 `x_axis` 參數的可選值：

參數|類別|默認值|含義
---|---|---|---
major_grid_lines|bool|`false`|主要網格線
minor_grid_lines|bool|`false`|次要網格線
tick_label_skip|int|`1`|指定標籤間隔單位
reverse_order|bool|`false`|逆序刻度值
maximum|int|`0`|最大值，`0` 代表自動
minimum|int|`0`|最小值，`0` 代表自動

下面是 `y_axis` 參數的可選值：

參數|類別|默認值|含義
---|---|---|---
major_grid_lines|bool|`false`|主要網格線
minor_grid_lines|bool|`false`|次要網格線
major_unit|float64|`0`|坐標軸主要刻度單位
reverse_order|bool|`false`|逆序刻度值
maximum|int|`0`|最大值，`0` 代表自動
minimum|int|`0`|最小值，`0` 代表自動

通過可選 `dimension` 對象設定圖表的大小，可選參數如下：

參數|類別|默認值|含義
---|---|---|---
height|int|290|高度
width|int|480|寬度

參數 `combo` 用來指定創建組合圖表，該圖表將兩個或多個圖表類別組合在一個圖表中。例如，在 `Sheet1!$E$1:$L$15` 區域創建一個 群組柱形圖 - 折線圖：

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
)

func main() {
    categories := map[string]string{
        "A2": "Small", "A3": "Normal", "A4": "Large", "B1": "Apple", "C1": "Orange", "D1": "Pear"}
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
            "name": "群組柱形圖 - 折線圖"
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
    // 儲存活頁簿
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 創建圖表工作表 {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, format string, combo ...string) error
```

根據給定的工作表名稱和圖表樣式屬性創建圖表工作表，圖表樣式屬性的定義與 [AddChart](chart.md#AddChart) 函數相同。Excel 中的圖表工作表是僅包含圖表的工作表。

## 刪除圖表 {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) (err error)
```

根據給定的工作表名稱和儲存格坐標刪除圖表。

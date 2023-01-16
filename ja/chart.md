# グラフ

## グラフを追加する {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

指定したワークシート名、セル座標、およびグラフスタイルのプロパティに基づいてグラフを挿入します。

次に示すのは、Excelize が作成をサポートするグラフの種類 `Type` です:

名前 | グラフの種類
---|---
area                        | 2D エリアチャート
areaStacked                 | 2D 積層型エリアチャート
areaPercentStacked          | 2D 100% 積み上げ面グラフ
area3D                      | 3D エリアチャート
area3DStacked               | 3D 積み上げ面グラフ
area3DPercentStacked        | 3D 100% 積み上げ面グラフ
bar                         | 2D クラスタ棒グラフ
barStacked                  | 2D 積み上げ棒グラフ
barPercentStacked           | 2D 100% 積み上げ棒グラフ
bar3DClustered              | 3D クラスター棒グラフ
bar3DStacked                | 3D 積み上げ棒グラフ
bar3DPercentStacked         | 3D 100% 積み上げ棒グラフ
bar3DConeClustered          | 3D 円グラフクラスタ付き棒グラフ
bar3DConeStacked            | 3D 円グラフ積み上げ棒グラフ
bar3DConePercentStacked     | 3D 100% 円グラフグラフ
bar3DPyramidClustered       | 3D ピラミッド クラスタ化棒グラフ
bar3DPyramidStacked         | 3D ピラミッド積み上げ棒グラフ
bar3DPyramidPercentStacked  | 3D 100% ピラミッド積み上げ棒グラフ
bar3DCylinderClustered      | 3D 円柱クラスタ化棒グラフ
bar3DCylinderStacked        | 3D 円柱積み上げ棒グラフ
bar3DCylinderPercentStacked | 3D 100% 円柱積み上げ棒グラフ
col                         | 2D クラスター縦棒グラフ
colStacked                  | 2D 積み上げ縦棒グラフ
colPercentStacked           | 2D 100% 積み上げ縦棒グラフ
col3D                       | 3D 縦棒グラフ
col3DClustered              | 3D クラスター縦棒グラフ
col3DStacked                | 3D 積み上げ縦棒グラフ
col3DPercentStacked         | 3D 100％ 積み上げ縦棒グラフ
col3DCone                   | 3D 円グラフグラフ
col3DConeClustered          | 3D 円グラフクラスタ化縦棒グラフ
col3DConeStacked            | 3D 円グラフ積み上げ縦棒グラフ
col3DConePercentStacked     | 3D 100% 円グラフ積み上げ縦棒グラフ
col3DPyramid                | 3D ピラミッド縦棒グラフ
col3DPyramidClustered       | 3D ピラミッド クラスタ化縦棒グラフ
col3DPyramidStacked         | 3D ピラミッド積み上げ縦棒グラフ
col3DPyramidPercentStacked  | 3D 100% ピラミッド積み上げ縦棒グラフ
col3DCylinder               | 3D 円柱縦棒グラフ
col3DCylinderClustered      | 3D 円柱クラスタ化縦棒グラフ
col3DCylinderStacked        | 3D 円柱積み上げ縦棒グラフ
col3DCylinderPercentStacked | 3D 100% 円柱積み上げ縦棒グラフ
doughnut                    | ドーナツチャート
line                        | 折れ線グラフ
pie                         | 円グラフ
pie3D                       | 3D 円グラフ
radar                       | レーダーチャート
scatter                     | 散布図
surface3D                   | 3D サーフェス チャート
wireframeSurface3D          | 3D ワイヤフレーム サーフェス チャート
contour                     | 輪郭グラフ
wireframeContour            | ワイヤフレーム輪郭グラフ
bubble                      | バブルチャート
bubble3D                    | 3D バブル チャート

Office Excel では、グラフデータ領域 `Series` は、データが描画される情報のセット、凡例專案 (系列)、および水平 (分類) 軸ラベルを指定します。

Excelize の `Series` のオプションパラメータは次のとおりです。

パラメータ | 意味
---|---
Name|凡例專案 (系列)、グラフの凡例と数式バーに表示されます。`Name` パラメータはオプションであり、`Series 1 .. n` によって表されます。`Name` は、次のような式表現の使用をサポートしています: `Sheet1!$A$1`。
Categories|水平 (カテゴリ) 軸ラベル。ほとんどの種類のグラフで，`Categories` プロパティはオプションであり、デフォルトでは `1..n` などの連続した図形のシーケンスになります。
Values|グラフのデータ領域は、`Series` で最も重要なパラメーターであり、グラフを作成するときに必要な唯一のパラメーターです。このオプションは、グラフが表示されるワークシートのデータにリンクします。
Line|これは折れ線グラフの線のフォーマットを設定します。`Line` プロパティはオプションであり、指定されない場合、デフォルトのスタイルになります。設定できるオプションは「幅」です。`Width` の範囲は 0.25pt-999pt です。`Width`の値が範囲外の場合、線のデフォルトの幅は 2pt です。
Marker|ラインチャートとスキャッターチャートのデータ系列のラインタイプ幅とラインエンドタイプを設定します。オプションのパラメータ `Size` は線種の幅を指定し、その値の範囲は2〜72です（デフォルト値は `5` です）。線種のオプションパラメータ `Symbol` の列挙値 (デフォルトは `auto`): `circle`、`dash`、`diamond`、`dot`、`none`、`picture`、`plus`、`square`、`star`、`triangle`、`x`、`auto`。

パラメータ `legend` は凡例專案のプロパティ設定メソッドを提供し、Excelize の `legend` の省略可能なパラメータは次のとおりです:

パラメータ | タイプ | 意味
---|---|---
Position        | `string` | 凡例の場所
ShowLegendKey   | `bool`   | データラベルに凡例アイテムラベルを表示するかどうかを指定します

チャートの凡例の `Position` を設定します。 デフォルトの凡例の位置は `right` です。このパラメータのオプションの値は次のとおりです:

オプション値 | 意味
---|---
none|凡例を無効にする
top|上
bottom|底
left|左
right|右
top_right|右上

ここで、パラメータ `ShowLegendKey`  のデフォルト値は `false` です。

オプションの `Title` オブジェクトの `Name` パラメータを使用してチャートタイトルを設定すると、タイトルがチャートの上に表示されます。パラメータ `Name` は、アイコンヘッダーの既定値が空であると指定されていない場合に、`Sheet1!$A$1` などの数式表現の使用をサポートします。

パラメータ `ShowBlanksAs` は、デフォルト値 `gap`、つまり「空のセルが空」として表示されている、非表示と空のセル設定を提供します。このパラメーターのオプション値は次のとおりです:

値 | 意味
---|---
gap|空距
span|データポイントを直線で接続する
zero|0 値

系列の各データ マーカーの色が `VaryColors` によって異なっていることを指定します。デフォルト値は `true` です。

パラメータ `format` は、[`AddPicture`](image.md#AddPicture) 関数で使用されるものと同じパラメータを使用して、チャートオフセット、ズーム、高さ幅比設定、印刷プロパティなどのパラメータの設定を提供します。

次のオプションパラメータを使用して、オプションの `plotarea` オブジェクトを使用してデータラベルの形式を設定します:

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
ShowBubbleSize  | `bool` | `false` | バブルサイズ
ShowCatName     | `bool` | `true`  | カテゴリ名
ShowLeaderLines | `bool` | `false` | ブートラインの表示
ShowPercent     | `bool` | `false` | 割合
ShowSerName     | `bool` | `false` | 系列名
ShowVal         | `bool` | `false` | 値

パラメータ `XAxis` と `YAxis` パラメータで軸オプションを設定します。

設定できる `XAxis` のプロパティは次のとおりです。

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
None           | `bool`     | `false` | 軸を無効にする
MajorGridLines | `bool`     | `false` | 主グリッド線を指定します
MinorGridLines | `bool`     | `false` | 副グリッド線を指定します
TickLabelSkip  | `int`      | `1`     | 描画されるラベル間でスキップする目盛りラベルの数を指定します。`TickLabelSkip` プロパティはオプションです。デフォルト値は auto です
ReverseOrder   | `bool`     | `false` | 逆シーケンススケール値
Maximum        | `*float64` | `0`     | 最大値、`0` は自動
Minimum        | `*float64` | `0`     | 最小値、`0` は自動

設定できる `YAxis` のプロパティは次のとおりです。

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
None           | `bool`     | `false` | 軸を無効にする
MajorGridLines | `bool`     | `false` | 主グリッド線を指定します
MinorGridLines | `bool`     | `false` | 副グリッド線を指定します
MajorUnit      | `float64`  | `0`     | 大目盛り間の距離を指定します。正の浮動小数点数を含める必要があります。`MajorUnit` プロパティはオプションです。デフォルト値は auto です
ReverseOrder   | `bool`     | `false` | 逆シーケンススケール値
Maximum        | `*float64` | `0`     | 最大値、`0` は自動
Minimum        | `*float64` | `0`     | 最小値、`0` は自動

次のオプションパラメーターを使用して、オプションの `Dimension` オブジェクトを使用してグラフのサイズを設定します:

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
height | `int` | 290 | 高さ
width  | `int` | 480 | 幅

パラメータ `combo` は、2つ以上のチャートタイプを1つのチャートに結合するチャートの作成を指定します。たとえば、クラスター化された列を作成します-データ `Sheet1!$E$1:$L$15` の折れ線グラフ：

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
            Name: "2D クラスター縦棒グラフ - 折れ線グラフ",
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
    // ブックを保存する
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## グラフシートを作成する {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet string, chart *ChartOptions, combo ...*ChartOptions) error
```

AddChartSheet は、指定されたグラフ形式セット（オフセット、スケール、アスペクト比の設定、印刷設定など）とプロパティセットによってグラフシートを作成するメソッドを提供します。Excelでは、グラフシートはグラフのみを含むワークシートです。

## チャートを削除 {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart は、指定されたワークシートとセル名でXLSXのグラフを削除する機能を提供します。

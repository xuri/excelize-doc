# グラフ

## グラフを追加する {#AddChart}

```go
func (f *File) AddChart(sheet, cell string, chart *ChartOptions, combo ...*ChartOptions) error
```

指定したワークシート名、セル座標、およびグラフスタイルのプロパティに基づいてグラフを挿入します。

次に示すのは、Excelize が作成をサポートするグラフの種類 `Type` です:

ID|列挙|グラフの種類
---|---|---
0  | Area                        | 2D エリアチャート
1  | AreaStacked                 | 2D 積層型エリアチャート
2  | AreaPercentStacked          | 2D 100% 積み上げ面グラフ
3  | Area3D                      | 3D エリアチャート
4  | Area3DStacked               | 3D 積み上げ面グラフ
5  | Area3DPercentStacked        | 3D 100% 積み上げ面グラフ
6  | Bar                         | 2D クラスタ棒グラフ
7  | BarStacked                  | 2D 積み上げ棒グラフ
8  | BarPercentStacked           | 2D 100% 積み上げ棒グラフ
9  | Bar3DClustered              | 3D クラスター棒グラフ
10 | Bar3DStacked                | 3D 積み上げ棒グラフ
11 | Bar3DPercentStacked         | 3D 100% 積み上げ棒グラフ
12 | Bar3DConeClustered          | 3D 円グラフクラスタ付き棒グラフ
13 | Bar3DConeStacked            | 3D 円グラフ積み上げ棒グラフ
14 | Bar3DConePercentStacked     | 3D 100% 円グラフグラフ
15 | Bar3DPyramidClustered       | 3D ピラミッド クラスタ化棒グラフ
16 | Bar3DPyramidStacked         | 3D ピラミッド積み上げ棒グラフ
17 | Bar3DPyramidPercentStacked  | 3D 100% ピラミッド積み上げ棒グラフ
18 | Bar3DCylinderClustered      | 3D 円柱クラスタ化棒グラフ
19 | Bar3DCylinderStacked        | 3D 円柱積み上げ棒グラフ
20 | Bar3DCylinderPercentStacked | 3D 100% 円柱積み上げ棒グラフ
21 | Col                         | 2D クラスター縦棒グラフ
22 | ColStacked                  | 2D 積み上げ縦棒グラフ
23 | ColPercentStacked           | 2D 100% 積み上げ縦棒グラフ
24 | Col3D                       | 3D 縦棒グラフ
25 | Col3DClustered              | 3D クラスター縦棒グラフ
26 | Col3DStacked                | 3D 積み上げ縦棒グラフ
27 | Col3DPercentStacked         | 3D 100％ 積み上げ縦棒グラフ
28 | Col3DCone                   | 3D 円グラフグラフ
29 | Col3DConeClustered          | 3D 円グラフクラスタ化縦棒グラフ
30 | Col3DConeStacked            | 3D 円グラフ積み上げ縦棒グラフ
31 | Col3DConePercentStacked     | 3D 100% 円グラフ積み上げ縦棒グラフ
32 | Col3DPyramid                | 3D ピラミッド縦棒グラフ
33 | Col3DPyramidClustered       | 3D ピラミッド クラスタ化縦棒グラフ
34 | Col3DPyramidStacked         | 3D ピラミッド積み上げ縦棒グラフ
35 | Col3DPyramidPercentStacked  | 3D 100% ピラミッド積み上げ縦棒グラフ
36 | Col3DCylinder               | 3D 円柱縦棒グラフ
37 | Col3DCylinderClustered      | 3D 円柱クラスタ化縦棒グラフ
38 | Col3DCylinderStacked        | 3D 円柱積み上げ縦棒グラフ
39 | Col3DCylinderPercentStacked | 3D 100% 円柱積み上げ縦棒グラフ
40 | Doughnut                    | ドーナツチャート
41 | Line                        | 折れ線グラフ
42 | Line3D                      | 3D 折れ線グラフ
43 | Pie                         | 円グラフ
44 | Pie3D                       | 3D 円グラフ
45 | PieOfPie                    | パイチャートのパイ
46 | BarOfPie                    | 円グラフのバー
47 | Radar                       | レーダーチャート
48 | Scatter                     | 散布図
49 | Surface3D                   | 3D サーフェス チャート
50 | WireframeSurface3D          | 3D ワイヤフレーム サーフェス チャート
51 | Contour                     | 輪郭グラフ
52 | WireframeContour            | ワイヤフレーム輪郭グラフ
53 | Bubble                      | バブルチャート
54 | Bubble3D                    | 3D バブル チャート
55 | StockHighLowClose           | 株価チャート (高値-安値-終値)
56 | StockOpenHighLowClose       | 株価チャート (始値-高値-安値-終値)

Office Excel では、グラフデータ領域 `Series` は、データが描画される情報のセット、凡例專案 (系列)、および水平 (分類) 軸ラベルを指定します。

Excelize の `Series` のオプションパラメータは次のとおりです。

パラメータ | 意味
---|---
Name              | 凡例專案 (系列)、グラフの凡例と数式バーに表示されます。`Name` パラメータはオプションであり、`Series 1 .. n` によって表されます。`Name` は、次のような式表現の使用をサポートしています: `Sheet1!$A$1`。
Categories        | 水平 (カテゴリ) 軸ラベル。ほとんどの種類のグラフで，`Categories` プロパティはオプションであり、デフォルトでは `1..n` などの連続した図形のシーケンスになります。
Values            | グラフのデータ領域は、`Series` で最も重要なパラメーターであり、グラフを作成するときに必要な唯一のパラメーターです。このオプションは、グラフが表示されるワークシートのデータにリンクします。
Fill              | これにより、データ シリーズの塗りつぶしの形式が設定されます。
Legend            | データ系列の凡例テキストのフォントを設定します。`Legend` プロパティはオプションです。
Line              | これは折れ線グラフの線のフォーマットを設定します。`Line` プロパティはオプションであり、指定されない場合、デフォルトのスタイルになります。設定できるオプションは「幅」です。`Width` の範囲は 0.25pt-999pt です。`Width`の値が範囲外の場合、線のデフォルトの幅は 2pt です。
Marker            | ラインチャートとスキャッターチャートのデータ系列のラインタイプ幅とラインエンドタイプを設定します。オプションのパラメータ `Size` は線種の幅を指定し、その値の範囲は2〜72です（デフォルト値は `5` です）。線種のオプションパラメータ `Symbol` の列挙値 (デフォルトは `auto`): `circle`、`dash`、`diamond`、`dot`、`none`、`picture`、`plus`、`square`、`star`、`triangle`、`x`、`auto`。
DataLabelPosition | これにより、グラフ シリーズのデータ ラベルの位置が設定されます。
DataPoint         | ドーナツグラフ、円グラフ、または3D円グラフ系列内の個々のデータポイントの書式を設定します。`DataPoint` プロパティはオプションです。

パラメータ `Legend` は凡例專案のプロパティ設定メソッドを提供し、Excelize の `Legend` の省略可能なパラメータは次のとおりです:

パラメータ | タイプ | 意味
---|---|---
Position      | `string` | 凡例の場所
ShowLegendKey | `bool`   | データラベルに凡例アイテムラベルを表示するかどうかを指定します
Font          | `Font`   | ラフの凡例テキストのフォントプロパティを設定します。設定できるプロパティは、セルの書式設定に使用されるフォントオブジェクトと同じです。フォントファミリー、サイズ、色、太字、斜体、下線、取り消し線などのプロパティを設定できます

チャートの凡例の `Position` を設定します。 デフォルトの凡例の位置は `right` です。このパラメータのオプションの値は次のとおりです:

オプション値 | 意味
---|---
none      | 凡例を無効にする
top       | 上
bottom    | 底
left      | 左
right     | 右
top_right | 右上

ここで、パラメータ `ShowLegendKey`  のデフォルト値は `false` です。

オプションの `Title` オブジェクトの `Name` パラメータを使用してチャートタイトルを設定すると、タイトルがチャートの上に表示されます。パラメータ `Name` は、アイコンヘッダーの既定値が空であると指定されていない場合に、`Sheet1!$A$1` などの数式表現の使用をサポートします。

パラメータ `ShowBlanksAs` は、デフォルト値 `gap`、つまり「空のセルが空」として表示されている、非表示と空のセル設定を提供します。このパラメーターのオプション値は次のとおりです:

値 | 意味
---|---
gap  | 空距
span | データポイントを直線で接続する
zero | 0 値

`Legend` プロパティを使用して、すべてのデータ系列のチャート凡例を設定します。`Legend` プロパティはオプションです。

バブル チャートまたは 3D バブル チャートのすべてのデータ系列のバブル サイズを `BubbleSizes` プロパティで設定します。`BubbleSizes` プロパティはオプションです。デフォルトの幅は `100` で、値は 0 より大きく、300 以下である必要があります。

`HoleSize` プロパティでドーナツ チャートのすべてのデータ系列のドーナツ ホール サイズを設定します。`HoleSize` プロパティはオプションです。デフォルトの幅は `75` で、値は 0 より大きく、90 以下である必要があります。

系列の各データ マーカーの色が `VaryColors` によって異なっていることを指定します。デフォルト値は `true` です。

パラメータ `Format` は、[`AddPicture`](image.md#AddPicture) 関数で使用されるものと同じパラメータを使用して、チャートオフセット、ズーム、高さ幅比設定、印刷プロパティなどのパラメータの設定を提供します。

次のオプションパラメータを使用して、オプションの `PlotArea` オブジェクトを使用してデータラベルの形式を設定します:

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
SecondPlotValues  | `int`            | `0`     | `PieOfPie` および `BarOfPie` チャートの 2 番目のプロットの値を指定します。
ShowBubbleSize    | `bool`           | `false` | バブルサイズ
ShowCatName       | `bool`           | `true`  | データラベルにカテゴリ名を表示することを指定します。`ShowCatName` プロパティはオプションです。
ShowDataTable     | `bool`           | `false` | グラフの下にデータ テーブルを追加するために使用されます。グラフの種類に応じて、面グラフ、棒グラフ、列グラフ、折れ線グラフのシリーズ タイプのグラフでのみ使用できます。
ShowDataTableKeys | `bool`           | `false` | データテーブルに凡例キーを追加するために使用されます。`ShowDataTable` が有効な場合にのみ機能します。`ShowDataTableKeys` プロパティはオプションです。
ShowLeaderLines   | `bool`           | `false` | データラベルに引き出し線を表示するかどうかを指定します。`ShowLeaderLines` プロパティはオプションです。
ShowPercent       | `bool`           | `false` | 割合
ShowSerName       | `bool`           | `false` | 系列名
ShowVal           | `bool`           | `false` | 値
Fill              | `Fill`           | N/A     | グラフの塗りつぶし色を設定します。
UpBars            | `ChartUpDownBar` | N/A     | 株価チャートの上昇バーの形式を指定します。`UpBars` プロパティはオプションです。
DownBars          | `ChartUpDownBar` | N/A     | 株価チャートの下降バーの形式を指定します。`DownBars` プロパティはオプションです。
NumFmt            | `ChartNumFmt`    | N/A     | ソースにリンクされている場合に指定し、データ ラベルのカスタム数値形式コードを設定します。`NumFmt` プロパティはオプションです。デフォルトのフォーマットコードは `General` です。

パラメータ `XAxis` と `YAxis` パラメータで軸オプションを設定します。

設定できる `XAxis` のプロパティは次のとおりです。

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
None           | `bool`          | `false` | 軸を無効にする
DropLines      | `bool`          | `false` | 2D および 3D 面グラフと折れ線グラフのドロップラインを指定します。ドロップラインは、グラフ内のデータポイントを横軸（カテゴリ軸）まで垂直に結ぶ線です。折れ線グラフや面グラフでは、各ポイントのカテゴリ位置を正確に把握しやすくするためによく使用されます。`DropLines` プロパティはオプションです
HighLowLines   | `bool`          | `false` | 2D 折れ線グラフの高低線を指定します。株価チャートではデフォルトで高低線が表示されます。高低線は各カテゴリーの最高値から最低値まで伸びています。`HighLowLines` プロパティはオプションです
MajorGridLines | `bool`          | `false` | 主グリッド線を指定します
MinorGridLines | `bool`          | `false` | 副グリッド線を指定します
TickLabelSkip  | `int`           | `1`     | 描画されるラベル間でスキップする目盛りラベルの数を指定します。`TickLabelSkip` プロパティはオプションです。デフォルト値は auto です
ReverseOrder   | `bool`          | `false` | 逆シーケンススケール値
Maximum        | `*float64`      | `0`     | 最大値、`0` は自動
Minimum        | `*float64`      | `0`     | 最小値、`0` は自動
Alignment      | `Alignment`     | N/A     | 水平軸と垂直軸の配置を指定します。設定できるフォントのプロパティは、`TextRotation` と `Vertical` です
Font           | `Font`          | N/A     | 横軸のフォントを指定します
NumFmt         | `ChartNumFmt`   | N/A     | ソースにリンクされている場合に指定し、軸のカスタム数値形式コードを設定します
Title          | `[]RichTextRun` | N/A     | グラフの主な横軸のタイトルとサイズ変更を指定します

設定できる `YAxis` のプロパティは次のとおりです。

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
None           | `bool`          | `false` | 軸を無効にする
MajorGridLines | `bool`          | `false` | 主グリッド線を指定します
MinorGridLines | `bool`          | `false` | 副グリッド線を指定します
MajorUnit      | `float64`       | `0`     | 大目盛り間の距離を指定します。正の浮動小数点数を含める必要があります。`MajorUnit` プロパティはオプションです。デフォルト値は auto です
ReverseOrder   | `bool`          | `false` | 逆シーケンススケール値
Maximum        | `*float64`      | `0`     | 最大値、`0` は自動
Minimum        | `*float64`      | `0`     | 最小値、`0` は自動
Alignment      | `Alignment`     | N/A     | 水平軸と垂直軸の配置を指定します。設定できるフォントのプロパティは、`TextRotation` と `Vertical` です
Font           | `Font`          | N/A     | 縦軸のフォントを指定します
LogBase        | `float64`       | N/A     | 縦軸の対数スケールの底番号を指定します
NumFmt         | `ChartNumFmt`   | N/A     | ソースにリンクされている場合に指定し、軸のカスタム数値形式コードを設定します
Title          | `[]RichTextRun` | N/A     | グラフの主な縦軸のタイトルとサイズ変更を指定します

-90 から 90 まで設定できる `TextRotation` の値。

設定できる `Vertical` の値は、`horz`、`vert`、`vert270`、`wordArtVert`、`eaVert`、`mongolianVert`、および `wordArtVertRtl` です。

次のオプションパラメーターを使用して、オプションの `Dimension` オブジェクトを使用してグラフのサイズを設定します:

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
Height | `uint` | 260 | 高さ
Width  | `uint` | 480 | 幅

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
                Text: "2D クラスター縦棒グラフ - 折れ線グラフ",
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

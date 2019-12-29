# グラフ

## グラフを追加する

```go
func (f *File) AddChart(sheet, cell, format string) error
```

指定したワークシート名、セル座標、およびグラフスタイルのプロパティに基づいてグラフを挿入します。

次に示すのは、Excelize が作成をサポートするグラフの種類 `type` です:


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

Office Excel では、グラフデータ領域 `series` は、データが描画される情報のセット、凡例項目 (系列)、および水平 (分類) 軸ラベルを指定します。

Excelize の `series` のオプションパラメータは次のとおりです。

パラメータ | 意味
---|---
name|凡例項目 (系列)、グラフの凡例と数式バーに表示されます。`name` パラメータはオプションであり、`Series 1 .. n` によって表されます。`name` は、次のような式表現の使用をサポートしています: `Sheet1!$A$1`。
categories|水平 (カテゴリ) 軸ラベル。 ほとんどの種類のグラフで，`categories` プロパティはオプションであり、デフォルトでは `1..n` などの連続した図形のシーケンスになります。
values|グラフのデータ領域は、`series` で最も重要なパラメーターであり、グラフを作成するときに必要な唯一のパラメーターです。 このオプションは、グラフが表示されるワークシートのデータにリンクします。
line|これは折れ線グラフの線のフォーマットを設定します。`line` プロパティはオプションであり、指定されない場合、デフォルトのスタイルになります。 設定できるオプションは「幅」です。`width` の範囲は 0.25pt-999pt です。`width`の値が範囲外の場合、線のデフォルトの幅は 2pt です。

パラメータ `legend` は凡例項目のプロパティ設定メソッドを提供し、Excelize の `legend` の省略可能なパラメータは次のとおりです:

パラメータ | タイプ | 意味
---|---|---
position|string|凡例の場所
show_legend_key|bool|凡例を表示しますが、グラフと重複しません

パラメータ `position` のデフォルト値が `right` の場合、以下はオプション値です:

オプション値 | 意味
---|---
top|上
bottom|底
left|左
right|右
top_right|右上

ここで、パラメータ `show_legend_key` のデフォルト値は `false` です。

オプションの `title` オブジェクトの `name` パラメータを使用してチャートタイトルを設定すると、タイトルがチャートの上に表示されます。 パラメータ `name` は、アイコンヘッダーの既定値が空であると指定されていない場合に、`Sheet1!$A$1` などの数式表現の使用をサポートします。

パラメータ `show_blanks_as` は、デフォルト値 `gap`、つまり「空のセルが空」として表示されている、非表示と空のセル設定を提供します。このパラメーターのオプション値は次のとおりです:

値 | 意味
---|---
gap|空距
span|データポイントを直線で接続する
zero|0 値

パラメータ `format` は、[`AddPicture()`](image.md#AddPicture) 関数で使用されるものと同じパラメータを使用して、チャートオフセット、ズーム、高さ幅比設定、印刷プロパティなどのパラメータの設定を提供します。

次のオプションパラメータを使用して、オプションの `plotarea` オブジェクトを使用してデータラベルの形式を設定します:

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
show_bubble_size|bool|`false`|バブルサイズ
show_cat_name|bool|`true`|カテゴリ名
show_leader_lines|bool|`false`|ブートラインの表示
show_percent|bool|`false`|割合
show_series_name|bool|`false`|系列名
show_val|bool|`false`|値

パラメータ `x_axis` と `y_axis` パラメータで軸オプションを設定します。

設定できる `x_axis` のプロパティは次のとおりです。

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
major_grid_lines｜bool|`false`|主グリッド線を指定します
minor_grid_lines｜bool|`false`|副グリッド線を指定します
tick_label_skip|int|`1`|描画されるラベル間でスキップする目盛りラベルの数を指定します。`tick_label_skip` プロパティはオプションです。 デフォルト値は auto です
reverse_order|bool|`false`|逆シーケンススケール値
maximum|int|`0`|最大値、`0` は自動
minimum|int|`0`|最小値、`0` は自動

設定できる `y_axis` のプロパティは次のとおりです。

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
major_grid_lines｜bool|`false`|主グリッド線を指定します
minor_grid_lines｜bool|`false`|副グリッド線を指定します
major_unit|float64|`0`|大目盛り間の距離を指定します。 正の浮動小数点数を含める必要があります。`major_unit` プロパティはオプションです。 デフォルト値は auto です
reverse_order|bool|`false`|逆シーケンススケール値
maximum|int|`0`|最大値、`0` は自動
minimum|int|`0`|最小値、`0` は自動

次のオプションパラメーターを使用して、オプションの `dimension` オブジェクトを使用してグラフのサイズを設定します:

パラメータ | タイプ | デフォルト値 | 意味
---|---|---|---
height|int|290|高さ
width|int|480|幅

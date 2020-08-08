# ツール機能

## テーブル作成 {#AddTable}

```go
func (f *File) AddTable(sheet, hcell, vcell, format string) error
```

AddTable は、ワークシート名、座標領域、および書式設定によってワークシートにテーブルを追加するメソッドを提供します。

- 例 1 では、`Sheet1` に `A1:D5` のテーブルを作成します:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="テーブルの追加"></p>

```go
err := f.AddTable("Sheet1", "A1", "D5", ``)
```

- 例 2 では、書式設定を使用して `Sheet2` に `F2:H6` のテーブルを作成します:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="書式設定を使用したテーブルの追加"></p>

```go
err := f.AddTable("Sheet2", "F2", "H6", `{
    "table_name": "table",
    "table_style": "TableStyleMedium2",
    "show_first_column": true,
    "show_last_column": true,
    "show_row_stripes": false,
    "show_column_stripes": true
}`)
```

テーブルは、ヘッダーを含む少なくとも2行でなければならないことに注意してください。 ヘッダーセルには文字列が含まれ、一意である必要があり、AddTable 関数を呼び出す前にテーブルのヘッダー行データを設定する必要があります。複数のテーブルは、交差できないエリアを調整します。

`table_name`: テーブルの同じワークシート名のテーブルの名前は一意である必要があります。

`table_style`: 組み込みのテーブル スタイル名:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

インデックス|スタイル|インデックス|スタイル|インデックス|スタイル
---|---|---|---|---|---
|<img src="../images/table_style/light/0.png" width="61">|TableStyleLight1|<img src="../images/table_style/light/1.png" width="61">|TableStyleLight2|<img src="../images/table_style/light/2.png" width="61">
TableStyleLight3|<img src="../images/table_style/light/3.png" width="61">|TableStyleLight4|<img src="../images/table_style/light/4.png" width="61">|TableStyleLight5|<img src="../images/table_style/light/5.png" width="61">
TableStyleLight6|<img src="../images/table_style/light/6.png" width="61">|TableStyleLight7|<img src="../images/table_style/light/7.png" width="61">|TableStyleLight8|<img src="../images/table_style/light/8.png" width="61">
TableStyleLight9|<img src="../images/table_style/light/9.png" width="61">|TableStyleLight10|<img src="../images/table_style/light/10.png" width="61">|TableStyleLight11|<img src="../images/table_style/light/11.png" width="61">
TableStyleLight12|<img src="../images/table_style/light/12.png" width="61">|TableStyleLight13|<img src="../images/table_style/light/13.png" width="61">|TableStyleLight14|<img src="../images/table_style/light/14.png" width="61">
TableStyleLight15|<img src="../images/table_style/light/15.png" width="61">|TableStyleLight16|<img src="../images/table_style/light/16.png" width="61">|TableStyleLight17|<img src="../images/table_style/light/17.png" width="61">
TableStyleLight18|<img src="../images/table_style/light/18.png" width="61">|TableStyleLight19|<img src="../images/table_style/light/19.png" width="61">|TableStyleLight20|<img src="../images/table_style/light/20.png" width="61">
TableStyleLight21|<img src="../images/table_style/light/21.png" width="61">|TableStyleMedium1|<img src="../images/table_style/medium/1.png" width="61">|TableStyleMedium2|<img src="../images/table_style/medium/2.png" width="61">
TableStyleMedium3|<img src="../images/table_style/medium/3.png" width="61">|TableStyleMedium4|<img src="../images/table_style/medium/4.png" width="61">|TableStyleMedium5|<img src="../images/table_style/medium/5.png" width="61">
TableStyleMedium6|<img src="../images/table_style/medium/6.png" width="61">|TableStyleMedium7|<img src="../images/table_style/medium/7.png" width="61">|TableStyleMedium8|<img src="../images/table_style/medium/8.png" width="61">
TableStyleMedium9|<img src="../images/table_style/medium/9.png" width="61">|TableStyleMedium10|<img src="../images/table_style/medium/10.png" width="61">|TableStyleMedium11|<img src="../images/table_style/medium/11.png" width="61">
TableStyleMedium12|<img src="../images/table_style/medium/12.png" width="61">|TableStyleMedium13|<img src="../images/table_style/medium/13.png" width="61">|TableStyleMedium14|<img src="../images/table_style/medium/14.png" width="61">
TableStyleMedium15|<img src="../images/table_style/medium/15.png" width="61">|TableStyleMedium16|<img src="../images/table_style/medium/16.png" width="61">|TableStyleMedium17|<img src="../images/table_style/medium/17.png" width="61">
TableStyleMedium18|<img src="../images/table_style/medium/18.png" width="61">|TableStyleMedium19|<img src="../images/table_style/medium/19.png" width="61">|TableStyleMedium20|<img src="../images/table_style/medium/20.png" width="61">
TableStyleMedium21|<img src="../images/table_style/medium/21.png" width="61">|TableStyleMedium22|<img src="../images/table_style/medium/22.png" width="61">|TableStyleMedium23|<img src="../images/table_style/medium/23.png" width="61">
TableStyleMedium24|<img src="../images/table_style/medium/24.png" width="61">|TableStyleMedium25|<img src="../images/table_style/medium/25.png" width="61">|TableStyleMedium26|<img src="../images/table_style/medium/26.png" width="61">
TableStyleMedium27|<img src="../images/table_style/medium/27.png" width="61">|TableStyleMedium28|<img src="../images/table_style/medium/28.png" width="61">|TableStyleDark1|<img src="../images/table_style/dark/1.png" width="61">
TableStyleDark2|<img src="../images/table_style/dark/2.png" width="61">|TableStyleDark3|<img src="../images/table_style/dark/3.png" width="61">|TableStyleDark4|<img src="../images/table_style/dark/4.png" width="61">
TableStyleDark5|<img src="../images/table_style/dark/5.png" width="61">|TableStyleDark6|<img src="../images/table_style/dark/6.png" width="61">|TableStyleDark7|<img src="../images/table_style/dark/7.png" width="61">
TableStyleDark8|<img src="../images/table_style/dark/8.png" width="61">|TableStyleDark9|<img src="../images/table_style/dark/9.png" width="61">|TableStyleDark10|<img src="../images/table_style/dark/10.png" width="61">
TableStyleDark11|<img src="../images/table_style/dark/11.png" width="61">||||

## 自動フィルタ {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, hcell, vcell, format string) error
```

AutoFilter は、ワークシートの名前、座標領域、および設定によってワークシートに自動フィルタを追加する方法を提供します。Excel の自動フィルタは、いくつかの単純な条件に基づいて 2D 範囲のデータをフィルター処理する方法です。

例 1, `Sheet1` のセル範囲 `A1:D4` にオートフィルタを適用します:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="自動フィルタの追加"></p>

```go
err := f.AutoFilter("Sheet1", "A1", "D4", "")
```

例 2，では、オートフィルターでデータをフィルター処理します:

```go
err := f.AutoFilter("Sheet1", "A1", "D4", `{"column":"B","expression":"x != blanks"}`)
```

`column` は、単純な条件に基づいて、自動フィルタ範囲内のフィルタ列を定義します。

フィルタ条件を指定するだけでは不十分です。また、フィルタ条件に一致しない行も非表示にする必要があります。行は、[`SetRowVisible()`](sheet.md#SetRowVisible) メットを使用して非表示になります。Excelize ではファイル形式の一部ではないため、行を自動的にフィルター処理することはできません。

列のフィルター条件を設定する:

`expression` は条件を定義し、フィルタ条件を設定するために次の演算子を使用できます:

```text
==
!=
>
<
>=
<=
and
or
```

式は、`and` 演算子と `or` 演算子で区切られた 1 つのステートメントまたは 2 つのステートメントで構成できます。例えば:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

ブランクまたは非ブランクのデータのフィルタリングは、式でブランクまたは非ブランクの値を使用して実現できます:

```text
x == Blanks
x == NonBlanks
```

Office Excel では、いくつかの単純な文字列照合操作も可能です:

```text
x == b*      // begins with b
x != b*      // doesn't begin with b
x == *b      // ends with b
x != *b      // doesn't end with b
x == *b*     // contains b
x != *b*     // doesn't contains b
```

また、任意の文字または数字を一致させるために `*` を使用し、任意の単一の文字または数字を一致させるために `?` を使用することもできます。Excel のフィルターでは、他の正規表現量量はサポートされていません。Excel の正規表現文字は `~` を使用してエスケープできます。

The placeholder variable `x` in the above examples can be replaced by any simple string. The actual placeholder name is ignored internally so the following are all equivalent:

```text
x     < 2000
col   < 2000
Price < 2000
```

## セルキャッシュをクリア {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

スプレッドシート内のリンクされた値を修正する UpdateLinkedValue は、Office Excel 2007 および 2010 では更新されません。この関数は、セルにリンクされた値を持つセルが満たされたときに値タグを削除します。リファレンス [https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating](https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating) 注意: XLSX ファイルを開くと、XlSXファイル Excel はリンクされた値を更新し、新しい値を生成し、保存ファイルをプロンプト表示されます。

ブック上のセル キャッシュをクリアすると、クリア前のセル キャッシュなど、`<v>` タグの変更として表示されます:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

セル キャッシュをクリアした後:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## セル名の分割 {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

SplitCellName は、セル名を列名と行番号に分割します。例えば:

```go
excelize.SplitCellName("AK74") // return "AK", 74, nil
```

## 結合セル名 {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

JoinCellName は、列名と行番号からセル名を結合します。

## 列名を番号に {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

ColumnNameToNumber は、Excel シートの列名を `int` に変換する関数を提供します。列名の大文字と小文字を区別しません。列名が正しくない場合、関数はエラーを返します。例えば:

```go
excelize.ColumnNameToNumber("AK") // returns 37, nil
```

## 名前の列番号 {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

ColumnNumberToName には、整数を Excel シート列タイトルに変換する関数が提供されます。例えば:

```go
excelize.ColumnNumberToName(37) // returns "AK", nil
```

## 座標に対するセル名 {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

CellNameToCoordinates は英数字のセル名を `[X, Y]` 座標に変換するか、エラーを返します。例えば:

```go
CellCoordinates("A1") // returns 1, 1, nil
CellCoordinates("Z3") // returns 26, 3, nil
```

## セル名に対する座標 {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int) (string, error)
```

CoordinatesToCellName は `[X, Y]` 座標を英数字のセル名に変換するか、エラーを返します。例えば:

```go
CoordinatesToCellName(1, 1) // returns "A1", nil
```

## 条件付き書式スタイルの作成 {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style string) (int, error)
```

NewConditionalStyle には、指定されたスタイル形式で条件付き書式のスタイルを作成する関数が提供されます。パラメータは関数 [`NewStyle()`](style.md#NewStyle) と同じです。カラー フィールドは RGB カラー コードを使用し、現在のフォント、塗りつぶし、位置合わせ、および罫線の設定のみをサポートすることに注意してください。

## 条件付き書式の設定 {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, area, formatSet string) error
```

SetConditionalFormat には、セル値の条件付き書式設定規則を作成する関数が提供されます。条件付き書式設定は Office Excel の機能で、特定の条件に基づいてセルまたはセル範囲に書式を適用できます。

`type` オプションは必須パラメーターであり、デフォルト値はありません。許容型値とその関連パラメーターは次のとおりです:

<table>
    <thead>
        <tr>
            <th>型</th>
            <th>パラメーター</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td rowspan=4>date</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>minimum</td>
        </tr>
        <tr>
            <td>maximum</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>duplicate</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>unique</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=2>top</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>criteria</td>
        </tr>
        <tr>
            <td>value</td>
        </tr>
        <tr>
            <td>blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_blanks</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td>no_errors</td>
            <td>(none)</td>
        </tr>
        <tr>
            <td rowspan=6>2_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>mid_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>mid_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>min_color</td>
        </tr>
        <tr>
            <td>mid_color</td>
        </tr>
        <tr>
            <td>max_color</td>
        </tr>
        <tr>
            <td rowspan=5>data_bar</td>
            <td>min_type</td>
        </tr>
        <tr>
            <td>max_type</td>
        </tr>
        <tr>
            <td>min_value</td>
        </tr>
        <tr>
            <td>max_value</td>
        </tr>
        <tr>
            <td>bar_color</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>criteria</td>
        </tr>
    </tbody>
</table>

`criteria` パラメータは、セルデータを評価する基準を設定するために使用されます。既定値はありません。`{"type"："cell"}` に適用される最も一般的な基準は次のとおりです:

テキスト記述文字|シンボリック表現
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

Excel のテキスト記述文字列は、上記の最初の列で使用することも、より一般的なシンボリックな代替文字列を使用することもできます。

その他の条件付き書式タイプに固有の追加の条件は、以下の関連セクションに示されています。

`value`: この値は、通常、セル データを評価するルールを設定する `criteria` パラメーターと共に使用されます:

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

`value` プロパティは、セル参照にすることもできます:

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "$C$1"
}]`, format))
```

type: `format` - `format` パラメーターは、条件付き書式基準が満たされたときにセルに適用される形式を指定するために使用されます。この形式は、セル形式と同じ方法で [`NewConditionalStyle()`](utils.md#NewConditionalStyle) メソッドを使用して作成されます:

```go
format, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9A0511"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEC7CE"],
        "pattern": 1
    }
}`)
if err != nil {
    fmt.Println(err)
}
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

注: Excel では、条件付き形式が既存のセル形式に重ね合わされ、すべてのセル形式のプロパティを変更することはできません。条件付き形式で変更できないプロパティは、フォント名、フォント サイズ、上付き文字と下付き文字、対角線の境界線、すべての配置プロパティ、およびすべての保護プロパティです。

Excel では、条件付き書式設定で使用する既定の形式がいくつか指定されています。これらは、次の excel 形式を使用してレプリケートできます:

```go
// 不適切な条件付きのローズ形式。
format1, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9A0511"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEC7CE"],
        "pattern": 1
    }
}`)

// ニュートラル条件のライトイエロー形式。
format2, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#9B5713"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#FEEAA0"],
        "pattern": 1
    }
}`)

// 良好な条件付きの薄緑色の形式。
format3, err = f.NewConditionalStyle(`{
    "font":
    {
        "color": "#09600B"
    },
    "fill":
    {
        "type": "pattern",
        "color": ["#C7EECF"],
        "pattern": 1
    }
}`)
```

type: `minimum` - `minimum` パラメーターは、`criteria` が `between` または `not between` でない場合に、より低い制限値を設定するために使用されます。

```go
// Highlight cells rules: between...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": "between",
    "format": %d,
    "minimum": "6",
    "maximum": "8"
}]`, format))
```

type: `maximum` - `maximum` パラメータは、条件が `between` または `not between` の場合に、上限制限値を設定するために使用されます。前の例を参照してください。

type: `average` - `average` タイプは、Office Excel の "平均" スタイルの条件付き形式を指定するために使用されます:

```go
// Top/Bottom rules: Above Average...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": true
}]`, format1))

// Top/Bottom rules: Below Average...
f.SetConditionalFormat("Sheet1", "B1:B10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": false
}]`, format2))
```

type: `duplicate` - `duplicate` タイプは、範囲内の重複セルを強調表示するために使用されます:

```go
// Highlight cells rules: Duplicate Values...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "duplicate",
    "criteria": "=",
    "format": %d
}]`, format))
```

type: `unique` - `unique` タイプは、範囲内の一意のセルを強調表示するために使用されます:

```go
// Highlight cells rules: Not Equal To...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "unique",
    "criteria": "=",
    "format": %d
}]`, format))
```

type: `top` - `top` 型は、範囲内の数値またはパーセンテージで上位 n 値を指定するために使用されます:

```go
// Top/Bottom rules: Top 10.
f.SetConditionalFormat("Sheet1", "H1:H10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6"
}]`, format))
```

条件は、パーセント条件が必要であることを示すために使用できます:

```go
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6",
    "percent": true
}]`, format))
```

type: `2_color_scale` - `2_color_scale` タイプは、Excel の "2 色スケール" スタイルの条件付き書式を指定するために使用されます:

```go
// Color scales: 2 color.
f.SetConditionalFormat("Sheet1", "A1:A10", `[
{
    "type": "2_color_scale",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "min_color": "#F8696B",
    "max_color": "#63BE7B"
}]`)
```

この条件付き型は、`min_type`、`max_type`、`min_value`、`max_value`、`min_color`、および `max_color` で変更できます，以下を参照してください。

type: `3_color_scale` - `3_color_scale` タイプは、Excel の "3 色スケール" スタイルの条件付き書式を指定するために使用されます:

```go
// Color scales: 3 color.
f.SetConditionalFormat("Sheet1", "A1:A10", `[
{
    "type": "3_color_scale",
    "criteria": "=",
    "min_type": "min",
    "mid_type": "percentile",
    "max_type": "max",
    "min_color": "#F8696B",
    "mid_color": "#FFEB84",
    "max_color": "#63BE7B"
}]`)
```

この条件付き型は、`min_type`、`mid_type`、`max_type`、`min_value`、`mid_value`、`max_value`、`min_color`、`mid_color` および `max_color` で変更できます，以下を参照してください。

type: `data_bar` - `data_bar` タイプは、Excel の "データ バー" スタイルの条件付き形式を指定するために使用されます:

`min_type` - 条件付き書式の種類が `2_color_scale`、`3_color_scale`、または `data_bar` の場合は、`min_type` および `max_type` プロパティを使用できます。`mid_type` は `3_color_scale` で使用できます。プロパティは次のように使用されます:

```go
// Data Bars: Gradient Fill.
f.SetConditionalFormat("Sheet1", "K1:K10", `[
{
    "type": "data_bar",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "bar_color": "#638EC6"
}]`)
```

使用可能な `min/mid/max` タイプは次のとおりです:

パラメータ|説明
---|---
min|Minimum value (for `min_type` only)
num|Numeric
percent|Percentage
percentile|Percentile
formula|Formula
max|Maximum (for `max_type` only)

`mid_type` - `3_color_scale` に使用されます。`min_type` と同じ, 上記を参照してください。

`max_type` - `min_type` と同じ, 上記を参照してください。

`min_value` - 条件付き書式の種類が `2_color_scale`、`3_color_scale` または `data_bar` の場合は、`min_value` プロパティと `max_value` プロパティを使用できます。`mid_value` は `3_color_scale` で使用できます。

`mid_value` - `3_color_scale` に使用されます。`min_value` と同じ, 上記を参照してください。

`max_value` - `min_value` と同じ, 上記を参照してください。

`min_color` - 条件付き書式の種類が `2_color_scale`、`3_color_scale`または `data_bar` の場合は、`min_color` および `max_color` プロパティを使用できます。`mid_color` は `3_color_scale` で使用できます。プロパティは次のように使用されます:

```go
// Color scales: 3 color.
f.SetConditionalFormat("Sheet1", "B1:B10", `[
{
    "type": "3_color_scale",
    "criteria": "=",
    "min_type": "min",
    "mid_type": "percentile",
    "max_type": "max",
    "min_color": "#F8696B",
    "mid_color": "#FFEB84",
    "max_color": "#63BE7B"
}]`)
```

`mid_color` - `3_color_scale` に使用されます。`min_color` と同じ, 上記を参照してください。

`max_color` - `min_color` と同じ, 上記を参照してください。

`bar_color` - `data_bar` に使用されます。`min_color` と同じ, 上記を参照してください。

## 条件付きフォーマットを削除 {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, area string) error
```

UnsetConditionalFormat は、指定されたワークシート名と範囲によって条件付き書式を設定解除する機能を提供します。

## 設定ペイン {#SetPanes}

```go
func (f *File) SetPanes(sheet, panes string)
```

SetPanes には、指定されたワークシート名とペインの書式設定によって、フリーズ ペインと分割ペインを作成および削除する機能が用意されています。

`activePane` は、アクティブなペインを定義します。この属性の可能な値は、次の表で定義されます:

列挙値|説明
---|---
bottomLeft (Bottom Left Pane) |垂直分割と水平分割の両方が適用される場合の左下ペイン。<br><br>この値は、ペインを上下の領域に分割して、水平分割のみが適用された場合にも使用されます。その場合、この値は下部ペインを指定します。
bottomRight (Bottom Right Pane) |垂直分割と水平分割の両方が適用される場合、右下のペイン。
topLeft (Top Left Pane)|垂直分割と水平分割の両方が適用される場合の左上ペイン。<br><br>この値は、ペインを上下の領域に分割して、水平分割のみが適用された場合にも使用されます。その場合、この値は上部ペインを指定します。<br><br>この値は、垂直分割のみが適用され、ペインを左右の領域に分割する場合にも使用されます。その場合、この値は左側のペインを指定します。
トップライト (右上ペイン)|垂直分割と水平分割の両方が適用される場合の右上のペイン。<br><br> この値は、垂直分割のみが適用され、ペインを左右の領域に分割する場合にも使用されます。その場合、この値は右側のペインを指定します。

ペインの状態の種類は、次の表に現在サポートされている値に制限されます:

列挙値|説明
---|---
frozen (Frozen)|ペインは凍結されますが、凍結されて分割されていませんでした。この状態では、ペインが再びフリーズ解除されると、分割されずに 1 つのペインが表示されます。<br><br>この状態では、分割バーは調整できません。
split (Split)|ペインは分割されますが、固定されません。この状態では、分割バーはユーザーが調整できます。

`x_split` - 分割の水平位置 (ポイントの1/20)。なしの場合は 0 (ゼロ) です。ペインがフリーズされている場合、この値は、上部ペインに表示される列の数を示します。

`y_split` - 分割の垂直位置、ポイントの 1/20 分の 1。なしの場合は 0 (ゼロ) です。ペインが固定されている場合、この値は左側のペインに表示される行数を示します。この属性の可能な値は、W3C XML スキーマ ダブル データ型によって定義されます。

`top_left_cell` - 右下ペインの左上の表示セルの位置 (左から右にモードの場合)。

`sqref` - 選択範囲。連続しない範囲のセットを使用できます。

例 1, `Sheet1` の列 `A` をフリーズし、アクティブセルを `Sheet1!K16` に設定します:

<p align="center"><img width="770" src="./images/setpans_01.png" alt="フリーズされた列"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": true,
    "split": false,
    "x_split": 1,
    "y_split": 0,
    "top_left_cell": "B1",
    "active_pane": "topRight",
    "panes": [
    {
        "sqref": "K16",
        "active_cell": "K16",
        "pane": "topRight"
    }]
}`)
```

例 2, `Sheet1` の行 1 - 9 をフリーズし、`Sheet1!A11:XFD11` でアクティブなセル範囲を設定します:

<p align="center"><img width="770" src="./images/setpans_02.png" alt="列をフリーズし、アクティブなセル範囲を設定する"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": true,
    "split": false,
    "x_split": 0,
    "y_split": 9,
    "top_left_cell": "A34",
    "active_pane": "bottomLeft",
    "panes": [
    {
        "sqref": "A11:XFD11",
        "active_cell": "A11",
        "pane": "bottomLeft"
    }]
}`)
```

例 3, `Sheet1` で分割ペインを作成し、アクティブセルを `Sheet1!J60` に設定します:

<p align="center"><img width="778" src="./images/setpans_03.png" alt="分割ペインの作成"></p>

```go
f.SetPanes("Sheet1", `{
    "freeze": false,
    "split": true,
    "x_split": 3270,
    "y_split": 1800,
    "top_left_cell": "N57",
    "active_pane": "bottomLeft",
    "panes": [
    {
        "sqref": "I36",
        "active_cell": "I36"
    },
    {
        "sqref": "G33",
        "active_cell": "G33",
        "pane": "topRight"
    },
    {
        "sqref": "J60",
        "active_cell": "J60",
        "pane": "bottomLeft"
    },
    {
        "sqref": "O60",
        "active_cell": "O60",
        "pane": "bottomRight"
    }]
}`)
```

例 4, `Sheet1` 上のすべてのペインのフリーズ解除と削除:

```go
f.SetPanes("Sheet1", `{"freeze":false,"split":false}`)
```

## カラー値計算 {#ThemeColor}

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor は色の値を持つ色を適用しました:

```go
package main

import (
    "fmt"
    "strings"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(getCellBgColor(f, "Sheet1", "A1"))
}

func getCellBgColor(f *excelize.File, sheet, axix string) string {
    styleID, err := f.GetCellStyle(sheet, axix)
    if err != nil {
        return err.Error()
    }
    fillID := f.Styles.CellXfs.Xf[styleID].FillID
    fgColor := f.Styles.Fills.Fill[fillID].PatternFill.FgColor
    if fgColor.Theme != nil {
        children := f.Theme.ThemeElements.ClrScheme.Children
        if *fgColor.Theme < 4 {
            dklt := map[int]string{
                0: children[1].SysClr.LastClr,
                1: children[0].SysClr.LastClr,
                2: children[3].SrgbClr.Val,
                3: children[2].SrgbClr.Val,
            }
            return strings.TrimPrefix(
                excelize.ThemeColor(dklt[*fgColor.Theme], fgColor.Tint), "FF")
        }
        srgbClr := children[*fgColor.Theme].SrgbClr.Val
        return strings.TrimPrefix(excelize.ThemeColor(srgbClr, fgColor.Tint), "FF")
    }
    return strings.TrimPrefix(fgColor.RGB, "FF")
}
```

## RGBおよびHSLカラースペースカラー値変換 {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL は、RGB トリプルを HSL トリプルに変換します。

## HSLとRGBカラースペースカラー値変換 {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB は HSL トリプルを RGB トリプルに変換します。

## ファイルライター {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer) error
```

書き込みは `io.Writer` に書き込む関数を提供します。

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer) (int64, error)
```

WriteTo は、ファイルを書き込む `io.WriterTo` を実装します。

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer は、保存されたファイルから `*bytes.Buffer` を取得する関数を提供します。

## VBA プロジェクトの追加 {#AddVBAProject}

```go
func (f *File) AddVBAProject(bin string) error
```

AddVBAProject は、関数やマクロを含む `vbaProject.bin` ファイルを追加するメソッドを提供します。ファイル拡張子は `.xlsm` である必要があります。例えば:

```go
err := f.SetSheetPrOptions("Sheet1", excelize.CodeName("Sheet1")); if err != nil {
    fmt.Println(err)
}
if err := f.AddVBAProject("vbaProject.bin"); err != nil {
    fmt.Println(err)
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
}
```

## Excel の日付を時刻に変換する {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime は、`float` ベースの Excel 日付表現を `time.Time` に変換します。

## 文字トランスコーダー {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn charsetTranscoderFn) *File
```

CharsetTranscoder 非 UTF-8 エンコーディングからオープン XLSX のユーザー定義コードページトランスコーダー関数を設定します。

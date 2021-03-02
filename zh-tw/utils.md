# 工具函數

## 創建表格 {#AddTable}

```go
func (f *File) AddTable(sheet, hcell, vcell, format string) error
```

根據給定的工作表名、儲存格坐標區域和條件式格式創建表格。

- 例1，在名為 `Sheet1` 的工作表 `A1:D5` 區域創建表格：

<p align="center"><img width="612" src="./images/addtable_01.png" alt="創建表格"></p>

```go
err := f.AddTable("Sheet1", "A1", "D5", ``)
```

- 例2，在名為 `Sheet2` 的工作表 `F2:H6` 區域創建帶有條件式格式的表格：

<p align="center"><img width="612" src="./images/addtable_02.png" alt="創建帶有條件式格式的表格"></p>

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

注意，表格坐標區域至少需要覆蓋兩列：字符型的標題列和內容列。每欄標題列的字符需保證是唯一的，並且必須在調用 AddTable 函數前設定表格的標題列資料。多個表格的坐標區域不能有交集。

可選參數 `table_name` 用以設定自定義表格名稱，同一個工作表內的表格名稱應該是唯一的。

Excelize 支持的表格樣式 `table_style` 參數：

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

索引|預覽|索引|預覽|索引|預覽
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

## 自動過濾器 {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, hcell, vcell, format string) error
```

根據給定的工作表名、儲存格坐標區域和條件式格式創建自動過濾器。Excel 中的自動過濾器可以對一些簡單的二維資料資料進列資料篩選。

例1，在名稱為 `Sheet1` 的工作表 `A1:D4` 區域創建自動過濾器：

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="創建自動過濾器"></p>

```go
err := f.AutoFilter("Sheet1", "A1", "D4", "")
```

例2，在名稱為 `Sheet1` 的工作表 `A1:D4` 區域創建帶有格式條件的自動過濾器：

```go
err := f.AutoFilter("Sheet1", "A1", "D4", `{"column":"B","expression":"x != blanks"}`)
```

參數 `column` 指定了自動過濾器在過濾範圍內的基準欄。 Excelize 暫不支持自動過濾器的計算，在設定過濾條件後，如果需要隱藏任何不符合過濾條件的列，可以使用 [`SetRowVisible()`](sheet.md#SetRowVisible) 設定列的可見性。

為欄設定過濾條件，參數 `expression` 用於指定過濾條件運算，支持下列運算符：

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

一個表達式可以包含一個或兩個由 `and` 和 `or` 運算符分隔的語句。例如：

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

可以通過在表達式中使用空白或非空白值來實現空白或非空白資料的過濾：

```text
x == Blanks
x == NonBlanks
```

Office Excel 還允許一些簡單的字符串匹配操作：

```text
x == b*      // 以 b 開始
x != b*      // 不以 b 開始
x == *b      // 以 b 結尾
x != *b      // 不以 b 結尾
x == *b*     // 包含 b
x != *b*     // 不包含 b
```

我們還可以使用 `*` 來匹配任何字符或數字，用
`?` 匹配任何單個字符或數字。除此之外，Office Excel 的自動過濾器不支持其他正則表達式的關鍵字。 Excel 的正則表達式字符可以使用 `~` 進行轉義。

上述示例中的佔位符變數 `x` 可以被任何簡單的字符串替換。實際的佔位符名稱在內部被忽略，所以以下所有表達式的效果都是等同的：

```text
x     < 2000
col   < 2000
Price < 2000
```

## 清除儲存格緩存 {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

Excel 會在儲存時將儲存帶有公式的儲存格的計算結果，這會導致在 Office Excel 2007 和 2010 中文檔在打開時，即便計算因子已經發生變化，公式的計算結果不會自動更新。參考鏈接：[https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating](https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating) 此函數會將活頁簿中所有緩存結果清除，這樣文檔在 Office Excel 中被重新打開時會自動計算新的公式結果，但是由於計算後文檔發生了變化，在關閉文檔時 Office Excel 會提示是否儲存活頁簿。

清除儲存格緩存對活頁簿的影響表現為對 `<v>` 標籤的修改，例如，清除前的儲存格緩存：

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

清除儲存格緩存後：

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## 儲存格坐標切分 {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

將工作表的儲存格坐標切分為欄名和列號。例如，將儲存格坐標 `AK74` 切分為 `AK` 和 `74`：

```go
excelize.SplitCellName("AK74") // return "AK", 74, nil
```

## 儲存格坐標組合 {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

將欄名和列號組合成工作表的儲存格坐標。

## 欄名轉索引 {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

將工作表的欄名（大小寫不敏感）轉換為索引，對於錯誤的欄名格式將傳回錯誤。例如：

```go
excelize.ColumnNameToNumber("AK") // returns 37, nil
```

## 索引轉欄名 {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

將資料類別為整型的索引轉換為欄名。例如：

```go
excelize.ColumnNumberToName(37) // returns "AK", nil
```

## 儲存格坐標轉索引 {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

將由字母和數字組合而成的儲存格坐標轉換為 `[X, Y]` 形式的列、欄索引，或傳回錯誤。例如：

```go
excelize.CellCoordinates("A1") // returns 1, 1, nil
excelize.CellCoordinates("Z3") // returns 26, 3, nil
```

## 索引轉儲存格坐標 {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int, abs ...bool) (string, error)
```

將 `[X, Y]` 形式的列、欄索引轉換為由字母和數字組合而成的儲存格坐標，或傳回錯誤。例如：

```go
excelize.CoordinatesToCellName(1, 1) // returns "A1", nil
excelize.CoordinatesToCellName(1, 1, true) // returns "$A$1", nil
```

## 創建條件式格式樣式 {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style string) (int, error)
```

通過給定樣式為條件式格式創建樣式，樣式參數與 [`NewStyle()`](style.md#NewStyle) 函數的相同。請注意，使用 RGB 色域色彩代碼時，目前僅支持設定字型、填滿、對齊和邊框的色彩。

## 設定條件式格式 {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, area, formatSet string) error
```

根據給定的工作表名稱、儲存格坐標區域和格式參數，為儲存格值創建條件式格式設定規則。條件式格式是 Office Excel 的一項功能，它允許您根據特定條件將格式應用於儲存格或一系列儲存格。

格式參數 `type` 選項是必需的參數，它沒有默認值。允許的類別值及其相關參數是：

<table>
    <thead>
        <tr>
            <th>類別</th>
            <th>參數</th>
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

`criteria` 參數用於設定儲存格資料的條件式格式運算符。它沒有默認值，同常與 `{"type"："cell"}` 一起使用，支持的參數為：

文本描述字符|符號表示
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

可以使用上面表格第一欄中的 Office Excel 文本描述字符，或者符號表示方法（`between` 與 `not between` 沒有符號表示法）作為條件式格式運算符。 下面的相關部分顯示了其他條件式格式類別的特定標準。

`value`：該值通常與 `criteria` 參數一起使用，可以用確定的值作為設定儲存格條件式格式的條件參數：

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "6"
}]`, format))
```

`value` 屬性也可以是儲存格引用：

```go
f.SetConditionalFormat("Sheet1", "D1:D10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": ">",
    "format": %d,
    "value": "$C$1"
}]`, format))
```

類別：`format` - `format` 參數用於指定滿足條件式格式標準時將應用於儲存格的格式。該參數可以通過 [`NewConditionalStyle()`](utils.md#NewConditionalStyle) 方法來創建：

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

注意：在 Office Excel 中，條件式格式疊加在現有儲存格格式上，並非所有儲存格格式屬性都可以修改。無法在條件式格式中修改的屬性包括：字型名稱、字型大小、上標和下標、對角邊框、所有對齊屬性和所有保護屬性。

Office Excel 中內置了一些與條件式格式一起使用的默認樣式。可以使用以下 excelize 設定實現這些樣式效果：

```go
// 淺紅填滿色深色文本代表較差
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

// 黃填滿色深黃色文本代表一般
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

// 綠填滿色深綠色文本代表較好
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

類別：`minimum` - 當條件式格式 `criteria` 為 `between` 或 `not between` 時，`minimum` 參數用於設定下限值。

```go
// 高亮儲存格條件式格式規則： between...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "cell",
    "criteria": "between",
    "format": %d,
    "minimum": "6",
    "maximum": "8"
}]`, format))
```

類別：`maximum` - 當條件式格式 `criteria` 為 `between` 或 `not between` 時，`maximum` 參數用於設定上限值，參考上面的例子。

類別：`average` - 平均類別用於指定 Office Excel 「最前最後規則」中「經典」樣式的「僅高於或低於平均值的數值設定格式」條件式格式：

```go
// 最前最後規則：高於平均值...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": true
}]`, format1))

// 最前最後規則：低於平均值...
f.SetConditionalFormat("Sheet1", "B1:B10", fmt.Sprintf(`[
{
    "type": "average",
    "criteria": "=",
    "format": %d,
    "above_average": false
}]`, format2))
```

類別：`duplicate` - 用於設定「突出顯示儲存格規則」中的「重復值 ...」：

```go
// 突出顯示儲存格規則: 重復值...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "duplicate",
    "criteria": "=",
    "format": %d
}]`, format))
```

類別：`unique` - 用於設定「突出顯示儲存格規則」中「只為以下內容的儲存格設定格式」的「特定文本」：

```go
// 突出顯示儲存格規則，只為以下內容的儲存格設定格式: 特定文本 不等於...
f.SetConditionalFormat("Sheet1", "A1:A10", fmt.Sprintf(`[
{
    "type": "unique",
    "criteria": "=",
    "format": %d
}]`, format))
```

類別：`top` -  用於設定「最前最後規則」中的「前 10 項...」或「前 10% ...」：

```go
// 最前最後規則： 前 10 項...
f.SetConditionalFormat("Sheet1", "H1:H10", fmt.Sprintf(`[
{
    "type": "top",
    "criteria": "=",
    "format": %d,
    "value": "6"
}]`, format))
```

設定帶有百分比條件的條件式格式：

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

類別：`2_color_scale` - 用於設定帶有「雙色刻度」的「色階樣式」條件式格式：

```go
// 色階：雙色刻度
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

雙色刻度色階條件式格式可選參數：`min_type`、`max_type`、`min_value`、`max_value`、`min_color` 和 `max_color`。

類別：`3_color_scale` - 用於設定帶有「三色刻度」的「色階樣式」條件式格式：

```go
// 色階：三色刻度
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

三色刻度色階條件式格式可選參數： `min_type`、`mid_type`、`max_type`、`min_value`、`mid_value`、`max_value`、`min_color`、`mid_color` 和 `max_color`。

類別：`data_bar` - 用於設定「資料條」類別的條件式格式。

`min_type` - 參數 `min_type` 在條件式格式類別為 `2_color_scale`、`3_color_scale` 或 `data_bar` 時可用。參數 `mid_type` 在條件式格式類別為 `3_color_scale` 時可用。例如：

```go
// 資料條：漸變填滿
f.SetConditionalFormat("Sheet1", "K1:K10", `[
{
    "type": "data_bar",
    "criteria": "=",
    "min_type": "min",
    "max_type": "max",
    "bar_color": "#638EC6"
}]`)
```

參數 `min/mid/max_types` 可選值列表:

參數|類別
---|---
min|最低值（僅用於 `min_type`）
num|數字
percent|百分比
percentile|百分點值
formula|公式
max|最高值（僅用於 `max_type`）

`mid_type` - 當條件式格式類別為 `3_color_scale` 時使用，與 `min_type` 用法相同，參考上面的表格。

`max_type` - 與 `min_type` 用法相同，參考上面的表格。

`min_value` - 參數 `min_value` 和 `max_value` 在條件式格式類別為 `2_color_scale`、`3_color_scale` 或 `data_bar` 時可用。參數 `mid_value` 在條件式格式類別為 `3_color_scale` 時可用。

`mid_value` - 在條件式格式類別為 `3_color_scale` 時可用，與 `min_value` 的用法相同，參考上述文檔。

`max_value` - 與 `min_value` 的用法相同，參考上述文檔。

`min_color` -  參數 `min_color` 和 `max_color` 在條件式格式類別為 `2_color_scale`、`3_color_scale` 或 `data_bar` 時可用。參數 `mid_color` 在條件式格式類別為 `3_color_scale` 時可用。例如：

```go
// 色階：三色刻度
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

`mid_color` - 當條件式格式類別為 `3_color_scale` 時使用。與 `min_color` 用法相同，參考上述文檔。

`max_color` - 與 `min_color` 用法相同，參考上述文檔。

`bar_color` - 當條件式格式類別為 `data_bar` 時使用。與 `min_color` 用法相同，參考上述文檔。

## 刪除條件式格式 {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, area string) error
```

根據給定的工作表名稱和儲存格坐標區域刪除條件式格式。

## 設定窗格 {#SetPanes}

```go
func (f *File) SetPanes(sheet, panes string)
```

通過給定的工作表名稱和窗格樣式參數設定凍結窗格或拆分窗格。

`activePane` 定義了活動窗格，下表為該屬性的可選值：

枚舉值|描述
---|---
bottomLeft (Bottom Left Pane) |當應用垂直和水平分割時，位於左下方的窗格。<br><br>此值也適用於僅應用了水平分割的情況，將窗格分為上下兩個區域。在這種情況下，該值指定底部窗格。
bottomRight (Bottom Right Pane) | 當垂直和水平時，位於底部右側的窗格。
topLeft (Top Left Pane)|當應用垂直和水平分割時，位於左上方的窗格。<br><br>此值也適用於僅應用了水平分割的情況，將窗格分為上下兩個區域。在這種情況下，該值指定頂部窗格。<br><br>此值也適用於僅應用垂直分割的情況，將窗格分割為右側和左側區域。在這種情況下，該值指定左側窗格。
topRight (Top Right Pane)|當應用垂直和水平分割時，位於右上方窗格。<br><br> 此值也適用於僅應用垂直分割的情況，將窗格分割為右側和左側區域。在這種情況下，該值指定右側窗格。

窗格狀態類別僅限於下表中當前列出的受支持的值：

枚舉值|描述
---|---
frozen (Frozen)|窗格被凍結，但並不分裂。在此狀態下，當窗格被解除凍結然後再次解凍時，會生成單個窗格，而不會被分割。<br><br>在這種狀態下，分割條不可調節。
split (Split)|窗格被分裂，但並不凍結。在此狀態下，用戶可以調整分割條。

`x_split` - 水平分割點的位置。如果窗格凍結，則此值用於設定頂部窗格中可見的欄數。

`y_split` - 垂直分割點的位置。如果窗格凍結，則此值用於設定左側窗格中可見的列數。該屬性的可能值由 W3C XML Schema double 資料類別定義。

`top_left_cell` - 處於「從左到右」模式時,右下方窗格中左上角可見儲存格的位置。

`sqref` - 參考儲存格坐標區域。可以是非連續的一組儲存格坐標區域。

例1，在名為 `Sheet1` 的工作表上凍結欄 `A` 並設定活動儲存格 `Sheet1!K16`：

<p align="center"><img width="770" src="./images/setpans_01.png" alt="凍結欄"></p>

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

例2，在名為 `Sheet1` 的工作表上凍結第 1 到第 9 列，並設定活動儲存格區域 `Sheet1!A11:XFD11`：

<p align="center"><img width="770" src="./images/setpans_02.png" alt="凍結欄並設定活動儲存格區域"></p>

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

例3，在名為 `Sheet1` 的工作表上創建拆分窗格，並設定活動儲存格 `Sheet1!J60`：

<p align="center"><img width="755" src="./images/setpans_03.png" alt="創建拆分窗格"></p>

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

例4，解凍並刪除名為 `Sheet1` 上的所有窗格：

```go
f.SetPanes("Sheet1", `{"freeze":false,"split":false}`)
```

## 色值計算 {#ThemeColor}

```go
func ThemeColor(baseColor string, tint float64) string
```

通過給定的 RGB 格式色值與色調參數，計算出最終色彩。例如，獲取名為 `Sheet1` 的工作表 `A1` 儲存格的背景色彩：

```go
package main

import (
    "fmt"
    "strings"

    "github.com/360EntSecGroup-Skylar/excelize/v2"
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
    fillID := *f.Styles.CellXfs.Xf[styleID].FillID
    fgColor := f.Styles.Fills.Fill[fillID].PatternFill.FgColor
    if fgColor.Theme != nil {
        children := f.Theme.ThemeElements.ClrScheme.Children
        if *fgColor.Theme < 4 {
            dklt := map[int]string{
                0: children[1].SysClr.LastClr,
                1: children[0].SysClr.LastClr,
                2: *children[3].SrgbClr.Val,
                3: *children[2].SrgbClr.Val,
            }
            return strings.TrimPrefix(
                excelize.ThemeColor(dklt[*fgColor.Theme], fgColor.Tint), "FF")
        }
        srgbClr := *children[*fgColor.Theme].SrgbClr.Val
        return strings.TrimPrefix(excelize.ThemeColor(srgbClr, fgColor.Tint), "FF")
    }
    return strings.TrimPrefix(fgColor.RGB, "FF")
}
```

## RGB與HSL色彩空間色值轉換 {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

該函數提供方法將 RGB 色彩空間三元組轉換為 HSL 色彩空間三元組。

## HSL與RGB色彩空間色值轉換 {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

該函數提供方法將 HSL 色彩空間三元組轉換為 RGB 色彩空間三元組。

## 檔案 Writer {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer) error
```

該函數提供方法將當前檔案內容寫入給定的 `io.Writer`。

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer) (int64, error)
```

該函數通過實現 `io.WriterTo` 以儲存檔案。

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

該函數提供獲取當前檔案內容 `*bytes.Buffer` 的方法。

## 嵌入 VBA 項目 {#AddVBAProject}

```go
func (f *File) AddVBAProject(bin string) error
```

該函數提供方法將包含函數和/或宏的 `vbaProject.bin` 檔案嵌入到 Excel 文檔中，檔案擴展名應為 `.xlsm`。例如:

```go
if err := f.SetSheetPrOptions("Sheet1", excelize.CodeName("Sheet1")); err != nil {
    fmt.Println(err)
}
if err := f.AddVBAProject("vbaProject.bin"); err != nil {
    fmt.Println(err)
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
}
```

## Excel 日期時間轉換 {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime 將 Excel 中以 `float` 類型表示的日期轉換為 `time.Time` 類型。

## 字符集轉碼器 {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn charsetTranscoderFn) *File
```

CharsetTranscoder 為非 UTF-8 編碼的電子錶格文檔設定用戶提供指定自定義編碼轉換器支持。

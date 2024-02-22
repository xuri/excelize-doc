# Utils

## Add table {#AddTable}

```go
func (f *File) AddTable(sheet string, table *Table) error
```

AddTable provides the method to add a table in a worksheet by given worksheet name, range reference, and format set.

- Example 1, create a table of `A1:D5` on `Sheet1`:

<p align="center"><img width="612" src="./images/addtable_01.png" alt="Add table"></p>

```go
err := f.AddTable("Sheet1", &excelize.Table{Range: "A1:D5"})
```

- Example 2, create a table of `F2:H6` on `Sheet2` with the format set:

<p align="center"><img width="612" src="./images/addtable_02.png" alt="Add table with format set"></p>

```go
disable := false
err := f.AddTable("Sheet2", &excelize.Table{
    Range:             "F2:H6",
    Name:              "table",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

Note that the table must be at least two lines including the header. The header cells must contain strings and must be unique, and must set the header row data of the table before calling the AddTable function. Multiple tables range reference that can't have an intersection.

`Name`: The name of the table, in the same worksheet name of the table, should be unique.

`StyleName`: The built-in table style names:

```text
TableStyleLight1 - TableStyleLight21
TableStyleMedium1 - TableStyleMedium28
TableStyleDark1 - TableStyleDark11
```

Index|Style|Index|Style|Index|Style
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

## Get tables {#GetTables}

```go
func (f *File) GetTables(sheet string) ([]Table, error)
```

GetTables provides the method to get all tables in a worksheet by given worksheet name.

## Delete table {#DeleteTable}

```go
func (f *File) DeleteTable(name string) error
```

DeleteTable provides the method to delete table by given table name.

## Auto filter {#AutoFilter}

```go
func (f *File) AutoFilter(sheet, rangeRef string, opts []AutoFilterOptions) error
```

AutoFilter provides the method to add an auto filter in a worksheet by given worksheet name, range reference, and settings. An auto filter in Excel is a way of filtering a 2D range of data based on some simple criteria.

Example 1, applying an auto filter to a cell range `A1:D4` in the `Sheet1`:

<p align="center"><img width="612" src="./images/autofilter_01.png" alt="Add auto filter"></p>

```go
err := f.AutoFilter("Sheet1", "A1:D4", []excelize.AutoFilterOptions{})
```

Example 2, filter data in an auto filter:

```go
err := f.AutoFilter("Sheet1", "A1:D4", []excelize.AutoFilterOptions{
    {Column: "B", Expression: "x != blanks"},
})
```

`Column` defines the filter columns in an auto filter range based on simple criteria.

It isn't sufficient to just specify the filter condition. You must also hide any rows that don't match the filter condition. Rows are hidden using the [`SetRowVisible()`](sheet.md#SetRowVisible) method. Excelize can't filter rows automatically since this isn't part of the file format.

Setting filter criteria for a column:

`Expression` defines the conditions, the following operators are available for setting the filter criteria:

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

An expression can comprise a single statement or two statements separated by the `and` and `or` operators. For example:

```text
x <  2000
x >  2000
x == 2000
x >  2000 and x <  5000
x == 2000 or  x == 5000
```

Filtering of blank or non-blank data can be achieved by using a value of Blanks or NonBlanks in the expression:

```text
x == Blanks
x == NonBlanks
```

Office Excel also allows some simple string matching operations:

```text
x == b*      // begins with b
x != b*      // doesn't begin with b
x == *b      // ends with b
x != *b      // doesn't end with b
x == *b*     // contains b
x != *b*     // doesn't contains b
```

You can also use `*` to match any character or number and `?` to match any single character or number. No other regular expression quantifier is supported by Excel's filters. Excel's regular expression characters can be escaped using `~`.

The placeholder variable `x` in the above examples can be replaced by any simple string. The actual placeholder name is ignored internally so the following are all equivalent:

```text
x     < 2000
col   < 2000
Price < 2000
```

## Update linked value {#UpdateLinkedValue}

```go
func (f *File) UpdateLinkedValue() error
```

UpdateLinkedValue fix linked values within a spreadsheet are not updating in Office Excel 2007 and 2010. This function will remove the value tag when met a cell have a linked value. Reference [https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating](https://social.technet.microsoft.com/Forums/office/en-US/e16bae1f-6a2c-4325-8013-e989a3479066/excel-2010-linked-cells-not-updating) Notice: after open the spreadsheet file Excel will be updating the linked value and generate a new value and will prompt the save file or not.

The effect of clearing the cell cache on the workbook appears as a modification to the `<v>` tag, for example, the cell cache before clearing:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
        <v>100</v>
     </c>
</row>
```

After clearing the cell cache:

```xml
<row r="19" spans="2:2">
    <c r="B19">
        <f>SUM(Sheet2!D2,Sheet2!D11)</f>
    </c>
</row>
```

## Split Cell Name {#SplitCellName}

```go
func SplitCellName(cell string) (string, int, error)
```

SplitCellName splits cell name to column name and row number. For example:

```go
excelize.SplitCellName("AK74") // return "AK", 74, nil
```

## Join Cell Name {#JoinCellName}

```go
func JoinCellName(col string, row int) (string, error)
```

JoinCellName joins cell name from column name and row number.

## Column Name To Number {#ColumnNameToNumber}

```go
func ColumnNameToNumber(name string) (int, error)
```

ColumnNameToNumber provides a function to convert Excel sheet column name to `int`. Column name case insensitive. The function returns an error if the column name incorrect. For example:

```go
excelize.ColumnNameToNumber("AK") // returns 37, nil
```

## Column Number To Name {#ColumnNumberToName}

```go
func ColumnNumberToName(num int) (string, error)
```

ColumnNumberToName provides a function to convert the integer to Excel sheet column title. For example:

```go
excelize.ColumnNumberToName(37) // returns "AK", nil
```

## Cell Name To Coordinates {#CellNameToCoordinates}

```go
func CellNameToCoordinates(cell string) (int, int, error)
```

CellNameToCoordinates converts alphanumeric cell name to `[X, Y]` coordinates or returns an error. For example:

```go
excelize.CellNameToCoordinates("A1") // returns 1, 1, nil
excelize.CellNameToCoordinates("Z3") // returns 26, 3, nil
```

## Coordinates To Cell Name {#CoordinatesToCellName}

```go
func CoordinatesToCellName(col, row int, abs ...bool) (string, error)
```

CoordinatesToCellName converts `[X, Y]` coordinates to alpha-numeric cell name or returns an error. For example:

```go
excelize.CoordinatesToCellName(1, 1) // returns "A1", nil
excelize.CoordinatesToCellName(1, 1, true) // returns "$A$1", nil
```

## Create conditional style {#NewConditionalStyle}

```go
func (f *File) NewConditionalStyle(style *Style) (int, error)
```

NewConditionalStyle provides a function to create a style for the conditional format by given style format. The parameters are the same with the [`NewStyle`](style.md#NewStyle) function. Note that the color field uses RGB color code and only supports setting the font, fills, alignment, and borders currently.

## Get conditional style {#GetConditionalStyle}

```go
func (f *File) GetConditionalStyle(idx int) (*Style, error)
```

GetConditionalStyle returns conditional format style definition by specified style index.

## Set conditional format {#SetConditionalFormat}

```go
func (f *File) SetConditionalFormat(sheet, rangeRef string, opts []ConditionalFormatOptions) error
```

SetConditionalFormat provides a function to create a conditional formatting rule for cell value. Conditional formatting is a feature of Office Excel which allows you to apply a format to a cell or a range of cells based on certain criteria.

The `Type` option is a required parameter and it has no default value. Allowable type values and their associated parameters are:

<table>
    <thead>
        <tr>
            <th>Type</th>
            <th>Parameters</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=4>cell</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>time_period</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td rowspan=2>text</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td>average</td>
            <td>Criteria</td>
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
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
        </tr>
        <tr>
            <td rowspan=2>bottom</td>
            <td>Criteria</td>
        </tr>
        <tr>
            <td>Value</td>
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
            <td>MinType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>MinColor</td>
        </tr>
        <tr>
            <td>MaxColor</td>
        </tr>
        <tr>
            <td rowspan=9>3_color_scale</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MidType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MidValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>MinColor</td>
        </tr>
        <tr>
            <td>MidColor</td>
        </tr>
        <tr>
            <td>MaxColor</td>
        </tr>
        <tr>
            <td rowspan=9>data_bar</td>
            <td>MinType</td>
        </tr>
        <tr>
            <td>MaxType</td>
        </tr>
        <tr>
            <td>MinValue</td>
        </tr>
        <tr>
            <td>MaxValue</td>
        </tr>
        <tr>
            <td>BarBorderColor</td>
        </tr>
        <tr>
            <td>BarColor</td>
        </tr>
        <tr>
            <td>BarDirection</td>
        </tr>
        <tr>
            <td>BarOnly</td>
        </tr>
        <tr>
            <td>BarSolid</td>
        </tr>
        <tr>
            <td rowspan=3>iconSet</td>
            <td>IconStyle</td>
        </tr>
        <tr>
            <td>ReverseIcons</td>
        </tr>
        <tr>
            <td>IconsOnly</td>
        </tr>
        <tr>
            <td>formula</td>
            <td>Criteria</td>
        </tr>
    </tbody>
</table>

The `Criteria` parameter is used to set the criteria by which the cell data will be evaluated. It has no default value. The most common criteria as applied to `excelize.ConditionalFormatOptions{Type: "cell"}` are:

Text description character|Symbolic representation
---|---
between|
not between|
equal to|==
not equal to|!=
greater than|>
less than|<
greater than or equal to|>=
less than or equal to|<=

You can either use Excel's textual description strings, in the first column above, or the more common symbolic alternatives.

Additional criteria that are specific to other conditional format types are shown in the relevant sections below.

`Value`: The value is generally used along with the `Criteria` parameter to set the rule by which the cell data will be evaluated:

```go
err := f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: ">",
            Format:   format,
            Value:    "6",
        },
    },
)
```

The `Value` property can also be a cell reference:

```go
err := f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: ">",
            Format:   format,
            Value:    "$C$1",
        },
    },
)
```

type: `Format` - The `Format` parameter is used to specify the format that will be applied to the cell when the conditional formatting criterion is met. The format is created using the [`NewConditionalStyle()`](utils.md#NewConditionalStyle) method in the same way as cell formats:

```go
format, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9A0511"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEC7CE"}, Pattern: 1,
        },
    },
)
if err != nil {
    fmt.Println(err)
}
err = f.SetConditionalFormat("Sheet1", "D1:D10",
    []excelize.ConditionalFormatOptions{
        {Type: "cell", Criteria: ">", Format: format, Value: "6"},
    },
)
```

Note: In Excel, a conditional format is superimposed over the existing cell format and not all cell format properties can be modified. Properties that cannot be modified in a conditional format are font name, font size, superscript and subscript, diagonal borders, all alignment properties and all protection properties.

Excel specifies some default formats to be used with conditional formatting. These can be replicated using the following excelize formats:

```go
// Rose format for bad conditional.
format1, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9A0511"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEC7CE"}, Pattern: 1,
        },
    },
)

// Light yellow format for neutral conditional.
format2, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "9B5713"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"FEEAA0"}, Pattern: 1,
        },
    },
)

// Light green format for good conditional.
format3, err := f.NewConditionalStyle(
    &excelize.Style{
        Font: &excelize.Font{Color: "09600B"},
        Fill: excelize.Fill{
            Type: "pattern", Color: []string{"C7EECF"}, Pattern: 1,
        },
    },
)
```

type: `MinValue` - The `MinValue` parameter is used to set the lower limiting value when the `Criteria` is either `between` or `not between`.

```go
// Highlight cells rule: between...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "cell",
            Criteria: "between",
            Format:   format,
            MinValue: "6",
            MaxValue: "8",
        },
    },
)
```

type: `MaxValue` - The `maximum` parameter is used to set the upper limiting value when the criteria are either `between` or `not between`. See the previous example.

type: `average` - The `average` type is used to specify Office Excel's "Average" style conditional format:

```go
// Top/Bottom rules: Above Average...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:         "average",
            Criteria:     "=",
            Format:       format1,
            AboveAverage: true,
        },
    },
)

// Top/Bottom rules: Below Average...
err := f.SetConditionalFormat("Sheet1", "B1:B10",
    []excelize.ConditionalFormatOptions{
        {
            Type:         "average",
            Criteria:     "=",
            Format:       format2,
            AboveAverage: false,
        },
    },
)
```

type: `duplicate` - The `duplicate` type is used to highlight duplicate cells in a range:

```go
// Highlight cells rules: Duplicate Values...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {Type: "duplicate", Criteria: "=", Format: format},
    },
)
```

type: `unique` - The `unique` type is used to highlight unique cells in a range:

```go
// Highlight cells rules: Not Equal To...
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {Type: "unique", Criteria: "=", Format: format},
    },
)
```

type: `top` - The `top` type is used to specify the top n values by number or percentage in a range:

```go
// Top/Bottom rules: Top 10.
err := f.SetConditionalFormat("Sheet1", "H1:H10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "top",
            Criteria: "=",
            Format:   format,
            Value:    "6",
        },
    },
)
```

The criteria can be used to indicate that a percentage condition is required:

```go
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "top",
            Criteria: "=",
            Format:   format,
            Value:    "6",
            Percent:  true,
        },
    },
)
```

type: `2_color_scale` - The `2_color_scale` type is used to specify Excel's "2 Color Scale" style conditional format:

```go
// Color scales: 2 color.
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "2_color_scale",
            Criteria: "=",
            MinType:  "min",
            MaxType:  "max",
            MinColor: "#F8696B",
            MaxColor: "#63BE7B",
        },
    },
)
```

This conditional type can be modified with `MinType`, `MaxType`, `MinValue`, `MaxValue`, `MinColor` and `MaxColor`, see below.

type: `3_color_scale` - The `3_color_scale` type is used to specify Excel's "3 Color Scale" style conditional format:

```go
// Color scales: 3 color.
err := f.SetConditionalFormat("Sheet1", "A1:A10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "3_color_scale",
            Criteria: "=",
            MinType:  "min",
            MidType:  "percentile",
            MaxType:  "max",
            MinColor: "#F8696B",
            MidColor: "#FFEB84",
            MaxColor: "#63BE7B",
        },
    },
)
```

This conditional type can be modified with `MinType`, `MidType`, `MaxType`, `MinValue`, `MidValue`, `MaxValue`, `MinColor`, `MidColor` and `MaxColor`, see below.

type: `data_bar` - The `data_bar` type is used to specify Excel's "Data Bar" style conditional format.

`MinType` - The `MinType` and `MaxType` properties are available when the conditional formatting type is `2_color_scale`, `3_color_scale` or `data_bar`. The `MidType` is available for `3_color_scale`. The properties are used as follows:

```go
// Data Bars: Gradient Fill.
err := f.SetConditionalFormat("Sheet1", "K1:K10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "data_bar",
            Criteria: "=",
            MinType:  "min",
            MaxType:  "max",
            BarColor: "#638EC6",
        },
    },
)
```

The available `min/mid/max` types are:

Parameter|Explanation
---|---
min|MinValue value (for `MinType` only)
num|Numeric
percent|Percentage
percentile|Percentile
formula|Formula
max|MaxValue (for `MaxType` only)

`MidType` - Used for `3_color_scale`. Same as `MinType`, see above.

`MaxType` - Same as `MinType`, see above.

`MinValue` - The `MinValue` and `MaxValue` properties are available when the conditional formatting type is `2_color_scale`, `3_color_scale` or `data_bar`. The `MidValue` is available for `3_color_scale`.

`MidValue` - Used for `3_color_scale`. Same as `MinValue`, see above.

`MaxValue` - Same as `MinValue`, see above.

`MinColor` - The `MinColor` and `MaxValue` properties are available when the conditional formatting type is `2_color_scale`, `3_color_scale` or `data_bar`. The `MidColor` is available for `3_color_scale`. The properties are used as follows:

```go
// Color scales: 3 color.
err := f.SetConditionalFormat("Sheet1", "B1:B10",
    []excelize.ConditionalFormatOptions{
        {
            Type:     "3_color_scale",
            Criteria: "=",
            MinType:  "min",
            MidType:  "percentile",
            MaxType:  "max",
            MinColor: "#F8696B",
            MidColor: "#FFEB84",
            MaxColor: "#63BE7B",
        },
    },
)
```

`MidColor` - Used for `3_color_scale`. Same as `MinColor`, see above.

`MaxColor` - Same as `MinColor`, see above.

`BarColor` - Used for `data_bar`. Same as `MinColor`, see above.

`BarBorderColor` - Used for sets the color for the border line of a data bar, this is only visible in Excel 2010 and later.

`BarDirection` - Used for sets the direction for data bars. The available options are:

Value|Explanation
---|---
context     | Data bar direction is set by spreadsheet application based on the context of the data displayed.
leftToRight | Data bar direction is from right to left.
rightToLeft | Data bar direction is from left to right.

`BarOnly` - Used for set displays a bar data but not the data in the cells.

`BarSolid` - Used for turns on a solid (non-gradient) fill for data bars, this is only visible in Excel 2010 and later.

`IconStyle` - The available options are:

|Value|
|---|
|3Arrows        |
|3ArrowsGray    |
|3Flags         |
|3Signs         |
|3Symbols       |
|3Symbols2      |
|3TrafficLights1|
|3TrafficLights2|
|4Arrows        |
|4ArrowsGray    |
|4Rating        |
|4RedToBlack    |
|4TrafficLights |
|5Arrows        |
|5ArrowsGray    |
|5Quarters      |
|5Rating        |

`ReverseIcons` - Used for set reversed icons sets.

`IconsOnly` - Used for set displayed without the cell value.

`StopIfTrue` - Used to set the "stop if true" feature of a conditional formatting rule when more than one rule is applied to a cell or a range of cells. When this parameter is set then subsequent rules are not evaluated if the current rule is true.

For example, highlight highest and lowest values in a range of cells `A1:D4` by set conditional formatting on `Sheet1`:

<p align="center"><img width="885" src="./images/condition_format_01.png" alt="Set conditional formatting in a range of cells"></p>

```go
func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    for r := 1; r <= 4; r++ {
        row := []int{
            rand.Intn(100), rand.Intn(100), rand.Intn(100), rand.Intn(100),
        }
        if err := f.SetSheetRow("Sheet1", fmt.Sprintf("A%d", r), &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    red, err := f.NewConditionalStyle(
        &excelize.Style{
            Font: &excelize.Font{
                Color: "9A0511",
            },
            Fill: excelize.Fill{
                Type:    "pattern",
                Color:   []string{"FEC7CE"},
                Pattern: 1,
            },
        },
    )
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4",
        []excelize.ConditionalFormatOptions{
            {
                Type:     "bottom",
                Criteria: "=",
                Value:    "1",
                Format:   red,
            },
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    green, err := f.NewConditionalStyle(
        &excelize.Style{
            Font: &excelize.Font{
                Color: "09600B",
            },
            Fill: excelize.Fill{
                Type:    "pattern",
                Color:   []string{"C7EECF"},
                Pattern: 1,
            },
        },
    )
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SetConditionalFormat("Sheet1", "A1:D4",
        []excelize.ConditionalFormatOptions{
            {
                Type:     "top",
                Criteria: "=",
                Value:    "1",
                Format:   green,
            },
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
        return
    }
}
```

## Get conditional format {#GetConditionalFormats}

```go
func (f *File) GetConditionalFormats(sheet string) (map[string][]ConditionalFormatOptions, error)
```

GetConditionalFormats returns conditional format settings by given worksheet name.

## Remove conditional format {#UnsetConditionalFormat}

```go
func (f *File) UnsetConditionalFormat(sheet, rangeRef string) error
```

UnsetConditionalFormat provides a function to unset the conditional format by given worksheet name and range reference.

## Set panes {#SetPanes}

```go
func (f *File) SetPanes(sheet string, panes *Panes) error
```

SetPanes provides a function to create and remove freeze panes and split panes by given worksheet name and panes format set.

`ActivePane` defines the pane that is active. The possible values for this attribute are defined in the following table:

Enumeration Value|Description
---|---
bottomLeft (Bottom Left Pane) |Bottom left pane, when both vertical and horizontal splits are applied.<br><br>This value is also used when only a horizontal split has been applied, dividing the pane into upper and lower regions. In that case, this value specifies the bottom pane.
bottomRight (Bottom Right Pane) | Bottom right pane, when both vertical and horizontal splits are applied.
topLeft (Top Left Pane)|Top left pane, when both vertical and horizontal splits are applied.<br><br>This value is also used when only a horizontal split has been applied, dividing the pane into upper and lower regions. In that case, this value specifies the top pane.<br><br>This value is also used when only a vertical split has been applied, dividing the pane into right and left regions. In that case, this value specifies the left pane.
topRight (Top Right Pane)|Top right pane, when both vertical and horizontal splits are applied.<br><br> This value is also used when only a vertical split has been applied, dividing the pane into right and left regions. In that case, this value specifies the right pane.

Pane state type is restricted to the values supported currently listed in the following table:

Enumeration Value|Description
---|---
frozen (Frozen)|Panes are frozen, but were not split being frozen. In this state, when the panes are unfrozen again, a single pane results, with no split.<br><br>In this state, the split bars are not adjustable.
split (Split)|Panes are split, but not frozen. In this state, the split bars are adjustable by the user.

`XSplit` - Horizontal position of the split, in 1/20th of a point; 0 (zero) if none. If the pane is frozen, this value indicates the number of columns visible in the top pane.

`YSplit` - Vertical position of the split, in 1/20th of a point; 0 (zero) if none. If the pane is frozen, this value indicates the number of rows visible in the left pane. The possible values for this attribute are defined by the W3C XML Schema double data type.

`TopLeftCell` - Location of the top left visible cell in the bottom right pane (when in Left-To-Right mode).

`SQRef` - Range of the selection. Can be a non-contiguous set of ranges.

Example 1: freeze column `A` in the `Sheet1` and set the active cell on `Sheet1!K16`:

<p align="center"><img width="770" src="./images/setpans_01.png" alt="Frozen column"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Freeze:      true,
    XSplit:      1,
    TopLeftCell: "B1",
    ActivePane:  "topRight",
    Selection: []excelize.Selection{
        {SQRef: "K16", ActiveCell: "K16", Pane: "topRight"},
    },
})
```

Example 2: freeze rows 1 to 9 in the `Sheet1` and set the active cell ranges on `Sheet1!A11:XFD11`:

<p align="center"><img width="770" src="./images/setpans_02.png" alt="Freeze columns and set active cell ranges"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Freeze:      true,
    YSplit:      9,
    TopLeftCell: "A34",
    ActivePane:  "bottomLeft",
    Selection: []excelize.Selection{
        {SQRef: "A11:XFD11", ActiveCell: "A11", Pane: "bottomLeft"},
    },
})
```

Example 3: create split panes in the `Sheet1` and set the active cell on `Sheet1!J60`:

<p align="center"><img width="775" src="./images/setpans_03.png" alt="Create split panes"></p>

```go
err := f.SetPanes("Sheet1", &excelize.Panes{
    Split:       true,
    XSplit:      3270,
    YSplit:      1800,
    TopLeftCell: "N57",
    ActivePane:  "bottomLeft",
    Selection: []excelize.Selection{
        {SQRef: "I36", ActiveCell: "I36"},
        {SQRef: "G33", ActiveCell: "G33", Pane: "topRight"},
        {SQRef: "J60", ActiveCell: "J60", Pane: "bottomLeft"},
        {SQRef: "O60", ActiveCell: "O60", Pane: "bottomRight"},
    },
})
```

Example 4, unfreeze and remove all panes on `Sheet1`:

```go
err := f.SetPanes("Sheet1", &excelize.Panes{Freeze: false, Split: false})
```

## Get panes {#GetPanes}

```go
func (f *File) GetPanes(sheet string) (Panes, error)
```

GetPanes provides a function to get freeze panes, split panes, and worksheet views by given worksheet name.

## Color {#ThemeColor}

```go
func (f *File) GetBaseColor(hexColor string, indexedColor int, themeColor *int) string
```

GetBaseColor returns the preferred hex color code by giving hex color code, indexed color, and theme color.

```go
func ThemeColor(baseColor string, tint float64) string
```

ThemeColor applied the color with tint value.

There 3 kinds of colors for the text in the spreadsheet: hex color, indexed color, and theme color. The priority of these colors is hex color takes precedence over theme color, and the theme color takes precedence over indexed color. In addition, the color also supports applying tint value based on the hex color, so we need to use the ThemeColor function to apply the tint for the based color to get the calculated hex color value. For example:

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    runs, err := f.GetCellRichText("Sheet1", "A1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, run := range runs {
        var hexColor string
        if run.Font != nil {
            baseColor := f.GetBaseColor(run.Font.Color, run.Font.ColorIndexed, run.Font.ColorTheme)
            hexColor = strings.TrimPrefix(excelize.ThemeColor(baseColor, run.Font.ColorTint), "FF")
        }
        fmt.Printf("text: %s, color: %s\r\n", run.Text, hexColor)
    }
}
```

## Convert RGB to HSL {#RGBToHSL}

```go
func RGBToHSL(r, g, b uint8) (h, s, l float64)
```

RGBToHSL converts an RGB triple to a HSL triple.

## Convert HSL to RGB {#HSLToRGB}

```go
func HSLToRGB(h, s, l float64) (r, g, b uint8)
```

HSLToRGB converts an HSL triple to a RGB triple.

## File Writer {#FileWriter}

### Write {#Write}

```go
func (f *File) Write(w io.Writer, opts ...Options) error
```

Write provides a function to write to an `io.Writer`.

### WriteTo {#WriteTo}

```go
func (f *File) WriteTo(w io.Writer, opts ...Options) (int64, error)
```

WriteTo implements `io.WriterTo` to write the file.

### WriteToBuffer {#WriteToBuffer}

```go
func (f *File) WriteToBuffer() (*bytes.Buffer, error)
```

WriteToBuffer provides a function to get `*bytes.Buffer` from the saved file.

## Add VBA Project {#AddVBAProject}

```go
func (f *File) AddVBAProject(file []byte) error
```

AddVBAProject provides the method to add `vbaProject.bin` file which contains functions and/or macros. The file extension should be `.xlsm` or `.xltm`. For example:

```go
codeName := "Sheet1"
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    CodeName: &codeName,
}); err != nil {
    fmt.Println(err)
    return
}
file, err := os.ReadFile("vbaProject.bin")
if err != nil {
    fmt.Println(err)
    return
}
if err := f.AddVBAProject(file); err != nil {
    fmt.Println(err)
    return
}
if err := f.SaveAs("macros.xlsm"); err != nil {
    fmt.Println(err)
    return
}
```

## Excel date to time {#ExcelDateToTime}

```go
func ExcelDateToTime(excelDate float64, use1904Format bool) (time.Time, error)
```

ExcelDateToTime converts a float-based excel date representation to a `time.Time`.

## Charset transcoder {#CharsetTranscoder}

```go
func (f *File) CharsetTranscoder(fn charsetTranscoderFn) *File
```

CharsetTranscoder set user-defined codepage transcoder function for open the spreadsheet from non-UTF-8 encoding.

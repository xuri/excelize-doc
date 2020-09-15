# ピボットテーブル {#PivotTable}

ピボットテーブルは、より広範なテーブル（データベース、スプレッドシート、ビジネスインテリジェンスプログラムなど）のデータを要約した統計のテーブルです。 このサマリーには、合計、平均、またはその他の統計が含まれる場合があります。これらの統計は、ピボットテーブルによって意味のある方法でグループ化されます。

PivotTableOption は、ピボットテーブルの形式設定を直接マップします。

```go
type PivotTableOption struct {
    DataRange           string
    PivotTableRange     string
    Rows                []PivotTableField
    Columns             []PivotTableField
    Data                []PivotTableField
    Filter              []PivotTableField
    RowGrandTotals      bool
    ColGrandTotals      bool
    ShowDrill           bool
    UseAutoFormatting   bool
    PageOverThenDown    bool
    MergeItem           bool
    CompactData         bool
    ShowRowHeaders      bool
    ShowColHeaders      bool
    ShowRowStripes      bool
    ShowColStripes      bool
    ShowLastColumn      bool
    PivotTableStyleName string
}
```

PivotTableField は、ピボットテーブルのフィールド設定を直接マップします。

```go
type PivotTableField struct {
    Data            string
    Name            string
    Subtotal        string
    DefaultSubtotal bool
}
```

Subtotal は、このデータフィールドに適用される集計関数を指定します。 デフォルト値は `Sum` です。 この属性に指定できる値は次のとおりです。

|オプション値|
|---|
|Average|
|Count|
|CountNums|
|Max|
|Min|
|Product|
|StdDev|
|StdDevp|
|Sum|
|Var|
|Varp|

Name は、データフィールドの名前を指定します。 データフィールド名には最大 `255` 文字を使用できますが、余分な文字は切り捨てられます。

## ピボットテーブルを作成する {#AddPivotTable}

```go
func (f *File) AddPivotTable(opt *PivotTableOption) error
```

AddPivotTable は、指定されたピボットテーブルオプションによってピボットテーブルを追加するメソッドを提供します。

たとえば、`Sheet1!$G$2:$M$34` 領域にピボットテーブルを作成し、データソースとして地域 `Sheet1!$A$1:$E$31` を使用し、売上の合計で集計します。

<p align="center"><img width="1117" src="./images/pivot_table_01.png" alt="Go を使用して excelize でピボットテーブルを作成する"></p>

```go
package main

import (
    "fmt"
    "math/rand"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    // シートにデータを作成する
    month := []string{"Jan", "Feb", "Mar", "Apr", "May",
        "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"}
    year := []int{2017, 2018, 2019}
    types := []string{"Meat", "Dairy", "Beverages", "Produce"}
    region := []string{"East", "West", "North", "South"}
    f.SetSheetRow("Sheet1", "A1", &[]string{"Month", "Year", "Type", "Sales", "Region"})
    for i := 0; i < 30; i++ {
        f.SetCellValue("Sheet1", fmt.Sprintf("A%d", i+2), month[rand.Intn(12)])
        f.SetCellValue("Sheet1", fmt.Sprintf("B%d", i+2), year[rand.Intn(3)])
        f.SetCellValue("Sheet1", fmt.Sprintf("C%d", i+2), types[rand.Intn(4)])
        f.SetCellValue("Sheet1", fmt.Sprintf("D%d", i+2), rand.Intn(5000))
        f.SetCellValue("Sheet1", fmt.Sprintf("E%d", i+2), region[rand.Intn(4)])
    }
    if err := f.AddPivotTable(&excelize.PivotTableOption{
        DataRange:       "Sheet1!$A$1:$E$31",
        PivotTableRange: "Sheet1!$G$2:$M$34",
        Rows: []excelize.PivotTableField{
            {Data: "Month", DefaultSubtotal: true}, {Data: "Year"}},
        Filter: []excelize.PivotTableField{
            {Data: "Region"}},
        Columns: []excelize.PivotTableField{
            {Data: "Type", DefaultSubtotal: true}},
        Data: []excelize.PivotTableField{
            {Data: "Sales", Name: "Summarize", Subtotal: "Sum"}},
        RowGrandTotals: true,
        ColGrandTotals: true,
        ShowDrill:      true,
        ShowRowHeaders: true,
        ShowColHeaders: true,
        ShowLastColumn: true,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

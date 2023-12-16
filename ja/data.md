# データ

## データ検証を追加する {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

指定されたワークシート名とデータ検証オブジェクトに基づいてデータ入力規則を設定すると、データ検証オブジェクトは、`NewDataValidation`  関数、データ検証タイプ、および条件参照[定数](constants.md) の定義を通じて作成できます。

例1、`Sheet1!A1:B2` 設定には、整数 10 ~ 20 の間のデータ入力規則を許可するための検証条件が含まれています: "error title"、エラーメッセージ "error body" というタイトルの無効なデータを入力すると、エラー警告が表示されます：

<p align="center"><img width="708" src="./images/data_validation_01.png" alt="データの検証"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dv)
```

例2、`Sheet1!A3:B4` の設定には、整数 10 より大きくすることができるデータ検証の検証規則が含まれており、セルが選択されたときに入力情報を表示し、入力情報は次のとおりです: "input body":

<p align="center"><img width="708" src="./images/data_validation_02.png" alt="データの検証"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

例3、`Sheet1!A5:B6` 検証条件のデータ入力規則をシーケンスとして設定し、空の値を無視してドロップダウン矢印を表示します:

<p align="center"><img width="708" src="./images/data_validation_03.png" alt="データの検証"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

データ検証ダイアログ ボックス (区切り文字で区切られたリスト) に項目を入力する場合、制限は区切り文字を含めて 255 文字です。データ検証リストのソース式が最大長制限を超えている場合は、ワークシートのセルに許容値を設定し、`SetSqrefDropList` 関数を使用してセルの参照を設定してください。

例4、`Sheet1!A7:B8` に設定されています。`Sheet1!E1:E3` はソースの検証条件であり、空の値を無視してドロップダウン矢印を表示します:

<p align="center"><img width="708" src="./images/data_validation_04.png" alt="データの検証"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("E1:E3")
f.AddDataValidation("Sheet1", dv)
```

データ検証ドロップダウン リストに表示される項目の数には制限があります。ワークシート上のリストから最大 32768 個の項目を表示できます。それ以上の項目が必要な場合は、カテゴリ別に分類された依存ドロップダウン リストを作成できます。

## データ検証を取得する {#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

GetDataValidations は、指定されたワークシート名でデータ検証リストを返します。

## データ検証の削除 {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

DeleteDataValidation 指定されたワークシート名と参照シーケンスによるデータ検証を削除します。参照シーケンスパラメータを指定しない場合、ワークシート内のすべてのデータ検証が削除されます。

## スライサーを追加する {#AddSlicer}

`SlicerOptions` はスライサーの設定を表します。

```go
type SlicerOptions struct {
    Name          string
    Table         string
    Cell          string
    Caption       string
    Macro         string
    Width         uint
    Height        uint
    DisplayHeader *bool
    ItemDesc      bool
    Format        GraphicOptions
}
```

`Name` は、スライサーの名前を指定し、テーブルのテーブルで動的に動的にテーブルを作成し、義務を負うパラメータを指定します。

`Table` は、テーブルの名を表し、ダイナミックなテーブルを規定し、義務を課します。

`Cell` は、スライサーの挿入位置、最高の義務を負う最高のセルルールを指定します。

`Caption` は、スライサーの最新情報、最高のパラメータを指定します。

`Macro` は、マクロ デュ スライサーの定義を使用し、XLSM または XLTM の拡張機能を提供します。

`Width` はスライサーの最大のパラメータであり、機能を指定します。

`Height` はスライサーのオート仕様であり、機能のパラメータです。

`DisplayHeader` は、スライサーの添付ファイルを指定し、機能のパラメータを設定し、添付ファイルのパラメータを指定します。

`ItemDesc` は、クロワッサンのトリデ要素 (Z-A) を指定し、機能のパラメータとデフォルトのパラメータを `false` に指定します (クロワッサンの注文を表します)。

`Format` はスライサーのフォーマットを指定し、パラメータを設定します。

```go
func (f *File) AddSlicer(sheet string, opts *SlicerOptions) error
```

AddSlicer 関数は、ワークシート名とスライサー設定を指定してスライサーを挿入します。たとえば、`Table1` という名前のテーブルのフィールド `Column1` を含むスライサーを `Sheet1!E1` に挿入します。

```go
err := f.AddSlicer("Sheet1", &excelize.SlicerOptions{
    Name:       "Column1",
    Cell:       "E1",
    TableSheet: "Sheet1",
    TableName:  "Table1",
    Caption:    "Column1",
    Width:      200,
    Height:     200,
})
```

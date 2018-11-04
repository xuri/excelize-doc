# Workbook

## Create Excel document {#NewFile}

```go
func NewFile() *File
```

NewFile provides a function to create new file by default template. The newly created workbook will by default contain a worksheet named `Sheet1`. For example:

## Open {#OpenFile}

```go
func OpenFile(filename string) (*File, error)
```

OpenFile take the name of an XLSX file and returns a populated XLSX file struct for it.

## Save {#Save}

```go
func (f *File) Save() error
```

Save provides a function to override the xlsx file with origin path.

## Save as {#SaveAs}

```go
func (f *File) SaveAs(name string) error
```

SaveAs provides a function to create or update to an xlsx file at the provided path.

## Create worksheet {#NewSheet}

```go
func (f *File) NewSheet(name string) int
```

NewSheet provides a function to create a new sheet by given worksheet name when creating a new XLSX file, the default sheet will be created, when you create a new file.

## Delete worksheet {#DeleteSheet}

```go
func (f *File) DeleteSheet(name string)
```

DeleteSheet provides a function to delete worksheet in a workbook by given worksheet name. Use this method with caution, which will affect changes in references such as formulas, charts, and so on. If there is any referenced value of the deleted worksheet, it will cause a file error when you open it. This function will be invalid when only the one worksheet is left.

## Copy worksheet {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

CopySheet provides a function to duplicate a worksheet by gave source and target worksheet index. Note that currently doesn't support duplicate workbooks that contain tables, charts or pictures. For Example:

```go
// Sheet1 already exists...
index := xlsx.NewSheet("Sheet2")
err := xlsx.CopySheet(1, index)
return err
```

## Worksheet background {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground provides a function to set background picture by given worksheet name.

## Set default worksheet {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet provides a function to set default active worksheet of XLSX by given index. Note that active index is different with the index that got by function [`GetSheetMap`](sheet.md#GetSheetMap), and it should be greater than `0` and less than total worksheet numbers.

## Get active sheet index {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

GetActiveSheetIndex provides a function to get an active sheet of XLSX. If not found the active sheet will return integer `0`.

## Get worksheet view properties {#GetSheetViewOptions}

```go
func (f *File) GetSheetViewOptions(name string, viewIndex int, opts ...SheetViewOptionPtr) error
```

GetSheetViewOptions gets the value of sheet view options. The `viewIndex` may be negative and if so is counted backward (`-1` is the last view). Available options:

Optional view parameter |Type
---|---
DefaultGridColor|bool
RightToLeft|bool
ShowFormulas|bool
ShowGridLines|bool
ShowRowColHeaders|bool

- Example 1, to get the gridline property settings for the last view on the worksheet named `Sheet1`:

```go
var showGridLines excelize.ShowGridLines
err = f.GetSheetViewOptions("Sheet1", -1, &showGridLines)
```

- Example 2:

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

var (
    defaultGridColor  excelize.DefaultGridColor
    rightToLeft       excelize.RightToLeft
    showFormulas      excelize.ShowFormulas
    showGridLines     excelize.ShowGridLines
    showRowColHeaders excelize.ShowRowColHeaders
)

if err := xl.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
    &showRowColHeaders,
); err != nil {
    panic(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showRowColHeaders:", showRowColHeaders)

if err := xl.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    panic(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
```

Get output:

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
After change:
- showGridLines: false
```
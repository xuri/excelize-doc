# Workbook

`Options` defines the options for reading and writing spreadsheets.

```go
type Options struct {
    MaxCalcIterations uint
    Password          string
    RawCellValue      bool
    UnzipSizeLimit    int64
    UnzipXMLSizeLimit int64
    TmpDir            string
    ShortDatePattern  string
    LongDatePattern   string
    LongTimePattern   string
    CultureInfo       CultureName
}
```

`MaxCalcIterations` specifies the maximum iterations for iterative calculation, the default value is 0.

`Password` specifies the password of the spreadsheet in plain text.

`RawCellValue` specifies if apply the number format for the cell value or get the raw value.

`UnzipSizeLimit` specifies the unzip size limit in bytes on open the spreadsheet, this value should be greater than or equal to `UnzipXMLSizeLimit`, the default size limit is 16GB.

`UnzipXMLSizeLimit` specifies the memory limit on unzipping worksheet and shared string table in bytes, worksheet XML will be extracted to system temporary directory when the file size is over this value, this value should be less than or equal to `UnzipSizeLimit`, the default value is 16MB.

`TmpDir` specifies the temporary directory for creating temporary files, if the value is empty, the system default temporary directory will be used.

`ShortDatePattern` specifies the short date number format code. In the spreadsheet applications, date formats display date and time serial numbers as date values. Date formats that begin with an asterisk (\*) respond to changes in regional date and time settings that are specified for the operating system. Formats without an asterisk are not affected by operating system settings. The `ShortDatePattern` used for specifies apply date formats that begin with an asterisk.

`LongDatePattern` specifies the long date number format code.

`LongTimePattern` specifies the long time number format code.

`CultureInfo` specifies the country code for applying built-in language number format code these effect by the system's local language settings.

`HeaderFooterImagePositionType` is the type of header and footer image position.

```go
type HeaderFooterImagePositionType byte
```

This section defines the worksheet header and footer image position types enumeration.

```go
const (
    HeaderFooterImagePositionLeft HeaderFooterImagePositionType = iota
    HeaderFooterImagePositionCenter
    HeaderFooterImagePositionRight
)
```

`CustomProperty` directly maps the custom property of the workbook. The value date type may be one of the following: `int32`, `float64`, `string`, `bool`, `time.Time`, or `nil`.

```go
type CustomProperty struct {
    Name  string
    Value interface{}
}
```

`CalcPropsOptions` defines the collection of properties the application uses to record calculation status and details.

```go
type CalcPropsOptions struct {
    CalcID                *uint
    CalcMode              *string
    FullCalcOnLoad        *bool
    RefMode               *string
    Iterate               *bool
    IterateCount          *uint
    IterateDelta          *float64
    FullPrecision         *bool
    CalcCompleted         *bool
    CalcOnSave            *bool
    ConcurrentCalc        *bool
    ConcurrentManualCount *uint
    ForceFullCalc         *bool
}
```

## Create Excel document {#NewFile}

```go
func NewFile(opts ...Options) *File
```

NewFile provides a function to create new file by default template. The newly created workbook will by default contain a worksheet named `Sheet1`. For example:

## Open {#OpenFile}

```go
func OpenFile(filename string, opts ...Options) (*File, error)
```

OpenFile takes the name of a spreadsheet file and returns a populated spreadsheet file struct for it. For example, open a spreadsheet with password protection:

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

Close the file by [`Close()`](workbook.md#Close) after opening the spreadsheet.

## Open data stream {#OpenReader}

```go
func OpenReader(r io.Reader, opts ...Options) (*File, error)
```

OpenReader read data stream from `io.Reader` and return a populated spreadsheet file.

For example, create HTTP server to handle upload template, then response download file with new worksheet added:

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/xuri/excelize/v2"
)

func process(w http.ResponseWriter, req *http.Request) {
    file, _, err := req.FormFile("file")
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    defer file.Close()
    f, err := excelize.OpenReader(file)
    if err != nil {
        fmt.Fprint(w, err.Error())
        return
    }
    f.Path = "Book1.xlsx"
    f.NewSheet("NewSheet")
    w.Header().Set("Content-Disposition", fmt.Sprintf("attachment; filename=%s", f.Path))
    w.Header().Set("Content-Type", req.Header.Get("Content-Type"))
    if err := f.Write(w); err != nil {
        fmt.Fprint(w, err.Error())
    }
}

func main() {
    http.HandleFunc("/process", process)
    http.ListenAndServe(":8090", nil)
}
```

Test with cURL:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xltx' -O -J
```

## Save {#Save}

```go
func (f *File) Save(opts ...Options) error
```

Save provides a function to override the spreadsheet file with the origin path.

## Save as {#SaveAs}

```go
func (f *File) SaveAs(name string, opts ...Options) error
```

SaveAs provides a function to create or update the spreadsheet file at the provided path.

## Close workbook {#Close}

```go
func (f *File) Close() error
```

Close closes and cleanup the open temporary file for the spreadsheet.

## Create worksheet {#NewSheet}

```go
func (f *File) NewSheet(sheet string) (int, error)
```

NewSheet provides the function to create a new sheet by given a worksheet name and returns the index of the sheets in the workbook (spreadsheet) after it appended. Note that when creating a new spreadsheet file, the default worksheet named `Sheet1` will be created.

## Delete worksheet {#DeleteSheet}

```go
func (f *File) DeleteSheet(sheet string) error
```

DeleteSheet provides a function to delete worksheet in a workbook by given worksheet name. Use this method with caution, which will affect changes in references such as formulas, charts, and so on. If there is any referenced value of the deleted worksheet, it will cause a file error when you open it. This function will be invalid when only one worksheet is left.

## Move worksheet {#MoveSheet}

```go
func (f *File) MoveSheet(source, target string) error
```

MoveSheet moves a sheet to a specified position in the workbook. The function moves the source sheet before the target sheet. After moving, other sheets will be shifted to the left or right. If the sheet is already at the target position, the function will not perform any action. Not that this function will be ungroup all sheets after moving. For example, move `Sheet2` before `Sheet1`:

```go
err := f.MoveSheet("Sheet2", "Sheet1")
```

## Copy worksheet {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

CopySheet provides a function to duplicate a worksheet by gave source and target worksheet index. Note that currently doesn't support duplicate workbooks that contain tables, charts or pictures. For example:

```go
// Sheet1 already exists...
index, err := f.NewSheet("Sheet2")
if err != nil {
    fmt.Println(err)
    return
}
err = f.CopySheet(0, index)
```

## Group worksheets {#GroupSheets}

```go
func (f *File) GroupSheets(sheets []string) error
```

GroupSheets provides a function to group worksheets by given worksheets names. Group worksheets must contain an active worksheet.

## Ungroup worksheets {#UngroupSheets}

```go
func (f *File) UngroupSheets() error
```

UngroupSheets provides a function to ungroup worksheets.

## Set worksheet background {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

SetSheetBackground provides a function to set background picture by given worksheet name and file path. Supported image types: BMP, EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF, and WMZ.

```go
func (f *File) SetSheetBackgroundFromBytes(sheet, extension string, picture []byte) error
```

SetSheetBackgroundFromBytes provides a function to set background picture by given worksheet name, extension name and image data. Supported image types: BMP, EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF, and WMZ.

## Set default worksheet {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

SetActiveSheet provides a function to set the default active sheet of the workbook by a given index. Note that the active index is different from the ID returned by function [`GetSheetMap`](sheet.md#GetSheetMap). It should be greater or equal to 0 and less than the total worksheet numbers.

## Get active sheet index {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

GetActiveSheetIndex provides a function to get an active worksheet of the workbook. If not found the active sheet will return integer `0`.

## Set worksheet visible {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(sheet string, visible bool, veryHidden ...bool) error
```

SetSheetVisible provides a function to set worksheet visible by given worksheet name. A workbook must contain at least one visible worksheet. If the given worksheet has been activated, this setting will be invalidated. The third optional `veryHidden` parameter only works when `visible` was `false`.

For example, hide `Sheet1`:

```go
err := f.SetSheetVisible("Sheet1", false)
```

## Get worksheet visible {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(sheet string) (bool, error)
```

GetSheetVisible provides a function to get worksheet visible by given worksheet name. For example, get the visible state of `Sheet1`:

```go
visible, err := f.GetSheetVisible("Sheet1")
```

## Set worksheet properties {#SetSheetProps}

```go
func (f *File) SetSheetProps(sheet string, opts *SheetPropsOptions) error
```

SetSheetProps provides a function to set worksheet properties. The properties that can be set are:

Options|Type|Description
---|---|---
CodeName                          | `*string`  | Specifies a stable name of the sheet, which should not change over time, and does not change from user input. This name should be used by code to reference a particular sheet
EnableFormatConditionsCalculation | `*bool`    | Indicating whether the conditional formatting calculations shall be evaluated. If set to false, then the min/max values of color scales or data bars or threshold values in Top N rules shall not be updated. Essentially the conditional formatting "calc" is off
Published                         | `*bool`    | Indicating whether the worksheet is published, the default value is `true`
AutoPageBreaks                    | `*bool`    | Indicating whether the sheet displays Automatic Page Breaks, the default value is `true`
FitToPage                         | `*bool`    | Indicating whether the Fit to Page print option is enabled, the default value is `false`
TabColorIndexed                   | `*int`     | Represents the indexed color value
TabColorRGB                       | `*string`  | Represents the standard ARGB (Alpha Red Green Blue) color value
TabColorTheme                     | `*int`     | Represents the zero-based index into the collection, referencing a particular value expressed in the Theme part
TabColorTint                      | `*float64` | Specifies the tint value applied to the color, the default value is `0.0`
OutlineSummaryBelow               | `*bool`    | Indicating whether summary rows appear below detail in an outline, when applying an outline, the default value is `true`
OutlineSummaryRight               | `*bool`    | Indicating whether summary columns appear to the right of detail in an outline, when applying an outline, the default value is `true`
BaseColWidth                      | `*uint8`   | Specifies the number of characters of the maximum digit width of the normal style's font. This value does not include margin padding or extra padding for grid lines. It is only the number of characters, the default value is `8`
DefaultColWidth                   | `*float64` | Specifies the default column width measured as the number of characters of the maximum digit width of the normal style's font
DefaultRowHeight                  | `*float64` | Specifies the default row height measured in point size. Optimization so we don't have to write the height on all rows. This can be written out if most rows have custom height, to achieve the optimization
CustomHeight                      | `*bool`    | Specifies the custom height, the default value is `false`
ZeroHeight                        | `*bool`    | Specifies if rows are hidden, the default value is `false`
ThickTop                          | `*bool`    | Specifies if rows have a thick top border by default, the default value is `false`
ThickBottom                       | `*bool`    | Specifies if rows have a thick bottom border by default, the default value is `false`

For example, make worksheet rows default as hidden:

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="Set worksheet properties"></p>

```go
f, enable := excelize.NewFile(), true
if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
    ZeroHeight: &enable,
}); err != nil {
    fmt.Println(err)
}
if err := f.SetRowVisible("Sheet1", 10, true); err != nil {
    fmt.Println(err)
}
f.SaveAs("Book1.xlsx")
```

There 4 kinds of presets "Custom Scaling Options" in the spreadsheet applications, if you need to set those kind of scaling options, please using the `SetSheetProps` and `SetPageLayout` functions to approach these 4 scaling options:

1. No Scaling (Print sheets at their actual size):

    ```go
    disable := false
    if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
        FitToPage: &disable,
    }); err != nil {
        fmt.Println(err)
    }
    ```

2. Fit Sheet on One Page (Shrink the printout so that it fits on one page):

    ```go
    enable := true
    if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
        FitToPage: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    ```

3. Fit All Columns on One Page (Shrink the printout so that it is one page wide):

    ```go
    enable, zero := true, 0
    if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
        FitToPage: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.SetPageLayout("Sheet1", &excelize.PageLayoutOptions{
        FitToHeight: &zero,
    }); err != nil {
        fmt.Println(err)
    }
    ```

4. Fit All Rows on One Page (Shrink the printout so that it is one page high):

    ```go
    enable, zero := true, 0
    if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
        FitToPage: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    if err := f.SetPageLayout("Sheet1", &excelize.PageLayoutOptions{
        FitToWidth: &zero,
    }); err != nil {
        fmt.Println(err)
    }
    ```

## Get worksheet properties {#GetSheetProps}

```go
func (f *File) GetSheetProps(sheet string) (SheetPropsOptions, error)
```

GetSheetProps provides a function to get worksheet properties.

## Set worksheet view properties {#SetSheetView}

```go
func (f *File) SetSheetView(sheet string, viewIndex int, opts *ViewOptions) error
```

SetSheetView sets sheet view properties. The `viewIndex` may be negative and if so is counted backward (`-1` is the last view). The properties that can be set are:

Options|Type|Description
---|---|---
DefaultGridColor  | `*bool`    | Indicating that the consuming application should use the default grid lines color(system dependent). Overrides any color specified in colorId, the default value is `true`
RightToLeft       | `*bool`    | Indicating whether the sheet is in "right to left" display mode. When in this mode, Column A is on the far right, Column B; is one column left of Column A, and so on. Also, information in cells is displayed in the Right to Left format, the default value is `false`
ShowFormulas      | `*bool`    | Indicating whether this sheet should display formulas, the default value is `false`
ShowGridLines     | `*bool`    | Indicating whether this sheet should display grid lines, the default value is `true`
ShowRowColHeaders | `*bool`    | Indicating whether the sheet should display row and column headings, the default value is `true`
ShowRuler         | `*bool`    | Indicating this sheet should display ruler, the default value is `true`
ShowZeros         | `*bool`    | Indicating whether to "show a zero in cells that have zero value". When using a formula to reference another cell which is empty, the referenced value becomes `0` when the flag is `true`, the default value is `true`
TopLeftCell       | `*string`  | Specifies a location of the top left visible cell Location of the top left visible cell in the bottom right pane (when in Left-to-Right mode)
View              | `*string`  | Indicating how sheet is displayed, by default it uses empty string, available options: `normal`，`pageBreakPreview` and `pageLayout`
ZoomScale         | `*float64` | Specifies a window zoom magnification for current view representing percent values. This attribute is restricted to values ranging from `10` to `400`. Horizontal & Vertical scale together, the default value is `100`

## Get worksheet view properties {#GetSheetView}

```go
func (f *File) GetSheetView(sheet string, viewIndex int) (ViewOptions, error)
```

GetSheetView gets the value of sheet view properties. The `viewIndex` may be negative and if so is counted backward (`-1` is the last view).

## Set worksheet page layout {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts *PageLayoutOptions) error
```

SetPageLayout provides a function to sets worksheet page layout. Available options:

`Size` specified the worksheet paper size, the default paper size of worksheet is "Letter paper (8.5 in. by 11 in.)". The following shows the paper size sorted by Excelize index number:

Index|Paper Size
---|---
1   | Letter paper (8.5 in. × 11 in.)
2   | Letter small paper (8.5 in. × 11 in.)
3   | Tabloid paper (11 in. × 17 in.)
4   | Ledger paper (17 in. × 11 in.)
5   | Legal paper (8.5 in. × 14 in.)
6   | Statement paper (5.5 in. × 8.5 in.)
7   | Executive paper (7.25 in. × 10.5 in.)
8   | A3 paper (297 mm × 420 mm)
9   | A4 paper (210 mm × 297 mm)
10  | A4 small paper (210 mm × 297 mm)
11  | A5 paper (148 mm × 210 mm)
12  | B4 paper (250 mm × 353 mm)
13  | B5 paper (176 mm × 250 mm)
14  | Folio paper (8.5 in. × 13 in.)
15  | Quarto paper (215 mm × 275 mm)
16  | Standard paper (10 in. × 14 in.)
17  | Standard paper (11 in. × 17 in.)
18  | Note paper (8.5 in. × 11 in.)
19  | #9 envelope (3.875 in. × 8.875 in.)
20  | #10 envelope (4.125 in. × 9.5 in.)
21  | #11 envelope (4.5 in. × 10.375 in.)
22  | #12 envelope (4.75 in. × 11 in.)
23  | #14 envelope (5 in. × 11.5 in.)
24  | C paper (17 in. × 22 in.)
25  | D paper (22 in. × 34 in.)
26  | E paper (34 in. × 44 in.)
27  | DL envelope (110 mm × 220 mm)
28  | C5 envelope (162 mm × 229 mm)
29  | C3 envelope (324 mm × 458 mm)
30  | C4 envelope (229 mm × 324 mm)
31  | C6 envelope (114 mm × 162 mm)
32  | C65 envelope (114 mm × 229 mm)
33  | B4 envelope (250 mm × 353 mm)
34  | B5 envelope (176 mm × 250 mm)
35  | B6 envelope (176 mm × 125 mm)
36  | Italy envelope (110 mm × 230 mm)
37  | Monarch envelope (3.875 in. × 7.5 in.)
38  | 6¾ envelope (3.625 in. × 6.5 in.)
39  | US standard fanfold (14.875 in. × 11 in.)
40  | German standard fanfold (8.5 in. × 12 in.)
41  | German legal fanfold (8.5 in. × 13 in.)
42  | ISO B4 (250 mm × 353 mm)
43  | Japanese postcard (100 mm × 148 mm)
44  | Standard paper (9 in. × 11 in.)
45  | Standard paper (10 in. × 11 in.)
46  | Standard paper (15 in. × 11 in.)
47  | Invite envelope (220 mm × 220 mm)
50  | Letter extra paper (9.275 in. × 12 in.)
51  | Legal extra paper (9.275 in. × 15 in.)
52  | Tabloid extra paper (11.69 in. × 18 in.)
53  | A4 extra paper (236 mm × 322 mm)
54  | Letter transverse paper (8.275 in. × 11 in.)
55  | A4 transverse paper (210 mm × 297 mm)
56  | Letter extra transverse paper (9.275 in. × 12 in.)
57  | SuperA/SuperA/A4 paper (227 mm × 356 mm)
58  | SuperB/SuperB/A3 paper (305 mm × 487 mm)
59  | Letter plus paper (8.5 in. × 12.69 in.)
60  | A4 plus paper (210 mm × 330 mm)
61  | A5 transverse paper (148 mm × 210 mm)
62  | JIS B5 transverse paper (182 mm × 257 mm)
63  | A3 extra paper (322 mm × 445 mm)
64  | A5 extra paper (174 mm × 235 mm)
65  | ISO B5 extra paper (201 mm × 276 mm)
66  | A2 paper (420 mm × 594 mm)
67  | A3 transverse paper (297 mm × 420 mm)
68  | A3 extra transverse paper (322 mm × 445 mm)
69  | Japanese Double Postcard (200 mm × 148 mm)
70  | A6 (105 mm × 148 mm)
71  | Japanese Envelope Kaku #2
72  | Japanese Envelope Kaku #3
73  | Japanese Envelope Chou #3
74  | Japanese Envelope Chou #4
75  | Letter Rotated (11 in. × 8½ in.)
76  | A3 Rotated (420 mm × 297 mm)
77  | A4 Rotated (297 mm × 210 mm)
78  | A5 Rotated (210 mm × 148 mm)
79  | B4 (JIS) Rotated (364 mm × 257 mm)
80  | B5 (JIS) Rotated (257 mm × 182 mm)
81  | Japanese Postcard Rotated (148 mm × 100 mm)
82  | Double Japanese Postcard Rotated (148 mm × 200 mm)
83  | A6 Rotated (148 mm × 105 mm)
84  | Japanese Envelope Kaku #2 Rotated
85  | Japanese Envelope Kaku #3 Rotated
86  | Japanese Envelope Chou #3 Rotated
87  | Japanese Envelope Chou #4 Rotated
88  | B6 (JIS) (128 mm × 182 mm)
89  | B6 (JIS) Rotated (182 mm × 128 mm)
90  | 12 in. × 11 in.
91  | Japanese Envelope You #4
92  | Japanese Envelope You #4 Rotated
93  | PRC 16K (146 mm × 215 mm)
94  | PRC 32K (97 mm × 151 mm)
95  | PRC 32K(Big) (97 mm × 151 mm)
96  | PRC Envelope #1 (102 mm × 165 mm)
97  | PRC Envelope #2 (102 mm × 176 mm)
98  | PRC Envelope #3 (125 mm × 176 mm)
99  | PRC Envelope #4 (110 mm × 208 mm)
100 | PRC Envelope #5 (110 mm × 220 mm)
101 | PRC Envelope #6 (120 mm × 230 mm)
102 | PRC Envelope #7 (160 mm × 230 mm)
103 | PRC Envelope #8 (120 mm × 309 mm)
104 | PRC Envelope #9 (229 mm × 324 mm)
105 | PRC Envelope #10 (324 mm × 458 mm)
106 | PRC 16K Rotated
107 | PRC 32K Rotated
108 | PRC 32K(Big) Rotated
109 | PRC Envelope #1 Rotated (165 mm × 102 mm)
110 | PRC Envelope #2 Rotated (176 mm × 102 mm)
111 | PRC Envelope #3 Rotated (176 mm × 125 mm)
112 | PRC Envelope #4 Rotated (208 mm × 110 mm)
113 | PRC Envelope #5 Rotated (220 mm × 110 mm)
114 | PRC Envelope #6 Rotated (230 mm × 120 mm)
115 | PRC Envelope #7 Rotated (230 mm × 160 mm)
116 | PRC Envelope #8 Rotated (309 mm × 120 mm)
117 | PRC Envelope #9 Rotated (324 mm × 229 mm)
118 | PRC Envelope #10 Rotated (458 mm × 324 mm)

`Orientation` specified worksheet orientation, the default orientation is `portrait`. The possible values for this field is `portrait` and `landscape`.

`FirstPageNumber` specified the first printed page number. If no value is specified, then "automatic" is assumed.

`AdjustTo` specified the print scaling. This attribute is restricted to values ranging from 10 (10%) to 400 (400%). This setting is overridden when `FitToWidth` and/or `FitToHeight` are in use.

`FitToHeight` specified the number of vertical pages to fit on.

`FitToWidth` specified the number of horizontal pages to fit on.

`BlackAndWhite` specified print black and white.

`PageOrder` specifies the ordering of multiple pages. Values accepted: `overThenDown` and `downThenOver`.

For example, set page layout for `Sheet1` with print black and white, first printed page number from `2`, landscape A4 small paper (210 mm by 297 mm), 2 vertical pages to fit on, and 2 horizontal pages to fit:

```go
f := excelize.NewFile()
var (
    size                 = 10
    orientation          = "landscape"
    firstPageNumber uint = 2
    adjustTo        uint = 100
    fitToHeight          = 2
    fitToWidth           = 2
    blackAndWhite        = true
)
if err := f.SetPageLayout("Sheet1", &excelize.PageLayoutOptions{
    Size:            &size,
    Orientation:     &orientation,
    FirstPageNumber: &firstPageNumber,
    AdjustTo:        &adjustTo,
    FitToHeight:     &fitToHeight,
    FitToWidth:      &fitToWidth,
    BlackAndWhite:   &blackAndWhite,
}); err != nil {
    fmt.Println(err)
}
```

## Get worksheet page layout {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string) (PageLayoutOptions, error)
```

GetPageLayout provides a function to gets worksheet page layout.

## Set worksheet page margins {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts *PageLayoutMarginsOptions) error
```

SetPageMargins provides a function to set worksheet page margins. Available options:

Options|Type|Description
---|---|---
Bottom       | `*float64` | Bottom
Footer       | `*float64` | Footer
Header       | `*float64` | Header
Left         | `*float64` | Left
Right        | `*float64` | Right
Top          | `*float64` | Top
Horizontally | `*bool`    | Center on page: Horizontally
Vertically   | `*bool`    | Center on page: Vertically

## Get worksheet page margins {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string) (PageLayoutMarginsOptions, error)
```

GetPageMargins provides a function to get worksheet page margins.

## Set workbook properties {#SetWorkbookProps}

```go
func (f *File) SetWorkbookProps(opts *WorkbookPropsOptions) error
```

SetWorkbookProps provides a function to sets workbook properties. Available options:

Options|Type|Description
---|---|---
Date1904      | `*bool`   | Indicates whether to use a 1900 or 1904 date system when converting serial date-times in the workbook to dates.
FilterPrivacy | `*bool`   | Specifies a boolean value that indicates whether the application has inspected the workbook for personally identifying information (PII). If this flag is set, the application warns the user any time the user performs an action that will insert PII into the document.
CodeName      | `*string` | Specifies the codename of the application that created this workbook. Use this attribute to track file content in incremental releases of the application.

## Get workbook properties {#GetWorkbookProps}

```go
func (f *File) GetWorkbookProps() (WorkbookPropsOptions, error)
```

GetWorkbookProps provides a function to gets workbook properties.

## Set header and footer {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, opts *HeaderFooterOptions) error
```

SetHeaderFooter provides a function to set headers and footers by given worksheet name and the control characters.

Headers and footers are specified using the following settings fields:

Fields           | Description
---|---
AlignWithMargins | Align header footer margins with page margins
DifferentFirst   | Different first-page header and footer indicator
DifferentOddEven | Different odd and even page headers and footers indicator
ScaleWithDoc     | Scale header and footer with document scaling
OddFooter        | Odd Page Footer, or primary Page Footer if `DifferentOddEven` is `false`
OddHeader        | Odd Header, or primary Page Header if `DifferentOddEven` is `false`
EvenFooter       | Even Page Footer
EvenHeader       | Even Page Header
FirstFooter      | First Page Footer
FirstHeader      | First Page Header

The following formatting codes can be used in 6 string type fields: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>Formatting Code</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>The character &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>Size of the text font, where font-size is a decimal font size in points</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>A text font-name string, font name, and a text font-type string, font type</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>Regular text format. Toggles bold and italic modes to off</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>Current worksheet&#39;s tab name</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>Bold text format, from off to on, or vice versa. The default mode is off</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>Current date</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>Center section</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>Double-underline text format</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>Current workbook&#39;s file name</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>Drawing object as background (Use AddHeaderFooterImage)</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>Shadow text format</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>Italic text format</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>Text font color<br>An RGB Color is specified as RRGGBB<br>A Theme Color is specified as TTSNNN where TT is the theme color Id, S is either &quot;+&quot; or &quot;-&quot; of the tint/shade value, and NNN is the tint/shade value</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>Left section</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>Total number of pages</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>Outline text format</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>Without the optional suffix, the current page number in decimal</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>Right section</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>Strikethrough text format</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>Current time</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>Single-underline text format. If double-underline mode is on, the next occurrence in a section specifier toggles double-underline mode to off; otherwise, it toggles single-underline mode, from off to on, or vice versa. The default mode is off</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>Superscript text format</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>Subscript text format</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>Current workbook&#39;s file path</td>
        </tr>
    </tbody>
</table>

For example:

```go
err := f.SetHeaderFooter("Sheet1", &excelize.HeaderFooterOptions{
    DifferentFirst:   true,
    DifferentOddEven: true,
    OddHeader:        "&R&P",
    OddFooter:        "&C&F",
    EvenHeader:       "&L&P",
    EvenFooter:       "&L&D&R&T",
    FirstHeader:      `&CCenter &"-,Bold"Bold&"-,Regular"HeaderU+000A&D`,
})
```

This example shows:

- The first page has its own header and footer
- Odd and even-numbered pages have different headers and footers
- Current page number in the right section of odd-page headers
- Current workbook's file name in the center section of odd-page footers
- Current page number in the left section of even-page headers
- Current date in the left section and the current time in the right section of even-page footers
- The text "Center Bold Header" on the first line of the center section of the first page, and the date on the second line of the center section of that same page
- No footer on the first page

## Add header and footer image {#AddHeaderFooterImage}

```go
func (f *File) AddHeaderFooterImage(sheet string, opts *HeaderFooterImageOptions) error
```

AddHeaderFooterImage provides a mechanism to set the graphics that can be referenced in the header and footer definitions via `&G`, supported image types: EMF, EMZ, GIF, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF and WMZ.

## Set defined name {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

SetDefinedName provides a function to set the defined names of the workbook or worksheet. If not specified scope, the default scope is the workbook. For example:

```go
err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

Print area and print titles settings for the worksheet:

<p align="center"><img width="628" src="./images/page_setup_01.png" alt="Print area and print titles settings for the worksheet"></p>

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Area",
    RefersTo: "Sheet1!$A$1:$Z$100",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A,Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

If you fill the `RefersTo` property with only one columns range without a comma, it will work as "Columns to repeat at left" only. For example:

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

If you fill the `RefersTo` property with only one rows range without a comma, it will work as "Rows to repeat at top" only. For example:

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

## Get defined name {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

GetDefinedName provides a function to get the defined names of the workbook or worksheet.

## Delete defined name {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

DeleteDefinedName provides a function to delete the defined names of the workbook or worksheet. If not specified scope, the default scope is workbook. For example:

```go
err := f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## Set application properties {#SetAppProps}

```go
func (f *File) SetAppProps(appProperties *AppProperties) error
```

SetAppProps provides a function to set document application properties. The properties that can be set are:

Property       | Description
---|---
Application       | The name of the application that created this document.
ScaleCrop         | Indicates the display mode of the document thumbnail. Set this element to `true` to enable scaling of the document thumbnail to the display. Set this element to `false` to enable cropping of the document thumbnail to show only sections that will fit the display.
DocSecurity       | Security level of a document as a numeric value. Document security is defined as:<br>1 - Document is password protected.<br>2 - Document is recommended to be opened as read-only.<br>3 - Document is enforced to be opened as read-only.<br>4 - Document is locked for annotation.
Company           | The name of a company associated with the document.
LinksUpToDate     | Indicates whether hyperlinks in a document are up-to-date. Set this element to `true` to indicate that hyperlinks are updated. Set this element to `false` to indicate that hyperlinks are outdated.
HyperlinksChanged | Specifies that one or more hyperlinks in this part were updated exclusively in this part by a producer. The next producer to open this document shall update the hyperlink relationships with the new hyperlinks specified in this part.
AppVersion        | Specifies the version of the application which produced this document. The content of this element shall be of the form XX.YYYY where X and Y represent numerical values, or the document shall be considered non-conformant.

For example:

```go
err := f.SetAppProps(&excelize.AppProperties{
    Application:       "Microsoft Excel",
    ScaleCrop:         true,
    DocSecurity:       3,
    Company:           "Company Name",
    LinksUpToDate:     true,
    HyperlinksChanged: true,
    AppVersion:        "16.0000",
})
```

## Get application properties {#GetAppProps}

```go
func (f *File) GetAppProps() (*AppProperties, error)
```

GetAppProps provides a function to get document application properties.

## Set document properties {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

SetDocProps provides a function to set document core properties. The properties that can be set are:

Property       | Description
---|---
Category       | A categorization of the content of this package.
ContentStatus  | The status of the content. For example: Values might include "Draft", "Reviewed" and "Final"
Created        | The created time of the content of the resource which represent in ISO 8601 UTC format, for example `2019-06-04T22:00:10Z`.
Creator        | An entity primarily responsible for making the content of the resource.
Description    | An explanation of the content of the resource.
Identifier     | An unambiguous reference to the resource within a given context.
Keywords       | A delimited set of keywords to support searching and indexing. This is typically a list of terms that are not available elsewhere in the properties.
Language       | The language of the intellectual content of the resource.
LastModifiedBy | The user who performed the last modification. The identification is environment-specific.
Modified       | The modified time of the content of the resource which represent in ISO 8601 UTC format, for example `2019-06-04T22:00:10Z`.
Revision       | The revision number of the content of the resource.
Subject        | The topic of the content of the resource.
Title          | The name given to the resource.
Version        | The version number. This value is set by the user or by the application.

For example:

```go
err := f.SetDocProps(&excelize.DocProperties{
    Category:       "category",
    ContentStatus:  "Draft",
    Created:        "2019-06-04T22:00:10Z",
    Creator:        "Go Excelize",
    Description:    "This file created by Go Excelize",
    Identifier:     "xlsx",
    Keywords:       "Spreadsheet",
    LastModifiedBy: "Go Author",
    Modified:       "2019-06-04T22:00:10Z",
    Revision:       "0",
    Subject:        "Test Subject",
    Title:          "Test Title",
    Language:       "en-US",
    Version:        "1.0.0",
})
```

## Get document properties {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

GetDocProps provides a function to get document core properties.

## Set custom properties {#SetCustomProps}

```go
func (f *File) SetCustomProps(prop CustomProperty) error
```

SetCustomProps provides a function to set custom file properties by given property name and value. If the property name already exists, it will be updated, otherwise a new property will be added. The value can be of type `int32`, `float64`, `bool`, `string`, `time.Time` or `nil`. The property will be delete if the value is `nil`. The function returns an error if the property value is not of the correct type.

## Get custom properties {#GetCustomProps}

```go
func (f *File) GetCustomProps() ([]CustomProperty, error)
```

GetCustomProps provides a function to get custom file properties.

## Set calculation properties {#SetCalcProps}

```go
func (f *File) SetCalcProps(opts *CalcPropsOptions) error
```

SetCalcProps provides a function to sets calculation properties.

Optional value of `CalcMode` property is: `manual`, `auto` or `autoNoTable`.

Optional value of `RefMode` property is: `A1` or `R1C1`.

## Get calculation properties {#GetCalcProps}

```go
func (f *File) GetCalcProps() (CalcPropsOptions, error)
```

GetCalcProps provides a function to gets calculation properties.

## Protect workbook {#ProtectWorkbook}

```go
func (f *File) ProtectWorkbook(opts *WorkbookProtectionOptions) error
```

ProtectWorkbook provides a function to prevent other users from accidentally or deliberately changing, moving, or deleting data in a workbook. The optional field `AlgorithmName` specified hash algorithm, support XOR, MD4, MD5, SHA-1, SHA2-56, SHA-384, and SHA-512 currently, if no hash algorithm specified, will be using the XOR algorithm as default. For example, protect workbook with protection settings:

```go
err := f.ProtectWorkbook(&excelize.WorkbookProtectionOptions{
    Password:      "password",
    LockStructure: true,
})
```

WorkbookProtectionOptions directly maps the settings of workbook protection.

```go
type WorkbookProtectionOptions struct {
    AlgorithmName string
    Password      string
    LockStructure bool
    LockWindows   bool
}
```

## Unprotect workbook {#UnprotectWorkbook}

```go
func (f *File) UnprotectWorkbook(password ...string) error
```

UnprotectWorkbook provides a function to remove protection for workbook, specified the optional password parameter to remove workbook protection with password verification.

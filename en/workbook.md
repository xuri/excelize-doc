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
    zoomScale         excelize.ZoomScale
    topLeftCell       excelize.TopLeftCell
)

if err := xl.GetSheetViewOptions(sheet, 0,
    &defaultGridColor,
    &rightToLeft,
    &showFormulas,
    &showGridLines,
    &showRowColHeaders,
    &zoomScale,
    &topLeftCell,
); err != nil {
    panic(err)
}

fmt.Println("Default:")
fmt.Println("- defaultGridColor:", defaultGridColor)
fmt.Println("- rightToLeft:", rightToLeft)
fmt.Println("- showFormulas:", showFormulas)
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- showRowColHeaders:", showRowColHeaders)
fmt.Println("- zoomScale:", zoomScale)
fmt.Println("- topLeftCell:", `"`+topLeftCell+`"`)

if err := xl.SetSheetViewOptions(sheet, 0, excelize.TopLeftCell("B2")); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &topLeftCell); err != nil {
    panic(err)
}

if err := xl.SetSheetViewOptions(sheet, 0, excelize.ShowGridLines(false)); err != nil {
    panic(err)
}

if err := xl.GetSheetViewOptions(sheet, 0, &showGridLines); err != nil {
    panic(err)
}

fmt.Println("After change:")
fmt.Println("- showGridLines:", showGridLines)
fmt.Println("- topLeftCell:", topLeftCell)
```

Get output:

```text
Default:
- defaultGridColor: true
- rightToLeft: false
- showFormulas: false
- showGridLines: true
- showRowColHeaders: true
- zoomScale: 0
- topLeftCell: ""
After change:
- showGridLines: false
- topLeftCell: B2
```

## Set worksheet page layout {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts ...PageLayoutOption) error
```

SetPageLayout provides a function to sets worksheet page layout. Available options:

- `PageLayoutOrientation` provides a method to sets worksheet orientation, the default orientation is "portrait". The following shows the orientation parameters supported by Excelize index number:

Parameter|Orientation
---|---
OrientationPortrait|portrait
OrientationLandscape|landscape

- `PageLayoutPaperSize` provides a method to sets worksheet paper size, the default paper size of worksheet is "Letter paper (8.5 in. by 11 in.)". The following shows the paper size sorted by Excelize index number:

Index|Paper Size
---|---
1   | Letter paper (8.5 in. by 11 in.)
2   | Letter small paper (8.5 in. by 11 in.)
3   | Tabloid paper (11 in. by 17 in.)
4   | Ledger paper (17 in. by 11 in.)
5   | Legal paper (8.5 in. by 14 in.)
6   | Statement paper (5.5 in. by 8.5 in.)
7   | Executive paper (7.25 in. by 10.5 in.)
8   | A3 paper (297 mm by 420 mm)
9   | A4 paper (210 mm by 297 mm)
10  | A4 small paper (210 mm by 297 mm)
11  | A5 paper (148 mm by 210 mm)
12  | B4 paper (250 mm by 353 mm)
13  | B5 paper (176 mm by 250 mm)
14  | Folio paper (8.5 in. by 13 in.)
15  | Quarto paper (215 mm by 275 mm)
16  | Standard paper (10 in. by 14 in.)
17  | Standard paper (11 in. by 17 in.)
18  | Note paper (8.5 in. by 11 in.)
19  | #9 envelope (3.875 in. by 8.875 in.)
20  | #10 envelope (4.125 in. by 9.5 in.)
21  | #11 envelope (4.5 in. by 10.375 in.)
22  | #12 envelope (4.75 in. by 11 in.)
23  | #14 envelope (5 in. by 11.5 in.)
24  | C paper (17 in. by 22 in.)
25  | D paper (22 in. by 34 in.)
26  | E paper (34 in. by 44 in.)
27  | DL envelope (110 mm by 220 mm)
28  | C5 envelope (162 mm by 229 mm)
29  | C3 envelope (324 mm by 458 mm)
30  | C4 envelope (229 mm by 324 mm)
31  | C6 envelope (114 mm by 162 mm)
32  | C65 envelope (114 mm by 229 mm)
33  | B4 envelope (250 mm by 353 mm)
34  | B5 envelope (176 mm by 250 mm)
35  | B6 envelope (176 mm by 125 mm)
36  | Italy envelope (110 mm by 230 mm)
37  | Monarch envelope (3.875 in. by 7.5 in.).
38  | 6 3/4 envelope (3.625 in. by 6.5 in.)
39  | US standard fanfold (14.875 in. by 11 in.)
40  | German standard fanfold (8.5 in. by 12 in.)
41  | German legal fanfold (8.5 in. by 13 in.)
42  | ISO B4 (250 mm by 353 mm)
43  | Japanese double postcard (200 mm by 148 mm)
44  | Standard paper (9 in. by 11 in.)
45  | Standard paper (10 in. by 11 in.)
46  | Standard paper (15 in. by 11 in.)
47  | Invite envelope (220 mm by 220 mm)
50  | Letter extra paper (9.275 in. by 12 in.)
51  | Legal extra paper (9.275 in. by 15 in.)
52  | Tabloid extra paper (11.69 in. by 18 in.)
53  | A4 extra paper (236 mm by 322 mm)
54  | Letter transverse paper (8.275 in. by 11 in.)
55  | A4 transverse paper (210 mm by 297 mm)
56  | Letter extra transverse paper (9.275 in. by 12 in.)
57  | SuperA/SuperA/A4 paper (227 mm by 356 mm)
58  | SuperB/SuperB/A3 paper (305 mm by 487 mm)
59  | Letter plus paper (8.5 in. by 12.69 in.)
60  | A4 plus paper (210 mm by 330 mm)
61  | A5 transverse paper (148 mm by 210 mm)
62  | JIS B5 transverse paper (182 mm by 257 mm)
63  | A3 extra paper (322 mm by 445 mm)
64  | A5 extra paper (174 mm by 235 mm)
65  | ISO B5 extra paper (201 mm by 276 mm)
66  | A2 paper (420 mm by 594 mm)
67  | A3 transverse paper (297 mm by 420 mm)
68  | A3 extra transverse paper (322 mm by 445 mm)
69  | Japanese Double Postcard (200 mm x 148 mm)
70  | A6 (105 mm x 148 mm)
71  | Japanese Envelope Kaku #2
72  | Japanese Envelope Kaku #3
73  | Japanese Envelope Chou #3
74  | Japanese Envelope Chou #4
75  | Letter Rotated (11in x 8 1/2 11 in)
76  | A3 Rotated (420 mm x 297 mm)
77  | A4 Rotated (297 mm x 210 mm)
78  | A5 Rotated (210 mm x 148 mm)
79  | B4 (JIS) Rotated (364 mm x 257 mm)
80  | B5 (JIS) Rotated (257 mm x 182 mm)
81  | Japanese Postcard Rotated (148 mm x 100 mm)
82  | Double Japanese Postcard Rotated (148 mm x 200 mm)
83  | A6 Rotated (148 mm x 105 mm)
84  | Japanese Envelope Kaku #2 Rotated
85  | Japanese Envelope Kaku #3 Rotated
86  | Japanese Envelope Chou #3 Rotated
87  | Japanese Envelope Chou #4 Rotated
88  | B6 (JIS) (128 mm x 182 mm)
89  | B6 (JIS) Rotated (182 mm x 128 mm)
90  | (12 in x 11 in)
91  | Japanese Envelope You #4
92  | Japanese Envelope You #4 Rotated
93  | PRC 16K (146 mm x 215 mm)
94  | PRC 32K (97 mm x 151 mm)
95  | PRC 32K(Big) (97 mm x 151 mm)
96  | PRC Envelope #1 (102 mm x 165 mm)
97  | PRC Envelope #2 (102 mm x 176 mm)
98  | PRC Envelope #3 (125 mm x 176 mm)
99  | PRC Envelope #4 (110 mm x 208 mm)
100 | PRC Envelope #5 (110 mm x 220 mm)
101 | PRC Envelope #6 (120 mm x 230 mm)
102 | PRC Envelope #7 (160 mm x 230 mm)
103 | PRC Envelope #8 (120 mm x 309 mm)
104 | PRC Envelope #9 (229 mm x 324 mm)
105 | PRC Envelope #10 (324 mm x 458 mm)
106 | PRC 16K Rotated
107 | PRC 32K Rotated
108 | PRC 32K(Big) Rotated
109 | PRC Envelope #1 Rotated (165 mm x 102 mm)
110 | PRC Envelope #2 Rotated (176 mm x 102 mm)
111 | PRC Envelope #3 Rotated (176 mm x 125 mm)
112 | PRC Envelope #4 Rotated (208 mm x 110 mm)
113 | PRC Envelope #5 Rotated (220 mm x 110 mm)
114 | PRC Envelope #6 Rotated (230 mm x 120 mm)
115 | PRC Envelope #7 Rotated (230 mm x 160 mm)
116 | PRC Envelope #8 Rotated (309 mm x 120 mm)
117 | PRC Envelope #9 Rotated (324 mm x 229 mm)
118 | PRC Envelope #10 Rotated (458 mm x 324 mm)

- For example, set page layout for `Sheet1` with landscape A4 small paper (210 mm by 297 mm):

```go
xl := excelize.NewFile()
const sheet = "Sheet1"

if err := xl.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutOrientation(excelize.OrientationLandscape),
); err != nil {
    panic(err)
}
if err := xl.SetPageLayout(
    "Sheet1",
    excelize.PageLayoutPaperSize(10),
); err != nil {
    panic(err)
}
```

## Get worksheet page layout {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string, opts ...PageLayoutOptionPtr) error
```

GetPageLayout provides a function to gets worksheet page layout. Available options:

- `PageLayoutOrientation` provides a method to gets worksheet orientation
- `PageLayoutPaperSize` provides a method to gets worksheet paper size

- For example, get page layout of `Sheet1`:

```go
xl := excelize.NewFile()
const sheet = "Sheet1"
var (
    orientation excelize.PageLayoutOrientation
    paperSize   excelize.PageLayoutPaperSize
)
if err := xl.GetPageLayout("Sheet1", &orientation); err != nil {
    panic(err)
}
if err := xl.GetPageLayout("Sheet1", &paperSize); err != nil {
    panic(err)
}
fmt.Println("Defaults:")
fmt.Printf("- orientation: %q\n", orientation)
fmt.Printf("- paper size: %d\n", paperSize)
// Output:
// Defaults:
// - orientation: "portrait"
// - paper size: 1
```

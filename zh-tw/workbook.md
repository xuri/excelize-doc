# 活頁簿

{{ book.info }}

`Options` 定義了讀寫電子表格檔案時的選項。

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

`MaxCalcIterations` 用以指定計算公式時最多迭代次數，默認值為 0。

`Password` 以明文形式指定開啓和儲存活頁簿時所使用的密碼，默認值為空。

`RawCellValue` 用以指定讀取儲存格值時是否獲取原始值，默認值為 `false`（應用數字格式）。

`UnzipSizeLimit` 用以指定開啓電子錶格檔案時的解壓縮大小限制（以位元組為單位），該值應大於或等於 `UnzipXMLSizeLimit`，默認大小限制為 16GB。

`UnzipXMLSizeLimit` 用以指定解壓每個工作表以及共享字符表時的記憶體限制（以位元組為單位），當大小超過此值時工作表 XML 檔案將被解壓至系統臨時目錄，該值應小於或等於 `UnzipSizeLimit`，默認大小限制為 16MB。

`TmpDir` 用以指定建立暫存檔案的暫存目錄，如果值為空，則使用系統預設的暫存目錄。

`ShortDatePattern` 用以指定短日期數字格式代碼。在電子錶格應用程式中，可以透過為儲存格設定帶有日期格式的數字格式，將日期和時間序列號顯示為日期值。其中以星號 (\*) 開頭的日期格式響應為作業系統指定的區域日期和時間設定的更改。沒有星號的格式不受作業系統設定的影響。`ShortDatePattern` 用於指定讀取以星號開頭的日期格式時所應用的短日期數字格式代碼。

`LongDatePattern` 用以指定長日期數字格式代碼。

`LongTimePattern` 用以指定長時間數字格式代碼。

`CultureInfo` 用以指定區域格式，該設定將在讀取受到作業系統特定的區域日期和時間設定影響的數字格式時使用。

`HeaderFooterImagePositionType` 定義了頁首和頁尾圖片位置類型。

```go
type HeaderFooterImagePositionType byte
```

下面是工作表頁首和頁尾位置枚舉值。

```go
const (
    HeaderFooterImagePositionLeft HeaderFooterImagePositionType = iota
    HeaderFooterImagePositionCenter
    HeaderFooterImagePositionRight
)
```

`CustomProperty` 定義了設定活頁簿自訂屬性時的選項。自訂屬性的值支持以下資料類型：`int32`、`float64`、`string`、`bool`、`time.Time` 和 `nil`。

```go
type CustomProperty struct {
    Name  string
    Value interface{}
}
```

`CalcPropsOptions` 定義了設定活頁簿計算屬性時的選項。

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

## 新增 {#NewFile}

```go
func NewFile(opts ...Options) *File
```

使用 `NewFile` 新增 Excel 活頁簿，新創建的活頁簿中會默認包含一個名為 `Sheet1` 的工作表。

## 開啓 {#OpenFile}

```go
func OpenFile(filename string, opts ...Options) (*File, error)
```

使用 `OpenFile` 開啓已有 Excel 檔案。例如，開啓帶有密碼保護的電子表格檔案：

```go
f, err := excelize.OpenFile("Book1.xlsx", excelize.Options{Password: "password"})
if err != nil {
    return
}
```

使用 [`Close()`](workbook.md#Close) 關閉已開啓的活頁簿。

## 開啓數據流 {#OpenReader}

```go
func OpenReader(r io.Reader, opts ...Options) (*File, error)
```

OpenReader 從 `io.Reader` 讀取數據流。

下面的例子中，我們創建一個簡單的 HTTP 服務器接收上傳的電子錶格檔案，向接收到的電子錶格檔案添加新工作表，並返回下載響應:

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

使用 cURL 進行測試:

```bash
curl --location --request GET 'http://127.0.0.1:8090/process' \
--form 'file=@/tmp/template.xltx' -O -J
```

## 儲存 {#Save}

```go
func (f *File) Save(opts ...Options) error
```

使用 `Save` 儲存對 Excel 檔案的編輯。

## 另存為 {#SaveAs}

```go
func (f *File) SaveAs(name string, opts ...Options) error
```

使用 `SaveAs` 儲存 Excel 檔案為指定檔案。

## 關閉活頁簿 {#Close}

```go
func (f *File) Close() error
```

關閉活頁簿並清理開啓檔案時可能產生的系統磁盤緩存。

## 新增工作表 {#NewSheet}

```go
func (f *File) NewSheet(sheet string) (int, error)
```

根據給定的工作表名稱來創建新工作表，並返回工作表在活頁簿中的索引。請注意，在創建新的活頁簿時，將包含名為 `Sheet1` 的默認工作表。

## 刪除工作表 {#DeleteSheet}

```go
func (f *File) DeleteSheet(sheet string) error
```

根據給定的工作表名稱刪除指定工作表，謹慎使用此方法，這將會影響到與被刪除工作表相關聯的公式、引用、圖表等元素。如果有其他組件引用了被刪除工作表上的值，將會引發錯誤提示，甚至將會導致開啓活頁簿失敗。當活頁簿中僅包含一個工作表時，調用此方法無效。

## 移動工作表 {#MoveSheet}

```go
func (f *File) MoveSheet(source, target string) error
```

將工作表移動到活頁簿中的指定位置。根據給定的被移動工作表名稱和目標工作表名稱，將工作表移動至目標工作表之前。移動後，其他工作表的位置將向左或向右移動，如果工作表已經在目標位置，則該函式不會執行任何操作。請注意，該函式在移動工作表後將取消所有工作表分組。例如，將名為 `Sheet2` 的工作表移動至工作表 `Sheet1` 之前：

```go
err := f.MoveSheet("Sheet2", "Sheet1")
```

## 複製工作表 {#CopySheet}

```go
func (f *File) CopySheet(from, to int) error
```

根據給定的被複製工作表與目標工作表索引複製工作表，目標工作表索引需要開發者自行確認是否已經存在。目前支援僅包含儲存格值和公式的工作表間的複製，不支援包含表格、圖片、圖表和透視表等元素的工作表之間的複製。

```go
// 名稱為 Sheet1 的工作表已經存在 ...
index, err := f.NewSheet("Sheet2")
if err != nil {
    fmt.Println(err)
    return
}
err = f.CopySheet(0, index)
```

## 工作表分組 {#GroupSheets}

```go
func (f *File) GroupSheets(sheets []string) error
```

根據給定的工作表名稱對工作表進行分組，給定的工作表中需包含默認工作表。

## 取消工作表分組 {#UngroupSheets}

```go
func (f *File) UngroupSheets() error
```

取消工作表分組。

## 設定工作表背景圖片 {#SetSheetBackground}

```go
func (f *File) SetSheetBackground(sheet, picture string) error
```

根據給定的工作表名稱和圖片檔案路徑為指定的工作表設定平鋪效果的背景圖片。支援的圖片檔案格式為：BMP、EMF、EMZ、GIF、JPEG、JPG、PNG、SVG、TIF、TIFF、WMF 和 WMZ。

```go
func (f *File) SetSheetBackgroundFromBytes(sheet, extension string, picture []byte) error
```

根據給定的工作表名稱、圖片格式擴展名和圖片格式數據為指定的工作表設定平鋪效果的背景圖片。支援的圖片檔案格式為：BMP、EMF、EMZ、GIF、JPEG、JPG、PNG、SVG、TIF、TIFF、WMF 和 WMZ。

## 設定默認工作表 {#SetActiveSheet}

```go
func (f *File) SetActiveSheet(index int)
```

根據給定的索引值設定默認工作表，索引的值應該大於等於 `0` 且小於活頁簿所包含的累積工作表總數。

## 獲取默認工作表索引 {#GetActiveSheetIndex}

```go
func (f *File) GetActiveSheetIndex() int
```

獲取默認工作表的索引，如果沒有找到默認工作表將傳回 `0`。

## 設定工作表可見性 {#SetSheetVisible}

```go
func (f *File) SetSheetVisible(sheet string, visible bool, veryHidden ...bool) error
```

根據給定的工作表名稱和可見性參數設定工作表的可見性。一個活頁簿中至少包含一個可見工作表。如果給定的工作表為默認工作表，則對其可見性設定無效。第三個可選參數 `veryHidden` 僅在 `visible` 參數值為 `false` 時有效。

例如，隱藏名為 `Sheet1` 的工作表：

```go
err := f.SetSheetVisible("Sheet1", false)
```

## 獲取工作表可見性 {#GetSheetVisible}

```go
func (f *File) GetSheetVisible(sheet string) (bool, error)
```

根據給定的工作表名稱獲取工作表可見性設定。例如，獲取名為 `Sheet1` 的工作表可見性設定:

```go
visible, err := f.GetSheetVisible("Sheet1")
```

## 設定工作表屬性 {#SetSheetProps}

```go
func (f *File) SetSheetProps(sheet string, opts *SheetPropsOptions) error
```

根據給定的工作表名稱和屬性參數設定工作表屬性。支援設定的工作表屬性選項：

屬性 | 類型 | 描述
---|---|---
CodeName                          | `*string`  | 代碼名
EnableFormatConditionsCalculation | `*bool`    | 指定條件式格式是否自動計算，默認值為 `true`
Published                         | `*bool`    | 指定工作表是否發佈，默認值為 `true`
AutoPageBreaks                    | `*bool`    | 指定工作表是否自動分頁，默認值為 `true`
FitToPage                         | `*bool`    | 指定是否開啓自適應頁面列印，默認值為 `false`
TabColorIndexed                   | `*int`     | 僅用於向後兼容的索引色值
TabColorRGB                       | `*string`  | 標準 ARGB 色值
TabColorTheme                     | `*int`     | 從 `0` 開始的主題色彩索引
TabColorTint                      | `*float64` | 應用於色彩的色調值，默認值為 `0.0`
OutlineSummaryBelow               | `*bool`    | 指定分級顯示方向，是否在明細數據的下方，默認值為 `true`
OutlineSummaryRight               | `*bool`    | 指定分級顯示方向，是否在明細數據的右側，默認值為 `true`
BaseColWidth                      | `*uint8`   | 以字符數為單位表示的基本列寬度，默認值為 `8`
DefaultColWidth                   | `*float64` | 包含邊界和網格線的默認欄寬度
DefaultRowHeight                  | `*float64` | 以磅為單位表示的行高度
CustomHeight                      | `*bool`    | 指定是否應用自訂列高度，默認值為 `false`
ZeroHeight                        | `*bool`    | 指定是否默認隱藏列，默認值為 `false`
ThickTop                          | `*bool`    | 指定默認情況下列是否具有粗上外框，默認值為 `false`
ThickBottom                       | `*bool`    | 指定默認情況下列是否具有粗下外框，默認值為 `false`

例如，設定名為 `Sheet1` 的工作表中列默認為隱藏：

<p align="center"><img width="612" src="./images/sheet_format_pr_01.png" alt="設定工作表屬性"></p>

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

在電子錶格應用中，有四種"自訂縮放比例"預設選項。如果您需要使用這些縮放選項，請使用 [`SetSheetProps`](workbook.md#SetSheetProps) 和 [`SetPageLayout`](workbook.md#SetPageLayout) 函數來設定這四種縮放選項:

1. 不變更比例（以實際大小列印工作表）:

    ```go
    disable := false
    if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
        FitToPage: &disable,
    }); err != nil {
        fmt.Println(err)
    }
    ```

2. 將工作表放入單一頁面（縮小列印成品，使其符合一頁大小）:

    ```go
    enable := true
    if err := f.SetSheetProps("Sheet1", &excelize.SheetPropsOptions{
        FitToPage: &enable,
    }); err != nil {
        fmt.Println(err)
    }
    ```

3. 將所有欄放入單一頁面（縮小列印成品，使其僅有一頁寬度）:

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

4. 將所有列放入單一頁面（縮小列印成品，使其僅有一頁高度）:

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

## 獲取工作表屬性 {#GetSheetProps}

```go
func (f *File) GetSheetProps(sheet string) (SheetPropsOptions, error)
```

根據給定的工作表名稱獲取工作表屬性。

## 設定工作表檢視屬性 {#SetSheetView}

```go
func (f *File) SetSheetView(sheet string, viewIndex int, opts *ViewOptions) error
```

根據給定的工作表名稱、檢視索引和檢視參數設定工作表檢視屬性，`viewIndex` 可以是負數，如果是這樣，則向後計數（`-1` 代表最後一個檢視）。支援設定的工作表檢視屬性選項：

屬性 | 類型 | 描述
---|---|---
DefaultGridColor  | `*bool`    | 指定是否使用默認網格線色彩，默認值為 `true`
RightToLeft       | `*bool`    | 指定是否使用從右到左顯示模式，默認值為 `false`
ShowFormulas      | `*bool`    | 指定工作表是否顯示公式，默認值為 `false`
ShowGridLines     | `*bool`    | 指定工作表是否顯示網格線，默認值為 `true`
ShowRowColHeaders | `*bool`    | 指定工作表是否顯示標題列和標題欄，默認值為 `true`
ShowRuler         | `*bool`    | 指定是否在頁面配置檢視中顯示標尺，默認值為 `true`
ShowZeros         | `*bool`    | 指定是否顯示儲存格的零值，默認值為 `true`，否則將顯示空白
TopLeftCell       | `*string`  | 指定左上角可見儲存格的坐標
View              | `*string`  | 指示工作表檢視類型，枚舉值為 `normal`，`pageBreakPreview` 和 `pageLayout`
ZoomScale         | `*float64` | 以百分比表示的當前檢視顯示窗口縮放比例，區間範圍限於 10 ~ 400，默認值為 `100`

## 獲取工作表檢視屬性 {#GetSheetView}

```go
func (f *File) GetSheetView(sheet string, viewIndex int) (ViewOptions, error)
```

根據給定的工作表名稱和檢視索引獲取工作表檢視屬性，`viewIndex` 可以是負數，如果是這樣，則向後計數（`-1` 代表最後一個檢視）。

## 設定工作表頁面配置 {#SetPageLayout}

```go
func (f *File) SetPageLayout(sheet string, opts *PageLayoutOptions) error
```

根據給定的工作表名稱和頁面配置參數設定工作表的頁面配置屬性。目前支援設定的頁面配置屬性：

`Size` 屬性用以設定頁面紙張大小，默認頁面配置大小為「信紙 (8½ 英吋 × 11 英吋)」。下面的表格是 Excelize 中頁面配置大小和索引 `Size` 參數的關係對照：

索引 | 紙張大小
---|---
1   | 信紙 (8½ 英吋 × 11 英吋)
2   | 簡式信紙 (8½ 英吋 × 11 英吋)
3   | 卡片 (11 英吋 × 17 英吋)
4   | 賬單 (17 英吋 × 11 英吋)
5   | 律師公文紙 (8½ 英吋 × 14 英吋)
6   | 報告單 (5½ 英吋 × 8½ 英吋)
7   | 行政公文紙 (7½ 英吋 × 10 英吋)
8   | A3 (297 公釐 × 420 公釐)
9   | A4 (210 公釐 × 297 公釐)
10  | A4(小) (210 公釐 × 297 公釐)
11  | A5 (148 公釐 × 210 公釐)
12  | B4 (250 公釐 × 353 公釐)
13  | B5 (176 公釐 × 250 公釐)
14  | 對開本 (8½ 英吋 × 13 英吋)
15  | 四開 (215 公釐 × 275 公釐)
16  | 美式標準紙張 (10 英吋 × 14 英吋)
17  | 美式標準紙張 (11 英吋 × 17 英吋)
18  | 便簽 (8.5 英吋 × 11 英吋)
19  | 信封 #9 (3.875 英吋 × 8.875 英吋)
20  | 信封 #10 (4⅛ 英吋 × 9½ 英吋)
21  | 信封 #11 (4.5 英吋 × 10.375 英吋)
22  | 信封 #12 (4.75 英吋 × 11 英吋)
23  | 信封 #14 (5 英吋 × 11.5 英吋)
24  | C paper (17 英吋 × 22 英吋)
25  | D paper (22 英吋 × 34 英吋)
26  | E paper (34 英吋 × 44 英吋)
27  | 信封 DL (110 公釐 × 220 公釐)
28  | 信封 C5 (162 公釐 × 229 公釐)
29  | 信封 C3 (324 公釐 × 458 公釐)
30  | 信封 C4 (229 公釐 × 324 公釐)
31  | 信封 C6 (114 公釐 × 162 公釐)
32  | 信封 C65 (114 公釐 × 229 公釐)
33  | 信封 B4 (250 公釐 × 353 公釐)
34  | 信封 B5 (176 公釐 × 250 公釐)
35  | 信封 B6 (176 公釐 × 125 公釐)
36  | 義大利信封 (110 公釐 × 230 公釐)
37  | 君主式信封 (3.88 英吋 × 7.5 英吋)
38  | 6¾ 信封 (3.625 英吋 × 6.5 英吋)
39  | 美國標準 fanfold (14.875 英吋 × 11 英吋)
40  | 德國標準 fanfold (8.5 英吋 × 12 英吋)
41  | 德國法律專用紙 fanfold (8.5 英吋 × 13 英吋)
42  | ISO B4 (250 公釐 × 353 公釐)
43  | 日式明信片 (100 公釐 × 148 公釐)
44  | Standard paper (9 英吋 × 11 英吋)
45  | Standard paper (10 英吋 × 11 英吋)
46  | Standard paper (15 英吋 × 11 英吋)
47  | 邀請信 (220 公釐 × 220 公釐)
50  | 信紙加大 (9.275 英吋 × 12 英吋)
51  | 特大法律專用紙 (9.275 英吋 × 15 英吋)
52  | Tabloid extra paper (11.69 英吋 × 18 英吋)
53  | A4 特大 (236 公釐 × 322 公釐)
54  | 信紙橫向旋轉 (8.275 英吋 × 11 英吋)
55  | A4 橫向旋轉 (210 公釐 × 297 公釐)
56  | 信紙特大橫向旋轉 (9.275 英吋 × 12 英吋)
57  | SuperA/SuperA/A4 paper (227 公釐 × 356 公釐)
58  | SuperB/SuperB/A3 paper (305 公釐 × 487 公釐)
59  | 信紙加大 (8.5 英吋 × 12.69 英吋)
60  | A4 加大 (210 公釐 × 330 公釐)
61  | A5 橫向旋轉 (148 公釐 × 210 公釐)
62  | JIS B5 橫向旋轉 (182 公釐 × 257 公釐)
63  | A3 特大 (322 公釐 × 445 公釐)
64  | A5 特大 (174 公釐 × 235 公釐)
65  | ISO B5 特大 (201 公釐 × 276 公釐)
66  | A2 (420 公釐 × 594 公釐)
67  | A3 橫向旋轉 (297 公釐 × 420 公釐)
68  | A3 特大橫向旋轉 (322 公釐 × 445 公釐)
69  | 雙層日式明信片 (200 公釐 × 148 公釐)
70  | A6 (105 公釐 × 148 公釐)
71  | 日式信封 Kaku #2
72  | 日式信封 Kaku #3
73  | 日式信封 Chou #3
74  | 日式信封 Chou #4
75  | 信紙橫向旋轉 (11 英吋 × 8½ 英吋)
76  | A3 橫向旋轉 (420 公釐 × 297 公釐)
77  | A4 橫向旋轉 (297 公釐 × 210 公釐)
78  | A5 橫向旋轉 (210 公釐 × 148 公釐)
79  | B4 (JIS) 橫向旋轉 (364 公釐 × 257 公釐)
80  | B5 (JIS) 橫向旋轉 (257 公釐 × 182 公釐)
81  | 日式明信片 橫向旋轉 (148 公釐 × 100 公釐)
82  | 雙層日式明信片 橫向旋轉 (148 公釐 × 200 公釐)
83  | A6 橫向旋轉 (148 公釐 × 105 公釐)
84  | 日式信封 Kaku #2 橫向旋轉
85  | 日式信封 Kaku #3 橫向旋轉
86  | 日式信封 Chou #3 橫向旋轉
87  | 日式信封 Chou #4 橫向旋轉
88  | B6 (JIS) (128 公釐 × 182 公釐)
89  | B6 (JIS) 橫向旋轉 (182 公釐 × 128 公釐)
90  | 12 英吋 × 11 英吋
91  | 日式信封 You #4
92  | 日式信封 You #4 橫向旋轉
93  | 中式 16 開 (146 公釐 × 215 公釐)
94  | 中式 32 開 (97 公釐 × 151 公釐)
95  | 中式大 32 開 (97 公釐 × 151 公釐)
96  | 中式信封 #1 (102 公釐 × 165 公釐)
97  | 中式信封 #2 (102 公釐 × 176 公釐)
98  | 中式信封 #3 (125 公釐 × 176 公釐)
99  | 中式信封 #4 (110 公釐 × 208 公釐)
100 | 中式信封 #5 (110 公釐 × 220 公釐)
101 | 中式信封 #6 (120 公釐 × 230 公釐)
102 | 中式信封 #7 (160 公釐 × 230 公釐)
103 | 中式信封 #8 (120 公釐 × 309 公釐)
104 | 中式信封 #9 (229 公釐 × 324 公釐)
105 | 中式信封 #10 (324 公釐 × 458 公釐)
106 | 中式 16 開 橫向旋轉
107 | 中式 32 開 橫向旋轉
108 | 中式大 32 開 橫向旋轉
109 | 中式信封 #1 橫向旋轉 (165 公釐 × 102 公釐)
110 | 中式信封 #2 橫向旋轉 (176 公釐 × 102 公釐)
111 | 中式信封 #3 橫向旋轉 (176 公釐 × 125 公釐)
112 | 中式信封 #4 橫向旋轉 (208 公釐 × 110 公釐)
113 | 中式信封 #5 橫向旋轉 (220 公釐 × 110 公釐)
114 | 中式信封 #6 橫向旋轉 (230 公釐 × 120 公釐)
115 | 中式信封 #7 橫向旋轉 (230 公釐 × 160 公釐)
116 | 中式信封 #8 橫向旋轉 (309 公釐 × 120 公釐)
117 | 中式信封 #9 橫向旋轉 (324 公釐 × 229 公釐)
118 | 中式信封 #10 橫向旋轉 (458 公釐 × 324 公釐)

`Orientation` 屬性用以設定頁面配置方向，默認頁面配置方向為「直向」，可選值為 `portrait` 和 `landscape`。

`FirstPageNumber` 屬性用以設定頁面起始頁碼，默認為自動。

`AdjustTo` 屬性用以設定頁面縮放比例，取值範圍 10 至 400，即縮放 10% 至 400%，默認值為 `100` 正常尺寸。`FitToHeight` 或 `FitToWidth` 的設定會覆蓋此屬性。

`FitToHeight` 屬性用以設定頁面縮放調整頁寬，默認值為 `1`。

`FitToWidth` 屬性用以設定頁面縮放調整頁高，默認值為 `1`。

`BlackAndWhite` 屬性用以設定單色列印 `true` 或 `false`，默認值為 `false` 關閉。

`PageOrder` 屬性用以設定頁面順序，可選值為：`overThenDown`（循列欄印）和 `downThenOver`（循欄列印），默認值為 `downThenOver`。

- 例如，將名為 `Sheet1` 的工作表頁面配置設定為單色列印、起始頁碼為 `2`、橫向、使用 A4(小) 210 × 297 毫米紙張並調整為 2 頁寬、2 頁高：

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

## 獲取工作表頁面配置 {#GetPageLayout}

```go
func (f *File) GetPageLayout(sheet string) (PageLayoutOptions, error)
```

根據給定的工作表名稱和頁面配置參數獲取工作表的頁面配置屬性。

## 設定工作表頁邊界 {#SetPageMargins}

```go
func (f *File) SetPageMargins(sheet string, opts *PageLayoutMarginsOptions) error
```

根據給定的工作表名稱和頁邊界參數設定工作表的頁邊界。支援設定的頁邊界選項：

選項 | 類別 | 描述
---|---|---
Bottom       | `*float64` | 底端
Footer       | `*float64` | 頁尾
Header       | `*float64` | 頁首
Left         | `*float64` | 左
Right        | `*float64` | 右
Top          | `*float64` | 頂端
Horizontally | `*bool`    | 頁面置中方式：水平置中
Vertically   | `*bool`    | 頁面置中方式：垂直置中

## 獲取工作表頁邊界 {#GetPageMargins}

```go
func (f *File) GetPageMargins(sheet string) (PageLayoutMarginsOptions, error)
```

根據給定的工作表名稱和頁邊界參數獲取工作表的頁邊界。

## 設定活頁簿屬性 {#SetWorkbookProps}

```go
func (f *File) SetWorkbookProps(opts *WorkbookPropsOptions) error
```

SetWorkbookProps 用於設定活頁簿的屬性。支援設定的活頁簿屬性：

屬性 | 類別 | 描述
---|---|---
Date1904      | `*bool`   | 指示活頁簿是否使用 1904 日期系統
FilterPrivacy | `*bool`   | 篩選器隱私，指示應用程式是否檢查活頁簿中的個人識別信息
CodeName      | `*string` | 代碼名

## 獲取活頁簿屬性 {#GetWorkbookPrOptions}

```go
func (f *File) GetWorkbookProps() (WorkbookPropsOptions, error)
```

GetWorkbookProps 用於獲取活頁簿的屬性。

## 設定頁首和頁尾 {#SetHeaderFooter}

```go
func (f *File) SetHeaderFooter(sheet string, opts *HeaderFooterOptions) error
```

根據給定的工作表名稱和控制字符設定工作表的頁首和頁尾。

頁首和頁尾包含如下欄位：

欄位           | 描述
---|---
AlignWithMargins | 設定頁首頁尾邊界與頁邊界對齊
DifferentFirst   | 設定第一頁頁首和頁尾
DifferentOddEven | 設定奇數和偶數頁頁首和頁尾
ScaleWithDoc     | 設定頁首和頁尾跟隨檔案縮放
OddFooter        | 奇數頁頁尾控制字符，當 `DifferentOddEven` 的值為 `false` 時，用於設定第一頁頁尾
OddHeader        | 奇數頁頁首控制字符，當 `DifferentOddEven` 的值為 `false` 時，用於設定第一頁頁首
EvenFooter       | 偶數頁頁尾控制字符
EvenHeader       | 偶數頁頁首控制字符
FirstFooter      | 首頁頁尾控制字符
FirstHeader      | 首頁頁首控制字符

下表中的格式代碼可用於 6 個字符串類別欄位: `OddHeader`, `OddFooter`, `EvenHeader`, `EvenFooter`, `FirstFooter`, `FirstHeader`

<table>
    <thead>
        <tr>
            <th>格式代碼</th>
            <th>描述</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>&amp;&amp;</code></td>
            <td>字符 &quot;&amp;&quot;</td>
        </tr>
        <tr>
            <td><code>&amp;font-size</code></td>
            <td>文本字型的大小, 其中字型大小為以磅為單位的十進制字型大小</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;font name,font type&quot;</code></td>
            <td>文本字型名字符串、字型名稱和文本字型類別字符串、字型類別</td>
        </tr>
        <tr>
            <td><code>&amp;&quot;-,Regular&quot;</code></td>
            <td>常規文本格式。關閉粗體和斜體模式</td>
        </tr>
        <tr>
            <td><code>&amp;A</code></td>
            <td>當前工作表名稱</td>
        </tr>
        <tr>
            <td><code>&amp;B</code> or <code>&amp;&quot;-,Bold&quot;</code></td>
            <td>粗體文本格式, 關閉或開啓，默認關閉。</td>
        </tr>
        <tr>
            <td><code>&amp;D</code></td>
            <td>當前日期</td>
        </tr>
        <tr>
            <td><code>&amp;C</code></td>
            <td>中間部分</td>
        </tr>
        <tr>
            <td><code>&amp;E</code></td>
            <td>對文本使用雙底線</td>
        </tr>
        <tr>
            <td><code>&amp;F</code></td>
            <td>當前活頁簿檔案名稱</td>
        </tr>
        <tr>
            <td><code>&amp;G</code></td>
            <td>將指定對象做為背景（使用 AddHeaderFooterImage 函式添加頁首和頁尾圖片）</td>
        </tr>
        <tr>
            <td><code>&amp;H</code></td>
            <td>文字陰影</td>
        </tr>
        <tr>
            <td><code>&amp;I</code> or <code>&amp;&quot;-,Italic&quot;</code></td>
            <td>文字傾斜</td>
        </tr>
        <tr>
            <td><code>&amp;K</code></td>
            <td>字型色彩<br>格式為 RRGGBB 的 RGB 色彩<br>主題色彩被指定為 TTSNNN, 其中 TT 是主題色彩 id, S 是色調或陰影的 &quot;+&quot; 或者 &quot;-&quot;, 是色調或陰影的值</td>
        </tr>
        <tr>
            <td><code>&amp;L</code></td>
            <td>左側部分</td>
        </tr>
        <tr>
            <td><code>&amp;N</code></td>
            <td>總頁數</td>
        </tr>
        <tr>
            <td><code>&amp;O</code></td>
            <td>大綱文本格式</td>
        </tr>
        <tr>
            <td><code>&amp;P[[+\|-]n]</code></td>
            <td>如果沒有可選的後綴, 當前頁碼 (十進制)</td>
        </tr>
        <tr>
            <td><code>&amp;R</code></td>
            <td>右側部分</td>
        </tr>
        <tr>
            <td><code>&amp;S</code></td>
            <td>文本刪除線</td>
        </tr>
        <tr>
            <td><code>&amp;T</code></td>
            <td>當前時間</td>
        </tr>
        <tr>
            <td><code>&amp;U</code></td>
            <td>為文本添加單底線。默認模式處於關閉狀態</td>
        </tr>
        <tr>
            <td><code>&amp;X</code></td>
            <td>上標格式</td>
        </tr>
        <tr>
            <td><code>&amp;Y</code></td>
            <td>下標格式</td>
        </tr>
        <tr>
            <td><code>&amp;Z</code></td>
            <td>當前活頁簿檔案路徑</td>
        </tr>
    </tbody>
</table>

例如：

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

上面的例子蘊含如下格式：

- 第一頁有自己的頁首和頁尾
- 奇數和偶數頁具有不同的頁首和頁尾
- 奇數頁標題右側部分為當前頁碼
- 奇數頁頁尾中心部分為當前活頁簿的檔案名
- 偶數頁標題左側部分為當前頁碼
- 左側部分為當前日期，偶數頁頁尾右側部分為當前時間
- 第一頁中心部分的第一行上的文本為「Center Bold Header」, 第二行為日期
- 第一頁上沒有頁尾

## 添加頁首和頁尾圖片 {#AddHeaderFooterImage}

```go
func (f *File) AddHeaderFooterImage(sheet string, opts *HeaderFooterImageOptions) error
```

添加可透過 `&G` 控制字符在頁首和頁尾定義中引用的圖片，支援的圖片檔案格式為：EMF、EMZ、GIF、JPEG、JPG、PNG、SVG、TIF、TIFF、WMF 和 WMZ。

## 設定名稱 {#SetDefinedName}

```go
func (f *File) SetDefinedName(definedName *DefinedName) error
```

根據給定的名稱和引用區域設定名稱，默認範圍是活頁簿。例如：

```go
err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    RefersTo: "Sheet1!$A$2:$D$5",
    Comment:  "defined name comment",
    Scope:    "Sheet2",
})
```

工作表的列印區域和列印標題設定:

<p align="center"><img width="628" src="./images/page_setup_01.png" alt="工作表的列印區域和列印標題設定"></p>

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

在設定列印標題時，若將 `RefersTo` 選項的值設定為不包含逗號分隔符的欄範圍引用，將僅對「標題欄」生效。例如：

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$A:$A",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

在設定列印標題時，若將 `RefersTo` 選項的值設定為不包含逗號分隔符的列範圍引用，將僅對「標題列」生效。例如：

```go
if err := f.SetDefinedName(&excelize.DefinedName{
    Name:     "_xlnm.Print_Titles",
    RefersTo: "Sheet1!$1:$1",
    Scope:    "Sheet1",
}); err != nil {
    fmt.Println(err)
}
```

## 獲取名稱 {#GetDefinedName}

```go
func (f *File) GetDefinedName() []DefinedName
```

獲取作用範圍內的活頁簿和工作表的名稱列表。

## 刪除名稱 {#DeleteDefinedName}

```go
func (f *File) DeleteDefinedName(definedName *DefinedName) error
```

根據給定的名稱和名稱作用範圍刪除已定義的名稱，默認名稱的作用範圍為活頁簿。例如：

```go
err := f.DeleteDefinedName(&excelize.DefinedName{
    Name:     "Amount",
    Scope:    "Sheet2",
})
```

## 設定活頁簿應用程式屬性 {#SetAppProps}

```go
func (f *File) SetAppProps(appProperties *AppProperties) error
```

設定活頁簿的應用程式屬性。可以設定的屬性包括:

屬性           | 描述
---|---
Application       | 創建此檔案的應用程式的名稱
ScaleCrop         | 指定檔案縮略圖的顯示方式。設定為 `true` 指定將檔案縮略圖縮放顯示，設定為 `false` 指定將檔案縮略圖剪裁顯示
DocSecurity       | 以數值表示的檔案安全級別。檔案安全定義為: <br>1 - 檔案受密碼保護<br>2 - 建議以只讀方式開啓檔案<br>3 - 強制以只讀方式開啓檔案<br>4 - 檔案批注被鎖定
Company           | 與檔案關聯的公司的名稱
LinksUpToDate     | 設定檔案中的超鏈接是否是最新的。設定為 `true` 表示超鏈接已更新，設定為 `false` 表示超鏈接已過時
HyperlinksChanged | 指定下一次開啓此檔案時是否應使用本部分中指定的新超鏈接更新超鏈接關係
AppVersion        | 指定生成此檔案的應用程式的版本。值應為 XX.YYYY 格式，其中 X 和 Y 代表數值，否則檔案將不符合標準

例如：

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

## 獲取活頁簿應用程式屬性 {#GetAppProps}

```go
func (f *File) GetAppProps() (*AppProperties, error)
```

獲取活頁簿的應用程式屬性。

## 設定檔案屬性 {#SetDocProps}

```go
func (f *File) SetDocProps(docProperties *DocProperties) error
```

設定活頁簿的核心屬性。可以設定的屬性包括:

屬性           | 描述
---|---
Category       | 檔案內容的類別
ContentStatus  | 檔案內容的狀態。例如: 值可能包括 "Draft"、"Reviewed" 和 "Final"
Created        | 使用 ISO 8601 UTC 時間格式表示的檔案創建時間，例如 `2019-06-04T22:00:10Z`
Creator        | 創作者
Description    | 資源內容的說明
Identifier     | 對給定上下文中的資源的明確引用
Keywords       | 檔案關鍵詞
Language       | 檔案內容的主要語言
LastModifiedBy | 執行上次修改的用戶
Modified       | 使用 ISO 8601 UTC 時間格式表示的檔案修改時間，例如 `2019-06-04T22:00:10Z`
Revision       | 檔案修訂版本
Subject        | 檔案主題
Title          | 檔案標題
Version        | 版本號，該值由用戶或應用程式設定

例如：

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

## 獲取檔案屬性 {#GetDocProps}

```go
func (f *File) GetDocProps() (*DocProperties, error)
```

獲取活頁簿的核心屬性。

## 設定自訂屬性 {#SetDocCustomProps}

```go
func (f *File) SetCustomProps(prop CustomProperty) error
```

根據給定的屬性名稱和值設定活頁簿的自訂屬性。如果給定的屬性名稱已經存在，將會更新已存在屬性的值，否則將添加新的屬性。屬性值支持的資料類型為 `int32`、`float64`、`bool`、`string`、`time.Time` 或 `nil`。當設定屬性的值為 `nil` 時，將刪除指定的屬性。當給定的屬性值是不受支持的資料類型時，函數將會返回錯誤。

## 獲取自訂屬性 {#GetDocCustomProps}

```go
func (f *File) GetCustomProps() ([]CustomProperty, error)
```

獲取全部自訂屬性。

## 設定計算屬性 {#SetCalcProps}

```go
func (f *File) SetCalcProps(opts *CalcPropsOptions) error
```

設定活頁簿的計算屬性。

可選屬性 `CalcMode` 的有效值為：`manual`、`auto` 或 `autoNoTable`。

可選屬性 `RefMode` 的有效值為：`A1` 或 `R1C1`。

## 獲取計算屬性 {#GetCalcProps}

```go
func (f *File) GetCalcProps() (CalcPropsOptions, error)
```

獲取活頁簿的計算屬性。

## 保護活頁簿 {#ProtectWorkbook}

```go
func (f *File) ProtectWorkbook(opts *WorkbookProtectionOptions) error
```

使用密碼保護活頁簿的結構，以防止其他用戶查看隱藏的工作表，添加、移動或隱藏工作表以及重命名工作表，選字段 `AlgorithmName` 支援指定哈希算法 XOR、MD4、MD5、SHA-1、SHA-256、SHA-384 或 SHA-512，如果未指定哈希算法，默認使用 XOR 算法。例如，使用密碼保護活頁簿結構：

```go
err := f.ProtectWorkbook(&excelize.WorkbookProtectionOptions{
    Password:      "password",
    LockStructure: true,
})
```

WorkbookProtectionOptions 定義了保護活頁簿的設定選項。

```go
type WorkbookProtectionOptions struct {
    AlgorithmName string
    Password      string
    LockStructure bool
    LockWindows   bool
}
```

## 取消保護活頁簿 {#UnprotectWorkbook}

```go
func (f *File) UnprotectWorkbook(password ...string) error
```

取保護活頁簿，指定可選密碼參數以透過密碼驗證來取消活頁簿保護。

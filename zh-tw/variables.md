# 變數

{{ book.info }}

```go
var (
    // ErrAddVBAProject 定義了向活頁簿嵌入 VBA 專案發生異常時的錯誤提示信息
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrAttrValBool 定義了序列化或反序列化 XML 布爾類型值失敗時的錯誤提示信息
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrCellCharsLength 定義了單個儲存格字符長度超出最大限制時的錯誤提示信息
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrCellStyles 定義了儲存格格式數量超出最大限制時的錯誤提示信息
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrColumnNumber 定義了收到無效欄名時的錯誤提示信息
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth 定義了收到無效欄寬度時的錯誤提示信息
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrCoordinates 定義了收到無效儲存格坐標元組時的錯誤提示信息
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrCustomNumFmt 定義了指定自訂數字格式表達式為空時的錯誤提示信息
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrDataValidationFormulaLength 定義了數據驗證公式長度超出最大限制時錯誤提示信息
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange 定義了指定數據驗證小數範圍無效時的錯誤提示信息
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrDefinedNameDuplicate 定義了在給定範圍內已經存在相同指定名稱時的錯誤提示信息
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrDefinedNameScope 定義了在給定範圍內找不到指定名稱時的錯誤提示信息
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrExistsSheet 定義了檢測到已有相同名稱工作表存在時的錯誤提示信息
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrExistsTableName 定義了給定表格名稱已存在時的錯誤提示信息
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrFontLength 定義了字型名稱長度超出最大限制時的錯誤提示信息
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize 定義了收到無效字號時的錯誤提示信息
    ErrFontSize = fmt.Errorf("font size must be an integer from %d to %d points", MinFontSize, MaxFontSize)
    // ErrFormControlValue 定義了表單控制項捲軸值超過有效範圍時的錯誤提示信息
    ErrFormControlValue = fmt.Errorf("scroll value must be an integer from 0 to %d", MaxFormControlValue)
    // ErrGroupSheets 定義了工作表分組異常時的錯誤提示信息
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrImgExt 定義了不受支援的圖片擴展名的錯誤提示信息
    ErrImgExt = errors.New("unsupported image extension")
    // ErrInvalidFormula 定義了收到無效公式時的錯誤提示信息
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrMaxFilePathLength 定義了活頁簿存儲路徑長度超出最大限制時的錯誤提示信息
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // ErrMaxRowHeight 定義了收到無效列高度時的錯誤提示信息
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrMaxRows 定義了當列號超出最大限制時的錯誤提示信息
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrNameLength 定義了自訂名稱或表格名稱長度超出最大限制時的錯誤提示信息
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrOptionsUnzipSizeLimit 定義了開啓活頁簿時，「用以指定開啓電子錶格檔案時的解壓縮大小限制參數」和「用以指定解壓每個工作表時的記憶體限制參數」產生衝突時的錯誤提示信息
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrOutlineLevel 定義了在數據分組時收到無效級別時的錯誤提示信息
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrPageSetupAdjustTo 定義了在設定工作表頁面配置時頁面縮放比例超出範圍的錯誤提示信息
    ErrPageSetupAdjustTo = errors.New("adjust to value must be an integer from 0 to 400")
    // ErrParameterInvalid 定義了收到無效參數時的錯誤提示信息
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrParameterRequired 定義了必要參數為空時的錯誤提示信息
    ErrParameterRequired = errors.New("parameter is required")
    // ErrPasswordLengthInvalid 定義了密碼長度超出限制時的錯誤提示信息
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrPivotTableClassicLayout 定義了同時開啓 ClassicLayout 與 CompactData 選項創建樞紐分析表時的錯誤提示信息
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // ErrSave 定義了保存活頁簿時的錯誤提示信息
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrSheetIdx 定義了收到了無效工作表索引時的錯誤提示信息
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrSheetNameBlank 定義了收到的工作表名稱為空時的錯誤提示信息
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameInvalid 定義了收到帶有無效字符的工作表名稱時的錯誤提示信息
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameLength 定義了工作表名稱長度超出最大限制時的錯誤提示信息
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrSheetNameSingleQuote 定義了收到的工作表名稱中，第一個或者最後一個字符是單引號時的錯誤提示信息
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSparkline 定義了收到無效走勢圖創建參數時的錯誤提示信息
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineLocation 定義了創建走勢圖參數缺少 Location 欄位時的錯誤提示信息
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange 定義了創建走勢圖參數缺少 Range 欄位時的錯誤提示信息
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparklineStyle 定義了收到無效走勢圖創建樣式參數時的錯誤提示信息
    ErrSparklineStyle = errors.New("parameter 'Style' value must be an integer from 0 to 35")
    // ErrSparklineType 定義了創建走勢圖收到無效參數時的錯誤提示信息
    ErrSparklineType = errors.New("parameter 'Type' value must be one of 'line', 'column' or 'win_loss'")
    // ErrStreamSetColStyle 定義了在流式寫入模式下設定欄樣式時的錯誤提示信息
    ErrStreamSetColStyle = errors.New("must call the SetColStyle function before the SetRow function")
    // ErrStreamSetColWidth 定義了在流式寫入模式下設定欄寬度時的錯誤提示信息
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes 定義了在流式寫入模式下設定窗格時的錯誤提示信息
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrTotalSheetHyperlinks 定義了工作表包含的超鏈接總數超出最大限制時的錯誤提示信息
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrTransparency 定義了透明度超出取值範圍時的錯誤提示信息
    ErrTransparency = errors.New("transparency value must be an integer from 0 to 100")
    // ErrUnknownEncryptMechanism 定義了檢測到未知加密機制時的錯誤提示信息
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnprotectSheet 定義了取消保護工作表時的錯誤提示信息
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword 定義了透過密碼驗證取消保護工作表失敗時的錯誤提示信息
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrUnprotectWorkbook 定義了取消保護活頁簿時的錯誤提示信息
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword 定義了透過密碼驗證取消保護活頁簿失敗時的錯誤提示信息
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrUnsupportedEncryptMechanism 定義了檢測到不受支援的加密機制時的錯誤提示信息
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm 定義了檢測到不受支援的哈希算法時的錯誤提示信息
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat 定義了檢測到不受支援的數字格式時的錯誤提示信息
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrWorkbookFileFormat 定義了不受支援的活頁簿文件類型的錯誤提示信息
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrWorkbookPassword 定義了開啓活頁簿時密碼驗證失敗的錯誤提示信息
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

下列變數定義了 XML 源關係和命名空間列表、相關前綴和引入它的模式：

```go
var (
    NameSpaceDocumentPropertiesVariantTypes = xml.Attr{Name: xml.Name{Local: "vt", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes"}
    NameSpaceDrawing2016SVG                 = xml.Attr{Name: xml.Name{Local: "asvg", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2016/SVG/main"}
    NameSpaceDrawingML                      = xml.Attr{Name: xml.Name{Local: "a", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/main"}
    NameSpaceDrawingMLA14                   = xml.Attr{Name: xml.Name{Local: "a14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2010/main"}
    NameSpaceDrawingMLChart                 = xml.Attr{Name: xml.Name{Local: "c", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/chart"}
    NameSpaceDrawingMLSlicer                = xml.Attr{Name: xml.Name{Local: "sle", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2010/slicer"}
    NameSpaceDrawingMLSlicerX15             = xml.Attr{Name: xml.Name{Local: "sle15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2012/slicer"}
    NameSpaceDrawingMLSpreadSheet           = xml.Attr{Name: xml.Name{Local: "xdr", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"}
    NameSpaceMacExcel2008Main               = xml.Attr{Name: xml.Name{Local: "mx", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/mac/excel/2008/main"}
    NameSpaceSpreadSheet                    = xml.Attr{Name: xml.Name{Local: "xmlns"}, Value: "http://schemas.openxmlformats.org/spreadsheetml/2006/main"}
    NameSpaceSpreadSheetExcel2006Main       = xml.Attr{Name: xml.Name{Local: "xne", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/excel/2006/main"}
    NameSpaceSpreadSheetX14                 = xml.Attr{Name: xml.Name{Local: "x14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2009/9/main"}
    NameSpaceSpreadSheetX15                 = xml.Attr{Name: xml.Name{Local: "x15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2010/11/main"}
    NameSpaceSpreadSheetXR10                = xml.Attr{Name: xml.Name{Local: "xr10", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2016/revision10"}
    SourceRelationship                      = xml.Attr{Name: xml.Name{Local: "r", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/relationships"}
    SourceRelationshipChart20070802         = xml.Attr{Name: xml.Name{Local: "c14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"}
    SourceRelationshipChart2014             = xml.Attr{Name: xml.Name{Local: "c16", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2014/chart"}
    SourceRelationshipChart201506           = xml.Attr{Name: xml.Name{Local: "c16r2", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2015/06/chart"}
    SourceRelationshipCompatibility         = xml.Attr{Name: xml.Name{Local: "mc", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/markup-compatibility/2006"}
)
```

下面的變數定義了索引色彩和 RGB 色值的映射關係。為保證向後相容性，其中值為 0-7 與 8-15 的索引色彩是重復的。索引色彩的值範圍是 0-65。

```go
var IndexedColorMapping = []string{
    "000000", "FFFFFF", "FF0000", "00FF00", "0000FF", "FFFF00", "FF00FF", "00FFFF",
    "000000", "FFFFFF", "FF0000", "00FF00", "0000FF", "FFFF00", "FF00FF", "00FFFF",
    "800000", "008000", "000080", "808000", "800080", "008080", "C0C0C0", "808080",
    "9999FF", "993366", "FFFFCC", "CCFFFF", "660066", "FF8080", "0066CC", "CCCCFF",
    "000080", "FF00FF", "FFFF00", "00FFFF", "800080", "800000", "008080", "0000FF",
    "00CCFF", "CCFFFF", "CCFFCC", "FFFF99", "99CCFF", "FF99CC", "CC99FF", "FFCC99",
    "3366FF", "33CCCC", "99CC00", "FFCC00", "FF9900", "FF6600", "666699", "969696",
    "003366", "339966", "003300", "333300", "993300", "993366", "333399", "333333",
    "000000", "FFFFFF",
}
```

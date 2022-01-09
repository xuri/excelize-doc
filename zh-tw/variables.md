# 變數

```go
var (
    // ErrStreamSetColWidth 定義了在流式寫入模式下設定欄寬度時的錯誤提示信息
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber 定義了收到無效欄名時的錯誤提示信息
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth 定義了收到無效欄寬度時的錯誤提示信息
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel 定義了在數據分組時收到無效級別時的錯誤提示信息
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates 定義了收到無效存儲格坐標元組時的錯誤提示信息
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet 定義了檢測到已有相同名稱工作表存在時的錯誤提示信息
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks 定義了工作表包含的超鏈接總數超出最大限制時的錯誤提示信息
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula 定義了收到無效公式時的錯誤提示信息
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject 定義了向活頁簿嵌入 VBA 專案發生異常時的錯誤提示信息
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows 定義了當列號超出最大限制時的錯誤提示信息
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight 定義了收到無效列高度時的錯誤提示信息
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt 定義了不受支持的圖片擴展名的錯誤提示信息
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength 定義了活頁簿文件名長度超出最大限制時的錯誤提示信息
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt 定義了加密活頁簿時的錯誤提示信息
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism 定義了檢測到未知加密機制時的錯誤提示信息
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism 定義了檢測到不受支持的加密機制時的錯誤提示信息
    ErrUnsupportedEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired 定義了必要參數為空時的錯誤提示信息
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid 定義了收到無效參數時的錯誤提示信息
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope 定義了在給定範圍內找不到指定名稱時的錯誤提示信息
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate 定義了在給定範圍內已經存在相同指定名稱時的錯誤提示信息
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt 定義了指定自定義數字格式表達式為空時的錯誤提示信息
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength 定義了字體名稱長度超出最大限制時的錯誤提示信息
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize 定義了收到無效字號時的錯誤提示信息
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx 定義了收到了無效工作表索引時的錯誤提示信息
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrUnprotectSheet 定義了取消保護工作表時的錯誤提示信息
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword 定義了通過密碼驗證取消保護工作表失敗時的錯誤提示信息
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets 定義了工作表分組異常時的錯誤提示信息
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength 定義了數據驗證公式長度超出最大限制時錯誤提示信息
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange 定義了指定數據驗證小數範圍無效時的錯誤提示信息
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength 定義了單個存儲格字符長度超出最大限制時的錯誤提示信息
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit
    // 定義了打開活頁簿時，「用以指定打開電子錶格檔案時的解壓縮大小限制參數」和「用以指定解壓每個工作表時的內存限制參數」產生衝突時的錯誤提示信息
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave 定義了保存活頁簿時的錯誤提示信息
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool 定義了序列化或反序列化 XML 布爾類型值失敗時的錯誤提示信息
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType 定義了創建走勢圖收到無效參數時的錯誤提示信息
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation 定義了創建走勢圖參數缺少 Location 字段時的錯誤提示信息
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange 定義了創建走勢圖參數缺少 Range 字段時的錯誤提示信息
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline 定義了收到無效走勢圖創建參數時的錯誤提示信息
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle 定義了收到無效走勢圖創建樣式參數時的錯誤提示信息
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
)
```

下列變數定義了 XML 源關係和命名空間列表、相關前綴和引入它的模式：

```go
var (
    SourceRelationship                      = xml.Attr{Name: xml.Name{Local: "r", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/relationships"}
    SourceRelationshipCompatibility         = xml.Attr{Name: xml.Name{Local: "mc", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/markup-compatibility/2006"}
    SourceRelationshipChart20070802         = xml.Attr{Name: xml.Name{Local: "c14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"}
    SourceRelationshipChart2014             = xml.Attr{Name: xml.Name{Local: "c16", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2014/chart"}
    SourceRelationshipChart201506           = xml.Attr{Name: xml.Name{Local: "c16r2", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2015/06/chart"}
    NameSpaceSpreadSheet                    = xml.Attr{Name: xml.Name{Local: "xmlns"}, Value: "http://schemas.openxmlformats.org/spreadsheetml/2006/main"}
    NameSpaceSpreadSheetX14                 = xml.Attr{Name: xml.Name{Local: "x14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2009/9/main"}
    NameSpaceDrawingML                      = xml.Attr{Name: xml.Name{Local: "a", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/main"}
    NameSpaceDrawingMLChart                 = xml.Attr{Name: xml.Name{Local: "c", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/chart"}
    NameSpaceDrawingMLSpreadSheet           = xml.Attr{Name: xml.Name{Local: "xdr", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"}
    NameSpaceSpreadSheetX15                 = xml.Attr{Name: xml.Name{Local: "x15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2010/11/main"}
    NameSpaceSpreadSheetExcel2006Main       = xml.Attr{Name: xml.Name{Local: "xne", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/excel/2006/main"}
    NameSpaceMacExcel2008Main               = xml.Attr{Name: xml.Name{Local: "mx", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/mac/excel/2008/main"}
    NameSpaceDocumentPropertiesVariantTypes = xml.Attr{Name: xml.Name{Local: "vt", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes"}
)
```

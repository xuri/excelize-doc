# 变量

{{ book.info }}

```go
var (
    // ErrAddVBAProject 定义了向工作簿嵌入 VBA 项目发生异常时的错误提示信息
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrAttrValBool 定义了序列化或反序列化 XML 布尔类型值失败时的错误提示信息
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrCellCharsLength 定义了单个单元格字符长度超出最大限制时的错误提示信息
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrCellStyles 定义了单元格格式数量超出最大限制时的错误提示信息
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrColumnNumber 定义了收到无效列名时的错误提示信息
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth 定义了收到无效列宽度时的错误提示信息
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrCoordinates 定义了收到无效单元格坐标元组时的错误提示信息
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrCustomNumFmt 定义了指定自定义数字格式表达式为空时的错误提示信息
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrDataValidationFormulaLength 定义了数据验证公式长度超出最大限制时错误提示信息
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange 定义了指定数据验证小数范围无效时的错误提示信息
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrDefinedNameDuplicate 定义了在给定范围内已经存在相同指定名称时的错误提示信息
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrDefinedNameScope 定义了在给定范围内找不到指定名称时的错误提示信息
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrExistsSheet 定义了检测到已有相同名称工作表存在时的错误提示信息
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrExistsTableName 定义了给定表格名称已存在时的错误提示信息
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrFontLength 定义了字体名称长度超出最大限制时的错误提示信息
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize 定义了收到无效字号时的错误提示信息
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
    // ErrFormControlValue 定义了表单控件滚动值超过有效范围时的错误提示信息
    ErrFormControlValue = fmt.Errorf("scroll value must be between 0 and %d", MaxFormControlValue)
    // ErrGroupSheets 定义了工作表分组异常时的错误提示信息
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrImgExt 定义了不受支持的图片扩展名的错误提示信息
    ErrImgExt = errors.New("unsupported image extension")
    // ErrInvalidFormula 定义了收到无效公式时的错误提示信息
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrMaxFilePathLength 定义了工作簿保存路径长度超出最大限制时的错误提示信息
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // ErrMaxRowHeight 定义了收到无效行高度时的错误提示信息
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrMaxRows 定义了当行号超出最大限制时的错误提示信息
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrNameLength 定义了自定义名称或表格名称长度超出最大限制时的错误提示信息
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrOptionsUnzipSizeLimit 定义了打开工作簿时，“用以指定打开电子表格文档时的解压缩大小限制参数”和“用以指定解压每个工作表时的内存限制参数”产生冲突时的错误提示信息
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrOutlineLevel 定义了在数据分组时收到无效级别时的错误提示信息
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrPageSetupAdjustTo 定义了在设置工作表页面属性时页面缩放比例超出范围的错误提示信息
    ErrPageSetupAdjustTo = errors.New("adjust to value must be between 10 and 400")
    // ErrParameterInvalid 定义了收到无效参数时的错误提示信息
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrParameterRequired 定义了必要参数为空时的错误提示信息
    ErrParameterRequired = errors.New("parameter is required")
    // ErrPasswordLengthInvalid 定义了密码长度超出限制时的错误提示信息
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrPivotTableClassicLayout 定义了同时开启 ClassicLayout 与 CompactData 选项创建数据透视表时的错误提示信息
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // ErrSave 定义了保存工作簿时的错误提示信息
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrSheetIdx 定义了收到了无效工作表索引时的错误提示信息
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrSheetNameBlank 定义了收到的工作表名称为空时的错误提示信息
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameInvalid 定义了收到带有无效字符的工作表名称时的错误提示信息
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameLength 定义了工作表名称长度超出最大限制时的错误提示信息
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrSheetNameSingleQuote 定义了收到的工作表名称中，第一个或者最后一个字符是单引号时的错误提示信息
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSparkline 定义了收到无效迷你图创建参数时的错误提示信息
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineLocation 定义了创建迷你图参数缺少 Location 字段时的错误提示信息
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange 定义了创建迷你图参数缺少 Range 字段时的错误提示信息
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparklineStyle 定义了收到无效迷你图创建样式参数时的错误提示信息
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrSparklineType 定义了创建迷你图收到无效参数时的错误提示信息
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrStreamSetColWidth 定义了在流式写入模式下设置列宽度时的错误提示信息
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes 定义了在流式写入模式下设置窗格时的错误提示信息
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrTotalSheetHyperlinks 定义了工作表包含的超链接总数超出最大限制时的错误提示信息
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrUnknownEncryptMechanism 定义了检测到未知加密机制时的错误提示信息
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnprotectSheet 定义了取消保护工作表时的错误提示信息
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword 定义了通过密码验证取消保护工作表失败时的错误提示信息
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrUnprotectWorkbook 定义了取消保护工作簿时的错误提示信息
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword 定义了通过密码验证取消保护工作簿失败时的错误提示信息
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrUnsupportedEncryptMechanism 定义了检测到不受支持的加密机制时的错误提示信息
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm 定义了检测到不受支持的哈希算法时的错误提示信息
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat 定义了检测到不受支持的数字格式时的错误提示信息
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrWorkbookFileFormat 定义了不受支持的工作簿文件类型的错误提示信息
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrWorkbookPassword 定义了打开工作簿时密码验证失败的错误提示信息
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

下列变量定义了 XML 源关系和命名空间列表、相关前缀和引入它的模式：

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

下面的变量定义了索引颜色和 RGB 色值的映射关系。为保证向后兼容性，其中值为 0-7 与 8-15 的索引颜色是重复的。索引颜色的值范围是 0-65。

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

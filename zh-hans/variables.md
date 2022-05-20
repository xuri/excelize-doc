# 变量

```go
var (
    // ErrStreamSetColWidth 定义了在流式写入模式下设置列宽度时的错误提示信息
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber 定义了收到无效列名时的错误提示信息
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth 定义了收到无效列宽度时的错误提示信息
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel 定义了在数据分组时收到无效级别时的错误提示信息
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates 定义了收到无效单元格坐标元组时的错误提示信息
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet 定义了检测到已有相同名称工作表存在时的错误提示信息
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks 定义了工作表包含的超链接总数超出最大限制时的错误提示信息
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula 定义了收到无效公式时的错误提示信息
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject 定义了向工作簿嵌入 VBA 项目发生异常时的错误提示信息
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows 定义了当行号超出最大限制时的错误提示信息
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight 定义了收到无效行高度时的错误提示信息
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt 定义了不受支持的图片扩展名的错误提示信息
    ErrImgExt = errors.New("unsupported image extension")
    // ErrWorkbookFileFormat 定义了不受支持的工作簿文件类型的错误提示信息
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrMaxFilePathLength 定义了工作簿保存路径长度超出最大限制时的错误提示信息
    ErrMaxFilePathLength = errors.New("file path length exceeds maximum limit")
    // ErrEncrypt 定义了加密工作簿时的错误提示信息
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism 定义了检测到未知加密机制时的错误提示信息
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism 定义了检测到不受支持的加密机制时的错误提示信息
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm 定义了检测到不受支持的哈希算法时的错误提示信息
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat 定义了检测到不受支持的数字格式时的错误提示信息
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrPasswordLengthInvalid 定义了密码长度超出限制时的错误提示信息
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrParameterRequired 定义了必要参数为空时的错误提示信息
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid 定义了收到无效参数时的错误提示信息
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope 定义了在给定范围内找不到指定名称时的错误提示信息
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate 定义了在给定范围内已经存在相同指定名称时的错误提示信息
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt 定义了指定自定义数字格式表达式为空时的错误提示信息
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength 定义了字体名称长度超出最大限制时的错误提示信息
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize 定义了收到无效字号时的错误提示信息
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx 定义了收到了无效工作表索引时的错误提示信息
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrUnprotectSheet 定义了取消保护工作表时的错误提示信息
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword 定义了通过密码验证取消保护工作表失败时的错误提示信息
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets 定义了工作表分组异常时的错误提示信息
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength 定义了数据验证公式长度超出最大限制时错误提示信息
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange 定义了指定数据验证小数范围无效时的错误提示信息
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength 定义了单个单元格字符长度超出最大限制时的错误提示信息
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit
    // 定义了打开工作簿时，“用以指定打开电子表格文档时的解压缩大小限制参数”和
    // “用以指定解压每个工作表时的内存限制参数”产生冲突时的错误提示信息
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave 定义了保存工作簿时的错误提示信息
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool 定义了序列化或反序列化 XML 布尔类型值失败时的错误提示信息
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType 定义了创建迷你图收到无效参数时的错误提示信息
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation 定义了创建迷你图参数缺少 Location 字段时的错误提示信息
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange 定义了创建迷你图参数缺少 Range 字段时的错误提示信息
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline 定义了收到无效迷你图创建参数时的错误提示信息
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle 定义了收到无效迷你图创建样式参数时的错误提示信息
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrWorkbookPassword 定义了打开工作簿时密码验证失败时的错误提示信息
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

下列变量定义了 XML 源关系和命名空间列表、相关前缀和引入它的模式：

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

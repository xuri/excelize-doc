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
    // ErrMaxFileNameLength 定义了工作簿文件名长度超出最大限制时的错误提示信息
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt 定义了加密工作簿时的错误提示信息
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism 定义了检测到未知加密机制时的错误提示信息
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportEncryptMechanism 定义了检测到不受支持的加密机制时的错误提示信息
    ErrUnsupportEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired 定义了必要参数为空时的错误提示信息
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid 定义了收到无效参数时的错误提示信息
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope 定义了在给定范围内找不到指定名称时的错误提示信息
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameduplicate 定义了在给定范围内已经存在相同指定名称时的错误提示信息
    ErrDefinedNameduplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt 定义了指定自定义数字格式表达式为空时的错误提示信息
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength 定义了字体名称长度超出最大限制时的错误提示信息
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize 定义了收到无效字号时的错误提示信息
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx 定义了收到了无效工作表索引时的错误提示信息
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets 定义了工作表分组异常时的错误提示信息
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLenth 定义了数据验证公式长度超出最大限制时错误提示信息
    ErrDataValidationFormulaLenth = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange 定义了指定数据验证小数范围无效时的错误提示信息
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength 定义了单个单元格字符长度超出最大限制时的错误提示信息
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit
    // 定义了打开工作簿时，“用以指定打开电子表格文档时的解压缩大小限制参数”和“用以指定解压每个工作表时的内存限制参数”产生冲突时的错误提示信息
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to WorksheetUnzipMemLimit")
)
```

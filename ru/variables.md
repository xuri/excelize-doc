# Переменные

```go
var (
    // ErrStreamSetColWidth определяет сообщение об ошибке при установке
    // ширины столбца в режиме записи потока.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber определил сообщение об ошибке при получении
    // недопустимого номера столбца.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth определяет сообщение об ошибке при получении
    // недопустимой ширины столбца.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel определил сообщение об ошибке при получении
    // недопустимого номера уровня структуры.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates определила сообщение об ошибке при недопустимой длине
    // кортежей координат.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet определил сообщение об ошибке на заданном листе,
    // который уже существует.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks определил сообщение об ошибке при переполнении
    // счетчика гиперссылок.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula определил сообщение об ошибке при получении
    // недопустимой формулы.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject определил сообщение об ошибке при добавлении проекта
    // VBA в книгу.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows определил сообщение об ошибке при получении номера строки,
    // превышающей максимальный предел.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight определил сообщение об ошибке при получении
    // недопустимой высоты строки.
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt определил сообщение об ошибке при получении неподдерживаемого
    // расширения изображения.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength определяет сообщение об ошибке при получении
    // переполнения длины имени файла.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt определил сообщение об ошибке в электронной таблице
    // шифрования.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism определил сообщение об ошибке для
    // неподдерживаемого механизма шифрования.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism определил сообщение об ошибке для
    // неподдерживаемого механизма шифрования.
    ErrUnsupportedEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired определяет сообщение об ошибке при получении
    // пустого параметра.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid определяет сообщение об ошибке при получении
    // недопустимого параметра.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope определил сообщение об ошибке для не найденного
    // определенного имени в данной области.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate определил сообщение об ошибке с тем же именем,
    // которое уже существует в области.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt определил сообщение об ошибке при получении пустого
    // пользовательского числового формата.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength определил сообщение об ошибке о длине переполнения имени
    // семейства шрифтов.
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize определил сообщение об ошибке о недопустимом размере шрифта.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx определил сообщение об ошибке при получении недопустимого
    // индекса рабочего листа.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets определила сообщение об ошибке на групповых листах.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength определил сообщение об ошибке для
    // получения длины формулы проверки данных, превышающей лимит.
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange определил, что сообщение об ошибке в заданном
    // десятичном диапазоне превышает предел.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength определил сообщение об ошибке для получения длины
    // символа ячейки, превышающей лимит.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit определяет значение ошибки для получения
    // UnzipSizeLimit и UnzipXMLSizeLimit без ограничений.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
)
```

Исходные отношения и список пространств имен, связанные префиксы и схема, в которой они были представлены:

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


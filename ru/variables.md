# Переменные

```go
var (
    // ErrStreamSetColWidth определяет сообщение об ошибке при установке
    // ширины столбца в режиме записи потока
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber определил сообщение об ошибке при получении
    // недопустимого номера столбца
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth определяет сообщение об ошибке при получении
    // недопустимой ширины столбца
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel определил сообщение об ошибке при получении
    // недопустимого номера уровня структуры
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates определила сообщение об ошибке при недопустимой длине
    // кортежей координат
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsSheet определил сообщение об ошибке на заданном листе,
    // который уже существует
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrTotalSheetHyperlinks определил сообщение об ошибке при переполнении
    // счетчика гиперссылок
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula определил сообщение об ошибке при получении
    // недопустимой формулы
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject определил сообщение об ошибке при добавлении проекта
    // VBA в книгу
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows определил сообщение об ошибке при получении номера строки,
    // превышающей максимальный предел
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight определил сообщение об ошибке при получении
    // недопустимой высоты строки
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrImgExt определил сообщение об ошибке при получении неподдерживаемого
    // расширения изображения
    ErrImgExt = errors.New("unsupported image extension")
    // ErrWorkbookFileFormat определил сообщение об ошибке при получении
    // неподдерживаемого формата файла рабочей книги
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrMaxFilePathLength определяет сообщение об ошибке при получении
    // переполнения длины имени файла
    ErrMaxFilePathLength = errors.New("file path length exceeds maximum limit")
    // ErrUnknownEncryptMechanism определил сообщение об ошибке для
    // неподдерживаемого механизма шифрования
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism определил сообщение об ошибке для
    // неподдерживаемого механизма шифрования
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm определяет сообщение об ошибке для
    // неподдерживаемого алгоритма хеширования
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat определяет сообщение об ошибке в
    // неподдерживаемом выражении числового формата
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrPasswordLengthInvalid определяет сообщение об ошибке при неверной
    // длине пароля
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrParameterRequired определяет сообщение об ошибке при получении
    // пустого параметра
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid определяет сообщение об ошибке при получении
    // недопустимого параметра
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope определил сообщение об ошибке для не найденного
    // определенного имени в данной области
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate определил сообщение об ошибке с тем же именем,
    // которое уже существует в области
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt определил сообщение об ошибке при получении пустого
    // пользовательского числового формата
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength определил сообщение об ошибке о длине переполнения имени
    // семейства шрифтов
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize определил сообщение об ошибке о недопустимом размере шрифта
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
    // ErrSheetIdx определил сообщение об ошибке при получении недопустимого
    // индекса рабочего листа
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrUnprotectSheet определил, что сообщение об ошибке на листе не имеет защиты
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword определил сообщение об ошибке при удалении
    // защиты листа с ошибкой проверки пароля
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets определила сообщение об ошибке на групповых листах
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength определил сообщение об ошибке для
    // получения длины формулы проверки данных, превышающей лимит
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange определил, что сообщение об ошибке в заданном
    // десятичном диапазоне превышает предел
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength определил сообщение об ошибке для получения длины
    // символа ячейки, превышающей лимит
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit определяет значение ошибки для получения
    // UnzipSizeLimit и UnzipXMLSizeLimit без ограничений
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave определил сообщение об ошибке для сохранения файла
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool определил сообщение об ошибке для атрибута XML маршала и демаршала логического типа
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType определил сообщение об ошибке при получении недопустимых параметров спарклайна 'Type'
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation определил сообщение об ошибке при отсутствующих параметрах 'Location'
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange определил сообщение об ошибке при отсутствующих параметрах спарклайна 'Range'
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline определил сообщение об ошибке при получении недопустимых параметров спарклайна
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle определяет сообщение об ошибке при получении
    // недопустимых параметров 'Style' спарклайна
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrWorkbookPassword определил сообщение об ошибке при получении
    // неправильного пароля рабочей книги
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
    // ErrSheetNameInvalid определяет сообщение об ошибке при получении имени
    // листа, содержащего недопустимые символы
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameSingleQuote определял сообщение об ошибке, когда первый или
    // последний символ имени листа был одинарной кавычкой
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSheetNameBlank определяет сообщение об ошибке при получении имени
    // пустого листа
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameLength определяет сообщение об ошибке при получении длины
    // имени листа, превышающей лимит
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrUnprotectWorkbook определил, что сообщение об ошибке в рабочей книге
    // не имеет защиты
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword определил сообщение об ошибке при удалении
    // защиты книги с ошибкой проверки пароля
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
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

IndexedColorMapping — это таблица сопоставлений по умолчанию индексированного значения цвета со значением RGB. Обратите внимание, что 0–7 избыточны по сравнению с 8–15 для сохранения обратной совместимости. Устаревшая схема индексации цветов, которая по-прежнему требуется для некоторых записей, а также для обратной совместимости с устаревшими форматами. Этот элемент содержит последовательность значений цвета RGB, соответствующих цветовым индексам (начиная с нуля). При использовании индексированной цветовой палитры по умолчанию значения не записываются, а подразумеваются. Если цветовая палитра изменена по сравнению со стандартной, записывается вся цветовая палитра.

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

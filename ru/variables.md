# Переменные

```go
var (
    // ErrStreamSetColWidth defined the error message on set column width in
    // stream writing mode.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber defined the error message on receive an invalid column
    // number.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth defined the error message on receive an invalid column
    // width.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel defined the error message on receive an invalid outline
    // level number.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates defined the error message on invalid coordinates tuples
    // length.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet defined the error message on given worksheet already
    // exists.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks defined the error message on hyperlinks count
    // overflow.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula defined the error message on receive an invalid
    // formula.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject defined the error message on add the VBA project in
    // the workbook.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows defined the error message on receive a row number exceeds maximum limit.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight defined the error message on receive an invalid row
    // height.
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt defined the error message on receive an unsupported image
    // extension.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength defined the error message on receive the file name
    // length overflow.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt defined the error message on encryption spreadsheet.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism defined the error message on unsupport
    // encryption mechanism.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportEncryptMechanism defined the error message on unsupport
    // encryption mechanism.
    ErrUnsupportEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired defined the error message on receive the empty
    // parameter.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid defined the error message on receive the invalid
    // parameter.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope defined the error message on not found defined name
    // in the given scope.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameduplicate defined the error message on the same name
    // already exists on the scope.
    ErrDefinedNameduplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt defined the error message on receive the empty custom number format.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength defined the error message on the length of the font
    // family name overflow.
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize defined the error message on the size of the font is invalid.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx defined the error message on receive the invalid worksheet
    // index.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets defined the error message on group sheets.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLenth defined the error message for receiving a
    // data validation formula length that exceeds the limit.
    ErrDataValidationFormulaLenth = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange defined the error message on set decimal range
    // exceeds limit.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength defined the error message for receiving a cell
    // characters length that exceeds the limit.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit defined the error message for receiving
    // invalid UnzipSizeLimit and WorksheetUnzipMemLimit.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to WorksheetUnzipMemLimit")
)
```

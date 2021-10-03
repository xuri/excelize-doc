# Variablen

```go
var (
    // ErrStreamSetColWidth definierte die Fehlermeldung beim Setzen der
    // Spaltenbreite im Stream-Schreibmodus.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber definiert die Fehlermeldung beim Empfang einer ungültigen
    // Spaltennummer.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth definiert die Fehlermeldung beim Empfang einer ungültigen
    // Spaltenbreite.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel definierte die Fehlermeldung beim Empfang einer ungültigen
    // Gliederungsebenennummer.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates definierte die Fehlermeldung bei ungültiger
    // Koordinatentupellänge.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet definierte die Fehlermeldung für ein bestimmtes,
    // bereits vorhandenes Arbeitsblatt.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks definierte die Fehlermeldung zum
    // Hyperlink-Zählerüberlauf.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula hat die Fehlermeldung beim Empfang einer ungültigen
    // Formel definiert.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject definierte die Fehlermeldung beim Hinzufügen des
    // VBA-Projekts zur Arbeitsmappe.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows definiert die Fehlermeldung beim Empfangen einer Zeilennummer,
    // die das maximale Limit überschreitet.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight definiert die Fehlermeldung beim Empfang einer ungültigen
    // Zeilenhöhe.
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt hat die Fehlermeldung beim Empfang einer nicht unterstützten
    // Bilderweiterung definiert.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength definiert die Fehlermeldung beim Empfang des
    // Dateinamenlängenüberlaufs.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt hat die Fehlermeldung in der Verschlüsselungstabelle
    // definiert.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism hat die Fehlermeldung zu einem nicht
    // unterstützten Verschlüsselungsmechanismus definiert.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportEncryptMechanism hat die Fehlermeldung zu einem nicht
    // unterstützten Verschlüsselungsmechanismus definiert.
    ErrUnsupportEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired definiert die Fehlermeldung beim Empfang des leeren
    // Parameters.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid hat die Fehlermeldung beim Empfang des ungültigen
    // Parameters definiert.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope hat die Fehlermeldung für den nicht gefundenen
    // definierten Namen im angegebenen Bereich definiert.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameduplicate hat die Fehlermeldung für denselben Namen
    // definiert, der bereits im Bereich vorhanden ist.
    ErrDefinedNameduplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt hat die Fehlermeldung beim Empfang des leeren
    // benutzerdefinierten Zahlenformats definiert.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength definiert die Fehlermeldung zur Länge des Überlaufs des
    // Schriftfamiliennamens.
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize definiert die Fehlermeldung über die Größe der Schriftart ist
    // ungültig.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx hat die Fehlermeldung beim Empfang des ungültigen
    // Arbeitsblattindex definiert.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets definierte die Fehlermeldung auf Gruppenblättern.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLenth definiert die Fehlermeldung für den Empfang
    // einer Datenvalidierungsformellänge, die den Grenzwert überschreitet.
    ErrDataValidationFormulaLenth = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange definiert die Fehlermeldung, dass ein eingestellter
    // Dezimalbereich den Grenzwert überschreitet.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength definiert die Fehlermeldung für den Empfang einer Länge
    // eines Zellenzeichens, die das Limit überschreitet.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit definierte die Fehlermeldung für den Empfang von
    // ungültigem UnzipSizeLimit und WorksheetUnzipMemLimit.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to WorksheetUnzipMemLimit")
)
```

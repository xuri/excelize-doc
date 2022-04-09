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
    // ErrWorkbookExt hat die Fehlermeldung beim Empfang einer nicht
    // unterstützten Arbeitsmappenerweiterung definiert.
    ErrWorkbookExt = errors.New("unsupported workbook extension")
    // ErrMaxFileNameLength definiert die Fehlermeldung beim Empfang des
    // Dateinamenlängenüberlaufs.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt hat die Fehlermeldung in der Verschlüsselungstabelle
    // definiert.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism hat die Fehlermeldung zu einem nicht
    // unterstützten Verschlüsselungsmechanismus definiert.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism hat die Fehlermeldung zu einem nicht
    // unterstützten Verschlüsselungsmechanismus definiert.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm definiert die Fehlermeldung zu einem nicht
    // unterstützten Hash-Algorithmus.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat hat die Fehlermeldung für einen nicht
    // unterstützten Zahlenformatausdruck definiert.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrPasswordLengthInvalid definiert die Fehlermeldung bei ungültiger
    // Passwortlänge.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
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
    // ErrUnprotectSheet definiert die Fehlermeldung auf dem Arbeitsblatt hat
    // keinen Schutz gesetzt.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword hat die Fehlermeldung beim Entfernen des
    // Blattschutzes mit fehlgeschlagener Kennwortüberprüfung definiert.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets definierte die Fehlermeldung auf Gruppenblättern.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength definiert die Fehlermeldung für den Empfang
    // einer Datenvalidierungsformellänge, die den Grenzwert überschreitet.
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange definiert die Fehlermeldung, dass ein eingestellter
    // Dezimalbereich den Grenzwert überschreitet.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength definiert die Fehlermeldung für den Empfang einer Länge
    // eines Zellenzeichens, die das Limit überschreitet.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit definierte die Fehlermeldung für den Empfang von
    // ungültigem UnzipSizeLimit und UnzipXMLSizeLimit.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave definiert die Fehlermeldung zum Speichern der Datei.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool hat die Fehlermeldung für das XML-Attribut vom Typ
    // Marshall und Unmarshal vom Typ Boolean definiert.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType definierte die Fehlermeldung beim Empfang der
    // ungültigen Sparkline-'Type'-Parameter.
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation hat die Fehlermeldung bei fehlenden
    // 'Location'-Parametern definiert.
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange hat die Fehlermeldung bei fehlenden
    // Sparkline-'Range'-Parametern definiert.
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline hat die Fehlermeldung beim Empfang der ungültigen
    // Sparkline-Parameter definiert.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle definiert die Fehlermeldung beim Empfang der
    // ungültigen Sparkline-'Style'-Parameter.
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
)
```

Quellbeziehung und Namespace-Liste, zugehörige Präfixe und Schema, in dem sie eingeführt wurde:

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

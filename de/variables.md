# Variablen

```go
var (
    // ErrStreamSetColWidth definierte die Fehlermeldung beim Setzen der
    // Spaltenbreite im Stream-Schreibmodus.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes hat die Fehlermeldung für festgelegte Bereiche im
    // Stream-Schreibmodus definiert.
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrColumnNumber definiert die Fehlermeldung beim Empfang einer ungültigen
    // Spaltennummer.
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth definiert die Fehlermeldung beim Empfang einer ungültigen
    // Spaltenbreite.
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel definierte die Fehlermeldung beim Empfang einer ungültigen
    // Gliederungsebenennummer.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates definierte die Fehlermeldung bei ungültiger
    // Koordinatentupellänge.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsSheet definierte die Fehlermeldung für ein bestimmtes,
    // bereits vorhandenes Arbeitsblatt.
    ErrExistsSheet = errors.New("the same name sheet already exists")
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
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrImgExt hat die Fehlermeldung beim Empfang einer nicht unterstützten
    // Bilderweiterung definiert.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrWorkbookFileFormat definiert die Fehlermeldung beim Empfang eines
    // nicht unterstützten Arbeitsmappendateiformats.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrMaxFilePathLength definierte die Fehlermeldung beim Empfang des
    // Dateipfadlängenüberlaufs.
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
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
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize definiert die Fehlermeldung über die Größe der Schriftart ist
    // ungültig.
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
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
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
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
    // ErrWorkbookPassword definiert die Fehlermeldung beim Erhalt des falschen
    // Arbeitsmappenpassworts.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
    // ErrSheetNameInvalid hat die Fehlermeldung definiert, wenn der Blattname
    // ungültige Zeichen enthält.
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameSingleQuote definierte die Fehlermeldung, dass das erste oder
    // letzte Zeichen des Blattnamens ein einfaches Anführungszeichen war.
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSheetNameBlank definiert die Fehlermeldung beim Empfang des leeren
    // Blattnamens.
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameLength definierte die Fehlermeldung beim Empfang der Länge
    // des Blattnamens überschreitet das Limit.
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrNameLength definierte die Fehlermeldung beim Empfang des definierten
    // Namens oder die Länge des Tabellennamens überschreitet den Grenzwert.
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrExistsTableName hat die Fehlermeldung definiert, dass die angegebene
    // Tabelle bereits vorhanden ist.
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrCellStyles hat definiert, dass die Fehlermeldung zu Zellstilen den
    // Grenzwert überschreitet.
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrUnprotectWorkbook definiert die Fehlermeldung auf Arbeitsmappe hat
    // keinen Schutz gesetzt.
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword definierte die Fehlermeldung zum Entfernen
    // des Arbeitsmappenschutzes mit fehlgeschlagener Kennwortüberprüfung.
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrorFormControlValue definierte die Fehlermeldung für den Empfang eines
    // Bildlaufwerts, der den Grenzwert überschreitet.
    ErrorFormControlValue = fmt.Errorf("scroll value must be between 0 and %d", MaxFormControlValue)
)
```

Quellbeziehung und Namespace-Liste, zugehörige Präfixe und Schema, in dem sie eingeführt wurde:

```go
var (
    NameSpaceDocumentPropertiesVariantTypes = xml.Attr{Name: xml.Name{Local: "vt", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes"}
    NameSpaceDrawing2016SVG                 = xml.Attr{Name: xml.Name{Local: "asvg", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2016/SVG/main"}
    NameSpaceDrawingML                      = xml.Attr{Name: xml.Name{Local: "a", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/main"}
    NameSpaceDrawingMLChart                 = xml.Attr{Name: xml.Name{Local: "c", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/chart"}
    NameSpaceDrawingMLSpreadSheet           = xml.Attr{Name: xml.Name{Local: "xdr", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"}
    NameSpaceMacExcel2008Main               = xml.Attr{Name: xml.Name{Local: "mx", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/mac/excel/2008/main"}
    NameSpaceSpreadSheet                    = xml.Attr{Name: xml.Name{Local: "xmlns"}, Value: "http://schemas.openxmlformats.org/spreadsheetml/2006/main"}
    NameSpaceSpreadSheetExcel2006Main       = xml.Attr{Name: xml.Name{Local: "xne", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/excel/2006/main"}
    NameSpaceSpreadSheetX14                 = xml.Attr{Name: xml.Name{Local: "x14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2009/9/main"}
    NameSpaceSpreadSheetX15                 = xml.Attr{Name: xml.Name{Local: "x15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2010/11/main"}
    SourceRelationship                      = xml.Attr{Name: xml.Name{Local: "r", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/relationships"}
    SourceRelationshipChart20070802         = xml.Attr{Name: xml.Name{Local: "c14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"}
    SourceRelationshipChart2014             = xml.Attr{Name: xml.Name{Local: "c16", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2014/chart"}
    SourceRelationshipChart201506           = xml.Attr{Name: xml.Name{Local: "c16r2", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2015/06/chart"}
    SourceRelationshipCompatibility         = xml.Attr{Name: xml.Name{Local: "mc", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/markup-compatibility/2006"}
)
```

IndexedColorMapping ist die Tabelle der Standardzuordnungen vom indizierten Farbwert zum RGB-Wert. Beachten Sie, dass 0-7 redundant zu 8-15 sind, um die Abwärtskompatibilität zu wahren. Ein Legacy-Indexierungsschema für Farben, das für einige Datensätze noch erforderlich ist, und für die Abwärtskompatibilität mit Legacy-Formaten. Dieses Element enthält eine Folge von RGB-Farbwerten, die Farbindizes entsprechen (nullbasiert). Bei Verwendung der standardmäßig indizierten Farbpalette werden die Werte nicht ausgeschrieben, sondern impliziert. Wenn die Farbpalette von der Voreinstellung geändert wurde, wird die gesamte Farbpalette ausgeschrieben.

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

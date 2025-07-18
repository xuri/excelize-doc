# Variabili

```go
var (
    // ErrAddVBAProject ha definito il messaggio di errore sull'aggiunta del progetto VBA nella cartella di lavoro.
    ErrAddVBAProject = errors.New("unsupported VBA project")
    // ErrAttrValBool ha definito il messaggio di errore sull'attributo XML di tipo booleano marshal e unmarshal.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrCellCharsLength ha definito il messaggio di errore per la ricezione di una lunghezza di caratteri di cella che supera il limite.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrCellStyles ha definito che il messaggio di errore sugli stili di cella supera il limite.
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrColumnNumber ha definito il messaggio di errore alla ricezione di un numero di colonna non valido.
    ErrColumnNumber = fmt.Errorf("the column number must be greater than or equal to %d and less than or equal to %d", MinColumns, MaxColumns)
    // ErrColumnWidth ha definito il messaggio di errore alla ricezione di una larghezza di colonna non valida.
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrCoordinates ha definito il messaggio di errore sulla lunghezza delle tuple di coordinate non valide.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrCustomNumFmt ha definito il messaggio di errore alla ricezione del formato numero personalizzato vuoto.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrDataValidationFormulaLength ha definito il messaggio di errore per la ricezione di una lunghezza della formula di convalida dei dati che supera il limite.
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange ha definito il messaggio di errore relativo all'intervallo decimale impostato che supera il limite.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrDefinedNameDuplicate ha definito che il messaggio di errore con lo stesso nome esiste già nell'ambito.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrDefinedNameScope ha definito il messaggio di errore relativo al nome definito non trovato nell'ambito specificato.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrExistsSheet ha definito che il messaggio di errore su un determinato foglio esiste già.
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrExistsTableName ha definito che il messaggio di errore sulla tabella specificata esiste già.
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrFontLength ha definito il messaggio di errore sulla lunghezza dell'overflow del nome della famiglia di caratteri.
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize ha definito il messaggio di errore relativo alla dimensione del carattere non valido.
    ErrFontSize = fmt.Errorf("font size must be an integer from %d to %d points", MinFontSize, MaxFontSize)
    // ErrFormControlValue ha definito il messaggio di errore per la ricezione di un valore di scorrimento che supera il limite.
    ErrFormControlValue = fmt.Errorf("scroll value must be an integer from 0 to %d", MaxFormControlValue)
    // ErrGroupSheets ha definito il messaggio di errore sui fogli di gruppo.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrImgExt ha definito il messaggio di errore alla ricezione di un'estensione immagine non supportata.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrInvalidFormula ha definito il messaggio di errore alla ricezione di una formula non valida.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrMaxFilePathLength ha definito il messaggio di errore alla ricezione dell'overflow della lunghezza del percorso del file.
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // ErrMaxRowHeight ha definito il messaggio di errore alla ricezione di un'altezza di riga non valida.
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrMaxRows ha definito il messaggio di errore alla ricezione di un numero di riga che supera il limite massimo.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrNameLength ha definito il messaggio di errore alla ricezione del nome definito o la lunghezza del nome della tabella supera il limite.
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrOptionsUnzipSizeLimit ha definito il messaggio di errore per la ricezione di UnzipSizeLimit e UnzipXMLSizeLimit non validi.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrOutlineLevel ha definito il messaggio di errore alla ricezione di un numero di livello di struttura non valido.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrPageSetupAdjustTo ha definito il messaggio di errore per la ricezione di una regolazione dell'impostazione di pagina in base al valore che supera il limite.
    ErrPageSetupAdjustTo = errors.New("adjust to value must be an integer from 0 to 400")
    // ErrParameterInvalid ha definito il messaggio di errore alla ricezione del parametro non valido.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrParameterRequired ha definito il messaggio di errore alla ricezione del parametro vuoto.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrPasswordLengthInvalid ha definito il messaggio di errore sulla lunghezza della password non valida.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrPivotTableClassicLayout ha definito il messaggio di errore quando si abilitano ClassicLayout e CompactData contemporaneamente.
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // ErrSave ha definito il messaggio di errore per il salvataggio del file.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrSheetIdx ha definito il messaggio di errore alla ricezione dell'indice del foglio di lavoro non valido.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrSheetNameBlank ha definito il messaggio di errore alla ricezione del nome del foglio vuoto.
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameInvalid ha definito il messaggio di errore alla ricezione, il nome del foglio contiene caratteri non validi.
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameLength ha definito il messaggio di errore alla ricezione della lunghezza del nome del foglio che supera il limite.
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrSheetNameSingleQuote ha definito che il messaggio di errore relativo al primo o all'ultimo carattere del nome del foglio era una virgoletta singola.
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSparkline ha definito il messaggio di errore alla ricezione di parametri sparkline non validi.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineLocation ha definito il messaggio di errore sui parametri di posizione mancanti
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange ha definito il messaggio di errore sui parametri dell'intervallo sparkline mancanti
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparklineStyle ha definito il messaggio di errore alla ricezione di parametri di stile sparkline non validi.
    ErrSparklineStyle = errors.New("parameter 'Style' value must be an integer from 0 to 35")
    // ErrSparklineType ha definito il messaggio di errore alla ricezione di parametri di tipo sparkline non validi.
    ErrSparklineType = errors.New("parameter 'Type' value must be one of 'line', 'column' or 'win_loss'")
    // ErrStreamSetColStyle ha definito il messaggio di errore durante l'impostazione dello stile della colonna in modalità di scrittura del flusso.
    ErrStreamSetColStyle = errors.New("must call the SetColStyle function before the SetRow function")
    // ErrStreamSetColWidth ha definito il messaggio di errore sulla larghezza della colonna impostata nella modalità di scrittura del flusso.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes ha definito il messaggio di errore sui riquadri impostati in modalità di scrittura del flusso.
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrTotalSheetHyperlinks ha definito il messaggio di errore sull'overflow del conteggio dei collegamenti ipertestuali.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrTransparency ha definito il messaggio di errore per la ricezione di un valore di trasparenza che supera il limite.
    ErrTransparency = errors.New("transparency value must be an integer from 0 to 100")
    // ErrUnknownEncryptMechanism ha definito il messaggio di errore sul meccanismo di crittografia non supportato.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnprotectSheet ha definito che il messaggio di errore sul foglio di lavoro non ha impostato alcuna protezione.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword ha definito il messaggio di errore relativo alla rimozione della protezione del foglio con verifica della password non riuscita.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrUnprotectWorkbook ha definito che il messaggio di errore sulla cartella di lavoro non ha impostato alcuna protezione.
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword ha definito il messaggio di errore relativo alla rimozione della protezione della cartella di lavoro con verifica della password non riuscita.
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrUnsupportedEncryptMechanism ha definito il messaggio di errore sul meccanismo di crittografia non supportato.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm ha definito il messaggio di errore sull'algoritmo hash non supportato.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat ha definito il messaggio di errore sull'espressione del formato numerico non supportato.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrWorkbookFileFormat ha definito il messaggio di errore sulla ricezione di un formato file di cartella di lavoro non supportato.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrWorkbookPassword ha definito il messaggio di errore alla ricezione della password errata della cartella di lavoro.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

Relazione di origine ed elenco degli spazi dei nomi, prefissi associati e schema in cui è stato introdotto:

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

IndexedColorMapping è la tabella delle mappature predefinite dal valore del colore indicizzato al valore RGB. Tieni presente che 0-7 sono ridondanti di 8-15 per preservare la compatibilità con le versioni precedenti. Uno schema di indicizzazione legacy per i colori che è ancora richiesto per alcuni record e per la compatibilità con i formati legacy. Questo elemento contiene una sequenza di valori di colore RGB che corrispondono agli indici di colore (in base zero). Quando si utilizza la tavolozza dei colori indicizzati predefinita, i valori non vengono scritti, ma sono invece impliciti. Quando la tavolozza dei colori è stata modificata rispetto a quella predefinita, viene scritta l'intera tavolozza dei colori.

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

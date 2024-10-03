# Variables

```go
var (
    // ErrAddVBAProject a défini le message d'erreur lors de l'ajout du projet VBA dans le classeur.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrAttrValBool a défini le message d'erreur sur l'attribut XML de type booléen marshal et unmarshal.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrCellCharsLength a défini le message d'erreur pour la réception d'une longueur de caractère de cellule qui dépasse la limite.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrCellStyles defined the error message on cell styles exceeds the limit.
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrColumnNumber a défini le message d'erreur lors de la réception d'un numéro de colonne invalide.
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth a défini le message d'erreur lors de la réception d'une largeur de colonne non valide.
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrCoordinates a défini le message d'erreur sur la longueur des tuples de coordonnées non valides.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrCustomNumFmt a défini le message d'erreur lors de la réception du format de nombre personnalisé vide.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrDataValidationFormulaLength a défini le message d'erreur pour la réception d'une longueur de formule de validation de données qui dépasse la limite.
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange a défini le message d'erreur sur une plage décimale définie dépassant la limite.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrDefinedNameDuplicate a défini le message d'erreur sur le même nom qui existe déjà sur l'étendue.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrDefinedNameScope a défini le message d'erreur sur le nom défini introuvable dans la portée donnée.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrExistsSheet a défini le message d'erreur sur une feuille de calcul donnée qui existe déjà.
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrExistsTableName a défini que le message d'erreur sur la table donnée existe déjà.
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrFontLength a défini le message d'erreur sur la longueur du débordement du nom de famille de police.
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize a défini le message d'erreur sur la taille de la police n'est pas valide.
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
    // ErrFormControlValue a défini le message d'erreur pour la réception d'une valeur de défilement dépassant la limite.
    ErrFormControlValue = fmt.Errorf("scroll value must be between 0 and %d", MaxFormControlValue)
    // ErrGroupSheets a défini le message d'erreur sur les feuilles de groupe.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrImgExt a défini le message d'erreur lors de la réception d'une extension d'image non prise en charge.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrInvalidFormula a défini le message d'erreur lors de la réception d'une formule invalide.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrMaxFilePathLength a défini le message d'erreur lors de la réception du dépassement de longueur de nom de fichier.
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // ErrMaxRowHeight a défini le message d'erreur lors de la réception d'une hauteur de ligne invalide.
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrMaxRows a défini le message d'erreur lors de la réception d'un numéro de ligne qui dépasse la limite maximale.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrNameLength a défini le message d'erreur lors de la réception du nom défini ou la longueur du nom de table dépasse la limite.
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrOptionsUnzipSizeLimit a défini le message d'erreur pour la réception d'UnzipSizeLimit et de UnzipXMLSizeLimit non valides.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrOutlineLevel a défini le message d'erreur lors de la réception d'un numéro de niveau hiérarchique non valide.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrParameterInvalid a défini le message d'erreur lors de la réception du paramètre invalide.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrParameterRequired a défini le message d'erreur lors de la réception du paramètre vide.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrPasswordLengthInvalid a défini le message d'erreur sur la longueur du mot de passe non valide.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrPivotTableClassicLayout a défini le message d'erreur lors de l'activation simultanée de ClassicLayout et CompactData.
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // ErrSave a défini le message d'erreur pour l'enregistrement du fichier.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrSheetIdx a défini le message d'erreur lors de la réception de l'index de feuille de calcul non valide.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrSheetNameBlank a défini le message d'erreur lors de la réception du nom de la feuille vierge.
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameInvalid a défini le message d'erreur lors de la réception du nom de la feuille contenant des caractères non valides.
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameLength défini le message d'erreur lors de la réception de la longueur du nom de la feuille dépasse la limite.
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrSheetNameSingleQuote défini le message d'erreur sur le premier ou le dernier caractère du nom de la feuille était un guillemet simple.
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSparkline a défini le message d'erreur lors de la réception des paramètres de sparkline non valides.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineLocation a défini le message d'erreur sur les paramètres 'Location' manquants.
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange a défini le message d'erreur sur les paramètres manquants de sparkline 'Range'.
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparklineStyle a défini le message d'erreur lors de la réception des paramètres 'Style' de sparkline non valides.
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrSparklineType a défini le message d'erreur lors de la réception des paramètres de type sparkline non valides.
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrStreamSetColWidth a défini le message d'erreur sur la largeur de colonne définie en mode d'écriture de flux.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes a défini le message d'erreur sur les volets définis en mode d'écriture de flux.
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrTotalSheetHyperlinks a défini le message d'erreur sur le dépassement du nombre de liens hypertexte.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrUnknownEncryptMechanism a défini le message d'erreur sur un mécanisme de chiffrement non pris en charge.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnprotectSheet a défini que le message d'erreur sur la feuille de calcul n'a défini aucune protection.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword a défini le message d'erreur lors de la suppression de la protection de la feuille avec échec de la vérification du mot de passe.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrUnprotectWorkbook a défini le message d'erreur sur le classeur n'a défini aucune protection.
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword a défini le message d'erreur lors de la suppression de la protection du classeur avec échec de la vérification du mot de passe.
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrUnsupportedEncryptMechanism a défini le message d'erreur sur un mécanisme de chiffrement non pris en charge.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm a défini le message d'erreur sur l'algorithme de hachage non pris en charge.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat a défini le message d'erreur sur l'expression de format numérique non prise en charge.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrWorkbookFileFormat a défini le message d'erreur lors de la réception d'un format de fichier de classeur non pris en charge.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrWorkbookPassword a défini le message d'erreur lors de la réception du mot de passe de classeur incorrect.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

Relation source et liste d'espaces de noms, préfixes associés et schéma dans lesquels il a été introduit:

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

IndexedColorMapping est le tableau des mappages par défaut de la valeur de couleur indexée à la valeur RGB. Notez que 0-7 sont redondants de 8-15 pour préserver la rétrocompatibilité. Un schéma d'indexation hérité pour les couleurs qui est toujours requis pour certains enregistrements, et pour la rétrocompatibilité avec les formats hérités. Cet élément contient une séquence de valeurs de couleur RGB qui correspondent à des index de couleur (basés sur zéro). Lors de l'utilisation de la palette de couleurs indexées par défaut, les valeurs ne sont pas écrites, mais implicites. Lorsque la palette de couleurs a été modifiée par défaut, la totalité de la palette de couleurs est écrite.

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

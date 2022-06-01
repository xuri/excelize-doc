# Variables

```go
var (
    // ErrStreamSetColWidth a défini le message d'erreur sur la largeur de
    // colonne définie en mode d'écriture de flux.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber a défini le message d'erreur lors de la réception d'un
    // numéro de colonne invalide.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth a défini le message d'erreur lors de la réception d'une
    // largeur de colonne non valide.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel a défini le message d'erreur lors de la réception d'un
    // numéro de niveau hiérarchique non valide.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates a défini le message d'erreur sur la longueur des tuples
    // de coordonnées non valides.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet a défini le message d'erreur sur une feuille de
    // calcul donnée qui existe déjà.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks a défini le message d'erreur sur le dépassement
    // du nombre de liens hypertexte.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula a défini le message d'erreur lors de la réception
    // d'une formule invalide.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject a défini le message d'erreur lors de l'ajout du projet
    // VBA dans le classeur.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows a défini le message d'erreur lors de la réception d'un
    // numéro de ligne qui dépasse la limite maximale.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight a défini le message d'erreur lors de la réception d'une
    // hauteur de ligne invalide.
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be smaller than or equal to %d points", MaxRowHeight)
    // ErrImgExt a défini le message d'erreur lors de la réception d'une
    // extension d'image non prise en charge.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrWorkbookFileFormat a défini le message d'erreur lors de la réception
    // d'un format de fichier de classeur non pris en charge.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrMaxFilePathLength a défini le message d'erreur lors de la réception
    // du dépassement de longueur de nom de fichier.
    ErrMaxFilePathLength = errors.New("file path length exceeds maximum limit")
    // ErrUnknownEncryptMechanism a défini le message d'erreur sur un
    // mécanisme de chiffrement non pris en charge.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism a défini le message d'erreur sur un
    // mécanisme de chiffrement non pris en charge.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm a défini le message d'erreur sur
    // l'algorithme de hachage non pris en charge.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat a défini le message d'erreur sur l'expression
    // de format numérique non prise en charge.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrPasswordLengthInvalid a défini le message d'erreur sur la longueur
    // du mot de passe non valide.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrParameterRequired a défini le message d'erreur lors de la réception
    // du paramètre vide.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid a défini le message d'erreur lors de la réception
    // du paramètre invalide.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope a défini le message d'erreur sur le nom défini
    // introuvable dans la portée donnée.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate a défini le message d'erreur sur le même nom
    // qui existe déjà sur l'étendue.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt a défini le message d'erreur lors de la réception du
    // format de nombre personnalisé vide.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength a défini le message d'erreur sur la longueur du
    // débordement du nom de famille de police.
    ErrFontLength = fmt.Errorf("the length of the font family name must be smaller than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize a défini le message d'erreur sur la taille de la police
    // n'est pas valide.
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
    // ErrSheetIdx a défini le message d'erreur lors de la réception de
    // l'index de feuille de calcul non valide.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrUnprotectSheet a défini que le message d'erreur sur la feuille de
    // calcul n'a défini aucune protection.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword a défini le message d'erreur lors de la
    // suppression de la protection de la feuille avec échec de la vérification
    // du mot de passe.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets a défini le message d'erreur sur les feuilles de groupe.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength a défini le message d'erreur pour la
    // réception d'une longueur de formule de validation de données qui
    // dépasse la limite.
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange a défini le message d'erreur sur une plage
    // décimale définie dépassant la limite.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength a défini le message d'erreur pour la réception d'une
    // longueur de caractère de cellule qui dépasse la limite.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit a défini le message d'erreur pour la réception
    // d'UnzipSizeLimit et de UnzipXMLSizeLimit non valides.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave a défini le message d'erreur pour l'enregistrement du fichier.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool a défini le message d'erreur sur l'attribut XML de type
    // booléen marshal et unmarshal.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType a défini le message d'erreur lors de la réception des
    // paramètres de type sparkline non valides.
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation a défini le message d'erreur sur les paramètres
    // 'Location' manquants.
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange a défini le message d'erreur sur les paramètres
    // manquants de sparkline 'Range'.
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline a défini le message d'erreur lors de la réception des
    // paramètres de sparkline non valides.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle a défini le message d'erreur lors de la réception des
    // paramètres 'Style' de sparkline non valides.
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrWorkbookPassword a défini le message d'erreur lors de la réception du
    // mot de passe de classeur incorrect.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

Relation source et liste d'espaces de noms, préfixes associés et schéma dans lesquels il a été introduit:

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

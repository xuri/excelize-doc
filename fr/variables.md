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
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt a défini le message d'erreur lors de la réception d'une
    // extension d'image non prise en charge.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength a défini le message d'erreur lors de la réception
    // du dépassement de longueur de nom de fichier.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt a défini le message d'erreur sur la feuille de calcul de
    // chiffrement.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism a défini le message d'erreur sur un
    // mécanisme de chiffrement non pris en charge.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportEncryptMechanism a défini le message d'erreur sur un
    // mécanisme de chiffrement non pris en charge.
    ErrUnsupportEncryptMechanism = errors.New("unsupport encryption mechanism")
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
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize a défini le message d'erreur sur la taille de la police
    // n'est pas valide.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx a défini le message d'erreur lors de la réception de
    // l'index de feuille de calcul non valide.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets a défini le message d'erreur sur les feuilles de groupe.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLenth a défini le message d'erreur pour la
    // réception d'une longueur de formule de validation de données qui
    // dépasse la limite.
    ErrDataValidationFormulaLenth = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange a défini le message d'erreur sur une plage
    // décimale définie dépassant la limite.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength a défini le message d'erreur pour la réception d'une
    // longueur de caractère de cellule qui dépasse la limite.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit a défini le message d'erreur pour la réception
    // d'UnzipSizeLimit et de WorksheetUnzipMemLimit non valides.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to WorksheetUnzipMemLimit")
)
```

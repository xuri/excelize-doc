# Variables

```go
var (
    // ErrStreamSetColWidth definió el mensaje de error en el ancho de columna
    // establecido en el modo de escritura de flujo.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber definió el mensaje de error al recibir un número de
    // columna no válido.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth definió el mensaje de error al recibir un ancho de
    // columna no válido.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel definió el mensaje de error al recibir un número de
    // nivel de esquema no válido.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates definió el mensaje de error en la longitud de las tuplas
    // de coordenadas no válidas.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet definió el mensaje de error en una hoja de trabajo
    // determinada que ya existe.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks definió el mensaje de error sobre el
    // desbordamiento del recuento de hipervínculos.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula definió el mensaje de error al recibir una fórmula no
    // válida.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject definió el mensaje de error al agregar el proyecto VBA
    // en el libro de trabajo.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows definió el mensaje de error al recibir un número de fila que
    // excede el límite máximo.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight definió el mensaje de error al recibir una altura de
    // fila no válida.
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt definió el mensaje de error al recibir una extensión de
    // imagen no admitida.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength definió el mensaje de error al recibir el
    // desbordamiento de la longitud del nombre de archivo.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt definió el mensaje de error en la hoja de cálculo de cifrado.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism definió el mensaje de error en un mecanismo
    // de cifrado no compatible.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism definió el mensaje de error en un
    // mecanismo de cifrado no compatible.
    ErrUnsupportedEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired definió el mensaje de error al recibir el
    // parámetro vacío.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid definió el mensaje de error al recibir el parámetro
    // no válido.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope definió el mensaje de error en el nombre definido
    // no encontrado en el alcance dado.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate definió el mensaje de error con el mismo nombre
    // que ya existe en el alcance.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt definió el mensaje de error al recibir el formato de
    // número personalizado vacío.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength definió el mensaje de error sobre la longitud del
    // desbordamiento del nombre de la familia de fuentes.
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize definió que el mensaje de error sobre el tamaño de la
    // fuente no es válido.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx definió el mensaje de error al recibir el índice de hoja de
    // trabajo no válido.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets definió el mensaje de error en las hojas de grupo.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength definió el mensaje de error para recibir
    // una longitud de fórmula de validación de datos que excede el límite.
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange definió el mensaje de error en un rango decimal
    // establecido que excede el límite.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength definió el mensaje de error para recibir la longitud
    // de un carácter de celda que excede el límite.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit definió el mensaje de error para recibir
    // UnzipSizeLimit y UnzipXMLSizeLimit no válidos.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
)
```

Relación de origen y lista de espacios de nombres, prefijos asociados y esquema en el que se introdujo:

```go
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
```

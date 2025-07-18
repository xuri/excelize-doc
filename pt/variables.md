# Variáveis

```go
var (
    // ErrAddVBAProject definiu a mensagem de erro ao adicionar o projeto VBA na pasta de trabalho.
    ErrAddVBAProject = errors.New("unsupported VBA project")
    // ErrAttrValBool definiu a mensagem de erro no atributo XML do tipo booleano marshal e unmarshal.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrCellCharsLength definiu a mensagem de erro ao receber um comprimento de caracteres de célula que excede o limite.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrCellStyles definiu que a mensagem de erro em estilos de célula excede o limite.
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrColumnNumber definiu a mensagem de erro ao receber um número de coluna inválido.
    ErrColumnNumber = fmt.Errorf("the column number must be greater than or equal to %d and less than or equal to %d", MinColumns, MaxColumns)
    // ErrColumnWidth definiu a mensagem de erro ao receber uma largura de coluna inválida.
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrCoordens definiu a mensagem de erro no comprimento das tuplas de coordenadas inválidas.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrCustomNumFmt definiu a mensagem de erro ao receber o formato de número personalizado vazio.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrDataValidationFormulaLength definiu a mensagem de erro para receber um comprimento de fórmula de validação de dados que excede o limite.
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange definiu a mensagem de erro quando o intervalo decimal definido excede o limite.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrDefinedNameDuplicate definiu que a mensagem de erro com o mesmo nome já existe no escopo.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrDefinedNameScope definiu a mensagem de erro no nome definido não encontrado no escopo fornecido.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrExistsSheet definiu que a mensagem de erro em determinada planilha já existe.
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrExistsTableName definiu que a mensagem de erro em determinada tabela já existe.
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrFontLength definiu a mensagem de erro no comprimento do estouro do nome da família de fontes.
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize definiu que a mensagem de erro sobre o tamanho da fonte é inválida.
    ErrFontSize = fmt.Errorf("font size must be an integer from %d to %d points", MinFontSize, MaxFontSize)
    // ErrFormControlValue definiu a mensagem de erro para receber um valor de rolagem que excede o limite.
    ErrFormControlValue = fmt.Errorf("scroll value must be an integer from 0 to %d", MaxFormControlValue)
    // ErrGroupSheets definiu a mensagem de erro nas planilhas de grupo.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrImgExt definiu a mensagem de erro ao receber uma extensão de imagem não suportada.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrInvalidFormula definiu a mensagem de erro ao receber uma fórmula inválida.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrMaxFilePathLength definiu a mensagem de erro ao receber o estouro do comprimento do caminho do arquivo.
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // ErrMaxRowHeight definiu a mensagem de erro ao receber uma altura de linha inválida.
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrMaxRows definiu a mensagem de erro ao receber um número de linha que excede o limite máximo.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrNameLength definiu a mensagem de erro ao receber o nome definido ou o comprimento do nome da tabela excede o limite.
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrOptionsUnzipSizeLimit definiu a mensagem de erro para receber UnzipSizeLimit e UnzipXMLSizeLimit inválidos.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrOutlineLevel definiu a mensagem de erro ao receber um número de nível de estrutura de tópicos inválido.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrPageSetupAdjustTo definiu a mensagem de erro para receber um ajuste de configuração de página quando o valor excede o limite.
    ErrPageSetupAdjustTo = errors.New("adjust to value must be an integer from 0 to 400")
    // ErrParameterInvalid definiu a mensagem de erro ao receber o parâmetro inválido.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrParameterRequired definiu a mensagem de erro ao receber o parâmetro vazio.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrPasswordLengthInvalid definiu a mensagem de erro sobre comprimento de senha inválido.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrPivotTableClassicLayout definiu a mensagem de erro ao ativar o ClassicLayout e o CompactData ao mesmo tempo.
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // ErrSave definiu a mensagem de erro para salvar o arquivo.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrSheetIdx definiu a mensagem de erro ao receber o índice da planilha inválido.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrSheetNameBlank definiu a mensagem de erro ao receber o nome da planilha em branco.
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameInvalid definiu a mensagem de erro ao receber o nome da planilha contém caracteres inválidos.
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameLength definiu a mensagem de erro ao receber o comprimento do nome da planilha excede o limite.
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrSheetNameSingleQuote definiu que a mensagem de erro no primeiro ou último caractere do nome da planilha era uma aspa simples.
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSparkline definiu a mensagem de erro ao receber os parâmetros inválidos do minigráfico.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineLocation definiu a mensagem de erro sobre parâmetros de localização ausentes
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange definiu a mensagem de erro na falta de parâmetros de intervalo do sparkline
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparklineStyle definiu a mensagem de erro ao receber os parâmetros de estilo do sparkline inválidos.
    ErrSparklineStyle = errors.New("parameter 'Style' value must be an integer from 0 to 35")
    // ErrSparklineType definiu a mensagem de erro ao receber os parâmetros de tipo de sparkline inválidos.
    ErrSparklineType = errors.New("parameter 'Type' value must be one of 'line', 'column' or 'win_loss'")
    // ErrStreamSetColStyle definiu a mensagem de erro ao definir o estilo da coluna no modo de escrita de fluxo.
    ErrStreamSetColStyle = errors.New("must call the SetColStyle function before the SetRow function")
    // ErrStreamSetColWidth definiu a mensagem de erro ao definir a largura da coluna no modo de gravação de fluxo.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes definiu a mensagem de erro nos painéis definidos no modo de gravação de fluxo.
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrTotalSheetHyperlinks definiu a mensagem de erro no estouro de contagem de hiperlinks.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrTransparency definiu a mensagem de erro para receber um valor de transparência que excede o limite.
    ErrTransparency = errors.New("transparency value must be an integer from 0 to 100")
    // ErrUnknownEncryptMechanism definiu a mensagem de erro no mecanismo de criptografia não suportado.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnprotectSheet definiu que a mensagem de erro na planilha não definiu nenhuma proteção.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword definiu a mensagem de erro ao remover a proteção da planilha com falha na verificação de senha.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrUnprotectWorkbook definiu que a mensagem de erro na pasta de trabalho não definiu nenhuma proteção.
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword definiu a mensagem de erro ao remover a proteção da pasta de trabalho com falha na verificação de senha.
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrUnsupportedEncryptMechanism definiu a mensagem de erro no mecanismo de criptografia não suportado.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm definiu a mensagem de erro no algoritmo hash não suportado.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat definiu a mensagem de erro na expressão de formato de número não suportada.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrWorkbookFileFormat definiu a mensagem de erro ao receber um formato de arquivo de pasta de trabalho não suportado.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrWorkbookPassword definiu a mensagem de erro ao receber a senha incorreta da pasta de trabalho.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

Relacionamento de origem e lista de namespaces, prefixos associados e esquema no qual foi introduzido:

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

IndexedColorMapping é a tabela de mapeamentos padrão do valor da cor indexada ao valor da cor hexadecimal. Observe que 0 a 7 são redundantes de 8 a 15 para preservar a compatibilidade com versões anteriores. Um esquema de indexação legado para cores que ainda é necessário para alguns registros e para compatibilidade retroativa com formatos legados. Este elemento contém uma sequência de valores de cores hexadecimais que correspondem a índices de cores (baseados em zero). Ao usar a paleta de cores indexadas padrão, os valores não são escritos, mas sim implícitos. Quando a paleta de cores for modificada do padrão, toda a paleta de cores será gravada.

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

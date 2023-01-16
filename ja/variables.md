# 変数

```go
var (
    // ErrStreamSetColWidth は、ストリーム書き込みモードでの列幅の設定に関するエラーメッセージを定義しました
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber は、無効な列番号を受信したときのエラーメッセージを定義しました
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth は、無効な列幅を受信したときのエラーメッセージを定義しました
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel は、無効なアウトラインレベル番号を受信したときのエラーメッセージを定義しました
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates は、無効な座標タプルの長さに関するエラーメッセージを定義しました
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsSheet は、すでに存在する特定のワークシートにエラーメッセージを定義しました
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrTotalSheetHyperlinks は、ハイパーリンクカウントオーバーフローに関するエラーメッセージを定義しました
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula は、無効な数式を受信したときのエラーメッセージを定義しました
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject は、ブックにVBAプロジェクトを追加する際のエラーメッセージを定義しました
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows は、最大制限を超える行番号を受信したときのエラーメッセージを定義しました
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight は、無効な行の高さを受け取ったときのエラーメッセージを定義しました
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrImgExt は、サポートされていない画像拡張を受信したときのエラーメッセージを定義しました
    ErrImgExt = errors.New("unsupported image extension")
    // ErrWorkbookFileFormat は、サポートされていないワークブックファイル形式を受信したときのエラーメッセージを定義しました
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrMaxFilePathLength は、ファイルパス長のオーバーフローを受信したときのエラーメッセージを定義しました
    ErrMaxFilePathLength = errors.New("file path length exceeds maximum limit")
    // ErrUnknownEncryptMechanism は、サポートされていない暗号化メカニズムに関するエラーメッセージを定義しました
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism は、サポートされていない暗号化メカニズムに関するエラーメッセージを定義しました
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm は、サポートされていないハッシュアルゴリズムに関するエラーメッセージを定義しました
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat は、サポートされていない数値形式式に関するエラーメッセージを定義しました
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrPasswordLengthInvalid は、無効なパスワードの長さに関するエラーメッセージを定義しました
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrParameterRequired は、空のパラメーターを受信したときのエラーメッセージを定義しました
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid は、無効なパラメーターを受信したときのエラーメッセージを定義しました
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope は、指定されたスコープで定義された名前が見つからないというエラーメッセージを定義しました
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate は、スコープにすでに存在する同じ名前でエラーメッセージを定義しました
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt は、空のカスタム数値形式を受信したときのエラーメッセージを定義しました
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength は、フォントファミリ名のオーバーフローの長さに関するエラーメッセージを定義しました
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize は、フォントのサイズに関するエラーメッセージが無効であると定義しました
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
    // ErrSheetIdx は、無効なワークシートインデックスを受信したときのエラーメッセージを定義しました
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrUnprotectSheet は、ワークシートのエラーメッセージが保護を設定していないことを定義しました
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword は、パスワード検証に失敗したシート保護の削除に関するエラーメッセージを定義しました
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets は、グループシートにエラーメッセージを定義しました
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength は、制限を超えるデータ検証式の長さを受信するためのエラーメッセージを定義しました
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange は、設定された10進範囲のエラーメッセージが制限を超えると定義しました
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength は、制限を超えるセル文字の長さを受信するためのエラーメッセージを定義しました
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit は、無効 なUnzipSizeLimit と UnzipXMLSizeLimit
    // を受信した場合のエラーメッセージを定義しました
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave は、ファイルを保存するためのエラーメッセージを定義しました
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool は、マーシャルおよびアンマーシャルブール型 XML 属性に関するエラーメッセージを定義しました
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType は、無効なスパークラインの Type パラメーターを受信したときのエラーメッセージを定義しました
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation は、Locationパラメーターが欠落している場合のエラーメッセージを定義しました
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange は、スパークラインの Range パラメーターが欠落している場合のエラーメッセージを定義しました
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline は、無効なスパークラインパラメータを受信したときのエラーメッセージを定義しました
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle は、無効なスパークラインの Style パラメータを受信したときのエラーメッセージを定義しました
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrWorkbookPassword は、誤ったブックパスワードを受信したときのエラーメッセージを定義しました
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
    // ErrSheetNameInvalid は、シート名に無効な文字が含まれている場合のエラー メッセージを定義しました
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameSingleQuote は、シート名の最初または最後の文字のエラー メッセージが一重引用符であると定義しました
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSheetNameBlank は、空白のシート名を受け取ったときのエラー メッセージを定義しました
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameLength は、シート名の長さが制限を超えた場合のエラー メッセージを定義しました
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrUnprotectWorkbook は、ワークブックのエラー メッセージを定義し、保護を設定していません
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword は、パスワードの検証に失敗したワークブックの保護を削除する際のエラー メッセージを定義しました
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
)
```

ソース関係と名前空間リスト、関連するプレフィックスとそれが導入されたスキーマ：

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

IndexedColorMapping は、インデックス付きカラー値から RGB 値へのデフォルト マッピングのテーブルです。下位互換性を維持するために、0～7 は 8～15 と重複していることに注意してください。一部のレコードでまだ必要な色の従来のインデックス スキーム、および従来の形式との下位互換性。この要素には、カラー インデックス (ゼロ ベース) に対応する一連の RGB カラー値が含まれます。デフォルトのインデックス付きカラー パレットを使用する場合、値は書き出されず、代わりに暗示されます。カラー パレットがデフォルトから変更されると、カラー パレット全体が書き出されます。

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

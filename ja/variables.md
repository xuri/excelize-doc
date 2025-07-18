# 変数

```go
var (
    // ErrAddVBAProject は、ブックにVBAプロジェクトを追加する際のエラーメッセージを定義しました
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrAttrValBool は、マーシャルおよびアンマーシャルブール型 XML 属性に関するエラーメッセージを定義しました
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrCellCharsLength は、制限を超えるセル文字の長さを受信するためのエラーメッセージを定義しました
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrCellStyles で定義されたセル スタイルのエラー メッセージが制限を超えています
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // ErrColumnNumber は、無効な列番号を受信したときのエラーメッセージを定義しました
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth は、無効な列幅を受信したときのエラーメッセージを定義しました
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrCoordinates は、無効な座標タプルの長さに関するエラーメッセージを定義しました
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrCustomNumFmt は、空のカスタム数値形式を受信したときのエラーメッセージを定義しました
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrDataValidationFormulaLength は、制限を超えるデータ検証式の長さを受信するためのエラーメッセージを定義しました
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange は、設定された10進範囲のエラーメッセージが制限を超えると定義しました
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrDefinedNameDuplicate は、スコープにすでに存在する同じ名前でエラーメッセージを定義しました
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrDefinedNameScope は、指定されたスコープで定義された名前が見つからないというエラーメッセージを定義しました
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrExistsSheet は、すでに存在する特定のワークシートにエラーメッセージを定義しました
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // ErrExistsTableName は、指定されたテーブルにエラー メッセージを定義しましたが、すでに存在します
    ErrExistsTableName = errors.New("the same name table already exists")
    // ErrFontLength は、フォントファミリ名のオーバーフローの長さに関するエラーメッセージを定義しました
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize は、フォントのサイズに関するエラーメッセージが無効であると定義しました
    ErrFontSize = fmt.Errorf("font size must be an integer from %d to %d points", MinFontSize, MaxFontSize)
    // ErrFormControlValue は、スクロール値が制限を超えた場合のエラー メッセージを定義しました
    ErrFormControlValue = fmt.Errorf("scroll value must be an integer from 0 to %d", MaxFormControlValue)
    // ErrGroupSheets は、グループシートにエラーメッセージを定義しました
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrImgExt は、サポートされていない画像拡張を受信したときのエラーメッセージを定義しました
    ErrImgExt = errors.New("unsupported image extension")
    // ErrInvalidFormula は、無効な数式を受信したときのエラーメッセージを定義しました
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrMaxFilePathLength は、ファイルパス長のオーバーフローを受信したときのエラーメッセージを定義しました
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // ErrMaxRowHeight は、無効な行の高さを受け取ったときのエラーメッセージを定義しました
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrMaxRows は、最大制限を超える行番号を受信したときのエラーメッセージを定義しました
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrNameLength は、定義された名前またはテーブル名の長さが制限を超えていることを受信した際のエラー メッセージを定義しました
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // ErrOptionsUnzipSizeLimit は、無効 なUnzipSizeLimit と UnzipXMLSizeLimit を受信した場合のエラーメッセージを定義しました
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrOutlineLevel は、無効なアウトラインレベル番号を受信したときのエラーメッセージを定義しました
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrPageSetupAdjustTo は、ページ設定調整値が制限を超えた場合のエラー メッセージを定義します
    ErrPageSetupAdjustTo = errors.New("adjust to value must be an integer from 0 to 400")
    // ErrParameterInvalid は、無効なパラメーターを受信したときのエラーメッセージを定義しました
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrParameterRequired は、空のパラメーターを受信したときのエラーメッセージを定義しました
    ErrParameterRequired = errors.New("parameter is required")
    // ErrPasswordLengthInvalid は、無効なパスワードの長さに関するエラーメッセージを定義しました
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrPivotTableClassicLayout は、ClassicLayout と CompactData を同時に有効にした場合のエラーメッセージを定義しました
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // ErrSave は、ファイルを保存するためのエラーメッセージを定義しました
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrSheetIdx は、無効なワークシートインデックスを受信したときのエラーメッセージを定義しました
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrSheetNameBlank は、空白のシート名を受け取ったときのエラー メッセージを定義しました
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // ErrSheetNameInvalid は、シート名に無効な文字が含まれている場合のエラー メッセージを定義しました
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // ErrSheetNameLength は、シート名の長さが制限を超えた場合のエラー メッセージを定義しました
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // ErrSheetNameSingleQuote は、シート名の最初または最後の文字のエラー メッセージが一重引用符であると定義しました
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // ErrSparkline は、無効なスパークラインパラメータを受信したときのエラーメッセージを定義しました
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineLocation は、Locationパラメーターが欠落している場合のエラーメッセージを定義しました
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange は、スパークラインの Range パラメーターが欠落している場合のエラーメッセージを定義しました
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparklineStyle は、無効なスパークラインの Style パラメータを受信したときのエラーメッセージを定義しました
    ErrSparklineStyle = errors.New("parameter 'Style' value must be an integer from 0 to 35")
    // ErrSparklineType は、無効なスパークラインの Type パラメーターを受信したときのエラーメッセージを定義しました
    ErrSparklineType = errors.New("parameter 'Type' value must be one of 'line', 'column' or 'win_loss'")
    // ErrStreamSetColStyle は、ストリーム書き込みモードでの列スタイル設定に関するエラー メッセージを定義します
    ErrStreamSetColStyle = errors.New("must call the SetColStyle function before the SetRow function")
    // ErrStreamSetColWidth は、ストリーム書き込みモードでの列幅の設定に関するエラーメッセージを定義しました
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrStreamSetPanes は、ストリーム書き込みモードのセット ペインでのエラー メッセージを定義しました
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // ErrTotalSheetHyperlinks は、ハイパーリンクカウントオーバーフローに関するエラーメッセージを定義しました
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrTransparency は、透明度の値が制限を超えた場合に送信されるエラー メッセージを定義します
    ErrTransparency = errors.New("transparency value must be an integer from 0 to 100")
    // ErrUnknownEncryptMechanism は、サポートされていない暗号化メカニズムに関するエラーメッセージを定義しました
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnprotectSheet は、ワークシートのエラーメッセージが保護を設定していないことを定義しました
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword は、パスワード検証に失敗したシート保護の削除に関するエラーメッセージを定義しました
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrUnprotectWorkbook は、ワークブックのエラー メッセージを定義し、保護を設定していません
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // ErrUnprotectWorkbookPassword は、パスワードの検証に失敗したワークブックの保護を削除する際のエラー メッセージを定義しました
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // ErrUnsupportedEncryptMechanism は、サポートされていない暗号化メカニズムに関するエラーメッセージを定義しました
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm は、サポートされていないハッシュアルゴリズムに関するエラーメッセージを定義しました
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat は、サポートされていない数値形式式に関するエラーメッセージを定義しました
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrWorkbookFileFormat は、サポートされていないワークブックファイル形式を受信したときのエラーメッセージを定義しました
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrWorkbookPassword は、誤ったブックパスワードを受信したときのエラーメッセージを定義しました
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

ソース関係と名前空間リスト、関連するプレフィックスとそれが導入されたスキーマ：

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

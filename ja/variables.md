# 変数

```go
var (
    // ErrStreamSetColWidth は、ストリーム書き込みモードでの列幅の設定に関するエラーメッセージを定義しました。
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber は、無効な列番号を受信したときのエラーメッセージを定義しました。
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth は、無効な列幅を受信したときのエラーメッセージを定義しました。
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel は、無効なアウトラインレベル番号を受信したときのエラーメッセージを定義しました。
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates は、無効な座標タプルの長さに関するエラーメッセージを定義しました。
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet は、すでに存在する特定のワークシートにエラーメッセージを定義しました。
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks は、ハイパーリンクカウントオーバーフローに関するエラーメッセージを定義しました。
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula は、無効な数式を受信したときのエラーメッセージを定義しました。
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject は、ブックにVBAプロジェクトを追加する際のエラーメッセージを定義しました。
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows は、最大制限を超える行番号を受信したときのエラーメッセージを定義しました。
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight は、無効な行の高さを受け取ったときのエラーメッセージを定義しました。
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt は、サポートされていない画像拡張を受信したときのエラーメッセージを定義しました。
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength は、ファイル名の長さのオーバーフローを受信したときのエラーメッセージを定義しました。
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt は、暗号化スプレッドシートにエラーメッセージを定義しました。
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism は、サポートされていない暗号化メカニズムに関するエラーメッセージを定義しました。
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism は、サポートされていない暗号化メカニズムに関するエラーメッセージを定義しました。
    ErrUnsupportedEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired は、空のパラメーターを受信したときのエラーメッセージを定義しました。
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid は、無効なパラメーターを受信したときのエラーメッセージを定義しました。
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope は、指定されたスコープで定義された名前が見つからないというエラーメッセージを定義しました。
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate は、スコープにすでに存在する同じ名前でエラーメッセージを定義しました。
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt は、空のカスタム数値形式を受信したときのエラーメッセージを定義しました。
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength は、フォントファミリ名のオーバーフローの長さに関するエラーメッセージを定義しました。
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize は、フォントのサイズに関するエラーメッセージが無効であると定義しました。
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx は、無効なワークシートインデックスを受信したときのエラーメッセージを定義しました。
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets は、グループシートにエラーメッセージを定義しました。
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength は、制限を超えるデータ検証式の長さを受信するためのエラーメッセージを定義しました。
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange は、設定された10進範囲のエラーメッセージが制限を超えると定義しました。
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength は、制限を超えるセル文字の長さを受信するためのエラーメッセージを定義しました。
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit は、無効 なUnzipSizeLimit と UnzipXMLSizeLimit
    // を受信した場合のエラーメッセージを定義しました。
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
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

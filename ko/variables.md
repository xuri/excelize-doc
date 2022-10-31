# 변수

```go
var (
    // ErrStreamSetColWidth 는 스트림 쓰기 모드에서 설정된 열 너비에 대한 오류 메시지를 정의했습니다
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber 는 잘못된 열 번호를 수신할 때 오류 메시지를 정의했습니다
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // ErrColumnWidth 는 잘못된 열 너비를 수신할 때 오류 메시지를 정의했습니다
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel 은 잘못된 개요 수준 번호를 수신할 때 오류 메시지를 정의했습니다
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates 는 잘못된 좌표 튜플 길이에 대한 오류 메시지를 정의했습니다
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet 는 이미 존재하는 주어진 워크시트에 오류 메시지를 정의했습니다
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks 는 하이퍼링크 카운트 오버플로에 대한 오류 메시지를 정의했습니다
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula 는 잘못된 수식을 수신할 때 오류 메시지를 정의했습니다
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject 는 통합 문서에 VBA 프로젝트를 추가할 때 오류 메시지를 정의했습니다
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows 는 최대 제한을 초과하는 행 번호를 수신할 때 오류 메시지를 정의했습니다
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight 는 잘못된 행 높이 수신 시 오류 메시지를 정의했습니다
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // ErrImgExt 는 지원되지 않는 이미지 확장자를 수신할 때 오류 메시지를 정의했습니다
    ErrImgExt = errors.New("unsupported image extension")
    // ErrWorkbookFileFormat 은 지원되지 않는 통합 문서 파일 형식을 수신할 때 오류 메시지를 정의했습니다
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // ErrMaxFilePathLength 는 파일 이름 길이 오버플로 수신 시 오류 메시지를 정의했습니다
    ErrMaxFilePathLength = errors.New("file path length exceeds maximum limit")
    // ErrUnknownEncryptMechanism 이 지원되지 않는 암호화 메커니즘에 대한 오류 메시지를 정의했습니다
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportedEncryptMechanism 이 지원되지 않는 암호화 메커니즘에 대한 오류 메시지를 정의했습니다
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // ErrUnsupportedHashAlgorithm 이 지원되지 않는 해시 알고리즘에 대한 오류 메시지를 정의했습니다
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // ErrUnsupportedNumberFormat 이 지원되지 않는 숫자 형식 표현식에 대한 오류 메시지를 정의했습니다
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // ErrPasswordLengthInvalid 가 잘못된 암호 길이에 대한 오류 메시지를 정의했습니다
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // ErrParameterRequired 는 빈 매개변수 수신 시 오류 메시지를 정의했습니다
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid 는 잘못된 매개변수 수신 시 오류 메시지를 정의했습니다
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope 는 지정된 범위에서 정의된 이름을 찾을 수 없다는 오류 메시지를 정의했습니다
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate 는 범위에 이미 존재하는 동일한 이름에 대한 오류 메시지를 정의했습니다
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt 는 빈 사용자 정의 숫자 형식을 수신할 때 오류 메시지를 정의했습니다
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength 는 글꼴 패밀리 이름 오버플로의 길이에 대한 오류 메시지를 정의했습니다
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // ErrFontSize 는 글꼴 크기가 잘못되었다는 오류 메시지를 정의했습니다
    ErrFontSize = fmt.Errorf("font size must be between %d and %d points", MinFontSize, MaxFontSize)
    // ErrSheetIdx 는 잘못된 워크시트 인덱스를 수신할 때 오류 메시지를 정의했습니다
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrUnprotectSheet 는 워크시트의 오류 메시지가 보호를 설정하지 않음을 정의했습니다
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // ErrUnprotectSheetPassword 는 암호 확인이 실패한 시트 보호 제거에 대한 오류 메시지를 정의했습니다
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // ErrGroupSheets 가 그룹 시트에 오류 메시지를 정의했습니다
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLength 는 제한을 초과하는 데이터 유효성 검사 공식 길이를 수신하는 오류 메시지를 정의했습니다
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // ErrDataValidationRange 이(가) 설정된 소수 범위가 제한을 초과하는 오류 메시지를 정의했습니다
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength 는 제한을 초과하는 셀 문자 길이를 수신하는 오류 메시지를 정의했습니다
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit 은 잘못된 UnzipSizeLimit 및 UnzipXMLSizeLimit
    // 수신에 대한 오류 메시지를 정의했습니다
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // ErrSave 는 파일 저장에 대한 오류 메시지를 정의했습니다
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // ErrAttrValBool 은 마샬링 및 비정렬 부울 유형 XML 속성에 대한 오류 메시지를 정의했습니다
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // ErrSparklineType 이 잘못된 스파크라인 'Type' 매개변수 수신 시 오류 메시지를 정의했습니다
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // ErrSparklineLocation 은 'Location' 매개변수 누락에 대한 오류 메시지를 정의했습니다
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // ErrSparklineRange 는 누락된 스파크라인 'Range' 매개변수에 대한 오류 메시지를 정의했습니다
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // ErrSparkline 이 잘못된 스파크라인 매개변수 수신 시 오류 메시지를 정의했습니다
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // ErrSparklineStyle 은 잘못된 스파크라인 'Style' 매개변수 수신 시 오류 메시지를 정의했습니다
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // ErrWorkbookPassword 는 잘못된 통합 문서 암호 수신 시 오류 메시지를 정의했습니다
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

소스 관계 및 네임스페이스 목록, 관련 접두사 및 도입된 스키마:

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

IndexedColorMapping 은 색인된 색상 값에서 RGB 값으로의 기본 매핑 테이블입니다. 이전 버전과의 호환성을 유지하기 위해 0-7 은 8-15 와 중복됩니다. 일부 레코드 및 레거시 형식과의 역호환성을 위해 여전히 필요한 색상에 대한 레거시 인덱싱 체계입니다. 이 요소는 색상 인덱스 (0 부터 시작) 에 해당하는 RGB 색상 값 시퀀스를 포함합니다. 기본 색인 색상 팔레트를 사용할 때 값이 기록되지 않고 대신 암시됩니다. 색상 팔레트가 기본값에서 수정되면 전체 색상 팔레트가 작성됩니다.

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

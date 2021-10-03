# 변수

```go
var (
    // ErrStreamSetColWidth 는 스트림 쓰기 모드에서 설정된 열 너비에 대한 오류 메시지를 정의했습니다.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // ErrColumnNumber 는 잘못된 열 번호를 수신할 때 오류 메시지를 정의했습니다.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // ErrColumnWidth 는 잘못된 열 너비를 수신할 때 오류 메시지를 정의했습니다.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // ErrOutlineLevel 은 잘못된 개요 수준 번호를 수신할 때 오류 메시지를 정의했습니다.
    ErrOutlineLevel = errors.New("invalid outline level")
    // ErrCoordinates 는 잘못된 좌표 튜플 길이에 대한 오류 메시지를 정의했습니다.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // ErrExistsWorksheet 는 이미 존재하는 주어진 워크시트에 오류 메시지를 정의했습니다.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // ErrTotalSheetHyperlinks 는 하이퍼링크 카운트 오버플로에 대한 오류 메시지를 정의했습니다.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // ErrInvalidFormula 는 잘못된 수식을 수신할 때 오류 메시지를 정의했습니다.
    ErrInvalidFormula = errors.New("formula not valid")
    // ErrAddVBAProject 는 통합 문서에 VBA 프로젝트를 추가할 때 오류 메시지를 정의했습니다.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // ErrMaxRows 는 최대 제한을 초과하는 행 번호를 수신할 때 오류 메시지를 정의했습니다.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // ErrMaxRowHeight 는 잘못된 행 높이 수신 시 오류 메시지를 정의했습니다.
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // ErrImgExt 는 지원되지 않는 이미지 확장자를 수신할 때 오류 메시지를 정의했습니다.
    ErrImgExt = errors.New("unsupported image extension")
    // ErrMaxFileNameLength 는 파일 이름 길이 오버플로 수신 시 오류 메시지를 정의했습니다.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // ErrEncrypt 가 암호화 스프레드시트에 오류 메시지를 정의했습니다.
    ErrEncrypt = errors.New("not support encryption currently")
    // ErrUnknownEncryptMechanism 이 지원되지 않는 암호화 메커니즘에 대한 오류 메시지를 정의했습니다.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // ErrUnsupportEncryptMechanism 이 지원되지 않는 암호화 메커니즘에 대한 오류 메시지를 정의했습니다.
    ErrUnsupportEncryptMechanism = errors.New("unsupport encryption mechanism")
    // ErrParameterRequired 는 빈 매개변수 수신 시 오류 메시지를 정의했습니다.
    ErrParameterRequired = errors.New("parameter is required")
    // ErrParameterInvalid 는 잘못된 매개변수 수신 시 오류 메시지를 정의했습니다.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // ErrDefinedNameScope 는 지정된 범위에서 정의된 이름을 찾을 수 없다는 오류 메시지를 정의했습니다.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // ErrDefinedNameDuplicate 는 범위에 이미 존재하는 동일한 이름에 대한 오류 메시지를 정의했습니다.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // ErrCustomNumFmt 는 빈 사용자 정의 숫자 형식을 수신할 때 오류 메시지를 정의했습니다.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // ErrFontLength 는 글꼴 패밀리 이름 오버플로의 길이에 대한 오류 메시지를 정의했습니다.
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // ErrFontSize 는 글꼴 크기가 잘못되었다는 오류 메시지를 정의했습니다.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // ErrSheetIdx 는 잘못된 워크시트 인덱스를 수신할 때 오류 메시지를 정의했습니다.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // ErrGroupSheets 가 그룹 시트에 오류 메시지를 정의했습니다.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // ErrDataValidationFormulaLenth 는 제한을 초과하는 데이터 유효성 검사 공식 길이를 수신하는 오류 메시지를 정의했습니다.
    ErrDataValidationFormulaLenth = errors.New("data validation must be 0-255 characters")
    // ErrDataValidationRange 이(가) 설정된 소수 범위가 제한을 초과하는 오류 메시지를 정의했습니다.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // ErrCellCharsLength 는 제한을 초과하는 셀 문자 길이를 수신하는 오류 메시지를 정의했습니다.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // ErrOptionsUnzipSizeLimit 은 잘못된 UnzipSizeLimit 및 WorksheetUnzipMemLimit
    // 수신에 대한 오류 메시지를 정의했습니다.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to WorksheetUnzipMemLimit")
)
```

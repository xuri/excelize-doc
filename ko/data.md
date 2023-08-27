# 데이터

## 데이터 유효성 검사 추가 {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

AddDataValidation는 주어진 데이터 유효성 검사 개체 및 워크 시트 이름으로 워크 시트 범위에 대한 집합 데이터 유효성 검사를 제공합니다. 데이터 유효성 검사 개체는 `NewDataValidation` 함수로 만들 수 있습니다. 데이터 유효성 검사 유형 및 연산자는 [상수](constants.md) 섹션에서 찾을 수 있습니다.

예제 1, 유효성 검사 조건 설정으로 `Sheet1!A1:B2` 에 대한 데이터 유효성 검사를 설정하고, 잘못된 데이터가 "Stop" 스타일 및 사용자 지정 제목 "error body" 로 입력된 후 오류 경고를 표시합니다:

<p align="center"><img width="654" src="./images/data_validation_01.png" alt="Data validation"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dv)
```

예제 2, 에서는 유효성 검사 조건 설정을 사용하여 `Sheet1!A3:B4` 에 대한 데이터 유효성 검사를 설정하고 셀을 선택할 때 입력 메시지를 표시합니다:

<p align="center"><img width="654" src="./images/data_validation_02.png" alt="Data validation"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

예제 3, 유효성 검사 기준 설정을 사용 하 여 `Sheet1!A5:B6` 에 데이터 유효성 검사를 설정, 목록 소스를 허용 하 여 셀 내 드롭다운을 만듭니다:

<p align="center"><img width="654" src="./images/data_validation_03.png" alt="Data validation"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

데이터 유효성 검사 대화 상자 (구분된 목록) 에 항목을 입력하는 경우 구분 기호를 포함하여 255 자로 제한됩니다. 데이터 유효성 검사 목록 소스 수식이 최대 길이 제한을 초과하는 경우 워크시트 셀에 허용되는 값을 설정하고 `SetSqrefDropList` 함수를 사용하여 해당 셀에 대한 참조를 설정하세요.

예제 4, 유효성 검사 기준 소스 `Sheet1!E1:E3` 설정으로 `Sheet1!A7:B8` 에 대한 데이터 유효성 검사를 설정하고 목록 소스를 허용하여 셀 내 드롭다운을 만듭니다:

<p align="center"><img width="654" src="./images/data_validation_04.png" alt="Data validation"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dv)
```

데이터 유효성 검사 드롭다운 목록에 표시되는 항목 수에는 제한이 있습니다. 목록은 워크시트 목록의 최대 32768 개 항목을 표시할 수 있습니다. 그보다 더 많은 항목이 필요한 경우 카테고리별로 분류된 종속 드롭다운 목록을 만들 수 있습니다.

## 데이터 유효성 검사 받기 {#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

GetDataValidations 는 지정된 워크시트 이름별로 데이터 유효성 검사 목록을 반환합니다.

## 데이터 유효성 검사 삭제 {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

DeleteDataValidation 은 주어진 워크시트 이름과 참조 순서로 데이터 유효성 검사를 삭제합니다. 참조 시퀀스 매개변수를 지정하지 않으면 워크시트의 모든 데이터 유효성 검사가 삭제됩니다.

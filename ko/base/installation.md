# 빠르게 시작 하기

## 설치 {#install}

다음 표는 각 Excelize 릴리스 버전에서 Go 언어의 최소 요구 사항을 보여줍니다:

Excelize 버전 | 최소 Go 언어 버전 요구 사항
---|---
v2.8.1 | 1.18
v2.7.0 ~ v2.8.0 | 1.16
v2.4.0 ~ v2.6.1 | 1.15
v2.0.2 ~ v2.3.2 | 1.10
v1.0.0 ~ v2.0.1 | 1.6

최신 버전의 Excelize 라이브러리를 사용하려면 Go 버전 1.16 이상이 필요합니다. Go 1.21.0 에는 일부 [호환되지 않는 변경 사항](https://github.com/golang/go/issues/61881) 이 있습니다. 이 라이브러리는 해당 버전에서 작동할 수 없습니다. Go 1.21.x 를 사용하는 경우 Go 1.21.1 이상 버전으로 업그레이드하세요.

- 설치 명령

```bash
go get github.com/xuri/excelize
```

- [Go Modules](https://go.dev/blog/using-go-modules) 로 패키지를 관리하는 경우 다음 명령으로 설치하십시오.

```bash
go get github.com/xuri/excelize/v2
```

## 업데이트 {#update}

- 업데이트 명령

```bash
go get -u github.com/xuri/excelize/v2
```

## Excel 문서 만들기 {#NewFile}

다음은 Excel 문서를 만드는 간단한 예제입니다：

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // 워크시트 만들기
    index, err := f.NewSheet("Sheet2")
    if err != nil {
        fmt.Println(err)
        return
    }
    // 셀 값 설정
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // 통합 문서에 대 한 기본 워크시트를 설정 합니다
    f.SetActiveSheet(index)
    // 지정 된 경로를 기반으로 파일 저장
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Excel 문서 읽기 {#read}

다음은 Excel 문서를 읽는 예제입니다：

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // 워크시트에서 지정 된 셀의 값을 가져옵니다
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Sheet1 의 모든 셀 가져오기
    rows, err := f.GetRows("Sheet1")
    if err != nil {
        fmt.Println(err)
        return
    }
    for _, row := range rows {
        for _, colCell := range row {
            fmt.Print(colCell, "\t")
        }
        fmt.Println()
    }
}
```

## Excel 문서에 차트 추가 {#chart}

Excelize 을 사용 하 여 차트를 생성 하는 것은 간단 하며 몇 줄의 코드만 필요 합니다. 워크시트의 기존 데이터를 기반으로 차트를 작성 하거나 워크시트에 데이터를 추가 하 고 차트를 만들 수 있습니다.

<p align="center"><img width="769" src="../images/base.png" alt="Excel 문서에서 차트 만들기"></p>

```go
package main

import (
    "fmt"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    for idx, row := range [][]interface{}{
        {nil, "Apple", "Orange", "Pear"}, {"Small", 2, 3, 3},
        {"Normal", 5, 2, 4}, {"Large", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        f.SetSheetRow("Sheet1", cell, &row)
    }
    if err := f.AddChart("Sheet1", "E1", &excelize.Chart{
        Type: excelize.Col3DClustered,
        Series: []excelize.ChartSeries{
            {
                Name:       "Sheet1!$A$2",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$2:$D$2",
            },
            {
                Name:       "Sheet1!$A$3",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$3:$D$3",
            },
            {
                Name:       "Sheet1!$A$4",
                Categories: "Sheet1!$B$1:$D$1",
                Values:     "Sheet1!$B$4:$D$4",
            }},
        Title: []excelize.RichTextRun{
            {
                Text: "Fruit 3D Clustered Column Chart",
            },
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // 지정 된 경로를 기반으로 파일 저장
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Excel 문서에 그림 추가 {#image}

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/xuri/excelize/v2"
)

func main() {
    f, err := excelize.OpenFile("Book1.xlsx")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // 그림 삽입
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // 워크시트에 그림을 삽입 하 고 그림의 확대/축소 배율을 설정 합니다
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{ScaleX: 0.5, ScaleY: 0.5}); err != nil {
        fmt.Println(err)
        return
    }
    // 워크시트에 그림을 삽입 하 고 그림의 인쇄 속성을 설정 합니다
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            PrintObject:     &enable,
            LockAspectRatio: false,
            OffsetX:         15,
            OffsetY:         10,
            Locked:          &disable,
        }); err != nil {
        fmt.Println(err)
        return
    }
    // 파일 저장
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

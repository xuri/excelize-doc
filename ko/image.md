# 그림

## 그림 추가 {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

AddPicture 는 주어진 그림 형식 집합(예: 오프셋, 축척, 종횡비 설정 및 인쇄 설정) 및 파일 경로를 사용하여 시트에 그림을 추가하는 방법을 제공합니다.

예를 들어:

```go
package main

import (
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    // 그림을 삽입합니다.
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        println(err.Error())
    }
    // 위치 하이퍼링크가 있는 셀에 그림 배율을 삽입합니다.
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{"x_scale": 0.5, "y_scale": 0.5, "hyperlink": "#Sheet2!D8", "hyperlink_type": "Location"}`); err != nil {
        println(err.Error())
    }
    // 외부 하이퍼링크, 인쇄 및 위치 지정 지원이 있는 셀에 그림 오프셋을 삽입합니다.
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{"x_offset": 15, "y_offset": 10, "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize", "hyperlink_type": "External", "print_obj": true, "lock_aspect_ratio": false, "locked": false, "positioning": "oneCell"}`); err != nil {
        println(err.Error())
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        println(err.Error())
    }
}
```

LinkType 은 웹 사이트에 대한 두 가지 유형의 하이퍼링크 `External` 또는 이 통합 문서의 셀 중 하나로 이동하기 위한 `Location` 를 정의합니다. `hyperlink_type` 이 `Location` 인 경우 좌표는 `#` 으로 시작해야 합니다.

포지셔닝은 Excel 스프레드시트에서 사진의 위치의 두 가지 유형인 `oneCell` (셀로 는 이동하지만 크기는 커지지 않습니다) 또는 "absolute" (셀로 이동하거나 크기를 조정하지 마십시오) 를 정의합니다. 이 매개 변수를 설정하지 않으면 기본 `positioning` 은 셀이 있는 이동 및 크기입니다.

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

AddPictureFromBytes는 주어진 그림 형식 집합 (예: 오프셋, 축척, 종횡비 설정 및 인쇄 설정), 대체 텍스트 설명, 확장자 이름 및 파일 콘텐츠 (`[]byte` 유형) 를 사용하여 시트에 그림을 추가하는 방법을 제공합니다.

예를 들어:

```go
package main

import (
    _ "image/jpeg"
    "io/ioutil"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()

    file, err := ioutil.ReadFile("image.jpg")
    if err != nil {
        println(err.Error())
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        println(err.Error())
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        println(err.Error())
    }
}
```

## 사진 가져 오기 {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

GetPicture 는 주어진 워크 시트 및 셀 이름으로 XLSX 에 포함 된 그림 기본 이름 및 원시 콘텐츠를 얻을 수 있는 기능을 제공 합니다. 이 함수는 XLSX 에서 파일 이름과 파일 내용을 `[]byte` 데이터 유형으로 반환합니다.

예를 들어:

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    println(err.Error())
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    println(err.Error())
    return
}
if err := ioutil.WriteFile(file, raw, 0644); err != nil {
    println(err.Error())
}
```

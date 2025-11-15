# 그림

## 그림 추가 {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

AddPicture 는 지정된 그림 형식(예: 오프셋, 크기 조절, 종횡비 설정, 인쇄 설정)과 파일 경로를 사용하여 워크시트에 그림을 추가하는 메서드를 제공합니다. 지원되는 이미지 형식은 BMP, EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF, WMZ 입니다. 이 함수는 동시 실행 시 안전합니다. 단, 이 함수는 현재 셀 위에 배치된 그림 추가만 지원하며, 셀 안에 배치된 그림 추가나 Kingsoft WPS Office 내장 이미지 셀 생성은 지원하지 않습니다.

예를 들어:

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
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    // 그림을 삽입합니다.
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // 위치 하이퍼링크가 있는 셀에 그림 배율을 삽입합니다.
    enable, disable := true, false
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{
            ScaleX:        0.5,
            ScaleY:        0.5,
            Hyperlink:     "#Sheet2!D8",
            HyperlinkType: "Location",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    // 외부 하이퍼링크, 인쇄 및 위치 지정 지원이 있는 셀에 그림 오프셋을 삽입합니다.
    if err := f.AddPicture("Sheet1", "H2", "image.gif",
        &excelize.GraphicOptions{
            OffsetX:         15,
            OffsetY:         10,
            Hyperlink:       "https://github.com/xuri/excelize",
            HyperlinkType:   "External",
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
            Positioning:     "oneCell",
        },
    ); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

선택적 매개변수 `AltText` 는 그래프 개체에 대체 텍스트를 추가하는 데 사용됩니다.

선택적 매개변수 `PrintObject` 는 워크시트가 인쇄될 때 이미지가 인쇄되는지 여부를 나타내며, 기본값은 `true` 입니다.

선택적 매개변수 `Locked` 는 이미지를 잠글지 여부를 나타냅니다. 시트가 보호되지 않는 한 개체를 잠그면 효과가 없습니다.

선택적 매개변수 `LockAspectRatio` 는 이미지의 종횡비 잠금 여부를 나타내며 기본값은 `false` 입니다.

선택적 매개변수 `AutoFit` 은 이미지 크기를 셀에 자동으로 맞출지 여부를 지정하며, 기본값은 `false` 입니다.

선택적 매개변수 `OffsetX` 은 셀과 이미지의 수평 오프셋을 지정하며 기본값은 0 입니다.

선택적 매개변수 `OffsetY` 은 셀이 있는 이미지의 수직 오프셋을 지정하며 기본값은 0 입니다.

선택적 매개변수 `ScaleX` 은 이미지의 수평 스케일을 지정하며 기본값은 100%를 나타내는 1.0 입니다.

선택적 매개변수 `ScaleY` 은 이미지의 수직 스케일을 지정하며 기본값은 100%를 나타내는 1.0 입니다.

선택적 매개변수 `Hyperlink` 는 이미지의 하이퍼링크를 지정합니다.

선택적 매개변수 `HyperlinkType` 은 웹사이트에 대한 `External` 하이퍼링크 또는 이 통합 문서의 셀 중 하나로 이동하기 위한 `Location` 의 두 가지 유형의 하이퍼링크를 정의합니다. `HyperlinkType` 이 `Location` 인 경우 좌표는 `#` 로 시작해야 합니다.

선택적 매개변수 `Positioning` 은 스프레드시트에서 그래프 개체 위치의 3가지 유형인 `oneCell` (셀과 함께 이동하지만 크기 조정 안함), `twoCell`(셀과 함께 이동 및 크기 조정) 및 `absolute` (셀과 함께 이동하거나 크기를 조정하지 마십시오). 이 매개변수를 설정하지 않으면 기본 위치는 셀과 함께 이동하고 크기를 조정하는 것입니다.

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

AddPictureFromBytes 는 주어진 그림 형식 집합 (예: 오프셋, 축척, 종횡비 설정 및 인쇄 설정), 대체 텍스트 설명, 확장자 이름 및 파일 콘텐츠 (`[]byte` 유형) 를 사용하여 시트에 그림을 추가하는 방법을 제공합니다. 지원되는 이미지 유형: EMF, EMZ, GIF, ICO, JPEG, JPG, PNG, SVG, TIF, TIFF, WMF, WMZ. 이 기능은 현재 셀 위에 배치된 그림 추가만 지원하며, 셀 안에 그림을 추가하거나 Kingsoft WPS Office 내장 이미지 셀을 생성하는 기능은 지원하지 않습니다.

예를 들어:

```go
package main

import (
    "fmt"
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()
    defer func() {
        if err := f.Close(); err != nil {
            fmt.Println(err)
        }
    }()
    file, err := os.ReadFile("image.jpg")
    if err != nil {
        fmt.Println(err)
        return
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", &excelize.Picture{
        Extension: ".jpg",
        File:      file,
        Format:    &excelize.GraphicOptions{AltText: "Excel Logo"},
    }); err != nil {
        fmt.Println(err)
        return
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 사진 가져 오기 {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

GetPicture 는 주어진 워크 시트 및 셀 이름으로 XLSX 에 포함 된 그림 기본 이름 및 원시 콘텐츠를 얻을 수 있는 기능을 제공 합니다. 이 기능은 동시성 안전에 사용될 수 있습니다. 이 함수는 XLSX 에서 파일 이름과 파일 내용을 `[]byte` 데이터 유형으로 반환합니다.

예를 들어:

```go
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
pics, err := f.GetPictures("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
}
for idx, pic := range pics {
    name := fmt.Sprintf("image%d%s", idx+1, pic.Extension)
    if err := os.WriteFile(name, pic.File, 0644); err != nil {
        fmt.Println(err)
    }
}
```

## 삭제 이미지 {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture 는 주어진 워크 시트와 셀 이름으로 XLSX 에서 차트를 삭제하는 기능을 제공합니다. 이미지 파일은 현재 문서에서 삭제되지 않습니다.

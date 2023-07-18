# イメージ

## 図を挿入する {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture string, opts *GraphicOptions) error
```

指定されたワークシート名、セル座標、ピクチャアドレス、およびピクチャ形式 (オフセット、ズーム、印刷設定など) に基づいて、対応するセルに図を挿入します。この関数は、同時実行セーフをサポートします。

例えば：

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
    // 図を挿入する
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // ズーム倍率とハイパーリンクを使用して図を挿入する
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
    // 図を挿入し、図の外部ハイパーリンク、印刷、および場所のプロパティを設定する
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

オプションのパラメータ `AltText` は、グラフ オブジェクトに代替テキストを追加するために使用されます。

オプションのパラメータ `PrintObject` は、ワークシートの印刷時に画像を印刷するかどうかを示します。デフォルト値は `true` です。

オプションのパラメータ `Locked`は、画像をロックするかどうかを示します。シートが保護されていない限り、オブジェクトをロックしても効果はありません。

オプションのパラメータ `LockAspectRatio` は、画像のアスペクト比をロックするかどうかを示します。デフォルト値は `false` です。

オプションのパラメータ `AutoFit` は、画像サイズを自動でセルに合わせるかどうかを指定します。デフォルト値は `false` です。

オプションのパラメータ `OffsetX` は、セルを含む画像の水平オフセットを指定します。デフォルト値は 0 です。

オプションのパラメータ `OffsetY` は、セルを含む画像の垂直オフセットを指定します。デフォルト値は 0 です。

オプションのパラメータ `ScaleX` は、画像の水平スケールを指定します。デフォルト値は 1.0 で、100％ を表します。

オプションのパラメータ `ScaleY` は、画像の垂直スケールを指定します。デフォルト値は 1.0 で、100％ を表します。

オプションのパラメータ `Hyperlink` は、画像のハイパーリンクを指定します。

オプションのパラメータ `HyperlinkType` は、Webサイト用の2種類のハイパーリンク `External`またはこのワークブックのセルの1つに移動するための `Location`を定義します。`HyperlinkType` が `Location` の場合、座標は `＃`で始まる必要があります。

オプションのパラメータ `Positioning` は、スプレッドシート内のグラフ オブジェクトの位置の 3 つのタイプを定義します: `oneCell` (移動するがセルに合わせてサイズ変更しない)、`twoCell` (セルに合わせて移動およびサイズ変更する)、および `absolute` (セルを移動したりサイズ変更したりしないでください)。 このパラメータを設定しない場合、デフォルトの配置では、セルに合わせて移動およびサイズ変更が行われます。

```go
func (f *File) AddPictureFromBytes(sheet, cell string, pic *Picture) error
```

指定されたワークシート名、セル座標、ピクチャアドレス、およびピクチャ形式 (オフセット、ズーム、印刷設定など)、ピクチャの説明、画像の拡張子、および `[]byte` の種類のピクチャコンテンツに基づいて、対応するセルにピクチャを挿入します。

例えば：

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

## 画像を取得 {#GetPicture}

```go
func (f *File) GetPictures(sheet, cell string) ([]Picture, error)
```

指定されたワークシート名とセルの座標に基づいてブックのピクチャを取得し、Excel ドキュメントに埋め込まれているピクチャを `[]byte` 型で返します。この関数は、同時実行セーフをサポートします。たとえば、`Sheet1` という名前のワークシートの `A2`セルにピクチャを取得します。

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

## 画像を削除 {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) error
```

DeletePicture は、指定されたワークシートとセル名で XLSX のチャートを削除する機能を提供します。現在、画像ファイルはドキュメントから削除されないことに注意してください。

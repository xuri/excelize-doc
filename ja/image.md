# イメージ

## 図を挿入する {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
```

指定されたワークシート名、セル座標、ピクチャアドレス、およびピクチャ形式 (オフセット、ズーム、印刷設定など) に基づいて、対応するセルに図を挿入します。

例えば：

```go
package main

import (
    "fmt"
    _ "image/gif"
    _ "image/jpeg"
    _ "image/png"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    f := excelize.NewFile()
    // 図を挿入する
    if err := f.AddPicture("Sheet1", "A2", "image.jpg", ""); err != nil {
        fmt.Println(err)
    }
    // ズーム倍率とハイパーリンクを使用して図を挿入する
    if err := f.AddPicture("Sheet1", "D2", "image.png", `{
        "x_scale": 0.5,
        "y_scale": 0.5,
        "hyperlink": "#Sheet2!D8",
        "hyperlink_type": "Location"
    }`); err != nil {
        fmt.Println(err)
    }
    // 図を挿入し、図の外部ハイパーリンク、印刷、および場所のプロパティを設定する
    if err := f.AddPicture("Sheet1", "H2", "image.gif", `{
        "x_offset": 15,
        "y_offset": 10,
        "hyperlink": "https://github.com/360EntSecGroup-Skylar/excelize",
        "hyperlink_type": "External",
        "print_obj": true,
        "lock_aspect_ratio": false,
        "locked": false,
        "positioning": "oneCell"
    }`); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

リンクタイプ `hyperlink_type` は外部リンクと内部リンクの両方の `External` タイプをサポートし、`Location` を使用してセル位置に接続する場合、座標は `#` で始まる必要があります。

位置プロパティ `positioning` は、2つのタイプの `oneCell` (サイズ固定、セルによる位置変更) と `absolute` (サイズ、位置が固定されている) をサポートし、このパラメータが設定されていない場合、デフォルトプロパティはサイズと位置がセルによって変更されます。

```go
func (f *File) AddPictureFromBytes(sheet, cell, format, name, extension string, file []byte) error
```

指定されたワークシート名、セル座標、ピクチャアドレス、およびピクチャ形式 (オフセット、ズーム、印刷設定など)、ピクチャの説明、画像の拡張子、および `[]byte` の種類のピクチャコンテンツに基づいて、対応するセルにピクチャを挿入します。

例えば：

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
        fmt.Println(err)
    }
    if err := f.AddPictureFromBytes("Sheet1", "A2", "", "Excel Logo", ".jpg", file); err != nil {
        fmt.Println(err)
    }
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## 画像を取得 {#GetPicture}

```go
func (f *File) GetPicture(sheet, cell string) (string, []byte, error)
```

指定されたワークシート名 (大文字小文字を区別する) とセルの座標に基づいてブックのピクチャを取得し、Excel ドキュメントに埋め込まれているピクチャを `[]byte` 型で返します。たとえば、`Sheet1` という名前のワークシートの `A2`セルにピクチャを取得します。

```go
f, err := excelize.OpenFile("Book1.xlsx")
if err != nil {
    fmt.Println(err)
    return
}
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := ioutil.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## 画像を削除 {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture は、指定されたワークシートとセル名で XLSX のチャートを削除する機能を提供します。 現在、画像ファイルはドキュメントから削除されないことに注意してください。

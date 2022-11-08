# イメージ

## 図を挿入する {#AddPicture}

```go
func (f *File) AddPicture(sheet, cell, picture, format string) error
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
        "hyperlink": "https://github.com/xuri/excelize",
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

オプションのパラメータ `autofit` は、画像サイズを自動でセルに合わせるかどうかを指定します。デフォルト値は `false` です。

オプションのパラメータ `hyperlink` は、画像のハイパーリンクを指定します。

オプションのパラメータ `hyperlink_type` は、Webサイト用の2種類のハイパーリンク `External`またはこのワークブックのセルの1つに移動するための `Location`を定義します。`hyperlink_type` が `Location` の場合、座標は `＃`で始まる必要があります。

オプションのパラメータ `positioning` は、Excelスプレッドシート内の画像の位置の2つのタイプ、`oneCell` 移動するがセルでサイズ変更しない）または `absolute`（移動しないかセルでサイズ変更しない）を定義します。このパラメータを設定しない場合、デフォルトの配置は移動とセルのサイズです。

オプションのパラメータ `print_obj` は、ワークシートの印刷時に画像を印刷するかどうかを示します。デフォルト値は `true` です。

オプションのパラメータ `lock_aspect_ratio` は、画像のアスペクト比をロックするかどうかを示します。デフォルト値は `false` です。

オプションのパラメータ `locked`は、画像をロックするかどうかを示します。シートが保護されていない限り、オブジェクトをロックしても効果はありません。

オプションのパラメータ `x_offset` は、セルを含む画像の水平オフセットを指定します。デフォルト値は 0 です。

オプションのパラメータ `x_scale` は、画像の水平スケールを指定します。デフォルト値は 1.0 で、100％ を表します。

オプションのパラメータ `y_offset` は、セルを含む画像の垂直オフセットを指定します。デフォルト値は 0 です。

オプションのパラメータ `y_scale` は、画像の垂直スケールを指定します。デフォルト値は 1.0 で、100％ を表します。

```go
func (f *File) AddPictureFromBytes(sheet, cell, opts, name, extension string, file []byte) error
```

指定されたワークシート名、セル座標、ピクチャアドレス、およびピクチャ形式 (オフセット、ズーム、印刷設定など)、ピクチャの説明、画像の拡張子、および `[]byte` の種類のピクチャコンテンツに基づいて、対応するセルにピクチャを挿入します。

例えば：

```go
package main

import (
    _ "image/jpeg"
    "os"

    "github.com/xuri/excelize/v2"
)

func main() {
    f := excelize.NewFile()

    file, err := os.ReadFile("image.jpg")
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
file, raw, err := f.GetPicture("Sheet1", "A2")
if err != nil {
    fmt.Println(err)
    return
}
if err := os.WriteFile(file, raw, 0644); err != nil {
    fmt.Println(err)
}
```

## 画像を削除 {#DeletePicture}

```go
func (f *File) DeletePicture(sheet, cell string) (err error)
```

DeletePicture は、指定されたワークシートとセル名で XLSX のチャートを削除する機能を提供します。現在、画像ファイルはドキュメントから削除されないことに注意してください。

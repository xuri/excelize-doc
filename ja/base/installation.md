# 基本的な使い方

## インストール {#install}

次の表は、Excelize の各リリース バージョンでの Go 言語の最小要件を示しています:

Excelize バージョン | Go 言語の最小バージョン要件
---|---
v2.7.0 | 1.16
v2.4.0 ~ v2.6.1 | 1.15
v2.0.2 ~ v2.3.2 | 1.10
v1.0.0 ~ v2.0.1 | 1.6

最新バージョンの Excelize ライブラリを使用するには、Go 1.16 以降が必要です。Go 1.21.0 には[互換性のない変更](https://github.com/golang/go/issues/61881)がいくつかあることに注意してください。このライブラリはそのバージョンでは動作しません。Go 1.21.x を使用している場合は、Go 1.21.1 以降のバージョンにアップグレードしてください。

- インストールコマンド

```bash
go get github.com/xuri/excelize
```

- [Go Modules](https://go.dev/blog/using-go-modules) でパッケージを管理している場合は、次のコマンドでインストールしてください。

```bash
go get github.com/xuri/excelize/v2
```

## アップグレード {#update}

- 更新コマンド

```bash
go get -u github.com/xuri/excelize/v2
```

## Excel 文書を作成する {#NewFile}

これは、Excel ドキュメントを作成する簡単な例です。

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
    // ワークシートを作成する
    index, err := f.NewSheet("Sheet2")
    if err != nil {
        fmt.Println(err)
        return
    }
    // セルの値を設定
    f.SetCellValue("Sheet2", "A2", "Hello world.")
    f.SetCellValue("Sheet1", "B2", 100)
    // ワークブックのデフォルトワークシートを設定します
    f.SetActiveSheet(index)
    // 指定されたパスに従ってファイルを保存します
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Excel 文書を読む {#read}

これは Excel 文書を読む例です：

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
    // ワークシート内の指定されたセルの値を取得します
    cell, err := f.GetCellValue("Sheet1", "B2")
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(cell)
    // Sheet1 のすべてのセルを取得
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

## Excel 文書にチャートを追加する {#chart}

Excel でグラフを生成するのは簡単で、1 行のコードで済みます。ワークシート内の既存のデータに基づいてチャートを作成することも、ワークシートにデータを追加してチャートを作成することもできます。

<p align="center"><img width="771" src="../images/base.png" alt="作成中のエクセル文"></p>

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
    // 指定されたパスに従ってファイルを保存します
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Excel 文書に画像を追加する {#image}

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
    // 写真を挿入
    if err := f.AddPicture("Sheet1", "A2", "image.png", nil); err != nil {
        fmt.Println(err)
        return
    }
    // ワークシートに画像を挿入して画像の縮尺を設定する
    if err := f.AddPicture("Sheet1", "D2", "image.jpg",
        &excelize.GraphicOptions{ScaleX: 0.5, ScaleY: 0.5}); err != nil {
        fmt.Println(err)
        return
    }
    // ワークシートに画像を挿入して画像の印刷プロパティを設定する
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
    // ファイルを保存
    if err = f.Save(); err != nil {
        fmt.Println(err)
    }
}
```

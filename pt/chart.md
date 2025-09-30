# Gráfico

## Adicionar gráfico {#AddChart}

```go
func (f *File) AddChart(sheet, cell, opts string, combo ...string) error
```

AddChart fornece o método para adicionar um gráfico em uma planilha por determinado conjunto de formato de gráfico (como deslocamento, escala, configuração de proporção de aspecto e configurações de impressão) e conjunto de propriedades.

O seguinte mostra o `Type` de gráfico suportado pelo Excelize:

ID|Enumeração|Gráfico
---|---|---
0  | Area                        | Gráfico de área 2D
1  | AreaStacked                 | Gráfico de áreas empilhadas 2D
2  | AreaPercentStacked          | Gráfico de áreas 2D 100% empilhadas
3  | Area3D                      | Gráfico de área 3D
4  | Area3DStacked               | Gráfico de áreas empilhadas 3D
5  | Area3DPercentStacked        | Gráfico de áreas 3D 100% empilhadas
6  | Bar                         | Gráfico de barras agrupadas 2D
7  | BarStacked                  | Gráfico de barras empilhadas 2D
8  | BarPercentStacked           | Gráfico de barras 2D 100% empilhadas
9  | Bar3DClustered              | Gráfico de barras agrupadas 3D
10 | Bar3DStacked                | Gráfico de barras empilhadas 3D
11 | Bar3DPercentStacked         | Gráfico de barras 3D 100% empilhadas
12 | Bar3DConeClustered          | Gráfico de barras agrupadas em cone 3D
13 | Bar3DConeStacked            | Gráfico de barras empilhadas em cone 3D
14 | Bar3DConePercentStacked     | Gráfico de barras cônicas 3D 100%
15 | Bar3DPyramidClustered       | Gráfico de barras agrupadas em pirâmide 3D
16 | Bar3DPyramidStacked         | Gráfico de barras empilhadas em pirâmide 3D
17 | Bar3DPyramidPercentStacked  | Gráfico de barras empilhadas 3D com cilindro 100%
18 | Bar3DCylinderClustered      | Gráfico de barras agrupadas de cilindro 3D
19 | Bar3DCylinderStacked        | Gráfico de barras empilhadas de cilindro 3D
20 | Bar3DCylinderPercentStacked | Gráfico de barras empilhadas 3D com cilindro 100%
21 | Col                         | Gráfico de colunas agrupadas 2D
22 | ColStacked                  | Gráfico de colunas empilhadas 2D
23 | ColPercentStacked           | Gráfico de colunas 2D 100% empilhadas
24 | Col3DClustered              | Gráfico de colunas agrupadas 3D
25 | Col3D                       | Gráfico de colunas 3D
26 | Col3DStacked                | Gráfico de colunas empilhadas 3D
27 | Col3DPercentStacked         | Gráfico de colunas 3D 100% empilhadas
28 | Col3DCone                   | Gráfico de colunas de cone 3D
29 | Col3DConeClustered          | Gráfico de colunas agrupadas em cone 3D
30 | Col3DConeStacked            | Gráfico de colunas empilhadas em cone 3D
31 | Col3DConePercentStacked     | Gráfico de colunas 3D 100% empilhadas em cone
32 | Col3DPyramid                | Gráfico de colunas em pirâmide 3D
33 | Col3DPyramidClustered       | Gráfico de colunas agrupadas em pirâmide 3D
34 | Col3DPyramidStacked         | Gráfico de colunas empilhadas em pirâmide 3D
35 | Col3DPyramidPercentStacked  | Gráfico de colunas empilhadas em pirâmide 3D 100%
36 | Col3DCylinder               | Gráfico de colunas de cilindro 3D
37 | Col3DCylinderClustered      | Gráfico de colunas agrupadas em cilindro 3D
38 | Col3DCylinderStacked        | Gráfico de colunas empilhadas de cilindro 3D
39 | Col3DCylinderPercentStacked | Gráfico de colunas empilhadas 100% cilindro 3D
40 | Doughnut                    | Gráfico de rosca
41 | Line                        | Gráfico de linha
42 | Line3D                      | Gráfico de linhas 3D
43 | Pie                         | Gráfico de pizza
44 | Pie3D                       | Gráfico de pizza 3D
45 | PieOfPie                    | Gráfico pizza of pizza
46 | BarOfPie                    | Gráfico barra do pizza
47 | Radar                       | Gráfico de radar
48 | Scatter                     | Gráfico de dispersão
49 | Surface3D                   | Gráfico de superfície 3D
50 | WireframeSurface3D          | Gráfico de superfície de wireframe 3D
51 | Contour                     | Gráfico de contorno
52 | WireframeContour            | Gráfico de contorno de wireframe
53 | Bubble                      | Gráfico de bolhas
54 | Bubble3D                    | Gráfico de bolhas 3D
55 | StockHighLowClose           | Gráfico de ações de alta-baixa-fechamento
56 | StockOpenHighLowClose       | Gráfico de ações Abertura-Máxima-Mínima-Fechamento

No intervalo de dados do gráfico do Office Excel, `Series` especifica o conjunto de informações para os quais os dados serão desenhados, o item da legenda (série) e o rótulo do eixo horizontal (categoria).

As opções de `Series` que podem ser definidas são:

Parâmetro|Explicação
---|---
Name              | Item de legenda (série), exibido na legenda do gráfico e na barra de fórmulas. O parâmetro `Name` é opcional. Se você não especificar esse valor, o padrão será `Series 1 .. n`. suporte `Name` para representação de fórmula, por exemplo: `Planilha1!$A$1`.
Categories        | Etiqueta do eixo horizontal (categoria). O parâmetro `Categories` é opcional na maioria dos tipos de gráficos, o padrão é uma sequência contígua no formato `1..n`.
Values            | A área de dados do gráfico, que é o parâmetro mais importante em `Series`, também é o único parâmetro obrigatório ao criar um gráfico. Esta opção vincula o gráfico aos dados da planilha que ele exibe.
Fill              | Isso define o formato do preenchimento da série de dados.
Legend            | Isso define a fonte do texto da legenda para uma série de dados. A propriedade `Legend` é opcional.
Line              | Isso define o formato da linha do gráfico de linhas. A propriedade `Line` é opcional e se não for fornecida será o estilo padrão. As opções que podem ser definidas são `Width`. O intervalo de `Width` é 0,25pt - 999pt. Se o valor da largura estiver fora do intervalo, a largura padrão da linha será 2pt.
Marker            | Isso define o marcador do gráfico de linhas e do gráfico de dispersão. O intervalo do campo opcional `Size` é 2-72 (o valor padrão é `5`). O valor de enumeração do campo opcional `Symbol` é (o valor padrão é `auto`): `circle`, `dash`, `diamond`, `dot`, `none`, `picture`, `plus`, `square`, `star`, `triangle`, `x` e `auto`.
DataLabelPosition | Isso define a posição do rótulo de dados da série do gráfico.

Defina as propriedades da legenda do gráfico. As opções que podem ser definidas são:

Parâmetro|Tipo|Explicação
---|---|---
Position      | `string` | A posição da legenda do gráfico
ShowLegendKey | `bool`   | Defina as chaves de legenda que serão mostradas nos rótulos de dados
Font          | `Font`   | Defina as propriedades da fonte do texto da legenda do gráfico. As propriedades que podem ser definidas são as mesmas do objeto de fonte usado para formatação de células. As propriedades de família, tamanho, cor, negrito, itálico, sublinhado e tachado da fonte podem ser definidas

Defina a `Position` da legenda do gráfico. A posição padrão da legenda é `right`. Este parâmetro só entra em vigor quando `none` é `false`. As vagas disponíveis são:

Parâmetro|Explicação
---|---
none      | Disable legend
top       | On top
bottom    | On bottom
left      | On left
right     | On right
top_right | On top right

O parâmetro `ShowLegendKey` define as chaves de legenda que serão mostradas nos rótulos de dados. O valor padrão é `false`.

O título do gráfico é definido selecionando o parâmetro `Name` do objeto `Title`, e o título será exibido acima do gráfico. O parâmetro `Name` suporta o uso de representações de fórmulas, como `Planilha1!$A$1`, se você não especificar um título de ícone, o valor padrão é nulo.

O parâmetro `ShowBlanksAs` fornece a configuração "Ocultar e esvaziar células". O valor padrão é: `gap`. No aplicativo Excel, "a célula vazia é exibida como": "espaço". A seguir estão os valores opcionais para este parâmetro:

Parâmetro|Explicação
---|---
gap  | Espaço
span | Conecte pontos de dados com linhas retas
zero | Valor zero

Defina a legenda do gráfico para todas as séries de dados pela propriedade `Legend`. A propriedade `Legend` é opcional.

Defina o tamanho da bolha em todas as séries de dados para o gráfico de bolhas ou gráfico de bolhas 3D pela propriedade `BubbleSizes`. A propriedade `BubbleSizes` é opcional. A largura padrão é `100` e o valor deve ser maior que 0 e menor ou igual a 300.

Defina o tamanho do furo de rosca em todas as séries de dados para o gráfico de rosca pela propriedade `HoleSize`. A propriedade `HoleSize` é opcional. A largura padrão é `75` e o valor deve ser maior que 0 e menor ou igual a 90.

Especifica que cada marcador de dados na série possui uma cor diferente por `VaryColors`. O valor padrão é `true`.

O parâmetro `Formato` fornece configurações para parâmetros como deslocamento do gráfico, escala, configurações de proporção e propriedades de impressão, bem como aqueles usados na função X [`AddPicture`](image.md#AddPicture).

Defina a posição da área de plotagem do gráfico por área de plotagem. As propriedades que podem ser definidas são:

Parâmetro|Tipo|Valores padrão|Explicação
---|---|---|---
SecondPlotValues  | `int`            | `0`     | Especifica os valores no segundo gráfico para o gráfico `PieOfPie` e `BarOfPie`.
ShowBubbleSize    | `bool`           | `false` | Especifica que o tamanho da bolha deve ser mostrado em um rótulo de dados.
ShowCatName       | `bool`           | `true`  | Specifies that the category name shall be shown in the data label. The `ShowCatName` property is optional.
ShowDataTable     | `bool`           | `false` | Usado para adicionar tabela de dados no gráfico, dependendo do tipo de gráfico, disponível somente para gráficos de área, barra, coluna e série de linhas.
ShowDataTableKeys | `bool`           | `false` | Usado para adicionar chave de legenda na tabela de dados, funciona somente quando `ShowDataTable` está habilitado. A propriedade `ShowDataTableKeys` é opcional.
ShowLeaderLines   | `bool`           | `false` | Especifica que as linhas de chamada devem ser exibidas para rótulos de dados. A propriedade `ShowLeaderLines` é opcional.
ShowPercent       | `bool`           | `false` | E1specifica que a porcentagem deve ser mostrada em um rótulo de dados.
ShowSerName       | `bool`           | `false` | Especifica que o nome da série deve ser mostrado em um rótulo de dados.
ShowVal           | `bool`           | `false` | Especifica que o valor deve ser mostrado em um rótulo de dados.
Fill              | `Fill`           | N/A     | Defina a cor de preenchimento do gráfico.
UpBars            | `ChartUpDownBar` | N/A     | Especifica o formato das barras ascendentes do gráfico de ações. A propriedade `UpBars` é opcional.
DownBars          | `ChartUpDownBar` | N/A     | Especifica o formato das barras descendentes do gráfico de ações. A propriedade `DownBars` é opcional.
NumFmt            | `ChartNumFmt`    | N/D     | Especifica que se estiver vinculado à origem e definir o código de formato numérico personalizado para rótulos de dados. A propriedade `NumFmt` é opcional. O código de formato padrão é `General`.

Defina as opções primárias dos eixos horizontal e vertical por `XAxis` e `YAxis`.

As propriedades de `XAxis` que podem ser definidas são:

Parâmetro|Tipo|Valores padrão|Explicação
---|---|---|---
None           | `bool`          | `false` | Desative eixos.
MajorGridLines | `bool`          | `false` | Especifica as principais linhas de grade.
MinorGridLines | `bool`          | `false` | Especifica linhas de grade secundárias.
TickLabelSkip  | `int`           | `1`     | Especifica quantos rótulos de escala devem ser ignorados entre os rótulos desenhados. A propriedade `TickLabelSkip` é opcional. O valor padrão é automático.
ReverseOrder   | `bool`          | `false` | Especifica que as categorias ou valores estão na ordem inversa (orientação do gráfico). A propriedade `ReverseOrder` é opcional.
Maximum        | `*float64`      | `0`     | Especifica que o máximo fixo, 0, é automático. A propriedade máxima é opcional.
Minimum        | `*float64`      | `0`     | Especifica que o mínimo fixo, 0, é automático. A propriedade mínima é opcional. O valor padrão é automático.
Alignment      | `Alignment`     | N/D     | Especifica o alinhamento dos eixos horizontal e vertical. As propriedades de fonte que podem ser definidas são: `TextRotation` e `Vertical`
Font           | `Font`          | N/D     | Especifica a fonte do eixo horizontal.
NumFmt         | `ChartNumFmt`   | N/D     | Especifica que se estiver vinculado à origem e definir o código de formato numérico personalizado para o eixo.
Title          | `[]RichTextRun` | N/D     | Especifica que o título do eixo horizontal primário e o gráfico de redimensionamento.

As propriedades de `YAxis` que podem ser definidas são:

Parâmetro|Tipo|Valores padrão|Explicação
---|---|---|---
None           | `bool`          | `false` | Desative eixos.
MajorGridLines | `bool`          | `false` | Especifica as principais linhas de grade.
MinorGridLines | `bool`          | `false` | Especifica linhas de grade secundárias.
MajorUnit      | `float64`       | `0`     | Especifica a distância entre os ticks principais. Deve conter um número de ponto flutuante positivo. A propriedade `MajorUnit` é opcional. O valor padrão é automático.
ReverseOrder   | `bool`          | `false` | Especifica que as categorias ou valores estão na ordem inversa (orientação do gráfico). A propriedade `ReverseOrder` é opcional.
Maximum        | `*float64`      | `0`     | Especifica que o máximo fixo, 0, é automático. A propriedade máxima é opcional.
Minimum        | `*float64`      | `0`     | Especifica que o mínimo fixo, 0, é automático. A propriedade mínima é opcional. O valor padrão é automático.
Alignment      | `Alignment`     | N/D     | Especifica o alinhamento dos eixos horizontal e vertical. As propriedades de fonte que podem ser definidas são: `TextRotation` e `Vertical`
Font           | `Font`          | N/D     | Especifica a fonte do eixo vertical.
LogBase        | `float64`       | N/D     | Especifica o número base da escala logarítmica do eixo vertical.
NumFmt         | `ChartNumFmt`   | N/D     | Especifica que se estiver vinculado à origem e definir o código de formato numérico personalizado para o eixo.
Title          | `[]RichTextRun` | N/D     | Especifica que o título do eixo vertical principal e o gráfico de redimensionamento.

O valor de `TextRotation` que pode ser definido de -90 a 90.

Os valores de `Vertical` que podem ser definidos são: `horz`, `vert`, `vert270`, `wordArtVert`, `eaVert`, `mongolianVert` e `wordArtVertRtl`.

Defina o tamanho do gráfico pela propriedade `Dimension`. A propriedade de dimensão é opcional. As propriedades que podem ser definidas são:

Parâmetro|Tipo|Valores padrão|Explicação
---|---|---|---
Height | `uint` | 260 | Altura
Width  | `uint` | 480 | Largura

O parâmetro `combo` especifica a criação de um gráfico que combina dois ou mais tipos de gráfico em um único gráfico. Por exemplo, crie um gráfico de linhas e colunas agrupadas com dados `Planilha1!$E$1:$L$15`:

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
    if err := f.SetSheetName("Sheet1", "Planilha1"); err != nil {
        fmt.Println(err)
        return
    }
    for idx, row := range [][]interface{}{
        {nil, "Maçã", "Laranja", "Pera"},
        {"Pequeno", 2, 3, 3},
        {"Normal", 5, 2, 4},
        {"Grande", 6, 7, 8},
    } {
        cell, err := excelize.CoordinatesToCellName(1, idx+1)
        if err != nil {
            fmt.Println(err)
            return
        }
        if err := f.SetSheetRow("Planilha1", cell, &row); err != nil {
            fmt.Println(err)
            return
        }
    }
    enable, disable := true, false
    if err := f.AddChart("Planilha1", "E1", &excelize.Chart{
        Type: excelize.Col,
        Series: []excelize.ChartSeries{
            {
                Name:       "Planilha1!$A$2",
                Categories: "Planilha1!$B$1:$D$1",
                Values:     "Planilha1!$B$2:$D$2",
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Title: []excelize.RichTextRun{
            {
                Text: "Coluna agrupada - gráfico de linhas",
            },
        },
        Legend: excelize.ChartLegend{
            Position: "left",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }, &excelize.Chart{
        Type: excelize.Line,
        Series: []excelize.ChartSeries{
            {
                Name:       "Planilha1!$A$4",
                Categories: "Planilha1!$B$1:$D$1",
                Values:     "Planilha1!$B$4:$D$4",
                Marker: excelize.ChartMarker{
                    Symbol: "none", Size: 10,
                },
            },
        },
        Format: excelize.GraphicOptions{
            ScaleX:          1,
            ScaleY:          1,
            OffsetX:         15,
            OffsetY:         10,
            PrintObject:     &enable,
            LockAspectRatio: false,
            Locked:          &disable,
        },
        Legend: excelize.ChartLegend{
            Position: "right",
        },
        PlotArea: excelize.ChartPlotArea{
            ShowCatName:     false,
            ShowLeaderLines: false,
            ShowPercent:     true,
            ShowSerName:     true,
            ShowVal:         true,
        },
    }); err != nil {
        fmt.Println(err)
        return
    }
    // Salve a planilha pelo caminho indicado.
    if err := f.SaveAs("Pasta1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

## Adicionar planilha de gráfico {#AddChartSheet}

```go
func (f *File) AddChartSheet(sheet, opts string, combo ...string) error
```

AddChartSheet fornece o método para criar uma planilha de gráfico por determinado conjunto de formato de gráfico (como deslocamento, escala, configuração de proporção de aspecto e configurações de impressão) e conjunto de propriedades. No Excel, uma planilha de gráfico é uma planilha que contém apenas um gráfico.

## Excluir gráfico {#DeleteChart}

```go
func (f *File) DeleteChart(sheet, cell string) error
```

DeleteChart fornece uma função para excluir gráficos em planilhas por determinado nome de planilha e referência de célula.

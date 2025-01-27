# Escrever em modo de fluxo

`StreamWriter` definiu o tipo de gravador de fluxo.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contém campos filtrados ou não exportados
}
```

`Cell` pode ser usado diretamente em `StreamWriter.SetRow` para especificar um estilo e um valor.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

`RowOpts` define as opções para a linha definida, pode ser usado diretamente em `StreamWriter.SetRow` para especificar o estilo e as propriedades da linha.

```go
type RowOpts struct {
    Height       float64
    Hidden       bool
    StyleID      int
    OutlineLevel int
}
```

## Obtenha o gravador de fluxo {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter retorna a estrutura do gravador de fluxo por determinado nome de planilha usado para gravar dados em uma nova planilha vazia existente com grandes quantidades de dados. Observe que depois de gravar dados com o gravador de fluxo para a planilha, você deve chamar o método [`Flush`](stream.md#Flush) para encerrar o processo de gravação de streaming, garantir que a ordem dos números das linhas seja crescente ao definir as linhas e que as funções do modo normal e as funções do modo de fluxo não possam trabalho misturado à gravação de dados nas planilhas. O gravador de fluxo tentará usar arquivos temporários no disco para reduzir o uso de memória quando a memória agrupar dados acima de 16 MB e você não conseguir obter o valor da célula neste momento. Por exemplo, defina dados para uma planilha de tamanho `102400` linhas x `50` colunas com números e estilo:

```go
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
sw, err := f.NewStreamWriter("Planilha1")
if err != nil {
    fmt.Println(err)
    return
}

styleID, err := f.NewStyle(&excelize.Style{Font: &excelize.Font{Color: "777777"}})
if err != nil {
    fmt.Println(err)
    return
}
if err := sw.SetRow("A1",
    []interface{}{
        excelize.Cell{StyleID: styleID, Value: "Dados"},
        []excelize.RichTextRun{
            {Text: "Texto ", Font: &excelize.Font{Color: "2354E8"}},
            {Text: "Rico", Font: &excelize.Font{Color: "E83723"}},
        },
    },
    excelize.RowOpts{Height: 45, Hidden: false}); err != nil {
    fmt.Println(err)
    return
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, err := excelize.CoordinatesToCellName(1, rowID)
    if err != nil {
        fmt.Println(err)
        break
    }
    if err := sw.SetRow(cell, row); err != nil {
        fmt.Println(err)
        break
    }
}
if err := sw.Flush(); err != nil {
    fmt.Println(err)
    return
}
if err := f.SaveAs("Pasta1.xlsx"); err != nil {
    fmt.Println(err)
}
```

Defina o valor da célula e a fórmula da célula para uma planilha com gravador de fluxo:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}})
```

Defina o valor da célula e o estilo das linhas para uma planilha com gravador de fluxo:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}},
    excelize.RowOpts{StyleID: styleID, Height: 20, Hidden: false})
```

Defina o valor da célula e o nível do contorno da linha para uma planilha com gravador de fluxo:

```go
err := sw.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1}}, excelize.RowOpts{OutlineLevel: 1})
```

## Gravar linha da planilha para transmitir {#SetRow}

```go
func (sw *StreamWriter) SetRow(cell string, values []interface{}, opts ...RowOpts) error
```

SetRow grava um array para transmitir linhas, fornecendo uma referência de célula inicial e um ponteiro para um array de valores. Observe que você deve chamar a função [`Flush`](stream.md#Flush) para encerrar o processo de gravação do streaming.

## Adicionar tabela ao fluxo {#AddTable}

```go
func (sw *StreamWriter) AddTable(table *Table) error
```

AddTable cria uma tabela Excel para o `StreamWriter` usando o intervalo de células fornecido e o conjunto de formatos.

Exemplo 1, crie uma tabela de `A1:D5`:

```go
err := sw.AddTable(&excelize.Table{Range: "A1:D5"})
```

Exemplo 2, crie uma tabela de `F2:H6` com formato definido:

```go
disable := false
err := sw.AddTable(&excelize.Table{
    Range:             "F2:H6",
    Name:              "tabela",
    StyleName:         "TableStyleMedium2",
    ShowFirstColumn:   true,
    ShowLastColumn:    true,
    ShowRowStripes:    &disable,
    ShowColumnStripes: true,
})
```

Observe que a tabela deve ter pelo menos duas linhas incluindo o cabeçalho. As células de cabeçalho devem conter strings e ser exclusivas. Atualmente apenas uma tabela é permitida para um `StreamWriter`. [`AddTable`](stream.md#AddTable) deve ser chamado depois que as linhas forem escritas, mas antes de `Flush`. Consulte [`AddTable`](stream.md#AddTable) para obter detalhes sobre o formato da tabela.

## Insira quebra de página para transmitir {#InsertPageBreak}

```go
func (sw *StreamWriter) InsertPageBreak(cell string) error
```

InsertPageBreak cria uma quebra de página para determinar onde termina a página impressa e onde começa a próxima por uma determinada referência de célula, o conteúdo antes da quebra de página será impresso em uma página e depois da quebra em outra.

## Definir painéis para transmitir {#SetPanes}

```go
func (sw *StreamWriter) SetPanes(panes *Panes) error
```

SetPanes fornece uma função para criar e remover painéis congelados e divididos, fornecendo opções de painéis para o `StreamWriter`. Observe que você deve chamar a função `SetPanes` antes da função [`SetRow`](stream.md#SetRow).

## Mesclar célula para transmitir {#MergeCell}

```go
func (sw *StreamWriter) MergeCell(topLeftCell, bottomRightCell string) error
```

MergeCell fornece uma função para mesclar células por uma determinada referência de intervalo para o `StreamWriter`. Não crie uma célula mesclada que se sobreponha a outra célula mesclada existente.

## Defina a largura da coluna para transmitir {#SetColWidth}

```go
func (sw *StreamWriter) SetColWidth(min, max int, width float64) error
```

SetColWidth fornece uma função para definir a largura de uma única coluna ou de várias colunas para o `StreamWriter`. Observe que você deve chamar a função `SetColWidth` antes da função [`SetRow`](stream.md#SetRow). Por exemplo, defina a coluna de largura `B:C` como `20`:

```go
err := sw.SetColWidth(2, 3, 20)
```

## Fluxo de descarga {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush encerrando o processo de gravação do streaming.

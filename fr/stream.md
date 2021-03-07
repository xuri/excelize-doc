# Écriture en flux

StreamWriter a défini le type d'écrivain de flux.

```go
type StreamWriter struct {
    File    *File
    Sheet   string
    SheetID int
    // contient des champs filtrés ou non exportés
}
```

Cell peut être utilisée directement dans StreamWriter.SetRow pour spécifier un style et une valeur.

```go
type Cell struct {
    StyleID int
    Formula string
    Value   interface{}
}
```

## Obtenez le flux écrivain {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter renvoie la structure de l'écrivain de flux par un nom de feuille de calcul donné pour générer une nouvelle feuille de calcul avec de grandes quantités de données. Notez qu'après avoir défini des lignes, vous devez appeler la méthode [`Flush`](stream.md#Flush) pour terminer le processus d'écriture en continu et vous assurer que l'ordre des numéros de ligne est croissant, l'API commune et l'API de flux ne peuvent pas être mélangées à l'écriture de données sur les feuilles de calcul. Par exemple, définissez des données pour la feuille de calcul de taille `102400` lignes x `50` colonnes avec des nombres:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    fmt.Println(err)
}
styleID, err := file.NewStyle(`{"font":{"color":"#777777"}}`)
if err != nil {
    fmt.Println(err)
}
if err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{StyleID: styleID, Value: "Data"}}); err != nil {
    fmt.Println(err)
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, row); err != nil {
        fmt.Println(err)
    }
}
if err := streamWriter.Flush(); err != nil {
    fmt.Println(err)
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    fmt.Println(err)
}
```

Définissez la valeur de la cellule et la formule de la cellule pour une feuille de calcul avec l'écrivain de flux:

```go
err := streamWriter.SetRow("A1", []interface{}{
    excelize.Cell{Value: 1},
    excelize.Cell{Value: 2},
    excelize.Cell{Formula: "SUM(A1,B1)"}});
```

## Écrire la ligne de feuille au flux {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow écrit un tableau sur une ligne de flux par un nom de feuille de calcul donné, une coordonnée de départ et un pointeur sur le type de tableau `slice`. Notez que vous devez appeler la méthode [`Flush`](stream.md#Flush) pour terminer le processus d'écriture en continu.

## Flush le flux {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush mettant fin au processus d'écriture en streaming.

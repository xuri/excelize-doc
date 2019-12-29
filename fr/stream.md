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

## Obtenez le flux écrivain {#NewStreamWriter}

```go
func (f *File) NewStreamWriter(sheet string) (*StreamWriter, error)
```

NewStreamWriter renvoie la structure de l'écrivain de flux par un nom de feuille de calcul donné pour générer une nouvelle feuille de calcul avec de grandes quantités de données. Notez qu'après avoir défini des lignes, vous devez appeler la méthode [`Flush`](stream.md#Flush) pour terminer le processus d'écriture en continu et vous assurer que l'ordre des numéros de ligne est croissant. Par exemple, définissez des données pour la feuille de calcul de taille `102400` lignes x `50` colonnes avec des nombres:

```go
file := excelize.NewFile()
streamWriter, err := file.NewStreamWriter("Sheet1")
if err != nil {
    println(err.Error())
}
styleID, err := file.NewStyle(`{"font":{"color":"#777777"}}`)
if err != nil {
    println(err.Error())
}
if err := streamWriter.SetRow("A1", []interface{}{excelize.Cell{StyleID: styleID, Value: "Data"}}); err != nil {
    println(err.Error())
}
for rowID := 2; rowID <= 102400; rowID++ {
    row := make([]interface{}, 50)
    for colID := 0; colID < 50; colID++ {
        row[colID] = rand.Intn(640000)
    }
    cell, _ := excelize.CoordinatesToCellName(1, rowID)
    if err := streamWriter.SetRow(cell, row); err != nil {
        println(err.Error())
    }
}
if err := streamWriter.Flush(); err != nil {
    println(err.Error())
}
if err := file.SaveAs("Book1.xlsx"); err != nil {
    println(err.Error())
}
```

## Écrire la ligne de feuille au flux {#SetRow}

```go
func (sw *StreamWriter) SetRow(axis string, slice interface{}) error
```

SetRow écrit un tableau sur une ligne de flux par un nom de feuille de calcul donné, une coordonnée de départ et un pointeur sur le type de tableau `slice`. Notez que les paramètres de cellule avec des styles ne sont pas pris en charge actuellement et après les lignes définies, vous devez appeler la méthode [`Flush`](stream.md#Flush) pour mettre fin au processus d'écriture en continu.

## Flush le flux {#Flush}

```go
func (sw *StreamWriter) Flush() error
```

Flush mettant fin au processus d'écriture en streaming.

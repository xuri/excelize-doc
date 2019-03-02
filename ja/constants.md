# 定数

次の定数は、現在サポートされているグラフの種類を定義します:

```go
const (
    Bar                 = "bar"
    BarStacked          = "barStacked"
    BarPercentStacked   = "barPercentStacked"
    Bar3DClustered      = "bar3DClustered"
    Bar3DStacked        = "bar3DStacked"
    Bar3DPercentStacked = "bar3DPercentStacked"
    Col                 = "col"
    ColStacked          = "colStacked"
    ColPercentStacked   = "colPercentStacked"
    Col3DClustered      = "col3DClustered"
    Col3D               = "col3D"
    Col3DStacked        = "col3DStacked"
    Col3DPercentStacked = "col3DPercentStacked"
    Doughnut            = "doughnut"
    Line                = "line"
    Pie                 = "pie"
    Pie3D               = "pie3D"
    Radar               = "radar"
    Scatter             = "scatter"
)
```

次の定数は、XML ラベルの名前空間を定義します:

```go
const (
    SourceRelationship              = "http://schemas.openxmlformats.org/officeDocument/2006/relationships"
    SourceRelationshipChart         = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/chart"
    SourceRelationshipComments      = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/comments"
    SourceRelationshipImage         = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/image"
    SourceRelationshipTable         = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/table"
    SourceRelationshipDrawingML     = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/drawing"
    SourceRelationshipDrawingVML    = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/vmlDrawing"
    SourceRelationshipHyperLink     = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/hyperlink"
    SourceRelationshipWorkSheet     = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/worksheet"
    SourceRelationshipChart201506   = "http://schemas.microsoft.com/office/drawing/2015/06/chart"
    SourceRelationshipChart20070802 = "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"
    SourceRelationshipChart2014     = "http://schemas.microsoft.com/office/drawing/2014/chart"
    SourceRelationshipCompatibility = "http://schemas.openxmlformats.org/markup-compatibility/2006"
    NameSpaceDrawingML              = "http://schemas.openxmlformats.org/drawingml/2006/main"
    NameSpaceDrawingMLChart         = "http://schemas.openxmlformats.org/drawingml/2006/chart"
    NameSpaceDrawingMLSpreadSheet   = "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"
    NameSpaceSpreadSheet            = "http://schemas.openxmlformats.org/spreadsheetml/2006/main"
    NameSpaceXML                    = "http://www.w3.org/XML/1998/namespace"
)
```

次の定数は、EMU (English Metric Units) 単位を定義します:

```go
const (
    EMU int = 9525
)
```

次の定数は、XML ドキュメント内で独立した宣言を定義します:

```go
const XMLHeader = "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n"
```

次の定数は、現在サポートされているデータの入力規則の種類を定義します:

```go
const (
    DataValidationTypeCustom
    DataValidationTypeDate
    DataValidationTypeDecimal
    DataValidationTypeTextLeng
    DataValidationTypeTime
    DataValidationTypeWhole
)
```

次の定数は、現在サポートされているデータ検証条件を定義します:

```go
const (
    DataValidationOperatorBetween
    DataValidationOperatorEqual
    DataValidationOperatorGreaterThan
    DataValidationOperatorGreaterThanOrEqual
    DataValidationOperatorLessThan
    DataValidationOperatorLessThanOrEqual
    DataValidationOperatorNotBetween
    DataValidationOperatorNotEqual
)
```
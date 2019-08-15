# Constants

This section defines the currently supported chart types:

```go
const (
    Area                        = "area"
    AreaStacked                 = "areaStacked"
    AreaPercentStacked          = "areaPercentStacked"
    Area3D                      = "area3D"
    Area3DStacked               = "area3DStacked"
    Area3DPercentStacked        = "area3DPercentStacked"
    Bar                         = "bar"
    BarStacked                  = "barStacked"
    BarPercentStacked           = "barPercentStacked"
    Bar3DClustered              = "bar3DClustered"
    Bar3DStacked                = "bar3DStacked"
    Bar3DPercentStacked         = "bar3DPercentStacked"
    Bar3DConeClustered          = "bar3DConeClustered"
    Bar3DConeStacked            = "bar3DConeStacked"
    Bar3DConePercentStacked     = "bar3DConePercentStacked"
    Bar3DPyramidClustered       = "bar3DPyramidClustered"
    Bar3DPyramidStacked         = "bar3DPyramidStacked"
    Bar3DPyramidPercentStacked  = "bar3DPyramidPercentStacked"
    Bar3DCylinderClustered      = "bar3DCylinderClustered"
    Bar3DCylinderStacked        = "bar3DCylinderStacked"
    Bar3DCylinderPercentStacked = "bar3DCylinderPercentStacked"
    Col                         = "col"
    ColStacked                  = "colStacked"
    ColPercentStacked           = "colPercentStacked"
    Col3D                       = "col3D"
    Col3DClustered              = "col3DClustered"
    Col3DStacked                = "col3DStacked"
    Col3DPercentStacked         = "col3DPercentStacked"
    Col3DCone                   = "col3DCone"
    Col3DConeClustered          = "col3DConeClustered"
    Col3DConeStacked            = "col3DConeStacked"
    Col3DConePercentStacked     = "col3DConePercentStacked"
    Col3DPyramid                = "col3DPyramid"
    Col3DPyramidClustered       = "col3DPyramidClustered"
    Col3DPyramidStacked         = "col3DPyramidStacked"
    Col3DPyramidPercentStacked  = "col3DPyramidPercentStacked"
    Col3DCylinder               = "col3DCylinder"
    Col3DCylinderClustered      = "col3DCylinderClustered"
    Col3DCylinderStacked        = "col3DCylinderStacked"
    Col3DCylinderPercentStacked = "col3DCylinderPercentStacked"
    Doughnut                    = "doughnut"
    Line                        = "line"
    Pie                         = "pie"
    Pie3D                       = "pie3D"
    Radar                       = "radar"
    Scatter                     = "scatter"
    Surface3D                   = "surface3D"
    WireframeSurface3D          = "wireframeSurface3D"
    Contour                     = "contour"
    WireframeContour            = "wireframeContour"
    Bubble                      = "bubble"
    Bubble3D                    = "bubble3D"
)
```

Source relationship and namespace:

```go
const (
    SourceRelationship                   = "http://schemas.openxmlformats.org/officeDocument/2006/relationships"
    SourceRelationshipChart              = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/chart"
    SourceRelationshipComments           = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/comments"
    SourceRelationshipImage              = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/image"
    SourceRelationshipTable              = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/table"
    SourceRelationshipDrawingML          = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/drawing"
    SourceRelationshipDrawingVML         = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/vmlDrawing"
    SourceRelationshipHyperLink          = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/hyperlink"
    SourceRelationshipWorkSheet          = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/worksheet"
    SourceRelationshipVBAProject         = "http://schemas.microsoft.com/office/2006/relationships/vbaProject"
    SourceRelationshipChart201506        = "http://schemas.microsoft.com/office/drawing/2015/06/chart"
    SourceRelationshipChart20070802      = "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"
    SourceRelationshipChart2014          = "http://schemas.microsoft.com/office/drawing/2014/chart"
    SourceRelationshipCompatibility      = "http://schemas.openxmlformats.org/markup-compatibility/2006"
    NameSpaceDrawingML                   = "http://schemas.openxmlformats.org/drawingml/2006/main"
    NameSpaceDrawingMLChart              = "http://schemas.openxmlformats.org/drawingml/2006/chart"
    NameSpaceDrawingMLSpreadSheet        = "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"
    NameSpaceSpreadSheet                 = "http://schemas.openxmlformats.org/spreadsheetml/2006/main"
    NameSpaceSpreadSheetX14              = "http://schemas.microsoft.com/office/spreadsheetml/2009/9/main"
    NameSpaceSpreadSheetX15              = "http://schemas.microsoft.com/office/spreadsheetml/2010/11/main"
    NameSpaceSpreadSheetExcel2006Main    = "http://schemas.microsoft.com/office/excel/2006/main"
    NameSpaceMacExcel2008Main            = "http://schemas.microsoft.com/office/mac/excel/2008/main"
    NameSpaceXML                         = "http://www.w3.org/XML/1998/namespace"
    NameSpaceXMLSchemaInstance           = "http://www.w3.org/2001/XMLSchema-instance"
    StrictSourceRelationship             = "http://purl.oclc.org/ooxml/officeDocument/relationships"
    StrictSourceRelationshipChart        = "http://purl.oclc.org/ooxml/officeDocument/relationships/chart"
    StrictSourceRelationshipComments     = "http://purl.oclc.org/ooxml/officeDocument/relationships/comments"
    StrictSourceRelationshipImage        = "http://purl.oclc.org/ooxml/officeDocument/relationships/image"
    StrictNameSpaceSpreadSheet           = "http://purl.oclc.org/ooxml/spreadsheetml/main"
    NameSpaceDublinCore                  = "http://purl.org/dc/elements/1.1/"
    NameSpaceDublinCoreTerms             = "http://purl.org/dc/terms/"
    NameSpaceDublinCoreMetadataIntiative = "http://purl.org/dc/dcmitype/"
)
```

Define the default cell size and EMU (English Metric Units) unit of measurement:

```go
const (
    EMU int = 9525
)
```

XMLHeader define an XML declaration can also contain a standalone declaration:

```go
const XMLHeader = "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n"
```

This section defines the data validation types.

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

This section defines the data validation operators.

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
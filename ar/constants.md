# الثوابت

يحدد هذا القسم أنواع المخططات المدعومة حاليًا:

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
    PieOfPieChart               = "pieOfPie"
    BarOfPieChart               = "barOfPie"
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

علاقة المصدر ومساحة الاسم:

```go
const (
    SourceRelationshipOfficeDocument             = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"
    SourceRelationshipChart                      = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/chart"
    SourceRelationshipComments                   = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/comments"
    SourceRelationshipImage                      = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/image"
    SourceRelationshipTable                      = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/table"
    SourceRelationshipDrawingML                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/drawing"
    SourceRelationshipDrawingVML                 = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/vmlDrawing"
    SourceRelationshipHyperLink                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/hyperlink"
    SourceRelationshipWorkSheet                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/worksheet"
    SourceRelationshipChartsheet                 = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/chartsheet"
    SourceRelationshipDialogsheet                = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/dialogsheet"
    SourceRelationshipPivotTable                 = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/pivotTable"
    SourceRelationshipPivotCache                 = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/pivotCacheDefinition"
    SourceRelationshipSharedStrings              = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/sharedStrings"
    SourceRelationshipVBAProject                 = "http://schemas.microsoft.com/office/2006/relationships/vbaProject"
    NameSpaceXML                                 = "http://www.w3.org/XML/1998/namespace"
    NameSpaceXMLSchemaInstance                   = "http://www.w3.org/2001/XMLSchema-instance"
    StrictSourceRelationship                     = "http://purl.oclc.org/ooxml/officeDocument/relationships"
    StrictSourceRelationshipOfficeDocument       = "http://purl.oclc.org/ooxml/officeDocument/relationships/officeDocument"
    StrictSourceRelationshipChart                = "http://purl.oclc.org/ooxml/officeDocument/relationships/chart"
    StrictSourceRelationshipComments             = "http://purl.oclc.org/ooxml/officeDocument/relationships/comments"
    StrictSourceRelationshipImage                = "http://purl.oclc.org/ooxml/officeDocument/relationships/image"
    StrictNameSpaceSpreadSheet                   = "http://purl.oclc.org/ooxml/spreadsheetml/main"
    NameSpaceDublinCore                          = "http://purl.org/dc/elements/1.1/"
    NameSpaceDublinCoreTerms                     = "http://purl.org/dc/terms/"
    NameSpaceDublinCoreMetadataInitiative        = "http://purl.org/dc/dcmitype/"
    ContentTypeDrawing                           = "application/vnd.openxmlformats-officedocument.drawing+xml"
    ContentTypeDrawingML                         = "application/vnd.openxmlformats-officedocument.drawingml.chart+xml"
    ContentTypeSheetML                           = "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet.main+xml"
    ContentTypeTemplate                          = "application/vnd.openxmlformats-officedocument.spreadsheetml.template.main+xml"
    ContentTypeAddinMacro                        = "application/vnd.ms-excel.addin.macroEnabled.main+xml"
    ContentTypeMacro                             = "application/vnd.ms-excel.sheet.macroEnabled.main+xml"
    ContentTypeTemplateMacro                     = "application/vnd.ms-excel.template.macroEnabled.main+xml"
    ContentTypeSpreadSheetMLChartsheet           = "application/vnd.openxmlformats-officedocument.spreadsheetml.chartsheet+xml"
    ContentTypeSpreadSheetMLComments             = "application/vnd.openxmlformats-officedocument.spreadsheetml.comments+xml"
    ContentTypeSpreadSheetMLPivotCacheDefinition = "application/vnd.openxmlformats-officedocument.spreadsheetml.pivotCacheDefinition+xml"
    ContentTypeSpreadSheetMLPivotTable           = "application/vnd.openxmlformats-officedocument.spreadsheetml.pivotTable+xml"
    ContentTypeSpreadSheetMLSharedStrings        = "application/vnd.openxmlformats-officedocument.spreadsheetml.sharedStrings+xml"
    ContentTypeSpreadSheetMLTable                = "application/vnd.openxmlformats-officedocument.spreadsheetml.table+xml"
    ContentTypeSpreadSheetMLWorksheet            = "application/vnd.openxmlformats-officedocument.spreadsheetml.worksheet+xml"
    ContentTypeVBA                               = "application/vnd.ms-office.vbaProject"
    ContentTypeVML                               = "application/vnd.openxmlformats-officedocument.vmlDrawing"
    // ExtURIConditionalFormattings is the extLst child element
    // ([ISO/IEC29500-1:2016] section 18.2.10) of the worksheet element
    // ([ISO/IEC29500-1:2016] section 18.3.1.99) is extended by the addition of
    // new child ext elements ([ISO/IEC29500-1:2016] section 18.2.7)
    ExtURIConditionalFormattings = "{78C0D931-6437-407D-A8EE-F0AAD7539E65}"
    ExtURIDataValidations        = "{CCE6A557-97BC-4B89-ADB6-D9C93CAAB3DF}"
    ExtURISparklineGroups        = "{05C60535-1F16-4fd2-B633-F4F36F0B64E0}"
    ExtURISlicerListX14          = "{A8765BA9-456A-4DAB-B4F3-ACF838C121DE}"
    ExtURISlicerCachesListX14    = "{BBE1A952-AA13-448e-AADC-164F8A28A991}"
    ExtURISlicerListX15          = "{3A4CF648-6AED-40f4-86FF-DC5316D8AED3}"
    ExtURIProtectedRanges        = "{FC87AEE6-9EDD-4A0A-B7FB-166176984837}"
    ExtURIIgnoredErrors          = "{01252117-D84E-4E92-8308-4BE1C098FCBB}"
    ExtURIWebExtensions          = "{F7C9EE02-42E1-4005-9D12-6889AFFD525C}"
    ExtURITimelineRefs           = "{7E03D99C-DC04-49d9-9315-930204A7B6E9}"
    ExtURIDrawingBlip            = "{28A0092B-C50C-407E-A947-70E740481C1C}"
    ExtURIMacExcelMX             = "{64002731-A6B0-56B0-2670-7721B7C09600}"
)
```

مواصفات وقيود Excel:

```go
const (
    UnzipSizeLimit       = 1000 << 24
    StreamChunkSize      = 1 << 24
    MaxFontFamilyLength  = 31
    MaxFontSize          = 409
    MaxFilePathLength    = 207
    MaxFieldLength       = 255
    MaxColumnWidth       = 255
    MaxRowHeight         = 409
    TotalRows            = 1048576
    TotalColumns         = 16384
    TotalSheetHyperlinks = 65529
    TotalCellChars       = 32767
)
```

حدد حجم الخلية الافتراضي ووحدة القياس EMU (وحدات القياس الإنجليزية):

```go
const (
    EMU int = 9525
)
```

تعريف XMLHeader يمكن أن يحتوي تعريف XML أيضًا على تصريح مستقل:

```go
const XMLHeader = "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n"
```

يحدد هذا القسم أنواع التحقق من صحة البيانات.

```go
const (
    DataValidationTypeCustom
    DataValidationTypeDate
    DataValidationTypeDecimal
    DataValidationTypeTextLength
    DataValidationTypeTime
    DataValidationTypeWhole
)
```

يحدد هذا القسم عوامل التحقق من صحة البيانات.

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

CellType هو نوع نوع قيمة الخلية.

```go
const (
    CellTypeUnset CellType = iota
    CellTypeBool
    CellTypeDate
    CellTypeError
    CellTypeNumber
    CellTypeString
)
```

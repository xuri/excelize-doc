# 상수

이 섹션에서는 현재 지원되는 차트 유형을 정의합니다:

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

소스 관계 및 네임스페이스:

```go
const (
    ContentTypeAddinMacro                         = "application/vnd.ms-excel.addin.macroEnabled.main+xml"
    ContentTypeDrawing                            = "application/vnd.openxmlformats-officedocument.drawing+xml"
    ContentTypeDrawingML                          = "application/vnd.openxmlformats-officedocument.drawingml.chart+xml"
    ContentTypeMacro                              = "application/vnd.ms-excel.sheet.macroEnabled.main+xml"
    ContentTypeSheetML                            = "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet.main+xml"
    ContentTypeSpreadSheetMLChartsheet            = "application/vnd.openxmlformats-officedocument.spreadsheetml.chartsheet+xml"
    ContentTypeSpreadSheetMLComments              = "application/vnd.openxmlformats-officedocument.spreadsheetml.comments+xml"
    ContentTypeSpreadSheetMLPivotCacheDefinition  = "application/vnd.openxmlformats-officedocument.spreadsheetml.pivotCacheDefinition+xml"
    ContentTypeSpreadSheetMLPivotTable            = "application/vnd.openxmlformats-officedocument.spreadsheetml.pivotTable+xml"
    ContentTypeSpreadSheetMLSharedStrings         = "application/vnd.openxmlformats-officedocument.spreadsheetml.sharedStrings+xml"
    ContentTypeSpreadSheetMLTable                 = "application/vnd.openxmlformats-officedocument.spreadsheetml.table+xml"
    ContentTypeSpreadSheetMLWorksheet             = "application/vnd.openxmlformats-officedocument.spreadsheetml.worksheet+xml"
    ContentTypeTemplate                           = "application/vnd.openxmlformats-officedocument.spreadsheetml.template.main+xml"
    ContentTypeTemplateMacro                      = "application/vnd.ms-excel.template.macroEnabled.main+xml"
    ContentTypeVBA                                = "application/vnd.ms-office.vbaProject"
    ContentTypeVML                                = "application/vnd.openxmlformats-officedocument.vmlDrawing"
    NameSpaceDrawingMLMain                        = "http://schemas.openxmlformats.org/drawingml/2006/main"
    NameSpaceDublinCore                           = "http://purl.org/dc/elements/1.1/"
    NameSpaceDublinCoreMetadataInitiative         = "http://purl.org/dc/dcmitype/"
    NameSpaceDublinCoreTerms                      = "http://purl.org/dc/terms/"
    NameSpaceExtendedProperties                   = "http://schemas.openxmlformats.org/officeDocument/2006/extended-properties"
    NameSpaceXML                                  = "http://www.w3.org/XML/1998/namespace"
    NameSpaceXMLSchemaInstance                    = "http://www.w3.org/2001/XMLSchema-instance"
    SourceRelationshipChart                       = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/chart"
    SourceRelationshipChartsheet                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/chartsheet"
    SourceRelationshipComments                    = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/comments"
    SourceRelationshipDialogsheet                 = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/dialogsheet"
    SourceRelationshipDrawingML                   = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/drawing"
    SourceRelationshipDrawingVML                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/vmlDrawing"
    SourceRelationshipExtendProperties            = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/extended-properties"
    SourceRelationshipHyperLink                   = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/hyperlink"
    SourceRelationshipImage                       = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/image"
    SourceRelationshipOfficeDocument              = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"
    SourceRelationshipPivotCache                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/pivotCacheDefinition"
    SourceRelationshipPivotTable                  = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/pivotTable"
    SourceRelationshipSharedStrings               = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/sharedStrings"
    SourceRelationshipTable                       = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/table"
    SourceRelationshipVBAProject                  = "http://schemas.microsoft.com/office/2006/relationships/vbaProject"
    SourceRelationshipWorkSheet                   = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/worksheet"
    StrictNameSpaceDocumentPropertiesVariantTypes = "http://purl.oclc.org/ooxml/officeDocument/docPropsVTypes"
    StrictNameSpaceDrawingMLMain                  = "http://purl.oclc.org/ooxml/drawingml/main"
    StrictNameSpaceExtendedProperties             = "http://purl.oclc.org/ooxml/officeDocument/extendedProperties"
    StrictNameSpaceSpreadSheet                    = "http://purl.oclc.org/ooxml/spreadsheetml/main"
    StrictSourceRelationship                      = "http://purl.oclc.org/ooxml/officeDocument/relationships"
    StrictSourceRelationshipChart                 = "http://purl.oclc.org/ooxml/officeDocument/relationships/chart"
    StrictSourceRelationshipComments              = "http://purl.oclc.org/ooxml/officeDocument/relationships/comments"
    StrictSourceRelationshipExtendProperties      = "http://purl.oclc.org/ooxml/officeDocument/relationships/extendedProperties"
    StrictSourceRelationshipImage                 = "http://purl.oclc.org/ooxml/officeDocument/relationships/image"
    StrictSourceRelationshipOfficeDocument        = "http://purl.oclc.org/ooxml/officeDocument/relationships/officeDocument"
    // ExtURIConditionalFormattings is the extLst child element
    // ([ISO/IEC29500-1:2016] section 18.2.10) of the worksheet element
    // ([ISO/IEC29500-1:2016] section 18.3.1.99) is extended by the addition of
    // new child ext elements ([ISO/IEC29500-1:2016] section 18.2.7)
    ExtURIConditionalFormattingRuleID = "{B025F937-C7B1-47D3-B67F-A62EFF666E3E}"
    ExtURIConditionalFormattings      = "{78C0D931-6437-407d-A8EE-F0AAD7539E65}"
    ExtURIDataValidations             = "{CCE6A557-97BC-4B89-ADB6-D9C93CAAB3DF}"
    ExtURIDrawingBlip                 = "{28A0092B-C50C-407E-A947-70E740481C1C}"
    ExtURIIgnoredErrors               = "{01252117-D84E-4E92-8308-4BE1C098FCBB}"
    ExtURIMacExcelMX                  = "{64002731-A6B0-56B0-2670-7721B7C09600}"
    ExtURIProtectedRanges             = "{FC87AEE6-9EDD-4A0A-B7FB-166176984837}"
    ExtURISlicerCachesListX14         = "{BBE1A952-AA13-448e-AADC-164F8A28A991}"
    ExtURISlicerListX14               = "{A8765BA9-456A-4DAB-B4F3-ACF838C121DE}"
    ExtURISlicerListX15               = "{3A4CF648-6AED-40f4-86FF-DC5316D8AED3}"
    ExtURISparklineGroups             = "{05C60535-1F16-4fd2-B633-F4F36F0B64E0}"
    ExtURISVG                         = "{96DAC541-7B7A-43D3-8B79-37D633B846F1}"
    ExtURITimelineRefs                = "{7E03D99C-DC04-49d9-9315-930204A7B6E9}"
    ExtURIWebExtensions               = "{F7C9EE02-42E1-4005-9D12-6889AFFD525C}"
)
```

Excel 사양 및 제한:

```go
const (
    MaxCellStyles        = 64000
    MaxColumns           = 16384
    MaxColumnWidth       = 255
    MaxFieldLength       = 255
    MaxFilePathLength    = 207
    MaxFontFamilyLength  = 31
    MaxFontSize          = 409
    MaxRowHeight         = 409
    MaxSheetNameLength   = 31
    MinColumns           = 1
    MinFontSize          = 1
    StreamChunkSize      = 1 << 24
    TotalCellChars       = 32767
    TotalRows            = 1048576
    TotalSheetHyperlinks = 65529
    UnzipSizeLimit       = 1000 << 24
)
```

기본 셀 크기 및 EMU(영어 메트릭 단위) 측정 단위 정의:

```go
const (
    EMU int = 9525
)
```

이 섹션에서는 데이터 유효성 검사 형식을 정의합니다.

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

이 섹션에서는 데이터 유효성 검사 연산자.

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

CellType 은 셀 값 유형의 유형입니다.

```go
const (
    CellTypeUnset CellType = iota
    CellTypeBool
    CellTypeDate
    CellTypeError
    CellTypeFormula
    CellTypeInlineString
    CellTypeNumber
    CellTypeSharedString
)
```

ColorMappingType 은 색상 변환 유형입니다.

```go
const (
    ColorMappingTypeLight1 ColorMappingType = iota
    ColorMappingTypeDark1
    ColorMappingTypeLight2
    ColorMappingTypeDark2
    ColorMappingTypeAccent1
    ColorMappingTypeAccent2
    ColorMappingTypeAccent3
    ColorMappingTypeAccent4
    ColorMappingTypeAccent5
    ColorMappingTypeAccent6
    ColorMappingTypeHyperlink
    ColorMappingTypeFollowedHyperlink
    ColorMappingTypeUnsetValue int = -1
)
```

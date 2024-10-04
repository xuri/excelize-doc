# 常量

{{ book.info }}

CultureName 是受支援的區域格式類別定義。

```go
type CultureName byte
```

部分存儲格數字格式受到作業系統特定的區域日期和時間設定的影響，以下這些常量定義了當前支援的區域格式類別列舉：

```go
const (
    CultureNameUnknown CultureName = iota
    CultureNameEnUS
    CultureNameZhCN
)
```

ChartType 是受支援的圖表類別定義。

```go
type ChartType byte
```

以下這些常量定義了當前支援的圖表類別列舉：

```go
const (
    Area ChartType = iota
    AreaStacked
    AreaPercentStacked
    Area3D
    Area3DStacked
    Area3DPercentStacked
    Bar
    BarStacked
    BarPercentStacked
    Bar3DClustered
    Bar3DStacked
    Bar3DPercentStacked
    Bar3DConeClustered
    Bar3DConeStacked
    Bar3DConePercentStacked
    Bar3DPyramidClustered
    Bar3DPyramidStacked
    Bar3DPyramidPercentStacked
    Bar3DCylinderClustered
    Bar3DCylinderStacked
    Bar3DCylinderPercentStacked
    Col
    ColStacked
    ColPercentStacked
    Col3D
    Col3DClustered
    Col3DStacked
    Col3DPercentStacked
    Col3DCone
    Col3DConeClustered
    Col3DConeStacked
    Col3DConePercentStacked
    Col3DPyramid
    Col3DPyramidClustered
    Col3DPyramidStacked
    Col3DPyramidPercentStacked
    Col3DCylinder
    Col3DCylinderClustered
    Col3DCylinderStacked
    Col3DCylinderPercentStacked
    Doughnut
    Line
    Line3D
    Pie
    Pie3D
    PieOfPie
    BarOfPie
    Radar
    Scatter
    Surface3D
    WireframeSurface3D
    Contour
    WireframeContour
    Bubble
    Bubble3D
)
```

以下這些常量定義了 XML 標籤的命名空間：

```go
const (
    ContentTypeAddinMacro                         = "application/vnd.ms-excel.addin.macroEnabled.main+xml"
    ContentTypeDrawing                            = "application/vnd.openxmlformats-officedocument.drawing+xml"
    ContentTypeDrawingML                          = "application/vnd.openxmlformats-officedocument.drawingml.chart+xml"
    ContentTypeMacro                              = "application/vnd.ms-excel.sheet.macroEnabled.main+xml"
    ContentTypeRelationships                      = "application/vnd.openxmlformats-package.relationships+xml"
    ContentTypeSheetML                            = "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet.main+xml"
    ContentTypeSlicer                             = "application/vnd.ms-excel.slicer+xml"
    ContentTypeSlicerCache                        = "application/vnd.ms-excel.slicerCache+xml"
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
    SourceRelationshipSlicer                      = "http://schemas.microsoft.com/office/2007/relationships/slicer"
    SourceRelationshipSlicerCache                 = "http://schemas.microsoft.com/office/2007/relationships/slicerCache"
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
    // The following constants defined the extLst child element
    // ([ISO/IEC29500-1:2016] section 18.2.10) of the workbook and worksheet
    // elements extended by the addition of new child ext elements.
    ExtURICalcFeatures                   = "{B58B0392-4F1F-4190-BB64-5DF3571DCE5F}"
    ExtURIConditionalFormattingRuleID    = "{B025F937-C7B1-47D3-B67F-A62EFF666E3E}"
    ExtURIConditionalFormattings         = "{78C0D931-6437-407d-A8EE-F0AAD7539E65}"
    ExtURIDataField                      = "{E15A36E0-9728-4E99-A89B-3F7291B0FE68}"
    ExtURIDataModel                      = "{FCE2AD5D-F65C-4FA6-A056-5C36A1767C68}"
    ExtURIDataValidations                = "{CCE6A557-97BC-4b89-ADB6-D9C93CAAB3DF}"
    ExtURIDrawingBlip                    = "{28A0092B-C50C-407E-A947-70E740481C1C}"
    ExtURIExternalLinkPr                 = "{FCE6A71B-6B00-49CD-AB44-F6B1AE7CDE65}"
    ExtURIIgnoredErrors                  = "{01252117-D84E-4E92-8308-4BE1C098FCBB}"
    ExtURIMacExcelMX                     = "{64002731-A6B0-56B0-2670-7721B7C09600}"
    ExtURIModelTimeGroupings             = "{9835A34E-60A6-4A7C-AAB8-D5F71C897F49}"
    ExtURIPivotCacheDefinition           = "{725AE2AE-9491-48be-B2B4-4EB974FC3084}"
    ExtURIPivotCachesX14                 = "{876F7934-8845-4945-9796-88D515C7AA90}"
    ExtURIPivotCachesX15                 = "{841E416B-1EF1-43b6-AB56-02D37102CBD5}"
    ExtURIPivotField                     = "{2946ED86-A175-432a-8AC1-64E0C546D7DE}"
    ExtURIPivotFilter                    = "{0605FD5F-26C8-4aeb-8148-2DB25E43C511}"
    ExtURIPivotHierarchy                 = "{F1805F06-0CD304483-9156-8803C3D141DF}"
    ExtURIPivotTableReferences           = "{983426D0-5260-488c-9760-48F4B6AC55F4}"
    ExtURIProtectedRanges                = "{FC87AEE6-9EDD-4A0A-B7FB-166176984837}"
    ExtURISlicerCacheDefinition          = "{2F2917AC-EB37-4324-AD4E-5DD8C200BD13}"
    ExtURISlicerCacheHideItemsWithNoData = "{470722E0-AACD-4C17-9CDC-17EF765DBC7E}"
    ExtURISlicerCachesX14                = "{BBE1A952-AA13-448e-AADC-164F8A28A991}"
    ExtURISlicerCachesX15                = "{46BE6895-7355-4a93-B00E-2C351335B9C9}"
    ExtURISlicerListX14                  = "{A8765BA9-456A-4dab-B4F3-ACF838C121DE}"
    ExtURISlicerListX15                  = "{3A4CF648-6AED-40f4-86FF-DC5316D8AED3}"
    ExtURISparklineGroups                = "{05C60535-1F16-4fd2-B633-F4F36F0B64E0}"
    ExtURISVG                            = "{96DAC541-7B7A-43D3-8B79-37D633B846F1}"
    ExtURITimelineCachePivotCaches       = "{A2CB5862-8E78-49c6-8D9D-AF26E26ADB89}"
    ExtURITimelineCacheRefs              = "{D0CA8CA8-9F24-4464-BF8E-62219DCF47F9}"
    ExtURITimelineRefs                   = "{7E03D99C-DC04-49d9-9315-930204A7B6E9}"
    ExtURIWebExtensions                  = "{F7C9EE02-42E1-4005-9D12-6889AFFD525C}"
    ExtURIWorkbookPrX14                  = "{79F54976-1DA5-4618-B147-ACDE4B953A38}"
    ExtURIWorkbookPrX15                  = "{140A7094-0E35-4892-8432-C4D2E57EDEB5}"
)
```

下面的常量定義了 Excel 工作表和活頁簿規範與限制：

```go
const (
    MaxCellStyles        = 65430
    MaxColumns           = 16384
    MaxColumnWidth       = 255
    MaxFieldLength       = 255
    MaxFilePathLength    = 207
    MaxFormControlValue  = 30000
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

下面的常量定義了 EMU (English Metric Units) 單位：

```go
const (
    EMU int = 9525
)
```

以下這些常量定義了當前支援的資料驗證類別：

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

以下這些常量定義了當前支援的資料驗證條件：

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

CellType 定義了存儲格的數據類型：

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

ColorMappingType 定義了色彩轉換枚舉類型：

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

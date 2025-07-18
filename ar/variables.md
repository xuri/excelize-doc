# المتغيرات

```go
var (
    // حدد ErrAddVBAProject رسالة الخطأ عند إضافة مشروع VBA في المصنف.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // حدد ErrAttrValBool رسالة الخطأ على سمة XML من النوع المنطقي التنظيمي وغير المنظم.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // حدد ErrCellCharsLength رسالة الخطأ لتلقي طول حرف الخلية الذي يتجاوز الحد.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // حدد ErrCellStyles رسالة الخطأ على أنماط الخلية يتجاوز الحد.
    ErrCellStyles = fmt.Errorf("the cell styles exceeds the %d limit", MaxCellStyles)
    // حدد ErrColumnNumber رسالة الخطأ عند تلقي رقم عمود غير صالح.
    ErrColumnNumber = fmt.Errorf(`the column number must be greater than or equal to %d and less than or equal to %d`, MinColumns, MaxColumns)
    // حدد ErrColumnWidth رسالة الخطأ عند تلقي عرض عمود غير صالح.
    ErrColumnWidth = fmt.Errorf("the width of the column must be less than or equal to %d characters", MaxColumnWidth)
    // حدد ErrCoordinates رسالة الخطأ على طول مجموعات الإحداثيات غير الصالحة.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // حدد ErrCustomNumFmt رسالة الخطأ عند استلام تنسيق الأرقام المخصص الفارغ.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // حدد ErrDataValidationFormulaLength رسالة الخطأ لتلقي طول صيغة التحقق من صحة البيانات الذي يتجاوز الحد.
    ErrDataValidationFormulaLength = fmt.Errorf("data validation must be 0-%d characters", MaxFieldLength)
    // حدد ErrDataValidationRange رسالة الخطأ على نطاق عشري معين يتجاوز الحد.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // حدد ErrDefinedNameDuplicate رسالة الخطأ على نفس الاسم الموجود بالفعل في النطاق.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // حدد ErrDefinedNameScope رسالة الخطأ على الاسم المعرّف غير الموجود في النطاق المحدد.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // حدد ErrExistsSheet رسالة الخطأ في ورقة عمل معينة موجودة بالفعل.
    ErrExistsSheet = errors.New("the same name sheet already exists")
    // حدد ErrExistsTableName رسالة الخطأ في الجدول المحدد موجود بالفعل.
    ErrExistsTableName = errors.New("the same name table already exists")
    // حدد ErrFontLength رسالة الخطأ على طول تجاوز اسم عائلة الخط.
    ErrFontLength = fmt.Errorf("the length of the font family name must be less than or equal to %d", MaxFontFamilyLength)
    // حدد ErrFontSize رسالة الخطأ على حجم الخط غير صالح.
    ErrFontSize = fmt.Errorf("font size must be an integer from %d to %d points", MinFontSize, MaxFontSize)
    // حدد ErrFormControlValue رسالة الخطأ لتلقي قيمة تمرير تتجاوز الحد.
    ErrFormControlValue = fmt.Errorf("scroll value must be an integer from 0 to %d", MaxFormControlValue)
    // حدد ErrGroupSheets رسالة الخطأ في أوراق المجموعة.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // حدد ErrImgExt رسالة الخطأ عند تلقي ملحق صورة غير مدعوم.
    ErrImgExt = errors.New("unsupported image extension")
    // حدد ErrInvalidFormula رسالة الخطأ عند تلقي صيغة غير صالحة.
    ErrInvalidFormula = errors.New("formula not valid")
    // حدد ErrMaxFilePathLength رسالة الخطأ عند تلقي تجاوز طول مسار الملف.
    ErrMaxFilePathLength = fmt.Errorf("file path length exceeds maximum limit %d characters", MaxFilePathLength)
    // حدد ErrMaxRowHeight رسالة الخطأ عند تلقي ارتفاع غير صالح للصف.
    ErrMaxRowHeight = fmt.Errorf("the height of the row must be less than or equal to %d points", MaxRowHeight)
    // حدد ErrMaxRows رسالة الخطأ عند تلقي رقم صف يتجاوز الحد الأقصى.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // حدد ErrNameLength رسالة الخطأ عند تلقي الاسم المحدد أو تجاوز طول اسم الجدول الحد.
    ErrNameLength = fmt.Errorf("the name length exceeds the %d characters limit", MaxFieldLength)
    // حدد ErrOptionsUnzipSizeLimit رسالة الخطأ لتلقي UnzipSizeLimit و UnzipXMLSizeLimit غير صالحين.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // حدد ErrOutlineLevel رسالة الخطأ عند تلقي رقم مستوى مخطط تفصيلي غير صالح.
    ErrOutlineLevel = errors.New("invalid outline level")
    // قام ErrPageSetupAdjustTo بتعريف رسالة الخطأ الخاصة باستلام ضبط إعداد الصفحة لقيمة تتجاوز الحد.
    ErrPageSetupAdjustTo = errors.New("adjust to value must be an integer from 0 to 400")
    // حدد ErrParameterInvalid رسالة الخطأ عند تلقي المعلمة غير الصالحة.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // حدد ErrParameterRequired رسالة الخطأ عند تلقي المعلمة الفارغة.
    ErrParameterRequired = errors.New("parameter is required")
    // حدد ErrPasswordLengthInvalid رسالة الخطأ بطول كلمة المرور غير الصالحة.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // قام ErrPivotTableClassicLayout بتعريف رسالة الخطأ عند تمكين ClassicLayout و CompactData في نفس الوقت.
    ErrPivotTableClassicLayout = errors.New("cannot enable ClassicLayout and CompactData in the same time")
    // حدد ErrSave رسالة الخطأ لحفظ الملف.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // حدد ErrSheetIdx رسالة الخطأ عند تلقي فهرس ورقة العمل غير صالح.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // حدد ErrSheetNameBlank رسالة الخطأ عند تلقي اسم الورقة الفارغة.
    ErrSheetNameBlank = errors.New("the sheet name can not be blank")
    // حدد ErrSheetNameInvalid رسالة الخطأ عند تلقي اسم الورقة يحتوي على أحرف غير صالحة.
    ErrSheetNameInvalid = errors.New("the sheet can not contain any of the characters :\\/?*[or]")
    // حدد ErrSheetNameLength رسالة الخطأ عند تلقي اسم الورقة يتجاوز الحد المسموح به.
    ErrSheetNameLength = fmt.Errorf("the sheet name length exceeds the %d characters limit", MaxSheetNameLength)
    // حدد ErrSheetNameSingleQuote رسالة الخطأ على الحرف الأول أو الأخير من اسم الورقة كان اقتباسًا منفردًا.
    ErrSheetNameSingleQuote = errors.New("the first or last character of the sheet name can not be a single quote")
    // حدد ErrSparkline رسالة الخطأ عند تلقي معلمات خط المؤشر غير الصالحة.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // حدد ErrSparklineLocation رسالة الخطأ على معلمات 'Location' المفقودة.
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // حدد ErrSparklineRange رسالة الخطأ على معلمات خط المؤشر المفقودة 'Range'.
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // حدد ErrSparklineStyle رسالة الخطأ عند تلقي معلمات خط المؤشر غير الصالحة 'Style'.
    ErrSparklineStyle = errors.New("parameter 'Style' value must be an integer from 0 to 35")
    // حدد ErrSparklineType رسالة الخطأ عند تلقي معلمات نوع خط المؤشر غير الصالحة.
    ErrSparklineType = errors.New("parameter 'Type' value must be one of 'line', 'column' or 'win_loss'")
    // قام ErrStreamSetColStyle بتعريف رسالة الخطأ عند تعيين نمط العمود في وضع الكتابة المتدفقة.
    ErrStreamSetColStyle = errors.New("must call the SetColStyle function before the SetRow function")
    // حدد ErrStreamSetColWidth رسالة الخطأ على عرض العمود المحدد في وضع كتابة الدفق.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // حدد ErrStreamSetPanes رسالة الخطأ في الأجزاء المحددة في وضع كتابة الدفق.
    ErrStreamSetPanes = errors.New("must call the SetPanes function before the SetRow function")
    // حدد ErrTotalSheetHyperlinks رسالة الخطأ على تجاوز عدد الارتباطات التشعبية.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // قام ErrTransparency بتعريف رسالة الخطأ الخاصة باستلام قيمة شفافية تتجاوز الحد.
    ErrTransparency = errors.New("transparency value must be an integer from 0 to 100")
    // حدد ErrUnknownEncryptMechanism رسالة الخطأ على آلية تشفير غير مدعومة.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // حدد ErrUnprotectSheet رسالة الخطأ في ورقة العمل ولم تحدد أي حماية.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // حدد ErrUnprotectSheetPassword رسالة الخطأ على إزالة حماية الورقة مع فشل التحقق من كلمة المرور.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // حدد ErrUnprotectWorkbook رسالة الخطأ في المصنف ولم يقم بتعيين أي حماية.
    ErrUnprotectWorkbook = errors.New("workbook has set no protect")
    // حدد ErrUnprotectWorkbookPassword رسالة الخطأ عند إزالة حماية المصنف مع فشل التحقق من كلمة المرور.
    ErrUnprotectWorkbookPassword = errors.New("workbook protect password not match")
    // حدد ErrUnsupportedEncryptMechanism رسالة الخطأ على آلية تشفير غير مدعومة.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // حدد ErrUnsupportedHashAlgorithm رسالة الخطأ على خوارزمية تجزئة غير مدعومة.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // حدد ErrUnsupportedNumberFormat رسالة الخطأ على تعبير تنسيق رقم غير مدعوم.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // حدد ErrWorkbookFileFormat رسالة الخطأ عند تلقي تنسيق ملف مصنف غير معتمد.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // حدد ErrWorkbookPassword رسالة الخطأ عند تلقي كلمة مرور المصنف غير الصحيحة.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

علاقة المصدر وقائمة مساحة الاسم والبادئات المرتبطة والمخطط الذي تم تقديمه فيه:

```go
var (
    NameSpaceDocumentPropertiesVariantTypes = xml.Attr{Name: xml.Name{Local: "vt", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes"}
    NameSpaceDrawing2016SVG                 = xml.Attr{Name: xml.Name{Local: "asvg", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2016/SVG/main"}
    NameSpaceDrawingML                      = xml.Attr{Name: xml.Name{Local: "a", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/main"}
    NameSpaceDrawingMLA14                   = xml.Attr{Name: xml.Name{Local: "a14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2010/main"}
    NameSpaceDrawingMLChart                 = xml.Attr{Name: xml.Name{Local: "c", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/chart"}
    NameSpaceDrawingMLSlicer                = xml.Attr{Name: xml.Name{Local: "sle", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2010/slicer"}
    NameSpaceDrawingMLSlicerX15             = xml.Attr{Name: xml.Name{Local: "sle15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2012/slicer"}
    NameSpaceDrawingMLSpreadSheet           = xml.Attr{Name: xml.Name{Local: "xdr", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"}
    NameSpaceMacExcel2008Main               = xml.Attr{Name: xml.Name{Local: "mx", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/mac/excel/2008/main"}
    NameSpaceSpreadSheet                    = xml.Attr{Name: xml.Name{Local: "xmlns"}, Value: "http://schemas.openxmlformats.org/spreadsheetml/2006/main"}
    NameSpaceSpreadSheetExcel2006Main       = xml.Attr{Name: xml.Name{Local: "xne", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/excel/2006/main"}
    NameSpaceSpreadSheetX14                 = xml.Attr{Name: xml.Name{Local: "x14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2009/9/main"}
    NameSpaceSpreadSheetX15                 = xml.Attr{Name: xml.Name{Local: "x15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2010/11/main"}
    NameSpaceSpreadSheetXR10                = xml.Attr{Name: xml.Name{Local: "xr10", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2016/revision10"}
    SourceRelationship                      = xml.Attr{Name: xml.Name{Local: "r", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/relationships"}
    SourceRelationshipChart20070802         = xml.Attr{Name: xml.Name{Local: "c14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"}
    SourceRelationshipChart2014             = xml.Attr{Name: xml.Name{Local: "c16", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2014/chart"}
    SourceRelationshipChart201506           = xml.Attr{Name: xml.Name{Local: "c16r2", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2015/06/chart"}
    SourceRelationshipCompatibility         = xml.Attr{Name: xml.Name{Local: "mc", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/markup-compatibility/2006"}
)
```

IndexedColorMapping هو جدول التعيينات الافتراضية من قيمة اللون المفهرس إلى قيمة RGB. لاحظ أن 0-7 هي زائدة عن الحاجة من 8-15 للحفاظ على التوافق مع الإصدارات السابقة. نظام فهرسة قديم للألوان لا يزال مطلوبًا لبعض السجلات وللتوافق مع الإصدارات السابقة مع التنسيقات القديمة. يحتوي هذا العنصر على تسلسل من قيم ألوان RGB التي تتوافق مع فهارس الألوان (على أساس الصفر). عند استخدام لوحة الألوان المفهرسة الافتراضية ، لا يتم كتابة القيم ، ولكن يتم تضمينها بدلاً من ذلك. عندما يتم تعديل لوحة الألوان عن الوضع الافتراضي ، يتم كتابة لوحة الألوان بالكامل.

```go
var IndexedColorMapping = []string{
    "000000", "FFFFFF", "FF0000", "00FF00", "0000FF", "FFFF00", "FF00FF", "00FFFF",
    "000000", "FFFFFF", "FF0000", "00FF00", "0000FF", "FFFF00", "FF00FF", "00FFFF",
    "800000", "008000", "000080", "808000", "800080", "008080", "C0C0C0", "808080",
    "9999FF", "993366", "FFFFCC", "CCFFFF", "660066", "FF8080", "0066CC", "CCCCFF",
    "000080", "FF00FF", "FFFF00", "00FFFF", "800080", "800000", "008080", "0000FF",
    "00CCFF", "CCFFFF", "CCFFCC", "FFFF99", "99CCFF", "FF99CC", "CC99FF", "FFCC99",
    "3366FF", "33CCCC", "99CC00", "FFCC00", "FF9900", "FF6600", "666699", "969696",
    "003366", "339966", "003300", "333300", "993300", "993366", "333399", "333333",
    "000000", "FFFFFF",
}
```

# المتغيرات

```go
var (
    // حدد ErrStreamSetColWidth رسالة الخطأ على عرض العمود المحدد في وضع كتابة
    // الدفق.
    ErrStreamSetColWidth = errors.New("must call the SetColWidth function before the SetRow function")
    // حدد ErrColumnNumber رسالة الخطأ عند تلقي رقم عمود غير صالح.
    ErrColumnNumber = errors.New("column number exceeds maximum limit")
    // حدد ErrColumnWidth رسالة الخطأ عند تلقي عرض عمود غير صالح.
    ErrColumnWidth = fmt.Errorf("the width of the column must be smaller than or equal to %d characters", MaxColumnWidth)
    // حدد ErrOutlineLevel رسالة الخطأ عند تلقي رقم مستوى مخطط تفصيلي غير صالح.
    ErrOutlineLevel = errors.New("invalid outline level")
    // حددت ErrCoordinates رسالة الخطأ على طول مجموعات الإحداثيات غير الصالحة.
    ErrCoordinates = errors.New("coordinates length must be 4")
    // حددت ErrExistsWorksheet رسالة الخطأ في ورقة عمل معينة موجودة بالفعل.
    ErrExistsWorksheet = errors.New("the same name worksheet already exists")
    // حدد ErrTotalSheetHyperlinks رسالة الخطأ على تجاوز عدد الارتباطات
    // التشعبية.
    ErrTotalSheetHyperlinks = errors.New("over maximum limit hyperlinks in a worksheet")
    // حدد ErrInvalidFormula رسالة الخطأ عند تلقي صيغة غير صالحة.
    ErrInvalidFormula = errors.New("formula not valid")
    // حدد ErrAddVBAProject رسالة الخطأ عند إضافة مشروع VBA في المصنف.
    ErrAddVBAProject = errors.New("unsupported VBA project extension")
    // حدد ErrMaxRows رسالة الخطأ عند تلقي رقم صف يتجاوز الحد الأقصى.
    ErrMaxRows = errors.New("row number exceeds maximum limit")
    // حدد ErrMaxRowHeight رسالة الخطأ عند تلقي ارتفاع غير صالح للصف.
    ErrMaxRowHeight = errors.New("the height of the row must be smaller than or equal to 409 points")
    // حدد ErrImgExt رسالة الخطأ عند تلقي ملحق صورة غير مدعوم.
    ErrImgExt = errors.New("unsupported image extension")
    // حدد ErrWorkbookFileFormat رسالة الخطأ عند تلقي تنسيق ملف مصنف غير معتمد.
    ErrWorkbookFileFormat = errors.New("unsupported workbook file format")
    // حدد ErrMaxFilePathLength رسالة الخطأ عند تلقي تجاوز طول مسار الملف.
    ErrMaxFilePathLength = errors.New("file path length exceeds maximum limit")
    // حدد ErrEncrypt رسالة الخطأ في جدول بيانات التشفير.
    ErrEncrypt = errors.New("not support encryption currently")
    // حدد ErrUnknownEncryptMechanism رسالة الخطأ على آلية تشفير غير مدعومة.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // حدد ErrUnsupportedEncryptMechanism رسالة الخطأ على آلية تشفير غير مدعومة.
    ErrUnsupportedEncryptMechanism = errors.New("unsupported encryption mechanism")
    // حدد ErrUnsupportedHashAlgorithm رسالة الخطأ على خوارزمية تجزئة غير مدعومة.
    ErrUnsupportedHashAlgorithm = errors.New("unsupported hash algorithm")
    // حدد ErrUnsupportedNumberFormat رسالة الخطأ على تعبير تنسيق رقم غير مدعوم.
    ErrUnsupportedNumberFormat = errors.New("unsupported number format token")
    // حدد ErrPasswordLengthInvalid رسالة الخطأ بطول كلمة المرور غير الصالحة.
    ErrPasswordLengthInvalid = errors.New("password length invalid")
    // حدد ErrParameterRequired رسالة الخطأ عند تلقي المعلمة الفارغة.
    ErrParameterRequired = errors.New("parameter is required")
    // حدد ErrParameterInvalid رسالة الخطأ عند تلقي المعلمة غير الصالحة.
    ErrParameterInvalid = errors.New("parameter is invalid")
    // حدد ErrDefinedNameScope رسالة الخطأ على الاسم المعرّف غير الموجود في
    // النطاق المحدد.
    ErrDefinedNameScope = errors.New("no defined name on the scope")
    // حدد ErrDefinedNameDuplicate رسالة الخطأ على نفس الاسم الموجود بالفعل في
    // النطاق.
    ErrDefinedNameDuplicate = errors.New("the same name already exists on the scope")
    // حدد ErrCustomNumFmt رسالة الخطأ عند استلام تنسيق الأرقام المخصص الفارغ.
    ErrCustomNumFmt = errors.New("custom number format can not be empty")
    // حدد ErrFontLength رسالة الخطأ على طول تجاوز اسم عائلة الخط.
    ErrFontLength = errors.New("the length of the font family name must be smaller than or equal to 31")
    // حدد ErrFontSize رسالة الخطأ على حجم الخط غير صالح.
    ErrFontSize = errors.New("font size must be between 1 and 409 points")
    // حدد ErrSheetIdx رسالة الخطأ عند تلقي فهرس ورقة العمل غير صالح.
    ErrSheetIdx = errors.New("invalid worksheet index")
    // حدد ErrUnprotectSheet رسالة الخطأ في ورقة العمل ولم تحدد أي حماية.
    ErrUnprotectSheet = errors.New("worksheet has set no protect")
    // حدد ErrUnprotectSheetPassword رسالة الخطأ على إزالة حماية الورقة مع فشل
    // التحقق من كلمة المرور.
    ErrUnprotectSheetPassword = errors.New("worksheet protect password not match")
    // حدد ErrGroupSheets رسالة الخطأ في أوراق المجموعة.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // حدد ErrDataValidationFormulaLength رسالة الخطأ لتلقي طول صيغة التحقق من
    // صحة البيانات الذي يتجاوز الحد.
    ErrDataValidationFormulaLength = errors.New("data validation must be 0-255 characters")
    // حدد ErrDataValidationRange رسالة الخطأ على نطاق عشري معين يتجاوز الحد.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // حدد ErrCellCharsLength رسالة الخطأ لتلقي طول حرف الخلية الذي يتجاوز
    // الحد.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // حدد ErrOptionsUnzipSizeLimit رسالة الخطأ لتلقي UnzipSizeLimit و
    // UnzipXMLSizeLimit غير صالحين.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to UnzipXMLSizeLimit")
    // حدد ErrSave رسالة الخطأ لحفظ الملف.
    ErrSave = errors.New("no path defined for file, consider File.WriteTo or File.Write")
    // حدد ErrAttrValBool رسالة الخطأ على سمة XML من النوع المنطقي التنظيمي
    // وغير المنظم.
    ErrAttrValBool = errors.New("unexpected child of attrValBool")
    // حدد ErrSparklineType رسالة الخطأ عند تلقي معلمات نوع خط المؤشر غير الصالحة.
    ErrSparklineType = errors.New("parameter 'Type' must be 'line', 'column' or 'win_loss'")
    // حدد ErrSparklineLocation رسالة الخطأ على معلمات 'Location' المفقودة.
    ErrSparklineLocation = errors.New("parameter 'Location' is required")
    // حدد ErrSparklineRange رسالة الخطأ على معلمات خط المؤشر المفقودة 'Range'.
    ErrSparklineRange = errors.New("parameter 'Range' is required")
    // حدد ErrSparkline رسالة الخطأ عند تلقي معلمات خط المؤشر غير الصالحة.
    ErrSparkline = errors.New("must have the same number of 'Location' and 'Range' parameters")
    // حدد ErrSparklineStyle رسالة الخطأ عند تلقي معلمات خط المؤشر غير
    // الصالحة 'Style'.
    ErrSparklineStyle = errors.New("parameter 'Style' must between 0-35")
    // حدد ErrWorkbookPassword رسالة الخطأ عند تلقي كلمة مرور المصنف غير
    // الصحيحة.
    ErrWorkbookPassword = errors.New("the supplied open workbook password is not correct")
)
```

علاقة المصدر وقائمة مساحة الاسم والبادئات المرتبطة والمخطط الذي تم تقديمه فيه:

```go
var (
    SourceRelationship                      = xml.Attr{Name: xml.Name{Local: "r", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/relationships"}
    SourceRelationshipCompatibility         = xml.Attr{Name: xml.Name{Local: "mc", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/markup-compatibility/2006"}
    SourceRelationshipChart20070802         = xml.Attr{Name: xml.Name{Local: "c14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2007/8/2/chart"}
    SourceRelationshipChart2014             = xml.Attr{Name: xml.Name{Local: "c16", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2014/chart"}
    SourceRelationshipChart201506           = xml.Attr{Name: xml.Name{Local: "c16r2", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/drawing/2015/06/chart"}
    NameSpaceSpreadSheet                    = xml.Attr{Name: xml.Name{Local: "xmlns"}, Value: "http://schemas.openxmlformats.org/spreadsheetml/2006/main"}
    NameSpaceSpreadSheetX14                 = xml.Attr{Name: xml.Name{Local: "x14", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2009/9/main"}
    NameSpaceDrawingML                      = xml.Attr{Name: xml.Name{Local: "a", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/main"}
    NameSpaceDrawingMLChart                 = xml.Attr{Name: xml.Name{Local: "c", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/chart"}
    NameSpaceDrawingMLSpreadSheet           = xml.Attr{Name: xml.Name{Local: "xdr", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/drawingml/2006/spreadsheetDrawing"}
    NameSpaceSpreadSheetX15                 = xml.Attr{Name: xml.Name{Local: "x15", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/spreadsheetml/2010/11/main"}
    NameSpaceSpreadSheetExcel2006Main       = xml.Attr{Name: xml.Name{Local: "xne", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/excel/2006/main"}
    NameSpaceMacExcel2008Main               = xml.Attr{Name: xml.Name{Local: "mx", Space: "xmlns"}, Value: "http://schemas.microsoft.com/office/mac/excel/2008/main"}
    NameSpaceDocumentPropertiesVariantTypes = xml.Attr{Name: xml.Name{Local: "vt", Space: "xmlns"}, Value: "http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes"}
)
```

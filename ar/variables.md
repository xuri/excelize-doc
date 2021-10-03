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
    // حدد ErrMaxFileNameLength رسالة الخطأ عند تلقي تجاوز طول اسم الملف.
    ErrMaxFileNameLength = errors.New("file name length exceeds maximum limit")
    // حدد ErrEncrypt رسالة الخطأ في جدول بيانات التشفير.
    ErrEncrypt = errors.New("not support encryption currently")
    // حدد ErrUnknownEncryptMechanism رسالة الخطأ على آلية تشفير غير مدعومة.
    ErrUnknownEncryptMechanism = errors.New("unknown encryption mechanism")
    // حدد ErrUnsupportEncryptMechanism رسالة الخطأ على آلية تشفير غير مدعومة.
    ErrUnsupportEncryptMechanism = errors.New("unsupport encryption mechanism")
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
    // حدد ErrGroupSheets رسالة الخطأ في أوراق المجموعة.
    ErrGroupSheets = errors.New("group worksheet must contain an active worksheet")
    // حدد ErrDataValidationFormulaLenth رسالة الخطأ لتلقي طول صيغة التحقق من
    // صحة البيانات الذي يتجاوز الحد.
    ErrDataValidationFormulaLenth = errors.New("data validation must be 0-255 characters")
    // حدد ErrDataValidationRange رسالة الخطأ على نطاق عشري معين يتجاوز الحد.
    ErrDataValidationRange = errors.New("data validation range exceeds limit")
    // حدد ErrCellCharsLength رسالة الخطأ لتلقي طول حرف الخلية الذي يتجاوز الحد.
    ErrCellCharsLength = fmt.Errorf("cell value must be 0-%d characters", TotalCellChars)
    // حدد ErrOptionsUnzipSizeLimit رسالة الخطأ لتلقي UnzipSizeLimit و
    // WorksheetUnzipMemLimit غير صالحين.
    ErrOptionsUnzipSizeLimit = errors.New("the value of UnzipSizeLimit should be greater than or equal to WorksheetUnzipMemLimit")
)
```

# 数据

## 添加数据验证 {#AddDataValidation}

```go
func (f *File) AddDataValidation(sheet string, dv *DataValidation)
```

根据给定的工作表名和数据验证对象设置数据验证规则，数据验证对象可通过 `NewDataValidation` 函数创建，数据验证类型和条件参考[常量](constants.md)中的定义。

例1，为 `Sheet1!A1:B2` 设置包含验证条件为允许介于整数 10 到 20 的数据验证规则，输入无效数据时显示出错警告，标题为: "error title"，错误信息 "error body":

<p align="center"><img width="654" src="./images/data_validation_01.png" alt="数据验证"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A1:B2")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorBetween)
dv.SetError(excelize.DataValidationErrorStyleStop, "error title", "error body")
f.AddDataValidation("Sheet1", dv)
```

例2，为 `Sheet1!A3:B4` 设置包含验证条件为允许大于整数 10 的数据验证规则，选定单元格时显示输入信息，输入信息为: "input body":

<p align="center"><img width="654" src="./images/data_validation_02.png" alt="数据验证"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A3:B4")
dv.SetRange(10, 20, excelize.DataValidationTypeWhole, excelize.DataValidationOperatorGreaterThan)
dv.SetInput("input title", "input body")
f.AddDataValidation("Sheet1", dv)
```

例3，为 `Sheet1!A5:B6` 设置验证条件为序列的数据验证规则，忽略空值并提供下拉箭头:

<p align="center"><img width="654" src="./images/data_validation_03.png" alt="数据验证"></p>

```go
dv = excelize.NewDataValidation(true)
dv.SetSqref("A5:B6")
dv.SetDropList([]string{"1", "2", "3"})
f.AddDataValidation("Sheet1", dv)
```

如果您在序列中设置的项目超过限制累计 255 个字符的限制，请使用另一种方式设置：在工作表单元格中设置允许的值，并使用 `SetSqrefDropList` 函数设置序列中引用单元格的范围。

例4，为 `Sheet1!A7:B8` 设置以 `Sheet1!E1:E3` 为来源的验证条件，忽略空值并提供下拉箭头:

<p align="center"><img width="654" src="./images/data_validation_04.png" alt="数据验证"></p>

```go
dv := excelize.NewDataValidation(true)
dv.SetSqref("A7:B8")
dv.SetSqrefDropList("$E$1:$E$3")
f.AddDataValidation("Sheet1", dv)
```

数据验证下拉列表中显示的项目数量有限制：该列表最多可以显示 32768 个项目。如果您需要更多项目，可以通过级联列表将项目分类。

## 获取数据验证 {#GetDataValidations}

```go
func (f *File) GetDataValidations(sheet string) ([]*DataValidation, error)
```

根据给定的工作表名获取改工作表中全部数据验证区域和数据验证规则。

## 删除数据验证 {#DeleteDataValidation}

```go
func (f *File) DeleteDataValidation(sheet string, sqref ...string) error
```

根据给定的工作表名和数据验证区域删除数据验证规则。若未指定数据验证区域，将删除给定工作表中全部数据验证规则。

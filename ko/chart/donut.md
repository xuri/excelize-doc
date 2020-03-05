# 도넛 차트 {#doughnut}

예를 들어 다음과 같은 도넛 차트 를 추가합니다:

<p align="center"><img width="770" src="../images/doughnut_chart.png" alt="Go 언어를 사용하여 엑셀리즈로 도넛 차트 만들기"></p>

```go
package main

import (
    "fmt"

    "github.com/360EntSecGroup-Skylar/excelize"
)

func main() {
    categories := map[string]string{"A1": "Apple", "B1": "Orange", "C1": "Pear"}
    values := map[string]int{"A2": 2, "B2": 3, "C2": 3}
    f := excelize.NewFile()
    for k, v := range categories {
        f.SetCellValue("Sheet1", k, v)
    }
    for k, v := range values {
        f.SetCellValue("Sheet1", k, v)
    }
    if err := f.AddChart("Sheet1", "E1", `{"type":"doughnut","series":[{"name":"Sheet1!$A$2","categories":"Sheet1!$A$1:$C$1","values":"Sheet1!$A$2:$C$2"}],"format":{"x_scale":1.0,"y_scale":1.0,"x_offset":15,"y_offset":10,"print_obj":true,"lock_aspect_ratio":false,"locked":false},"legend":{"position":"right","show_legend_key":false},"title":{"name":"Fruit Doughnut Chart"},"plotarea":{"show_bubble_size":false,"show_cat_name":false,"show_leader_lines":false,"show_percent":true,"show_series_name":false,"show_val":false},"show_blanks_as":"zero"}`); err != nil {
        fmt.Println(err)
    }
    // 통합 문서 저장
    if err := f.SaveAs("Book1.xlsx"); err != nil {
        fmt.Println(err)
    }
}
```

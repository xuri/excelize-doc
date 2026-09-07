# 性能資料

{{ book.info }}

<a href="https://xuri.me/wp-content/uploads/2016/08/excelize-performance.svg"><img src="https://xuri.me/wp-content/uploads/2016/08/excelize-performance.svg" alt="Excelize benchmark" width="1506"></a>

性能數據由[此基準測試腳本](https://github.com/xuri/excelize-benchmark)生成。

## 相關 Excel 開源類庫性能對比

下圖展示了 Go, Python, Java, PHP 和 NodeJS 語言中典型 Excel 開源基礎庫，基於普通個人計算機 (10 Core Apple M4, 16GB DDR5, 500GB SSD, darwin/arm64, macOS Tahoe 26.6.2) 生成 `50` 列 `102400` 行純文本儲存格的性能表現。

<p align="center"><img width="800" src="https://xuri.me/wp-content/uploads/2016/08/excelize-golang-library-for-reading-and-writing-xlsx-files-3.svg" alt="相關 Excel 開源類庫性能對比"></p>

# パフォーマンスデータ

<a href="https://xuri.me/wp-content/uploads/2016/08/excelize-performance.svg"><img src="https://xuri.me/wp-content/uploads/2016/08/excelize-performance.svg" alt="Excelize benchmark" width="1506"></a>

パフォーマンスデータは、[このベンチマークテストスクリプト](https://github.com/xuri/excelize-benchmark)によって生成されます。

## 類似ライブラリの性能比較

次の図は、Go、Python、Java、PHP、および NodeJS 言語での主要な Excel のオープンソースクラスライブラリと、通常のパーソナルコンピュータに基づいて `50` 列 `102400` 行を生成するプレーンテキストセルのパフォーマンス比較を示しています。普通のパソコンによるテスト環境 (10 Core Apple M4, 16GB DDR5, 500GB SSD, darwin/arm64, macOS Tahoe 26.6.2)。

<p align="center"><img width="800" src="https://xuri.me/wp-content/uploads/2016/08/excelize-golang-library-for-reading-and-writing-xlsx-files-3.svg" alt="Excel 類似ライブラリの性能比較"></p>

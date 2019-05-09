# はじめに

<p align="center"><img width="650" src="../images/excelize.png" alt="Excelize logo"></p>

<p align="center">
    <a href="https://travis-ci.org/360EntSecGroup-Skylar/excelize"><img src="https://travis-ci.org/360EntSecGroup-Skylar/excelize.svg?branch=master" alt="Build Status"></a>
    <a href="https://codecov.io/gh/360EntSecGroup-Skylar/excelize"><img src="https://codecov.io/gh/360EntSecGroup-Skylar/excelize/branch/master/graph/badge.svg" alt="Code Coverage"></a>
    <a href="https://goreportcard.com/report/github.com/360EntSecGroup-Skylar/excelize"><img src="https://goreportcard.com/badge/github.com/360EntSecGroup-Skylar/excelize" alt="Go Report Card"></a>
    <a href="https://godoc.org/github.com/360EntSecGroup-Skylar/excelize"><img src="https://godoc.org/github.com/360EntSecGroup-Skylar/excelize?status.svg" alt="GoDoc"></a>
    <a href="https://opensource.org/licenses/BSD-3-Clause"><img src="https://img.shields.io/badge/license-bsd-orange.svg" alt="Licenses"></a>
    <a href="https://www.paypal.me/xuri"><img src="https://img.shields.io/badge/Donate-PayPal-green.svg" alt="Donate"></a>
</p>

Excelize は、ECMA-376 Office OpenXML 標準に基づいて Office Excel ドキュメントを操作するための Go 言語で書かれたクラスライブラリです。 XLSX ファイルの読み書きに使用できます。 Excelize は、他のオープンソースライブラリと比較して、イメージ（テーブル）付きのドキュメントの作成、Excel へのイメージの挿入、および保存後のチャートスタイルの保存をサポートしており、さまざまなレポートシステムに適用できます。

- ソースコード: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- 問題: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- GoDoc: [godoc.org/github.com/360EntSecGroup-Skylar/excelize](https://godoc.org/github.com/360EntSecGroup-Skylar/excelize)
- ライセンス契約: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 現在のバージョン: [v2.0.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- ドキュメントの更新：2019年5月7日

## プロジェクトミッション

Excelize の目的は、Office Open XML（OOXML）標準に準拠する xlsx ファイルを処理するための Excel ドキュメント API の Go 言語バージョンを作成して維持することです。Excelize を使用すると、Goを使用して MS Excel ファイルを読み書きできます。

## Excelizeを使用する理由

場合によっては、既存の Excel ドキュメントコンテンツの読み込み、新しい Excel ドキュメントの作成、既存のドキュメント（テンプレート）に基づく新しい Excel ドキュメントの生成、Excel ドキュメントへのイメージの挿入、チャートなどの Excel ドキュメントをプログラムで操作する必要があります。 テーブルなどの要素。プラットフォーム間でこれらの操作を実装する必要がある場合があります。 Excelize はこれらのニーズを容易に満たすことができます。

## 使用中の会社

<a href="https://360.net" title="360 企業セキュリティ" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="360 企業セキュリティ"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com@2x.png" alt="Qi An Xin Group"></a>

あなたの会社または製品がExcelizeも使用している場合は、ようこそ [ロゴを送る](mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A) 私たちを与えてください。
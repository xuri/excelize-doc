# はじめに

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize は、純粋な Go で記述されたライブラリで、XLSX / XLSM / XLTM ファイルの読み書きを可能にする一連の関数を提供します。Microsoft Excel&trade; 2007 以降で生成されたスプレッドシートドキュメントの読み取りと書き込みをサポートします。 高い互換性により複雑なコンポーネントをサポートし、大量のデータを含むワークシートからデータを生成または読み取るためのストリーミング API を提供します。

- ソースコード: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- 問題: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- ライセンス契約: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 現在のバージョン: [v2.2.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- ドキュメントの更新：2020年6月26日

## プロジェクトミッション

Excelize の目的は、Office Open XML（OOXML）標準に準拠する xlsx ファイルを処理するための Excel ドキュメント API の Go 言語バージョンを作成して維持することです。Excelize を使用すると、Goを使用して MS Excel ファイルを読み書きできます。

## Excelizeを使用する理由

場合によっては、既存の Excel ドキュメントコンテンツの読み込み、新しい Excel ドキュメントの作成、既存のドキュメント（テンプレート）に基づく新しい Excel ドキュメントの生成、Excel ドキュメントへのイメージの挿入、チャートなどの Excel ドキュメントをプログラムで操作する必要があります。 テーブルなどの要素。プラットフォーム間でこれらの操作を実装する必要がある場合があります。Excelize はこれらのニーズを容易に満たすことができます。

## 使用中の会社

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![CCi. Inc.](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="https://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="http://www.bigbaser.com" title="Big Baser" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="Big Baser"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a>

あなたの会社または製品がExcelizeも使用している場合は、ようこそ <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="ロゴを送る">ロゴを送る</a> 私たちを与えてください。

<a href="https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw" title="Excelize Slack Channel" target="_blank"><img style="margin-top: 25px;" height="60" src="../images/slack.svg" alt="Excelize Slack Channel"></a>

## Excelize の開発に協賛

プロジェクトの開発は、あなたのサポートから分離することはできません、著者にコーヒーバーのカップをしてください! Excelize は、以下の方法でスポンサーシップを受け入れます。

<a href="https://www.paypal.me/xuri" title="Paypal で寄付する" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Paypal で寄付する"></a>

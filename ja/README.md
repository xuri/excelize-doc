# はじめに

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize は、純粋な Go で記述されたライブラリで、XLAM / XLSM / XLSX / XLTM / XLTX ファイルの読み書きを可能にする一連の関数を提供します。Microsoft Excel&trade; 2007 以降で生成されたスプレッドシートドキュメントの読み取りと書き込みをサポートします。高い互換性により複雑なコンポーネントをサポートし、大量のデータを含むワークシートからデータを生成または読み取るためのストリーミング API を提供します。このライブラリには Go バージョン 1.23.0 以降が必要です。

- ソースコード: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- 問題: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- ライセンス契約: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 現在のバージョン: [v2.9.1](https://github.com/xuri/excelize/releases/latest)
- ドキュメントの更新：2025年6月30日

## プロジェクトミッション

Excelize の目的は、Office Open XML（OOXML）標準に準拠する xlsx ファイルを処理するための Excel ドキュメント API の Go 言語バージョンを作成して維持することです。Excelize を使用すると、Goを使用して MS Excel ファイルを読み書きできます。

## Excelizeを使用する理由

場合によっては、既存の Excel ドキュメントコンテンツの読み込み、新しい Excel ドキュメントの作成、既存のドキュメント（テンプレート）に基づく新しい Excel ドキュメントの生成、Excel ドキュメントへのイメージの挿入、チャートなどの Excel ドキュメントをプログラムで操作する必要があります。テーブルなどの要素。プラットフォーム間でこれらの操作を実装する必要がある場合があります。Excelize はこれらのニーズを容易に満たすことができます。

## 使用中の会社

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

あなたの会社または製品が Excelize も使用している場合は、ようこそ <a href="mailto: xuri.me@gmail.com?Subject=Excelize%20%E3%81%AE%E7%B4%B9%E4%BB%8B%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AB%E5%BD%93%E7%A4%BE%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84&amp;Body=%E3%81%93%E3%82%93%E3%81%AB%E3%81%A1%E3%81%AF%E3%80%81%3C%E8%B2%B4%E7%A4%BE%E5%90%8D%3E%20%E3%81%AE%20%3C%E8%B2%B4%E7%A4%BE%E5%90%8D%3E%20%E3%81%A7%E3%81%99%E3%80%82%0A%E5%BD%93%E7%A4%BE%E3%81%AF%20Excelize%20%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%81%8A%E3%82%8A%E3%80%81Excelize%20%E3%81%AE%E7%B4%B9%E4%BB%8B%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AB%E5%BD%93%E7%A4%BE%E3%81%AE%E5%90%8D%E5%89%8D%E3%82%92%E6%8E%B2%E8%BC%89%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%82%92%E8%AA%87%E3%82%8A%E3%81%AB%E6%80%9D%E3%81%84%E3%81%BE%E3%81%99%E3%80%82%0A%E5%BD%93%E7%A4%BE%E3%81%AE%E3%83%AD%E3%82%B4%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6%E3%81%AF%E6%B7%BB%E4%BB%98%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E3%81%94%E8%A6%A7%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%E3%80%82%20%3C%E6%B7%BB%E4%BB%98%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AB%E3%81%AF%E5%BF%85%E3%81%9A%E3%83%AD%E3%82%B4%E3%82%92%E8%A8%98%E8%BC%89%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%3E%0A" title="ロゴを送る">ロゴを送る</a> 私たちを与えてください。

## コミュニティ

- [Facebook Group](https://www.facebook.com/groups/excelize)
- [Google Group](https://groups.google.com/g/excelize)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/excelize)
- [Slack Channel](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Community on Telegram](https://t.me/excelize)
- [Community on Discord](https://discord.gg/MWV8MBQGtv)
- [Excelize Community on Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Skype Community](https://join.skype.com/YW3OFS5QjYcV?source=qr-ios): <a href="../images/skype_group@2x.png" title="Excelize Skype Community" target="_blank">join via QR Code</a>
- [Line Community](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" title="Excelize Line Community" target="_blank">join via QR Code</a>
- [DingTalk Group ID](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" title="Excelize DingTalk Group" target="_blank">join via QR Code</a>
- QQ Group ID: `1302058237` (Verification info: Excelize) | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">join via QR Code</a>
- Excelize WeChat ID: `hixuri` (Verification info: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">join via QR Code</a>
- WeCom Group (Verification info: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">join via QR Code</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">join via QR Code</a>

## Excelize の開発に協賛

プロジェクトの開発は、あなたのサポートから分離することはできません、著者にコーヒーバーのカップをしてください! Excelize は、以下の方法でスポンサーシップを受け入れます。スポンサーになることでこのプロジェクトをサポートする。

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Paypal で寄付する" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Paypal で寄付する"></a> <a href="https://opencollective.com/excelize" title="スポンサーになる" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="スポンサーになる"></a> <a href="https://www.patreon.com/xuri" title="Patreon での Excelize のサポート" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Patreon での Excelize のサポート"></a>

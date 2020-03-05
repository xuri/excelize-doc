# 簡介

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

<p align="center">
    <a href="https://travis-ci.org/360EntSecGroup-Skylar/excelize"><img src="https://travis-ci.org/360EntSecGroup-Skylar/excelize.svg?branch=master" alt="Build Status"></a>
    <a href="https://codecov.io/gh/360EntSecGroup-Skylar/excelize"><img src="https://codecov.io/gh/360EntSecGroup-Skylar/excelize/branch/master/graph/badge.svg" alt="Code Coverage"></a>
    <a href="https://goreportcard.com/report/github.com/360EntSecGroup-Skylar/excelize"><img src="https://goreportcard.com/badge/github.com/360EntSecGroup-Skylar/excelize" alt="Go Report Card"></a>
    <a href="https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc"><img src="https://img.shields.io/badge/go.dev-reference-007d9c?logo=go&logoColor=white" alt="go.dev"></a>
    <a href="https://opensource.org/licenses/BSD-3-Clause"><img src="https://img.shields.io/badge/license-bsd-orange.svg" alt="Licenses"></a>
    <a href="https://www.paypal.me/xuri"><img src="https://img.shields.io/badge/Donate-PayPal-green.svg" alt="Donate"></a>
</p>

Excelize 是 Go 語言編寫的一個用來操作 Office Excel 文檔類庫，基於 ECMA-376 Office OpenXML 標準。可以使用它來讀取、寫入 XLSX 檔案。相比較其他的開源類庫，Excelize 支持寫入原本帶有圖片(表)的文檔，還支持向 Excel 中插入圖片，並且在儲存後不會丟失圖表樣式，可以應用在各種報表系統中。

- Source Code: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- Issue: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- 許可協議: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 當前版本: [v2.1.0](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- 文檔更新: 2020年3月6日

## 項目使命

Excelize 的目標是創建並維護一個 Go 語言版本的 Excel 文檔 API，以處理符合基於 Office Open XML（OOXML）標準的 xlsx 檔案，借助 Excelize 您可以使用 Go 讀取和寫入 MS Excel 檔案。

## 為什麼要使用 Excelize

在一些情況下我們需要通過程式操作 Excel 文檔，例如：打開讀取已有 Excel 文檔內容、創建新的 Excel 文檔、基於已有文檔（模版）生成新的 Excel 文檔、向 Excel 文檔中插入圖片、圖表和表格等元素，有時還需要跨平台實現這些操作。使用 Excelize 可以方便的滿足上述需求。

## 項目榮譽

入選 2018 年開源中國碼雲最有價值開源項目 ([Gitee Most Valuable Project](https://gitee.com/xurime/excelize))

<p align="center"><img width="330" src="../images/gvp2018.jpg" alt="2018 年開源中國碼雲最有價值開源項目"></p>

## 知名用戶

<a href="https://www.360.cn" title="奇虎 360 公司" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="奇虎 360 公司"></a> <a href="https://www.baidu.com" title="百度" target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="百度"></a> [![合合信息](../images/vendor/ccint.com.png)](https://www.ccint.com) <a href="https://www.inke.cn" title="映客直播" target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="映客直播"></a> <a href="https://www.meituan.com" title="美團點評" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="美團點評"></a> <a href="https://www.163.com" title="網易" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="網易"></a> <a href="https://www.bilibili.com" title="嗶哩嗶哩" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="嗶哩嗶哩"></a> <a href="https://www.qianxin.com" title="奇安信集團" target="_blank"><img width="165" src="../images/vendor/qianxin.com@2x.png" alt="奇安信集團"></a> <a href="https://www.alibabagroup.com" title="阿里巴巴集團" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="阿里巴巴集團"></a> <a href="https://www.ele.me" title="餓了麼" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="餓了麼"></a> <a href="https://www.huifu.com" title="匯付天下" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="匯付天下"></a> <a href="https://www.dodoca.com" title="點點客" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="點點客"></a> <a href="https://bytedance.com" title="字節跳動" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="字節跳動"></a> <a href="https://www.flashexpress.com" title="閃電快車" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="閃電快車"></a> <a href="http://www.bigbaser.com" title="比格基地" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="比格基地"></a> <a href="https://jimengio.com" title="積夢智能" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="積夢智能"></a>

如果您的公司或產品也在使用 Excelize，歡迎 <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A%E4%BD%A0%E5%A5%BD%EF%BC%8C%E6%88%91%E6%98%AF%E3%80%90%E5%85%AC%E5%8F%B8%E5%90%8D%E7%A7%B0%E3%80%91%E7%9A%84%E3%80%90%E6%82%A8%E7%9A%84%E5%90%8D%E5%AD%97%E3%80%91%E3%80%82%0A%E6%88%91%E4%BB%AC%E5%85%AC%E5%8F%B8%E4%BD%BF%E7%94%A8%E4%BA%86%20Excelize%20%E5%B9%B6%E4%B8%94%E5%BE%88%E4%B9%90%E6%84%8F%E5%9C%A8%20Excelize%20%E7%9A%84%E2%80%9C%E4%BB%8B%E7%BB%8D%E2%80%9D%E9%A1%B5%E9%9D%A2%E5%8A%A0%E4%B8%8A%E6%88%91%E4%BB%AC%E5%85%AC%E5%8F%B8%E7%9A%84%20logo%E3%80%82%0A%E8%AF%B7%E5%9C%A8%E9%99%84%E4%BB%B6%E4%B8%AD%E6%9F%A5%E9%98%85%20logo%E3%80%82%E3%80%90%E8%AF%B7%E9%99%84%E4%B8%8A%20logo%20%E5%B9%B6%E5%8F%91%E9%80%81%E7%BB%99%20Excelize%E3%80%91" title="通過 E-mail 發送 Logo">發送 Logo</a> 給我們。

## 技術交流群

DingTalk Group ID: [`30047129`](https://qr.dingtalk.com/action/joingroup?code=v1,k1,2oHMIIOyvPcGezVdHJjsHwdZzzYNI6xs3Oww8uhlvCk=&_dt_no_comment=1&origin=11)
QQ Group ID: [`207895940`](https://jq.qq.com/?_wv=1027&k=5imdV9h)

<img width="400" src="./images/group@2x.png" alt="Excel 技術交流群">

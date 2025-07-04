# Introduction

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize is a library written in pure Go providing a set of functions that allow you to write to and read from XLAM / XLSM / XLSX / XLTM / XLTX files. Supports reading and writing spreadsheet documents generated by Microsoft Excel&trade; 2007 and later. Supports complex components by high compatibility, and provided streaming API for generating or reading data from a worksheet with huge amounts of data. This library needs Go version 1.23.0 or later.

- Source Code: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- Issue: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- Licenses: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- Last version: [v2.9.1](https://github.com/xuri/excelize/releases/latest)
- Document update time: June 30, 2025

## Project mission

The goal of Excelize is to create and maintain a Go language version of the Excel Document API to handle xlsx files that conform to the Office Open XML (OOXML) standard. With Excelize you can use Go to read and write MS Excel files.

## Why use Excelize

In some cases, we need to manipulate Excel documents through programs, such as: open to read existing Excel document content, create new Excel documents, generate new Excel documents based on existing documents (templates), insert images into Excel documents, charts Elements such as tables and sometimes need to implement these operations across platforms. Excelize can easily meet these needs.

## Well-known customers

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

If your company or product is also using Excelize, welcome <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="send Logo via E-mail">send Logo</a> to us.

## Community

- [Facebook Group](https://www.facebook.com/groups/excelize)
- [Google Group](https://groups.google.com/g/excelize)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/excelize)
- [Slack Channel](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [Community on Telegram](https://t.me/excelize)
- [Community on Discord](https://discord.gg/MWV8MBQGtv)
- [Excelize Community on Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Skype Community](https://join.skype.com/YW3OFS5QjYcV?source=qr-ios): <a href="../images/skype_group@2x.png" alt="Excelize Skype Community" target="_blank" target="_blank">join via QR Code</a>
- [Line Community](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" alt="Excelize Line Community" target="_blank" target="_blank">join via QR Code</a>
- [DingTalk Group ID](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" alt="Excelize DingTalk Group" target="_blank" target="_blank">join via QR Code</a>
- QQ Group ID: `1302058237` (Verification info: Excelize) | <a href="../images/qq_group@2x.png" alt="Excelize QQ Group ID" target="_blank" target="_blank">join via QR Code</a>
- Excelize WeChat ID: `hixuri` (Verification info: Excelize) | <a href="../images/wechat_group@2x.png" alt="Excelize WeChat Community" target="_blank" target="_blank">join via QR Code</a>
- WeCom Group (Verification info: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">join via QR Code</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" alt="Excelize Inflow Group" target="_blank" target="_blank">join via QR Code</a>

## Sponsor Excelize Development

If you are an individual user and have enjoyed the productivity of using Excelize, consider donating as a sign of appreciation - like buying me coffee once in a while, or support this project by becoming a sponsor.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Donate with Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Donate with Paypal"></a> <a href="https://opencollective.com/excelize" title="Become a Sponsor" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="Become a Sponsor"></a> <a href="https://www.patreon.com/xuri" title="Support Excelize on Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Support Excelize on Patreon"></a>

## Commercial Support

Let us help you reach the maximum potential of your app, to make working with Excel fun. Besides offering a completely free and open source package, we can also offer support on a commercial basis：

- Prioritize your issue

Having a bug ticket, a question or a feature request on our Github issue tracker that needs urgent attention? We are happy to give your ticket priority based on commercial support, contact us to get more details.

- Technical advisory services

Need help implementing Excelize in your application and you are on a shortage of technology or resources? We are happy to supercharge your imports and exports and can step in your team on an hourly-basis contract.

Please contact us by <a href="mailto: xuri.me@gmail.com">E-mail</a>.

## Excelize Tutorial Video

**Chapter 1：Introduction and Development Environment Setup**

[1.1 Introduction of Excelize](https://youtu.be/HrNmX5WbZY0)<br>[1.2 Go language and Excelize Develop Environment Setup (Windows & Mac)](https://youtu.be/leuW6czJ5mU)<br>[1.3 Basic Concepts](https://youtu.be/ih1N4d6hBdA)

**Chapter 2: Basic Usage**

[2.1 Quickstart, Set Cell Value, Styles, Insert Picture, and Create Chart](https://youtu.be/JkWrAB_9DA0)<br>[2.2 Conditional Formatting, Comment and Data Validation](https://youtu.be/U8SQIGKo0Nk)<br>[2.3 Converting CSV to XLSX, Row Height, Column Width, and Rich Text Settings](https://youtu.be/4yjrdMUlckc)<br>[2.4 Create Pivot Table, Shape, Cell Formula and Workbook Properties](https://youtu.be/rZ6FYUFNEkA)<br>[2.5 Sparkline, Header, Footer, Hidden and Worksheet Protection Settings](https://youtu.be/siLjtk3KGuo)<br>[2.6 Reading Workbook, Worksheets, Images, and Formula Calculation](https://youtu.be/0X5FyUGjiLc)

**Chapter 3：Working with Large Spreadsheet Efficiently**

[3.1 High-Performance I/O, Create a Huge Amounts of Data by Streaming API](https://youtu.be/mzQhoVrKOz8)

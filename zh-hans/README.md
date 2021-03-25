# 简介

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize 是 Go 语言编写的用于操作 Office Excel 文档基础库，基于 ECMA-376，ISO/IEC 29500 国际标准。可以使用它来读取、写入由 Microsoft Excel&trade; 2007 及以上版本创建的电子表格文档。支持 XLSX / XLSM / XLTM 等多种文档格式，高度兼容带有样式、图片(表)、透视表、切片器等复杂组件的文档，并提供流式读写 API，用于处理包含大规模数据的工作簿。可应用于各类报表平台、云计算、边缘计算等系统。使用本类库要求使用的 Go 语言为 1.10 或更高版本。

- Source Code: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- Issue: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- 许可协议: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 当前版本: [v2.3.2](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- 文档更新: 2021年3月26日

## 项目使命

Excelize 的目标是创建并维护一个 Go 语言版本的 Excel 文档 API，以处理符合基于 Office Open XML（OOXML）标准的 xlsx 文件，借助 Excelize 您可以使用 Go 读取和写入 MS Excel 文件。

## 为什么要使用 Excelize

在一些情况下我们需要通过程序操作 Excel 文档，例如：打开读取已有 Excel 文档内容、创建新的 Excel 文档、基于已有文档（模版）生成新的 Excel 文档、向 Excel 文档中插入图片、图表和表格等元素，有时还需要跨平台实现这些操作。使用 Excelize 可以方便的满足上述需求。

## 项目荣誉

入选 2020 Gopher China - Go 领域明星开源项目 ([GSP](https://mp.weixin.qq.com/s/XyLAaqpN-3urYcNmM_vPeg))

<p align="center"><img width="100" src="../images/gsp2020.png" alt="2020 Gopher China Go 领域明星开源项目"></p>

入选 2018 年开源中国码云最有价值开源项目 ([Gitee Most Valuable Project](https://gitee.com/xurime/excelize))

<p align="center"><img width="330" src="../images/gvp2018.jpg" alt="2018 年开源中国码云最有价值开源项目"></p>

## 知名用户

<a href="https://www.360.cn" title="奇虎 360 公司" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="奇虎 360 公司"></a> <a href="https://www.baidu.com" title="百度" target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="百度"></a> [![合合信息](../images/vendor/intsig.com.png)](https://www.intsig.com) <a href="https://www.inke.cn" title="映客直播" target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="映客直播"></a> <a href="https://www.meituan.com" title="美团点评" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="美团点评"></a> <a href="https://www.163.com" title="网易" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="网易"></a> <a href="https://www.bilibili.com" title="哔哩哔哩" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="哔哩哔哩"></a> <a href="https://www.qianxin.com" title="奇安信集团" target="_blank"><img width="165" src="../images/vendor/qianxin.com@2x.png" alt="奇安信集团"></a> <a href="https://www.alibabagroup.com" title="阿里巴巴集团" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="阿里巴巴集团"></a> <a href="https://www.ele.me" title="饿了么" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="饿了么"></a> <a href="https://www.huifu.com" title="汇付天下" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="汇付天下"></a> <a href="https://www.dodoca.com" title="点点客" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="点点客"></a> <a href="https://bytedance.com" title="字节跳动" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="字节跳动"></a> <a href="https://www.flashexpress.com" title="闪电快车" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="闪电快车"></a> <a href="http://www.bigbaser.com" title="比格基地" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="比格基地"></a> <a href="https://jimengio.com" title="积梦智能" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="积梦智能"></a> <a href="https://www.shannonai.com" title="香侬科技" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="香侬科技"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a> <a href="https://www.meitu.com" title="美图" target="_blank"><img width="165" src="../images/vendor/meitu.com@2x.png" alt="美图"></a>

如果您的公司或产品也在使用 Excelize，欢迎 <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A%E4%BD%A0%E5%A5%BD%EF%BC%8C%E6%88%91%E6%98%AF%E3%80%90%E5%85%AC%E5%8F%B8%E5%90%8D%E7%A7%B0%E3%80%91%E7%9A%84%E3%80%90%E6%82%A8%E7%9A%84%E5%90%8D%E5%AD%97%E3%80%91%E3%80%82%0A%E6%88%91%E4%BB%AC%E5%85%AC%E5%8F%B8%E4%BD%BF%E7%94%A8%E4%BA%86%20Excelize%20%E5%B9%B6%E4%B8%94%E5%BE%88%E4%B9%90%E6%84%8F%E5%9C%A8%20Excelize%20%E7%9A%84%E2%80%9C%E4%BB%8B%E7%BB%8D%E2%80%9D%E9%A1%B5%E9%9D%A2%E5%8A%A0%E4%B8%8A%E6%88%91%E4%BB%AC%E5%85%AC%E5%8F%B8%E7%9A%84%20logo%E3%80%82%0A%E8%AF%B7%E5%9C%A8%E9%99%84%E4%BB%B6%E4%B8%AD%E6%9F%A5%E9%98%85%20logo%E3%80%82%E3%80%90%E8%AF%B7%E9%99%84%E4%B8%8A%20logo%20%E5%B9%B6%E5%8F%91%E9%80%81%E7%BB%99%20Excelize%E3%80%91" title="通过 E-mail 发送 Logo">发送 Logo</a> 给我们。

## 技术交流群

<a href="https://groups.google.com/g/excelize" title="Excelize Google Group" target="_blank"><img style="margin: 25px 20px 0 0;" height="45" src="../images/google_groups@2x.png" alt="Excelize Google Group"></a> <a href="https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw" title="Excelize Slack Channel" target="_blank"><img style="margin-top: 25px;" height="45" src="../images/slack.svg" alt="Excelize Slack Channel"></a> <a href="https://t.me/excelize" title="Excelize Community on Telegram" target="_blank"><img style="margin: 25px 0 0 25px;" height="45" src="../images/telegram.svg" alt="Excelize Community on Telegram"></a> <a href="https://discord.gg/MWV8MBQGtv" title="Excelize Community on Discord" target="_blank"><img style="margin: 25px 0 0 25px;" height="45" src="../images/discord.svg" alt="Excelize Community on Discord"></a>

DingTalk Group ID: [`30047129`](https://qr.dingtalk.com/action/joingroup?code=v1,k1,ydu1Um4a+7sGezVdHJjsH2BifuEaXGW4Gkw7czNk25A=&_dt_no_comment=1&origin=11)
QQ Group ID: [`207895940`](https://jq.qq.com/?_wv=1027&k=5imdV9h)
WeChat ID: `hixuri` (请备注: Excelize)

<img width="700" src="../images/group@2x.png" alt="Excelize 技术交流群">

## 商业支持

帮助您的应用发挥最大潜力，让使用电子表格文档变得有趣。除了提供完全免费和开源的基础库软件包之外，Excelize 还可以在商业上提供技术咨询支持服务：

- 优先考虑您的问题

有急需解决的问题或新功能需求吗？Excelize 很乐意根据商业支持为您提供优先服务，请与 Excelize 联系以获取更多详细信息。

- 专业技术咨询服务

在您的应用程序使用 Excelize 开发过程中提供技术支持，提供解决方案咨询服务，并可以按小时为基础加入您的团队。

请通过 <a href="mailto: xuri.me@gmail.com">E-mail</a> 与我们取得联系。

# 소개

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize 는 순수 Go로 작성된 라이브러리로 XLAM / XLSM / XLSX / XLTM / XLTX 파일에서 읽고 쓸 수있는 기능 세트를 제공합니다. Microsoft Excel&trade; 2007 이상에서 생성 된 스프레드 시트 문서 읽기 및 쓰기를 지원합니다. 높은 호환성으로 복잡한 구성 요소를 지원하고 대량의 데이터가있는 워크 시트에서 데이터를 생성하거나 읽을 수있는 스트리밍 API 를 제공했습니다. 이 라이브러리에는 Go 버전 1.16 이상이 필요합니다.

- 소스 코드: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- 발행물: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- 면허: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- 마지막 버전: [v2.7.0](https://github.com/xuri/excelize/releases/latest)
- 문서 업데이트 시간: 2023 년 3 월 22 일

## 프로젝트 미션

Excelize 의 목표는 OOXML (Office Open XML) 표준을 준수하는 xlsx 파일을 처리하는 Excel 문서 API의 Go 언어 버전을 만들고 유지 관리하는 것입니다. Excelize 를 사용하면 Go를 사용하여 MS Excel 파일을 읽고 쓸 수 있습니다.

## Excelize 를 사용해야하는 이유

어떤 경우에는 기존 Excel 문서 내용 읽기, 새 Excel 문서 작성, 기존 문서 (템플릿) 기반의 새 Excel 문서 생성, Excel 문서에 이미지 삽입, 차트 등의 프로그램을 통해 Excel 문서를 조작해야합니다. 테이블로 사용하고 때로는 여러 플랫폼에서 이러한 작업을 구현해야합니다. Excelize 는 이러한 요구를 쉽게 충족시킬 수 있습니다.

## 잘 알려진 고객

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![INTSIG](../images/vendor/intsig.com_en.png)](https://en.intsig.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="http://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a> <a href="https://www.shannonai.com" title="Shannon.AI" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a> <a href="https://www.meitu.com" title="Meitui" target="_blank"><img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"></a> <a href="https://www.amazon.com" title="Amazon" target="_blank"><img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"></a> <a href="https://www.deloitte.com" title="Deloitte" target="_blank"><img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"></a> <a href="https://nl-a.ru" title="Neuro Lab! Algorithms" target="_blank"><img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"></a>

회사 나 제품이 Excelize 도 사용하고 있다면 <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="로고 보내주기">로고 보내주기</a>.

## 커뮤니티

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
- [QQ Group ID](https://jq.qq.com/?_wv=1027&k=5imdV9h): `207895940` | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">join via QR Code</a>
- Excelize WeChat ID: `hixuri` (Verification info: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">join via QR Code</a>
- WeCom Group (Verification info: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">join via QR Code</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">join via QR Code</a>
- Feishu Group: <a href="../images/feishu_group@2x.png" title="Feishu Group" target="_blank">join via QR Code</a>
- Lark Group: <a href="../images/larksuite_group@2x.png" title="Lark Group" target="_blank">join via QR Code</a>

## 스폰서 Excelize 개발

개인 사용자이고 Excelize 를 사용하는 생산성을 즐겼다면 가끔 커피를 사는 것과 같이 감사의 표시로 기부하는 것이 좋습니다. 스폰서되기 를 통해이 프로젝트를 지원할 수도 있습니다.

<a href="https://www.paypal.com/paypalme/xuri" title="Paypal 로 기부하기" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Paypal 로 기부하기"></a> <a href="https://opencollective.com/excelize" title="스폰서되기" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="스폰서되기"></a> <a href="https://www.patreon.com/xuri" title="Patreon 에서 Excelize 지원" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="Patreon 서 Excelize 지원"></a>

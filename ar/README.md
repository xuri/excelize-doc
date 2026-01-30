# المقدمة

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize شعار"></p>

Excelize هي مكتبة مكتوبة في الذهاب نقية توفير مجموعة من الوظائف التي تسمح لك الكتابة إلى وقراءة من XLAM / XLSM / XLSX / XLTM / XLTX الملفات. يدعم قراءة وكتابة مستندات جداول البيانات التي تم إنشاؤها بواسطة Microsoft Excel&trade; 2007 والإصدارات الأحدث. يدعم المكونات المعقدة من خلال التوافق العالي ، ويوفر واجهة برمجة التطبيقات المتدفقة لتوليد أو قراءة البيانات من ورقة عمل تحتوي على كميات هائلة من البيانات. تحتاج هذه المكتبة إلى Go الإصدار 1.23.0 أو الإصدار الأحدث.

- شفرة المصدر: [github.com/xuri/excelize](https://github.com/xuri/excelize)
- المساله: [github.com/xuri/excelize/issues](https://github.com/xuri/excelize/issues)
- go.dev: [pkg.go.dev/github.com/xuri/excelize/v2](https://pkg.go.dev/github.com/xuri/excelize/v2)
- التراخيص: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- الإصدار الأخير: [v2.10.0](https://github.com/xuri/excelize/releases/latest)
- وقت تحديث المستند: كانون الثاني 30, 2026

## بعثة المشروع

الهدف من Excelize هو إنشاء وصيانة إصدار لغة الانتقال من API المستند Excel لمعالجة ملفات xlsx التي تتوافق مع Office فتح XML (OOXML) القياسية. مع Excelize يمكنك استخدام الذهاب لقراءة وكتابة ملفات MS Excel.

## لماذا استخدام Excelize

في بعض الحالات، نحن بحاجة إلى التعامل مع مستندات Excel من خلال برامج، مثل: فتح لقراءة محتوى مستند Excel الحالي، إنشاء مستندات Excel جديدة، إنشاء مستندات Excel جديدة استناداً إلى المستندات الموجودة (القوالب)، إدراج الصور في مستندات Excel، مخططات عناصر مثل الجداول، وأحيانا تحتاج إلى تنفيذ هذه العمليات عبر الأنظمة الأساسية. يمكن أن تلبي Excelize بسهولة هذه الاحتياجات.

## الرعاة الذهبيون

<a href="https://www.gravityclimate.com" alt="Gravity"><img width="165" src="../images/vendor/gravityclimate.com.svg" alt="Gravity"></a>

## العملاء المعروفين

<img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"> <img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."> ![INTSIG](../images/vendor/intsig.com_en.png) <img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."> <img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"> <img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"> <img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"> <img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"> <img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"> <img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"> <img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"> <img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"> <img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"> <img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"> <img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"> <img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"> <img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"> <img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"> <img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"> <img width="165" src="../images/vendor/amazon@2x.png" alt="Amazon"> <img width="165" src="../images/vendor/deloitte@2x.png" alt="Deloitte"> <img width="165" src="../images/vendor/cisco@2x.png" alt="Cisco"> <img width="165" src="../images/vendor/nl-a.ru@2x.png" alt="Neuro Lab! Algorithms"> <img width="165" src="../images/vendor/58.com@2x.png" alt="58.com"> <img width="165" src="../images/vendor/ke.com@2x.png" alt="ke.com"> <img width="165" src="../images/vendor/microsoft@2x.png" alt="Microsoft"> <img width="165" src="../images/vendor/bytebase.com@2x.png" alt="ByteBase"> <img width="165" src="../images/vendor/intel@2x.png" alt="Intel"> <img width="165" src="../images/vendor/icbc.com.cn@2x.png" alt="Industrial and Commercial Bank of China"> <img width="165" src="../images/vendor/ccb.com@2x.png" alt="China Construction Bank"> <img width="165" src="../images/vendor/chinatelecom@2x.png" alt="China Telecommunications Corporation"> <img width="165" src="../images/vendor/tencent@2x.png" alt="Tencent"> <img width="165" src="../images/vendor/mihoyo@2x.png" alt="miHoYo"> <img width="165" src="../images/vendor/nsfocus@2x.png" alt="NSFOCUS Technologies Group Co Ltd"> <img width="165" src="../images/vendor/gree.com@2x.png" alt="Gree"> <img width="165" src="../images/vendor/jd.com@2x.png" alt="JD.com, Inc."> <img width="165" src="../images/vendor/zhiyitech.cn@2x.png" alt="Hangzhou Zhiyi Technology Co., Ltd.">

إذا كانت شركتك أو منتجك يستخدم أيضا Excelize، نرحب <a href="mailto: xuri.me@gmail.com?Subject=%D8%A7%D9%84%D8%B1%D8%AC%D8%A7%D8%A1%20%D8%A5%D8%B6%D8%A7%D9%81%D8%A9%20%D8%B4%D8%B1%D9%83%D8%AA%D9%86%D8%A7%20%D9%81%D9%8A%20%D8%B5%D9%81%D8%AD%D8%A9%20%D9%85%D9%82%D8%AF%D9%85%D8%A9%20Excelize&amp;Body=%D9%85%D8%B1%D8%AD%D8%A8%D9%8B%D8%A7%D8%8C%20%D9%87%D8%B0%D8%A7%20%3C%D8%A7%D8%B3%D9%85%D9%83%3E%20%D9%85%D9%86%20%3C%D8%A7%D8%B3%D9%85%20%D8%B4%D8%B1%D9%83%D8%AA%D9%83%3E.%0A%D9%86%D8%AD%D9%86%20%D9%86%D8%B3%D8%AA%D8%AE%D8%AF%D9%85%20Excelize%20%D9%88%D8%B3%D9%86%D9%81%D8%AE%D8%B1%20%D8%A8%D8%A5%D8%B6%D8%A7%D9%81%D8%A9%20%D8%A7%D8%B3%D9%85%20%D8%B4%D8%B1%D9%83%D8%AA%D9%86%D8%A7%20%D8%A5%D9%84%D9%89%20%D8%B5%D9%81%D8%AD%D8%A9%20%D9%85%D9%82%D8%AF%D9%85%D8%A9%20Excelize.%0A%D9%8A%D8%B1%D8%AC%D9%89%20%D8%A7%D9%84%D8%A7%D8%B7%D9%84%D8%A7%D8%B9%20%D8%B9%D9%84%D9%89%20%D8%A7%D9%84%D9%85%D8%B1%D9%81%D9%82%20%D9%84%D8%B4%D8%B9%D8%A7%D8%B1%D9%86%D8%A7.%20%3C%D8%AA%D8%A3%D9%83%D8%AF%20%D9%85%D9%86%20%D8%AA%D8%B6%D9%85%D9%8A%D9%86%20%D8%A7%D9%84%D8%B4%D8%B9%D8%A7%D8%B1%20%D9%81%D9%8A%20%D8%A7%D9%84%D9%85%D8%B1%D9%81%D9%82%3E%0A" title="إرسال الشعار عبر البريد الإلكتروني">إرسال الشعار</a> لنا

## تواصل اجتماعي

- [مجموعة الفيسبوك](https://www.facebook.com/groups/excelize)
- [مجموعة جوجل](https://groups.google.com/g/excelize)
- [تجاوز سعة المكدس](https://stackoverflow.com/questions/tagged/excelize)
- [قناة سلاك](https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw)
- [Gitter](https://gitter.im/excelize/community)
- [المجتمع على التليجرام](https://t.me/excelize)
- [المجتمع على الديسكورد](https://discord.gg/MWV8MBQGtv)
- [مجتمع Excelize على Microsoft Teams](https://teams.live.com/l/invite/FBA8aHkflqEj5SNzQM)
- [Line Community](http://line.me/ti/g/NFIjhfbP_g): <a href="../images/line_group@2x.png" title="Excelize Line Community" target="_blank">الانضمام عبر رمز الاستجابة السريعة</a>
- [معرف مجموعة DingTalk](https://qr.dingtalk.com/action/joingroup?code=v1,k1,6tmzbBbJuQkGezVdHJjsHz29CZI9F49xeW+cvOaECtk=&_dt_no_comment=1&origin=11): `30047129` | <a href="../images/dingtalk_group@2x.png" title="مجموعة Excelize DingTalk" target="_blank">الانضمام عبر رمز الاستجابة السريعة</a>
- QQ Group ID: `1302058237` (معلومات التحقق: Excelize) | <a href="../images/qq_group@2x.png" title="Excelize QQ Group ID" target="_blank">الانضمام عبر رمز الاستجابة السريعة</a>
- معرف Excelize WeChat: `hixuri` (معلومات التحقق: Excelize) | <a href="../images/wechat_group@2x.png" title="Excelize WeChat Community" target="_blank">الانضمام عبر رمز الاستجابة السريعة</a>
- WeCom Group (معلومات التحقق: Excelize): <a href="../images/wecom_group@2x.png" title="Excelize WeCom Group" target="_blank">الانضمام عبر رمز الاستجابة السريعة</a>
- Inflow Group ID: `4375928` | <a href="../images/inflow_group@2x.png" title="Excelize Inflow Group" target="_blank">الانضمام عبر رمز الاستجابة السريعة</a>

## الراعي إكسلسيز التنمية

إذا كنت مستخدم فرديا وتتمتع إنتاجية استخدام Excelize، والنظر في التبرع كعلامة على التقدير - مثل شراء لي القهوة مرة واحدة في كل حين. ادعم هذا المشروع من خلال أن تصبح راعيًا.

<a href="https://github.com/sponsors/xuri" title="GitHub Sponsor" target="_blank"><img width="170" src="../images/github_sponsor@2x.png" alt="GitHub Sponsor"></a> <a href="https://www.paypal.com/paypalme/xuri" title="Donate with Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Donate with Paypal"></a> <a href="https://opencollective.com/excelize" title="تصبح راعيا" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="تصبح راعيا"></a> <a href="https://www.patreon.com/xuri" title="دعم Excelize على Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="دعم Excelize على Patreon"></a>

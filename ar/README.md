# المقدمة

<p align="center"><img width="650" src="../images/excelize.svg" alt="Excelize logo"></p>

Excelize هي مكتبة مكتوبة في الذهاب نقية توفير مجموعة من الوظائف التي تسمح لك الكتابة إلى وقراءة من XLSX / XLSM / XLTM الملفات. يدعم قراءة وكتابة مستندات جداول البيانات التي تم إنشاؤها بواسطة Microsoft Excel&trade; 2007 والإصدارات الأحدث. يدعم المكونات المعقدة من خلال التوافق العالي ، ويوفر واجهة برمجة التطبيقات المتدفقة لتوليد أو قراءة البيانات من ورقة عمل تحتوي على كميات هائلة من البيانات. تحتاج هذه المكتبة إلى Go الإصدار 1.10 أو الإصدار الأحدث.

- شفرة المصدر: [github.com/360EntSecGroup-Skylar/excelize](https://github.com/360EntSecGroup-Skylar/excelize)
- المساله: [github.com/360EntSecGroup-Skylar/excelize/issues](https://github.com/360EntSecGroup-Skylar/excelize/issues)
- go.dev: [pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc](https://pkg.go.dev/github.com/360EntSecGroup-Skylar/excelize/v2?tab=doc)
- التراخيص: [BSD 3-Clause](https://opensource.org/licenses/BSD-3-Clause)
- الإصدار الأخير: [v2.3.2](https://github.com/360EntSecGroup-Skylar/excelize/releases/latest)
- وقت تحديث المستند: مارس 26, 2021

## بعثة المشروع

الهدف من Excelize هو إنشاء وصيانة إصدار لغة الانتقال من API المستند Excel لمعالجة ملفات xlsx التي تتوافق مع Office فتح XML (OOXML) القياسية. مع Excelize يمكنك استخدام الذهاب لقراءة وكتابة ملفات MS Excel.

## لماذا استخدام Excelize

في بعض الحالات، نحن بحاجة إلى التعامل مع مستندات Excel من خلال برامج، مثل: فتح لقراءة محتوى مستند Excel الحالي، إنشاء مستندات Excel جديدة، إنشاء مستندات Excel جديدة استناداً إلى المستندات الموجودة (القوالب)، إدراج الصور في مستندات Excel، مخططات عناصر مثل الجداول، وأحيانا تحتاج إلى تنفيذ هذه العمليات عبر الأنظمة الأساسية. يمكن أن تلبي Excelize بسهولة هذه الاحتياجات.

## العملاء المعروفين

<a href="https://www.360.cn" title="Qihoo 360" target="_blank"><img width="165" src="../images/vendor/360@2x.png" alt="Qihoo 360"></a> <a href="https://www.baidu.com" title="Baidu, Inc." target="_blank"><img width="165" src="../images/vendor/baidu@2x.png" alt="Baidu, Inc."></a> [![INTSIG](../images/vendor/intsig.com_en.png)](https://en.intsig.com) <a href="https://www.inke.cn" title="Inke, Inc." target="_blank"><img width="165" src="../images/vendor/inke@2x.png" alt="Inke, Inc."></a> <a href="https://www.meituan.com" title="Meituan-Dianping" target="_blank"><img width="165" src="../images/vendor/meituan@2x.png" alt="Meituan-Dianping"></a> <a href="https://www.163.com" title="NetEase" target="_blank"><img width="165" src="../images/vendor/netease@2x.png" alt="NetEase"></a> <a href="https://www.bilibili.com" title="Bilibili" target="_blank"><img width="165" src="../images/vendor/bilibili@2x.png" alt="Bilibili"></a> <a href="https://www.qianxin.com" title="Qi An Xin Group" target="_blank"><img width="165" src="../images/vendor/qianxin.com_en@2x.png" alt="Qi An Xin Group"></a> <a href="https://www.alibabagroup.com" title="Alibaba Group" target="_blank"><img width="165" src="../images/vendor/alibabagroup@2x.png" alt="Alibaba Group"></a> <a href="https://www.ele.me" title="ele.me" target="_blank"><img width="165" src="../images/vendor/ele.me@2x.png" alt="ele.me"></a> <a href="https://www.huifu.com" title="Huifu" target="_blank"><img width="165" src="../images/vendor/huifu.com@2x.png" alt="Huifu"></a> <a href="https://www.dodoca.com" title="Dodoca Information Technology" target="_blank"><img width="165" src="../images/vendor/dodoca.com@2x.png" alt="Dodoca Information Technology"></a> <a href="https://bytedance.com" title="ByteDance" target="_blank"><img width="165" src="../images/vendor/bytedance@2x.png" alt="ByteDance"></a> <a href="https://www.flashexpress.com" title="Flash Express" target="_blank"><img width="165" src="../images/vendor/flashexpress.com@2x.png" alt="Flash Express"></a> <a href="http://www.bigbaser.com" title="Big Baser" target="_blank"><img width="165" src="../images/vendor/bigbaser.com@2x.png" alt="Big Baser"></a> <a href="https://jimengio.com" title="JimengIO" target="_blank"><img width="165" src="../images/vendor/jimengio.com@2x.png" alt="JimengIO"></a> <a href="https://www.shannonai.com" title="Shannon.AI" target="_blank"><img width="165" src="../images/vendor/shannonai.com@2x.png" alt="Shannon.AI"></a> <a href="https://ibm.com" title="IBM" target="_blank"><img width="165" src="../images/vendor/ibm@2x.png" alt="IBM"></a> <a href="https://www.basedig.com" title="Basedig" target="_blank"><img width="165" src="../images/vendor/basedig.com@2x.png" alt="Basedig"></a> <a href="https://www.meitu.com" title="Meitui" target="_blank"><img width="165" src="../images/vendor/meitu.com@2x.png" alt="Meitui"></a>

إذا كانت شركتك أو منتجك يستخدم أيضا Excelize، نرحب <a href="mailto: xuri.me@gmail.com?Subject=Please add our company in Excelize Introduction page&amp;Body=Hello%2C%20this%20is%20%3Cyour%20name%3E%20from%20%3Cyour%20company%20name%3E.%0AWe%20are%20using%20Excelize%20and%20will%20be%20proud%20to%20add%20our%20company%20name%20to%20Excelize%20Introduction%20page.%0APlease%20see%20attachment%20for%20our%20logo.%20%3CBe%20sure%20to%20include%20logo%20in%20attachment%3E%0A" title="send Logo via E-mail">إرسال الشعار</a> لنا

<a href="https://groups.google.com/g/excelize" title="Excelize Google Group" target="_blank"><img style="margin: 25px 20px 0 0;" height="45" src="../images/google_groups@2x.png" alt="Excelize Google Group"></a> <a href="https://join.slack.com/t/xuri/shared_invite/zt-eriqdkeo-wV04zcCdBiiZveFgY86Wzw" title="Excelize Slack Channel" target="_blank"><img style="margin-top: 25px;" height="45" src="../images/slack.svg" alt="Excelize Slack Channel"></a> <a href="https://t.me/excelize" title="Excelize Community on Telegram" target="_blank"><img style="margin: 25px 0 0 25px;" height="45" src="../images/telegram.svg" alt="Excelize Community on Telegram"></a> <a href="https://discord.gg/MWV8MBQGtv" title="Excelize Community on Discord" target="_blank"><img style="margin: 25px 0 0 25px;" height="45" src="../images/discord.svg" alt="Excelize Community on Discord"></a>

## الراعي إكسلسيز التنمية

إذا كنت مستخدم فرديا وتتمتع إنتاجية استخدام Excelize، والنظر في التبرع كعلامة على التقدير - مثل شراء لي القهوة مرة واحدة في كل حين. ادعم هذا المشروع من خلال أن تصبح راعيًا.

<a href="https://www.paypal.com/paypalme/xuri" title="Donate with Paypal" target="_blank"><img width="170" src="../images/donate@2x.png" alt="Donate with Paypal"></a> <a href="https://opencollective.com/excelize" title="تصبح راعيا" target="_blank"><img height="61" src="../images/opencollective.com@2x.png" alt="تصبح راعيا"></a> <a href="https://www.patreon.com/xuri" title="دعم Excelize على Patreon" target="_blank"><img height="61" src="../images/patreon.com@2x.png" alt="دعم Excelize على Patreon"></a>

# أداء

توضح أرقام الأداء أدناه استخدام وقت التنفيذ والذاكرة لأوراق العمل ذات الحجم `N` من الصفوف ×` 50` من الأعمدة بمزيج 50/50 من السلاسل والأرقام. الأرقام مأخوذة من جهاز تعسفي متوسط المدى (نظام التشغيل: macOS Catalina الإصدار 10.15.7 ، وحدة المعالجة المركزية: 3.4 جيجاهرتز Intel Core i5 ، ذاكرة الوصول العشوائي: 16 جيجابايت 2400 ميجاهرتز DDR4 ، محرك الأقراص الثابتة: 1 تيرابايت ، إصدار Go: `go1.15.2 darwin/amd64` ، الالتزام: [`9316028`](https://github.com/360EntSecGroup-Skylar/excelize/tree/93160287bb7fa6479c73ee031b5ed771972a17a8)). تختلف الأرقام المحددة من آلة إلى أخرى ولكن الاتجاهات يجب أن تكون هي نفسها.

<table>
    <tr>
        <th>اكتب</th>
        <th>صفوف</th>
        <th>الأعمدة</th>
        <th>الوقت (بالثواني)</th>
        <th>ذاكرة (MB)</th>
    </tr>
    <tr>
        <td rowspan="10">تعيين قيمة الخلية</td>
        <td>200</td>
        <td>50</td>
        <td>0.018</td>
        <td>2</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>0.033</td>
        <td>2</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>0.060</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>0.119</td>
        <td>11</td>
    </tr>
    <tr>
        <td>3200</td>
        <td>50</td>
        <td>0.240</td>
        <td>22</td>
    </tr>
    <tr>
        <td>6400</td>
        <td>50</td>
        <td>0.458</td>
        <td>44</td>
    </tr>
    <tr>
        <td>12800</td>
        <td>50</td>
        <td>0.960</td>
        <td>46</td>
    </tr>
    <tr>
        <td>25600</td>
        <td>50</td>
        <td>1.973</td>
        <td>49</td>
    </tr>
    <tr>
        <td>52100</td>
        <td>50</td>
        <td>4.044</td>
        <td>67</td>
    </tr>
    <tr>
        <td>102400</td>
        <td>50</td>
        <td>7.791</td>
        <td>131</td>
    </tr>
    <tr>
        <td rowspan="1">إضافة مخطط</td>
        <td>200</td>
        <td>50</td>
        <td>8.77</td>
        <td>156</td>
    </tr>
    <tr>
        <td rowspan="4">قم بتعيين الارتباطات التشعبية</td>
        <td>200</td>
        <td>50</td>
        <td>1.08</td>
        <td>9</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>1.12</td>
        <td>9</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>16.9</td>
        <td>31</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>0.59</td>
        <td>63</td>
    </tr>
    <tr>
        <td rowspan="4">إدراج صورة</td>
        <td>200</td>
        <td>50</td>
        <td>1,57</td>
        <td>47</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>5.01</td>
        <td>94</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>18.56</td>
        <td>188</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>74</td>
        <td>374</td>
    </tr>
</table>

## مقارنة أداء المكتبات المماثلة

يوضح الرسم البياني التالي مقارنة أداء إنشاء مصفوفة نص عادي `102400*50` من خلال برامج Excel مفتوحة المصدر الرئيسية تحت الكمبيوتر الشخصي (نظام التشغيل: macOS Catalina الإصدار 10.15.7 ، وحدة المعالجة المركزية: 3.4 جيجا هرتز Intel Core i5 ، ذاكرة الوصول العشوائي: 16 جيجا بايت 2400 ميجاهرتز DDR4 ، HDD: 1 تيرابايت) ، بما في ذلك Go و Python و Java و PHP و NodeJS.

<p align="center"><img width="688" src="https://xuri.me/wp-content/uploads/2016/08/excelize-golang-library-for-reading-and-writing-xlsx-files-3.png" alt="مقارنة أداء المكتبات المماثلة"></p>

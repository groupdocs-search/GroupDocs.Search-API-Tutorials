---
date: '2025-12-16'
description: تعلم كيفية تنفيذ بحث نطاق التاريخ وميزات البحث المتقدمة الأخرى مثل البحث
  الموجه باستخدام Java باستخدام GroupDocs.Search للغة Java، بما في ذلك معالجة الأخطاء
  وتحسين الأداء.
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: 'GroupDocs.Search Java - البحث عن نطاق التاريخ والميزات المتقدمة'
type: docs
url: /ar/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# إتقان GroupDocs.Search Java: البحث بنطاق التاريخ والميزات المتقدمة

في التطبيقات المعتمدة على البيانات اليوم، **البحث بنطاق التاريخ** هو قدرة أساسية تتيح لك تصفية المستندات وفق فترات زمنية، مما يحسن الصلة والسرعة بشكل كبير. سواءً كنت تبني بوابة امتثال، أو كتالوجًا للتجارة الإلكترونية، أو نظامًا لإدارة المحتوى، فإن إتقان البحث بنطاق التاريخ إلى جانب أنواع الاستعلام القوية الأخرى سيجعل حلك مرنًا وقويًا. يوضح هذا الدليل معالجة الأخطاء، مجموعة كاملة من أنواع الاستعلامات، ونصائح الأداء، كل ذلك مع شفرة Java حقيقية يمكنك نسخها ولصقها.

## إجابات سريعة
- **ما هو البحث بنطاق التاريخ؟** تصفية المستندات التي تحتوي على تواريخ ضمن فترة بدء‑نهاية محددة.  
- **أي مكتبة توفره؟** GroupDocs.Search للـ Java.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم ترخيص إنتاج للاستخدام التجاري.  
- **هل يمكن دمجه مع استعلامات أخرى؟** نعم—يمكنك دمج نطاقات التاريخ مع استعلامات بوليانية، أو موجهة، أو regex.  
- **هل هو سريع للمجموعات الكبيرة؟** عندما يتم فهرستها بشكل صحيح، تُجرى عمليات البحث في أقل من ثانية حتى على ملايين السجلات.

## ما هو البحث بنطاق التاريخ؟
يتيح لك البحث بنطاق التاريخ العثور على المستندات التي تشمل تواريخ تقع بين حدين، مثل “2023‑01‑01 ~~ 2023‑12‑31”. وهو أساسي للتقارير، وسجلات التدقيق، وأي سيناريو يتطلب تصفية زمنية.

## لماذا نستخدم GroupDocs.Search للـ Java؟
توفر GroupDocs.Search واجهة برمجة تطبيقات موحدة للعديد من أنواع الاستعلام—البسيط، wildcard، faceted، numeric، date range، regex، boolean، وphrase—وبذلك يمكنك بناء تجارب بحث متقدمة دون الحاجة إلى مكتبات متعددة. كما أن معالجة الأخطاء المدفوعة بالأحداث تجعل خط أنابيب الفهرسة resilient.

## المتطلبات المسبقة
- **مكتبة GroupDocs.Search Java** (الإصدار 25.4 أو أحدث).  
- **مجموعة تطوير Java (JDK)** المتوافقة مع مشروعك.  
- Maven لإدارة التبعيات (أو تحميل يدوي).  

### المكتبات المطلوبة وإعداد البيئة
أضف مستودع GroupDocs والاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

### إعداد بديل
للتنزيلات المباشرة، زر [إصدارات GroupDocs.Search للـ Java](https://releases.groupdocs.com/search/java/).

### الترخيص والإعداد الأولي
ابدأ بنسخة تجريبية مجانية أو ترخيص مؤقت:

- زر [خيارات ترخيص GroupDocs](https://purchase.groupdocs.com/temporary-license/) للحصول على التفاصيل.

الآن لننشئ مجلد الفهرس الذي سيحفظ بياناتك القابلة للبحث.

## إعداد GroupDocs.Search للـ Java

### التهيئة الأساسية
أولاً، أنشئ كائن `Index` يشير إلى مجلد على القرص:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

أنت الآن تملك بوابة لجميع عمليات البحث.

## دليل التنفيذ

### الميزة 1: معالجة الأخطاء أثناء الفهرسة
#### كيفية التقاط أخطاء الفهرسة (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*لماذا يهم*: من خلال الاستماع إلى `ErrorOccurred`، يمكنك تسجيل المشكلات، إعادة محاولة الملفات الفاشلة، أو تنبيه المستخدمين دون تعطل العملية بأكملها.

### الميزة 2: استعلام بحث بسيط
#### ما هو البحث البسيط؟

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*النتيجة*: تُرجع كل مستند يحتوي على المصطلح **volutpat**.

### الميزة 3: استعلام بحث wildcard
#### كيف يعمل بحث wildcard؟

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*النتيجة*: يطابق كلًا من **affect** و **effect**، مظهرًا قوة الحرف النائب `?`.

### الميزة 4: استعلام بحث موجه (Faceted)
#### كيفية إجراء بحث موجه في Java

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*النتيجة*: يحدّ البحث إلى حقل **Content**، مثالي لتصفية النتائج حسب بيانات التعريف مثل الفئة أو المؤلف.

### الميزة 5: استعلام نطاق رقمي
#### كيفية البحث في نطاقات رقمية

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*النتيجة*: يسترجع المستندات التي تقع قيمها الرقمية بين 2000 و 3000.

### الميزة 6: استعلام نطاق تاريخ
#### كيفية تنفيذ بحث بنطاق تاريخ

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*التفسير*: من خلال تخصيص `SearchOptions`، تخبر المحرك بالتعرف على التواريخ بصيغة **MM/DD/YYYY**، ثم تسترجع جميع السجلات بين 1 يناير 2000 و 15 يونيو 2001.

### الميزة 7: استعلام بحث تعبير منتظم (Regex)
#### كيفية تشغيل بحث regex في Java

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*النتيجة*: يجد تسلسلات من ثلاثة أحرف متماثلة أو أكثر (مثل “aaa”، “111”).

### الميزة 8: استعلام بحث بولياني
#### كيفية دمج الشروط باستخدام البحث البولياني في Java

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*النتيجة*: تُرجع المستندات التي تحتوي على **justo** وتستثني أي مستند يحتوي أيضًا على **3456**.

### الميزة 9: استعلام بحث بولياني معقد
#### كيفية صياغة استعلامات بوليانية متقدمة

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*النتيجة*: يبحث عن أسماء ملفات مشابهة لـ “English” (مع السماح بتغييرات 1‑3 أحرف) **أو** محتوى يحتوي على كلٍ من **3456** و **consequat**.

### الميزة 10: استعلام بحث عبارة (Phrase)
#### كيفية البحث عن عبارات دقيقة

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*النتيجة*: يسترجع فقط المستندات التي تحتوي على العبارة الدقيقة **ipsum dolor sit amet**.

## تطبيقات عملية
1. **منصات التجارة الإلكترونية** – استخدم البحث الموجه في Java لتصفية المنتجات حسب الحجم، اللون، والعلامة التجارية.  
2. **أنظمة إدارة المحتوى** – دمج البحث البولياني في Java مع بحث العبارة لتوفير أدوات تحرير متقدمة.  
3. **أدوات تحليل البيانات** – استغلال البحث بنطاق التاريخ لإنشاء تقارير ولوحات معلومات زمنية.

## المشكلات الشائعة والحلول
- **عدم ظهور نتائج للبحث بنطاق التاريخ** – تأكد من أن صيغة التاريخ في مستنداتك تتطابق مع `DateFormat` المخصص الذي أضفته.  
- **استعلامات regex تُعيد عددًا كبيرًا من النتائج** – قم بتحسين النمط أو حدّ نطاق البحث ب qualifiers حقل إضافية.  
- **أخطاء الفهرسة غير مُلتقطة** – تأكد من ربط معالج الحدث **قبل** استدعاء `index.add(...)`.

## الأسئلة المتكررة

**س: هل يمكن دمج البحث بنطاق التاريخ مع أنواع استعلام أخرى؟**  
ج: بالتأكيد. يمكنك دمج شرط نطاق التاريخ مع عوامل بوليانية، فلاتر موجهة، أو أنماط regex في سلسلة استعلام واحدة.

**س: هل يجب إعادة بناء الفهرس بعد تغيير صيغ التاريخ؟**  
ج: نعم. الفهرس يخزن المصطلحات المُجزأة؛ تعديل `SearchOptions` وحده لن يُعيد تجزئة البيانات الموجودة. أعد فهرسة المستندات بعد تغيير الصيغ.

**س: كيف يتعامل GroupDocs.Search مع الفهارس الكبيرة؟**  
ج: يستخدم الفهرسة المتزايدة والتخزين على القرص، مما يتيح لك التوسع إلى ملايين المستندات مع الحفاظ على استهلاك منخفض للذاكرة.

**س: هل هناك حد لعدد أحرف الـ wildcard؟**  
ج: تُعالج الـ wildcards بكفاءة، لكن استخدام العديد من wildcards في بداية الكلمة (مثل `*term`) قد يُبطئ الأداء. يُفضَّل استخدام wildcards في النهاية أو البداية فقط.

**س: أي نموذج ترخيص يُنصح به للإنتاج؟**  
ج: ترخيص دائم أو اشتراك من GroupDocs يضمن لك الحصول على التحديثات، الدعم، والقدرة على النشر دون قيود النسخة التجريبية.

## الخلاصة
من خلال إتقان **البحث بنطاق التاريخ** ومجموعة الاستعلامات المتقدمة التي تقدمها GroupDocs.Search للـ Java، يمكنك بناء تجارب بحث سريعة، غنية بالميزات، ومُحسّنة. نفّذ معالجة أخطاء قوية، اضبط فهرسك، وادمج الاستعلامات لتلبية أي سيناريو استرجاع تقريبًا. ابدأ التجربة اليوم وارتقِ بقدرات وصول البيانات في تطبيقك.

---

**آخر تحديث:** 2025-12-16  
**تم الاختبار مع:** GroupDocs.Search 25.4 (Java)  
**المؤلف:** GroupDocs
---
date: '2025-12-18'
description: تعلم كيفية تنفيذ عمليات بحث Java بتنسيق تاريخ مخصص باستخدام GroupDocs.Search،
  بما في ذلك استعلامات نطاق التاريخ، الأنماط المخصصة، ونصائح الأداء.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'تنسيق تاريخ مخصص في جافا: البحث عن نطاق التاريخ باستخدام GroupDocs'
type: docs
url: /ar/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# تنسيق التاريخ المخصص في جافا: البحث عن نطاق التاريخ باستخدام GroupDocs

البحث عن المستندات حسب التاريخ هو متطلب شائع — سواء كنت تبني نظام أرشفة، أداة تقارير مالية، أو بوابة إدارة محتوى. في هذا البرنامج التعليمي ستتعلم **custom date format java** باستخدام GroupDocs.Search، تغطي استعلامات نطاق التاريخ، تعريف الأنماط المخصصة، ونصائح **optimize search performance**. في النهاية، ستكون قادرًا على السماح للمستخدمين باسترجاع السجلات التي تقع ضمن أي فترة زمنية، بغض النظر عن الصيغة التي يستخدمونها.

## إجابات سريعة
- **ما هي الفئة الأساسية للفهرسة؟** `Index` من حزمة `com.groupdocs.search`.  
- **كيف تعرف نمط تاريخ مخصص؟** استخدم `DateFormat` مع كائنات `DateFormatElement` وفاصل.  
- **هل يمكنني البحث باستخدام استعلام نصي؟** نعم، صيغة `daterange(start ~~ end)` تعمل مباشرة في سلسلة الاستعلام.  
- **ما هي إحداثيات Maven المطلوبة؟** `com.groupdocs:groupdocs-search:25.4` (أو أحدث).  
- **هل أحتاج إلى ترخيص للتطوير؟** نسخة تجريبية مجانية أو ترخيص مؤقت يكفي للاختبار؛ ترخيص تجاري مطلوب للإنتاج.

## ما هو **custom date format java**؟
يخبر **custom date format java** GroupDocs.Search كيف يفسر سلاسل التاريخ التي لا تتبع نمط ISO الافتراضي (YYYY‑MM‑DD). من خلال تعريف نمطك الخاص — مثل `MM/dd/yyyy` أو `dd‑MM‑yyyy` — يمكنك تمكين المحرك من التعرف على التواريخ المضمنة في المستندات التي تستخدم صيغًا إقليمية أو قديمة.

## لماذا تستخدم GroupDocs.Search لاستعلامات نطاق التاريخ؟
- **السرعة:** الفهرسة المدمجة تجعل عمليات البحث O(log n).  
- **المرونة:** يدعم إنشاء الاستعلامات النصية والكائنية.  
- **دعم متعدد الصيغ:** يتعامل مع PDFs، Word، Excel، النص العادي، وأكثر دون الحاجة إلى كود إضافي.

## كيفية **search documents by date** باستخدام GroupDocs.Search
ستجد أدناه دليلًا خطوة بخطوة يوضح لك كيفية إعداد المكتبة، فهرسة الملفات، وتنفيذ عمليات البحث عن نطاق التاريخ البسيطة والمتقدمة.

### المتطلبات المسبقة
- Java 8 أو أحدث مثبت.  
- Maven لإدارة التبعيات.  
- الوصول إلى ترخيص GroupDocs.Search (التجريبي أو المؤقت يعمل للتطوير).

### إعداد GroupDocs.Search لجافا

#### التثبيت باستخدام Maven
Add the repository and dependency to your `pom.xml`:

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

#### التحميل المباشر
بدلاً من ذلك، يمكنك تنزيل أحدث نسخة مباشرة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### التهيئة الأساسية والإعداد
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## الميزة 1: إنشاء استعلامات بحث نطاق التاريخ

### استخدام استعلام نصي
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**شرح**: صيغة `daterange` تتوقع تواريخ بصيغة `YYYY‑MM‑DD`. تُرجع جميع المستندات التي تقع تواريخها المفهرسة ضمن الفاصل.

### استخدام كائن الاستعلام
For programmatic control and custom parsing, build a `SearchQuery` object:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**شرح**: `createDateRangeQuery` يتيح لك توفير كائنات `java.util.Date`، مما يمنحك مرونة كاملة حول المناطق الزمنية ومعالجة خاصة باللغات.

## الميزة 2: تحديد أنماط **custom date format java**
### إعداد صيغ تاريخ مخصصة
Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**شرح**: عن طريق مسح الصيغ الافتراضية وإضافة `DateFormat` يستخدم `/` كفاصل، يصبح المحرك الآن قادرًا على فهم التواريخ المكتوبة بصيغة `MM/dd/yyyy`. هذا أمر أساسي لـ **search documents by date** في المناطق التي تفضل صيغة الشهر أولاً.

## نصائح لـ **optimize search performance**
- **فهرسة تدريجية**: أضف ملفات جديدة إلى الفهرس الحالي بدلاً من إعادة بناءه من الصفر.  
- **إزالة البيانات القديمة**: احذف بشكل دوري المستندات التي لم تعد بحاجة إليها.  
- **ضبط إعدادات الذاكرة**: زيادة حجم heap الخاص بـ JVM (`-Xmx`) عند العمل مع فهارس كبيرة.  

## المشكلات الشائعة والحلول
- **أخطاء تحليل التاريخ**: تأكد من أن سلاسل التاريخ في المستند تتطابق تمامًا مع النمط المخصص الذي حددته.  
- **نتائج مفقودة**: تأكد من أن الحقول المفهرسة تحتوي على بيانات تعريفية للتاريخ؛ وإلا لن يتمكن المحرك من مطابقة استعلامات التاريخ.  
- **استثناءات الوصول إلى الفهرس**: تأكد من أن مسار `indexFolder` قابل للكتابة وغير مقفل من قبل عملية أخرى.

## التطبيقات العملية
1. **أنظمة الأرشفة** – استرجاع السجلات من فترة تاريخية محددة.  
2. **إدارة المحتوى** – دعم صيغ التاريخ الإقليمية مثل `dd/MM/yyyy` للجمهور الأوروبي.  
3. **البرمجيات المالية** – تصفية المعاملات حسب الربع المالي أو السنة بسرعة.

## الخلاصة
أصبحت الآن تمتلك مجموعة أدوات **custom date format java** كاملة لبناء عمليات بحث قوية عن نطاق التاريخ باستخدام GroupDocs.Search. نفّذ هذه الأنماط، اضبط الأداء بدقة، وسيقدم تطبيقك نتائج سريعة ودقيقة لأي استعلام زمني.

## الأسئلة المتكررة

**س: ما الفرق بين استعلام النصي واستعلام الكائنات للتاريخ؟**  
ج: الاستعلام النصي سريع وسهل لكنه محدود بصيغة ISO الافتراضية؛ استعلامات الكائنات تتيح لك توفير كائنات `Date` وصيغ مخصصة لمزيد من المرونة.

**س: هل يمكنني البحث عن نطاقات تاريخ متعددة في استعلام واحد؟**  
ج: نعم، يمكنك دمج عبارات `daterange` مع عوامل منطقية مثل `AND` أو `OR` لبناء استعلامات معقدة.

**س: هل ستؤدي صيغ التاريخ المخصصة إلى إبطاء البحث؟**  
ج: هناك عبء بسيط إضافي للتحليل، لكن الأثر ضئيل بالنسبة لأعباء العمل المعتادة ويتفوق على الفوائد في الدقة.

**س: هل GroupDocs.Search مناسب للنشر على نطاق واسع؟**  
ج: بالتأكيد. مع استراتيجيات الفهرسة المناسبة وضبط JVM، يمكنه التعامل مع ملايين المستندات.

**س: أين يمكنني العثور على المزيد من أمثلة جافا؟**  
ج: استكشف [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) للحصول على عينات إضافية وتنفيذ حالات الاستخدام.

---

**الوثائق**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
**مرجع API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
**التنزيل**: [Get the latest version here](https://releases.groupdocs.com/search/java/)  
**مستودع GitHub**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
**منتدى الدعم المجاني**: [Join the discussion](https://forum.groupdocs.com/c/search/10)  
**ترخيص مؤقت**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2025-12-18  
**تم الاختبار مع:** GroupDocs.Search Java 25.4  
**المؤلف:** GroupDocs
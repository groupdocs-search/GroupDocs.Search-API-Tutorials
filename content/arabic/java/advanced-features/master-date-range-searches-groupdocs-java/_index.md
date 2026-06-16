---
date: '2026-03-04'
description: تعلم كيفية تنفيذ عمليات بحث Java بتنسيق تاريخ مخصص باستخدام GroupDocs.Search،
  مع تغطية استعلامات نطاق التاريخ، الأنماط المخصصة، ونصائح الأداء.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: تنسيق تاريخ مخصص في جافا | البحث عن نطاق التاريخ باستخدام GroupDocs
type: docs
url: /ar/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# تنسيق تاريخ مخصص Java | البحث عن نطاق التاريخ باستخدام GroupDocs

البحث عن المستندات حسب التاريخ هو طلب شائع—سواء كنت تبني نظام أرشفة، أداة تقارير مالية، أو بوابة إدارة محتوى. في هذا الدرس ستتعلم تقنيات **custom date format java** باستخدام GroupDocs.Search، مع تغطية استعلامات نطاق التاريخ، تعريف الأنماط المخصصة، ونصائح **optimize search performance**. في النهاية، سيمكنك السماح للمستخدمين باسترجاع السجلات التي تقع ضمن أي فترة تاريخية، بغض النظر عن الصيغة التي يستخدمونها.

## إجابات سريعة
- **ما هي الفئة الأساسية للفهرسة؟** `Index` من حزمة `com.groupdocs.search`.  
- **كيف يمكن تعريف نمط تاريخ مخصص؟** استخدم `DateFormat` مع كائنات `DateFormatElement` وفاصل.  
- **هل يمكن البحث باستخدام استعلام نصي؟** نعم، صيغة `daterange(start ~~ end)` تعمل مباشرة في سلسلة الاستعلام.  
- **ما هي إحداثيات Maven المطلوبة؟** `com.groupdocs:groupdocs-search:25.4` (أو أحدث).  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي أو مؤقت يكفي للاختبار؛ الترخيص التجاري مطلوب للإنتاج.

## ما هو **custom date format java**؟
**custom date format java** يخبر GroupDocs.Search كيفية تفسير سلاسل التاريخ التي لا تتبع نمط ISO الافتراضي (YYYY‑MM‑DD). من خلال تعريف نمطك الخاص—مثل `MM/dd/yyyy` أو `dd‑MM‑yyyy`—تتمكن المحرك من التعرف على التواريخ المدمجة في المستندات التي تستخدم صيغ إقليمية أو قديمة.

## لماذا نستخدم GroupDocs.Search لاستعلامات نطاق التاريخ؟
- **السرعة:** الفهرسة المدمجة تجعل عمليات البحث O(log n).  
- **المرونة:** يدعم إنشاء الاستعلامات بنص أو كائن.  
- **دعم صيغ متعددة:** يتعامل مع PDFs، Word، Excel، النص العادي، وأكثر دون الحاجة إلى كود إضافي.  

## كيف **search documents by date** باستخدام GroupDocs.Search
فيما يلي دليل خطوة بخطوة يوضح إعداد المكتبة، فهرسة الملفات، وتنفيذ عمليات بحث نطاق تاريخ بسيطة ومتقدمة.

### المتطلبات المسبقة
- Java 8 أو أحدث مثبتة.  
- Maven لإدارة التبعيات.  
- الوصول إلى ترخيص GroupDocs.Search (التجريبي أو المؤقت يكفي للتطوير).  

### إعداد GroupDocs.Search للـ Java

#### التثبيت باستخدام Maven
أضف المستودع والتبعيات إلى ملف `pom.xml` الخاص بك:

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
أنشئ كائن `Index` وأضف مستنداتك:

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
أسهل طريقة هي تضمين نطاق التاريخ مباشرة في سلسلة الاستعلام:

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

**التفسير**: صيغة `daterange` تتوقع تواريخ بصيغة `YYYY‑MM‑DD`. تُعيد جميع المستندات التي تقع تواريخها المفهرسة ضمن الفاصل الزمني.

### استخدام كائن الاستعلام
للسيطرة البرمجية وتخصيص التحليل، أنشئ كائن `SearchQuery`:

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

**التفسير**: `createDateRangeQuery` يتيح لك تمرير كائنات `java.util.Date`، مما يمنحك مرونة كاملة في التعامل مع المناطق الزمنية ومعالجة الصيغ الخاصة بالإقليم.

## الميزة 2: تحديد أنماط **custom date format java**

### ضبط صيغ تاريخ مخصصة
عرّف `DateFormat` يتطابق مع تمثيل التاريخ في مستندك:

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

**التفسير**: من خلال مسح الصيغ الافتراضية وإضافة `DateFormat` يستخدم `/` كفاصل، يصبح المحرك قادرًا على فهم التواريخ المكتوبة بصيغة `MM/dd/yyyy`. هذا أساسي لـ **search documents by date** في المناطق التي تفضّل كتابة الشهر أولًا.

## نصائح **optimize search performance**
- **الفهرسة التدريجية**: أضف ملفات جديدة إلى الفهرس الحالي بدلاً من إعادة بناءه من الصفر.  
- **إزالة البيانات القديمة**: احذف دوريًا المستندات التي لم تعد بحاجة إليها.  
- **ضبط إعدادات الذاكرة**: زد حجم heap الخاص بـ JVM (`-Xmx`) عند التعامل مع فهارس كبيرة.  

## المشكلات الشائعة والحلول
- **أخطاء تحليل التاريخ**: تأكد من أن سلاسل التاريخ في المستند تطابق تمامًا النمط المخصص الذي عرّفته.  
- **نتائج مفقودة**: تأكد من أن الحقول المفهرسة تحتوي على بيانات تعريفية للتاريخ؛ وإلا لن يتمكن المحرك من مطابقة استعلامات التاريخ.  
- **استثناءات الوصول إلى الفهرس**: تحقق من أن مسار `indexFolder` قابل للكتابة وليس مقفلًا بعملية أخرى.  

## تطبيقات عملية
1. **أنظمة الأرشفة** – استرجاع السجلات من فترة تاريخية محددة.  
2. **إدارة المحتوى** – دعم صيغ تاريخ إقليمية مثل `dd/MM/yyyy` للجمهور الأوروبي.  
3. **البرمجيات المالية** – تصفية المعاملات حسب الربع المالي أو السنة بسرعة.  

## لماذا هذا مهم
معالجة **custom date format java** تزيل العوائق الناتجة عن تمثيلات تاريخ غير متسقة عبر المستندات. تتيح لك **handle multiple date formats** في فهرس واحد، مما يضمن حصول المستخدمين النهائيين على نتائج دقيقة مهما كانت صيغة التاريخ الأصلية.

## الخطوات التالية
- استكشف تركيبات استعلامات أكثر تقدمًا باستخدام عوامل `AND`، `OR`، و`NOT`.  
- جرب المحللات المخصصة إذا احتجت إلى فهرسة بيانات زمنية إضافية.  
- راجع دليل تحسين الأداء في الوثائق الرسمية لتوسيع حلّك إلى ملايين المستندات.

## الأسئلة المتكررة

**س: ما الفرق بين استعلامات التاريخ النصية وتلك القائمة على الكائن؟**  
ج: الاستعلام النصي سريع وسهل لكنه مقيد بصيغة ISO الافتراضية؛ استعلامات الكائن تسمح بتمرير كائنات `Date` وصيغ مخصصة لمزيد من المرونة.

**س: هل يمكن البحث عن نطاقات تاريخ متعددة في استعلام واحد؟**  
ج: نعم، يمكن دمج عبارات `daterange` مع عوامل منطقية مثل `AND` أو `OR` لبناء استعلامات مركبة.

**س: هل تؤدي صيغ التاريخ المخصصة إلى إبطاء البحث؟**  
ج: هناك تكلفة بسيطة إضافية للتحليل، لكن تأثيرها ضئيل بالنسبة لأحمال العمل العادية ويتفوق على فوائد الدقة.

**س: هل GroupDocs.Search مناسب للنشر على نطاق واسع؟**  
ج: بالتأكيد. مع استراتيجيات الفهرسة المناسبة وضبط JVM، يمكنه التعامل مع ملايين المستندات.

**س: أين يمكنني العثور على المزيد من أمثلة Java؟**  
ج: استكشف [مستودع GroupDocs على GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) للحصول على عينات إضافية وتطبيقات عملية.

---

**الموارد**

- **الوثائق**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **مرجع API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **التنزيل**: [احصل على أحدث نسخة هنا](https://releases.groupdocs.com/search/java/)
- **مستودع GitHub**: [عرض على GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **منتدى الدعم المجاني**: [انضم إلى النقاش](https://forum.groupdocs.com/c/search/10)
- **ترخيص مؤقت**: [احصل على ترخيص مؤقت هنا](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-03-04  
**تم الاختبار مع:** GroupDocs.Search Java 25.4  
**المؤلف:** GroupDocs
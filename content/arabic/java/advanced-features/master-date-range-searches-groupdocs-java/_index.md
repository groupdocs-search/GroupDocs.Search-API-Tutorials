---
date: '2026-10-07'
description: تعلم كيفية تنفيذ عمليات بحث تنسيق تاريخ مخصص Java باستخدام GroupDocs،
  مع تغطية استعلامات نطاق التاريخ، الأنماط المخصصة، ونصائح الأداء.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: يظهر درس تنسيق تاريخ مخصص Java كيفية تكوين GroupDocs.Search للغة Java،
  تشغيل استعلامات نطاق التاريخ، وتحسين الأداء. اتبع أمثلة خطوة بخطوة.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: تنسيق تاريخ مخصص Java – دليل بحث نطاق التاريخ مع GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: تنسيق تاريخ مخصص Java | بحث نطاق التاريخ مع GroupDocs
type: docs
url: /ar/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# تنسيق تاريخ مخصص جافا | بحث نطاق التاريخ باستخدام GroupDocs

البحث عن المستندات حسب التاريخ هو طلب شائع — سواء كنت تبني نظام أرشفة، أو أداة تقارير مالية، أو بوابة إدارة محتوى. في هذا البرنامج التعليمي ستتعلم **custom date format java** باستخدام GroupDocs.Search، مع تغطية استعلامات نطاق التاريخ، وتعريف الأنماط المخصصة، ونصائح **optimize search performance**. في النهاية، ستتمكن من تمكين المستخدمين من استرجاع السجلات التي تقع ضمن أي فترة تاريخية، بغض النظر عن التنسيق الذي يستخدمونه.

## إجابات سريعة
- **ما هي الفئة الأساسية للفهرسة؟** `Index` from the `com.groupdocs.search` package.  
- **كيف تعرف نمط تاريخ مخصص؟** استخدم `DateFormat` مع كائنات `DateFormatElement` وفاصل.  
- **هل يمكنني البحث باستخدام استعلام نصي؟** نعم، الصيغة `daterange(start ~~ end)` تعمل مباشرة في سلسلة الاستعلام.  
- **ما هي إحداثيات Maven المطلوبة؟** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **هل أحتاج إلى ترخيص للتطوير؟** تجربة مجانية أو ترخيص مؤقت كافية للاختبار؛ ترخيص تجاري مطلوب للإنتاج.

## ما هو تنسيق تاريخ مخصص جافا؟
يخبر تنسيق تاريخ مخصص جافا GroupDocs.Search كيفية تفسير سلاسل التاريخ التي لا تتبع نمط ISO الافتراضي (YYYY‑MM‑DD). من خلال تعريف نمطك الخاص — مثل `MM/dd/yyyy` أو `dd‑MM‑yyyy` — يمكنك تمكين المحرك من التعرف على التواريخ المضمنة في المستندات التي تستخدم تنسيقات إقليمية أو قديمة. تتيح لك هذه القدرة فهرسة واستعلام التواريخ بشكل متسق عبر مصادر متنوعة، مما يحسن كلًا من الاسترجاع والدقة في عمليات البحث التي تركز على التاريخ.

## لماذا تستخدم GroupDocs.Search لاستعلامات نطاق التاريخ؟
يجمع GroupDocs.Search بين الفهرسة عالية السرعة وبناء الاستعلامات المرن، مما يجعله مثاليًا لسيناريوهات نطاق التاريخ. يمكن للمحرك بسرعة تحديد المستندات التي تحتوي على تواريخ ضمن فترة محددة، حتى عندما تظهر تلك التواريخ في نص حر أو حقول البيانات الوصفية. دعمه المدمج لعدة تنسيقات ملفات ومحللات تواريخ قابلة للتخصيص يعني أنك تستطيع التعامل مع مجموعات مستندات متنوعة دون كتابة شفرة خاصة بالتنسيق، مع الحفاظ على أوقات استجابة أقل من الثانية على الفهارس الكبيرة.

## كيفية البحث عن المستندات حسب التاريخ باستخدام GroupDocs.Search
ستقوم بإعداد المكتبة، فهرسة مجلد تجريبي، ثم تشغيل كل من استعلامات النص البسيطة والاستعلامات القائمة على الكائنات الغنية. تبدأ العملية بإنشاء مثيل `Index`، وتكوين أي تنسيقات تاريخ مخصصة تحتاجها، ثم استدعاء واجهة برمجة البحث إما بسلسلة نصية عادية أو بـ `SearchQuery` منظم. يتيح لك هذا النهج اختيار مستوى التحكم الذي يتناسب مع متطلبات تطبيقك.

### المتطلبات المسبقة
- Java 8 أو أحدث مثبت.  
- Maven لإدارة الاعتمادات.  
- الوصول إلى ترخيص GroupDocs.Search (التجربة أو الترخيص المؤقت يعمل للتطوير).  

### إعداد GroupDocs.Search لجافا

#### التثبيت باستخدام Maven
أضف المستودع والاعتماد إلى ملف `pom.xml` الخاص بك:

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
بدلاً من ذلك، يمكنك تنزيل أحدث إصدار مباشرةً من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### التهيئة الأساسية والإعداد
أنشئ مثيل `Index` وأضف مستنداتك:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**مرساة التعريف:** فئة `Index` هي الحاوية الأساسية التي تخزن البيانات الوصفية القابلة للبحث لكل ملف تضيفه، مما يتيح عمليات بحث سريعة عبر مجموعات كبيرة.

## الميزة 1: إنشاء استعلامات بحث نطاق التاريخ

### استخدام استعلام نصي
أسهل طريقة هي تضمين نطاق التاريخ مباشرةً في سلسلة الاستعلام:

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

**الإجابة المباشرة:** حمّل فهرسك، ثم استدعِ `search("daterange(2022-01-01 ~~ 2022-12-31)")` لاسترجاع كل مستند تاريخ فهرسته يقع بين 1 يناير 2022 و31 ديسمبر 2022. يعمل هذا الاستعلام ذو السطر الواحد مباشرةً ويعيد النتائج مرتبة حسب الصلة.

**شرح:** صيغة `daterange` تتوقع تواريخ بصيغة `YYYY‑MM‑DD`. تُرجع جميع المستندات التي تقع تواريخ فهرستها ضمن الفاصل.

### استخدام كائن الاستعلام
للسيطرة البرمجية والتحليل المخصص، أنشئ كائن `SearchQuery`. تمثل فئة `SearchQuery` استعلامًا منظمًا يمكنه دمج معايير متعددة مثل الكلمات المفتاحية، الفلاتر، ونطاقات التاريخ.

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

**الإجابة المباشرة:** أنشئ `SearchQuery` باستخدام `createDateRangeQuery(startDate, endDate)` حيث أن `startDate` و `endDate` هما كائنات `java.util.Date`؛ ثم مرّر الاستعلام إلى `index.search(query)` للحصول على نتائج دقيقة تحترم فروق المناطق الزمنية والتقويمات الخاصة بالمحلية.

**مرساة التعريف:** فئة `SearchQuery` تغلف جميع معايير البحث، مما يتيح لك دمج نطاقات التاريخ مع فلاتر الكلمات المفتاحية، عوامل بوليانية، وقواعد التعزيز.

**شرح:** `createDateRangeQuery` يتيح لك توفير كائنات `java.util.Date`، مما يمنحك مرونة كاملة على المناطق الزمنية ومعالجة خاصة بالمحلية.

## الميزة 2: تحديد أنماط تنسيق تاريخ مخصص جافا

### إعداد تنسيقات تاريخ مخصصة
تخبر فئة `DateFormat` المحرك كيفية تقسيم وتفسير سلسلة التاريخ بناءً على ترتيب العناصر وحروف الفاصل. عرّف `DateFormat` يتطابق مع تمثيل تاريخ مستندك:

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

**الإجابة المباشرة:** امسح التنسيقات الافتراضية باستخدام `dateFormat.clear()`، ثم أضف `DateFormat` جديدًا مبنيًا من كائنات `DateFormatElement` (شهر، يوم، سنة) واضبط الفاصل إلى `/`. بعد ذلك، سيقوم المحرك بتحليل التواريخ المكتوبة كـ `MM/dd/yyyy` بشكل صحيح أثناء الفهرسة ووقت الاستعلام.

**مرساة التعريف:** `DateFormat` هو كائن تكوين يخبر GroupDocs.Search كيفية تقسيم وتفسير سلسلة التاريخ بناءً على ترتيب العناصر وحروف الفاصل.

**شرح:** بمسح التنسيقات الافتراضية وإضافة `DateFormat` يستخدم `/` كفاصل، يصبح المحرك الآن يفهم التواريخ المكتوبة كـ `MM/dd/yyyy`. هذا أمر أساسي لـ **search documents by date** في المناطق التي تفضّل كتابة الشهر أولًا.

## نصائح لتحسين أداء البحث
- **فهرسة تدريجية:** أضف ملفات جديدة إلى الفهرس الحالي بدلاً من إعادة بناءه من الصفر؛ هذا يقلل من استهلاك المعالج بنسبة تصل إلى 70 % للتحديثات اليومية.  
- **إزالة البيانات القديمة:** قم بإزالة المستندات غير المطلوبة بشكل دوري؛ فهرس خفيف يحسن معدلات الضربات في الذاكرة المؤقتة ويقلل من زمن استجابة الاستعلام.  
- **ضبط إعدادات الذاكرة:** زد حجم ذاكرة JVM (`-Xmx4g` أو أعلى) عند التعامل مع فهارس أكبر من 5 GB لتجنب أخطاء نفاد الذاكرة.  
- **تمكين الفهرسة متعددة الخيوط:** استخدم `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` لتوازي معالجة المستندات وتقليل وقت الفهرسة بما يعادل عدد أنوية المعالج.  

## المشكلات الشائعة والحلول
- **أخطاء تحليل التاريخ:** تحقق من أن سلاسل تاريخ المستند تتطابق تمامًا مع النمط المخصص الذي عرّفته؛ الفواصل غير المتطابقة أو فقدان الأصفار البادئة يسبب فشل.  
- **نتائج مفقودة:** تأكد من أن الحقول المفهرسة تحتوي على بيانات وصفية للتاريخ؛ إذا كان المستند يحتوي على تواريخ فقط في فقرات النص الحر، فعّل خيار `ExtractDateMetadata` أثناء الفهرسة.  
- **استثناءات وصول الفهرس:** تأكد من أن مسار `indexFolder` قابل للكتابة وغير مقفل من عملية أخرى؛ استخدم مجلدًا مخصصًا لكل بيئة (dev, test, prod) لتجنب التعارض.  

## التطبيقات العملية
1. **Archival systems** – استرجاع السجلات من فترة تاريخية محددة دون الحاجة إلى تطبيع التواريخ يدويًا.  
2. **Content management** – دعم تنسيقات التاريخ الإقليمية مثل `dd/MM/yyyy` للجمهور الأوروبي، مما يحسن رضا المستخدم.  
3. **Financial software** – تصفية المعاملات حسب الربع المالي أو السنة بسرعة، مما يتيح لوحات تقارير في الوقت الفعلي.  

## لماذا هذا مهم
تنفيذ معالجة **custom date format java** يزيل العوائق الناتجة عن التعامل مع تمثيلات تاريخ غير متسقة عبر المستندات. يتيح لك **handle multiple date formats** في فهرس واحد، مما يضمن حصول المستخدمين النهائيين على نتائج دقيقة بغض النظر عن طريقة تسجيل التواريخ أصلاً. هذه المرونة تحسن صلة البحث، وتقلل من جهد ما قبل المعالجة، وتقصّر زمن الوصول للقيمة في التطبيقات التي تركز على التاريخ.

## الخطوات التالية
- استكشف تركيبات استعلامات متقدمة باستخدام عوامل `AND`، `OR`، و `NOT`.  
- جرّب المحللات المخصصة إذا كنت بحاجة إلى فهرسة بيانات وصفية زمنية إضافية مثل الطوابع الزمنية المدمجة في وسوم XML.  
- راجع دليل تحسين الأداء في الوثائق الرسمية لتوسيع حلّك لملايين المستندات وبيئات متعددة المستأجرين.  

## الأسئلة المتكررة

**س: ما الفرق بين استعلامات النصية واستعلامات الكائنات القائمة على التاريخ؟**  
ج: الشكل النصي سريع وسهل لكنه مقيد بصيغة ISO الافتراضية؛ استعلامات الكائنات تسمح لك بتوفير كائنات `Date` وتنسيقات مخصصة لمزيد من المرونة.

**س: هل يمكنني البحث عن نطاقات تاريخ متعددة في استعلام واحد؟**  
ج: نعم، يمكنك دمج عبارات `daterange` مع عوامل منطقية مثل `AND` أو `OR` لبناء استعلامات معقدة.

**س: هل ستؤدي تنسيقات التاريخ المخصصة إلى إبطاء البحث؟**  
ج: هناك عبء بسيط إضافي للتحليل، لكن الأثر ضئيل بالنسبة لأحمال العمل النموذجية ويتفوق على الفوائد في الدقة.

**س: هل GroupDocs.Search مناسب للنشر على نطاق واسع؟**  
ج: بالتأكيد. مع استراتيجيات الفهرسة المناسبة وضبط JVM، يمكنه التعامل مع ملايين المستندات مع الحفاظ على أوقات استجابة أقل من الثانية.

**س: أين يمكنني العثور على المزيد من أمثلة جافا؟**  
ج: استكشف [مستودع GroupDocs على GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) للحصول على عينات إضافية وتنفيذات حالات الاستخدام.

**الموارد**
- **التوثيق:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **مرجع API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **التنزيل:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **مستودع GitHub:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **عرض على GitHub:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **منتدى الدعم المجاني:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **ترخيص مؤقت:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-10-07  
**تم الاختبار مع:** GroupDocs.Search Java 25.4  
**المؤلف:** GroupDocs  

## دروس ذات صلة
- [ميزات البحث المتقدم في Groupdocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [مكتبة البحث النصي الكامل لجافا – تحسين الفهرس باستخدام GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [كيفية إضافة مستندات إلى الفهرس باستخدام فهرسة البيانات الوصفية في جافا باستخدام GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
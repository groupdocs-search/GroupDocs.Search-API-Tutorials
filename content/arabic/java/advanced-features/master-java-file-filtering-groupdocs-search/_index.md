---
date: '2026-09-06'
description: تعلم كيفية تصفية امتدادات الملفات java باستخدام GroupDocs.Search لـ Java،
  مع تغطية عوامل التشغيل المنطقية AND و OR و NOT، وفلاتر نطاق التاريخ، وفلاتر المسار.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: تصفية امتدادات الملفات java باستخدام GroupDocs.Search. تعلم كيفية
  دمج فلاتر الامتداد، ونطاق التاريخ، والمسار مع عوامل التشغيل المنطقية في Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: تصفية امتدادات الملفات java باستخدام GroupDocs.Search – دليل شامل
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: كيفية تصفية امتدادات الملفات java باستخدام GroupDocs.Search
type: docs
url: /ar/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# تصفية امتدادات الملفات java مع GroupDocs.Search

في هذا الدرس الشامل ستتعلم كيفية **تصفية امتدادات الملفات java** عند فهرسة المستندات باستخدام GroupDocs.Search. في نهاية الدليل ستكون قادرًا على تضمين أنواع الملفات التي تحتاجها فقط، استبعاد الصيغ غير المرغوب فيها، ودمج تلك القواعد مع فلاتر النطاق الزمني والمسار باستخدام عمليات AND و OR و NOT المنطقية. هذه الطريقة تحافظ على خفة الفهرس، تسرّع عمليات البحث، وتساعدك على الالتزام بسياسات معالجة البيانات.

## إجابات سريعة
- **ما هو مرشح امتداد ملف java؟** هو قاعدة تخبر GroupDocs.Search أي امتدادات ملفات يجب تضمينها أو استبعادها أثناء الفهرسة.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Search for Java.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني دمج الفلاتر؟** نعم – يمكنك ربط فلاتر الامتداد، التاريخ، الحجم، والمسار باستخدام منطق AND أو OR أو NOT.  
- **هل هو متوافق مع Maven؟** بالتأكيد – أضف تبعية GroupDocs.Search إلى ملف `pom.xml` الخاص بك.

## ما هو مرشح امتداد ملف java؟
**مرشح امتداد ملف java** هو مجموعة قواعد تقيم امتداد كل ملف قبل إرساله إلى محرك الفهرسة. من خلال تحديد امتدادات مثل `.txt` أو `.pdf` أو `.epub`، يمكنك **تضمين ملفات حسب الامتداد** أو **استبعاد ملفات حسب الامتداد** للحفاظ على تركيز الفهرس وجعل نتائج البحث ذات صلة.

## لماذا نستخدم تصفية امتداد الملفات مع GroupDocs.Search؟
تحسّن تصفية امتداد الملفات كفاءة الفهرسة عبر استبعاد الصيغ غير ذات الصلة، تقلل من متطلبات التخزين، وتساعد على الالتزام بالقواعد التنظيمية عبر منع المحتوى غير المرغوب فيه من الدخول إلى الفهرس. كما تُتيح استجابات أسرع للاستعلامات لأن محرك البحث يعالج مجموعة بيانات أصغر وأكثر صلة.

- **الأداء:** تخطي الملفات غير المرغوب فيها يقلل من عمليات الإدخال/الإخراج ويسرّع الفهرسة بنسبة تصل إلى 40 % في المستودعات الكبيرة.  
- **توفير التخزين:** تُخزن المستندات ذات الصلة فقط في الفهرس، مما يقلل من استهلاك القرص بنسبة متوسطها 30 %.  
- **الامتثال:** منع فهرسة الملفات السرية أو غير المدعومة عن طريق الخطأ.  
- **المرونة:** دمج مع ميزات **date range filter java** لاستهداف الملفات التي تم إنشاؤها أو تعديلها خلال فترات زمنية محددة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

### المكتبات والاعتمادات المطلوبة
- **GroupDocs.Search for Java** – الإصدار 25.4 أو أحدث (يدعم أكثر من 60 صيغة إدخال).  
- **مجموعة تطوير جافا (JDK)** – أي نسخة متوافقة (8 أو أحدث).

### إعداد البيئة
- بيئة تطوير متكاملة (IDE): IntelliJ IDEA، Eclipse، أو أي IDE متوافق مع Maven.

### المتطلبات المعرفية
- برمجة جافا أساسية.  
- الإلمام بعمليات إدخال/إخراج الملفات في جافا.  
- فهم التعابير النمطية (regular expressions) ومعالجة التاريخ‑الوقت.

## إعداد GroupDocs.Search لجافا
لبدء استخدام GroupDocs.Search، تحتاج إلى إضافتها كاعتمادية في مشروعك.

### تكوين Maven
أضف مستودع الاعتماد وتكوين الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

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

### التحميل المباشر
بدلاً من ذلك، حمّل أحدث نسخة مباشرة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### الحصول على الترخيص
1. **نسخة تجريبية** – استكشف الميزات دون تكلفة.  
2. **ترخيص مؤقت** – احصل على الوظائف الكاملة لفترة محدودة.  
3. **شراء** – احصل على ترخيص دائم للاستخدام الإنتاجي.

### التهيئة الأساسية والإعداد
بعد إضافة المكتبة، قم بتهيئة بيئة الفهرسة. تحمل فئة `IndexSettings` جميع خيارات التكوين، بما في ذلك الفلاتر.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## دليل التنفيذ
فيما يلي نستعرض كل نوع من الفلاتر، موضحين **سبب أهميته** ومقدمين تعليمات خطوة بخطوة يمكنك نسخها إلى مشروعك.

### تصفية امتداد الملفات
تصفية الملفات حسب امتداداتها أثناء الفهرسة. هذا مثالي عندما تريد معالجة الكتب الإلكترونية فقط (`.fb2`، `.epub`) والملفات النصية البسيطة (`.txt`).

#### نظرة عامة
`DocumentFilter.createFileExtension` ينشئ قائمة بيضاء من الامتدادات.

#### خطوات التنفيذ
1. **إنشاء الفلتر** – حدد الامتدادات التي تريد الاحتفاظ بها.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **تهيئة الفهرس وإضافة المستندات** – طبّق الفلتر عند إنشاء كائن `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلتر NOT المنطقي
استبعد امتدادات معينة، مثل صفحات الويب وملفات PDF، عندما لا تكون مطلوبة في سيناريو البحث الخاص بك.

#### خطوات التنفيذ
1. **إنشاء فلتر الاستبعاد** – حدد الامتدادات التي تريد رفضها.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **تطبيقه على إعدادات الفهرس** – دمج فلتر NOT مع قواعد أخرى.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **إضافة المستندات** – تُفهرس فقط الملفات التي تجتاز الفلتر المدمج.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلتر AND المنطقي
دمج عدة شروط—تاريخ الإنشاء، الامتداد، وحجم الملف—بحيث **يتم فهرسة الملفات التي تلبي جميع المعايير** فقط.

#### نظرة عامة
`DocumentFilter.createAnd` يدمج عدة فلاتر في قاعدة واحدة.

#### خطوات التنفيذ
1. **تعريف الفلاتر** – أنشئ فلاتر منفصلة لكل شرط.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **دمج الفلاتر** – استخدم عامل AND لفرض جميع الشروط.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **فهرسة المستندات** – مرّر الفلتر المدمج إلى خط أنابيب الفهرسة.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلتر OR المنطقي
تضمين الملفات التي تستوفي **أي** من الشروط المحددة—مفيد عندما تريد التقاط كل من الملفات النصية الصغيرة والملفات غير النصية الأكبر.

#### خطوات التنفيذ
1. **تعريف الفلاتر** – أنشئ فلاتر منفصلة لكل شرط بديل.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **دمج الفلاتر باستخدام الشروط المنطقية** – استخدم عامل OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **إنهاء فلتر OR** – اربط الفلتر المدمج بإعدادات الفهرس.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلاتر وقت الإنشاء
استهدف الملفات التي تم إنشاؤها ضمن فترة زمنية محددة—سيناريو **date range filter java** كلاسيكي.

#### خطوات التنفيذ
1. **تعريف فلتر النطاق الزمني** – حدد تاريخ البدء وتاريخ الانتهاء.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **فهرسة المستندات** – تُفهرس فقط الملفات التي تقع طوابعها الزمنية داخل النطاق المحدد.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلاتر وقت التعديل
استبعد الملفات التي تم تعديلها بعد تاريخ قطع معين.

#### خطوات التنفيذ
1. **تعريف الفلتر** – عيّن الحد الأقصى لطابع التعديل الزمني.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **فهرسة المستندات** – تُتجاهل الملفات الأحدث من تاريخ القطع.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### تصفية مسار الملف
قصر الفهرسة على الملفات الموجودة في مجلدات معينة أو التي تطابق نمطًا ما—مثالي لـ **include files by extension** داخل هيكل دليل محدد.

#### خطوات التنفيذ
1. **تعريف فلتر مسار الملف** – استخدم أنماط glob أو regex لمطابقة الدلائل.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **تهيئة الفهرس وإضافة المستندات** – طبّق فلتر المسار إلى جانب القواعد الأخرى.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## الأخطاء الشائعة والنصائح

- **لا تخلط بين المسارات المطلقة والنسبية** في نفس تكوين الفلتر – قد يؤدي ذلك إلى استثناءات غير متوقعة.  
- **أعد ضبط `IndexSettings`** عند تغيير مجموعات الفلاتر؛ وإلا قد تستمر الفلاتر السابقة في العمل.  
- **ادمج حدًا أعلى للطول مع فلتر الامتداد** للمجموعات الكبيرة لتقليل استهلاك الذاكرة.  
- تتحكم `LoggingOptions` في إعدادات تسجيل GroupDocs.Search.  
- **فعّل التسجيل** (`LoggingOptions.setEnabled(true)`) لتعرف سبب رفض ملف معين.  

## الأسئلة المتكررة

**س: هل يمكنني تغيير معايير الفلتر بعد إنشاء الفهرس؟**  
ج: نعم. أعد بناء الفهرس باستخدام `DocumentFilter` جديد أو استخدم الفهرسة التزايدية مع إعدادات محدثة.

**س: هل يعمل مرشح امتداد ملف java على الأرشيفات المضغوطة (مثل ZIP)؟**  
ج: يمكن لـ GroupDocs.Search فهرسة صيغ الأرشيف المدعومة، لكن فلتر الامتداد يُطبق على الأرشيف نفسه، وليس على الملفات الداخلية. استخدم فلاتر متداخلة للتحكم الأعمق.

**س: كيف يمكنني تتبع سبب استبعاد ملف معين؟**  
ج: فعّل تسجيل المكتبة (`LoggingOptions.setEnabled(true)`) وتفقد السجل – سيظهر أي فلتر رفض كل ملف.

**س: هل يمكن دمج مرشح امتداد ملف java مع فلاتر regex مخصصة؟**  
ج: بالتأكيد. ضع فلتر regex داخل `DocumentFilter.createAnd()` إلى جانب فلتر الامتداد.

**س: ما هو تأثير الأداء لإضافة العديد من الفلاتر؟**  
ج: كل فلتر يضيف عبئًا بسيطًا أثناء الفهرسة، لكن تقليل حجم البيانات المفهرسة عادةً ما يفوق تكلفة الفلاتر. اختبر على عينة تمثيلية لتحديد التوازن المثالي.

---

**آخر تحديث:** 2026-09-06  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [Custom Date Format Java | Date Range Search with GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Master Boolean Searches with GroupDocs.Search for Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optimize Search Performance with Advanced Indexing Techniques in GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
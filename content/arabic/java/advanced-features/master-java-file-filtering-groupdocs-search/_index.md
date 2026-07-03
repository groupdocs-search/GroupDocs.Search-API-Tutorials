---
date: '2026-02-21'
description: تعلم كيفية تنفيذ مرشح امتداد ملفات جافا باستخدام GroupDocs.Search للغة
  جافا، مع تغطية المشغلات المنطقية وتواريخ الإنشاء/التعديل ومرشحات المسار.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: مرشح امتداد ملفات جافا مع GroupDocs.Search – دليل
type: docs
url: /ar/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# إتقان مرشح امتداد ملفات java مع GroupDocs.Search

إدارة مستودع متنامٍ من المستندات يمكن أن تصبح مرهقة بسرعة، خاصةً عندما تحتاج إلى فهرسة أنواع ملفات معينة فقط. **مرشح امتداد ملفات java** يتيح لك إخبار GroupDocs.Search بالامتدادات التي تريد تضمينها أو استبعادها، مما يمنحك تحكمًا دقيقًا في خط أنابيب الفهرسة. في هذا الدليل سنستعرض إعداد GroupDocs.Search للغة Java ونوضح لك كيفية دمج تصفية امتداد الملفات مع عوامل المنطق AND و OR و NOT، بالإضافة إلى فلاتر نطاق التاريخ والمسار.

## إجابات سريعة
- **ما هو مرشح امتداد ملفات java؟** تكوين يخبر GroupDocs.Search أي امتدادات ملفات يجب تضمينها أو استبعادها أثناء الفهرسة.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Search for Java.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني دمج الفلاتر؟** نعم – يمكنك ربط فلاتر الامتداد، التاريخ، الحجم، والمسار باستخدام منطق AND، OR، NOT.  
- **هل هو متوافق مع Maven؟** بالتأكيد – أضف تبعية GroupDocs.Search إلى ملف `pom.xml` الخاص بك.

## ما هو مرشح امتداد ملفات java؟
**مرشح امتداد ملفات java** هو مجموعة من القواعد التي تقيم امتداد كل ملف قبل إرساله إلى محرك الفهرسة. من خلال تحديد امتدادات مثل `.txt`، `.pdf`، أو `.epub`، يمكنك **تضمين ملفات حسب الامتداد** أو **استبعاد ملفات حسب الامتداد** للحفاظ على تركيز الفهرس وملاءمة نتائج البحث.

## لماذا نستخدم تصفية امتداد الملفات مع GroupDocs.Search؟
- **الأداء:** تخطي الملفات غير المرغوب فيها يقلل من عمليات الإدخال/الإخراج ويسرّع الفهرسة.  
- **توفير التخزين:** يتم تخزين المستندات ذات الصلة فقط في الفهرس، مما يقلل من استهلاك القرص.  
- **الامتثال:** منع الفهرسة العرضية للملفات السرية أو غير المدعومة.  
- **المرونة:** دمج مع ميزات **date range filter java** لاستهداف الملفات التي تم إنشاؤها أو تعديلها ضمن فترات زمنية محددة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

### المكتبات والاعتمادات المطلوبة
- **GroupDocs.Search for Java**: الإصدار 25.4 أو أحدث  
- **Java Development Kit (JDK)**: نسخة متوافقة مثبتة  

### إعداد البيئة
- بيئة التطوير المتكاملة (IDE): IntelliJ IDEA، Eclipse، أو أي IDE متوافق مع Maven.

### المتطلبات المعرفية المسبقة
- برمجة Java الأساسية  
- الإلمام بعمليات الإدخال/الإخراج للملفات في Java  
- فهم التعبيرات النمطية (regular expressions) ومعالجة التاريخ والوقت  

## إعداد GroupDocs.Search للغة Java
للبدء في استخدام GroupDocs.Search، تحتاج إلى إضافته كاعتماد في مشروعك.

### تكوين Maven
أضف تكوين المستودع والاعتماد التالي إلى ملف `pom.xml` الخاص بك:

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
بدلاً من ذلك، قم بتحميل أحدث نسخة مباشرة من [إصدارات GroupDocs.Search للغة Java](https://releases.groupdocs.com/search/java/).

#### الحصول على الترخيص
1. **نسخة تجريبية مجانية** – استكشف الميزات دون تكلفة.  
2. **ترخيص مؤقت** – الحصول على الوظائف الكاملة لفترة محدودة.  
3. **شراء** – الحصول على ترخيص دائم للاستخدام في الإنتاج.  

### التهيئة الأساسية والإعداد
بمجرد إضافة المكتبة، قم بتهيئة بيئة الفهرسة الخاصة بك:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## دليل التنفيذ
أدناه نستعرض كل نوع من الفلاتر، موضحين **سبب أهميته** ومقدمين كود خطوة بخطوة يمكنك نسخه إلى مشروعك.

### تصفية امتداد الملفات
صَفِّ الملفات حسب امتداداتها أثناء الفهرسة. هذا مثالي عندما تريد معالجة الكتب الإلكترونية (`.fb2`, `.epub`) وملفات النص العادي (`.txt`) فقط.

#### نظرة عامة
استخدم `DocumentFilter.createFileExtension` لإنشاء قائمة بيضاء من الامتدادات.

#### خطوات التنفيذ
1. **إنشاء الفلتر**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **تهيئة الفهرس وإضافة المستندات**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلتر NOT المنطقي
استبعاد امتدادات محددة، مثل صفحات الويب وملفات PDF، عندما لا تكون مطلوبة في سيناريو البحث الخاص بك.

#### خطوات التنفيذ
1. **إنشاء فلتر الاستبعاد**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **تطبيقه على إعدادات الفهرس**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **إضافة المستندات**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلتر AND المنطقي
دمج عدة شروط—تاريخ الإنشاء، الامتداد، وحجم الملف—بحيث **فقط الملفات التي تلبي جميع المعايير** يتم فهرستها.

#### نظرة عامة
`DocumentFilter.createAnd` يدمج عدة فلاتر في قاعدة واحدة.

#### خطوات التنفيذ
1. **تعريف الفلاتر**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **دمج الفلاتر**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **فهرسة المستندات**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلتر OR المنطقي
تضمين الملفات التي تلبي **أي** من الشروط المحددة—مفيد عندما تريد التقاط كل من ملفات النص الصغيرة والملفات غير النصية الأكبر حجماً.

#### خطوات التنفيذ
1. **تعريف الفلاتر**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **دمج الفلاتر مع الشروط المنطقية**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **إنهاء فلتر OR**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلاتر وقت الإنشاء
استهداف الملفات التي تم إنشاؤها ضمن فترة محددة—سيناريو **date range filter java** كلاسيكي.

#### خطوات التنفيذ
1. **تعريف فلتر نطاق التاريخ**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **فهرسة المستندات**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### فلاتر وقت التعديل
استبعاد الملفات التي تم تعديلها بعد تاريخ قطع معين.

#### خطوات التنفيذ
1. **تعريف الفلتر**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **فهرسة المستندات**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### تصفية مسار الملف
تقييد الفهرسة للملفات الموجودة في مجلدات معينة أو التي تطابق نمطًا—مثالي لـ **include files by extension** داخل هيكل دليل محدد.

#### خطوات التنفيذ
1. **تعريف فلتر مسار الملف**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **تهيئة الفهرس وإضافة المستندات**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## الأخطاء الشائعة والنصائح
- **لا تخلط أبداً بين المسارات المطلقة والنسبية** في نفس تكوين الفلتر – قد يؤدي ذلك إلى استثناءات غير متوقعة.  
- **أعد ضبط `IndexSettings`** عند تبديل مجموعات الفلاتر؛ وإلا قد تستمر الفلاتر السابقة.  
- **اجمع حدًا أعلى للطول مع فلتر الامتداد** للمجموعات الكبيرة لتقليل استهلاك الذاكرة.  
- **فعّل التسجيل** (`LoggingOptions.setEnabled(true)`) لمعرفة سبب رفض ملف ما.  

## الأسئلة المتكررة

**س: هل يمكنني تغيير معايير الفلتر بعد إنشاء الفهرس؟**  
ج: نعم. أعد بناء الفهرس باستخدام `DocumentFilter` جديد أو استخدم الفهرسة التزايدية مع إعدادات محدثة.

**س: هل يعمل مرشح امتداد ملفات java على الأرشيفات المضغوطة (مثل ZIP)؟**  
ج: يمكن لـ GroupDocs.Search فهرسة صيغ الأرشيف المدعومة، لكن فلتر الامتداد يطبق على الأرشيف نفسه، وليس على الملفات الداخلية. استخدم فلاتر متداخلة للتحكم الأعمق.

**س: كيف يمكنني تتبع سبب استبعاد ملف معين؟**  
ج: فعّل تسجيل المكتبة (`LoggingOptions.setEnabled(true)`) وتفقد السجل – فهو يوضح أي فلتر رفض كل ملف.

**س: هل يمكن دمج مرشح امتداد ملفات java مع فلاتر regex مخصصة؟**  
ج: بالتأكيد. ضع فلتر regex داخل `DocumentFilter.createAnd()` إلى جانب فلتر الامتداد.

**س: ما هو تأثير الأداء عند إضافة العديد من الفلاتر؟**  
ج: كل فلتر يضيف عبئًا بسيطًا أثناء الفهرسة، لكن تقليل البيانات المفهرسة عادةً ما يفوق التكلفة. اختبر باستخدام عينة تمثيلية للعثور على التوازن المثالي.

---

**آخر تحديث:** 2026-02-21  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs
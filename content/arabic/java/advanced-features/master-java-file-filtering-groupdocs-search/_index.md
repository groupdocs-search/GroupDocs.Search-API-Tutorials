---
date: '2025-12-19'
description: تعلم كيفية تنفيذ مرشح امتداد ملفات جافا باستخدام GroupDocs.Search للغة
  جافا، مع تغطية عوامل التشغيل المنطقية وتواريخ الإنشاء/التعديل ومرشحات المسار.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: مرشح امتداد ملفات جافا مع GroupDocs.Search – دليل
type: docs
url: /ar/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# إتقان مرشح امتداد ملفات الجافا مع GroupDocs.Search

إدارة مستودع متزايد من المستندات يمكن أن تصبح مرهقة بسرعة. سواء كنت بحاجة إلى فهرسة أنواع مستندات محددة فقط أو استبعاد ملفات غير ذات صلة، فإن **مرشح امتداد ملفات الجافا** يمنحك تحكمًا دقيقًا في ما يتم معالجته. في هذا الدليل سنستعرض إعداد GroupDocs.Search للغة Java وسنظهر لك كيفية دمج تصفية امتداد الملفات مع عوامل المنطق AND و OR و NOT، بالإضافة إلى مرشحات النطاق الزمني والمسار.

## إجابات سريعة
- **ما هو مرشح امتداد ملفات الجافا؟** تكوين يخبر GroupDocs.Search أي امتدادات ملفات يجب تضمينها أو استبعادها أثناء الفهرسة.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Search للغة Java.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني دمج المرشحات؟** نعم – يمكنك ربط مرشحات الامتداد، التاريخ، الحجم، والمسار باستخدام منطق AND و OR و NOT.  
- **هل هو متوافق مع Maven؟** بالتأكيد – أضف تبعية GroupDocs.Search إلى ملف `pom.xml` الخاص بك.

## المقدمة

هل تواجه صعوبة في إدارة مستودع متزايد من الملفات بفعالية؟ سواء كنت تحتاج إلى تنظيم المستندات حسب النوع أو تصفية الملفات غير الضرورية أثناء الفهرسة، فإن المهمة قد تكون شاقة دون الأدوات المناسبة. **GroupDocs.Search للغة Java** هو مكتبة بحث متقدمة تبسط هذه التحديات من خلال قدرات تصفية ملفات قوية. سيوجهك هذا البرنامج التعليمي إلى تنفيذ تقنيات تصفية الملفات باستخدام GroupDocs.Search، مع التركيز على عوامل المنطق AND و OR و NOT.

### ما ستتعلمه
- إعداد GroupDocs.Search في بيئة Java الخاصة بك  
- تنفيذ مرشحات مختلفة: امتداد الملف، عوامل المنطق (AND, OR, NOT)، وقت الإنشاء، وقت التعديل، مسار الملف، والطول  
- تطبيقات واقعية لهذه المرشحات لإدارة مستندات فعّالة  
- نصائح تحسين الأداء لمهام الفهرسة على نطاق واسع  

هل أنت مستعد لاستكشاف الإمكانات الكاملة لتصفية الملفات في Java؟ لنبدأ بالمتطلبات المسبقة أولاً.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

### المكتبات والتبعيات المطلوبة
- **GroupDocs.Search للغة Java**: الإصدار 25.4 أو أحدث  
- **مجموعة تطوير جافا (JDK)**: تأكد من تثبيت نسخة متوافقة على نظامك  

### إعداد البيئة
- بيئة تطوير متكاملة (IDE): استخدم IntelliJ IDEA أو Eclipse أو أي IDE مفضلة تدعم مشاريع Maven.

### المتطلبات المعرفية
- فهم أساسي لبرمجة Java  
- إلمام بعمليات الإدخال/الإخراج للملفات في Java  
- فهم التعابير النمطية (Regular Expressions) ومعالجة التواريخ والأوقات  

## إعداد GroupDocs.Search للغة Java
لبدء استخدام GroupDocs.Search، تحتاج إلى إضافتها كاعتماد في مشروعك. إليك الطريقة:

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
بدلاً من ذلك، قم بتحميل أحدث نسخة مباشرة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### الحصول على الترخيص
1. **نسخة تجريبية مجانية**: ابدأ بنسخة تجريبية لاستكشاف ميزات GroupDocs.Search.  
2. **ترخيص مؤقت**: قدّم طلبًا للحصول على ترخيص مؤقت للوصول إلى جميع الوظائف دون قيود.  
3. **شراء**: للاستخدام طويل الأمد، اشترِ اشتراكًا.  

### التهيئة الأساسية والإعداد
بعد إضافة المكتبة، قم بتهيئة بيئة الفهرسة الخاصة بك:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## دليل التنفيذ
الآن، دعنا نستكشف كيفية تنفيذ ميزات تصفية الملفات المختلفة باستخدام GroupDocs.Search.

### تصفية امتداد الملف
تصفية الملفات حسب امتداداتها أثناء الفهرسة. هذه الميزة مفيدة لمعالجة أنواع مستندات محددة فقط مثل FB2 و EPUB و TXT.

#### نظرة عامة
تصفية المستندات بناءً على امتداد الملف باستخدام تكوين مرشح مخصص.

#### خطوات التنفيذ
1. **إنشاء مرشح**:
    
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

### مرشح NOT المنطقي
استبعاد امتدادات ملفات محددة أثناء الفهرسة، مثل HTM و HTML و PDF.

#### خطوات التنفيذ
1. **إنشاء مرشح الاستبعاد**:
    
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

### مرشح AND المنطقي
دمج معايير متعددة لتضمين الملفات التي تفي بجميع الشروط المحددة.

#### نظرة عامة
استخدام عمليات AND المنطقية لتصفية الملفات بناءً على وقت الإنشاء، امتداد الملف، والطول.

#### خطوات التنفيذ
1. **تعريف المرشحات**:
    
    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **دمج المرشحات**:
    
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

### مرشح OR المنطقي
تضمين الملفات التي تفي بأي من المعايير المحددة باستخدام عمليات OR المنطقية.

#### خطوات التنفيذ
1. **تعريف المرشحات**:
    
    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **دمج المرشحات مع الشروط المنطقية**:
    
    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **إنهاء مرشح OR**:
    
    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### مرشحات وقت الإنشاء
تصفية الملفات بناءً على وقت إنشائها لتضمين فقط تلك التي تقع ضمن نطاق تاريخ محدد.

#### خطوات التنفيذ
1. **تعريف مرشح نطاق التاريخ**:
    
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

### مرشحات وقت التعديل
استبعاد الملفات التي تم تعديلها بعد تاريخ معين.

#### خطوات التنفيذ
1. **تعريف المرشح**:
    
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
تصفية الملفات بناءً على مساراتها لتضمين فقط تلك الموجودة في أدلة محددة.

#### خطوات التنفيذ
1. **تعريف مرشح مسار الملف**:
    
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

- **لا تخلط بين المسارات المطلقة والنسبية** في نفس تكوين المرشح – ذلك قد يؤدي إلى استثناءات غير متوقعة.  
- **تذكر إعادة ضبط `IndexSettings`** عند الانتقال من مجموعة مرشحات إلى أخرى؛ وإلا قد تبقى المرشحات السابقة سارية.  
- **المجموعات الكبيرة من الملفات** تستفيد من دمج حد أعلى للطول مع مرشح الامتداد لتقليل استهلاك الذاكرة.  

## الأسئلة المتكررة

**س: هل يمكنني تغيير معايير المرشح بعد إنشاء الفهرس؟**  
ج: نعم. يمكنك إعادة بناء الفهرس باستخدام `DocumentFilter` جديد أو استخدام الفهرسة التزايدية مع إعدادات محدثة.

**س: هل يعمل مرشح امتداد ملفات الجافا على الأرشيفات المضغوطة (مثل ZIP)؟**  
ج: يمكن لـ GroupDocs.Search فهرسة صيغ الأرشيف المدعومة، لكن مرشح الامتداد يطبق على الأرشيف نفسه، وليس على الملفات الداخلية. استخدم مرشحات متداخلة إذا لزم الأمر.

**س: كيف يمكنني تتبع سبب استبعاد ملف معين؟**  
ج: فعّل تسجيل المكتبة (اضبط `LoggingOptions.setEnabled(true)`) وتفقد السجل المُنشأ – سيظهر أي مرشح رفض كل ملف.

**س: هل يمكن دمج مرشح امتداد ملفات الجافا مع مرشحات regex مخصصة؟**  
ج: بالتأكيد. يمكنك تغليف مرشح regex داخل `DocumentFilter.createAnd()` إلى جانب مرشح الامتداد.

**س: هو تأثير الأداء عند إضافة العديد من المرشحات؟**  
ج: كل مرشح إضافي يضيف عبئًا بسيطًا أثناء الفهرسة، لكن الفائدة من تقليل حجم الفهرس عادةً ما تفوق التكلفة. اختبر على مجموعة عينات لتحديد التوازن المثالي.

---

**آخر تحديث:** 2025-12-19  
**تم الاختبار مع:** GroupDocs.Search 25.4 للغة Java  
**المؤلف:** GroupDocs  

---
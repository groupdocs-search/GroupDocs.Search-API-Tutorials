---
date: '2026-08-05'
description: تعلم كيفية بناء مستخرج log file للبحث full-text search في Java باستخدام
  GroupDocs.Search. أضف المستندات إلى index، حسّن أداء البحث، وتعامل مع log files
  الكبيرة بكفاءة.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: يظهر دليل بحث النص الكامل Java كيفية بناء مستخرج مخصص لملفات السجل
  باستخدام GroupDocs.Search، إضافة المستندات إلى index، وتحسين أداء البحث لأرشيفات
  السجل الضخمة.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'بحث النص الكامل Java: مستخرج log file باستخدام GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'بحث النص الكامل Java: مستخرج log file باستخدام GroupDocs'
type: docs
url: /ar/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# بحث النص الكامل جافا: مستخرج ملفات السجل مع GroupDocs

بحث النص الكامل جافا هو حجر الأساس لأي نظام يجب أن يحدد المعلومات بسرعة داخل مجموعات ضخمة من المستندات. في هذا الدرس ستتعلم كيفية تكوين GroupDocs.Search، إنشاء مستخرج ملفات سجل مخصص، إضافة مستندات إلى الفهرس، وتحسين أداء البحث عند التعامل مع جيغابايتات من بيانات السجل.

## ما ستتعلمه
- إعداد وتكوين GroupDocs.Search لجافا.  
- تنفيذ **مستخرج ملفات السجل** الذي يحلل سجلات النص العادي بالطريقة التي تحتاجها.  
- **إضافة مستندات إلى الفهرس** جنبًا إلى جنب مع PDFs، DOCX، وغيرها من الصيغ.  
- سيناريوهات واقعية حيث يضيف **مستخرج ملفات السجل** قيمة قابلة للقياس.  
- نصائح مثبتة لـ **تحسين أداء البحث** لأرشيفات السجل متعددة الجيغابايت.

## إجابات سريعة
- **ما هو مستخرج ملفات السجل؟** مكوّن مخصص يخبر GroupDocs.Search كيفية قراءة وفهرسة ملفات السجل النصية.  
- **لماذا تستخدم GroupDocs.Search؟** يدعم فهرسة أكثر من 50 صيغة، يوفر إعادة فهرسة تلقائية، ويتعامل مع فهارس تصل إلى 10 GB بأقل من 2 GB RAM.  
- **هل أحتاج إلى ترخيص؟** نعم – يلزم ترخيص تجريبي أو كامل لتفعيل المكتبة.  
- **هل يمكنني فهرسة أنواع ملفات أخرى في نفس الوقت؟** بالتأكيد؛ امزج PDFs، DOCX، وملفات السجل المخصصة في نفس الفهرس.  
- **كيف تحسن الأداء؟** استخدم الفهرسة المتزايدة، اضبط `IndexSettings`، وفعل علم `autoReindex`.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك ما يلي:

### المكتبات المطلوبة
أضف تبعية GroupDocs.Search Maven إلى ملف `pom.xml`. استخدم أحدث نسخة تتطابق مع مستوى جافا في مشروعك.

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

بدلاً من ذلك، قم بتنزيل أحدث نسخة مباشرة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### إعداد البيئة
- JDK 8 أو أعلى.  
- الإلمام ببرمجة جافا ومفاهيم التعامل مع الملفات الأساسية.

### الحصول على الترخيص
ابدأ بتنزيل ترخيص تجريبي مجاني لاستكشاف ميزات GroupDocs.Search. للاستخدام في الإنتاج، اشترِ ترخيصًا كاملًا أو اطلب ترخيصًا مؤقتًا عبر [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## إعداد GroupDocs.Search لجافا

للشروع، قم بتهيئة المكتبة وتطبيق ملف الترخيص الخاص بك:

1. **إعداد Maven** – تأكد من وجود التبعية من الخطوة السابقة.  
2. **تهيئة الترخيص** – حمّل ملف الترخيص قبل أي استدعاءات API أخرى.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

مع جاهزية البيئة، يمكنك المتابعة لبناء **مستخرج ملفات السجل** المخصص.

## ما هو مستخرج ملفات السجل؟

مستخرج ملفات السجل هو قطعة من الشيفرة تخبر GroupDocs.Search كيفية قراءة ملفات السجل الخام (عادةً `.log`) وتحويل محتوياتها إلى نص قابل للبحث. من خلال توفير مستخرج خاص بك تحصل على تحكم كامل في قواعد التحليل، تصفية الضوضاء، واستخراج المعلومات التي تهم حالة البحث الخاصة بك.

## إنشاء مستخرج ملفات السجل

يتيح لك GroupDocs.Search توصيل مستخرجات نص مخصصة لأي نوع ملف. اتبع الخطوات التالية لإنشاء واحد لملفات السجل.

### الخطوة 1: تعريف المستخرج المخصص
`TextExtractorBase` هو الفئة الأساسية المجردة التي تقوم بتمديدها لإنشاء مستخرج مخصص. يعلن عن امتدادات الملفات التي يدعمها المستخرج ويحتوي على منطق الاستخراج الأساسي.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**نقاط رئيسية**  
- `getFileExtensions()` يسجل المستخرج لملفات `.log`.  
- `extractText` هو المكان الذي يمكنك فيه إزالة الطوابع الزمنية، تصفية خطوط التصحيح، أو تطبيق أي معالجة مسبقة ضرورية لـ **البحث في ملفات السجل الكبيرة**.

### الخطوة 2: تكوين إعدادات الفهرس مع المستخرج
أضف المستخرج إلى `IndexSettings` وفعل `autoReindex` بحيث يتم فهرسة السجلات الجديدة تلقائيًا دون تدخل يدوي.

`IndexSettings` يكوّن سلوك الفهرس مثل حدود الذاكرة والمستخرجات المخصصة.  
`autoReindex` يحدث الفهرس تلقائيًا عندما تتغير ملفات المصدر.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### الخطوة 3: إضافة مستندات إلى الفهرس
الآن بعد أن الفهرس يتعرف على ملفات السجل، يمكنك **إضافة مستندات إلى الفهرس** كما هو الحال مع أي صيغة مدعومة أخرى.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### الخطوة 4: البحث في الفهرس
قم بتنفيذ استعلامات نصية عادية. يضمن المستخرج المخصص أن كل إدخال سجل قابل للبحث.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## نصائح لتحسين أداء البحث

- **الفهرسة المتزايدة** – أضف فقط ملفات السجل الجديدة أو المتغيرة بدلاً من إعادة بناء الفهرس بالكامل.  
- **إدارة الذاكرة** – علم `autoReindex` يحافظ على انخفاض استهلاك الذاكرة عن طريق تفريغ البيانات الوسيطة إلى القرص.  
- **إعدادات الفهرس** – اضبط `setMaxMemoryUsage` بناءً على سعة الخادم؛ الإعداد النموذجي هو 1 GB لفهرس بحجم 10 GB.  
- **تحسين الاستعلام** – استخدم استعلامات العبارة، الأحرف البديلة، أو الفلاتر لتضييق النتائج عند البحث في أرشيفات السجل الضخمة.

## تطبيقات عملية

يمكن تطبيق GroupDocs.Search في العديد من السيناريوهات الواقعية، مثل:

- **إدارة السجلات** – تحديد رسائل الخطأ، إجراءات المستخدم، أو طوابع زمنية محددة عبر جيغابايتات من بيانات السجل في ثوانٍ.  
- **أنظمة استرجاع المستندات** – الحفاظ على مستودع واحد قابل للبحث يشمل PDFs، مستندات Word، جداول البيانات، وملفات السجل المخصصة.  
- **تحليل المحتوى** – تشغيل تقارير تكرار الكلمات المفتاحية أو اكتشاف الشذوذ في بيانات السجل المتدفقة.

## اعتبارات الأداء

عند نشر GroupDocs.Search على نطاق واسع، احرص على مراعاة هذه الممارسات الأفضل:

- خزن الفهارس على SSDs سريعة لتقليل زمن القراءة/الكتابة.  
- راقب استهلاك كومة JVM؛ فكر في تفريغ الفهارس الكبيرة إلى عملية منفصلة إذا أصبحت الذاكرة عنق زجاجة.  
- فعّل `autoReindex` (كما هو موضح) للحفاظ على تحديث الفهرس دون إعادة بناء يدوية.

## الخلاصة

حتى الآن، لقد أنشأت **مستخرج ملفات السجل**، وتعلمت كيفية **إضافة مستندات إلى الفهرس**، واكتشفت طرقًا لـ **تحسين أداء البحث** لأرشيفات السجل الكبيرة. هذه المجموعة تمكّن تطبيقات جافا الخاصة بك من توفير بحث نص كامل سريع ودقيق عبر أي نوع مستند.

لمزيد من الاستكشاف، راجع [GroupDocs documentation](https://docs.groupdocs.com/search/java/) الرسمي أو جرب تنفيذات مستخرج مختلفة لتناسب حالة الاستخدام الفريدة الخاصة بك.

## قسم الأسئلة المتكررة
1. **ما أنواع الملفات التي يمكنني فهرستها باستخدام GroupDocs.Search؟**  
   - يمكنك فهرسة PDFs، مستندات Word، جداول البيانات، والعديد من الصيغ الأخرى، بالإضافة إلى ملفات السجل المخصصة عبر مستخرجات النص.  
2. **كيف أتعامل مع مجموعات مستندات كبيرة بكفاءة؟**  
   - استخدم التحديثات المتزايدة، قسّم الفهارس، واضبط `IndexSettings` لإدارة الموارد بفعالية.  
3. **هل يمكن دمج GroupDocs.Search مع أنظمة أخرى؟**  
   - نعم، فهو يقدم API جافا نظيف يمكن دمجه في الخدمات الحالية، الخدمات الصغيرة (micro‑services)، أو تطبيقات الويب.  
4. **ما هو الترخيص المؤقت، وكيف أحصل عليه؟**  
   - الترخيص المؤقت يمنح كامل الوظائف للتقييم دون حدود زمنية. قدِّم طلبًا عبر [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## أسئلة متكررة

**س: كيف يختلف مستخرج ملفات السجل عن المستخرج الافتراضي؟**  
ج: المستخرج الافتراضي يتعامل مع الصيغ الشائعة (PDF، DOCX، إلخ). يتيح لك مستخرج ملفات السجل المخصص تحديد كيفية تحليل وفهرسة إدخالات السجل النصية بدقة.

**س: هل يمكنني فهرسة أرشيفات السجل المضغوطة (مثل .zip)؟**  
ج: نعم، عبر إضافة خطوة معالجة مسبقة تستخرج الملفات من الأرشيف قبل تمريرها إلى الفهرس.

**س: ما هي أفضل طريقة للحفاظ على تحديث الفهرس مع السجلات التي تُولد باستمرار؟**  
ج: فعّل `autoReindex` وجدول مراقب خلفية يستدعي `index.add(newLogFile)` كلما ظهر ملف جديد.

**س: هل هناك حد لحجم ملف سجل واحد يمكن فهرسته؟**  
ج: عمليًا، الحد مرتبط بالذاكرة المتاحة. يُنصح بتقسيم السجلات الكبيرة جدًا إلى أجزاء أصغر قبل الفهرسة.

**س: هل يدعم GroupDocs.Search البحث الضبابي أو باستخدام الأحرف البديلة؟**  
ج: نعم، تشمل API البحث مطابقة ضبابية، أحرف بديلة، واستعلامات القرب لتحسين صلة النتائج.

---

**آخر تحديث:** 2026-08-05  
**تم الاختبار مع:** GroupDocs.Search 25.4 لجافا  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [بحث النص الكامل جافا: بناء الفهرس باستخدام GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [كيفية إضافة مستندات إلى الفهرس باستخدام GroupDocs.Search لجافا](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [تحسين أداء الاستعلام مع GroupDocs.Search جافا: تحسين الفهرس والبحث](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
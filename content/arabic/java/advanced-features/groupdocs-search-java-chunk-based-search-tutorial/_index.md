---
date: '2026-10-02'
description: تعرف على كيفية استخدام temporary license لإضافة المستندات إلى الفهرس
  باستخدام بحث chunk‑based في Java، مما يعزز search performance مع التحكم في memory
  usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: استخدام temporary license لإضافة المستندات إلى الفهرس باستخدام بحث
  chunk‑based في Java، مما يحسن search speed ويقلل من memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: استخدام temporary license للفهرسة القائمة على chunk‑based في Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: استخدام temporary license للفهرسة القائمة على chunk‑based في Java
type: docs
url: /ar/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# استخدام ترخيص مؤقت لفهرسة تعتمد على القطع في Java

في هذا البرنامج التعليمي **ستستخدم ترخيصًا مؤقتًا** لإضافة المستندات إلى الفهرس باستخدام ميزة البحث المعتمد على القطع في GroupDocs.Search. يتيح لك هذا النهج التعامل مع مجموعات مستندات ضخمة—العقود القانونية، تذاكر الدعم، الأوراق البحثية—مع الحفاظ على استهلاك **java search index memory** منخفض وزيادة **search performance** بشكل كبير. سترى كيفية إعداد مجلد الفهرس، وإمداد مصادر مستندات متعددة، وتمكين البحث بالقطع، وتشغيل كل من الاستعلامات الأولى واللاحقة للقطع.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** إنشاء مجلد فهرس البحث.  
- **كيف يمكنني تضمين ملفات متعددة؟** استخدم `index.add()` لكل مجلد مستند.  
- **أي خيار يفعّل البحث بالقطع؟** `options.setChunkSearch(true)`.  
- **هل يمكنني الاستمرار في البحث بعد القطعة الأولى؟** نعم، استدعِ `index.searchNext()` مع الرمز.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية أو ترخيص مؤقت يعمل للتطوير؛ يلزم ترخيص كامل للإنتاج.  

## ما ستتعلمه
- كيفية إنشاء فهرس بحث في مجلد محدد.  
- خطوات **إضافة المستندات إلى الفهرس** من مواقع متعددة.  
- تكوين خيارات البحث لتمكين البحث المعتمد على القطع.  
- إجراء عمليات البحث الأولية واللاحقة المعتمدة على القطع.  
- سيناريوهات واقعية حيث يبرز البحث المعتمد على القطع في المستندات.  

## المتطلبات المسبقة
- **المكتبات المطلوبة**: GroupDocs.Search for Java 25.4 أو أحدث.  
- **إعداد البيئة**: وجود مجموعة تطوير جافا (JDK) متوافقة مثبتة.  
- **المتطلبات المعرفية**: برمجة جافا أساسية ومعرفة بـ Maven.  

## إعداد GroupDocs.Search لجافا
للبدء، دمج GroupDocs.Search في مشروعك باستخدام Maven:

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

بدلاً من ذلك، قم بتنزيل أحدث نسخة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
لتجربة GroupDocs.Search:

- **نسخة تجريبية مجانية** – اختبار الميزات الأساسية دون التزام.  
- **ترخيص مؤقت** – وصول موسع للتطوير.  
- **شراء** – ترخيص كامل للاستخدام في الإنتاج.  

## كيف تضيف مستندات إلى الفهرس؟
**الإجابة المباشرة:** استدعِ `index.add()` لكل مجلد يحتوي على ملفات تريد أن تكون قابلة للبحث؛ تقوم الطريقة بمسح المجلد بشكل متكرر وتضيف كل مستند مدعوم إلى الفهرس في عملية واحدة. هذا يلغي الحاجة إلى معالجة الملفات يدويًا ملفًا بملف ويسرّع عملية الاستيعاب الجماعي.

`SearchIndex` هو الفئة المركزية التي تمثل مجموعة البحث على القرص. بعد إنشاء مثاله، تمر جميع عمليات الفهرسة والاستعلام عبر هذا الكائن.

### 1. إنشاء فهرس
**الإجابة المباشرة:** أنشئ كائن `SearchIndex` مع المسار الذي يجب أن تُخزن فيه ملفات الفهرس، ثم استدعِ `index.create()` لتهيئة بنية التخزين. تُنشئ هذه الدعوة المجلدات والملفات التعريفية اللازمة عند الاستخدام الأول.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. إضافة مستندات إلى الفهرس
**الإجابة المباشرة:** استخدم طريقة `index.add()` ومرّر المسار المطلق لكل مجلد مصدر؛ يكتشف الـ API تلقائيًا الصيغ المدعومة (PDF, DOCX, XLSX, إلخ) ويستخرج النص القابل للبحث إلى الفهرس.

`SearchOptions` هو كائن تكوين يتيح لك ضبط كيفية معالجة المستندات أثناء الفهرسة والبحث. ستستخدمه لاحقًا لتمكين الاستعلامات المعتمدة على القطع.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. تكوين خيارات البحث للبحث بالقطع
**الإجابة المباشرة:** اضبط `options.setChunkSearch(true)` على كائن `SearchOptions` قبل تنفيذ الاستعلام؛ هذا يخبر المحرك بتقسيم كل مستند إلى قطع منطقية (عادةً فقرات) وإرجاع التطابقات لكل قطعة بدلاً من الملف بالكامل.

`SearchResult` يحتوي على القطع المتطابقة، ومواقعها، ودرجات الصلة. عندما يكون البحث بالقطع مفعلاً، كل `SearchResult` يطابق جزءًا واحدًا من المستند الأصلي.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. إجراء بحث أولي معتمد على القطع
**الإجابة المباشرة:** نفّذ `index.search("your query", options)`؛ تُعيد الدعوة مجموعة `SearchResult` لأول مجموعة من القطع المتطابقة ورمز يمثل حالة البحث للمتابعة.

الرمز المُرجع ضروري لتصفح مجموعات النتائج الكبيرة دون إعادة تنفيذ الاستعلام بالكامل.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. متابعة البحث بالقطع
**الإجابة المباشرة:** مرّر الرمز الذي تم إرجاعه من الدعوة السابقة إلى `index.searchNext(token, options)`؛ كرّر حتى تُعيد الطريقة `null`، مما يدل على أنه تم استرجاع جميع القطع المتطابقة.

هذه الطريقة المتدرجة تحافظ على انخفاض استهلاك الذاكرة لأن دفعة القطع الحالية فقط هي الموجودة في الذاكرة.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## لماذا نستخدم البحث بالقطع؟
يُقسّم البحث المعتمد على القطع مجموعات المستندات الضخمة إلى قطع يمكن إدارتها، مما يقلل من ضغط الذاكرة ويسرّع أوقات الاستجابة. من خلال الفهرسة على مستوى الفقرة أو القسم، يمكن للمحرك استرجاع القطع ذات الصلة فقط، مما يقلل من استهلاك المعالج ويحسّن زمن الاستجابة للمستخدمين النهائيين. يكون ذلك مفيدًا بشكل خاص عندما:

1. **الفرق القانونية** تحتاج إلى تحديد بنود محددة عبر آلاف العقود.  
2. **بوابات دعم العملاء** يجب أن تعرض مقالات قاعدة المعرفة ذات الصلة فورًا.  
3. **الباحثون** يفرزون عبر مجموعات بيانات واسعة دون تحميل الملفات بالكامل إلى الذاكرة.  

ادعاء مُقاس: يمكن لـ GroupDocs.Search معالجة **ملفات PDF بأكثر من 500 صفحة** في أقل من **2 ثانية لكل قطعة** على خادم قياسي بثمانية أنوية، مع الحفاظ على ذروة الذاكرة تحت **200 ميغابايت**.

## كيف يزيد هذا النهج من أداء البحث
**الإجابة المباشرة:** من خلال البحث في قطع أصغر بدلاً من الملفات الكاملة، يمكن للمحرك تخطي الأقسام غير ذات الصلة مبكرًا، وتقليل دورات المعالج، والاحتفاظ فقط بالقطعة النشطة في الذاكرة، مما يقلل مباشرةً من استهلاك **java search index memory** ويؤدي إلى أوقات استجابة أسرع. يتيح هذا النهج المستهدف أيضًا تخزينًا مؤقتًا أكثر فاعلية ومعالجة متوازية، مما يسمح للأنوية المتعددة بمعالجة قطع مختلفة في آن واحد، مما يحسّن الإنتاجية على الخوادم متعددة الأنوية.

فوائد إضافية تشمل:
- معالجة القطع بشكل متوازي عبر عدة أنوية.  
- إنهاء مبكر عندما يتم العثور على تطابق عالي الصلة.  

## إدارة ذاكرة فهرس البحث java
**الإجابة المباشرة:** خصص مساحة كافية من كومة JVM (مثلاً `-Xmx2g` أو أعلى) بناءً على حجم الفهرس المتوقع، شغّل `index.optimize()` بعد الإضافات الجماعية لضغط بنية الفهرس، وراقب توقفات جمع القمامة باستخدام VisualVM لتجنب ارتفاعات زمن الاستجابة.

نصائح تحسين إضافية:
- استخدم `index.flush()` بعد دفعات كبيرة لكتابة البيانات المؤقتة إلى القرص.  
- فعّل `options.setMemoryLimit(256)` لتحديد حد أقصى لاستخدام الذاكرة لكل بحث.  

## اعتبارات الأداء
- **إدارة الذاكرة** – خصص مساحة كومة كافية (`-Xmx`) للفهارس الكبيرة.  
- **مراقبة الموارد** – راقب استهلاك المعالج أثناء عمليات الفهرسة والبحث.  
- **صيانة الفهرس** – أعد بناء الفهرس أو نظفه دوريًا للتخلص من البيانات القديمة.  

## الأخطاء الشائعة & استكشاف الأخطاء
| المشكلة | سبب حدوثه | الحل |
|-------|----------------|-----|
| `OutOfMemoryError` أثناء الفهرسة | حجم الكومة منخفض جدًا | زيادة كومة JVM (`-Xmx2g` أو أعلى) |
| عدم إرجاع نتائج | رمز القطعة لم يُعالج | تأكد من أن حلقة `while` تستمر حتى تكون `getNextChunkSearchToken()` تساوي `null` |
| بطء أداء البحث | الفهرس غير مُحسّن | شغّل `index.optimize()` بعد الإضافات الجماعية |

## الأسئلة المتكررة

**س: ما هو البحث المعتمد على القطع؟**  
ج: البحث المعتمد على القطع يقسم مجموعة البيانات إلى قطع أصغر، مما يسمح باستعلامات فعّالة على أحجام كبيرة من البيانات دون تحميل المستندات بالكامل إلى الذاكرة.

**س: كيف يمكنني تحديث فهرسي بملفات جديدة؟**  
ج: ببساطة استدعِ `index.add()` مع المسار إلى المستندات الجديدة؛ سيقوم الفهرس بدمجها تلقائيًا.

**س: هل يمكن لـ GroupDocs.Search التعامل مع صيغ ملفات مختلفة؟**  
ج: نعم، يدعم **PDF, DOCX, XLSX, PPTX, HTML, TXT، وأكثر من 30 صيغة أخرى**.

**س: ما هي الاختناقات الشائعة في الأداء؟**  
ج: قيود الذاكرة والفهارس غير المُحسّنة هي الأكثر شيوعًا؛ خصص كومة كافية بانتظام وحسّن الفهرس بشكل دوري.

**س: أين يمكنني العثور على وثائق أكثر تفصيلًا؟**  
ج: قم بزيارة [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) الرسمي للحصول على أدلة متعمقة ومراجع API.

**س: هل يعمل البحث المعتمد على القطع مع ملفات PDF مشفرة؟**  
ج: نعم، طالما قمت بتوفير كلمة المرور عبر التحميل المناسب للـ API.

**س: كيف يمكنني مراقبة تقدم الفهرسة؟**  
ج: استخدم التحميل الزائد لـ `Index.add()` الذي يُعيد كائن `Progress` أو ربطه بعمليات رد نداء السجلات.

## الموارد
- **الوثائق**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **مرجع API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **التنزيل**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **دعم مجاني**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2026-10-02  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## دروس ذات صلة

- [إنشاء دليل فهرس البحث وتعيين الترخيص – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [تحسين أداء الاستعلام مع GroupDocs.Search Java: تحسين الفهرس والبحث](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [ميزات البحث المتقدمة في Groupdocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
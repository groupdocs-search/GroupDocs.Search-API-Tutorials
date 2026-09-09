---
date: '2026-08-15'
description: تعرف على كيفية تحسين زمن استجابة البحث باستخدام ميزات الفهرسة المتقدمة
  في GroupDocs.Search لـ Java، بما في ذلك cancellation، async operations، multithreading،
  و metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: تحسين زمن استجابة البحث مع GroupDocs.Search لـ Java باستخدام cancellation،
  asynchronous indexing، multithreading، و metadata customization. زيادة الأداء وتقليل
  استهلاك الموارد.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: تحسين زمن استجابة البحث باستخدام الفهرسة المتقدمة في GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: تحسين زمن استجابة البحث باستخدام الفهرسة المتقدمة في GroupDocs
type: docs
url: /ar/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# تحسين زمن استجابة البحث باستخدام الفهرسة المتقدمة في GroupDocs

في بيئة الرقمية سريعة الوتيرة اليوم، **تحسين زمن استجابة البحث** أمر أساسي لتقديم نتائج فورية للمستخدمين. سواء كنت تبني محرك بحث مخصصًا أو تعزز نظام إدارة مستندات موجود، يمكن لاستراتيجية الفهرسة الصحيحة أن تقلل زمن الاستجابة بشكل كبير، وتخفض استهلاك الموارد، وتُحسّن **تحسين زمن استجابة البحث** عبر جميع الجوانب. في هذا البرنامج التعليمي سنستعرض أقوى ميزات GroupDocs.Search للغة Java — الإلغاء، الفهرسة غير المتزامنة، تعدد الخيوط، وتخصيص البيانات الوصفية — حتى تتمكن من **إضافة مستندات إلى الفهرس** بشكل أسرع وأكثر كفاءة.

**ما ستتعلمه**

- كيفية إلغاء عملية الفهرسة بعد وقت محدد  
- إجراء عمليات الفهرسة غير المتزامنة ومعالجة تغييرات الحالة  
- تكوين تعدد الخيوط لفهرسة أسرع  
- تخصيص خيارات فهرسة البيانات الوصفية لت **تخصيص بيانات البحث الوصفية**  

دعنا نتأكد من أن لديك كل ما تحتاجه قبل أن نغوص في الشيفرة.

## إجابات سريعة
- **ماذا يفعل الإلغاء؟** يتوقف عن الفهرسة بعد انتهاء مهلة محددة، مما يحرّر وحدة المعالجة المركزية والذاكرة للمهام الأخرى.  
- **هل يمكنني فهرسة المستندات بشكل غير متزامن؟** نعم – فعّل ذلك باستخدام `options.setAsync(true)`.  
- **كم عدد الخيوط التي يمكنني استخدامها؟** أي عدد صحيح موجب؛ عادةً 2‑4 خيوط هي المعتادة لمعظم الخوادم.  
- **هل فهرسة البيانات الوصفية اختيارية؟** بالتأكيد – يمكنك تمكينها أو ضبطها بدقة لكل حقل.  
- **هل أحتاج إلى ترخيص لهذه الميزات؟** النسخة التجريبية تعمل للاختبار؛ الترخيص الكامل مطلوب للإنتاج.

## المتطلبات المسبقة

- **مكتبة GroupDocs.Search** – الإصدار 25.4 أو أحدث.  
- **بيئة تطوير Java** – يُنصح بـ JDK 8 أو أعلى.  
- إلمام أساسي بـ Java ومفهوم الفهرسة.

### إعداد GroupDocs.Search للغة Java

#### تثبيت Maven

أضف المستودع والاعتماد إلى ملف `pom.xml` الخاص بك:

`pom.xml` يخبر Maven أي مكوّنات GroupDocs.Search يجب تنزيلها وإدراجها في مشروعك.

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

#### تحميل مباشر

بدلاً من ذلك، قم بتنزيل أحدث ملف JAR من [إصدارات GroupDocs.Search للغة Java](https://releases.groupdocs.com/search/java/).

**الحصول على الترخيص** – ابدأ بنسخة تجريبية مجانية أو اطلب ترخيصًا مؤقتًا لفتح مجموعة الميزات الكاملة.

### التهيئة الأساسية والإعداد

فئة `SearchIndex` هي نقطة الدخول التي تمثل فهرسًا قابلاً للبحث مخزنًا على القرص أو في الذاكرة.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## ما معنى “تحسين أداء البحث” في هذا السياق؟

يعني تحسين أداء البحث ضبط عملية الفهرسة بحيث تستهلك الكمية المناسبة من وحدة المعالجة المركزية والذاكرة والوقت مع تقديم أكثر النتائج صلةً على الفور. من خلال التحكم في الإلغاء، التنفيذ غير المتزامن، تعدد الخيوط، ومعالجة البيانات الوصفية، تؤثر مباشرةً على سرعة قدرة المحرك على **إضافة مستندات إلى الفهرس** والاستجابة للاستعلامات.

## لماذا نستخدم ميزات الفهرسة المتقدمة؟

تحافظ الفهرسة غير المتزامنة وتعدد الخيوط على استجابة تطبيقك، بينما يمنع الإلغاء العمليات المتطرفة. تسمح خيارات البيانات الوصفية المضبوطة بدقة بإظهار أهم المعلومات، مما **يحسن زمن استجابة البحث** للمستخدمين النهائيين مباشرةً. بالإضافة إلى ذلك، تقلل هذه الميزات من ارتفاعات وحدة المعالجة المركزية، وتخفض ضغط الذاكرة، وتتيح توسيعًا أكثر سلاسة عند التعامل مع أحجام مستندات كبيرة.

## كيف تحسن زمن استجابة البحث باستخدام الفهرسة المتقدمة؟

حمّل كائن `SearchIndex` الخاص بك، واضبط `IndexingOptions` مع إعدادات الإلغاء، غير المتزامن، وعدد الخيوط، ثم استدعِ `index.add(document)` — هذا الجمع يقلل من إجمالي وقت الفهرسة بنسبة تصل إلى 60 % في الأحمال النموذجية ويضمن أن الوظائف الطويلة لا تحجب العمليات الأخرى. يمكنك أيضًا تعديل حدود فهرسة البيانات الوصفية ومراقبة التقدم عبر أحداث تغيير الحالة لضمان بقاء خط الأنابيب ضمن ميزانيات الأداء.

## دليل التنفيذ

### خاصية الإلغاء

**نظرة عامة** – إلغاء الفهرسة بعد مدة محددة لتجنب استهلاك الموارد بشكل مفرط.

#### الخطوة 1: إعداد البيئة

أنشئ كائن `SearchIndex` يشير إلى مجلد الفهرس الخاص بك.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: إنشاء خيارات الفهرسة مع الإلغاء

`IndexingOptions` يتيح لك تحديد سلوك محرك الفهرسة.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**نقاط رئيسية**

- `setCancellation()` يفعّل الخاصية.  
- `cancelAfter(int milliseconds)` يحدد المهلة (3 ثوانٍ في هذا المثال).

### خاصية غير المتزامنة

**نظرة عامة** – تشغيل الفهرسة على خيط خلفي والاستماع لتغييرات الحالة.

#### الخطوة 1: إعداد البيئة

أنشئ الفهرس وحضر مجموعة المستندات.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: الاشتراك في حدث تغيير الحالة

حدث `StatusChanged` يُخطرُك عندما ينتقل مهمة الفهرسة بين الحالات.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### الخطوة 3: ضبط خيارات غير المتزامنة

فعّل وضع غير المتزامن بحيث تُعيد الاستدعاء فورًا وتستمر المعالجة في الخلفية.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### خاصية الخيوط

**نظرة عامة** – تسريع الفهرسة باستخدام عدة نوى CPU.

#### الخطوة 1: إعداد البيئة

جهّز الفهرس وتأكد من أن JVM لديها ما يكفي من ذاكرة الكومة.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: ضبط تعدد الخيوط

حدد عدد خيوط العامل؛ كل خيط يعالج جزءًا من المستندات.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### خاصية خيارات فهرسة البيانات الوصفية

**نظرة عامة** – ضبط دقيق للبيانات الوصفية للمستند التي يتم فهرستها وكيفية تخزينها.

#### الخطوة 1: إعداد البيئة

حمّل مستندًا يحتوي على حقول بيانات وصفية مثل المؤلف، العنوان، والوسوم المخصصة.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: ضبط خيارات البيانات الوصفية

`MetadataIndexingOptions` يتيح لك تمكين أو تعطيل حقول البيانات الوصفية الفردية وتحديد حدود الحجم.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## تطبيقات عملية

1. **أنظمة إدارة المستندات** – استخدم الفهرسة غير المتزامنة للحفاظ على استجابة واجهة المستخدم بينما تُعالج الدفعات الكبيرة في الخلفية.  
2. **محركات بحث المحتوى** – طبّق الإلغاء لمنع الوظائف الطويلة من استهلاك موارد الخادم أثناء فترات الذروة.  
3. **خطوط إدخال على نطاق واسع** – استفد من تعدد الخيوط لـ **إضافة مستندات إلى الفهرس** على نطاق واسع، مما يقلل وقت المعالجة بشكل كبير.  

## اعتبارات الأداء

- **إدارة الخيوط** – راقب استخدام وحدة المعالجة المركزية؛ كثرة الخيوط قد تتسبب في عبء تبديل السياق.  
- **بصمة الذاكرة** – حدود البيانات الوصفية (مثل `setMaxBytesToIndexField`) تحافظ على توقع استهلاك الذاكرة.  
- **جمع القمامة** – استخدم علامات JVM المناسبة (`-Xmx`, `-XX:+UseG1GC`) عند فهرسة مجموعات ضخمة.  

## المشكلات الشائعة والحلول

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| الفهرسة لا تنتهي أبداً | تم ضبط الإلغاء منخفضًا جدًا | زيادة قيمة `cancelAfter` أو إزالة الإلغاء للوظائف الطويلة |
| لا توجد تحديثات حالة في وضع غير المتزامن | معالج الحدث غير مرفق بشكل صحيح | تأكد من استدعاء `index.getEvents().StatusChanged.add(...)` قبل `index.add` |
| أخطاء نفاد الذاكرة | عدد كبير جدًا من الخيوط أو حدود بيانات وصفية مرتفعة | قلل `options.setThreads` وخفض حدود حقول البيانات الوصفية |
| البيانات الوصفية مفقودة في النتائج | فهرسة البيانات الوصفية معطلة | تحقق من تكوين `options.getMetadataIndexingOptions()` وعدم ضبطه لتجاهل الحقول |

## الأسئلة المتكررة

**س: كيف أحصل على ترخيص مؤقت لـ GroupDocs.Search؟**  
ج: زر [صفحة الترخيص المؤقت لـ GroupDocs](https://purchase.groupdocs.com/temporary-license/) واتبع التعليمات على الشاشة.

**س: هل يمكنني إلغاء عملية الفهرسة في منتصفها؟**  
ج: نعم – استخدم خاصية الإلغاء مع `cancelAfter()` أو استدعِ `Cancellation.cancel()` برمجيًا.

**س: ما هي بعض حالات الاستخدام للفهرسة غير المتزامنة؟**  
ج: استرجاع المستندات في الوقت الحقيقي، معالجة الدفعات في الخلفية، وتطبيقات ذات واجهة مستخدم سريعة الاستجابة تستفيد من الفهرسة غير المتزامنة.

**س: هل من الآمن زيادة عدد الخيوط على خادم مشترك؟**  
ج: زد العدد تدريجيًا وراقب حمل وحدة المعالجة المركزية؛ في البيئات المشتركة بشكل كبير، حافظ على عدد الخيوط معتدلًا (2‑4).

**س: كيف تؤثر فهرسة البيانات الوصفية على صلة البحث؟**  
ج: يمكن أن تُعطى البيانات الوصفية المفهرسة بشكل صحيح (المؤلف، تاريخ الإنشاء، الوسوم) وزنًا أعلى في الاستعلامات، مما يحسن دقة النتائج.

## الخلاصة

من خلال تبني هذه الميزات المتقدمة لـ GroupDocs.Search للغة Java، سـ **تحسن زمن استجابة البحث** عبر مجموعة متنوعة من السيناريوهات — من استيعاب المستندات بسرعة إلى التحكم الدقيق في البيانات الوصفية. جرّب تكوينات مختلفة، راقب استهلاك الموارد، وصمّم الإعدادات وفقًا لحجم عملك المحدد للحصول على أفضل النتائج.

---

**Last Updated:** 2026-08-15  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## دروس ذات صلة

- [تحسين أداء الاستعلام مع GroupDocs.Search Java: تحسين الفهرس والبحث](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [كيفية إضافة مستندات إلى الفهرس باستخدام فهرسة البيانات الوصفية في Java باستخدام GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [كيفية إضافة عدة أسماء مستعارة وإضافة مستندات إلى الفهرس في GroupDocs.Search للغة Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
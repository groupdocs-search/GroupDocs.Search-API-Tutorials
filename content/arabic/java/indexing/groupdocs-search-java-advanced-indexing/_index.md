---
date: '2025-12-29'
description: تعرّف على كيفية تحسين أداء البحث باستخدام ميزات الفهرسة المتقدمة في GroupDocs.Search
  للغة Java، بما في ذلك الإلغاء، والعمليات غير المتزامنة، وتعدد الخيوط، وتخصيص البيانات
  الوصفية.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: تحسين أداء البحث باستخدام تقنيات الفهرسة المتقدمة في GroupDocs.Search للغة
  Java
type: docs
url: /ar/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# تحسين أداء البحث باستخدام تقنيات الفهرسة المتقدمة في GroupDocs.Search للغة Java

في بيئة رقمية سريعة الوتيرة اليوم، **تحسين أداء البحث** أمر أساسي لتقديم نتائج فورية للمستخدمين. سواء كنت تبني محرك بحث مخصصًا أو تعزز نظام إدارة مستندات موجود، فإن استراتيجية الفهرسة الصحيحة يمكن أن تقلل بشكل كبير من زمن الاستجابة واستهلاك الموارد. في هذا البرنامج التعليمي سنستعرض أقوى ميزات GroupDocs.Search للغة Java — الإلغاء، الفهرسة غير المتزامنة، المعالجة المتعددة الخيوط، وتخصيص الفهرسة الوصفية — حتى تتمكن من **إضافة فهرس المستندات** بسرعة وكفاءة أكبر.

**ما ستتعلمه**

- كيفية إلغاء عملية الفهرسة بعد مدة محددة  
- تنفيذ عمليات الفهرسة غير المتزامنة ومعالجة تغيّر الحالة  
- تكوين المعالجة المتعددة الخيوط لفهرسة أسرع  
- تخصيص خيارات فهرسة البيانات الوصفية  

لنتأكد من أن لديك كل ما تحتاجه قبل الغوص في الشيفرة.

## المتطلبات المسبقة

- **مكتبة GroupDocs.Search** – الإصدار 25.4 أو أحدث.  
- **بيئة تطوير Java** – يُنصح باستخدام JDK 8 أو أعلى.  
- إلمام أساسي بـ Java ومفهوم الفهرسة.

### إعداد GroupDocs.Search للغة Java

#### تثبيت عبر Maven

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

بدلاً من ذلك، حمّل أحدث ملف JAR من [إصدارات GroupDocs.Search للغة Java](https://releases.groupdocs.com/search/java/).

**الحصول على الترخيص** – ابدأ بنسخة تجريبية مجانية أو اطلب ترخيصًا مؤقتًا لفتح مجموعة الميزات الكاملة.

### التهيئة الأساسية والإعداد

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

## إجابات سريعة
- **ماذا يفعل الإلغاء؟** يوقف الفهرسة بعد وقت محدد لتوفير الموارد.  
- **هل يمكنني فهرسة المستندات بشكل غير متزامن؟** نعم – اضبط `options.setAsync(true)`.  
- **كم عدد الخيوط التي يمكنني استخدامها؟** أي عدد صحيح موجب؛ القيم النموذجية هي 2‑4 لمعظم الخوادم.  
- **هل فهرسة البيانات الوصفية اختيارية؟** بالتأكيد – يمكنك تمكينها أو ضبطها حسب كل حقل.  
- **هل أحتاج إلى ترخيص لهذه الميزات؟** النسخة التجريبية تكفي للاختبار؛ الترخيص الكامل مطلوب للإنتاج.

## ما معنى “تحسين أداء البحث” في هذا السياق؟

تحسين أداء البحث يعني تكوين عملية الفهرسة بحيث تستهلك الكمية المناسبة من وحدة المعالجة المركزية والذاكرة والوقت مع تقديم أكثر النتائج صلةً على الفور. من خلال التحكم في الإلغاء، التنفيذ غير المتزامن، المعالجة المتعددة الخيوط، ومعالجة البيانات الوصفية، تؤثر مباشرةً على سرعة قدرة المحرك على **إضافة فهرس المستندات** والاستجابة للاستعلامات.

## لماذا نستخدم ميزات الفهرسة المتقدمة؟

- **تقليل زمن الاستجابة** – الفهرسة غير المتزامنة والمتعددة الخيوط تحافظ على استجابة تطبيقك.  
- **إدارة موارد أفضل** – الإلغاء يمنع العمليات التي تستهلك الموارد بشكل مفرط.  
- **تحسين صلة البحث** – خيارات البيانات الوصفية تتيح لك إبراز أهم المعلومات.

## دليل التنفيذ

### خاصية الإلغاء

**نظرة عامة** – إلغاء الفهرسة بعد مدة محددة لتجنب استهلاك مفرط للموارد.

#### الخطوة 1: إعداد البيئة

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: إنشاء خيارات الفهرسة مع الإلغاء

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

- `setCancellation()` يفعّل الميزة.  
- `cancelAfter(int milliseconds)` يحدد مهلة الإلغاء (3 ثوانٍ في هذا المثال).

### خاصية الفهرسة غير المتزامنة

**نظرة عامة** – تشغيل الفهرسة في خيط خلفي والاستماع لتغيّر الحالة.

#### الخطوة 1: إعداد البيئة

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: الاشتراك في حدث تغيّر الحالة

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

#### الخطوة 3: تكوين خيارات الفهرسة غير المتزامنة

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### خاصية الخيوط

**نظرة عامة** – تسريع الفهرسة عبر الاستفادة من عدة نوى للمعالج.

#### الخطوة 1: إعداد البيئة

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: تكوين المعالجة المتعددة الخيوط

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### خاصية خيارات فهرسة البيانات الوصفية

**نظرة عامة** – ضبط أي من بيانات المستند الوصفية تُفهرس وكيفية تخزينها.

#### الخطوة 1: إعداد البيئة

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: تكوين خيارات البيانات الوصفية

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

1. **أنظمة إدارة المستندات** – استخدم الفهرسة غير المتزامنة للحفاظ على استجابة واجهة المستخدم أثناء معالجة دفعات كبيرة في الخلفية.  
2. **محركات البحث المحتوى** – طبّق الإلغاء لمنع الوظائف طويلة الأمد من استهلاك موارد الخادم خلال فترات الذروة.  
3. **خطوط أنابيب الإدخال على نطاق واسع** – استفد من المعالجة المتعددة الخيوط لـ **إضافة فهرس المستندات** على نطاق واسع، مما يقلل وقت المعالجة بشكل كبير.

## اعتبارات الأداء

- **إدارة الخيوط** – راقب استهلاك وحدة المعالجة؛ عدد كبير جدًا من الخيوط قد يسبب عبءً إضافيًا بسبب تبديل السياق.  
- **بصمة الذاكرة** – حدود البيانات الوصفية (مثل `setMaxBytesToIndexField`) تساعد في الحفاظ على استهلاك الذاكرة بشكل متوقع.  
- **جمع القمامة** – استخدم إعدادات JVM المناسبة (`-Xmx`, `-XX:+UseG1GC`) عند فهرسة مجموعات ضخمة من النصوص.

## المشكلات الشائعة والحلول

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| الفهرسة لا تنتهي أبدًا | تم ضبط الإلغاء بقيمة منخفضة جدًا | زد قيمة `cancelAfter` أو أزل الإلغاء للوظائف الطويلة |
| لا توجد تحديثات حالة في الوضع غير المتزامن | لم يتم ربط معالج الحدث بشكل صحيح | تأكد من استدعاء `index.getEvents().StatusChanged.add(...)` قبل `index.add` |
| أخطاء نفاد الذاكرة | عدد كبير من الخيوط أو حدود بيانات وصفية مرتفعة | قلل `options.setThreads` وخفض حدود حقول البيانات الوصفية |
| فقدان البيانات الوصفية في النتائج | تم تعطيل فهرسة البيانات الوصفية | تحقق من تكوين `options.getMetadataIndexingOptions()` وعدم تعيينه لتجاهل الحقول |

## الأسئلة المتكررة

**س: كيف أحصل على ترخيص مؤقت لـ GroupDocs.Search؟**  
ج: زر [صفحة الترخيص المؤقت لـ GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**س: هل يمكنني إلغاء عملية الفهرسة في منتصفها؟**  
ج: نعم – استخدم خاصية الإلغاء مع `cancelAfter()` أو استدعِ `Cancellation.cancel()` برمجيًا.

**س: ما هي بعض حالات الاستخدام للفهرسة غير المتزامنة؟**  
ج: الاسترجاع الفوري للمستندات، معالجة الدُفعات في الخلفية، وتطبيقات ذات واجهة مستخدم سريعة الاستجابة تستفيد من الفهرسة غير المتزامنة.

**س: هل من الآمن زيادة عدد الخيوط على خادم مشترك؟**  
ج: زد العدد تدريجيًا وراقب حمل المعالج؛ في البيئات المشتركة بشكل كبير، حافظ على عدد الخيوط معتدلًا (2‑4).

**س: كيف تؤثر فهرسة البيانات الوصفية على صلة البحث؟**  
ج: البيانات الوصفية المفهرسة بشكل صحيح (مثل المؤلف، تاريخ الإنشاء، العلامات) يمكن أن تُعطى وزنًا أعلى في الاستعلامات، مما يحسن دقة النتائج.

## الخلاصة

من خلال تبني هذه الميزات المتقدمة في GroupDocs.Search للغة Java، ستتمكن من **تحسين أداء البحث** عبر مجموعة متنوعة من السيناريوهات — من إدخال المستندات بسرعة إلى التحكم الدقيق في البيانات الوصفية. جرّب تكوينات مختلفة، راقب استخدام الموارد، واضبط الإعدادات وفقًا لحجم عملك للحصول على أفضل النتائج.

---

**آخر تحديث:** 2025-12-29  
**تم الاختبار مع:** GroupDocs.Search 25.4 للغة Java  
**المؤلف:** GroupDocs  

---
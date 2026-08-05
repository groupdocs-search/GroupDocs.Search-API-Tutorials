---
date: '2026-03-01'
description: تعرّف على كيفية تحسين أداء البحث وتقليل زمن استجابة البحث باستخدام ميزات
  الفهرسة المتقدمة في GroupDocs.Search للغة Java، بما في ذلك الإلغاء، والعمليات غير
  المتزامنة، وتعدد الخيوط، وتخصيص البيانات الوصفية.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: تحسين أداء البحث باستخدام تقنيات الفهرسة المتقدمة في GroupDocs.Search لجافا
type: docs
url: /ar/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# تحسين أداء البحث باستخدام تقنيات الفهرسة المتقدمة في GroupDocs.Search للغة Java

في بيئة الرقمية السريعة اليوم، **تحسين أداء البحث** أمر أساسي لتقديم نتائج فورية للمستخدمين. سواء كنت تبني محرك بحث مخصصًا أو تحسن نظام إدارة مستندات موجود، فإن استراتيجية الفهرسة الصحيحة يمكنها تقليل الكمون بشكل كبير، وخفض استهلاك الموارد، و**تحسين زمن استجابة البحث** عبر جميع الجوانب. في هذا البرنامج التعليمي سنستعرض أقوى ميزات GroupDocs.Search للغة Java — الإلغاء، الفهرسة غير المتزامنة، المعالجة المتعددة الخيوط، وتخصيص البيانات الوصفية — حتى تتمكن من **إضافة فهرس المستندات** بسرعة وكفاءة أكبر.

**ما ستتعلمه**

- كيفية إلغاء عملية الفهرسة بعد وقت محدد  
- إجراء عمليات الفهرسة غير المتزامنة ومعالجة تغيّر الحالة  
- تهيئة المعالجة المتعددة الخيوط لتسريع الفهرسة  
- تخصيص خيارات فهرسة البيانات الوصفية  

دعنا نتأكد من أن لديك كل ما تحتاجه قبل الغوص في الشيفرة.

## المتطلبات المسبقة

- **مكتبة GroupDocs.Search** – الإصدار 25.4 أو أحدث.  
- **بيئة تطوير Java** – يُنصح بـ JDK 8 أو أعلى.  
- إلمام أساسي بـ Java ومفهوم الفهرسة.

### إعداد GroupDocs.Search للغة Java

#### تثبيت Maven

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

بدلاً من ذلك، قم بتحميل أحدث ملف JAR من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**الحصول على الترخيص** – ابدأ بتجربة مجانية أو اطلب ترخيصًا مؤقتًا لفتح مجموعة الميزات الكاملة.

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
- **هل فهرسة البيانات الوصفية اختيارية؟** بالتأكيد – يمكنك تمكينها أو ضبطها بدقة لكل حقل.  
- **هل أحتاج إلى ترخيص لهذه الميزات؟** التجربة تعمل للاختبار؛ يلزم ترخيص كامل للإنتاج.

## ما هو “تحسين أداء البحث” في هذا السياق؟

يعني تحسين أداء البحث ضبط عملية الفهرسة بحيث تستهلك الكمية المناسبة من وحدة المعالجة المركزية والذاكرة والوقت مع تقديم أكثر النتائج صلةً على الفور. من خلال التحكم في الإلغاء، التنفيذ غير المتزامن، الخيوط، ومعالجة البيانات الوصفية، تؤثر مباشرةً على سرعة قدرة المحرك على **إضافة فهرس المستندات** والاستجابة للاستعلامات.

## لماذا نستخدم ميزات الفهرسة المتقدمة؟

- **تقليل الكمون** – الفهرسة غير المتزامنة والمتعددة الخيوط تحافظ على استجابة تطبيقك.  
- **إدارة موارد أفضل** – الإلغاء يمنع العمليات المتجاوزة.  
- **ملاءمة بحث مخصصة** – خيارات البيانات الوصفية تتيح لك إظهار أهم المعلومات.  

## كيف تحسن زمن استجابة البحث باستخدام الفهرسة المتقدمة؟

عندما تحتاج إلى **تحسين زمن استجابة البحث**، فكر في دمج الميزات التي سنستكشفها: إلغاء الوظائف الطويلة، تشغيل الفهرسة في الخلفية، وتوزيع العمل عبر عدة نوى للمعالج. هذا النهج المتعدد الجوانب غالبًا ما يحقق أكبر تحسين في السرعة.

## دليل التنفيذ

### خاصية الإلغاء

**نظرة عامة** – إلغاء الفهرسة بعد مدة محددة لتجنب الاستهلاك المفرط للموارد.

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

### خاصية غير المتزامنة

**نظرة عامة** – تشغيل الفهرسة على خيط خلفي والاستماع لتغيّر الحالة.

#### الخطوة 1: إعداد البيئة

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### الخطوة 2: الاشتراك في حدث تغيير الحالة

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

#### الخطوة 3: تكوين الخيارات غير المتزامنة

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### خاصية الخيوط

**نظرة عامة** – تسريع الفهرسة باستخدام عدة نوى للمعالج.

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

**نظرة عامة** – ضبط دقيق للبيانات الوصفية التي يتم فهرستها وكيفية تخزينها.

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
2. **محركات بحث المحتوى** – طبق الإلغاء لمنع الوظائف الطويلة من استهلاك موارد الخادم خلال فترات الذروة.  
3. **خطوط إدخال البيانات على نطاق واسع** – استفد من المعالجة المتعددة الخيوط لـ **إضافة فهرس المستندات** على نطاق واسع، مما يقلل وقت المعالجة بشكل كبير.

## اعتبارات الأداء

- **إدارة الخيوط** – راقب استخدام المعالج؛ كثرة الخيوط قد تسبب عبء تبديل السياق.  
- **بصمة الذاكرة** – حدود البيانات الوصفية (مثل `setMaxBytesToIndexField`) تساعد في الحفاظ على استهلاك الذاكرة متوقعًا.  
- **جمع القمامة** – استخدم أعلام JVM المناسبة (`-Xmx`, `-XX:+UseG1GC`) عند فهرسة مجموعات نصية ضخمة.

## المشكلات الشائعة والحلول

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| الفهرسة لا تنتهي أبداً | تم ضبط الإلغاء منخفضًا جدًا | زيادة قيمة `cancelAfter` أو إزالة الإلغاء للوظائف الطويلة |
| لا توجد تحديثات حالة في الوضع غير المتزامن | معالج الحدث غير مرفق بشكل صحيح | تأكد من استدعاء `index.getEvents().StatusChanged.add(...)` قبل `index.add` |
| أخطاء نفاد الذاكرة | عدد كبير من الخيوط أو حدود بيانات وصفية مرتفعة | قلل `options.setThreads` وخفض حدود حقول البيانات الوصفية |
| البيانات الوصفية مفقودة في النتائج | فهرسة البيانات الوصفية معطلة | تحقق من تكوين `options.getMetadataIndexingOptions()` وعدم ضبطه لتجاهل الحقول |

## الأسئلة المتكررة

**س: كيف أحصل على ترخيص مؤقت لـ GroupDocs.Search؟**  
ج: زر [صفحة الترخيص المؤقت لـ GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**س: هل يمكنني إلغاء عملية الفهرسة في منتصفها؟**  
ج: نعم – استخدم خاصية الإلغاء مع `cancelAfter()` أو استدعِ `Cancellation.cancel()` برمجيًا.

**س: ما هي بعض حالات الاستخدام للفهرسة غير المتزامنة؟**  
ج: الاسترجاع الفوري للمستندات، معالجة الدُفعات في الخلفية، وتطبيقات ذات واجهة مستخدم سريعة الاستجابة تستفيد من الفهرسة غير المتزامنة.

**س: هل من الآمن زيادة عدد الخيوط على خادم مشترك؟**  
ج: زد العدد تدريجيًا وراقب حمل المعالج؛ في البيئات المشتركة بشكل كبير، حافظ على عدد خيوط معتدل (2‑4).

**س: كيف تؤثر فهرسة البيانات الوصفية على ملاءمة البحث؟**  
ج: البيانات الوصفية المفهرسة بشكل صحيح (المؤلف، تاريخ الإنشاء، الوسوم) يمكن أن تُعطى وزنًا أعلى في الاستعلامات، مما يحسن دقة النتائج.

## الخلاصة

من خلال تبني هذه الميزات المتقدمة في GroupDocs.Search للغة Java، ستقوم **بتحسين أداء البحث** عبر مجموعة متنوعة من السيناريوهات — من إدخال المستندات بسرعة إلى التحكم الدقيق في البيانات الوصفية. جرب إعدادات مختلفة، راقب استهلاك الموارد، واضبط الإعدادات وفقًا لحجم عملك المحدد للحصول على أفضل النتائج.

---

**آخر تحديث:** 2026-03-01  
**تم الاختبار مع:** GroupDocs.Search 25.4 للغة Java  
**المؤلف:** GroupDocs
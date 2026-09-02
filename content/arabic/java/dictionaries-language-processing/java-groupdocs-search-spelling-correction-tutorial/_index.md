---
date: '2026-09-02'
description: تعلم كيفية إنشاء search index java وتمكين تصحيح الإملاء باستخدام GroupDocs.Search.
  اتبع التعليمات خطوة بخطوة لإضافة المستندات، وتكوين max mistake count، وتحسين search
  accuracy.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: تعلم كيفية إنشاء search index java وتمكين تصحيح الإملاء باستخدام GroupDocs.Search.
  اتبع التعليمات خطوة بخطوة لإضافة المستندات، وتكوين max mistake count، وتحسين search
  accuracy.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: كيفية إنشاء search index java وتمكين التدقيق الإملائي
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: كيفية إنشاء search index java وتمكين التدقيق الإملائي
type: docs
url: /ar/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# كيفية إنشاء فهرس بحث Java وتمكين التصحيح الإملائي

في تطبيقات Java الحديثة، تقديم نتائج بحث دقيقة هو ميزة أساسية. يُظهر هذا البرنامج التعليمي **كيفية إنشاء فهرس بحث Java** وتفعيل التصحيح الإملائي باستخدام GroupDocs.Search، بحيث يحصل المستخدمون على نتائج ذات صلة حتى عندما يخطئون في كتابة الاستعلامات. سترى كيفية إعداد المكتبة، إضافة المستندات، تكوين الحد الأقصى لعدد الأخطاء، وتشغيل بحث يتحمل الأخطاء الإملائية — كل ذلك دون كتابة سطر واحد من كود التكوين الإضافي.

## إجابات سريعة
- **ماذا يفعل “تمكين التصحيح الإملائي”?** يقوم بتنشيط مدقق الإملاء المدمج الذي يعيد كتابة المصطلحات المكتوبة خطأً إلى أقرب صيغ صحيحة أثناء البحث.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Search for Java.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتقييم؛ يتطلب الاستخدام في الإنتاج ترخيصًا كاملاً.  
- **هل يمكنني التحكم في مستوى التحمل؟** نعم – استخدم `setMaxMistakeCount` لتحديد عدد الأخطاء المسموح بها لكل استعلام.  
- **هل هو مناسب للفهارس الكبيرة؟** بالطبع – يتعامل المحرك مع فهارس تحتوي على ملايين السجلات مع الحفاظ على زمن استجابة الاستعلام أقل من 100 مللي ثانية على عتاد الخادم المعتاد.

## ما هو GroupDocs.Search؟
GroupDocs.Search هي مكتبة Java توفر فهرسة نصية كاملة سريعة وميزات بحث متقدمة، بما في ذلك التصحيح الإملائي المدمج. تدعم أكثر من 50 تنسيق إدخال ويمكنها معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة.

## لماذا تمكين التصحيح الإملائي في تطبيقات Java؟
- **يعزز رضا المستخدم** – يحصل الزوار على نتائج صحيحة حتى مع كتابة غير مثالية.  
- **يقلل معدلات الارتداد** – النتائج الدقيقة تبقي المستخدمين متفاعلين لفترة أطول.  
- **يعمل عبر المجالات** – من كتالوجات المكتبات إلى بحث منتجات التجارة الإلكترونية، تحسين الإملاء يعزز الصلة في كل مكان.

## المتطلبات المسبقة
- Java Development Kit (JDK) مثبت.  
- معرفة أساسية بـ Java و Maven.  
- فهم مفاهيم الفهرسة.  
- نسخة تجريبية أو مفتاح مرخص من GroupDocs.Search.

### إعداد GroupDocs.Search لـ Java
دمج المكتبة في مشروع Maven الخاص بك.

**إعداد Maven**  
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

**تحميل مباشر**  
بدلاً من ذلك، قم بتحميل أحدث نسخة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
احصل على ترخيص تجريبي مجاني للتقييم. للاستخدام في الإنتاج، اشترِ ترخيصًا كاملاً أو اطلب مفتاحًا مؤقتًا من الموقع الرسمي.

## كيف يمكنني إنشاء فهرس بحث في Java؟
`SearchIndex` هي الفئة الأساسية التي تمثل فهرسًا قابلًا للبحث مخزنًا على القرص.  
أنشئ كائن `SearchIndex` يشير إلى مجلد على القرص، ثم أضف المستندات من دليل المصدر. يبني المحرك فهرسًا معكوسًا يتيح عمليات بحث سريعة. يمكنك استدعاء `index.add()` لكل ملف؛ تقوم المكتبة باستخراج النص تلقائيًا بناءً على نوع الملف.

## كيف يمكنني تمكين التصحيح الإملائي؟
`getSpellingOptions()` تُعيد كائن تكوين الإملاء للفهرس، مما يتيح لك تمكين أو تعديل ميزات تدقيق الإملاء.  
قم بتمكين الإملاء عن طريق استدعاء `index.getSpellingOptions().setEnabled(true)`. هذا يخبر المحرك بتحليل مصطلحات الاستعلام واقتراح بدائل مصححة عند اكتشاف عدم تطابق. الميزة تعمل مباشرةً لجميع اللغات المفهرسة التي تدعمها المكتبة.

## ما هو إعداد الحد الأقصى لعدد الأخطاء؟
`setMaxMistakeCount` يضبط الحد الأقصى لعدد التعديلات على الأحرف التي سيتحملها مدقق الإملاء لكل مصطلح.  
`setMaxMistakeCount(int)` يحدد الحد الأقصى لعدد تعديلات الأحرف (إدراجات، حذف، استبدالات) التي سيتحملها مدقق الإملاء لكل مصطلح. ضبطه على **2** يسمح للمحرك بإصلاح الأخطاء الشائعة ذات الحرفين مع تجنب التصحيحات المفرطة التي قد تُعيد نتائج غير ذات صلة.

## كيفية إجراء بحث مصحح إملائيًا
`search()` ينفّذ استعلامًا ضد الفهرس ويعيد كائن `SearchResult` يحتوي على التطابقات وأية مصطلحات مصححة.  
قم بتشغيل استعلام بحث باستخدام طريقة `search()`. إذا كان الاستعلام يحتوي على كلمات مكتوبة خطأً، سيعيد المحرك `SearchResult` يتضمن المصطلحات المصححة وقائمة بأكثر المستندات صلة. يمكنك عرض كل من الاستعلام الأصلي والإصدار المصحح للمستخدم للشفافية.  
`SearchResult` يحتفظ بقائمة المستندات المتطابقة ومعلومات حول تصحيحات الاستعلام.

## تطبيقات عملية
1. **أنظمة المكتبة** – تصحيح عناوين الكتب أو أسماء المؤلفين المكتوبة خطأً تلقائيًا.  
2. **منصات التجارة الإلكترونية** – تصحيح الأخطاء في أسماء المنتجات لزيادة معدلات التحويل.  
3. **إدارة المحتوى** – مساعدة فريق التحرير في العثور على المقالات حتى مع كلمات مفتاحية غير مثالية.

## اعتبارات الأداء
- **حافظ على تحديث الفهرس** – أعد فهرسة الملفات الجديدة أو المعدلة بانتظام.  
- **ضبط إعدادات ذاكرة JVM** – خصص مساحة كافية من الذاكرة للفهارس الكبيرة (مثال: `-Xmx4g`).  
- **راقب استخدام الموارد** – عدّل إعدادات جامع القمامة إذا لاحظت توقفات أثناء الفهرسة الضخمة.

## المشكلات الشائعة & استكشاف الأخطاء
| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| لا توجد نتائج بعد تمكين التصحيح الإملائي | مسار مجلد الفهرس غير صحيح أو فارغ | تحقق من أن `indexFolder` يشير إلى فهرس صالح وأن `index.add()` نجح |
| مدقق الإملاء لا يصحح الأخطاء الواضحة | `setMaxMistakeCount` مضبوط منخفضًا جدًا | زد العدد إلى 2 أو 3 لتصحيح أكثر تسامحًا |
| التطبيق يتعطل عند مجموعات مستندات كبيرة | ذاكرة JVM غير كافية | زد خيار `-Xmx` (مثال: `-Xmx4g`) |

## الأسئلة المتكررة

**Q: ما هو GroupDocs.Search?**  
A: GroupDocs.Search هي مكتبة Java توفر فهرسة سريعة، قدرات استعلام متقدمة، وتصحيح إملائي مدمج لأي تطبيق Java.

**Q: كيف أحصل على ترخيص لـ GroupDocs.Search?**  
A: قم بزيارة الموقع الرسمي لتنزيل نسخة تجريبية مجانية أو شراء ترخيص كامل؛ كما يتوفر مفتاح مؤقت للاختبار قصير المدى.

**Q: هل يمكنني دمج GroupDocs.Search مع أطر Java أخرى؟**  
A: نعم، يعمل بسلاسة مع Spring و Jakarta EE وأي تطبيق Java قياسي.

**Q: ما هي المشكلات الشائعة عند إعداد فهرس؟**  
A: مسارات المجلد غير الصحيحة، أذونات الملفات المفقودة، أو عدم وجود تبعيات Maven هي الأسباب الشائعة.

**Q: كيف يحسن التصحيح الإملائي نتائج البحث؟**  
A: يقوم تلقائيًا بإعادة كتابة الاستعلامات المكتوبة خطأً إلى أقرب مصطلحات صحيحة، مما يُعيد نتائج أكثر صلة ويقلل من إحباط المستخدم.

## موارد إضافية
- [الوثائق](https://docs.groupdocs.com/search/java/)
- [مرجع API](https://reference.groupdocs.com/search/java)
- [تحميل](https://releases.groupdocs.com/search/java/)
- [مستودع GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-09-02  
**تم الاختبار مع:** GroupDocs.Search 25.4  
**المؤلف:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## الدروس ذات الصلة

- [كيفية إنشاء فهرس مستند وإضافة مستندات باستخدام واجهة GroupDocs.Search API لـ Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [معالجة اللغة Java – إنشاء قاموس مرادفات باستخدام GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [كلمات التوقف في البحث: إضافة مستندات إلى الفهرس باستخدام GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
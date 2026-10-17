---
date: '2026-10-17'
description: تعلم كيفية استخدام المرادفات في Java مع GroupDocs.Search، استيراد قواميس
  المرادفات، إدارة مجموعات المرادفات، وتحسين فهرس البحث للحصول على صلة أفضل.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: تعلم كيفية استخدام المرادفات في Java مع GroupDocs.Search، استيراد
  قواميس المرادفات، إدارة مجموعات المرادفات، وتحسين فهرس البحث للحصول على صلة أفضل.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: كيفية استخدام المرادفات في Java مع GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: كيفية استخدام المرادفات في Java مع GroupDocs.Search
type: docs
url: /ar/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام المرادفات في Java مع GroupDocs.Search

## إجابات سريعة
- **ما هي الخطوة الأولى لإضافة المرادفات؟** إنشاء مثيل `Index` والعمل مع واجهة برمجة تطبيقات `SynonymDictionary`.  
- **هل يمكنني استيراد قاموس مرادفات جاهز؟** نعم – استدعِ `importDictionary(path)` مع موقع الملف.  
- **كيف يمكنني تفعيل البحث المدعم بالمرادفات؟** فعّل `SearchOptions.setUseSynonymSearch(true)`.  
- **هل يمكن تعديل مجموعات المرادفات أثناء التشغيل؟** بالتأكيد – يمكنك مسح، إضافة، أو استرجاع المجموعات عبر واجهة برمجة تطبيقات القاموس.  
- **ما الذي يجب مراقبته عند توسيع الفهرس؟** احذف بانتظام الإدخالات غير المستخدمة واضبط مساحة الذاكرة JVM للملفات الكبيرة للمرادفات.

## ما هو البحث بالمرادفات؟
**Search with synonyms** يعني أن المحرك يتعامل مع مجموعة من الكلمات أو العبارات كبدائل بعضها لبعض. عندما يكتب المستخدم **“better”**، يبحث المحرك أيضًا عن **“improve”**, **“enhance”**, أو أي مصطلح آخر قمت بتعريفه في نفس مجموعة المرادفات، مما يقدم نتائج أغنى دون تغيير استعلام المستخدم.

## لماذا تمكين دعم المرادفات في GroupDocs.Search؟
تمكين دعم المرادفات يسمح للمحرك بتوسيع الاستعلامات تلقائيًا لتشمل المصطلحات المكافئة، مما يحسن صلة النتائج، يزيد من رضا المستخدم، ويمكن أن يرفع معدلات التحويل للمواقع التجارية أو المواقع القائمة على المحتوى. كما أنه يركز إدارة المصطلحات، مما يقلل من عبء الصيانة عبر تطبيقات متعددة.

## المتطلبات المسبقة
- نسخة GroupDocs.Search for Java **25.4** أو أحدث.  
- بيئة تطوير Java (IntelliJ IDEA، Eclipse، إلخ) مع دعم Maven.  
- معرفة أساسية بـ Java وإلمام بهيكل مشروع Maven.

### المكتبات المطلوبة والإصدارات
- GroupDocs.Search for Java **25.4** أو أعلى.

### إعداد البيئة
- بيئة التطوير التي تختارها (IntelliJ IDEA، Eclipse، إلخ).  
- Maven لإدارة التبعيات.

### متطلبات المعرفة
- برمجة كائنية التوجه في Java.  
- عمليات الإدخال/الإخراج الأساسية للملفات.

## إعداد GroupDocs.Search للـ Java

### معلومات التثبيت
Add the repository and dependency to your `pom.xml`:

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

**تحميل مباشر** – يمكنك أيضًا تحميل أحدث JAR من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **تجربة مجانية:** اختبار الميزات الأساسية دون ترخيص.  
- **ترخيص مؤقت:** توسيع قدرات التجربة أثناء التقييم.  
- **شراء:** مطلوب للاستخدام في الإنتاج وللحصول على مجموعة الميزات الكاملة.

#### التهيئة الأساسية والإعداد
Create an `Index` instance, then add documents to be searchable:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## كيفية إضافة المرادفات إلى فهرس البحث الخاص بك

### الميزة 1: إنشاء وفهرسة الفهرس
فئة `Index` تمثل مجموعة قابلة للبحث من المستندات المخزنة على القرص أو في الذاكرة.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### الميزة 2: استرجاع المرادفات لكلمة
`SynonymDictionary` تدير مجموعات المرادفات وتوفر طرقًا لاستعلام المرادفات لمصطلح.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### الميزة 3: استرجاع مجموعات المرادفات
`SynonymDictionary.getGroups()` تُرجع قائمة بجميع مجموعات المرادفات المعرفة مع معرّفاتها.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### الميزة 4: إدارة إدخالات قاموس المرادفات
`add(word, synonym)` يضيف علاقة مرادفة جديدة إلى القاموس. `clear()` يزيل جميع الإدخالات، و `remove(word)` يحذف مصطلحًا محددًا من القاموس.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### الميزة 5: تصدير المرادفات إلى ملف
`exportDictionary(path)` يكتب قاموس المرادفات الحالي إلى ملف .dat ثنائي في الموقع المحدد.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### الميزة 6: استيراد المرادفات من ملف
`importDictionary(path)` يحمل ملف .dat الذي تم تصديره مسبقًا إلى قاموس المرادفات.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### الميزة 7: إجراء بحث مدعم بالمرادفات
`SearchOptions` يضبط سلوك الاستعلام، بما في ذلك ما إذا كان توسيع المرادفات مفعلاً. `setUseSynonymSearch(true)` يفعّل البحث المدعم بالمرادفات للاستعلام القادم.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## كيفية البحث بالمرادفات
حمّل `Index` الخاص بك، فعّل البحث بالمرادفات، ونفّذ استعلامًا. يقوم المحرك تلقائيًا بتوسيع الاستعلام باستخدام قاموس المرادفات الذي أنشأته أو استوردته، ويعيد المطابقات لجميع المصطلحات ذات الصلة.

## كيفية استيراد قاموس المرادفات
إذا كان لديك بالفعل ملف `.dat` مُعد من بيئة أخرى، ما عليك سوى استدعاء `importDictionary(path)`. هذا مثالي لمزامنة القواميس عبر خوادم التطوير، والاختبار، والإنتاج.

## كيفية إدارة مجموعات المرادفات
تسمح لك مجموعات المرادفات بمعاملة مجموعة من المصطلحات ككيان منطقي واحد. يتم إضافة أو مسح أو استرجاع المجموعات عبر واجهة برمجة تطبيقات `SynonymDictionary`، كما هو موضح في مقتطفات الشيفرة أعلاه.

## كيفية تحسين فهرس البحث
- **احذف بانتظام الإدخالات غير المستخدمة:** استخدم `clear()` قبل التحديثات الضخمة.  
- **ضبط مساحة الذاكرة JVM:** القواميس الكبيرة قد تحتاج إلى المزيد من الذاكرة؛ زد قيمة المعامل `-Xmx` وفقًا لذلك.  
- **حافظ على تحديث المكتبة:** الإصدارات الجديدة تحتوي على تحسينات في الأداء وإصلاحات للأخطاء.

## تطبيقات عملية
1. **أنظمة إدارة المحتوى (CMS):** يجد المستخدمون المقالات حتى عندما يستخدمون مصطلحات بديلة.  
2. **منصات التجارة الإلكترونية:** يصبح البحث عن المنتجات متسامحًا مع المرادفات مثل “laptop” مقابل “notebook”.  
3. **مستودعات المستندات:** تستفيد الأرشيفات القانونية أو الطبية من مجموعات المرادفات المتخصصة بالمجال، مما يحسن إمكانية الاكتشاف للمهنيين.

## اعتبارات الأداء
- **تحسين تخزين الفهرس:** أعد بناء الفهرس دوريًا لإزالة البيانات القديمة.  
- **إدارة استهلاك الذاكرة:** راقب استهلاك الذاكرة heap عند تحميل ملفات مرادفات كبيرة؛ عادةً ما يتطلب قاموس بحجم 500 ميغابايت مساحة heap بحجم 2 جيجابايت على JVM 64‑bit.  
- **تحديثات دورية:** ابق على أحدث نسخة من GroupDocs.Search للحصول على إصلاحات الأخطاء وتحسينات السرعة.

## المشكلات الشائعة والحلول
| المشكلة | السبب المحتمل | الحل |
|-------|--------------|-----|
| لا تظهر أي مطابقة للمرادفات | `setUseSynonymSearch(true)` غير مفعّل أو القاموس غير مستورد | تحقق من تمكين الخيار ووجود ملف القاموس. |
| أخطاء نفاد الذاكرة أثناء الاستيراد | ملف `.dat` كبير جدًا يتجاوز مساحة heap في JVM | زد حجم heap باستخدام `-Xmx` أو استورد على دفعات أصغر. |
| تكرار الإدخالات في النتائج | نفس المصطلح يظهر في مجموعات مرادفات متعددة | دمج المجموعات المتداخلة باستخدام `clear()` ثم `addRange()`. |

## الأسئلة المتكررة

**س: ما هو الحد الأدنى لمتطلبات النظام لاستخدام GroupDocs.Search؟**  
ج: أي نظام تشغيل حديث مع JDK متوافق (Java 8 أو أحدث) يكفي.

**س: كم مرة يجب أن أقوم بتحديث قاموس المرادفات؟**  
ج: حدّثه كلما ظهرت مصطلحات جديدة—استخدم `clear()` ثم `addRange()` لتحديث نظيف.

**س: هل يمكن تشغيل GroupDocs.Search دون شراء ترخيص؟**  
ج: تجربة مجانية تعمل للتقييم، لكن الترخيص مطلوب للنشر في بيئة الإنتاج.

**س: ما هي أفضل الممارسات لفهرسة مجموعات البيانات الكبيرة؟**  
ج: قسّم البيانات إلى دفعات منطقية، راقب استهلاك الheap، وجدول صيانة دورية للفهرس.

**س: لا أرى مطابقة المرادفات المتوقعة—ما الذي يجب التحقق منه؟**  
ج: تأكد من أن القاموس مستورد بشكل صحيح، وأن `setUseSynonymSearch(true)` مفعّل، وأن المصطلحات موجودة في مجموعات المرادفات.

**الموارد**  
- [التوثيق](https://docs.groupdocs.com/search/java/)  
- [مرجع API](https://reference.groupdocs.com/search/java)  
- [تحميل GroupDocs.Search للـ Java](https://releases.groupdocs.com/search/java/)  
- [مستودع GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)  
- [الحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) 

---

**آخر تحديث:** 2026-10-17  
**تم الاختبار مع:** GroupDocs.Search 25.4 للـ Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [إنشاء وإدارة فهرس Groupdocs Search للـ Java](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [مكتبة البحث النصي الكامل للـ Java – تحسين الفهرس باستخدام GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [بحث غير دقيق في Java: إضافة مستندات إلى الفهرس باستخدام GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
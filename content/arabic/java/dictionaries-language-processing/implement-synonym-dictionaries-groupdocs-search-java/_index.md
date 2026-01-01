---
date: '2025-12-19'
description: تعلم كيفية إضافة المرادفات، والبحث باستخدام المرادفات، وإدارة مجموعات
  المرادفات في جافا باستخدام GroupDocs.Search. عزّز أداء موثوقية فهرس البحث الخاص
  بك.
keywords:
- synonym dictionaries java
- groupdocs.search synonym implementation
- java search functionality enhancement
title: كيفية إضافة المرادفات في جافا باستخدام GroupDocs.Search – دليل شامل
type: docs
url: /ar/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

# كيفية إضافة المرادفات في جافا باستخدام GroupDocs.Search

مرحبًا بكم في دليلنا الشامل حول **كيفية إضافة المرادفات** في جافا باستخدام GroupDocs.Search. سواءً كنت تبني نظام إدارة محتوى غني بالمحتوى، أو كتالوجًا للتجارة الإلكترونية، أو مستودعًا للوثائق، فإن تمكين دعم المرادفات يمكن أن يحسن بشكل كبير من قابلية اكتشاف بياناتك. في هذا البرنامج التعليمي ستتعلم كيفية إنشاء وإدارة قواميس المرادفات، واستيراد ملفات قواميس المرادفات، وتحسين فهرس البحث للحصول على نتائج سريعة ودقيقة.

## إجابات سريعة
- **ما هي الخطوة الأساسية لإضافة المرادفات؟** قم بتهيئة `Index` واستخدم واجهة برمجة التطبيقات `SynonymDictionary`.  
- **هل يمكنني استيراد قاموس مرادفات؟** نعم – استخدم `importDictionary(path)` لتحميل ملف مُعد مسبقًا.  
- **كيف يمكنني تمكين البحث بالمرادفات؟** اضبط `SearchOptions.setUseSynonymSearch(true)`.  
- **هل من الممكن إدارة مجموعات المرادفات؟** بالتأكيد – يمكنك مسح، إضافة، أو استرجاع المجموعات عبر واجهة برمجة التطبيقات للقاموس.  
- **ما الذي يجب أن أضعه في الاعتبار عند تحسين فهرس البحث؟** قم بانتظام بإزالة الإدخالات غير المستخدمة وضبط مساحة الذاكرة JVM للبيانات الكبيرة.  

## ما هو “كيفية إضافة المرادفات”؟
إضافة المرادفات تعني تعريف كلمات أو عبارات بديلة يعتبرها محرك البحث مكافئة. هذا يسمح لاستعلام مثل **“better”** بمطابقة المستندات التي تحتوي على **“improve”**، **“enhance”** أو **“upgrade”**.

## لماذا نستخدم دعم المرادفات في GroupDocs.Search؟
- **تحسين تجربة المستخدم:** يجد المستخدمون المحتوى المناسب حتى إذا استخدموا مصطلحات مختلفة.  
- **معدلات تحويل أعلى:** مواقع التجارة الإلكترونية تحقق مبيعات أكثر من خلال مطابقة استعلامات المنتجات المتنوعة.  
- **تقليل الصيانة:** يمكن لقاموس واحد خدمة تطبيقات متعددة، مما يبسط عمليات التحديث.  

## المتطلبات المسبقة
- **GroupDocs.Search for Java** الإصدار 25.4 أو أحدث.  
- بيئة تطوير جافا (IntelliJ IDEA، Eclipse، إلخ) مع دعم Maven.  
- معرفة أساسية بجافا وإلمام بهيكل مشروع Maven.  

### المكتبات المطلوبة والإصدارات
- GroupDocs.Search for Java الإصدار 25.4 أو أعلى.  

### إعداد البيئة
- بيئة التطوير التي تختارها (IntelliJ IDEA، Eclipse، إلخ).  
- Maven لإدارة التبعيات.  

### متطلبات المعرفة
- برمجة كائنية التوجه في جافا.  
- عمليات الإدخال/الإخراج الأساسية للملفات.  

## إعداد GroupDocs.Search لجافا

### معلومات التثبيت
أضف المستودع والتبعيات إلى ملف `pom.xml` الخاص بك:

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

**تحميل مباشر** – يمكنك أيضًا تنزيل أحدث JAR من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **تجربة مجانية:** اختبار الميزات الأساسية بدون ترخيص.  
- **ترخيص مؤقت:** توسيع قدرات التجربة أثناء التقييم.  
- **شراء:** مطلوب للاستخدام في بيئة الإنتاج والحصول على مجموعة الميزات الكاملة.  

#### التهيئة الأساسية والإعداد
أنشئ كائن `Index`، ثم أضف المستندات لتكون قابلة للبحث:

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
إنشاء فهرس هو الأساس. أدناه نستعرض الخطوات الأساسية، كل منها مع الكود الدقيق الذي تحتاجه.

### الميزة 1: إنشاء وفهرسة فهرس
```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### الميزة 2: استرجاع المرادفات لكلمة
```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### الميزة 3: استرجاع مجموعات المرادفات
```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### الميزة 4: إدارة إدخالات قاموس المرادفات
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
```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### الميزة 6: استيراد المرادفات من ملف
```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### الميزة 7: إجراء بحث بدعم المرادفات
```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## كيفية البحث بالمرادفات
من خلال تمكين `setUseSynonymSearch(true)`، يقوم المحرك تلقائيًا بتوسيع الاستعلام باستخدام قاموس المرادفات الذي أنشأته أو استوردته. هذه الخطوة حاسمة لتقديم نتائج أغنى دون تغيير سلوك البحث للمستخدم.

## كيفية استيراد قاموس المرادفات
إذا كان لديك ملف `.dat` مُعد من بيئة أخرى، ما عليك سوى استدعاء `importDictionary(path)`. هذا مثالي لمزامنة القواميس عبر خوادم التطوير، والاختبار، والإنتاج.

## كيفية إدارة مجموعات المرادفات
تتيح لك مجموعات المرادفات التعامل مع مجموعة من المصطلحات ككيان منطقي واحد. يتم إضافة أو مسح أو استرجاع المجموعات عبر واجهة برمجة التطبيقات `SynonymDictionary`، كما هو موضح في مقتطفات الكود أعلاه.

## كيفية تحسين فهرس البحث
- **إزالة الإدخالات غير المستخدمة بانتظام:** استخدم `clear()` قبل التحديثات الضخمة.  
- **ضبط مساحة الذاكرة JVM:** قد تتطلب القواميس الكبيرة مزيدًا من الذاكرة.  
- **الحفاظ على تحديث المكتبة:** الإصدارات الجديدة تحتوي على تحسينات في الأداء.  

## تطبيقات عملية
1. **أنظمة إدارة المحتوى (CMS):** يجد المستخدمون المقالات حتى عندما يستخدمون مصطلحات بديلة.  
2. **منصات التجارة الإلكترونية:** تصبح عمليات البحث عن المنتجات متسامحة مع المرادفات مثل “laptop” مقابل “notebook”.  
3. **مستودعات الوثائق:** تستفيد الأرشيفات القانونية أو الطبية من مجموعات المرادفات المتخصصة بالمجال.  

## اعتبارات الأداء
- **تحسين تخزين الفهرس:** أعد بناء الفهرس بشكل دوري لإزالة البيانات القديمة.  
- **إدارة استهلاك الذاكرة:** راقب استهلاك الذاكرة عند تحميل ملفات مرادفات كبيرة.  
- **تحديثات منتظمة:** حافظ على استخدام أحدث إصدار من GroupDocs.Search للحصول على إصلاحات الأخطاء وتحسين السرعة.  

## الخلاصة
الآن لديك خارطة طريق كاملة، خطوة بخطوة، لـ **كيفية إضافة المرادفات**، استيراد ملفات قواميس المرادفات، إدارة مجموعات المرادفات، و**البحث بالمرادفات** باستخدام GroupDocs.Search لجافا. طبّق هذه التقنيات لتعزيز الصلة، تحسين رضا المستخدم، والحفاظ على أداء فهرس البحث بأفضل حال.

## الأسئلة المتكررة

**س: ما هو الحد الأدنى لمتطلبات النظام لاستخدام GroupDocs.Search؟**  
ج: أي نظام تشغيل حديث مع JDK متوافق (Java 8 أو أحدث) يكفي.

**س: كم مرة يجب أن أقوم بتحديث قاموس المرادفات؟**  
ج: قم بتحديثه كلما ظهرت مصطلحات جديدة—استخدم `clear()` ثم `addRange()` لتحديث نظيف.

**س: هل يمكن تشغيل GroupDocs.Search بدون شراء ترخيص؟**  
ج: تجربة مجانية تعمل للتقييم، لكن الترخيص مطلوب لتطبيقات الإنتاج.

**س: ما هي أفضل الممارسات لفهرسة مجموعات البيانات الكبيرة؟**  
ج: قسّم البيانات إلى دفعات منطقية، راقب استهلاك الذاكرة، وجدول صيانة الفهرس بانتظام.

**س: لا أحصل على مطابقة المرادفات المتوقعة—ما الذي يجب التحقق منه؟**  
ج: تأكد من أن القاموس تم استيراده بشكل صحيح، وأن `setUseSynonymSearch(true)` مفعّل، وأن المصطلحات موجودة في مجموعات المرادفات.

**الموارد**  
- [التوثيق](https://docs.groupdocs.com/search/java/)  
- [مرجع API](https://reference.groupdocs.com/search/java)  
- [تحميل GroupDocs.Search لجافا](https://releases.groupdocs.com/search/java/)  
- [مستودع GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)  
- [الحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2025-12-19  
**تم الاختبار مع:** GroupDocs.Search 25.4 لجافا  
**المؤلف:** GroupDocs  

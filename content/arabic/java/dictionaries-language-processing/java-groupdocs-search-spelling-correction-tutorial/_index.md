---
date: '2026-02-21'
description: تعلم كيفية تمكين تصحيح الأخطاء الإملائية في جافا باستخدام GroupDocs.Search،
  وإضافة المستندات إلى الفهرس، وتعيين الحد الأقصى لعدد الأخطاء لتحسين دقة البحث.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: كيفية تمكين التدقيق الإملائي في جافا باستخدام GroupDocs.Search
type: docs
url: /ar/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# كيفية تمكين التدقيق الإملائي في Java باستخدام GroupDocs.Search

نتائج البحث الدقيقة ضرورية لأي تطبيق حديث. في هذا الدرس ستتعلم **كيفية تمكين التدقيق الإملائي** في Java باستخدام GroupDocs.Search، بحيث يحصل المستخدمون على النتائج الصحيحة حتى عندما يخطئون في كتابة الاستعلامات. سنستعرض إنشاء فهرس، **إضافة مستندات إلى الفهرس**، تكوين خيارات التدقيق الإملائي، وتشغيل بحث يصحح الأخطاء تلقائيًا.

## إجابات سريعة
- **ماذا يعني “كيفية تمكين التدقيق الإملائي”؟** يفعّل مدقق الإملاء المدمج الذي يصحّح أخطاء الكتابة للمستخدم أثناء البحث.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Search for Java.  
- **هل أحتاج إلى ترخيص؟** ترخيص تجريبي مجاني يعمل للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني التحكم في مستوى التحمل؟** نعم – استخدم `setMaxMistakeCount` لتحديد عدد الأخطاء المسموح بها.  
- **هل هو مناسب للفهارس الكبيرة؟** بالتأكيد – المحرك مُحسّن للفهرسة والبحث عاليي الأداء.

## ما هو “كيفية تمكين التدقيق الإملائي” في GroupDocs.Search؟
تمكين التدقيق الإملائي يُخبر محرك البحث بالبحث عن أقرب المصطلحات الصحيحة عندما يحتوي الاستعلام على أخطاء. هذه الميزة تحسّن تجربة المستخدم بشكل كبير من خلال إرجاع نتائج ذات صلة حتى مع إدخال مكتوب بشكل خاطئ.

## لماذا تمكين تصحيح الإملاء في تطبيقات Java؟
- **يعزز رضا المستخدم** – لا يحتاج المستخدمون إلى كتابة النص بشكل مثالي.  
- **يقلل معدلات الارتداد** – النتائج الأكثر دقة تحافظ على تفاعل الزوار.  
- **يعمل عبر المجالات** – من كتالوجات المكتبات إلى عمليات بحث المنتجات في التجارة الإلكترونية.

## المتطلبات المسبقة
- مجموعة تطوير Java (JDK) مثبتة.  
- معرفة أساسية بـ Java و Maven.  
- فهم مفاهيم الفهرسة.  
- إصدار تجريبي أو مفتاح مرخص من GroupDocs.Search.

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
بدلاً من ذلك، قم بتنزيل أحدث نسخة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
احصل على ترخيص تجريبي مجاني للتقييم. للاستخدام في الإنتاج، اشترِ ترخيصًا كاملاً أو اطلب مفتاحًا مؤقتًا من الموقع الرسمي.

## كيفية إضافة مستندات إلى الفهرس
إنشاء فهرس هو الأساس لأي تطبيق يدعم البحث. أدناه مثال بسيط ي **يضيف مستندات إلى الفهرس** من مجلد.

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

*نصيحة:* تأكد من صحة المسارات وأن التطبيق يمتلك صلاحيات الكتابة على مجلد الفهرس.

## كيفية تكوين تصحيح الإملاء (set max mistake count)
يمكنك ضبط مدقق الإملاء بدقة من خلال تمكينه وتحديد مستوى التحمل للأخطاء.

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

*لماذا `setMaxMistakeCount` مهم:* يحدد عدد الأخطاء التي سيتحملها المحرك. عدّل هذه القيمة بناءً على أنماط الأخطاء الشائعة في مجالك.

## كيفية إجراء بحث مصحّح إملائيًا
مع جاهزية الفهرس وتكوين خيارات الإملاء، نفّذ استعلامًا قد يحتوي على أخطاء.

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

تُعيد الدالة `search()` كائن `SearchResult` الذي يحتوي على المصطلحات المصححة وأهم المستندات ذات الصلة.

## تطبيقات عملية
1. **أنظمة المكتبة:** تصحيح عناوين الكتب أو أسماء المؤلفين المكتوبة بشكل خاطئ.  
2. **منصات التجارة الإلكترونية:** إصلاح أخطاء الكتابة للمستخدمين في بحث المنتجات لزيادة التحويلات.  
3. **أنظمة إدارة المحتوى:** تحسين استرجاع المقالات للموظفين التحريريين.

## اعتبارات الأداء
- **حافظ على تحديث الفهرس** – أعد فهرسة الملفات الجديدة أو المعدلة بانتظام.  
- **ضبط إعدادات ذاكرة JVM** – خصص مساحة كافية من الذاكرة (heap) للفهارس الكبيرة.  
- **مراقبة استهلاك الموارد** – عدّل إعدادات جامع القمامة إذا لزم الأمر.

## المشكلات الشائعة & استكشاف الأخطاء
| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| عدم إرجاع أي نتائج بعد تمكين التدقيق الإملائي | مسار مجلد الفهرس غير صحيح أو فارغ | تحقق من أن `indexFolder` يشير إلى فهرس صالح وأن `index.add()` نجح |
| مدقق الإملاء لا يصحّح الأخطاء الواضحة | `setMaxMistakeCount` مضبوط منخفضًا جدًا | زد العدد إلى 2 أو 3 لتصحيح أكثر تسامحًا |
| تتعطل التطبيق عند مجموعات مستندات كبيرة | ذاكرة JVM غير كافية | زد خيار `-Xmx` (مثال: `-Xmx4g`). |

## الأسئلة المتكررة

**س: ما هو GroupDocs.Search؟**  
ج: إنه مكتبة Java توفر فهرسة سريعة، ميزات بحث متقدمة، وتدقيق إملائي مدمج.

**س: كيف أحصل على ترخيص لـ GroupDocs.Search؟**  
ج: زر الموقع الرسمي لتنزيل نسخة تجريبية مجانية أو شراء ترخيص كامل.

**س: هل يمكنني دمج GroupDocs.Search مع أطر Java أخرى؟**  
ج: نعم، يعمل مع Spring، Jakarta EE، وأي تطبيق Java قياسي.

**س: ما هي المشكلات الشائعة عند إعداد فهرس؟**  
ج: مسارات المجلد غير صحيحة، صلاحيات ملفات غير كافية، أو تبعيات مفقودة في `pom.xml`.

**س: كيف يحسّن تصحيح الإملاء نتائج البحث؟**  
ج: يعيد كتابة الاستعلامات المكتوبة بشكل خاطئ تلقائيًا إلى أقرب المصطلحات الصحيحة، مما يُرجع نتائج أكثر صلة.

## موارد إضافية
- [التوثيق](https://docs.groupdocs.com/search/java/)
- [مرجع API](https://reference.groupdocs.com/search/java)
- [تحميل](https://releases.groupdocs.com/search/java/)
- [مستودع GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-02-21  
**تم الاختبار مع:** GroupDocs.Search 25.4  
**المؤلف:** GroupDocs
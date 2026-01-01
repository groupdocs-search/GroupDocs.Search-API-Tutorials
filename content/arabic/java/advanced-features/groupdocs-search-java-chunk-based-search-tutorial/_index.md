---
date: '2025-12-19'
description: تعلم كيفية إضافة المستندات إلى الفهرس وتمكين البحث القائم على القطع في
  جافا باستخدام GroupDocs.Search، مما يعزز الأداء لمجموعات المستندات الكبيرة.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: إضافة مستندات إلى الفهرس باستخدام البحث القائم على القطع في جافا
type: docs
url: /ar/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# إضافة مستندات إلى الفهرس مع البحث القائم على القطع في Java

في عالم اليوم القائم على البيانات، القدرة على **إضافة مستندات إلى الفهرس** بسرعة ثم إجراء عمليات بحث قائمة على القطع أمر أساسي لأي تطبيق يتعامل مع مجموعات كبيرة من الملفات. سواء كنت تتعامل مع العقود القانونية، أو أرشيفات دعم العملاء، أو مكتبات بحث ضخمة، فإن هذا الدليل يوضح لك بالضبط كيفية إعداد GroupDocs.Search للـ Java بحيث يمكنك فهرسة المستندات بكفاءة واسترجاع المعلومات ذات الصلة في قطع صغيرة.

## ما ستتعلمه
- كيفية إنشاء فهرس بحث في مجلد محدد.  
- خطوات **إضافة مستندات إلى الفهرس** من مواقع متعددة.  
- تكوين خيارات البحث لتمكين البحث القائم على القطع.  
- إجراء عمليات بحث أولية وتالية قائمة على القطع.  
- سيناريوهات واقعية حيث يبرز البحث القائم على القطع للمستندات.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** إنشاء مجلد فهرس البحث.  
- **كيف يمكنني تضمين ملفات متعددة؟** استخدم `index.add()` لكل مجلد مستندات.  
- **أي خيار يفعّل البحث القائم على القطع؟** `options.setChunkSearch(true)`.  
- **هل يمكنني الاستمرار في البحث بعد القطعة الأولى؟** نعم، استدعِ `index.searchNext()` مع الرمز المميز.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية أو ترخيص مؤقت يكفي للتطوير؛ الترخيص الكامل مطلوب للإنتاج.

## المتطلبات المسبقة
للتبع هذا الدليل، تأكد من وجود:

- **المكتبات المطلوبة**: GroupDocs.Search للـ Java 25.4 أو أحدث.  
- **إعداد البيئة**: وجود مجموعة تطوير جافا (JDK) متوافقة مثبتة.  
- **المتطلبات المعرفية**: معرفة أساسية ببرمجة جافا وإلمام بـ Maven.

## إعداد GroupDocs.Search للـ Java
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

بدلاً من ذلك، حمّل أحدث نسخة من [إصدارات GroupDocs.Search للـ Java](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
لتجربة GroupDocs.Search:

- **نسخة تجريبية مجانية** – اختبار الميزات الأساسية دون التزام.  
- **ترخيص مؤقت** – وصول ممتد للتطوير.  
- **شراء** – ترخيص كامل للاستخدام في الإنتاج.

### التهيئة الأساسية والإعداد
أنشئ فهرسًا في المجلد الذي تريد أن تعيش فيه البيانات القابلة للبحث:

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

## كيفية إضافة مستندات إلى الفهرس
الآن بعد أن تم إنشاء الفهرس، الخطوة المنطقية التالية هي **إضافة مستندات إلى الفهرس** من المواقع التي تُخزن فيها ملفاتك.

### 1. إنشاء فهرس
**نظرة عامة**: إعداد دليل لفهرس البحث.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. إضافة مستندات إلى الفهرس
**نظرة عامة**: جلب الملفات من عدة مجلدات مصدر.

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

### 3. تكوين خيارات البحث للبحث القائم على القطع
فعّل البحث القائم على القطع بتعديل كائن الخيارات.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. إجراء بحث أولي قائم على القطع
نفّذ الاستعلام الأول باستخدام الخيارات المفعّلة للقطع.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. الاستمرار في البحث القائم على القطع
كرر عبر القطع المتبقية حتى يكتمل البحث.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## لماذا نستخدم البحث القائم على القطع؟
يقسم البحث القائم على القطع مجموعات المستندات الضخمة إلى أجزاء يمكن التحكم فيها، مما يقلل من الضغط على الذاكرة ويسرّع أوقات الاستجابة. يكون ذلك مفيدًا بشكل خاص عندما:

1. **الفرق القانونية** تحتاج إلى العثور على بنود محددة عبر آلاف العقود.  
2. **بوابات دعم العملاء** يجب أن تعرض مقالات قاعدة المعرفة ذات الصلة فورًا.  
3. **الباحثون** يتنقلون عبر مجموعات بيانات واسعة دون تحميل الملفات بالكامل في الذاكرة.

## اعتبارات الأداء
- **إدارة الذاكرة** – خصص مساحة كافية للـ heap (`-Xmx`) للفهارس الكبيرة.  
- **مراقبة الموارد** – راقب استهلاك وحدة المعالجة المركزية أثناء عمليات الفهرسة والبحث.  
- **صيانة الفهرس** – أعد بناء الفهرس أو نظفه دوريًا للتخلص من البيانات القديمة.

## الأخطاء الشائعة & استكشاف الأخطاء وإصلاحها
| المشكلة | السبب | الحل |
|-------|----------------|-----|
| `OutOfMemoryError` أثناء الفهرسة | حجم الـ heap منخفض | زيادة حجم heap للـ JVM (`-Xmx2g` أو أعلى) |
| لا تُرجع أي نتائج | لم يتم معالجة رمز القطعة | تأكد من أن حلقة `while` تستمر حتى يكون `getNextChunkSearchToken()` يساوي `null` |
| بطء أداء البحث | الفهرس غير مُحسّن | نفّذ `index.optimize()` بعد الإضافات الجماعية |

## الأسئلة المتكررة

**س: ما هو البحث القائم على القطع؟**  
ج: يقسم البحث القائم على القطع مجموعة البيانات إلى أجزاء أصغر، مما يسمح بإجراء استعلامات فعّالة على أحجام كبيرة من البيانات دون تحميل المستندات بالكامل في الذاكرة.

**س: كيف أقوم بتحديث فهرسي بملفات جديدة؟**  
ج: ببساطة استدعِ `index.add()` مع مسار المستندات الجديدة؛ سيُدمج الفهرس هذه الملفات تلقائيًا.

**س: هل يستطيع GroupDocs.Search التعامل مع صيغ ملفات مختلفة؟**  
ج: نعم، يدعم PDFs، DOCX، XLSX، PPTX، والعديد من الصيغ الشائعة الأخرى.

**س: ما هي الاختناقات الشائعة في الأداء؟**  
ج: قيود الذاكرة والفهارس غير المُحسّنة هي الأكثر شيوعًا؛ خصص heap كافيًا وحسّن الفهرس بانتظام.

**س: أين يمكنني العثور على وثائق أكثر تفصيلًا؟**  
ج: زر [توثيق GroupDocs.Search الرسمي](https://docs.groupdocs.com/search/java/) للحصول على أدلة متعمقة ومراجع API.

## موارد
- **التوثيق**: [وثائق GroupDocs.Search للـ Java](https://docs.groupdocs.com/search/java/)  
- **مرجع API**: [مرجع GroupDocs.Search API](https://reference.groupdocs.com/search/java)  
- **التحميل**: [إصدارات GroupDocs.Search](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [مستودع GroupDocs.Search على GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **دعم مجاني**: [منتدى GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت**: [الحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2025-12-19  
**تم الاختبار مع:** GroupDocs.Search 25.4 للـ Java  
**المؤلف:** GroupDocs  

---
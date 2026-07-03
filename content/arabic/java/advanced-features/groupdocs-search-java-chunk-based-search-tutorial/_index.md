---
date: '2026-02-21'
description: تعلم كيفية إضافة المستندات إلى الفهرس وزيادة أداء البحث باستخدام البحث
  القائم على القطع في جافا باستخدام GroupDocs.Search، مع تحسين ذاكرة فهرس البحث في
  جافا لمجموعات المستندات الكبيرة.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: إضافة مستندات إلى الفهرس باستخدام البحث القائم على القطع في جافا
type: docs
url: /ar/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

 to translate table content. Keep pipe separators.

Make sure Arabic RTL but just normal text.

Let's produce translation.

Be careful: In markdown, headings start with #. We'll translate after #.

Also bullet lists.

Let's translate.

We'll keep URLs unchanged.

Let's produce final answer.# إضافة مستندات إلى الفهرس مع البحث القائم على القطع في Java

في التطبيقات الحديثة التي تحتاج إلى **إضافة مستندات إلى الفهرس** بسرعة ثم إجراء استعلامات سريعة قائمة على القطع، ستحتاج إلى حل يتوسع دون استهلاك الذاكرة بشكل مفرط. يوضح هذا البرنامج التعليمي كيفية إعداد GroupDocs.Search لـ Java، وإضافة مجلدات مستندات متعددة، وتكوين المحرك لت **زيادة أداء البحث** مع الحفاظ على استهلاك **ذاكرة فهرس البحث java** تحت السيطرة. سواء كنت تقوم بفهرسة العقود القانونية أو تذاكر الدعم أو الأوراق البحثية، ستوفر لك الخطوات أدناه تنفيذًا جاهزًا للإنتاج.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** إنشاء مجلد فهرس البحث.  
- **كيف يمكنني تضمين ملفات متعددة؟** استخدم `index.add()` لكل مجلد مستندات.  
- **أي خيار يفعّل البحث القائم على القطع؟** `options.setChunkSearch(true)`.  
- **هل يمكنني الاستمرار في البحث بعد القطعة الأولى؟** نعم، استدعِ `index.searchNext()` مع الرمز المميز.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية أو ترخيص مؤقت يكفي للتطوير؛ الترخيص الكامل مطلوب للإنتاج.  

## ما ستتعلمه
- كيفية إنشاء فهرس بحث في مجلد محدد.  
- خطوات **إضافة مستندات إلى الفهرس** من مواقع متعددة.  
- تكوين خيارات البحث لتمكين البحث القائم على القطع.  
- إجراء عمليات بحث أولية وتالية قائمة على القطع.  
- سيناريوهات واقعية حيث يبرز البحث القائم على القطع.  

## المتطلبات المسبقة
للتبع هذا الدليل، تأكد من وجود ما يلي:

- **المكتبات المطلوبة**: GroupDocs.Search لـ Java 25.4 أو أحدث.  
- **إعداد البيئة**: وجود مجموعة تطوير Java (JDK) متوافقة مثبتة.  
- **المتطلبات المعرفية**: معرفة أساسية ببرمجة Java وإلمام بـ Maven.

## إعداد GroupDocs.Search لـ Java
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

بدلاً من ذلك، حمّل أحدث نسخة من [إصدارات GroupDocs.Search لـ Java](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
لتجربة GroupDocs.Search:

- **نسخة تجريبية** – اختبار الميزات الأساسية دون التزام.  
- **ترخيص مؤقت** – وصول ممتد للتطوير.  
- **شراء** – ترخيص كامل للاستخدام الإنتاجي.

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
**نظرة عامة**: سحب الملفات من عدة مجلدات مصدر.

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
فعّل البحث القائم على القطع عن طريق تعديل كائن الخيارات.

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
تكرار عبر القطع المتبقية حتى يكتمل البحث.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## لماذا نستخدم البحث القائم على القطع؟
يقسّم البحث القائم على القطع مجموعات المستندات الضخمة إلى أجزاء يمكن التحكم فيها، مما يقلل من ضغط الذاكرة ويسرّع أوقات الاستجابة. يكون ذلك مفيدًا خصوصًا عندما:

1. **الفرق القانونية** تحتاج إلى العثور على بنود محددة عبر آلاف العقود.  
2. **بوابات دعم العملاء** يجب أن تعرض مقالات قاعدة المعرفة ذات الصلة فورًا.  
3. **الباحثون** يتنقلون عبر مجموعات بيانات واسعة دون تحميل الملفات بالكامل في الذاكرة.

## كيف يزيد هذا النهج **أداء البحث**
من خلال البحث في قطع أصغر بدلاً من الملفات الكاملة، يمكن للمحرك:

- تخطي الأقسام غير ذات الصلة مبكرًا، مما يقلل من دورات CPU.  
- إبقاء القطعة النشطة فقط في الذاكرة، مما يقلل مباشرةً من استهلاك **ذاكرة فهرس البحث java**.  
- موازاة معالجة القطع على أجهزة متعددة الأنوية للحصول على نتائج أسرع.

## إدارة **ذاكرة فهرس البحث java**
بينما يقلل البحث القائم على القطع من البصمة الذاكرية بالفعل، يمكنك تحسين JVM أكثر:

- خصص حجم heap كافٍ (`-Xmx2g` أو أعلى) بناءً على حجم الفهرس.  
- استخدم `index.optimize()` بعد الإضافات الضخمة لضغط بنية الفهرس.  
- راقب توقفات GC باستخدام أدوات مثل VisualVM لتجنب spikes في زمن الاستجابة.

## اعتبارات الأداء
- **إدارة الذاكرة** – خصص مساحة heap كافية (`-Xmx`) للفهارس الكبيرة.  
- **مراقبة الموارد** – راقب استهلاك CPU أثناء عمليات الفهرسة والبحث.  
- **صيانة الفهرس** – أعد بناء الفهرس أو نظفه دوريًا للتخلص من البيانات القديمة.

## المشكلات الشائعة & استكشاف الأخطاء
| المشكلة | السبب | الحل |
|-------|----------------|-----|
| `OutOfMemoryError` أثناء الفهرسة | حجم heap منخفض | زيادة حجم heap في JVM (`-Xmx2g` أو أعلى) |
| لا تُرجع أي نتائج | رمز القطعة غير معالج | تأكد من أن حلقة `while` تستمر حتى يصبح `getNextChunkSearchToken()` `null` |
| بطء في أداء البحث | الفهرس غير مُحسّن | تشغيل `index.optimize()` بعد الإضافات الضخمة |

## الأسئلة المتكررة

**س: ما هو البحث القائم على القطع؟**  
ج: البحث القائم على القطع يقسم مجموعة البيانات إلى أجزاء أصغر، مما يسمح باستعلامات فعّالة على أحجام كبيرة من البيانات دون تحميل المستندات بالكامل في الذاكرة.

**س: كيف أقوم بتحديث فهرسي بملفات جديدة؟**  
ج: ما عليك سوى استدعاء `index.add()` مع مسار المستندات الجديدة؛ سيُدمج الفهرس هذه الملفات تلقائيًا.

**س: هل يدعم GroupDocs.Search صيغ ملفات مختلفة؟**  
ج: نعم، يدعم PDFs، DOCX، XLSX، PPTX، والعديد من الصيغ الشائعة الأخرى.

**س: ما هي الاختناقات الأداء النموذجية؟**  
ج: قيود الذاكرة والفهارس غير المُحسّنة هي الأكثر شيوعًا؛ خصص heap كافيًا وحسّن الفهرس بانتظام.

**س: أين يمكنني العثور على وثائق أكثر تفصيلًا؟**  
ج: زر الوثائق الرسمية لـ [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) للحصول على أدلة متعمقة ومراجع API.

**س: هل يعمل البحث القائم على القطع مع ملفات PDF مشفّرة؟**  
ج: نعم، طالما قمت بتوفير كلمة المرور عبر التحميل المناسب للـ API.

**س: كيف يمكنني مراقبة تقدم الفهرسة؟**  
ج: استخدم التحميل الزائد `Index.add()` الذي يُعيد كائن `Progress` أو اربط callbacks للتسجيل.

## الموارد
- **الوثائق**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **مرجع API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **التنزيل**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **الدعم المجاني**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2026-02-21  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs  

---
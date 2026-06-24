---
date: '2026-05-22'
description: تعلم بحث Java الضبابي باستخدام GroupDocs.Search Java، إضافة المستندات
  إلى الفهرس، تمكين البحث النصي المتقدم، ومعالجة أنواع الملفات المتعددة بكفاءة.
keywords:
- java fuzzy search
- advanced text search java
- search file types java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn java fuzzy search with GroupDocs.Search Java, add documents to
    index, enable advanced text search, and handle multiple file types efficiently.
  headline: 'Java Fuzzy Search: Add Documents to Index with GroupDocs.Search'
  type: TechArticle
- description: Learn java fuzzy search with GroupDocs.Search Java, add documents to
    index, enable advanced text search, and handle multiple file types efficiently.
  name: 'Java Fuzzy Search: Add Documents to Index with GroupDocs.Search'
  steps:
  - name: '**Free Trial** – explore the API without cost.'
    text: '**Free Trial** – explore the API without cost.'
  - name: '**Temporary License** – extend the trial period for deeper testing.'
    text: '**Temporary License** – extend the trial period for deeper testing.'
  - name: '**Purchase** – obtain a commercial license for production use.'
    text: '**Purchase** – obtain a commercial license for production use.'
  - name: '**Corporate Document Management** – Quickly locate policies, contracts,
      or HR manuals across thousands of files.'
    text: '**Corporate Document Management** – Quickly locate policies, contracts,
      or HR manuals across thousands of files.'
  - name: '**Legal Research** – Find precedent cases even when the exact phrasing
      differs, thanks to word‑form search.'
    text: '**Legal Research** – Find precedent cases even when the exact phrasing
      differs, thanks to word‑form search.'
  - name: '**E‑commerce Catalogs** – Allow shoppers to search product descriptions
      using varied terminology, improving conversion rates.'
    text: '**E‑commerce Catalogs** – Allow shoppers to search product descriptions
      using varied terminology, improving conversion rates.'
  type: HowTo
- questions:
  - answer: It means loading source files into a searchable data structure that GroupDocs.Search
      can query.
    question: What does “add documents to index” mean?
  - answer: GroupDocs.Search for Java 25.4 (or newer) includes all features demonstrated
      here.
    question: Which library version is required?
  - answer: A free trial works for development; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—enable `setUseWordFormsSearch(true)` in `SearchOptions`.
    question: Can I search different word forms?
  - answer: No, you can also download the JAR directly (see the Direct Download link).
    question: Is Maven the only way to install?
  type: FAQPage
title: 'بحث Java الضبابي: إضافة المستندات إلى الفهرس باستخدام GroupDocs.Search'
type: docs
url: /ar/java/searching/groupdocs-search-java-advanced-text-search-guide/
weight: 1
---

# بحث Java الضبابي: إضافة مستندات إلى الفهرس باستخدام GroupDocs.Search

## الإجابات السريعة
- **ماذا يعني “add documents to index”؟** يعني تحميل ملفات المصدر إلى بنية بيانات قابلة للبحث يمكن لـ GroupDocs.Search الاستعلام منها.  
- **ما هو إصدار المكتبة المطلوب؟** يحتوي GroupDocs.Search for Java 25.4 (أو أحدث) على جميع الميزات الموضحة هنا.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتطوير؛ يتطلب الاستخدام في الإنتاج ترخيصًا تجاريًا.  
- **هل يمكنني البحث عن صيغ كلمات مختلفة؟** نعم—قم بتمكين `setUseWordFormsSearch(true)` في `SearchOptions`.  
- **هل Maven هو الطريقة الوحيدة للتثبيت؟** لا، يمكنك أيضًا تنزيل ملف JAR مباشرة (انظر رابط التحميل المباشر).  

## ما هو “add documents to index”؟
إضافة مستندات إلى الفهرس يعني مسح ملفات المصدر، استخراج النص القابل للبحث، وتخزين تلك المعلومات في تنسيق منظم يتيح البحث السريع. يدعم GroupDocs.Search العديد من أنواع الملفات جاهزةً، لذا يمكنك التركيز على منطق الأعمال بدلاً من التحليل. يمكن تخزين الفهرس الناتج على القرص أو في الذاكرة، مما يسمح باسترجاع سريع دون إعادة قراءة الملفات الأصلية في كل مرة يتم فيها تنفيذ استعلام.

## لماذا تستخدم تقنيات البحث النصي المتقدمة في Java؟
حمّل فهرسك مرة واحدة ثم نفّذ استعلامات ضبابية، غير حساسة لحالة الأحرف، أو استعلامات القرب دون إعادة معالجة الملفات. تفعيل هذه التقنيات يزيد الاسترجاع بنسبة تصل إلى 30 % في الاختبارات الواقعية، مما يسمح للمستخدمين بالعثور على نتائج ذات صلة حتى عندما يخطئون في الصياغة أو الإملاء.

## المتطلبات المسبقة
- **المكتبات المطلوبة**: GroupDocs.Search for Java 25.4.  
- **إعداد البيئة**: Java JDK 8 أو أحدث، Maven (أو التعامل اليدوي مع JAR).  
- **المتطلبات المعرفية**: برمجة Java الأساسية وإدارة تبعيات Maven.

## إعداد GroupDocs.Search لـ Java
قبل كتابة أي كود، تأكد من أن المكتبة متاحة لمشروعك.

### إعداد Maven
ملف `pom.xml` هو وصف مشروع Maven حيث يتم إعلان التبعيات.

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

### التحميل المباشر
إذا كنت تفضل عدم استخدام Maven، يمكنك تنزيل أحدث ملف JAR من الصفحة الرسمية: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

للحصول على تعليمات الاستخدام التفصيلية، راجع [GroupDocs Documentation](https://docs.groupdocs.com/search/java/).

### خطوات الحصول على الترخيص
1. **النسخة التجريبية المجانية** – استكشف الـ API بدون تكلفة.  
2. **ترخيص مؤقت** – تمديد فترة التجربة للاختبار المتعمق.  
3. **شراء** – الحصول على ترخيص تجاري للاستخدام في الإنتاج.

## أنوع ملفات البحث المدعومة في Java
يدعم GroupDocs.Search **أكثر من 50 تنسيقًا للإدخال والإخراج** — بما في ذلك DOCX و PDF و PPTX و XLSX و TXT و HTML وأنواع الصور الشائعة — بحيث يمكنك فهرسة أي مستند تقريبًا يستخدمه عملك.

## دليل التنفيذ خطوة بخطوة

### 1. إنشاء وتكوين فهرس
الفئة `Index` هي الكائن الأعلى مستوى الذي يمثل مستودعًا قابلًا للبحث مخزنًا على القرص.

#### نظرة عامة
سنقوم بإنشاء مجلد على القرص سيحتوي على ملفات الفهرس.

#### Code
```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/SearchForDifferentWordForms";
Index index = new Index(indexFolder);
```

*شرح*: يُشير مُنشئ `Index` إلى مجلد حيث سيتم حفظ جميع بيانات الفهرس. استبدل `YOUR_DOCUMENT_DIRECTORY` بالمسار الفعلي على جهازك.

### 2. كيفية إضافة مستندات إلى الفهرس
طريقة `add` تقوم بمسح المجلد بشكل متكرر، تستخرج النص، وتخزنه في الفهرس.

#### نظرة عامة
يقوم GroupDocs.Search بمسح الدليل المحدد وفهرسة كل نوع ملف مدعوم يجده.

#### Code
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
index.add(documentsFolder);
```

*شرح*: تأكد من صحة المسار وأن التطبيق لديه أذونات القراءة. تقوم الطريقة بمعالجة الملفات على دفعات للحفاظ على انخفاض استهلاك الذاكرة.

### 3. تكوين خيارات البحث لصيغ الكلمات
`SearchOptions` يحتوي على معلمات تتحكم في كيفية معالجة الاستعلامات.

#### نظرة عامة
سنقوم بضبط `SearchOptions` لتفعيل البحث عن صيغ الكلمات (الضبابي).

#### Code
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
options.setUseWordFormsSearch(true); // Enables search for different grammatical variations of words.
```

*شرح*: ضبط `setUseWordFormsSearch(true)` يُخبر المحرك بتوسيع الاستعلامات لتشمل الصيغ المعروفة، مما يحسن الاسترجاع للتغييرات مثل “wish”، “wished”، و “wishes”.

### 4. تنفيذ البحث
`SearchResult` يحتوي على قائمة المستندات المتطابقة ومقتطفات النص.

#### نظرة عامة
سنبحث عن كلمة “wished” ونسترجع المستندات المتطابقة.

#### Code
```java
import com.groupdocs.search.SearchResult;

String query = "wished";
SearchResult result = index.search(query, options);
```

*شرح*: طريقة `search` تنفّذ الاستعلام على المحتوى المفهرس باستخدام الخيارات التي حددناها. تُعيد `SearchResult` مراجع المستندات ومقتطفات مُبرزّة لكل نتيجة.

## المشكلات الشائعة وإصلاح الأخطاء
- **مسارات غير صحيحة** – تحقق مرة أخرى من كل من `indexFolder` و `documentsFolder` للتأكد من عدم وجود أخطاء إملائية وصلاحيات الوصول المناسبة.  
- **تنسيقات ملفات غير مدعومة** – تأكد من أن مستنداتك من بين أكثر من 50 تنسيقًا المذكورة في وثائق GroupDocs.Search.  
- **بطء الأداء** – بالنسبة لمجموعات بيانات كبيرة، قم بالفهرسة على دفعات، راقب استهلاك الذاكرة في JVM، وخزن الفهرس على تخزين SSD.

## التطبيقات العملية
1. **إدارة المستندات المؤسسية** – تحديد سياسات، عقود، أو كتيبات الموارد البشرية بسرعة عبر آلاف الملفات.  
2. **البحث القانوني** – العثور على القضايا السابقة حتى عندما تختلف الصياغة الدقيقة، بفضل بحث صيغ الكلمات.  
3. **كتالوجات التجارة الإلكترونية** – تمكين المتسوقين من البحث في أوصاف المنتجات باستخدام مصطلحات متنوعة، مما يحسن معدلات التحويل.

## نصائح الأداء
- أعد الفهرسة فقط عندما تُضاف مستندات جديدة أو تتغير المستندات الحالية.  
- استخدم علامة `-Xmx` في Java لتخصيص ذاكرة كافية للفهرس الكبير (مثال: `-Xmx4g`).  
- استدعِ `index.optimize()` دوريًا (إن كان متاحًا) لضغط ملفات الفهرس وتقليل عمليات الإدخال/الإخراج على القرص.

## الخلاصة
أنت الآن تعرف كيف **تضيف مستندات إلى الفهرس**، وتفعيل بحث Java الضبابي، وتحسين GroupDocs.Search لـ Java. تمكّنك هذه التقنيات من بناء تجارب بحث سريعة وغنية بالميزات عبر أي مجموعة مستندات.

### الخطوات التالية
- تجربة المطابقة الضبابية والترتيب المخصص.  
- دمج وحدة البحث في واجهة برمجة تطبيقات REST للاستخدام من الواجهة الأمامية.  
- استكشاف دعم متعدد اللغات عن طريق تكوين محللات مخصصة للغات.

## الأسئلة المتكررة

**س1: ما هي الصيغ التي يدعمها GroupDocs.Search؟**  
ج1: يدعم أكثر من 50 صيغة بما في ذلك DOCX و PDF و PPTX و XLSX و TXT و HTML وأنواع الصور الشائعة. راجع الوثائق الرسمية للقائمة الكاملة.

**س2: كيف أقوم بتحديث الفهرس بمستندات جديدة؟**  
ج2: استدعِ `index.add(newDocumentsFolder)` مرة أخرى؛ ستضيف المكتبة فقط الملفات الجديدة أو التي تم تعديلها، مع ترك الإدخالات الحالية دون تغيير.

**س3: هل يمكنني تخصيص استعلامات البحث أكثر؟**  
ج3: نعم—توفر `SearchOptions` خيارات للبحث الضبابي، حساسية الحالة، تقسيم النتائج إلى صفحات، وخوارزميات ترتيب مخصصة.

**س4: بحثي بطيء—ماذا أفعل؟**  
ج4: خزن الفهرس على تخزين SSD سريع، زِد حجم الذاكرة في JVM (`-Xmx`)، وتجنب فهرسة الملفات الكبيرة غير الضرورية. كذلك، فعّل بحث صيغ الكلمات فقط عند الحاجة.

**س5: أين يمكنني الحصول على مساعدة من المجتمع؟**  
ج5: استخدم منتدى الدعم الرسمي: [GroupDocs Support Forum](https://forum.groupdocs.com/c/search/10).

---

**آخر تحديث:** 2026-05-22  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs  

## الدروس ذات الصلة

- [GroupDocs.Search Java - بحث نطاق التاريخ والميزات المتقدمة](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [كيفية إضافة مرادفات في Java باستخدام GroupDocs.Search – دليل شامل](/search/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/)
- [إضافة مستندات إلى الفهرس باستخدام البحث القائم على القطع في Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)
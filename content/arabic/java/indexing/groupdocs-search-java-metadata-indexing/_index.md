---
date: '2026-10-22'
description: تعلم كيفية إجراء بحث metadata باستخدام GroupDocs في Java، وتكوين index
  settings، وإضافة المستندات، والاستعلام عن حقول metadata بكفاءة.
keywords:
- metadata search with groupdocs
- metadata indexing java
- groupdocs search java
lastmod: '2026-10-22'
og_description: تعلم كيفية إجراء بحث metadata باستخدام GroupDocs في Java، وتكوين index
  settings، وإضافة المستندات، والاستعلام عن حقول metadata بكفاءة.
og_image_alt: Guide showing Java code for metadata indexing using GroupDocs.Search
og_title: كيفية إجراء بحث metadata باستخدام GroupDocs في Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-22'
  description: Learn how to perform metadata search with GroupDocs in Java, configure
    index settings, add documents, and query by metadata fields efficiently.
  headline: How to do metadata search with GroupDocs in Java
  type: TechArticle
- description: Learn how to perform metadata search with GroupDocs in Java, configure
    index settings, add documents, and query by metadata fields efficiently.
  name: How to do metadata search with GroupDocs in Java
  steps:
  - name: Visit the GroupDocs website and go to the **Purchase** section.
    text: Visit the GroupDocs website and go to the **Purchase** section.
  - name: Choose a **temporary license** plan that matches your evaluation needs.
    text: Choose a **temporary license** plan that matches your evaluation needs.
  - name: '**Enterprise document management:** Retrieve contracts by contract date
      or signatory name.'
    text: '**Enterprise document management:** Retrieve contracts by contract date
      or signatory name.'
  - name: '**Digital library catalogs:** Let users browse books by genre, publication
      year, or author.'
    text: '**Digital library catalogs:** Let users browse books by genre, publication
      year, or author.'
  - name: '**CRM systems:** Quickly locate client files using custom metadata like
      customer ID or region.'
    text: '**CRM systems:** Quickly locate client files using custom metadata like
      customer ID or region.'
  type: HowTo
- questions:
  - answer: Metadata indexing stores document attributes (author, title, custom tags)
      in a searchable structure, enabling fast look‑ups without scanning full text.
    question: What is metadata indexing?
  - answer: Visit the GroupDocs purchase page and follow the steps to acquire a trial
      license.
    question: How do I obtain a temporary license?
  - answer: Yes, GroupDocs.Search supports PDF, DOCX, PPT, and many other formats.
    question: Can I index PDFs with this setup?
  - answer: Verify correct file paths and ensure the application has read permissions
      for the directories.
    question: What are common issues when adding documents?
  - answer: Regularly update your index, use incremental adds, and tune JVM memory
      settings.
    question: How do I optimize search performance?
  type: FAQPage
tags:
- metadata search
- GroupDocs
- Java indexing
title: كيفية إجراء بحث metadata باستخدام GroupDocs في Java
type: docs
url: /ar/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# كيفية إجراء بحث بالبيانات الوصفية باستخدام GroupDocs في Java

إضافة المستندات إلى الفهرس بسرعة وبشكل موثوق هو العمود الفقري لأي تطبيق حديث يعتمد على البحث. سواءً كنت تبني مستودعًا قانونيًا، أو قاعدة معرفة لدعم العملاء، أو بوابة مستندات داخلية، **metadata search with GroupDocs** يتيح لك العثور على الملفات حسب المؤلف، العنوان، أو أي علامة مخصصة دون فحص محتوى النص الكامل. في هذا البرنامج التعليمي ستتعلم كيفية تكوين إعدادات الفهرس، إنشاء فهرس يركز على البيانات الوصفية، إضافة ملفاتك، وإجراء عمليات بحث دقيقة — كل ذلك باستخدام GroupDocs.Search for Java.

## إجابات سريعة
- **ما هو الهدف الأساسي لفهرسة البيانات الوصفية؟** إنّه يتيح عمليات بحث سريعة بناءً على خصائص المستند بدلاً من محتوى النص الكامل.  
- **ما هي الطريقة التي تضيف الملفات إلى الفهرس؟** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **هل يمكنني البحث باستخدام حقول البيانات الوصفية المخصصة؟** نعم، بمجرد فهرسة الحقول يمكنك استعلامها مباشرة.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مؤقت يكفي للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** يوصى باستخدام JDK 8 أو أعلى.  

## ما هو فهرسة البيانات الوصفية في GroupDocs.Search؟
فهرسة البيانات الوصفية تستخرج وتخزن سمات المستند (مثل المؤلف، تاريخ الإنشاء، العلامات المخصصة) في بنية قابلة للبحث. عندما **add documents to index**، يقوم المحرك بتسجيل هذه السمات، مما يتيح لك تنفيذ استعلامات دقيقة مثل “العثور على جميع ملفات PDF التي كتبها *John Doe*” أو “search pdf by author”.

## لماذا تستخدم GroupDocs.Search لفهرسة البيانات الوصفية؟
يقدم بحث البيانات الوصفية باستخدام GroupDocs استجابة خفيفة الوزن وتستغرق أقل من الثانية حتى عندما يحتوي الفهرس على ملايين السجلات. يدعم **over 30 input and output formats** — بما في ذلك PDF و DOCX و PPTX و HTML وملفات الصور — ويستهلك أقل من 200 ميغابايت من ذاكرة الـ heap لفهرس يحتوي على 100 000 مستند على خادم عادي.

## المتطلبات المسبقة
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 أو أحدث مثبت ومُكوَّن.  
- إلمام أساسي بـ Java و Maven.  

## إعداد GroupDocs.Search لـ Java

### تعليمات التثبيت
أضف مستودع GroupDocs والاعتماد إلى ملف `pom.xml` الخاص بك:

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

يمكنك أيضًا تنزيل أحدث الملفات الثنائية مباشرةً من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
للحصول على ترخيص مؤقت للاختبار:
1. زر موقع GroupDocs وانتقل إلى قسم **Purchase**.  
2. اختر خطة **temporary license** التي تتوافق مع احتياجات تقييمك.  

## كيف تقوم بتكوين إعدادات الفهرس للبيانات الوصفية؟
تكوين إعدادات الفهرس يخبر المحرك أي معلومات يجب استخراجها وتخزينها. عن طريق تعيين نوع الفهرس إلى `MetadataIndex`، تقوم بإرشاد GroupDocs.Search للتركيز على حقول البيانات الوصفية بدلاً من محتوى النص الكامل، مما يقلل حجم الفهرس ويسرع الاستعلامات. يتم تطبيق هذا التكوين عبر كائن `IndexSettings`، حيث يمكنك أيضًا تحديد حقول البيانات الوصفية المخصصة التي سيتم فهرستها.

```text
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);
```

## الميزة 1: تكوين إعدادات الفهرس
استدعاء `setIndexType(IndexType.MetadataIndex)` يخبر المحرك بالتركيز على البيانات الوصفية بدلاً من محتوى النص الكامل. **`IndexType.MetadataIndex`** هو قيمة تعداد تختار وضع الفهرسة للبيانات الوصفية فقط.

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

## الميزة 2: إنشاء فهرس في مجلد محدد
أنشئ دليل فهرس فعلي حيث سيتم تخزين جميع البيانات الوصفية:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

استبدل `YOUR_DOCUMENT_DIRECTORY` بالمسار الذي يتوافق مع بنية مشروعك.

## الميزة 3: كيفية إضافة المستندات إلى الفهرس
طريقة `index.add` تضيف الملفات من مجلد إلى الفهرس وتستخرج بياناتها الوصفية. **`index.add`** تفحص كل مستند، تقرأ حقول البيانات الوصفية المدعومة، وتخزنها في الفهرس لاسترجاع سريع.

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**نصائح:**  
- تأكد من أن مسار المجلد صحيح وأن التطبيق يمتلك أذونات القراءة.  
- GroupDocs.Search يستخرج تلقائيًا البيانات الوصفية المدعومة من كل ملف.

## الميزة 4: البحث عن المستندات بالبيانات الوصفية
نفّذ استعلامًا يستهدف حقول البيانات الوصفية، على سبيل المثال البحث عن المستندات التي تكون اللغة فيها الإنجليزية:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

طريقة `search(query)` تبحث عبر البيانات الوصفية المفهرسة وتعيد المستندات المطابقة. يمكنك أيضًا **search pdf by author** باستخدام اسم المؤلف كسلسلة الاستعلام.

## التطبيقات العملية
1. **Enterprise document management:** استرجاع العقود حسب تاريخ العقد أو اسم الموقع.  
2. **Digital library catalogs:** السماح للمستخدمين بتصفح الكتب حسب النوع، سنة النشر، أو المؤلف.  
3. **CRM systems:** تحديد ملفات العملاء بسرعة باستخدام بيانات وصفية مخصصة مثل معرف العميل أو المنطقة.  

## نصائح وأفضل الممارسات
- **Incremental updates:** استخدم `index.addOrUpdate()` للملفات الجديدة أو المعدلة بدلاً من إعادة بناء الفهرس بالكامل.  
- **Batch processing:** عند التعامل مع آلاف الملفات، أضفها على دفعات أصغر للحفاظ على انخفاض استهلاك الذاكرة.  
- **Metadata validation:** تأكد من أن المستندات المصدرية تحتوي فعليًا على البيانات الوصفية التي تنوي الاستعلام عنها (مثل حقول المؤلف في ملفات PDF).  

## اعتبارات الأداء
- **Memory tuning:** اضبط حجم heap للـ JVM (`-Xmx`) بناءً على حجم البيانات الوصفية المفهرسة.  
- **Optimized storage:** استدعِ `index.optimize()` بشكل دوري لضغط الفهرس وتحسين سرعة الاستعلام.  

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **لا توجد نتائج** | تأكد من أن حقول البيانات الوصفية التي تتوقعها موجودة فعليًا في الملفات المصدرية. |
| **أخطاء الأذونات** | تأكد من أن عملية Java لديها صلاحية قراءة كل من مجلد المستندات ودليل الفهرس. |
| **أخطاء نفاد الذاكرة** | زد حجم heap للـ JVM أو قسّم عملية `add` إلى مجموعات أصغر لمعالجة الملفات. |

## الأسئلة المتكررة

**Q: ما هو فهرسة البيانات الوصفية؟**  
**A:** فهرسة البيانات الوصفية تخزن سمات المستند (المؤلف، العنوان، العلامات المخصصة) في بنية قابلة للبحث، مما يتيح عمليات بحث سريعة دون فحص النص الكامل.

**Q: كيف أحصل على ترخيص مؤقت؟**  
**A:** زر صفحة شراء GroupDocs واتبع الخطوات للحصول على ترخيص تجريبي.

**Q: هل يمكنني فهرسة ملفات PDF باستخدام هذا الإعداد؟**  
**A:** نعم، يدعم GroupDocs.Search ملفات PDF و DOCX و PPT والعديد من الصيغ الأخرى.

**Q: ما هي المشكلات الشائعة عند إضافة المستندات؟**  
**A:** تحقق من صحة مسارات الملفات وتأكد من أن التطبيق يمتلك أذونات القراءة للمجلدات.

**Q: كيف أحسن أداء البحث؟**  
**A:** قم بتحديث فهرسك بانتظام، استخدم الإضافات المتزايدة، واضبط إعدادات ذاكرة JVM.

## الموارد

- **الوثائق:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **مرجع API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **التنزيل:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **مستودع GitHub:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **منتدى الدعم المجاني:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-10-22  
**تم الاختبار مع:** GroupDocs.Search Java 25.4  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)  
- [How to Create Document Index and Add Documents Using the GroupDocs.Search API for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)  
- [Mastering Groupdocs Search Java Index Management Guide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
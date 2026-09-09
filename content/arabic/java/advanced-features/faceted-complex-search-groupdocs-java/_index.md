---
date: '2026-08-26'
description: تعلم كيف تمكنك Boolean operators Java من بناء search index سريع، وإجراء
  content search Java، وتشغيل faceted queries باستخدام GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: تعلم كيف تمكنك Boolean operators Java من بناء search index سريع، وإجراء
  content search Java، وتنفيذ faceted queries باستخدام GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – بناء search index و faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – إنشاء search index & faceted search
type: docs
url: /ar/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# المعاملات البوليانية Java – إنشاء فهرس بحث & بحث موجه

إن تنفيذ تجربة **search experience** قوية في Java قد يبدو مرهقًا، خاصةً عندما تحتاج إلى **create a search index Java** التي تدعم **boolean operators Java** للبحث الموجه والاستعلامات المعقدة. في هذا البرنامج التعليمي سنستعرض إعداد **GroupDocs.Search for Java**، بناء فهرس، إضافة مستندات، وصياغة كل من عمليات البحث الموجه البسيطة والاستعلامات المتعددة المعايير المتقدمة التي تستخدم المنطق البولياني. في النهاية ستتمكن من الاستفادة من عمليات **content search Java**، **filename search Java**، وحتى **update index Java** للحفاظ على تحديث بياناتك.

## إجابات سريعة
- **ما هو البحث الموجه؟** طريقة لتصفية النتائج حسب فئات محددة مسبقًا مثل نوع الملف أو التاريخ.  
- **كيف أنشئ search index Java؟** قم بتهيئة كائن `Index` يشير إلى مجلد وأضف المستندات.  
- **هل يمكنني دمج معايير متعددة باستخدام boolean operators؟** نعم—استخدم استعلامات مبنية على الكائن أو Boolean operators في استعلام نصي.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتطوير؛ الترخيص التجاري يزيل القيود.  
- **ما هو أفضل بيئة تطوير متكاملة (IDE)؟** أي IDE للـ Java (IntelliJ IDEA، Eclipse، NetBeans) يعمل بشكل جيد.

## ما هو “create search index java”؟
إنشاء search index Java يعني بناء بنية تعتمد على القرص تخزن نص المستند والبيانات الوصفية، مما يتيح استرجاعًا فوريًا للمستندات المتطابقة عبر الاستعلامات. يقوم الفهرس بربط المصطلحات بمعرفات المستندات، يدعم عمليات البحث السريعة، ويمكن تحديثه بشكل تدريجي مع تغير الملفات، مما يوفر الأساس لميزات بحث قوية.

## لماذا نستخدم GroupDocs.Search للبحث الموجه والاستعلامات المعقدة؟
يقدم GroupDocs.Search for Java إمكانات faceting مدمجة، ودعم استعلامات Boolean، وفهرسة عالية الأداء يمكنها التعامل مع ما يصل إلى 10 ملايين مستند مع الحفاظ على زمن استجابة الاستعلام أقل من 200 مللي ثانية على عتاد الخادم المعتاد. يوفر مرشحات حقول جاهزة، لغة استعلام غنية، وتوافق كامل مع Java، مما يجعله مثاليًا لسيناريوهات البحث على مستوى المؤسسات.

## المتطلبات المسبقة
- **JDK 8 أو أحدث** مثبت ومُعد في IDE الخاص بك.  
- **Maven** (أو Gradle) لإدارة الاعتمادات.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- إلمام أساسي بمفاهيم OOP في Java وبنية مشروع Maven.

## إعداد GroupDocs.Search for Java

### إعداد Maven
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

### التحميل المباشر
بدلاً من ذلك، قم بتحميل أحدث JAR من صفحة الإصدارات الرسمية:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### الحصول على الترخيص
لإلغاء قفل جميع الوظائف:

1. **نسخة تجريبية مجانية** – مثالية للتطوير والاختبار.  
2. **ترخيص تقييم مؤقت** – يمدد حدود النسخة التجريبية.  
3. **ترخيص تجاري** – يزيل جميع القيود للاستخدام في الإنتاج.

### التهيئة الأساسية والإعداد
فئة `Index` هي المكوّن الأساسي الذي يمثل فهرسًا قابلًا للبحث مخزنًا على القرص. يوضح المقتطف التالي كيفية **create a search index Java** عن طريق إنشاء كائن من فئة `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

مع جاهزية الفهرس، يمكننا الانتقال إلى استعلامات البحث الموجه والمعقدة في العالم الحقيقي.

## كيفية استخدام boolean operators java – بحث موجه بسيط

حمّل الفهرس الخاص بك، أضف المستندات، وأصدر استعلام حقل؛ نمط الخطوتين يتيح لك استرجاع عدد الواجهات والنتائج المصفاة في استدعاء واحد. يمنح هذا النهج المستخدمين طريقة بديهية لتضييق النتائج حسب فئات مثل نوع الملف، المؤلف، أو البيانات الوصفية المخصصة.

### الخطوة 1: إنشاء فهرس
أولاً، وجه `Index` إلى مجلد سيتم تخزين ملفات الفهرس فيه.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### الخطوة 2: إضافة مستندات إلى الفهرس
أخبر GroupDocs.Search بمكان وجود المستندات المصدرية. جميع أنواع الملفات المدعومة (PDF، DOCX، TXT، إلخ) سيتم فهرستها تلقائيًا.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### الخطوة 3: إجراء بحث في حقل المحتوى باستخدام استعلام نصي
استعلام نصي سريع يفلتر حسب حقل `content`. الصياغة `content: Pellentesque` تقصر النتائج على المستندات التي تحتوي على كلمة *Pellentesque* في نصها.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### الخطوة 4: إجراء بحث باستخدام استعلام كائن
توفر الاستعلامات القائمة على الكائن تحكمًا دقيقًا. هنا نبني استعلام كلمة، نغلفه في استعلام حقل، ثم ننفذه.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## كيفية استخدام boolean operators java – بحث استعلام معقد

لتنفيذ استعلام معقد، اجمع بين عدة شروط حقل باستخدام عوامل AND/OR/NOT، ويمكنك اختيارًا تضمين بحث عبارات. يمكنك تحديد كل شرط باستخدام استعلامات حقل، وتضمينها داخل عوامل Boolean، والتحكم في الصلة باستخدام التعزيز (boosting)، مما يتيح لك استرجاع المستندات الأكثر صلة فقط التي تلبي جميع المعايير المطلوبة.

### الخطوة 1: إنشاء فهرس للاستعلامات المعقدة
أعد استخدام نفس بنية المجلد؛ يمكنك مشاركة الفهرس بين السيناريوهات البسيطة والمعقدة.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### الخطوة 2: إجراء بحث باستخدام استعلام نصي
الاستعلام التالي يبحث عن ملفات باسم *lorem* **و** *ipsum* **أو** محتوى يحتوي على أي من العبارتين الدقيقتين.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### الخطوة 3: إجراء بحث باستخدام استعلام كائن
إنشاء استعلام مبني على الكائن يعكس الاستعلام النصي لكنه يوفر أمان النوع ومساعدة IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## تطبيقات عملية للبحث الموجه والمعقد

| السيناريو | كيف يساعد faceting | استعلام مثال |
|-----------|-------------------|--------------|
| **دليل التجارة الإلكترونية** | تصفية حسب الفئة، السعر، العلامة التجارية | `category: Electronics AND price:[100 TO 500]` |
| **مستودع المستندات القانونية** | تضييق حسب رقم القضية، الاختصاص | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **أرشيفات البحث** | دمج المؤلف، سنة النشر، الكلمات المفتاحية | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **الإنترانت المؤسسي** | بحث حسب نوع الملف والقسم | `filetype: pdf AND department: HR` |

## المشكلات الشائعة & استكشاف الأخطاء

كائن `SearchResult` يحتوي على المستندات التي تطابق استعلامًا ويُوفر الوصول إلى درجات الصلة والقطاعات المميزة.  
فئة `CommonFieldNames` تُعرّف أسماء الحقول القياسية مثل `Content` و `FileName` المستخدمة عبر الـ API.

- **نتائج فارغة** – تحقق من أن المستندات قد أضيفت بنجاح (`index.getDocumentCount()` يمكن أن يساعد).  
- **فهرس قديم** – بعد إضافة أو إزالة ملفات، استدعِ `index.update()` لـ **update index java** والحفاظ على تزامن الفهرس.  
- **أسماء حقول غير صحيحة** – استخدم ثوابت `CommonFieldNames` (`Content`، `FileName`، إلخ) لتجنب الأخطاء المطبعية.  
- **عنق زجاجة في الأداء** – للمجموعات الضخمة، فكر في تمكين `index.setCacheSize()` أو استخدام SSD مخصص لمجلد الفهرس.  
- **غياب التمييز** – لـ **highlight search results java**، استرجع القطاعات المتطابقة عبر `SearchResult.getFragments()` (غير معروض هنا لكن متاح في الـ API).  

## الأسئلة المتكررة

**س: هل يمكنني استخدام GroupDocs.Search مع Spring Boot؟**  
**ج:** بالتأكيد. أضف اعتماد Maven، قم بتكوين الفهرس كـ Spring bean، وحقنه أينما احتجت إلى إمكانات البحث.

**س: هل تدعم المكتبة حقول بيانات وصفية مخصصة؟**  
**ج:** نعم – يمكنك إضافة حقول معرفة من قبل المستخدم أثناء الفهرسة ثم إجراء faceting عليها.

**س: ما هو الحد الأقصى لحجم الفهرس؟**  
**ج:** الفهرس القائم على القرص يمكنه التعامل مع ما يصل إلى 10 ملايين مستند؛ فقط تأكد من وجود مساحة تخزين كافية ومراقبة إعدادات الذاكرة المؤقتة.

**س: هل هناك طريقة لترتيب النتائج حسب الصلة؟**  
**ج:** يقوم GroupDocs.Search تلقائيًا بحساب درجات التطابق؛ يمكنك استرجاع الدرجة عبر `SearchResult.getDocument(i).getScore()`.

**س: ماذا يحدث إذا قمت بفهرسة ملفات PDF مشفرة؟**  
**ج:** قدم كلمة المرور عند إضافة المستند: `index.add(filePath, password)`.

## الخلاصة

بحلول الآن يجب أن تكون مرتاحًا لـ **create a search index Java** باستخدام GroupDocs.Search، إضافة المستندات، وصياغة كل من استعلامات البحث الموجه البسيطة والبحث البولياني المتقدم باستخدام **boolean operators java**. هذه القدرات تمكّنك من تقديم تجارب بحث سريعة، دقيقة، وسهلة الاستخدام عبر مجموعة واسعة من التطبيقات—من منصات التجارة الإلكترونية إلى قواعد المعرفة المؤسسية.

هل أنت مستعد للخطوة التالية؟ استكشف الميزات المتقدمة لـ **GroupDocs.Search** مثل **highlighting**، **suggestions**، و **real‑time indexing** لتعزيز قوة البحث في تطبيقك.

---

**آخر تحديث:** 2026-08-26  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [بحث Wildcard Java مع GroupDocs.Search – ميزات متقدمة](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [كيفية تحديث Index Java مع GroupDocs.Search – دليل شامل](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [كيفية تنفيذ بحث نص كامل في Java: إنشاء دليل فهرس مع GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
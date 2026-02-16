---
date: '2026-02-16'
description: تعلم كيفية استخدام عوامل التشغيل البوليانية في Java مع GroupDocs.Search
  لإنشاء فهرس بحث، وإجراء بحث محتوى باستخدام Java واستعلامات متعددة الجوانب، مما يعزز
  الأداء وتجربة المستخدم.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: العوامل البوليانية في جافا – إنشاء فهرس بحث والبحث الفئوي
type: docs
url: /ar/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean Operators Java – إنشاء فهرس بحث وبحث موجه بالواجهات

تنفيذ تجربة **search experience** قوية في Java قد يبدو مرهقًا، خاصةً عندما تحتاج إلى **create a search index Java** يدعم **boolean operators Java** للبحث الموجه والاستعلامات المعقدة. في هذا الدرس سنستعرض إعداد **GroupDocs.Search for Java**، بناء الفهرس، إضافة المستندات، وإنشاء كل من عمليات البحث الموجه البسيطة والاستعلامات المتعددة المعايير المتقدمة التي تستخدم المنطق البولياني. في النهاية ستتمكن من الاستفادة من **content search Java**، **filename search Java**، وحتى عمليات **update index java** للحفاظ على تحديث بياناتك.

## إجابات سريعة
- **What is a faceted search?** طريقة لتصفية النتائج وفقًا لفئات محددة مسبقًا مثل نوع الملف أو التاريخ.  
- **How do I create a search index Java?** قم بتهيئة كائن `Index` يشير إلى مجلد وأضف المستندات.  
- **Can I combine multiple criteria with boolean operators?** نعم—استخدم استعلامات مبنية على الكائنات أو مشغلات بوليان في استعلام نصي.  
- **Do I need a license?** النسخة التجريبية المجانية تكفي للتطوير؛ الترخيص التجاري يزيل القيود.  
- **Which IDE works best?** أي بيئة تطوير Java (IntelliJ IDEA، Eclipse، NetBeans) تعمل بشكل جيد.

## ما هو “create search index java”؟
إنشاء فهرس بحث في Java يعني بناء بنية بيانات قابلة للبحث تخزن بيانات تعريف المستند ومحتواه، مما يتيح استرجاعًا سريعًا بناءً على استعلامات المستخدم. مع GroupDocs.Search، يُخزن الفهرس على القرص، ويمكن تحديثه بشكل تدريجي، ويدعم ميزات متقدمة مثل الواجهات (faceting)، **boolean operators Java**، والمنطق البولياني المعقد.

## لماذا تستخدم GroupDocs.Search للبحث الموجه والاستعلامات المعقدة؟
- **Out‑of‑the‑box faceting** – تصفية حسب الحقول مثل اسم الملف، الحجم، أو بيانات التعريف المخصصة.  
- **Rich query language** – دمج استعلامات النص، العبارة، والحقل باستخدام مشغلات AND/OR/NOT (جوهر **boolean operators java**).  
- **Scalable performance** – يفهرس ملايين المستندات مع الحفاظ على زمن استجابة منخفض.  
- **Pure Java** – لا يعتمد على مكونات أصلية، يعمل على أي منصة تدعم JDK 8+.  
- **Easy index maintenance** – استدعِ `index.update()` لـ **update index java** بعد إضافة أو إزالة الملفات.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

- **JDK 8 أو أحدث** مثبت ومُكوَّن في بيئة التطوير الخاصة بك.  
- **Maven** (أو Gradle) لإدارة الاعتمادات.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- إلمام أساسي بمفاهيم OOP في Java وبنية مشروع Maven.

## إعداد GroupDocs.Search للـ Java

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
بدلاً من ذلك، قم بتحميل أحدث ملف JAR من صفحة الإصدارات الرسمية:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### الحصول على الترخيص
لإلغاء تقييد جميع الوظائف:

1. **Free trial** – مثالية للتطوير والاختبار.  
2. **Temporary evaluation license** – يمدد حدود النسخة التجريبية.  
3. **Commercial license** – يزيل جميع القيود للاستخدام في بيئة الإنتاج.

### التهيئة الأساسية والإعداد
المقتطف التالي يوضح كيفية **create a search index Java** عن طريق إنشاء كائن من فئة `Index`:

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

مع جاهزية الفهرس، يمكننا الانتقال إلى استعلامات موجهة ومعقدة في العالم الحقيقي.

## كيفية استخدام boolean operators java – بحث موجه بسيط

يسمح البحث الموجه للمستخدمين النهائيين بتضييق النتائج عن طريق اختيار قيم من فئات محددة مسبقًا (facets). أدناه شرح خطوة بخطوة.

### الخطوة 1: إنشاء فهرس
أولاً، وجه `Index` إلى مجلد سيُخزن فيه ملفات الفهرس.

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

### الخطوة 3: تنفيذ بحث في حقل المحتوى باستخدام استعلام نصي
استعلام نصي سريع يفلتر حسب حقل `content`. الصيغة `content: Pellentesque` تقصر النتائج على المستندات التي تحتوي على كلمة *Pellentesque* في نصها.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### الخطوة 4: تنفيذ بحث باستخدام استعلام كائن
توفر الاستعلامات القائمة على الكائنات تحكمًا دقيقًا. هنا نقوم بإنشاء استعلام كلمة، نغلفه في استعلام حقل، ثم ننفذه.

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

تجمع الاستعلامات المعقدة بين حقول متعددة، مشغلات بوليان، والبحث عن عبارات. هذا مثالي لسيناريوهات مثل فلاتر التجارة الإلكترونية أو البحث في الوثائق القانونية.

### الخطوة 1: إنشاء فهرس للاستعلامات المعقدة
أعد استخدام نفس بنية المجلد؛ يمكنك مشاركة الفهرس بين السيناريوهات البسيطة والمعقدة.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### الخطوة 2: تنفيذ بحث باستخدام استعلام نصي
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

### الخطوة 3: تنفيذ بحث باستخدام استعلام كائن
إنشاء الاستعلام القائم على الكائن يعكس الاستعلام النصي لكنه يوفر أمان النوع ومساعدة IDE.

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

| السيناريو | كيف يساعد الواجهات | استعلام مثال |
|----------|-------------------|---------------|
| **E‑commerce catalog** | تصفية حسب الفئة، السعر، العلامة التجارية | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | تضييق حسب رقم القضية، الاختصاص | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | دمج المؤلف، سنة النشر، الكلمات المفتاحية | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | بحث حسب نوع الملف والقسم | `filetype: pdf AND department: HR` |

## المشكلات الشائعة & استكشاف الأخطاء

- **Empty results** – تحقق من أن المستندات قد أضيفت بنجاح (`index.getDocumentCount()` يمكن أن يساعد).  
- **Stale index** – بعد إضافة أو إزالة الملفات، استدعِ `index.update()` لـ **update index java** والحفاظ على توافق الفهرس.  
- **Incorrect field names** – استخدم ثوابت `CommonFieldNames` (`Content`, `FileName`, إلخ) لتجنب الأخطاء الإملائية.  
- **Performance bottlenecks** – للمجموعات الضخمة، فكر في تمكين `index.setCacheSize()` أو استخدام SSD مخصص لمجلد الفهرس.  
- **Missing highlights** – للحصول على **highlight search results java**، استرجع القطع المتطابقة عبر `SearchResult.getFragments()` (غير معروض هنا لكن متاح في الـ API).  

## الأسئلة المتكررة

**س: هل يمكنني استخدام GroupDocs.Search مع Spring Boot؟**  
ج: بالتأكيد. أضف اعتماد Maven، قم بتكوين الفهرس كـ Spring bean، وحقنه في أي مكان تحتاج فيه إلى قدرات البحث.

**س: هل تدعم المكتبة حقول بيانات تعريف مخصصة؟**  
ج: نعم – يمكنك إضافة حقول معرفة من قبل المستخدم أثناء الفهرسة ثم إجراء الواجهات (faceting) عليها.

**س: ما هو الحد الأقصى لحجم الفهرس؟**  
ج: الفهرس يعتمد على القرص ويمكنه التعامل مع ملايين المستندات؛ فقط تأكد من وجود مساحة تخزين كافية ومراقبة إعدادات الذاكرة المؤقتة.

**س: هل هناك طريقة لترتيب النتائج حسب الصلة؟**  
ج: يقوم GroupDocs.Search تلقائيًا بحساب درجة التطابق؛ يمكنك استرجاع الدرجة عبر `SearchResult.getDocument(i).getScore()`.

**س: ماذا يحدث إذا قمت بفهرسة ملفات PDF مشفرة؟**  
ج: قدم كلمة المرور عند إضافة المستند: `index.add(filePath, password)`.

## الخلاصة

بحلول الآن يجب أن تكون مرتاحًا في **creating a search index Java** باستخدام GroupDocs.Search، إضافة المستندات، وإنشاء كل من استعلامات الواجهات البسيطة والبحث البولياني المتقدم باستخدام **boolean operators java**. هذه القدرات تمكنك من تقديم تجارب بحث سريعة، دقيقة، وسهلة الاستخدام عبر مجموعة واسعة من التطبيقات—من منصات التجارة الإلكترونية إلى قواعد المعرفة المؤسسية.

هل أنت مستعد للخطوة التالية؟ استكشف الميزات المتقدمة لـ **GroupDocs.Search** مثل **highlighting**، **suggestions**، و **real‑time indexing** لتعزيز قوة البحث في تطبيقك.

---

**آخر تحديث:** 2026-02-16  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs
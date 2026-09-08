---
date: '2026-07-21'
description: يوضح دليل إنشاء استعلام بولياني Java كيفية تنفيذ عمليات البحث البوليانية
  AND، OR، NOT باستخدام GroupDocs.Search for Java، إضافة المستندات إلى الفهرس، وتعزيز
  استرجاع المستندات.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: يوضح دليل إنشاء استعلام بولياني Java خطوة بخطوة كيفية بناء استعلامات
  AND، OR، NOT باستخدام GroupDocs.Search for Java، إضافة المستندات إلى الفهرس، وتحسين
  أداء الاسترجاع.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: إنشاء استعلام بولياني Java – إتقان عمليات البحث البوليانية باستخدام GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'إنشاء استعلام بولياني Java: إتقان عمليات البحث البوليانية باستخدام GroupDocs.Search
  for Java'
type: docs
url: /ar/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# إنشاء استعلام بولياني Java: إتقان عمليات البحث البوليانية مع GroupDocs.Search للـ Java

## إجابات سريعة
- **ما هو استعلام بولياني AND؟** يُرجع فقط المستندات التي تحتوي على *جميع* المصطلحات المحددة.  
- **كيف يختلف OR عن AND؟** OR يطابق المستندات التي تحتوي على *أي* من المصطلحات، موسعًا مجموعة النتائج.  
- **متى يجب استخدام NOT؟** استخدم NOT لتصفية المستندات التي تحتوي على كلمات غير مرغوب فيها.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للاختبار؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** Java 8+ مدعومة؛ يُنصح بـ JDK 11+.

## ما هو **create boolean query java**؟
`create boolean query java` يشير إلى إنشاء استعلام بحث في Java يجمع بين عوامل منطقية مثل AND وOR وNOT باستخدام واجهة برمجة تطبيقات GroupDocs.Search. من خلال تجميع هذه العوامل يمكنك التحكم بدقة في المستندات التي تتطابق، مما يتيح تصفية متقدمة، وضبط الصلة، وسيناريوهات بحث معقدة.

## لماذا تستخدم GroupDocs.Search للـ Java؟
- **أداء عالي** على مجموعات مستندات كبيرة — يمكنه فهرسة والبحث في 500 GB من النص في أقل من دقيقة على خادم عادي.  
- **API غني** يدعم كل من الاستعلامات النصية والاستعلامات القائمة على الكائنات، مما يتيح لك اختيار النمط الذي يناسب بنية تطبيقك.  
- **دعم مدمج للغات** للتجذير، والكلمات الوقفية، والبحث الضبابي عبر أكثر من 30 لغة.  
- **تكامل سهل** مع Maven أو تحميل JAR مباشرة، ويتطلب فقط بضع أسطر من الشفرة للبدء.

## المتطلبات الأساسية
قبل الغوص في التفاصيل، تأكد من أن لديك:
- **GroupDocs.Search for Java** (الإصدار v25.4 أو أحدث) – راجع رابط التحميل أدناه.  
- JDK 8+ مثبت ومُعد في بيئة التطوير المتكاملة الخاصة بك (IntelliJ IDEA، Eclipse، إلخ).  
- معرفة أساسية بـ Java وMaven لإدارة التبعيات.

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

### تحميل مباشر
بدلاً من ذلك، قم بتحميل أحدث JAR من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
ابدأ برخصة تجريبية مجانية لاستكشاف جميع الميزات. للاستخدام في الإنتاج، اشترِ رخصة تجارية لفتح جميع الوظائف.

### التهيئة الأساسية والإعداد
أنشئ مجلد فهرس وقم بإنشاء كائن `Index`:
```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## كيف تنشئ استعلام بولياني java؟
تمثل فئة `Index` مجموعة قابلة للبحث من المستندات المخزنة على القرص. تجمع `BooleanQuery` بين عدة استعلامات فرعية باستخدام عوامل منطقية. تقوم `createAndQuery` و`createOrQuery` و`createNotQuery` بإنشاء استعلامات فرعية AND وOR وNOT على التوالي. قم بتحميل أو إنشاء مثيل `Index`، أضف المستندات، ثم أنشئ كائن `BooleanQuery` باستخدام `createAndQuery` أو `createOrQuery` أو `createNotQuery`. استدعِ `index.search(query)` لاسترجاع المستندات المطابقة. هذا النمط يعمل لكل من السيناريوهات البسيطة والمعقدة ويتطلب فقط ثلاث خطوات منطقية: تهيئة الفهرس، إضافة المستندات، وتنفيذ الاستعلام.

## بحث بولياني AND

### نظرة عامة
يقوم استعلام AND بتضييق النتائج، مما يحسن الصلة عندما تحتاج إلى مستندات تطابق معايير متعددة.

### خطوات التنفيذ
1. **تهيئة الفهرس** – يوضح هذا أيضًا **إضافة مستندات إلى الفهرس** لسيناريو AND.
   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```
2. **فهرسة المستندات**
   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```
3. **إجراء بحث استعلام نصي** – باستخدام صيغة السلسلة العادية.
   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```
4. **إجراء بحث استعلام كائن** – مفيد عند بناء الاستعلامات برمجيًا (**search with and java**).
   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## بحث بولياني OR

### نظرة عامة
يُعد استعلام OR مثاليًا للبحث الاستكشافي حيث تريد التقاط المستندات التي تحتوي على كلمة مفتاحية واحدة على الأقل من عدة كلمات (**search with or java**).

### خطوات التنفيذ
1. **تهيئة الفهرس**
   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```
2. **فهرسة المستندات**
   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```
3. **إجراء بحث استعلام نصي**
   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```
4. **إجراء بحث استعلام كائن**
   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## بحث بولياني NOT

### نظرة عامة
يساعدك استعلام NOT على حذف المستندات غير ذات الصلة، مثل تصفية اسم علامة تجارية لمنافس (**boolean search examples java**).

### خطوات التنفيذ
1. **تهيئة الفهرس**
   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```
2. **فهرسة المستندات**
   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```
3. **إجراء بحث استعلام نصي**
   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```
4. **إجراء بحث استعلام كائن**
   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## استعلامات بوليانية معقدة

### نظرة عامة
تتيح لك الاستعلامات المعقدة نمذجة سيناريوهات البحث الواقعية، مثل “العثور على مقالات رياضية إيجابية مع استبعاد أي ذكر لرياضيين محددين”.

### خطوات التنفيذ
1. **تهيئة الفهرس**
   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```
2. **فهرسة المستندات**
   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```
3. **إجراء بحث استعلام نصي**
   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```
4. **إجراء بحث استعلام كائن**
   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## تطبيقات عملية لاستعلامات **java boolean and or**
- **أنظمة إدارة المستندات** – تحديد العقود التي تحتوي على كل من “confidential” **AND** “renewal”.  
- **البحث القانوني** – تصفية القوانين القضائية باستخدام **AND**/ **OR** مع استبعاد القوانين القديمة باستخدام **NOT**.  
- **دعم العملاء** – استرجاع التذاكر التي تذكر “login” **AND** “error” ولكن ليس “resolved”.  
- **تنسيق المحتوى** – جمع مقالات المدونة حول “cloud” **OR** “serverless” للنشرة الإخبارية.

## الأخطاء الشائعة & استكشاف الأخطاء وإصلاحها
- **عدم تحديث الفهرس** – بعد إضافة مستندات جديدة، استدعِ `index.update()` لضمان إمكانية البحث فيها.  
- **مسافات غير صحيحة حول العوامل** – تتوقع GroupDocs.Search وجود مسافات حول العوامل (`AND`, `OR`, `NOT`).  
- **حساسية الأحرف** – الاستعلامات غير حساسة لحالة الأحرف بشكل افتراضي، لكن المحللات المخصصة قد تؤثر على ذلك.  
- **مجموعات نتائج كبيرة** – استخدم التجزئة (`search(query, 0, 100)`) لتجنب استنزاف الذاكرة.  

## الأسئلة المتكررة

**س: هل يمكنني دمج أكثر من مصطلحين في استعلام AND؟**  
ج: بالتأكيد. يمكنك ربط عدة كائنات `createWordQuery` باستخدام `createAndQuery`، أو ببساطة كتابة `"term1 AND term2 AND term3"` في استعلام النص.

**س: هل يدعم GroupDocs.Search البحث باستخدام الأحرف البديلة (wildcard) أو البحث الضبابي؟**  
ج: نعم. أضف `*` للبحث بالأحرف البديلة (مثال: `promot*`) أو استخدم `~` للبحث الضبابي (مثال: `comfort~`).

**س: كيف يمكنني تحديد البحث إلى أنواع ملفات معينة؟**  
`FileTypeQuery` يحد من نتائج البحث إلى تنسيقات ملفات محددة مثل PDF أو DOCX.  
ج: استخدم الفئة `FileTypeQuery` لتقييد النتائج إلى PDFs، DOCX، إلخ، وادمجها مع استعلامك البولياني.

**س: ما هي أفضل طريقة لمراقبة أداء الفهرسة؟**  
ج: فعّل المسجل المدمج (`index.getLogger().setLevel(Level.INFO)`) وراجع مقاييس الوقت بعد كل عملية `add`.

**س: هل هناك طريقة لتعزيز صلة بعض المصطلحات؟**  
`BoostQuery` يعزز درجة الصلة للمصطلحات المحددة في استعلام البحث.  
ج: نعم. غلف الكلمات المهمة بـ `BoostQuery` لزيادة وزنها في خوارزمية التقييم.

---

**آخر تحديث:** 2026-07-21  
**تم الاختبار مع:** GroupDocs.Search 25.4 (Java)  
**المؤلف:** GroupDocs

## دروس ذات صلة
- [مشغلات بوليانية Java – إنشاء فهرس بحث والبحث المتعدد الأوجه](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [إتقان GroupDocs.Search Java&#58; بحث مستندات فعال وإدارة الفهرس](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - إتقان GroupDocs.Search Java – إنشاء وإدارة فهرس البحث](/search/java/indexing/groupdocs-search-java-create-index-guide/)
---
date: '2026-01-29'
description: تعلم كيفية تنفيذ استعلامات بوليانية AND OR في Java باستخدام GroupDocs.Search
  for Java، وإضافة المستندات إلى الفهرس وتعزيز استرجاع المستندات.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'جافا بوليان AND OR: إتقان عمليات البحث المنطقية مع GroupDocs.Search لجافا'
type: docs
url: /ar/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: إتقان عمليات البحث البوليانية مع GroupDocs.Search للغة Java

البحث في مجموعات ضخمة من المستندات قد يشعر كأنه العثور على إبرة في كومة قش. باستخدام استعلامات **java boolean and or** يمكنك إخبار المحرك بالضبط ما تحتاجه — مستندات تحتوي على *كلا* المصطلحين، *أي* منهما، أو *استبعاد* الكلمات غير المرغوب فيها. في هذا الدليل سنستعرض إعداد **GroupDocs.Search للغة Java**، إضافة المستندات إلى الفهرس، وصياغة استعلامات بوليانية قوية تعزز سير عمل **document retrieval java** الخاص بك.

## إجابات سريعة
- **ما هو استعلام boolean AND؟** يُرجع فقط المستندات التي تحتوي على *جميع* المصطلحات المحددة.  
- **كيف يختلف OR عن AND؟** يطابق OR المستندات التي تحتوي على *أي* من المصطلحات، موسعًا مجموعة النتائج.  
- **متى يجب استخدام NOT؟** استخدم NOT لتصفية المستندات التي تحتوي على كلمات غير مرغوب فيها.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للاختبار؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** تدعم Java 8+؛ يُنصح باستخدام JDK 11+.

## ما هو **java boolean and or**؟
استعلام **java boolean and or** يجمع بين عوامل منطقية (AND، OR، NOT) لتقليل نتائج البحث. من خلال هيكلة الاستعلامات تخبر GroupDocs.Search بالضبط كيف ترتبط المصطلحات ببعضها، مما يمنحك تحكمًا دقيقًا في عملية الاسترجاع.

## لماذا تستخدم GroupDocs.Search للغة Java؟
- **أداء عالي** على مجموعات مستندات ضخمة.  
- **API غني** يدعم الاستعلامات النصية والكائنية على حدٍ سواء.  
- **دعم مدمج للغات** لتجذير الكلمات، الكلمات الشائعة، والبحث الضبابي.  
- **تكامل سهل** مع Maven أو تحميل JAR مباشرة.

## المتطلبات المسبقة
قبل المتابعة، تأكد من وجود ما يلي:

- **GroupDocs.Search للغة Java** (الإصدار 25.4 أو أحدث) – راجع رابط التحميل أدناه.  
- JDK 8+ مثبت ومُعد في بيئة التطوير المتكاملة (IntelliJ IDEA، Eclipse، إلخ).  
- معرفة أساسية بـ Java وMaven لإدارة الاعتمادات.  

## إعداد GroupDocs.Search للغة Java

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
بدلاً من ذلك، حمّل أحدث JAR من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
ابدأ بترخيص تجريبي مجاني لاستكشاف جميع الميزات. للاستخدام الإنتاجي، اشترِ ترخيصًا تجاريًا لفتح كامل الوظائف.

### التهيئة الأساسية والإعداد
أنشئ مجلد فهرس واستدعِ كائن `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: تنفيذ عمليات البحث البوليانية

سنعرض أدناه استعلامات **AND**، **OR**، **NOT**، والاستعلامات **المعقدة**. كل قسم يوضح كلًا من استعلام النص العادي والاستعلام الكائني المكافئ، لتختار النمط الأنسب لقاعدة شفرتك.

### بحث Boolean AND
اجمع المصطلحات باستخدام **AND** لاسترجاع فقط المستندات التي تحتوي على *جميع* الكلمات المفتاحية.

#### نظرة عامة
استعلام AND يضيق النتائج، محسنًا الصلة عندما تحتاج إلى مستندات تطابق عدة معايير.

#### خطوات التنفيذ

1. **تهيئة الفهرس** – يوضح أيضًا **add documents to index** لسيناريو AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **فهرسة المستندات**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **تنفيذ بحث استعلام نصي** – باستخدام صيغة السلسلة النصية البسيطة.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **تنفيذ بحث استعلام كائني** – مفيد عند بناء الاستعلامات برمجيًا (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### بحث Boolean OR
استخدم **OR** لتوسيع النتائج، مطابقة أي من المصطلحات المقدمة.

#### نظرة عامة
استعلام OR مثالي للبحث الاستكشافي حيث تريد التقاط المستندات التي تحتوي على كلمة واحدة على الأقل من عدة كلمات مفتاحية (**search with or java**).

#### خطوات التنفيذ

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

3. **تنفيذ بحث استعلام نصي**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **تنفيذ بحث استعلام كائني**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### بحث Boolean NOT
استبعد المصطلحات غير المرغوب فيها باستخدام **NOT** لتصفية الضوضاء من النتائج.

#### نظرة عامة
استعلام NOT يساعدك على حذف المستندات غير ذات الصلة، مثل استبعاد اسم علامة تجارية لمنافس (**boolean search examples java**).

#### خطوات التنفيذ

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

3. **تنفيذ بحث استعلام نصي**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **تنفيذ بحث استعلام كائني**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### استعلامات بوليانية معقدة
اجمع بين **AND**، **OR**، و**NOT** لتصميم منطق بحث معقد يلبي احتياجات استرجاع دقيقة للغاية.

#### نظرة عامة
الاستعلامات المعقدة تسمح بنمذجة سيناريوهات بحث واقعية، مثل “العثور على مقالات رياضية إيجابية مع استبعاد أي ذكر لرياضيين محددين”.

#### خطوات التنفيذ

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

3. **تنفيذ بحث استعلام نصي**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **تنفيذ بحث استعلام كائني**

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

## تطبيقات عملية لاستعلامات java boolean and or
- **أنظمة إدارة المستندات** – تحديد العقود التي تحتوي على كل من “confidential” **AND** “renewal”.  
- **البحث القانوني** – تصفية القوانين القضائية باستخدام **AND**/**OR** مع استبعاد التشريعات القديمة عبر **NOT**.  
- **دعم العملاء** – استرجاع التذاكر التي تذكر “login” **AND** “error” لكن ليس “resolved”.  
- **تنسيق المحتوى** – جمع مقالات المدونة حول “cloud” **OR** “serverless” للنشرة الإخبارية.

## الأخطاء الشائعة & استكشاف الأخطاء وإصلاحها
- **عدم تحديث الفهرس** – بعد إضافة مستندات جديدة، استدعِ `index.update()` لضمان إمكانية البحث فيها.  
- **مسافات غير صحيحة حول العامل** – يتوقع GroupDocs.Search وجود مسافات حول العوامل (`AND`, `OR`, `NOT`).  
- **حساسية الأحرف** – الاستعلامات غير حساسة لحالة الأحرف بشكل افتراضي، لكن المحللات المخصصة قد تغير ذلك.  
- **مجموعات نتائج كبيرة** – استخدم التجزئة (`search(query, 0, 100)`) لتجنب استهلاك الذاكرة.

## الأسئلة المتكررة

**س: هل يمكنني دمج أكثر من مصطلحين في استعلام AND؟**  
ج: بالتأكيد. يمكنك ربط عدة كائنات `createWordQuery` باستخدام `createAndQuery`، أو ببساطة كتابة `"term1 AND term2 AND term3"` في استعلام النص.

**س: هل يدعم GroupDocs.Search البحث باستخدام البدل أو البحث الضبابي؟**  
ج: نعم. أضف `*` للبدل (مثال: `promot*`) أو استخدم `~` للبحث الضبابي (مثال: `comfort~`).

**س: كيف يمكنني حصر البحث على أنواع ملفات معينة؟**  
ج: استخدم فئة `FileTypeQuery` لتقييد النتائج إلى PDFs، DOCX، إلخ، وادمجها مع استعلامك البولياني.

**س: ما هي أفضل طريقة لمراقبة أداء الفهرسة؟**  
ج: فعّل السجل المدمج (`index.getLogger().setLevel(Level.INFO)`) وراجع مقاييس الوقت بعد كل عملية `add`.

**س: هل هناك طريقة لتعزيز صلة بعض المصطلحات؟**  
ج: نعم. غلف الكلمات المهمة بـ `BoostQuery` لزيادة وزنها في خوارزمية التقييم.

---

**آخر تحديث:** 2026-01-29  
**تم الاختبار مع:** GroupDocs.Search 25.4 (Java)  
**المؤلف:** GroupDocs
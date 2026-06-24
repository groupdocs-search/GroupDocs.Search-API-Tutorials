---
date: '2026-05-28'
description: تعلم كيفية البحث في المستندات بكفاءة باستخدام GroupDocs.Search for Java،
  بما في ذلك البحث الضبابي Java وكيفية إنشاء فهرس للبحث النصي الكامل.
keywords:
- how to search documents
- how to create index
- fuzzy search java
- java full text search
- implement fuzzy matching
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search documents efficiently with GroupDocs.Search for
    Java, including fuzzy search Java and how to create index for full‑text search.
  headline: How to Search Documents Using GroupDocs.Search Java
  type: TechArticle
- description: Learn how to search documents efficiently with GroupDocs.Search for
    Java, including fuzzy search Java and how to create index for full‑text search.
  name: How to Search Documents Using GroupDocs.Search Java
  steps:
  - name: '**Legal Document Management:** Locate clauses or parties across thousands
      of contracts in seconds.'
    text: '**Legal Document Management:** Locate clauses or parties across thousands
      of contracts in seconds.'
  - name: '**Academic Research:** Retrieve relevant papers even if the search term
      is misspelled.'
    text: '**Academic Research:** Retrieve relevant papers even if the search term
      is misspelled.'
  - name: '**Enterprise Content Management:** Power internal portals with fast, typo‑tolerant
      search across reports, emails, and presentations.'
    text: '**Enterprise Content Management:** Power internal portals with fast, typo‑tolerant
      search across reports, emails, and presentations.'
  type: HowTo
- questions:
  - answer: Fuzzy search Java enables approximate string matching, allowing queries
      to return results despite typos or alternate spellings, which improves end‑user
      experience.
    question: What is fuzzy search Java and why is it useful?
  - answer: Call `index.add("new/files/folder")` again; the library intelligently
      merges new content without rebuilding the entire index.
    question: How do I update my index after adding new files?
  - answer: Yes—provide the password in the `DocumentLoadOptions` when adding the
      file, and the engine will decrypt and index the content.
    question: Can GroupDocs.Search handle password‑protected PDFs?
  - answer: The library scales to millions of files; performance depends on hardware
      and storage, not a hard‑coded limit.
    question: Is there a limit to the number of documents I can index?
  - answer: Visit the official documentation for deeper topics like custom analyzers
      and result ranking.
    question: Where can I find more advanced examples?
  type: FAQPage
title: كيفية البحث في المستندات باستخدام GroupDocs.Search Java
type: docs
url: /ar/java/searching/groupdocs-search-java-fuzzy-document-indexing/
weight: 1
---

# كيفية البحث في المستندات باستخدام GroupDocs.Search Java

في تطبيقات المؤسسات الحديثة، **كيفية البحث في المستندات** بسرعة ودقة تُعد متطلبًا حاسمًا. سواء كنت تتعامل مع العقود أو التقارير أو أي مستودع مستندات كبير، يوفر GroupDocs.Search for Java محرك بحث نص كامل قوي مع مطابقة غير دقيقة مدمجة. يشرح هذا البرنامج التعليمي كيفية إعداد المكتبة، إنشاء الفهرس، إضافة المستندات، تكوين البحث غير الدقيق في Java، واسترجاع النتائج—كل ذلك بشرح واضح ومحادث.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** تثبيت مكتبة GroupDocs.Search Java عبر Maven أو تنزيلها مباشرة.  
- **كيف أنشئ فهرسًا؟** إنشاء كائن `Index` يشير إلى مجلد على القرص؛ المكتبة تبني الهيكل القابل للبحث تلقائيًا.  
- **هل يمكنني البحث مع الأخطاء الإملائية؟** نعم—قم بتمكين البحث غير الدقيق لمطابقة المصطلحات التي تحتوي على أخطاء إملائية أو اختلافات طفيفة.  
- **كيف أضيف مستندات؟** استخدم طريقة `add` على كائن `Index`، مع تمرير المجلد الذي يحتوي على ملفاتك.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أعلى مدعومة.

## ما هو “كيفية البحث في المستندات” في سياق GroupDocs.Search؟
**“كيفية البحث في المستندات”** تشير إلى عملية بناء فهرس قابل للبحث وإصدار استعلامات تُعيد الملفات المتطابقة، مع إمكانية استخدام المنطق غير الدقيق لتحمل الأخطاء الإملائية. يتعامل GroupDocs.Search مع التجزئة والفهرسة والترتيب في الخلفية، بحيث يمكنك التركيز على منطق الأعمال.

## لماذا تستخدم GroupDocs.Search للـ Java؟
يدعم GroupDocs.Search **أكثر من 30 تنسيق ملف** (بما في ذلك DOCX، PDF، TXT، HTML، و XLSX) ويمكنه فهرسة **مستندات متعددة المئات من الصفحات** دون تحميل الملف بالكامل في الذاكرة، مما يوفر استجابات استعلام بأقل من ثانية على عتاد الخادم المعتاد. تحسين البحث غير الدقيق يحسن تجربة المستخدم عن طريق إرجاع نتائج ذات صلة حتى عندما تحتوي الاستعلامات على أخطاء إملائية.

## المتطلبات المسبقة
- **Java Development Kit (JDK):** الإصدار 8 أو أحدث.  
- **IDE:** IntelliJ IDEA، Eclipse، أو أي محرر متوافق مع Java.  
- **مكتبة GroupDocs.Search للـ Java:** أضفها عبر Maven (مستحسن) أو قم بتنزيل ملف JAR.

## كيفية إعداد GroupDocs.Search للـ Java؟
لبدء العمل، أضف تبعية GroupDocs.Search إلى ملف البناء الخاص بك، تأكد من أن عنوان URL للمستودع قابل للوصول، وتحقق من أن نسخة JDK تلبي الحد الأدنى المطلوب. بعد حل المكتبة، يمكنك استيراد فصولها في الكود وإنشاء مجلد فهرس على القرص حيث سيتم تخزين جميع البيانات القابلة للبحث.

### إعداد Maven
أضف المستودع والتبعية إلى ملف `pom.xml` الخاص بك تمامًا كما هو موضح في الدليل الأصلي.

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
بدلاً من ذلك، احصل على ملف JAR من صفحة الإصدار الرسمية:

[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

[GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)

## كيفية إنشاء فهرس؟
أنشئ مجلد فهرس دائم حيث يخزن GroupDocs.Search البيانات المجزأة. حمّل فهرسك الأول بسطر واحد من الكود—`new Index("path/to/indexFolder")`. فئة `Index` هي المكوّن الأساسي الذي يمثل مجموعة قابلة للبحث من المستندات في الذاكرة وعلى القرص.

```java
   import com.groupdocs.search.*;

   String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/SearchResults";
   Index index = new Index(indexFolder);
   ```

## كيفية إضافة مستندات إلى الفهرس؟
استخدم طريقة `add` لكائن `Index` لتحديد مجلد يحتوي على ملفات المصدر الخاصة بك. سيقوم المحرك بمسح الصيغ المدعومة بشكل متكرر، استخراج المحتوى النصي، وتحديث الهياكل الداخلية. هذه الدعوة الواحدة تتعامل مع دفعات كبيرة بكفاءة، مما يلغي الحاجة إلى معالجة الملفات يدويًا واحدةً تلو الأخرى.

```java
   String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentFolder);
   ```

## كيفية تكوين البحث غير الدقيق في Java؟
تحدد فئة `FuzzySearchOptions` معلمات مثل مسافة التحرير وطول البادئة التي تتحكم في مدى تحمل البحث للأخطاء الإملائية. يجمع كائن `SearchOptions` جميع إعدادات وقت البحث، بما في ذلك خيارات البحث غير الدقيق، حدود النتائج، وتفضيلات التمييز. قم بتمكين المطابقة غير الدقيقة عن طريق تعيين `FuzzySearchOptions` على كائن `SearchOptions`. هذا يخبر المحرك بأخذ المصطلحات ضمن مسافة تحرير قابلة للتكوين في الاعتبار، مما يجعل عمليات البحث تتحمل الأخطاء الإملائية.

```java
  String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/SearchResults";
  Index index = new Index(indexFolder);
  ```

## كيفية تنفيذ عملية بحث؟
استدعِ طريقة `search` على كائن `Index`، مع توفير سلسلة الاستعلام وإعدادات `SearchOptions` المكوّنة. يعالج المحرك الطلب، يطبق المطابقة غير الدقيقة إذا تم تمكينها، ويرتب النتائج بناءً على درجات الصلة. تكتمل العملية بسرعة حتى على فهارس كبيرة لأن البحث يتم على هياكل الرموز المُنشأة مسبقًا. تُعيد الطريقة مجموعة `SearchResult` التي تحتوي على المستندات المتطابقة، عدد النتائج، والقطع المميزة.

```java
  String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
  index.add(documentFolder);
  ```

## كيفية معالجة وعرض نتائج البحث؟
`SearchResult` هي مجموعة تحتفظ بكائنات `SearchResultItem` الفردية، كل منها يصف مستندًا متطابقًا، عدد النتائج، والقطع المميزة. قم بالتكرار على عناصر `SearchResult` واطبع مسار كل مستند، عدد مرات الظهور، والعبارات المتطابقة. يتيح لك هذا الحلقة البسيطة بناء جداول واجهة المستخدم، سجلات، أو استجابات API تُظهر بالضبط لماذا تم مطابقة المستند.

```java
  import com.groupdocs.search.options.*;

  SearchOptions options = new SearchOptions();
  options.getFuzzySearch().setEnabled(true);
  options.getFuzzySearch().setFuzzyAlgorithm(new TableDiscreteFunction(3));
  ```

## تطبيقات عملية
سيناريوهات واقعية حيث **كيفية البحث في المستندات** مهمة:
1. **إدارة المستندات القانونية:** العثور على البنود أو الأطراف عبر آلاف العقود في ثوانٍ.  
2. **البحث الأكاديمي:** استرجاع الأوراق ذات الصلة حتى إذا كان مصطلح البحث مكتوبًا بشكل خاطئ.  
3. **إدارة محتوى المؤسسة:** تمكين البوابات الداخلية من بحث سريع يتحمل الأخطاء الإملائية عبر التقارير، البريد الإلكتروني، والعروض التقديمية.

## اعتبارات الأداء
- **تحديث الفهرس:** أعد تشغيل `add` أو `update` كلما تغيرت ملفات المصدر للحفاظ على حداثة النتائج.  
- **إدارة الذاكرة:** يقوم GroupDocs.Search ببث الملفات الكبيرة، لذا يبقى استهلاك الذاكرة منخفضًا حتى لملفات PDF ذات 500 صفحة.  
- **الفهرسة المجزأة:** قسّم مجموعات البيانات الضخمة إلى مجلدات فهرس متعددة لتوازي المعالجة وتحسين زمن استجابة الاستعلام.

## الأسئلة المتكررة
**س: ما هو البحث غير الدقيق في Java ولماذا هو مفيد؟**  
ج: يتيح البحث غير الدقيق في Java مطابقة تقريبية للسلاسل، مما يسمح للاستعلامات بإرجاع نتائج رغم الأخطاء الإملائية أو التهجئات البديلة، وهو ما يحسن تجربة المستخدم النهائي.

**س: كيف أقوم بتحديث فهرسي بعد إضافة ملفات جديدة؟**  
ج: استدعِ `index.add("new/files/folder")` مرة أخرى؛ تقوم المكتبة بدمج المحتوى الجديد بذكاء دون إعادة بناء الفهرس بالكامل.

**س: هل يمكن لـ GroupDocs.Search التعامل مع ملفات PDF محمية بكلمة مرور؟**  
ج: نعم—قدّم كلمة المرور في `DocumentLoadOptions` عند إضافة الملف، وسيقوم المحرك بفك التشفير وفهرسة المحتوى.

**س: هل هناك حد لعدد المستندات التي يمكنني فهرستها؟**  
ج: المكتبة تتوسع لتشمل ملايين الملفات؛ الأداء يعتمد على العتاد والتخزين، وليس هناك حد ثابت مبرمج.

**س: أين يمكنني العثور على أمثلة أكثر تقدماً؟**  
ج: زر الوثائق الرسمية لمواضيع أعمق مثل المحللات المخصصة وترتيب النتائج.

## الخلاصة
أنت الآن تعرف **كيفية البحث في المستندات** باستخدام GroupDocs.Search للـ Java، من إنشاء الفهرس إلى تمكين البحث غير الدقيق في Java ومعالجة النتائج. نفّذ هذه الخطوات لتقديم تجارب بحث سريعة تتحمل الأخطاء الإملائية في أي تطبيق مبني على Java.

---

**Last Updated:** 2026-05-28  
**Tested With:** GroupDocs.Search 23.10 for Java  
**Author:** GroupDocs  

---

```java
  String query = "water OR \"Lorem ipsum\"";
  SearchResult result = index.search(query, options);
  ```

```java
  for (int i = 0; i < result.getDocumentCount(); i++) {
      FoundDocument document = result.getFoundDocument(i);
      System.out.println("\tDocument: " + document.getDocumentInfo().getFilePath());
      System.out.println("\tOccurrences: " + document.getOccurrenceCount());

      for (FoundDocumentField field : document.getFoundFields()) {
          System.out.println("\t\tField: " + field.getFieldName());
          if (field.getTerms() != null) {
              for (int k = 0; k < field.getTerms().length; k++) {
                  System.out.println("\t\t\t" + field.getTerms()[k] + " - " + field.getTermsOccurrences()[k]);
              }
          }
      }
  }
  ```

## دروس ذات صلة

- [إنشاء فهرس مستند باستخدام GroupDocs.Search للـ Java](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [تنفيذ بحث نص كامل في Java باستخدام GroupDocs.Search: دليل شامل](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [كيفية إضافة مستندات إلى الفهرس مع فهرسة البيانات الوصفية في Java باستخدام GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
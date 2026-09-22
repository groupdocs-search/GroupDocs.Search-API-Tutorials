---
date: '2026-09-21'
description: تعلم كيفية إنشاء فهرس بحث نص كامل Java باستخدام GroupDocs.Search، وإضافة
  المستندات، وتفعيل دعم المتجانسات الصوتية للحصول على نتائج أكثر دقة.
keywords:
- java full text search
- homophone search java
- GroupDocs.Search Java
- document indexing java
- search index java
lastmod: '2026-09-21'
og_description: اكتشف كيفية إنشاء فهرس بحث نص كامل Java مع GroupDocs.Search، وإضافة
  المستندات، وتفعيل دعم المتجانسات الصوتية للحصول على عمليات بحث أسرع وأكثر دقة.
og_image_alt: Illustration of a Java full text search index with homophone support
og_title: كيفية بناء فهرس بحث نص كامل Java مع homophones
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  headline: How to build a java full text search index with homophones
  type: TechArticle
- description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  name: How to build a java full text search index with homophones
  steps:
  - name: '**Install via Maven** or download directly from the provided links.'
    text: '**Install via Maven** or download directly from the provided links.'
  - name: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
    text: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
  - name: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
    text: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
  - name: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
    text: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
  - name: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
    text: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
  type: HowTo
- questions:
  - answer: A data structure that enables fast full‑text search across documents.
    question: What is a search index?
  - answer: It improves recall by matching words that sound alike, e.g., “mail” vs.
      “male”.
    question: Why use homophone recognition?
  - answer: GroupDocs.Search for Java (v25.4).
    question: Which library provides this in Java?
  - answer: A free trial works for evaluation; a permanent license is required for
      production.
    question: Do I need a license?
  - answer: JDK 8 or higher.
    question: What Java version is required?
  type: FAQPage
tags:
- java full text search
- homophone search
- GroupDocs.Search
- document indexing
- search index
title: كيفية بناء فهرس بحث نص كامل Java مع homophones
type: docs
url: /ar/java/document-management/groupdocs-search-java-homophone-document-management-guide/
weight: 1
---

# كيفية بناء فهرس بحث نص كامل بجافا مع الكلمات المتجانسة

في هذا الدليل ستتعلم كيفية بناء فهرس **java full text search** باستخدام GroupDocs.Search، وإضافة مستندات إليه، وتمكين دعم الكلمات المتجانسة بحيث تفهم عمليات البحث الكلمات التي تُنطق بشكل مشابه. بنهاية البرنامج التعليمي ستحصل على فهرس سريع، واعٍ للغة يمكن الاستعلام عنه خلال مللي ثانية، مما يجعل تطبيقاتك أكثر سهولة للمستخدم ودقة.

## إجابات سريعة
- **ما هو فهرس البحث؟** بنية بيانات تمكّن من البحث النصي الكامل السريع عبر المستندات.  
- **لماذا نستخدم التعرف على الكلمات المتجانسة؟** يحسن الاسترجاع عن طريق مطابقة الكلمات التي تُنطق بشكل مشابه، مثل “mail” مقابل “male”.  
- **أي مكتبة توفر ذلك في جافا؟** GroupDocs.Search for Java (v25.4).  
- **هل أحتاج إلى ترخيص؟** تجربة مجانية تكفي للتقييم؛ يلزم ترخيص دائم للإنتاج.  
- **ما نسخة جافا المطلوبة؟** JDK 8 أو أعلى.

## ما هو بحث النص الكامل بجافا؟
`java full text search` هو عملية فهرسة محتوى المستند بحيث يمكنك الاستعلام عن النص بسرعة واسترجاع الملفات ذات الصلة في الوقت الحقيقي. يخزن الفهرس المصطلحات المُجزأة، المواقع، والبيانات الوصفية، مما يسمح باستجابات بحث أقل من الثانية حتى على مجموعات كبيرة.

## لماذا نستخدم GroupDocs.Search لجافا؟
GroupDocs.Search يدعم **أكثر من 50 تنسيق ملف**—بما في ذلك PDF وDOCX وXLSX وPPTX وHTML—مع توفير قاموس كلمات متجانسة مدمج يزيد الاسترجاع حتى **30 %** للمصطلحات الغامضة. الـ API يُجرد تفاصيل الفهرسة منخفضة المستوى، مما يتيح لك التركيز على منطق الأعمال. كما يوفر تكاملًا سهلاً مع مشاريع Maven ووثائق واضحة لتطوير سريع.

## المتطلبات المسبقة

قبل الغوص في الشيفرة، تأكد من أن لديك ما يلي:

- **GroupDocs.Search for Java** (متاح عبر Maven أو التحميل المباشر).  
- **JDK متوافق** (8 أو أحدث).  
- بيئة تطوير متكاملة مثل **IntelliJ IDEA** أو **Eclipse**.  
- معرفة أساسية بجافا وMaven.

### المكتبات والاعتمادات المطلوبة
ستحتاج إلى GroupDocs.Search لجافا. أدرجه باستخدام Maven أو قم بتحميله مباشرة.

**تثبيت Maven:**  
أضف ما يلي إلى ملف `pom.xml` الخاص بك:

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

**تحميل مباشر:**  
بدلاً من ذلك، قم بتحميل أحدث نسخة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### متطلبات إعداد البيئة
تأكد من تثبيت JDK متوافق (JDK 8 أو أعلى) وبيئة تطوير مثل IntelliJ IDEA أو Eclipse مُعدّة على جهازك.

### المتطلبات المعرفية
الإلمام بمفاهيم برمجة جافا والخبرة في استخدام Maven لإدارة الاعتمادات سيكون مفيدًا. كما أن الفهم الأساسي لفهرسة المستندات وخوارزميات البحث يمكن أن يساعد أيضًا.

## إعداد GroupDocs.Search لجافا

بمجرد ترتيب المتطلبات المسبقة، يصبح إعداد GroupDocs.Search بسيطًا:

1. **التثبيت عبر Maven** أو التحميل مباشرة من الروابط المقدمة.  
2. **الحصول على ترخيص:** يمكنك البدء بتجربة مجانية أو الحصول على ترخيص مؤقت بزيارة [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).  
3. **تهيئة المكتبة:** المقتطف أدناه يوضح الحد الأدنى من الشيفرة المطلوبة للبدء في استخدام GroupDocs.Search.

```java
import com.groupdocs.search.*;

public class SetupExample {
    public static void main(String[] args) {
        // Define the directory for storing index files.
        String indexFolder = "path/to/index/directory";
        
        // Initialize an Index instance.
        Index index = new Index(indexFolder);
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## دليل التنفيذ

الآن بعد أن أصبحت البيئة جاهزة، دعنا نستكشف الميزات الأساسية التي ستحتاجها **لإنشاء فهرس بحث نص كامل بجافا** وإدارة الكلمات المتجانسة.

### إنشاء وإدارة فهرس
#### نظرة عامة
إنشاء فهرس بحث هو الخطوة الأولى في إدارة المستندات بفعالية. يتيح ذلك استرجاعًا سريعًا للمعلومات بناءً على محتوى مستندك.

#### خطوات إنشاء فهرس
**الخطوة 1:** حدد الدليل لملفات الفهرس الخاصة بك.

```java
String indexFolder = "YOUR_INDEX_DIRECTORY";
Index index = new Index(indexFolder);
```

*فئة `Index` تمثل الحاوية القابلة للبحث التي تحتفظ بالمصطلحات المُجزأة والبيانات الوصفية لكل مستند، وتوفر البنية الأساسية التي تمكّن من تنفيذ الاستعلامات بسرعة وتخزين معلومات المستند بفعالية عبر الفهرس بأكمله.*

**الخطوة 2:** أضف المستندات من مجلد محدد إلى هذا الفهرس.

```java
String documentsFolder = "YOUR_DOCUMENTS_SOURCE_DIRECTORY";
index.add(documentsFolder);
System.out.println("Documents added to the index.");
```

*استدعاء `index.add()` يدرج كل ملف، يستخرج النص، ويملأ الهياكل الداخلية اللازمة للاستعلامات السريعة، مما يضمن أن كل مستند مفهرس بالكامل ويمكن البحث فيه فورًا دون الحاجة إلى خطوة معالجة منفصلة.*

### كيفية إضافة مستندات إلى الفهرس
يمكنك إضافة ملفات أخرى برمجيًا لاحقًا عن طريق استدعاء `index.add()` مرة أخرى مع مسار مجلد جديد أو مسارات ملفات فردية. هذه الطريقة التراكمية تحافظ على تحديث الفهرس دون الحاجة إلى إعادة بناء كاملة. إضافة المستندات بهذه الطريقة تتيح لك الحفاظ على فهرس حي يعكس أحدث تغييرات المحتوى، مما يدعم توفر البحث المستمر للمستخدمين النهائيين ويقلل من وقت التوقف المرتبط بعمليات إعادة الفهرسة الدفعية.

### استرجاع الكلمات المتجانسة لكلمة
استرجاع الكلمات المتجانسة لمصطلح معين يساعد محرك البحث على اعتبار التهجئات البديلة التي تُنطق بنفس الطريقة، مما يحسن الاسترجاع للاستعلامات التي قد يخطئ فيها المستخدمون أو يستخدمون صيغًا مختلفة. من خلال توسيع الاستعلام بالبدائل الصوتية، يستطيع المحرك مطابقة المستندات التي تحتوي على أي من الأشكال المتجانسة، مما يقدم نتائج أكثر شمولًا.

*فئة `HomophoneDictionary` تخزن مجموعات من الكلمات التي تشترك في النطق نفسه، وتعمل كمستودع مركزي يستشيرها محرك البحث عند توسيع الاستعلامات بالبدائل الصوتية، مما يعزز صلة نتائج البحث.*

```java
String[] homophones = index.getDictionaries().getHomophoneDictionary().getHomophones("braid");
```

### استرجاع مجموعات الكلمات المتجانسة
تجميع الكلمات المتجانسة يوفر طريقة منظمة لإدارة الكلمات ذات المعاني المتعددة، مما يتيح للمطورين استرجاع مجموعات كاملة من البدائل الصوتية في عملية واحدة. يمكن أن يكون ذلك مفيدًا للتحليلات، إدارة القاموس المخصص، أو تحديثات جماعية لقائمة الكلمات المتجانسة.

*كل مجموعة تُرجعها `getGroups()` تحتوي على كلمات يمكن استبدالها في عمليات البحث الصوتية، وتوفر الطريقة مجموعة شاملة من هذه المجموعات لتتمكن من فحصها أو تعديلها أو تصدير مجموعة العلاقات المتجانسة الكاملة التي يحتفظ بها القاموس.*

```java
String[][] groups = index.getDictionaries().getHomophoneDictionary().getHomophoneGroups("braid");
```

### مسح قاموس الكلمات المتجانسة
مسح الإدخالات القديمة أو غير الضرورية يضمن بقاء القاموس ملائمًا ولا يضيف ضوضاء إلى نتائج البحث. عادةً ما يتم تنفيذ هذه العملية عندما تحتاج إلى إعادة تعيين القاموس إلى حالته الافتراضية قبل تحميل مجموعة مخصصة جديدة.

*طريقة `clear()` تزيل جميع الإدخالات المخصصة، وتعيد القاموس إلى المجموعة الافتراضية، وتضمن أن أي مجموعات كلمات متجانسة مضافة مسبقًا تُحذف بالكامل، مما يوفر لوحة نظيفة لتكوين القاموس اللاحق.*

```java
if (index.getDictionaries().getHomophoneDictionary().getCount() > 0) {
    index.getDictionaries().getHomophoneDictionary().clear();
}
System.out.println("Homophone dictionary cleared.");
```

### إضافة كلمات متجانسة إلى القاموس
تخصيص قاموس الكلمات المتجانسة يتيح قدرات بحث مخصصة تعكس المصطلحات الخاصة بالمجال أو العامية أو أسماء العلامات التجارية. بإضافة مجموعات جديدة، يمكنك التأكد من أن عمليات البحث تتعرف على العلاقات الصوتية المقصودة الفريدة لتطبيقك.

*استخدم `addGroup()` لإدراج قائمة من الكلمات ذات النطق المتشابه، مما يعزز الاسترجاع للمصطلحات الخاصة بالمجال، وتتحقق الطريقة من صحة كل إدخال لمنع التكرارات بينما تدمج المجموعة الجديدة بسلاسة في بنية القاموس الحالية.*

```java
String[][] homophoneGroups = {
    new String[] { "awe", "oar", "or", "ore" },
    new String[] { "aye", "eye", "i" },
    new String[] { "call", "caul" }
};
index.getDictionaries().getHomophoneDictionary().addRange(homophoneGroups);
System.out.println("Homophones added to the dictionary.");
```

### تصدير واستيراد قواميس الكلمات المتجانسة
تصدير واستيراد القواميس يمكن أن يكون مفيدًا لأغراض النسخ الاحتياطي أو النقل، مما يتيح لك الحفاظ على التكوينات المخصصة عبر البيئات أو مشاركتها مع أعضاء الفريق. تدعم هذه الوظيفة تنسيق JSON لسهولة القراءة والتكامل مع الأدوات الأخرى.

*هذه الطرق تتيح لك حفظ القواميس المخصصة كملفات JSON لإعادة استخدامها بسهولة، وتلتقط عملية التصدير الحالة الكاملة للقاموس بينما يتحقق روتين الاستيراد من بنية JSON قبل تطبيقها على نسخة القاموس النشطة.*

```java
String fileName = "path/to/exported/dictionary.file";
index.getDictionaries().getHomophoneDictionary().exportDictionary(fileName);
```

**الخطوة 2:** إعادة الاستيراد من ملف إذا لزم الأمر.

```java
index.getDictionaries().getHomophoneDictionary().importDictionary(fileName);
System.out.println("Homophone dictionary imported successfully.");
```

*عملية الاستيراد تقرأ ملف JSON، تعيد بناء كل مجموعة متجانسة، وتدمجها في القاموس الحالي، مما يضمن استعادة جميع الإدخالات المخصصة بدقة وجاهزيتها للاستخدام الفوري في استعلامات البحث.*

### البحث باستخدام الكلمات المتجانسة
استفد من بحث الكلمات المتجانسة لاسترجاع مستندات شامل، مما يسمح للمستخدمين بالعثور على المحتوى ذي الصلة حتى عندما يستخدمون تهجئات مختلفة تُنطق بشكل مشابه. هذه الميزة يمكن أن تحسن تجربة المستخدم بشكل كبير في المجالات متعددة اللغات أو التي تعتمد على الصوتيات.

*ضبط `setUseHomophoneSearch(true)` يوجه المحرك لتوسيع الاستعلامات بالبدائل الصوتية قبل التنفيذ، وتعمل هذه الخاصية بالتزامن مع إعدادات البحث الأخرى مثل المطابقة الضبابية لتوفير تجربة بحث قوية ومرنة تلتقط مجموعة واسعة من النتائج ذات الصلة.*

```java
String query = "caul";
SearchOptions options = new SearchOptions();
options.setUseHomophoneSearch(true);
SearchResult result = index.search(query, options);

System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## التطبيقات العملية

فهم كيفية تنفيذ هذه الميزات يفتح عالمًا من التطبيقات العملية:

1. **إدارة المستندات القانونية:** التمييز بين المصطلحات القانونية المتشابهة في النطق مثل “lease” مقابل “least”.  
2. **إنشاء محتوى تعليمي:** ضمان خلو المواد التعليمية من الصياغات الغامضة التي قد تربك المتعلمين.  
3. **أنظمة دعم العملاء:** تحسين دقة البحث في قاعدة المعرفة، مما يساعد الوكلاء على العثور على المقالات الصحيحة بسرعة أكبر.

## اعتبارات الأداء

للحفاظ على أداء **java full text search**:

- **تحديث الفهرس بانتظام** لتعكس تغييرات المستندات.  
- **مراقبة استهلاك الذاكرة** وضبط إعدادات كومة جافا للمجموعات الكبيرة من البيانات.  
- **إغلاق الموارد غير المستخدمة بسرعة** (مثلاً، استدعاء `index.close()` عند الانتهاء).  

## الخلاصة

بحلول الآن يجب أن تكون لديك فهم قوي لـ **كيفية فهرسة المستندات** باستخدام GroupDocs.Search، وإدارة الكلمات المتجانسة، وتحسين تجربة البحث. هذه الأدوات لا تقدر بثمن لتقديم نتائج دقيقة وتعزيز كفاءة إدارة المستندات بشكل عام.

## الأسئلة المتكررة

**س:** هل يمكنني استخدام قاموس الكلمات المتجانسة مع لغات غير الإنجليزية؟  
**ج:** نعم، يمكنك ملء القاموس بأي لغة طالما أنك توفر مجموعات الكلمات المناسبة.

**س:** هل أحتاج إلى ترخيص للاختبار التطويري؟  
**ج:** ترخيص التجربة المجانية كافٍ للتطوير والاختبار؛ يلزم ترخيص مدفوع للنشر في بيئة الإنتاج.

**س:** ما هو الحد الأقصى لحجم الفهرس؟  
**ج:** حجم الفهرس يقتصر فقط على موارد الأجهزة لديك؛ خصص مساحة قرص وذاكرة كافية لتحقيق الأداء المثالي.

**س:** هل يمكن الجمع بين بحث الكلمات المتجانسة والمطابقة الضبابية؟  
**ج:** بالتأكيد. فعّل كل من `setUseHomophoneSearch(true)` و `setFuzzySearch(true)` في `SearchOptions` للحصول على أفضل ما فيهما.

**س:** ماذا يحدث إذا أضفت مجموعات كلمات متجانسة مكررة؟  
**ج:** يتم تجاهل الإدخالات المكررة؛ القاموس يحافظ على مجموعة فريدة من مجموعات الكلمات.

---

**آخر تحديث:** 2026-09-21  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [كيفية تنفيذ بحث نص كامل بجافا: إنشاء دليل الفهرس باستخدام GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [كيفية إضافة مستندات إلى الفهرس مع فهرسة البيانات الوصفية في جافا باستخدام GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [مكتبة بحث نص كامل بجافا – تحسين الفهرس باستخدام GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
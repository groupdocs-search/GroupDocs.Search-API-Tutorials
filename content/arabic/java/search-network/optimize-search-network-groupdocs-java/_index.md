---
date: '2026-05-17'
description: تعلم كيفية تكوين شبكة البحث Java، تحسين الشظايا، إجراء بحث نصي، ومعالجة
  تعارضات المنافذ باستخدام GroupDocs.Search for Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'كيفية تحسين الشظايا في GroupDocs.Search for Java: دليل شامل'
type: docs
url: /ar/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# كيفية تحسين الشرائح (shards) في GroupDocs.Search للـ Java: دليل شامل

البحث الفعال في المستندات أمر أساسي للمطورين والشركات التي تدير مجموعات بيانات كبيرة أو تحتاج إلى استرجاع داخلي سريع. في هذا الدليل ستتعلم **كيفية تكوين شبكة البحث java**، وكيفية فهرسة واستعلام المستندات، والخطوات الدقيقة **لتحسين الشرائح** لتحقيق أقصى أداء. سنغطي أيضًا حالات الاستخدام الواقعية، والمشكلات الشائعة، ونصائح عملية للحفاظ على تشغيل عقد البحث بسلاسة.

## إجابات سريعة
- **ما هو تحسين الشرائح؟** يعيد تنظيم بيانات الفهرس لتسريع الاستعلامات وتقليل استهلاك التخزين.  
- **كيف يتم تكوين شبكة البحث؟** حدد دليلًا أساسيًا ومنفذًا، ثم انشر العقد باستخدام الـ API المقدم.  
- **كيف يتم تنفيذ بحث نصي؟** استخدم `TextSearchInNetwork.searchAll` مع سلسلة الاستعلام الخاصة بك.  
- **كيف يتم فهرسة المستندات في Java؟** أضف دلائل المستندات إلى العقدة الرئيسية باستخدام `IndexingDocuments.addDirectories`.  
- **كيف يتم التعامل مع تعارضات المنافذ؟** غيّر المتغير `basePort` إلى منفذ غير مستخدم على جهازك.

## كيفية تكوين شبكة البحث
`Configuration` يخزن جميع الإعدادات المطلوبة لإطلاق شبكة GroupDocs.Search، مثل موقع مجلد الفهرس ومنفذ الاتصال.  
`SearchNetwork` يدير العقد، ويتعامل مع الفهرسة وتوزيع الاستعلامات.

حمّل إعدادات البحث الخاصة بك، عيّن مسار المستند الأساسي، اختر منفذًا فارغًا، وابدأ الشبكة—كل ذلك في بضع أسطر من الشيفرة. يوضح هذا الجواب المباشر العملية بالكامل في أقل من 70 كلمة: **أنشئ كائن `Configuration`، عيّن `basePath` و `basePort`، ثم استدعِ `SearchNetwork.start(configuration)`.** ستقوم الشبكة تلقائيًا بإنشاء عقدة رئيسية وأية عقد عمل مطلوبة، جاهزة لاستقبال طلبات الفهرسة.

### تعريف
`Configuration` هي الفئة الأساسية التي تخزن جميع الإعدادات المطلوبة لإطلاق شبكة GroupDocs.Search، مثل موقع مجلد الفهرس ومنفذ الاتصال.

لتجنب الخطأ المخيف “المنفذ مستخدم بالفعل”، تحقق أولاً من أن المنفذ المختار فارغ (مثلاً باستخدام `netstat` أو اختبار مقبس بسيط) قبل تهيئة الشبكة.

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

## كيفية فهرسة المستندات في Java
`IndexingDocuments` هي فئة مساعدة تُبسّط إضافة دلائل متعددة إلى عقدة البحث وتُطلق خط أنابيب الفهرسة.

أضف مجلدات المستندات الخاصة بك إلى العقدة الرئيسية، ثم دع الفهرس يزحف إليها. **الجواب المباشر:** استدعِ `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` ثم نفّذ `masterNode.index()`؛ سيُنشئ المحرك شرائح قابلة للبحث لكل مجلد قمت بتوفيرها. هذا النهج يتوسع أفقياً—أضف المزيد من العقد، وستقوم الطريقة نفسها بتوزيع عبء العمل تلقائيًا.

### تعريف
`IndexingDocuments` هي فئة مساعدة تُبسّط إضافة دلائل متعددة إلى عقدة البحث وتُطلق خط أنابيب الفهرسة.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## كيفية تنفيذ بحث نصي
`TextSearchInNetwork` توفر طرقًا ثابتة للمساعدة في بث استعلام نصي إلى كل عقدة في الشبكة وتجميع النتائج.  
`SearchResult` يضم معرف المستند المتطابق، المقتطف، ودرجة الصلة.

نفّذ استعلامًا عبر جميع الشرائح باستدعاء طريقة واحدة. **الجواب المباشر:** استخدم `TextSearchInNetwork.searchAll("your query", searchNetwork)`؛ تُعيد الطريقة مجموعة من كائنات `SearchResult` التي تحتوي على معرفات المستندات، المقتطفات، ودرجات الصلة. يمكنك أيضًا تصفية النتائج حسب اللغة، نوع الملف، أو البيانات الوصفية المخصصة دون كتابة شيفرة إضافية.

### تعريف
`TextSearchInNetwork` توفر طرقًا ثابتة للمساعدة في بث استعلام نصي إلى كل عقدة في الشبكة وتجميع النتائج.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## كيفية التعامل مع تعارضات المنافذ
إذا كان المنفذ الافتراضي (`49132`) مشغولًا، اختر ببساطة منفذًا فارغًا آخر وقم بتحديث حقل `basePort` قبل بدء الشبكة. **الجواب المباشر:** غيّر `int basePort = 49132;` إلى قيمة غير مستخدمة مثل `49133`، أعد البناء، وأعد التشغيل؛ ستربط الشبكة بالمنفذ الجديد دون التأثير على العقد الموجودة.

نصيحة احترافية: احتفظ بملف إعدادات صغير (مثلاً `search-config.properties`) لتتمكن من تغيير المنفذ دون إعادة التجميع.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من توفر المتطلبات المسبقة التالية:

### المكتبات المطلوبة، الإصدارات، والاعتمادات
لتنفيذ هذا الحل، أدرج مكتبة GroupDocs.Search باستخدام Maven بإضافة التكوين التالي إلى ملف `pom.xml` الخاص بك:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
بدلاً من ذلك، قم بتنزيل أحدث إصدار من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### متطلبات إعداد البيئة
- Java Development Kit (JDK) 8 أو أحدث.  
- أذونات الشبكة التي تسمح بالربط بالمنفذ `basePort` المختار.  
- مساحة قرص كافية لملفات الفهرس (كل شريحة يمكن أن تشغل ~10 ميغابايت لكل 1,000 مستند).

### المتطلبات المعرفية
فهم أساسي للغة Java، البرمجة الكائنية، ومعالجة الاستثناءات سيساعدك على متابعة الأمثلة بسلاسة.

## إعداد GroupDocs.Search للـ Java
لبدء استخدام GroupDocs.Search في مشروعك، اتبع الخطوات التالية:

1. **إضافة الاعتماد**: كما هو موضح أعلاه، أضف الاعتماد الضروري لـ Maven إلى مشروعك أو قم بتنزيله مباشرة من صفحة الإصدارات.  
2. **اكتساب الترخيص**:  
   - **تجربة مجانية** – لا يلزم مفتاح ترخيص، لكن الاستخدام يقتصر على 500 مستند يوميًا.  
   - **ترخيص مؤقت** – اطلب مفتاح تجربة لمدة 30 يومًا من [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **ترخيص كامل** – اشترِ ترخيص إنتاج للوصول غير المحدود والدعم ذو الأولوية.  
3. **التهيئة الأساسية والإعداد**:  
   ابدأ تهيئة الإعدادات باستخدام فئة `Configuration`، مع تحديد مسار المستندات الأساسي وتحديد رقم المنفذ:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## دليل التنفيذ
الآن لنستكشف تنفيذ الميزات الرئيسية باستخدام GroupDocs.Search للـ Java.

### الميزة: تكوين شبكة البحث
**نظرة عامة**: إعداد شبكة بحث يتضمن تعريف دليل المستندات وتكوينه بمنفذ محدد للتواصل بين العقد.

#### الخطوة 1: تعريف دلائل المستندات والمنفذ
`DocumentDirectory` هو حاوية بسيطة للمسار المطلق لمجلد تريد فهرسته. قدم مسارًا واحدًا أو أكثر إلى التكوين.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### الخطوة 2: تكوين شبكة البحث
أنشئ كائن التكوين باستخدام المسارات المحددة:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### الميزة: نشر عقد شبكة البحث
**نظرة عامة**: نشر العقد للتعامل مع بحث المستندات بكفاءة عبر شبكتك.

#### الخطوة 1: نشر العقد باستخدام التكوين
انشر عقد شبكة البحث وحدد العقدة الرئيسية للإدارة المركزية:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### الميزة: الاشتراك في أحداث عقد الشبكة
**نظرة عامة**: راقب شبكة البحث الخاصة بك بالاشتراك في الأحداث التي تُعلمك بالتغييرات أو الإجراءات المهمة.

#### الخطوة 1: الاشتراك في أحداث العقدة الرئيسية
`SearchNetworkEventListener` يتيح لك الاستجابة لإكمال الفهرسة، فشل العقد، أو تحسين الشرائح.

CODE_BLOCK_PLACEHOLDER_9_END

### الميزة: فهرسة المستندات في عقد الشبكة
**نظرة عامة**: أضف دلائل تحتوي على مستندات إلى عملية الفهرسة للحصول على بحث فعال.

#### الخطوة 1: إضافة دلائل المستندات إلى عملية الفهرسة
مرّر قائمة بمسارات المجلدات إلى العقدة الرئيسية؛ سيُنشئ المحرك شريحة منفصلة لكل مجلد، مما يتيح تنفيذ الاستعلامات بشكل متوازي.

CODE_BLOCK_PLACEHOLDER_10_END

### الميزة: بحث نصي في عقد الشبكة
**نظرة عامة**: تنفيذ بحث نصي عبر جميع المستندات المفهرسة داخل شبكة البحث الخاصة بك.

#### الخطوة 1: تنفيذ بحث نصي
استدعِ المساعد الثابت لتشغيل استعلام واسترجاع المستندات المتطابقة مع درجات الصلة.

CODE_BLOCK_PLACEHOLDER_11_END

### الميزة: تحسين الشرائح
**نظرة عامة**: تحسين الأداء عن طريق تحسين الشرائح داخل فهرس عقدة شبكة البحث الخاصة بك.

#### الخطوة 1: تحسين شرائح الفهرس
حسّن الشرائح لتحسين كفاءة البحث (هنا يأتي دور **كيفية تحسين الشرائح** فعليًا):

CODE_BLOCK_PLACEHOLDER_12_END

## التطبيقات العملية
يمكن تطبيق GroupDocs.Search للـ Java في سيناريوهات واقعية متعددة، كل منها يستفيد من تحسين الشرائح:

1. **إدارة المستندات المؤسسية** – يتعامل مع أرشيفات تزيد عن 10 تيرابايت مع أوقات استعلام أقل من ثانية بعد تحسين الشرائح.  
2. **منصات التجارة الإلكترونية** – يدعم بحث المنتجات عبر مليون SKU، ويقلل زمن الاستجابة حتى 45 % عند تحسين الشرائح.  
3. **مكاتب المحاماة** – تسترجع ملفات القضايا من مستودعات بحجم 200 غيغابايت في أقل من 200 مللي ثانية.  
4. **أنظمة المكتبة** – تدعم بحث الفهرس لـ 500 ألف كتاب رقمي مع استخدام فعال للذاكرة.  
5. **أنظمة إدارة المحتوى (CMS)** – تمكّن من اكتشاف المحتوى فورًا للنشر المتعدد المواقع بأكثر من 2 مليون صفحة.

## اعتبارات الأداء
لضمان الأداء الأمثل لتطبيق GroupDocs.Search الخاص بك:

- **قم بتحسين الشرائح بانتظام** – تشغيل `optimizeShards()` بعد كل 10 غيغابايت من البيانات الجديدة يقلل أوقات استجابة الاستعلامات بنسبة 30‑50 %.  
- **راقب استخدام الذاكرة** – حافظ على حجم كومة JVM أقل من 75 % من الذاكرة الفعلية؛ فعّل G1GC للفهارس الكبيرة.  
- **استخدم الفهرسة التزايدية** – أضف الملفات المتغيرة فقط لتجنب الفهرسة الكاملة.  
- **استفد من التوسع متعدد العقد** – أضف عقد عمل لتوزيع الشرائح؛ كل عقدة إضافية يمكن أن تحسن معدل النقل بنحو ~20 % لأعباء القراءة الثقيلة.

## المشكلات الشائعة والحلول
| المشكلة | العَرَض | الحل |
|-------|---------|----------|
| تعارض المنفذ عند بدء التشغيل | `java.net.BindException: Address already in use` | غيّر `basePort` إلى قيمة غير مستخدمة؛ تحقق باستخدام `netstat -ano`. |
| أخطاء نفاد الذاكرة أثناء التحسين | `java.lang.OutOfMemoryError: Java heap space` | زدِ قيمة علمة JVM `-Xmx` أو نفّذ التحسين على عقدة مخصصة بذاكرة RAM أكبر. |
| المستندات المفقودة في نتائج البحث | عدم إرجاع أي نتائج بعد الفهرسة | تأكد من إضافة الدلائل بشكل صحيح عبر `IndexingDocuments.addDirectories` وأن `masterNode.index()` انتهى دون استثناءات. |
| شرائح قديمة بعد حذف جماعي | الملفات المحذوفة لا تزال تظهر | شغّل `optimizeShards()` لدمج القطاعات وإزالة العلامات (tombstones). |

## الأسئلة المتكررة

**س: كيف يؤثر تحسين الشرائح على سرعة الاستعلام؟**  
ج: تحسين الشرائح يضغط الفهرس، يقلل من عمليات إدخال/إخراج القرص، وعادةً ما ينتج استجابات استعلام أسرع بنسبة 30‑50 % لمجموعات البيانات الكبيرة.

**س: هل من الآمن تشغيل `optimizeShards` على عقدة حية؟**  
ج: نعم، تم تصميم العملية لتعمل دون توقف، لكن يُنصح بجدولتها خلال فترات انخفاض الحركة للفهارس التي تزيد عن 20 غيغابايت.

**س: هل يمكنني تخصيص `OptimizeOptions`؟**  
ج: بالتأكيد. يمكنك ضبط معلمات مثل `maxSegmentSize` أو `mergeFactor` لتعديل عملية التحسين بدقة.

**س: ماذا أفعل إذا واجهت `IOException` أثناء التحسين؟**  
ج: تحقق من أذونات نظام الملفات، تأكد من وجود مساحة كافية على القرص، وتأكد من عدم وجود عملية أخرى تقفل ملفات الفهرس.

**س: هل يقوم تحسين الشرائح أيضًا باستعادة مساحة المستندات المحذوفة؟**  
ج: نعم، يقوم المحسن بدمج القطاعات وإزالة العلامات (tombstones)، مما يحرر المساحة التي كانت مشغولة بالمستندات المحذوفة.

## الخلاصة
باتباع هذا الدليل الشامل، أصبحت الآن تعرف **كيفية تكوين شبكة البحث java**، فهرسة المستندات، تشغيل استعلامات نصية، والأهم من ذلك **تحسين الشرائح** للحفاظ على أداء البحث حادًا كالشفرة. طبّق هذه الأنماط على أي حل بحث مؤسسي قائم على Java، وستلاحظ تحسينات ملموسة في زمن الاستجابة، القابلية للتوسع، واستخدام الموارد. للخطوات التالية، استكشف الميزات المتقدمة مثل المحللات المخصصة، البحث الموجه بالواجهات، والتكامل مع مزودي التخزين السحابي.

**آخر تحديث:** 2026-05-17  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [تكوين شبكة GroupDocs.Search في .NET: دليل شامل](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [فهرسة المستندات الرئيسية في .NET باستخدام GroupDocs.Search: دليل شامل](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [دروس وأمثلة على GroupDocs.Search للـ Java](/search/net/)
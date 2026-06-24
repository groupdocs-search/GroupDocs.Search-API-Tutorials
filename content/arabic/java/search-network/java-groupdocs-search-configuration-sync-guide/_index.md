---
date: '2026-05-17'
description: تعلم كيفية إضافة تبعية groupdocs Maven، إعداد شبكة بحث Java، وإضافة الأدلة
  إلى الفهرس للحصول على استرجاع مستندات سريع وقابل للتوسع.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: كيفية إضافة تبعية GroupDocs Maven لشبكة البحث
type: docs
url: /ar/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# كيفية إضافة اعتماد GroupDocs Maven لشبكة البحث

في هذا الدليل الشامل ستكتشف **كيفية إضافة اعتماد groupdocs Maven**، وتكوين شبكة بحث Java قوية باستخدام GroupDocs.Search، والحفاظ على تزامن القطع (shards). سواءً كنت تقوم بفهرسة المذكرات القانونية، أو البيانات المالية، أو الأوراق الأكاديمية، فإن الخطوات أدناه ستساعدك على إنشاء فهارس قابلة للبحث، وتوزيع حمل الاستعلامات عبر العقد، والحفاظ على تناسق البيانات بأقل جهد.

## إجابات سريعة
- **ما هو اعتماد GroupDocs Maven؟** عنصر Maven يجمع مكتبة GroupDocs.Search لمشاريع Java.  
- **لماذا تستخدم شبكة بحث؟** تقوم بتوزيع حمل الفهرسة والاستعلام عبر عدة عقد، مما يحسن السرعة والموثوقية.  
- **كيف أضيف أدلة للفهرسة؟** استخدم `IndexingDocuments.addDirectories` على العقدة الرئيسية.  
- **كيف تزامن القطع (shards)؟** استدعِ `SynchronizeOptions` على `Indexer` لكل عقدة.  
- **هل أحتاج إلى ترخيص؟** نعم، يلزم وجود ترخيص تجريبي أو تجاري للاستخدام في الإنتاج.

## ما هو اعتماد GroupDocs Maven؟

إن `GroupDocs Maven dependency` هو عنصر Maven يجمع مكتبة GroupDocs.Search لمشاريع Java.  
يوفر جميع الفئات المطلوبة لإنشاء فهارس قابلة للبحث، وإدارة عقد الشبكة، وتنفيذ استعلامات سريعة، كما يقوم Maven بحل الاعتمادات المتعاقبة تلقائيًا، مما يمنحك محرك بحث جاهزًا للاستخدام ببضع أسطر فقط في ملف `pom.xml` الخاص بك.

## كيفية إضافة اعتماد GroupDocs Maven

أضف مستودع الاعتماد وإدخالات الاعتماد إلى ملف `pom.xml` الخاص بك، ثم نفّذ `mvn clean install`؛ يقوم Maven بتنزيل JAR الخاص بـ `groupdocs-search` ومكتباته المطلوبة، مما يجعل الـ API متاحًا في مشروعك. بعد نجاح عملية البناء يمكنك البدء في استخدام فئات `com.groupdocs.search` فورًا.

### تكوين Maven

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

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار من خلال مراجعة صفحة الإصدارات الرسمية.

يمكنك أيضًا تنزيل ملف JAR مباشرةً من الموقع الرسمي: [إصدارات GroupDocs.Search للـ Java](https://releases.groupdocs.com/search/java/).

## لماذا تستخدم شبكة بحث؟

تمكن شبكة البحث من التوسع الأفقي عن طريق تقسيم الفهرس إلى قطع (shards) تتواجد على عقد منفصلة. يمكن لـ GroupDocs.Search معالجة **أكثر من 50 تنسيقًا مدخلًا** ومعالجة **مستندات مئات الصفحات** دون تحميل الملف بالكامل في الذاكرة، مما يوفر استجابات استعلام بأقل من ثانية حتى مع زيادة حجم البيانات.

## المتطلبات المسبقة

- **JDK** (الإصدار 11 أو أحدث) مثبت.  
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse.  
- معرفة أساسية بـ Java، وإلمام بـ Maven، وفهم مفاهيم عقد الشبكة.  
- ترخيص صالح لـ GroupDocs.Search (تجريبي مجاني أو تجاري).

## التهيئة الأساسية والإعداد

ابدأ بإنشاء دليل الفهرس:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

## دليل التنفيذ

### الميزة 1: تكوين شبكة البحث

#### نظرة عامة

تحديد تكوين شبكة البحث يحدد مسارات الملفات والمنافذ التي ستستخدمها العقد للتواصل.

##### إعداد المسارات والمنافذ

Configuration هي فئة تحتفظ بمسارات الشبكة، والمنافذ، وإعدادات أخرى لمجموعة البحث.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
الآن كائن `configuration` يحتوي على جميع الإعدادات اللازمة لشبكة البحث الخاصة بك.

### الميزة 2: نشر عقد شبكة البحث

#### نظرة عامة

نشر العقد لتوزيع عبء العمل عبر شبكتك. تدير العقدة الرئيسية العمليات والأحداث.

##### كود النشر

SearchNetworkNode تمثل عقدة في شبكة البحث يمكن أن تعمل كعقدة رئيسية أو عاملة.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### الميزة 3: الاشتراك في أحداث عقد شبكة البحث

#### نظرة عامة

الاستماع إلى الأحداث يتيح معالجة ديناميكية للتغييرات أو التحديثات في شبكتك.

##### تنفيذ الاشتراك

SearchNetworkNodeEvents توفر نقاط ربط للأحداث لدورة حياة العقدة وإجراءات الفهرسة.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### الميزة 4: إضافة أدلة للفهرسة

#### نظرة عامة

إضافة الأدلة هي الخطوة الأساسية التي تجعل مستنداتك قابلة للبحث.

##### إضافة المستندات

`IndexingDocuments.addDirectories` يضيف مسارات المجلدات إلى الفهرس للمعالجة.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### الميزة 5: مزامنة القطع في عقدة شبكة البحث

#### نظرة عامة

المزامنة تضمن تناسق البيانات عبر جميع القطع.

##### كود المزامنة

`SynchronizeOptions` يحدد كيفية مزامنة القطع عبر العقد.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### الميزة 6: إغلاق عقد شبكة البحث

#### نظرة عامة

إغلاق العقد بشكل صحيح يحرر الموارد ويمنع تسرب الذاكرة.

##### إغلاق العقدة

`close()` يحرر الموارد ويغلق عقدة شبكة البحث.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## التطبيقات العملية

1. **إدارة المستندات القانونية** – استرجاع ملفات القضايا والسوابق بسرعة.  
2. **حفظ السجلات المالية** – الوصول إلى البيانات المالية وسجلات التدقيق في ثوانٍ.  
3. **البحث الأكاديمي** – البحث عبر آلاف الأوراق للعثور على الاستشهادات ذات الصلة.

## اعتبارات الأداء

- **تحسين الاستعلامات** – كتابة استعلامات مختصرة لتقليل زمن الاستجابة.  
- **إدارة الذاكرة** – مراقبة استخدام Heap في JVM؛ النظر في ضبط GC للفهارس الكبيرة.  
- **استراتيجية التوسع** – إضافة عقد بنسب تتناسب مع حجم البيانات وحمل الاستعلامات.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|----------|
| فشل العقد في الاتصال | تعارض المنافذ | غيّر `basePort` إلى قيمة غير مستخدمة |
| الفهرس لا يتم تحديثه | غياب اشتراك الحدث | تأكد من استدعاء `SearchNetworkNodeEvents.subscribe(masterNode)` |
| ارتفاع زمن الاستجابة | عدد القطع غير كافٍ | زيادة عدد العقد وموازنة توزيع المستندات |

## الأسئلة المتكررة

**Q:** ما هو الفائدة الأساسية من استخدام GroupDocs.Search؟  
**A:** توفر قدرات بحث سريعة وقابلة للتوسع عبر مجموعات مستندات كبيرة مع إعدادات قليلة.

**Q:** هل يمكنني تخصيص إعدادات العقد في شبكة البحث؟  
**A:** نعم، يمكنك ضبط مسارات مخصصة، ومنافذ، وخيارات أخرى عبر كائن `Configuration`.

**Q:** كيف أضيف أدلة للفهرسة بعد تشغيل الشبكة؟  
**A:** استدعِ `IndexingDocuments.addDirectories(masterNode, "path")` كلما احتجت إلى فهرسة مجلدات جديدة.

**Q:** كيف يتم مزامنة القطع عندما تنضم عقدة جديدة إلى الشبكة؟  
**A:** استخدم طريقة `synchronizeShards` الموضحة أعلاه على العقدة المضافة حديثًا.

**Q:** هل أحتاج إلى ترخيص للتطوير؟  
**A:** ترخيص تجريبي مجاني يكفي للاختبار؛ يلزم ترخيص تجاري للإنتاج.

## الخلاصة

باتباع هذا الدليل، أصبحت الآن تعرف **كيفية إضافة اعتماد groupdocs Maven**، وتكوين شبكة بحث متعددة العقد، وفهرسة الأدلة، والحفاظ على تزامن القطع. تشكل هذه الخطوات أساس حل بحث مستندات عالي الأداء يمكن أن يتوسع مع احتياجات مؤسستك.

---

**آخر تحديث:** 2026-05-17  
**تم الاختبار مع:** GroupDocs.Search 25.4  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [دروس وأمثلة GroupDocs.Search للـ Java](/search/net/)
- [تكوين شبكة GroupDocs.Search في .NET: دليل شامل](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [كيفية تنفيذ شبكة بحث باستخدام GroupDocs.Search في .NET لأنظمة إدارة المستندات](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
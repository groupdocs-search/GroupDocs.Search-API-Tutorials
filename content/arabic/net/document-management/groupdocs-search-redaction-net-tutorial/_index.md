---
date: '2026-06-12'
description: تعلم كيفية إنشاء فهرس بحث .NET وتطبيق الحجب على ملفات PDF باستخدام GroupDocs.Search
  و GroupDocs.Redaction. شرح الإعداد، النشر، الفهرسة، والبحث المتقدم.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: إنشاء فهرس بحث .NET باستخدام GroupDocs Search و GroupDocs Redaction – دليل
  شامل
type: docs
url: /ar/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# إنشاء فهرس بحث .NET باستخدام GroupDocs Search و Redaction – دليل شامل

في المشهد الرقمي اليوم، **إنشاء فهرس بحث .NET** حل يمكنه كل من تحديد المعلومات بسرعة وحماية البيانات الحساسة هو أولوية قصوى لأي مؤسسة. يشرح هذا الدليل كيفية تكوين شبكة GroupDocs.Search قابلة للتوسع، نشر العقد، فهرسة المستندات، واستخدام GroupDocs.Redaction **لتطبيق التشويه على ملفات PDF** — كل ذلك داخل بيئة .NET.

## إجابات سريعة
- **ما هي الخطوة الأولى لإنشاء فهرس بحث .NET؟** حدد مسار قاعدة ومنفذ، ثم نشر عقد الشبكة.  
- **كيف يمكنني تطبيق التشويه على PDF باستخدام GroupDocs؟** ابدأ بإنشاء مثيل `Redactor`، حمّل ملف PDF، واستدعِ `Redact` مع الأنماط المطلوبة.  
- **هل يمكن تشغيل شبكة البحث على عدة آلات؟** نعم—انشر العقد على خوادم منفصلة ودع العقدة الرئيسية تنسق الفهرسة والاستعلامات.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم وجود ترخيص GroupDocs صالح للإنتاج؛ يتوفر ترخيص تجريبي مؤقت للتقييم.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.7.2+، .NET Core 3.1+، و .NET 5/6/7 مدعومة بالكامل.

## ما هو “إنشاء فهرس بحث .NET”؟
*إنشاء فهرس بحث .NET* يشير إلى بناء مستودع قابل للبحث يحتوي على بيانات تعريف المستندات ومحتواها باستخدام مكتبات .NET، التي تستخرج النص، تقسم المصطلحات إلى رموز، وتخزنها في بنية فهرس محسّنة. يتيح ذلك استجابات استعلام فورية عبر العقد الموزعة، يدعم صيغ ملفات متعددة، ويسمح باسترجاع مستندات عالي الأداء وقابل للتوسع في تطبيقات المؤسسات.

## لماذا نستخدم GroupDocs Search و Redaction معًا؟
يدعم GroupDocs.Search **أكثر من 50 صيغة ملف** — بما في ذلك DOCX و PDF و PPTX و HTML — ويمكنه فهرسة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة. عند الجمع مع GroupDocs.Redaction، الذي يمكنه **تطبيق التشويه على PDF** في أقل من 200 مللي ثانية لكل صفحة، تحصل على خط أنابيب لإدارة المستندات آمن وعالي الأداء.

## المتطلبات المسبقة

### المكتبات والاعتمادات المطلوبة
لتنفيذ هذا الدليل، قم بتثبيت الحزم التالية:
- **GroupDocs.Search** لـ .NET
- **GroupDocs.Redaction** لـ .NET  

يمكنك استخدام أي من هذه الطرق لتثبيت المكتبات اللازمة:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ابحث عن "GroupDocs.Search" و "GroupDocs.Redaction" وقم بتثبيت أحدث نسخة.

### متطلبات إعداد البيئة
- .NET Framework 4.7.2 أو أعلى (أو .NET Core 3.1+)
- بيئة تطوير Visual Studio (Community، Professional، أو Enterprise)

### المتطلبات المعرفية
- برمجة C# الأساسية
- مفاهيم البرمجة الكائنية
- الإلمام بتكوينات الشبكة وأنظمة إدارة المستندات

## إعداد GroupDocs.Redaction لـ .NET

### معلومات التثبيت
لدمج ميزات التشويه في تطبيقك، ابدأ بإضافة مكتبة GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ابحث عن "GroupDocs.Redaction" وقم بتثبيتها.

### الحصول على الترخيص
لبدء تجربة مجانية أو الحصول على ترخيص مؤقت، اتبع الخطوات التالية:
- زر [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/) لطلب ترخيص مؤقت.  
- لخيارات الشراء، انتقل إلى [صفحة التسعير](https://groupdocs.com/pricing).

بمجرد حصولك على ملف الترخيص، طبقه في إعداد تطبيقك:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### التهيئة الأساسية
لتهيئة GroupDocs.Redaction للعمليات الأساسية، استخدم المقتطف البرمجي التالي:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## دليل التنفيذ

### إعداد التكوين

#### نظرة عامة
تقوم هذه الميزة بتكوين شبكة البحث الخاصة بك باستخدام مسار قاعدة ورقم منفذ، مما يشكل أساس نظام إدارة المستندات.

#### تعريف العنصر
`SearchNetworkDeployment` هي الفئة التي تنسق نشر عقد البحث عبر الشبكة.

#### الخطوة 1: تحديد مسار القاعدة والمنفذ  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### الخطوة 2: تكوين الشبكة
استخدم طريقة `Configure` لإعداد شبكة البحث بالمسار والمنفذ المحددين:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### نشر عقد الشبكة

#### نظرة عامة
انشر العقد داخل شبكة البحث التي تم تكوينها للبحث الموزع عن المستندات.

#### تعريف العنصر
`SearchNetworkNode` تمثل عقدة بحث فردية تتواصل مع العقدة الرئيسية.

#### الخطوة 1: تهيئة النشر  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### الاشتراك في الأحداث للعقدة الرئيسية

#### نظرة عامة
اشترك في الأحداث على العقدة الرئيسية لمراقبة وإدارة عمليات الشبكة بفعالية.

#### تعريف العنصر
`SearchNetworkNodeEvents` توفر ردود نداء لأحداث الفهرسة، تنفيذ الاستعلام، ومعالجة الأخطاء.

#### الخطوة 1: تحديد العقدة الرئيسية
اختر أول عقدة كالعقدة الرئيسية:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### الخطوة 2: الاشتراك في الأحداث
اشترك في الأحداث باستخدام:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### فهرسة المستندات

#### نظرة عامة
قم بفهرسة المستندات لعمليات بحث فعّالة. هذه الخطوة حاسمة لضمان قدرة شبكتك على استرجاع البيانات المطلوبة بسرعة.

#### تعريف العنصر
`SearchIndex` هو الكائن الأساسي الذي يخزن الرموز القابلة للبحث والبيانات الوصفية لكل ملف مفهرس.

#### الخطوة 1: إضافة الأدلة إلى الفهرس
حدد الأدلة التي تحتوي على مستنداتك:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### وظيفة البحث – الاستخدام الأساسي

#### نظرة عامة
قم بأداء عمليات بحث أساسية عبر العقد في الشبكة.

#### إجابة مباشرة
استدعِ `SearchNetwork.Query("your term")` على العقدة الرئيسية لاسترجاع المستندات المتطابقة فورًا. تُعيد الطريقة مجموعة من كائنات `SearchResult` التي تشمل مسارات الملفات ودرجات الصلة.  
`SearchNetwork.Query` هي طريقة تنفّذ استعلام بحث عبر الشبكة بأكملها وتُعيد النتائج المتطابقة.

#### الخطوة 1: تحديد معلمات البحث  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### وظيفة البحث المتقدم

#### نظرة عامة
استخدم تقنيات بحث متقدمة مع معلمات قابلة للتخصيص للحصول على نتائج أكثر دقة.

#### إجابة مباشرة
نفّذ طريقة تُنشئ كائن `SearchOptions`، وتضبط خصائص `UseFuzzySearch` و `Highlight` و `PageSize`، ثم تمرّرها إلى `SearchNetwork.QueryAdvanced`. ينتج عن ذلك نتائج مُرقّمة ومُبرزّة مع تمكين المطابقة الضبابية.  
`SearchNetwork.QueryAdvanced` هي طريقة تُجري استعلامًا بخيارات متقدمة مثل المطابقة الضبابية والصفحات.

#### الخطوة 1: تنفيذ طريقة البحث المتقدم  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### تطبيق التشويه على ملفات PDF

#### نظرة عامة
احمِ المعلومات الحساسة عن طريق تشويه محتوى PDF قبل تخزينه أو مشاركته.

#### إجابة مباشرة
أنشئ مثيل `Redactor`، حمّل ملف PDF المستهدف، عرّف `RedactionPattern` (مثلاً تعبير regex للرقم الوطني)، استدعِ `redactor.Apply(pattern)`، وأخيرًا احفظ المستند المشوّه. يضمن هذا العملية إزالة البيانات الشخصية بشكل دائم.

#### تعريف العنصر
`Redactor` هو الفئة الأساسية في GroupDocs.Redaction التي تعالج المستندات وتطبق قواعد التشويه.

#### مثال سير العمل (بدون كتلة كود جديدة)
1. تهيئة `Redactor` باستخدام الترخيص الخاص بك.  
2. حمّل ملف PDF باستخدام `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` يمثل قاعدة تحدد النص أو النمط الذي سيُشوه. عرّف أنماطًا مثل `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. نفّذ `redactor.Apply(pattern)`.  
5. احفظ الناتج باستخدام `redactor.Save("sample_redacted.pdf")`.

### تطبيقات عملية

#### حالات الاستخدام في العالم الحقيقي
1. **إدارة المستندات القانونية** – ابحث عن العقود بفعالية وقم تلقائيًا بتشويه معرفات العملاء.  
2. **سجلات الرعاية الصحية** – حدد ملاحظات المرضى مع ضمان تشويه PHI وفقًا لمتطلبات HIPAA.  
3. **الامتثال المؤسسي** – افحص الاتصالات الداخلية للبحث عن مصطلحات محظورة وقم بتشويهها قبل الأرشفة.

## الخاتمة
يوفر هذا الدليل مسارًا شاملاً لـ **إنشاء فهرس بحث .NET** حل يتوسع، يفهرس بسرعة، ويحمي البيانات عبر التشويه. من خلال تكوين العقد، فهرسة المستندات، الاستفادة من ميزات البحث المتقدمة، وتطبيق التشويه، يمكن للمطورين تحسين سير عمل إدارة المستندات بشكل كبير مع الحفاظ على معايير أمان صارمة.

## الأسئلة المتكررة

**س: كيف أقوم بإعداد شبكة بحث موزعة في .NET باستخدام GroupDocs؟**  
ج: حدد مسار قاعدة ومنفذ، ثم استدعِ `SearchNetworkDeployment.Deploy()` لإطلاق العقد الرئيسية والعاملية عبر الأجهزة.

**س: هل يمكنني إجراء بحث متقدم مع عدة معلمات في GroupDocs؟**  
ج: نعم—استخدم `SearchOptions` لدمج المطابقة الضبابية، دعم الأحرف البديلة، وتحديد النتائج في استعلام واحد.

**س: هل يمكن مراقبة نشاط الشبكة على العقدة الرئيسية؟**  
ج: بالتأكيد—اشترك في `SearchNetworkNodeEvents` مثل `IndexingCompleted` و `QueryExecuted` للحصول على رؤى في الوقت الحقيقي.

**س: كيف يمكنني تطبيق التشويه على ملفات PDF باستخدام GroupDocs؟**  
ج: ابدأ بإنشاء `Redactor`، حمّل ملف PDF، عرّف كائنات `RedactionPattern` (regex أو سلاسل نصية حرفية)، استدعِ `Apply`، واحفظ المستند المنقّح.

**س: ما هي أسهل طريقة لتحسين أداء البحث في بيئة شبكية؟**  
ج: قم بفهرسة مجموعة المستندات بالكامل قبل الاستعلامات، وزّع العقد للاستفادة من المعالجة المتوازية، واضبط `SearchOptions` للتخزين المؤقت والصفحات.

**آخر تحديث:** 2026-06-12  
**تم الاختبار مع:** GroupDocs.Search 23.9 لـ .NET، GroupDocs.Redaction 23.9 لـ .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [إتقان فهرسة مستندات .NET مع GroupDocs.Search: دليل شامل](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [إتقان فهرسة المستندات واستعلامات البحث المتقدمة مع GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [إتقان GroupDocs Search و Redaction في .NET: إدارة مستندات متقدمة](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
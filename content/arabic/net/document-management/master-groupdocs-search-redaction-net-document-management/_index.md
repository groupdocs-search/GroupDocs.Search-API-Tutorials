---
date: '2026-07-16'
description: تعلم كيفية حذف المعلومات الحساسة من المستندات في .NET باستخدام GroupDocs
  Search و Redaction، بالإضافة إلى تمييز نتائج البحث لتسريع إدارة المستندات.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: تعلم كيفية حذف المعلومات الحساسة من المستندات في .NET باستخدام GroupDocs
  Search و Redaction، بالإضافة إلى تمييز نتائج البحث لتسريع إدارة المستندات.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: كيفية حذف المعلومات الحساسة من المستندات باستخدام GroupDocs Search في .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: كيفية حذف المعلومات الحساسة من المستندات باستخدام GroupDocs Search في .NET
type: docs
url: /ar/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# كيفية تمويه المستندات باستخدام GroupDocs Search في .NET

في المؤسسات الحديثة، **كيفية تمويه المستندات** بسرعة وأمان هي تحدٍ يومي. يوفّر استخدام GroupDocs.Search مع GroupDocs.Redaction لـ .NET حلاً قويًا جاهزًا لا يقتصر فقط على تمويه المحتوى الحساس بل يتيح لك أيضًا إجراء عمليات بحث غير دقيقة و**تمييز نتائج البحث** في HTML. يشرح هذا البرنامج التعليمي كيفية تثبيت المكتبات، إنشاء فهرس، تشغيل استعلام غير دقيق، وإنتاج مخرجات مميزة — كل ذلك باستخدام مقتطفات شفرة واضحة وجاهزة للإنتاج.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** تثبيت حزم NuGet الخاصة بـ GroupDocs.Search و GroupDocs.Redaction.  
- **هل يمكنني تمويه ملفات PDF و Word؟** نعم، كلا التنسيقين مدعومان مباشرة.  
- **هل البحث غير الدقيق متاح؟** بالتأكيد – يمكنك ضبط الدقة من 0 % إلى 100 %.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مجاني يعمل للاختبار؛ يلزم ترخيص مدفوع للإنتاج.  
- **هل سيعمل الحل على .NET 6؟** نعم، المكتبات متوافقة مع .NET Framework 4.5+، .NET Core 3.1+، .NET 5+، و .NET 6+.

## ما هو GroupDocs.Search؟
GroupDocs.Search هي مكتبة .NET توفر فهرسة سريعة والبحث النصي الكامل عبر أكثر من 100 تنسيق ملف. يمكنها معالجة المستندات حتى 2 GB دون تحميل الملف بالكامل إلى الذاكرة، مما يجعلها مثالية للمستودعات الضخمة. تدعم الفهرسة التزايدية، التحليل متعدد اللغات، وتندمج بسلاسة مع تطبيقات .NET، مما يتيح للمطورين بناء تجارب بحث قوية بأقل قدر من الشفرة.

## لماذا نستخدم GroupDocs.Redaction لتمويه المستندات؟
GroupDocs.Redaction تقدم أكثر من 30 نمط تمويه مدمج وتدعم المعالجة الدفعية، مما يضمن إزالة البيانات الشخصية، البنود السرية، أو العلامات التنظيمية بشكل دائم. في اختبارات الأداء، يستغرق تمويه ملف PDF مكوّن من 500 صفحة أقل من ثانيتين على خادم عادي. يعمل المحرك على تدفق محتوى المستند، مما يضمن عدم إمكانية استعادة المناطق المموهة، ويحافظ على التنسيق والتخطيط الأصلي.

## المتطلبات المسبقة
- **المكتبات المطلوبة:** GroupDocs.Search، GroupDocs.Redaction  
- **المنصات المدعومة:** .NET Framework 4.5+، .NET Core 3.1+، .NET 5+، .NET 6+  
- **بيئة التطوير المتكاملة:** Visual Studio 2022 أو أحدث (أي إصدار)  
- **المهارات الأساسية:** الإلمام بـ C#، إدخال/إخراج الملفات، ومفاهيم البرمجة الكائنية.

## كيف تقوم بإعداد GroupDocs.Search و GroupDocs.Redaction في مشروع .NET؟
قم بتثبيت حزم NuGet عبر .NET CLI أو Package Manager Console أو واجهة المستخدم، ثم أضف ملف الترخيص إلى مشروعك. هذه الإعدادات ذات الخطوتين هي كل ما تحتاجه قبل كتابة أي شفرة فهرسة أو تمويه. بعد إضافة الحزم، يجب وضع ملف الترخيص في جذر التطبيق وإحالة المساحات الاسمية في ملفات الشفرة الخاصة بك.

## إعداد GroupDocs.Redaction لـ .NET
لبدء استخدام GroupDocs.Search و GroupDocs.Redaction في تطبيقات .NET الخاصة بك، اتبع خطوات التثبيت التالية:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ابحث عن "GroupDocs.Redaction" وقم بتثبيت أحدث نسخة.

### خطوات الحصول على الترخيص
1. **إصدار تجريبي**: سجّل على [GroupDocs](https://www.groupdocs.com) للحصول على ترخيص مؤقت.  
2. **شراء**: للحصول على وصول كامل، اشترِ ترخيصًا من موقع GroupDocs.  
3. **ترخيص مؤقت**: احصل عليه لأغراض التقييم عبر الرابط المقدم.

#### التهيئة الأساسية والإعداد
تمثل الفئة `Index` فهرسًا قابلًا للبحث يُخزن على القرص وتوفر طرقًا لإضافة، تحديث، واستعلام المستندات. بعد التثبيت، قم بتهيئة مشروعك بالإعدادات اللازمة:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## دليل التنفيذ

### إنشاء وفهرسة المستندات
**نظرة عامة**  
هذه الميزة توضح كيفية تنظيم المستندات بكفاءة عن طريق إنشاء فهرس لمجلد يحتوي على ملفات متعددة.

#### الخطوة 1: تحديد المسارات  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### إعداد وتنفيذ البحث غير الدقيق
**نظرة عامة**  
يسمح البحث غير الدقيق لك بالعثور على المستندات حتى مع وجود اختلافات بسيطة في مصطلحات البحث. تُظهر هذه الميزة إعداد بحث غير دقيق بدقة قابلة للتعديل.

#### الخطوة 1: تمكين البحث غير الدقيق  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### تمييز نتائج البحث بتنسيق HTML
**نظرة عامة**  
تمييز نتائج البحث يحدد بصريًا الأقسام ذات الصلة داخل الملف، مما يسهل التحليل السريع.

#### الخطوة 1: إعداد ضغط عالي  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### الخطوة 2: التمييز والإخراج  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### نصائح استكشاف الأخطاء وإصلاحها
- تأكد من تحديد المسارات بشكل صحيح لتجنب أخطاء عدم العثور على الملف.  
- تحقق من ضبط جميع الأذونات اللازمة لعمليات القراءة/الكتابة على الأدلة.  

## التطبيقات العملية
1. **مراجعة المستندات القانونية** – تحديد المصطلحات المتعلقة بالقضايا بسرعة في مجموعات قانونية ضخمة.  
2. **البحث الأكاديمي** – البحث عبر آلاف الأوراق العلمية عن منهجيات محددة.  
3. **تحليل الأعمال** – استخراج المقاييس الرئيسية من التقارير الفصلية دون الحاجة إلى البحث اليدوي.  
4. **دعم العملاء** – فحص تذاكر الدعم للعثور على المشكلات المتكررة وتمويه البيانات الشخصية قبل التحليل.  
5. **أنظمة إدارة المحتوى (CMS)** – تحسين استرجاع المحتوى باستخدام البحث غير الدقيق والتمويه التلقائي للقطع الحساسة.  

## اعتبارات الأداء
- تحسين إعدادات تخزين الفهرس لتحقيق توازن بين السرعة واستهلاك القرص.  
- تحديث الفهارس بانتظام للحفاظ على حداثة البيانات، مما يقلل من المعالجة غير الضرورية.  
- التخلص من الكائنات غير المستخدمة بسرعة لمنع تسرب الذاكرة، خاصةً عند معالجة دفعات كبيرة.  

## كيفية تمويه المعلومات الحساسة من ملف PDF باستخدام GroupDocs Redaction؟
`Redactor` هي الفئة الرئيسية المستخدمة لتطبيق أنماط التمويه على صيغ المستندات المدعومة. حمّل ملف PDF المستهدف باستخدام `Redactor redactor = new Redactor("file.pdf")`، عرّف نمط تمويه (مثال: `redactor.AddRedaction(new RedactionPhrase("confidential"))`)، ثم استدعِ `redactor.Apply()` – تقوم المكتبة بالكتابة فوق الملف الأصلي بالمحتوى المموه مع الحفاظ على التخطيط. يضمن هذا التدفق خطوة واحدة عدم بقاء أي أثر للعبارة المحمية.

## كيفية تمييز نتائج البحث في HTML بعد استعلام غير دقيق؟
`SearchResultHighlighter` توفر أدوات لإنشاء مقاطع HTML مميزة من نتائج البحث. نفّذ الاستعلام غير الدقيق، استرجع القطع المتطابقة، ومرّرها إلى `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`. تقوم الطريقة بلف كل ظهور بالوسوم المقدمة، مما ينتج مقطع HTML حيث يتم إبراز كل مصطلح ذي صلة بصريًا. يمكن تضمين HTML المميز مباشرةً في صفحات الويب أو حفظه كتقرير، مما يسهل على المستخدمين النهائيين رؤية سياق كل تطابق.

## الأسئلة المتكررة
**س: ما هو البحث غير الدقيق؟**  
ج: البحث غير الدقيق يجد التطابقات التقريبية، ويتسامح مع الأخطاء الإملائية أو الاختلافات الطفيفة في مصطلح الاستعلام.

**س: هل يمكنني استخدام هذه المكتبات في مشروع تجاري؟**  
ج: نعم، ترخيص GroupDocs صالح يمنح حقوق الاستخدام التجاري.

**س: كيف يمكنني التعامل مع مجموعات مستندات كبيرة بكفاءة؟**  
ج: استخدم الفهرسة التزايدية، اضبط `IndexingOptions` لحجم الدفعة، وجدول عمليات إعادة بناء الفهرس بانتظام للحفاظ على الأداء المثالي.

**س: ما هي صيغ الملفات التي يدعمها GroupDocs.Search؟**  
ج: يتم دعم أكثر من 100 صيغة، بما في ذلك PDF، DOCX، XLSX، PPTX، HTML، TXT، وأنواع الصور مثل JPEG و PNG.

**س: هل هناك دعم متعدد اللغات للبحث والتمويه؟**  
ج: نعم، تشمل المكتبات محللات لغوية لأكثر من 30 لغة، مما يتيح بحثًا وتمويهاً دقيقًا عبر المحتوى العالمي.

## الموارد
- [التوثيق](https://docs.groupdocs.com/search/net/)  
- [التوثيق](https://docs.groupdocs.com/search/net/)  
- [منتدى الدعم](https://forum.groupdocs.com/c/search/10)  
- [مرجع API](https://reference.groupdocs.com/redaction/net)  
- [تحميل](https://www.groupdocs.com/products/search-net)

---

**آخر تحديث:** 2026-07-16  
**تم الاختبار مع:** GroupDocs.Search 2.0.0 و GroupDocs.Redaction 2.0.0 لـ .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة
- [تمييز نتائج البحث في مستندات .NET باستخدام GroupDocs.Search و Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)  
- [إتقان GroupDocs Redaction والبحث في .NET: إدارة مستندات فعّالة والبحث الآمن](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)  
- [إتقان تمويه المستندات باستخدام GroupDocs.Redaction .NET: الفهرسة وإدارة الأسماء المستعارة لإدارة مستندات آمنة](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)
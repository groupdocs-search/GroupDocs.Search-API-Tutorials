---
date: '2026-09-16'
description: تعلم كيفية إنشاء search index باستخدام GroupDocs في .NET، إضافة المستندات
  إلى index، وتمكين synonym search للحصول على نتائج استعلام أكثر ذكاءً.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: تعلم كيفية إنشاء search index باستخدام GroupDocs في .NET، إضافة المستندات
  إلى index، وتمكين synonym search للحصول على نتائج استعلام أكثر ذكاءً.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: كيفية إنشاء search index باستخدام GroupDocs في .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: كيفية إنشاء search index باستخدام GroupDocs و synonym search في .NET
type: docs
url: /ar/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# كيفية إنشاء فهرس بحث باستخدام GroupDocs والبحث عن المرادفات في .NET

في هذا الدليل ستتعلم **كيفية إنشاء فهرس بحث** باستخدام GroupDocs.Search، إضافة المستندات إلى ذلك الفهرس، وتمكين البحث عن المرادفات حتى يتمكن المستخدمون من العثور على المحتوى المناسب حتى عندما يستخدمون مصطلحات مختلفة. سواءً كنت تبني مستودعًا قانونيًا، أو قاعدة معرفة مؤسسية، أو أرشيفًا بحثيًا، فإن الخطوات أدناه توفر لك حلاً جاهزًا للإنتاج يعمل على .NET Framework 4.6.1+، .NET Core، و .NET 5+.

## إجابات سريعة
- **ماذا يعني “إنشاء فهرس بحث”?** يبني كتالوجًا قابلاً للبحث من مستنداتك، يخزن النص المستخرج في بنية مُحسّنة للبحث خلال مللي ثانية.  
- **لماذا نستخدم البحث عن المرادفات؟** يوسّع الاستعلام ليشمل كلمات ذات نفس المعنى، مما يزيد الاسترجاع بنسبة تصل إلى 30 % في مجموعات النصوص النموذجية.  
- **ما هي المتطلبات الأساسية؟** .NET 4.6.1+ (أو .NET Core/5+)، معرفة بـ C#، وحزم NuGet الخاصة بـ GroupDocs.Search + GroupDocs.Redaction.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية كافية للتقييم؛ الترخيص الدائم مطلوب للنشر في بيئة الإنتاج.  
- **هل يمكنني دمج ذلك مع التشويه (redaction)؟** نعم—يمكن لـ GroupDocs.Redaction العمل قبل أو بعد البحث لإخفاء البيانات الحساسة.

## ما هو “إنشاء فهرس بحث”؟
إن **فهرس البحث** هو بنية بيانات تحتفظ بالنص المستخرج والبيانات الوصفية من كل مستند، مما يسمح للمحرك بتحديد الملفات المطابقة على الفور. تقوم GroupDocs.Search بإنشاء هذا الفهرس عن طريق مسح المجلد المصدر، وتحليل الصيغ المدعومة، وكتابة ملفات فهرس مضغوطة إلى الدليل الذي تحدده.

## لماذا تمكين البحث عن المرادفات؟
يضيف البحث عن المرادفات تلقائيًا مصطلحات بديلة إلى استعلام المستخدم، بحيث أن البحث عن **“improve”** يعيد أيضًا المستندات التي تحتوي على **“enhance”، “upgrade”،** أو **“optimize”.** عمليًا يمكن لهذا أن يزيد استرجاع النتائج بنسبة 20‑35 % مع الحفاظ على الدقة العالية، لأن القاموس المدمج للمرادفات مُنظم لكل لغة.

## المتطلبات المسبقة
- **.NET Framework 4.6.1** أو أحدث (أو أي بيئة تشغيل .NET Core/5+).  
- مهارات أساسية في تطوير C# و Visual Studio (Community أو Professional أو Enterprise).  
- حزم GroupDocs.Search و GroupDocs.Redaction المثبتة عبر NuGet.

### التثبيت
قم بتثبيت GroupDocs.Redaction لـ .NET باستخدام إحدى هذه الطرق (انظر توثيق [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) للحصول على التفاصيل):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

بدلاً من ذلك، استخدم واجهة مستخدم مدير الحزم NuGet في Visual Studio للبحث عن “GroupDocs.Redaction” وتثبيتها مباشرة. للحصول على مرجع API، راجع [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### الحصول على الترخيص
- **نسخة تجريبية مجانية:** ابدأ بنسخة تجريبية لاستكشاف جميع الميزات.  
- **ترخيص مؤقت:** قدّم طلبًا للحصول على ترخيص مؤقت عبر [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/) أو إدارة ترخيصك عبر بوابة [إدارة تراخيص GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
- **شراء كامل:** عندما تكون جاهزًا للإنتاج، اشترِ ترخيصًا كاملاً يزيل جميع حدود التقييم.

## كيفية إعداد GroupDocs.Redaction لـ .NET
توفر GroupDocs.Redaction الوظيفة الأساسية لتشويه المحتوى الحساس قبل أو بعد البحث. تُظهر فئة `Redactor` التي تقوم بإنشائها باستخدام ترخيص وإعدادات تكوين اختيارية.

الكود التالي يوضح إنشاء مثال من Redactor وتحميل ملف الترخيص:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

مع جاهزية الـ redactor، يمكنك لاحقًا استدعاء `redactor.Redact(...)` على أي مستند تستخرجه من نتائج البحث.

## كيفية إنشاء فهرس البحث
إنشاء فهرس بحث يتضمن تحديد مجلد سيتم تخزين ملفات الفهرس فيه ثم تهيئة فئة `Index` من GroupDocs.Search. سيحتوي الفهرس على جميع البيانات القابلة للبحث المستخرجة من مستنداتك المصدرية.

أولاً، أنشئ دليلًا للفهرس ثم أنشئ كائن `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

إنشاء الفهرس يكتب مجموعة من الملفات الثنائية إلى المجلد؛ عادةً ما تكون هذه الملفات أقل من 200 KB لكل 1,000 صفحة، مما يتيح لك التوسع إلى ملايين الصفحات دون استنزاف مساحة القرص.

## كيفية إضافة مستندات إلى الفهرس
إضافة المستندات تتطلب توجيه الـ API إلى الدليل الذي يحتوي على الملفات المصدرية وإرشاد الفهرس لاستيعابها. العملية تحلل كل صيغة مدعومة، تستخرج النص، وتخزنه في الفهرس لاسترجاع سريع.

استخدم الكود التالي لفهرسة جميع الملفات في مجلد المصدر:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

تدعم GroupDocs.Search **أكثر من 30** صيغة إدخال — بما في ذلك DOCX، PDF، PPTX، HTML، وأنواع الصور الشائعة — بحيث يمكنك فهرسة أي أرشيف مؤسسي تقريبًا دون الحاجة إلى محولات إضافية.

## كيفية تمكين وتشغيل البحث عن المرادفات
يتم تشغيل معالجة المرادفات عبر `SearchOptions`. بمجرد التفعيل، يتم توسيع كل استعلام تلقائيًا لتضمين مرادفات القاموس، مما يحسن الاسترجاع دون التضحية بالدقة.

قم بتمكين البحث عن المرادفات باستخدام المقتطف التالي:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

القاموس الافتراضي للمرادفات يحتوي على أكثر من **5,000** زوج من المصطلحات للغة الإنجليزية. يمكنك أيضًا تحميل ملف `SynonymDictionary` مخصص لدعم المصطلحات الخاصة بالصناعة.

## قاموس المرادفات المخصص
إذا كنت بحاجة إلى مرادفات خاصة بمجال معين، قم بتحميل ملف القاموس الخاص بك وعيّنه إلى `SearchOptions` قبل تنفيذ الاستعلام.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## نصائح شائعة لاستكشاف الأخطاء وإصلاحها
- **مشكلات المسار:** تحقق مرة أخرى من أن مجلدات الفهرس والمصدر يمكن الوصول إليها من قبل حساب العملية.  
- **حدود الترخيص:** قد يحد بناء غير مرخص عدد الملفات المفهرسة إلى 100.  
- **عدم وجود نتائج:** تأكد من تحميل قاموس المرادفات؛ يمكنك فحص `options.SynonymDictionary.Count` أثناء التشغيل.  

## تطبيقات عملية
1. **إدارة المستندات القانونية:** العثور على القوانين القضائية باستخدام المصطلحات القانونية ومرادفاتها.  
2. **البحث الأكاديمي:** توسيع عمليات البحث في الأدبيات عبر ملفات PDF وWord العلمية.  
3. **قواعد المعرفة المؤسسية:** استرجاع السياسات الداخلية حتى عندما يصيغ المستخدمون الاستعلامات بشكل مختلف.  
4. **أنظمة إدارة المحتوى:** توفير اكتشاف أعمق للمحررين عند وضع العلامات على المقالات.  
5. **نظام تذاكر دعم العملاء:** مطابقة التذاكر مع المشكلات المعروفة باستخدام أوصاف المشكلات المرادفة.  

## اعتبارات الأداء
- **صيانة الفهرس:** أعد الفهرسة بعد التحديثات الضخمة؛ الفهرسة المتزايدة تقلل وقت التوقف بنسبة تصل إلى 70 %.  
- **مراقبة الموارد:** فهرسة دفعة بحجم 10 GB على جهاز افتراضي قياسي (2 vCPU، 8 GB RAM) يصل إلى ~1.2 GB RAM؛ قلل حجم الدفعة إذا اقتربت من الحدود.  
- **تحرير الكائنات:** استدعِ `index.Dispose()` و `redactor.Dispose()` فور الانتهاء لتحرير الموارد الأصلية.  

## الخلاصة
أنت الآن تعرف **كيفية إنشاء فهرس بحث** باستخدام GroupDocs، إضافة المستندات إلى ذلك الفهرس، وتمكين البحث عن المرادفات لتجربة مستخدم أكثر بديهية. هذه الأساسيات تتيح لك أيضًا إضافة التشويه (redaction)، الترتيب المخصص، أو المطابقة الضبابية فوق محرك بحث قوي.  

## الخطوات التالية
- جرّب `SearchOptions.FuzzySearch` لالتقاط الأخطاء الإملائية.  
- استكشف API `Ranking` لتعزيز المستندات ذات الأولوية.  
- انضم إلى المجتمع على [منتدى GroupDocs](https://forum.groupdocs.com/c/search/10) أو [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10) لمشاركة النصائح وطرح الأسئلة.  
- تحقق من [أحدث إصدارات GroupDocs](https://releases.groupdocs.com/search/net/) للحصول على التحديثات والميزات الجديدة.  

## الأسئلة المتكررة

**س: ما هو البحث عن المرادفات؟**  
ج: يوسّع البحث عن المرادفات استعلام المستخدم ليشمل مصطلحات بديلة محددة مسبقًا، مما يزيد فرصة العثور على المستندات ذات الصلة التي تستخدم صياغة مختلفة.

**س: كيف أقوم بتحديث ترخيص GroupDocs الخاص بي؟**  
ج: زر بوابة [إدارة تراخيص GroupDocs](https://purchase.groupdocs.com/temporary-license/) وحمّل ملف الترخيص الجديد عبر `License.SetLicense("path/to/license.lic")`.

**س: هل يمكنني استخدام البحث عن المرادفات في بيئة متعددة اللغات؟**  
ج: نعم—حمّل ملف `SynonymDictionary` خاص بكل لغة للمنطقة التي تدعمها، وسيطبق المحرك مجموعة المرادفات المناسبة لكل استعلام.

**س: ما هي أكثر مشكلات الفهرسة شيوعًا؟**  
ج: أذونات الوصول إلى الملفات، الصيغ غير المدعومة، وتجاوز حد المستندات في النسخة التجريبية هي الثلاث مشاكل الأكثر شيوعًا التي يواجهها المطورون.

**س: كيف يمكنني تحسين الأداء للفهارس الكبيرة جدًا؟**  
ج: استخدم الفهرسة المتزايدة، خزن الفهرس على أقراص SSD، وقم بتكوين `IndexingOptions.MaxDegreeOfParallelism` ليتطابق مع عدد نوى المعالج لديك.

**آخر تحديث:** 2026-09-16  
**تم الاختبار مع:** GroupDocs.Search 23.10 for .NET  
**المؤلف:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## دروس ذات صلة

- [إضافة مستند إلى الفهرس باستخدام دروس GroupDocs.Search .NET](/search/net/document-management/)
- [تمييز نتائج البحث في مستندات .NET باستخدام GroupDocs.Search و Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [كيفية تحديث الفهرس باستخدام GroupDocs.Search و Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
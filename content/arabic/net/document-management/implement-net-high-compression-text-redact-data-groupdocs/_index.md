---
date: '2026-06-07'
description: تعلم كيفية تنفيذ ضغط عالي .NET لتخزين النصوص وتصحيح البيانات السرية باستخدام
  GroupDocs.Search و GroupDocs.Redaction في تطبيقات .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'تنفيذ ضغط عالي .NET مع GroupDocs: دليل النص والتصحيح'
type: docs
url: /ar/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# تنفيذ ضغط عالي .NET مع GroupDocs: دليل النص وإزالة المعلومات الحساسة

في حلول .NET الحديثة، يُعد **implement high compression .net** أمرًا أساسيًا عندما تحتاج إلى تخزين مجموعات نصية ضخمة دون استهلاك مساحة القرص. في الوقت نفسه، يتطلب حماية المعلومات الحساسة—مثل المعرفات الشخصية أو الأرقام المالية—إزالة معلومات موثوقة. يوضح هذا الدليل، خطوة بخطوة، كيفية تكوين تخزين نصي بضغط عالي باستخدام **GroupDocs.Search** وكيفية إزالة البيانات السرية بأمان باستخدام **GroupDocs.Redaction**. في النهاية، ستتمكن من ضغط النص المفهرس بنسبة تصل إلى 90 % وإزالة المحتوى الخاص من ملفات PDF وWord والعديد من الصيغ الأخرى.

## إجابات سريعة
- **ما المكتبة التي توفر فهرسة ضغط عالي؟** GroupDocs.Search for .NET.  
- **ما الأداة التي تزيل البيانات الحساسة؟** GroupDocs.Redaction for .NET.  
- **هل يمكنني إضافة مستندات إلى الفهرس تلقائيًا؟** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **هل الضغط غير فقدان للبيانات بالنسبة للبحث؟** Yes, the text remains fully searchable after compression.  
- **هل أحتاج إلى ترخيص للإنتاج؟** A permanent GroupDocs license is required for commercial use.

## ما هو “implement high compression .net”؟
يعني تنفيذ ضغط عالي .net تكوين محرك فهرسة GroupDocs.Search لتخزين المحتوى النصي المستخرج في شكل مضغوط. هذا يقلل بشكل كبير من حجم الفهرس على القرص مع الحفاظ على إمكانية البحث الكامل في النص. الضغط غير فقدان للبيانات، لذا تعمل صلة الاستعلام واستخراج المقاطع بنفس الطريقة كما في الفهرس غير المضغوط.

## لماذا استخدام GroupDocs للضغط وإزالة المعلومات الحساسة؟
يدعم GroupDocs.Search أكثر من خمسين صيغة إدخال ويمكنه ضغط النص المفهرس بنسبة تصل إلى تسعين بالمئة، مما يسمح لمجموعات المستندات الكبيرة باحتلال جزء صغير فقط من حجمها الأصلي. يكمل GroupDocs.Redaction ذلك عن طريق محو أو إخفاء المعلومات الحساسة بشكل دائم في أكثر من ثلاثين نوعًا من الملفات، مما يساعدك على الالتزام باللوائح الصارمة مثل GDPR وHIPAA دون الحاجة إلى أدوات إضافية.

## المتطلبات المسبقة
- **بيئة التطوير:** Visual Studio 2022 أو أحدث، .NET 6+ (أو .NET Framework 4.7.2).  
- **المكتبات:** حزم NuGet `GroupDocs.Search` و `GroupDocs.Redaction`.  
- **الأذونات:** صلاحية قراءة/كتابة للمجلدات التي تحتوي على المستندات المصدر وموقع إخراج الفهرس.  
- **المعرفة الأساسية:** صsyntax C#، إدخال/إخراج الملفات، ومعرفة بنية مشروع .NET.

## كيف تنفذ ضغط عالي .NET مع GroupDocs؟
لتنفيذ ضغط عالي .NET مع GroupDocs، ابدأ بإنشاء كائن `TextStorageSettings` واضبط خاصية `CompressionLevel` إلى `High`. ثم أنشئ كائن `Index`، مع تمرير الإعدادات والمجلد الذي سيُخزن فيه الفهرس. بعد أن يصبح الفهرس جاهزًا، أضف المستندات باستخدام `AddDocument`، وأخيرًا نفّذ عمليات البحث باستخدام طريقة `Search`، بينما يتعامل المحرك بشكل شفاف مع الضغط وفك الضغط.

### الخطوة 1: تثبيت حزم NuGet المطلوبة
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- ابحث عن “GroupDocs.Search” وانقر **Install**.  

### الخطوة 2: تثبيت GroupDocs.Redaction (لإزالة البيانات)
- افتح **NuGet Package Manager**.  
- ابحث عن **GroupDocs.Redaction** وقم بتثبيت أحدث نسخة مستقرة.  

### الخطوة 3: الحصول على ترخيص وتطبيقه
- **نسخة تجريبية مجانية:** سجّل في بوابة GroupDocs للحصول على مفتاح تجريبي لمدة 30 يومًا.  
- **ترخيص مؤقت:** اطلب مفتاحًا مؤقتًا لبيئات التطوير.  
- **ترخيص دائم:** اشترِ ترخيصًا للإنتاج لإزالة قيود التقييم.

### الخطوة 4: التهيئة الأساسية للمكتبتين
تشارك محركات `Search` و `Redaction` نموذج ترخيص مشترك. قم بتهيئتها عند بدء تشغيل التطبيق:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## الميزة 1: إعدادات تخزين النص بضغط عالي

### إعداد تكوين الفهرسة
`TextStorageSettings` هي الفئة التي تخبر GroupDocs.Search كيفية حفظ النص المستخرج. تمكين الضغط العالي يقلل حجم الفهرس بنسبة تصل إلى **10×** دون التأثير على سرعة البحث.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**شرح:**  
- `CompressionLevel.High` يُفعِّل خوارزمية تعتمد على ZSTD تضغط كتل النص بفعالية.  
- `UseMemoryCache = false` يجبر المحرك على بث البيانات من القرص، وهو مثالي للنشر على نطاق واسع.

### إنشاء وإدارة الفهرس
كائن `Index` يمثل المستودع القابل للبحث على القرص. تحدد المجلد الذي ستُخزن فيه ملفات الفهرس وتمرر إعدادات الضغط المحددة أعلاه.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**شرح:**  
- `indexFolder` يحدد مكان وجود ملفات الفهرس المضغوطة.  
- `settings` يدمج إعداد الضغط العالي، مما يضمن استفادة كل مستند مضاف منه.

## الميزة 2: إضافة مستندات إلى الفهرس

### إضافة مستندات إلى الفهرس الخاص بك
`AddDocument` يضيف ملفًا واحدًا إلى الفهرس، يستخرج نصه، يضغطه وفقًا للإعدادات المكوَّنة، ويخزن النتيجة. يمكن لـ GroupDocs.Search استيعاب الملفات من شجرة الدليل. الحلقة التالية تتجول عبر `documentsFolder`، تضيف كل ملف، وتسجل التقدم.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**شرح:**  
- `AddDocument` يحلل الملف، يستخرج النص القابل للبحث، يضغطه وفقًا لـ `TextStorageSettings`، ويخزنه في الفهرس.  
- هذا النهج يعمل مع **PDF, DOCX, TXT, HTML** وأكثر من **30** صيغة أخرى.

## الميزة 3: تنفيذ استعلام بحث

### تنفيذ بحث
`Search` ينفّذ استعلامًا على الفهرس المضغوط ويعيد مجموعة من كائنات `DocumentResult` المتطابقة مع درجات الصلة ومقاطع مميزة. بمجرد ملء الفهرس، يمكنك تشغيل استعلامات سريعة. طريقة `Search` تُعيد مجموعة من كائنات `DocumentResult` التي تشمل مسارات الملفات والمقاطع المميزة.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**شرح:**  
- يقوم محرك البحث بمسح النص المضغوط مباشرة، لذا يبقى زمن استجابة الاستعلام منخفضًا حتى للفهارس التي تحتوي على **ملايين الصفحات**.  
- `Score` يشير إلى الصلة؛ القيم الأعلى تعني تطابقًا أفضل.

## كيف تزيل البيانات السرية باستخدام GroupDocs.Redaction؟
بدءًا بإزالة البيانات السرية باستخدام GroupDocs.Redaction يتم بإنشاء كائن `Redactor` للملف المستهدف. عرّف كائنًا أو أكثر من `SearchPattern` يصف النص المراد إزالته، مثل التعبيرات النمطية لأرقام الضمان الاجتماعي. طبّق كل نمط باستخدام `Redact`، محددًا `RedactionType` مثل `BlackOut`، واحفظ النتيجة كمستند جديد، مع ضمان بقاء الأصل دون تعديل.

`Redactor` هو الفئة الأساسية في GroupDocs.Redaction المستخدمة لتحميل المستند وتنفيذ عمليات الإزالة.  
`SearchPattern` يحدد تعبيرًا نمطيًا يحدد النص الذي سيُزال.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**شرح:**  
- `SearchPattern` يستخدم تعبيرًا نمطيًا لتحديد أرقام الضمان الاجتماعي.  
- `RedactionType.BlackOut` يستبدل النص المطابق بمستطيل أسود صلب، مما يضمن عدم إمكانية استعادة البيانات.

## تطبيقات عملية
1. **إدارة المستندات القانونية:** ضغط ملفات القضايا الضخمة تلقائيًا وإزالة معرفات العملاء قبل الأرشفة.  
2. **سجلات الرعاية الصحية:** تخزين سنوات من ملاحظات المرضى في فهرس مضغوط وإزالة معلومات الصحة المحمية (PHI) قبل مشاركتها مع شركاء البحث.  
3. **التقارير المالية:** تأمين التقارير ربع السنوية بإزالة أرقام الحسابات مع الحفاظ على النص القابل للبحث لاستفسارات التدقيق.

## اعتبارات الأداء
- **تأثير الضغط:** الضغط العالي يقلل حجم الفهرس بنسبة تصل إلى **90 %**، مما يقلل من تآكل SSD ويسرّع عمليات النسخ الاحتياطي.  
- **استخدام الذاكرة:** عطل التخزين المؤقت في الذاكرة للفهارس الكبيرة جدًا للحفاظ على حجم العملية أقل من **500 MB**.  
- **تحسين الإدخال/الإخراج:** أضف المستندات على دفعات من 100 لتقليل اضطراب القرص.  
- **المعالجة غير المتزامنة:** غلف استدعاءات `AddDocument` داخل `Task.Run` للحفاظ على استجابة خيوط واجهة المستخدم في تطبيقات سطح المكتب.

## المشكلات الشائعة وإصلاح الأخطاء
- **مسارات ملفات غير صحيحة:** تأكد من أن `documentsFolder` و `indexFolder` مسارات مطلقة وأن التطبيق لديه صلاحيات قراءة/كتابة.  
- **أخطاء الترخيص:** تأكد من نشر ملفات `.lic` بجانب الملف التنفيذي أو تضمينها كموارد.  
- **البحث لا يُرجع نتائج:** تحقق من أن مستوى ضغط `TextStorageSettings` يطابق المستوى المستخدم أثناء الفهرسة؛ الإعدادات غير المتطابقة قد تتسبب في فشل فك التسلسل.

## الأسئلة المتكررة

**س: هل يمكنني إضافة مستندات إلى الفهرس بعد الإنشاء الأولي؟**  
ج: نعم—ما عليك سوى استدعاء `index.AddDocument` للملفات الجديدة؛ يقوم المحرك بتحديث الفهرس المضغوط بشكل تدريجي.

**س: هل تؤثر الإزالة على الملف الأصلي؟**  
ج: لا—الملف الأصلي يبقى دون تعديل؛ يتم حفظ النسخة المُزالة كملف جديد، مع الحفاظ على سلامة المستند.

**س: ما الصيغ التي يدعمها GroupDocs.Redaction؟**  
ج: أكثر من **30** صيغة، بما في ذلك PDF، DOCX، PPTX، XLSX، الصور (PNG، JPEG)، والنص العادي.

**س: كيف يؤثر الضغط العالي على صلة البحث؟**  
ج: لا يؤثر. الضغط غير فقدان للبيانات للنص، لذا تكون درجات الصلة مطابقة لتلك في فهرس غير مضغوط.

**س: هل هناك حد لحجم المستندات التي يمكنني فهرستها؟**  
ج: يمكن لـ GroupDocs.Search التعامل مع ملفات متعددة الجيجابايت عن طريق بث المحتوى؛ ومع ذلك، تأكد من توفر مساحة قرص كافية للفهرس المضغوط (حوالي 10 % من الحجم الأصلي).

## موارد
- [الوثائق](https://docs.groupdocs.com/search/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل GroupDocs.Redaction لـ .NET](https://releases.groupdocs.com/search/net/)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)
- [الحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-06-07  
**تم الاختبار مع:** GroupDocs.Search 23.12 و GroupDocs.Redaction 23.12 لـ .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [تنفيذ GroupDocs.Search وإزالة المعلومات في .NET لإدارة المستندات](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [كيفية تحسين GroupDocs.Redaction لـ .NET: دليل إدارة الفهرس والتهجئة الفعّال](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [إتقان GroupDocs Redaction والبحث في .NET: إدارة مستندات فعّالة والبحث الآمن](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
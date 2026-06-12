---
date: '2026-06-12'
description: تعلم كيفية البحث وإزالة المعلومات الحساسة من المستندات في .NET باستخدام
  GroupDocs.Search و GroupDocs.Redaction، مع تحسين أداء البحث ومعالجة أخطاء الفهرسة.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: كيفية البحث وإزالة المعلومات الحساسة من المستندات في .NET باستخدام GroupDocs.Search
  و GroupDocs.Redaction
type: docs
url: /ar/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# بحث وتحرير المستندات في .NET باستخدام GroupDocs.Search & GroupDocs.Redaction

في بيئات المؤسسات الحديثة، تُعد قدرات **search and redact** أساسية لحماية المعلومات الحساسة مع الحفاظ على إمكانية اكتشاف المستندات بسهولة. يشرح هذا الدليل كيفية بناء حل .NET قوي يجمع بين GroupDocs.Search للبحث النصي السريع وGroupDocs.Redaction لإزالة البيانات السرية بأمان. في النهاية، ستعرف كيف تُعد المكتبات، وتُنشئ مُجزئ نص مخصص، وتُجري عمليات بحث عالية الأداء، وتُطبق عمليات التحرير بأمان.

## إجابات سريعة
- **ما معنى “search and redact”؟** يعني العثور على النص في المستندات وإخفائه بشكل دائم.  
- **ما المكتبات المطلوبة؟** GroupDocs.Search وGroupDocs.Redaction لـ .NET.  
- **هل يمكنني التعامل مع محتوى متعدد اللغات؟** نعم—استخدم مُجزئ نص مخصص لتقسيم الكلمات بشكل صحيح.  
- **كيف أحسن سرعة البحث؟** قم بفهرسة مرة واحدة، أعد استخدام الفهرس، وفعل إعدادات `optimize search performance`.  
- **ماذا إذا فشل الفهرسة؟** اتبع إرشادات “handle indexing errors” في قسم استكشاف الأخطاء وإصلاحها.

## ما هو “search and redact”؟
search and redact هو عملية تحديد المصطلحات المحددة داخل مجموعة من المستندات ثم إخفاؤها أو إزالتها بشكل دائم لحماية الخصوصية أو للامتثال التنظيمي. يجمع بين البحث النصي الكامل للعثور على المعلومات الحساسة وأدوات التحرير التي تستبدل المحتوى مع الحفاظ على تنسيق المستند الأصلي.

## لماذا نستخدم GroupDocs.Search وGroupDocs.Redaction معًا؟
GroupDocs.Search يدعم **50+ file formats** ويمكنه فهرسة **100,000+ مستند** في أقل من دقيقة على خادم عادي، بينما GroupDocs.Redaction يمكنه تطبيق عمليات التحرير على **PDF, DOCX, PPTX، وأكثر** دون تغيير التخطيط الأصلي. الجمع بينهما يمنحك حلاً موحدًا يُـ **optimizes search performance** و**handles indexing errors** بسلاسة.

## المتطلبات المسبقة
- Visual Studio 2022 أو أحدث مع دعم .NET 6+.
- حزم NuGet: **GroupDocs.Search** و**GroupDocs.Redaction** (أحدث الإصدارات المستقرة).
- ترخيص GroupDocs صالح (تجريبي أو مُشترى).

### المكتبات المطلوبة
- **GroupDocs.Search** – يوفر الفهرسة، الاستعلام، والتجزئة المخصصة.
- **GroupDocs.Redaction** – يقدم تحرير النصوص، الصور، والبيانات الوصفية عبر الصيغ المدعومة.

### متطلبات إعداد البيئة
تأكد من أن جهاز التطوير لديك يمتلك أذونات كتابة للمجلد الذي سيُخزن فيه الفهرس.

### المتطلبات المعرفية
- الإلمام بـ C# وهياكل مشاريع .NET.
- فهم أساسي لمفاهيم معالجة المستندات (اختياري لكن مفيد).

## كيف أقوم بتثبيت GroupDocs.Redaction لـ .NET؟
يمكنك إضافة حزمة Redaction إلى مشروعك باستخدام .NET CLI أو مدير حزم NuGet. يقوم الأمر بتحميل أحدث نسخة مستقرة وتسجيلها في ملف المشروع، مما يجعل الـ API متاحًا للاستخدام فورًا.  

```bash
dotnet add package GroupDocs.Redaction
```  

## كيف أحصل على ترخيص لـ GroupDocs؟
تقدم GroupDocs ثلاثة خيارات للترخيص: تجربة مجانية للتقييم، ترخيص مؤقت لاختبار التطوير الممتد، وترخيص تجاري كامل للاستخدام في الإنتاج. توفر التجربة وظائف محدودة، بينما يطيل المفتاح المؤقت فترة التقييم، ويتيح الترخيص المشتراة جميع الميزات والدعم ذو الأولوية.

## كيف أقوم بتهيئة GroupDocs.Redaction في تطبيقى؟
فئة `Redaction` هي نقطة الدخول الأساسية لتطبيق عمليات التحرير على المستندات المدعومة. تقوم بتحميل ملف، تحضير كائنات التحرير، وتنفيذ عملية التحرير، مع إرجاع مستند معدل مع الحفاظ على التخطيط الأصلي. يمكنك أيضًا ضبط خيارات التحرير مثل اللون، التراكب، وإزالة البيانات الوصفية لتلبية متطلبات الامتثال المحددة.  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## كيف أقوم بإعداد فهرس باستخدام GroupDocs.Search؟
فئة `Index` تمثل مستودعًا قابلًا للبحث يُخزن على القرص. تدير إنشاء الفهرس، تحديثه، واستعلاماته، مما يتيح لك إضافة مستندات، إعادة بناء الفهرس، وتنفيذ عمليات بحث سريعة عبر مجموعات كبيرة. يمكن أن يكون مجلد الفهرس على تخزين محلي أو شبكة، ويمكنك ضبط إعدادات الضغط والتشفير لحماية البيانات المفهرسة.  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## ما هو مُجزئ النص المخصص ولماذا يجب استخدامه؟
يحدد مُجزئ النص المخصص كيفية تقسيم النص الخام إلى رموز قابلة للبحث. من خلال تخصيص قواعد التجزئة للغات أو المجالات المحددة، تحسن دقة التجزئة، مما يؤدي إلى استرجاع أعلى وصلة أفضل في نتائج البحث. هذا مفيد بشكل خاص للغات ذات حدود كلمات معقدة، مثل اليابانية أو العربية، حيث قد تقسم المُجزئات الافتراضية الكلمات بشكل غير صحيح.  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## كيف أقوم بإجراء بحث نص كامل باستخدام المُجزئ المخصص؟
كائن `SearchQuery` يضمّن استعلام المستخدم ويعمل مع المُجزئ المخصص لتحديد التطابقات. يدعم المطابقة الضبابية، استعلامات العبارات، والوزن، ويُرجع مجموعة نتائج تحتوي على معرفات المستندات، مواضع الضربات، ودرجات الصلة. يمكنك أيضًا تطبيق فلاتر مثل نوع الملف أو نطاق التاريخ لتضييق النتائج للحصول على استهداف أكثر دقة.  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## كيف أقوم بتطبيق عمليات التحرير بعد العثور على النص الحساس؟
تتيح لك واجهة برمجة التطبيقات `Redaction` استبدال أو إزالة النصوص، الصور، والبيانات الوصفية في المستندات المدعومة. بعد تحديد المصطلحات الحساسة، تقوم بإنشاء كائنات تحرير، تطبيقها، وحفظ الملف المُحرّر، مما يضمن إخفاء المعلومات السرية بشكل دائم. تشمل خيارات التحرير وضع صناديق سوداء، تطبيق ألوان مخصصة، أو إزالة الكائنات بالكامل مع الحفاظ على بنية المستند.  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## المشكلات الشائعة وكيفية التعامل مع أخطاء الفهرسة
- **Index Not Found:** تحقق من وجود مسار الفهرس وأن التطبيق يمتلك أذونات القراءة/الكتابة.  
- **Search Returns No Results:** أعد تشغيل عملية الفهرسة وتأكد من تسجيل المُجزئ المخصص بشكل صحيح.  
- **Redaction Fails on Certain Formats:** تأكد من أن نوع الملف مدعوم؛ بالنسبة لملفات PDF، استخدم أحدث نسخة من Redaction لمعالجة ميزات PDF 2.0.

## تطبيقات عملية
1. **Legal Document Management:** ابحث في العقود عن “non‑disclosure” وقم تلقائيًا بتحرير البنود قبل المشاركة الخارجية.  
2. **Academic Research:** حدد البيانات غير المنشورة في المخطوطات وأخفها لعمليات مراجعة الأقران.  
3. **Business Contracts:** عالج آلاف الاتفاقيات دفعيًا، مع تحرير المعرفات الشخصية مع الحفاظ على اللغة القانونية.

## كيف يمكنني تحسين أداء البحث لمجموعات المستندات الكبيرة؟
لتحقيق أقصى أداء، قم بفهرسة المستندات مرة واحدة وأعد استخدام الفهرس نفسه للاستعلامات اللاحقة. فعّل المعالجة المتوازية، اضبط التخزين المؤقت، وحسّن إعدادات الفهرس لتقليل الكمون وتحسين الإنتاجية على الخوادم متعددة النوى. بالإضافة إلى ذلك، اضبط علامة `EnableMemoryMapping` للسماح بربط الفهرس بالذاكرة، مما يسرّع عمليات القراءة لمجموعات البيانات الكبيرة.

## كيف أدير ذاكرة .NET عند التعامل مع ملفات كبيرة؟
إدارة الذاكرة بكفاءة أمر حاسم عند التعامل مع مستندات كبيرة. احwrap كائنات `Index` و`Redaction` داخل عبارات `using` لضمان التخلص الحتمي، وعالج الملفات كتيارات بدلاً من تحميل المستندات بالكامل في الذاكرة. يساعد مراقبة عدادات الأداء على اكتشاف ارتفاعات الذاكرة مبكرًا، مما يتيح لك تعديل أحجام الدُفعات أو تفعيل ضبط جمع القمامة.

## الأسئلة المتكررة
**س: هل يمكنني استخدام GroupDocs.Search مع بيانات وصفية غير نصية؟**  
ج: نعم—يمكن فهرسة حقول البيانات الوصفية جنبًا إلى جنب مع محتوى المستند، مما يتيح بحثًا مثل “author:JohnDoe”.

**س: هل يدعم GroupDocs.Redaction التحرير في الوقت الحقيقي عبر واجهة برمجة تطبيقات ويب؟**  
ج: نعم؛ يمكنك استدعاء واجهة Redaction API بشكل متزامن للملفات الصغيرة أو وضع وظائف أكبر في قائمة الانتظار للمعالجة غير المتزامنة.

**س: ماذا أفعل إذا أصبح الفهرس معطوبًا؟**  
ج: احذف مجلد الفهرس المعطوب وأعد بنائه باستخدام نفس روتين الفهرسة؛ تسجل المكتبة رسائل خطأ مفصلة لمساعدتك في تحديد السبب.

**س: هل يمكن معاينة المستندات المحررة قبل الحفظ؟**  
ج: بالتأكيد—استدعِ `redaction.Apply()` مع علامة `preview` لإنشاء نسخة مؤقتة للمراجعة.

**س: أي إصدارات .NET مدعومة رسميًا؟**  
ج: تدعم GroupDocs.Search وGroupDocs.Redaction .NET 6، .NET 5، .NET Core 3.1، و.NET Framework 4.6.2+.

## الموارد
- **الوثائق:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **مرجع API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **التنزيل:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)
- **دعم مجاني:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **ترخيص مؤقت:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-06-12  
**تم الاختبار مع:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**المؤلف:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## دروس ذات صلة
- [إتقان GroupDocs Search وRedaction في .NET: إدارة مستندات متقدمة](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [تنفيذ GroupDocs.Search وRedaction: تحديث وإدارة فهارس المستندات في .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [تحسين فهرسة المستندات في .NET باستخدام GroupDocs.Redaction: الإلغاء، غير المتزامن، والخيوط](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
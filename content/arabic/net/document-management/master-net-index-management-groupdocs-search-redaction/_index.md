---
date: '2026-07-26'
description: تعلم كيفية إنشاء فهرس في .NET باستخدام GroupDocs.Search وتكامل عملية
  التشويه مع GroupDocs.Redaction، مما يتيح بحثًا سريعًا في المستندات ومعالجة البيانات.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: تعلم كيفية إنشاء فهرس في .NET باستخدام GroupDocs.Search وتكامل عملية
  التشويه مع GroupDocs.Redaction، مما يتيح بحثًا سريعًا في المستندات ومعالجة البيانات.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: كيفية إنشاء فهرس في .NET باستخدام GroupDocs Search API
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: كيفية إنشاء فهرس في .NET باستخدام GroupDocs Search API
type: docs
url: /ar/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# كيفية إنشاء فهرس في .NET باستخدام GroupDocs Search API

في هذا البرنامج التعليمي ستكتشف **كيفية إنشاء فهرس** لتطبيقات .NET الخاصة بك باستخدام GroupDocs.Search ثم حماية المحتوى الحساس باستخدام GroupDocs.Redaction. في نهاية الدليل ستكون قادرًا على بناء وتحديث وتقليم فهرس قابل للبحث، وستفهم لماذا الجمع بين البحث والتمويه يُعد ممارسةً مثالية لإدارة المستندات الآمنة.

## إجابات سريعة
- **ماذا يعني “كيفية إنشاء فهرس”؟** يعني بناء بنية بيانات قابلة للبحث تربط محتوى المستند بمفاتيح بحث سريعة.  
- **ما المكتبات المطلوبة؟** GroupDocs.Search و GroupDocs.Redaction لـ .NET (حزم NuGet).  
- **هل يمكنني فهرسة ملفات PDF و Word والصور؟** نعم—يتم دعم أكثر من 150 تنسيقًا مباشرةً.  
- **كيف أحذف مستندًا من الفهرس؟** استدعِ طريقة `Delete` مع مسار المستند أو معرّفه.  
- **هل يتم تنفيذ التمويه قبل أو بعد الفهرسة؟** يجب أن يحدث التمويه أولًا حتى لا يدخل البيانات المحمية إلى الفهرس.

## ما هو “كيفية إنشاء فهرس”؟
تشير عبارة **كيفية إنشاء فهرس** إلى عملية إنشاء بنية بيانات قابلة للبحث تخزن تعيينات المصطلح إلى المستند لتسريع الاسترجاع. في GroupDocs، هذه البنية موجودة على القرص ويمكن تحديثها بشكل تدريجي دون الحاجة إلى إعادة بناء المجموعة بالكامل.

## لماذا نستخدم GroupDocs.Search و GroupDocs.Redaction معًا؟
يدعم GroupDocs.Search فهرسة **أكثر من 150 تنسيق ملف** ويمكنه التعامل مع فهارس أكبر من **10 GB** مع الحفاظ على استهلاك الذاكرة أقل من 200 MB لأنه يبث الملفات بدلاً من تحميلها بالكامل. إضافة GroupDocs.Redaction يضمن إزالة أي نص سري أو صور أو بيانات وصفية قبل أن يصل المحتوى إلى الفهرس، مما يضمن الامتثال للـ GDPR و HIPAA وغيرها من اللوائح.

## المتطلبات المسبقة
- **المكتبات والإصدارات** – قم بتثبيت أحدث حزم NuGet الخاصة بـ **GroupDocs.Search** و **GroupDocs.Redaction** المتوافقة مع .NET 6 أو أحدث.  
- **بيئة التطوير المتكاملة (IDE)** – Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET 6).  
- **المعرفة** – مهارات أساسية في C#، إلمام بملفات الإدخال/الإخراج، وفهم لمفاهيم الفهرسة.

## إعداد GroupDocs.Redaction لـ .NET

### التثبيت

**استخدام .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**استخدام Package Manager Console في Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

يمكنك أيضًا العثور على “GroupDocs.Redaction” في واجهة مدير الحزم NuGet وتثبيت أحدث نسخة مستقرة.

### الحصول على الترخيص

يمكنك الحصول على نسخة تجريبية مجانية أو طلب ترخيص مؤقت لاستكشاف جميع الميزات دون قيود. زر [صفحة شراء GroupDocs](https://purchase.groupdocs.com/temporary-license/) لمزيد من التفاصيل حول الحصول على ترخيص.

### التهيئة الأساسية

Redactor هو الفئة الأساسية التي تقوم بعمليات التمويه على المستند.  
المقتطف التالي يوضح الحد الأدنى من الشيفرة المطلوبة للبدء في استخدام GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

هذه الإعدادات البسيطة هي كل ما تحتاجه للبدء في استخدام GroupDocs.Redaction.

## دليل التنفيذ

### كيفية إنشاء فهرس؟

`Index` يمثل الحاوية القابلة للبحث التي تحتفظ بقواميس المصطلحات وبيانات تعريف المستند.  
قم بتحميل أو إنشاء كائن `Index`، ووجهه إلى مجلد سيتم تخزين ملفات الفهرس فيه، ثم استدعِ `Create`. تقوم العملية بكتابة ملفات البيانات الوصفية اللازمة وتجهّز المحرك لاستيعاب المستندات.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### الخطوة 1: إنشاء الفهرس
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### كيفية إضافة مستندات إلى الفهرس؟

`Add` يضيف مستندًا واحدًا إلى الفهرس، بينما `AddFolder` يعالج جميع الملفات في دليل.  
تضيف الملفات عن طريق استدعاء `Add` أو `AddFolder`. يقرأ المحرك كل ملف مدعوم، يستخرج النص، ويحدّث قاموس المصطلحات.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### الخطوة 2: إضافة مجلدات المستندات
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### كيفية استرجاع المسارات المفهرسة؟

`GetIndexedPaths` تُعيد مجموعة من جميع مسارات المستندات المخزنة في الفهرس.  
استرجاع قائمة مسارات الملفات المفهرسة يتيح لك التحقق من المستندات القابلة للبحث حاليًا.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### الخطوة 3: عرض المسارات المفهرسة
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### كيفية حذف مستند من الفهرس؟

`Delete` يزيل مستندًا من الفهرس باستخدام مساره أو معرّفه.  
عندما يُزال ملف أو يصبح غير صالح، يجب حذف مدخله للحفاظ على دقة نتائج البحث.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### الخطوة 4: حذف مسارات محددة
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### كيفية التحقق من المسارات المفهرسة المتبقية بعد الحذف؟

بعد الإزالة، يمكنك إعادة تشغيل طريقة الاسترجاع للتأكد من أن الفهرس يعكس الحالة الحالية.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### الخطوة 5: التحقق من المسارات المتبقية
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## تطبيقات عملية

1. **أنظمة إدارة المستندات** – تحديد سريع للعقود والفواتير أو الأدلة عبر ملايين الملفات.  
2. **مراجعة المستندات القانونية** – تمويه المعلومات المحمية قبل الفهرسة لتجنب الكشف غير المقصود.  
3. **حلول الأرشفة** – الحفاظ على بيانات وصفية قابلة للبحث للسجلات التاريخية دون تحميل الأرشيفات بالكامل في الذاكرة.  
4. **منصات إدارة المحتوى** – تمكين البحث عبر الموقع للمدونات وقواعد المعرفة ومكتبات الوسائط المتعددة.  
5. **تدقيق الامتثال للبيانات** – التأكد من أن المحتوى المنقّى فقط هو القابل للبحث، لتلبية متطلبات اللوائح.

## اعتبارات الأداء

- **تحسين الفهرسة** – جدولة فهرسة تدريجية ليلاً؛ استخدم `AddFolder` بحجم دفعة 100 ملف لتقليل تقلبات الإدخال/الإخراج.  
- **إدارة الموارد** – راقب وحدة المعالجة المركزية والذاكرة؛ يقوم GroupDocs.Search بمعالجة الملفات بطريقة تدفقية، مما يحافظ على استهلاك الذاكرة القصوى تحت 200 MB حتى للفهارس بحجم 10 GB.  
- **أفضل الممارسات** – احفظ الفهرس على أقراص SSD للحصول على استجابة استعلام أقل من ثانية، وفعل الضغط (`index.Compression = true`) لتقليل استهلاك القرص إلى النصف.

## الأسئلة المتكررة

**س: هل يمكنني فهرسة ملفات غير نصية باستخدام GroupDocs؟**  
ج: نعم، يمكن لـ GroupDocs.Search فهرسة أكثر من 150 تنسيقًا — بما في ذلك PDFs و DOCX و PPTX و XLSX وأنواع الصور — عن طريق استخراج النص المضمن عبر OCR عند الحاجة.

**س: كيف أتعامل مع حجم كبير من المستندات؟**  
ج: استخدم `AddFolder` مع حجم دفعة قابل للتكوين، نفّذ الفهرسة في خدمة خلفية، واستدعِ `Optimize()` دوريًا لدمج مقاطع الفهرس الصغيرة.

**س: ما هي فوائد استخدام التمويه مع الفهرسة؟**  
ج: يزيل التمويه المعلومات الشخصية القابلة للتعريف قبل أن تصل إلى الفهرس، مما يضمن أن نتائج البحث لا تكشف أبدًا عن البيانات المحمية.

**س: هل يمكن تخصيص خوارزميات البحث؟**  
ج: يوفر GroupDocs.Search قواميس المرادفات، ومحللات مخصصة، ومرشحات تعبيرات نمطية، مما يتيح لك ضبط درجة الصلة بدقة.

**س: كيف يمكنني استكشاف مشكلات الفهرسة الشائعة؟**  
ج: تحقق من أذونات المجلد، تأكد من توافق وقت تشغيل .NET مع هدف المكتبة، وتفقد ملف السجل المُنشأ في مجلد الفهرس للحصول على رسائل خطأ مفصلة.

## الموارد

- **الوثائق**: [GroupDocs Redaction .NET Docs](https://docs.groupdocs.com/search/net/)  
- **مرجع API**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **التنزيل**: [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **دعم مجاني**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت**: [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

استكشف هذه الموارد لتعميق فهمك وتعزيز تنفيذك لـ GroupDocs.Search و Redaction في .NET. برمجة سعيدة!

---

**آخر تحديث:** 2026-07-26  
**تم الاختبار مع:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 لـ .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [إنشاء الفهرس الرئيسي ودمجه مع GroupDocs.Redaction .NET لإدارة مستندات فعّالة](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [إتقان GroupDocs.Redaction .NET: إنشاء فهرس فعال وإدارة الأسماء المستعارة للبحث المتقدم في المستندات](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [إتقان GroupDocs Search و Redaction في .NET: دليل شامل لإدارة المستندات](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)
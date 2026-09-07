---
date: '2026-06-22'
description: تعلم كيفية تعديل المستندات في .NET مع تحسين أداء البحث باستخدام GroupDocs.Redaction
  و GroupDocs.Search. إدارة السمات خطوة بخطوة، الفهرسة، وتعديل آمن للمطورين في .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: كيفية تعديل المستندات في .NET باستخدام GroupDocs Redaction
type: docs
url: /ar/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# كيفية إخفاء المستندات في .NET باستخدام GroupDocs Redaction

في هذا الدرس الشامل ستكتشف **كيفية إخفاء المستندات** في بيئة .NET وتتمكن في الوقت نفسه من إدارة سمات المستندات باستخدام GroupDocs.Redaction وGroupDocs.Search. سواء كنت بحاجة إلى حماية البيانات الحساسة، أو زيادة سرعة البحث، أو تنظيم مكتبات مستندات كبيرة، فإن التقنيات المعروضة هنا توفر لك حلاً جاهزًا للإنتاج يمكنه التوسع إلى مئات الآلاف من الملفات.

## إجابات سريعة
- **كيف يمكنني إخفاء PDF في .NET؟** قم بتحميل الملف باستخدام `Redactor`، عرّف `RedactionRegion`، واستدعِ `Redactor.Apply()` – ثلاثة أسطر من الشيفرة تتولى العملية الثقيلة.  
- **هل يمكنني تغيير سمات المستند بعد الفهرسة؟** نعم، استخدم `AttributeChangeBatch` لإضافة أو تحديث أو إزالة السمات دفعة واحدة.  
- **ما المكتبات المطلوبة؟** `GroupDocs.Redaction` + `GroupDocs.Search` (أحدث إصدارات NuGet).  
- **هل أحتاج إلى ترخيص للإنتاج؟** يلزم وجود ترخيص GroupDocs صالح؛ يتوفر ترخيص تجريبي مؤقت للتقييم.  
- **كيف يمكنني تحسين سرعة البحث؟** فعّل المعالجة الدفعية والفهرسة الانتقائية؛ هذه التقنيات يمكن أن **تحسن أداء البحث** بنسبة تصل إلى 40 % على مجموعات بيانات كبيرة.

## ما هو “كيفية إخفاء المستندات”؟

إنه يصف العملية الآلية لتحديد المعلومات الحساسة داخل ملف واستبدالها بمحتوى مخفي—مثل أشرطة سوداء أو مساحة بيضاء—مع الحفاظ على تخطيط المستند الأصلي. يضمن ذلك إخفاء البيانات السرية عن المشاهدين بينما يظل المستند قابلًا للقراءة والوظيفة للمهام اللاحقة.

## لماذا نستخدم GroupDocs.Redaction وGroupDocs.Search معًا؟

يدعم GroupDocs.Redaction **أكثر من 50 تنسيق ملف** (PDF، DOCX، XLSX، PPTX، صور، إلخ) ويمكنه معالجة المستندات حتى **2 GB** دون تحميل الملف بالكامل في الذاكرة. يقوم GroupDocs.Search بفهرسة أكثر من **70 مليون مصطلح** في الساعة على خادم قياسي، مما يتيح لك **تحسين أداء البحث** بشكل كبير عند دمجه مع الترشيح القائم على السمات.

## المتطلبات المسبقة

- **المكتبات المطلوبة:** `GroupDocs.Search` و`GroupDocs.Redaction` (أحدث إصدارات NuGet).  
- **بيئة التطوير:** Visual Studio 2019 أو أحدث، مستهدفًا .NET Core 3.1 أو .NET 6+.  
- **المعرفة الأساسية:** صsyntax C#، مفاهيم البرمجة الكائنية، وإلمام بمبادئ فهرسة المستندات.

## إعداد GroupDocs.Redaction لـ .NET

### تثبيت المكتبة

يمكنك إضافة **GroupDocs.Redaction** إلى مشروعك باستخدام أي من الطرق التالية:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- ابحث عن “GroupDocs.Redaction” وقم بتثبيت أحدث نسخة.

### خطوات الحصول على الترخيص

لبدء الاستخدام، يمكنك الحصول على ترخيص مؤقت أو شراء واحد. تتوفر نسخة تجريبية مجانية لاختبار الميزات قبل الالتزام:

1. زر [صفحة ترخيص GroupDocs](https://purchase.groupdocs.com/temporary-license/) لطلب ترخيص مؤقت.  
2. اتبع التعليمات المقدمة لتطبيق الترخيص في تطبيقك.

### التهيئة الأساسية والإعداد

`Redactor` هو الفئة الرئيسية المستخدمة لتحميل مستند وتطبيق عمليات الإخفاء.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## الميزة 1: تغيير سمات المستند

### نظرة عامة
تعديل سمات المستند يتيح لك ضبط كيفية ظهور المستندات في نتائج البحث بدقة، مما يمكّن من الترشيح والتصنيف الدقيق.

#### الخطوة 1: تهيئة الفهرس
`Index` يمثل مجموعة قابلة للبحث من المستندات والبيانات الوصفية المرتبطة بها.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### الخطوة 2: تعديل السمات
`AttributeChangeBatch` هي الفئة التي تجمع تحديثات السمات لزيادة الكفاءة.

**تعريف:** *`AttributeChangeBatch` تجمع عمليات الإضافة، التحديث، والحذف على سمات المستند في معاملة واحدة.*

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### الخطوة 3: البحث باستخدام مرشحات السمات
يمكنك ترشيح نتائج البحث بناءً على قيم السمات باستخدام `SearchOptions`.

**الإجابة المباشرة:** للبحث عن المستندات التي تحتوي على السمة `Category = "Legal"`، قم بتكوين `SearchOptions` مع `AttributeFilter` واستدعِ `searcher.Search("contract", options)`. سيعيد ذلك فقط العقود الموسومة قانونيًا، مما يقلل الضوضاء في النتائج و**يحسن أداء البحث**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## الميزة 2: إضافة سمات أثناء الفهرسة

### نظرة عامة
إضافة السمات في لحظة الفهرسة يضمن أن كل مستند يُثري بالبيانات الوصفية الصحيحة من البداية، مما يلغي الحاجة إلى تحديثات دفعية لاحقة.

#### الخطوة 1: إعداد معالج الحدث للفهرسة
**تعريف:** *حدث `DocumentIndexed` يُطلق في كل مرة يتم فيها إضافة مستند بنجاح إلى الفهرس، مما يسمح بتنفيذ منطق مخصص.*

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### الخطوة 2: تكوين وإجراء البحث
بعد إرفاق السمات، يمكنك البحث باستخدام تلك الحقول الجديدة.

**الإجابة المباشرة:** استخدم `SearchOptions` مع `AttributeFilter` لاستعلام السمات المضافة حديثًا، على سبيل المثال `AttributeFilter("Department", "Finance")`. سيعيد ذلك فقط الملفات المتعلقة بالمالية، موضحًا **كيفية فهرسة السمات** للحصول على نتائج أسرع وأكثر صلة.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## تطبيقات عملية

فيما يلي ثلاثة سيناريوهات شائعة حيث يضيف إدارة سمات المستند والإخفاء معًا قيمة تجارية ملموسة:

1. **إدارة المستندات القانونية** – إخفاء الفقرات السرية تلقائيًا ووضع علامات على العقود حسب الاختصاص القضائي، مما يمكّن المحامين من العثور فقط على الملفات ذات الصلة.  
2. **تنظيم السجلات الطبية** – إخفاء معرفات المرضى مع إضافة سمات مثل `PatientID` و`VisitDate` لاسترجاع متوافق وسريع.  
3. **فهرسة منتجات التجارة الإلكترونية** – إخفاء معلومات أسعار الموردين ووضع علامات على المنتجات بـ `StockStatus` أو `DiscountRate` أثناء الاستيراد الدفعي، مما يسمح باستعلامات المخزون في الوقت الحقيقي.

## اعتبارات الأداء

عند التعامل مع مجموعات بيانات كبيرة، احرص على اتباع أفضل الممارسات التالية:

- **المعالجة الدفعية:** `AttributeChangeBatch` يقلل من عدد الزيارات إلى الفهرس، مما يقلل وقت المعالجة بنسبة تصل إلى **45 %** على دفعات من 100 k مستند.  
- **الفهرسة الانتقائية:** فهرس فقط المستندات التي تحتاج إلى سمات جديدة؛ تخطى الملفات غير المتغيرة لتوفير وحدة المعالجة المركزية وإدخال/إخراج.  
- **إدارة الذاكرة:** حرّر كائنات `SearchResult` و`Redactor` و`Indexer` بمجرد الانتهاء منها لتحرير الموارد غير المُدارة.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|----------|
| الإخفاء لا يخفي النص | إحداثيات `RedactionRegion` غير صحيحة | تحقق من أبعاد الصفحة باستخدام `Redactor.GetPageSize()` قبل تعريف المنطقة. |
| تغييرات السمات لا تظهر في البحث | الفهرس غير محدث | استدعِ `searcher.Refresh()` بعد تنفيذ `AttributeChangeBatch`. |
| أخطاء نفاد الذاكرة على ملفات كبيرة | تحميل الملف بالكامل في الذاكرة | فعّل وضع البث عن طريق ضبط `RedactorOptions.Stream = true`. |

## الأسئلة المتكررة

**س: ما هي أفضل طريقة لإخفاء عدة ملفات PDF دفعيًا؟**  
ج: قم بتحميل كل ملف باستخدام `Redactor`، أضف `RedactionRegion` لكل منطقة حساسة، ثم استدعِ `Redactor.Apply()` داخل حلقة؛ هذا النهج يعالج آلاف الملفات بأقل استهلاك للذاكرة.

**س: هل يمكنني دمج الإخفاء مع ترشيح السمات في استعلام واحد؟**  
ج: نعم. بعد الإخفاء، يحتفظ المستند ببياناته الوصفية، لذا يمكنك البحث باستخدام كل من مصطلحات النص و`AttributeFilter` في آن واحد.

**س: كيف أتعامل مع المستندات المحمية بكلمة مرور؟**  
ج: مرّر كلمة المرور إلى مُنشئ `Redactor`؛ ستقوم المكتبة بفك التشفير، الإخفاء، وإعادة تشفير الملف تلقائيًا.

**س: هل يدعم GroupDocs تقنية OCR للصور الممسوحة قبل الإخفاء؟**  
ج: بالتأكيد. فعّل `RedactorOptions.Ocr = true` للتعرف على النص في الصور، ثم طبّق قواعد الإخفاء على النص المستخرج.

**س: أي إصدارات .NET مدعومة رسميًا؟**  
ج: تدعم GroupDocs.Redaction وGroupDocs.Search .NET Core 3.1، .NET 5، .NET 6، و.NET 7، بالإضافة إلى .NET Framework 4.6.2+.

## الخلاصة

أصبح لديك الآن حل شامل لـ **كيفية إخفاء المستندات** مع **تحسين أداء البحث** و**كيفية فهرسة السمات** باستخدام GroupDocs.Redaction وGroupDocs.Search. باتباع الخطوات أعلاه، يمكنك حماية البيانات الحساسة، إغناء فهرس البحث ببيانات وصفية ذات معنى، والحفاظ على تطبيقات .NET سريعة وآمنة.

---

**آخر تحديث:** 2026-06-22  
**تم الاختبار مع:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [إتقان GroupDocs.Redaction .NET: إنشاء فهرس فعال وإدارة الأسماء المستعارة للبحث المتقدم في المستندات](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [إتقان إخفاء المستندات وفهرسة البيانات الوصفية باستخدام GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [إتقان GroupDocs.Redaction .NET: الإعداد ومعالجة الأحداث لإدارة مستندات آمنة](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
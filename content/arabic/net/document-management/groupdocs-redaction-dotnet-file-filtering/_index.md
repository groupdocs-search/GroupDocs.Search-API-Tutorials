---
date: '2026-04-21'
description: تعرّف على كيفية تصفية الملفات باستخدام GroupDocs.Redaction لـ .NET، بما
  في ذلك التصفية حسب تاريخ الإنشاء، حجم الملف، تاريخ التعديل، وكيفية تطبيق عوامل التصفية
  NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: كيفية تصفية الملفات باستخدام GroupDocs.Redaction لـ .NET
type: docs
url: /ar/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# كيفية تصفية الملفات باستخدام GroupDocs.Redaction لـ .NET

في بيئة الرقمية السريعة اليوم، **كيفية تصفية الملفات** بفعالية يمكن أن تكون عاملاً حاسماً في إنتاجيتك. سواء كنت بحاجة إلى عزل المستندات حسب الامتداد أو تاريخ الإنشاء أو الحجم أو تاريخ التعديل، فإن استراتيجية التصفية القوية توفر الوقت، وتقلل تكاليف التخزين، وتحافظ على ترتيب فهرس البحث. في هذا البرنامج التعليمي سنستعرض أمثلة واقعية باستخدام GroupDocs.Redaction لـ .NET، موضحين لك بالضبط كيفية تصفية الملفات لتلبية احتياجات الأعمال الشائعة.

## إجابات سريعة
- **ما المكتبة التي أحتاجها؟** GroupDocs.Redaction لـ .NET (التثبيت عبر NuGet).  
- **هل يمكنني التصفية حسب تاريخ الإنشاء؟** نعم – استخدم `CreateCreationTimeRange`.  
- **كيف يمكنني استبعاد أنواع معينة؟** استخدم فلتر NOT مع `DocumentFilter.CreateNot`.  
- **هل تدعم التصفية حسب حجم الملف؟** بالتأكيد، عبر `CreateFileLengthRange` أو الحدود العليا/السفلى.  
- **هل أحتاج إلى ترخيص؟** يلزم وجود ترخيص تجريبي أو كامل للاستخدام في الإنتاج.

## ما هي تصفية الملفات باستخدام GroupDocs.Redaction؟
تتيح لك تصفية الملفات إخبار محرك الفهرسة أي المستندات يجب تضمينها أو تجاهلها بناءً على البيانات الوصفية مثل الامتداد، التواريخ، أنماط المسار، أو الحجم. من خلال تعريف قواعد `DocumentFilter` الدقيقة، تحافظ على خفة فهرسك وسرعة عمليات البحث.

## لماذا تستخدم GroupDocs.Redaction لـ .NET؟
- **مساعدات الفلترة المدمجة** – لا حاجة لكتابة كود نظام ملفات مخصص.  
- **العوامل المنطقية** – دمج معايير متعددة باستخدام AND، OR، و NOT.  
- **محسّن للأداء** – يتم تطبيق الفلاتر أثناء الفهرسة، وليس بعد ذلك.  
- **متعدد المنصات** – يعمل مع .NET Framework، .NET Core، و .NET 5/6+.  

## المتطلبات المسبقة
- .NET Framework 4.6+ أو .NET Core 3.1+ مثبت.  
- Visual Studio أو بيئة التطوير المتكاملة المفضلة لـ C#.  
- معرفة أساسية بـ C#.  

### المكتبات المطلوبة والإعداد
قم بتثبيت حزمة NuGet باستخدام الطريقة المفضلة لديك:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **نصيحة احترافية:** بعد التثبيت، أضف ملف الترخيص إلى جذر المشروع واستدعِ `License.SetLicense("license-file-path")` قبل إنشاء أي كائنات Redactor أو Index.

## إعداد GroupDocs.Redaction لـ .NET

أولاً، أنشئ كائن `Redactor` يشير إلى المستند الذي تريد العمل معه:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **لماذا هذا مهم:** تهيئة Redactor يضمن أن المكتبة جاهزة لتطبيق الفلاتر وقواعد الإخفاء لاحقًا في سير العمل.

## كيفية تصفية الملفات حسب الامتداد

تصفية الملفات حسب الامتداد هي الطريقة الأكثر شيوعًا لتقليل مجموعة المستندات. أدناه نحتفظ فقط بملفات FB2 و EPUB و TXT.

### تصفية حسب امتداد الملف

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية تطبيق فلتر NOT لاستبعاد الأنواع غير المرغوب فيها

إذا كنت بحاجة إلى **تطبيق منطق فلتر NOT**—مثلاً استبعاد ملفات HTML و PDF—استخدم `CreateNot`.

### استبعاد ملفات HTM و HTML و PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية تصفية الملفات حسب تاريخ الإنشاء

عندما تحتاج إلى **تصفية حسب تاريخ الإنشاء**، حدد `DateTime` للبداية والنهاية.

### تصفية حسب نطاق تاريخ الإنشاء

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية تصفية الملفات حسب تاريخ التعديل

مشابه لتواريخ الإنشاء، يمكنك تحديد النتائج للملفات التي تم تعديلها قبل نقطة معينة.

### تصفية حسب تاريخ التعديل

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية تصفية الملفات حسب المسار باستخدام التعابير النمطية

إذا كان هيكل المجلدات يتبع تسميات محددة، يمكن للتعبير النمطي استهداف مسارات معينة.

### تصفية حسب نمط مسار الملف

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية تصفية الملفات حسب الحجم

التحكم في حجم المستند أمر أساسي عند التعامل مع حدود النطاق الترددي أو التخزين.

### تصفية حسب حجم الملف (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية دمج عدة شروط باستخدام AND

عندما تحتاج إلى **تصفية الملفات** باستخدام عدة معايير في آن واحد، دمجها باستخدام `CreateAnd`.

### مثال على AND المنطقي

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## كيفية دمج عدة شروط باستخدام OR

استخدم `CreateOr` عندما يجب أن ينجح أي من عدة قواعد.

### مثال على OR المنطقي

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## المشكلات الشائعة والحلول
- **لم يتم تطبيق الفلتر:** تأكد من تعيين `settings.DocumentFilter` **قبل** إنشاء كائن `Index`.  
- **ظهور ملفات غير متوقعة:** تحقق مرة أخرى من أن امتدادات الملفات تشمل النقطة الأولية (`.txt`).  
- **تباطؤ الأداء:** دمج الفلاتر باستخدام AND لتقليل عدد الملفات التي يتم فحصها مبكرًا في خط أنابيب الفهرسة.  
- **أخطاء التعبير النمطي:** هرب الأحرف الخاصة في نمط المسار أو استخدم `RegexOptions.IgnoreCase` للمطابقات غير حساسة لحالة الأحرف.  

## الأسئلة المتكررة

**س: هل يمكنني دمج فلتر NOT مع فلتر AND؟**  
ج: نعم. أنشئ فلتر NOT أولاً (`DocumentFilter.CreateNot`) ثم أدرجه كأحد المعاملات إلى `DocumentFilter.CreateAnd`.

**س: كيف يمكنني تصفية الملفات الأكبر من 10 ميغابايت؟**  
ج: استخدم `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` لتضمين الملفات التي تتجاوز هذا الحجم فقط.

**س: هل من الممكن تصفية حسب تاريخ الإنشاء وتاريخ التعديل معًا؟**  
ج: بالتأكيد. أنشئ كل فلتر على حدة ودمجهما باستخدام `CreateAnd`.

**س: هل تعمل هذه الفلاتر مع مسارات التخزين السحابي؟**  
ج: الفلاتر تعمل على نظام الملفات المحلي. بالنسبة للمصادر السحابية، قم بتنزيل الملفات إلى مجلد مؤقت أولاً، ثم طبق نفس الفلاتر.

**س: هل سيتطلب تغيير الفلتر إعادة الفهرسة؟**  
ج: نعم. يتم تقييم الفلاتر عند استدعاء `index.Add`. تغيير الفلتر يعني أنه يجب إعادة بناء الفهرس لتطبيق المعايير الجديدة.

## الخلاصة

من خلال إتقان **كيفية تصفية الملفات** باستخدام GroupDocs.Redaction لـ .NET—سواءً بالامتداد، تاريخ الإنشاء، تاريخ التعديل، حجم الملف، أو باستخدام منطق NOT—يمكنك تبسيط إدارة المستندات، الحفاظ على أداء الفهارس، والتركيز على المحتوى الحقيقي المهم. جرب العوامل المنطقية لتخصيص التصفية وفقًا لقواعد عملك الدقيقة، وستلاحظ تحسينات فورية في السرعة وكفاءة التخزين.

---

**آخر تحديث:** 2026-04-21  
**تم الاختبار مع:** GroupDocs.Redaction 24.11 لـ .NET  
**المؤلف:** GroupDocs
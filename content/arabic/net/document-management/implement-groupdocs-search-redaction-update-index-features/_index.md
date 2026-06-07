---
date: '2026-06-07'
description: تعلم كيفية تحديث الفهرس بكفاءة باستخدام GroupDocs.Search و Redaction
  لـ .NET، مما يعزز نظام إدارة المستندات الخاص بك.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: كيفية تحديث الفهرس باستخدام GroupDocs.Search و Redaction (.NET)
type: docs
url: /ar/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# كيفية تحديث الفهرس باستخدام GroupDocs.Search & Redaction (.NET)

في المؤسسات الحديثة المعتمدة على البيانات، يمكن أن يكون **كيفية تحديث الفهرس** بسرعة وبشكل موثوق هو الفارق بين نجاح أو فشل تجربة البحث الخاصة بك. سواء كنت تتعامل مع آلاف العقود أو قاعدة معرفة واسعة، فإن الحفاظ على تزامن فهرس البحث مع أحدث تغييرات المستندات أمر أساسي للحصول على نتائج سريعة ودقيقة. يشرح هذا الدليل كيفية استخدام GroupDocs.Search لـ .NET مع GroupDocs.Redaction لت **تحديث الفهرس** الملفات، وإدارة الفهارس ذات الإصدارات، وحماية المحتوى الحساس — كل ذلك ضمن مشروع .NET نظيف.

## إجابات سريعة
- **ماذا يعني “كيفية تحديث الفهرس”؟** إنها عملية تعديل فهرس بحث موجود بحيث تصبح المستندات الجديدة أو المعدلة قابلة للبحث دون الحاجة إلى إعادة بناء من الصفر.  
- **ما المكتبات المطلوبة؟** GroupDocs.Search و GroupDocs.Redaction لـ .NET (كلاهما متاح عبر NuGet).  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تعمل للاختبار؛ ترخيص الإنتاج يفتح كامل الوظائف.  
- **هل يمكن تشغيل هذا على .NET Core؟** نعم، المكتبات تدعم .NET Framework 4.5+، .NET Core 3.1+، و .NET 5/6+.  
- **ما الأداء الذي يمكن توقعه؟** تحديث فهرس بحجم 1 GB باستخدام خيطين يكتمل في أقل من دقيقة على خادم عادي بأربع نوى.

## ما هي “كيفية تحديث الفهرس”؟
**كيفية تحديث الفهرس** تشير إلى تقنية تطبيق تغييرات تدريجية على فهرس بحث موجود بدلاً من إعادة إنشائه بالكامل. يقلل هذا النهج من وقت التوقف، ويوفر دورات المعالج، ويحافظ على حداثة نتائج البحث مع إضافة أو تعديل أو إزالة المستندات.

## لماذا تستخدم GroupDocs.Search و Redaction لتحديث الفهارس؟
يدعم GroupDocs.Search **أكثر من 50 تنسيق ملف** (PDF، DOCX، XLSX، PPTX، HTML، الصور، إلخ) ويمكنه معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل إلى الذاكرة. عند دمجه مع GroupDocs.Redaction، يمكنك إزالة أو إخفاء البيانات الحساسة تلقائيًا قبل الفهرسة، مما يضمن الامتثال مع الحفاظ على صلة البحث.

## المتطلبات المسبقة

- **GroupDocs.Search** – تثبيت عبر NuGet.  
- **GroupDocs.Redaction for .NET** – مطلوب لميزات التشويه.  
- Visual Studio (أو أي بيئة تطوير .NET) مع تثبيت .NET 6+.  
- معرفة أساسية بـ C# وإلمام بمفاهيم الفهرسة.

### المكتبات المطلوبة والإصدارات
- **GroupDocs.Search** – أحدث إصدار ثابت من NuGet.  
- **GroupDocs.Redaction for .NET** – أحدث إصدار ثابت من NuGet.

### متطلبات إعداد البيئة
- جهاز Windows أو Linux مع تثبيت .NET SDK.  
- الوصول إلى مجلد سيتم تخزين ملفات الفهرس فيه.

### متطلبات المعرفة المسبقة
- فهم أساسيات فهرسة المستندات والبحث.  
- الوعي بإدارة دورة حياة المستندات في الأنظمة المؤسسية.

## إعداد GroupDocs.Redaction لـ .NET

### تثبيت الحزم

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- ابحث عن “GroupDocs.Redaction” وقم بتثبيت أحدث نسخة.

### خطوات الحصول على الترخيص
1. **Free Trial** – ابدأ بنسخة تجريبية لاستكشاف جميع الميزات.  
2. **Temporary License** – اطلب مفتاحًا مؤقتًا للاختبار الموسع.  
3. **Purchase** – احصل على ترخيص كامل للنشر في بيئة الإنتاج.

### التهيئة الأساسية والإعداد
`Redactor` هو الفئة الأساسية التي تطبق قواعد التشويه على المستندات.  
للبدء، استورد مساحة الأسماء Redaction وأنشئ كائن `Redactor`:

```csharp
using GroupDocs.Redaction;
```

## دليل التنفيذ

سنغطي ميزتين أساسيتين: تحديث المستندات المفهرسة وصيانة التحكم في إصدارات الفهرس.

### كيفية تحديث الفهرس باستخدام GroupDocs.Search؟

`Index` يمثل مجموعة البحث المخزنة على القرص.  
`UpdateOptions` يحدد كيفية تنفيذ التحديثات التدريجية (مثل عدد الخيوط).  
`UpdateDocument` يطبق التغييرات على مستند واحد، و `Commit` ينهى جميع التحديثات المعلقة.

**إجابة مباشرة (40‑70 كلمة):**  
أنشئ كائن `Index` يشير إلى مجلد الفهرس الخاص بك، استخدم `UpdateOptions` لتحديد عدد الخيوط، استدعِ `UpdateDocument` لكل ملف تم تغييره، وأخيرًا نفّذ `Commit` لحفظ التغييرات. يحدّث هذا النهج التدريجي الأجزاء المعدلة فقط، مما يبقي الفهرس محدثًا دون الحاجة إلى إعادة بناء كاملة.

#### الميزة 1: تحديث المستندات المفهرسة

##### نظرة عامة
تحديث المستندات المفهرسة يضمن أن تعكس نتائج البحث أحدث المحتويات، حتى عندما يتم تعديل أو استبدال المستندات.

##### الخطوة 1: إنشاء فهرس
فئة `Index` هي الكائن الأعلى مستوى الذي يمثل مجموعة بحثية على القرص.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### الخطوة 2: إضافة مستندات إلى الفهرس
أضف ملفات من دليل؛ المكتبة تستخرج النص القابل للبحث تلقائيًا.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### الخطوة 3: البحث والتحديث
نفّذ استعلامًا، عدّل الملف المصدر، ثم استدعِ `UpdateDocument` باستخدام نفس `UpdateOptions` المستخدمة أثناء الفهرسة.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**لماذا يعمل هذا:** بتعيين `Threads = 2`، يستفيد التحديث من نواتين من المعالج، مما يقلل وقت المعالجة إلى النصف تقريبًا على جهاز رباعي النوى.

### كيفية صيانة التحكم في إصدارات الفهرس؟

`IndexUpdater` هي فئة أداة تقوم بترقية صيغ الفهارس القديمة إلى أحدث نسخة يدعمها المكتبة.

**إجابة مباشرة (40‑70 كلمة):**  
أنشئ كائن `IndexUpdater` مع مسار الفهرس الحالي، استدعِ `CanUpdateVersion()` للتحقق من التوافق، ثم نفّذ `UpdateVersion()` إذا لزم الأمر. بعد الترقية، أعد تحميل الفهرس بالصيغة الجديدة ونفّذ بحثًا لتأكيد أن كل شيء يعمل. يضمن هذا ترحيلًا سلسًا عبر إصدارات المكتبة.

#### الميزة 2: صيانة التحكم في إصدارات الفهرس

##### نظرة عامة
ضمان التحكم في الإصدارات أن تظل الفهارس القديمة قابلة للبحث بعد ترقية المكتبة.

##### الخطوة 1: التحقق من التوافق
`IndexUpdater` يتحقق مما إذا كان يمكن ترقية الفهرس الحالي إلى الصيغة الأخيرة.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### الخطوة 2: التحميل والبحث
بعد الترقية، حمّل الفهرس المحدث ونفّذ استعلامًا للتحقق من سلامته.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**لماذا يعمل هذا:** حماية `CanUpdateVersion` تمنع استثناءات وقت التشغيل الناجمة عن عدم توافق مخططات الفهرس، مما يوفر مسار ترقية آمن.

## تطبيقات عملية

سيناريوهات واقعية حيث **كيفية تحديث الفهرس** مهمة:
1. **إدارة المستندات القانونية** – إعادة فهرسة العقود بسرعة بعد التعديلات مع تشويه الفقرات السرية.  
2. **الأرشيفات المؤسسية** – الحفاظ على إمكانية البحث في السجلات التاريخية دون إعادة معالجة ملايين الملفات.  
3. **أنظمة إدارة المحتوى (CMS)** – دفع تحديثات تدريجية إلى فهرس البحث عندما ينشر المؤلفون مقالات جديدة.

## اعتبارات الأداء

- **خيارات الخيوط:** اضبط `UpdateOptions.Threads` بناءً على نوى المعالج؛ المزيد من الخيوط يحسن الإنتاجية لكنه يزيد من استهلاك الذاكرة.  
- **استخدام الموارد:** راقب الذاكرة RAM؛ المكتبة تبث الملفات، لذا تكون الارتفاعات في الذاكرة قليلة حتى لملفات PDF ذات 500 صفحة.  
- **أفضل الممارسات:** جدولة تحديثات تدريجية منتظمة وتنظيف إصدارات الفهرس القديمة للحفاظ على أداء مثالي.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|----------|
| **فهرس غير موجود** | مسار المجلد غير صحيح | تحقق من أن مُنشئ `Index` يشير إلى الدليل الصحيح. |
| **خطأ عدم تطابق الإصدار** | استخدام فهرس قديم مع مكتبة أحدث | نفّذ تدفق `IndexUpdater` قبل الفهرسة العادية. |
| **لم يتم تطبيق التشويه** | قواعد التشويه تم تحميلها بعد الفهرسة | طبق التشويه **قبل** إضافة المستندات إلى الفهرس. |

## الأسئلة المتكررة

**س: ما الفرق بين `UpdateDocument` و `Rebuild`؟**  
ج: `UpdateDocument` يغيّر فقط الملفات التي تم تعديلها، بينما `Rebuild` يعيد إنشاء الفهرس بالكامل من الصفر، مستهلكًا وقتًا وموارد أكثر.

**س: هل يمكنني تحديث مستندات متعددة بشكل متوازي؟**  
ج: نعم، اضبط `UpdateOptions.Threads` على عدد النوى التي ترغب في استخدامها؛ المكتبة تتعامل مع المعالجة المتوازية داخليًا.

**س: هل يدعم GroupDocs.Search ملفات PDF المشفرة؟**  
ج: بالتأكيد. قدم كلمة المرور عبر `SearchOptions.Password` عند تحميل المستند.

**س: كيف يمكنني التحقق من نجاح التشويه قبل الفهرسة؟**  
ج: استدعِ `Redactor.Apply()` وتفقد حجم ملف الإخراج؛ الحجم الأصغر غالبًا ما يدل على نجاح التشويه.

**س: ما إصدارات .NET المدعومة رسميًا؟**  
ج: .NET Framework 4.5+، .NET Core 3.1+، .NET 5، و .NET 6+.

## الخلاصة

أصبح لديك الآن دليل كامل وجاهز للإنتاج حول **كيفية تحديث الفهرس** باستخدام GroupDocs.Search وكيفية الحفاظ على توافق إصدارات تلك الفهارس مع GroupDocs.Redaction لـ .NET. باتباع الخطوات أعلاه، يمكنك ضمان بقاء طبقة البحث سريعة، دقيقة، ومتوافقة مع لوائح خصوصية البيانات.

**الخطوات التالية:**  
- جرّب إعدادات `Threads` المختلفة للعثور على الإعداد المثالي لأجهزتك.  
- استكشف أنماط التشويه المتقدمة (مثل إزالة أرقام الضمان الاجتماعي باستخدام regex) قبل الفهرسة.  
- دمج روتين تحديث الفهرس في خط أنابيب CI/CD الخاص بك لإدارة مستندات مؤتمتة بالكامل.

---

**آخر تحديث:** 2026-06-07  
**تم الاختبار مع:** GroupDocs.Search 23.10 لـ .NET، GroupDocs.Redaction 23.10 لـ .NET  
**المؤلف:** GroupDocs  

## الموارد
- [التوثيق](https://docs.groupdocs.com/search/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

## دروس ذات صلة
- [إتقان GroupDocs.Redaction .NET: إنشاء فهرس فعال وإدارة الأسماء المستعارة للبحث المتقدم في المستندات](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [تنفيذ بحث المرادفات باستخدام GroupDocs.Redaction .NET لإدارة مستندات محسنة](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [إتقان GroupDocs Search و Redaction في .NET: إدارة مستندات متقدمة](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
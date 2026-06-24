---
date: '2026-04-02'
description: تعلم كيفية إنشاء فهرس بحث GroupDocs وإضافة المستندات إلى الفهرس أثناء
  تنفيذ البحث الموجه باستخدام GroupDocs.Search وGroupDocs.Redaction في .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: إنشاء فهرس بحث GroupDocs مع التعتيم والبحث الموجه بالخصائص في .NET
type: docs
url: /ar/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# إنشاء فهرس بحث GroupDocs مع Redaction .NET للبحث الموجه

في التطبيقات الحديثة، **إنشاء فهرس بحث مع GroupDocs** أمر أساسي لاسترجاع المستندات بسرعة ودقة. سواء كنت تتعامل مع العقود القانونية، أو كتالوجات المنتجات، أو قواعد معرفة ضخمة، فإن فهرسًا مُصممًا جيدًا يتيح لك **إضافة مستندات إلى الفهرس** وتشغيل عمليات بحث موجهة قوية في ثوانٍ. هذا الدليل يشرح لك العملية بالكامل — من إعداد GroupDocs.Redaction إلى صياغة استعلامات موجهة بسيطة ومعقدة — لتتمكن من تقديم تجربة بحث سريعة في مشاريع .NET الخاصة بك.

## إجابات سريعة
- **ما هو الهدف الأساسي؟** لإنشاء فهرس بحث مع GroupDocs وتمكين البحث الموجه.  
- **ما المكتبات المطلوبة؟** GroupDocs.Redaction و GroupDocs.Search لـ .NET.  
- **كيف يمكنني إضافة مستندات إلى الفهرس؟** استخدم `index.Add(documentsFolder)` بعد تهيئة الفهرس.  
- **هل يمكنني تشغيل استعلامات معقدة؟** نعم، اجمع استعلامات الكائنات مع عوامل منطقية للتصفية المتقدمة.  
- **هل تحتاج إلى ترخيص؟** نسخة تجريبية مجانية تعمل للتطوير؛ الترخيص التجاري مطلوب للإنتاج.

## ما هو البحث الموجه ولماذا يستخدم مع GroupDocs؟

يسمح البحث الموجه للمستخدمين بتصفية النتائج عن طريق تطبيق عدة عوامل تصفية—مثل الفئة، التاريخ، أو المؤلف—في آن واحد. عند دمجه مع **GroupDocs.Redaction**، تحصل على محتوى آمن وقابل للبحث يحترم قواعد الإخفاء، مما يجعله مثاليًا للبيئات ذات المتطلبات الصارمة للامتثال.

## المتطلبات المسبقة

### المكتبات المطلوبة، الإصدارات، والاعتمادات
- **GroupDocs.Redaction .NET** – أحدث إصدار مستقر.  
- **GroupDocs.Search .NET** – يعمل جنبًا إلى جنب مع Redaction للفهرسة.

### متطلبات إعداد البيئة
- **IDE**: Visual Studio 2019 أو أحدث.  
- **Framework**: .NET Core 3.1، .NET 5، أو .NET 6.  
- **OS Compatibility**: Windows، Linux، macOS.

### متطلبات المعرفة
ستساعد مهارات C# الأساسية وفهم عالي المستوى لمفاهيم البحث الموجه، لكن الدليل خطوة بخطوة صديق للمبتدئين أيضًا.

## إعداد GroupDocs.Redaction لـ .NET

### معلومات التثبيت
يمكنك إضافة حزمة GroupDocs.Redaction باستخدام أي من الطرق التالية:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- ابحث عن "GroupDocs.Redaction" وقم بتثبيت أحدث إصدار.

### خطوات الحصول على الترخيص
لفتح جميع الميزات، ابدأ بنسخة تجريبية مجانية أو احصل على ترخيص دائم:

1. زر [شراء GroupDocs](https://purchase.groupdocs.com/temporary-license/) لاستكشاف خيارات الترخيص.  
2. اتبع التعليمات على الشاشة لتلقي ملف الترخيص التجريبي أو المشترا.

### التهيئة الأساسية والإعداد
Once the package is installed, initialize the Redactor in your application:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## كيفية إنشاء فهرس بحث groupdocs

فيما يلي نقسم التنفيذ إلى جزأين: **Simple Faceted Search** و **Complex Query**. يوضح كل جزء كيفية **إنشاء فهرس بحث groupdocs**، إضافة المستندات، وتشغيل الاستعلامات.

### الميزة 1: بحث موجه بسيط

**نظرة عامة**  
يسمح البحث الموجه للمستخدمين بتضييق النتائج عن طريق اختيار معايير متعددة. يوضح هذا القسم نهجًا بسيطًا باستخدام GroupDocs.Search.

#### الخطوة 1: تعريف مجلدات الفهرس والمستندات
قم بإعداد مسارات المجلدات حيث سيقع الفهرس وأين توجد المستندات المصدر.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### الخطوة 2: إنشاء فهرس
تهيئة فهرس البحث في المجلد الذي حددته.

```csharp
Index index = new Index(indexFolder);
```

#### الخطوة 3: إضافة مستندات إلى الفهرس
حمّل مستنداتك لتصبح قابلة للبحث.

```csharp
index.Add(documentsFolder);
```

#### الخطوة 4: تنفيذ بحث نصي
نفّذ استعلام نصي أساسي ضد حقل **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### الخطوة 5: تنفيذ بحث استعلام كائن
استخدم استعلامات موجهة للكائنات للحصول على تحكم أدق.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### الميزة 2: استعلام معقد

**نظرة عامة**  
عندما تحتاج إلى دمج عدة عوامل تصفية—مثل أنماط أسماء الملفات ومطابقات العبارات—يمكنك بناء استعلام معقد باستخدام عوامل منطقية.

#### الخطوة 1: تعريف مجلدات الفهرس والمستندات
أعد استخدام نفس بنية المجلدات لسيناريو أكثر تقدمًا.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### الخطوة 2: إنشاء فهرس وإضافة مستندات
(انظر الخطوتين 2‑3 من المثال البسيط؛ يبقيان كما هما.)

#### الخطوة 3: تنفيذ بحث استعلام نصي
نفّذ استعلام نصي مركب يجمع بين معايير اسم الملف والمحتوى.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### الخطوة 4: بناء وتنفيذ استعلامات كائن
أنشئ نفس المنطق برمجيًا.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

استمر في دمج العبارات، النطاقات، وعوامل بوليانية لتطابق قواعد عملك الدقيقة.

## التطبيقات العملية

1. **E‑Commerce Platforms** – تصفية المنتجات حسب الفئة، السعر، والتقييم.  
2. **Document Management Systems** – العثور على العقود حسب المؤلف، التاريخ، أو مستوى السرية.  
3. **Content Portals** – السماح للقراء بالتعمق عبر الوسوم، المواضيع، وتواريخ النشر.

## اعتبارات الأداء

- **Index Refresh**: أعد فهرسة الملفات الجديدة أو المحدثة بانتظام للحفاظ على سرعة البحث.  
- **Memory Management**: حرّر كائنات `Index` عند الانتهاء، خاصةً لمجموعات البيانات الكبيرة.  
- **Asynchronous Indexing**: استخدم `Task.Run` أو خدمات الخلفية لتجنب تجميد واجهة المستخدم أثناء الفهرسة الثقيلة.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **Index not found** | تحقق من مسار `indexFolder` وتأكد من أن المجلد يملك أذونات كتابة. |
| **No results returned** | تأكد من أن الحقول التي تستعلم عنها (مثل `Content`، `Filename`) مفهرسة. |
| **Out‑of‑memory errors** | عالج المستندات على دفعات وفكّر في زيادة حجم كومة .NET GC. |

## الأسئلة المتكررة

**س: ما هو البحث الموجه؟**  
ج: يسمح البحث الموجه للمستخدمين بتصفية النتائج باستخدام عدة عوامل تصفية مستقلة مثل الفئة، التاريخ، أو المؤلف.

**س: كيف أتعامل مع مجموعات بيانات كبيرة باستخدام GroupDocs.Search؟**  
ج: استخدم الفهرسة المتزايدة، المعالجة على دفعات، والعمليات غير المتزامنة للحفاظ على انخفاض استهلاك الذاكرة وارتفاع الأداء.

**س: هل يمكن دمج وظائف GroupDocs في تطبيقات .NET الحالية؟**  
ج: نعم، تم تصميم المكتبات لتكامل سلس مع أي مشروع .NET.

**س: ما هي بعض المشكلات الشائعة مع البحث الموجه؟**  
ج: صعوبة صياغة الاستعلامات المعقدة وضمان فهرسة جميع الحقول ذات الصلة هي تحديات شائعة؛ الاختبار المناسب وصيانة الفهرس يخففان منها.

**س: كيف أحصل على ترخيص مؤقت لـ GroupDocs؟**  
ج: زر [صفحة ترخيص GroupDocs](https://purchase.groupdocs.com/temporary-license/) لتقديم طلب للحصول على ترخيص تجريبي يفتح جميع الوظائف أثناء التقييم.

## الموارد

- **الوثائق**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **مرجع API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**آخر تحديث:** 2026-04-02  
**تم الاختبار مع:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**المؤلف:** GroupDocs
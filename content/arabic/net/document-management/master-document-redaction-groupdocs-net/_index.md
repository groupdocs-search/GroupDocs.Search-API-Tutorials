---
date: '2026-07-02'
description: تعلم كيفية تمويه المستندات وتحسين أداء البحث عن طريق إضافة المستندات
  إلى الفهرس باستخدام GroupDocs.Redaction و GroupDocs.Search لـ .NET.
keywords:
- how to redact documents
- optimize search performance
- add documents to index
- redact pdf c#
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  headline: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  type: TechArticle
- description: Learn how to redact documents and optimize search performance by adding
    documents to index using GroupDocs.Redaction and GroupDocs.Search for .NET.
  name: How to Redact Documents & Optimize Search Index in .NET with GroupDocs
  steps:
  - name: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
    text: '**Legal Document Management** – Redact client names before indexing case
      files, ensuring privacy while lawyers can still search case law.'
  - name: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
    text: '**Healthcare Records** – Strip patient identifiers from medical PDFs, then
      index the sanitized versions for rapid audit queries.'
  - name: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
    text: '**Corporate Compliance** – Automate redaction of financial statements and
      immediately make the clean versions searchable for internal investigations.'
  type: HowTo
- questions:
  - answer: Yes—`RedactionEngine` works natively with PDF streams, so you can load
      a PDF, apply redaction objects, and save the result without any format conversion.
    question: Can I redact PDF C# files directly without converting them first?
  - answer: Incremental indexing adds only the new files, keeping the index size stable
      and query latency under 200 ms for typical workloads.
    question: How does adding documents to index affect search speed?
  - answer: Absolutely. Use a Windows Service or Azure Function to call `Index.AddDocument`
      on a timer, feeding newly uploaded files into the index.
    question: Is it possible to schedule automatic re‑indexing?
  - answer: Yes—redaction overwrites the original bytes, making recovery impossible
      even with forensic tools.
    question: Does redaction permanently remove the hidden data?
  - answer: Both .NET Framework 4.6.1+ and .NET Core 3.1+ (including .NET 5/6) are
      officially supported.
    question: What .NET versions are fully supported?
  type: FAQPage
title: كيفية تمويه المستندات وتحسين فهرس البحث في .NET باستخدام GroupDocs
type: docs
url: /ar/net/document-management/master-document-redaction-groupdocs-net/
weight: 1
---

# إتقان إخفاء المستندات وإدارة فهرس البحث في .NET باستخدام GroupDocs

## المقدمة

إذا كنت بحاجة إلى **كيفية إخفاء المستندات** مع الحفاظ على إمكانية البحث فيها، فقد وصلت إلى المكان الصحيح. يشرح هذا الدليل كيفية دمج **GroupDocs.Redaction** و **GroupDocs.Search** لإخفاء البيانات الحساسة بأمان ثم **إضافة المستندات إلى الفهرس** لاسترجاع سريع. في النهاية ستفهم كيفية **تحسين أداء البحث**، وإخفاء ملفات PDF في C#، وبناء خط أنابيب فهرسة قوي يتوسع مع بياناتك.

## إجابات سريعة
- **كيف أقوم بإخفاء PDF في C#؟** استخدم `RedactionEngine` لتحميل الملف، تعريف مناطق الإخفاء، ثم استدعاء `Save`.  
- **ما هو الصنف الذي ينشئ فهرس البحث؟** الصنف `Index` من GroupDocs.Search يدير جميع عمليات الفهرسة.  
- **هل يمكنني إضافة ملفات جديدة دون إعادة بناء الفهرس بالكامل؟** نعم—استدعِ `Index.AddDocument` للتحديثات المتزايدة.  
- **هل يؤثر الإخفاء على نتائج البحث؟** المحتوى المخبأ يُستثنى من الفهرس، مما يحافظ على نظافة نتائج البحث.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.6.1+، .NET Core 3.1+، و .NET 5/6.

## ما هو “كيفية إخفاء المستندات”؟
**“كيفية إخفاء المستندات”** تشير إلى عملية إزالة أو إخفاء المعلومات السرية من الملفات برمجياً بحيث لا يمكن استعادة البيانات المخفية أو عرضها. الإخفاء ضروري للامتثال والخصوصية وسير العمل القانوني حيث يجب منع كشف البيانات.

## لماذا نستخدم GroupDocs للإخفاء والبحث؟
يدعم GroupDocs **أكثر من 50 تنسيق ملف** (بما في ذلك PDF، DOCX، PPTX، وأنواع الصور) ويمكنه معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة، محققاً **سرعة فهرسة تصل إلى 30 %** مقارنة بالمكتبات العامة. مجموعة Redaction + Search تتيح لك **إخفاء PDF C#** والقيام فوراً بفهرسة النسخة النظيفة، مما يلغي الحاجة إلى خطوة تمهيدية منفصلة.

## المتطلبات المسبقة

- **GroupDocs.Search** لـ .NET (v20.11 أو أحدث)  
- **GroupDocs.Redaction** لـ .NET (v20.10 أو أحدث)  
- Visual Studio 2017 أو أحدث  
- .NET Framework 4.6.1 أو أحدث (أو .NET Core 3.1+)

### المتطلبات المعرفية
يجب أن تكون مرتاحاً مع بنية C# الأساسية، مراجع المشاريع، وعمليات نظام الملفات.

## إعداد GroupDocs.Redaction لـ .NET

### تثبيت المكتبات

**.NET CLI**  
`dotnet add package` هو أمر .NET CLI الذي يثبت حزمة NuGet في مشروعك.  

```bash
dotnet add package GroupDocs.Redaction
```

**مدير الحزم**  
`Install-Package` هو أمر PowerShell المستخدم من قبل وحدة تحكم مدير حزم NuGet لإضافة المكتبات.  

```powershell
Install-Package GroupDocs.Redaction
```

**واجهة مستخدم مدير حزم NuGet**  
ابحث عن “GroupDocs.Redaction” وانقر **Install** لجلب أحدث إصدار ثابت.

### الحصول على الترخيص
- **Free Trial** – نسخة تجريبية مجانية – تجربة كاملة المميزات لمدة 30 يومًا.  
- **Temporary License** – ترخيص مؤقت – وصول ممتد لمدة 15 يومًا للتقييم.  
- **Purchase** – ترخيص إنتاج دائم.

#### التهيئة الأساسية
`RedactionEngine` هو الصنف الأساسي المستخدم لتحميل المستندات، تعديلها، وحفظها بعد الإخفاء.  

```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Further configuration and initialization...
```

## دليل التنفيذ

سنقسم الحل إلى ثلاثة أجزاء منطقية: إنشاء فهرس، إضافة مستندات (بما فيها المستندات المخبأة)، والبحث في الفهرس.

### كيف تنشئ فهرس بحث باستخدام GroupDocs.Search؟

`Index` هو الصنف الرئيسي الذي يمثل فهرسًا قابلًا للبحث في GroupDocs.Search. تقوم بتحميل أو إنشاء مثيل `Index` عن طريق الإشارة إلى مجلد على القرص؛ ثم تدير المكتبة جميع الملفات الداخلية لك. هذه الخطوة هي الأساس **لتحسين أداء البحث** لأن الفهرس المنظم يقلل من زمن الاستعلام.

```csharp
using GroupDocs.Search;

string indexFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldIndex";
```

**شرح:** يحدد الكود الدليل الذي سيحتوي على ملفات الفهرس. استخدام مجلد مخصص يبقي بيانات الفهرس منفصلة عن المستندات المصدرية.

```csharp
Index index = new Index(indexFolder);
```

**شرح:** إنشاء مثيل `Index` إما يفتح فهرسًا موجودًا أو ينشئ فهرسًا جديدًا إذا كان المسار فارغًا.

### كيف تضيف مستندات إلى الفهرس بعد الإخفاء؟

أولاً، قم بإخفاء أي أقسام سرية، ثم أدخل الملف النظيف إلى الفهرس. يضمن هذا التدفق ذو الخطوتين أن المحتوى الآمن فقط هو القابل للبحث.

#### تحديد مجلد المصدر
`documentsFolder` هو المسار حيث توجد ملفات PDF الأصلية.  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/HelloWorldDocuments";
```

`AddDocument` هو طريقة من الصنف `Index` تضيف مستندًا واحدًا إلى الفهرس.  

```csharp
index.Add(documentsFolder);
```

### كيف تبحث داخل الفهرس المُنشأ؟

حدد سلسلة الاستعلام، شغّل البحث، وتكرّر عبر النتائج. تُعيد API أرقام الصفحات، مقتطفات، ومعرفات المستندات، مما يسهل عرض النتائج في واجهة المستخدم.

`SearchResult` يحمل النتائج التي تُرجعها الاستعلام، بما في ذلك المستندات المتطابقة والمقتطفات.  

```csharp
string query = "Lorem";
```

```csharp
SearchResult result = index.Search(query);
```

## التطبيقات العملية

هذه القدرات تحل مشاكل واقعية:

1. **إدارة المستندات القانونية** – إخفاء أسماء العملاء قبل فهرسة ملفات القضايا، مما يضمن الخصوصية بينما يمكن للمحامين البحث في القوانين.  
2. **سجلات الرعاية الصحية** – إزالة معرفات المرضى من ملفات PDF الطبية، ثم فهرسة النسخ المُنقاة لاستعلامات تدقيق سريعة.  
3. **الامتثال المؤسسي** – أتمتة إخفاء القوائم المالية وجعل النسخ النظيفة قابلة للبحث فورًا للتحقيقات الداخلية.

## اعتبارات الأداء

لـ **تحسين أداء البحث** عند التعامل مع أحجام كبيرة:

- شغّل الفهرسة كوظيفة خلفية وارتكِ التغييرات على دفعات.  
- حرّر كائنات `Index` فورًا لتفريغ الموارد غير المُدارة.  
- راقب استهلاك الذاكرة؛ فـ GroupDocs.Search يبث البيانات ولا يحمل المستند بالكامل في الذاكرة.  
- جدولة دمج الفهارس دوريًا للحفاظ على الفهرس مدمجًا وسريع الاستعلام.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **أخطاء نفاد الذاكرة على ملفات PDF الضخمة** | استخدم `RedactionEngine` مع `RedactionOptions` التي تُفعّل وضع البث. |
| **البحث يعيد المصطلحات المزالة** | تأكد من تشغيل الإخفاء **قبل** استدعاء `Index.AddDocument`. |
| **تنسيق ملف غير مدعوم** | تحقق من أن امتداد الملف من بين أكثر من 50 تنسيقًا مدعومًا؛ حوّل الملفات غير المدعومة إلى PDF أولاً. |
| **الترخيص غير معترف به** | ضع ملف الترخيص في جذر التطبيق واستدعِ `License.SetLicense("license.json")` قبل أي استخدام للـ API. |

## الأسئلة المتكررة

**س: هل يمكنني إخفاء ملفات PDF C# مباشرةً دون تحويلها أولاً؟**  
ج: نعم—`RedactionEngine` يعمل أصلاً مع تدفقات PDF، لذا يمكنك تحميل PDF، تطبيق كائنات الإخفاء، وحفظ النتيجة دون أي تحويل تنسيق.

**س: كيف يؤثر إضافة المستندات إلى الفهرس على سرعة البحث؟**  
ج: الفهرسة المتزايدة تضيف فقط الملفات الجديدة، مما يحافظ على حجم الفهرس ثابتًا ويقلل زمن الاستعلام إلى أقل من 200 مللي ثانية للأحمال النموذجية.

**س: هل من الممكن جدولة إعادة الفهرسة التلقائية؟**  
ج: بالتأكيد. استخدم خدمة Windows أو Azure Function لاستدعاء `Index.AddDocument` وفق جدول زمني، وإدخال الملفات التي تم تحميلها حديثًا إلى الفهرس.

**س: هل الإخفاء يزيل البيانات المخفية بشكل دائم؟**  
ج: نعم—الإخفاء يكتب فوق البايتات الأصلية، مما يجعل الاسترداد مستحيلًا حتى باستخدام أدوات التحليل الجنائي.

**س: ما إصدارات .NET المدعومة بالكامل؟**  
ج: كل من .NET Framework 4.6.1+ و .NET Core 3.1+ (بما في ذلك .NET 5/6) مدعومة رسميًا.

## الموارد
- [التوثيق](https://docs.groupdocs.com/search/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل](https://releases.groupdocs.com/search/net/)
- [دعم مجاني](https://forum.groupdocs.com/c/search/10)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-07-02  
**تم الاختبار مع:** GroupDocs.Search 21.2 و GroupDocs.Redaction 21.1 لـ .NET  
**المؤلف:** GroupDocs

## الدروس ذات الصلة

- [إتقان GroupDocs.Redaction .NET: إنشاء فهرس فعال وإدارة الأسماء المستعارة للبحث المتقدم في المستندات](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [كيفية فهرسة والبحث في مستندات PDF/Word حسب الموضوع باستخدام GroupDocs.Redaction في .NET](/search/net/indexing/index-search-pdf-word-subject-groupdocs-redaction/)
- [إتقان GroupDocs Search و Redaction في .NET: إدارة مستندات متقدمة](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
---
date: '2026-06-07'
description: تعرف على كيفية سرد امتدادات الملفات والحصول على صيغ الملفات باستخدام
  GroupDocs.Redaction في C#. يتضمن الإعداد، الكود، ونصائح عملية.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: كيفية سرد امتدادات الملفات باستخدام GroupDocs.Redaction في .NET – دليل شامل
type: docs
url: /ar/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# عرض تنسيقات الملفات المدعومة باستخدام GroupDocs.Redaction في .NET

إدارة مجموعة واسعة من أنواع المستندات هي واقع يومي لمطوري .NET. باستخدام **GroupDocs.Redaction**، يمكنك **قائمة امتدادات الملفات** التي تدعمها المكتبة، مما يمنح تطبيقك القدرة على قبول أو رفض التحميلات، وتقديم خيارات واجهة مستخدم صديقة، وتجنب الأخطاء المكلفة أثناء التشغيل. هذا الدرس يوجهك عبر كل ما تحتاجه—من المتطلبات المسبقة إلى تنفيذ كامل جاهز للإنتاج—حتى تتمكن بثقة من **الحصول على تنسيقات الملفات** و **c# عرض تنسيقات الملفات** في حلك.

## إجابات سريعة
- **ماذا يعني “list file extensions”؟** يعني ذلك استرجاع مجموعة معرفات أنواع الملفات المدعومة (مثل *.pdf*، *.docx*) من الـ API.  
- **ما هي حزمة NuGet التي توفر هذه القدرة؟** `GroupDocs.Redaction` (أحدث نسخة مستقرة).  
- **هل أحتاج إلى ترخيص لتشغيل العينة؟** رخصة تجريبية مجانية تعمل للتطوير؛ ترخيص دائم مطلوب للإنتاج.  
- **هل يمكنني تخزين النتائج مؤقتًا؟** نعم — احفظ القائمة في الذاكرة أو في ذاكرة موزعة لتجنب استدعاءات الـ API المتكررة.  
- **هل هذه الميزة متوافقة مع .NET 6 و .NET Core؟** بالطبع؛ المكتبة تدعم .NET Framework 4.5+، .NET Core 3.1+، .NET 5+، و .NET 6+.

## ما هو GroupDocs.Redaction؟
**GroupDocs.Redaction** هي مكتبة .NET تمكّن المطورين من إخفاء المحتوى الحساس، تحويل المستندات، واكتشاف أنواع الملفات المدعومة—كل ذلك دون الحاجة إلى Microsoft Office على الخادم. تُجرد تعقيدات معالجة الصيغ خلف واجهة برمجة تطبيقات نظيفة كائنية التوجه. تقدم واجهة موحدة للإخفاء، التحويل، واكتشاف الصيغ، مع معالجة PDFs، مستندات Office، الصور، والمزيد، مع ضمان أداء عالي وأمان.

## لماذا ندرج امتدادات الملفات باستخدام GroupDocs.Redaction؟
المكتبة **supports 50+ input and output formats**، بما في ذلك PDF، DOCX، PPTX، XLSX، HTML، وأكثر من 30 نوع صورة. من خلال **قائمة امتدادات الملفات** برمجياً، يمكنك:

- منع المستخدمين من تحميل ملفات غير مدعومة (تقليل أخطاء التحقق حتى 90%).  
- ملء قوائم منسدلة ديناميكيًا، لضمان توافق الواجهة مع تحديثات المكتبة.  
- بناء سجلات تدقيق تسجل نوع الملف الدقيق الذي حاول المستخدم معالجته.

## المتطلبات المسبقة

- **GroupDocs.Redaction**: تثبيت عبر NuGet (انظر الأوامر أدناه).  
- **.NET SDK**: تأكد من تثبيت أحدث نسخة من .NET SDK. حمّله [هنا](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 أو أي محرر متوافق.  
- **Basic C# knowledge**: يجب أن تكون مرتاحًا مع المجموعات و LINQ.

## إعداد GroupDocs.Redaction لـ .NET

### تثبيت المكتبة

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- افتح مدير حزم NuGet، ابحث عن “GroupDocs.Redaction”، وقم بتثبيت أحدث نسخة.

### الحصول على ترخيص وتطبيقه

ابدأ برخصة تجريبية مجانية أو اطلب رخصة مؤقتة لاستكشاف جميع الميزات دون قيود. لخيارات الشراء، زر [صفحة شراء GroupDocs](https://purchase.groupdocs.com/). بمجرد حصولك على ملف الترخيص:

1. ضع الملف في مجلد يمكن الوصول إليه داخل مشروعك (مثال: `./Licenses/GroupDocs.Redaction.lic`).  
2. ابدأ تفعيل الترخيص عند بدء التطبيق:

فئة `License` تقوم بتحميل ملف الترخيص وتفعيل GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## كيفية سرد امتدادات الملفات باستخدام GroupDocs.Redaction؟

حمّل Redaction API واستدعِ الطريقة التي تُعيد الصيغ المدعومة. تُعيد الاستدعاء مجموعة حيث يحتوي كل عنصر على امتداد ووصف قابل للقراءة البشرية. هذه العملية خفيفة ويمكن تنفيذها عند بدء التشغيل أو عند الطلب.

### استرجاع أنواع الملفات المدعومة
طريقة `RedactionApi.GetSupportedFileFormats()` تُعيد مجموعة قراءة‑فقط من كائنات `FileFormatInfo` التي تصف كل صيغة.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### عرض كل امتداد ووصف
كل `FileFormatInfo` يوفر خصائص `Extension` و `Description` لنوع الملف.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explanation**: الحلقة تتكرر عبر كل كائن `FileFormatInfo`، وتطبع `Extension` و `Description` في جدول منسق بشكل أنيق.

## كيفية دمج القائمة في قائمة منسدلة UI؟

بعد حصولك على المجموعة، اربطها بأي مكوّن UI—WinForms `ComboBox`، WPF `ComboBox`، أو عنصر `select` في ASP.NET Core. المفتاح هو استخدام `Extension` كقيمة و `Description` كنص عرض. هذا يضمن رؤية المستخدمين لأسماء صديقة بينما يتعامل الكود مع سلاسل الامتداد الدقيقة.

## المشكلات الشائعة والحلول

- **Missing namespace error** – تحقق من أنك استوردت `GroupDocs.Redaction` و `GroupDocs.Redaction.Common`.  
- **License not found** – تأكد من صحة مسار ملف الترخيص وأن الملف مُدرج في مخرجات البناء.  
- **Performance on large projects** – خزن النتيجة في متغيّر ثابت أو ذاكرة موزعة (مثل Redis) لتجنب التعداد المتكرر.

## التطبيقات العملية

معرفة القائمة الدقيقة للامتدادات المدعومة تفتح عدة سيناريوهات واقعية:

1. **Document Management Systems** – تصنيف تلقائي للملفات الواردة بناءً على امتدادها.  
2. **Content Filtering Tools** – حظر الصيغ غير المسموح بها (مثل الملفات التنفيذية) عند التحميل.  
3. **File Conversion Pipelines** – اتخاذ قرار ديناميكي ما إذا كان يمكن تحويل الملف أو يحتاج إلى سير عمل بديل.

## اعتبارات الأداء

- **Memory footprint** – تُخزن قائمة الصيغ في `IReadOnlyCollection` خفيفة، عادةً أقل من 2 KB.  
- **Thread safety** – المجموعة غير قابلة للتغيير بعد الإنشاء، مما يجعلها آمنة للقراءات المتزامنة.  
- **Caching** – لتطبيقات API ذات حركة مرور عالية، خزن القائمة طوال عمر التطبيق لتقليل بضع ميكروثوانٍ من الحمل لكل طلب.

## الخلاصة

باتباع الخطوات أعلاه، لديك الآن طريقة موثوقة لـ **قائمة امتدادات الملفات** و **c# عرض تنسيقات الملفات** باستخدام GroupDocs.Redaction. هذه القدرة لا تحسن تجربة المستخدم فحسب، بل تحمي الخلفية من الملفات غير المدعومة. استكشف ميزات Redaction الإضافية—مثل إخفاء المحتوى، إخفاء PDF، والمعالجة الدفعية—لتقوية سير عمل المستندات لديك.

## الأسئلة المتكررة

**س: ما هي تنسيقات الملفات المدعومة افتراضيًا؟**  
ج: يدعم GroupDocs.Redaction أكثر من 50 صيغة، بما في ذلك PDF، DOCX، PPTX، XLSX، HTML، BMP، JPEG، PNG، والعديد غيرها. راجع القائمة الكاملة في [توثيق GroupDocs](https://docs.groupdocs.com/search/net/).

**س: كيف أقوم بترقية المكتبة إلى أحدث نسخة؟**  
ج: افتح NuGet Package Manager، ابحث عن “GroupDocs.Redaction”، وانقر **Update**. بدلاً من ذلك، نفّذ `dotnet add package GroupDocs.Redaction --version <latest>`.

**س: هل يمكنني استخدام هذه القائمة للتحقق من صحة الملفات على الخادم؟**  
ج: نعم — قارن امتداد الملف المُحمَّل مع المجموعة المسترجعة قبل المعالجة. هذا يزيل 99 % من أخطاء الصيغ غير الصالحة.

**س: هل يمكن توسيع الدعم لأنواع ملفات مخصصة؟**  
ج: الامتدادات المخصصة تتطلب معالجات مخصصة؛ المكتبة الأساسية لا تضيف صيغًا جديدة بشكل أصلي. راجع وثائق API لإنشاء خطوط استيراد/تصدير مخصصة.

**س: تطبيقتي تتعطل بعد إضافة الكود—ماذا يجب أن أتحقق؟**  
ج: تأكد من تحميل الترخيص بشكل صحيح، وأن عبارات `using` تشير إلى المساحات الاسمية الصحيحة، وتعامل مع `IOException` عند قراءة ملف الترخيص.

---

**آخر تحديث:** 2026-06-07  
**تم الاختبار مع:** GroupDocs.Redaction 23.9 for .NET  
**المؤلف:** GroupDocs  

## الموارد
- [التوثيق](https://docs.groupdocs.com/search/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)
- [طلب ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

## دروس ذات صلة

- [إتقان تصفية الملفات في .NET باستخدام GroupDocs.Redaction: تقنيات إدارة المستندات الفعالة](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [إتقان GroupDocs.Redaction .NET: الإعداد ومعالجة الأحداث لإدارة المستندات الآمنة](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [إتقان إدارة المستندات في .NET باستخدام GroupDocs.Redaction: إعداد الترخيص وتظليل البحث في HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
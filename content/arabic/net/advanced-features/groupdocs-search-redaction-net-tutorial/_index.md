---
date: '2026-04-04'
description: تعلم كيفية البحث في المستندات القانونية وإدارة الفهارس باستخدام GroupDocs.Search،
  وتكامل التمويه للسجلات الطبية مع GroupDocs.Redaction في .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: ابحث عن المستندات القانونية باستخدام GroupDocs Search & Redaction لـ .NET
type: docs
url: /ar/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# بحث المستندات القانونية باستخدام GroupDocs Search & Redaction في .NET

في بيئة اليوم المعتمدة على البيانات، **البحث في المستندات القانونية** بسرعة وأمان هو مطلب حاسم لأي مؤسسة. سواء كنت تتعامل مع العقود أو ملفات المحكمة أو تقارير الامتثال، يوفر لك GroupDocs.Search فهرسًا سريعًا وقابلًا للتوسع، بينما يضمن GroupDocs.Redaction إخفاء المعلومات الحساسة. يوضح لك هذا البرنامج التعليمي كيفية إعداد فهرس قابل للبحث، إضافة مستندات من مجلدات متعددة، وتكوين الممحاة لتتمكن من البحث بأمان في السجلات الطبية وغيرها من الملفات السرية.

## الإجابات السريعة
- **ما الذي يفعله GroupDocs.Search؟** إنه ينشئ فهرسًا قابلًا للبحث بالنص الكامل لمجموعة واسعة من صيغ المستندات.  
- **هل يمكنني محو المعلومات قبل البحث؟** نعم – استخدم GroupDocs.Redaction لإخفاء أو إزالة البيانات الحساسة.  
- **كيف يمكنني إضافة مستندات إلى الفهرس؟** استدعِ `index.Add("folderPath")` لكل مجلد تريد تضمينه.  
- **ما أنواع الملفات المدعومة؟** PDFs، DOCX، PPTX، TXT، والعديد غيرها.  
- **هل أحتاج إلى ترخيص للإنتاج؟** تتوفر نسخة تجريبية مؤقتة؛ يلزم الحصول على ترخيص دائم للاستخدام التجاري.

## المتطلبات المسبقة
لتتبع هذا البرنامج التعليمي، تأكد من أن لديك:
- .NET Core SDK (3.1 أو أحدث) مثبتًا.
- Visual Studio Code أو Visual Studio أو أي بيئة تطوير تدعم .NET.
- إلمام أساسي ببرمجة C#.

### الحصول على الترخيص
يمكنك البدء بنسخة تجريبية مجانية من كلا المكتبتين. للاستخدام الموسع، فكر في الحصول على ترخيص مؤقت أو شراء واحد من [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/).

## تثبيت الحزم المطلوبة

**تثبيت GroupDocs.Search:**  
باستخدام **.NET CLI**، نفّذ:
```bash
dotnet add package GroupDocs.Search
```
بدلاً من ذلك، استخدم وحدة التحكم Package Manager Console في Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**تثبيت GroupDocs.Redaction:**  
- استخدم .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- أو عبر Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

قم بزيارة واجهة NuGet Package Manager UI وابحث عن "GroupDocs.Redaction" لتثبيتها إذا كنت تفضّل واجهة رسومية.

## تكوين إعدادات الممحاة
قبل أن تبدأ بالمحو، قد ترغب في تعديل سلوك الممحاة (مثل ضبط لون الممحاة أو تعريف أنماط مخصصة). يوضح المقتطف التالي التهيئة الأساسية:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **نصيحة احترافية:** اضبط `redactorSettings` لتتناسب مع سياسات الامتثال في مؤسستك (مثل استبدال النص بمربعات سوداء، تطبيق OCR قبل الممحاة، إلخ).

## دليل التنفيذ

### كيفية البحث في المستندات القانونية؟
إنشاء فهرس قابل للبحث هو الأساس لاسترجاع المستندات القانونية بسرعة. يتيح لك GroupDocs.Search الإشارة إلى أي مجلد، بناء فهرس، ثم تنفيذ استعلامات معقدة عبر آلاف الملفات.

### كيفية إضافة مستندات إلى الفهرس
إضافة المستندات بسيطة—فقط وجه المكتبة إلى الدلائل التي تحتوي على ملفاتك. يمكنك إضافة مجلدات متعددة، وهو ما يكون مفيدًا عندما يكون مجموعة المستندات القانونية موزعة عبر مواقع مختلفة.

#### إنشاء وإدارة فهرس
**نظرة عامة:**  
إنشاء فهرس هو الخطوة الأولى نحو عمليات بحث مستندات فعّالة. يسمح لك GroupDocs.Search بإنشاء فهرس قابل للبحث في أي دليل تختاره، مما يتيح استرجاعًا سريعًا للمستندات.

##### الخطوة 1: إنشاء الفهرس
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*شرح:* `Index` يهيئ فهرس بحث في الدليل المحدد. تأكد من أن المسار يعكس بنية مجلدات مشروعك.

##### الخطوة 2: إضافة مستندات إلى الفهرس
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*شرح:* طريقة `Add` تفحص المجلد المحدد وتضم كل مستند مدعوم في الفهرس. استخدم ذلك **لإضافة مستندات إلى الفهرس** من مصادر متعددة، مثل العقود أو ملفات القضايا أو السجلات الطبية.

### استرجاع وعرض تقارير الفهرسة
**نظرة عامة:**  
تقارير الفهرسة تمنحك نظرة على عدد المستندات التي تمت معالجتها، إجمالي عدد المصطلحات، وحجم التخزين—وهي مقاييس أساسية لضبط الأداء.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*شرح:* `GetIndexingReports` تُرجع مصفوفة من التقارير التي تفصل عملية الفهرسة، مما يساعدك على مراقبة وتحسين الأداء.

## التطبيقات العملية
1. **إدارة المستندات القانونية:** أتمتة فهرسة ملفات القضايا لاسترجاع فوري للأنظمة، المذكرات، والأحكام.  
2. **نظام السجلات الطبية:** البحث في سجلات المرضى مع الحفاظ على الخصوصية باستخدام GroupDocs.Redaction لإخفاء معلومات PHI.  
3. **بوابة الموارد البشرية للشركة:** دمج ملفات الموظفين القابلة للبحث مع الممحاة لحماية البيانات الشخصية.

## اعتبارات الأداء
- **تحسين حجم الفهرس:** قم بانتظام بحذف الإدخالات القديمة وإعادة بناء الفهرس للحفاظ على خفته.  
- **إدارة الذاكرة:** استفد من جامع القمامة في .NET؛ حرّر كائنات `Index` عندما لا تكون بحاجة إليها.  
- **أفضل ممارسات القابلية للتوسع:** خزن الفهرس على تخزين SSD سريع وفكّ شظايا مجموعات البيانات الكبيرة عبر فهارس متعددة.

## الأسئلة المتكررة

**س: ما هي الاستخدامات الأساسية لـ GroupDocs.Search؟**  
ج: إنه مثالي لإنشاء فهارس قابلة للبحث من مجموعات مستندات ضخمة، مما يتيح استرجاعًا سريعًا للملفات القانونية والطبية.

**س: كيف يضمن GroupDocs.Redaction خصوصية البيانات؟**  
ج: يتيح لك تعريف أنماط الممحاة التي تزيل أو تخفي المعلومات الحساسة بشكل دائم قبل فهرسة المستند أو مشاركته.

**س: هل يمكنني استخدام هذه المكتبات في بيئة سحابية؟**  
ج: نعم—كلا المكتبتين تعملان في Azure أو AWS أو أي نشر .NET محوَّل بالحاويات مع الترخيص المناسب.

**س: ما صيغ الملفات التي يدعمها GroupDocs.Search؟**  
ج: PDFs، Word، Excel، PowerPoint، TXT، HTML، والعديد من صيغ المؤسسات الأخرى.

**س: كيف أقوم باستكشاف أخطاء الفهرسة؟**  
ج: تحقق من مسارات المجلدات، افحص أذونات الملفات، وراجع مخرجات وحدة التحكم من `IndexingReport` للحصول على رموز الأخطاء المحددة.

## الموارد
- **الوثائق:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **مرجع API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **تحميل:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **دعم مجاني:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**آخر تحديث:** 2026-04-04  
**تم الاختبار مع:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**المؤلف:** GroupDocs
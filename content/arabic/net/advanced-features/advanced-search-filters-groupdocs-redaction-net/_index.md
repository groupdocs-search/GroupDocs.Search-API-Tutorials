---
date: '2026-04-02'
description: تعلم كيفية التصفية حسب امتداد الملف والبحث فقط عن ملفات txt باستخدام
  GroupDocs.Redaction لـ .NET — عزّز كفاءة إدارة المستندات.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: تصفية حسب امتداد الملف في .NET باستخدام GroupDocs.Redaction
type: docs
url: /ar/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# تصفية حسب امتداد الملف في .NET باستخدام GroupDocs.Redaction

يمكن أن يكون البحث عبر مجموعة ضخمة من الملفات أمرًا مرهقًا، خاصة عندما تحتاج فقط إلى نتائج من أنواع ملفات محددة. في هذا البرنامج التعليمي ستكتشف **كيفية التصفية حسب امتداد الملف** باستخدام GroupDocs.Redaction لـ .NET، مما يتيح لك البحث فقط عن ملفات txt أو أي امتداد آخر تختاره. سنستعرض إعداد كل من الفلاتر القائمة على نوع الملف والمسار، حتى تتمكن من تحديد المستندات التي تحتاجها بسرعة.

## إجابات سريعة
- **ما الذي تفعله “filter by file extension”?** إنها تقصر البحث على المستندات التي تطابق امتداد ملف معين (مثال: *.txt).  
- **لماذا تستخدم GroupDocs.Redaction لهذا؟** إنها توفر واجهات برمجة تطبيقات (APIs) تصفية مدمجة سريعة وسهلة التكامل.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للاختبار؛ الترخيص المدفوع مطلوب للإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6+.  
- **هل يمكنني دمج فلاتر نوع الملف والمسار؟** نعم—يمكن تطبيق فلاتر متعددة للحصول على بحث دقيق للغاية.

## ما ستتعلمه
- كيفية **filter by file extension** بحيث يتم البحث فقط في ملفات النص.  
- كيفية إعداد **file path filters** لتضييق النتائج إلى مجلدات محددة أو أنماط تسمية.  
- نصائح للحفاظ على فهرسك سريعًا وفعّالًا في الذاكرة.

## المتطلبات المسبقة
قبل الغوص في التفاصيل، تأكد من أن لديك:
- **GroupDocs.Redaction Library** مثبتة ومتوافقة مع مشروع .NET الخاص بك.  
- بيئة تطوير مثل Visual Studio أو VS Code.  
- معرفة أساسية بـ C# وإلمام بهيكل مشروع .NET.

## إعداد GroupDocs.Redaction لـ .NET
أولاً، أضف المكتبة إلى مشروعك.

**استخدام .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**استخدام Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

أو ابحث عن “GroupDocs.Redaction” في واجهة NuGet Package Manager وقم بتثبيت أحدث نسخة.

### الحصول على الترخيص
يمكنك البدء بنسخة تجريبية مجانية أو طلب ترخيص مؤقت. للمشاريع طويلة الأجل، قم بشراء ترخيص من الموقع الرسمي.

### التهيئة الأساسية
بعد تثبيت الحزمة، أنشئ فهرسًا سيحمل مراجع مستنداتك:
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## دليل التنفيذ
### الميزة 1: إعداد فلتر للمستندات النصية (.txt)
#### كيفية التصفية حسب امتداد الملف للمستندات النصية
1. **تحديد الفهرس ومجلدات المستندات**  
   حدد المسارات التي توجد فيها ملفات المصدر الخاصة بك:
   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **إنشاء فهرس**  
   حمّل جميع الملفات من مجلد المصدر إلى الفهرس:
   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **تكوين خيارات البحث باستخدام فلتر امتداد الملف**  
   أخبر المحرك بأن يقتصر على ملفات *.txt فقط:
   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **تنفيذ البحث**  
   نفّذ استعلامًا؛ يضمن الفلتر تجاهل الملفات غير النصية:
   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *شرح*: طريقة `Search` تُعيد النتائج التي تلبي الفلتر، مما يقلل الضوضاء بشكل كبير ويحسن الأداء.

### الميزة 2: فلاتر مسار الملف
#### لماذا تستخدم فلاتر مسار الملف؟
أحيانًا تحتاج إلى تقييد البحث إلى مجلد قسم معين أو مجموعة من الملفات التي تشترك في نمط تسمية. فلاتر المسار تتيح لك القيام بذلك بالضبط.

1. **تحديد الفهرس ومجلدات المستندات**  
   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **إنشاء فهرس**  
   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **تكوين خيارات البحث باستخدام تعبير عادي قائم على المسار**  
   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   هذا التعبير العادي يطابق أي ملف يحتوي مساره الكامل على كلمة “Lorem”، مما يتيح لك استهداف مجلدات فرعية محددة.

4. **تنفيذ البحث القائم على المسار**  
   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## تطبيقات عملية
- **Legal Document Management** – حدد بسرعة العقود ذات الصلة المخزنة كملفات نصية عادية.  
- **Academic Research** – استخرج فقط ملاحظات البحث بصيغة *.txt التي تنتمي إلى مجلد مشروع معين.  
- **Corporate Reporting** – صَفِّ التقارير الداخلية حسب مسار القسم (مثال: `/Finance/2025/`).  

## اعتبارات الأداء
- قم بفهرسة فقط أنواع المستندات التي تحتاجها فعليًا؛ الملفات غير الضرورية تزيد من حجم الفهرس ووقت البحث.  
- احافظ على تحديث فهرسك باستخدام مهمة مجدولة تستدعي `index.Add()` للملفات الجديدة أو المعدلة.  
- استخدم تعبيرات عادية بسيطة؛ الأنماط المعقدة جدًا قد تبطئ محرك البحث.  
- تخلص من كائنات `Index` عندما لا تحتاجها بعد الآن لتوفير الذاكرة.

## الخلاصة
أنت الآن تعرف كيفية **filter by file extension** وتطبيق **file path filters** باستخدام GroupDocs.Redaction لـ .NET. تمنحك هذه التقنيات تحكمًا دقيقًا في مجموعات المستندات الكبيرة، مما يجعل عمليات البحث أسرع وأكثر صلة. بعد ذلك، جرب دمج فلاتر متعددة أو دمج البحث في سير عمل تطبيق أكبر.

## قسم الأسئلة المتكررة
**س1: هل يمكنني تصفية مستندات غير ملفات النص؟**  
A1: نعم، يدعم GroupDocs.Redaction العديد من الصيغ. غيّر الوسيط في `CreateFileExtension` إلى الامتداد المطلوب (مثال: ".pdf").

**س2: كيف أقوم بتحديث فهرس البحث بانتظام؟**  
A2: جدولة خدمة خلفية أو مهمة cron تقوم بتشغيل `index.Add()` على الأدلة التي تريد إبقاؤها محدثة.

**س3: هل هناك تأثير على الأداء عند التصفية حسب مسار الملف؟**  
A3: التعبيرات العادية المُحسّنة بشكل صحيح لها تأثير ضئيل، لكن يجب دائمًا قياس الأداء باستخدام مجموعة البيانات الخاصة بك.

**س4: هل يمكنني دمج فلاتر متعددة للحصول على بحث أكثر دقة؟**  
A4: بالتأكيد. يمكنك ربط الفلاتر أو إنشاء فلاتر مركبة لاستهداف كل من نوع الملف والمسار في آن واحد.

**س5: أين يمكنني العثور على المزيد من الموارد حول GroupDocs.Redaction؟**  
A5: زر الوثائق الرسمية على [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) للحصول على أدلة مفصلة ومراجع API.

## الأسئلة المتكررة
**س: هل يعمل `SearchDocumentFilter` مع الملفات المشفرة؟**  
A: الفلتر نفسه يعمل على بيانات تعريف الملف، لذا لا تزال الملفات المشفرة تُفهرس إذا قمت بتوفير بيانات الاعتماد اللازمة لفك التشفير أثناء الفهرسة.

**س: هل يمكنني استخدام أحرف البدل بدلاً من تعبير عادي لتصفية المسار؟**  
A: يتطلب API حاليًا تعبيرًا عاديًا، ولكن يمكنك محاكاة أحرف بدل بسيطة (مثال: `.*` لأي أحرف).

**س: ما هو الحد الأقصى لحجم الفهرس قبل الحاجة إلى تقسيمه؟**  
A: قد تستفيد الفهارس التي يبلغ حجمها عدة مئات من الجيجابايت من تقسيمها إلى فهارس منطقية متعددة؛ اختبر الأداء مع نمو مجموعتك.

**س: هل هناك طرق مدمجة لإزالة المستندات من الفهرس؟**  
A: نعم—استدعِ `index.Delete(documentId)` أو `index.DeleteAll()` لإدارة الإدخالات القديمة.

**س: هل هناك طريقة لمعاينة نتائج البحث قبل تحميل المستند بالكامل؟**  
A: كائن `SearchResult` يتضمن معلومات مقتطف يمكنك عرضها في واجهة المستخدم دون فتح الملف بالكامل.

## الموارد
- **الوثائق**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)  
- **مرجع API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **تحميل**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)  
- **دعم مجاني**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2026-04-02  
**تم الاختبار مع:** GroupDocs.Redaction 23.12 لـ .NET  
**المؤلف:** GroupDocs
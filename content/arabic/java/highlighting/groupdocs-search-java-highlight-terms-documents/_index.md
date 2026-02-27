---
date: '2026-02-27'
description: تعلم كيفية تمييز النص في جافا باستخدام GroupDocs.Search for Java، مع
  تغطية البحث في المستندات بجافا، فهرسة المستندات بجافا، وتحديد القطع المميزة.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: تمييز النص في جافا باستخدام GroupDocs.Search
type: docs
url: /ar/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# تمييز النص Java باستخدام GroupDocs.Search

في بيئة الرقمية السريعة اليوم، القدرة على **تمييز النص java** عبر مجموعات كبيرة من الملفات تُعد ميزة أساسية. سواءً كنت تبني منصة مراجعة قانونية، أو محرك بحث أكاديمي، أو وحدة دعم عملاء، فإن اكتشاف المصطلحات التي يبحث عنها المستخدمون فورًا يجعل التجربة أكثر كفاءة. يوضح هذا الدليل كيفية استخدام **GroupDocs.Search for Java** للـ **search documents java**، و **index documents java**، وتطبيق تمييز غني—لكل من المستندات الكاملة والقطع المقتطفة.

## إجابات سريعة
- **ماذا يعني “search and highlight text”؟** يشير إلى تحديد مصطلحات الاستعلام داخل مستند وتأكيدها بصريًا (مثلاً، بلون خلفية).  
- **أي مكتبة توفر هذه القدرة؟** GroupDocs.Search for Java.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتقييم؛ يتطلب الترخيص الكامل للإنتاج.  
- **هل يمكنني تخصيص ألوان التمييز؟** نعم—يمكن ضبط أي لون RGB عبر `HighlightOptions`.  
- **هل يدعم تمييز القطع المقتطفة؟** بالتأكيد؛ يمكنك تحديد عدد الكلمات قبل/بعد التطابق لإنشاء مقتطفات مختصرة.

## كيفية تمييز النص Java في المستندات
يتضمن تمييز النص Java ثلاث خطوات أساسية:

1. **فهرسة ملفات المصدر** حتى يمكن البحث فيها بسرعة.  
2. **تشغيل استعلام** على الفهرس للعثور على المستندات المطابقة.  
3. **عرض النتائج مع إشارات بصرية** باستخدام واجهة برمجة تطبيقات الـ highlighter.

أدناه نستعرض كل خطوة بالتفصيل، أولاً لإخراج المستند بالكامل ثم لمستوى القطع المقتطفة.

## ما هو Search and Highlight Text؟
Search and highlight text هو عملية مسح فهرس المستندات لاستعلام معين، استرجاع المستندات المطابقة، ثم وضع علامة على كل ظهور لمصطلح الاستعلام داخل مخرجات المستند (HTML، PDF، إلخ). تساعد هذه الإشارة البصرية المستخدمين النهائيين على اكتشاف المعلومات ذات الصلة فورًا.

## لماذا نستخدم GroupDocs.Search for Java؟
- **فهرسة عالية الأداء** مع ضغط قابل للتكوين (`index documents java`).  
- **واجهة برمجة تطبيقات تمييز غنية** تعمل على المستندات الكاملة وعلى القطع المخصصة (`highlight search terms java`).  
- **دعم صيغ متعددة** (DOCX، PDF، PPTX، TXT، وأكثر).  
- **تكامل Maven بسيط** وتصميم موجه للـ Java.

## المتطلبات المسبقة
- مجموعة تطوير Java (JDK) 8 أو أحدث.  
- Maven لإدارة الاعتمادات.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse.  
- إلمام أساسي بصياغة Java.

## إعداد GroupDocs.Search for Java

أضف مستودع GroupDocs والاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

يمكنك أيضًا تنزيل أحدث JAR مباشرة من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
ابدأ بنسخة تجريبية مجانية أو احصل على ترخيص مؤقت للتقييم. بالنسبة للنشر في بيئة الإنتاج، اشترِ ترخيصًا كاملاً لفتح جميع الميزات.

## دليل التنفيذ

يتم تقسيم التنفيذ إلى قسمين عمليين: **التمييز في المستندات الكاملة** و**التمييز في القطع المقتطفة**. يحتوي كل قسم على الخطوات الأساسية لـ **how to highlight Java** المستندات باستخدام GroupDocs.Search.

### تكوين إعدادات الفهرس
قبل الفهرسة، قم بتكوين التخزين لاستخدام ضغط عالي—هذا يقلل من استهلاك القرص مع الحفاظ على سرعة البحث.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### التمييز في المستندات الكاملة

#### الخطوة 1: إنشاء الفهرس وتعبئته
أنشئ مجلد فهرس وأضف جميع ملفات المصدر التي تريد البحث فيها.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### الخطوة 2: تنفيذ البحث وتطبيق التمييز
ابحث عن المصطلح (مثلاً `ipsum`) وأنشئ ملف HTML يحتوي على التطابقات المميزة.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**شرح الخيارات الأساسية**  
- **Compression** – الضغط العالي يوفر مساحة التخزين.  
- **HighlightColor** – اضبط أي قيمة RGB لتتناسب مع لوحة ألوان واجهتك.  
- **UseInlineStyles** – `false` يولد HTML نظيف يمكن تنسيقه عالميًا باستخدام CSS.  

### التمييز في القطع المقتطفة

#### الخطوة 1: الفهرسة والبحث (نفس الخطوات أعلاه)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### الخطوة 2: تعريف سياق القطعة والتمييز
حدد عدد المصطلحات قبل وبعد التطابق التي يجب ظهورها في كل قطعة.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### الخطوة 3: استرجاع وكتابة القطع المميزة
اجمع القطع المولدة واكتبها إلى ملف HTML.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## تطبيقات عملية
1. **مراجعة المستندات القانونية** – تمييز القوانين، البنود، أو مراجع القضايا فورًا.  
2. **البحث الأكاديمي** – استخراج المصطلحات الرئيسية عبر عشرات ملفات PDF وWord.  
3. **دعم العملاء** – تحديد أرقام الطلبات أو رموز الأخطاء داخل سجلات التذاكر.

## اعتبارات الأداء
- **حجم الفهرس** – الضغط العالي (`Compression.High`) يقلل من البصمة على القرص.  
- **سياق القطعة** – القيم الأكبر لـ `termsBefore/After` تزيد الدقة لكن قد تؤثر على السرعة.  
- **إدارة الذاكرة** – راقب مساحة heap في JVM عند فهرسة مجموعات ضخمة؛ فكر في الفهرسة التدريجية للمجموعات الكبيرة جدًا.

## المشكلات الشائعة والحلول
- **أخطاء الفهرسة** – تحقق من مسارات الملفات وتأكد من أن التطبيق يملك صلاحيات القراءة/الكتابة.  
- **عدم ظهور التمييز** – تأكد من أن `UseInlineStyles` يتطابق مع صيغة المخرجات (HTML مقابل PDF).  
- **عدم تطبيق اللون** – تأكد من أن قيم RGB ضمن النطاق 0‑255 وأن عارض HTML يدعم النمط.

## الأسئلة المتكررة

**س: ما هي فوائد استخدام GroupDocs.Search for Java؟**  
ج: يوفر فهرسة سريعة وقابلة للتوسع، تمييز قابل للتخصيص، ودعم للعديد من صيغ المستندات.

**س: كيف يمكنني دمج GroupDocs.Search مع واجهة REST API؟**  
ج: عرّض طرق البحث والتمييز عبر متحكمات Spring Boot، مع إرجاع HTML أو JSON.

**س: هل تتعامل المكتبة مع الملفات المحمية بكلمة مرور؟**  
ج: نعم—قم بتمرير كلمة المرور عند إضافة المستند إلى الفهرس.

**س: هل يمكنني تخصيص وسوم التمييز إلى ما هو أبعد عن اللون؟**  
ج: بالتأكيد؛ يمكنك حقن فئات CSS عبر `HighlightOptions` أو تعديل HTML بعد الإنشاء.

**س: أي نسخة تم اختبارها لهذا الدليل؟**  
ج: تم التحقق من الكود مع GroupDocs.Search 25.4.

**س: كيف أُعيّن highlight options java لاستخدام فئة CSS بدلاً من الأنماط المضمنة؟**  
ج: اضبط `options.setUseInlineStyles(false)` وأضف قاعدة CSS للفئة التي تحددها عبر `options.setCssClass("myHighlight")`.

**س: هل هناك طريقة لتحديد terms pdf java مباشرة عندما يكون المصدر PDF؟**  
ج: نعم—GroupDocs.Search يعمل مع مدخلات PDF، والتمييز سيُنتج HTML يمكنك دمجه في عارض PDF أو تحويله مرة أخرى إلى PDF باستخدام GroupDocs.Conversion.

---

**آخر تحديث:** 2026-02-27  
**تم الاختبار مع:** GroupDocs.Search 25.4  
**المؤلف:** GroupDocs
---
date: '2025-12-26'
description: تعرّف على كيفية البحث وتحديد النص في المستندات باستخدام GroupDocs.Search
  للـ Java. استكشف تقنيات تمييز المستند بالكامل والجزء.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: البحث وتحديد النص باستخدام GroupDocs.Search لجافا
type: docs
url: /ar/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# البحث وتحديد النص في المستندات باستخدام GroupDocs.Search للغة Java

في العصر الرقمي اليوم، **البحث وتحديد النص** عبر مجموعات ضخمة من المستندات هو مطلب شائع. سواءً كنت تبني أداة مراجعة قانونية، أو بوابة بحث أكاديمي، أو لوحة تحكم لدعم العملاء، فإن القدرة على تحديد المواقع الفورية للمصطلحات الرئيسية وتأكيدها تحسن بشكل كبير من قابلية الاستخدام. في هذا الدليل الشامل، ستكتشف كيفية تنفيذ **البحث وتحديد النص** باستخدام GroupDocs.Search للغة Java—مغطياً كل من التحديد على مستوى المستند الكامل وتحديد على مستوى القطع للحصول على سياق مركّز.

## إجابات سريعة
- **ماذا يعني “البحث وتحديد النص”؟** يشير إلى العثور على مصطلحات الاستعلام في المستند وتأكيدها بصريًا (مثلاً، باستخدام لون خلفية).  
- **أي مكتبة توفر هذه القدرة؟** GroupDocs.Search للغة Java.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني تخصيص ألوان التحديد؟** نعم—يمكن ضبط أي لون RGB عبر `HighlightOptions`.  
- **هل يدعم التحديد على مستوى القطع؟** بالتأكيد؛ يمكنك تحديد المصطلحات قبل/بعد التطابق لإنشاء مقتطفات مختصرة.

## ما هو البحث وتحديد النص؟
البحث وتحديد النص هو عملية فحص فهرس المستندات لاستعلام معين، استرجاع المستندات المطابقة، ثم وضع علامة على كل ظهور لمصطلح الاستعلام داخل ناتج المستند (HTML، PDF، إلخ). هذه الإشارة البصرية تساعد المستخدمين النهائيين على spotting المعلومات ذات الصلة فورًا.

## لماذا نستخدم GroupDocs.Search للغة Java؟
- **فهرسة عالية الأداء** مع ضغط قابل للتكوين.  
- **واجهة برمجة تطبيقات غنية للتحديد** تعمل على المستندات الكاملة وعلى القطع المخصصة.  
- **دعم صيغ متعددة** (DOCX، PDF، PPTX، TXT، وأكثر).  
- **تكامل سهل مع Maven** وواجهة برمجة تطبيقات واضحة موجهة للـ Java.

## المتطلبات المسبقة
- مجموعة تطوير جافا (JDK) 8 أو أحدث.  
- Maven لإدارة الاعتمادات.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse.  
- إلمام أساسي بصياغة جافا.

## إعداد GroupDocs.Search للغة Java

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

يمكنك أيضًا تنزيل أحدث ملف JAR مباشرة من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
ابدأ بنسخة تجريبية مجانية أو احصل على ترخيص مؤقت للتقييم. بالنسبة للنشر في بيئة الإنتاج، اشترِ ترخيصًا كاملاً لفتح جميع الميزات.

## دليل التنفيذ

يتم تقسيم التنفيذ إلى قسمين عمليين: **التحديد في المستندات الكاملة** و**التحديد في القطع**. كلا القسمين يتضمنان الخطوات الأساسية **لكيفية تحديد مستندات Java** باستخدام GroupDocs.Search.

### تكوين إعدادات الفهرس
قبل الفهرسة، قم بتكوين التخزين لاستخدام ضغط عالي—هذا يقلل من استهلاك القرص مع الحفاظ على سرعة البحث.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### التحديد في المستندات الكاملة

#### الخطوة 1: إنشاء الفهرس وتعبئته
أنشئ مجلد فهرس وأضف جميع الملفات المصدرية التي تريد البحث فيها.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### الخطوة 2: تنفيذ البحث وتطبيق التحديد
ابحث عن المصطلح (مثلاً `ipsum`) وولّد ملف HTML يحتوي على التطابقات المحددة.

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

**شرح الخيارات الرئيسية**
- **Compression** – الضغط العالي يوفر مساحة التخزين.  
- **HighlightColor** – اضبط أي قيمة RGB لتتناسب مع لوحة ألوان واجهتك.  
- **UseInlineStyles** – `false` يولّد HTML نظيف يمكن تنسيقه عالميًا باستخدام CSS.

### التحديد في القطع

#### الخطوة 1: الفهرسة والبحث (نفس الخطوات السابقة)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### الخطوة 2: تعريف سياق القطعة وتحديده
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

#### الخطوة 3: استرجاع وكتابة القطع المحددة
اجمع القطع التي تم توليدها واكتبها إلى ملف HTML.

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
1. **مراجعة المستندات القانونية** – تحديد القوانين، الفقرات، أو المراجع القضائية فورًا.  
2. **البحث الأكاديمي** – استخراج المصطلحات الرئيسية عبر عشرات ملفات PDF وWord.  
3. **دعم العملاء** – تحديد أرقام الطلبات أو رموز الأخطاء داخل سجلات التذاكر.

## اعتبارات الأداء
- **حجم الفهرس** – الضغط العالي (`Compression.High`) يقلل من البصمة على القرص.  
- **سياق القطعة** – القيم الأكبر لـ `termsBefore/After` تزيد الدقة لكن قد تؤثر على السرعة.  
- **إدارة الذاكرة** – راقب مساحة heap في JVM عند فهرسة مجموعات كبيرة؛ فكر في الفهرسة المتزايدة للمجموعات الضخمة جدًا.

## المشكلات الشائعة والحلول
- **أخطاء الفهرسة** – تحقق من مسارات الملفات وتأكد من أن التطبيق يمتلك صلاحيات القراءة/الكتابة.  
- **عدم ظهور التحديدات** – تأكد من أن `UseInlineStyles` يتوافق مع صيغة الإخراج (HTML مقابل PDF).  
- **عدم تطبيق اللون** – تأكد من أن قيم RGB ضمن النطاق 0‑255 وأن عارض HTML يدعم النمط.

## الأسئلة المتكررة

**س: ما هي فوائد استخدام GroupDocs.Search للغة Java؟**  
ج: يوفر فهرسة سريعة وقابلة للتوسع، وتحديد قابل للتخصيص، ودعم للعديد من صيغ المستندات.

**س: كيف يمكنني دمج GroupDocs.Search مع واجهة برمجة تطبيقات REST؟**  
ج: قم بتعريض طرق البحث والتحديد عبر وحدات تحكم Spring Boot، مع إرجاع HTML أو حمولة JSON.

**س: هل تتعامل المكتبة مع الملفات المحمية بكلمة مرور؟**  
ج: نعم—قم بتمرير كلمة المرور عند إضافة المستند إلى الفهرس.

**س: هل يمكنني تخصيص علامة التحديد بخلاف اللون؟**  
ج: بالتأكيد؛ يمكنك حقن فئات CSS عبر `HighlightOptions` أو تعديل HTML بعد الإنشاء.

**س: أي نسخة تم اختبارها لهذا الدليل؟**  
ج: تم التحقق من الكود مع GroupDocs.Search 25.4.

---

**آخر تحديث:** 2025-12-26  
**تم الاختبار مع:** GroupDocs.Search 25.4  
**المؤلف:** GroupDocs
---
date: '2026-02-24'
description: تعلم كيفية إنشاء مسجل مخصص، وتحديد الحد الأقصى لحجم السجل، وتكوين مسجل
  وحدة التحكم أو ملف السجل في GroupDocs.Search للغة Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: كيفية إنشاء مسجل مخصص وتحديد حجم ملف السجل باستخدام GroupDocs.Search Java
type: docs
url: /ar/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

 okay.

Let's produce final content.

We'll translate each bullet.

Make sure to keep bold markers.

Let's start.

I'll write Arabic translation.

Be careful with punctuation.

Proceed.

# تحديد حجم ملف السجل باستخدام مسجلات GroupDocs.Search Java

في هذا الدليل ستقوم **بإنشاء تطبيقات مسجل مخصصة** وتتعلم كيفية **تحديد حجم ملف السجل** أثناء استخدام GroupDocs.Search للغة Java. التحكم في نمو السجلات أمر حاسم لفهرسة المستندات على نطاق واسع، وتتيح لك المسجلات المدمجة **تحديد الحد الأقصى لحجم السجل**، **تدوير ملف السجل**، أو التحول إلى **استخدام مسجل وحدة التحكم** للحصول على ملاحظات فورية. دعنا نستعرض الإعداد الكامل، من تكوين Maven إلى تشغيل استعلام بحث، ونرى كيف **نضيف مستندات إلى الفهرس** مع وجود المسجل.

## إجابات سريعة
- **ماذا يعني “تحديد حجم ملف السجل”؟** يحدد الحد الأقصى لحجم ملف السجل، مما يمنع النمو غير المتحكم فيه على القرص.  
- **أي مسجل يتيح لك تحديد حجم ملف السجل؟** المسجل المدمج `FileLogger` يقبل معامل الحد الأقصى للحجم.  
- **كيف أستخدم مسجل وحدة التحكم في Java؟** أنشئ كائنًا من `ConsoleLogger` وضعه في `IndexSettings`.  
- **هل أحتاج إلى ترخيص لـ GroupDocs.Search؟** النسخة التجريبية تكفي للتقييم؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما هي الخطوة الأولى؟** أضف تبعية GroupDocs.Search إلى مشروع Maven الخاص بك.  

## ما هو تحديد حجم ملف السجل؟
تحديد حجم ملف السجل يعني تكوين المسجل بحيث عندما يصل الملف إلى عتبة محددة مسبقًا (مثلاً 4 ميغابايت)، يتوقف عن النمو أو يتم تدويره. هذا يحافظ على بُعد التخزين لتطبيقك متوقعًا ويتجنب تدهور الأداء.

## لماذا نستخدم مسجلات الملفات والمسجلات المخصصة مع GroupDocs.Search؟
- **قابلية التدقيق:** الاحتفاظ بسجل دائم لأحداث الفهرسة والبحث.  
- **التصحيح:** تحديد المشكلات بسرعة من خلال مراجعة سجلات مختصرة.  
- **المرونة:** الاختيار بين سجلات ملفات مستمرة وإخراج فوري إلى وحدة التحكم (`use console logger`).  

## المتطلبات المسبقة
- **GroupDocs.Search للغة Java** ≥ 25.4.  
- JDK 8 أو أحدث، بيئة تطوير (IntelliJ IDEA، Eclipse، إلخ).  
- معرفة أساسية بـ Java و Maven.  

## إعداد GroupDocs.Search للغة Java

أضف المكتبة إلى مشروعك باستخدام إحدى الطرق أدناه.

**إعداد Maven:**

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

**تحميل مباشر:**  
حمّل أحدث ملف JAR من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
احصل على نسخة تجريبية أو اشترِ ترخيصًا عبر [صفحة الترخيص](https://purchase.groupdocs.com/temporary-license/).

## كيفية إنشاء مسجل مخصص لـ GroupDocs.Search
يتيح لك GroupDocs.Search توصيل أي تنفيذ لواجهة `ILogger`. من خلال توسيع `FileLogger` أو `ConsoleLogger`، يمكنك إضافة سلوك إضافي—مثل تدوير ملف السجل أو توجيه الرسائل إلى خدمة مراقبة عن بُعد. هذه المرونة هي السبب في أن العديد من الفرق **تنشئ مسجلات مخصصة** تتناسب مع احتياجاتها التشغيلية.

## كيفية تحديد حجم ملف السجل باستخدام File Logger
فيما يلي دليل خطوة بخطوة يوضح كيفية **تكوين مسجل الملف** بحيث لا يتجاوز حجم الملف المحدد.

### 1️⃣ استيراد الحزم الضرورية
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ إعداد إعدادات الفهرس مع File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ إنشاء أو تحميل الفهرس
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ إضافة مستندات إلى الفهرس
```java
index.add(documentsFolder);
```

### 5️⃣ تنفيذ استعلام بحث
```java
SearchResult result = index.search(query);
```

**نقطة أساسية:** المعامل الثاني (`4.0`) في مُنشئ `FileLogger` يحدد **الحد الأقصى لحجم السجل** بالميغابايت، مما يلبي متطلب **تحديد حجم ملف السجل**.

## كيفية استخدام مسجل وحدة التحكم في Java
إذا كنت تفضّل الحصول على ملاحظات فورية في الطرفية، استبدل مسجل الملف بمسجل وحدة التحكم.

### 1️⃣ استيراد مسجل وحدة التحكم
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ إعداد إعدادات الفهرس مع مسجل وحدة التحكم
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ إنشاء أو تحميل الفهرس
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ إضافة مستندات وتنفيذ بحث
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**نصيحة:** مسجل وحدة التحكم مثالي أثناء التطوير لأنه يطبع كل سجل فورًا، مما يساعدك على التحقق من سلوك الفهرسة والبحث كما هو متوقع.

## تطبيقات عملية
1. **أنظمة إدارة المستندات:** الحفاظ على سجلات تدقيق لكل مستند يتم فهرسته.  
2. **محركات البحث المؤسسية:** مراقبة أداء الاستعلامات ومعدلات الأخطاء في الوقت الحقيقي.  
3. **البرمجيات القانونية والامتثال:** تسجيل مصطلحات البحث للتقارير التنظيمية.

## اعتبارات الأداء
- **حجم السجل:** من خلال **تحديد الحد الأقصى لحجم السجل**، تتجنب استهلاك مساحة قرص مفرط قد يبطئ تطبيقك.  
- **التسجيل غير المتزامن:** إذا كنت تحتاج إلى معدل نقل أعلى، فكر في تغليف المسجل في طابور غير متزامن (خارج نطاق هذا الدليل).  
- **إدارة الذاكرة:** حرّر كائنات `Index` الكبيرة عندما لا تحتاجها لتقليل البصمة الذاكرية لـ JVM.

## المشكلات الشائعة والحلول
- **مسار السجل غير قابل للوصول:** تحقق من وجود الدليل ومن أن التطبيق يملك صلاحيات الكتابة.  
- **المسجل لا يعمل:** تأكد من استدعاء `settings.setLogger(...)` *قبل* إنشاء كائن `Index`.  
- **غياب مخرجات وحدة التحكم:** تأكد من تشغيل التطبيق في طرفية تُظهر `System.out`.

## الأسئلة المتكررة

**س: ماذا يتحكم فيه المعامل الثاني لـ `FileLogger`؟**  
ج: يحدد الحد الأقصى لحجم ملف السجل بالميغابايت، مما يتيح لك **تحديد الحد الأقصى لحجم السجل**.

**س: هل يمكنني دمج مسجلات الملف ووحدة التحكم؟**  
ج: نعم، بإنشاء مسجل مخصص يرسل الرسائل إلى الوجهتين.

**س: كيف أضيف مستندات إلى الفهرس بعد الإنشاء الأولي؟**  
ج: استدعِ `index.add(pathToNewDocs)` في أي وقت؛ سيقوم المسجل بتسجيل العملية.

**س: هل `ConsoleLogger` آمن للاستخدام في بيئات متعددة الخيوط؟**  
ج: يكتب مباشرة إلى `System.out`، الذي يتم مزامنته بواسطة JVM، مما يجعله آمنًا لمعظم الحالات.

**س: هل سيؤثر تحديد حجم ملف السجل على كمية المعلومات المخزنة؟**  
ج: عند الوصول إلى حد الحجم، قد تُهمل الإدخالات الجديدة أو يتم **تدوير ملف السجل**، حسب تنفيذ المسجل.

## موارد
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**آخر تحديث:** 2026-02-24  
**تم الاختبار مع:** GroupDocs.Search للغة Java 25.4  
**المؤلف:** GroupDocs
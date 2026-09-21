---
date: '2026-09-21'
description: تعلم كيفية إنشاء logger، وتعيين الحد الأقصى لحجم السجل، واستخدام console
  logger في GroupDocs.Search لـ Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: تعلم كيفية إنشاء logger، وتعيين الحد الأقصى لحجم السجل، واستخدام console
  logger في GroupDocs.Search لـ Java. اتبع تعليمات خطوة بخطوة ونصائح أفضل الممارسات.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: كيفية إنشاء logger وتحديد الحد الأقصى لحجم السجل في GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: كيفية إنشاء logger وتحديد الحد الأقصى لحجم السجل في GroupDocs.Search لـ Java
type: docs
url: /ar/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# كيفية إنشاء مسجل وتحديد حجم ملف السجل في GroupDocs.Search للـ Java

في هذا البرنامج التعليمي ستتعلم **كيفية إنشاء مسجل** لتطبيقات GroupDocs.Search، وتكوين الحد الأقصى لحجم ملف السجل، والتبديل بين التسجيل المستند إلى الملفات وتسجيل وحدة التحكم. إدارة السجلات بشكل صحيح تمنع امتلاء الأقراص أثناء مهام الفهرسة الكبيرة، وتحسن استكشاف الأخطاء، وتوفر لك ملاحظات فورية أثناء التطوير. سنبدأ بإعداد Maven، ثم نتناول تكوين المسجل، وننتهي باستعلام بحث بسيط يوضح عمل المسجل.

## إجابات سريعة
- **ماذا يعني “limit log file size”؟** يحد من الحجم الأقصى لملف السجل، مما يمنع النمو غير المتحكم فيه على القرص.  
- **أي مسجل يتيح لك تحديد حجم ملف السجل؟** `FileLogger` المدمج يقبل معامل الحد الأقصى للحجم.  
- **كيف أستخدم console logger java؟** أنشئ كائنًا من `ConsoleLogger` وضعه في `IndexSettings`.  
- **هل أحتاج إلى ترخيص لـ GroupDocs.Search؟** النسخة التجريبية تكفي للتقييم؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما هي الخطوة الأولى؟** أضف تبعية GroupDocs.Search إلى مشروع Maven الخاص بك.  

## ما هو حد حجم ملف السجل؟
إعداد **limit log file size** يخبر المسجل بالتوقف عن كتابة إدخالات جديدة بمجرد أن يصل الملف إلى العتبة المحددة (مثلاً 4 ميغابايت). عندما يتم الوصول إلى الحد، إما أن يتجاهل المسجل الرسائل الإضافية أو ينتقل إلى ملف جديد، مما يحافظ على استهلاك predictable للقرص.

## لماذا تستخدم سجلات الملفات والسجلات المخصصة مع GroupDocs.Search؟
توفر سجلات الملفات والسجلات المخصصة إمكانية التدقيق، ورؤية أعمق للأخطاء، ومرونة أكبر. في بيئات الإنتاج، توفر سجلات الملفات سجلًا دائمًا لكل عملية فهرسة وبحث، بينما تقدم سجلات وحدة التحكم ملاحظات فورية أثناء التطوير. تساعد هذه السجلات الفرق على مراقبة الأداء، وتتبع الأخطاء، وتلبية متطلبات الامتثال من خلال الحفاظ على مسار نشاط مفصل.

## المتطلبات المسبقة
- GroupDocs.Search للـ Java ≥ 25.4.  
- JDK 8 أو أحدث، مع بيئة تطوير مثل IntelliJ IDEA أو Eclipse.  
- إلمام أساسي بـ Maven وبرمجة Java.  

## إعداد GroupDocs.Search للـ Java

أضف المكتبة إلى مشروعك باستخدام إحدى الطرق أدناه.

**إعداد Maven:**  

```text
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
```

**تحميل مباشر:**  
قم بتنزيل أحدث JAR من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
احصل على نسخة تجريبية أو اشترِ ترخيصًا عبر [licensing page](https://purchase.groupdocs.com/temporary-license/).

## كيفية إنشاء مسجل مخصص لـ GroupDocs.Search
إنشاء مسجل مخصص أمر بسيط لأن GroupDocs.Search يعتمد على واجهة `ILogger`. من خلال تنفيذ هذه الواجهة — أو توسيع `FileLogger` أو `ConsoleLogger` المتوفرين — يمكنك حقن سلوك إضافي مثل التحويل عن بُعد أو تدوير السجلات. يمكنك أيضًا إضافة منطق تهيئة، مثل فتح اتصالات شبكية، وضمان إغلاق الموارد في طريقة إغلاق المسجل. يتيح لك هذا النهج التكامل مع منصات المراقبة مثل ELK أو Splunk.

### مرساة التعريف
`ILogger` هو عقد التسجيل الأساسي في GroupDocs.Search؛ أي فئة تنفذ طريقة `log(Level, String)` يمكنها أن تصبح مسجلاً.

### نهج مثال (بدون كتلة شفرة)
1. أنشئ فئة تنفذ `ILogger`.  
2. قم بتجاوز طريقة `log` لكتابة الرسائل إلى الوجهة المختارة (ملف، قاعدة بيانات، نقطة نهاية HTTP).  
3. في تكوين الفهرس، استدعِ `settings.setLogger(new YourCustomLogger())`.  

## كيفية تحديد حجم ملف السجل باستخدام File Logger
تكتب فئة `FileLogger` إدخالات السجل إلى ملف على القرص وتقبل معامل الحد الأقصى للحجم. من خلال تحديد حد الحجم، يتوقف المسجل تلقائيًا عن إضافة إدخالات جديدة أو ينشئ ملفًا جديدًا عندما يتم الوصول إلى العتبة، مما يمنع النمو غير المتحكم فيه للقرص. يضمن هذا السلوك أن التسجيل لا يتداخل مع أداء الفهرسة مع الحفاظ على سجل مختصر للأحداث.

### مرساة التعريف
`FileLogger` هو مسجل مدمج يحفظ الرسائل في ملف نصي ويدعم حجم ملف أقصى قابل للتكوين.

### دليل خطوة بخطوة
1️⃣ **استيراد الحزم اللازمة**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **إعداد إعدادات الفهرس مع File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **إنشاء أو تحميل الفهرس**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **إضافة مستندات إلى الفهرس**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **تنفيذ استعلام بحث**  
```text
```java
SearchResult result = index.search(query);
```
```

**نقطة رئيسية:** يحدد المعامل الثاني (`4.0`) في مُنشئ `FileLogger` **set max log size** بالميغابايت، مما يلبي مباشرةً متطلب **limit log file size**.

## كيفية استخدام console logger java
عندما تحتاج إلى رؤية فورية لأحداث السجل، يكتب `ConsoleLogger` كل رسالة إلى `System.out`. هذا المسجل خفيف الوزن وآمن للخطوط المتعددة، مما يجعله مناسبًا لجلسات التطوير وتصحيح الأخطاء. يوفر ملاحظات فورية حول تقدم الفهرسة، واستعلامات البحث، وحالات الخطأ دون الحاجة إلى عمليات I/O على الملفات، مما قد يسرّع الاختبار المتكرر.

### مرساة التعريف
`ConsoleLogger` هو مسجل خفيف الوزن يخرج إدخالات السجل إلى تدفق وحدة التحكم القياسي، مما يجعله مثاليًا لجلسات التصحيح.

### خطوات التكوين
1️⃣ **استيراد مسجل وحدة التحكم**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **إعداد إعدادات الفهرس مع Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **إنشاء أو تحميل الفهرس**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **إضافة مستندات وتنفيذ بحث**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**نصيحة:** مسجل وحدة التحكم مثالي أثناء التطوير لأنه يطبع كل إدخال سجل فورًا، مما يساعدك على التحقق من أن الفهرسة والبحث يعملان كما هو متوقع.

## التطبيقات العملية
1. **أنظمة إدارة المستندات:** الحفاظ على سجلات تدقيق لكل مستند يتم فهرسته، لتلبية متطلبات الامتثال.  
2. **محركات البحث المؤسسية:** مراقبة أداء الاستعلام ومعدلات الأخطاء في الوقت الفعلي، مما يتيح فحص سريع للاتفاقيات مستوى الخدمة.  
3. **البرمجيات القانونية والامتثال:** تسجيل مصطلحات البحث والطوابع الزمنية للتقارير التنظيمية، مع الاحتفاظ بالسجلات للفترة المطلوبة.

## اعتبارات الأداء
- **حجم السجل:** من خلال **set max log size**، تتجنب استهلاكًا مفرطًا للقرص قد يبطئ جامع القمامة في JVM.  
- **التسجيل غير المتزامن:** في سيناريوهات عالية الإنتاجية، يمكنك تغليف المسجل في طابور غير متزامن لفصل I/O عن خيط الفهرسة (التنفيذ خارج نطاق هذا الدليل).  
- **إدارة الذاكرة:** حرّر كائنات `Index` الكبيرة باستخدام `index.close()` عندما لا تحتاجها لتقليل البصمة الذاكرية لـ JVM.

## المشكلات الشائعة والحلول
- **مسار السجل غير قابل للوصول:** تحقق من وجود الدليل ومن أن التطبيق يمتلك أذونات كتابة للمستخدم الذي يشغل JVM.  
- **المسجل لا يعمل:** تأكد من استدعاء `settings.setLogger(...)` *قبل* إنشاء كائن `Index`؛ وإلا سيُستخدم المسجل الافتراضي.  
- **عدم ظهور مخرجات وحدة التحكم:** تأكد من تشغيل التطبيق في طرفية تعرض `System.out`، وأنه لا يوجد إطار تسجيل (مثل SLF4J) يعترض الإخراج.

## الأسئلة المتكررة

**س: ماذا يتحكم المعامل الثاني لـ `FileLogger`؟**  
ج: يحدد الحد الأقصى لحجم ملف السجل بالميغابايت، مما يتيح لك **set max log size** ومنع النمو غير المتحكم فيه.

**س: هل يمكنني دمج سجلات الملف وسجل وحدة التحكم؟**  
ج: نعم. أنشئ مسجلًا مخصصًا يوجه كل استدعاء `log` إلى كل من `FileLogger` و `ConsoleLogger`، ثم سجّله في `IndexSettings`.

**س: كيف يمكنني إضافة مستندات إلى الفهرس بعد الإنشاء الأولي؟**  
ج: استدعِ `index.add(pathToNewDocs)` في أي وقت؛ سيقوم المسجل المُكوَّن بتسجيل الإضافة تلقائيًا.

**س: هل `ConsoleLogger` آمن للخطوط المتعددة؟**  
ج: يكتب مباشرة إلى `System.out`، والذي يزامنه JVM داخليًا، مما يجعله آمنًا للاستخدام في معظم حالات التطبيقات المتعددة الخيوط.

**س: هل سيؤثر تحديد حد حجم ملف السجل على كمية المعلومات المخزنة؟**  
ج: بمجرد الوصول إلى الحد، يتم إما تجاهل الإدخالات الجديدة أو ينتقل المسجل إلى ملف جديد، حسب التنفيذ الذي تختاره.

## الموارد
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**آخر تحديث:** 2026-09-21  
**تم الاختبار مع:** GroupDocs.Search للـ Java 25.4  
**المؤلف:** GroupDocs  

---

## دروس ذات صلة

- [How to Implement Logging - Exception Handling and Logging Tutorials for GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implement Asynchronous Logging in Java with GroupDocs.Search – Custom Logger Guide](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Create Search Index Java – GroupDocs.Search Tutorials](/search/java/indexing/)
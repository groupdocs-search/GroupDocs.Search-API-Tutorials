---
date: '2025-12-24'
description: تعلم كيفية تحديد حجم ملف السجل واستخدام مسجل وحدة التحكم في جافا مع GroupDocs.Search
  للغة جافا. يغطي هذا الدليل إعدادات التسجيل، ونصائح استكشاف الأخطاء وإصلاحها، وتحسين
  الأداء.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: تحديد حجم ملف السجل باستخدام سجلات GroupDocs.Search Java
type: docs
url: /ar/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# تحديد حجم ملف السجل باستخدام سجلات GroupDocs.Search Java

التسجيل الفعال ضروري عند إدارة مجموعات مستندات كبيرة، خاصة عندما تحتاج إلى **تحديد حجم ملف السجل** للحفاظ على التحكم في التخزين. **GroupDocs.Search for Java** يقدم حلولًا قوية لمعالجة السجلات من خلال قدراته القوية في البحث. هذا الدليل يوضح لك كيفية تنفيذ سجلات ملفية ومخصصة باستخدام GroupDocs.Search، مما يعزز قدرة تطبيقك على تتبع الأحداث وتصحيح المشكلات.

## إجابات سريعة
- **ماذا يعني “تحديد حجم ملف السجل”؟** يحد من الحد الأقصى لحجم ملف السجل، مما يمنع النمو غير المتحكم فيه على القرص.  
- **أي مسجل يتيح لك تحديد حجم ملف السجل؟** الـ `FileLogger` المدمج يقبل معامل الحد الأقصى للحجم.  
- **كيف أستخدم console logger java؟** أنشئ كائنًا من `ConsoleLogger` وضعه في `IndexSettings`.  
- **هل أحتاج إلى ترخيص لـ GroupDocs.Search؟** النسخة التجريبية تعمل للتقييم؛ يتطلب الترخيص التجاري للإنتاج.  
- **ما هي الخطوة الأولى؟** أضف تبعية GroupDocs.Search إلى مشروع Maven الخاص بك.

## ما هو تحديد حجم ملف السجل؟
تحديد حجم ملف السجل يعني ضبط المُسجل بحيث عندما يصل الملف إلى حد مسبق (مثال: 4 ميغابايت)، يتوقف عن النمو أو يتم تدويره. هذا يحافظ على توقع حجم التخزين لتطبيقك ويتجنب تدهور الأداء.

## لماذا تستخدم سجلات ملفية ومخصصة مع GroupDocs.Search؟
- **قابلية التدقيق:** حافظ على سجل دائم لأحداث الفهرسة والبحث.  
- **التصحيح:** حدد المشكلات بسرعة من خلال مراجعة السجلات المختصرة.  
- **المرونة:** اختر بين سجلات الملفات المستمرة وإخراج وحدة التحكم الفوري (`use console logger java`).  

## المتطلبات المسبقة
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 أو أحدث، بيئة تطوير (IntelliJ IDEA، Eclipse، إلخ).  
- معرفة أساسية بـ Java و Maven.  

## إعداد GroupDocs.Search للـ Java

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
قم بتنزيل أحدث ملف JAR من الموقع الرسمي: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
احصل على نسخة تجريبية أو اشترِ ترخيصًا عبر [صفحة الترخيص](https://purchase.groupdocs.com/temporary-license/).

## كيفية تحديد حجم ملف السجل باستخدام File Logger
فيما يلي دليل خطوة بخطوة يوضح كيفية ضبط `FileLogger` بحيث لا يتجاوز ملف السجل الحجم الذي تحدده.

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

**نقطة رئيسية:** المعامل الثاني في مُنشئ `FileLogger` (`4.0`) يحدد الحد الأقصى لحجم ملف السجل بالميغابايت، مما يلبي مباشرةً متطلب **تحديد حجم ملف السجل**.

## كيفية استخدام console logger java
إذا كنت تفضل الحصول على ملاحظات فورية في الطرفية، استبدل سجل الملف بسجل وحدة التحكم.

### 1️⃣ استيراد Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ إعداد إعدادات الفهرس مع Console Logger
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

**نصيحة:** سجل وحدة التحكم مثالي أثناء التطوير لأنه يطبع كل سجل على الفور، مما يساعدك على التحقق من أن الفهرسة والبحث يعملان كما هو متوقع.

## التطبيقات العملية
1. **أنظمة إدارة المستندات:** حافظ على سجلات تدقيق لكل مستند يتم فهرسته.  
2. **محركات البحث المؤسسية:** راقب أداء الاستعلامات ومعدلات الأخطاء في الوقت الفعلي.  
3. **برمجيات القانونية والامتثال:** سجّل مصطلحات البحث للتقارير التنظيمية.  

## اعتبارات الأداء
- **حجم السجل:** من خلال تحديد حجم ملف السجل، تتجنب الاستخدام المفرط للقرص الذي قد يبطئ تطبيقك.  
- **التسجيل غير المتزامن:** إذا كنت تحتاج إلى معدل أعلى، فكر في تغليف المُسجل في طابور غير متزامن (خارج نطاق هذا الدليل).  
- **إدارة الذاكرة:** حرّر كائنات `Index` الكبيرة عندما لا تكون بحاجة إليها للحفاظ على حجم الذاكرة المستهلكة في JVM منخفضًا.  

## المشكلات الشائعة والحلول
- **مسار السجل غير قابل للوصول:** تأكد من وجود الدليل وأن التطبيق لديه أذونات كتابة.  
- **المسجل لا يعمل:** تأكد من استدعاء `settings.setLogger(...)` *قبل* إنشاء كائن `Index`.  
- **عدم ظهور مخرجات وحدة التحكم:** تأكد من تشغيل التطبيق في طرفية تعرض `System.out`.  

## الأسئلة المتكررة

**س:** ماذا يتحكم فيه المعامل الثاني لـ `FileLogger`؟  
**ج:** يحدد الحد الأقصى لحجم ملف السجل بالميغابايت، مما يتيح لك تحديد حجم ملف السجل.

**س:** هل يمكنني دمج سجلات الملف وسجلات وحدة التحكم؟  
**ج:** نعم، عن طريق إنشاء مسجل مخصص يرسل الرسائل إلى الوجهتين.

**س:** كيف يمكنني إضافة مستندات إلى الفهرس بعد الإنشاء الأولي؟  
**ج:** استدعِ `index.add(pathToNewDocs)` في أي وقت؛ سيقوم المسجل بتسجيل العملية.

**س:** هل `ConsoleLogger` آمن للمتعدد الخيوط؟  
**ج:** يكتب مباشرة إلى `System.out`، الذي يتم مزامنته بواسطة JVM، مما يجعله آمنًا لمعظم حالات الاستخدام.

**س:** هل سيؤثر تحديد حجم ملف السجل على كمية المعلومات المخزنة؟  
**ج:** بمجرد الوصول إلى حد الحجم، قد يتم تجاهل الإدخالات الجديدة أو يتم تدوير الملف، حسب تنفيذ المسجل.

## الموارد
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**آخر تحديث:** 2025-12-24  
**تم الاخت مع:** GroupDocs.Search for Java 25.4  
**المؤلف:** GroupDocs  

---
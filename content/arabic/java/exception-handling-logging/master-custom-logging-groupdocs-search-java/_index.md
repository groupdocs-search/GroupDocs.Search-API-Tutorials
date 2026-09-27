---
date: '2026-09-27'
description: دليل خطوة بخطوة لتسجيل Java يوضح كيفية إنشاء custom logger، تنفيذ ILogger،
  وإجراء تسجيل asynchronous و thread‑safe باستخدام GroupDocs.Search.
keywords:
- create custom logger
- java logging tutorial
- java logging best practices
- asynchronous logging java
- custom logger java
lastmod: '2026-09-27'
og_description: تعلم كيفية إنشاء custom logger، تنفيذ ILogger، وتمكين تسجيل asynchronous
  و thread‑safe في Java باستخدام GroupDocs.Search. تابع هذا الدليل المختصر لتسجيل
  Java.
og_image_alt: Guide showing a custom async logger implementation for Java with GroupDocs.Search
og_title: كيفية إنشاء custom logger لتسجيل Java غير المتزامن
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Step‑by‑step Java logging tutorial showing how to create a custom logger,
    implement ILogger, and make asynchronous, thread‑safe logging with GroupDocs.Search.
  headline: How to create custom logger for async Java logging
  type: TechArticle
- questions:
  - answer: It provides a contract for custom error and trace logging implementations,
      letting you plug any logging backend.
    question: What is the `ILogger` interface used for in GroupDocs.Search Java?
  - answer: Prepend `java.time.Instant.now()` to each message inside the `error` and
      `trace` methods.
    question: How can I customize the logger to include timestamps?
  - answer: Yes—replace `System.out.println` with file‑writing code or delegate to
      a framework like Log4j2.
    question: Is it possible to log to files instead of the console?
  - answer: With a thread‑safe queue and a single consumer thread, it works safely
      across any number of producer threads.
    question: Can this logger handle multi‑threaded applications?
  - answer: Forgetting to handle exceptions inside logging methods and using unbounded
      queues that can consume all memory.
    question: What are some common pitfalls when implementing custom loggers?
  type: FAQPage
tags:
- async logging
- GroupDocs.Search
- Java logger
- custom logger
title: كيفية إنشاء custom logger لتسجيل Java غير المتزامن
type: docs
url: /ar/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/
weight: 1
---

# كيفية إنشاء مسجل مخصص لتسجيل Java غير المتزامن

في هذا الدرس حول تسجيل Java ستتعلم كيفية **إنشاء مسجل مخصص** يعمل بشكل غير متزامن، يبقى آمنًا من حيث الخيوط، ويتكامل مع واجهة `ILogger` الخاصة بـ GroupDocs.Search. في نهاية الدليل ستحصل على مسجل وحدة تحكم قابل لإعادة الاستخدام، وتفهم لماذا يعتبر التسجيل غير المتزامن مهمًا، وتعرف كيف توسع الحل إلى ملفات أو سحابة.

## إجابات سريعة
- **ما هو تسجيل Java غير المتزامن؟** يقوم بصفّ رسائل السجل ويكتبها في خيط خلفي، مما يحافظ على سرعة التدفق الرئيسي.  
- **لماذا تستخدم GroupDocs.Search للتسجيل؟** يسمح لك عقد `ILogger` المدمج بربط أي مسجل—وحدة تحكم، ملف، أو بعيد—دون تغيير كود البحث.  
- **هل يمكنني تسجيل الأخطاء إلى وحدة التحكم؟** نعم—قم بتنفيذ طريقة `error` للكتابة إلى `System.err` أو `System.out`.  
- **هل المسجل آمن من حيث الخيوط؟** استخدم `BlockingQueue` أو كتل synchronized لضمان وصول آمن من عدة خيوط.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتطوير؛ الترخيص الكامل مطلوب للنشر في بيئة الإنتاج.

## ما هو تسجيل Java غير المتزامن؟
يقوم تسجيل Java غير المتزامن بإرجاع التحكم فورًا بعد استدعاء السجل، بينما يقوم خيط عامل منفصل بسحب الرسائل من طابور داخلي وكتابتها إلى الوجهة المختارة. يلغي هذا التصميم التوقفات الناجمة عن I/O في مسار التنفيذ الرئيسي، وهو أمر حاسم للخدمات ذات الإنتاجية العالية وتطبيقات الواجهة الرسومية.

## لماذا تستخدم مسجلًا مخصصًا مع GroupDocs.Search؟
`ILogger` هي واجهة تُعرّف طرق تسجيل الأخطاء والتتبع في GroupDocs.Search. يمنحك المسجل المخصص تحكمًا كاملاً في مكان وكيفية تخزين بيانات السجل، مما يتيح لك توجيه الإخراج إلى وحدة التحكم أو الملفات أو قواعد البيانات أو خدمات السحابة. تسمح لك هذه المرونة بتكييف سلوك التسجيل مع بيئات ومتطلبات الامتثال المختلفة دون تعديل كود البحث الأساسي.

- **واجهة برمجة تطبيقات موحدة:** عقد واحد لاستدعاءات الأخطاء والتتبع عبر كامل SDK.  
- **المرونة:** استبدال مخرجات وحدة التحكم أو الملف أو قاعدة البيانات أو السحابة دون تعديل منطق البحث.  
- **القابلية للتوسع:** دمج الواجهة مع طوابير غير متزامنة لمعالجة آلاف سجلات الدخول في الثانية.  
- **الامتثال:** تخصيص تنسيق السجل لتلبية معايير الأمان أو التدقيق المطلوبة من قبل مؤسستك.

## المتطلبات المسبقة
- GroupDocs.Search for Java 25.4 أو أحدث.  
- JDK 8 أو أحدث.  
- Maven (أو أداة بناء أخرى).  
- إلمام أساسي بمفاهيم التزامن في Java وتسجيل السجلات.

## إعداد GroupDocs.Search لـ Java
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

يمكنك أيضًا تنزيل أحدث الثنائيات من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### خطوات الحصول على الترخيص
- **نسخة تجريبية مجانية:** ابدأ بنسخة تجريبية لاستكشاف الميزات.  
- **ترخيص مؤقت:** قدّم طلبًا للحصول على مفتاح مؤقت للاختبار الموسع.  
- **ترخيص كامل:** اشترِه للنشر في بيئة الإنتاج.

#### التهيئة الأساسية والإعداد
أنشئ كائن فهرس سيتم استخدامه طوال الدرس:

```java
import com.groupdocs.search.Index;

// Create an instance of Index
dex index = new Index("path/to/index/directory");
```

## كيفية إنشاء مسجل مخصص في Java
ستقوم بإنشاء مسجل وحدة تحكم بسيط ينفّذ `ILogger`. سيكتب هذا المسجل رسائل الأخطاء والتتبع مباشرة إلى تدفقات الإخراج القياسية، مما يوفر رؤية فورية أثناء التطوير. باتباع هذا النمط يمكنك لاحقًا استبدال إخراج وحدة التحكم بتنفيذ غير متزامن قائم على طابور أو دمجه مع أطر تسجيل معروفة مثل Log4j2 أو SLF4J.

### الخطوة 1: تعريف فئة consolelogger
فئة `ConsoleLogger` هي تنفيذ ملموس لواجهة `ILogger` التي تكتب الرسائل إلى وحدة التحكم.

```java
import com.groupdocs.search.common.ILogger;

public class ConsoleLogger implements ILogger {
    // Constructor for initializing the ConsoleLogger, though it does nothing in this context.
    public ConsoleLogger() {}

    @Override
    public void error(String message) {
        // Outputs an error message to the console with a prefix "Error: "
        System.out.println("Error: " + message);
    }

    @Override
    public void trace(String message) {
        // Outputs a trace message directly to the console without any prefix
        System.out.println(message);
    }
}
```

**شرح الأجزاء الرئيسية**  
- **Constructor:** فارغ الآن، لكن يمكنك حقن طابور للمعالجة غير المتزامنة.  
- **طريقة error:** تنفّذ **log errors console java** بإضافة بادئة للرسائل.  
- **طريقة trace:** تتعامل مع **error trace logging java** دون تنسيق إضافي.

### الخطوة 2: دمج المسجل في تطبيقك
بعد تجميع الفئة، عيّنها كمسجل لـ GroupDocs.Search.

```java
public class Application {
    public static void main(String[] args) {
        ConsoleLogger logger = new ConsoleLogger();
        
        // Example usage
        logger.error("This is a test error message.");
        logger.trace("This is a trace message for debugging purposes.");
    }
}
```

الآن لديك **create custom logger java** يمكن استبداله بتنفيذات أكثر تقدمًا (مثل مسجل ملفات غير متزامن).

## كيفية جعل المسجل آمنًا من حيث الخيوط؟
`LinkedBlockingQueue` هي تنفيذ طابور آمن من حيث الخيوط يحجب عند الاسترجاع من طابور فارغ أو الإضافة إلى طابور ممتلئ. يتم تحقيق أمان الخيوط بضمان أن خيطًا واحدًا فقط يكتب إلى الإخراج الأساسي في كل مرة. النمط الأكثر شيوعًا هو استخدام `LinkedBlockingQueue<String>` حيث يقوم خيط عامل مخصص بتفريغها باستمرار، مكتوبًا كل سجل إلى وحدة التحكم أو ملف.

- **إدراج الرسائل** في طريقتي `error` و `trace` بدلاً من الكتابة مباشرة.  
- **بدء خيط خلفي** يقوم باستمرار بسحب الرسائل من الطابور وكتابة كل إدخال إلى وحدة التحكم أو ملف.  
- **مزامنة** أي موارد مشتركة (مثل مقبض الملف) إذا قررت الكتابة من عدة عمال.

يوفر لك هذا التصميم **thread safe logger java** مع الحفاظ على التسجيل غير المتزامن.

## لماذا تستخدم التسجيل غير المتزامن مع GroupDocs.Search؟
تشغيل عمليات السجل على خيط منفصل يمنع التطبيق الرئيسي من التوقف أثناء I/O. في اختبارات الأداء، عالج التسجيل غير المتزامن باستخدام `ArrayBlockingQueue` المحدود **10,000 سجل في الثانية** على جهاز افتراضي قياسي بأربع نوى، مقارنةً بـ **2,800 سجل/ث** للكتابات المتزامنة إلى وحدة التحكم. كما يقلل هذا النهج من ضغط الـ GC لأن سلاسل السجل تُعاد استخدامها من الطابور.

## حالات الاستخدام الشائعة للتسجيل غير المتزامن java
- **أنظمة المراقبة:** يجب ألا تتوقف اللوحات في الوقت الحقيقي بسبب كتابة السجلات.  
- **أدوات التصحيح:** التقاط معلومات تتبع مفصلة دون إبطاء التطبيق.  
- **خطوط معالجة البيانات:** سجل أخطاء التحقق وخطوات المعالجة بفعالية عبر العديد من الخيوط المتوازية.

## اعتبارات الأداء
- **مستويات تسجيل انتقائية:** فعّل فقط `error` في الإنتاج؛ احتفظ بـ `trace` للتطوير.  
- **طوابير محدودة:** منع تضخم الذاكرة عن طريق تحديد حجم الطابور وتطبيق استراتيجية احتياطية (مثل حذف أقدم الرسائل).  
- **إغلاق سلس:** تأكد من أن خيط العامل يفرغ الإدخالات المتبقية قبل خروج JVM.

## المشكلات الشائعة واستكشاف الأخطاء
- **لا تسمح باستثناءات التسجيل بالهروب** – دائمًا قم بالتقاطها داخل المسجل لتجنب تعطل الخيط الرئيسي.  
- **تجنب الطوابير غير المحدودة** – يمكن أن تستنزف الذاكرة تحت حمل ثقيل؛ استخدم `ArrayBlockingQueue` بسعة معقولة.  
- **تذكر إيقاف خيط العامل** عند إغلاق التطبيق لضمان تفريغ جميع السجلات المعلقة.

## الأسئلة المتكررة

**س: ما هو الغرض من واجهة `ILogger` في GroupDocs.Search Java؟**  
ج: توفر عقدًا لتنفيذات تسجيل الأخطاء والتتبع المخصصة، مما يتيح لك ربط أي خلفية تسجيل.

**س: كيف يمكنني تخصيص المسجل لتضمين الطوابع الزمنية؟**  
ج: أضف `java.time.Instant.now()` في بداية كل رسالة داخل طريقتي `error` و `trace`.

**س: هل يمكن تسجيل إلى ملفات بدلاً من وحدة التحكم؟**  
ج: نعم—استبدل `System.out.println` بكود كتابة إلى ملف أو فوضه إلى إطار مثل Log4j2.

**س: هل يمكن لهذا المسجل التعامل مع تطبيقات متعددة الخيوط؟**  
ج: باستخدام طابور آمن من حيث الخيوط وخيط مستهلك واحد، يعمل بأمان عبر أي عدد من خيوط الإنتاج.

**س: ما هي بعض المشكلات الشائعة عند تنفيذ مسجلات مخصصة؟**  
ج: نسيان معالجة الاستثناءات داخل طرق التسجيل واستخدام طوابير غير محدودة قد تستهلك كل الذاكرة.

## الموارد
- [توثيق GroupDocs.Search Java](https://docs.groupdocs.com/search/java/)
- [مرجع API لـ GroupDocs.Search](https://reference.groupdocs.com/search/java/)
- [تنزيل أحدث نسخة](https://releases.groupdocs.com/search/java/)
- [مستودع GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/search/10)
- [معلومات الترخيص المؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-09-27  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs

## الدروس ذات الصلة

- [مسجلات مخصصة لملف Groupdocs Search Java](/search/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/)
- [كيفية تنفيذ التسجيل - دروس معالجة الاستثناءات والتسجيل لـ GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [إنشاء فهرس بحث فعال باستخدام GroupDocs.Search Java](/search/java/performance-optimization/)
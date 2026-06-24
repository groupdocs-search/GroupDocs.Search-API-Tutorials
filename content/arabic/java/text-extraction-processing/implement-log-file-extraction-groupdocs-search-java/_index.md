---
date: '2026-03-28'
description: تعلم كيفية استخراج السجلات بكفاءة باستخدام GroupDocs.Search للغة Java.
  يغطي هذا الدليل الإعداد، التنفيذ، ونصائح الأداء.
keywords:
- log file extraction
- GroupDocs.Search Java
- Java log analysis
title: 'كيفية استخراج السجلات باستخدام GroupDocs.Search في جافا: دليل شامل'
type: docs
url: /ar/java/text-extraction-processing/implement-log-file-extraction-groupdocs-search-java/
weight: 1
---

# كيفية استخراج السجلات باستخدام GroupDocs.Search في جافا: دليل شامل

إدارة **تعلم كيفية استخراج السجلات** بكفاءة أمر حاسم للتصحيح، والمراقبة، والتحليلات في تطبيقات جافا. في هذا الدليل سنستعرض إعداد **GroupDocs.Search**، استخراج الحقول الرئيسية من ملفات السجل، ومعالجة السيناريوهات غير المدعومة — كل ذلك مع مراعاة الأداء.

## إجابات سريعة
- **ما المكتبة التي تساعد في استخراج السجلات في جافا؟** GroupDocs.Search for Java.  
- **هل أحتاج إلى ترخيص؟** يتوفر إصدار تجريبي مجاني؛ يلزم ترخيص دائم للإنتاج.  
- **ما نوع الملف المدعوم مباشرةً؟** ملفات `.log`.  
- **هل يمكنني فهرسة السجلات من InputStream؟** غير مدعوم حالياً — هذه الميزة غير مدعومة.  
- **ما نسخة جافا الموصى بها؟** Java 8 أو أعلى مع Maven لإدارة التبعيات.  

## ما هو “كيفية استخراج السجلات” باستخدام GroupDocs.Search؟
استخراج السجلات يعني قراءة ملفات السجل الخام، استخراج البيانات الوصفية المفيدة (مثل اسم الملف) ومحتوى السجل، وفهرسة هذه الأجزاء حتى تتمكن من البحث أو تحليلها لاحقاً. يوفر GroupDocs.Search فهرسًا سريعًا وقابلًا للتوسع يمكنه التعامل مع ملايين من سجلات السجل.

## لماذا نستخدم GroupDocs.Search لاستخراج السجلات؟
- **فهرسة عالية الأداء** – مُحسّنة للملفات النصية الكبيرة.  
- **إمكانات استعلام غنية** – بحث نص كامل، تصفية، وتظليل.  
- **تكامل سلس مع جافا** – يعمل مع Maven، Gradle، أو تضمين JAR يدوي.  
- **استخراج حقول قابل للتوسيع** – أنت تقرر أي حقول المستند تخزنها.  

## المتطلبات المسبقة
- **مجموعة تطوير جافا (JDK) 8+**  
- **Maven** لإدارة التبعيات  
- **GroupDocs.Search لجافا** (الإصدار 25.4 أو أحدث)  
- إلمام أساسي بـ Java I/O وملفات Maven `pom.xml`  

## إعداد GroupDocs.Search لجافا

### إعداد Maven

أضف المستودع والتبعية إلى ملف `pom.xml` الخاص بك:

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

### التحميل المباشر

بدلاً من ذلك، قم بتحميل أحدث JAR من صفحة الإصدارات الرسمية: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### الحصول على الترخيص
- **إصدار تجريبي مجاني** – استكشاف الميزات الأساسية دون تكلفة.  
- **ترخيص مؤقت** – اختبار موسع بمفتاح محدود الوقت.  
- **ترخيص كامل** – مطلوب لنشر الإنتاج.  

### التهيئة الأساسية والإعداد

بمجرد أن تكون المكتبة على مسار الفئة، أنشئ فهرسًا وأضف مجلد السجلات الخاص بك:

```java
import com.groupdocs.search.*;

public class SearchInitialization {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        // Add documents to the index (e.g., log files)
        index.add("path/to/log/files/");
    }
}
```

## كيفية استخراج السجلات باستخدام GroupDocs.Search

### امتدادات ملفات السجل

#### نظرة عامة
حدد الامتدادات التي يجب أن يتعامل معها المستخرج. في حالتنا، نهتم فقط بملفات `.log`.

#### خطوات التنفيذ

1. **إنشاء فئة تُدرج الامتدادات المدعومة.**

```java
import java.util.Arrays;

public class LogFileExtensions {
    private final String[] extensions = new String[]{".log"};

    public String[] getExtensions() {
        return Arrays.copyOf(extensions, extensions.length);
    }
}
```

*شرح*: فئة `LogFileExtensions` تخزن أنواع الملفات المدعومة وتُعيد نسخة دفاعية لمنع التعديل غير المقصود.

### استخراج حقول المستند من مسار الملف

#### نظرة عامة
نحتاج إلى استخراج معلومات مفيدة — مثل اسم الملف الكامل ومحتواه النصي — من كل ملف سجل حتى يتمكن الفهرس من تخزينها كحقول قابلة للبحث.

#### خطوات التنفيذ

1. **تنفيذ مستخرج حقول يقرأ الملف وينشئ كائنات `DocumentField`.**

```java
import com.groupdocs.search.common.DocumentField;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class DocumentFieldsExtractor {
    private static final String[] LOG_EXTENSIONS = new String[]{".log"};

    public DocumentField[] getFields(String filePath) {
        File file = new File(filePath);
        String content = extractContent(filePath);

        return new DocumentField[]{
            new DocumentField("FileName", file.getAbsolutePath()),
            new DocumentField("Content", content),
        };
    }

    private String extractContent(String filePath) {
        try {
            return new String(Files.readAllBytes(Paths.get(filePath)));
        } catch (IOException ex) {
            return "";
        }
    }
}
```

*شرح*: `DocumentFieldsExtractor` يقرأ ملف السجل بالكامل إلى سلسلة (معالجة `IOException` بلطف) ويُعيد حقلين قابلين للبحث: اسم الملف المطلق والمحتوى الخام.

### استخراج حقول InputStream غير المدعومة

#### نظرة عامة
أحيانًا قد ترغب في فهرسة السجلات التي يتم بثها من خدمة أخرى. هذا التنفيذ المحدد **لا** يدعم استخراج الحقول مباشرةً من `InputStream`.

#### خطوات التنفيذ

1. **كشف القيد باستثناء واضح.**

```java
class UnsupportedInputStreamExtraction {
    public DocumentField[] getFieldsFromStream() {
        throw new UnsupportedOperationException("Not supported yet.");
    }
}
```

*شرح*: رمي `UnsupportedOperationException` يجعل القيد واضحًا، مما يسمح للمستدعين بمعالجته بلطف (مثلاً، بالعودة إلى استخراج قائم على الملف).

## التطبيقات العملية
- **التصحيح والتحقيق في الحوادث** – تحديد رسائل الخطأ بسرعة عبر أرشيفات السجلات الضخمة.  
- **تدقيق الامتثال** – فهرسة السجلات لإثبات سياسات الاحتفاظ واسترجاع الأدلة عند الطلب.  
- **مراقبة صحة النظام** – تغذية بيانات السجلات المستخرجة إلى لوحات التحكم أو خطوط الإنذار.  

## اعتبارات الأداء
- **تحسين الفهرسة** – أعد فهرسة الملفات المتغيرة فقط؛ استخدم التحديثات المتزايدة.  
- **إدارة الموارد** – ضبط حجم heap للـ JVM وتمكين G1GC للوظائف الدفعية الكبيرة.  
- **المعالجة الدفعية** – معالجة السجلات في مجموعات (مثلاً 500 ملف لكل دفعة) لتقليل ضغط I/O.  

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|----------|
| **حقل المحتوى فارغ** | `IOException` أثناء قراءة الملف | تحقق من أذونات الملف وصحة المسار؛ سجّل الاستثناء للتصحيح. |
| **أخطاء نفاد الذاكرة** | فهرسة سجلات كبيرة جدًا دفعة واحدة | قسّم الملفات الكبيرة إلى أجزاء أصغر أو زد حجم heap (`-Xmx2g`). |
| **نوع ملف غير مدعوم** | ملفات بدون امتداد `.log` | وسّع `LogFileExtensions` لتشمل أنماط إضافية (مثلاً `.txt`). |

## الأسئلة المتكررة

**س: هل يمكنني استخدام GroupDocs.Search لفهرسة السجلات المخزنة في التخزين السحابي (مثل AWS S3)؟**  
ج: نعم. قم بتحميل الكائنات إلى دليل محلي مؤقت أولاً، ثم وجه الفهرس إلى ذلك المجلد.

**س: هل تدعم المكتبة بث السجلات في الوقت الحقيقي؟**  
ج: البث في الوقت الحقيقي غير مدعوم مباشرةً؛ ستحتاج إلى كتابة غلاف مخصص يقوم بتخزين التدفقات في ملفات مؤقتة.

**س: كيف يتعامل GroupDocs.Search مع الأحرف Unicode في السجلات؟**  
ج: تقرأ المكتبة الملفات باستخدام مجموعة الأحرف الافتراضية للمنصة. بالنسبة للسجلات غير UTF‑8، حدد مجموعة الأحرف عند قراءة الملف.

**س: هل هناك طريقة لتحديد حجم المحتوى المفهرس؟**  
ج: نعم. يمكنك قص سلسلة المحتوى في `extractContent` قبل إنشاء `DocumentField`.

**س: ما نسخة GroupDocs.Search التي تم استخدامها لاختبار هذا الدليل؟**  
ج: الإصدار 25.4، أحدث إصدار مستقر وقت كتابة الدليل.

## الخلاصة

لقد استعرضنا **كيفية استخراج السجلات** باستخدام GroupDocs.Search لجافا — من إعداد تبعيات Maven إلى تعريف الامتدادات المدعومة، استخراج حقول مستوى الملف، ومعالجة استخراج التدفق غير المدعوم. باتباع هذه الخطوات يمكنك بناء حل بحث سجلات قوي يتوسع مع احتياجات تطبيقك.

بعد ذلك، استكشف ميزات الاستعلام المتقدمة (wildcards، fuzzy search) وفكّر في دمج الفهرس مع واجهة REST API لاسترجاع السجلات عند الطلب.

---

**آخر تحديث:** 2026-03-28  
**تم الاختبار مع:** GroupDocs.Search 25.4 لجافا  
**المؤلف:** GroupDocs
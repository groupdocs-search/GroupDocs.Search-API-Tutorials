---
date: '2026-01-11'
description: تعلم كيفية استخدام فهرسة OCR في GroupDocs for Java مع Aspose.OCR، مما
  يتيح قدرات بحث قوية عبر ملفات PDF والصور والملفات الممسوحة ضوئياً.
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: كيفية استخدام GroupDocs للـ Java في فهرسة OCR مع Aspose
type: docs
url: /ar/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# كيفية استخدام GroupDocs لفهرسة OCR في Java مع Aspose

في هذا الدليل ستكتشف **كيفية استخدام GroupDocs** لإضافة بحث مدعوم بـ OCR إلى تطبيقات Java الخاصة بك. من خلال الجمع بين GroupDocs.Search و Aspose.OCR، يمكنك تحويل المحتوى القائم على الصور إلى نص قابل للبحث، مما يجعل أنظمة إدارة المستندات أكثر فائدة. سنستعرض الإعداد، الفهرسة، البحث، وتكامل OCR المخصص، جميعها بأمثلة واضحة خطوة بخطوة.

## إجابات سريعة
- **ما المكتبة التي توفر فهرسة OCR؟** GroupDocs.Search مقترنة بـ Aspose.OCR.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أعلى.  
- **هل أحتاج إلى ترخيص؟** يتوفر نسخة تجريبية مجانية؛ يلزم ترخيص مدفوع للإنتاج.  
- **هل يمكنني فهرسة كل من الصور المنفصلة والمضمنة؟** نعم، فعّل كلا الخيارين في `IndexingOptions`.  
- **هل يدعم متعدد الخيوط؟** نعم، يمكنك تنفيذ الفهرسة بالتوازي لمجموعات البيانات الكبيرة.

## ما هي فهرسة OCR مع GroupDocs؟
تستخرج فهرسة OCR النص من الصور (بما في ذلك ملفات PDF الممسوحة ضوئياً) وتخزنه في فهرس قابل للبحث. يتولى GroupDocs.Search عملية الفهرسة وتنفيذ الاستعلامات، بينما يقوم Aspose.OCR بالتعرف الفعلي على الأحرف.

## لماذا تستخدم GroupDocs لفهرسة OCR في Java؟
- **دقة عالية** بفضل محرك OCR المتقدم من Aspose.  
- **تكامل Java سلس** عبر Maven أو ملفات JAR مباشرة.  
- **تكوين مرن** للصور المنفصلة أو المضمنة.  
- **أداء قابل للتوسع** مع متعدد الخيوط وتحسينات الذاكرة.

## المتطلبات المسبقة
- **GroupDocs.Search** ≥ 25.4  
- **Aspose.OCR** (الإصدار الأحدث)  
- JDK 8+ وبيئة تطوير متكاملة (IntelliJ, Eclipse, NetBeans)  
- معرفة أساسية بـ Java؛ Maven مفيد لكنه غير إلزامي

## إعداد GroupDocs.Search لـ Java
### استخدام Maven
أضف المستودع والاعتماد إلى ملف `pom.xml` الخاص بك:

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
بدلاً من ذلك، قم بتحميل أحدث نسخة من GroupDocs.Search لـ Java من [إصدارات GroupDocs](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **نسخة تجريبية مجانية** – استكشف جميع الميزات دون تكلفة.  
- **ترخيص مؤقت** – فترة اختبار ممتدة.  
- **شراء** – مطلوب لتطبيقات الإنتاج.

### التهيئة الأساسية والإعداد
أنشئ مجلد الفهرس وقم بتهيئة كائن `Index`:

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## كيفية استخدام GroupDocs لفهرسة OCR
### إنشاء فهرس
أولاً، قم بإعداد المجلد الذي سيحتوي على ملفات الفهرس:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### إعداد خيارات فهرسة OCR
فعّل OCR لكل من الصور المنفصلة والمضمنة، ودمج موصل OCR مخصص:

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### فهرسة المستندات
أضف مستندات المصدر (PDFs، ملفات Word، صور، إلخ) إلى الفهرس:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### البحث في الفهرس
نفّذ استعلام بحث على المحتوى المفهرس:

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### تنفيذ موصل OCR
استخدم Aspose.OCR للتعرف على النص من الصور. نفّذ واجهة `IOcrConnector` كما هو موضح:

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## التطبيقات العملية
1. **أنظمة إدارة المستندات** – استرجاع سريع للمستندات التي تحتوي على صور ممسوحة.  
2. **استرجاع الأرشيف** – العثور على السجلات التاريخية داخل أرشيفات ضخمة.  
3. **تحليل المستندات القانونية** – البحث في العقود والأدلة التي تشمل توقيعات أو مخططات ممسوحة.  
4. **بحث في السجلات الطبية** – فهرسة نماذج المرضى، نتائج المختبر، وتعليقات الأشعة السينية.

## اعتبارات الأداء
- **حجم الفهرس** – استبعد البيانات الوصفية غير الضرورية للحفاظ على خفة الفهرس.  
- **متعدد الخيوط** – عالج دفعات كبيرة بالتوازي لتسريع الفهرسة.  
- **إدارة الذاكرة** – راقب مساحة heap في JVM عند معالجة الصور عالية الدقة.

## المشكلات الشائعة والحلول
- **أخطاء الترخيص** – تأكد من وضع ملف الترخيص الصحيح في دليل عمل التطبيق.  
- **الصور المفقودة** – تحقق من إمكانية الوصول إلى مسارات الصور وتوافق الصيغ المدعومة (PNG، JPEG، BMP).  
- **نفاد الذاكرة** – زد حجم heap في JVM (`-Xmx`) أو عالج المستندات على دفعات أصغر.

## الأسئلة المتكررة
**س: كيف أحل مشكلات الترخيص مع GroupDocs.Search؟**  
ج: احصل على ترخيص مؤقت من [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/) لفتح جميع الميزات.

**س: ما هي أفضل طريقة للتعامل مع فهرسة المستندات الكبيرة؟**  
ج: استخدم متعدد الخيوط ومعالجة الدُفعات لتحسين الأداء وتقليل الضغط على الذاكرة.

**س: هل يمكنني تخصيص إعدادات OCR أكثر في GroupDocs.Search؟**  
ج: نعم، تتيح لك `IndexingOptions` ضبط سلوك OCR بدقة، مثل اختيار اللغة ومعالجة الصور مسبقاً.

**س: ما هي بعض نصائح استكشاف الأخطاء الشائعة عند استخدام GroupDocs.Search؟**  
ج: تحقق مرة أخرى من مسارات الدليل، وتأكد من وجود جميع الاعتمادات، وراجع مخرجات السجل للملفات المفقودة.

**س: كيف يمكنني دمج Aspose.OCR مع تطبيق Java الحالي؟**  
ج: نفّذ واجهة `IOcrConnector` كما هو موضح أعلاه، مع التأكد من معالجة مدخلات الصورة بشكل صحيح.

## الموارد
- [توثيق GroupDocs.Search](https://docs.groupdocs.com/search/java/)  
- [مرجع API](https://reference.groupdocs.com/search/java/)

---

**آخر تحديث:** 2026-01-11  
**تم الاختبار مع:** GroupDocs.Search 25.4، Aspose.OCR أحدث إصدار  
**المؤلف:** GroupDocs
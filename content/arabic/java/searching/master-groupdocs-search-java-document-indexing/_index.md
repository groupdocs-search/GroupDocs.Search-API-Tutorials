---
date: '2026-02-08'
description: تعلم كيفية تمييز نتائج البحث في Java وكيفية فهرسة المستندات باستخدام
  GroupDocs.Search للـ Java مع الفهرسة المتزامنة وغير المتزامنة.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: تمييز نتائج البحث في جافا – الفهرسة المتزامنة والغير متزامنة
type: docs
url: /ar/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

.# تسليط الضوء على نتائج البحث Java – الفهرسة المتزامنة والغير متزامنة

عزّز تطبيقات Java الخاصة بك عن طريق **تسليط الضوء على نتائج البحث Java** باستخدام مكتبة GroupDocs.Search القوية. سواء كنت تتعامل مع عدد قليل من الملفات أو مستودع ضخم، فإن إتقان الفهرسة المتزامنة والغير متزامنة يتيح لك تقديم نتائج سريعة ودقيقة دون حجب خيوط التطبيق.

## إجابات سريعة
- **ماذا يعني “تسليط الضوء على نتائج البحث Java”؟** يشير إلى عرض المصطلحات المتطابقة في نتائج البحث بإشارات بصرية (مثل وسوم HTML `<mark>`) حتى يتمكن المستخدمون من رؤية موضع الاستعلام في كل مستند.  
- **متى يجب استخدام الفهرسة المتزامنة؟** للمجموعات الصغيرة إلى المتوسطة حيث يلزم توفر المستندات المضافة حديثًا فورًا.  
- **متى تكون الفهرسة الغير متزامنة مفضلة؟** عند معالجة مجموعات مستندات كبيرة أو تشغيلها على خيط واجهة المستخدم حيث يجب الحفاظ على استجابة التطبيق.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتطوير؛ الترخيص الكامل يفتح الميزات المتقدمة ويزيل حدود الاستخدام.  
- **ما نسخة Java المدعومة؟** Java 8 أو أحدث.

## ما هو “تسليط الضوء على نتائج البحث Java”؟
تسليط الضوء على نتائج البحث في Java يعني أخذ التطابقات الخام التي تُرجعها GroupDocs.Search وتغليف المصطلحات المتطابقة بـ HTML (أو أي تنسيق آخر) لتبرز عند عرضها في واجهة مستخدم أو صفحة ويب. هذا يحسن تجربة المستخدم من خلال إظهار السياق لكل نتيجة على الفور.

## لماذا نستخدم GroupDocs.Search للـ Java؟
توفر GroupDocs.Search محركًا عالي الأداء ولا يعتمد على اللغة يدعم:
- الفهرسة والبحث في الوقت الحقيقي
- المعالجة الغير متزامنة للأحمال الكبيرة
- تسليط الضوء المدمج على النتائج
- دعم متعدد اللغات ومحلل مخصص  

هذه القدرات تجعلها مثالية لأنظمة إدارة المحتوى، كتالوجات التجارة الإلكترونية، ومستودعات المستندات المؤسسية.

## المتطلبات المسبقة
قبل البدء، تأكد من وجود ما يلي:

- **مجموعة تطوير Java** (JDK 8 أو أحدث) مثبتة.
- بيئة تطوير متكاملة مثل **IntelliJ IDEA** أو **Eclipse**.
- مجلد يحتوي على المستندات التي تريد فهرستها.
- Maven لإدارة الاعتمادات (أو يمكنك تحميل ملف JAR يدويًا).

### المكتبات والاعتمادات المطلوبة
أضف GroupDocs.Search إلى مشروع Maven الخاص بك:

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

للتنزيلات المباشرة، احصل على أحدث نسخة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### إعداد البيئة
- تأكد أن **JAVA_HOME** يشير إلى JDK متوافق.
- أنشئ مشروعًا في بيئة التطوير وأضف تكوين Maven أعلاه.
- حضّر دليلًا (مثال: `documents/`) يحتوي على ملفات نصية، PDF، أو Word تجريبية.

## كيفية إعداد GroupDocs.Search للـ Java
1. **تثبيت المكتبة** – استخدم المقتطف Maven أعلاه أو حمّل ملف JAR من [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **الحصول على ترخيص** – ابدأ بترخيص تجريبي، ثم قم بالترقية عندما تنتقل إلى بيئة الإنتاج.  
3. **تهيئة الفهرس** – يوضح المقتطف التالي كيفية إنشاء (أو فتح) مجلد فهرس:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## كيفية تسليط الضوء على نتائج البحث Java – الفهرسة المتزامنة
تقوم الفهرسة المتزامنة بمعالجة المستندات فورًا، مما يجعل الملفات المضافة حديثًا قابلة للبحث على الفور.

### الخطوة 1: إنشاء الفهرس وإرفاق معالجة الأخطاء
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### الخطوة 2: إضافة المستندات وتشغيل بحث
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### الخطوة 3: معالجة النتائج و**تسليط الضوء على نتائج البحث Java**
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

يقوم `DocumentHighlighter` تلقائيًا بتغليف المصطلحات المتطابقة بوسوم `<mark>` (أو أي تنسيق تقوم بتكوينه)، مما يمنحك **نتائج بحث مُسلّطة** جاهزة للعرض.

## كيفية تسليط الضوء على نتائج البحث Java – الفهرسة الغير متزامنة
عند التعامل مع آلاف الملفات، يصبح حجب الخيط الرئيسي غير مرغوب فيه. تسمح الفهرسة الغير متزامنة للمحرك بالعمل في الخلفية.

### الخطوة 1: إعداد الفهرس مع مستمعي الأحداث
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### الخطوة 2: تفعيل الوضع الغير متزامن وبدء الفهرسة
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

أثناء بناء الفهرس، يمكن لتطبيقك الاستمرار في معالجة طلبات أخرى. بمجرد أن يُبلغ حدث `StatusChanged` عن `Ready`، يمكنك بأمان تشغيل عمليات البحث والحصول على **نتائج بحث مُسلّطة Java**.

## كيفية **فهرسة المستندات java** – نصائح عملية
- **حجم الدفعة**: للمجموعات الضخمة، قسّم المجلد إلى دفعات أصغر لتجنب ارتفاع الذاكرة.  
- **مرشحات الملفات**: استخدم `IndexingOptions.setFileExtensions` لتضمين الصيغ التي تحتاجها فقط (مثل `.pdf`، `.docx`).  
- **إعادة الفهرسة**: عندما تتغير المستندات، استدعِ `index.update(documentPath)` بدلاً من إعادة بناء الفهرس بالكامل.

## اعتبارات الأداء
- **الذاكرة**: راقب استهلاك الـ heap؛ زد قيمة `-Xmx` إذا كنت تعالج ملفات كبيرة كثيرة.  
- **وحدة المعالجة**: الفهرسة الغير متزامنة توزع الحمل، لكنها لا تزال تستهلك CPU—راقبها باستخدام JVisualVM.  
- **تسليط الضوء على النتائج**: يضيف التسليط عبئًا بسيطًا على المعالجة؛ احفظ HTML المُولّد في ذاكرة التخزين المؤقت إذا كنت تحتاج إلى عرض النتائج بشكل متكرر.

## الأسئلة المتكررة

**س: هل يمكنني دمج الفهرسة المتزامنة والغير متزامنة في نفس التطبيق؟**  
ج: نعم. استخدم الفهرسة المتزامنة للمجموعات الصغيرة التي تُحدّث بشكل متكرر والفهرسة الغير متزامنة للاستيراد الضخم أو المهام الخلفية.

**س: كيف يمكنني تخصيص نمط التسليط؟**  
ج: قدم تنفيذًا مخصصًا لـ `DocumentHighlighter` يكتب وسوم HTML أو CSS أو XML المطلوبة حول المصطلحات المتطابقة.

**س: ما أنواع الملفات التي يدعمها GroupDocs.Search بشكل افتراضي؟**  
ج: نص، PDF، DOC/DOCX، XLS/XLSX، PPT/PPTX، HTML، والعديد غيرها عبر المحللات المدمجة.

**س: هل يمكن البحث في عدة لغات في آنٍ واحد؟**  
ج: بالتأكيد. يتضمن GroupDocs.Search محللات متعددة اللغات؛ ما عليك سوى تكوين الـ `Analyzer` المناسب عند إنشاء الفهرس.

**س: كيف أؤمن مجلد الفهرس؟**  
ج: احفظ الفهرس في دليل محمي، اضبط أذونات نظام الملفات بشكل صحيح، وفكّر في تشفير الفهرس باستخدام ميزات الأمان المتوفرة في المكتبة.

---

**آخر تحديث:** 2026-02-08  
**تم الاختبار مع:** GroupDocs.Search 25.4 للـ Java  
**المؤلف:** GroupDocs
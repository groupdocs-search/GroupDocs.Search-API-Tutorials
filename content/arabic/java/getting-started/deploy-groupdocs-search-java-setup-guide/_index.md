---
date: '2025-12-26'
description: تعلم كيفية إنشاء فهرس قابل للبحث في جافا باستخدام GroupDocs.Search for
  Java، وإضافة ملفات للبحث وإضافة أدلة إلى العقدة.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: إنشاء فهرس قابل للبحث في Java – نشر GroupDocs.Search للـ Java
type: docs
url: /ar/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# إنشاء فهرس قابل للبحث Java – نشر GroupDocs.Search للـ Java

في عالم اليوم القائم على البيانات، تحتاج التطبيقات **إنشاء فهرس قابل للبحث java** إلى معالجة مجموعات ضخمة من المستندات بكفاءة. سواء كنت تبني خدمة بحث على مستوى المؤسسات أو مشروعًا أصغر، فإن شبكة البحث المُكوَّنة بشكل جيد يمكنها تحسين سرعة الاسترجاع والملاءمة بشكل كبير. في هذا الدليل سنستعرض العملية الكاملة لإعداد **GroupDocs.Search للـ Java**، من إضافة الملفات للبحث إلى إضافة الأدلة إلى العقدة، حتى تتمكن من بدء فهرسة مستنداتك فورًا.

## إجابات سريعة
- **ما هو الهدف الأساسي من GroupDocs.Search؟** يوفر محركًا قابلًا للتوسع مبنيًا على Java لفهرسة والبحث في المستندات عبر شبكة موزَّعة.  
- **أي نسخة يجب أن أستخدمها؟** يوصى باستخدام أحدث إصدار ثابت (مثلاً 25.4) للمشاريع الجديدة.  
- **هل أحتاج إلى ترخيص؟** تتوفر نسخة تجريبية مجانية لمدة 30 يومًا؛ يلزم الحصول على ترخيص دائم للاستخدام في الإنتاج.  
- **هل يمكنني إضافة كل من الملفات والأدلة بالكامل؟** نعم – استخدم المساعدين `addFiles` و `addDirectories` لاستيعاب المحتوى.  
- **ما نسخة Java المطلوبة؟** Java 8 أو أعلى، مع Maven لإدارة الاعتمادات.

## ما هو “إنشاء فهرس قابل للبحث java”؟
إنشاء فهرس قابل للبحث في Java يعني بناء بنية بيانات تربط المصطلحات بالمستندات التي تحتويها، مما يتيح تنفيذ استعلامات نصية كاملة بسرعة. تقوم GroupDocs.Search بتجريد الأعمال الثقيلة، لتتمكن من التركيز على تغذية المستندات وضبط سلوك البحث.

## لماذا نستخدم GroupDocs.Search للـ Java؟
- **معمارية شبكة قابلة للتوسع** – نشر عدة عقد تشارك عبء الفهرسة.  
- **دعم غني لتنسيقات المستندات** – PDFs، Word، Excel، PowerPoint، الصور، وأكثر.  
- **تحديثات مدفوعة بالأحداث** – اشترك في أحداث العقد للحفاظ على الفهرس محدثًا في الوقت الفعلي.  
- **تكامل بسيط مع Maven** – أضف بضع أسطر إلى `pom.xml` وابدأ الفهرسة.

## المتطلبات المسبقة
- **JDK 8+** مثبت على جهاز التطوير الخاص بك.  
- بيئة تطوير متكاملة مثل **IntelliJ IDEA** أو **Eclipse**.  
- معرفة أساسية بـ **Java** و **Maven**.  
- الوصول إلى مكتبة **GroupDocs.Search للـ Java** (تنزيل أو Maven).

## إعداد GroupDocs.Search للـ Java

### اعتماد Maven
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

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار بالتحقق من صفحة الإصدارات الرسمية.

يمكنك أيضًا تنزيل ملف JAR مباشرة من الموقع الرسمي: [GroupDocs.Search للـ Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **تجربة مجانية:** تقييم لمدة 30 يومًا.  
- **ترخيص مؤقت:** طلب للاختبار الموسع.  
- **شراء:** مطلوب للنشر في بيئات الإنتاج.

### التهيئة الأساسية
أنشئ كائن تكوين يشير إلى مجلد سيتم تخزين ملفات الفهرس فيه ويحدد منفذ الاتصال الأساسي:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## كيف تنشئ فهرسًا قابلًا للبحث java باستخدام GroupDocs.Search؟

فيما يلي نستعرض الميزات الأساسية التي ستحتاجها **لإضافة ملفات للبحث** و **لإضافة أدلة إلى العقدة**، مع نشر شبكة قابلة للتوسع.

### الميزة 1 – التكوين وإعداد الشبكة
تكوين شبكة البحث هو الخطوة الأولى نحو بناء فهرس قابل للبحث.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – الدليل الذي سيتم فيه حفظ بيانات الفهرس.  
- **`basePort`** – المنفذ الابتدائي؛ كل عقدة ستزيد هذا الرقم.

### الميزة 2 – نشر عقد شبكة البحث
نشر العقد يوزع عبء الفهرسة عبر عدة آلات أو عمليات.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

كل `SearchNetworkNode` يشغل خدمة فهرسة خاصة به، مما يتيح لك **إنشاء فهرس قابل للبحث java** يتوسع أفقياً.

### الميزة 3 – الاشتراك في أحداث العقد
التحديثات في الوقت الفعلي تحافظ على تزامن الفهرس مع تغييرات نظام الملفات.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

من خلال الاستماع إلى الأحداث، يمكنك تشغيل إعادة الفهرسة تلقائيًا عند وصول ملفات جديدة.

### الميزة 4 – إضافة أدلة إلى عقدة الشبكة
استخدم هذا المساعد **لإضافة أدلة إلى العقدة**، مع جمع جميع المستندات المدعومة بشكل متكرر.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### الميزة 5 – إضافة ملفات إلى عقدة الشبكة
عند الحاجة إلى تحكم دقيق، **أضف ملفات للبحث** بشكل فردي:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

هذه الطريقة تمنحك المرونة لفهرسة الملفات القادمة من تدفقات، تخزين سحابي، أو مواقع مؤقتة.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|--------|-----|
| **عدم ظهور المستندات في نتائج البحث** | الفهرس غير مُلتزم | استدعِ `node.getIndexer().commit()` بعد إضافة الملفات. |
| **خطأ تعارض المنفذ** | خدمة أخرى تستخدم `basePort` | اختر `basePort` مختلفًا أو تحقق من المنافذ المتاحة. |
| **تنسيق ملف غير مدعوم** | المكتبة لا تحتوي على محلل | تأكد من أن امتداد الملف مدعوم أو أضف مستخرجًا مخصصًا. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام GroupDocs.Search في تطبيق Java سحابي؟**  
ج: نعم. تعمل المكتبة مع أي بيئة تشغيل Java، ويمكنك توجيه `basePath` إلى مجلد مركب على الشبكة أو تخزين سحابي مُركَّب محليًا.

**س: كيف أقوم بتحديث الفهرس عندما يتغير ملف؟**  
ج: اشترك في أحداث العقد (انظر الميزة 3) واستدعِ `addFiles` أو `addDirectories` مرة أخرى للمسارات المعدلة.

**س: هل هناك حد لعدد العقد التي يمكن نشرها؟**  
ج: عمليًا، الحد يُحدَّده العتاد وعرض النطاق الترددي للشبكة. لا يفرض الـ API حدًا ثابتًا.

**س: هل يجب إعادة تشغيل العقد بعد إضافة ملفات جديدة؟**  
ج: لا. إضافة الملفات تُطلق الفهرسة تلقائيًا؛ تحتاج فقط إلى الالتزام إذا أجلت العملية.

**س: ما هي صيغ المستندات المدعومة مباشرةً؟**  
ج: PDFs، DOC/DOCX، XLS/XLSX، PPT/PPTX، TXT، HTML، والعديد من أنواع الصور. راجع الوثائق الرسمية للقائمة الكاملة.

---

**آخر تحديث:** 2025-12-26  
**تم الاختبار مع:** GroupDocs.Search للـ Java 25.4  
**المؤلف:** GroupDocs
---
date: '2026-01-16'
description: تعلم كيفية تكوين شبكة بحث GroupDocs في Java وإضافة المرادفات إلى الفهرس
  لتعزيز كفاءة البحث.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: تكوين شبكة GroupDocs.Search في Java – تحسين البحث
type: docs
url: /ar/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# تكوين شبكة GroupDocs.Search في Java – تعزيز البحث

في التطبيقات المعتمدة على البيانات اليوم، **configure groupdocs search network** هي الخطوة الأساسية لتقديم نتائج سريعة ودقيقة عبر مجموعات ضخمة من المستندات. سواءً كنت تبني بوابة بحث على مستوى المؤسسة أو توسع حلًا موجودًا، فإن شبكة GroupDocs.Search المُكوَّنة جيدًا تتيح لك التوسع أفقيًا، إضافة دعم المرادفات، والحفاظ على انخفاض زمن الاستجابة. في هذا البرنامج التعليمي ستتعلم كيفية إعداد، نشر، وضبط شبكة GroupDocs.Search باستخدام Java، بالإضافة إلى نصائح عملية لإضافة المرادفات إلى الفهرس وإدارة دورات حياة العقد.

## إجابات سريعة
- **ما الفائدة الأساسية من تكوين شبكة GroupDocs.Search؟** يتيح ذلك الفهرسة والاستعلام الموزع، مما يحسن الأداء وقابلية التوسع.  
- **هل أحتاج إلى ترخيص لتشغيل الأمثلة؟** الإصدار التجريبي المجاني يكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكن إضافة المرادفات دون إعادة بناء الفهرس؟** نعم—استخدم قاموس المرادفات في وقت التشغيل **add synonyms to index**.  
- **كم عدد العقد التي يمكنني نشرها؟** يمكنك نشر عدد العقد التي تسمح به بنية تحتية الخاصة؛ كل عقدة تعمل على منفذ خاص بها.  

## ما هو تكوين شبكة GroupDocs.Search؟
تكوين شبكة GroupDocs.Search يعني تعريف هيكل المجلدات، المنافذ، وإعدادات العقد التي تسمح لعدة مثيلات JVM بالتعاون في الفهرسة والبحث. هذا الإعداد ينشئ عقدة رئيسية تُنسق العاملين (shards) وتضمن تنفيذ الاستعلامات عبر مجموعة البيانات بالكامل.

## لماذا نكوّن شبكة GroupDocs.Search؟
- **قابلية التوسع** – توزيع حمل الفهرسة عبر عدة آلات.  
- **الموثوقية** – يمكن إضافة أو إزالة العقد دون توقف.  
- **ملاءمة البحث** – إضافة مرادفات إلى الفهرس للحصول على نتائج أغنى.  
- **الأداء** – تنفيذ الاستعلامات بشكل متوازي يقلل من زمن الاستجابة.

## المتطلبات المسبقة
- مجموعة تطوير جافا (JDK) 8 أو أحدث  
- Maven لبناء المشروع  
- إلمام أساسي بصياغة Java  
- الوصول إلى مكتبة GroupDocs.Search for Java (تنزيل عبر Maven أو صفحة الإصدار الرسمية)

## إعداد GroupDocs.Search لـ Java

أضف المستودع والاعتماد إلى ملف **pom.xml** الخاص بـ Maven:

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

بدلاً من ذلك، حمّل أحدث نسخة مباشرة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **الإصدار التجريبي** – استكشف الميزات الأساسية دون تكلفة.  
- **ترخيص مؤقت** – افتح جميع القدرات لاختبار قصير‑الأمد.  
- **ترخيص تجاري** – مطلوب للنشر في بيئات الإنتاج.

### التهيئة الأساسية والإعداد
أنشئ فئة Java بسيطة للتحقق من تحميل المكتبة بشكل صحيح:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## دليل خطوة بخطوة لتكوين شبكة GroupDocs.Search

### 1. تكوين شبكة البحث
حدد مجلد المستندات الأساسي ومنفذ البدء للتواصل بين العقد.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – حيث توجد القواميس (مثل ملفات المرادفات).  
- **basePort** – المنفذ الأول؛ العقد اللاحقة تزداد من هذه القيمة.

### 2. نشر عقد شبكة البحث
شغّل عدة عقد عاملية تشترك في نفس الإعداد.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

كل عقدة تعمل على منفذ خاص بها (basePort + index) وتحمل جزءًا من الفهرس الكلي.

### 3. الاشتراك في أحداث العقد
راقب الصحة، تقدم الفهرسة، وحالات الخطأ عبر ربط مستمع أحداث بالعقدة الرئيسية.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

تتيح ردود الفعل على الأحداث لك التفاعل مع بدء/إيقاف العقدة، إكمال الفهرسة، والفشل غير المتوقع.

### 4. إضافة مرادفات إلى فهرس العقدة  
حسّن الملاءمة عبر **add synonyms to index** في وقت التشغيل.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – مصفوفة من المصطلحات التي يجب اعتبارها مكافئة.  
- **clearBeforeAdding** – اضبطها على `true` إذا رغبت في استبدال الإدخالات الحالية.

### 5. إضافة أدلة للفهرسة
أخبر العقدة الرئيسية أي مجلدات تحتوي على المستندات التي تريد جعلها قابلة للبحث.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

تقوم الطريقة بمسح الدليل بشكل متكرر وتوزيع الملفات عبر الأجزاء.

### 6. تنفيذ بحث نصي في الشبكة
نفّذ استعلامًا عبر جميع العقد، مع إمكانية فرض سلوك التطابق الدقيق.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

غيّر `exactMatchOnly` إلى `true` عندما تحتاج إلى مطابقة صريحة للمصطلحات دون تجذير.

### 7. إغلاق عقد الشبكة
حرّر الموارد بشكل سليم بمجرد انتهاء المعالجة.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

الإغلاق الصحيح يمنع تسرب الذاكرة ويحافظ على صحة JVM.

## تطبيقات عملية
| السيناريو | كيف تساعد الشبكة |
|----------|-------------------|
| **بحث مؤسسي** | توزيع الفهرسة عبر خوادم مركز البيانات لمجموعات بيانات بحجم بيتابايت. |
| **إدارة المستندات** | إضافة مرادفات إلى الفهرس بحيث يجد المستخدمون المستندات حتى مع اختلاف المصطلحات. |
| **كتالوج التجارة الإلكترونية** | نشر عقد إقليمية لتقديم عمليات بحث منتجات محلية بسرعة. |
| **إدارة المحتوى** | الحفاظ على قابلية البحث للمحتوى بينما يضيف المحررون ملفات جديدة إلى أدلة محددة. |

## المشكلات الشائعة والحلول
- **تعارض المنافذ** – تأكد من أن منفذ كل عقدة (basePort + index) متاح؛ عدّل `basePort` إذا لزم الأمر.  
- **المرادف غير مطبق** – تحقق من أنك استدعيت `indexer.setDictionary(dictionary)` بعد إضافة المصطلحات.  
- **العقدة لا تستجيب** – اشترك في الأحداث؛ ابحث عن ردود `NodeFailed` لتشخيص مشاكل الشبكة.  
- **تسرب الذاكرة عند الإغلاق** – استدعِ دائمًا `node.close()` لكل عقدة تم نشرها.

## الأسئلة المتكررة

**س: كيف يحسن نشر عدة عقد أداء البحث؟**  
ج: كل عقدة تفهرس جزءًا من البيانات، مما يسمح بالمعالجة المتوازية وتقليل زمن الاستجابة لأن الحمل يُوزَّع.

**س: هل يمكن إضافة مرادفات دون إعادة فهرسة المستندات الموجودة؟**  
ج: نعم، يمكنك **add synonyms to index** في وقت التشغيل عبر قاموس المرادفات؛ التغييرات تُطبق فورًا على الاستعلامات الجديدة.

**س: هل الاشتراك في أحداث العقد إلزامي؟**  
ج: ليس ضروريًا للتشغيل الأساسي، لكن الاشتراك يمنحك رؤية حول صحة العقد ويساعدك على الاستجابة للفشل بسرعة.

**س: ما هي أفضل الممارسات لإدارة موارد العقد؟**  
ج: أغلق العقد غير النشطة بانتظام، راقب استهلاك ذاكرة JVM، وأعد تدوير العقد خلال فترات انخفاض النشاط للحفاظ على استهلاك موارد مثالي.

**س: هل يدعم GroupDocs.Search صيغ غير نصية مثل PDFs أو الصور؟**  
ج: بالتأكيد. المكتبة تستخرج النص من ملفات PDF، ملفات Office، وتقوم أيضًا بعملية OCR على الصور لتصبح قابلة للبحث مباشرة.

---

**آخر تحديث:** 2026-01-16  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs
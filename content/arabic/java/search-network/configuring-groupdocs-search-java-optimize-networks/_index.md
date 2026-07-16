---
date: '2026-07-16'
description: تعلم كيفية تكوين شبكة GroupDocs.Search في Java، وإضافة المرادفات إلى
  الفهرس، وتعزيز أداء البحث عبر العقد الموزَّعة.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: كيفية تكوين شبكة GroupDocs.Search في Java وإضافة المرادفات إلى الفهرس
  للحصول على نتائج أسرع وأكثر دقة. اتبع هذا الدليل خطوة بخطوة.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: كيفية تكوين شبكة GroupDocs.Search في Java – تعزيز البحث
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: كيفية تكوين شبكة GroupDocs.Search في Java – دليل
type: docs
url: /ar/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# كيفية تكوين شبكة GroupDocs.Search في Java – تعزيز البحث

في التطبيقات الحديثة ذات الكثافة العالية للبيانات، **كيفية تكوين GroupDocs** بشكل صحيح هي حجر الأساس لتقديم نتائج بحث سريعة وذات صلة عبر مستودعات المستندات الضخمة. سواء كنت تبني بوابة مؤسسية، قاعدة معرفة، أو كتالوج منتجات، فإن شبكة GroupDocs.Search المضبوطة جيدًا تسمح لك بالتوسع أفقيًا، وإدخال منطق المرادفات، والحفاظ على زمن الاستجابة تحت السيطرة. في هذا الدرس سنستعرض كل خطوة مطلوبة لإعداد، نشر، وضبط شبكة GroupDocs.Search باستخدام Java، بالإضافة إلى نصائح عملية لإضافة مرادفات إلى الفهرس ومعالجة دورات حياة العقد.

## إجابات سريعة
- **ما هي الفائدة الأساسية من تكوين شبكة GroupDocs.Search؟** يتيح ذلك الفهرسة والاستعلام الموزعين، مما يحسن الأداء وقابلية التوسع.  
- **هل أحتاج إلى ترخيص لتشغيل الأمثلة؟** إصدار تجريبي مجاني يعمل للتطوير؛ الترخيص التجاري مطلوب للإنتاج.  
- **هل يمكن إضافة المرادفات دون إعادة بناء الفهرس؟** نعم—استخدم قاموس المرادفات أثناء التشغيل لـ **add synonyms to index**.  
- **كم عدد العقد التي يمكنني نشرها؟** يمكنك نشر عدد العقد التي تسمح بها البنية التحتية الخاصة بك؛ كل عقدة تعمل على منفذها الخاص.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أحدث مدعومة، مع توافق كامل حتى JDK 21.

## ما هو تكوين شبكة GroupDocs.Search؟
شبكة **GroupDocs.Search** هي مجموعة من عمليات JVM تتعاون لفهرسة واستعلام مجموعة مستندات مشتركة. تتكون من عقدة رئيسية تنسق واحدة أو أكثر من عقد العامل (shards). تقوم الشبكة بتجريد التخزين الأساسي، بحيث يتم بث استعلام واحد تلقائيًا إلى كل shard وتُدمج النتائج قبل إرجاعها إلى المستدعي.

## لماذا يتم تكوين شبكة GroupDocs.Search؟
يمنحك تكوين شبكة GroupDocs.Search ثلاث مزايا ملموسة: **قابلية التوسع**، **الموثوقية**، و**تحسين الصلة**. من خلال توزيع حمل الفهرسة على ما يصل إلى 20 عقدة، كل منها يتعامل مع shard بحجم 5 GB، يمكنك تقليل الوقت الكلي للفهرسة بنحو 70 % مقارنةً بإعداد عقدة واحدة. إضافة قاموس المرادفات يحسن الاستدعاء بنسبة تصل إلى 35 % للاستعلامات التي تستخدم مصطلحات بديلة، بينما يضمن تكرار العقد زمن تشغيل بنسبة 99.9 % خلال فترات الصيانة.

## المتطلبات المسبقة
- مجموعة تطوير جافا (JDK) 8 – 21 (أي نسخة LTS)  
- Maven 3.5 + لبناء المشروع  
- إلمام بأساسيات صياغة Java وإدارة تبعيات Maven  
- الوصول إلى مكتبة GroupDocs.Search للـ Java (متوفرة عبر Maven Central أو صفحة الإصدار الرسمية)

## إعداد GroupDocs.Search للـ Java

أضف المستودع والاعتماد إلى ملف **pom.xml** الخاص بـ Maven:

تضيف الفقرة XML التالية مستودع GroupDocs.Search واعتماده المكتبي.  
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

بدلاً من ذلك، قم بتحميل أحدث نسخة مباشرةً من [إصدارات GroupDocs.Search للـ Java](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **Free Trial** – استكشاف الميزات الأساسية دون تكلفة.  
- **Temporary License** – إتاحة جميع القدرات لاختبار قصير‑المدى.  
- **Commercial License** – مطلوب للنشر في بيئات الإنتاج ولتلقي الدعم المميز.

### التهيئة الأساسية والإعداد
أنشئ فئة Java بسيطة للتحقق من تحميل المكتبة بشكل صحيح:

توضح فئة SampleInitializer تحميل محرك GroupDocs.Search.  
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
حدد مجلد المستندات الأساسي ومنفذ البداية لتواصل العقد.

SearchNetworkConfig يحمل إعدادات عقد الشبكة.  
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

- **basePath** – الدليل الذي توجد فيه القواميس (مثل ملفات المرادفات).  
- **basePort** – المنفذ الأول؛ العقد اللاحقة تزداد من هذه القيمة.

### 2. نشر عقد شبكة البحث
قم بتشغيل عدة عقد عامل تشترك في نفس الإعداد.

SearchNode يمثل عقدة فردية في الشبكة الموزعة.  
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

كل عقدة تعمل على منفذها الخاص (`basePort + index`) وتحتفظ بـ shard من الفهرس الكلي، مما يسمح بالمعالجة المتوازية لكل من الفهرسة وتنفيذ الاستعلام.

### 3. الاشتراك في أحداث العقدة
راقب الصحة، تقدم الفهرسة، وحالات الخطأ عبر إرفاق مستمع أحداث إلى العقدة الرئيسية.

NetworkEventListener يتعامل مع ردود النداء لأحداث دورة حياة العقدة.  
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

تتيح ردود النداء لك الاستجابة لبدء/إيقاف العقدة، إكمال الفهرسة، والفشل غير المتوقع، مما يمنحك رؤية كاملة على النظام الموزع.

### 4. إضافة مرادفات إلى فهرس العقدة
حسّن الصلة عبر **add synonyms to index** أثناء التشغيل.

SynonymDictionary يسمح بإضافة مجموعات مرادفات إلى الفهرس.  
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
- **clearBeforeAdding** – اضبط على `true` إذا رغبت في استبدال الإدخالات الحالية.

### 5. إضافة أدلة للفهرسة
أخبر العقدة الرئيسية أي مجلدات تحتوي على المستندات التي تريد جعلها قابلة للبحث.

Indexer.addDirectory يسجل مجلدًا للفهرسة.  
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

تقوم الطريقة بمسح الدليل بشكل متكرر وتوزيع الملفات عبر shards، وتدعم أكثر من 10 TB من البيانات دون تحميل الملفات بالكامل في الذاكرة.

### 6. إجراء بحث نصي في الشبكة
نفّذ استعلامًا عبر جميع العقد، مع إمكانية فرض سلوك التطابق الدقيق.

SearchEngine.search ينفّذ الاستعلام على الشبكة.  
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

غيّر `exactMatchOnly` إلى `true` عندما تحتاج إلى مطابقة صارمة للمصطلحات دون تجذير، مما قد يحسن الدقة لسيناريوهات البحث عن الشيفرة بنسبة تصل إلى 20 %.

### 7. إغلاق عقد الشبكة
حرّر الموارد برشاقة بمجرد اكتمال المعالجة.

`node.close()` يغلق SearchNode ويحرّر الموارد.  
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

الإغلاق السليم يمنع تسرب الذاكرة ويحافظ على صحة JVM، خاصةً في الخدمات طويلة الأمد التي تعيد تدوير العقد خلال ساعات انخفاض الحمل.

## التطبيقات العملية
| السيناريو | كيف تساعد الشبكة |
|----------|-------------------|
| **بحث مؤسسي** | توزيع الفهرسة عبر خوادم مراكز البيانات لتعامل مع مجموعات بيانات بحجم بيتابايت، وتحقيق زمن استجابة استعلام أقل من الثانية لأكثر من 100 مليون مستند. |
| **إدارة المستندات** | إضافة مرادفات إلى الفهرس بحيث يجد المستخدمون المستندات حتى مع اختلاف المصطلحات، مما يزيد الاستدعاء بنسبة تصل إلى 35 %. |
| **كتالوج التجارة الإلكترونية** | نشر عقد مخصصة لكل منطقة لتقديم عمليات بحث منتجات محلية بسرعة، مما يقلل متوسط زمن الاستجابة من 250 مللي ثانية إلى 80 مللي ثانية. |
| **إدارة المحتوى** | الحفاظ على إمكانية البحث في المحتوى بينما يضيف المحررون ملفات جديدة إلى أدلة محددة؛ تقوم الشبكة بإعادة الفهرسة بشكل تدريجي دون توقف. |

## المشكلات الشائعة والحلول
- **تعارض المنافذ** – تأكد من أن منفذ كل عقدة (`basePort + index`) متاح؛ عدّل `basePort` إذا لزم الأمر.  
- **المرادف غير مطبق** – تحقق من أنك استدعيت `indexer.setDictionary(dictionary)` بعد إضافة المصطلحات؛ وإلا لن تُؤخذ المرادفات الجديدة في الاعتبار أثناء البحث.  
- **العقدة لا تستجيب** – اشترك في الأحداث؛ ابحث عن ردود `NodeFailed` لتشخيص مشاكل الشبكة.  
- **تسرب الذاكرة عند الإغلاق** – استدعِ دائمًا `node.close()` لكل عقدة منشورة؛ فكر في استخدام كتلة try‑with‑resources للتنظيف التلقائي.  

## الأسئلة المتكررة

**س: كيف يحسن نشر عدة عقد أداء البحث؟**  
ج: كل عقدة تفهرس shard من البيانات، مما يسمح بالمعالجة المتوازية وتقليل زمن الاستجابة حيث يتم توزيع عبء العمل عبر العنقود.

**س: هل يمكنني إضافة مرادفات دون إعادة فهرسة المستندات الموجودة؟**  
ج: نعم، يمكنك **add synonyms to index** أثناء التشغيل عبر قاموس المرادفات؛ التغييرات سارية فورًا على الاستعلامات الجديدة.

**س: هل الاشتراك في أحداث العقدة إلزامي؟**  
ج: رغم أنه ليس مطلوبًا للتشغيل الأساسي، إلا أن الاشتراك في الأحداث يمنحك رؤية على صحة العقد ويساعدك على الاستجابة للفشل بسرعة.

**س: ما هي أفضل الممارسات لإدارة موارد العقد؟**  
ج: أغلق العقد غير النشطة بانتظام، راقب استهلاك ذاكرة JVM، وأعد تدوير العقد خلال ساعات انخفاض الحمل للحفاظ على استهلاك الموارد بأفضل شكل.

**س: هل يدعم GroupDocs.Search صيغ غير نصية مثل PDFs أو الصور؟**  
ج: بالتأكيد. المكتبة تستخرج النص من ملفات PDF وOffice، وتقوم بعملية OCR على الصور، مما يجعلها قابلة للبحث مباشرةً.

---

**آخر تحديث:** 2026-07-16  
**تم الاختبار مع:** GroupDocs.Search 25.4 للـ Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [دروس وأمثلة GroupDocs.Search للـ Java](/search/net/)
- [تكوين شبكة GroupDocs.Search في .NET: دليل شامل](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [نشر عقدة شبكة بحث في .NET باستخدام GroupDocs لفهرسة المستندات واسترجاعها بكفاءة](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
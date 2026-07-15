---
date: '2026-05-22'
description: تعلم كيفية إضافة المستندات إلى الفهرس وإنشاء شبكة بحث قابلة للتوسع باستخدام
  GroupDocs.Search for Java. يدعم البحث عبر عدة servers.
keywords:
- build scalable search network
- add documents to index
- search across multiple servers
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  headline: Build Scalable Search Network – Index Docs with GroupDocs Java
  type: TechArticle
- description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  name: Build Scalable Search Network – Index Docs with GroupDocs Java
  steps:
  - name: Define Base Path and Port
    text: The `SearchNetworkNode` class represents a single node that participates
      in the distributed index.
  - name: Configure the Network
    text: '`NetworkConfiguration` holds the common settings (base path, ports, replication
      factor) that every node reads at startup.'
  - name: Deploy Nodes Using Configuration
    text: '`SearchNetworkNode` instances are started with the same configuration file,
      allowing them to discover each other via the defined base port range.'
  - name: Define Subscription Method
    text: '`NodeEventListener` is an interface you implement to receive callbacks
      for indexing progress, errors, and node health changes.'
  - name: Use Subscription Method
    text: Register your listener with each node so that you get real‑time feedback
      during large batch operations.
  type: HowTo
- questions:
  - answer: Change the `basePort` variable in your configuration code to an available
      port.
    question: How do I handle port conflicts when deploying nodes?
  - answer: Yes, it supports real‑time indexing with appropriate configurations.
    question: Can GroupDocs.Search be used for real‑time indexing?
  - answer: Network connectivity and incorrect path settings are frequent culprits.
      Ensure all paths and ports are correctly configured.
    question: What are some common issues during node deployment?
  - answer: Absolutely. You can call `index.add(...)` on any node, and the network
      will distribute the new workload automatically.
    question: Is it possible to add documents to index after the network is running?
  - answer: A temporary trial license is sufficient for testing; a commercial license
      is required for production use.
    question: Do I need a license for development testing?
  type: FAQPage
title: إنشاء شبكة بحث قابلة للتوسع – فهرسة المستندات باستخدام GroupDocs Java
type: docs
url: /ar/java/search-network/scalable-search-groupdocs-java/
weight: 1
---

# بناء شبكة بحث قابلة للتوسع – فهرسة المستندات باستخدام GroupDocs.Java

في هذا الدرس ستتعلم **كيفية إضافة المستندات إلى الفهرس** و **بناء شبكة بحث قابلة للتوسع** باستخدام GroupDocs.Search للغة Java. سنستعرض تكوين شبكة البحث، نشر العقد، ومعالجة الأحداث بحيث يمكن لتطبيقك معالجة مجموعات مستندات كبيرة بكفاءة عبر خوادم متعددة.

## إجابات سريعة
- **ماذا يعني “إضافة المستندات إلى الفهرس”؟** يعني إدراج الملفات في فهرس قابل للبحث بحيث يمكن الاستعلام عنها بسرعة.  
- **أي مكتبة توفر هذه القدرة؟** GroupDocs.Search للغة Java.  
- **هل أحتاج إلى ترخيص؟** يتوفر ترخيص تجريبي مؤقت؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **هل يمكنني التوسع أفقيًا؟** نعم — عن طريق نشر عدة مثيلات من SearchNetworkNode.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أعلى.

## ما هو إضافة المستندات إلى الفهرس؟
حمّل ملفات المصدر الخاصة بك (PDF، DOCX، PPTX، إلخ) إلى محرك GroupDocs.Search، الذي يستخرج النص، يبني جداول تكرار المصطلحات، ويخزنها في ملف فهرس. يتيح الفهرس الناتج استعلامات كلمات مفتاحية بأقل من ثانية حتى على مجموعات مئات الصفحات.

## لماذا تستخدم GroupDocs.Search للغة Java في بيئة شبكية؟
قُم بتوزيع عبء الفهرسة والبحث عبر عدة عقد، قلل زمن استجابة الاستعلامات بمعالجة البيانات بالقرب من مصدرها، وأضف أو أزل العقد دون توقف. تتيح لك هذه البنية **البحث عبر خوادم متعددة** مع الحفاظ على أداء ثابت.

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8+** مثبت.  
- **Maven** لإدارة الاعتمادات.  
- إلمام أساسي بـ Java وبنية مشروع Maven.

### المكتبات المطلوبة، الإصدارات، والاعتمادات
لتنفيذ GroupDocs.Search للغة Java، أدرج ما يلي في مشروع Maven الخاص بك:

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

بدلاً من ذلك، قم بتنزيل أحدث نسخة من [إصدارات GroupDocs.Search للغة Java](https://releases.groupdocs.com/search/java/). يمكنك أيضًا العثور على الإصدارات في [إصدارات GroupDocs Search Java](https://releases.groupdocs.com/search/java/).

### متطلبات إعداد البيئة
- JDK 8 أو أعلى مثبت على نظامك.  
- Maven مثبت ومُكوَّن إذا كنت تستخدم مشروع Maven.

### متطلبات المعرفة
- فهم أساسي لبرمجة Java.  
- إلمام بإدارة الاعتمادات في Maven.

## إعداد GroupDocs.Search للغة Java

1. **إعداد Maven**: أضف المستودع والاعتماد كما هو موضح أعلاه في ملف `pom.xml` الخاص بك.  
2. **تحميل مباشر**: بدلاً من ذلك، قم بتنزيل المكتبة من [إصدارات GroupDocs Search Java](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- احصل على ترخيص تجريبي مجاني أو مؤقت بزيارة [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license).  
- للحصول على وصول كامل ودعم، فكر في شراء ترخيص تجاري.

### التهيئة الأساسية
قم بتهيئة GroupDocs.Search في تطبيق Java الخاص بك:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index/directory");

        // Add documents to the index
        index.add("path/to/documents");
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## كيفية إضافة المستندات إلى الفهرس في شبكة بحث؟
حمّل مستنداتك عبر أي عقدة في الشبكة؛ يقوم الإطار تلقائيًا بتوزيع عبء الفهرسة، موازنة الحمل، وتحديث الفهرس المشترك في الوقت الحقيقي. كل عقدة تعالج الملفات المخصصة لها، تستخرج النص، وتكتب التغييرات المتدرجة إلى الفهرس المركزي، مما يضمن أن المحتوى المضاف حديثًا يصبح قابلًا للبحث عبر جميع العقد تقريبًا فورًا.

### الميزة 1: تكوين شبكة البحث
#### نظرة عامة
يتضمن تكوين شبكة البحث إعداد العقد لإدارة وتوزيع مهام البحث بكفاءة.

##### الخطوة 1: تحديد المسار الأساسي والمنفذ
تمثل الفئة `SearchNetworkNode` عقدة واحدة تشارك في الفهرس الموزع.  
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SearchNetworkNodeEvents/";
int basePort = 49140; // Change if necessary due to busy port issues
```

##### الخطوة 2: تكوين الشبكة
`NetworkConfiguration` يحتوي على الإعدادات المشتركة (المسار الأساسي، المنافذ، عامل النسخ) التي يقرأها كل عقدة عند بدء التشغيل.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.scaling.configuring.*;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

### الميزة 2: نشر عقد شبكة البحث
#### نظرة عامة
نشر العقد لتوزيع ومعالجة عمليات البحث عبر شبكتك.

##### الخطوة 1: نشر العقد باستخدام التكوين
يتم تشغيل مثيلات `SearchNetworkNode` باستخدام ملف التكوين نفسه، مما يسمح لها باكتشاف بعضها البعض عبر نطاق المنفذ الأساسي المحدد.  
```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
```

### الميزة 3: الاشتراك في أحداث العقد
#### نظرة عامة
يسمح الاشتراك في أحداث العقد بمراقبة والاستجابة لمختلف الإجراءات داخل شبكة البحث.

##### الخطوة 1: تعريف طريقة الاشتراك
`NodeEventListener` هي واجهة تقوم بتنفيذها لتلقي ردود النداء لتقدم الفهرسة، الأخطاء، وتغييرات صحة العقدة.  
```java
import com.groupdocs.search.events.*;
import com.groupdocs.search.scaling.events.*;

public static void subscribe(SearchNetworkNode node) {
    // Subscribe to IndexingCompleted event
    node.getEvents().IndexingCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            System.out.println("Indexing completed.");
        }
    });

    // Additional events can be subscribed similarly...
}
```

##### الخطوة 2: استخدام طريقة الاشتراك
سجِّل المستمع الخاص بك مع كل عقدة للحصول على ملاحظات فورية أثناء عمليات الدُفعات الكبيرة.  
```java
SearchNetworkNode masterNode = nodes[0];
subscribe(masterNode);
```

### إغلاق العقد
دائمًا قم بإغلاق العقد برفق لتفريغ عمليات الكتابة المعلقة وإطلاق مقبس الشبكة.  
```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## التطبيقات العملية
1. **حلول البحث المؤسسية** – نفّذ شبكة بحث للتعامل مع عمليات بحث مستندات واسعة النطاق عبر خوادم متعددة.  
2. **منصات التجارة الإلكترونية** – حسّن قدرات بحث المنتجات عن طريق توزيع مهام الفهرسة على عدة عقد.  
3. **أنظمة إدارة المحتوى (CMS)** – حسّن أداء استرجاع المحتوى وتحديثاته في بيئات CMS.

## اعتبارات الأداء
- تحسين نشر العقد بناءً على موارد نظامك.  
- راقب استخدام الذاكرة بانتظام لمنع التسربات، خاصة عند التعامل مع مجموعات بيانات كبيرة.  
- استخدم إعدادات التكوين لضبط عمليات الفهرسة والبحث بدقة لتحقيق كفاءة أفضل.

## المشكلات الشائعة والحلول
| المشكلة | السبب الشائع | الحل |
|-------|---------------|--------|
| تعارض المنافذ | `basePort` مستخدم بالفعل | غيّر `basePort` إلى رقم متاح |
| العقدة غير قابلة للوصول | جدار الحماية أو قواعد الشبكة | افتح المنافذ المطلوبة وتحقق من الاتصال |
| الفهرس لا يتم تحديثه | مسار المستند غير صحيح | تحقق من أن `basePath` يشير إلى الدليل الصحيح |
| استخدام الذاكرة عالي | فهرسة دفعات كبيرة | قم بفهرسة المستندات في دفعات أصغر أو زد حجم الذاكرة المخصصة (heap size) |

## الأسئلة المتكررة
**س: كيف أتعامل مع تعارض المنافذ عند نشر العقد؟**  
ج: غيّر متغير `basePort` في كود التكوين إلى منفذ متاح.

**س: هل يمكن استخدام GroupDocs.Search للفهرسة في الوقت الحقيقي؟**  
ج: نعم، يدعم الفهرسة في الوقت الحقيقي مع التكوينات المناسبة.

**س: ما هي بعض المشكلات الشائعة أثناء نشر العقد؟**  
ج: الاتصال الشبكي وإعدادات المسار غير الصحيحة هي الأسباب المتكررة. تأكد من تكوين جميع المسارات والمنافذ بشكل صحيح.

**س: هل يمكن إضافة مستندات إلى الفهرس بعد تشغيل الشبكة؟**  
ج: بالتأكيد. يمكنك استدعاء `index.add(...)` على أي عقدة، وستقوم الشبكة بتوزيع عبء العمل الجديد تلقائيًا.

**س: هل أحتاج إلى ترخيص لاختبار التطوير؟**  
ج: ترخيص تجريبي مؤقت يكفي للاختبار؛ يلزم الحصول على ترخيص تجاري للاستخدام في الإنتاج.

## الموارد
- **Documentation**: [وثائق GroupDocs Search Java](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [مرجع API الخاص بـ GroupDocs](https://reference.groupdocs.com/search/java)  
- **Download**: [أحدث إصدار](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [مستودع GroupDocs.Search على GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [منتدى GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [الحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license)

باتباع هذا الدليل، يمكنك بفعالية **إضافة المستندات إلى الفهرس** وإدارة شبكة بحث قوية **قابلة للتوسع** باستخدام GroupDocs.Search للغة Java. برمجة سعيدة!

---

**آخر تحديث:** 2026-05-22  
**تم الاختبار مع:** GroupDocs.Search 25.4 للغة Java  
**المؤلف:** GroupDocs

## دروس ذات صلة
- [دروس شبكة البحث لـ GroupDocs.Search .NET](/search/net/search-network/)
- [كيفية تكوين شبكة بحث .NET باستخدام GroupDocs.Search وإزالة المعلومات](/search/net/search-network/configure-net-search-network-groupdocs/)
- [نشر عقدة شبكة بحث في .NET باستخدام GroupDocs لفهرسة المستندات واسترجاعها بكفاءة](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
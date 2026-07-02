---
date: '2026-07-02'
description: تعلم كيفية الحصول على temporary license لـ GroupDocs.Search، وإضافة directories
  إلى index، وإضافة custom document attributes أثناء إدارة Java search network nodes.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: الحصول على temporary license لـ GroupDocs – Master Search Nodes (Java)
type: docs
url: /ar/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# الحصول على ترخيص مؤقت GroupDocs – عقد البحث الرئيسية (Java)

في هذا الدليل الشامل ستقوم **بالحصول على ترخيص مؤقت لـ GroupDocs.Search**، وتكوين شبكة بحث متعددة العقد، وتعلم كيفية **إضافة أدلة إلى الفهرس** و**إضافة سمات مستند مخصصة** باستخدام Java. سواء كنت تبني نظام إدارة مستندات مؤسسي أو كتالوج منتجات قابل للبحث، فإن إتقان هذه الخطوات يتيح لك تقييم المنصة دون قيود وتوسيع قدرات البحث بسرعة.

## إجابات سريعة
- **ما هي الخطوة الأولى لبدء استخدام GroupDocs.Search؟** الحصول على ترخيص مؤقت من بوابة GroupDocs.  
- **أي مستودع Maven يستضيف المكتبة؟** `https://releases.groupdocs.com/search/java/`.  
- **كيف يمكنني إضافة أدلة إلى الفهرس؟** استدعِ المساعد `addDirectoriesToIndex` على العقدة الرئيسية.  
- **هل يمكنني إضافة سمات مستند مخصصة؟** نعم—استدعِ `addAttribute` مع مفتاح المستند واسم السمة.  
- **كيف يمكن إغلاق العقد بشكل نظيف؟** استدعِ `closeNodes` لتحرير الموارد.

## ما هو الترخيص المؤقت ولماذا أحتاجه؟
يتيح لك الترخيص المؤقت تقييم GroupDocs.Search دون أي قيود على التقييم. إنه مثالي للتطوير أو الاختبار أو مشاريع إثبات المفهوم قبل الالتزام بشراء كامل. يمنح الترخيص وصولًا إلى جميع الميزات لفترة محدودة، مما يسمح لك بقياس الأداء، واختبار نقاط التكامل، وضمان أن الحل يلبي متطلباتك دون التزام مالي.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر المتطلبات التالية:

### المكتبات والاعتمادات المطلوبة
للعمل مع GroupDocs.Search لـ Java، أدرج الاعتمادات اللازمة في Maven:
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
يمكنك أيضًا تنزيل أحدث نسخة مباشرةً من [إصدارات GroupDocs.Search لـ Java](https://releases.groupdocs.com/search/java/).

### إعداد البيئة
- تأكد من تثبيت JDK متوافق (Java 8 أو أحدث).  
- قم بإعداد بيئة التطوير المتكاملة (IDE) لدعم مشاريع Maven.

### المتطلبات المعرفية
ستكون معرفة أساسية ببرمجة Java وإلمام بإدارة مشاريع Maven مفيدة. إذا كنت جديدًا على هذه المفاهيم، فكر في استكشاف موارد تمهيدية للبدء.

## كيفية الحصول على ترخيص مؤقت
يتم الحصول على ترخيص مؤقت بزيارة بوابة GroupDocs، وإكمال نموذج طلب قصير، ووضع ملف `.lic` المستلم في مجلد `resources` الخاص بمشروعك. ثم قم بتهيئة الترخيص ببضع أسطر من الشيفرة (انظر المقتطف أدناه). لاستخدام نموذج الطلب، استخدم الصفحة الرسمية: [ترخيص GroupDocs المؤقت](https://purchase.groupdocs.com/temporary-license/).

## إعداد GroupDocs.Search لـ Java

### معلومات التثبيت
لبدء استخدام GroupDocs.Search لـ Java في مشروعك، اتبع خطوات Maven المذكورة أعلاه أو قم بتنزيل أحدث نسخة مباشرةً من صفحة الإصدارات الرسمية.

#### خطوات الحصول على الترخيص
1. **تجربة مجانية** – استكشف الميزات دون أي التزام.  
2. **ترخيص مؤقت** – احصل على مفتاح قصير الأجل للاختبار (انظر القسم أعلاه).  
3. **شراء** – للاستخدام في الإنتاج، اشترِ ترخيصًا كاملاً من **[صفحة شراء GroupDocs](https://purchase.groupdocs.com/)**.

### التهيئة الأساسية والإعداد
قم بتهيئة مشروعك باستخدام GroupDocs.Search كما يلي:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
هذه الخطوة التهيئية ضرورية لضمان عمل جميع المكونات بسلاسة داخل شبكة البحث الخاصة بك.

## دليل التنفيذ
الآن، دعنا نقسم العملية إلى أقسام قابلة للإدارة، كل منها يركز على ميزة محددة لنشر وإدارة عقد شبكة البحث.

### الميزة 1: إعداد التكوين
**نظرة عامة:** إعداد التكوين لشبكة البحث الخاصة بك هو الخطوة الأولى في نشر العقد. يتضمن هذا الإعداد تحديد المسارات والمنافذ الحرجة لنشر العقد.

#### خطوات التنفيذ:
##### الخطوة 1: تعريف المسار الأساسي والمنفذ
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### الخطوة 2: تكوين شبكة البحث
دالة `configureSearchNetwork` تُعدّ كائن التكوين الضروري لنشر العقد.  
`Configuration` هي فئة تحتفظ بجميع الإعدادات مثل مجلد الفهرس، ومنافذ الشبكة، وأدوار العقد.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **المعلمات:** يُستخدم المسار الأساسي والمنفذ لتحديد الموارد وإنشاء قنوات الاتصال.  
- **قيمة الإرجاع:** كائن `Configuration` مُكوَّن وفقًا لاحتياجات النشر الخاصة بك.

### الميزة 2: نشر شبكة البحث
**نظرة عامة:** نشر العقد أمر أساسي لتوسيع قدرات البحث عبر بيئات أو أقسام بيانات مختلفة.

#### خطوات التنفيذ:
##### الخطوة 1: نشر العقد
دالة `deploySearchNetwork` تُهيئ وتُعيد مصفوفة من عقد شبكة البحث.  
`SearchNetworkNodes` تمثل كل مثال عقدة يشارك في مجموعة البحث الموزعة.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **المعلمات:** يُستخدم المسار الأساسي، والمنفذ، والتكوين لتحديد بيئة النشر.  
- **قيمة الإرجاع:** مصفوفة تحتوي على `SearchNetworkNodes` المُهيأة.

### الميزة 3: الاشتراك في أحداث الشبكة
**نظرة عامة:** مراقبة أنشطة شبكة البحث أمر حاسم للحفاظ على الأداء والموثوقية المثلى.

#### خطوات التنفيذ:
##### الخطوة 1: الاشتراك في أحداث العقدة الرئيسية
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **الغرض:** تضمن هذه الخطوة إعلامك بالأحداث أو التغييرات الهامة داخل شبكة البحث الخاصة بك.

### الميزة 4: فهرسة المستندات
**نظرة عامة:** إضافة أدلة تحتوي على مستندات لتُفهرس يسمح باسترجاع بيانات فعال عبر شبكتك.

#### كيفية إضافة أدلة إلى الفهرس
`addDirectoriesToIndex` هي طريقة مساعدة تسجل مسارات المجلد للفهرسة على العقدة الرئيسية.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **الغرض:** يسهل الوصول السريع وقابلية البحث لجميع المستندات داخل الأدلة المحددة.

### الميزة 5: إضافة سمات إلى المستندات
**نظرة عامة:** السمات المخصصة تعزز بيانات المستند الوصفية، مما يجعل عمليات البحث أكثر مرونة وإفادة.

#### كيفية إضافة سمات مستند مخصصة
`addAttribute` يضيف سمة بيانات وصفية مخصصة إلى مستند محدد في الفهرس.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **المعلمات:** حدد العقدة، ومفتاح المستند، والسمة التي سيتم إضافتها.  
- **الغرض:** يوسّع وظيفة البحث من خلال إغناء المستندات ببيانات وصفية إضافية.

### الميزة 6: استرجاع المستندات المفهرسة
**نظرة عامة:** استرجاع وقائمة المستندات المفهرسة بكفاءة لضمان دقة واكتمال البيانات.

#### خطوات التنفيذ:
##### الخطوة 1: الحصول على المستندات المفهرسة
```java
getIndexedDocuments(nodes[0]);
```  
- **الغرض:** يتحقق من نجاح فهرسة جميع المستندات الضرورية داخل شبكة البحث الخاصة بك.

### الميزة 7: إغلاق عقد الشبكة
**نظرة عامة:** إغلاق العقد بشكل صحيح أمر حاسم لإدارة الموارد ومنع تسرب الذاكرة.

#### خطوات التنفيذ:
##### الخطوة 1: إغلاق جميع العقد
`closeNodes` يغلق جميع عقد البحث النشطة ويحرّر الموارد المخصصة.  
```java
closeNodes(nodes);
```  
- **الغرض:** يحرّر الموارد التي تحتلها كل عقدة، مما يضمن عملية إغلاق نظيفة.

## لماذا استخدام ترخيص مؤقت لـ GroupDocs.Search؟
يوفر الترخيص المؤقت **وصولًا إلى جميع الميزات لمدة 30 يومًا** ويدعم حتى **50,000 مستند مفهرس** دون تقليل الأداء. يتيح لك ذلك قياس سرعة الفهرسة، وزمن استجابة الاستعلام، وقابلية التوسع على بيانات واقعية قبل شراء ترخيص إنتاجي. كما يزيل العلامات المائية للتقييم، مما يمنحك تمثيلًا حقيقيًا لقدرات المنتج النهائي.

## حالات الاستخدام الشائعة
1. **إدارة المستندات المؤسسية** – فهرسة ملايين الملفات الداخلية عبر الأقسام، مما يتيح بحثًا نصيًا كاملًا فوريًا.  
2. **منصات التجارة الإلكترونية** – بناء كتالوج منتجات قابل للبحث يمتد عبر مستودعات متعددة ومصادر طرف ثالث.  
3. **مكاتب المحاماة** – تنظيم ملفات القضايا والعقود والأدلة باستخدام بيانات وصفية مخصصة للاسترجاع السريع.

تشمل إمكانيات التكامل مع أنظمة أخرى منصات CRM، وأنظمة إدارة المحتوى (CMS)، وأدوات تحليل البيانات، مستفيدًا من ميزات الفهرسة والبحث القوية التي توفرها GroupDocs.Search لـ Java.

## اعتبارات الأداء
لتحسين الأداء عند استخدام GroupDocs.Search لـ Java:
- **تحسين التكوين** – خصص إعدادات التكوين لتتناسب مع بيئة النشر المحددة الخاصة بك.  
- **مراقبة استخدام الموارد** – تحقق بانتظام من وحدة المعالجة المركزية والذاكرة ومدخلات/مخرجات النظام لمنع الاختناقات أو تسرب الذاكرة.  
- **اتباع أفضل الممارسات** – الالتزام بإرشادات إدارة الذاكرة في Java، لضمان استخدام فعال لموارد النظام.

## الأسئلة المتكررة

**س: كم من الوقت يبقى الترخيص المؤقت صالحًا؟**  
ج: عادةً ما تكون التراخيص المؤقتة صالحة لمدة 30 يومًا، مما يمنحك وقتًا كافيًا لتقييم المنتج.

**س: هل يمكنني التحويل من ترخيص مؤقت إلى ترخيص كامل دون إعادة تثبيت؟**  
ج: نعم—استبدل ملف الترخيص المؤقت بملف الترخيص الكامل وأعد تشغيل التطبيق.

**س: هل أحتاج إلى إعادة فهرسة المستندات بعد تطبيق ترخيص جديد؟**  
ج: لا، يظل الفهرس سليمًا؛ الترخيص يتحكم فقط في حقوق الاستخدام.

**س: ماذا يحدث إذا نسيت إغلاق العقد؟**  
ج: قد تؤدي الموارد غير المُحررة إلى تسرب الذاكرة؛ احرص دائمًا على استدعاء `closeNodes` أثناء الإغلاق.

**س: هل يمكن إضافة أكثر من سمة مخصصة لكل مستند؟**  
ج: بالتأكيد—استدعِ `addAttribute` عدة مرات بأسماء سمات مختلفة.

---

**آخر تحديث:** 2026-07-02  
**تم الاختبار مع:** GroupDocs.Search لـ Java 25.4  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [نشر عقدة شبكة بحث في .NET باستخدام GroupDocs لفهرسة المستندات واسترجاعها بفعالية](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [كيفية تنفيذ شبكة بحث باستخدام GroupDocs.Search في .NET لأنظمة إدارة المستندات](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [تكوين شبكة Aspose.Search وإضافة سمات المستندات باستخدام GroupDocs.Redaction لـ .NET: دليل شامل](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
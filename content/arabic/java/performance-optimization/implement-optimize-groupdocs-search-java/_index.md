---
date: '2026-07-07'
description: تعلم كيفية حذف الفهرس، وإجراء بحث نصي كامل في Java، وتحسين أداء البحث
  باستخدام GroupDocs.Search for Java. دليل خطوة بخطوة مع إعداد الشبكة والفهرسة.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: كيفية حذف الفهرس وإجراء بحث نصي كامل في Java باستخدام GroupDocs.Search.
  اتبع هذا الدليل لإعداد شبكة بحث، وإنشاء فهرس قابل للبحث، وتحسين أداء البحث.
og_title: كيفية حذف الفهرس وإجراء بحث نصي باستخدام GroupDocs.Search for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: كيفية حذف الفهرس وإجراء بحث نصي باستخدام GroupDocs.Search for Java
type: docs
url: /ar/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# كيفية حذف الفهرس وإجراء بحث نصي باستخدام GroupDocs.Search للـ Java

في عالم اليوم القائم على البيانات، فإن **how to delete index** بسرعة مع الاستمرار في تقديم قدرات بحث نصي كامل سريعة للغاية في Java يُعد ميزة تنافسية. سواء كنت تبني قاعدة معرفة داخلية، أو مستودع قضايا قانونية، أو كتالوج منتجات للتجارة الإلكترونية، فإن شبكة البحث المُضبوطة جيدًا يمكنها تحسين رضا المستخدم بشكل كبير. في هذا الدليل ستتعلم كيفية **set up a search network**، **create a searchable index**، **optimize search performance**، و **delete documents from the index** عند الحاجة — كل ذلك باستخدام GroupDocs.Search للـ Java.

## إجابات سريعة
- **What is the main purpose of GroupDocs.Search for Java?** يوفر بحثًا نصيًا كاملًا عبر أكثر من 50 تنسيق مستند، مما يتيح استرجاع الكلمات المفتاحية بسرعة.  
- **How do I perform text search in a distributed environment?** نشر شبكة بحث، فهرسة المستندات على عقدة رئيسية، ثم الاستعلام من أي عقدة.  
- **Can I delete documents from the index without rebuilding it?** نعم، استخدم Delete API لإزالة الملفات المحددة، مما يحقق *how to delete index* دون الحاجة إلى إعادة فهرسة كاملة.  
- **What Java version is required?** JDK 8 أو أعلى.  
- **Is a license needed for production?** يتطلب ترخيص صالح لـ GroupDocs.Search؛ يتوفر نسخة تجريبية مجانية.

## ما هو “perform text search”؟
يعني إجراء بحث نصي الاستعلام عن فهرس نص كامل لاسترجاع المستندات التي تحتوي على الكلمات المفتاحية أو العبارات المحددة. تقوم GroupDocs.Search بإنشاء فهرس عكسي يجعل هذه عمليات البحث سريعة للغاية، حتى عبر آلاف الملفات.

## لماذا إعداد شبكة بحث؟
توزع شبكة البحث مهام الفهرسة والاستعلام عبر عدة عقد، مما يتيح لك **optimize search performance**، التوسع أفقيًا، والحفاظ على توافر عالي. هذه البنية مثالية لمستودعات المستندات على مستوى المؤسسات حيث تكون الكمون ومعدل النقل مهمين.

## كيفية تنفيذ وتحسين شبكة بحث باستخدام GroupDocs.Search للـ Java
حمّل تكوينك، ابدأ عقدة رئيسية، ثم أضف عقد عمل تشترك في نفس مسار القاعدة والمنفذ. يتيح نشر الشبكة بهذه الطريقة لأي عقدة معالجة طلبات الفهرسة أو الاستعلام، مما يوفر أوقات استجابة ثابتة حتى مع زيادة عدد المستندات إلى مئات الآلاف.

### نظرة عامة خطوة بخطوة
1. **Define a base configuration** التي تشمل دليلًا مشتركًا ومنفذ TCP.  
2. **Start the master node** لإدارة الفهرس وتنسيق عقد العمل.  
3. **Add worker nodes** التي تتصل بالرئيسية، مما يتيح الفهرسة والبحث المتوازي.  
4. **Monitor resource usage** وضبط إعدادات ذاكرة JVM للحفاظ على انخفاض الكمون.

## كيفية حذف الفهرس في GroupDocs.Search للـ Java
`SearchNode` يمثل عقدة في شبكة GroupDocs.Search التي تدير عمليات الفهرسة والاستعلام. طريقة `delete` تزيل المستندات المحددة من الفهرس.

### خطوات الحذف المباشر
- استدعِ طريقة `delete` على كائن `SearchNode`.  
- قدّم مصفوفة من مسارات الملفات النسبية.  
- قم بارتكاب التغييرات؛ يتم تحديث الفهرس فورًا ولا تعيد عمليات البحث اللاحقة الملفات التي تم إزالتها.

## ما هي شبكة البحث؟
**search network** هي مجموعة من العقد المترابطة التي تشترك في مستودع فهرس مشترك، مما يسمح بالفهرسة الموزعة وتنفيذ الاستعلامات. تمكّن من التوسع الأفقي وتحمل الأخطاء لمجموعات المستندات الكبيرة.

## كيفية إنشاء فهرس قابل للبحث (index documents java)
طريقة `add` تقوم بفهرسة مستند في فهرس البحث. أضف المستندات إلى العقدة الرئيسية باستخدام طريقة `add`؛ تقوم الشبكة بنشر التغييرات إلى جميع عقد العمل. يضمن هذا النهج أن كل عقدة يمكنها خدمة الاستعلامات ضد أحدث فهرس دون خطوات مزامنة إضافية.

### الإجراءات الرئيسية
- وجه العقدة الرئيسية إلى المجلد الذي يحتوي على الملفات المصدر.  
- استدعِ روتين الفهرسة؛ تقوم الشبكة بمعالجة كل ملف وتحديث الفهرس العكسي.  
- تحقق من ظهور ملفات الفهرس في دليل التخزين المحدد.

## كيفية إزالة الملفات المفهرسة (remove indexed files)
عندما يصبح المستند غير صالح، استدعِ API `delete` مع مساره. يزيل النظام إدخالات الملف من الفهرس العكسي، مما يحرّر مساحة التخزين ويمنع النتائج القديمة.

## إعداد GroupDocs.Search للـ Java
للبدء، دمج GroupDocs.Search في مشروع Java الخاص بك باستخدام الإعداد التالي:

### إعداد Maven
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
بدلاً من ذلك، يمكنك [قم بتنزيل أحدث نسخة مباشرة من GroupDocs](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
تقدم GroupDocs نسخة تجريبية مجانية، تسمح لك بتقييم ميزاتها قبل الشراء. يمكنك الحصول على ترخيص مؤقت باتباع الخطوات على [صفحة الشراء](https://purchase.groupdocs.com/temporary-license/). سيمكنك هذا من الحصول على الوظائف الكاملة خلال مرحلة الاختبار.

### التهيئة الأساسية والإعداد
قم بتهيئة GroupDocs.Search في تطبيق Java الخاص بك باستخدام:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## دليل التنفيذ

### تكوين شبكة البحث
**Overview:** إنشاء مسار أساسي ومنفذ لشبكة البحث الخاصة بك، مما يسمح للعقد بالتواصل بفعالية.

#### الخطوة 1: تعريف التكوين الأساسي
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **المعلمات:**  
  - `basePath`: مسار الدليل لعمليات الشبكة.  
  - `basePort`: رقم المنفذ المستخدم من قبل شبكة البحث.

#### الخطوة 2: استكشاف الأخطاء وإصلاحها
تأكد من أن المنفذ المحدد غير محجوب بواسطة إعدادات جدار الحماية أو مستخدم من قبل تطبيق آخر. عدّل حسب الحاجة لتجنب التعارضات.

### نشر عقد شبكة البحث
**Overview:** باستخدام التكوين الخاص بك، انشر العقد عبر شبكتك للفهرسة والبحث الموزع.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **خيارات التكوين الرئيسية:**  
  - **Base Path & Port:** يجب أن تتطابق هذه القيم مع تلك المستخدمة في التكوين الأولي لضمان التناسق.

### فهرسة المستندات (`create searchable index`)
**Overview:** أضف المستندات إلى فهرس البحث بفعالية باستخدام عقدة رئيسية.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **الغرض:**  
  - `masterNode`: العقدة الأساسية التي تدير فهرسة المستندات.  
  - `documentsPath`: مسار الدليل الذي يحتوي على المستندات.

#### نصائح استكشاف الأخطاء
تحقق من صحة مسارات المستندات وإمكانية الوصول إليها. تأكد من أن الأذونات تسمح بالقراءة من هذه الأدلة.

### البحث النصي في الشبكة (`perform text search`)
**Overview:** إجراء عمليات بحث نصية شاملة عبر شبكة الفهرسة الخاصة بك.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- `query`: النص الذي تبحث عنه.  
- `masterNode`: العقدة التي تجري البحث.

### حذف المستندات من الفهرس (`delete documents index`)
**Overview:** إزالة مستندات محددة من الفهرس باستخدام مسارات ملفاتها.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- `node`: العقدة المستهدفة لعمليات الحذف.  
- `filePaths`: مسارات المستندات التي سيتم إزالتها من الفهرس.

#### استكشاف الأخطاء
تأكد من دقة مسارات الملفات وأن الملفات موجودة في الدليل الخاص بك. إذا استمرت المشكلات، تحقق من أذونات الشبكة والاتصال.

## التطبيقات العملية
1. **Enterprise Document Management:** تبسيط استرجاع المعرفة الداخلية.  
2. **Legal Case Analysis:** تحديد ملفات القضايا ذات الصلة بسرعة عبر مستودعات متعددة.  
3. **E‑commerce Platforms:** تعزيز سرعة بحث المنتجات عن طريق فهرسة الوصف والمراجعات.  
4. **Academic Research:** البحث بفعالية في مكتبات رقمية ضخمة من الأوراق والرسائل.  
5. **Customer Support Systems:** تقليل وقت الاستجابة بتمكين الوكلاء من البحث في التذاكر السابقة فورًا.

## اعتبارات الأداء
- **Optimize Indexing Speed:** إضافة المستندات الجديدة تدريجيًا خلال ساعات انخفاض الحمل للحفاظ على انخفاض الكمون.  
- **Resource Usage Guidelines:** مراقبة وحدة المعالجة المركزية والذاكرة، خاصةً عند توسيع عدد العقد.  
- **Java Memory Management:** ضبط إعدادات ذاكرة JVM وفقًا لحجم عملك (مثال: `-Xmx2g` للفهارس المتوسطة الحجم).

## الخلاصة
باتباع هذا الدليل، تعلمت كيفية **set up a search network**، **create a searchable index**، **perform text search**، و **delete documents index** باستخدام GroupDocs.Search للـ Java. تتيح هذه القدرات استرجاع مستندات سريع وموثوق عبر بيئات موزعة.

**الخطوات التالية**
- جرّب تكوينات عقد مختلفة للعثور على التوازن المثالي لحجم عملك.  
- تعمق أكثر في خيارات الفهرسة المتقدمة مثل المحللات المخصصة وضبط الصلة.  
- استكشف التكامل مع منتجات GroupDocs الأخرى لمعالجة المستندات من البداية إلى النهاية.

## الأسئلة الشائعة

**س: ما هو الاستخدام الأساسي لـ GroupDocs.Search للـ Java؟**  
ج: يوفر بحثًا نصيًا كاملًا عبر العديد من تنسيقات المستندات، مما يتيح لك **perform text search** في مستودعات كبيرة.

**س: كيف يمكنني تحسين سرعة البحث في شبكة كبيرة؟**  
ج: نشر عقد إضافية، ضبط ذاكرة JVM، وجدولة الفهرسة خلال فترات انخفاض الحركة لتحسين **optimize search performance**.

**س: هل يمكن حذف مستند واحد دون إعادة فهرسة المجموعة بأكملها؟**  
ج: نعم، استخدم API **delete documents index** كما هو موضح في مثال الشيفرة لإزالة ملفات محددة.

**س: هل أحتاج إلى ترخيص للتطوير؟**  
ج: ترخيص تجريبي مجاني يكفي للاختبار؛ يتطلب الترخيص التجاري للنشر في بيئات الإنتاج.

**س: هل يمكنني فهرسة ملفات PDF وWord والبريد الإلكتروني معًا؟**  
ج: بالتأكيد—يدعم GroupDocs.Search مجموعة واسعة من التنسيقات مباشرةً.

---

**آخر تحديث:** 2026-07-07  
**تم الاختبار مع:** GroupDocs.Search للـ Java 25.4  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [كيفية فهرسة النص في Java باستخدام دليل GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [تحسين أداء البحث باستخدام تقنيات الفهرسة المتقدمة في GroupDocs.Search للـ Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [تحسين أداء الاستعلام مع GroupDocs.Search Java: تحسين الفهرس والبحث](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
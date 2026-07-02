---
date: '2026-01-16'
description: تعلم كيفية إجراء البحث النصي وتحسين أداء البحث باستخدام GroupDocs.Search
  للغة Java. يتضمن خطوات إعداد شبكة البحث، إنشاء فهرس قابل للبحث، وحذف فهرس المستندات.
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: إجراء بحث نصي باستخدام GroupDocs.Search لجافا
type: docs
url: /ar/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# إجراء بحث نصي باستخدام GroupDocs.Search للغة Java
## تحسين الأداء

## كيفية تنفيذ وتحسين شبكة بحث باستخدام GroupDocs.Search للغة Java

### المقدمة
في عالم اليوم القائم على البيانات، القدرة على **perform text search** بسرعة عبر مجموعات ضخمة من المستندات تُعد ميزة تنافسية. سواء كنت تبني قاعدة معرفة داخلية، أو مستودع قضايا قانونية، أو كتالوج منتجات للتجارة الإلكترونية، فإن شبكة البحث المُضبوطة جيدًا يمكنها تحسين رضا المستخدم بشكل كبير. في هذا الدليل ستتعلم كيفية **set up search network**، **create searchable index**، **optimize search performance**، وحتى **delete documents index** عند الحاجة—كل ذلك باستخدام GroupDocs.Search للغة Java.

**ما ستتعلمه**
- تهيئة شبكة بحث باستخدام GroupDocs.Search  
- نشر العقد داخل الشبكة  
- فهرسة المستندات بفعالية (`index documents java`)  
- إجراء بحث نصي عبر شبكتك (`perform text search`)  
- حذف مستندات محددة من الفهرس (`delete documents index`)  

لنغوص في كيفية الاستفادة من هذه الميزات لإنشاء تجربة بحث محسّنة.

## إجابات سريعة
- **ما هو الهدف الرئيسي من GroupDocs.Search للغة Java؟** إنه يوفر بحثًا نصيًا كاملاً عبر العديد من صيغ المستندات.  
- **كيف أقوم بإجراء بحث نصي في بيئة موزعة؟** قم بنشر شبكة بحث، فهرس المستندات على عقدة رئيسية، ثم استعلم من أي عقدة.  
- **هل يمكنني حذف مستندات من الفهرس دون إعادة بنائه؟** نعم، استخدم Delete API لإزالة الملفات المحددة.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أعلى.  
- **هل يلزم وجود ترخيص للإنتاج؟** يتطلب ترخيص صالح لـ GroupDocs.Search؛ يتوفر نسخة تجريبية مجانية.

## ما هو “perform text search”؟
إجراء بحث نصي يعني استعلام فهرس نص كامل لاسترجاع المستندات التي تحتوي على الكلمات المفتاحية أو العبارات المحددة. يبني GroupDocs.Search فهرسًا عكسيًا يجعل هذه عمليات البحث سريعة للغاية، حتى عبر آلاف الملفات.

## لماذا إعداد شبكة بحث؟
توزع شبكة البحث عمليات الفهرسة والاستعلام عبر عدة عقد، مما يتيح لك **optimize search performance**، التوسع أفقيًا، والحفاظ على توافر عالي. هذه البنية مثالية لمستودعات المستندات على مستوى المؤسسات حيث تكون الكمون وسرعة النقل أمرًا حاسمًا.

### المتطلبات المسبقة
- **المكتبات المطلوبة:** GroupDocs.Search للغة Java الإصدار 25.4 (الأحدث).  
- **البيئة:** Java JDK 8+، Maven.  
- **المعرفة:** برمجة Java أساسية وإلمام بمفاهيم الشبكات.

### إعداد GroupDocs.Search للغة Java
لبدء العمل، دمج GroupDocs.Search في مشروع Java الخاص بك باستخدام الإعداد التالي:

#### إعداد Maven
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

#### تحميل مباشر
بدلاً من ذلك، يمكنك [download the latest version directly from GroupDocs](https://releases.groupdocs.com/search/java/).

#### الحصول على الترخيص
تقدم GroupDocs نسخة تجريبية مجانية، تسمح لك بتقييم ميزاتها قبل الشراء. يمكنك الحصول على ترخيص مؤقت باتباع الخطوات على صفحة [purchase page](https://purchase.groupdocs.com/temporary-license/). سيمكنك ذلك من الحصول على كامل الوظائف خلال مرحلة الاختبار.

#### التهيئة الأساسية والإعداد
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

### دليل التنفيذ

#### تهيئة شبكة البحث
**نظرة عامة:** حدد مسار قاعدة و منفذ لشبكة البحث الخاصة بك، مما يسمح للعقد بالتواصل بفعالية.

##### الخطوة 1: تعريف التكوين الأساسي

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

##### الخطوة 2: استكشاف الأخطاء وإصلاحها
تأكد من أن المنفذ المحدد غير محجوب بإعدادات جدار الحماية أو مستخدم من قبل تطبيق آخر. عدّل حسب الحاجة لتجنب التعارضات.

#### نشر عقد شبكة البحث
**نظرة عامة:** باستخدام التكوين الخاص بك، انشر العقد عبر شبكتك للفهرسة والبحث الموزع.

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

#### فهرسة المستندات (`create searchable index`)
**نظرة عامة:** أضف المستندات إلى فهرس البحث بفعالية باستخدام عقدة رئيسية.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **الغرض:**  
  - `masterNode`: العقدة الأساسية التي تدير فهرسة المستندات.  
  - `documentsPath`: مسار الدليل الذي يحتوي على المستندات.

##### نصائح استكشاف الأخطاء وإصلاحها
تحقق من صحة مسارات المستندات وإمكانية الوصول إليها. تأكد من أن الأذونات تسمح بالقراءة من هذه الأدلة.

#### البحث النصي في الشبكة (`perform text search`)
**نظرة عامة:** قم بإجراء عمليات بحث نصية شاملة عبر شبكتك المفهرسة.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **المعلمات:**  
  - `query`: النص الذي تبحث عنه.  
  - `masterNode`: العقدة التي تجري البحث.

#### حذف المستندات من الفهرس (`delete documents index`)
**نظرة عامة:** أزل مستندات محددة من فهرسك باستخدام مسارات ملفاتها.

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

- **غرض الطريقة:**  
  - `node`: العقدة المستهدفة لعمليات الحذف.  
  - `filePaths`: مسارات المستندات التي سيتم إزالتها من الفهرس.

##### استكشاف الأخطاء وإصلاحها
تأكد من دقة مسارات الملفات وأن الملفات موجودة في الدليل الخاص بك. إذا استمرت المشكلات، تحقق من أذونات الشبكة والاتصال.

### التطبيقات العملية
1. **Enterprise Document Management:** تبسيط استرجاع المعرفة الداخلية.  
2. **Legal Case Analysis:** تحديد ملفات القضايا ذات الصلة بسرعة عبر مستودعات متعددة.  
3. **E‑commerce Platforms:** تعزيز سرعة بحث المنتجات عبر فهرسة الأوصاف والمراجعات.  
4. **Academic Research:** البحث بكفاءة في مكتبات رقمية ضخمة من الأوراق والرسائل.  
5. **Customer Support Systems:** تقليل زمن الاستجابة بتمكين الوكلاء من البحث في التذاكر السابقة فورًا.  

### اعتبارات الأداء
- **Optimize Indexing Speed:** أضف المستندات الجديدة تدريجيًا خلال ساعات انخفاض الحمل للحفاظ على انخفاض الكمون.  
- **Resource Usage Guidelines:** راقب وحدة المعالجة المركزية والذاكرة، خاصةً عند توسيع عدد العقد.  
- **Java Memory Management:** اضبط إعدادات كومة JVM وفقًا لحجم عملك (مثال: `-Xmx2g` للفهارس المتوسطة الحجم).  

### الخلاصة
باتباع هذا الدليل، تعلمت كيفية **set up search network**، **create searchable index**، **perform text search**، و**delete documents index** باستخدام GroupDocs.Search للغة Java. تتيح لك هذه القدرات استرجاع مستندات سريع وموثوق عبر بيئات موزعة.

**الخطوات التالية**
- جرّب تكوينات عقد مختلفة للعثور على التوازن المثالي لحجم عملك.  
- تعمق في خيارات الفهرسة المتقدمة مثل المحللات المخصصة وضبط الصلة.  
- استكشف التكامل مع منتجات GroupDocs الأخرى لمعالجة المستندات من البداية إلى النهاية.

## الأسئلة المتكررة

**س: ما هو الاستخدام الأساسي لـ GroupDocs.Search للغة Java؟**  
ج: يوفر بحثًا نصيًا كاملاً عبر العديد من صيغ المستندات، مما يتيح لك **perform text search** في مستودعات كبيرة.

**س: كيف يمكنني تحسين سرعة البحث في شبكة كبيرة؟**  
ج: انشر عقدًا إضافية، اضبط كومة JVM، وجدول الفهرسة خلال فترات انخفاض الحركة لتـ **optimize search performance**.

**س: هل يمكن حذف مستند واحد دون إعادة فهرسة المجموعة بالكامل؟**  
ج: نعم، استخدم واجهة برمجة التطبيقات **delete documents index** كما هو موضح في مثال الشيفرة لإزالة ملفات محددة.

**س: هل أحتاج إلى ترخيص للتطوير؟**  
ج: ترخيص تجريبي مجاني يكفي للاختبار؛ يتطلب الترخيص التجاري للنشر في بيئات الإنتاج.

**س: هل يمكنني فهرسة ملفات PDF وWord والبريد الإلكتروني معًا؟**  
ج: بالتأكيد—يدعم GroupDocs.Search مجموعة واسعة من الصيغ مباشرةً.

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search للغة Java 25.4  
**Author:** GroupDocs
---
date: '2026-05-02'
description: تعلم كيفية تكوين البحث وتمكين تحديثات البحث في الوقت الفعلي باستخدام
  GroupDocs.Search للغة Java. دليل خطوة بخطوة لإعداد الشبكة، نشر العقد، والفهرسة.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: كيفية تكوين البحث باستخدام GroupDocs.Search في جافا - دليل التكوين والنشر
type: docs
url: /ar/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# كيفية تكوين البحث باستخدام GroupDocs.Search في Java

في عالمنا الرقمي سريع الحركة اليوم، **كيفية تكوين البحث** بفعالية يمكن أن يحدد نجاح المشروع أو فشله. سواءً كنت تتعامل مع آلاف العقود أو الأوراق البحثية أو التقارير الداخلية، فإن شبكة البحث المصممة جيدًا تتيح لك العثور على المستند الصحيح في ثوانٍ. يشرح هذا الدليل كيفية تكوين شبكة البحث، نشر العقد، وتمكين **تحديثات البحث في الوقت الحقيقي** باستخدام GroupDocs.Search لـ Java.

## إجابات سريعة
- **ما هو الغرض الأساسي من شبكة البحث؟** لتوزيع الفهرسة ومعالجة الاستعلامات عبر عدة عقد لتحقيق القابلية للتوسع والسرعة.  
- **ما نسخة المكتبة المطلوبة؟** GroupDocs.Search for Java v25.4 أو أحدث.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتقييم؛ الترخيص التجاري مطلوب للإنتاج.  
- **كيف يتم التعامل مع تحديثات الوقت الحقيقي؟** عن طريق الاشتراك في أحداث العقد التي تُطلق عند تغيّر الفهرسة.  
- **هل يمكنني إضافة مجلدات مستندات جديدة أثناء التشغيل؟** نعم—استخدم طريقة `addDirectories` الخاصة بالفهرس.

## ما هو “كيفية تكوين البحث” في سياق GroupDocs؟
تكوين البحث يعني إعداد **شبكة البحث** التي تعرف مكان وجود مستنداتك، وكيفية تواصل العقد، وكيفية تنسيق الفهرسة. بمجرد تكوين الشبكة، يمكنك إضافة أو إزالة العقد دون توقف، مما يضمن الوصول المستمر إلى نتائج البحث المحدثة.

## لماذا تستخدم GroupDocs.Search لـ Java؟
- **القابلية للتوسع:** توزيع الأحمال عبر عدة آلات.  
- **تحديثات الوقت الحقيقي:** عكس الملفات المفهرسة حديثًا عبر الشبكة فورًا.  
- **سهولة التكامل:** إعداد Maven بسيط وواجهات برمجة تطبيقات Java واضحة.  
- **جاهز للمؤسسات:** يتعامل مع مجموعات بيانات ضخمة وسيناريوهات استعلام معقدة.

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8+** مثبت.  
- **Maven** لإدارة التبعيات.  
- إلمام أساسي بـ Java و Maven ومفاهيم البحث.

## إعداد GroupDocs.Search لـ Java

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

**التنزيل المباشر:** يمكنك أيضًا الحصول على المكتبة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **Free Trial:** احصل على ترخيص تجريبي لاستكشاف جميع الميزات.  
- **Temporary License:** طلب للحصول على فترات تقييم ممتدة.  
- **Commercial License:** مطلوب للنشر في بيئات الإنتاج.

### التهيئة الأساسية
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## كيفية تكوين شبكة البحث في Java

### الخطوة 1: استيراد الحزم المطلوبة
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### الخطوة 2: تكوين الشبكة
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameters:** `basePath` يشير إلى مجلد المستندات الخاص بك؛ `basePort` هو منفذ TCP المستخدم لتواصل العقد.

## نشر عقد شبكة البحث

### الخطوة 1: استيراد حزمة النشر
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### الخطوة 2: نشر العقد
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Node:** ينسق عمليات البحث والفهرسة عبر جميع العقد. يمكنك **configure master node** الإعدادات مثل تخصيص الشظايا وفحوصات الصحة.

## الاشتراك في أحداث العقد لتحديثات البحث في الوقت الحقيقي

### الخطوة 1: استيراد حزمة الأحداث
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### الخطوة 2: الاشتراك في أحداث العقد الرئيسية
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Event Handling:** يتيح **real time search updates** كلما تم إضافة مستندات أو تحديثها أو إزالتها.

## إضافة أدلة للفهرسة

### الخطوة 1: استيراد حزمة الفهرس
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### الخطوة 2: إضافة أدلة المستندات
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dynamic Indexing:** استخدم طريقة `addDirectories` لـ **add directories to index** أثناء التشغيل دون إعادة تشغيل الشبكة.

## استرجاع المستندات المفهرسة

### الخطوة 1: استيراد حزمة الباحث
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### الخطوة 2: استرجاع معلومات المستند
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Shard Management:** يدير مجموعات البيانات الكبيرة بكفاءة عن طريق توزيع المستندات عبر الشظايا. لـ **optimize shard size**، راقب إحصائيات الشظايا واضبط إعداد `shardSize` في الإصدارات المستقبلية.

## لماذا هذا مهم لمشروعك
شبكة بحث مُكوَّنة بشكل صحيح تُزيل عنق الزجاجة، تقلل الكمون، وتضمن أن المستخدمين يرون دائمًا أحدث نسخة من المستند. تحديثات الوقت الحقيقي والقدرة على **add directories to index** دون توقف هي ذات قيمة خاصة للمكاتب القانونية، والمؤسسات البحثية، وأي منظمة تتعامل مع مجموعات مستندات تتغير باستمرار.

## التطبيقات العملية
1. **Enterprise Document Management:** مركز البحث عبر ملايين الملفات.  
2. **Legal Firms:** العثور بسرعة على ملفات القضايا والعقود والأدلة.  
3. **Academic Research:** فهرسة المجلات والأوراق للبحث الفوري.

## اعتبارات الأداء
- **Optimize Indexing:** جدولة تجديدات الفهرس المنتظمة وإزالة البيانات القديمة.  
- **Memory Management:** مراقبة ذاكرة JVM، خاصةً عند التعامل مع شظايا كبيرة.  
- **Scalability Planning:** إضافة عقد مع نمو مجموعة البيانات؛ الشبكة توازن الحمل تلقائيًا.  
- **Optimize shard size:** الشظايا الصغيرة تحسن زمن استجابة الاستعلام، بينما الشظايا الكبيرة تقلل الحمل الزائد. اضبط بناءً على عتادك وأنماط الاستعلام.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| العقد لا يمكنها الاتصال | تعارض في المنفذ أو جدار حماية | تأكد من أن `basePort` مفتوح ولا يستخدمه خدمات أخرى |
| الفهرس لا يتم تحديثه | اشتراك الحدث مفقود | استدعِ `SearchNetworkNodeEvents.subscribe(masterNode)` بعد النشر |
| أخطاء نفاد الذاكرة | تحميل شظايا كبيرة كثيرة | قلل حجم الشظايا أو زد حجم ذاكرة JVM (`-Xmx` flag) |

## الأسئلة المتكررة

**س: هل يمكنني إضافة أدلة جديدة بعد تشغيل الشبكة؟**  
ج: نعم—استخدم طريقة `indexer.addDirectories()`؛ ستقوم الأحداث المشترك فيها بنشر التحديثات في الوقت الحقيقي.

**س: كيف أراقب صحة العقد؟**  
ج: كل `SearchNetworkNode` يوفر واجهات برمجة تطبيقات الحالة؛ دمجها مع أداة المراقبة التي تختارها.

**س: هل يمكن تشغيل العقدة الرئيسية على جهاز منفصل؟**  
ج: بالتأكيد. فقط تأكد من أن جميع العقد تشترك في نفس `basePort` ويمكنها الوصول إلى بعضها عبر الشبكة.

**س: ما صيغ الملفات المدعومة؟**  
ج: يدعم GroupDocs.Search ملفات PDF، Word، Excel، PowerPoint، النص العادي، والعديد من الصيغ الأخرى مباشرةً.

**س: هل أحتاج إلى إعادة تشغيل الشبكة بعد إضافة عقدة جديدة؟**  
ج: لا—يمكن إضافة أو إزالة العقد ديناميكيًا؛ ستعيد العقدة الرئيسية موازنة الشظايا تلقائيًا.

## الخلاصة
الآن بعد أن عرفت **كيفية تكوين البحث** باستخدام GroupDocs.Search لـ Java، يمكنك بناء حلول بحث مستندات سريعة، قابلة للتوسع، وموثوقة تتماشى مع نمو مؤسستك. طبّق هذه الأنماط لإنشاء تجارب بحث موزعة وفي الوقت الحقيقي لأي صناعة.

---

**آخر تحديث:** 2026-05-02  
**تم الاختبار مع:** GroupDocs.Search for Java 25.4  
**المؤلف:** GroupDocs
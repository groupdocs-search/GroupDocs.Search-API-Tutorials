---
date: '2026-01-08'
description: تعلم كيفية تكوين البحث وتمكين تحديثات البحث في الوقت الفعلي باستخدام
  GroupDocs.Search للغة Java. دليل خطوة بخطوة لإعداد الشبكة، نشر العقد، والفهرسة.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'كيفية تكوين البحث باستخدام GroupDocs.Search في جافا: دليل التكوين والنشر'
type: docs
url: /ar/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# كيفية تكوين البحث باستخدام GroupDocs.Search في Java

في عالمنا الرقمي سريع الحركة اليوم، يمكن أن يكون **كيفية تكوين البحث** بكفاءة هو العامل الحاسم في نجاح أو فشل المشروع. سواء كنت تتعامل مع آلاف العقود أو الأوراق البحثية أو التقارير الداخلية، فإن شبكة البحث المصممة بشكل جيد تتيح لك العثور على المستند الصحيح في ثوانٍ. يشرح هذا الدليل كيفية تكوين شبكة البحث، نشر العقد، وتمكين **تحديثات البحث في الوقت الفعلي** باستخدام GroupDocs.Search للـ Java.

## إجابات سريعة
- **ما هو الغرض الأساسي من شبكة البحث؟** لتوزيع الفهرسة ومعالجة الاستعلامات عبر عدة عقد لتحقيق القابلية للتوسع والسرعة.  
- **ما هو إصدار المكتبة المطلوب؟** GroupDocs.Search للـ Java الإصدار v25.4 أو أحدث.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتقييم؛ يلزم ترخيص تجاري للإنتاج.  
- **كيف يتم التعامل مع التحديثات في الوقت الفعلي؟** عن طريق الاشتراك في أحداث العقد التي تُطلق عند تغييرات الفهرسة.  
- **هل يمكنني إضافة مجلدات مستندات جديدة أثناء التشغيل؟** نعم—استخدم طريقة `addDirectories` في الفهرس.

## ما هو “كيفية تكوين البحث” في سياق GroupDocs؟
يعني تكوين البحث إعداد **شبكة بحث** تعرف مكان وجود مستنداتك، وكيفية تواصل العقد، وكيفية تنسيق الفهرسة. بمجرد تكوين الشبكة، يمكنك إضافة أو إزالة العقد دون توقف، مما يضمن الوصول المستمر إلى نتائج البحث المحدثة.

## لماذا تستخدم GroupDocs.Search للـ Java؟
- **القابلية للتوسع:** توزيع عبء العمل عبر عدة آلات.  
- **تحديثات في الوقت الفعلي:** عكس الملفات المفهرسة حديثًا عبر الشبكة فورًا.  
- **سهولة التكامل:** إعداد Maven بسيط وواجهات برمجة تطبيقات Java واضحة.  
- **جاهزية للمؤسسات:** يتعامل مع مجموعات بيانات كبيرة وسيناريوهات استعلام معقدة.

## المتطلبات المسبقة
- **مجموعة تطوير جافا (JDK) 8+** مثبتة.  
- **Maven** لإدارة التبعيات.  
- إلمام أساسي بـ Java و Maven ومفاهيم البحث.  

## إعداد GroupDocs.Search للـ Java

### تبعية Maven
أضف المستودع والتبعيات إلى ملف `pom.xml` الخاص بك:

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

**تحميل مباشر:** يمكنك أيضًا الحصول على المكتبة من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **تجربة مجانية:** احصل على ترخيص تجريبي لاستكشاف جميع الميزات.  
- **ترخيص مؤقت:** طلب لفترات تقييم ممتدة.  
- **ترخيص تجاري:** مطلوب للنشر في بيئات الإنتاج.

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
- **المعلمات:** `basePath` يشير إلى مجلد المستندات الخاص بك؛ `basePort` هو منفذ TCP المستخدم لتواصل العقد.

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
- **العقدة الرئيسية:** تنسق عمليات البحث والفهرسة عبر جميع العقد.

## الاشتراك في أحداث العقد لتحديثات البحث في الوقت الفعلي

### الخطوة 1: استيراد حزمة الأحداث
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### الخطوة 2: الاشتراك في أحداث العقدة الرئيسية
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **معالجة الأحداث:** يتيح **تحديثات البحث في الوقت الفعلي** كلما تم إضافة أو تحديث أو إزالة المستندات.

## إضافة مجلدات للفهرسة

### الخطوة 1: استيراد حزمة الفهرس
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### الخطوة 2: إضافة مجلدات المستندات
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **فهرسة ديناميكية:** أضف عددًا من المجلدات حسب الحاجة؛ ستقوم الشبكة بفهرستها تلقائيًا.

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
- **إدارة القطع (Shard):** يتعامل بفعالية مع مجموعات البيانات الكبيرة عن طريق توزيع المستندات عبر القطع.

## التطبيقات العملية
1. **إدارة المستندات للمؤسسات:** مركزية البحث عبر ملايين الملفات.  
2. **المكاتب القانونية:** العثور بسرعة على ملفات القضايا والعقود والأدلة.  
3. **البحث الأكاديمي:** فهرسة المجلات والأوراق للبحث الفوري.

## اعتبارات الأداء
- **تحسين الفهرسة:** جدولة تحديثات الفهرسة بانتظام وإزالة البيانات القديمة.  
- **إدارة الذاكرة:** مراقبة مساحة الذاكرة heap في JVM، خاصة عند التعامل مع قطع كبيرة.  
- **تخطيط القابلية للتوسع:** إضافة عقد مع نمو مجموعة البيانات؛ تقوم الشبكة بموازنة الحمل تلقائيًا.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|-----|
| العقد لا يمكنها الاتصال | تعارض في المنفذ أو جدار حماية | تأكد من أن `basePort` مفتوح ولا يستخدمه خدمات أخرى |
| الفهرس لا يتم تحديثه | اشتراك الحدث مفقود | استدعِ `SearchNetworkNodeEvents.subscribe(masterNode)` بعد النشر |
| أخطاء نفاد الذاكرة | تحميل عدد كبير من القطع الكبيرة | قلل حجم القطع أو زد مساحة heap في JVM (علامة `-Xmx`) |

## الأسئلة المتكررة

**س: هل يمكنني إضافة مجلدات جديدة بعد تشغيل الشبكة؟**  
ج: نعم—استخدم طريقة `indexer.addDirectories()`؛ ستقوم الأحداث المشترك فيها بنشر التحديثات في الوقت الفعلي.

**س: كيف يمكنني مراقبة صحة العقد؟**  
ج: كل `SearchNetworkNode` يوفر واجهات برمجة تطبيقات الحالة؛ دمجها مع أداة المراقبة التي تختارها.

**س: هل يمكن تشغيل العقدة الرئيسية على جهاز منفصل؟**  
ج: بالتأكيد. فقط تأكد من أن جميع العقد تشترك في نفس `basePort` ويمكنها الوصول إلى بعضها عبر الشبكة.

**س: ما هي صيغ الملفات المدعومة؟**  
ج: يدعم GroupDocs.Search ملفات PDF، Word، Excel، PowerPoint، النص العادي، والعديد من الصيغ الأخرى مباشرة.

**س: هل أحتاج إلى إعادة تشغيل الشبكة بعد إضافة عقدة جديدة؟**  
ج: لا—يمكن إضافة أو إزالة العقد ديناميكيًا؛ ستقوم العقدة الرئيسية بإعادة موازنة القطع تلقائيًا.

## الخلاصة
أنت الآن تمتلك فهماً كاملاً خطوة بخطوة لـ **كيفية تكوين البحث** باستخدام GroupDocs.Search للـ Java، من الإعداد الأولي إلى التحديثات في الوقت الفعلي والفهرسة الموزعة. طبق هذه الأنماط لبناء حلول بحث مستندات سريعة، قابلة للتوسع، وموثوقة لأي صناعة.

---

**آخر تحديث:** 2026-01-08  
**تم الاختبار مع:** GroupDocs.Search للـ Java 25.4  
**المؤلف:** GroupDocs
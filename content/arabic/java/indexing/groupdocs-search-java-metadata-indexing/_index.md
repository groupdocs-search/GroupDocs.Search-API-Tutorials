---
date: '2026-01-06'
description: تعلم كيفية إضافة المستندات إلى الفهرس والبحث عن المستندات عبر البيانات
  الوصفية باستخدام GroupDocs.Search Java. اتقن إعدادات الفهرس، أنشئ الفهارس، أضف المستندات،
  ونفّذ عمليات بحث دقيقة.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: كيفية إضافة المستندات إلى الفهرس مع فهرسة البيانات الوصفية في جافا باستخدام
  GroupDocs.Search
type: docs
url: /ar/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# كيفية إضافة المستندات إلى الفهرس باستخدام فهرسة البيانات الوصفية في Java باستخدام GroupDocs.Search

في التطبيقات الحديثة، يُعد **إضافة المستندات إلى الفهرس** بسرعة وبشكل موثوق أمرًا أساسيًا لتقديم تجارب بحث سريعة. سواءً كنت تبني مستودعًا قانونيًا، أو قاعدة معرفة لدعم العملاء، أو بوابة مستندات داخلية، فإن الاستفادة من البيانات الوصفية تجعل من الممكن **البحث عن المستندات عبر البيانات الوصفية** مثل المؤلف، العنوان، أو العلامات المخصصة. يوضح هذا الدليل العملية بالكامل — تكوين إعدادات الفهرس، إنشاء فهرس يركز على البيانات الوصفية، إضافة ملفاتك، وتشغيل عمليات بحث قوية — كل ذلك باستخدام GroupDocs.Search للـ Java.

## إجابات سريعة
- **ما هو الغرض الأساسي من فهرسة البيانات الوصفية؟** يتيح عمليات بحث سريعة تعتمد على خصائص المستند بدلاً من محتوى النص الكامل.  
- **ما هي الطريقة التي تضيف الملفات إلى الفهرس؟** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **هل يمكنني البحث عبر حقول البيانات الوصفية المخصصة؟** نعم، بمجرد فهرسة الحقول يمكنك الاستعلام عنها مباشرة.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مؤقت يكفي للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** يوصى بـ JDK 8 أو أعلى.  

## ما هي فهرسة البيانات الوصفية في GroupDocs.Search؟
تستخرج فهرسة البيانات الوصفية وتخزن سمات المستند (مثل المؤلف، تاريخ الإنشاء، العلامات المخصصة) في بنية قابلة للبحث. عندما **تضيف المستندات إلى الفهرس**، يقوم المحرك بتسجيل هذه السمات، مما يتيح لك تنفيذ استعلامات دقيقة مثل “العثور على جميع ملفات PDF التي كتبها *John Doe*”.

## لماذا تستخدم GroupDocs.Search لفهرسة البيانات الوصفية؟
- **الأداء:** عمليات البحث عبر البيانات الوصفية خفيفة الوزن وتعيد النتائج في مليثانية.  
- **المرونة:** يدعم مجموعة واسعة من صيغ الملفات (PDF، DOCX، PPT، إلخ).  
- **القابلية للتوسع:** يتعامل مع ملايين المستندات بأقل استهلاك للذاكرة.  

## المتطلبات المسبقة
- GroupDocs.Search للـ Java ≥ 25.4.  
- JDK 8 أو أحدث مثبت ومُكوَّن.  
- إلمام أساسي بـ Java و Maven.  

## إعداد GroupDocs.Search للـ Java

### تعليمات التثبيت
أضف مستودع GroupDocs والاعتماد إلى ملف `pom.xml` الخاص بك:

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

يمكنك أيضًا تنزيل أحدث الملفات الثنائية مباشرةً من [إصدارات GroupDocs.Search للـ Java](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
للحصول على ترخيص مؤقت للاختبار:
1. زر موقع GroupDocs وانتقل إلى قسم **الشراء**.  
2. اختر خطة **ترخيص مؤقت** التي تتناسب مع احتياجات تقييمك.  

## تنفيذ خطوة بخطوة

### الميزة 1: تكوين إعدادات الفهرس
قم بتكوين الفهرس للتركيز على البيانات الوصفية:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` يخبر المحرك بإعطاء الأولوية للبيانات الوصفية على محتوى النص الكامل.

### الميزة 2: إنشاء فهرس في مجلد محدد
أنشئ دليل فهرس فعلي حيث سيتم تخزين جميع البيانات الوصفية:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

استبدل `YOUR_DOCUMENT_DIRECTORY` بالمسار الذي يتطابق مع بنية مشروعك.

### الميزة 3: كيفية إضافة المستندات إلى الفهرس
الآن بعد أن الفهرس موجود، يمكنك **إضافة المستندات إلى الفهرس** لتصبح قابلة للبحث:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**نصائح:**  
- تأكد من أن مسار المجلد صحيح وأن التطبيق لديه أذونات القراءة.  
- يقوم GroupDocs.Search تلقائيًا باستخراج البيانات الوصفية المدعومة من كل ملف.

### الميزة 4: البحث عن المستندات عبر البيانات الوصفية
نفّذ استعلامًا يستهدف حقول البيانات الوصفية، على سبيل المثال البحث عن المستندات التي تكون اللغة فيها الإنجليزية:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` يبحث في البيانات الوصفية المفهرسة ويعيد المستندات المطابقة.

## تطبيقات عملية
1. **إدارة المستندات المؤسسية:** استرجاع العقود حسب تاريخ العقد أو اسم الموقع.  
2. **كتالوجات المكتبة الرقمية:** السماح للمستخدمين بتصفح الكتب حسب النوع، سنة النشر، أو المؤلف.  
3. **أنظمة CRM:** تحديد ملفات العملاء بسرعة باستخدام بيانات وصفية مخصصة مثل معرف العميل أو المنطقة.  

## اعتبارات الأداء
- **التحديثات المتزايدة:** استخدم `index.addOrUpdate()` للملفات الجديدة أو المعدلة بدلاً من إعادة بناء الفهرس بالكامل.  
- **ضبط الذاكرة:** عدّل حجم كومة JVM (`-Xmx`) بناءً على حجم البيانات الوصفية المفهرسة.  
- **التخزين المُحسّن:** استدعِ `index.optimize()` بشكل دوري لضغط الفهرس وتحسين سرعة الاستعلام.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **لا توجد نتائج** | تأكد من أن حقول البيانات الوصفية التي تتوقعها موجودة فعليًا في الملفات المصدر. |
| **أخطاء الأذونات** | تأكد من أن عملية Java لديها صلاحية قراءة كل من مجلد المستندات ودليل الفهرس. |
| **أخطاء نفاد الذاكرة** | قم بزيادة حجم كومة JVM أو نفّذ عملية `add` على دفعات لمعالجة الملفات في مجموعات أصغر. |

## الأسئلة المتكررة

**س: ما هي فهرسة البيانات الوصفية؟**  
ج: تخزن فهرسة البيانات الوصفية سمات المستند (المؤلف، العنوان، العلامات المخصصة) في بنية قابلة للبحث، مما يتيح عمليات بحث سريعة دون فحص النص الكامل.

**س: كيف أحصل على ترخيص مؤقت؟**  
ج: زر صفحة شراء GroupDocs واتبع الخطوات للحصول على ترخيص تجريبي.

**س: هل يمكنني فهرسة ملفات PDF باستخدام هذا الإعداد؟**  
ج: نعم، يدعم GroupDocs.Search ملفات PDF، DOCX، PPT، والعديد من الصيغ الأخرى.

**س: ما هي المشكلات الشائعة عند إضافة المستندات؟**  
ج: تحقق من صحة مسارات الملفات وتأكد من أن التطبيق لديه أذونات قراءة للمجلدات.

**س: كيف أحسن أداء البحث؟**  
ج: قم بتحديث الفهرس بانتظام، استخدم الإضافات المتزايدة، واضبط إعدادات ذاكرة JVM.

## الموارد

- **التوثيق:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **مرجع API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **التنزيل:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **مستودع GitHub:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **منتدى الدعم المجاني:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **ترخيص مؤقت:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**آخر تحديث:** 2026-01-06  
**تم الاختبار مع:** GroupDocs.Search Java 25.4  
**المؤلف:** GroupDocs
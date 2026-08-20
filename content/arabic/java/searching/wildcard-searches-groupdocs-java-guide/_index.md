---
date: '2026-03-23'
description: تعلم كيفية إضافة المستندات إلى الفهرس وتحسين فهرس البحث باستخدام GroupDocs.Search
  للغة Java، مما يتيح عمليات بحث قوية باستخدام الأحرف البديلة.
keywords:
- wildcard searches in Java
- text-based wildcard search
- object-based wildcard search
title: إضافة مستندات إلى الفهرس – البحث باستخدام أحرف البدل في جافا
type: docs
url: /ar/java/searching/wildcard-searches-groupdocs-java-guide/
weight: 1
---

# إضافة المستندات إلى الفهرس – إتقان عمليات البحث باستخدام البدل في جافا مع GroupDocs.Search

استكشف قوة عمليات البحث باستخدام البدل القائمة على النص والبدل القائمة على الكائنات باستخدام GroupDocs.Search لجافا. في هذا الدليل ستتعلم كيفية **إضافة المستندات إلى الفهرس**، وتكوين الأنماط المتقدمة، والحفاظ على تحسين فهرس البحث للحصول على نتائج سريعة.

## إجابات سريعة
- **ماذا يعني “إضافة المستندات إلى الفهرس”?** إنه ينشئ بنية بيانات قابلة للبحث يمكن لـ GroupDocs.Search الاستعلام عنها بكفاءة.  
- **ما هي الكلمة المفتاحية التي تعزز الأداء؟** استخدام أنماط بديل مختصرة وإجراء عمليات **تحسين فهرس البحث** بانتظام.  
- **هل أحتاج إلى إعدادات ذاكرة خاصة؟** نعم—راقب **إدارة ذاكرة البحث في جافا** لتجنب أخطاء نفاد الذاكرة في مجموعات البيانات الكبيرة.  
- **هل يمكنني استخدام هذه الميزات في تطبيق Spring Boot؟** بالتأكيد؛ فقط أدرج تبعية Maven وقم بتكوين مجلد الفهرس.  
- **هل يلزم وجود ترخيص للإنتاج؟** يلزم وجود ترخيص صالح لـ GroupDocs.Search للعمليات التجارية.

## ما هو “إضافة المستندات إلى الفهرس” في GroupDocs.Search؟
إضافة المستندات إلى الفهرس تعني تغذية ملفات المصدر الخاصة بك (PDFs، DOCX، TXT، إلخ) إلى مستودع قابل للبحث تقوم GroupDocs.Search بإنشائه خلف الكواليس. بمجرد فهرسة الملفات، يمكنك تشغيل استعلامات بديل سريعة دون الحاجة إلى مسح الملفات الأصلية في كل مرة.

## لماذا نستخدم عمليات البحث بالبدل مع GroupDocs.Search؟
تتيح لك عمليات البحث بالبدل مطابقة أجزاء من الكلمات أو الأنماط—مثالية للسيناريوهات التي يتذكر فيها المستخدمون فقط أجزاء من مصطلح. هذه المرونة تحسن تجربة المستخدم في أنظمة إدارة المستندات، وبوابات المحتوى، وأدوات استخراج البيانات.

## المتطلبات المسبقة
- **Java Development Kit (JDK)** – الإصدار 8 أو أحدث.  
- معرفة أساسية ببرمجة جافا.  
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse.  
- Maven لإدارة التبعيات (أو يمكنك تنزيل ملف JAR مباشرة).  

## إعداد GroupDocs.Search لجافا

### إعداد Maven
أضف المستودع والتبعية إلى ملف `pom.xml` الخاص بك:

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
إذا كنت تفضل عدم استخدام Maven، قم بتنزيل أحدث ملف JAR من [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### الحصول على الترخيص
- **Free Trial:** استكشف الميزات الأساسية دون تكلفة.  
- **Temporary License:** فعّل القدرات المتقدمة أثناء التقييم.  
- **Purchase:** احصل على ترخيص تجاري للاستخدام في الإنتاج.

## دليل التنفيذ

### الميزة 1: بحث بديل قائم على النص

#### الخطوة 1 – إعداد الفهرس و **إضافة المستندات إلى الفهرس**
أولاً، أنشئ مجلد فهرس وأضف مستندات المصدر الخاصة بك:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInTextForm";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### الخطوة 2 – تنفيذ استعلامات بديل
قم بتشغيل عمليات بحث قائمة على الأنماط مباشرة على النص:

```java
// Search for words matching 'm???is'
String query1 = "m???is";
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Search for words matching 'pri?(1~7)'
String query2 = "pri?(1~7)";
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**شرح**  
- `indexFolder` يخزن الفهرس القابل للبحث على القرص.  
- `documentsFolder` يشير إلى موقع الملفات التي تريد **إضافة المستندات إلى الفهرس**.  
- `search()` ينفذ استعلام البدل ويعيد النتائج المطابقة.

### الميزة 2: بحث بديل قائم على الكائن

#### الخطوة 1 – إعداد الفهرس (نفس السابق)
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### الخطوة 2 – بناء `WordPattern` لاستعلامات معقدة
تمنحك عمليات البحث القائمة على الكائنات تحكمًا دقيقًا في كل عنصر من عناصر النمط:

```java
// Create a WordPattern for 'm???is'
WordPattern pattern1 = new WordPattern();
pattern1.appendString("m");
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendString("is");

SearchQuery query1 = SearchQuery.createWordPatternQuery(pattern1);
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Create a WordPattern for 'pri?(1~7)'
WordPattern pattern2 = new WordPattern();
pattern2.appendString("pri");
pattern2.appendWildcard(1, 7);

SearchQuery query2 = SearchQuery.createWordPatternQuery(pattern2);
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**شرح**  
- `WordPattern` يتيح لك تجميع نمط بحث خطوة بخطوة.  
- `appendOneCharacterWildcard()` يضيف عنصر نائب `?`.  
- `appendWildcard(min, max)` يضيف بديلًا يعتمد على النطاق (`?(min~max)`).  

## التطبيقات العملية
1. **Document Management:** حدد موقع الملفات بسرعة عندما يكون معروفًا فقط جزء من المصطلح.  
2. **Content Retrieval Engines:** تشغيل أشرطة البحث في منصات CMS مع مطابقة مرنة.  
3. **Data Mining:** استخراج بيانات نمطية من مجموعات نصية كبيرة دون مسح النص الكامل.

## اعتبارات الأداء

### تحسين فهرس البحث
- **Regular Re‑indexing:** بعد التحديثات الضخمة، أعد بناء الفهرس للحفاظ على انخفاض أوقات البحث.  
- **Compact Storage:** استخدم `index.optimize()` (إن كان متاحًا) لتقليل حجم الفهرس.

### إدارة ذاكرة البحث في جافا
- **Heap Size:** خصص مساحة كومة كافية (`-Xmx2g` أو أعلى) لمجموعات المستندات الكبيرة.  
- **Streaming Indexing:** عالج الملفات على دفعات لتجنب تحميل كل شيء في الذاكرة مرة واحدة.

### ممارسات عامة موصى بها
- حافظ على أن تكون أنماط البدل محددة قدر الإمكان؛ الأنماط الواسعة جدًا تزيد من حمل المعالج.  
- راقب توقفات GC إذا لاحظت ارتفاعًا في زمن الاستجابة أثناء أعباء البحث الثقيلة.

## الخلاصة
من خلال تعلم كيفية **إضافة المستندات إلى الفهرس** والاستفادة من استعلامات البدل القائمة على النص والكائن، يمكنك تحسين تجربة البحث بشكل كبير في أي تطبيق جافا. تذكر أن تقوم **تحسين فهرس البحث** بانتظام وإدارة الذاكرة بحكمة للحصول على أداء قابل للتوسع. جرب أنماطًا مختلفة، ودمج الكود في خدماتك، واستمتع بنتائج بحث سريعة ومرنة اليوم!

## الأسئلة المتكررة

**س1: ما هو البحث بالبدل؟**  
ج: يسمح لك البحث بالبدل بمطابقة كلمات أو عبارات باستخدام عناصر نائبة مثل `?` (حرف واحد) أو `*` (عدة أحرف).

**س2: كيف أقوم بتثبيت GroupDocs.Search لجافا؟**  
ج: استخدم Maven مع المستودع والتبعية الموضحة أعلاه، أو قم بتنزيل ملف JAR مباشرة من صفحة الإصدار الرسمية.

**س3: هل يمكن لعمليات البحث بالبدل التعامل مع مجموعات بيانات كبيرة؟**  
ج: نعم، ولكن يجب عليك **تحسين فهرس البحث** ومراقبة **إدارة ذاكرة البحث في جافا** للحفاظ على الأداء.

**س4: ما هي الأخطاء الشائعة؟**  
ج: مسارات الفهرس غير الصحيحة، واستخدام بدائل عامة جدًا، وإهمال إعدادات الذاكرة يمكن أن يسبب بطء في البحث أو أخطاء نفاد الذاكرة.

**س5: أين يمكنني العثور على المزيد من الموارد؟**  
ج: زر [GroupDocs documentation](https://docs.groupdocs.com/search/java/) للحصول على أدلة مفصلة ومراجع API.

## الموارد

- **Documentation:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference:** [GroupDocs Search API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [GroupDocs.Search Downloads](https://releases.groupdocs.com/search/java/)
- **GitHub:** [GroupDocs.Search on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**آخر تحديث:** 2026-03-23  
**تم الاختبار مع:** GroupDocs.Search 25.4 for Java  
**المؤلف:** GroupDocs
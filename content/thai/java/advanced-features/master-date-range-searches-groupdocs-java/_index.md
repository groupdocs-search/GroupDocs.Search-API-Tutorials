---
date: '2026-10-07'
description: เรียนรู้วิธีการทำการค้นหาแบบกำหนดรูปแบบวันที่สำหรับ Java ด้วย GroupDocs
  รวมถึงการค้นหาช่วงวันที่, รูปแบบกำหนดเอง, และเคล็ดลับประสิทธิภาพ
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: บทแนะนำรูปแบบวันที่แบบกำหนดเองสำหรับ Java แสดงวิธีการตั้งค่า GroupDocs.Search
  สำหรับ Java, รันการค้นหาช่วงวันที่, และเพิ่มประสิทธิภาพ. ทำตามตัวอย่างขั้นตอนต่อขั้นตอน
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: รูปแบบวันที่แบบกำหนดเองสำหรับ Java – คู่มือการค้นหาช่วงวันที่ด้วย GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: รูปแบบวันที่แบบกำหนดเองสำหรับ Java | การค้นหาช่วงวันที่ด้วย GroupDocs
type: docs
url: /th/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# รูปแบบวันที่แบบกำหนดเองใน Java | การค้นหาช่วงวันที่ด้วย GroupDocs

การค้นหาเอกสารตามวันที่เป็นความต้องการที่พบบ่อย—ไม่ว่าจะคุณกำลังสร้างระบบจัดเก็บเอกสาร, เครื่องมือรายงานการเงิน, หรือพอร์ทัลการจัดการเนื้อหา ในบทแนะนำนี้คุณจะได้เรียนรู้เทคนิค **custom date format java** ด้วย GroupDocs.Search ครอบคลุมการค้นหาช่วงวันที่, การกำหนดรูปแบบแบบกำหนดเอง, และเคล็ดลับเพื่อ **optimize search performance**. เมื่อจบคุณจะสามารถให้ผู้ใช้ดึงบันทึกที่อยู่ในช่วงวันที่ใด ๆ ไม่ว่ารูปแบบจะเป็นแบบใดก็ตาม

## คำตอบสั้น
- **คลาสหลักสำหรับการทำดัชนีคืออะไร?** `Index` from the `com.groupdocs.search` package.  
- **คุณกำหนดรูปแบบวันที่แบบกำหนดเองอย่างไร?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **ฉันสามารถค้นหาด้วยข้อความ query ได้หรือไม่?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **พิกัด Maven ที่ต้องการคืออะไร?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## custom date format java คืออะไร?
Custom date format java บอก GroupDocs.Search ว่าจะตีความสตริงวันที่ที่ไม่เป็นไปตามรูปแบบ ISO เริ่มต้น (YYYY‑MM‑DD) อย่างไร โดยการกำหนดรูปแบบของคุณเอง—เช่น `MM/dd/yyyy` หรือ `dd‑MM‑yyyy`—คุณทำให้เอนจินสามารถรับรู้วันที่ที่ฝังอยู่ในเอกสารที่ใช้รูปแบบตามภูมิภาคหรือรูปแบบเก่า ความสามารถนี้ทำให้คุณสามารถทำดัชนีและค้นหาวันที่ได้อย่างสม่ำเสมอจากแหล่งข้อมูลที่หลากหลาย ปรับปรุงทั้งการเรียกคืนและความแม่นยำสำหรับการค้นหาที่เน้นวันที่

## ทำไมต้องใช้ GroupDocs.Search สำหรับการค้นหาช่วงวันที่?
GroupDocs.Search ผสานการทำดัชนีความเร็วสูงกับการสร้าง query ที่ยืดหยุ่น ทำให้เหมาะสำหรับสถานการณ์ช่วงวันที่ เอนจินสามารถค้นหาเอกสารที่มีวันที่อยู่ในช่วงที่กำหนดได้อย่างรวดเร็ว แม้ว่าวันที่นั้นจะปรากฏในข้อความอิสระหรือฟิลด์เมตาดาต้า การสนับสนุนในตัวสำหรับหลายรูปแบบไฟล์และตัวแยกวิเคราะห์วันที่ที่กำหนดเองหมายความว่าคุณสามารถจัดการกับคอลเลกชันเอกสารที่หลากหลายโดยไม่ต้องเขียนโค้ดเฉพาะรูปแบบ ในขณะเดียวกันยังคงให้เวลาตอบสนองระดับมิลลิวินาทีสำหรับดัชนีขนาดใหญ่

## วิธีค้นหาเอกสารตามวันที่ด้วย GroupDocs.Search
คุณจะตั้งค่าห้องสมุด, ทำดัชนีโฟลเดอร์ตัวอย่าง, แล้วรันทั้ง query แบบข้อความธรรมดาและ query แบบออบเจกต์ที่ซับซ้อน กระบวนการเริ่มจากการสร้างอินสแตนซ์ `Index`, กำหนดค่ารูปแบบวันที่แบบกำหนดเองที่ต้องการ, แล้วเรียกใช้ API การค้นหาด้วยสตริงธรรมดาหรือ `SearchQuery` ที่มีโครงสร้าง วิธีนี้ทำให้คุณเลือกระดับการควบคุมที่ตรงกับความต้องการของแอปพลิเคชันของคุณ

### ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า
- Maven สำหรับการจัดการ dependencies
- เข้าถึงใบอนุญาต GroupDocs.Search (รุ่นทดลองหรือชั่วคราวใช้ได้สำหรับการพัฒนา)

### การตั้งค่า GroupDocs.Search สำหรับ Java

#### การติดตั้งโดยใช้ Maven
Add the repository and dependency to your `pom.xml`:

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

#### ดาวน์โหลดโดยตรง
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### การเริ่มต้นและตั้งค่าพื้นฐาน
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** คลาส `Index` เป็นคอนเทนเนอร์หลักที่เก็บเมตาดาต้าสำหรับการค้นหาของทุกไฟล์ที่คุณเพิ่ม ทำให้ค้นหาได้อย่างรวดเร็วในคอลเลกชันขนาดใหญ่

## คุณลักษณะ 1: การสร้าง query ค้นหาช่วงวันที่

### ใช้ query แบบข้อความ
วิธีที่ง่ายที่สุดคือฝังช่วงวันที่โดยตรงในสตริง query:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** โหลดดัชนีของคุณ, จากนั้นเรียก `search("daterange(2022-01-01 ~~ 2022-12-31)")` เพื่อดึงเอกสารทุกไฟล์ที่วันที่ทำดัชนีอยู่ระหว่าง 1 มกราคม 2022 ถึง 31 ธันวาคม 2022 Query หนึ่งบรรทัดนี้ทำงานได้ทันทีและคืนผลลัพธ์ตามความเกี่ยวข้อง

**Explanation:** ไวยากรณ์ `daterange` คาดหวังวันที่ในรูปแบบ `YYYY‑MM‑DD`. มันจะคืนเอกสารทั้งหมดที่วันที่ทำดัชนีอยู่ในช่วงนั้น

### ใช้ query แบบออบเจกต์
สำหรับการควบคุมแบบโปรแกรมและการแยกวิเคราะห์แบบกำหนดเอง, สร้างออบเจกต์ `SearchQuery`. คลาส `SearchQuery` แสดง query ที่มีโครงสร้างซึ่งสามารถรวมหลายเกณฑ์เช่น คำสำคัญ, ตัวกรอง, และช่วงวันที่

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** สร้าง `SearchQuery` ด้วย `createDateRangeQuery(startDate, endDate)` โดยที่ `startDate` และ `endDate` เป็นอินสแตนซ์ของ `java.util.Date`; จากนั้นส่ง query ไปยัง `index.search(query)` เพื่อรับผลลัพธ์ที่แม่นยำซึ่งคำนึงถึงการชดเชยโซนเวลาและปฏิทินตามท้องถิ่น

**Definition anchor:** คลาส `SearchQuery` รวมเกณฑ์การค้นหาทั้งหมด, ช่วยให้คุณรวมช่วงวันที่กับตัวกรองคำสำคัญ, ตัวดำเนินการ Boolean, และกฎการเพิ่มคะแนน

**Explanation:** `createDateRangeQuery` ให้คุณส่งออบเจกต์ `java.util.Date`, ให้ความยืดหยุ่นเต็มที่ต่อโซนเวลาและการจัดการตามท้องถิ่น

## คุณลักษณะ 2: การระบุรูปแบบวันที่แบบกำหนดเองใน Java

### การตั้งค่ารูปแบบวันที่แบบกำหนดเอง
คลาส `DateFormat` บอกเอนจินว่าจะตัดและตีความสตริงวันที่อย่างไรโดยอิงจากลำดับขององค์ประกอบและอักขระตัวคั่น กำหนด `DateFormat` ที่ตรงกับการแสดงวันที่ของเอกสารของคุณ:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** ล้างรูปแบบเริ่มต้นด้วย `dateFormat.clear()`, จากนั้นเพิ่ม `DateFormat` ใหม่ที่สร้างจากออบเจกต์ `DateFormatElement` (เดือน, วัน, ปี) และตั้งค่าตัวคั่นเป็น `/`. หลังจากนี้เอนจินจะสามารถแยกวิเคราะห์วันที่ที่เขียนเป็น `MM/dd/yyyy` ได้อย่างถูกต้องในระหว่างการทำดัชนีและการ query

**Definition anchor:** `DateFormat` เป็นออบเจกต์การกำหนดค่าที่บอก GroupDocs.Search วิธีการตัดและตีความสตริงวันที่โดยอิงจากลำดับขององค์ประกอบและอักขระตัวคั่น

**Explanation:** โดยการล้างรูปแบบเริ่มต้นและเพิ่ม `DateFormat` ที่ใช้ `/` เป็นตัวคั่น, เอนจินจะเข้าใจวันที่ที่เขียนเป็น `MM/dd/yyyy` ตอนนี้ นี่เป็นสิ่งสำคัญสำหรับ **search documents by date** ในภูมิภาคที่นิยมรูปแบบเดือน‑ก่อนวัน

## เคล็ดลับเพื่อเพิ่มประสิทธิภาพการค้นหา
- **Index incrementally:** เพิ่มไฟล์ใหม่ลงในดัชนีที่มีอยู่แทนการสร้างใหม่จากศูนย์; นี้ลดการใช้ CPU ได้สูงสุด 70 % สำหรับการอัปเดตรายวัน.  
- **Prune stale data:** ลบเอกสารที่ไม่จำเป็นออกเป็นระยะ; ดัชนีที่เบาจะเพิ่มอัตราการฮิตของแคชและลดความหน่วงของ query.  
- **Adjust memory settings:** เพิ่มขนาด heap ของ JVM (`-Xmx4g` หรือสูงกว่า) เมื่อทำงานกับดัชนีที่ใหญ่กว่า 5 GB เพื่อหลีกเลี่ยงข้อผิดพลาด out‑of‑memory.  
- **Enable multi‑threaded indexing:** ใช้ `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` เพื่อทำให้การประมวลผลเอกสารทำงานแบบขนานและลดเวลาการทำดัชนีโดยประมาณเท่ากับจำนวนคอร์ของ CPU.

## ปัญหาทั่วไปและวิธีแก
- **Date parsing errors:** ตรวจสอบให้แน่ใจว่าสตริงวันที่ของเอกสารตรงกับรูปแบบที่คุณกำหนด; ตัวคั่นที่ไม่ตรงหรือขาดศูนย์นำหน้าอาจทำให้ล้มเหลว.  
- **Missing results:** ตรวจสอบให้แน่ใจว่าฟิลด์ที่ทำดัชนีมีเมตาดาต้าของวันที่; หากเอกสารมีวันที่เฉพาะในย่อหน้าข้อความอิสระ, ให้เปิดใช้งานตัวเลือก `ExtractDateMetadata` ระหว่างการทำดัชนี.  
- **Index access exceptions:** ยืนยันว่าเส้นทาง `indexFolder` สามารถเขียนได้และไม่ได้ถูกล็อกโดยกระบวนการอื่น; ใช้โฟลเดอร์แยกสำหรับแต่ละสภาพแวดล้อม (dev, test, prod) เพื่อหลีกเลี่ยงความขัดแย้ง.

## การประยุกต์ใช้งานจริง
1. **Archival systems** – ดึงบันทึกจากช่วงเวลาประวัติศาสตร์ที่กำหนดโดยไม่ต้องทำการปรับรูปแบบวันที่ด้วยตนเอง.  
2. **Content management** – รองรับรูปแบบวันที่ตามภูมิภาคเช่น `dd/MM/yyyy` สำหรับผู้ใช้ในยุโรป, เพิ่มความพึงพอใจของผู้ใช้.  
3. **Financial software** – กรองธุรกรรมตามไตรมาสหรือปีการเงินอย่างรวดเร็ว, ทำให้แดชบอร์ดรายงานแบบเรียลไทม์ทำงานได้.

## ทำไมเรื่องนี้ถึงสำคัญ
การนำการจัดการ **custom date format java** ไปใช้ช่วยขจัดความยุ่งยากจากการจัดการรูปแบบวันที่ที่ไม่สอดคล้องกันในเอกสารต่าง ๆ ทำให้คุณสามารถ **handle multiple date formats** ในดัชนีเดียว, ทำให้ผู้ใช้ปลายทางได้รับผลลัพธ์ที่แม่นยำไม่ว่ารูปแบบวันที่จะบันทึกอย่างไร ความยืดหยุ่นนี้ปรับปรุงความเกี่ยวข้องของการค้นหา, ลดความพยายามในการเตรียมข้อมูลล่วงหน้า, และลดเวลาในการสร้างคุณค่าให้กับแอปพลิเคชันที่เน้นวันที่

## ขั้นตอนต่อไป
- สำรวจการรวม query ขั้นสูงเพิ่มเติมโดยใช้ตัวดำเนินการ `AND`, `OR`, และ `NOT`.  
- ทดลองใช้ custom analyzers หากคุณต้องการทำดัชนีเมตาดาต้าเชิงเวลาเพิ่มเติม เช่น timestamp ที่ฝังในแท็ก XML.  
- ตรวจสอบคู่มือการปรับจูนประสิทธิภาพในเอกสารอย่างเป็นทางการเพื่อขยายโซลูชันของคุณให้รองรับเอกสารหลายล้านรายการและสภาพแวดล้อมหลายผู้เช่า.

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง query แบบข้อความและ query แบบออบเจกต์คืออะไร?**  
A: รูปแบบข้อความเร็วและง่ายแต่จำกัดอยู่ที่รูปแบบ ISO เริ่มต้น; query แบบออบเจกต์ให้คุณส่งออบเจกต์ `Date` และรูปแบบกำหนดเองเพื่อความยืดหยุ่นที่มากขึ้น.

**Q: ฉันสามารถค้นหาหลายช่วงวันที่ใน query เดียวได้หรือไม่?**  
A: ได้, รวมเงื่อนไข `daterange` กับตัวดำเนินการเชิงตรรกะเช่น `AND` หรือ `OR` เพื่อสร้าง query ที่ซับซ้อน.

**Q: รูปแบบวันที่แบบกำหนดเองจะทำให้การค้นหาช้าลงหรือไม่?**  
A: มีค่าใช้จ่ายเล็กน้อยสำหรับการแยกวิเคราะห์เพิ่มเติม, แต่ผลกระทบนั้นเล็กน้อยสำหรับภาระงานทั่วไปและได้รับการชดเชยโดยความแม่นยำที่เพิ่มขึ้น.

**Q: GroupDocs.Search เหมาะสำหรับการใช้งานขนาดใหญ่หรือไม่?**  
A: แน่นอน. ด้วยกลยุทธ์การทำดัชนีที่เหมาะสมและการปรับจูน JVM, มันสามารถขยายได้ถึงหลายล้านเอกสารพร้อมรักษาเวลาตอบสนองของ query ในระดับมิลลิวินาที.

**Q: ฉันสามารถหา ตัวอย่าง Java เพิ่มเติมได้จากที่ไหน?**  
A: สำรวจ [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) เพื่อดูตัวอย่างเพิ่มเติมและการนำไปใช้ในกรณีต่าง ๆ.

**Resources**
- **Documentation:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub repository:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **View on GitHub:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free support forum:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Temporary license:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

**Last Updated:** 2026-10-07  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง
- [คุณลักษณะการค้นหาเชิงลึกของ Groupdocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [ไลบรารีการค้นหาข้อความเต็ม Java – ปรับแต่งดัชนีด้วย GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [วิธีเพิ่มเอกสารลงในดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
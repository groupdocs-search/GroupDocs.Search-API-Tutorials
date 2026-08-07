---
date: '2026-03-04'
description: เรียนรู้วิธีการทำการค้นหาแบบกำหนดรูปแบบวันที่ใน Java ด้วย GroupDocs.Search
  รวมถึงการค้นหาช่วงวันที่ รูปแบบที่กำหนดเอง และเคล็ดลับด้านประสิทธิภาพ
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: รูปแบบวันที่กำหนดเองใน Java | การค้นหาช่วงวันที่ด้วย GroupDocs
type: docs
url: /th/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Custom Date Format Java | Date Range Search with GroupDocs

การค้นหาเอกสารตามวันที่เป็นความต้องการที่พบบ่อย—ไม่ว่าจะเป็นการสร้างระบบจัดเก็บเอกสาร, เครื่องมือรายงานการเงิน, หรือพอร์ทัลการจัดการเนื้อหา ในบทแนะนำนี้คุณจะได้เรียนรู้เทคนิค **custom date format java** ด้วย GroupDocs.Search ครอบคลุมการค้นหาแบบช่วงวันที่, การกำหนดรูปแบบแบบกำหนดเอง, และเคล็ดลับเพื่อ **optimize search performance** เมื่อจบคุณจะสามารถให้ผู้ใช้ดึงข้อมูลที่อยู่ในช่วงวันที่ใดก็ได้ ไม่ว่าฟอร์แมตจะเป็นแบบใดก็ตาม

## Quick Answers
- **What is the primary class for indexing?** `Index` จากแพคเกจ `com.groupdocs.search`  
- **How do you define a custom date pattern?** ใช้ `DateFormat` พร้อมอ็อบเจกต์ `DateFormatElement` และตัวคั่น  
- **Can I search with a text query?** ได้, ไวยากรณ์ `daterange(start ~~ end)` ทำงานโดยตรงในสตริงคิวรี  
- **Which Maven coordinates are required?** `com.groupdocs:groupdocs-search:25.4` (หรือใหม่กว่า)  
- **Do I need a license for development?** ไลเซนส์ทดลองหรือไลเซนส์ชั่วคราวเพียงพอสำหรับการทดสอบ; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง  

## What is **custom date format java**?
**custom date format java** บอก GroupDocs.Search ว่าจะตีความสตริงวันที่ที่ไม่เป็นไปตามรูปแบบ ISO เริ่มต้น (YYYY‑MM‑DD) อย่างไร โดยการกำหนดรูปแบบของคุณเอง เช่น `MM/dd/yyyy` หรือ `dd‑MM‑yyyy` ทำให้เอนจินสามารถรับรู้วันที่ที่ฝังอยู่ในเอกสารที่ใช้รูปแบบตามภูมิภาคหรือรูปแบบเก่าได้  

## Why use GroupDocs.Search for date range queries?
- **Speed:** การทำดัชนีในตัวทำให้การค้นหาเป็น O(log n)  
- **Flexibility:** รองรับการสร้างคิวรีทั้งแบบข้อความและแบบอ็อบเจกต์  
- **Multi‑format support:** จัดการ PDF, Word, Excel, plain text และอื่น ๆ โดยไม่ต้องเขียนโค้ดเพิ่ม  

## How to **search documents by date** with GroupDocs.Search
ต่อไปนี้เป็นคู่มือขั้นตอนต่อขั้นตอนที่อธิบายการตั้งค่าห้องสมุด, การทำดัชนีไฟล์, และการดำเนินการค้นหาแบบช่วงวันที่ทั้งแบบง่ายและขั้นสูง  

### Prerequisites
- ติดตั้ง Java 8 หรือใหม่กว่า  
- มี Maven สำหรับจัดการ dependencies  
- มีไลเซนส์ GroupDocs.Search (ไลเซนส์ทดลองหรือชั่วคราวใช้ได้สำหรับการพัฒนา)  

### Setting Up GroupDocs.Search for Java

#### Installation Using Maven
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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

#### Direct Download
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)  

#### Basic Initialization and Setup
สร้างอินสแตนซ์ `Index` แล้วเพิ่มเอกสารของคุณ:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Feature 1: Creating Date Range Search Queries

### Using Text Form Query
วิธีที่ง่ายที่สุดคือใส่ช่วงวันที่โดยตรงในสตริงคิวรี:

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

**Explanation**: ไวยากรณ์ `daterange` ต้องการวันที่ในรูปแบบ `YYYY‑MM‑DD` และจะคืนเอกสารทั้งหมดที่วันที่ที่ทำดัชนีอยู่ในช่วงที่กำหนด  

### Using Query Object
หากต้องการควบคุมโปรแกรมและการแปลงแบบกำหนดเอง ให้สร้างอ็อบเจกต์ `SearchQuery`:

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

**Explanation**: `createDateRangeQuery` ให้คุณส่งอ็อบเจกต์ `java.util.Date` ทำให้คุณจัดการโซนเวลาและการแปลงตาม locale ได้อย่างเต็มที่  

## Feature 2: Specifying **custom date format java** Patterns

### Setting Custom Date Formats
กำหนด `DateFormat` ที่ตรงกับรูปแบบวันที่ในเอกสารของคุณ:

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

**Explanation**: การล้างรูปแบบเริ่มต้นและเพิ่ม `DateFormat` ที่ใช้ `/` เป็นตัวคั่น ทำให้เอนจินเข้าใจวันที่ในรูปแบบ `MM/dd/yyyy` ซึ่งจำเป็นสำหรับ **search documents by date** ในภูมิภาคที่นิยมใช้รูปแบบเดือน‑วัน‑ปี  

## Tips to **optimize search performance**
- **Index Incrementally**: เพิ่มไฟล์ใหม่ลงในดัชนีที่มีอยู่แทนการสร้างใหม่ทั้งหมด  
- **Prune Stale Data**: ลบเอกสารที่ไม่จำเป็นออกเป็นระยะ  
- **Adjust Memory Settings**: เพิ่มขนาด heap ของ JVM (`-Xmx`) เมื่อทำงานกับดัชนีขนาดใหญ่  

## Common Issues and Solutions
- **Date Parsing Errors**: ตรวจสอบให้แน่ใจว่าสตริงวันที่ในเอกสารตรงกับรูปแบบที่คุณกำหนดไว้  
- **Missing Results**: ยืนยันว่า ฟิลด์ที่ทำดัชนีมีเมตาดาต้าด้านวันที่; หากไม่มีเอนจินจะไม่สามารถจับคู่คิวรีวันที่ได้  
- **Index Access Exceptions**: ตรวจสอบว่าเส้นทาง `indexFolder` สามารถเขียนได้และไม่ได้ถูกล็อกโดยโปรเซสอื่น  

## Practical Applications
1. **Archival Systems** – ดึงบันทึกจากช่วงเวลาประวัติศาสตร์ที่กำหนด  
2. **Content Management** – รองรับรูปแบบวันที่ตามภูมิภาคเช่น `dd/MM/yyyy` สำหรับผู้ใช้ยุโรป  
3. **Financial Software** – กรองธุรกรรมตามไตรมาสหรือปีการเงินอย่างรวดเร็ว  

## Why This Matters
การจัดการ **custom date format java** ช่วยขจัดความยุ่งยากจากรูปแบบวันที่ที่ไม่สอดคล้องกันในเอกสารหลายประเภท ทำให้คุณสามารถ **handle multiple date formats** ในดัชนีเดียวได้ และผู้ใช้จะได้รับผลลัพธ์ที่แม่นยำไม่ว่าข้อมูลวันที่จะบันทึกไว้ในรูปแบบใด  

## Next Steps
- ทดลองผสมผสานคิวรีขั้นสูงด้วยตัวดำเนินการ `AND`, `OR`, และ `NOT`  
- ทดลองใช้ custom analyzers หากต้องการทำดัชนีเมตาดาต้าเชิงเวลาเพิ่มเติม  
- ศึกษาคู่มือการปรับจูนประสิทธิภาพในเอกสารอย่างเป็นทางการเพื่อขยายโซลูชันให้รองรับเอกสารหลายล้านฉบับ  

## Frequently Asked Questions

**Q: What is the difference between text form and object‑based date queries?**  
A: Text form รวดเร็วและง่ายแต่จำกัดที่รูปแบบ ISO เริ่มต้น; object‑based queries ให้คุณส่งอ็อบเจกต์ `Date` และรูปแบบกำหนดเองเพื่อความยืดหยุ่นมากขึ้น  

**Q: Can I search for multiple date ranges in a single query?**  
A: ใช่, สามารถรวม clause `daterange` ด้วยตัวดำเนินการเชิงตรรกะเช่น `AND` หรือ `OR` เพื่อสร้างคิวรีซับซ้อน  

**Q: Will custom date formats slow down the search?**  
A: มีค่าโอเวอร์เฮดจากการแปลงเพิ่มเล็กน้อย แต่ผลกระทบโดยรวมถือว่าไม่สำคัญสำหรับงานทั่วไปและคุ้มค่ากับความแม่นยำที่เพิ่มขึ้น  

**Q: Is GroupDocs.Search suitable for large‑scale deployments?**  
A: แน่นอน. ด้วยกลยุทธ์การทำดัชนีที่เหมาะสมและการปรับจูน JVM สามารถรองรับเอกสารระดับล้านฉบับได้  

**Q: Where can I find more Java examples?**  
A: สำรวจ [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) เพื่อดูตัวอย่างและการใช้งานเพิ่มเติม  

---

**Resources**

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-03-04  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs
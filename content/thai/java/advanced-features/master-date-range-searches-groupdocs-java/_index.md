---
date: '2025-12-18'
description: เรียนรู้วิธีการใช้งานการค้นหา Java ด้วยรูปแบบวันที่ที่กำหนดเองใน GroupDocs.Search
  รวมถึงการค้นหาช่วงวันที่ รูปแบบที่กำหนดเอง และเคล็ดลับด้านประสิทธิภาพ
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'รูปแบบวันที่กำหนดเองใน Java: การค้นหาช่วงวันที่ด้วย GroupDocs'
type: docs
url: /th/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# รูปแบบวันที่กำหนดเองใน Java: การค้นหาช่วงวันที่ด้วย GroupDocs

การค้นหาเอกสารตามวันที่เป็นความต้องการที่พบบ่อย—ไม่ว่าจะเป็นการสร้างระบบจัดเก็บเอกสาร, เครื่องมือรายงานการเงิน, หรือพอร์ทัลการจัดการเนื้อหา ในบทแนะนำนี้คุณจะได้เรียนรู้เทคนิค **custom date format java** ด้วย GroupDocs.Search ซึ่งครอบคลุมการค้นหาช่วงวันที่, การกำหนดรูปแบบที่กำหนดเอง, และเคล็ดลับเพื่อ **optimize search performance**. เมื่อจบคุณจะสามารถให้ผู้ใช้ดึงข้อมูลที่อยู่ในช่วงวันที่ใด ๆ ไม่ว่าจะใช้รูปแบบใดก็ตาม

## คำตอบด่วน
- **คลาสหลักสำหรับการทำดัชนีคืออะไร?** `Index` from the `com.groupdocs.search` package.  
- **คุณกำหนดรูปแบบวันที่กำหนดเองอย่างไร?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **ฉันสามารถค้นหาด้วยข้อความ query ได้หรือไม่?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **ต้องการพิกัด Maven ใด?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## **custom date format java** คืออะไร?
**custom date format java** บอกกับ GroupDocs.Search ว่าจะตีความสตริงวันที่ที่ไม่เป็นไปตามรูปแบบ ISO เริ่มต้น (YYYY‑MM‑DD) อย่างไร โดยการกำหนดรูปแบบของคุณเอง—เช่น `MM/dd/yyyy` หรือ `dd‑MM‑yyyy`—คุณทำให้เอนจินสามารถรับรู้วันที่ที่ฝังอยู่ในเอกสารที่ใช้รูปแบบตามภูมิภาคหรือรูปแบบเก่าได้

## ทำไมต้องใช้ GroupDocs.Search สำหรับการค้นหาช่วงวันที่?
- **ความเร็ว:** Built‑in indexing makes look‑ups O(log n).  
- **ความยืดหยุ่น:** Supports both text‑based and object‑based query creation.  
- **รองรับหลายรูปแบบ:** Handles PDFs, Word, Excel, plain text, and more without extra code.  

## วิธี **search documents by date** ด้วย GroupDocs.Search
ด้านล่างคุณจะพบคู่มือแบบขั้นตอนต่อขั้นตอนที่พาคุณผ่านการตั้งค่าห้องสมุด, การทำดัชนีไฟล์, และการดำเนินการค้นหาช่วงวันที่ทั้งแบบง่ายและขั้นสูง

### ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า
- Maven สำหรับการจัดการ dependencies
- เข้าถึงใบอนุญาต GroupDocs.Search (รุ่นทดลองหรือชั่วคราวใช้ได้สำหรับการพัฒนา)

### การตั้งค่า GroupDocs.Search สำหรับ Java

#### การติดตั้งโดยใช้ Maven
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

#### ดาวน์โหลดโดยตรง
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### การเริ่มต้นและตั้งค่าเบื้องต้น
สร้างอินสแตนซ์ `Index` และเพิ่มเอกสารของคุณ:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## ฟีเจอร์ 1: การสร้างคำค้นหาช่วงวันที่

### การใช้ Text Form Query
วิธีที่ง่ายที่สุดคือการฝังช่วงวันที่โดยตรงในสตริง query:

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

**คำอธิบาย**: The `daterange` syntax expects dates in `YYYY‑MM‑DD`. It returns all documents whose indexed dates fall within the interval.

### การใช้ Query Object
สำหรับการควบคุมแบบโปรแกรมและการแยกวิเคราะห์แบบกำหนดเอง ให้สร้างอ็อบเจ็กต์ `SearchQuery`:

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

**คำอธิบาย**: `createDateRangeQuery` lets you supply `java.util.Date` objects, giving you full flexibility over time zones and locale‑specific handling.

## ฟีเจอร์ 2: การระบุรูปแบบ **custom date format java** 

### การตั้งค่ารูปแบบวันที่กำหนดเอง
กำหนด `DateFormat` ที่ตรงกับการแสดงวันที่ในเอกสารของคุณ:

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

**คำอธิบาย**: By clearing the default formats and adding a `DateFormat` that uses `/` as the separator, the engine now understands dates written as `MM/dd/yyyy`. This is essential for **search documents by date** in regions that prefer month‑first notation.

## เคล็ดลับเพื่อ **optimize search performance**
- **เพิ่มดัชนีแบบต่อเนื่อง**: Add new files to the existing index instead of rebuilding from scratch.  
- **ลบข้อมูลที่ล้าสมัย**: Periodically remove documents that are no longer needed.  
- **ปรับการตั้งค่าหน่วยความจำ**: Increase the JVM heap (`-Xmx`) when working with large indexes.  

## ปัญหาที่พบบ่อยและวิธีแก้
- **ข้อผิดพลาดการแยกวิเคราะห์วันที่**: Verify that the document’s date strings exactly match the custom pattern you defined.  
- **ผลลัพธ์หายไป**: Ensure the indexed fields contain date metadata; otherwise, the engine cannot match date queries.  
- **ข้อยกเว้นการเข้าถึงดัชนี**: Confirm that the `indexFolder` path is writable and not locked by another process.  

## การประยุกต์ใช้งานจริง
1. **ระบบจัดเก็บเอกสาร** – Retrieve records from a specific historical period.  
2. **การจัดการเนื้อหา** – Support regional date formats like `dd/MM/yyyy` for European audiences.  
3. **ซอฟต์แวร์การเงิน** – Filter transactions by fiscal quarter or year quickly.  

## สรุป
คุณตอนนี้มีชุดเครื่องมือ **custom date format java** ครบถ้วนสำหรับการสร้างการค้นหาช่วงวันที่ที่มีประสิทธิภาพด้วย GroupDocs.Search. นำรูปแบบเหล่านี้ไปใช้, ปรับแต่งประสิทธิภาพ, และแอปพลิเคชันของคุณจะให้ผลลัพธ์ที่เร็วและแม่นยำสำหรับการค้นหาเชิงเวลาใด ๆ  

## คำถามที่พบบ่อย

**ถาม: ความแตกต่างระหว่างการค้นหาแบบ text form กับ object‑based คืออะไร?**  
A: การค้นหาแบบ text form เร็วและง่ายแต่จำกัดอยู่ที่รูปแบบ ISO เริ่มต้น; การค้นหาแบบ object‑based ให้คุณส่งอ็อบเจ็กต์ `Date` และรูปแบบกำหนดเองเพื่อความยืดหยุ่นที่มากขึ้น  

**ถาม: ฉันสามารถค้นหาหลายช่วงวันที่ใน query เดียวได้หรือไม่?**  
A: ใช่, รวมเงื่อนไข `daterange` กับตัวดำเนินการเชิงตรรกะเช่น `AND` หรือ `OR` เพื่อสร้าง query ที่ซับซ้อน  

**ถาม: รูปแบบวันที่กำหนดเองจะทำให้การค้นหาช้าลงหรือไม่?**  
A: มีค่าโอเวอร์เฮดเล็กน้อยสำหรับการแยกวิเคราะห์เพิ่มเติม, แต่ผลกระทบนั้นเล็กน้อยสำหรับงานทั่วไปและคุ้มค่ากับความแม่นยำที่เพิ่มขึ้น  

**ถาม: GroupDocs.Search เหมาะกับการใช้งานขนาดใหญ่หรือไม่?**  
A: แน่นอน. ด้วยกลยุทธ์การทำดัชนีที่เหมาะสมและการปรับจูน JVM, สามารถขยายได้ถึงหลายล้านเอกสาร  

**ถาม: ฉันจะหา ตัวอย่าง Java เพิ่มเติมได้จากที่ไหน?**  
A: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) for additional samples and use‑case implementations.  

---

**เอกสาร**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
**อ้างอิง API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
**ดาวน์โหลด**: [Get the latest version here](https://releases.groupdocs.com/search/java/)  
**ที่เก็บ GitHub**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
**ฟอรั่มสนับสนุนฟรี**: [Join the discussion](https://forum.groupdocs.com/c/search/10)  
**ใบอนุญาตชั่วคราว**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)  

---

**อัปเดตล่าสุด:** 2025-12-18  
**ทดสอบด้วย:** GroupDocs.Search Java 25.4  
**ผู้เขียน:** GroupDocs  

---
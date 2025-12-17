---
date: '2025-12-16'
description: เรียนรู้วิธีสร้างดัชนีการค้นหาใน Java และดำเนินการค้นหาแบบ faceted และซับซ้อนโดยใช้
  GroupDocs.Search เพื่อเพิ่มประสิทธิภาพการค้นหาและประสบการณ์ผู้ใช้
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: สร้างดัชนีการค้นหา Java – การค้นหาแบบหลายมิติและซับซ้อน
type: docs
url: /th/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# สร้างดัชนีการค้นหา Java – Faceted & Complex Searches

การนำประสบการณ์ **search experience** ที่ทรงพลังใน Java ไปใช้สามารถรู้สึกท่วมท้นได้ โดยเฉพาะเมื่อคุณต้อง **create search index Java** โครงการที่จัดการกับคอลเลกชันเอกสารขนาดใหญ่ โชคดีที่ **GroupDocs.Search for Java** มี API ที่ครอบคลุมซึ่งช่วยให้คุณสร้างการค้นหาแบบ faceted และ complex ด้วยเพียงไม่กี่บรรทัดของโค้ด ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีตั้งค่าไลบรารี, **create a search index Java**, เพิ่มเอกสาร, และรันการค้นหา faceted แบบง่ายและการค้นหา multi‑criteria ที่ซับซ้อน

## Quick Answers
- **What is a faceted search?** วิธีการกรองผลลัพธ์โดยใช้หมวดหมู่ที่กำหนดไว้ล่วงหน้า (เช่น file type, date).  
- **How do I create a search index Java?** เริ่มต้นอ็อบเจ็กต์ `Index` ที่ชี้ไปยังโฟลเดอร์และเพิ่มเอกสาร.  
- **Can I combine multiple criteria?** ใช่—ใช้การค้นหาแบบ object‑based หรือโอเปอร์เรเตอร์ Boolean ในข้อความค้นหา.  
- **Do I need a license?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; ไลเซนส์เชิงพาณิชย์จะลบข้อจำกัดทั้งหมด.  
- **Which IDE works best?** IDE Java ใดก็ได้ (IntelliJ IDEA, Eclipse, NetBeans) ทำงานได้ดี.

## What is “create search index java”?
การสร้างดัชนีการค้นหาใน Java หมายถึงการสร้างโครงสร้างข้อมูลที่สามารถค้นหาได้ซึ่งเก็บเมตาดาต้าและเนื้อหาเอกสาร ทำให้การดึงข้อมูลตามคำค้นของผู้ใช้ทำได้อย่างรวดเร็ว ด้วย GroupDocs.Search ดัชนีจะอยู่บนดิสก์ สามารถอัปเดตแบบเพิ่มส่วนได้ และรองรับฟีเจอร์ขั้นสูงเช่น faceting และตรรกะ Boolean ที่ซับซ้อน

## Why use GroupDocs.Search for faceted and complex queries?
- **Out‑of‑the‑box faceting** – กรองตามฟิลด์เช่น file name, size, หรือ custom metadata.  
- **Rich query language** – ผสมผสานการค้นหาแบบ text, phrase, และ field queries โดยใช้ AND/OR/NOT operators.  
- **Scalable performance** – ดัชนีหลายล้านเอกสารพร้อมรักษาความหน่วงของการค้นหาให้ต่ำ.  
- **Pure Java** – ไม่มีการพึ่งพา native, ทำงานบนแพลตฟอร์มใดก็ได้ที่รัน JDK 8+.

## Prerequisites

- **JDK 8 หรือใหม่กว่า** ที่ติดตั้งและกำหนดค่าใน IDE ของคุณ.  
- **Maven** (หรือ Gradle) สำหรับการจัดการ dependencies.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- ความคุ้นเคยพื้นฐานกับแนวคิด OOP ของ Java และโครงสร้างโครงการ Maven.

## Setting Up GroupDocs.Search for Java

### Maven Setup
เพิ่ม repository และ dependency ไปยังไฟล์ `pom.xml` ของคุณ:

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

### Direct Download
หรืออีกทางหนึ่ง ดาวน์โหลด JAR ล่าสุดจากหน้า release อย่างเป็นทางการ:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### License Acquisition
เพื่อเปิดใช้งานฟังก์ชันเต็ม:

1. **Free trial** – perfect for development and testing.  
2. **Temporary evaluation license** – extends trial limits.  
3. **Commercial license** – removes all restrictions for production use.

### Basic Initialization and Setup
โค้ดต่อไปนี้แสดงวิธี **create a search index Java** โดยการสร้างอินสแตนซ์ของคลาส `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

เมื่อดัชนีพร้อมแล้ว เราสามารถดำเนินการต่อไปยังการค้นหา faceted และ complex ในโลกจริงได้

## How to create search index java – Simple Faceted Search

การค้นหา faceted ช่วยให้ผู้ใช้ปลายทางสามารถจำกัดผลลัพธ์โดยการเลือกค่าจากหมวดหมู่ที่กำหนดไว้ล่วงหน้า (facets). ด้านล่างเป็นขั้นตอนแบบทีละขั้นตอน

### Step 1: Create an Index
ขั้นตอนที่ 1: สร้างดัชนี  
แรกสุด ให้ชี้ `Index` ไปยังโฟลเดอร์ที่ไฟล์ดัชนีจะถูกจัดเก็บ.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Step 2: Add Documents to the Index
ขั้นตอนที่ 2: เพิ่มเอกสารลงในดัชนี  
บอก GroupDocs.Search ว่าเอกสารต้นฉบับของคุณอยู่ที่ไหน. ทุกประเภทไฟล์ที่รองรับ (PDF, DOCX, TXT, ฯลฯ) จะถูกทำดัชนีโดยอัตโนมัติ.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Step 3: Perform a Search in the Content Field with a Text Query
ขั้นตอนที่ 3: ทำการค้นหาในฟิลด์ Content ด้วยข้อความค้นหา  
ข้อความค้นหาอย่างรวดเร็วจะกรองโดยฟิลด์ `content`. ไวยากรณ์ `content: Pellentesque` จะจำกัดผลลัพธ์ให้กับเอกสารที่มีคำ *Pellentesque* อยู่ในเนื้อความ.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Step 4: Perform a Search Using an Object Query
ขั้นตอนที่ 4: ทำการค้นหาโดยใช้ Object Query  
การค้นหาแบบ object‑based ให้การควบคุมที่ละเอียด. ที่นี่เราสร้าง word query, ห่อไว้ใน field query, แล้วดำเนินการ.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## How to create search index java – Complex Query Search

การค้นหาแบบ complex รวมหลายฟิลด์, โอเปอร์เรเตอร์ Boolean, และการค้นหาวลี. เหมาะสำหรับสถานการณ์เช่นการกรอง e‑commerce หรือการวิจัยเอกสารกฎหมาย

### Step 1: Create an Index for Complex Queries
ขั้นตอนที่ 1: สร้างดัชนีสำหรับการค้นหาแบบ Complex  
ใช้โครงสร้างโฟลเดอร์เดียวกัน; คุณสามารถแชร์ดัชนีระหว่างสถานการณ์แบบง่ายและซับซ้อนได้.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Step 2: Perform a Search with a Text Query
ขั้นตอนที่ 2: ทำการค้นหาด้วยข้อความค้นหา  
คำสั่งต่อไปนี้ค้นหาไฟล์ที่ชื่อ *lorem* **และ** *ipsum* **หรือ** เนื้อหาที่มีหนึ่งในสองวลีที่ตรงกัน.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Step 3: Perform a Search with an Object Query
ขั้นตอนที่ 3: ทำการค้นหาโดยใช้ Object Query  
การสร้างแบบ object‑based สะท้อนคำสั่งข้อความแต่ให้ความปลอดภัยของประเภทและความช่วยเหลือจาก IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Practical Applications of Faceted & Complex Searches

| สถานการณ์ | วิธีที่ Faceting ช่วย | ตัวอย่าง Query |
|----------|-------------------|---------------|
| **E‑commerce catalog** | กรองตามหมวดหมู่, ราคา, ยี่ห้อ | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | จำกัดโดย case number, jurisdiction | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | รวม author, year, keywords | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | ค้นหาตาม filetype และ department | `filetype: pdf AND department: HR` |

ตัวอย่างเหล่านี้แสดงให้เห็นว่าทำไมการเชี่ยวชาญเทคนิค **create search index java** จึงเป็นการเปลี่ยนเกมสำหรับแอปพลิเคชันที่มีข้อมูลจำนวนมาก

## Common Pitfalls & Troubleshooting

- **Empty results** – ตรวจสอบว่าเอกสารถูกเพิ่มสำเร็จ (`index.getDocumentCount()` สามารถช่วยได้).  
- **Stale index** – หลังจากเพิ่มหรือเอาไฟล์ออก, เรียก `index.update()` เพื่อให้ดัชนีสอดคล้อง.  
- **Incorrect field names** – ใช้ค่าสถิต `CommonFieldNames` (`Content`, `FileName`, ฯลฯ) เพื่อหลีกเลี่ยงการพิมพ์ผิด.  
- **Performance bottlenecks** – สำหรับคอลเลกชันขนาดใหญ่, พิจารณาเปิดใช้งาน `index.setCacheSize()` หรือใช้ SSD เฉพาะสำหรับโฟลเดอร์ดัชนี.

## Frequently Asked Questions

**Q: Can I use GroupDocs.Search with Spring Boot?**  
A: แน่นอน. เพียงเพิ่ม dependency ของ Maven, ตั้งค่าดัชนีเป็น Spring bean, แล้ว inject ไปที่ต้องการ.

**Q: Does the library support custom metadata fields?**  
A: ใช่ – คุณสามารถเพิ่มฟิลด์ที่ผู้ใช้กำหนดระหว่างการทำดัชนีและทำ faceting บนฟิลด์เหล่านั้น.

**Q: How large can the index grow?**  
A: ดัชนีเป็นแบบอิงดิสก์และสามารถจัดการกับเอกสารหลายล้านรายการ; เพียงตรวจสอบพื้นที่จัดเก็บเพียงพอและเฝ้าติดตามการตั้งค่า cache.

**Q: Is there a way to rank results by relevance?**  
A: GroupDocs.Search จะให้คะแนนการจับคู่โดยอัตโนมัติ; คุณสามารถดึงคะแนนได้ผ่าน `SearchResult.getDocument(i).getScore()`.

**Q: What happens if I index encrypted PDFs?**  
A: ให้รหัสผ่านเมื่อเพิ่มเอกสาร: `index.add(filePath, password)`.

## Conclusion

ตอนนี้คุณควรจะรู้สึกมั่นใจในการ **create search index Java** ด้วย GroupDocs.Search, การเพิ่มเอกสาร, และการสร้างทั้งการค้นหา faceted แบบง่ายและการค้นหา Boolean ที่ซับซ้อน ความสามารถเหล่านี้ทำให้คุณสามารถมอบประสบการณ์การค้นหาที่เร็ว, แม่นยำ, และเป็นมิตรต่อผู้ใช้ในแอปพลิเคชันหลากหลาย – ตั้งแต่แพลตฟอร์ม e‑commerce ไปจนถึงฐานความรู้ขององค์กร

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? สำรวจฟีเจอร์ขั้นสูงของ **GroupDocs.Search** เช่น **highlighting**, **suggestions**, และ **real‑time indexing** เพื่อเพิ่มพลังการค้นหาในแอปของคุณต่อไป

---

**อัปเดตล่าสุด:** 2025-12-16  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs
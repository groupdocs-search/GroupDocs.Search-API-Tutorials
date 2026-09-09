---
date: '2026-08-26'
description: เรียนรู้ว่า Boolean operators Java ช่วยให้คุณสร้าง fast search index,
  ทำ content search Java, และรัน faceted queries ด้วย GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: เรียนรู้ว่า Boolean operators Java ช่วยให้คุณสร้าง fast search index,
  ทำ content search Java, และดำเนินการ faceted queries ด้วย GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – สร้าง search index และ faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – สร้าง search index & faceted search
type: docs
url: /th/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# ตัวดำเนินการบูลีน Java – สร้างดัชนีการค้นหา & การค้นหาแบบ faceted

การนำ **search experience** ที่ทรงพลังไปใช้ใน Java อาจรู้สึกท่วมท้น โดยเฉพาะเมื่อคุณต้อง **create a search index Java** ที่รองรับ **boolean operators Java** สำหรับการค้นหาแบบ faceted และคำค้นหาซับซ้อน ในบทแนะนำนี้เราจะพาคุณผ่านการตั้งค่า **GroupDocs.Search for Java**, การสร้างดัชนี, การเพิ่มเอกสาร, และการสร้างการค้นหา faceted แบบง่ายและคำค้นหาหลายเงื่อนไขที่ซับซ้อนโดยใช้ตรรกะ Boolean. เมื่อเสร็จสิ้นคุณจะเข้าใจวิธีใช้ **content search Java**, **filename search Java**, และแม้กระทั่งการทำ **update index Java** เพื่อให้ข้อมูลของคุณเป็นปัจจุบัน.

## คำตอบอย่างรวดเร็ว
- **การค้นหาแบบ faceted คืออะไร?** วิธีการกรองผลลัพธ์ตามหมวดหมู่ที่กำหนดไว้ล่วงหน้า เช่น ประเภทไฟล์หรือวันที่.  
- **ฉันจะสร้างดัชนีการค้นหา Java อย่างไร?** เริ่มต้นอ็อบเจ็กต์ `Index` ที่ชี้ไปยังโฟลเดอร์และเพิ่มเอกสาร.  
- **ฉันสามารถรวมหลายเงื่อนไขด้วยตัวดำเนินการบูลีนได้หรือไม่?** ใช่—ใช้การค้นหาแบบ object‑based หรือ Boolean operators ในข้อความค้นหา.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้งานฟรีทำงานสำหรับการพัฒนา; ไลเซนส์เชิงพาณิชย์จะลบข้อจำกัด.  
- **IDE ไหนทำงานได้ดีที่สุด?** IDE Java ใดก็ได้ (IntelliJ IDEA, Eclipse, NetBeans) ทำงานได้ดี.

## “create search index java” คืออะไร

การสร้างดัชนีการค้นหา Java หมายถึงการสร้างโครงสร้างบนดิสก์ที่เก็บข้อความและเมตาดาต้าของเอกสาร ทำให้สามารถดึงคืนเอกสารที่ตรงกันได้ทันทีผ่านคำค้นหา ดัชนีจะแมปคำกับตัวระบุเอกสาร, รองรับการค้นหาอย่างรวดเร็ว, และสามารถอัปเดตแบบเพิ่มส่วนได้เมื่อไฟล์เปลี่ยนแปลง, ให้พื้นฐานสำหรับคุณลักษณะการค้นหาที่ทรงพลัง.

## ทำไมต้องใช้ GroupDocs.Search สำหรับการค้นหาแบบ faceted และซับซ้อน

GroupDocs.Search for Java มีฟีเจอร์ faceting ในตัว, รองรับการค้นหาแบบ Boolean, และการทำดัชนีที่มีประสิทธิภาพสูงที่สามารถจัดการได้ถึง 10 ล้านเอกสารโดยคงความหน่วงของการค้นหาให้อยู่ต่ำกว่า 200 ms บนฮาร์ดแวร์เซิร์ฟเวอร์ทั่วไป มันมีตัวกรองฟิลด์พร้อมใช้, ภาษาคำค้นที่หลากหลาย, และความเข้ากันได้แบบ pure‑Java, ทำให้เหมาะสำหรับสถานการณ์การค้นหาระดับองค์กร.

## ข้อกำหนดเบื้องต้น

- **JDK 8 หรือใหม่กว่า** ติดตั้งและกำหนดค่าใน IDE ของคุณ.  
- **Maven** (หรือ Gradle) สำหรับการจัดการ dependencies.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- ความคุ้นเคยพื้นฐานกับแนวคิด OOP ของ Java และโครงสร้างโครงการ Maven.

## การตั้งค่า GroupDocs.Search for Java

### การตั้งค่า Maven
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

### ดาวน์โหลดโดยตรง
หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจากหน้า release อย่างเป็นทางการ:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### การรับไลเซนส์
เพื่อเปิดใช้งานฟังก์ชันทั้งหมด:

1. **Free trial** – เหมาะสำหรับการพัฒนาและการทดสอบ.  
2. **Temporary evaluation license** – ขยายขีดจำกัดของการทดลอง.  
3. **Commercial license** – ลบข้อจำกัดทั้งหมดสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

### การเริ่มต้นและตั้งค่าเบื้องต้น
คลาส `Index` เป็นส่วนประกอบหลักที่แสดงถึงดัชนีที่สามารถค้นหาได้ซึ่งเก็บบนดิสก์ ตัวอย่างต่อไปนี้แสดงวิธี **create a search index Java** โดยการสร้างอินสแตนซ์ของคลาส `Index`:

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

เมื่อดัชนีพร้อมแล้ว เราสามารถดำเนินต่อไปสู่การค้นหา faceted และซับซ้อนในโลกจริง.

## วิธีใช้ boolean operators java – การค้นหา faceted แบบง่าย

โหลดดัชนีของคุณ, เพิ่มเอกสาร, และส่งคำสั่ง field query; รูปแบบสองขั้นตอนนี้ทำให้คุณสามารถดึงจำนวน facet และผลลัพธ์ที่กรองได้ในหนึ่งการเรียกใช้งาน วิธีนี้ให้ผู้ใช้วิธีที่เข้าใจง่ายในการจำกัดผลลัพธ์ตามหมวดหมู่เช่น ประเภทไฟล์, ผู้เขียน, หรือเมตาดาต้ากำหนดเอง.

### ขั้นตอนที่ 1: สร้างดัชนี
แรกสุด, ชี้ `Index` ไปยังโฟลเดอร์ที่ไฟล์ดัชนีจะถูกเก็บ.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### ขั้นตอนที่ 2: เพิ่มเอกสารลงในดัชนี
บอก GroupDocs.Search ว่าเอกสารต้นทางของคุณอยู่ที่ไหน ประเภทไฟล์ที่รองรับทั้งหมด (PDF, DOCX, TXT, ฯลฯ) จะถูกทำดัชนีโดยอัตโนมัติ.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### ขั้นตอนที่ 3: ทำการค้นหาในฟิลด์ content ด้วยข้อความ query
ข้อความ query อย่างรวดเร็วจะกรองโดยฟิลด์ `content`. ไวยากรณ์ `content: Pellentesque` จะจำกัดผลลัพธ์ให้เป็นเอกสารที่มีคำ *Pellentesque* ในเนื้อความของมัน.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### ขั้นตอนที่ 4: ทำการค้นหาโดยใช้ object query
การค้นหาแบบ object‑based ให้การควบคุมที่ละเอียดมากขึ้น ที่นี่เราสร้าง word query, ห่อมันใน field query, และดำเนินการ.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## วิธีใช้ boolean operators java – การค้นหาแบบซับซ้อน

เพื่อดำเนินการค้นหาแบบซับซ้อน, ให้รวมหลายเงื่อนไขฟิลด์ด้วยตัวดำเนินการ AND/OR/NOT, และอาจรวมการค้นหาประโยคด้วย คุณสามารถระบุแต่ละเงื่อนไขโดยใช้ field query, ซ้อนกันด้วย Boolean operators, และควบคุมความสำคัญด้วยการ boost, ทำให้คุณดึงเอกสารที่เกี่ยวข้องที่สุดที่ตรงตามเกณฑ์ทั้งหมด.

### ขั้นตอนที่ 1: สร้างดัชนีสำหรับการค้นหาแบบซับซ้อน
ใช้โครงสร้างโฟลเดอร์เดียวกันซ้ำ; คุณสามารถแชร์ดัชนีระหว่างสถานการณ์แบบง่ายและซับซ้อนได้.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### ขั้นตอนที่ 2: ทำการค้นหาด้วยข้อความ query
คำค้นต่อไปนี้มองหาไฟล์ที่ชื่อ *lorem* **และ** *ipsum* **หรือ** เนื้อหาที่มีหนึ่งในสองวลีที่ตรงกัน.

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

### ขั้นตอนที่ 3: ทำการค้นหาโดยใช้ object query
การสร้างแบบ object‑based สะท้อนคำค้นข้อความแต่ให้ความปลอดภัยของประเภทและความช่วยเหลือจาก IDE.

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

## การประยุกต์ใช้การค้นหา faceted & complex

| สถานการณ์ | วิธีที่ faceting ช่วย | ตัวอย่าง query |
|----------|-------------------|---------------|
| **แคตาล็อกอี‑คอมเมิร์ซ** | กรองตามหมวดหมู่, ราคา, แบรนด์ | `category: Electronics AND price:[100 TO 500]` |
| **คลังเอกสารกฎหมาย** | จำกัดตามหมายเลขคดี, เขตอำนาจ | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **คลังข้อมูลการวิจัย** | รวมผู้เขียน, ปีการตีพิมพ์, คำสำคัญ | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **อินทราเน็ตองค์กร** | ค้นหาตามประเภทไฟล์และแผนก | `filetype: pdf AND department: HR` |

ตัวอย่างเหล่านี้แสดงให้เห็นว่าการเชี่ยวชาญ **boolean operators java** และเทคนิค **filename search java** เป็นกุญแจสำคัญสำหรับแอปพลิเคชันที่ต้องจัดการข้อมูลจำนวนมาก.

## ข้อผิดพลาดทั่วไป & การแก้ปัญหา

อ็อบเจ็กต์ `SearchResult` มีเอกสารที่ตรงกับ query และให้การเข้าถึงคะแนนความเกี่ยวข้องและส่วนที่ไฮไลท์ของพวกมัน.  
คลาส `CommonFieldNames` กำหนดชื่อฟิลด์มาตรฐานเช่น `Content` และ `FileName` ที่ใช้ทั่ว API.

- **Empty results** – ตรวจสอบว่าเอกสารถูกเพิ่มสำเร็จ (`index.getDocumentCount()` สามารถช่วยได้).  
- **Stale index** – หลังจากเพิ่มหรือเอาไฟล์ออก, เรียก `index.update()` เพื่อ **update index java** และทำให้ดัชนีสอดคล้องกัน.  
- **Incorrect field names** – ใช้คอนสแตนท์ `CommonFieldNames` (`Content`, `FileName`, ฯลฯ) เพื่อหลีกเลี่ยงการพิมพ์ผิด.  
- **Performance bottlenecks** – สำหรับคอลเลกชันขนาดใหญ่, พิจารณาเปิดใช้งาน `index.setCacheSize()` หรือใช้ SSD แยกสำหรับโฟลเดอร์ดัชนี.  
- **Missing highlights** – เพื่อ **highlight search results java**, ดึงส่วนที่ตรงกันผ่าน `SearchResult.getFragments()` (ไม่ได้แสดงที่นี่แต่มีใน API).  

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้ GroupDocs.Search กับ Spring Boot ได้หรือไม่?**  
A: แน่นอน. เพิ่ม dependency ของ Maven, ตั้งค่าดัชนีเป็น Spring bean, และฉีดเข้าไปที่ที่คุณต้องการความสามารถการค้นหา.

**Q: ไลบรารีนี้รองรับฟิลด์เมตาดาต้ากำหนดเองหรือไม่?**  
A: ใช่ – คุณสามารถเพิ่มฟิลด์ที่ผู้ใช้กำหนดระหว่างการทำดัชนีและจากนั้นทำ faceting บนฟิลด์เหล่านั้น.

**Q: ดัชนีสามารถเติบโตได้ใหญ่แค่ไหน?**  
A: ดัชนีแบบดิสก์สามารถจัดการได้ถึง 10 ล้านเอกสาร; เพียงให้แน่ใจว่ามีพื้นที่จัดเก็บเพียงพอและตรวจสอบการตั้งค่า cache.

**Q: มีวิธีจัดอันดับผลลัพธ์ตามความเกี่ยวข้องหรือไม่?**  
A: GroupDocs.Search จะให้คะแนนการจับคู่โดยอัตโนมัติ; คุณสามารถดึงคะแนนผ่าน `SearchResult.getDocument(i).getScore()`.

**Q: จะเกิดอะไรขึ้นหากฉันทำดัชนี PDF ที่เข้ารหัส?**  
A: ให้รหัสผ่านเมื่อเพิ่มเอกสาร: `index.add(filePath, password)`.

## สรุป

ตอนนี้คุณควรจะรู้สึกมั่นใจในการ **creating a search index Java** ด้วย GroupDocs.Search, การเพิ่มเอกสาร, และการสร้างทั้ง query faceted แบบง่ายและการค้นหา Boolean ที่ซับซ้อนโดยใช้ **boolean operators java**. ความสามารถเหล่านี้ทำให้คุณสามารถมอบประสบการณ์การค้นหาที่เร็ว, แม่นยำ, และเป็นมิตรต่อผู้ใช้ในหลากหลายแอปพลิเคชัน — ตั้งแต่แพลตฟอร์ม e‑commerce ไปจนถึงฐานความรู้ขององค์กร.

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? สำรวจฟีเจอร์ขั้นสูงของ **GroupDocs.Search** เช่น **highlighting**, **suggestions**, และ **real‑time indexing** เพื่อเพิ่มพลังการค้นหาของแอปพลิเคชันของคุณต่อไป.

---

**อัปเดตล่าสุด:** 2026-08-26  
**ทดสอบกับ:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [Wildcard Search Java กับ GroupDocs.Search – ฟีเจอร์ขั้นสูง](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [วิธีอัปเดต Index Java ด้วย GroupDocs.Search – คู่มือครบวงจร](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [วิธีทำ java full text search: สร้างไดเรกทอรีดัชนีด้วย GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
---
date: '2026-08-10'
description: เรียนรู้วิธีทำดัชนีเอกสารและเพิ่มเอกสารลงในดัชนีโดยใช้ GroupDocs.Search
  for Java. สร้างแอปค้นหาที่มีประสิทธิภาพด้วยการค้นหาข้อความและออบเจกต์.
keywords:
- how to index documents
- create search index
- index pdf files
- search word documents
- update search index
lastmod: '2026-08-10'
og_description: เรียนรู้วิธีทำดัชนีเอกสารด้วย GroupDocs.Search for Java. คู่มือขั้นตอนต่อขั้นตอนในการสร้างดัชนีการค้นหา,
  เพิ่มไฟล์ PDF, Word, Excel, และรันคิวรีที่เร็ว.
og_image_alt: Code example showing Java indexing with GroupDocs.Search
og_title: วิธีทำดัชนีเอกสารด้วย GroupDocs.Search for Java – คู่มือการค้นหาเร็ว
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  headline: How to index documents with GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to index documents and add documents to index using GroupDocs.Search
    for Java. Build powerful search apps with text and object queries.
  name: How to index documents with GroupDocs.Search for Java
  steps:
  - name: '**Free trial** – explore the library without cost.'
    text: '**Free trial** – explore the library without cost.'
  - name: '**Temporary license** – request a short‑term key for extended evaluation.'
    text: '**Temporary license** – request a short‑term key for extended evaluation.'
  - name: '**Purchase** – obtain a full license for production use.'
    text: '**Purchase** – obtain a full license for production use.'
  - name: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
    text: '**Legal document management** – locate clauses, case numbers, or dates
      across thousands of contracts in seconds.'
  - name: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
    text: '**Financial reporting** – pull transactions that fall within a specific
      monetary range without scanning each spreadsheet.'
  - name: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
    text: '**Inventory tracking** – find items by serial numbers, batch codes, or
      SKU ranges across a distributed file system.'
  type: HowTo
- questions:
  - answer: Call `index.add("NEW_DOCUMENT_PATH")` again; the library merges the new
      entries without recreating the whole index.
    question: How do I update an existing index with new documents?
  - answer: Yes, it supports 30+ formats—including PDF, DOCX, XLSX, PPTX, TXT, and
      HTML—so you can index virtually any business document.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Java 8+ runtime, at least 2 GB RAM for modest collections (larger sets
      benefit from 4 GB+), and read/write access to the index folder.
    question: What are the system requirements for using GroupDocs.Search?
  - answer: Keep the index up‑to‑date, profile your queries, and review JVM memory
      settings. Reducing the number of indexed fields or using object queries can
      also speed up execution.
    question: How can I troubleshoot search performance issues?
  - answer: Yes, you can enable synonym dictionaries and fuzzy search via the `SearchOptions`
      class to broaden matching without sacrificing relevance. The `SearchOptions`
      class configures advanced search behavior such as synonyms and fuzzy matching.
    question: Is there support for synonyms or fuzzy matching?
  type: FAQPage
tags:
- document indexing
- GroupDocs.Search
- Java search library
- search API
- indexing tutorial
title: วิธีทำดัชนีเอกสารด้วย GroupDocs.Search for Java
type: docs
url: /th/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# วิธีทำดัชนีเอกสารด้วย GroupDocs.Search สำหรับ Java

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **วิธีทำดัชนีเอกสาร** อย่างมีประสิทธิภาพเป็นทักษะสำคัญสำหรับนักพัฒนา Java ที่ต้องจัดการกับคอลเลกชันไฟล์ขนาดใหญ่ ไม่ว่าคุณจะกำลังประมวลผลสัญญากฎหมาย, งบการเงิน, หรือรายงานภายใน, ดัชนีการค้นหาที่สร้างอย่างดีจะทำให้คุณค้นหาข้อมูลที่ต้องการได้ในไม่กี่วินาทีแทนที่จะใช้เวลาหลายชั่วโมงในการสแกนด้วยตนเอง บทแนะนำนี้จะพาคุณผ่านการสร้างดัชนีการค้นหา, การเพิ่มเอกสาร, และการรันคิวรีทั้งแบบข้อความและแบบอ็อบเจ็กต์ด้วย GroupDocs.Search สำหรับ Java

## คำตอบด่วน
- **ขั้นตอนแรกในการทำดัชนีเอกสารคืออะไร?** สร้างอินสแตนซ์ `Index` ที่ชี้ไปยังโฟลเดอร์ที่ไฟล์ดัชนีจะถูกจัดเก็บ.  
- **เมธอดใดที่ใช้เพิ่มเอกสารลงในดัชนี?** เรียก `index.add("PATH_TO_DOCUMENTS")` เพื่อสแกนไดเรกทอรีและนำไฟล์ที่รองรับเข้า.  
- **ฉันสามารถค้นหาช่วงตัวเลขได้หรือไม่?** ใช่ – ใช้ข้อความค้นหาเช่น `"400 ~~ 4000"` หรืออ็อบเจ็กต์คิวรีผ่าน `SearchQuery.createNumericRangeQuery`. เมธอด `createNumericRangeQuery` สร้างอ็อบเจ็กต์คิวรีช่วงตัวเลข.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; ไลเซนส์เชิงพาณิชย์จะเปิดใช้งานคุณสมบัติทั้งหมดและลบข้อจำกัดการใช้งาน.  
- **ต้องการเวอร์ชัน Java ใด?** รองรับ JDK 8 หรือสูงกว่า.

## วิธีทำดัชนีเอกสารด้วย GroupDocs.Search คืออะไร?
การทำดัชนีเอกสารสร้างที่เก็บโทเค็นที่สามารถค้นหาได้สำหรับแต่ละไฟล์, ทำให้เอนจินสามารถดึงผลลัพธ์โดยไม่ต้องอ่านไฟล์ต้นฉบับทุกครั้ง ขั้นตอนการเตรียมข้อมูลนี้แปลงเนื้อหาดิบเป็นดัชนีที่ปรับให้เหมาะสมซึ่งสามารถคิวรีได้ในระดับมิลลิวินาที ดัชนีจะเก็บคำ, ตำแหน่ง, และเมตาดาต้า, ทำให้การค้นหาวลีและความใกล้เคียงทำได้อย่างรวดเร็วในทุกประเภทเอกสารที่รองรับ

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
การดำเนินการค้นหามักเสร็จสิ้นภายในน้อยกว่า 50 ms บนคอลเลกชัน 10 000 ไฟล์ (โดยเฉลี่ย 1 KB ต่อไฟล์) ที่ทำงานบน VM มาตรฐาน 2‑CPU, 8 GB. ไลบรารีรองรับ **30+ รูปแบบการนำเข้าและส่งออก** — รวมถึง PDF, DOCX, XLSX, PPTX, TXT, และ HTML — ทำให้คุณสามารถทำดัชนีเอกสารธุรกิจใด ๆ ได้โดยไม่ต้องใช้ตัวแปลงเพิ่มเติม API ที่ยืดหยุ่นช่วยให้คุณผสานคิวรีข้อความธรรมดา, ช่วงตัวเลข, และคิวรีอ็อบเจ็กต์ซับซ้อนได้, ในขณะที่การอัปเดตแบบเพิ่มส่วนช่วยให้คุณเพิ่มไฟล์ใหม่โดยไม่ต้องสร้างดัชนีใหม่ทั้งหมด

## ข้อกำหนดเบื้องต้น
- Maven ที่ติดตั้งแล้วสำหรับการจัดการ dependencies.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse.  
- ความรู้พื้นฐาน Java (แนวคิด OOP, การจัดการข้อยกเว้น).  

## การตั้งค่า GroupDocs.Search สำหรับ Java
### การตั้งค่า Maven
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

### ดาวน์โหลดโดยตรง
คุณยังสามารถดาวน์โหลด JAR ล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### ขั้นตอนการรับไลเซนส์
1. **ทดลองใช้ฟรี** – สำรวจไลบรารีโดยไม่มีค่าใช้จ่าย.  
2. **ไลเซนส์ชั่วคราว** – ขอคีย์ระยะสั้นสำหรับการประเมินต่อเนื่อง.  
3. **ซื้อ** – รับไลเซนส์เต็มสำหรับการใช้งานในผลิตภัณฑ์.  

## การเริ่มต้นและตั้งค่าพื้นฐาน
เพื่อ **เพิ่มเอกสารลงในดัชนี**, คุณต้องสร้างอ็อบเจ็กต์ `Index` ที่ชี้ไปยังโฟลเดอร์ที่ไฟล์ดัชนีจะถูกจัดเก็บ:

`Index` is the core class that represents a searchable index on disk.  
```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

บรรทัดนี้สร้าง (หรือเปิด) ดัชนีพร้อมรับเอกสาร

## คู่มือการใช้งาน
### การสร้างและทำดัชนีเอกสาร
#### วิธีเพิ่มเอกสารลงในดัชนี
เมธอด `add` สแกนโฟลเดอร์และเก็บข้อมูลที่สามารถค้นหาได้สำหรับแต่ละไฟล์ มันจะประมวลผลทุกเอกสารที่รองรับแบบเรียกซ้ำ, ดึงข้อความและเมตาดาต้า, และเขียนโทเค็นลงในโฟลเดอร์ดัชนีที่คุณระบุไว้ก่อนหน้า.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **พารามิเตอร์:** สตริงพาธชี้ไปยังโฟลเดอร์ที่มีไฟล์ที่คุณต้องการทำดัชนี.  
- **วัตถุประสงค์:** หลังจากขั้นตอนนี้ ดัชนีจะมีโทเค็นจากทุกประเภทเอกสารที่รองรับ ทำให้การค้นหาเร็วขึ้นทั่วทั้งคอลเลกชัน.

## การค้นหาด้วยข้อความ
#### วิธีทำการค้นหาช่วงตัวเลขโดยใช้ข้อความ
คุณสามารถค้นหาโดยใช้สตริงง่าย ๆ ที่กำหนดช่วง เอนจินจะตีความตัวดำเนินการ `~~` เป็น “ระหว่าง” และคืนเอกสารทั้งหมดที่มีตัวเลขอยู่ในขอบเขตที่กำหนด.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **พารามิเตอร์:** สตริงคิวรี `"400 ~~ 4000"` บอกเอนจินให้ค้นหาตัวเลขระหว่าง 400 ถึง 4000.  
- **ค่าที่คืน:** `SearchResult` เก็บรายการเอกสารที่ตรงกันและไฮไลท์ส่วนที่ตรงกัน.

## การค้นหาแบบอ็อบเจ็กต์
#### วิธีใช้คิวรีอ็อบเจ็กต์สำหรับช่วงตัวเลข
คิวรีแบบอ็อบเจ็กต์ให้คุณควบคุมเกณฑ์การค้นหาแบบโปรแกรมเมติก, สามารถผสานเงื่อนไขหลายอย่างหรือสร้างคิวรีแบบไดนามิกในขณะรันไทม์.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **พารามิเตอร์:** `createNumericRangeQuery` รับจำนวนเต็มเริ่มต้นและสิ้นสุด.  
- **วัตถุประสงค์:** เมธอดนี้เหมาะเมื่อคุณต้องการกรองผลลัพธ์ตามฟิลด์ตัวเลข เช่น ยอดใบแจ้งหนี้ อายุ หรือรหัสสินค้า.

## การประยุกต์ใช้งานจริง
ต่อไปนี้เป็นสถานการณ์จริงที่ **วิธีทำดัชนีเอกสาร** กลายเป็นตัวเปลี่ยนเกม:

1. **การจัดการเอกสารทางกฎหมาย** – ค้นหาข้อ, หมายเลขคดี หรือวันที่ในหลายพันสัญญาในเวลาไม่กี่วินาที.  
2. **การรายงานทางการเงิน** – ดึงธุรกรรมที่อยู่ในช่วงจำนวนเงินเฉพาะโดยไม่ต้องสแกนสเปรดชีตแต่ละไฟล์.  
3. **การติดตามสินค้าคงคลัง** – ค้นหารายการโดยหมายเลขซีเรียล, รหัสแบตช์ หรือช่วง SKU ในระบบไฟล์กระจาย.  

การผสาน GroupDocs.Search กับฐานข้อมูล, ที่เก็บบนคลาวด์, หรือคิวข้อความสามารถทำให้เวิร์กโฟลว์เอกสารอัตโนมัติมากยิ่งขึ้น.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **การอัปเดตดัชนีเป็นประจำ:** เรียก `index.add` ใหม่สำหรับไฟล์ใหม่เพื่อให้ดัชนีเป็นปัจจุบัน.  
- **การจัดการทรัพยากร:** ตรวจสอบการใช้ heap; ดัชนีขนาดใหญ่ได้ประโยชน์จากการตั้งค่า JVM garbage‑collection ที่ปรับแต่ง.  
- **การปรับแต่งคิวรี:** ใช้คิวรีอ็อบเจ็กต์สำหรับฟิลเตอร์ซับซ้อนเพื่อลดการสแกนที่ไม่จำเป็นและปรับปรุงเวลาในการตอบสนอง.

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| **การค้นหาไม่พบผลลัพธ์** | ดัชนียังไม่ได้สร้างหรือพาธโฟลเดอร์ไม่ถูกต้อง | ตรวจสอบว่าได้เรียก `index.add` ในไดเรกทอรีที่ถูกต้องและโฟลเดอร์ดัชนีสามารถเขียนได้. |
| **OutOfMemoryError ระหว่างทำดัชนี** | ไฟล์ขนาดใหญ่มากหรือ heap ไม่เพียงพอ | เพิ่มค่า JVM `-Xmx` หรือทำดัชนีไฟล์เป็นชุดเล็กลง. |
| **รูปแบบไฟล์ที่ไม่รองรับ** | ประเภทไฟล์ไม่ถูกจดจำโดย GroupDocs.Search | ตรวจสอบให้ส่วนขยายอยู่ในรายการที่รองรับ (PDF, DOCX, XLSX, PPTX, TXT, HTML ฯลฯ). |

## คำถามที่พบบ่อย
**Q: วิธีอัปเดตดัชนีที่มีอยู่ด้วยเอกสารใหม่?**  
A: เรียก `index.add("NEW_DOCUMENT_PATH")` อีกครั้ง; ไลบรารีจะผสานรายการใหม่โดยไม่ต้องสร้างดัชนีใหม่ทั้งหมด.

**Q: GroupDocs.Search รองรับรูปแบบไฟล์ต่าง ๆ หรือไม่?**  
A: ใช่, รองรับกว่า 30 รูปแบบ — รวมถึง PDF, DOCX, XLSX, PPTX, TXT, และ HTML — ทำให้คุณสามารถทำดัชนีเอกสารธุรกิจใด ๆ ได้โดยแทบไม่มีข้อจำกัด.

**Q: ความต้องการระบบสำหรับการใช้ GroupDocs.Search คืออะไร?**  
A: จำเป็นต้องมี Java 8+ runtime, RAM อย่างน้อย 2 GB สำหรับคอลเลกชันขนาดเล็ก (คอลเลกชันใหญ่ควรมี 4 GB ขึ้นไป), และการเข้าถึงอ่าน/เขียนโฟลเดอร์ดัชนี.

**Q: จะวิเคราะห์ปัญหาประสิทธิภาพการค้นหาอย่างไร?**  
A: รักษาดัชนีให้เป็นปัจจุบัน, ทำโปรไฟล์คิวรีของคุณ, และตรวจสอบการตั้งค่า memory ของ JVM. การลดจำนวนฟิลด์ที่ทำดัชนีหรือใช้คิวรีอ็อบเจ็กต์ก็ช่วยเร่งการทำงานได้.

**Q: มีการสนับสนุนคำพ้องหรือการค้นหาแบบ fuzzy หรือไม่?**  
A: มี, คุณสามารถเปิดใช้งานพจนานุกรมคำพ้องและการค้นหาแบบ fuzzy ผ่านคลาส `SearchOptions` เพื่อขยายการจับคู่โดยไม่ลดความเกี่ยวข้อง. คลาส `SearchOptions` กำหนดพฤติกรรมการค้นหาขั้นสูง เช่น คำพ้องและการค้นหาแบบ fuzzy.

**อัปเดตล่าสุด:** 2026-08-10  
**ทดสอบกับ:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเพิ่มเอกสารลงในดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [วิธีเพิ่มเอกสารลงในดัชนีและจัดการ Alias ใน GroupDocs.Search สำหรับ Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
- [วิธีอัปเดตดัชนี Java ด้วย GroupDocs.Search – คู่มือฉบับสมบูรณ์](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
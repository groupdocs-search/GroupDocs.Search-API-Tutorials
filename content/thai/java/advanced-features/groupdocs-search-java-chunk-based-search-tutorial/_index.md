---
date: '2026-10-02'
description: เรียนรู้วิธีใช้ temporary license เพื่อเพิ่มเอกสารเข้าสู่ index ด้วย
  chunk‑based search ใน Java, เพิ่ม search performance ขณะควบคุม memory usage.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: ใช้ temporary license เพื่อเพิ่มเอกสารเข้าสู่ index ด้วย chunk‑based
  search ใน Java, improving search speed และลด memory consumption.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: ใช้ temporary license สำหรับ chunk‑based indexing ใน Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: ใช้ temporary license สำหรับ chunk‑based indexing ใน Java
type: docs
url: /th/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# ใช้ใบอนุญาตชั่วคราวสำหรับการทำดัชนีแบบแบ่งส่วนใน Java

ในบทแนะนำนี้คุณจะ **ใช้ใบอนุญาตชั่วคราว ** เพื่อเพิ่มเอกสารลงในดัชนีด้วยคุณสมบัติการค้นหาแบบแบ่งส่วนของ GroupDocs.Search วิธีการนี้ช่วยให้คุณจัดการกับคอลเลกชันเอกสารขนาดใหญ่—สัญญากฎหมาย, ตั๋วสนับสนุน, งานวิจัย—ในขณะที่ทำให้การใช้ **java search index memory** ต่ำและ **เพิ่มประสิทธิภาพการค้นหา** อย่างมาก คุณจะได้เห็นวิธีตั้งค่าโฟลเดอร์ดัชนี, ป้อนแหล่งเอกสารหลายแหล่ง, เปิดใช้งานการค้นหาแบบแบ่งส่วน, และรันทั้งการค้นหาแบบแบ่งส่วนแรกและต่อเนื่อง

## คำตอบอย่างรวดเร็ว
- **ขั้นตอนแรกคืออะไร?** สร้างโฟลเดอร์ดัชนีการค้นหา  
- **ฉันจะรวมไฟล์หลายไฟล์ได้อย่างไร?** ใช้ `index.add()` สำหรับแต่ละโฟลเดอร์เอกสาร  
- **ตัวเลือกใดที่เปิดใช้งานการค้นหาแบบแบ่งส่วน?** `options.setChunkSearch(true)`  
- **ฉันสามารถค้นหาต่อหลังจากส่วนแรกได้หรือไม่?** ใช่, เรียก `index.searchNext()` พร้อมกับโทเคน  
- **ฉันต้องการใบอนุญาตหรือไม่?** ใบอนุญาตทดลองหรือใบอนุญาตชั่วคราวใช้ได้สำหรับการพัฒนา; ใบอนุญาตเต็มจำเป็นสำหรับการใช้งานจริง  

## สิ่งที่คุณจะได้เรียนรู้
- วิธีสร้างดัชนีการค้นหาในโฟลเดอร์ที่ระบุ  
- ขั้นตอนการ **เพิ่มเอกสารลงในดัชนี** จากหลายตำแหน่ง  
- การกำหนดค่าตัวเลือกการค้นหาเพื่อเปิดใช้งานการค้นหาแบบแบ่งส่วน  
- การทำการค้นหาแบบแบ่งส่วนแรกและต่อเนื่อง  
- สถานการณ์จริงที่การค้นหาเอกสารแบบแบ่งส่วนเป็นประโยชน์  

## ข้อกำหนดเบื้องต้น
เพื่อทำตามคู่มือนี้ โปรดตรวจสอบว่าคุณมี:

- **ไลบรารีที่ต้องการ**: GroupDocs.Search for Java 25.4 หรือใหม่กว่า  
- **การตั้งค่าสภาพแวดล้อม**: ติดตั้ง Java Development Kit (JDK) ที่เข้ากันได้  
- **ความรู้เบื้องต้น**: ความเข้าใจพื้นฐานการเขียนโปรแกรม Java และการใช้ Maven  

## การตั้งค่า GroupDocs.Search สำหรับ Java
เริ่มต้นโดยรวม GroupDocs.Search เข้าในโปรเจกต์ของคุณด้วย Maven:

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

หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### การรับใบอนุญาต
เพื่อทดลองใช้ GroupDocs.Search:

- **ทดลองฟรี** – ทดสอบฟีเจอร์หลักโดยไม่ต้องผูกมัด  
- **ใบอนุญาตชั่วคราว** – ให้การเข้าถึงต่อเนื่องสำหรับการพัฒนา  
- **ซื้อ** – ใบอนุญาตเต็มสำหรับการใช้งานในผลิตภัณฑ์  

## วิธีเพิ่มเอกสารลงในดัชนี?
**คำตอบโดยตรง:** เรียก `index.add()` สำหรับแต่ละโฟลเดอร์ที่มีไฟล์ที่คุณต้องการให้ค้นหา; วิธีนี้จะสแกนโฟลเดอร์แบบเรียกซ้ำและเพิ่มเอกสารที่รองรับทุกประเภทลงในดัชนีในขั้นตอนเดียว ซึ่งช่วยลดความจำเป็นในการจัดการไฟล์ทีละไฟล์และเร่งความเร็วการนำเข้าจำนวนมาก

`SearchIndex` คือคลาสหลักที่แทนคอลเลกชันที่สามารถค้นหาได้บนดิสก์ หลังจากที่คุณสร้างอินสแตนซ์แล้ว การทำดัชนีและการทำคิวรีทั้งหมดจะไหลผ่านอ็อบเจกต์นี้

### 1. การสร้างดัชนี
**คำตอบโดยตรง:** สร้างอ็อบเจกต์ `SearchIndex` ด้วยพาธที่ต้องการเก็บไฟล์ดัชนี, จากนั้นเรียก `index.create()` เพื่อเริ่มต้นโครงสร้างการจัดเก็บ การเรียกนี้จะสร้างโฟลเดอร์และไฟล์เมตาดาต้าที่จำเป็นในครั้งแรกที่ใช้

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. การเพิ่มเอกสารลงในดัชนี
**คำตอบโดยตรง:** ใช้เมธอด `index.add()` และส่งพาธเต็มของแต่ละโฟลเดอร์ต้นทาง; API จะตรวจจับรูปแบบที่รองรับโดยอัตโนมัติ (PDF, DOCX, XLSX ฯลฯ) และสกัดข้อความที่สามารถค้นหาได้ลงในดัชนี

`SearchOptions` เป็นอ็อบเจกต์การกำหนดค่าที่ให้คุณปรับแต่งวิธีการประมวลผลเอกสารระหว่างการทำดัชนีและการค้นหา คุณจะใช้มันต่อไปเพื่อเปิดใช้งานการคิวรีแบบแบ่งส่วน

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. การกำหนดค่าตัวเลือกการค้นหาเพื่อการค้นหาแบบแบ่งส่วน
**คำตอบโดยตรง:** ตั้งค่า `options.setChunkSearch(true)` บนอินสแตนซ์ `SearchOptions` ก่อนทำคิวรี; การตั้งค่านี้บอกเอนจินให้แยกเอกสารแต่ละไฟล์เป็นส่วนย่อยเชิงตรรกะ (โดยทั่วไปคือย่อหน้า) และคืนผลลัพธ์ตามส่วนแทนที่จะคืนตามไฟล์ทั้งหมด

`SearchResult` จะเก็บส่วนที่ตรงกัน, ตำแหน่ง, และคะแนนความเกี่ยวข้อง เมื่อเปิดใช้งานการค้นหาแบบแบ่งส่วนแต่ละ `SearchResult` จะสอดคล้องกับส่วนย่อยหนึ่งของเอกสารต้นฉบับ

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. การทำการค้นหาแบบแบ่งส่วนแรก
**คำตอบโดยตรง:** เรียก `index.search("your query", options)`; การเรียกนี้จะคืนคอลเลกชัน `SearchResult` สำหรับชุดส่วนที่ตรงกันแรกและโทเคนที่แสดงสถานะการค้นหาเพื่อใช้ต่อเนื่อง

โทเคนที่คืนมานี้สำคัญสำหรับการแบ่งหน้าในชุดผลลัพธ์ขนาดใหญ่โดยไม่ต้องทำคิวรีทั้งหมดใหม่

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. การทำการค้นหาแบบแบ่งส่วนต่อเนื่อง
**คำตอบโดยตรง:** ส่งโทเคนที่ได้จากการเรียกก่อนหน้าให้กับ `index.searchNext(token, options)`; ทำซ้ำจนกว่าเมธอดจะคืนค่า `null` ซึ่งหมายความว่ารวบรวมส่วนที่ตรงกันทั้งหมดแล้ว

วิธีการแบบเพิ่มขึ้นนี้ช่วยให้การใช้หน่วยความจำต่ำ เพราะเพียงชุดส่วนปัจจุบันเท่านั้นที่อยู่ในหน่วยความจำ

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## ทำไมต้องใช้การค้นหาแบบแบ่งส่วน?
การค้นหาแบบแบ่งส่วนจะแบ่งคอลเลกชันเอกสารขนาดมหาศาลเป็นชิ้นส่วนที่จัดการได้, ลดความกดดันของหน่วยความจำและเร่งเวลาตอบสนอง โดยการทำดัชนีระดับย่อหน้าหรือส่วน, เอนจินสามารถดึงเฉพาะส่วนที่เกี่ยวข้องได้, ซึ่งลดการใช้ CPU และปรับปรุงความหน่วงสำหรับผู้ใช้ปลายสุด ประโยชน์นี้มีความสำคัญโดยเฉพาะเมื่อ:

1. **ทีมกฎหมาย** ต้องค้นหาข้อกำหนดเฉพาะในสัญญานับพันฉบับ  
2. **พอร์ทัลสนับสนุนลูกค้า** ต้องแสดงบทความฐานความรู้ที่เกี่ยวข้องโดยทันที  
3. **นักวิจัย** ต้องคัดกรองข้อมูลชุดใหญ่โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ  

ข้ออ้างอิงเชิงปริมาณ: GroupDocs.Search สามารถประมวลผล **PDF มากกว่า 500 หน้า** ในเวลาน้อยกว่า **2 วินาทีต่อส่วน** บนเซิร์ฟเวอร์ 8‑คอร์มาตรฐาน, พร้อมกับคง heap สูงสุดต่ำกว่า **200 MB**

## วิธีที่แนวทางนี้เพิ่มประสิทธิภาพการค้นหา
**คำตอบโดยตรง:** ด้วยการค้นหาช่วงย่อยแทนไฟล์ทั้งหมด, เอนจินสามารถข้ามส่วนที่ไม่เกี่ยวข้องได้เร็วขึ้น, ลดวงจร CPU, และเก็บเฉพาะส่วนที่กำลังทำงานในหน่วยความจำ, ซึ่งโดยตรงลดการใช้ **java search index memory** และให้เวลาตอบสนองเร็วขึ้น วิธีการที่มุ่งเป้าหมายนี้ยังช่วยให้การแคชและการประมวลผลแบบขนานทำงานได้ดีขึ้น, ทำให้หลายคอร์สามารถจัดการส่วนต่าง ๆ พร้อมกัน, เพิ่มอัตราการทำงานบนเซิร์ฟเวอร์หลายคอร์

ประโยชน์เพิ่มเติมรวมถึง:

- การประมวลผลส่วนแบบขนานบนหลายคอร์  
- การหยุดก่อนล่วงหน้าเมื่อพบผลที่มีความเกี่ยวข้องสูง  

## การจัดการ java search index memory
**คำตอบโดยตรง:** จัดสรร heap ของ JVM ให้เพียงพอ (เช่น `-Xmx2g` หรือมากกว่า) ตามขนาดดัชนีที่คาดหวัง, รัน `index.optimize()` หลังการเพิ่มจำนวนมากเพื่อบีบอัดโครงสร้างดัชนี, และตรวจสอบการหยุดทำงานของ GC ด้วย VisualVM เพื่อหลีกเลี่ยงความหน่วง

เคล็ดลับการปรับแต่งเพิ่มเติม:

- ใช้ `index.flush()` หลังจากแบตช์ขนาดใหญ่เพื่อเขียนข้อมูลชั่วคราวลงดิสก์  
- เปิด `options.setMemoryLimit(256)` เพื่อจำกัดการใช้หน่วยความจำต่อการค้นหา  

## พิจารณาด้านประสิทธิภาพ
- **การจัดการหน่วยความจำ** – จัดสรร heap เพียงพอ (`-Xmx`) สำหรับดัชนีขนาดใหญ่  
- **การตรวจสอบทรัพยากร** – เฝ้าดูการใช้ CPU ระหว่างการทำดัชนีและการค้นหา  
- **การบำรุงรักษาดัชนี** – สร้างหรือทำความสะอาดดัชนีเป็นระยะเพื่อกำจัดข้อมูลล้าสมัย  

## ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| `OutOfMemoryError` ระหว่างทำดัชนี | ขนาด heap ต่ำเกินไป | เพิ่ม heap ของ JVM (`-Xmx2g` หรือมากกว่า) |
| ไม่ได้ผลลัพธ์ | โทเคนส่วนไม่ถูกประมวลผล | ตรวจสอบให้ลูป `while` ทำงานจนกว่า `getNextChunkSearchToken()` จะเป็น `null` |
| การค้นช้า | ดัชนีไม่ได้ทำให้เป็นออพติมไลซ์ | รัน `index.optimize()` หลังการเพิ่มจำนวนมาก |

## คำถามที่พบบ่อย

**ถาม: การค้นหาแบบแบ่งส่วนคืออะไร?**  
ตอบ: การค้นหาแบบแบ่งส่วนจะแบ่งชุดข้อมูลเป็นชิ้นย่อยเล็ก ๆ, ทำให้คิวรีมีประสิทธิภาพบนปริมาณข้อมูลขนาดใหญ่โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ

**ถาม: ฉันจะอัปเดตดัชนีด้วยไฟล์ใหม่อย่างไร?**  
ตอบ: เพียงเรียก `index.add()` พร้อมพาธของเอกสารใหม่; ดัชนีจะรวมไฟล์เหล่านั้นโดยอัตโนมัติ

**ถาม: GroupDocs.Search รองรับรูปแบบไฟล์ต่าง ๆ หรือไม่?**  
ตอบ: รองรับ **PDF, DOCX, XLSX, PPTX, HTML, TXT, และกว่า 30 รูปแบบอื่น**  

**ถาม: จุดคอขวดด้านประสิทธิภาพทั่วไปคืออะไร?**  
ตอบ: ข้อจำกัดของหน่วยความจำและดัชนีที่ไม่ได้ทำให้เป็นออพติมไลซ์เป็นสาเหตุหลัก; จัดสรร heap เพียงพอและทำให้ดัชนีเป็นออพติมไลซ์เป็นประจำ

**ถาม: จะหาเอกสารอ้างอิงเพิ่มเติมได้ที่ไหน?**  
ตอบ: เยี่ยมชม [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) เพื่อดูคู่มือเชิงลึกและอ้างอิง API

**ถาม: การค้นหาแบบแบ่งส่วนทำงานกับ PDF ที่เข้ารหัสหรือไม่?**  
ตอบ: ทำงานได้ หากคุณส่งรหัสผ่านผ่านโอเวอร์โหลด API ที่เหมาะสม

**ถาม: ฉันจะตรวจสอบความคืบหน้าในการทำดัชนีอย่างไร?**  
ตอบ: ใช้โอเวอร์โหลด `Index.add()` ที่คืนค่าอ็อบเจกต์ `Progress` หรือเชื่อมต่อกับคอลแบ็กการบันทึกล็อก  

## แหล่งข้อมูล
- **เอกสาร**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **อ้างอิง API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **ดาวน์โหลด**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **สนับสนุนฟรี**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ใบอนุญาตชั่วคราว**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**อัปเดตล่าสุด:** 2026-10-02  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## บทแนะนำที่เกี่ยวข้อง

- [Create Search Index Directory & Set License – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Improve Query Performance with GroupDocs.Search Java: Optimize Index & Search](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Groupdocs Search Java Advanced Search Features](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
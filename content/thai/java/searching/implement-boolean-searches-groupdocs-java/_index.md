---
date: '2026-07-21'
description: Create Boolean Query Java tutorial แสดงวิธีการทำการค้นหาแบบ boolean AND,
  OR, NOT ด้วย GroupDocs.Search for Java, เพิ่มเอกสารลงใน index, และเพิ่มประสิทธิภาพการดึงคืนเอกสาร.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Create Boolean Query Java tutorial อธิบายขั้นตอนโดยละเอียดว่าอย่างไรในการสร้าง
  query แบบ AND, OR, NOT ด้วย GroupDocs.Search for Java, เพิ่มเอกสารลงใน index, และปรับปรุงประสิทธิภาพการดึงคืนข้อมูล.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – เชี่ยวชาญการค้นหาแบบ Boolean ด้วย GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'สร้าง Boolean Query Java: เชี่ยวชาญการค้นหาแบบ Boolean ด้วย GroupDocs.Search
  for Java'
type: docs
url: /th/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# สร้างการค้นหาแบบบูลีนใน Java: เชี่ยวชาญการค้นหาแบบบูลีนด้วย GroupDocs.Search สำหรับ Java

การค้นหาคอลเลกชันเอกสารขนาดมหาศาลอาจรู้สึกเหมือนการตามหาเข็มในกองฟาง **Create Boolean Query Java** ให้คุณบอกเครื่องมืออย่างชัดเจนว่าต้องการอะไร — เอกสารที่มี *ทั้ง* คำสองคำ, *หรือ* คำใดคำหนึ่ง, หรือ *ยกเว้น* คำที่ไม่ต้องการ ในคู่มือนี้เราจะพาคุณผ่านการตั้งค่า **GroupDocs.Search for Java**, การเพิ่มเอกสารลงในดัชนี, และการสร้างคำค้นแบบบูลีนที่ทรงพลังเพื่อเพิ่มประสิทธิภาพการทำงาน **document retrieval java** ของคุณ เมื่อเสร็จสิ้นคุณจะสามารถเขียนโค้ดที่สะอาดและดูแลได้ง่ายเพื่อสร้างคำค้นแบบบูลีนใน Java เพียงไม่กี่บรรทัด

## คำตอบอย่างรวดเร็ว
- **อะไรคือการค้นหาแบบ AND แบบบูลีน?** คืนเฉพาะเอกสารที่มีคำ *ทั้งหมด* ที่ระบุ  
- **OR แตกต่างจาก AND อย่างไร?** OR จับคู่เอกสารที่มีคำ *ใดคำหนึ่ง* ขยายผลลัพธ์  
- **ควรใช้ NOT เมื่อใด?** ใช้ NOT เพื่อตัดเอกสารที่มีคำที่ไม่ต้องการออก  
- **ต้องการใบอนุญาตหรือไม่?** ทดลองใช้ฟรีสำหรับการทดสอบ; ต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานจริง  
- **ต้องใช้ Java เวอร์ชันใด?** รองรับ Java 8+; แนะนำ JDK 11+

## **create boolean query java** คืออะไร?
`create boolean query java` หมายถึงการสร้างคำค้นใน Java ที่รวมตัวดำเนินการตรรกะเช่น AND, OR, และ NOT โดยใช้ GroupDocs.Search API การประกอบตัวดำเนินการเหล่านี้ทำให้คุณควบคุมได้อย่างแม่นยำว่าเอกสารใดจะตรงกับเงื่อนไข, เปิดใช้งานการกรองขั้นสูง, การปรับความเกี่ยวข้อง, และสถานการณ์การค้นหาที่ซับซ้อน

## ทำไมต้องใช้ GroupDocs.Search for Java?
- **ประสิทธิภาพสูง** กับชุดเอกสารขนาดใหญ่ – สามารถทำดัชนีและค้นหา 500 GB ของข้อความได้ภายในน้อยกว่าหนึ่งนาทีบนเซิร์ฟเวอร์มาตรฐาน  
- **API ครบครัน** รองรับการค้นหาแบบข้อความและแบบอ็อบเจ็กต์, ให้คุณเลือกสไตล์ที่เหมาะกับสถาปัตยกรรมของคุณ  
- **รองรับหลายภาษา** ในการทำ stemming, stop‑words, และ fuzzy matching ครอบคลุมกว่า 30 ภาษา  
- **การรวมระบบง่าย** ด้วย Maven หรือการดาวน์โหลด JAR โดยตรง, เพียงไม่กี่บรรทัดของโค้ดก็พร้อมใช้งาน

## ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำงาน, ตรวจสอบว่าคุณมี:

- **GroupDocs.Search for Java** (เวอร์ชัน 25.4 หรือใหม่กว่า) – ดูลิงก์ดาวน์โหลดด้านล่าง  
- JDK 8+ ที่ติดตั้งและกำหนดค่าใน IDE ของคุณ (IntelliJ IDEA, Eclipse, ฯลฯ)  
- ความรู้พื้นฐานของ Java และ Maven สำหรับการจัดการ dependencies  

## การตั้งค่า GroupDocs.Search for Java

### การตั้งค่า Maven
เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [เวอร์ชัน GroupDocs.Search สำหรับ Java](https://releases.groupdocs.com/search/java/)

### การรับใบอนุญาต
เริ่มต้นด้วยใบอนุญาตทดลองฟรีเพื่อสำรวจคุณสมบัติทั้งหมด สำหรับการใช้งานในสภาพแวดล้อมจริง, ซื้อใบอนุญาตเชิงพาณิชย์เพื่อเปิดใช้งานฟังก์ชันเต็มรูปแบบ

### การเริ่มต้นและตั้งค่าพื้นฐาน
สร้างโฟลเดอร์ดัชนีและสร้างอ็อบเจ็กต์ `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## คุณสร้าง boolean query java อย่างไร?
คลาส `Index` แทนชุดเอกสารที่สามารถค้นหาได้บนดิสก์ `BooleanQuery` รวมหลาย sub‑query ด้วยตัวดำเนินการตรรกะ `createAndQuery`, `createOrQuery`, และ `createNotQuery` สร้าง sub‑query ของ AND, OR, และ NOT ตามลำดับ โหลดหรือสร้างอินสแตนซ์ `Index`, เพิ่มเอกสาร, แล้วสร้างอ็อบเจ็กต์ `BooleanQuery` ด้วยเมธอดที่กล่าวมา เรียก `index.search(query)` เพื่อดึงเอกสารที่ตรงกัน รูปแบบนี้ทำงานได้ทั้งกรณีง่ายและซับซ้อนโดยต้องทำเพียงสามขั้นตอนหลัก: การเริ่มต้นดัชนี, การเพิ่มเอกสาร, และการดำเนินการค้นหา

## การค้นหาแบบ AND แบบบูลีน

### ภาพรวม
การค้นหาแบบ AND ช่วยจำกัดผลลัพธ์, เพิ่มความเกี่ยวข้องเมื่อคุณต้องการเอกสารที่ตรงกับหลายเงื่อนไขพร้อมกัน

### ขั้นตอนการดำเนินการ

1. **Initialize Index** – นี้ยังแสดงวิธี **add documents to index** สำหรับสถานการณ์ AND  

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**  

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – ใช้ไวยากรณ์สตริงธรรมดา  

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – มีประโยชน์เมื่อสร้างคำค้นแบบโปรแกรม (**search with and java**)  

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## การค้นหาแบบ OR แบบบูลีน

### ภาพรวม
การค้นหาแบบ OR เหมาะสำหรับการสำรวจที่ต้องการจับเอกสารที่มีอย่างน้อยหนึ่งคำสำคัญจากหลายคำ (**search with or java**)

### ขั้นตอนการดำเนินการ

1. **Initialize Index**  

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**  

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**  

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**  

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## การค้นหาแบบ NOT แบบบูลีน

### ภาพรวม
การค้นหาแบบ NOT ช่วยกำจัดเอกสารที่ไม่เกี่ยวข้อง, เช่นการกรองชื่อแบรนด์ของคู่แข่ง (**boolean search examples java**)

### ขั้นตอนการดำเนินการ

1. **Initialize Index**  

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**  

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**  

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**  

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## คำค้นแบบบูลีนที่ซับซ้อน

### ภาพรวม
คำค้นที่ซับซ้อนช่วยจำลองสถานการณ์การค้นหาในโลกจริง, เช่น “ค้นหาบทความกีฬาเชิงบวกแต่ยกเว้นการกล่าวถึงนักกีฬาบางคน”

### ขั้นตอนการดำเนินการ

1. **Initialize Index**  

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**  

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**  

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**  

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## การประยุกต์ใช้จริงของ Queries **java boolean and or**
- **Document Management Systems** – ค้นหาสัญญาที่มีทั้ง “confidential” **AND** “renewal”  
- **Legal Research** – กรองกฎหมายกรณีด้วย **AND**/**OR** พร้อมยกเว้นกฎหมายที่ล้าสมัยด้วย **NOT**  
- **Customer Support** – ดึงตั๋วที่มี “login” **AND** “error” แต่ไม่รวม “resolved”  
- **Content Curation** – รวบรวมบล็อกโพสต์เกี่ยวกับ “cloud” **OR** “serverless” สำหรับจดหมายข่าว

## ข้อผิดพลาดทั่วไป & การแก้ไขปัญหา

- **Missing Index Refresh** – หลังจากเพิ่มเอกสารใหม่, เรียก `index.update()` เพื่อให้สามารถค้นหาได้  
- **Incorrect Operator Spacing** – GroupDocs.Search ต้องการช่องว่างรอบตัวดำเนินการ (`AND`, `OR`, `NOT`)  
- **Case Sensitivity** – คำค้นไม่แยกตัวพิมพ์ใหญ่‑เล็กโดยค่าเริ่มต้น, แต่ Analyzer ที่กำหนดเองอาจมีผล  
- **Large Result Sets** – ใช้การแบ่งหน้า (`search(query, 0, 100)`) เพื่อหลีกเลี่ยงการใช้หน่วยความจำเกิน

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถรวมมากกว่าสองคำในคำค้น AND ได้หรือไม่?**  
ตอบ: แน่นอน คุณสามารถเชื่อมต่อหลาย `createWordQuery` ด้วย `createAndQuery`, หรือเขียน `"term1 AND term2 AND term3"` ในคำค้นข้อความได้เลย

**ถาม: GroupDocs.Search รองรับการค้นหาแบบ wildcard หรือ fuzzy หรือไม่?**  
ตอบ: ใช่. ใส่ `*` สำหรับ wildcard (เช่น `promot*`) หรือใช้ `~` สำหรับ fuzzy matching (เช่น `comfort~`)

**ถาม: ฉันจะจำกัดการค้นหาให้เฉพาะประเภทไฟล์ใดไฟล์หนึ่งได้อย่างไร?**  
`FileTypeQuery` จำกัดผลลัพธ์ให้กับรูปแบบไฟล์เฉพาะเช่น PDF หรือ DOCX.  
ตอบ: ใช้คลาส `FileTypeQuery` เพื่อจำกัดผลลัพธ์เป็น PDF, DOCX ฯลฯ และผสานกับคำค้นแบบบูลีนของคุณ

**ถาม: วิธีที่ดีที่สุดในการตรวจสอบประสิทธิภาพการทำดัชนีคืออะไร?**  
ตอบ: เปิดใช้งาน logger ในตัว (`index.getLogger().setLevel(Level.INFO)`) และตรวจสอบเมตริกเวลาแต่ละครั้งหลังการ `add`

**ถาม: มีวิธีเพิ่มน้ำหนักให้กับคำบางคำเพื่อบูสต์ความเกี่ยวข้องหรือไม่?**  
`BoostQuery` เพิ่มคะแนนความเกี่ยวข้องของคำที่ระบุในคำค้น.  
ตอบ: ใช่. ห่อคำสำคัญด้วย `BoostQuery` เพื่อเพิ่มน้ำหนักในอัลกอริทึมการให้คะแนน

---

**Last Updated:** 2026-07-21  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs

## บทเรียนที่เกี่ยวข้อง

- [Boolean Operators Java – Create Search Index & Faceted Search](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java&#58; Efficient Document Search and Index Management](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Mastering GroupDocs.Search Java – Create and Manage a Search Index](/search/java/indexing/groupdocs-search-java-create-index-guide/)
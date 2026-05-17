---
date: '2026-01-29'
description: เรียนรู้วิธีการใช้งานการค้นหาแบบบูลีน AND/OR ใน Java ด้วย GroupDocs.Search
  for Java, เพิ่มเอกสารลงในดัชนีและปรับปรุงการดึงข้อมูลเอกสาร
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: เชี่ยวชาญการค้นหาแบบบูลีนด้วย GroupDocs.Search สำหรับ
  Java'
type: docs
url: /th/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: ควบคุมการค้นหา Boolean อย่างเชี่ยวชาญด้วย GroupDocs.Search สำหรับ Java

การค้นหาคอลเลกชันเอกสารขนาดมหาศาลอาจรู้สึกเหมือนการหาสิ่งที่เล็กที่สุดในกองฟาง ด้วยการสอบถาม **java boolean and or** คุณสามารถบอกเครื่องมือได้อย่างชัดเจนว่าต้องการอะไร — เอกสารที่มี *ทั้ง* คำ, *หรือ* คำใดคำหนึ่ง, หรือ *ยกเว้น* คำที่ไม่ต้องการ ในคู่มือนี้เราจะอธิบายการตั้งค่า **GroupDocs.Search Java**, การเพิ่มเอกสารลงในดัชนี, และการสร้างการสอบถาม Boolean ที่ทรงพลังเพื่อเพิ่มประสิทธิภาพการทำงาน **document retrieval java** ของคุณ

## Quick Answers
- **What is a boolean AND query?** คืนค่าเฉพาะเอกสารที่มี *all* คำที่ระบุ  
- **How does OR differ from AND?** OR จับคู่เอกสารที่มี *any* ของคำ, ทำให้ชุดผลลัพธ์กว้างขึ้น  
- **When should I use NOT?** ใช้ NOT เพื่อกรองเอกสารที่มีคำที่ไม่ต้องการออก  
- **Do I need a license?** การทดลองใช้ฟรีเพียงพอสำหรับการทดสอบ; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **Which Java version is required?** รองรับ Java 8+; แนะนำให้ใช้ JDK 11+

## **java boolean and or** คืออะไร?
การสอบถาม **java boolean and or** ผสานตัวดำเนินการตรรกะ (AND, OR, NOT) เพื่อปรับผลการค้นหา โดยการจัดโครงสร้างการสอบถาม คุณบอก GroupDocs.Search ว่าคำต่าง ๆ มีความสัมพันธ์อย่างไร ทำให้คุณควบคุมกระบวนการดึงข้อมูลได้อย่างแม่นยำ

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
- **High performance** บนชุดเอกสารขนาดใหญ่  
- **Rich API** ที่รองรับการสอบถามทั้งแบบข้อความและแบบอ็อบเจ็กต์  
- **Built‑in language support** สำหรับการสเตมม, คำหยุด, และการจับคู่แบบ fuzzy  
- **Easy integration** กับ Maven หรือการดาวน์โหลด JAR โดยตรง  

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search for Java** (v25.4 หรือใหม่กว่า) – ดูลิงก์ดาวน์โหลดด้านล่าง  
- JDK 8+ ที่ติดตั้งและกำหนดค่าใน IDE ของคุณ (IntelliJ IDEA, Eclipse, เป็นต้น)  
- ความรู้พื้นฐานของ Java และ Maven สำหรับการจัดการ dependencies  

## Setting Up GroupDocs.Search for Java

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
หรือดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับลิขสิทธิ์
เริ่มต้นด้วยลิขสิทธิ์ทดลองใช้งานฟรีเพื่อสำรวจคุณสมบัติทั้งหมด. สำหรับการใช้งานจริง, ซื้อใบอนุญาตเชิงพาณิชย์เพื่อเปิดใช้งานฟังก์ชันเต็มรูปแบบ.

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

## java boolean and or: การใช้งานการค้นหา Boolean

ต่อไปนี้เราจะครอบคลุมการสอบถาม **AND**, **OR**, **NOT**, และการสอบถาม **complex**. แต่ละส่วนจะแสดงทั้งการสอบถามแบบข้อความธรรมดาและการสอบถามแบบอ็อบเจ็กต์ที่เทียบเท่า, เพื่อให้คุณเลือกสไตล์ที่เหมาะกับโค้ดของคุณ.

### การค้นหา Boolean AND
รวมคำด้วย **AND** เพื่อดึงเฉพาะเอกสารที่มี *all* คำสำคัญ.

#### ภาพรวม
การสอบถามแบบ AND จะทำให้ผลลัพธ์แคบลง, เพิ่มความเกี่ยวข้องเมื่อคุณต้องการเอกสารที่ตรงกับหลายเกณฑ์.

#### ขั้นตอนการดำเนินการ

1. **Initialize Index** – นี้ยังแสดงตัวอย่าง **add documents to index** สำหรับสถานการณ์ AND.  

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**  

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – ใช้ไวยากรณ์สตริงธรรมดา.  

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – มีประโยชน์เมื่อสร้างการสอบถามแบบโปรแกรม (**search with and java**).  

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### การค้นหา Boolean OR
ใช้ **OR** เพื่อขยายผลลัพธ์, จับคู่กับคำใดคำหนึ่งที่ระบุ.

#### ภาพรวม
การสอบถามแบบ OR เหมาะสำหรับการค้นหาเชิงสำรวจที่คุณต้องการจับเอกสารที่มีอย่างน้อยหนึ่งคำสำคัญจากหลายคำ (**search with or java**).

#### ขั้นตอนการดำเนินการ

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

### การค้นหา Boolean NOT
ยกเว้นคำที่ไม่ต้องการด้วย **NOT** เพื่อกรองสัญญาณรบกวนออกจากผลลัพธ์ของคุณ.

#### ภาพรวม
การสอบถามแบบ NOT ช่วยคุณกำจัดเอกสารที่ไม่เกี่ยวข้อง, เช่นการกรองชื่อแบรนด์ของคู่แข่ง (**boolean search examples java**).

#### ขั้นตอนการดำเนินการ

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

### การสอบถาม Boolean ขั้นซับซ้อน
ผสาน **AND**, **OR**, และ **NOT** เพื่อสร้างตรรกะการค้นหาที่ซับซ้อนสำหรับความต้องการการดึงข้อมูลที่เฉพาะเจาะจงสูง.

#### ภาพรวม
การสอบถามขั้นซับซ้อนทำให้คุณจำลองสถานการณ์การค้นหาในโลกจริง, เช่น “ค้นหาบทความกีฬาแบบบวกแต่ยกเว้นการกล่าวถึงนักกีฬาที่ระบุเฉพาะ”.

#### ขั้นตอนการดำเนินการ

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

## การประยุกต์ใช้จริงของการสอบถาม java boolean and or
- **Document Management Systems** – ค้นหาสัญญาที่มีทั้ง “confidential” **AND** “renewal”.  
- **Legal Research** – กรองกฎหมายกรณีด้วย **AND**/**OR** พร้อมยกเว้นกฎหมายที่ล้าสมัยโดยใช้ **NOT**.  
- **Customer Support** – ดึงตั๋วที่กล่าวถึง “login” **AND** “error” แต่ไม่รวม “resolved”.  
- **Content Curation** – รวบรวมบล็อกโพสต์เกี่ยวกับ “cloud” **OR** “serverless” สำหรับจดหมายข่าว.

## ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา
- **Missing Index Refresh** – หลังจากเพิ่มเอกสารใหม่, เรียก `index.update()` เพื่อให้แน่ใจว่าสามารถค้นหาได้.  
- **Incorrect Operator Spacing** – GroupDocs.Search ต้องการช่องว่างรอบตัวดำเนินการ (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – การสอบถามไม่แยกแยะตัวพิมพ์ใหญ่‑เล็กโดยค่าเริ่มต้น, แต่ตัววิเคราะห์แบบกำหนดเองอาจมีผล.  
- **Large Result Sets** – ใช้การแบ่งหน้า (`search(query, 0, 100)`) เพื่อหลีกเลี่ยงการใช้หน่วยความจำเกิน.

## คำถามที่พบบ่อย

**Q: Can I combine more than two terms in an AND query?**  
A: แน่นอน. คุณสามารถต่อเชื่อมหลาย `createWordQuery` กับ `createAndQuery` หรือเขียนแบบง่าย `"term1 AND term2 AND term3"` ในการสอบถามข้อความได้.

**Q: Does GroupDocs.Search support wildcard or fuzzy searches?**  
A: ใช่. เพิ่ม `*` สำหรับไวลด์การ์ด (เช่น `promot*`) หรือใช้ `~` สำหรับการจับคู่แบบ fuzzy (เช่น `comfort~`).

**Q: How do I limit the search to specific file types?**  
A: ใช้คลาส `FileTypeQuery` เพื่อจำกัดผลลัพธ์ให้เป็น PDF, DOCX ฯลฯ และผสานกับการสอบถาม Boolean ของคุณ.

**Q: What is the best way to monitor indexing performance?**  
A: เปิดใช้งาน logger ในตัว (`index.getLogger().setLevel(Level.INFO)`) และตรวจสอบเมตริกเวลา หลังจากแต่ละการดำเนินการ `add`.

**Q: Is there a way to boost the relevance of certain terms?**  
A: ใช่. หุ้มคำสำคัญด้วย `BoostQuery` เพื่อเพิ่มน้ำหนักของพวกมันในอัลกอริทึมการให้คะแนน.

**อัปเดตล่าสุด:** 2026-01-29  
**ทดสอบด้วย:** GroupDocs.Search 25.4 (Java)  
**ผู้เขียน:** GroupDocs
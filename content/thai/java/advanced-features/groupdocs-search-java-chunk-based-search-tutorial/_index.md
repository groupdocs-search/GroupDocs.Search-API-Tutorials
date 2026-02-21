---
date: '2026-02-21'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและเพิ่มประสิทธิภาพการค้นหาด้วยการค้นหาแบบแบ่งส่วนใน
  Java โดยใช้ GroupDocs.Search ปรับแต่งหน่วยความจำของดัชนีการค้นหา Java สำหรับชุดเอกสารขนาดใหญ่.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: เพิ่มเอกสารลงในดัชนีด้วยการค้นหาแบบแบ่งส่วนใน Java
type: docs
url: /th/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# เพิ่มเอกสารลงในดัชนีด้วยการค้นหาแบบ chunk‑based ใน Java

ในแอปพลิเคชันสมัยใหม่ที่ต้องการ **add documents to index** อย่างรวดเร็วและจากนั้นทำการค้นหาแบบ chunk‑based อย่างเร็ว คุณจะต้องการโซลูชันที่สามารถขยายได้โดยไม่ทำให้หน่วยความจำพุ่งสูงขึ้น บทแนะนำนี้จะพาคุณผ่านการตั้งค่า GroupDocs.Search สำหรับ Java, การเพิ่มโฟลเดอร์เอกสารหลายโฟลเดอร์, และการกำหนดค่าเอนจินเพื่อ **increase search performance** พร้อมควบคุมการใช้ **java search index memory** ไม่ให้เกินขอบเขต ไม่ว่าคุณจะทำการจัดทำดัชนีสัญญากฎหมาย, ตั๋วสนับสนุน, หรือเอกสารวิจัย ขั้นตอนด้านล่างจะให้การนำไปใช้ในระดับผลิตจริง

## Quick Answers
- **What is the first step?** Create a search index folder.  
- **How do I include many files?** Use `index.add()` for each document folder.  
- **Which option enables chunk search?** `options.setChunkSearch(true)`.  
- **Can I continue searching after the first chunk?** Yes, call `index.searchNext()` with the token.  
- **Do I need a license?** A free trial or temporary license works for development; a full license is required for production.  

## What You’ll Learn
- วิธีสร้างดัชนีการค้นหาในโฟลเดอร์ที่ระบุ  
- ขั้นตอนการ **add documents to index** จากหลายตำแหน่ง  
- การกำหนดค่า search options เพื่อเปิดใช้งานการค้นหาแบบ chunk‑based  
- การทำการค้นหาแบบ chunk‑based ครั้งแรกและต่อเนื่อง  
- สถานการณ์จริงที่การค้นหาเอกสารแบบ chunk‑based มีประโยชน์มาก  

## Prerequisites
เพื่อทำตามคู่มือนี้ โปรดตรวจสอบว่าคุณมี:

- **Required Libraries**: GroupDocs.Search for Java 25.4 หรือใหม่กว่า  
- **Environment Setup**: ติดตั้ง Java Development Kit (JDK) ที่เข้ากันได้  
- **Knowledge Prerequisites**: ความรู้พื้นฐานการเขียนโปรแกรม Java และความคุ้นเคยกับ Maven  

## Setting Up GroupDocs.Search for Java
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

### License Acquisition
เพื่อทดลองใช้ GroupDocs.Search:

- **Free Trial** – ทดสอบฟีเจอร์หลักโดยไม่มีข้อผูกมัด  
- **Temporary License** – เข้าถึงแบบขยายสำหรับการพัฒนา  
- **Purchase** – ไลเซนส์เต็มสำหรับการใช้งานในผลิตภัณฑ์  

### Basic Initialization and Setup
สร้างดัชนีในโฟลเดอร์ที่คุณต้องการให้ข้อมูลที่สามารถค้นหาได้อยู่:

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

## How to add documents to index
เมื่อดัชนีมีอยู่แล้ว ขั้นตอนต่อไปที่สมเหตุสมผลคือการ **add documents to index** จากตำแหน่งที่ไฟล์ของคุณถูกจัดเก็บ

### 1. Creating an Index
**Overview**: ตั้งค่าไดเรกทอรีสำหรับดัชนีการค้นหา

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adding Documents to Index
**Overview**: ดึงไฟล์จากหลายโฟลเดอร์ต้นทาง

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

### 3. Configuring Search Options for Chunk Search
เปิดใช้งานการค้นหาแบบ chunk‑based โดยปรับแต่งอ็อบเจ็กต์ options

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Performing Initial Chunk‑Based Search
เรียกใช้คำค้นแรกโดยใช้ตัวเลือกที่เปิดใช้งาน chunk

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuing Chunk‑Based Search
วนซ้ำผ่านชังก์ที่เหลือจนกว่าการค้นหาจะเสร็จสมบูรณ์

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Why use chunk‑based search?
การค้นหาแบบ chunk‑based แบ่งคอลเลกชันเอกสารขนาดใหญ่เป็นส่วนย่อยที่จัดการได้ ลดความกดดันของหน่วยความจำและเร่งความเร็วในการตอบสนอง โดยเฉพาะอย่างยิ่งเมื่อ:

1. **Legal teams** ต้องค้นหาข้อกำหนดเฉพาะในสัญญานับพันฉบับ  
2. **Customer support portals** ต้องแสดงบทความฐานความรู้ที่เกี่ยวข้องโดยทันที  
3. **Researchers** คัดกรองชุดข้อมูลขนาดใหญ่โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ  

## How this approach **increases search performance**
โดยการค้นหาในชังก์ขนาดเล็กแทนไฟล์ทั้งหมด เอนจินสามารถ:

- ข้ามส่วนที่ไม่เกี่ยวข้องได้เร็วขึ้น ลดการใช้ CPU  
- เก็บเฉพาะชังก์ที่กำลังทำงานในหน่วยความจำ ซึ่งช่วยลดการใช้ **java search index memory** โดยตรง  
- ประมวลผลชังก์แบบขนานบนเครื่องหลายคอร์เพื่อให้ได้ผลลัพธ์เร็วขึ้น  

## Managing **java search index memory**
แม้ว่าการค้นหาแบบ chunk‑based จะลดขนาดหน่วยความจำแล้ว คุณยังสามารถปรับจูน JVM เพิ่มเติมได้:

- จัดสรร heap เพียงพอ (`-Xmx2g` หรือสูงกว่า) ตามขนาดดัชนี  
- ใช้ `index.optimize()` หลังจากการเพิ่มจำนวนมากเพื่อบีบอัดโครงสร้างดัชนี  
- ตรวจสอบการหยุดทำงานของ GC ด้วยเครื่องมือเช่น VisualVM เพื่อหลีกเลี่ยงการกระตุกของระบบ  

## Performance Considerations
- **Memory Management** – จัดสรร heap เพียงพอ (`-Xmx`) สำหรับดัชนีขนาดใหญ่  
- **Resource Monitoring** – ติดตามการใช้ CPU ระหว่างการทำดัชนีและการค้นหา  
- **Index Maintenance** – สร้างหรือทำความสะอาดดัชนีเป็นระยะเพื่อกำจัดข้อมูลที่ล้าสมัย  

## Common Pitfalls & Troubleshooting
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Frequently Asked Questions

**Q: What is chunk‑based searching?**  
A: Chunk‑based searching divides the dataset into smaller pieces, allowing efficient queries over large volumes of data without loading entire documents into memory.

**Q: How do I update my index with new files?**  
A: Simply call `index.add()` with the path to the new documents; the index will incorporate them automatically.

**Q: Can GroupDocs.Search handle different file formats?**  
A: Yes, it supports PDFs, DOCX, XLSX, PPTX, and many other common formats.

**Q: What are typical performance bottlenecks?**  
A: Memory constraints and unoptimized indexes are the most common; allocate sufficient heap and regularly optimize the index.

**Q: Where can I find more detailed documentation?**  
A: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) for in‑depth guides and API references.

**Q: Does chunk‑based search work with encrypted PDFs?**  
A: Yes, as long as you provide the password via the appropriate API overload.

**Q: How can I monitor indexing progress?**  
A: Use the `Index.add()` overload that returns a `Progress` object or hook into logging callbacks.

## Resources
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---
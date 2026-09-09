---
date: '2026-08-05'
description: เรียนรู้วิธีสร้างตัวสกัดไฟล์บันทึกสำหรับการค้นหาแบบเต็มข้อความใน Java
  ด้วย GroupDocs.Search. เพิ่มเอกสารเข้าสู่ดัชนี, ปรับประสิทธิภาพการค้นหา, และจัดการไฟล์บันทึกขนาดใหญ่อย่างมีประสิทธิภาพ.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: บทแนะนำ Full text search java แสดงวิธีสร้างตัวสกัดไฟล์บันทึกแบบกำหนดเองโดยใช้
  GroupDocs.Search, เพิ่มเอกสารเข้าสู่ดัชนี, และปรับประสิทธิภาพการค้นหาเพื่อจัดการกับคลังไฟล์บันทึกขนาดมหาศาล.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java: ตัวสกัดไฟล์บันทึกด้วย GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java: ตัวสกัดไฟล์บันทึกด้วย GroupDocs'
type: docs
url: /th/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# การค้นหาแบบเต็มข้อความใน Java: ตัวสกัดไฟล์บันทึกด้วย GroupDocs

การค้นหาแบบเต็มข้อความใน Java เป็นหัวใจสำคัญของระบบใด ๆ ที่ต้องค้นหาข้อมูลอย่างรวดเร็วภายในคอลเลกชันเอกสารขนาดมหาศาล ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีการกำหนดค่า GroupDocs.Search, สร้างตัวสกัดไฟล์บันทึกแบบกำหนดเอง, เพิ่มเอกสารลงในดัชนี, และเพิ่มประสิทธิภาพการค้นหาเมื่อจัดการกับข้อมูลบันทึกหลายกิกะไบต์

## สิ่งที่คุณจะได้เรียนรู้
- ตั้งค่าและกำหนดค่า GroupDocs.Search สำหรับ Java.  
- สร้าง **log file extractor** ที่แยกวิเคราะห์ไฟล์บันทึกข้อความธรรมดาตามที่คุณต้องการ.  
- **Add documents to index** พร้อมกับ PDF, DOCX, และรูปแบบอื่น ๆ.  
- สถานการณ์จริงที่ **log file extractor** เพิ่มคุณค่าอย่างวัดได้.  
- เคล็ดลับที่พิสูจน์แล้วในการ **optimise search performance** สำหรับคลังบันทึกหลายกิกะไบต์  

## คำตอบอย่างรวดเร็ว
- **What is a log file extractor?** ส่วนประกอบแบบกำหนดเองที่บอก GroupDocs.Search วิธีการอ่านและทำดัชนีไฟล์บันทึกข้อความธรรมดา.  
- **Why use GroupDocs.Search?** รองรับการทำดัชนีของรูปแบบกว่า 50 รูปแบบ, มีการทำ auto‑reindexing, และจัดการดัชนีได้ถึง 10 GB ด้วย RAM ต่ำกว่า 2 GB.  
- **Do I need a license?** ใช่ – จำเป็นต้องมีไลเซนส์ทดลองหรือเต็มเพื่อเปิดใช้งานไลบรารี.  
- **Can I index other file types simultaneously?** แน่นอน; สามารถผสม PDF, DOCX, และไฟล์บันทึกแบบกำหนดเองในดัชนีเดียวกัน.  
- **How to improve performance?** ใช้การทำดัชนีแบบ incremental, ปรับ `IndexSettings`, และเปิดใช้แฟล็ก `autoReindex`.  

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่ม, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

### ไลบรารีที่จำเป็น
เพิ่ม dependency ของ GroupDocs.Search ใน Maven ไปยังไฟล์ `pom.xml` ของคุณ ใช้เวอร์ชันล่าสุดที่ตรงกับระดับ Java ของโครงการของคุณ.

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

หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การตั้งค่าสภาพแวดล้อม
- JDK 8 หรือสูงกว่า.  
- ความคุ้นเคยกับการเขียนโปรแกรม Java และแนวคิดพื้นฐานของการจัดการไฟล์.  

### การรับไลเซนส์
เริ่มต้นด้วยการดาวน์โหลดไลเซนส์ทดลองฟรีเพื่อสำรวจคุณสมบัติของ GroupDocs.Search สำหรับการใช้งานในผลิตภัณฑ์, ให้ซื้อไลเซนส์เต็มหรือขอไลเซนส์ชั่วคราวผ่าน [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพื่อเริ่มต้น, ให้เริ่มต้นไลบรารีและใช้ไฟล์ไลเซนส์ของคุณ:

1. **Maven setup** – ยืนยันว่า dependency จากขั้นตอนก่อนหน้ามีอยู่.  
2. **License initialisation** – โหลดไฟล์ไลเซนส์ก่อนทำการเรียก API ใด ๆ.  

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

เมื่อสภาพแวดล้อมพร้อม, คุณสามารถดำเนินต่อไปเพื่อสร้าง **log file extractor** แบบกำหนดเอง.

## log file extractor คืออะไร?

log file extractor คือส่วนของโค้ดที่บอก GroupDocs.Search วิธีการอ่านไฟล์บันทึกดิบ (โดยทั่วไปเป็น `.log`) และแปลงเนื้อหาเป็นข้อความที่สามารถค้นหาได้ โดยการให้ extractor ของคุณเองคุณจะได้ควบคุมกฎการแยกวิเคราะห์, กรองสัญญาณรบกวน, และดึงข้อมูลที่สำคัญต่อกรณีการค้นหาของคุณอย่างเต็มที่.

## สร้าง log file extractor

GroupDocs.Search ให้คุณเชื่อมต่อ custom text extractors สำหรับไฟล์ประเภทใดก็ได้ ทำตามขั้นตอนต่อไปนี้เพื่อสร้าง extractor สำหรับไฟล์บันทึก.

### ขั้นตอนที่ 1: กำหนด custom extractor
`TextExtractorBase` คือคลาสฐานแบบ abstract ที่คุณต้องสืบทอดเพื่อสร้าง custom extractor. มันระบุส่วนขยายไฟล์ที่ extractor รองรับและมีตรรกะการสกัดหลัก.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Key points**  
- `getFileExtensions()` ลงทะเบียน extractor สำหรับไฟล์ `.log`.  
- `extractText` คือที่คุณสามารถลบ timestamps, กรองบรรทัด debug, หรือทำการ preprocessing ใด ๆ ที่จำเป็นสำหรับ **search large log files**.  

### ขั้นตอนที่ 2: กำหนดค่า index settings ด้วย extractor
เพิ่ม extractor ของคุณไปยัง `IndexSettings` และเปิดใช้งาน `autoReindex` เพื่อให้ไฟล์บันทึกใหม่ถูกทำดัชนีโดยอัตโนมัติโดยไม่ต้องทำด้วยตนเอง.

`IndexSettings` กำหนดพฤติกรรมของดัชนีเช่นขีดจำกัดหน่วยความจำและ custom extractors.  
`autoReindex` จะอัปเดตดัชนีโดยอัตโนมัติเมื่อไฟล์ต้นทางมีการเปลี่ยนแปลง.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### ขั้นตอนที่ 3: เพิ่มเอกสารลงในดัชนี
ตอนนี้ดัชนีรับรู้ไฟล์บันทึกแล้ว, คุณสามารถ **add documents to index** เช่นเดียวกับรูปแบบที่รองรับอื่น ๆ.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### ขั้นตอนที่ 4: ค้นหาดัชนี
ทำการค้นหาแบบ plain‑text. custom extractor รับประกันว่าทุกรายการบันทึกจะสามารถค้นหาได้.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## เคล็ดลับเพื่อเพิ่มประสิทธิภาพการค้นหา
- **Incremental indexing** – เพิ่มเฉพาะไฟล์บันทึกใหม่หรือที่เปลี่ยนแปลงแทนการสร้างดัชนีใหม่ทั้งหมด.  
- **Memory management** – แฟล็ก `autoReindex` ช่วยให้การใช้ RAM ต่ำโดยการล้างข้อมูลกลางลงดิสก์.  
- **Index settings** – ปรับ `setMaxMemoryUsage` ตามความจุของเซิร์ฟเวอร์; การตั้งค่าทั่วไปคือ 1 GB สำหรับดัชนีขนาด 10 GB.  
- **Query optimisation** – ใช้ phrase queries, wildcards, หรือ filters เพื่อจำกัดผลลัพธ์เมื่อค้นหาคลังบันทึกขนาดใหญ่.  

## การประยุกต์ใช้ในทางปฏิบัติ

GroupDocs.Search สามารถนำไปใช้ในหลายสถานการณ์จริง, เช่น:

- **Log management** – ค้นหาข้อความข้อผิดพลาด, การกระทำของผู้ใช้, หรือ timestamps เฉพาะในข้อมูลบันทึกหลายกิกะไบต์ภายในไม่กี่วินาที.  
- **Document retrieval systems** – รักษาที่เก็บข้อมูลที่สามารถค้นหาได้เป็นหนึ่งเดียวที่รวม PDF, เอกสาร Word, สเปรดชีต, และไฟล์บันทึกแบบกำหนดเอง.  
- **Content analysis** – รันรายงานความถี่ของคีย์เวิร์ดหรือค้นหาความผิดปกติในข้อมูลบันทึกแบบสตรีมมิ่ง.  

## ข้อควรพิจารณาด้านประสิทธิภาพ

เมื่อทำการปรับใช้ GroupDocs.Search ในระดับใหญ่, ควรคำนึงถึงแนวทางปฏิบัติที่ดีที่สุดต่อไปนี้:
- เก็บดัชนีบน SSD ที่เร็วเพื่อให้ latency การอ่าน/เขียนต่ำสุด.  
- ตรวจสอบการใช้ heap ของ JVM; พิจารณา off‑loading ดัชนีขนาดใหญ่ไปยังกระบวนการแยกหากหน่วยความจำเป็นคอขวด.  
- เปิดใช้งาน `autoReindex` (ตามที่แสดง) เพื่อให้ดัชนีเป็นปัจจุบันโดยไม่ต้องสร้างใหม่ด้วยตนเอง.  

## สรุป

จนถึงตอนนี้คุณได้สร้าง **log file extractor**, เรียนรู้วิธี **add documents to index**, และค้นพบวิธีการ **optimise search performance** สำหรับคลังบันทึกขนาดใหญ่ การผสานนี้ทำให้แอปพลิเคชัน Java ของคุณสามารถให้การค้นหาแบบเต็มข้อความที่เร็วและแม่นยำในทุกประเภทเอกสาร.

สำหรับการสำรวจเพิ่มเติม, ตรวจสอบ [GroupDocs documentation](https://docs.groupdocs.com/search/java/) อย่างเป็นทางการ หรือทดลองกับการทำงานของ extractor ต่าง ๆ เพื่อให้เหมาะกับกรณีการใช้งานของคุณ.

## ส่วนคำถามที่พบบ่อย
1. **What file types can I index using GroupDocs.Search?**  
   - คุณสามารถทำดัชนี PDF, เอกสาร Word, สเปรดชีต, และรูปแบบอื่น ๆ มากมาย, รวมถึงไฟล์บันทึกแบบกำหนดเองผ่าน text extractors.  
2. **How do I handle large document collections efficiently?**  
   - ใช้การอัปเดตแบบ incremental, แบ่ง partition ดัชนี, และปรับ `IndexSettings` เพื่อจัดการทรัพยากรอย่างมีประสิทธิภาพ.  
3. **Can GroupDocs.Search be integrated with other systems?**  
   - ใช่, มันมี Java API ที่สะอาดสามารถฝังลงในบริการที่มีอยู่, micro‑services, หรือเว็บแอปพลิเคชัน.  
4. **What is a temporary license, and how do I acquire one?**  
   - ไลเซนส์ชั่วคราวให้ฟังก์ชันเต็มสำหรับการประเมินโดยไม่มีขีดจำกัดเวลา. ขอผ่าน [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).  

## คำถามที่พบบ่อย
**Q: How does a log file extractor differ from the default extractor?**  
A: ตัว extractor เริ่มต้นจัดการรูปแบบทั่วไป (PDF, DOCX, ฯลฯ). ตัว **log file extractor** แบบกำหนดเองทำให้คุณกำหนดวิธีการแยกวิเคราะห์และทำดัชนีรายการบันทึกข้อความธรรมดาอย่างแม่นยำ.  

**Q: Can I index compressed log archives (e.g., .zip)?**  
A: ใช่, โดยเพิ่มขั้นตอน pre‑processing ที่สกัดไฟล์จาก archive ก่อนนำเข้าสู่ดัชนี.  

**Q: What’s the best way to keep the index up‑to‑date with continuously generated logs?**  
A: เปิดใช้งาน `autoReindex` และกำหนดเวลา watcher เบื้องหลังที่เรียก `index.add(newLogFile)` ทุกครั้งที่ไฟล์ใหม่ปรากฏ.  

**Q: Is there a limit to the size of a single log file that can be indexed?**  
A: โดยปฏิบัติแล้ว ขีดจำกัดขึ้นอยู่กับหน่วยความจำที่มีอยู่. แนะนำให้แบ่งไฟล์บันทึกขนาดใหญ่มากเป็นชิ้นย่อยก่อนทำดัชนี.  

**Q: Does GroupDocs.Search support fuzzy or wildcard searches?**  
A: ใช่, API การค้นหามีการจับคู่แบบ fuzzy, wildcards, และ proximity queries เพื่อปรับปรุงความเกี่ยวข้องของผลลัพธ์.  

---

**อัปเดตล่าสุด:** 2026-08-05  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง
- [Java Full Text Search: สร้างดัชนีด้วย GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [วิธีเพิ่มเอกสารลงในดัชนีด้วย GroupDocs.Search สำหรับ Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [ปรับปรุงประสิทธิภาพการค้นหาด้วย GroupDocs.Search Java: ปรับแต่งดัชนีและการค้นหา](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
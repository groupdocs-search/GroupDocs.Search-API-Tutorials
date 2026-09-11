---
date: '2026-09-11'
description: เรียนรู้วิธีการไฮไลท์ผลการค้นหา Java และทำดัชนีเอกสาร Java ด้วย GroupDocs.Search
  for Java ด้วยการทำดัชนีแบบ synchronous และ asynchronous
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: ไฮไลท์ผลการค้นหา Java ด้วย GroupDocs.Search. เรียนรู้การทำดัชนีแบบ
  synchronous และ asynchronous, การอัปเดตแบบ real‑time, และการไฮไลท์ผลในแอปพลิเคชัน
  Java.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: ไฮไลท์ผลการค้นหา Java – Fast synchronous & async indexing
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: ไฮไลท์ผลการค้นหา Java – Synchronous & async indexing
type: docs
url: /th/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# ไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบซิงโครนัสและอะซิงโครนัส

ในคู่มือนี้คุณจะได้ค้นพบวิธี **highlight search results Java** ด้วยไลบรารี GroupDocs.Search และคุณจะเห็นขั้นตอนการทำดัชนีเอกสาร Java ทั้งแบบซิงโครนัสและอะซิงโครนัส ไม่ว่าคุณจะสร้างเครื่องมือเดสก์ท็อปขนาดเล็กหรือบริการค้นหาองค์กรขนาดใหญ่ เทคนิคเหล่านี้ช่วยให้คุณส่งมอบผลลัพธ์ที่ตรงและชัดเจนทันทีโดยไม่บล็อกเธรดของแอปพลิเคชันของคุณ

## คำตอบอย่างรวดเร็ว
- **What does “highlight search results Java” mean?** หมายถึงการห่อหุ้มแต่ละคำที่ตรงกันในสแนปช็อตที่ส่งกลับด้วยมาร์กอัป (เช่น `<mark>`) เพื่อให้ผู้ใช้เห็นบริบทของผลลัพธ์ได้ทันที  
- **When should I use synchronous indexing?** ใช้สำหรับคอลเลกชันขนาดเล็กถึงกลางที่คุณต้องการให้เอกสารสามารถค้นหาได้ทันทีเมื่อเพิ่ม  
- **When is asynchronous indexing preferable?** เลือกใช้สำหรับชุดข้อมูลขนาดใหญ่หรือเมื่อเธรด UI ต้องตอบสนองต่อผู้ใช้ต่อเนื่องขณะดัชนีกำลังสร้างในพื้นหลัง  
- **Do I need a license?** การทดลองใช้ฟรีทำงานได้สำหรับการพัฒนา; ไลเซนส์เต็มจะลบข้อจำกัดและเปิดฟีเจอร์ขั้นสูง  
- **Which Java version is supported?** Java 8 หรือใหม่กว่า  

## “highlight search results Java” คืออะไร?
`highlight search results java` คือกระบวนการนำข้อมูลการจับคู่ดิบจาก GroupDocs.Search แล้วแทรกสัญญาณภาพ—โดยทั่วไปคือแท็ก HTML `<mark>`—รอบแต่ละคำที่พบ สิ่งนี้ทำให้สแนปช็อตผลลัพธ์อ่านได้ทันทีในหน้าเว็บหรือคอมโพเนนต์ Swing ช่วยปรับประสบการณ์ผู้ใช้โดยแสดงตำแหน่งที่คำค้นปรากฏอย่างชัดเจน

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
GroupDocs.Search มอบเครื่องยนต์ที่มีประสิทธิภาพสูงและไม่ขึ้นกับภาษา ซึ่งสามารถ **process up to 5 000 documents per second**, **support 30+ file formats**, และ **index 10 million‑document collections** โดยไม่ต้องโหลดคอร์ปัสทั้งหมดเข้าสู่หน่วยความจำ ฟีเจอร์ไฮไลท์ในตัว การทำดัชนีแบบเรียลไทม์ และตัววิเคราะห์หลายภาษา ทำให้เหมาะสำหรับระบบจัดการเนื้อหา, แคตาล็อกอีคอมเมิร์ซ, และคลังเอกสารระดับองค์กร

## ข้อกำหนดเบื้องต้น
- **Java Development Kit** (JDK 8 หรือใหม่กว่า) ที่ติดตั้งและตั้งค่า `JAVA_HOME` อย่างถูกต้อง  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**  
- โฟลเดอร์ (เช่น `documents/`) ที่มีไฟล์ที่คุณต้องการทำดัชนี—เช่น plain text, PDF, DOCX ฯลฯ  
- Maven สำหรับการจัดการ dependencies (หรือคุณสามารถเพิ่ม JAR ด้วยตนเองได้)  

### ไลบรารีและ dependencies ที่จำเป็น
เพิ่ม GroupDocs.Search ไปยังไฟล์ `pom.xml` ของ Maven ของคุณ:

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

สำหรับการดาวน์โหลดโดยตรง ให้รับเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การตั้งค่าสภาพแวดล้อม
- ตรวจสอบว่า `JAVA_HOME` ชี้ไปยัง JDK ที่เข้ากันได้  
- สร้างโปรเจกต์ Maven ใหม่และวางโค้ดสแนปที่ด้านบนลงในส่วน `<dependencies>`  
- วางไฟล์ตัวอย่างในไดเรกทอรีเช่น `src/main/resources/documents/`

## วิธีตั้งค่า GroupDocs.Search สำหรับ Java
`Index` คือคลาสหลักที่แทนคอลเลกชันที่สามารถค้นหาได้และถูกจัดเก็บบนดิสก์

สร้างอินสแตนซ์ `Index` ที่ชี้ไปยังโฟลเดอร์บนดิสก์, ใส่ไลเซนส์หากคุณมี, และกำหนดค่า analyzer สำหรับการทำโทเคนตามภาษาตามต้องการ ขั้นตอนการเตรียมนี้ทำให้เอนจินสามารถอ่าน, เขียน, และค้นหาดัชนีได้อย่างมีประสิทธิภาพ

คลาส `Index` เป็นส่วนประกอบหลักที่แทนคอลเลกชันที่สามารถค้นหาได้บนดิสก์ หลังจากคุณสร้างอินสแตนซ์แล้ว การทำดัชนีและการคิวรีทั้งหมดจะไหลผ่านอ็อบเจ็กต์นี้

1. **Install the library** – ใช้สแนป Maven ด้านบนหรือดาวน์โหลด JAR จาก [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Obtain a license** – เริ่มต้นด้วยไลเซนส์ทดลอง; แทนที่ด้วยคีย์ผลิตภัณฑ์ก่อนการใช้งานจริง  
3. **Initialize the index** – สแนปต่อไปนี้แสดงวิธีสร้าง (หรือเปิด) โฟลเดอร์ดัชนี:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## วิธีไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบซิงโครนัส
`DocumentHighlighter` คือคลาสยูทิลิตี้ที่สร้างสแนปไฮไลท์จากผลการค้นหา

โหลดดัชนี, เพิ่มเอกสารด้วย `index.add(documentPath)`, รันคิวรี, แล้วเรียก `DocumentHighlighter` เพื่อห่อผลลัพธ์ด้วยแท็ก `<mark>` กระบวนการทั้งหมดทำงานบนเธรดที่เรียกใช้ ดังนั้นเอกสารจะสามารถค้นหาได้ทันทีหลังจาก `add` คืนค่าให้ผู้ใช้

### ขั้นตอน 1: สร้างดัชนีและแนบการจัดการข้อผิดพลาด
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### ขั้นตอน 2: เพิ่มเอกสารและรันการค้นหา
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### ขั้นตอน 3: ประมวลผลผลลัพธ์และไฮไลท์ผลการค้นหา Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## วิธีไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบอะซิงโครนัส
`IndexingOptions` กำหนดวิธีการทำงานของกระบวนการทำดัชนี รวมถึงโหมดซิงโครนัสหรืออะซิงโครนัส

กำหนดค่า `IndexingOptions` ให้ทำงานในโหมดแบ็กกราวด์, สมัครรับเหตุการณ์ `StatusChanged`, และให้เอนจินทำดัชนีไฟล์ขณะ UI ของคุณยังคงให้บริการคำขออื่นๆ เมื่อสถานะเปลี่ยนเป็น `Ready` คุณสามารถทำการค้นหาและรับสแนปไฮไลท์ได้เช่นเดียวกับโหมดซิงโครนัส

`AsyncIndexingListener` รับการอัปเดตความคืบหน้า ช่วยให้คุณแสดงแถบความคืบหน้าหรือบันทึกสถานะโดยไม่บล็อกเธรดหลัก

### ขั้นตอน 1: ตั้งค่าดัชนีพร้อมผู้ฟังเหตุการณ์
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### ขั้นตอน 2: เปิดโหมดอะซิงโครนัสและเริ่มทำดัชนี
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## วิธีทำดัชนีเอกสาร Java – เคล็ดลับปฏิบัติ
`index.update(path)` อัปเดตเอกสารที่มีอยู่ในดัชนีด้วยไฟล์ที่ตำแหน่งที่ระบุ

แบ่งคอลเลกชันขนาดใหญ่เป็นชุดละ 1 000–5 000 ไฟล์, กรองตามส่วนขยายเพื่อหลีกเลี่ยงการพาร์เซที่ไม่จำเป็น, และใช้ `index.update(path)` สำหรับไฟล์ที่เปลี่ยนแปลงแทนการสร้างดัชนีใหม่ทั้งหมด วิธีเหล่านี้ช่วยให้การใช้หน่วยความจำน้อยและเวลาการทำดัชนีคาดเดาได้เพื่อรักษาความสอดคล้อง

- **Batch size**: สำหรับคอลเลกชันขนาดใหญ่ ให้แยกโฟลเดอร์เป็นชุดย่อยเพื่อหลีกเลี่ยงการพุ่งของหน่วยความจำ  
- **File filters**: ใช้ `IndexingOptions.setFileExtensions` เพื่อรวมเฉพาะรูปแบบที่คุณต้องการ (เช่น `.pdf`, `.docx`)  
- **Re‑indexing**: เมื่อเอกสารมีการเปลี่ยนแปลง ให้เรียก `index.update(documentPath)` แทนการสร้างดัชนีใหม่จากศูนย์  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Memory**: ตรวจสอบการใช้ heap; เพิ่ม `-Xmx` หากคุณประมวลผลไฟล์ขนาดใหญ่หลายไฟล์พร้อมกัน  
- **CPU**: การทำดัชนีแบบอะซิงโครนัสกระจายภาระงานไปยังเธรดหลายตัวแต่ยังคงใช้ CPU—ตรวจสอบการใช้ด้วย JVisualVM  
- **Result highlighting**: การไฮไลท์เพิ่มภาระเล็กน้อย (≈ 2–5 ms ต่อผลลัพธ์). แคช HTML ที่สร้างขึ้นหากต้องการแสดงสแนปเดียวกันหลายครั้ง  

## คำถามที่พบบ่อย

**Q: ฉันสามารถรวมการทำดัชนีแบบซิงโครนัสและอะซิงโครนัสในแอปพลิเคชันเดียวกันได้หรือไม่?**  
A: ใช่. ใช้การทำดัชนีแบบซิงโครนัสสำหรับชุดข้อมูลขนาดเล็กที่อัปเดตบ่อยและการทำดัชนีแบบอะซิงโครนัสสำหรับการนำเข้าจำนวนมากหรืองานเบื้องหลัง  

**Q: ฉันจะปรับแต่งสไตล์การไฮไลท์อย่างไร?**  
A: ให้สร้างการทำงานของ `DocumentHighlighter` แบบกำหนดเองที่เขียน HTML, CSS หรือ XML ที่ต้องการรอบคำที่ตรงกัน  

**Q: GroupDocs.Search รองรับไฟล์ประเภทใดบ้างโดยไม่ต้องกำหนดค่าเพิ่มเติม?**  
A: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML และอื่น ๆ อีกมากมายผ่านตัวพาร์เซในตัว—รองรับกว่า 30 รูปแบบทั้งหมด  

**Q: สามารถค้นหาในหลายภาษาได้พร้อมกันหรือไม่?**  
A: แน่นอน. GroupDocs.Search มีตัววิเคราะห์หลายภาษา; เพียงกำหนดค่า `Analyzer` ที่เหมาะสมเมื่อสร้างดัชนี  

**Q: ฉันจะรักษาความปลอดภัยของโฟลเดอร์ดัชนีอย่างไร?**  
A: เก็บดัชนีในไดเรกทอรีที่ได้รับการปกป้อง, ตั้งค่าการอนุญาตระบบไฟล์อย่างเข้มงวด, และอาจเข้ารหัสดัชนีโดยใช้ฟีเจอร์ความปลอดภัยของไลบรารี  

---

**อัปเดตล่าสุด:** 2026-09-11  
**ทดสอบกับ:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [วิธีสร้างดัชนีเอกสารและเพิ่มเอกสารโดยใช้ GroupDocs.Search API สำหรับ Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [วิธีสร้างที่เก็บดัชนี Java ด้วย GroupDocs.Search: การทำดัชนีและการค้นหาเอกสารอย่างมีประสิทธิภาพ](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [การทำดัชนีเอกสารอย่างมีประทธิภาพด้วย Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)
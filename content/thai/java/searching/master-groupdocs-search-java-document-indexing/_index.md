---
date: '2026-02-08'
description: เรียนรู้วิธีการไฮไลท์ผลการค้นหาใน Java และวิธีการทำดัชนีเอกสารด้วย Java
  โดยใช้ GroupDocs.Search for Java พร้อมการทำดัชนีแบบซิงโครนัสและอะซิงโครนัส
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: ไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบซิงโครนัสและอะซิงโครนัส
type: docs
url: /th/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# ไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบซิงโครนัสและอะซิงโครนัส

เพิ่มประสิทธิภาพแอปพลิเคชัน Java ของคุณด้วย **การไฮไลท์ผลการค้นหา Java** ด้วยไลบรารี GroupDocs.Search ที่ทรงพลัง ไม่ว่าคุณจะทำงานกับไฟล์ไม่กี่ไฟล์หรือคลังข้อมูลขนาดใหญ่ การเชี่ยวชาญทั้งการทำดัชนีแบบซิงโครนัสและอะซิงโครนัสจะช่วยให้คุณส่งมอบผลลัพธ์ที่เร็วและแม่นยำโดยไม่บล็อกเธรดของแอปพลิเคชัน

## คำตอบอย่างรวดเร็ว
- **“highlight search results Java” หมายถึงอะไร?** หมายถึงการแสดงคำที่ตรงกันในผลการค้นหาด้วยสัญญาณภาพ (เช่น แท็ก HTML `<mark>`) เพื่อให้ผู้ใช้เห็นว่าคำค้นปรากฏที่ไหนในแต่ละเอกสาร  
- **ควรใช้การทำดัชนีแบบซิงโครนัสเมื่อใด?** สำหรับชุดข้อมูลขนาดเล็กถึงกลางที่ต้องการให้เอกสารที่เพิ่มใหม่พร้อมใช้งานทันที  
- **การทำดัชนีแบบอะซิงโครนัสเหมาะเมื่อใด?** เมื่อประมวลผลคอลเลกชันเอกสารขนาดใหญ่หรือทำงานบน UI thread ที่ต้องรักษาความตอบสนองของแอปพลิเคชัน  
- **ต้องการไลเซนส์หรือไม่?** ทดลองใช้ฟรีสำหรับการพัฒนา; ไลเซนส์เต็มจะเปิดฟีเจอร์ขั้นสูงและลบข้อจำกัดการใช้งาน  
- **รองรับเวอร์ชัน Java ใด?** Java 8 หรือใหม่กว่า  

## “highlight search results Java” คืออะไร?
การไฮไลท์ผลการค้นหาใน Java หมายถึงการนำผลการจับคู่ดิบที่ GroupDocs.Search คืนมาและห่อหุ้มคำที่ตรงกันด้วย HTML (หรือมาร์กอัปอื่น) เพื่อให้เด่นชัดเมื่อแสดงใน UI หรือหน้าเว็บ สิ่งนี้ช่วยปรับประสบการณ์ผู้ใช้โดยแสดงบริบทของแต่ละผลลัพธ์ทันที  

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
GroupDocs.Search ให้เครื่องมือค้นหาที่มีประสิทธิภาพสูงและไม่ขึ้นกับภาษา รองรับ:
- การทำดัชนีและการค้นหาแบบเรียลไทม์
- การประมวลผลแบบอะซิงโครนัสสำหรับงานปริมาณมาก
- การไฮไลท์ผลลัพธ์ในตัว
- รองรับหลายภาษาและตัววิเคราะห์แบบกำหนดเอง  

ความสามารถเหล่านี้ทำให้เหมาะกับระบบจัดการเนื้อหา, แคตาล็อกอีคอมเมิร์ซ, และคลังเอกสารระดับองค์กร  

## ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

- **Java Development Kit** (JDK 8 หรือใหม่กว่า) ติดตั้งแล้ว  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**  
- โฟลเดอร์ที่มีเอกสารที่คุณต้องการทำดัชนี  
- Maven สำหรับการจัดการ dependencies (หรือคุณสามารถดาวน์โหลด JAR ด้วยตนเอง)  

### ไลบรารีและ dependencies ที่จำเป็น
เพิ่ม GroupDocs.Search ไปยังโปรเจกต์ Maven ของคุณ:

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

สำหรับการดาวน์โหลดโดยตรง ให้รับเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### การตั้งค่าสภาพแวดล้อม
- ตรวจสอบว่า **JAVA_HOME** ของคุณชี้ไปยัง JDK ที่เข้ากันได้  
- สร้างโปรเจกต์ใน IDE ของคุณและเพิ่มการกำหนดค่า Maven ด้านบน  
- เตรียมไดเรกทอรี (เช่น `documents/`) ที่มีไฟล์ข้อความ, PDF หรือ Word ตัวอย่าง  

## วิธีตั้งค่า GroupDocs.Search สำหรับ Java
1. **Install the Library** – ใช้สแนปช็อต Maven ด้านบนหรือดาวน์โหลด JAR จาก [GroupDocs](https://releases.groupdocs.com/search/java/)  
2. **Obtain a License** – เริ่มต้นด้วยไลเซนส์ทดลอง แล้วอัปเกรดเมื่อย้ายไปสู่การผลิต  
3. **Initialize the Index** – ตัวอย่างโค้ดต่อไปนี้แสดงวิธีสร้าง (หรือเปิด) โฟลเดอร์ดัชนี:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## วิธีไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบซิงโครนัส
การทำดัชนีแบบซิงโครนัสจะประมวลผลเอกสารทันที ทำให้ไฟล์ที่เพิ่มใหม่พร้อมค้นหาได้โดยทันที  

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

### ขั้นตอน 2: เพิ่มเอกสารและทำการค้นหา
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### ขั้นตอน 3: ประมวลผลผลลัพธ์และ **ไฮไลท์ผลการค้นหา Java**
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

`DocumentHighlighter` จะห่อหุ้มคำที่ตรงกันโดยอัตโนมัติด้วยแท็ก `<mark>` (หรือรูปแบบใด ๆ ที่คุณกำหนด) ทำให้คุณได้ **ผลลัพธ์การค้นหาที่ไฮไลท์** พร้อมแสดงผล  

## วิธีไฮไลท์ผลการค้นหา Java – การทำดัชนีแบบอะซิงโครนัส
เมื่อจัดการกับไฟล์หลายพันไฟล์ การบล็อกเธรดหลักเป็นสิ่งที่ไม่ต้องการ การทำดัชนีแบบอะซิงโครนัสทำให้เอนจินทำงานในพื้นหลัง  

### ขั้นตอน 1: ตั้งค่าดัชนีพร้อมกับ event listeners
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

### ขั้นตอน 2: เปิดใช้งานโหมดอะซิงโครนัสและเริ่มทำดัชนี
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

ขณะที่ดัชนีกำลังสร้าง แอปพลิเคชันของคุณสามารถให้บริการคำขออื่นต่อไปได้ เมื่อเหตุการณ์ `StatusChanged` รายงาน `Ready` คุณสามารถทำการค้นหาอย่างปลอดภัยและรับ **ผลลัพธ์การค้นหาที่ไฮไลท์ Java**  

## วิธี **index documents java** – เคล็ดลับปฏิบัติ
- **Batch size**: สำหรับคอลเลกชันขนาดใหญ่ ให้แบ่งโฟลเดอร์เป็นชุดย่อยเพื่อหลีกเลี่ยงการกระตุ้นหน่วยความจำสูงขึ้น  
- **File filters**: ใช้ `IndexingOptions.setFileExtensions` เพื่อรวมเฉพาะรูปแบบที่ต้องการ (เช่น `.pdf`, `.docx`)  
- **Re‑indexing**: เมื่อเอกสารมีการเปลี่ยนแปลง ให้เรียก `index.update(documentPath)` แทนการสร้างดัชนีใหม่ทั้งหมด  

## พิจารณาด้านประสิทธิภาพ
- **Memory**: ตรวจสอบการใช้ heap; เพิ่ม `-Xmx` หากประมวลผลไฟล์ขนาดใหญ่หลายไฟล์  
- **CPU**: การทำดัชนีแบบอะซิงโครนัสกระจายภาระงาน แต่ยังคงใช้ CPU — ควรตรวจสอบด้วย JVisualVM  
- **Result Highlighting**: การไฮไลท์เพิ่มภาระการประมวลผลเล็กน้อย; ควรแคช HTML ที่สร้างขึ้นหากต้องแสดงผลลัพธ์ซ้ำหลายครั้ง  

## คำถามที่พบบ่อย

**Q: สามารถผสานการทำดัชนีแบบซิงโครนัสและอะซิงโครนัสในแอปพลิเคชันเดียวกันได้หรือไม่?**  
A: ได้. ใช้การทำดัชนีแบบซิงโครนัสสำหรับชุดข้อมูลขนาดเล็กที่อัปเดตบ่อย และใช้การทำดัชนีแบบอะซิงโครนัสสำหรับการนำเข้าจำนวนมากหรืองานพื้นหลัง  

**Q: จะปรับแต่งสไตล์การไฮไลท์อย่างไร?**  
A: ให้สร้างการนำเข้า `DocumentHighlighter` แบบกำหนดเองที่เขียนแท็ก HTML, CSS หรือ XML ที่ต้องการล้อมรอบคำที่ตรงกัน  

**Q: GroupDocs.Search รองรับประเภทไฟล์ใดบ้างโดยตรง?**  
A: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, และอื่น ๆ อีกมากมายผ่านตัวแปลงในตัว  

**Q: สามารถค้นหาในหลายภาษาพร้อมกันได้หรือไม่?**  
A: แน่นอน. GroupDocs.Search มีตัววิเคราะห์หลายภาษา; เพียงกำหนด `Analyzer` ที่เหมาะสมเมื่อสร้างดัชนี  

**Q: จะรักษาความปลอดภัยของโฟลเดอร์ดัชนีอย่างไร?**  
A: เก็บดัชนีในไดเรกทอรีที่ได้รับการปกป้อง ตั้งค่าการอนุญาตไฟล์ระบบให้เหมาะสม และพิจารณาเข้ารหัสดัชนีด้วยฟีเจอร์ความปลอดภัยของไลบรารี  

---

**Last Updated:** 2026-02-08  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
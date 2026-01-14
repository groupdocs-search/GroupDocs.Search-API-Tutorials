---
date: '2026-01-14'
description: เรียนรู้วิธีสร้างดัชนี Java และสกัดข้อความ Java อย่างมีประสิทธิภาพด้วย
  GroupDocs.Search for Java ปรับปรุงการค้นหาเอกสาร ส่งออกข้อความไปยังไฟล์ และจัดการการสกัดข้อความที่มีโครงสร้าง
keywords:
- GroupDocs.Search for Java
- efficient document search
- index creation in Java
title: วิธีสร้างดัชนี Java ด้วย GroupDocs.Search สำหรับ Java
type: docs
url: /th/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# เชี่ยวชาญการค้นหาเอกสารอย่างมีประสิทธิภาพด้วย GroupDocs.Search for Java

ในโลกของการจัดการเอกสาร การค้นหาเนื้อหาเฉพาะอย่างรวดเร็วในเอกสารจำนวนมากเป็นสิ่งสำคัญ ไม่ว่าคุณจะจัดการสัญญากฎหมายหรือเอกสารวิชาการ **create index java** สามารถประหยัดเวลาการทำงานด้วยมือหลายชั่วโมง บทแนะนำนี้จะพาคุณไปใช้ **GroupDocs.Search for Java**, ไลบรารี **java search library** ที่ทรงพลัง ช่วยให้คุณสร้าง index, **add documents to index**, และ **extract text java** จากไฟล์ของคุณได้อย่างมีประสิทธิภาพ เมื่ออ่านจบคุณจะรู้วิธีตั้งค่า indexing ด้วยการกำหนดค่าที่กำหนดเองและส่งออกข้อความเอกสารในรูปแบบต่าง ๆ รวมถึงการสกัดข้อความแบบโครงสร้าง

## คำตอบสั้น
- **วัตถุประสงค์หลักคืออะไร?** เพื่อ **create index java** และดึงเนื้อหาเอกสารอย่างรวดเร็ว.  
- **ควรใช้ไลบรารีอะไร?** **GroupDocs.Search for Java** **java search library**.  
- **ฉันสามารถส่งออกข้อความเป็นไฟล์ได้หรือไม่?** ได้, ใช้ **output text to file** adapters ที่ให้มา.  
- **การสกัดข้อมูลแบบโครงสร้างได้รับการสนับสนุนหรือไม่?** แน่นอน – ใช้ **structured text extraction** adapter.  
- **ฉันต้องการไลเซนส์หรือไม่?** จำเป็นต้องมีไลเซนส์แบบทดลองหรือไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## สิ่งที่คุณจะได้เรียนรู้
- วิธี **create index java** และ **add documents to index** ด้วย GroupDocs.Search for Java.  
- เทคนิคสำหรับ **output text to file**, streams, strings, และ structured data.  
- เคล็ดลับการเพิ่มประสิทธิภาพการทำงานสำหรับการค้นหาอย่างมีประสิทธิภาพและการจัดการหน่วยความจำ.  
- การประยุกต์ใช้จริงของคุณลักษณะเหล่านี้.

### ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำตามบทแนะนำ, ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้พร้อมใช้งาน:
- **Java Development Kit (JDK)**: แนะนำให้ใช้เวอร์ชัน 8 หรือสูงกว่า.  
- **GroupDocs.Search for Java** library.  
- **Maven** สำหรับการจัดการ dependencies และการสร้างโปรเจคของคุณ.  
- ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม Java, โดยเฉพาะการทำงานกับไฟล์ I/O.

### การตั้งค่า GroupDocs.Search for Java
เพื่อเริ่มใช้ GroupDocs.Search for Java, คุณต้องเพิ่ม dependencies ที่จำเป็นในโปรเจคของคุณ. นี่คือวิธีตั้งค่าโดยใช้ Maven:

**Maven Setup**  
เพิ่มการกำหนด repository และ dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

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

สำหรับผู้ที่ต้องการดาวน์โหลดโดยตรง, คุณสามารถรับเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition**  
เพื่อใช้ GroupDocs.Search, พิจารณาได้รับไลเซนส์ทดลองฟรีหรือไลเซนส์ชั่วคราว. สำหรับการซื้อเต็มรูปแบบ, เยี่ยมชมเว็บไซต์อย่างเป็นทางการของพวกเขาเพื่อรับไลเซนส์ถาวร.

## วิธีสร้าง index java ด้วยการตั้งค่าที่กำหนดเอง
ส่วนนี้จะแนะนำคุณผ่านการสร้าง index, การเพิ่มเอกสาร, และการกำหนดค่าการบีบอัดเพื่อการจัดเก็บที่เหมาะสมที่สุด.

### การสร้าง Index และการทำ Index เอกสาร

#### ภาพรวม
การสร้าง index ช่วยให้คุณค้นหาเอกสารได้อย่างมีประสิทธิภาพ. ตัวอย่างด้านล่างแสดงวิธี **create index java** ด้วยการบีบอัดสูงและจากนั้น **add documents to index**.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**Explanation**  
- **Index Settings**: เราเปิดใช้งานการบีบอัดสูงสำหรับการจัดเก็บข้อความ, เพื่อเพิ่มประสิทธิภาพการใช้พื้นที่ดิสก์.  
- **Adding Documents**: เมธอด `index.add()` **adds documents to index**, สแกนโฟลเดอร์แบบเรียกซ้ำ.

## วิธีส่งออกข้อความเป็นไฟล์, สตรีม, สตริง, และรูปแบบโครงสร้าง
ต่อไปนี้คือสี่วิธีทั่วไปในการดึงและจัดเก็บเนื้อหาที่สกัดหลังจากที่คุณ **created index java**.

### การส่งออกข้อความเอกสารเป็นไฟล์

#### ภาพรวม
ตัวอย่างนี้แสดงวิธี **output text to file** ในรูปแบบ HTML, ซึ่งสะดวกสำหรับการตรวจสอบภาพหรือการประมวลผลต่อไป.

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**Explanation**  
- **FileOutputAdapter**: แปลงข้อความของเอกสารที่ทำ index เป็น HTML และเขียนลงในเส้นทางไฟล์ที่ระบุ.

### การส่งออกข้อความเอกสารเป็นสตรีม

#### ภาพรวม
เมื่อคุณต้องการการประมวลผลในหน่วยความจำ—เช่นการสร้างเนื้อหาเว็บแบบไดนามิก—การส่งออกเป็นสตรีมเป็นทางเลือกที่เหมาะสม.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**Explanation**  
- **StreamOutputAdapter**: ส่งข้อความของเอกสารไปยัง `ByteArrayOutputStream`, ทำให้จัดการได้อย่างยืดหยุ่นโดยไม่ต้องเข้าถึงระบบไฟล์.

### การส่งออกข้อความเอกสารเป็นสตริง

#### ภาพรวม
หากคุณต้องการบันทึกหรือแสดงเนื้อหา, การแปลงผลลัพธ์เป็น `String` เป็นวิธีที่เร็วที่สุด.

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**Explanation**  
- **StringOutputAdapter**: จับข้อความของเอกสารใน `String`, ทำให้สามารถฝังลงในบันทึกหรือส่วนประกอบ UI ได้ง่าย.

### การส่งออกข้อความเอกสารเป็นรูปแบบโครงสร้าง

#### ภาพรวม
สำหรับการแยกวิเคราะห์ขั้นสูง—เช่นการสกัดฟิลด์, ตาราง, หรือเมตาดาต้ากำหนดเอง—ใช้ structured output adapter.

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**Explanation**  
- **StructuredOutputAdapter**: สกัดข้อความเอกสารเป็นรูปแบบ **structured text extraction**, ทำให้สามารถวิเคราะห์อย่างละเอียดหรือใช้ใน pipeline ข้อมูลต่อไปได้.

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **Index not created** | เส้นทางโฟลเดอร์ไม่ถูกต้องหรือไม่มีสิทธิ์การเขียน | ตรวจสอบว่า `indexFolder` มีอยู่และแอปพลิเคชันมีสิทธิ์การเขียน |
| **No documents returned** | `index.add()` ไม่ได้ถูกเรียกหรือโฟลเดอร์ต้นทางผิด | ตรวจสอบว่า `documentsFolder` ชี้ไปยังไดเรกทอรีที่ถูกต้องและมีไฟล์ประเภทที่รองรับ |
| **Output file empty** | เส้นทางของ Output adapter ไม่ถูกต้องหรือไม่มีไดเรกทอรี | สร้างไดเรกทอรีเป้าหมาย (`YOUR_OUTPUT_DIRECTORY`) ก่อนทำงาน |
| **Memory spikes with large files** | โหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ | ใช้ stream adapters (`StreamOutputAdapter`) เพื่อประมวลผลข้อมูลเป็นขั้นตอน |

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้ GroupDocs.Search กับภาษา JVM อื่น ๆ เช่น Kotlin หรือ Scala ได้หรือไม่?**  
A: ใช่, ไลบรารีเป็น Java แท้และทำงานร่วมกับภาษา JVM ใดก็ได้อย่างไม่มีปัญหา.

**Q: การบีบอัดส่งผลต่อความเร็วการค้นหาอย่างไร?**  
A: การบีบอัดสูงช่วยลดการใช้พื้นที่ดิสก์แต่อาจเพิ่มภาระ CPU เล็กน้อยในระหว่างการทำ index. ประสิทธิภาพการค้น่ายังคงเร็วเพราะไลบรารีทำการแตกบีบอัดแบบ on‑the‑fly.

**Q: สามารถอัปเดต index ที่มีอยู่โดยไม่ต้องสร้างใหม่ได้หรือไม่?**  
A: แน่นอน. ใช้ `index.add()` สำหรับไฟล์ใหม่และ `index.remove()` เพื่อลบไฟล์ที่ล้าสมัย.

**Q: รูปแบบการส่งออกใดเหมาะที่สุดสำหรับการประมวลผลภาษาธรรมชาติต่อไป?**  
A: `PlainText` ผ่าน **structured text extraction** adapter ให้เนื้อหาที่สะอาดและไม่ขึ้นกับภาษา เหมาะสำหรับ pipeline NLP.

**Q: ฉันต้องการไลเซนส์สำหรับการพัฒนาและการทดสอบหรือไม่?**  
A: ไลเซนส์ทดลองฟรีใช้ได้สำหรับการพัฒนาและการประเมิน. การใช้งานในสภาพแวดล้อมการผลิตต้องมีไลเซนส์ที่ซื้อมา.

---

อัปเดตล่าสุด: 2026-01-14  
ทดสอบกับ: GroupDocs.Search 25.4 for Java  
ผู้เขียน: GroupDocs
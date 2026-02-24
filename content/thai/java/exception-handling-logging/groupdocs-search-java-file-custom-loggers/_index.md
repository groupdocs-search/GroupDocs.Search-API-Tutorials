---
date: '2026-02-24'
description: เรียนรู้วิธีสร้าง logger แบบกำหนดเอง ตั้งค่าขนาดสูงสุดของ log และกำหนดค่าการบันทึกลงคอนโซลหรือไฟล์ใน
  GroupDocs.Search สำหรับ Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: วิธีสร้าง Logger แบบกำหนดเองและจำกัดขนาดไฟล์บันทึกด้วย GroupDocs.Search Java
type: docs
url: /th/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

 content.# จำกัดขนาดไฟล์บันทึกด้วย GroupDocs.Search Java Loggers

ในคู่มือนี้คุณจะ **สร้าง custom logger** implementation และเรียนรู้วิธี **จำกัดขนาดไฟล์บันทึก** ขณะใช้ GroupDocs.Search สำหรับ Java การควบคุมการเติบโตของบันทึกเป็นสิ่งสำคัญสำหรับการทำดัชนีเอกสารขนาดใหญ่ และ logger ที่มาพร้อมให้คุณ **ตั้งค่า max log size**, **roll over log file**, หรือสลับไปใช้ **use console logger** เพื่อรับฟีดแบ็กทันที เราจะเดินผ่านการตั้งค่าครบถ้วน ตั้งแต่การกำหนดค่า Maven ไปจนถึงการรัน query การค้นหา และดูวิธี **add documents index** พร้อม logger

## Quick Answers
- **What does “limit log file size” mean?** มันจำกัดขนาดสูงสุดของไฟล์บันทึก เพื่อป้องกันการเติบโตโดยไม่มีการควบคุมบนดิสก์.  
- **Which logger lets you limit log file size?** Logger ที่มาพร้อม `FileLogger` รองรับพารามิเตอร์ max‑size.  
- **How do I use console logger java?** สร้างอินสแตนซ์ `ConsoleLogger` แล้วตั้งค่าให้กับ `IndexSettings`.  
- **Do I need a license for GroupDocs.Search?** สามารถใช้รุ่นทดลองเพื่อประเมินผลได้; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **What’s the first step?** เพิ่ม dependency ของ GroupDocs.Search ลงในโปรเจกต์ Maven ของคุณ.  

## ขนาดไฟล์บันทึกที่จำกัดคืออะไร?
การจำกัดขนาดไฟล์บันทึกหมายถึงการกำหนดค่า logger ให้เมื่อไฟล์ถึงเกณฑ์ที่กำหนดไว้ (เช่น 4 MB) จะหยุดเพิ่มขนาดหรือทำการ roll over. สิ่งนี้ทำให้การใช้พื้นที่จัดเก็บของแอปพลิเคชันคาดเดาได้และหลีกเลี่ยงการลดประสิทธิภาพ.

## ทำไมต้องใช้ไฟล์และ custom logger กับ GroupDocs.Search?
- **Auditability:** เก็บ audit trail ของทุกเอกสารที่ทำดัชนี.  
- **Debugging:** ระบุปัญหาได้อย่างรวดเร็วโดยการตรวจสอบบันทึกที่กระชับ.  
- **Flexibility:** เลือกใช้ระหว่างไฟล์บันทึกที่คงอยู่กับการแสดงผลบนคอนโซลทันที (`use console logger`).  

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 หรือใหม่กว่า, IDE (IntelliJ IDEA, Eclipse, ฯลฯ).  
- ความรู้พื้นฐานเกี่ยวกับ Java และ Maven.  

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพิ่มไลบรารีลงในโปรเจกต์ของคุณโดยใช้หนึ่งในวิธีต่อไปนี้.

**Maven Setup:**

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

**Direct Download:**  
ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับลิขสิทธิ์
รับรุ่นทดลองหรือซื้อใบอนุญาตผ่าน [licensing page](https://purchase.groupdocs.com/temporary-license/).

## วิธีสร้าง custom logger สำหรับ GroupDocs.Search
GroupDocs.Search อนุญาตให้คุณเชื่อมต่อการทำงานของ `ILogger` ใด ๆ ได้. โดยการสืบทอดจาก `FileLogger` หรือ `ConsoleLogger` คุณสามารถเพิ่มพฤติกรรมเพิ่มเติม—เช่นการ roll over ไฟล์บันทึกหรือส่งข้อความไปยังบริการตรวจสอบระยะไกล ความยืดหยุ่นนี้เป็นเหตุผลที่หลายทีม **create custom logger** โซลูชันที่ตรงกับความต้องการการดำเนินงานของพวกเขา.

## วิธีจำกัดขนาดไฟล์บันทึกด้วย File Logger
ด้านล่างเป็นคู่มือขั้นตอนที่แสดงวิธี **configure file logger** เพื่อให้ไฟล์บันทึกไม่เกินขนาดที่คุณกำหนด.

### 1️⃣ นำเข้าแพ็กเกจที่จำเป็น
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ ตั้งค่า Index Settings ด้วย File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ สร้างหรือโหลด Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ เพิ่มเอกสารลงใน Index
```java
index.add(documentsFolder);
```

### 5️⃣ ดำเนินการค้นหา Query
```java
SearchResult result = index.search(query);
```

**Key point:** ตัวสร้าง `FileLogger` พารามิเตอร์ที่สอง (`4.0`) กำหนด **set max log size** เป็นเมกะไบต์ ซึ่งตอบสนองต่อความต้องการ **limit log file size** โดยตรง.

## วิธีใช้ console logger java
หากคุณต้องการฟีดแบ็กทันทีในเทอร์มินัล ให้สลับจาก file logger ไปเป็น console logger.

### 1️⃣ นำเข้า Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ ตั้งค่า Index Settings ด้วย Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ สร้างหรือโหลด Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ เพิ่มเอกสารและดำเนินการค้นหา
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** console logger เหมาะสำหรับการพัฒนาเนื่องจากพิมพ์แต่ละบันทึกทันที ช่วยให้คุณตรวจสอบว่าการทำดัชนีและการค้นหาทำงานตามที่คาดหวัง.

## การประยุกต์ใช้ในทางปฏิบัติ
1. **Document Management Systems:** เก็บ audit trail ของทุกเอกสารที่ทำดัชนี.  
2. **Enterprise Search Engines:** ตรวจสอบประสิทธิภาพของ query และอัตราข้อผิดพลาดแบบเรียลไทม์.  
3. **Legal & Compliance Software:** บันทึกคำค้นหาเพื่อการรายงานตามกฎระเบียบ.

## พิจารณาด้านประสิทธิภาพ
- **Log Size:** ด้วยการ **set max log size** คุณจะหลีกเลี่ยงการใช้ดิสก์มากเกินไปซึ่งอาจทำให้แอปพลิเคชันช้าลง.  
- **Asynchronous Logging:** หากต้องการ throughput สูงขึ้น ให้พิจารณาห่อ logger ด้วยคิวแบบ async (อยู่นอกขอบเขตของคู่มือนี้).  
- **Memory Management:** ปล่อยวัตถุ `Index` ขนาดใหญ่เมื่อไม่ต้องการใช้งานแล้ว เพื่อรักษาขนาด JVM ให้ต่ำ.

## ปัญหาทั่วไปและวิธีแก้
- **Log path not accessible:** ตรวจสอบว่าไดเรกทอรีมีอยู่และแอปพลิเคชันมีสิทธิ์เขียน.  
- **Logger not firing:** ตรวจสอบว่าคุณเรียก `settings.setLogger(...)` *ก่อน* สร้างวัตถุ `Index`.  
- **Console output missing:** ยืนยันว่าคุณกำลังรันแอปพลิเคชันในเทอร์มินัลที่แสดง `System.out`.

## คำถามที่พบบ่อย

**Q: What does the second parameter of `FileLogger` control?**  
A: มันกำหนดขนาดสูงสุดของไฟล์บันทึกเป็นเมกะไบต์ ทำให้คุณสามารถ **set max log size**.

**Q: Can I combine file and console loggers?**  
A: ใช่ โดยการสร้าง custom logger ที่ส่งข้อความไปยังทั้งสองปลายทาง.

**Q: How do I add documents to index after the initial creation?**  
A: เรียก `index.add(pathToNewDocs)` ได้ตลอดเวลา; logger จะบันทึกการดำเนินการ.

**Q: Is `ConsoleLogger` thread‑safe?**  
A: มันเขียนโดยตรงไปยัง `System.out` ซึ่ง JVM ทำการซิงโครไนซ์ ทำให้ปลอดภัยสำหรับการใช้งานส่วนใหญ่.

**Q: Will limiting the log file size affect the amount of information stored?**  
A: เมื่อถึงขีดจำกัดขนาด ไฟล์บันทึกใหม่อาจถูกละทิ้งหรือไฟล์อาจ **roll over log file** ขึ้นอยู่กับการทำงานของ logger.

## แหล่งข้อมูล
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**อัปเดตล่าสุด:** 2026-02-24  
**ทดสอบด้วย:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs
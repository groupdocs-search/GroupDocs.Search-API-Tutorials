---
date: '2025-12-24'
description: เรียนรู้วิธีจำกัดขนาดไฟล์บันทึกและใช้คอนโซลล็อกเกอร์ใน Java กับ GroupDocs.Search
  สำหรับ Java คู่มือนี้ครอบคลุมการกำหนดค่าการบันทึก, เคล็ดลับการแก้ปัญหา, และการเพิ่มประสิทธิภาพการทำงาน.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: จำกัดขนาดไฟล์บันทึกด้วย GroupDocs.Search Java Loggers
type: docs
url: /th/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# จำกัดขนาดไฟล์บันทึกด้วย GroupDocs.Search Java Loggers

การบันทึกที่มีประสิทธิภาพเป็นสิ่งสำคัญเมื่อจัดการคอลเลกชันเอกสารขนาดใหญ่, โดยเฉพาะเมื่อคุณต้อง **limit log file size** เพื่อควบคุมการใช้พื้นที่จัดเก็บ. **GroupDocs.Search for Java** มีโซลูชันที่แข็งแกร่งสำหรับการจัดการบันทึกผ่านความสามารถการค้นหาที่ทรงพลัง. บทแนะนำนี้จะสอนคุณเกี่ยวกับการใช้งาน file และ custom loggers ด้วย GroupDocs.Search, เพื่อเพิ่มความสามารถของแอปพลิเคชันในการติดตามเหตุการณ์และดีบักปัญหา.

## คำตอบด่วน
- **What does “limit log file size” mean?** มันจำกัดขนาดสูงสุดของไฟล์บันทึก, ป้องกันการเติบโตโดยไม่มีการควบคุมบนดิสก์.  
- **Which logger lets you limit log file size?** `FileLogger` ที่มาพร้อมระบบรับพารามิเตอร์ max‑size.  
- **How do I use console logger java?** สร้างอินสแตนซ์ของ `ConsoleLogger` แล้วตั้งค่าให้กับ `IndexSettings`.  
- **Do I need a license for GroupDocs.Search?** สามารถใช้รุ่นทดลองเพื่อประเมิน; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **What’s the first step?** เพิ่ม dependency ของ GroupDocs.Search ลงในโปรเจค Maven ของคุณ.

## limit log file size คืออะไร?
การจำกัดขนาดไฟล์บันทึกหมายถึงการกำหนดค่า logger ให้เมื่อไฟล์ถึงเกณฑ์ที่กำหนดไว้ (เช่น 4 MB) มันจะหยุดเพิ่มขนาดหรือทำการ roll over. สิ่งนี้ทำให้การใช้พื้นที่จัดเก็บของแอปพลิเคชันคาดเดาได้และหลีกเลี่ยงการลดประสิทธิภาพ.

## ทำไมต้องใช้ file และ custom loggers กับ GroupDocs.Search?
- **Auditability:** เก็บบันทึกถาวรของเหตุการณ์การทำดัชนีและการค้นหา.  
- **Debugging:** ระบุปัญหาได้อย่างรวดเร็วโดยการตรวจสอบบันทึกที่กระชับ.  
- **Flexibility:** เลือกใช้ระหว่างไฟล์บันทึกที่คงอยู่และการแสดงผลบนคอนโซลทันที (`use console logger java`).  

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 หรือใหม่กว่า, IDE (IntelliJ IDEA, Eclipse, ฯลฯ).  
- ความรู้พื้นฐานของ Java และ Maven.  

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพิ่มไลบรารีลงในโปรเจคของคุณโดยใช้หนึ่งในวิธีต่อไปนี้.

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
รับรุ่นทดลองหรือซื้อไลเซนส์ผ่าน [licensing page](https://purchase.groupdocs.com/temporary-license/).

## วิธีจำกัดขนาดไฟล์บันทึกด้วย File Logger
ต่อไปนี้เป็นคู่มือขั้นตอนที่แสดงวิธีตั้งค่า `FileLogger` เพื่อให้ไฟล์บันทึกไม่เกินขนาดที่คุณระบุ.

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

### 5️⃣ ทำการค้นหา Query
```java
SearchResult result = index.search(query);
```

**Key point:** ตัวสร้าง `FileLogger` พารามิเตอร์ที่สอง (`4.0`) กำหนดขนาดสูงสุดของไฟล์บันทึกเป็นเมกะไบต์, ตรงกับความต้องการ **limit log file size**.

## วิธีใช้ console logger java
หากคุณต้องการรับฟีดแบ็กทันทีในเทอร์มินัล, ให้เปลี่ยนจาก file logger ไปเป็น console logger.

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

### 4️⃣ เพิ่มเอกสารและทำการค้นหา
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** console logger เหมาะสำหรับการพัฒนาเพราะมันพิมพ์แต่ละบันทึกทันที, ช่วยให้คุณตรวจสอบว่าการทำดัชนีและการค้นหาทำงานตามที่คาดหวัง.

## การประยุกต์ใช้งานจริง
1. **Document Management Systems:** เก็บ audit trail ของทุกเอกสารที่ทำดัชนี.  
2. **Enterprise Search Engines:** ตรวจสอบประสิทธิภาพของ query และอัตราข้อผิดพลาดแบบเรียลไทม์.  
3. **Legal & Compliance Software:** บันทึกคำค้นหาเพื่อการรายงานตามกฎระเบียบ.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Log Size:** ด้วยการจำกัดขนาดไฟล์บันทึก, คุณหลีกเลี่ยงการใช้ดิสก์มากเกินไปซึ่งอาจทำให้แอปพลิเคชันช้าลง.  
- **Asynchronous Logging:** หากต้องการ throughput สูงขึ้น, พิจารณาใส่ logger ลงในคิวแบบ async (อยู่นอกขอบเขตของคู่มือนี้).  
- **Memory Management:** ปล่อยวัตถุ `Index` ขนาดใหญ่เมื่อไม่ต้องการใช้งานแล้วเพื่อให้ footprint ของ JVM ต่ำ.

## ปัญหาทั่วไปและวิธีแก้
- **Log path not accessible:** ตรวจสอบว่าไดเรกทอรีมีอยู่และแอปพลิเคชันมีสิทธิ์เขียน.  
- **Logger not firing:** ตรวจสอบว่าคุณเรียก `settings.setLogger(...)` *ก่อน* สร้างวัตถุ `Index`.  
- **Console output missing:** ยืนยันว่าคุณกำลังรันแอปพลิเคชันในเทอร์มินัลที่แสดง `System.out`.

## คำถามที่พบบ่อย

**Q: What does the second parameter of `FileLogger` control?**  
A: มันกำหนดขนาดสูงสุดของไฟล์บันทึกเป็นเมกะไบต์, ทำให้คุณสามารถ limit log file size ได้.

**Q: Can I combine file and console loggers?**  
A: ได้, โดยสร้าง custom logger ที่ส่งข้อความไปยังทั้งสองปลายทาง.

**Q: How do I add documents to index after the initial creation?**  
A: เรียก `index.add(pathToNewDocs)` ได้ตลอดเวลา; logger จะบันทึกการดำเนินการ.

**Q: Is `ConsoleLogger` thread‑safe?**  
A: มันเขียนโดยตรงไปยัง `System.out` ซึ่ง JVM ทำการซิงโครไนซ์ไว้, ทำให้ปลอดภัยสำหรับการใช้งานส่วนใหญ่.

**Q: Will limiting the log file size affect the amount of information stored?**  
A: เมื่อถึงขีดจำกัดขนาด, รายการใหม่อาจถูกละทิ้งหรือไฟล์อาจ roll over, ขึ้นอยู่กับการทำงานของ logger.

## แหล่งข้อมูล
- [เอกสาร](https://docs.groupdocs.com/search/java/)
- [อ้างอิง API](https://reference.groupdocs.com/search/java/)

---

**อัปเดตล่าสุด:** 2025-12-24  
**ทดสอบด้วย:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs
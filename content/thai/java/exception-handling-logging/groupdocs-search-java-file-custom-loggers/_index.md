---
date: '2026-09-21'
description: เรียนรู้วิธีสร้าง logger, ตั้งค่า max log size, และใช้ console logger
  ใน GroupDocs.Search สำหรับ Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: เรียนรู้วิธีสร้าง logger, ตั้งค่า max log size, และใช้ console logger
  ใน GroupDocs.Search สำหรับ Java. ทำตามคำแนะนำแบบขั้นตอนต่อขั้นตอนและเคล็ดลับการปฏิบัติที่ดีที่สุด.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: วิธีสร้าง logger และจำกัดขนาด log ใน GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: วิธีสร้าง logger และจำกัดขนาด log ใน GroupDocs.Search สำหรับ Java
type: docs
url: /th/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# วิธีสร้าง logger และจำกัดขนาดไฟล์บันทึกใน GroupDocs.Search สำหรับ Java

ในบทแนะนำนี้คุณจะ **สร้าง logger** implementations สำหรับ GroupDocs.Search, ตั้งค่าขนาดไฟล์บันทึกสูงสุด, และสลับระหว่างการบันทึกแบบไฟล์และคอนโซล การจัดการบันทึกที่เหมาะสมช่วยป้องกันดิสก์จากการเต็มในงานทำดัชนีขนาดใหญ่, ปรับปรุงการแก้ปัญหา, และให้ข้อเสนอแนะทันทีขณะพัฒนา เราจะเริ่มด้วยการตั้งค่า Maven, ผ่านการกำหนดค่า logger, และสรุปด้วยการค้นหาง่าย ๆ ที่แสดงการทำงานของ logger

## คำตอบอย่างรวดเร็ว
- **อะไรหมายถึง “limit log file size”?** มันจำกัดขนาดสูงสุดของไฟล์บันทึก, ป้องกันการเติบโตที่ไม่ควบคุมบนดิสก์.  
- **Logger ตัวใดที่ให้คุณจำกัดขนาดไฟล์บันทึก?** `FileLogger` ที่สร้างมาในตัวรับพารามิเตอร์ max‑size.  
- **ฉันจะใช้ console logger java อย่างไร?** สร้างอินสแตนซ์ของ `ConsoleLogger` และตั้งค่าใน `IndexSettings`.  
- **ฉันต้องมีไลเซนส์สำหรับ GroupDocs.Search หรือไม่?** รุ่นทดลองใช้ได้สำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ขั้นตอนแรกคืออะไร?** เพิ่ม dependency ของ GroupDocs.Search ลงในโปรเจค Maven ของคุณ.  

## limit log file size คืออะไร?
การตั้งค่า **limit log file size** บอกให้ logger หยุดเขียนรายการใหม่เมื่อไฟล์ถึงเกณฑ์ที่กำหนด (เช่น 4 MB). เมื่อถึงขีดจำกัด, logger จะละทิ้งข้อความต่อไปหรือทำการ rollover ไปยังไฟล์ใหม่, ทำให้การใช้ดิสก์คาดการณ์ได้.

## ทำไมต้องใช้ file และ custom logger กับ GroupDocs.Search?
File และ custom logger ให้ความสามารถในการตรวจสอบ, เข้าใจการดีบัก, และความยืดหยุ่น ในสภาพแวดล้อมการผลิต, file log ให้บันทึกถาวรของทุกการทำดัชนีและการค้นหา, ส่วน console log ให้ข้อเสนอแนะทันทีระหว่างการพัฒนา Log เหล่านี้ช่วยทีมตรวจสอบประสิทธิภาพ, ติดตามข้อผิดพลาด, และตอบสนองข้อกำหนดการปฏิบัติตามโดยเก็บบันทึกกิจกรรมอย่างละเอียด.

## ข้อกำหนดเบื้องต้น
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 หรือใหม่กว่า, พร้อม IDE เช่น IntelliJ IDEA หรือ Eclipse.  
- ความคุ้นเคยพื้นฐานกับ Maven และการเขียนโปรแกรม Java.  

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพิ่มไลบรารีลงในโปรเจคของคุณโดยใช้วิธีใดวิธีหนึ่งด้านล่าง.

**การตั้งค่า Maven:**  

```text
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
```

**ดาวน์โหลดโดยตรง:**  
ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
รับรุ่นทดลองหรือซื้อไลเซนส์ผ่าน [licensing page](https://purchase.groupdocs.com/temporary-license/).

## วิธีสร้าง custom logger สำหรับ GroupDocs.Search
การสร้าง custom logger ทำได้ง่ายเพราะ GroupDocs.Search พึ่งพา interface `ILogger`. โดยการทำ implement interface นี้—หรือโดยการสืบทอดจาก `FileLogger` หรือ `ConsoleLogger` ที่ให้มา—คุณสามารถเพิ่มพฤติกรรมเพิ่มเติมเช่นการส่งต่อระยะไกลหรือการหมุนเวียนบันทึก คุณยังสามารถเพิ่มตรรกะการเริ่มต้น เช่น การเปิดการเชื่อมต่อเครือข่าย, และทำให้แน่ใจว่าแหล่งทรัพยากรถูกปิดในเมธอด shutdown ของ logger วิธีนี้ทำให้คุณสามารถรวมกับแพลตฟอร์มการตรวจสอบเช่น ELK หรือ Splunk.

### คำจำกัดความ
`ILogger` คือสัญญาการบันทึกหลักใน GroupDocs.Search; คลาสใดที่ทำ implement เมธอด `log(Level, String)` ของมันสามารถเป็น logger ได้.

### ตัวอย่างวิธีการ (ไม่มี code block)
1. สร้างคลาสที่ implements `ILogger`.  
2. Override เมธอด `log` เพื่อเขียนข้อความไปยังปลายทางที่คุณเลือก (ไฟล์, ฐานข้อมูล, endpoint HTTP).  
3. ในการกำหนดค่า index, เรียก `settings.setLogger(new YourCustomLogger())`.  

## วิธีจำกัดขนาดไฟล์บันทึกด้วย File Logger
`FileLogger` เขียนรายการบันทึกลงไฟล์บนดิสก์และรับอาร์กิวเมนต์ขนาดสูงสุด โดยการระบุขีดจำกัดขนาด, logger จะหยุดเพิ่มรายการใหม่โดยอัตโนมัติหรือสร้างไฟล์ใหม่เมื่อถึงเกณฑ์, ป้องกันการเติบโตของดิสก์ที่ไม่ควบคุม พฤติกรรมนี้ทำให้การบันทึกไม่รบกวนประสิทธิภาพการทำดัชนีขณะยังคงบันทึกเหตุการณ์อย่างกระชับ.

### คำจำกัดความ
`FileLogger` คือ logger ที่สร้างมาในตัวซึ่งบันทึกข้อความลงไฟล์ข้อความและรองรับขนาดไฟล์สูงสุดที่กำหนดได้.

### คู่มือขั้นตอน
1️⃣ **นำเข้าแพ็คเกจที่จำเป็น**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **ตั้งค่า index settings ด้วย File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **สร้างหรือโหลด index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **เพิ่มเอกสารลงใน index**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **ทำการค้นหา**  
```text
```java
SearchResult result = index.search(query);
```
```

**จุดสำคัญ:** อาร์กิวเมนต์ที่สองของคอนสตรัคเตอร์ `FileLogger` (`4.0`) กำหนด **set max log size** เป็นเมกะไบต์, ตรงกับความต้องการ **limit log file size**.

## วิธีใช้ console logger java
เมื่อคุณต้องการมองเห็นเหตุการณ์บันทึกแบบทันที, `ConsoleLogger` จะเขียนแต่ละข้อความไปยัง `System.out`. Logger นี้มีน้ำหนักเบาและ thread‑safe, ทำให้เหมาะกับการพัฒนาและดีบัก มันให้ข้อเสนอแนะทันทีเกี่ยวกับความคืบหน้าการทำดัชนี, คำค้นหา, และเงื่อนไขข้อผิดพลาดโดยไม่ต้องใช้ I/O ของไฟล์, ซึ่งสามารถเร่งการทดสอบแบบวนซ้ำ.

### คำจำกัดความ
`ConsoleLogger` คือ logger ที่น้ำหนักเบาซึ่งส่งออกรายการบันทึกไปยังสตรีมคอนโซลมาตรฐาน, ทำให้เหมาะสำหรับเซสชันการดีบัก.

### ขั้นตอนการกำหนดค่า
1️⃣ **นำเข้า console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **ตั้งค่า index settings ด้วย Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **สร้างหรือโหลด index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **เพิ่มเอกสารและทำการค้นหา**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**เคล็ดลับ:** console logger เหมาะในระหว่างการพัฒนาเพราะมันพิมพ์แต่ละรายการบันทึกทันที, ช่วยให้คุณตรวจสอบว่าการทำดัชนีและการค้นหาทำงานตามที่คาดหวัง.

## การประยุกต์ใช้งานจริง
1. ระบบจัดการเอกสาร: เก็บบันทึกการตรวจสอบของทุกเอกสารที่ทำดัชนี, ตอบสนองข้อกำหนดการปฏิบัติตาม.  
2. เครื่องมือค้นหาองค์กร: ตรวจสอบประสิทธิภาพของคำค้นและอัตราข้อผิดพลาดแบบเรียลไทม์, ช่วยให้ตรวจสอบการปฏิบัติตาม SLA อย่างรวดเร็ว.  
3. ซอฟต์แวร์ด้านกฎหมายและการปฏิบัติตาม: บันทึกคำค้นและเวลาที่ทำการค้นหาเพื่อการรายงานตามกฎระเบียบ, โดยบันทึกจะถูกเก็บตามระยะเวลาที่กำหนด.  

## พิจารณาด้านประสิทธิภาพ
- **ขนาดบันทึก:** ด้วย **set max log size**, คุณหลีกเลี่ยงการใช้ดิสก์เกินที่อาจทำให้ garbage collector ของ JVM ช้าลง.  
- **การบันทึกแบบอะซิงโครนัส:** สำหรับสถานการณ์ที่มี throughput สูง, ห่อ logger ของคุณในคิวแบบอะซิงโครนัสเพื่อแยก I/O ออกจากเธรดการทำดัชนี (การทำงานนี้อยู่นอกขอบเขตของคู่มือนี้).  
- **การจัดการหน่วยความจำ:** ปล่อยอ็อบเจกต์ `Index` ขนาดใหญ่ด้วย `index.close()` เมื่อไม่ต้องการแล้วเพื่อรักษาขนาด JVM ให้ต่ำ.  

## ปัญหาทั่วไปและวิธีแก้
- **เส้นทางบันทึกไม่สามารถเข้าถึงได้:** ตรวจสอบว่าไดเรกทอรีมีอยู่และแอปพลิเคชันมีสิทธิ์เขียนสำหรับบัญชีผู้ใช้ที่รัน JVM.  
- **Logger ไม่ทำงาน:** ตรวจสอบว่าคุณเรียก `settings.setLogger(...)` *ก่อน* สร้างอ็อบเจกต์ `Index`; มิฉะนั้น logger เริ่มต้นจะถูกใช้.  
- **ไม่มีการแสดงผลบนคอนโซล:** ยืนยันว่าคุณรันแอปพลิเคชันในเทอร์มินัลที่แสดง `System.out`, และไม่มีเฟรมเวิร์กบันทึก (เช่น SLF4J) ดักจับเอาต์พุต.  

## คำถามที่พบบ่อย

**ถาม: พารามิเตอร์ที่สองของ `FileLogger` ควบคุมอะไร?**  
A: มันกำหนดขนาดสูงสุดของไฟล์บันทึกเป็นเมกะไบต์, ทำให้คุณสามารถ **set max log size** และป้องกันการเติบโตที่ไม่ควบคุม.

**ถาม: ฉันสามารถรวม file และ console logger ได้หรือไม่?**  
A: ได้. สร้าง custom logger ที่ส่งต่อแต่ละการเรียก `log` ไปยังทั้ง `FileLogger` และ `ConsoleLogger`, แล้วลงทะเบียน logger ประกอบนั้นกับ `IndexSettings`.

**ถาม: ฉันจะเพิ่มเอกสารลงใน index หลังจากการสร้างครั้งแรกอย่างไร?**  
A: เรียก `index.add(pathToNewDocs)` ได้ตลอดเวลา; logger ที่กำหนดจะบันทึกการเพิ่มโดยอัตโนมัติ.

**ถาม: `ConsoleLogger` ปลอดภัยต่อเธรดหรือไม่?**  
A: มันเขียนโดยตรงไปยัง `System.out`, ซึ่ง JVM ทำการซิงโครไนซ์ภายใน, ทำให้ปลอดภัยสำหรับการใช้งานหลายเธรดทั่วไป.

**ถาม: การจำกัดขนาดไฟล์บันทึกจะส่งผลต่อปริมาณข้อมูลที่บันทึกหรือไม่?**  
A: เมื่อถึงขีดจำกัดขนาด, รายการใหม่จะถูกละทิ้งหรือ logger จะทำการ rollover ไปยังไฟล์ใหม่, ขึ้นอยู่กับการทำงานที่คุณเลือก.

## แหล่งข้อมูล
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**อัปเดตล่าสุด:** 2026-09-21  
**ทดสอบกับ:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs  

---

## บทแนะนำที่เกี่ยวข้อง

- [วิธีการทำ Logging - บทแนะนำการจัดการข้อยกเว้นและ Logging สำหรับ GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [การทำ Asynchronous Logging ใน Java กับ GroupDocs.Search – คู่มือ Custom Logger](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [สร้าง Search Index Java – บทแนะนำ GroupDocs.Search](/search/java/indexing/)
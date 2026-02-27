---
date: '2026-01-11'
description: เรียนรู้วิธีใช้ GroupDocs for Java OCR indexing ร่วมกับ Aspose.OCR เพื่อเปิดใช้งานความสามารถการค้นหาเอกสารที่ทรงพลังในไฟล์
  PDF, รูปภาพ และไฟล์สแกน.
keywords:
- Java OCR indexing
- document searchability
- OCR with GroupDocs
title: วิธีใช้ GroupDocs สำหรับ Java ในการทำดัชนี OCR ด้วย Aspose
type: docs
url: /th/java/ocr-image-search/java-ocr-indexing-aspose-groupdocs-search/
weight: 1
---

# วิธีใช้ GroupDocs สำหรับ OCR Indexing ด้วย Java และ Aspose

ในคู่มือนี้คุณจะได้ค้นพบ **วิธีใช้ GroupDocs** เพื่อเพิ่มการค้นหาที่ขับเคลื่อนด้วย OCR ให้กับแอปพลิเคชัน Java ของคุณ โดยการผสานรวม GroupDocs.Search กับ Aspose.OCR คุณสามารถแปลงเนื้อหาที่เป็นรูปภาพให้เป็นข้อความที่สามารถค้นหาได้ ทำให้ระบบจัดการเอกสารมีประโยชน์มากยิ่งขึ้น เราจะอธิบายขั้นตอนการตั้งค่า การทำดัชนี การค้นหา และการผสานรวม OCR แบบกำหนดเอง พร้อมตัวอย่างที่ชัดเจนเป็นขั้นตอน

## Quick Answers
- **ไลบรารีใดที่ให้การทำดัชนี OCR?** GroupDocs.Search คู่กับ Aspose.OCR.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 หรือสูงกว่า.  
- **ต้องการไลเซนส์หรือไม่?** มีการทดลองใช้ฟรี; ต้องมีไลเซนส์แบบชำระเงินสำหรับการใช้งานในผลิตภัณฑ์.  
- **สามารถทำดัชนีรูปภาพแยกและฝังได้หรือไม่?** ได้, เปิดใช้งานทั้งสองตัวเลือกใน `IndexingOptions`.  
- **รองรับการทำงานแบบหลายเธรดหรือไม่?** ได้, คุณสามารถทำการทำดัชนีแบบขนานสำหรับชุดข้อมูลขนาดใหญ่.

## OCR Indexing กับ GroupDocs คืออะไร?
OCR indexing จะสกัดข้อความจากรูปภาพ (รวมถึง PDF ที่สแกน) แล้วเก็บไว้ในดัชนีที่สามารถค้นหาได้ GroupDocs.Search ดูแลการทำดัชนีและการดำเนินการค้นหา ส่วน Aspose.OCR ทำการจดจำอักขระจริง

## ทำไมต้องใช้ GroupDocs สำหรับ OCR indexing ด้วย Java?
- **ความแม่นยำสูง** ด้วยเครื่องมือ OCR ขั้นสูงของ Aspose.  
- **การผสานรวมกับ Java อย่างไร้รอยต่อ** ผ่าน Maven หรือ JAR โดยตรง.  
- **การกำหนดค่าที่ยืดหยุ่น** สำหรับรูปภาพแยกหรือฝัง.  
- **ประสิทธิภาพที่ขยายได้** ด้วยการทำงานหลายเธรดและการปรับแต่งหน่วยความจำ.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search** ≥ 25.4  
- **Aspose.OCR** (รุ่นล่าสุด)  
- JDK 8+ และ IDE (IntelliJ, Eclipse, NetBeans)  
- ความรู้พื้นฐาน Java; Maven มีประโยชน์แต่ไม่จำเป็น

## การตั้งค่า GroupDocs.Search สำหรับ Java
### ใช้ Maven
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดของ GroupDocs.Search สำหรับ Java ได้จาก [GroupDocs releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
- **Free Trial** – ทดลองใช้ทุกฟีเจอร์โดยไม่มีค่าใช้จ่าย.  
- **Temporary License** – ระยะเวลาทดสอบต่อเนื่อง.  
- **Purchase** – จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

### การเริ่มต้นและตั้งค่าเบื้องต้น
สร้างโฟลเดอร์สำหรับดัชนีและเริ่มต้นอ็อบเจกต์ `Index`:

```java
import com.groupdocs.search.Index;
// Specify the directory where the index will be stored.
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
// Create an instance of Index class at the specified location.
Index index = new Index(indexFolder);
```

## วิธีใช้ GroupDocs สำหรับ OCR Indexing
### การสร้างดัชนี
ขั้นแรกตั้งค่าโฟลเดอร์ที่จะเก็บไฟล์ดัชนี:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/OcrSupport";
Index index = new Index(indexFolder);
```

### การตั้งค่า OCR Indexing Options
เปิดใช้งาน OCR สำหรับรูปภาพแยกและฝัง พร้อมเชื่อมต่อ OCR แบบกำหนดเอง:

```java
import com.groupdocs.search.options.IndexingOptions;
IndexingOptions options = new IndexingOptions();
options.getOcrIndexingOptions().setEnabledForSeparateImages(true);
options.getOcrIndexingOptions().setEnabledForEmbeddedImages(true);
// Set a custom OCR connector.
options.getOcrIndexingOptions().setOcrConnector(new OcrConnector());
```

### การทำดัชนีเอกสาร
เพิ่มเอกสารต้นทางของคุณ (PDF, ไฟล์ Word, รูปภาพ ฯลฯ) ลงในดัชนี:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder, options);
```

### การค้นหาในดัชนี
ดำเนินการค้นหาด้วย query ต่อเนื้อหาที่ทำดัชนีแล้ว:

```java
import com.groupdocs.search.results.SearchResult;
String query = "water";
SearchResult result = index.search(query);
```

### การทำ OCR Connector
ใช้ Aspose.OCR เพื่อจดจำข้อความจากรูปภาพ. Implement อินเทอร์เฟซ `IOcrConnector` ตามตัวอย่าง:

```java
import com.groupdocs.search.options.IOcrConnector;
import com.groupdocs.search.options.OcrContext;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import com.aspose.ocr.AsposeOCR;

public class OcrConnector implements IOcrConnector {
    @Override
    public final String recognize(OcrContext context) {
        if (null == context.getImageLocation()) {
            throw new RuntimeException("The image type is not supported: " + context.getImageLocation());
        }
        
        BufferedImage image = ImageIO.read(context.getImageLocation().toFile());
        AsposeOCR api = new AsposeOCR();
        String text = api.RecognizePage(image);
        return text;
    }
}
```

## การประยุกต์ใช้งานจริง
1. **Document Management Systems** – การดึงเอกสารที่มีรูปภาพสแกนอย่างรวดเร็ว.  
2. **Archival Retrieval** – ค้นหารายการบันทึกประวัติในคลังข้อมูลขนาดใหญ่.  
3. **Legal Document Analysis** – ค้นหาสัญญาและหลักฐานที่มีลายเซ็นหรือแผนภาพสแกน.  
4. **Medical Records Search** – ทำดัชนีแบบฟอร์มผู้ป่วย, ผลการตรวจแลบ, และหมายเหตุบนภาพ X‑ray.

## การพิจารณาประสิทธิภาพ
- **ขนาดดัชนี** – ลบเมตาดาต้าที่ไม่จำเป็นเพื่อให้ดัชนีมีขนาดเล็ก.  
- **Multi‑Threading** – ประมวลผลชุดข้อมูลขนาดใหญ่แบบขนานเพื่อเร่งความเร็วการทำดัชนี.  
- **การจัดการหน่วยความจำ** – ติดตาม heap ของ JVM เมื่อจัดการรูปภาพความละเอียดสูง.

## ปัญหาที่พบบ่อยและวิธีแก้ไข
- **License Errors** – ตรวจสอบให้แน่ใจว่าไฟล์ไลเซนส์ที่ถูกต้องอยู่ในไดเรกทอรีทำงานของแอปพลิเคชัน.  
- **Missing Images** – ยืนยันว่าเส้นทางรูปภาพเข้าถึงได้และเป็นฟอร์แมตที่รองรับ (PNG, JPEG, BMP).  
- **Out‑Of‑Memory** – เพิ่มขนาด heap ของ JVM (`-Xmx`) หรือทำการประมวลผลเอกสารเป็นชุดเล็กลง.

## คำถามที่พบบ่อย
**Q: จะจัดการกับปัญหาไลเซนส์ของ GroupDocs.Search อย่างไร?**  
A: รับไลเซนส์ชั่วคราวจาก [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) เพื่อเปิดใช้งานฟีเจอร์ทั้งหมด.

**Q: วิธีที่ดีที่สุดในการทำดัชนีเอกสารขนาดใหญ่คืออะไร?**  
A: ใช้การทำงานหลายเธรดและการประมวลผลเป็นชุดเพื่อเพิ่มประสิทธิภาพและลดภาระหน่วยความจำ.

**Q: สามารถปรับแต่งการตั้งค่า OCR เพิ่มเติมใน GroupDocs.Search ได้หรือไม่?**  
A: ได้, `IndexingOptions` ให้คุณปรับจูนพฤติกรรม OCR เช่น การเลือกภาษาและการเตรียมรูปภาพล่วงหน้า.

**Q: มีเคล็ดลับการแก้ไขปัญหาที่พบบ่อยเมื่อใช้ GroupDocs.Search อย่างไร?**  
A: ตรวจสอบเส้นทางไดเรกทอรีอีกครั้ง, ยืนยันว่าขึ้นต่อ dependencies ทั้งหมดอยู่, และตรวจสอบ log เพื่อหาไฟล์ที่หายไป.

**Q: จะผสานรวม Aspose.OCR กับแอปพลิเคชัน Java ที่มีอยู่ได้อย่างไร?**  
A: Implement อินเทอร์เฟซ `IOcrConnector` ตามที่แสดงด้านบน, โดยให้แน่ใจว่าจัดการอินพุตของรูปภาพอย่างถูกต้อง.

## แหล่งข้อมูล
- [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**อัพเดตล่าสุด:** 2026-01-11  
**ทดสอบกับ:** GroupDocs.Search 25.4, Aspose.OCR รุ่นล่าสุด  
**ผู้เขียน:** GroupDocs
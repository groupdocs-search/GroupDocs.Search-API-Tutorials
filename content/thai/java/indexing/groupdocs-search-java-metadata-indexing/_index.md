---
date: '2026-01-06'
description: เรียนรู้วิธีเพิ่มเอกสารเข้าสู่ดัชนีและค้นหาเอกสารโดยใช้เมตาดาต้าด้วย
  GroupDocs.Search Java. เชี่ยวชาญการตั้งค่าดัชนี, สร้างดัชนี, เพิ่มเอกสาร, และดำเนินการค้นหาที่แม่นยำ.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: วิธีเพิ่มเอกสารลงในดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search
type: docs
url: /th/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# วิธีเพิ่มเอกสารลงในดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search

ในแอปพลิเคชันสมัยใหม่ การ **add documents to index** อย่างรวดเร็วและเชื่อถือได้เป็นสิ่งสำคัญเพื่อมอบประสบการณ์การค้นหาที่เร็วขึ้น ไม่ว่าคุณจะสร้างคลังเอกสารด้านกฎหมาย ฐานความรู้การสนับสนุนลูกค้า หรือพอร์ทัลเอกสารภายใน การใช้เมตาดาต้าช่วยให้คุณสามารถ **search documents by metadata** เช่น ผู้เขียน ชื่อเรื่อง หรือแท็กที่กำหนดเอง คู่มือฉบับนี้จะพาคุณผ่านกระบวนการทั้งหมด — ตั้งค่าการกำหนดดัชนี สร้างดัชนีที่เน้นเมตาดาต้า เพิ่มไฟล์ของคุณ และรันการค้นหาที่มีประสิทธิภาพ — ทั้งหมดนี้ด้วย GroupDocs.Search สำหรับ Java.

## คำตอบสั้น
- **วัตถุประสงค์หลักของการทำดัชนีเมตาดาต้าคืออะไร?** ช่วยให้การค้นหาอย่างรวดเร็วโดยอิงคุณสมบัติของเอกสารแทนการค้นหาข้อความเต็ม.  
- **วิธีใดที่ใช้เพิ่มไฟล์ลงในดัชนี?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **ฉันสามารถค้นหาด้วยฟิลด์เมตาดาต้ากำหนดเองได้หรือไม่?** ได้, เมื่อฟิลด์ถูกทำดัชนีแล้วคุณสามารถสอบถามโดยตรง.  
- **ฉันต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ทดลองชั่วคราวเพียงพอสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ต้องการเวอร์ชัน Java ใด?** แนะนำให้ใช้ JDK 8 หรือสูงกว่า.

## ดัชนีเมตาดาต้าใน GroupDocs.Search คืออะไร?
การทำดัชนีเมตาดาต้า จะสกัดและเก็บคุณลักษณะของเอกสาร (เช่น ผู้เขียน วันที่สร้าง แท็กกำหนดเอง) ในโครงสร้างที่สามารถค้นหาได้ เมื่อคุณ **add documents to index** เอนจินจะบันทึกคุณลักษณะเหล่านี้ ทำให้คุณสามารถรันคำค้นที่แม่นยำเช่น “ค้นหา PDF ทั้งหมดที่เขียนโดย *John Doe*”.

## ทำไมต้องใช้ GroupDocs.Search สำหรับการทำดัชนีเมตาดาต้า?
- **Performance:** การค้นหาเมตาดาต้าเป็นการทำงานที่เบาและให้ผลลัพธ์ในระดับมิลลิวินาที.  
- **Flexibility:** รองรับรูปแบบไฟล์หลากหลาย (PDF, DOCX, PPT, ฯลฯ).  
- **Scalability:** จัดการกับเอกสารหลายล้านรายการด้วยการใช้หน่วยความจำน้อย.  

## ข้อกำหนดเบื้องต้น
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 หรือใหม่กว่า ติดตั้งและกำหนดค่าแล้ว.  
- มีความคุ้นเคยพื้นฐานกับ Java และ Maven.  

## การตั้งค่า GroupDocs.Search สำหรับ Java

### คำแนะนำการติดตั้ง
เพิ่มรีโพซิทอรีของ GroupDocs และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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

คุณยังสามารถดาวน์โหลดไบนารีล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
เพื่อรับไลเซนส์ชั่วคราวสำหรับการทดสอบ:

1. เข้าไปที่เว็บไซต์ของ GroupDocs และไปที่ส่วน **Purchase**.  
2. เลือกแผน **temporary license** ที่ตรงกับความต้องการการประเมินของคุณ.  

## การดำเนินการแบบขั้นตอน

### ฟีเจอร์ 1: การกำหนดค่าการตั้งค่าดัชนี
กำหนดค่าดัชนีให้เน้นเมตาดาต้า:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` บอกให้เอนจินให้ความสำคัญกับเมตาดาต้าเหนือเนื้อหาข้อความเต็ม.

### ฟีเจอร์ 2: การสร้างดัชนีในโฟลเดอร์ที่ระบุ
สร้างไดเรกทอรีดัชนีจริงที่เก็บเมตาดาต้าทั้งหมด:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

แทนที่ `YOUR_DOCUMENT_DIRECTORY` ด้วยเส้นทางที่ตรงกับโครงสร้างโปรเจกต์ของคุณ.

### ฟีเจอร์ 3: วิธีเพิ่มเอกสารลงในดัชนี
เมื่อดัชนีมีอยู่แล้ว คุณสามารถ **add documents to index** เพื่อให้สามารถค้นหาได้:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tips:**  
- ตรวจสอบว่าเส้นทางโฟลเดอร์ถูกต้องและแอปพลิเคชันมีสิทธิ์อ่าน.  
- GroupDocs.Search จะสกัดเมตาดาต้าที่รองรับจากแต่ละไฟล์โดยอัตโนมัติ.

### ฟีเจอร์ 4: การค้นหาเอกสารโดยเมตาดาต้า
รันคำค้นที่มุ่งเป้าไปที่ฟิลด์เมตาดาต้า เช่น การค้นหาเอกสารที่ภาษาคืออังกฤษ:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` จะค้นหาผ่านเมตาดาต้าที่ทำดัชนีและคืนเอกสารที่ตรงกัน.

## การประยุกต์ใช้งานจริง
1. **Enterprise Document Management:** ดึงสัญญาตามวันที่สัญญาหรือชื่อผู้ลงนาม.  
2. **Digital Library Catalogs:** ให้ผู้ใช้เรียกดูหนังสือตามประเภท ปีการตีพิมพ์ หรือผู้เขียน.  
3. **CRM Systems:** ค้นหาไฟล์ลูกค้าอย่างรวดเร็วโดยใช้เมตาดาต้ากำหนดเองเช่นรหัสลูกค้าหรือภูมิภาค.  

## การพิจารณาด้านประสิทธิภาพ
- **Incremental Updates:** ใช้ `index.addOrUpdate()` สำหรับไฟล์ใหม่หรือที่เปลี่ยนแปลงแทนการสร้างดัชนีใหม่ทั้งหมด.  
- **Memory Tuning:** ปรับขนาด heap ของ JVM (`-Xmx`) ตามปริมาณเมตาดาต้าที่ทำดัชนี.  
- **Optimized Storage:** เรียก `index.optimize()` อย่างสม่ำเสมอเพื่อบีบอัดดัชนีและเพิ่มความเร็วของการค้นหา.

## ปัญหาที่พบบ่อยและวิธีแก้

| Issue | Solution |
|-------|----------|
| **ไม่มีผลลัพธ์ที่ส่งกลับ** | ยืนยันว่าฟิลด์เมตาดาต้าที่คาดหวังมีอยู่จริงในไฟล์ต้นฉบับ. |
| **ข้อผิดพลาดด้านสิทธิ์** | ตรวจสอบให้แน่ใจว่ากระบวนการ Java มีสิทธิ์อ่านทั้งโฟลเดอร์เอกสารและไดเรกทอรีดัชนี. |
| **ข้อผิดพลาด Out‑of‑memory** | เพิ่มขนาด heap ของ JVM หรือทำการ batch การทำ `add` เพื่อประมวลผลไฟล์เป็นกลุ่มเล็กลง. |

## คำถามที่พบบ่อย

**Q: ดัชนีเมตาดาต้าคืออะไร?**  
A: ดัชนีเมตาดาต้าจะเก็บคุณลักษณะของเอกสาร (ผู้เขียน, ชื่อเรื่อง, แท็กกำหนดเอง) ในโครงสร้างที่สามารถค้นหาได้ ทำให้การค้นหาอย่างรวดเร็วโดยไม่ต้องสแกนข้อความเต็ม.

**Q: ฉันจะได้รับไลเซนส์ชั่วคราวได้อย่างไร?**  
A: ไปที่หน้าการซื้อของ GroupDocs และทำตามขั้นตอนเพื่อรับไลเซนส์ทดลอง.

**Q: ฉันสามารถทำดัชนี PDF ด้วยการตั้งค่านี้ได้หรือไม่?**  
A: ได้, GroupDocs.Search รองรับ PDF, DOCX, PPT และรูปแบบอื่น ๆ อีกหลายประเภท.

**Q: ปัญหาที่พบบ่อยเมื่อเพิ่มเอกสารคืออะไร?**  
A: ตรวจสอบว่าเส้นทางไฟล์ถูกต้องและแอปพลิเคชันมีสิทธิ์อ่านโฟลเดอร์เหล่านั้น.

**Q: ฉันจะเพิ่มประสิทธิภาพการค้นหาอย่างไร?**  
A: อัปเดตดัชนีเป็นประจำ ใช้การเพิ่มแบบ incremental และปรับตั้งค่าหน่วยความจำของ JVM.

## แหล่งข้อมูล

- **Documentation:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-01-06  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs
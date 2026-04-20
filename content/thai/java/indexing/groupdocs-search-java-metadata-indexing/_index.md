---
date: '2026-03-17'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและค้นหาเอกสารตามเมตาดาต้าด้วย GroupDocs.Search
  Java. เชี่ยวชาญการตั้งค่าดัชนี, สร้างดัชนี, เพิ่มเอกสาร, และดำเนินการค้นหาที่แม่นยำ.
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

การเพิ่มเอกสารลงในดัชนีอย่างรวดเร็วและเชื่อถือได้เป็นหัวใจของแอปพลิเคชันที่ขับเคลื่อนด้วยการค้นหาในยุคสมัยใหม่ ไม่ว่าคุณจะสร้างคลังเอกสารทางกฎหมาย ฐานความรู้การสนับสนุนลูกค้า หรือพอร์ทัลเอกสารภายใน **metadata indexing** จะช่วยให้คุณ *ค้นหาเอกสารโดยใช้เมตาดาต้า* เช่น ผู้เขียน, ชื่อเรื่อง หรือแท็กที่กำหนดเอง ในบทเรียนนี้คุณจะได้เรียนรู้วิธีกำหนดค่าการตั้งค่าดัชนี, สร้างดัชนีที่เน้นเมตาดาต้า, เพิ่มไฟล์ของคุณ, และรันการค้นหาที่แม่นยำ—all with GroupDocs.Search for Java.

## คำตอบสั้น ๆ
- **วัตถุประสงค์หลักของ metadata indexing คืออะไร?** ช่วยให้การค้นหาเร็วขึ้นโดยอิงคุณสมบัติของเอกสารแทนการค้นหาข้อความเต็ม.  
- **เมธอดใดที่ใช้เพิ่มไฟล์ลงในดัชนี?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **ฉันสามารถค้นหาโดยฟิลด์เมตาดาต้ากำหนดเองได้หรือไม่?** ได้, เมื่อฟิลด์ถูกทำดัชนีแล้วคุณสามารถคิวรีโดยตรง.  
- **ต้องใช้ไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ทดลองชั่วคราวเพียงพอสำหรับการประเมิน; ต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ต้องใช้เวอร์ชัน Java ใด?** แนะนำให้ใช้ JDK 8 หรือสูงกว่า.

## metadata indexing ใน GroupDocs.Search คืออะไร?
metadata indexing จะสกัดและจัดเก็บคุณลักษณะของเอกสาร (เช่น ผู้เขียน, วันที่สร้าง, แท็กกำหนดเอง) ในโครงสร้างที่สามารถค้นหาได้ เมื่อคุณ **add documents to index** เngine จะบันทึกคุณลักษณะเหล่านี้ ทำให้คุณสามารถรันคิวรีที่แม่นยำเช่น “ค้นหา PDF ทั้งหมดที่เขียนโดย *John Doe*” หรือ “search pdf by author”.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ metadata indexing?
- **Performance:** การค้นหาเมตาดาต้าใช้ทรัพยากรน้อยและให้ผลลัพธ์ในระดับมิลลิวินาที.  
- **Flexibility:** รองรับรูปแบบไฟล์หลากหลาย (PDF, DOCX, PPT, ฯลฯ).  
- **Scalability:** จัดการกับเอกสารหลายล้านรายการโดยใช้หน่วยความจำน้อย.

## ข้อกำหนดเบื้องต้น
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 หรือใหม่กว่าได้ติดตั้งและกำหนดค่าแล้ว.  
- มีความคุ้นเคยพื้นฐานกับ Java และ Maven.

## การตั้งค่า GroupDocs.Search for Java

### คำแนะนำการติดตั้ง
เพิ่มรีโพซิทอรีของ GroupDocs และ dependency ลงใน `pom.xml` ของคุณ:

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

คุณสามารถดาวน์โหลดไบนารีล่าสุดได้โดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การขอรับไลเซนส์
เพื่อรับไลเซนส์ชั่วคราวสำหรับการทดสอบ:

1. เข้าไปที่เว็บไซต์ GroupDocs แล้วไปที่ส่วน **Purchase**.  
2. เลือกแผน **temporary license** ที่ตรงกับความต้องการการประเมินของคุณ.

## การดำเนินการแบบขั้นตอน

### Feature 1: การกำหนดค่า Index Settings
กำหนดค่าดัชนีให้เน้นที่เมตาดาต้า:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` บอก engine ให้ให้ความสำคัญกับเมตาดาต้าเหนือเนื้อหาข้อความเต็ม.

### Feature 2: การสร้างดัชนีในโฟลเดอร์ที่ระบุ
สร้างโฟลเดอร์ดัชนีจริงที่ใช้เก็บเมตาดาต้าทั้งหมด:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

แทนที่ `YOUR_DOCUMENT_DIRECTORY` ด้วยพาธที่สอดคล้องกับโครงสร้างโปรเจกต์ของคุณ.

### Feature 3: วิธีเพิ่มเอกสารลงในดัชนี
เมื่อดัชนีมีอยู่แล้ว คุณสามารถ **add documents to index** เพื่อให้เอกสารเหล่านั้นสามารถค้นหาได้:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**เคล็ดลับ:**  
- ตรวจสอบให้แน่ใจว่าพาธของโฟลเดอร์ถูกต้องและแอปพลิเคชันมีสิทธิ์อ่าน.  
- GroupDocs.Search จะสกัดเมตาดาต้าที่รองรับจากแต่ละไฟล์โดยอัตโนมัติ.

### Feature 4: การค้นหาเอกสารโดยเมตาดาต้า
รันคิวรีที่มุ่งเป้าไปที่ฟิลด์เมตาดาต้า, ตัวอย่างเช่นค้นหาเอกสารที่ภาษาคือ English:

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
- คุณยังสามารถ **search pdf by author** ได้โดยใส่ชื่อผู้เขียนเป็นสตริงของคิวรี.

## การประยุกต์ใช้งานจริง
1. **Enterprise Document Management:** ดึงสัญญาตามวันที่สัญญาหรือชื่อผู้ลงนาม.  
2. **Digital Library Catalogs:** ให้ผู้ใช้เรียกดูหนังสือตามประเภท, ปีตีพิมพ์, หรือผู้เขียน.  
3. **CRM Systems:** ค้นหาไฟล์ลูกค้าอย่างรวดเร็วโดยใช้เมตาดาต้ากำหนดเองเช่นรหัสลูกค้าหรือภูมิภาค.

## เคล็ดลับและแนวทางปฏิบัติที่ดีที่สุด
- **Incremental Updates:** ใช้ `index.addOrUpdate()` สำหรับไฟล์ใหม่หรือไฟล์ที่เปลี่ยนแปลงแทนการสร้างดัชนีใหม่ทั้งหมด.  
- **Batch Processing:** เมื่อจัดการกับไฟล์หลายพันไฟล์ ให้เพิ่มไฟล์เป็นชุดเล็ก ๆ เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- **Metadata Validation:** ตรวจสอบให้แน่ใจว่าเอกสารต้นทางมีเมตาดาต้าที่คุณต้องการคิวรี (เช่นฟิลด์ผู้เขียนใน PDF).

## พิจารณาด้านประสิทธิภาพ
- **Memory Tuning:** ปรับขนาด heap ของ JVM (`-Xmx`) ตามปริมาณเมตาดาต้าที่ทำดัชนี.  
- **Optimized Storage:** เรียก `index.optimize()` เป็นระยะเพื่อบีบอัดดัชนีและเพิ่มความเร็วของคิวรี.

## ปัญหาทั่วไปและวิธีแก้
| Issue | Solution |
|-------|----------|
| **No results returned** | ยืนยันว่าฟิลด์เมตาดาต้าที่คุณคาดหวังมีอยู่จริงในไฟล์ต้นทาง. |
| **Permission errors** | ตรวจสอบให้แน่ใจว่าโปรเซส Java มีสิทธิ์อ่านทั้งโฟลเดอร์เอกสารและโฟลเดอร์ดัชนี. |
| **Out‑of‑memory errors** | เพิ่มขนาด heap ของ JVM หรือทำการ batch `add` เพื่อประมวลผลไฟล์เป็นกลุ่มย่อย. |

## คำถามที่พบบ่อย

**Q: metadata indexing คืออะไร?**  
A: metadata indexing จะเก็บคุณลักษณะของเอกสาร (author, title, custom tags) ในโครงสร้างที่สามารถค้นหาได้, ทำให้ค้นหาได้เร็วโดยไม่ต้องสแกนข้อความเต็ม.

**Q: จะขอรับไลเซนส์ชั่วคราวได้อย่างไร?**  
A: เข้าไปที่หน้าการซื้อของ GroupDocs แล้วทำตามขั้นตอนเพื่อรับไลเซนส์ทดลอง.

**Q: สามารถทำดัชนี PDF ด้วยการตั้งค่านี้ได้หรือไม่?**  
A: ได้, GroupDocs.Search รองรับ PDF, DOCX, PPT และรูปแบบอื่น ๆ อีกหลายประเภท.

**Q: ปัญหาที่พบบ่อยเมื่อเพิ่มเอกสารคืออะไร?**  
A: ตรวจสอบพาธไฟล์ให้ถูกต้องและให้แอปพลิเคชันมีสิทธิ์อ่านโฟลเดอร์ที่เกี่ยวข้อง.

**Q: จะปรับประสิทธิภาพการค้นหาอย่างไร?**  
A: อัปเดตดัชนีเป็นประจำ, ใช้การเพิ่มแบบ incremental, และปรับตั้งค่าหน่วยความจำของ JVM.

## แหล่งข้อมูล

- **Documentation:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs
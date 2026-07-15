---
date: '2026-05-12'
description: 'เรียนรู้ java full text search กับ GroupDocs.Search: เพิ่มเอกสารลงในดัชนี,
  กำหนดค่าตัวเลือกการรวม, และยกเลิกการดำเนินการรวม. เหมาะสำหรับโซลูชันการจัดการเอกสาร
  java.'
keywords:
- java full text search
- document management java
- GroupDocs.Search merging
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: 'Learn java full text search with GroupDocs.Search: add documents to
    index, configure merge options, and cancel merge operation. Ideal for document
    management java solutions.'
  headline: java full text search – add docs & merge with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It tells GroupDocs.Search to scan a folder, extract searchable tokens,
      and store metadata for each file.
    question: What does “add documents to index” mean?
  - answer: Yes—use the `Cancellation` object to abort a merge after a configurable
      timeout.
    question: Can I stop a long merge?
  - answer: A free trial or temporary license works for testing; a commercial license
      unlocks full features.
    question: Do I need a license?
  - answer: JDK 8 or newer.
    question: Which Java version is required?
  - answer: Absolutely—GroupDocs.Search can handle multi‑hundred‑page documents with
      incremental indexing.
    question: Is this suitable for large datasets?
  type: FAQPage
title: java full text search – เพิ่มเอกสารและรวมกับ GroupDocs.Search
type: docs
url: /th/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# การค้นหาข้อความเต็มใน Java – เพิ่มเอกสารและผสานกับ GroupDocs.Search

ในสภาพแวดล้อมองค์กรสมัยใหม่, **java full text search** เป็นกระดูกสันหลังของระบบจัดการเอกสาร java ที่แข็งแรง ไม่ว่าคุณจะต้องทำดัชนีสัญญา, ใบแจ้งหนี้, หรือรายงานภายใน, ดัชนีที่ออกแบบอย่างดีจะช่วยให้คุณดึงข้อมูลที่ต้องการได้ในเวลาไม่กี่มิลลิวินาที. บทแนะนำนี้จะพาคุณผ่านการสร้างดัชนี, การเพิ่มเอกสาร, การกำหนดค่าตัวเลือกการผสาน, และการยกเลิกการผสานอย่างปลอดภัย—ทั้งหมดโดยใช้ GroupDocs.Search สำหรับ Java.

## คำตอบด่วน
- **“add documents to index” หมายถึงอะไร?** มันบอก GroupDocs.Search ให้สแกนโฟลเดอร์, ดึงโทเคนที่สามารถค้นหาได้, และเก็บเมทาดาต้าสำหรับแต่ละไฟล์.  
- **ฉันสามารถหยุดการผสานที่ยาวได้หรือไม่?** ได้—ใช้วัตถุ `Cancellation` เพื่อยกเลิกการผสานหลังจากหมดเวลาที่กำหนดได้.  
- **ฉันต้องการไลเซนส์หรือไม่?** ไลเซนส์ทดลองฟรีหรือไลเซนส์ชั่วคราวสามารถใช้งานสำหรับการทดสอบ; ไลเซนส์เชิงพาณิชย์จะเปิดฟีเจอร์ทั้งหมด.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 หรือใหม่กว่า.  
- **เหมาะกับชุดข้อมูลขนาดใหญ่หรือไม่?** แน่นอน—GroupDocs.Search สามารถจัดการเอกสารหลายร้อยหน้าได้ด้วยการทำดัชนีแบบเพิ่มส่วน.

## “add documents to index” คืออะไรใน GroupDocs.Search?
**การเพิ่มเอกสารลงในดัชนีหมายถึงการป้อนชุดไฟล์เข้าสู่ GroupDocs.Search เพื่อให้ไลบรารีสามารถวิเคราะห์เนื้อหา, ดึงโทเคน, และสร้างโครงสร้างข้อมูลที่สามารถค้นหาได้.** กระบวนการนี้สร้างการแสดงผลที่กะทัดรัดซึ่งทำให้สามารถทำการค้นหาข้อความเต็มได้อย่างรวดเร็วเหนือเสียงฟ้าผ่าในทุกไฟล์ที่ทำดัชนี.

## ทำไมต้องใช้ GroupDocs.Search สำหรับการจัดการเอกสาร java?
GroupDocs.Search ให้บริการ **การทำดัชนีที่ขยายได้สำหรับรูปแบบอินพุตกว่า 50 ประเภท** (PDF, DOCX, XLSX, PPTX, HTML, รูปภาพ ฯลฯ) และสามารถประมวลผล **เอกสารขนาดถึง 2 GB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ**. API ของมันให้คุณควบคุมอย่างละเอียดในการทำดัชนี, การผสาน, และการยกเลิก, ทำให้เป็นตัวเลือกอันดับต้น ๆ สำหรับโซลูชันการค้นหาข้อความเต็มใน Java ระดับองค์กร.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search for Java** เวอร์ชัน 25.4 หรือใหม่กว่า.  
- Maven (หรือดาวน์โหลด JAR ด้วยตนเอง).  
- ความรู้พื้นฐานของ Java และสภาพแวดล้อม JDK 8+.

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การติดตั้งด้วย Maven
หากคุณจัดการ dependencies ด้วย Maven, เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ:

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
หรืออีกทางเลือกหนึ่ง, ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
- **Free Trial:** สมัครบนเว็บไซต์ GroupDocs เพื่อรับไลเซนส์ทดลอง.  
- **Temporary License:** ขอรับคีย์ชั่วคราวหากต้องการการประเมินผลที่ยาวนานขึ้น.  
- **Commercial License:** ซื้อเพื่อการใช้งานในสภาพแวดล้อมการผลิต.

หลังจากที่คุณมีไฟล์ไลเซนส์แล้ว, วางไว้ในโปรเจคของคุณและเริ่มต้นไลบรารีตามที่แสดงต่อไป.

## คู่มือการใช้งาน

### วิธีเพิ่มเอกสารลงในดัชนี – การสร้างดัชนีแรก
**โหลดหรือสร้างดัชนีเปล่าโดยการสร้างอินสแตนซ์ของคลาส `Index` ซึ่งเป็นตัวแทนของคอนเทนเนอร์ที่สามารถค้นหาได้บนดิสก์.** ขั้นตอนนี้เตรียมตำแหน่งจัดเก็บสำหรับโทเคนทั้งหมดที่จะสร้างจากเอกสารของคุณ.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **ทำไม:** ขั้นตอนนี้ตั้งค่าคอนเทนเนอร์จัดเก็บที่โทเคนที่ทำดัชนีจะถูกบันทึก.

#### การเพิ่มเอกสารลงในดัชนี
**เรียก `index.add` พร้อมเส้นทางโฟลเดอร์; เมธอดจะสแกนแต่ละไฟล์, ดึงข้อความ, และเก็บเมทาดาต้าที่สามารถค้นหาได้ในดัชนี.** การทำงานนี้ทำในหนึ่งรอบและเคารพ `IndexSettings` ที่กำหนด.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **ทำไม:** ไลบรารีอ่านแต่ละไฟล์, ดึงข้อความ, และเก็บไว้ใน `index1`.

### การสร้างดัชนีที่สองสำหรับกระบวนการทำงานที่ยืดหยุ่น
**สร้างอินสแตนซ์ของอ็อบเจกต์ `Index` อีกอันเพื่อเก็บชุดเอกสารแยก, ทำให้สามารถประมวลผลแยกก่อนการผสาน.** แพทเทิร์นนี้มีประโยชน์สำหรับสถานการณ์หลายผู้เช่า หรือการทำดัชนีแบบขั้นตอน.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **ทำไม:** ดัชนีหลายอันทำให้คุณจัดการชุดเอกสารที่แตกต่างกันและต่อมาผสานรวมได้.

### วิธีกำหนดค่าตัวเลือกการผสานและยกเลิกการผสาน
**สร้างอินสแตนซ์ `MergeOptions`, ตั้งค่าพารามิเตอร์ที่ต้องการ, และแนบโทเคน `Cancellation` ที่จะยกเลิกการผสานหลังจากหมดเวลาที่กำหนด.** สิ่งนี้ให้คุณควบคุมการใช้ทรัพยากรอย่างเต็มที่ระหว่างการผสานขนาดใหญ่.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **ทำไม:** `Cancellation` ให้คุณควบคุมเพื่อ **ยกเลิกการผสาน** อย่างอัตโนมัติ, ป้องกันงานที่วิ่งเกินขอบเขต.

### การผสานดัชนี
**เรียก `index1.merge(index2, mergeOptions)`; ดัชนีหลักจะดูดซับเอกสารทั้งหมดจากดัชนีรองพร้อมคงความสมบูรณ์ของโทเคน.** หลังจากการผสาน, คุณจะมีคลังข้อมูลที่สามารถค้นหาได้แบบรวม.

```java
index1.merge(index2, options);
```

- **ทำไม:** หลังจากเรียกนี้, `index1` จะมีเอกสารทั้งหมดจากทั้งสองแหล่ง, ให้คุณประสบการณ์การค้นหาที่รวมกัน.

## การประยุกต์ใช้งานจริงสำหรับการจัดการเอกสาร Java
- **Legal firms:** รวมไฟล์คดีจากหลายสำนักงานเป็นดัชนีที่สามารถค้นหาได้เดียว.  
- **Financial institutions:** ผสานรายงานไตรมาสเป็นคลังข้อมูลรวมเพื่อการสอบถามตรวจสอบอย่างรวดเร็ว.  
- **Enterprises:** รวมนโยบาย HR, คู่มือการปฏิบัติตาม, และคู่มือภายในเพื่อการค้นหาในระดับองค์กร.

## พิจารณาด้านประสิทธิภาพ
- **Incremental indexing:** เพิ่มไฟล์ใหม่เป็นระยะ ๆ แทนการสร้างดัชนีใหม่ทั้งหมด.  
- **Memory monitoring:** ชุดข้อมูลขนาดใหญ่สามารถใช้ RAM มาก; ประมวลผลไฟล์เป็นชิ้นเล็ก ๆ หรือเปิดโหมดสตรีมมิง.  
- **Garbage collection:** ปล่อยอ็อบเจกต์ `Index` ที่ไม่ได้ใช้โดยเร็วเพื่อคืนทรัพยากร.  
- **SSD storage:** การเก็บไฟล์ดัชนีบน SSD สามารถเพิ่มความเร็วการผสานได้ถึง 2 เท่า.

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | วิธีแก้ |
|-------|----------|
| **เส้นทางโฟลเดอร์ไม่ถูกต้อง** | ตรวจสอบเส้นทางเต็มและให้แน่ใจว่าแอปพลิเคชันมีสิทธิ์อ่าน. |
| **หน่วยความจำไม่เพียงพอ** | เพิ่มขนาด heap ของ JVM (`-Xmx`) หรือทำดัชนีไฟล์เป็นชุด. |
| **การยกเลิกไม่ทำงาน** | ตรวจสอบว่าได้ตั้งค่า `cancelAfter` ก่อนเรียก `merge`. |
| **รูปแบบไฟล์ที่ไม่รองรับ** | ติดตั้งปลั๊กอินรูปแบบเพิ่มเติมจาก GroupDocs หากจำเป็น. |

## คำถามที่พบบ่อย

**Q:** *ทำไมฉันจึงสร้างดัชนีหลายอันแทนที่จะเป็นหนึ่งอันเดียว?*  
**A:** ดัชนีแยกทำให้คุณแยกโดเมนข้อมูล, ใช้นโยบายความปลอดภัยที่แตกต่าง, และผสานเฉพาะเมื่อจำเป็น, ซึ่งช่วยปรับปรุงประสิทธิภาพและการจัดการ.

**Q:** *ฉันสามารถยกเลิกการทำดัชนีได้เช่นเดียวกับการยกเลิกการผสานหรือไม่?*  
**A:** ได้—ใช้วัตถุ `Cancellation` กับเมธอด `add` เพื่อหยุดงานทำดัชนีที่ทำงานนาน.

**Q:** *ฉันจะทำให้ประสิทธิภาพสูงสุดกับชุดเอกสารขนาดใหญ่มากได้อย่างไร?*  
**A:** ทำการทำดัชนีแบบเพิ่มส่วน, ตรวจสอบหน่วยความจำของ JVM, และเก็บดัชนีบน SSD. พิจารณาใช้การตั้งค่า `BatchSize` เพื่อจำกัดจำนวนเอกสารในหน่วยความจำ.

**Q:** *ฉันควรทำอย่างไรหากได้รับข้อผิดพลาด “Access denied”?*  
**A:** ตรวจสอบสิทธิ์โฟลเดอร์สำหรับผู้ใช้ที่รันกระบวนการ Java และให้แน่ใจว่าไฟล์ไลเซนส์สามารถอ่านได้.

**Q:** *GroupDocs.Search เข้ากันได้กับไลบรารี GroupDocs อื่นหรือไม่?*  
**A:** แน่นอน—คุณสามารถรวมกับ GroupDocs.Viewer, GroupDocs.Conversion, และอื่น ๆ เพื่อสร้างโซลูชันเอกสารแบบเต็มสแตก.

## สรุป
โดยทำตามคู่มือนี้คุณจะรู้วิธี **add documents to index**, กำหนดค่าพฤติกรรมการผสาน, และปลอดภัย **cancel merge operation** เมื่อจำเป็น—ทั้งหมดในกระบวนการ **java full text search** ที่แข็งแรง. ทดลองกับชุดข้อมูลที่ใหญ่ขึ้น, สำรวจตัวแยกโทเคนแบบกำหนดเอง, หรือผสาน GroupDocs.Search กับผลิตภัณฑ์ GroupDocs อื่นเพื่อสร้างโซลูชันระดับองค์กร.

**แหล่งข้อมูล**
- **เอกสาร:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **อ้างอิง API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **ดาวน์โหลด:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **ที่เก็บ GitHub:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **ฟอรั่มสนับสนุนฟรี:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **การสมัครไลเซนส์ชั่วคราว:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**อัปเดตล่าสุด:** 2026-05-12  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเพิ่มเอกสารลงในดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [เพิ่มเอกสารลงในดัชนีและปิดการใช้งาน Stop Words ใน GroupDocs.Search Java เพื่อความแม่นยำในการค้นหาที่ดีขึ้น](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
- [เพิ่มเอกสารลงในดัชนี – บทแนะนำ GroupDocs.Search Java](/search/java/document-management/)
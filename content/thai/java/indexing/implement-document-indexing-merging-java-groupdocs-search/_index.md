---
date: '2026-01-03'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและยกเลิกการผสานใน Java ด้วย GroupDocs.Search
  คู่มือฉบับสมบูรณ์สำหรับการจัดการเอกสารด้วย Java.
keywords:
- document indexing in Java
- merging documents with GroupDocs
- GroupDocs.Search Java tutorial
title: เพิ่มเอกสารลงในดัชนีและรวมใน Java ด้วย GroupDocs.Search
type: docs
url: /th/java/indexing/implement-document-indexing-merging-java-groupdocs-search/
weight: 1
---

# เพิ่มเอกสารเข้าสู่ดัชนีและรวมใน Java ด้วย GroupDocs.Search

ในสภาพแวดล้อมดิจิทัลที่เปลี่ยนแปลงอย่างรวดเร็วในวันนี้ การเรียนรู้ **how to add documents to index** อย่างมีประสิทธิภาพเป็นสิ่งสำคัญสำหรับโซลูชัน **document management java** ใด ๆ ไม่ว่าคุณจะจัดการกับสัญญา ใบแจ้งหนี้ หรือรายงานภายใน ดัชนีที่มีโครงสร้างดีจะทำให้คุณดึงข้อมูลได้ในเวลาเพียงไม่กี่มิลลิวินาที คู่มือฉบับนี้จะพาคุณผ่านการสร้างดัชนี การเพิ่มเอกสาร การกำหนดค่าตัวเลือกการรวม และแม้กระทั่ง **cancel merge operation** หากจำเป็น — ทั้งหมดนี้ด้วย GroupDocs.Search สำหรับ Java.

## คำตอบด่วน
- **What does “add documents to index” mean?** มันบอกให้ GroupDocs.Search สแกนโฟลเดอร์และเก็บเมตาดาต้าที่สามารถค้นหาได้สำหรับแต่ละไฟล์.  
- **Can I stop a long merge?** ใช่ — ใช้วัตถุ `Cancellation` เพื่อ **cancel merge operation** หลังจากหมดเวลา.  
- **Do I need a license?** การทดลองใช้ฟรีหรือใบอนุญาตชั่วคราวทำงานได้สำหรับการทดสอบ; ใบอนุญาตเชิงพาณิชย์จะเปิดฟีเจอร์ทั้งหมด.  
- **Which Java version is required?** JDK 8 หรือใหม่กว่า.  
- **Is this suitable for large datasets?** แน่นอน — เพียงตรวจสอบหน่วยความจำและใช้การทำดัชนีแบบเพิ่มส่วน.

## “add documents to index” คืออะไรใน GroupDocs.Search?
การเพิ่มเอกสารเข้าสู่ดัชนีหมายถึงการป้อนชุดไฟล์เข้าไปใน GroupDocs.Search เพื่อให้ไลบรารีสามารถวิเคราะห์เนื้อหา ดึงโทเคน และสร้างโครงสร้างข้อมูลที่สามารถค้นหาได้ เมื่อทำดัชนีแล้ว คุณสามารถทำการค้นหาแบบเต็มข้อความอย่างรวดเร็วในทุกเอกสารได้.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ document management java?
- **Scalable indexing** – จัดการไฟล์หลายพันไฟล์โดยไม่ทำให้ประสิทธิภาพลดลง.  
- **Rich API** – ให้การควบคุมระดับละเอียดในการทำดัชนี การรวม และการยกเลิก.  
- **Cross‑format support** – ทำงานกับ PDF, Word, Excel และรูปแบบอื่น ๆ มากมายโดยพร้อมใช้งาน.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search for Java** เวอร์ชัน 25.4 หรือใหม่กว่า.  
- Maven (หรือดาวน์โหลด JAR ด้วยตนเอง).  
- ความรู้พื้นฐานของ Java และสภาพแวดล้อม JDK 8+.

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การติดตั้งด้วย Maven
หากคุณจัดการ dependencies ด้วย Maven ให้เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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
หรืออีกทางหนึ่ง ให้ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
- **Free Trial:** ลงทะเบียนบนเว็บไซต์ GroupDocs เพื่อรับใบอนุญาตทดลอง.  
- **Temporary License:** ขอรับคีย์ชั่วคราวหากต้องการการประเมินผลที่ยาวนานขึ้น.  
- **Commercial License:** ซื้อเพื่อการใช้งานในสภาพแวดล้อมการผลิต.

หลังจากที่คุณมีไฟล์ใบอนุญาตแล้ว ให้วางไว้ในโปรเจกต์ของคุณและเริ่มต้นไลบรารีตามที่แสดงต่อไปนี้.

## คู่มือการดำเนินการ

### วิธีการเพิ่มเอกสารเข้าสู่ดัชนี – การสร้างดัชนีแรก
ขั้นแรก สร้างดัชนีเปล่าที่จะเก็บข้อมูลที่สามารถค้นหาได้ของคุณ.

```java
import com.groupdocs.search.Index;

// Create an instance of the index at the specified path
Index index1 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index1");
```

- **Why:** ขั้นตอนนี้ตั้งค่าตัวเก็บข้อมูลที่โทเคนที่ทำดัชนีจะถูกบันทึก.

#### การเพิ่มเอกสารเข้าสู่ดัชนี
ตอนนี้บอกให้ GroupDocs.Search สแกนโฟลเดอร์และ **add documents to index**.

```java
index1.add("YOUR_DOCUMENT_DIRECTORY"); // Add documents from this directory
```

- **Why:** ไลบรารีอ่านไฟล์แต่ละไฟล์ ดึงข้อความ และเก็บไว้ใน `index1`.

### การสร้างดัชนีที่สองสำหรับกระบวนการทำงานที่ยืดหยุ่น
บางครั้งคุณอาจต้องการดัชนีแยกกัน — ตัวอย่างเช่น เพื่อแยกข้อมูลของลูกค้า.

```java
Index index2 = new Index("YOUR_DOCUMENT_DIRECTORY\\\\Index2");
```

```java
index2.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Why:** ดัชนีหลายชุดทำให้คุณจัดการชุดเอกสารที่แตกต่างกันและรวมกันในภายหลังได้.

### วิธีการกำหนดค่าตัวเลือกการรวมและยกเลิกการรวม
ก่อนทำการรวม คุณสามารถปรับแต่งกระบวนการอย่างละเอียดและแม้กระทั่งหยุดมันหากทำงานนานเกินไป.

```java
import com.groupdocs.search.options.MergeOptions;
import com.groupdocs.search.options.Cancellation;

MergeOptions options = new MergeOptions();
options.setCancellation(new Cancellation()); // Initialize cancellation object
options.getCancellation().cancelAfter(5000); // Cancel merge operation after 5 seconds
```

- **Why:** `Cancellation` ให้คุณควบคุมเพื่อ **cancel merge operation** โดยอัตโนมัติ ป้องกันงานที่ทำงานต่อเนื่องโดยไม่มีที่สิ้นสุด.

### การรวมดัชนี
สุดท้าย ให้รวมดัชนีรองเข้ากับดัชนีหลัก.

```java
index1.merge(index2, options);
```

- **Why:** หลังจากเรียกนี้ `index1` จะมีเอกสารทั้งหมดจากทั้งสองแหล่ง ทำให้คุณได้ประสบการณ์การค้นหาแบบรวมศูนย์.

## การประยุกต์ใช้จริงสำหรับ Document Management Java
- **Legal firms:** รวมไฟล์คดีจากหลายสาขา.  
- **Financial institutions:** รวมรายงานไตรมาสเป็นคลังข้อมูลที่สามารถค้นหาได้เดียว.  
- **Enterprises:** รวมเอกสาร HR, compliance, และนโยบายเพื่อการค้นหาในระดับองค์กร.

## การพิจารณาด้านประสิทธิภาพ
- **Incremental indexing:** เพิ่มไฟล์ใหม่เป็นระยะ ๆ แทนการสร้างดัชนีใหม่ทั้งหมด.  
- **Memory monitoring:** ชุดข้อมูลขนาดใหญ่สามารถใช้ RAM มาก; พิจารณาประมวลผลเป็นส่วนย่อย.  
- **Garbage collection:** ปล่อยวัตถุ `Index` ที่ไม่ได้ใช้โดยเร็วเพื่อคืนทรัพยากร.

## ปัญหาทั่วไปและวิธีแก้

| Issue | Solution |
|-------|----------|
| **Incorrect folder path** | ตรวจสอบเส้นทางแบบเต็มและให้แน่ใจว่าแอปพลิเคชันมีสิทธิ์อ่าน. |
| **Insufficient memory** | เพิ่มขนาด heap ของ JVM (`-Xmx`) หรือทำดัชนีไฟล์เป็นชุด. |
| **Cancellation not triggered** | ตรวจสอบให้แน่ใจว่าได้ตั้งค่า `cancelAfter` ก่อนเรียก `merge`. |
| **Unsupported file format** | ติดตั้งปลั๊กอินรูปแบบเพิ่มเติมจาก GroupDocs หากจำเป็น. |

## คำถามที่พบบ่อย

**Q:** *ทำไมฉันจึงสร้างดัชนีหลายชุดแทนที่จะเป็นชุดเดียว?*  
**A:** ดัชนีแยกทำให้คุณแยกโดเมนข้อมูล ประยุกต์ใช้แนวทางความปลอดภัยที่ต่างกัน และรวมกันเฉพาะเมื่อจำเป็น ซึ่งช่วยปรับปรุงประสิทธิภาพและการจัดการ.

**Q:** *ฉันสามารถยกเลิกการทำดัชนีได้เช่นเดียวกับการยกเลิกการรวมหรือไม่?*  
**A:** ใช่ — ใช้วัตถุ `Cancellation` พร้อมเมธอด `add` เพื่อหยุดงานทำดัชนีที่ใช้เวลานาน.

**Q:** *ฉันจะทำให้ประสิทธิภาพสูงสุดกับคอลเลกชันเอกสารขนาดใหญ่มากได้อย่างไร?*  
**A:** ทำดัชนีแบบเพิ่มส่วน ตรวจสอบหน่วยความจำของ JVM และพิจารณาใช้ SSD สำหรับไดเรกทอรีดัชนี.

**Q:** *ควรทำอย่างไรหากได้รับข้อผิดพลาด “Access denied”?*  
**A:** ตรวจสอบสิทธิ์ของโฟลเดอร์สำหรับผู้ใช้ที่รันกระบวนการ Java และให้แน่ใจว่าไฟล์ใบอนุญาตสามารถอ่านได้.

**Q:** *GroupDocs.Search เข้ากันได้กับไลบรารี GroupDocs อื่นหรือไม่?*  
**A:** แน่นอน — คุณสามารถรวมกับ GroupDocs.Viewer, GroupDocs.Conversion ฯลฯ เพื่อสร้างโซลูชันเอกสารแบบเต็มสแตก.

## สรุป
โดยทำตามคู่มือนี้คุณจะรู้วิธี **add documents to index**, กำหนดค่าการรวม, และปลอดภัย **cancel merge operation** เมื่อจำเป็น — ทั้งหมดนี้อยู่ในกระบวนการ **document management java** ที่แข็งแกร่ง ทดลองกับชุดข้อมูลขนาดใหญ่ สำรวจตัวแยกโทเคนแบบกำหนดเอง หรือรวม GroupDocs.Search กับผลิตภัณฑ์ GroupDocs อื่นเพื่อสร้างโซลูชันระดับองค์กรที่แท้จริง.

---

**Last Updated:** 2026-01-03  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

**Resources**
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License Application:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)
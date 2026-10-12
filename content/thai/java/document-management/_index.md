---
date: 2026-10-12
description: เรียนรู้วิธีอัปเดตดัชนี, เพิ่มเอกสาร, และลบรายการดัชนีโดยใช้ GroupDocs.Search
  for Java. ขั้นตอนโดยละเอียด, แนวทางปฏิบัติที่ดีที่สุด, และตัวอย่างโค้ด.
keywords:
- how to update index
- how to add documents
- how to delete index
lastmod: 2026-10-12
og_description: เรียนรู้วิธีอัปเดตดัชนี, เพิ่มเอกสาร, และลบรายการดัชนีด้วย GroupDocs.Search
  for Java. ปฏิบัติตามคำแนะนำแบบขั้นตอนต่อขั้นตอนและเคล็ดลับด้านประสิทธิภาพ.
og_image_alt: Guide to updating index, adding and deleting documents using GroupDocs.Search
  Java SDK
og_title: วิธีอัปเดตดัชนีและเพิ่มเอกสารด้วย GroupDocs.Search Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: Learn how to update index, add documents, and delete index entries
    using GroupDocs.Search for Java. Detailed steps, best practices, and code examples.
  headline: How to update index and add docs with GroupDocs.Search Java
  type: TechArticle
- description: Learn how to update index, add documents, and delete index entries
    using GroupDocs.Search for Java. Detailed steps, best practices, and code examples.
  name: How to update index and add docs with GroupDocs.Search Java
  steps:
  - name: open or create the index
    text: '`Index index = new Index("path/to/index");` creates the folder if it does
      not exist and prepares internal structures for fast lookup.'
  - name: add a single document
    text: '`index.addDocument(new File("contracts/contract1.pdf"));` inserts the PDF,
      automatically detecting its format and extracting text.'
  - name: add multiple documents in a batch
    text: Iterate over a directory and call `addDocument` for each file. Batch processing
      reduces I/O overhead and improves overall throughput.
  type: HowTo
- questions:
  - answer: Call `deleteDocument(documentId)` with the unique identifier; the entry
      is instantly purged and storage is reclaimed.
    question: How do I remove documents from index?
  - answer: Yes, you can set custom metadata (e.g., category, author) via the `Document`
      object's attribute API before adding it to the index.
    question: Can I modify document attributes to enhance search accuracy?
  - answer: The official GroupDocs.Search documentation includes a step‑by‑step tutorial
      that covers index creation, document addition, and query execution.
    question: Is there a “search index tutorial” for beginners?
  - answer: The library includes linguistic features that improve accuracy for homophones
      and similar‑sounding words.
    question: Does GroupDocs.Search support homophone recognition?
  - answer: Java 8 or later is required; the library is fully compatible with Java
      11 and newer LTS releases.
    question: What version of Java is required for the latest GroupDocs.Search?
  type: FAQPage
tags:
- update index
- document management
- GroupDocs.Search Java
- add documents
title: วิธีอัปเดตดัชนีและเพิ่มเอกสารด้วย GroupDocs.Search Java
type: docs
url: /th/java/document-management/
weight: 6
---

# วิธีอัปเดตดัชนีและเพิ่มเอกสารด้วย GroupDocs.Search Java

การจัดการดัชนีการค้นหาอย่างมีประสิทธิภาพเป็นสิ่งสำคัญสำหรับแอปพลิเคชันที่ใช้ Java ที่ต้องการการดึงข้อมูลที่รวดเร็วและแม่นยำ ในบทเรียนนี้คุณจะได้เรียนรู้ **วิธีอัปเดตดัชนี** รวมถึงวิธีเพิ่มและลบเอกสารโดยใช้ GroupDocs.Search สำหรับ Java คุณจะได้เห็นรูปแบบการปฏิบัติที่ดีที่สุด เคล็ดลับด้านประสิทธิภาพ และตัวอย่างการใช้งานจริงที่ทำให้ดัชนีของคุณเบาและการค้นหาของคุณเร็วเหมือนสายฟ้า

## คำตอบสั้น
- **ขั้นตอนแรกในการเพิ่มเอกสารลงในดัชนีคืออะไร?** สร้างหรือเปิดอินสแตนซ์ `Index` แล้วเรียก `addDocument(...)`.
- **ฉันสามารถลบเอกสารจากดัชนีได้หรือไม่?** ได้, เรียกใช้ `deleteDocument(...)` พร้อมกับตัวระบุของเอกสาร.
- **ฉันต้องการใบอนุญาตพิเศษหรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs.Search สำหรับ Java ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต.
- **เวอร์ชัน Java ที่รองรับคืออะไร?** รองรับ Java 8 ขึ้นไปอย่างเต็มที่.
- **ฉันสามารถหาตัวอย่างเพิ่มเติมได้ที่ไหน?** ดูเอกสารและอ้างอิง API อย่างเป็นทางการของ GroupDocs.Search สำหรับ Java.

## “การเพิ่มเอกสารลงในดัชนี” ใน GroupDocs.Search คืออะไร?
การทำงาน `addDocument` จะใส่เนื้อหาที่สามารถค้นหาได้ของไฟล์ (PDF, DOCX, TXT ฯลฯ) ลงในโครงสร้างข้อมูลของดัชนี ทำให้เอกสารสามารถค้นหาได้ทันทีและรับประกันว่าการอัปเดตหรือการลบต่อมาจะสอดคล้องกับไฟล์ต้นฉบับ นอกจากนี้ยังบันทึกเมตาดาต้าเช่นชื่อไฟล์และขนาด ซึ่งสามารถใช้ในการกรองผลการค้นหาได้.

## ทำไมต้องใช้ GroupDocs.Search สำหรับโครงการจัดการเอกสารใน Java?
GroupDocs.Search สามารถประมวลผลได้ถึง **10 ล้านเอกสาร** ด้วยความหน่วงเวลาน้อยกว่า 1 วินาที รองรับ **ไฟล์รูปแบบกว่า 100** ประเภท และมีการปรับความเกี่ยวข้องในตัว API มีน้ำหนักเบา ต้องการเพียงไม่กี่บรรทัดของโค้ดและสามารถรวมเข้ากับแอปพลิเคชัน Java ใดก็ได้อย่างราบรื่น ไม่ว่าจะทำงานบนเดสก์ท็อป, เซิร์ฟเวอร์ หรือคลาวด์

## ข้อกำหนดเบื้องต้น
- สภาพแวดล้อมการพัฒนา Java 8 + (IDE, JDK, Maven/Gradle).  
- ไลบรารี GroupDocs.Search สำหรับ Java (ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการ).  
- ใบอนุญาต GroupDocs.Search ที่ถูกต้อง (มีใบอนุญาตชั่วคราวสำหรับการทดสอบ).

## วิธีเพิ่มเอกสารลงในดัชนีด้วย GroupDocs.Search สำหรับ Java?
โหลดไฟล์เป้าหมายและเรียก `addDocument` บนอินสแตนซ์ `Index` — การเรียกครั้งเดียวนี้จะสกัดข้อความ ตรวจจับภาษา และเก็บโทเคนที่สามารถค้นหาได้ วิธีนี้ยังคืนค่า ID ของเอกสารที่คุณควรบันทึกไว้สำหรับการอัปเดตหรือการลบในอนาคต.

คลาส `Index` เป็นอ็อบเจ็กต์หลักที่แสดงถึงคอลเลกชันที่สามารถค้นหาได้ซึ่งเก็บบนดิสก์ หลังจากที่คุณสร้างมันแล้ว การดำเนินการต่อ ๆ ไปทั้งหมด—การเพิ่ม, การอัปเดต, การลบ, และการปรับประสิทธิภาพ—จะทำผ่านอินสแตนซ์นี้.

### ขั้นตอนที่ 1: เปิดหรือสร้างดัชนี
```java
Index index = new Index("path/to/index");
```
สร้างโฟลเดอร์หากยังไม่มีและเตรียมโครงสร้างภายในสำหรับการค้นหาอย่างรวดเร็ว.

### ขั้นตอนที่ 2: เพิ่มเอกสารเดี่ยว
```java
index.addDocument(new File("contracts/contract1.pdf"));
```
แทรกไฟล์ PDF โดยอัตโนมัติตรวจจับรูปแบบและสกัดข้อความ.

### ขั้นตอนที่ 3: เพิ่มหลายเอกสารเป็นชุด
วนซ้ำผ่านไดเรกทอรีและเรียก `addDocument` สำหรับแต่ละไฟล์ การประมวลผลเป็นชุดช่วยลดภาระ I/O และเพิ่มอัตราการทำงานโดยรวม.

## วิธีอัปเดตดัชนีเมื่อไฟล์ต้นฉบับมีการเปลี่ยนแปลง?
`updateDocument` จะอัปเดตเอกสารที่มีอยู่ในดัชนีโดยใช้ตัวระบุของมัน แทนที่เนื้อหาเก่าด้วยเวอร์ชันล่าสุดโดยเรียกเมธอดนี้และส่งตัวระบุเอกสารเดียวกันที่คุณได้รับเมื่อเพิ่มไฟล์ครั้งแรก การดำเนินการนี้จะเขียนทับเฉพาะโทเคนที่เปลี่ยนแปลงเท่านั้น ทำให้ส่วนที่เหลือของดัชนียังคงไม่เปลี่ยนแปลงเพื่อประสิทธิภาพสูงสุด.

### ขั้นตอนการอัปเดตแบบทีละขั้นตอน
1. ดึง ID ของเอกสาร (บันทึกไว้เมื่อคุณเพิ่มไฟล์ครั้งแรก).  
2. เรียก `index.updateDocument(documentId, new File("contracts/contract1_v2.pdf"));` เพื่อรีเฟรชรายการ.  
3. หากต้องการ สามารถเรียก `index.optimize()` อีกครั้งหลังจากอัปเดตเป็นชุดใหญ่เพื่อให้ดัชนีมีขนาดกระชับ.

## วิธีลบรายการในดัชนีอย่างปลอดภัย?
`deleteDocument` จะลบเอกสารออกจากดัชนีโดยใช้ตัวระบุของมัน การลบเอกสารจะคืนพื้นที่จัดเก็บและป้องกันข้อมูลล้าสมัยจากการทำให้คะแนนความเกี่ยวข้องบิดเบือน เรียก `deleteDocument` พร้อมตัวระบุ; ดัชนีจะทันทีไม่รวมไฟล์นี้ในการค้นหาในอนาคตและอัปเดตรายการโพสต์ภายในเพื่อรักษาประสิทธิภาพการค้นหา.

## วิธีปรับประสิทธิภาพดัชนีให้ถึงจุดสูงสุด?
`optimize()` จะทำให้ดัชนีกระชับโดยการรวมเซกเมนต์และทำความสะอาดรายการที่ถูกลบ หลังจากการเพิ่ม, การอัปเดต หรือการลบเป็นจำนวนมาก ให้เรียกเมธอดนี้เพื่อบีบอัดรายการโพสต์และจัดโครงสร้างการจัดเก็บใหม่ ขั้นตอนนี้สามารถลดความหน่วงของการค้นหาได้ถึง **30 %** สำหรับดัชนีขนาดใหญ่และช่วยให้ขนาดดัชนีอยู่ในระดับที่จัดการได้.

## กรณีการใช้งานทั่วไป
- **คลังเอกสารทางกฎหมาย:** เพิ่ม, อัปเดต, และลบไฟล์คดีขณะรักษาความเกี่ยวข้องสูงสำหรับการค้นหาด้วยคีย์เวิร์ด.  
- **ฐานความรู้ขององค์กร:** ทำให้คู่มือภายใน, นโยบาย, และคำถามที่พบบ่อยสามารถค้นหาได้ขณะพัฒนา.  
- **แคตาล็อกอีคอมเมิร์ซ:** ทำดัชนีสเปคสินค้าและลบรายการที่หยุดผลิตโดยไม่ต้องหยุดทำงาน.

## การแก้ไขปัญหาและเคล็ดลับ
- **เคล็ดลับมืออาชีพ:** เพิ่มเอกสารเป็นชุดในช่วงเวลาที่ไม่ใช่ชั่วโมงเร่งด่วนเพื่อหลีกเลี่ยงการเพิ่มขึ้นของประสิทธิภาพ.  
- **ข้อผิดพลาด:** การข้าม `optimize()` หลังจากการลบจำนวนมากอาจทำให้ดัชนีเป็นชิ้นส่วนและการค้นหาช้าลง.  
- **การจัดการข้อผิดพลาด:** ห่อหุ้มการดำเนินการดัชนีทั้งหมดในบล็อก `try‑catch` เพื่อจัดการ `IndexException` อย่างราบรื่น.  
- **เคล็ดลับประสิทธิภาพ:** ใช้ `IndexSettings` เพื่อปรับการใช้หน่วยความจำเมื่อจัดการกับชุดข้อมูลขนาดใหญ่มาก (เช่น ตั้งค่า `maxMemoryUsage` เป็นค่าสูงบนเซิร์ฟเวอร์ที่มี RAM เพียงพอ).  
- **ความปลอดภัยของหน่วยความจำ:** สำหรับไฟล์ที่ใหญ่กว่า 500 MB ควรพิจารณาการสตรีมอินพุตไปยัง `addDocument` เพื่อให้การใช้หน่วยความจำของ JVM ต่ำ.

## คำถามที่พบบ่อย

**ถาม: ฉันจะลบเอกสารจากดัชนีได้อย่างไร?**  
ตอบ: เรียก `deleteDocument(documentId)` พร้อมกับตัวระบุที่ไม่ซ้ำกัน; รายการจะถูกลบทันทีและพื้นที่จัดเก็บจะถูกกู้คืน.

**ถาม: ฉันสามารถแก้ไขแอตทริบิวต์ของเอกสารเพื่อเพิ่มความแม่นยำของการค้นหาได้หรือไม่?**  
ตอบ: ได้, คุณสามารถตั้งค่าเมตาดาต้าตามต้องการ (เช่น หมวดหมู่, ผู้เขียน) ผ่าน API แอตทริบิวต์ของอ็อบเจ็กต์ `Document` ก่อนเพิ่มลงในดัชนี.

**ถาม: มี “บทเรียนการสร้างดัชนีการค้นหา” สำหรับผู้เริ่มต้นหรือไม่?**  
ตอบ: เอกสารอย่างเป็นทางการของ GroupDocs.Search มีบทเรียนแบบขั้นตอนที่ครอบคลุมการสร้างดัชนี, การเพิ่มเอกสาร, และการดำเนินการค้นหา.

**ถาม: GroupDocs.Search รองรับการจดจำโฮโมโฟนหรือไม่?**  
ตอบ: ไลบรารีนี้มีฟีเจอร์ด้านภาษาที่ช่วยเพิ่มความแม่นยำสำหรับโฮโมโฟนและคำที่ออกเสียงคล้ายกัน.

**ถาม: ต้องใช้เวอร์ชัน Java ใดสำหรับ GroupDocs.Search ล่าสุด?**  
ตอบ: จำเป็นต้องใช้ Java 8 หรือใหม่กว่า; ไลบรารีนี้เข้ากันได้อย่างเต็มที่กับ Java 11 และรุ่น LTS ที่ใหม่กว่า.

## บทเรียนที่พร้อมใช้งาน

### [วิธีอัปเดตและจัดการเวอร์ชันดัชนีใน GroupDocs.Search สำหรับ Java&#58; คู่มือครบถ้วน](./guide-updating-index-versions-groupdocs-search-java/)
### [การจัดการเอกสารขั้นสูงด้วย GroupDocs.Search สำหรับ Java&#58; คู่มือการจดจำโฮโมโฟนและการทำดัชนี](./groupdocs-search-java-homophone-document-management-guide/)
### [การควบคุมแอตทริบิวต์เอกสารด้วย GroupDocs.Search ใน Java เพื่อการทำดัชนีและการจัดการที่ดียิ่งขึ้น](./groupdocs-search-java-modify-attributes-indexing/)
### [เชี่ยวชาญ GroupDocs.Search ใน Java&#58; คู่มือครบถ้วนสำหรับการจัดการดัชนีและการค้นหาเอกสาร](./mastering-groupdocs-search-java-index-management-guide/)

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร GroupDocs.Search สำหรับ Java](https://docs.groupdocs.com/search/java/)
- [อ้างอิง API GroupDocs.Search สำหรับ Java](https://reference.groupdocs.com/search/java/)
- [ดาวน์โหลด GroupDocs.Search สำหรับ Java](https://releases.groupdocs.com/search/java/)
- [ฟอรั่ม GroupDocs.Search](https://forum.groupdocs.com/c/search)
- [สนับสนุนฟรี](https://forum.groupdocs.com/)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-10-12  
**ทดสอบด้วย:** GroupDocs.Search for Java 23.11  
**ผู้เขียน:** GroupDocs

## บทเรียนที่เกี่ยวข้อง

- [วิธีอัปเดตดัชนี Java ด้วย GroupDocs.Search – คู่มือครบถ้วน](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [วิธีสร้างดัชนีเอกสารและเพิ่มเอกสารโดยใช้ GroupDocs.Search API สำหรับ Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [วิธีเพิ่มหลายนามแฝงและเพิ่มเอกสารลงในดัชนีใน GroupDocs.Search สำหรับ Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
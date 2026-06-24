---
date: '2026-05-22'
description: เรียนรู้การค้นหาแบบฟัซซี่ใน Java ด้วย GroupDocs.Search Java, เพิ่มเอกสารลงในดัชนี,
  เปิดใช้งานการค้นหาข้อความขั้นสูง, และจัดการไฟล์หลายประเภทอย่างมีประสิทธิภาพ.
keywords:
- java fuzzy search
- advanced text search java
- search file types java
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn java fuzzy search with GroupDocs.Search Java, add documents to
    index, enable advanced text search, and handle multiple file types efficiently.
  headline: 'Java Fuzzy Search: Add Documents to Index with GroupDocs.Search'
  type: TechArticle
- description: Learn java fuzzy search with GroupDocs.Search Java, add documents to
    index, enable advanced text search, and handle multiple file types efficiently.
  name: 'Java Fuzzy Search: Add Documents to Index with GroupDocs.Search'
  steps:
  - name: '**Free Trial** – explore the API without cost.'
    text: '**Free Trial** – explore the API without cost.'
  - name: '**Temporary License** – extend the trial period for deeper testing.'
    text: '**Temporary License** – extend the trial period for deeper testing.'
  - name: '**Purchase** – obtain a commercial license for production use.'
    text: '**Purchase** – obtain a commercial license for production use.'
  - name: '**Corporate Document Management** – Quickly locate policies, contracts,
      or HR manuals across thousands of files.'
    text: '**Corporate Document Management** – Quickly locate policies, contracts,
      or HR manuals across thousands of files.'
  - name: '**Legal Research** – Find precedent cases even when the exact phrasing
      differs, thanks to word‑form search.'
    text: '**Legal Research** – Find precedent cases even when the exact phrasing
      differs, thanks to word‑form search.'
  - name: '**E‑commerce Catalogs** – Allow shoppers to search product descriptions
      using varied terminology, improving conversion rates.'
    text: '**E‑commerce Catalogs** – Allow shoppers to search product descriptions
      using varied terminology, improving conversion rates.'
  type: HowTo
- questions:
  - answer: It means loading source files into a searchable data structure that GroupDocs.Search
      can query.
    question: What does “add documents to index” mean?
  - answer: GroupDocs.Search for Java 25.4 (or newer) includes all features demonstrated
      here.
    question: Which library version is required?
  - answer: A free trial works for development; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—enable `setUseWordFormsSearch(true)` in `SearchOptions`.
    question: Can I search different word forms?
  - answer: No, you can also download the JAR directly (see the Direct Download link).
    question: Is Maven the only way to install?
  type: FAQPage
title: 'การค้นหาแบบฟัซซี่ใน Java: เพิ่มเอกสารลงในดัชนีด้วย GroupDocs.Search'
type: docs
url: /th/java/searching/groupdocs-search-java-advanced-text-search-guide/
weight: 1
---

# การค้นหาแบบฟัซซี่ใน Java: เพิ่มเอกสารลงในดัชนีด้วย GroupDocs.Search

## คำตอบด่วน
- **อะไรหมายถึง “add documents to index”?** หมายถึงการโหลดไฟล์ต้นทางเข้าสู่โครงสร้างข้อมูลที่สามารถค้นหาได้ซึ่ง GroupDocs.Search สามารถสืบค้นได้.  
- **เวอร์ชันของไลบรารีที่ต้องการคืออะไร?** GroupDocs.Search for Java 25.4 (หรือใหม่กว่า) มีคุณลักษณะทั้งหมดที่แสดงในที่นี้.  
- **ต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **สามารถค้นหารูปแบบคำที่แตกต่างได้หรือไม่?** ใช่—เปิดใช้งาน `setUseWordFormsSearch(true)` ใน `SearchOptions`.  
- **Maven เป็นวิธีเดียวในการติดตั้งหรือไม่?** ไม่, คุณสามารถดาวน์โหลด JAR โดยตรงได้ (ดูลิงก์ Direct Download).

## “add documents to index” คืออะไร?
การเพิ่มเอกสารลงในดัชนีหมายถึงการสแกนไฟล์ต้นทาง, ดึงข้อความที่สามารถค้นหาได้, และจัดเก็บข้อมูลนั้นในรูปแบบที่มีโครงสร้างซึ่งทำให้การค้นหาแบบรวดเร็วเป็นไปได้. GroupDocs.Search จัดการไฟล์หลายประเภทโดยอัตโนมัติ, ทำให้คุณมุ่งเน้นที่ตรรกะธุรกิจแทนการแยกวิเคราะห์ไฟล์. ดัชนีที่สร้างขึ้นสามารถเก็บบนดิสก์หรือในหน่วยความจำ, ทำให้การดึงข้อมูลทำได้อย่างรวดเร็วโดยไม่ต้องอ่านไฟล์ต้นฉบับใหม่ทุกครั้งที่มีการสืบค้น.

## ทำไมต้องใช้เทคนิคการค้นหาข้อความขั้นสูงใน Java?
โหลดดัชนีของคุณครั้งเดียวแล้วรันการค้นหาแบบฟัซซี่, ไม่สนใจตัวพิมพ์ใหญ่‑เล็ก, หรือการค้นหาแบบใกล้เคียงโดยไม่ต้องประมวลผลไฟล์ใหม่. การเปิดใช้เทคนิคเหล่านี้ช่วยเพิ่มความครอบคลุมได้ถึง 30 % ในการทดสอบจริง, ทำให้ผู้ใช้พบผลลัพธ์ที่เกี่ยวข้องแม้พิมพ์คำไม่ตรงหรือสะกดผิด.

## ข้อกำหนดเบื้องต้น
- **ไลบรารีที่ต้องการ**: GroupDocs.Search for Java 25.4.  
- **การตั้งค่าสภาพแวดล้อม**: Java JDK 8 หรือใหม่กว่า, Maven (หรือการจัดการ JAR ด้วยตนเอง).  
- **ความรู้เบื้องต้นที่จำเป็น**: การเขียนโปรแกรม Java ขั้นพื้นฐานและการจัดการ dependencies ของ Maven.

## การตั้งค่า GroupDocs.Search สำหรับ Java
ก่อนเขียนโค้ดใด ๆ, ตรวจสอบให้แน่ใจว่าไลบรารีพร้อมใช้งานในโปรเจกต์ของคุณ.

### การตั้งค่า Maven
ไฟล์ `pom.xml` เป็นตัวบรรยายโปรเจกต์ของ Maven ที่ระบุ dependencies.

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
หากคุณไม่ต้องการใช้ Maven, สามารถดาวน์โหลด JAR ล่าสุดจากหน้าอย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

สำหรับคำแนะนำการใช้งานโดยละเอียด, ดูที่ [GroupDocs Documentation](https://docs.groupdocs.com/search/java/).

### ขั้นตอนการรับไลเซนส์
1. **Free Trial** – ทดลองใช้ API ฟรี.  
2. **Temporary License** – ขยายระยะเวลาการทดลองเพื่อการทดสอบที่ลึกซึ้งขึ้น.  
3. **Purchase** – รับไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## ประเภทไฟล์ที่รองรับการค้นหาใน Java
GroupDocs.Search รองรับ **กว่า 50 รูปแบบไฟล์** รวมถึง DOCX, PDF, PPTX, XLSX, TXT, HTML, และรูปภาพทั่วไป, ทำให้คุณสามารถทำดัชนีเอกสารเกือบทุกประเภทที่ธุรกิจของคุณใช้ได้.

## คู่มือการดำเนินการแบบขั้นตอน

### 1. สร้างและกำหนดค่า Index
คลาส `Index` เป็นอ็อบเจ็กต์ระดับบนสุดที่แทนที่คลังข้อมูลที่สามารถค้นหาได้และจัดเก็บบนดิสก์.

#### ภาพรวม
เราจะสร้างโฟลเดอร์บนดิสก์เพื่อเก็บไฟล์ดัชนี.

#### Code
```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/SearchForDifferentWordForms";
Index index = new Index(indexFolder);
```

*Explanation*: ตัวสร้าง `Index` ชี้ไปยังโฟลเดอร์ที่ข้อมูลดัชนีทั้งหมดจะถูกบันทึกไว้. แทนที่ `YOUR_DOCUMENT_DIRECTORY` ด้วยเส้นทางจริงบนเครื่องของคุณ.

### 2. วิธีการเพิ่มเอกสารลงในดัชนี
เมธอด `add` จะสแกนโฟลเดอร์แบบเรียกซ้ำ, ดึงข้อความ, และเก็บไว้ในดัชนี.

#### ภาพรวม
GroupDocs.Search สแกนไดเรกทอรีที่ระบุและทำดัชนีทุกไฟล์ที่รองรับที่พบ.

#### Code
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
index.add(documentsFolder);
```

*Explanation*: ตรวจสอบให้แน่ใจว่าเส้นทางถูกต้องและแอปพลิเคชันมีสิทธิ์อ่าน. เมธอดจะประมวลผลไฟล์เป็นชุดเพื่อรักษาการใช้หน่วยความจำให้ต่ำ.

### 3. กำหนดค่า Search Options สำหรับรูปแบบคำ
`SearchOptions` เก็บพารามิเตอร์ที่ควบคุมวิธีการประมวลผลคิวรี.

#### ภาพรวม
เราจะปรับ `SearchOptions` เพื่อเปิดการค้นหารูปแบบคำ (ฟัซซี่).

#### Code
```java
import com.groupdocs.search.SearchOptions;

SearchOptions options = new SearchOptions();
options.setUseWordFormsSearch(true); // Enables search for different grammatical variations of words.
```

*Explanation*: การตั้งค่า `setUseWordFormsSearch(true)` บอกเอ็นจินให้ขยายคิวรีเพื่อรวมรูปแบบคำที่รู้จัก, ปรับปรุงการครอบคลุมสำหรับรูปแบบเช่น “wish”, “wished”, และ “wishes”.

### 4. ดำเนินการค้นหา
`SearchResult` มีรายการเอกสารที่ตรงกันและส่วนย่อยของข้อความที่ดึงมา.

#### ภาพรวม
เราจะค้นหาคำว่า “wished” และดึงเอกสารที่ตรงกัน.

#### Code
```java
import com.groupdocs.search.SearchResult;

String query = "wished";
SearchResult result = index.search(query, options);
```

*Explanation*: เมธอด `search` รันคิวรีต่อเนื้อหาที่ทำดัชนีโดยใช้ตัวเลือกที่เรากำหนด. `SearchResult` ที่คืนค่ามีการอ้างอิงเอกสารและสแนปช็อตที่ไฮไลท์สำหรับแต่ละผลลัพธ์.

## ปัญหาทั่วไปและการแก้ไขข้อผิดพลาด
- **Incorrect paths** – ตรวจสอบ `indexFolder` และ `documentsFolder` อีกครั้งเพื่อหาข้อผิดพลาดและสิทธิ์การเข้าถึงที่เหมาะสม.  
- **Unsupported file formats** – ยืนยันว่าเอกสารของคุณอยู่ใน 50+ รูปแบบที่ระบุในเอกสาร GroupDocs.Search.  
- **Performance slowness** – สำหรับคอร์ปัสขนาดใหญ่, ทำดัชนีเป็นชุด, ตรวจสอบการใช้ heap ของ JVM, และเก็บดัชนีบน SSD.

## การประยุกต์ใช้งานจริง
1. **Corporate Document Management** – ค้นหานโยบาย, สัญญา, หรือคู่มือ HR อย่างรวดเร็วในหลายพันไฟล์.  
2. **Legal Research** – ค้นหาคดีอ้างอิงแม้คำพูดไม่ตรงกัน, ด้วยการค้นหารูปแบบคำ.  
3. **E‑commerce Catalogs** – ให้ผู้ซื้อค้นหารายละเอียดสินค้าโดยใช้คำที่หลากหลาย, เพิ่มอัตราการแปลง.

## เคล็ดลับด้านประสิทธิภาพ
- ทำดัชนีใหม่เฉพาะเมื่อมีเอกสารใหม่เพิ่มหรือไฟล์เดิมเปลี่ยนแปลง.  
- ใช้แฟล็ก `-Xmx` ของ Java เพื่อจัดสรร heap เพียงพอสำหรับดัชนีขนาดใหญ่ (เช่น `-Xmx4g`).  
- เรียก `index.optimize()` เป็นระยะ (หากมี) เพื่อบีบอัดไฟล์ดัชนีและลด I/O ของดิสก์.

## สรุป
คุณได้เรียนรู้วิธี **add documents to index**, เปิดใช้การค้นหาแบบฟัซซี่ใน Java, และปรับจูน GroupDocs.Search for Java. เทคนิคเหล่านี้ช่วยให้คุณสร้างประสบการณ์การค้นหาที่ตอบสนองเร็วและมีคุณลักษณะครบถ้วนสำหรับคอลเลกชันเอกสารใด ๆ.

### ขั้นตอนต่อไป
- ทดลองจับคู่แบบฟัซซี่และการจัดอันดับแบบกำหนดเอง.  
- ผสานโมดูลการค้นหาเข้ากับ REST API เพื่อให้ส่วนหน้าใช้งาน.  
- สำรวจการสนับสนุนหลายภาษาโดยกำหนดตัววิเคราะห์เฉพาะภาษา.

## คำถามที่พบบ่อย

**Q1: GroupDocs.Search รองรับรูปแบบไฟล์อะไรบ้าง?**  
A1: รองรับกว่า 50 รูปแบบรวมถึง DOCX, PDF, PPTX, XLSX, TXT, HTML, และรูปภาพทั่วไป. ดูเอกสารอย่างเป็นทางการสำหรับรายการเต็ม.

**Q2: จะอัปเดตดัชนีด้วยเอกสารใหม่อย่างไร?**  
A2: เรียก `index.add(newDocumentsFolder)` อีกครั้ง; ไลบรารีจะเพิ่มเฉพาะไฟล์ใหม่หรือที่เปลี่ยนแปลง, ไม่กระทบรายการที่มีอยู่.

**Q3: สามารถปรับแต่งคิวรีการค้นหาเพิ่มเติมได้หรือไม่?**  
A3: ได้—`SearchOptions` มีตัวเลือกสำหรับการค้นหาแบบฟัซซี่, ความไวต่อขนาดอักษร, การแบ่งหน้าผลลัพธ์, และอัลกอริทึมการจัดอันดับแบบกำหนดเอง.

**Q4: การค้นหาของฉันช้า—ทำอย่างไร?**  
A4: เก็บดัชนีบน SSD ที่เร็ว, เพิ่มขนาด heap ของ JVM (`-Xmx`), และหลีกเลี่ยงการทำดัชนีไฟล์ขนาดใหญ่ที่ไม่จำเป็น. เปิดใช้การค้นหารูปแบบคำเฉพาะเมื่อจำเป็น.

**Q5: จะหาชุมชนช่วยเหลือได้จากที่ไหน?**  
A5: ใช้ฟอรั่มสนับสนุนอย่างเป็นทางการ: [GroupDocs Support Forum](https://forum.groupdocs.com/c/search/10).

**อัปเดตล่าสุด:** 2026-05-22  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง

- [GroupDocs.Search Java - การค้นหาช่วงวันที่และคุณลักษณะขั้นสูง](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [วิธีเพิ่มคำพ้องความหมายใน Java ด้วย GroupDocs.Search – คู่มือฉบับสมบูรณ์](/search/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/)
- [เพิ่มเอกสารลงในดัชนีด้วยการค้นหาแบบแบ่งส่วนใน Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)
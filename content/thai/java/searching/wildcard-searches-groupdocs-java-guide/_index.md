---
date: '2026-03-23'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและปรับแต่งดัชนีการค้นหาด้วย GroupDocs.Search
  สำหรับ Java เพื่อเปิดใช้งานการค้นหาแบบไวล์การ์ดที่ทรงพลัง
keywords:
- wildcard searches in Java
- text-based wildcard search
- object-based wildcard search
title: เพิ่มเอกสารลงในดัชนี – การค้นหาแบบไวล์การ์ดใน Java
type: docs
url: /th/java/searching/wildcard-searches-groupdocs-java-guide/
weight: 1
---

# เพิ่มเอกสารลงในดัชนี – การใช้การค้นหา Wildcard อย่างชำนาญใน Java กับ GroupDocs.Search

ปลดล็อกพลังของการค้นหา wildcard แบบข้อความและแบบอ็อบเจ็กต์โดยใช้ GroupDocs.Search สำหรับ Java ในคู่มือนี้คุณจะได้เรียนรู้วิธี **add documents to index**, กำหนดรูปแบบขั้นสูง, และทำให้ดัชนีการค้นหาของคุณได้รับการปรับให้เหมาะสมสำหรับผลลัพธ์ที่รวดเร็ว.

## คำตอบอย่างรวดเร็ว
- **“add documents to index” หมายถึงอะไร?** มันสร้างโครงสร้างข้อมูลที่สามารถค้นหาได้ซึ่ง GroupDocs.Search สามารถสืบค้นได้อย่างมีประสิทธิภาพ.  
- **คีย์เวิร์ดใดที่ช่วยเพิ่มประสิทธิภาพ?** การใช้รูปแบบ wildcard ที่กระชับและดำเนินการ **optimize search index** อย่างสม่ำเสมอ.  
- **ฉันต้องการการตั้งค่าหน่วยความจำพิเศษหรือไม่?** ใช่—ตรวจสอบ **java search memory management** เพื่อหลีกเลี่ยงข้อผิดพลาด out‑of‑memory ในชุดข้อมูลขนาดใหญ่.  
- **ฉันสามารถใช้ฟีเจอร์เหล่านี้ในแอป Spring Boot ได้หรือไม่?** แน่นอน; เพียงแค่เพิ่ม Maven dependency และกำหนดค่าโฟลเดอร์ดัชนี.  
- **จำเป็นต้องมีไลเซนส์สำหรับการใช้งานในโปรดักชันหรือไม่?** จำเป็นต้องมีไลเซนส์ GroupDocs.Search ที่ถูกต้องสำหรับการใช้งานเชิงพาณิชย์.

## “add documents to index” คืออะไรใน GroupDocs.Search?
การเพิ่มเอกสารลงในดัชนีหมายถึงการป้อนไฟล์ต้นฉบับของคุณ (PDF, DOCX, TXT ฯลฯ) ไปยังคลังข้อมูลที่สามารถค้นหาได้ซึ่ง GroupDocs.Search สร้างขึ้นเบื้องหลัง เมื่อทำการจัดทำดัชนีแล้ว คุณสามารถรันการค้นหา wildcard อย่างรวดเร็วโดยไม่ต้องสแกนไฟล์ต้นฉบับทุกครั้ง.

## ทำไมต้องใช้การค้นหา wildcard กับ GroupDocs.Search?
การค้นหา wildcard ช่วยให้คุณจับคู่คำหรือรูปแบบบางส่วน—เหมาะสำหรับสถานการณ์ที่ผู้ใช้จำเพียงส่วนหนึ่งของคำเท่านั้น ความยืดหยุ่นนี้ช่วยปรับปรุงประสบการณ์ผู้ใช้ในระบบจัดการเอกสาร, พอร์ทัลเนื้อหา, และเครื่องมือ data‑mining.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK)** – เวอร์ชัน 8 หรือใหม่กว่า.  
- ความรู้พื้นฐานการเขียนโปรแกรม Java.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse.  
- Maven สำหรับการจัดการ dependencies (หรือคุณสามารถดาวน์โหลด JAR โดยตรง).  

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การตั้งค่า Maven
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
หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
- **Free Trial:** ทดลองใช้ฟีเจอร์หลักโดยไม่มีค่าใช้จ่าย.  
- **Temporary License:** เปิดใช้งานความสามารถขั้นสูงในช่วงการประเมิน.  
- **Purchase:** ซื้อไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในโปรดักชัน.

## คู่มือการใช้งาน

### ฟีเจอร์ 1: การค้นหา Wildcard แบบข้อความ

#### ขั้นตอนที่ 1 – ตั้งค่าดัชนีและ **add documents to index**
แรก, สร้างโฟลเดอร์ดัชนีและเพิ่มเอกสารต้นฉบับของคุณ:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInTextForm";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### ขั้นตอนที่ 2 – ดำเนินการค้นหา Wildcard
รันการค้นหาแบบใช้รูปแบบโดยตรงบนข้อความ:

```java
// Search for words matching 'm???is'
String query1 = "m???is";
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Search for words matching 'pri?(1~7)'
String query2 = "pri?(1~7)";
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**คำอธิบาย**  
- `indexFolder` เก็บดัชนีที่สามารถค้นหาได้บนดิสก์.  
- `documentsFolder` ชี้ไปยังตำแหน่งของไฟล์ที่คุณต้องการ **add documents to index**.  
- `search()` ทำการดำเนินการค้นหา wildcard และคืนผลลัพธ์ที่ตรงกัน.

### ฟีเจอร์ 2: การค้นหา Wildcard แบบอ็อบเจ็กต์

#### ขั้นตอนที่ 1 – ตั้งค่าดัชนี (เช่นเดียวกับก่อนหน้า)
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\AdvancedUsage\\Searching\\WildcardSearch\\QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

#### ขั้นตอนที่ 2 – สร้าง `WordPattern` สำหรับการค้นหาที่ซับซ้อน
การค้นหาแบบอ็อบเจ็กต์ให้คุณควบคุมแต่ละองค์ประกอบของรูปแบบอย่างละเอียด:

```java
// Create a WordPattern for 'm???is'
WordPattern pattern1 = new WordPattern();
pattern1.appendString("m");
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendOneCharacterWildcard();
pattern1.appendString("is");

SearchQuery query1 = SearchQuery.createWordPatternQuery(pattern1);
SearchResult result1 = index.search(query1); // Finds words like 'mauris', 'mollis'

// Create a WordPattern for 'pri?(1~7)'
WordPattern pattern2 = new WordPattern();
pattern2.appendString("pri");
pattern2.appendWildcard(1, 7);

SearchQuery query2 = SearchQuery.createWordPatternQuery(pattern2);
SearchResult result2 = index.search(query2); // Finds words like 'private', 'principles'
```

**คำอธิบาย**  
- `WordPattern` ให้คุณประกอบรูปแบบการค้นหาแบบขั้นตอนต่อขั้นตอน.  
- `appendOneCharacterWildcard()` เพิ่มตัวแทน `?`.  
- `appendWildcard(min, max)` เพิ่ม wildcard แบบช่วง (`?(min~max)`).  

## การประยุกต์ใช้งานจริง
1. **Document Management:** ค้นหาไฟล์ได้อย่างรวดเร็วเมื่อรู้เพียงส่วนหนึ่งของคำ.  
2. **Content Retrieval Engines:** ให้พลังกับแถบค้นหาในแพลตฟอร์ม CMS ด้วยการจับคู่ที่ยืดหยุ่น.  
3. **Data Mining:** สกัดข้อมูลที่มีรูปแบบจากคอร์ปัสขนาดใหญ่โดยไม่ต้องสแกนข้อความทั้งหมด.

## ข้อควรพิจารณาด้านประสิทธิภาพ

### ปรับปรุงดัชนีการค้นหา
- **Regular Re‑indexing:** หลังจากการอัปเดตเป็นจำนวนมาก ให้สร้างดัชนีใหม่เพื่อให้เวลาการค้นหาต่ำ.  
- **Compact Storage:** ใช้ `index.optimize()` (หากมี) เพื่อลดขนาดดัชนี.

### การจัดการหน่วยความจำการค้นหา Java
- **Heap Size:** จัดสรร heap เพียงพอ (`-Xmx2g` หรือมากกว่า) สำหรับชุดเอกสารขนาดใหญ่.  
- **Streaming Indexing:** ประมวลผลไฟล์เป็นชุดเพื่อหลีกเลี่ยงการโหลดทุกอย่างเข้าสู่หน่วยความจำพร้อมกัน.

### แนวทางปฏิบัติที่ดีที่สุดทั่วไป
- ทำให้รูปแบบ wildcard มีความเฉพาะเจาะจงที่สุด; รูปแบบที่กว้างเกินไปจะเพิ่มภาระ CPU.  
- ตรวจสอบการหยุดทำงานของ GC หากคุณสังเกตเห็นการกระตุ้นความหน่วงเวลาขณะทำงานค้นหาที่หนัก.

## สรุป
โดยการเรียนรู้วิธี **add documents to index** และใช้การค้นหา wildcard ทั้งแบบข้อความและแบบอ็อบเจ็กต์ คุณสามารถปรับปรุงประสบการณ์การค้นหาในแอปพลิเคชัน Java ใด ๆ ได้อย่างมาก จำไว้ว่าให้ **optimize search index** อย่างสม่ำเสมอและจัดการหน่วยความจำอย่างชาญฉลาดเพื่อประสิทธิภาพที่สามารถขยายได้ ทดลองใช้รูปแบบต่าง ๆ ผสานโค้ดเข้ากับบริการของคุณ และสนุกกับผลลัพธ์การค้นหาที่เร็วและยืดหยุ่นวันนี้!

## คำถามที่พบบ่อย

**Q1: การค้นหา wildcard คืออะไร?**  
A: การค้นหา wildcard ช่วยให้คุณจับคู่คำหรือวลีโดยใช้ตัวแทนเช่น `?` (อักขระเดียว) หรือ `*` (หลายอักขระ).

**Q2: ฉันจะติดตั้ง GroupDocs.Search สำหรับ Java อย่างไร?**  
A: ใช้ Maven พร้อม repository และ dependency ที่แสดงข้างต้น หรือดาวน์โหลด JAR โดยตรงจากหน้ารปล่อยอย่างเป็นทางการ.

**Q3: การค้นหา wildcard สามารถจัดการกับชุดข้อมูลขนาดใหญ่ได้หรือไม่?**  
A: ได้, แต่คุณควร **optimize search index** และตรวจสอบ **java search memory management** เพื่อรักษาประสิทธิภาพ.

**Q4: ข้อผิดพลาดทั่วไปคืออะไร?**  
A: เส้นทางดัชนีที่ไม่ถูกต้อง, การใช้ wildcard ที่กว้างเกินไป, และการละเลยการตั้งค่าหน่วยความจำสามารถทำให้การค้นหาช้า หรือเกิดข้อผิดพลาด out‑of‑memory.

**Q5: ฉันจะหาแหล่งข้อมูลเพิ่มเติมได้จากที่ไหน?**  
A: เยี่ยมชม [GroupDocs documentation](https://docs.groupdocs.com/search/java/) เพื่อดูคู่มือโดยละเอียดและอ้างอิง API.

## แหล่งข้อมูล

- **Documentation:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference:** [GroupDocs Search API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [GroupDocs.Search Downloads](https://releases.groupdocs.com/search/java/)
- **GitHub:** [GroupDocs.Search on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**อัปเดตล่าสุด:** 2026-03-23  
**ทดสอบกับ:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs
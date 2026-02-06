---
date: '2026-02-06'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและเปิดใช้งานการค้นหาที่แยกแยะตัวพิมพ์ใหญ่‑เล็กใน
  Java ด้วย GroupDocs.Search เพื่อเพิ่มความแม่นยำของแอปพลิเคชันของคุณ
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'เพิ่มเอกสารลงในดัชนี: การค้นหา Java ที่แยกแยะตัวพิมพ์ใหญ่‑เล็กด้วย GroupDocs'
type: docs
url: /th/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# เพิ่มเอกสารลงในดัชนี: การเชี่ยวชาญการค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็กใน Java ด้วย GroupDocs

การดึงข้อมูลที่ต้องการจากคอลเลกชันเอกสารขนาดมหาศาลเป็นความต้องการหลักของแอปพลิเคชันสมัยใหม่ ในคู่มือนี้คุณจะได้เรียนรู้ **วิธีเพิ่มเอกสารลงในดัชนี** และทำ **การค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็ก** ด้วย GroupDocs.Search สำหรับ Java ไม่ว่าคุณจะกำลังสร้างคลังเอกสารทางกฎหมาย, แคตาล็อกอี‑คอมเมิร์ซ หรือระบบจัดการเนื้อหา ผลการค้นหาที่แม่นยำจะทำให้ผู้ใช้พอใจและข้อมูลของคุณเชื่อถือได้

## Quick Answers
- **ขั้นตอนแรกที่สำคัญในการเริ่มการค้นหาคืออะไร?** เพิ่มเอกสารลงในดัชนีด้วย `index.add(...)`  
- **จะเปิดใช้งานการค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็กอย่างไร?** ตั้งค่า `options.setUseCaseSensitiveSearch(true)`  
- **ฉันสามารถค้นหาข้ามหลายไดเรกทอรีได้หรือไม่?** ได้ – เรียก `index.add()` สำหรับแต่ละโฟลเดอร์ที่ต้องการรวม  
- **เมธอดใดที่ให้ฉันค้นหาด้วยอ็อบเจกต์?** ใช้ `SearchQuery.createWordQuery(...)`  
- **ต้องการไลเซนส์สำหรับการทดสอบหรือไม่?** มีไลเซนส์ชั่วคราวให้ใช้สำหรับการทดลอง

## What does “add documents to index” mean?
การเพิ่มเอกสารลงในดัชนีหมายถึงการป้อนไฟล์ต้นทางของคุณ (PDF, Word, ข้อความธรรมดา ฯลฯ) เข้าไปใน GroupDocs.Search เพื่อให้ระบบสร้างโครงสร้างข้อมูลที่สามารถค้นหาได้ เมื่อทำการจัดทำดัชนีแล้วเอนจินจะสามารถดำเนินการค้นหาอย่างรวดเร็ว รวมถึงการค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็กด้วย

## Why enable case‑sensitive search in Java?
- **การจับคู่คำอย่างแม่นยำ** – แยกความแตกต่างระหว่าง “Apple” (บริษัท) กับ “apple” (ผลไม้)  
- **การปฏิบัติตามกฎระเบียบ** – บางอุตสาหกรรมต้องการการจับคู่วลีอย่างแม่นยำ  
- **ความเกี่ยวข้องที่ดีขึ้น** – ผู้ใช้มักคาดหวังผลลัพธ์ที่แยกตามตัวพิมพ์ในบริบททางเทคนิคหรือกฎหมาย

## Prerequisites
- JDK (แนะนำ Java 17 หรือใหม่กว่า)  
- Maven สำหรับการจัดการ dependencies  
- IDE เช่น IntelliJ IDEA หรือ Eclipse  
- ความคุ้นเคยพื้นฐานกับการเขียนโปรแกรม Java  

## Setting Up GroupDocs.Search for Java
ก่อนอื่นให้เพิ่มรีโพสิตอรีของ GroupDocs และ dependency ลงใน `pom.xml` ของคุณ:

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

หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)  

### Licensing
เพื่อเริ่มต้นด้วยรุ่นทดลอง ให้ไปที่ GroupDocs เพื่อรับไลเซนส์ชั่วคราว ซึ่งจะทำให้คุณทดสอบฟีเจอร์ทั้งหมดโดยไม่มีข้อจำกัดใด ๆ  

## How to add documents to index – Text Query Search

### Step 1: Create an Index and add your documents
สร้างโฟลเดอร์ที่ไฟล์ดัชนีจะถูกเก็บไว้ แล้วเพิ่มไดเรกทอรีต้นทางที่มีเอกสารที่คุณต้องการค้นหา

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **เคล็ดลับ:** คุณสามารถเรียก `index.add()` หลายครั้งเพื่อ **ค้นหาข้ามหลายไดเรกทอรี** ในดัชนีเดียวได้  

### Step 2: Enable case‑sensitive search
กำหนดค่าตัวเลือกการค้นหาให้คำนึงถึงการใช้ตัวพิมพ์ใหญ่‑เล็ก

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Step 3: Execute a case‑sensitive text query
รันคิวรีที่แยกความแตกต่างระหว่าง “Advantages” กับ “advantages”

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

ลูปนี้จะแสดงพาธเต็มของแต่ละเอกสารที่มีคำที่ตรงกับตัวพิมพ์อย่างแม่นยำ

## How to add documents to index – Object Query Search

Object queries ให้ความยืดหยุ่นมากขึ้น โดยเฉพาะเมื่อคุณต้องการรวมหลายเงื่อนไขเข้าด้วยกัน

### Step 1: Initialize a second index (optional)
หากต้องการแยกการค้นหาแบบอ็อบเจกต์ออกจากกัน ให้สร้างโฟลเดอร์ดัชนีอีกอันหนึ่ง

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Step 2: Re‑use the case‑sensitive option
อินสแตนซ์ `SearchOptions` เดียวกันสามารถใช้กับการค้นหาแบบอ็อบเจกต์ได้

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Step 3: Build and run an object query
สร้างอ็อบเจกต์ word query แล้วส่งให้เอนจินค้นหา

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

การใช้ `createWordQuery` ทำให้คุณสามารถต่อมาผสานกับ phrase, wildcard หรือ Boolean query เพื่อสร้างสถานการณ์ที่ซับซ้อนได้  

## Practical Applications
- **การจัดการเอกสารทางกฎหมาย:** ดึงกฎหมายหรือข้อบังคับที่ต้องแยกตามตัวพิมพ์ใหญ่‑เล็ก  
- **แพลตฟอร์มอี‑คอมเมิร์ซ:** แยก SKU ของสินค้าเช่น “PRO‑X” กับ “pro‑x”  
- **ระบบจัดการเนื้อหา (CMS):** ทำให้ผู้เขียนค้นหาหัวข้อหรือแท็กที่ตรงกันได้อย่างแม่นยำ  

## Performance Considerations
- **รักษาดัชนีให้เป็นปัจจุบัน** – ทำการ re‑index เมื่อไฟล์ใหม่ถูกเพิ่มหรือไฟล์เดิมมีการเปลี่ยนแปลง  
- **ตรวจสอบการใช้หน่วยความจำ** – คอลเลกชันขนาดใหญ่จะได้ประโยชน์จากการทำดัชนีแบบ incremental และการกำหนดขนาด heap ของ JVM อย่างเหมาะสม  
- **ใช้ประโยชน์จาก garbage collector ของ Java** – ปล่อยอ็อบเจกต์ `Index` เมื่อไม่ต้องการใช้งานแล้ว  

## Common Issues and Solutions
| Issue | Solution |
|-------|----------|
| `useCaseSensitiveSearch` appears ignored | ตรวจสอบว่าคุณใช้เวอร์ชันล่าสุดของ GroupDocs.Search และว่าดัชนีถูกสร้างใหม่หลังจากเปลี่ยนตัวเลือกนี้ |
| No results returned for a known term | ตรวจสอบว่าตัวพิมพ์ของคำตรงกับที่จัดทำดัชนีอย่างแม่นยำและว่าเอกสารถูกเพิ่มลงในดัชนีสำเร็จ |
| Searching many folders slows down | เพิ่มแต่ละโฟลเดอร์แยกกันด้วย `index.add()` และพิจารณาแบ่งดัชนีเป็น shards สำหรับชุดข้อมูลขนาดใหญ่มาก |

## Frequently Asked Questions

**Q:** ฉันจะจัดการกับชุดข้อมูลขนาดใหญ่ด้วย GroupDocs.Search อย่างไร?  
**A:** ใช้การแบ่งพาร์ทิชันของดัชนี ปรับแต่งการตั้งค่า memory ของ JVM และทำการ compact ดัชนีเป็นระยะเพื่อรักษาประสิทธิภาพให้สูงสุด  

**Q:** ฉันสามารถค้นหาข้ามหลายไดเรกทอรีพร้อมกันได้หรือไม่?  
**A:** ได้ – เรียก `index.add()` สำหรับแต่ละไดเรกทอรีที่ต้องการรวม แล้วรันคิวรีเดียวบนดัชนีที่รวมกันแล้ว  

**Q:** ปัญหาที่พบบ่อยเมื่อตั้งค่าการค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็กคืออะไร?  
**A:** ลืมทำการสร้างดัชนีใหม่หลังจากเปิดใช้งาน `useCaseSensitiveSearch` หรือใช้ตัวพิมพ์ผิดในสตริงคิวรี  

**Q:** ฉันจะแก้ไขข้อผิดพลาดการค้นหาอย่างไร?  
**A:** ตรวจสอบไฟล์บันทึกที่ GroupDocs.Search สร้างขึ้นเพื่อดู stack trace และยืนยันว่า dependencies ของ Maven ทั้งหมดถูก resolve อย่างถูกต้อง  

**Q:** GroupDocs.Search เหมาะกับแอปพลิเคชันแบบเรียล‑ไทม์หรือไม่?  
**A:** ด้วยกลยุทธ์การทำดัชนีที่เหมาะสม (การอัปเดตแบบ incremental และการแคชในหน่วยความจำ) สามารถให้ผลลัพธ์การค้นหาใกล้เคียงกับเรียล‑ไทม์ได้  

## Resources
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [Java API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**Last Updated:** 2026-02-06  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs  

---
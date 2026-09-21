---
date: '2026-09-21'
description: เรียนรู้วิธีสร้าง java full text search index ด้วย GroupDocs.Search,
  เพิ่ม documents, และเปิดใช้งานการสนับสนุน homophone เพื่อผลลัพธ์ที่แม่นยำยิ่งขึ้น
keywords:
- java full text search
- homophone search java
- GroupDocs.Search Java
- document indexing java
- search index java
lastmod: '2026-09-21'
og_description: ค้นพบวิธีสร้าง java full text search index ด้วย GroupDocs.Search,
  เพิ่ม documents, และเปิดใช้งานการสนับสนุน homophone เพื่อการค้นหาที่เร็วขึ้นและแม่นยำยิ่งขึ้น
og_image_alt: Illustration of a Java full text search index with homophone support
og_title: วิธีสร้าง java full text search index ด้วย homophones
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  headline: How to build a java full text search index with homophones
  type: TechArticle
- description: Learn how to create a java full text search index using GroupDocs.Search,
    add documents, and enable homophone support for more accurate results.
  name: How to build a java full text search index with homophones
  steps:
  - name: '**Install via Maven** or download directly from the provided links.'
    text: '**Install via Maven** or download directly from the provided links.'
  - name: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Acquire a license:** You can start with a free trial or obtain a temporary
      license by visiting [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
    text: '**Initialize the library:** The snippet below shows the minimal code required
      to start using GroupDocs.Search.'
  - name: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
    text: '**Legal document management:** Distinguish between similar‑sounding legal
      terms such as “lease” vs. “least”.'
  - name: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
    text: '**Educational content creation:** Ensure teaching materials are free from
      ambiguous wording that could confuse learners.'
  - name: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
    text: '**Customer support systems:** Improve knowledge‑base search accuracy, helping
      agents locate the right articles faster.'
  type: HowTo
- questions:
  - answer: A data structure that enables fast full‑text search across documents.
    question: What is a search index?
  - answer: It improves recall by matching words that sound alike, e.g., “mail” vs.
      “male”.
    question: Why use homophone recognition?
  - answer: GroupDocs.Search for Java (v25.4).
    question: Which library provides this in Java?
  - answer: A free trial works for evaluation; a permanent license is required for
      production.
    question: Do I need a license?
  - answer: JDK 8 or higher.
    question: What Java version is required?
  type: FAQPage
tags:
- java full text search
- homophone search
- GroupDocs.Search
- document indexing
- search index
title: วิธีสร้าง java full text search index ด้วย homophones
type: docs
url: /th/java/document-management/groupdocs-search-java-homophone-document-management-guide/
weight: 1
---

# วิธีสร้างดัชนีการค้นหาข้อความเต็มของ Java พร้อมการสนับสนุนคำพ้องเสียง

ในคู่มือนี้คุณจะได้เรียนรู้วิธีสร้างดัชนี **java full text search** ด้วย GroupDocs.Search, เพิ่มเอกสารลงในดัชนี, และเปิดใช้งานการสนับสนุนคำพ้องเสียงเพื่อให้การค้นหาเข้าใจคำที่ออกเสียงคล้ายกัน เมื่อจบบทเรียนคุณจะมีดัชนีที่เร็วและรับรู้ภาษา สามารถสืบค้นได้ในระดับมิลลิวินาที ทำให้แอปพลิเคชันของคุณเป็นมิตรต่อผู้ใช้และแม่นยำยิ่งขึ้น.

## คำตอบสั้น
- **อะไรคือ search index?** โครงสร้างข้อมูลที่ทำให้การค้นหา full‑text อย่างรวดเร็วทั่วเอกสารเป็นไปได้.  
- **ทำไมต้องใช้การจดจำคำพ้องเสียง?** ช่วยเพิ่มการเรียกคืนโดยจับคู่คำที่ออกเสียงคล้ายกัน เช่น “mail” กับ “male”.  
- **ไลบรารีใดที่ให้ฟีเจอร์นี้ใน Java?** GroupDocs.Search for Java (v25.4).  
- **ต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีเพียงพอสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง.  
- **ต้องการเวอร์ชัน Java อะไร?** JDK 8 หรือสูงกว่า.

## java full text search คืออะไร?
`java full text search` คือกระบวนการทำดัชนีเนื้อหาเอกสารเพื่อให้คุณสามารถสืบค้นข้อความได้อย่างรวดเร็วและดึงไฟล์ที่เกี่ยวข้องในเวลาจริง ดัชนีจะเก็บคำที่แยกโทเคน, ตำแหน่ง, และเมตาดาต้า ทำให้การตอบสนองการค้นหาเป็นระดับมิลลิวินาทีแม้ในคอลเลกชันขนาดใหญ่.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
GroupDocs.Search รองรับ **ไฟล์ฟอร์แมตกว่า 50 ประเภท** เช่น PDF, DOCX, XLSX, PPTX, และ HTML พร้อมกับพจนานุกรมคำพ้องเสียงในตัวที่เพิ่มการเรียกคืนได้สูงถึง **30 %** สำหรับคำที่มีความหมายหลายแบบ API แยกความซับซ้อนของการทำดัชนีระดับต่ำ ทำให้คุณโฟกัสที่ตรรกะธุรกิจได้ นอกจากนี้ยังมีการผสานรวมง่ายกับโครงการ Maven และเอกสารที่ชัดเจนสำหรับการพัฒนาอย่างรวดเร็ว.

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะลงลึกในโค้ด โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- **GroupDocs.Search for Java** (สามารถดาวน์โหลดผ่าน Maven หรือดาวน์โหลดโดยตรง).  
- JDK **ที่เข้ากันได้** (8 หรือใหม่กว่า).  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**.  
- ความรู้พื้นฐานเกี่ยวกับ Java และ Maven.

### ไลบรารีและการพึ่งพาที่จำเป็น
คุณจะต้องใช้ GroupDocs.Search for Java. รวมเข้าด้วย Maven หรือดาวน์โหลดโดยตรง.

**การติดตั้งด้วย Maven:**  
เพิ่มโค้ดต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

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

**ดาวน์โหลดโดยตรง:**  
หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
ตรวจสอบว่าคุณได้ติดตั้ง JDK ที่เข้ากันได้ (JDK 8 หรือสูงกว่า) และตั้งค่า IDE เช่น IntelliJ IDEA หรือ Eclipse บนเครื่องของคุณแล้ว.

### ความรู้เบื้องต้นที่จำเป็น
ความคุ้นเคยกับแนวคิดการเขียนโปรแกรม Java และประสบการณ์การใช้ Maven สำหรับการจัดการการพึ่งพาจะเป็นประโยชน์ ความเข้าใจพื้นฐานเกี่ยวกับการทำดัชนีเอกสารและอัลกอริทึมการค้นหาก็ช่วยได้เช่นกัน.

## การตั้งค่า GroupDocs.Search สำหรับ Java
เมื่อจัดการข้อกำหนดเบื้องต้นเรียบร้อย การตั้งค่า GroupDocs.Search จะเป็นเรื่องง่าย:

1. **ติดตั้งผ่าน Maven** หรือดาวน์โหลดโดยตรงจากลิงก์ที่ให้ไว้.  
2. **รับไลเซนส์:** คุณสามารถเริ่มด้วยการทดลองใช้ฟรีหรือรับไลเซนส์ชั่วคราวโดยเยี่ยมชม [GroupDocs Purchase Page](https://purchase.groupdocs.com/temporary-license/).  
3. **เริ่มต้นไลบรารี:** โค้ดตัวอย่างด้านล่างแสดงโค้ดขั้นต่ำที่จำเป็นเพื่อเริ่มใช้ GroupDocs.Search.

```java
import com.groupdocs.search.*;

public class SetupExample {
    public static void main(String[] args) {
        // Define the directory for storing index files.
        String indexFolder = "path/to/index/directory";
        
        // Initialize an Index instance.
        Index index = new Index(indexFolder);
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## คู่มือการดำเนินการ
เมื่อสภาพแวดล้อมพร้อมแล้ว เรามาสำรวจฟีเจอร์หลักที่คุณต้องใช้เพื่อ **สร้างดัชนี java full text search** และจัดการคำพ้องเสียง.

### การสร้างและจัดการดัชนี
#### ภาพรวม
การสร้างดัชนีการค้นหาเป็นขั้นตอนแรกในการจัดการเอกสารอย่างมีประสิทธิภาพ ซึ่งทำให้สามารถดึงข้อมูลได้อย่างรวดเร็วตามเนื้อหาเอกสารของคุณ.

#### ขั้นตอนการสร้างดัชนี
**ขั้นตอน 1:** ระบุไดเรกทอรีสำหรับไฟล์ดัชนีของคุณ.

```java
String indexFolder = "YOUR_INDEX_DIRECTORY";
Index index = new Index(indexFolder);
```

`คลาส Index` แสดงถึงคอนเทนเนอร์ที่สามารถค้นหาได้ซึ่งเก็บคำที่แยกโทเคนและเมตาดาต้าของแต่ละเอกสาร ให้โครงสร้างหลักที่ทำให้การดำเนินการค้นหาเร็วและการจัดเก็บข้อมูลเอกสารอย่างมีประสิทธิภาพทั่วดัชนีทั้งหมด.

**ขั้นตอน 2:** เพิ่มเอกสารจากโฟลเดอร์ที่ระบุลงในดัชนีนี้.

```java
String documentsFolder = "YOUR_DOCUMENTS_SOURCE_DIRECTORY";
index.add(documentsFolder);
System.out.println("Documents added to the index.");
```

การเรียก `index.add()` จะทำการนำเข้าแต่ละไฟล์, ดึงข้อความ, และเติมโครงสร้างภายในที่จำเป็นสำหรับการสืบค้นอย่างรวดเร็ว ทำให้ทุกเอกสารถูกทำดัชนีอย่างเต็มที่และสามารถค้นหาได้ทันทีโดยไม่ต้องมีขั้นตอนการประมวลผลแยก.

### วิธีเพิ่มเอกสารลงในดัชนี
คุณสามารถเพิ่มไฟล์เพิ่มเติมในภายหลังโดยโปรแกรมโดยเรียก `index.add()` อีกครั้งพร้อมกับเส้นทางโฟลเดอร์ใหม่หรือเส้นทางไฟล์เดี่ยว วิธีการเพิ่มแบบเพิ่มขั้นนี้ทำให้ดัชนีอัปเดตอยู่เสมอโดยไม่ต้องสร้างใหม่ทั้งหมด การเพิ่มเอกสารแบบนี้ช่วยให้คุณรักษาดัชนีแบบสดที่สะท้อนการเปลี่ยนแปลงเนื้อหาล่าสุด รองรับการค้นหาอย่างต่อเนื่องสำหรับผู้ใช้ปลายทางและลดเวลาหยุดทำงานที่เกี่ยวข้องกับการทำดัชนีใหม่เป็นชุด.

### การดึงคำพ้องเสียงสำหรับคำ
การดึงคำพ้องเสียงสำหรับคำเฉพาะช่วยให้เครื่องมือค้นหาพิจารณาการสะกดที่เป็นทางเลือกที่ออกเสียงเดียวกัน เพิ่มการเรียกคืนสำหรับคำค้นที่ผู้ใช้อาจพิมพ์ผิดหรือใช้รูปแบบต่าง ๆ โดยการขยายคำค้นด้วยคำที่มีเสียงเดียวกัน เครื่องมือสามารถจับคู่เอกสารที่มีรูปแบบพ้องเสียงใด ๆ ทำให้ผลลัพธ์ครอบคลุมมากขึ้น.

*คลาส `HomophoneDictionary` เก็บกลุ่มคำที่มีการออกเสียงเดียวกัน ทำหน้าที่เป็นคลังศูนย์กลางที่เครื่องมือค้นหาอ้างอิงเมื่อขยายคำค้นด้วยทางเลือกทางเสียง ซึ่งช่วยเพิ่มความเกี่ยวข้องของผลลัพธ์การค้นหา.*

```java
String[] homophones = index.getDictionaries().getHomophoneDictionary().getHomophones("braid");
```

### การดึงกลุ่มคำพ้องเสียง
การจัดกลุ่มคำพ้องเสียงให้วิธีการจัดการคำที่มีหลายความหมายอย่างเป็นระบบ ทำให้นักพัฒนาสามารถดึงชุดเต็มของคำที่มีเสียงเดียวกันในหนึ่งการดำเนินการ ซึ่งมีประโยชน์สำหรับการวิเคราะห์, การจัดการพจนานุกรมแบบกำหนดเอง, หรือการอัปเดตรายการพ้องเสียงเป็นจำนวนมาก.

*แต่ละกลุ่มที่ `getGroups()` คืนค่ามีคำที่สามารถสลับกันได้ในการค้นหาแบบเสียง, และเมธอดนี้ให้คอลเลกชันที่ครอบคลุมของกลุ่มเหล่านี้เพื่อให้คุณตรวจสอบ, แก้ไข, หรือส่งออกชุดเต็มของความสัมพันธ์พ้องเสียงที่พจนานุกรมดูแล.*

```java
String[][] groups = index.getDictionaries().getHomophoneDictionary().getHomophoneGroups("braid");
```

### การลบพจนานุกรมคำพ้องเสียง
การลบรายการที่ล้าสมัยหรือไม่จำเป็นทำให้พจนานุกรมของคุณยังคงเกี่ยวข้องและไม่ทำให้ผลการค้นหามีเสียงรบกวน การดำเนินการนี้มักทำเมื่อคุณต้องการรีเซ็ตพจนานุกรมกลับสู่สถานะเริ่มต้นก่อนโหลดชุดกำหนดเองใหม่.

*เมธอด `clear()` จะลบรายการกำหนดเองทั้งหมด, คืนค่าเป็นชุดเริ่มต้น, และรับประกันว่ากลุ่มพ้องเสียงที่เพิ่มไว้ก่อนหน้านี้จะถูกลบอย่างสมบูรณ์ ทำให้มีพื้นฐานสะอาดสำหรับการกำหนดค่าพจนานุกรมต่อไป.*

```java
if (index.getDictionaries().getHomophoneDictionary().getCount() > 0) {
    index.getDictionaries().getHomophoneDictionary().clear();
}
System.out.println("Homophone dictionary cleared.");
```

### การเพิ่มคำพ้องเสียงลงในพจนานุกรม
การปรับแต่งพจนานุกรมคำพ้องเสียงของคุณทำให้สามารถค้นหาได้ตามความต้องการที่สะท้อนคำศัพท์เฉพาะโดเมน, สแลง, หรือชื่อแบรนด์ โดยการเพิ่มกลุ่มใหม่ คุณสามารถทำให้การค้นหาตระหนักถึงความสัมพันธ์ทางเสียงที่เฉพาะเจาะจงกับแอปพลิเคชันของคุณ.

*ใช้ `addGroup()` เพื่อแทรกรายการของคำที่มีเสียงเหมือนกัน, เพิ่มการเรียกคืนสำหรับคำศัพท์เฉพาะโดเมน, และเมธอดจะตรวจสอบความถูกต้องของแต่ละรายการเพื่อป้องกันการซ้ำซ้อนพร้อมผสานกลุ่มใหม่เข้าสู่โครงสร้างพจนานุกรมที่มีอยู่อย่างราบรื่น.*

```java
String[][] homophoneGroups = {
    new String[] { "awe", "oar", "or", "ore" },
    new String[] { "aye", "eye", "i" },
    new String[] { "call", "caul" }
};
index.getDictionaries().getHomophoneDictionary().addRange(homophoneGroups);
System.out.println("Homophones added to the dictionary.");
```

### การส่งออกและนำเข้าพจนานุกรมคำพ้องเสียง
การส่งออกและนำเข้าพจนานุกรมสามารถเป็นประโยชน์สำหรับการสำรองหรือการย้ายข้อมูล ทำให้คุณสามารถเก็บการกำหนดค่ากำหนดเองข้ามสภาพแวดล้อมหรือแชร์กับทีมได้ ฟังก์ชันนี้รองรับรูปแบบ JSON เพื่อความอ่านง่ายและการผสานรวมกับเครื่องมืออื่น.

*เมธอดเหล่านี้ทำให้คุณบันทึกพจนานุกรมกำหนดเองเป็นไฟล์ JSON เพื่อการใช้ซ้ำง่าย, กระบวนการส่งออกบันทึกสถานะเต็มของพจนานุกรม, ส่วนขั้นตอนนำเข้าจะตรวจสอบโครงสร้าง JSON ก่อนนำไปใช้กับอินสแตนซ์พจนานุกรมที่ทำงานอยู่.*

```java
String fileName = "path/to/exported/dictionary.file";
index.getDictionaries().getHomophoneDictionary().exportDictionary(fileName);
```

**ขั้นตอน 2:** นำเข้าจากไฟล์ใหม่หากจำเป็น.

```java
index.getDictionaries().getHomophoneDictionary().importDictionary(fileName);
System.out.println("Homophone dictionary imported successfully.");
```

*การดำเนินการนำเข้าจะอ่านไฟล์ JSON, สร้างกลุ่มพ้องเสียงแต่ละกลุ่มใหม่, และผสานเข้ากับพจนานุกรมปัจจุบัน, ทำให้แน่ใจว่ารายการกำหนดเองทั้งหมดถูกกู้คืนอย่างแม่นยำและพร้อมใช้งานทันทีในการสืบค้น.*

### การค้นหาคำพ้องเสียง
ใช้การค้นหาคำพ้องเสียงเพื่อการดึงเอกสารอย่างครอบคลุม ทำให้ผู้ใช้สามารถค้นหาเนื้อหาที่เกี่ยวข้องแม้ใช้การสะกดที่ต่างกันแต่เสียงเดียวกัน ฟีเจอร์นี้สามารถปรับปรุงประสบการณ์ผู้ใช้ได้อย่างมากในโดเมนหลายภาษา หรือโดเมนที่เน้นการออกเสียง.

*การตั้งค่า `setUseHomophoneSearch(true)` จะบอกให้เอนจินขยายคำค้นด้วยคำที่มีเสียงเดียวกันก่อนดำเนินการ, ตัวเลือกนี้ทำงานร่วมกับการตั้งค่าการค้นหาอื่น ๆ เช่น fuzzy matching เพื่อให้ประสบการณ์การค้นหาที่แข็งแรงและยืดหยุ่น สามารถจับผลลัพธ์ที่เกี่ยวข้องได้หลากหลาย.*

```java
String query = "caul";
SearchOptions options = new SearchOptions();
options.setUseHomophoneSearch(true);
SearchResult result = index.search(query, options);

System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## การประยุกต์ใช้งานจริง
การเข้าใจวิธีการใช้งานฟีเจอร์เหล่านี้เปิดประตูสู่การประยุกต์ใช้งานจริงหลายรูปแบบ:

1. **การจัดการเอกสารทางกฎหมาย:** แยกแยะคำทางกฎหมายที่ออกเสียงคล้ายกัน เช่น “lease” กับ “least”.  
2. **การสร้างเนื้อหาการศึกษา:** ทำให้สื่อการสอนปราศจากคำที่คลุมเครือซึ่งอาจทำให้ผู้เรียนสับสน.  
3. **ระบบสนับสนุนลูกค้า:** ปรับปรุงความแม่นยำของการค้นหาฐานความรู้ ช่วยให้เจ้าหน้าที่ค้นหาบทความที่ถูกต้องได้เร็วขึ้น.

## ข้อควรพิจารณาด้านประสิทธิภาพ
เพื่อให้ **java full text search** ของคุณทำงานได้อย่างมีประสิทธิภาพ:

- **อัปเดตดัชนีเป็นประจำ** เพื่อสะท้อนการเปลี่ยนแปลงของเอกสาร.  
- **ตรวจสอบการใช้หน่วยความจำ** และปรับตั้งค่า Java heap สำหรับชุดข้อมูลขนาดใหญ่.  
- **ปิดทรัพยากรที่ไม่ได้ใช้โดยเร็ว** (เช่น เรียก `index.close()` เมื่อเสร็จ).

## สรุป
ตอนนี้คุณควรมีความเข้าใจที่มั่นคงเกี่ยวกับ **วิธีทำดัชนีเอกสาร** ด้วย GroupDocs.Search, การจัดการคำพ้องเสียง, และการปรับแต่งประสบการณ์การค้นหา เครื่องมือนี้มีคุณค่าอย่างยิ่งในการให้ผลลัพธ์ที่แม่นยำและเพิ่มประสิทธิภาพการจัดการเอกสารโดยรวม.

## คำถามที่พบบ่อย

**Q:** ฉันสามารถใช้พจนานุกรมคำพ้องเสียงกับภาษาที่ไม่ใช่ภาษาอังกฤษได้หรือไม่?  
**A:** ใช่, คุณสามารถเติมพจนานุกรมด้วยภาษาใดก็ได้ตราบใดที่คุณให้กลุ่มคำที่เหมาะสม.

**Q:** ฉันต้องการไลเซนส์สำหรับการทดสอบการพัฒนาหรือไม่?  
**A:** ไลเซนส์ทดลองใช้งานฟรีเพียงพอสำหรับการพัฒนาและการทดสอบ; จำเป็นต้องมีไลเซนส์แบบชำระเงินสำหรับการใช้งานในสภาพแวดล้อมผลิตจริง.

**Q:** ดัชนีของฉันสามารถใหญ่ได้เท่าใด?  
**A:** ขนาดดัชนีจำกัดเพียงตามทรัพยากรฮาร์ดแวร์ของคุณ; จัดสรรพื้นที่ดิสก์และหน่วยความจำให้เพียงพอเพื่อประสิทธิภาพที่ดีที่สุด.

**Q:** สามารถผสานการค้นหาคำพ้องเสียงกับ fuzzy matching ได้หรือไม่?  
**A:** แน่นอน. เปิดใช้งานทั้ง `setUseHomophoneSearch(true)` และ `setFuzzySearch(true)` ใน `SearchOptions` เพื่อให้ได้ประโยชน์จากทั้งสองอย่าง.

**Q:** จะเกิดอะไรขึ้นหากฉันเพิ่มกลุ่มคำพ้องเสียงที่ซ้ำกัน?  
**A:** รายการที่ซ้ำกันจะถูกละเว้น; พจนานุกรมจะรักษาชุดกลุ่มคำที่เป็นเอกลักษณ์.

---

**อัปเดตล่าสุด:** 2026-09-21  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [วิธีทำ java full text search: สร้างไดเรกทอรีดัชนีด้วย GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [วิธีเพิ่มเอกสารลงในดัชนีด้วย Metadata Indexing ใน Java โดยใช้ GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Java Full Text Search Library – ปรับแต่งดัชนีด้วย GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
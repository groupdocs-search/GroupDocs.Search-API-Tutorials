---
date: '2026-07-31'
description: เรียนรู้วิธีการทำการค้นหาแบบไม่แยกแยะตัวพิมพ์ใน Java โดยการเพิ่มเอกสารเข้าสู่ดัชนีด้วย
  GroupDocs.Search พร้อมใช้การแทนที่อักขระเพื่อทำให้ข้อความเป็นมาตรฐานระหว่างการทำดัชนี
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: การค้นหาแบบไม่แยกแยะตัวพิมพ์ใน Java ช่วยให้คุณเพิ่มเอกสารเข้าสู่ดัชนีและค้นหาได้โดยไม่ต้องกังวลเรื่องตัวอักษรใหญ่‑เล็ก
  คู่มือฉบับนี้แสดงให้เห็นว่า GroupDocs.Search ทำให้ข้อความเป็นมาตรฐานระหว่างการทำดัชนีเพื่อผลลัพธ์ที่เร็วและเชื่อถือได้
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: การค้นหาแบบไม่แยกแยะตัวพิมพ์ใน Java – ดัชนีเอกสารด้วย GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: เพิ่มเอกสารเข้าสู่ดัชนีสำหรับการค้นหาแบบไม่แยกแยะตัวพิมพ์ใน Java
type: docs
url: /th/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# เพิ่มเอกสารไปยังดัชนีสำหรับการค้นหาแบบไม่แยกแยะตัวพิมพ์ใหญ่‑เล็กใน Java

เมื่อคุณต้องการ **case insensitive search java** ที่ค้นหาข้อมูลได้อย่างแม่นยำโดยไม่สนใจว่าผู้ใช้พิมพ์อย่างไร กุญแจสำคัญคือการเพิ่มเอกสารไปยังดัชนีพร้อมกับทำให้ข้อความเป็นมาตรฐาน ในบทแนะนำนี้เราจะอธิบายการตั้งค่า GroupDocs.Search สำหรับ Java เพื่อให้เอกสารทุกไฟล์ที่คุณทำดัชนีถูกแปลงเป็นตัวพิมพ์เล็กโดยอัตโนมัติ (หรือแปลงในรูปแบบอื่น) ระหว่างการทำดัชนี ทำให้ผลลัพธ์การค้นหาแบบไม่แยกแยะตัวพิมพ์ใหญ่‑เล็กได้โดยไม่ต้องมีตรรกะเพิ่มเติมในขั้นตอนการค้นหา

## คำตอบสั้น
- **“add documents to index” หมายถึงอะไร?** หมายถึงการโหลดไฟล์ต้นทางเข้าสู่โครงสร้างข้อมูลที่สามารถค้นหาได้ เพื่อให้สามารถสืบค้นได้ในภายหลัง.  
- **ทำไมต้องใช้การแทนที่อักขระ?** มันทำให้ทุกอักขระเป็นมาตรฐาน—โดยทั่วไปเป็นตัวพิมพ์เล็ก—เพื่อให้การค้นหาไม่สนใจความแตกต่างของตัวพิมพ์ใหญ่‑เล็กโดยอัตโนมัติ.  
- **ต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **ต้องการเวอร์ชัน Java ใด?** Java 8 หรือใหม่กว่า; ไลบรารีนี้มุ่งเป้าไปที่ Java 11+ เพื่อประสิทธิภาพที่ดีที่สุด.  
- **ฉันสามารถสลับไปใช้การค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็กเมื่อจำเป็นได้หรือไม่?** ได้—ตัวเลือกการค้นหาช่วยให้คุณเปิด/ปิดการแยกแยะตัวพิมพ์ใหญ่‑เล็กตามแต่ละคำค้น.

## “add documents to index” คืออะไรใน GroupDocs.Search?
โหลดไฟล์ต้นทางของคุณ (PDF, DOCX, TXT ฯลฯ) ไปยังดัชนีที่สามารถค้นหาได้ เพื่อให้เครื่องมือสามารถดึงข้อมูลได้อย่างรวดเร็ว การเพิ่มเอกสารไปยังดัชนีจะทำการวิเคราะห์แต่ละไฟล์ ดึงข้อความธรรมดาออกมา และจัดเก็บในโครงสร้างข้อมูลที่ปรับแต่งเพื่อให้การค้นหาแบบเร็ว ๆ ทำได้

## ทำไมต้องเปิดใช้งานการแทนที่อักขระระหว่างการทำดัชนี?
การแทนที่อักขระจะเปลี่ยนแต่ละอักขระให้เป็นค่าที่กำหนดไว้ล่วงหน้า—โดยส่วนใหญ่เป็นตัวพิมพ์เล็ก—ในระหว่างการสร้างดัชนี สิ่งนี้ทำให้การเปลี่ยนแปลงของตัวพิมพ์ใหญ่‑เล็ก, เครื่องหมายสำเนียง, หรือสัญลักษณ์เฉพาะภาษาต่าง ๆ ไม่ส่งผลต่อผลลัพธ์การค้นหา โดยการทำให้ข้อความเป็นมาตรฐานในขั้นตอนการทำดัชนี เครื่องมือจะสามารถจับคู่คำค้นกับชุดโทเคนที่สอดคล้องกัน ทำให้พฤติกรรมการค้นหาแบบไม่แยกแยะตัวพิมพ์ใหญ่‑เล็กเร็วและเชื่อถือได้โดยไม่ต้องประมวลผลเพิ่มเติมในแต่ละการค้นหา

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search for Java** เวอร์ชัน 25.4 หรือใหม่กว่า (ไลบรารีรองรับไฟล์รูปแบบกว่า 30 แบบและสามารถทำดัชนีเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ).  
- **Java Development Kit (JDK)** เวอร์ชัน 8 หรือใหม่กว่า ติดตั้งแล้ว.  
- ความคุ้นเคยพื้นฐานกับ **Maven** (หรือความสามารถในการเพิ่ม JAR ด้วยตนเอง).  

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การตั้งค่า Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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
หากคุณไม่ต้องการใช้ Maven ให้ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
- **Free Trial** – ดาวน์โหลดไลเซนส์ทดลองเพื่อเริ่มทดลองใช้งาน.  
- **Temporary License** – ขอไลเซนส์ทดสอบระยะยาวจากพอร์ทัลของ GroupDocs.  
- **Full License** – ซื้อไลเซนส์สำหรับการใช้งานจริงเมื่อพร้อมเปิดใช้งาน.

### การเริ่มต้นพื้นฐาน (สร้างดัชนี)
The following snippet creates an index folder and enables character replacements:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## คู่มือการใช้งาน

### เปิดใช้งานการแทนที่อักขระในการตั้งค่าดัชนี
การเปิดใช้งานฟีเจอร์นี้บอกให้เครื่องมือทำการแทนที่อักขระระหว่างการทำดัชนี ซึ่งเป็นขั้นตอนหลักสำหรับพฤติกรรมการค้นหาแบบไม่แยกแยะตัวพิมพ์ใหญ่‑เล็ก.

#### ขั้นตอนที่ 1: กำหนดค่า `IndexSettings`
`IndexSettings` เป็นอ็อบเจ็กต์การกำหนดค่าที่ควบคุมวิธีการจัดเก็บและประมวลผลข้อความของดัชนี โดยการตั้งค่า `useCharacterReplacements` เป็น **true** จะเปิดการแปลงเป็นตัวพิมพ์เล็กอัตโนมัติ (หรือแมปกำหนดเองใด ๆ ที่คุณระบุ).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### กำหนดค่าการแทนที่อักขระ
แมปแต่ละอักขระไปยังรูปแบบตัวพิมพ์เล็กที่สอดคล้อง (หรือแมปกำหนดเองใด ๆ ที่คุณต้องการ).

#### ขั้นตอนที่ 2: กำหนดและเพิ่มคู่การแทนที่
พจนานุกรมการแทนที่เก็บคู่เช่น `'A' → 'a'`, `'É' → 'e'` เป็นต้น การเพิ่มคู่เหล่านี้ก่อนทำดัชนีทำให้ทุกโทเคนถูกทำให้เป็นมาตรฐาน.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### การทำดัชนีเอกสาร
เมื่อดัชนีพร้อมแล้ว คุณสามารถ **add documents to index** จากโฟลเดอร์ใดก็ได้.

#### ขั้นตอนที่ 3: เพิ่มเอกสารสำหรับทำดัชนี
GroupDocs.Search จะสแกนไดเรกทอรีเป้าหมาย ดึงข้อความจากแต่ละประเภทไฟล์ที่รองรับ ใช้แผนที่การแทนที่ และเขียนโทเคนลงในที่เก็บดัชนี.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### ทำการค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็ก (ทางเลือก)

#### ขั้นตอนที่ 4: ดำเนินการค้นหาแบบแยกแยะตัวพิมพ์ใหญ่‑เล็ก
`SearchOptions` กำหนดพฤติกรรมของคำค้น เช่น การเปิด/ปิดการแยกแยะตัวพิมพ์ใหญ่‑เล็ก ให้ควบคุมการค้นหาได้อย่างละเอียด.  
`SearchOptions.setUseCaseSensitiveSearch(true)` บังคับให้เครื่องมือพิจารณาตัวอักษรพิมพ์ใหญ่และพิมพ์เล็กเป็นต่างกันในคำค้นเฉพาะ ทำให้พฤติกรรมเริ่มต้นแบบไม่แยกแยะตัวพิมพ์ใหญ่‑เล็กถูกแทนที่.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## การประยุกต์ใช้งานจริง
1. **Marketing Campaigns** – ทำให้ชื่อผลิตภัณฑ์เป็นมาตรฐานเพื่อให้ทีมขายสามารถค้นหาแหล่งข้อมูลได้โดยไม่ต้องกังวลเรื่องตัวพิมพ์.  
2. **Customer Support** – เสริมกล่องค้นหาของศูนย์ช่วยเหลือให้คืนบทความที่ถูกต้องไม่ว่าผู้ใช้พิมพ์ “login” หรือ “Login”.  
3. **E‑commerce Catalogs** – ทำให้ผู้ซื้อสามารถค้นหารายการได้ไม่ว่าพิมพ์ชื่อผลิตภัณฑ์อย่างไร ช่วยเพิ่มอัตราการแปลง.

## การพิจารณาด้านประสิทธิภาพ
- **Organize Source Files** – โครงสร้างโฟลเดอร์ที่เป็นระเบียบช่วยลดเวลาการสแกนในขั้นตอน **add documents to index**.  
- **Monitor Memory** – การทำดัชนีข้อมูลจำนวนมากอาจใช้ RAM มาก; การประมวลผลไฟล์เป็นชุดละ 500 – 1 000 รายการช่วยควบคุมการใช้ heap.  
- **Asynchronous Indexing** – หากรองรับ ให้ทำการทำดัชนีบนเธรดพื้นหลังเพื่อให้ UI ตอบสนองและหลีกเลี่ยงการบล็อกการทำงานของผู้ใช้.

## ปัญหาทั่วไปและการแก้ไขข้อผิดพลาด
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| ไม่มีผลลัพธ์คืนสำหรับคำที่รู้จัก | การแทนที่อักขระไม่ได้เปิดใช้งาน | ตรวจสอบว่า `settings.setUseCharacterReplacements(true)` ถูกตั้งค่าและแผนที่การแทนที่มีอักขระที่ต้องการอยู่. |
| ข้อผิดพลาด Out‑of‑memory ระหว่างการทำดัชนี | ทำดัชนีไฟล์ขนาดใหญ่จำนวนมากพร้อมกัน | ทำดัชนีเป็นชุดเล็กลงหรือเพิ่ม heap ของ JVM (`-Xmx4g`). |
| การค้นหาให้ผลลัพธ์แยกแยะตัวพิมพ์ใหญ่‑เล็กโดยไม่คาดคิด | `SearchOptions.setUseCaseSensitiveSearch(true)` ถูกตั้งค่า | ลบหรือตั้งค่าเป็น `false` เพื่อให้เป็นพฤติกรรมเริ่มต้นแบบไม่แยกแยะตัวพิมพ์ใหญ่‑เล็ก. |
| เวลาโหลดดัชนีเกินคาดหวัง | โครงสร้างโฟลเดอร์ไม่เหมาะสมหรือไม่ได้ใช้ SSD | จัดระเบียบไฟล์ใหม่, ลบเอกสารที่ไม่ได้ใช้, และเก็บดัชนีบน SSD ที่เร็ว. |
| อักขระพิเศษถูกละเลย | แผนที่การแทนที่ไม่มีรายการ Unicode | เพิ่มการแมปสำหรับอักขระเช่น “é”, “ß”, “ø” ให้เป็นค่าที่ต้องการ. |

## คำถามที่พบบ่อย

**Q: ฉันจะจัดการกับอักขระพิเศษ (เช่น “é”, “ß”) ระหว่างการทำดัชนีอย่างไร?**  
A: รวมอักขระเหล่านั้นในแผนที่การแทนที่ของคุณ โดยแมปเป็นค่า ASCII ที่เทียบเท่าหรือคงไว้ตามความต้องการของการค้นหา.

**Q: ฉันสามารถจำกัดการแทนที่อักขระให้เฉพาะภาษาหนึ่งได้หรือไม่?**  
A: ได้. สร้างอาร์เรย์การแทนที่แบบกำหนดเองที่มีเฉพาะอักขระของภาษาที่ต้องการก่อนเพิ่มลงในพจนานุกรม.

**Q: ควรทำอย่างไรหากดัชนีใช้เวลานานในการโหลด?**  
A: ปรับโครงสร้างโฟลเดอร์, ลบไฟล์ที่ไม่จำเป็น, และเก็บดัชนีบน SSD ความเร็วสูง การทำดัชนีแบบเพิ่มส่วนช่วยลดภาระการโหลดได้.

**Q: สามารถย้อนกลับการแทนที่อักขระหลังจากทำดัชนีได้หรือไม่?**  
A: ไม่ได้. การแทนที่ถูกฝังไว้ในข้อมูลที่ทำดัชนีแล้ว; คุณต้องสร้างดัชนีใหม่ด้วยการตั้งค่าใหม่เพื่อเปลี่ยนแปลง.

**Q: ฉันจะหาเอกสาร API รายละเอียดเพิ่มเติมได้จากที่ไหน?**  
A: เอกสารอย่างเป็นทางการและอ้างอิง API มีรายละเอียดครบถ้วน (ดูส่วน Resources ด้านล่าง).

## แหล่งข้อมูล
- [เอกสาร](https://docs.groupdocs.com/search/java/)
- [อ้างอิง API](https://reference.groupdocs.com/search/java)
- [ดาวน์โหลด GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [ที่เก็บ GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)
- [ข้อมูลไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/) 

---

**อัปเดตล่าสุด:** 2026-07-31  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง

- [การแทนที่อักขระใน GroupDocs.Search Java: คู่มือครบวงจรเพื่อเพิ่มประสิทธิภาพการค้นหาข้อความและการทำดัชนี](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [เพิ่มเอกสารไปยังดัชนี: การค้นหา Java แยกแยะตัวพิมพ์ใหญ่‑เล็กด้วย GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [วิธีเพิ่มเอกสารไปยังดัชนีด้วย GroupDocs.Search สำหรับ Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
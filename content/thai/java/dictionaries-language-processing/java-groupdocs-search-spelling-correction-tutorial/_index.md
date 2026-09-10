---
date: '2026-09-02'
description: เรียนรู้วิธีสร้างดัชนีการค้นหา java และเปิดใช้งานการแก้ไขการสะกดคำโดยใช้
  GroupDocs.Search. ทำตาม step‑by‑step instructions เพื่อเพิ่มเอกสาร, configure max
  mistake count, และปรับปรุงความแม่นยำของการค้นหา.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: เรียนรู้วิธีสร้างดัชนีการค้นหา java และเปิดใช้งานการแก้ไขการสะกดคำโดยใช้
  GroupDocs.Search. ทำตาม step‑by‑step instructions เพื่อเพิ่มเอกสาร, configure max
  mistake count, และปรับปรุงความแม่นยำของการค้นหา.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: วิธีสร้างดัชนีการค้นหา java และเปิดใช้งานการสะกดคำ
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: วิธีสร้างดัชนีการค้นหา java และเปิดใช้งานการสะกดคำ
type: docs
url: /th/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# วิธีสร้างดัชนีการค้นหา java และเปิดใช้งานการตรวจสอบการสะกด

ในแอปพลิเคชัน Java สมัยใหม่ การให้ผลการค้นหาที่แม่นยำเป็นฟีเจอร์ที่จำเป็น บทเรียนนี้แสดง **วิธีสร้างดัชนีการค้นหา java** และเปิดการแก้ไขการสะกดด้วย GroupDocs.Search เพื่อให้ผู้ใช้ได้รับผลลัพธ์ที่เกี่ยวข้องแม้พิมพ์คำค้นผิด คุณจะได้เห็นวิธีตั้งค่าห้องสมุด, เพิ่มเอกสาร, กำหนดจำนวนข้อผิดพลาดสูงสุด, และทำการค้นหาที่ทนต่อการพิมพ์ผิด—ทั้งหมดโดยไม่ต้องเขียนโค้ดการกำหนดค่าเพิ่มเติมใด ๆ

## คำตอบสั้น
- **การเปิดใช้งานการสะกดทำอะไร?** It activates the built‑in spell‑checker that rewrites misspelled terms to their closest correct forms during a search.  
- **ไลบรารีใดให้ฟีเจอร์นี้?** GroupDocs.Search for Java.  
- **ฉันต้องการไลเซนส์หรือไม่?** A free trial works for evaluation; a full license is required for production use.  
- **ฉันสามารถควบคุมระดับความทนทานได้หรือไม่?** Yes – use `setMaxMistakeCount` to define how many typos are allowed per query.  
- **มันเหมาะกับดัชนีขนาดใหญ่หรือไม่?** Absolutely – the engine handles indexes with millions of records while keeping query latency under 100 ms on typical server hardware.

## GroupDocs.Search คืออะไร?
GroupDocs.Search is a Java library that provides fast full‑text indexing and advanced search features, including built‑in spelling correction. It supports 50+ input formats and can process multi‑hundred‑page documents without loading the entire file into memory.

## ทำไมต้องเปิดการแก้ไขการสะกดในแอปพลิเคชัน Java?
- **เพิ่มความพึงพอใจของผู้ใช้** – ผู้เยี่ยมชมจะได้รับผลลัพธ์ที่ถูกต้องแม้การพิมพ์ไม่สมบูรณ์.  
- **ลดอัตราการออกจากหน้า** – ผลลัพธ์ที่แม่นยำทำให้ผู้ใช้มีส่วนร่วมนานขึ้น.  
- **ทำงานได้หลากหลายโดเมน** – ตั้งแต่แคตาล็อกห้องสมุดจนถึงการค้นหาผลิตภัณฑ์อี‑คอมเมิร์ซ, การแก้ไขการสะกดช่วยเพิ่มความเกี่ยวข้องทุกที่.

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java Development Kit (JDK) แล้ว.  
- มีความรู้พื้นฐานเกี่ยวกับ Java และ Maven.  
- เข้าใจแนวคิดการทำดัชนี.  
- มีไลเซนส์ทดลองหรือไลเซนส์ของ GroupDocs.Search.

### การตั้งค่า GroupDocs.Search สำหรับ Java
Integrate the library into your Maven project.

**การตั้งค่า Maven**  
Add the repository and dependency to your `pom.xml` file:

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

**ดาวน์โหลดโดยตรง**  
Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
Obtain a free trial license for evaluation. For production use, purchase a full license or request a temporary key from the official site.

## ฉันจะสร้างดัชนีการค้นหาใน Java อย่างไร?
`SearchIndex` is the primary class that represents a searchable index stored on disk.  
Create a `SearchIndex` instance pointing to a folder on disk, then add documents from a source directory. The engine builds an inverted index that powers fast look‑ups. You can call `index.add()` for each file; the library extracts text automatically based on file type.

## ฉันจะเปิดการแก้ไขการสะกดได้อย่างไร?
`getSpellingOptions()` returns the spelling configuration object for the index, allowing you to enable or tweak spell‑checking features.  
Enable spelling by calling `index.getSpellingOptions().setEnabled(true)`. This tells the engine to analyze query terms and suggest corrected alternatives when mismatches are detected. The feature works out‑of‑the‑box for all indexed languages supported by the library.

## การตั้งค่า max mistake count คืออะไร?
`setMaxMistakeCount` configures the maximum number of character edits the spell‑checker will tolerate per term.  
`setMaxMistakeCount(int)` defines the maximum number of character edits (insertions, deletions, substitutions) the spell‑checker will tolerate per term. Setting it to **2** allows the engine to fix common two‑character typos while avoiding overly aggressive corrections that could return unrelated results.

## วิธีทำการค้นหาที่แก้ไขการสะกด
`search()` executes a query against the index and returns a `SearchResult` object containing matches and any corrected terms.  
Run a search query using the `search()` method. If the query contains misspelled words, the engine returns a `SearchResult` that includes the corrected terms and a list of the most relevant documents. You can display both the original query and the corrected version to the user for transparency.  
`SearchResult` holds the list of matching documents and information about query corrections.

## การใช้งานเชิงปฏิบัติ
1. **ระบบห้องสมุด** – แก้ไขชื่อหนังสือหรือชื่อผู้เขียนที่พิมพ์ผิดโดยอัตโนมัติ.  
2. **แพลตฟอร์มอี‑คอมเมิร์ซ** – แก้ไขคำพิมพ์ผิดของชื่อสินค้าเพื่อเพิ่มอัตราการแปลง.  
3. **ระบบจัดการเนื้อหา** – ช่วยบรรณาธิการค้นหาบทความแม้ใช้คีย์เวิร์ดไม่สมบูรณ์.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **รักษาดัชนีให้เป็นปัจจุบัน** – ทำการ re‑index ไฟล์ใหม่หรือที่เปลี่ยนแปลงเป็นประจำ.  
- **ปรับการตั้งค่า JVM memory** – จัดสรร heap เพียงพอสำหรับดัชนีขนาดใหญ่ (เช่น `-Xmx4g`).  
- **ตรวจสอบการใช้ทรัพยากร** – ปรับค่า garbage‑collector หากพบการหยุดชะงักระหว่างการทำดัชนีจำนวนมาก.

## ปัญหาทั่วไปและการแก้ไขข้อผิดพลาด
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| No results after enabling spelling | Index folder path is wrong or empty | Verify `indexFolder` points to a valid index and that `index.add()` succeeded |
| Spell‑checker does not correct obvious typos | `setMaxMistakeCount` is set too low | Increase the count to 2 or 3 for more tolerant correction |
| Application crashes on large document sets | Insufficient JVM heap | Increase `-Xmx` option (e.g., `-Xmx4g`) |

## คำถามที่พบบ่อย

**ถาม: GroupDocs.Search คืออะไร?**  
A: GroupDocs.Search is a Java library that provides fast indexing, advanced query capabilities, and built‑in spelling correction for any Java application.

**ถาม: ฉันจะได้รับไลเซนส์สำหรับ GroupDocs.Search อย่างไร?**  
A: Visit the official site to download a free trial or purchase a full license; a temporary key is also available for short‑term testing.

**ถาม: ฉันสามารถรวม GroupDocs.Search กับเฟรมเวิร์ก Java อื่นได้หรือไม่?**  
A: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java application.

**ถาม: ปัญหาที่พบบ่อยเมื่อตั้งค่าดัชนีคืออะไร?**  
A: Incorrect folder paths, missing file permissions, or absent Maven dependencies are the typical culprits.

**ถาม: การแก้ไขการสะกดช่วยปรับปรุงผลการค้นหาอย่างไร?**  
A: It automatically rewrites misspelled queries to their closest correct terms, returning more relevant hits and reducing user frustration.

## แหล่งข้อมูลเพิ่มเติม
- [เอกสาร](https://docs.groupdocs.com/search/java/)
- [อ้างอิง API](https://reference.groupdocs.com/search/java)
- [ดาวน์โหลด](https://releases.groupdocs.com/search/java/)
- [ที่เก็บ GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)
- [ไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-09-02  
**ทดสอบกับ:** GroupDocs.Search 25.4  
**ผู้เขียน:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## บทแนะนำที่เกี่ยวข้อง

- [วิธีสร้างดัชนีเอกสารและเพิ่มเอกสารโดยใช้ GroupDocs.Search API สำหรับ Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [การประมวลผลภาษา Java – สร้างพจนานุกรมคำพ้องความหมายด้วย GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [คำหยุดในการค้นหา: เพิ่มเอกสารลงในดัชนีด้วย GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
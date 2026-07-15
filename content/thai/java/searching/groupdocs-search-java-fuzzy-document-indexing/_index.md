---
date: '2026-05-28'
description: เรียนรู้วิธีการค้นหาเอกสารอย่างมีประสิทธิภาพด้วย GroupDocs.Search for
  Java รวมถึง fuzzy search Java และวิธีสร้างดัชนีสำหรับ full‑text search
keywords:
- how to search documents
- how to create index
- fuzzy search java
- java full text search
- implement fuzzy matching
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search documents efficiently with GroupDocs.Search for
    Java, including fuzzy search Java and how to create index for full‑text search.
  headline: How to Search Documents Using GroupDocs.Search Java
  type: TechArticle
- description: Learn how to search documents efficiently with GroupDocs.Search for
    Java, including fuzzy search Java and how to create index for full‑text search.
  name: How to Search Documents Using GroupDocs.Search Java
  steps:
  - name: '**Legal Document Management:** Locate clauses or parties across thousands
      of contracts in seconds.'
    text: '**Legal Document Management:** Locate clauses or parties across thousands
      of contracts in seconds.'
  - name: '**Academic Research:** Retrieve relevant papers even if the search term
      is misspelled.'
    text: '**Academic Research:** Retrieve relevant papers even if the search term
      is misspelled.'
  - name: '**Enterprise Content Management:** Power internal portals with fast, typo‑tolerant
      search across reports, emails, and presentations.'
    text: '**Enterprise Content Management:** Power internal portals with fast, typo‑tolerant
      search across reports, emails, and presentations.'
  type: HowTo
- questions:
  - answer: Fuzzy search Java enables approximate string matching, allowing queries
      to return results despite typos or alternate spellings, which improves end‑user
      experience.
    question: What is fuzzy search Java and why is it useful?
  - answer: Call `index.add("new/files/folder")` again; the library intelligently
      merges new content without rebuilding the entire index.
    question: How do I update my index after adding new files?
  - answer: Yes—provide the password in the `DocumentLoadOptions` when adding the
      file, and the engine will decrypt and index the content.
    question: Can GroupDocs.Search handle password‑protected PDFs?
  - answer: The library scales to millions of files; performance depends on hardware
      and storage, not a hard‑coded limit.
    question: Is there a limit to the number of documents I can index?
  - answer: Visit the official documentation for deeper topics like custom analyzers
      and result ranking.
    question: Where can I find more advanced examples?
  type: FAQPage
title: วิธีการค้นหาเอกสารโดยใช้ GroupDocs.Search Java
type: docs
url: /th/java/searching/groupdocs-search-java-fuzzy-document-indexing/
weight: 1
---

# วิธีการค้นหาเอกสารโดยใช้ GroupDocs.Search Java

ในแอปพลิเคชันองค์กรสมัยใหม่ การ **how to search documents** อย่างรวดเร็วและแม่นยำเป็นความต้องการที่สำคัญ ไม่ว่าคุณจะจัดการกับสัญญา รายงาน หรือคลังเอกสารขนาดใหญ่ใด GroupDocs.Search สำหรับ Java ให้เครื่องมือค้นหาแบบเต็มข้อความที่แข็งแกร่งพร้อมการจับคู่แบบ fuzzy ในตัว บทเรียนนี้จะพาคุณผ่านการตั้งค่าห้องสมุด การสร้างดัชนี การเพิ่มเอกสาร การกำหนดค่าการค้นหา fuzzy Java และการดึงผลลัพธ์—ทั้งหมดด้วยคำอธิบายที่ชัดเจนและเป็นกันเอง

## คำตอบด่วน
- **ขั้นตอนแรกคืออะไร?** Install the GroupDocs.Search Java library via Maven or download it directly.  
- **ฉันจะสร้างดัชนีอย่างไร?** Instantiate an `Index` object pointing to a folder on disk; the library builds the searchable structure automatically.  
- **ฉันสามารถค้นหาด้วยการพิมพ์ผิดได้หรือไม่?** Yes—enable fuzzy search to match terms that are misspelled or have slight variations.  
- **วิธีการเพิ่มเอกสาร?** Use the `add` method on the `Index` instance, passing the folder that contains your files.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 or higher is supported.

## “how to search documents” คืออะไรในบริบทของ GroupDocs.Search?
**“How to search documents”** หมายถึงกระบวนการสร้างดัชนีที่ค้นหาได้และส่งคำค้นที่ส่งคืนไฟล์ที่ตรงกัน โดยอาจใช้ตรรกะ fuzzy เพื่อทนต่อข้อผิดพลาดในการสะกด GroupDocs.Search จัดการการแยกโทเคน การทำดัชนี และการจัดอันดับเบื้องหลัง เพื่อให้คุณมุ่งเน้นที่ตรรกะธุรกิจ

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
GroupDocs.Search รองรับ **ไฟล์ฟอร์แมตกว่า 30 ประเภท** (รวมถึง DOCX, PDF, TXT, HTML, และ XLSX) และสามารถทำดัชนี **เอกสารหลายร้อยหน้า** ได้โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้ตอบสนองคำค้นภายในระดับวินาทีบนฮาร์ดแวร์เซิร์ฟเวอร์ทั่วไป ความสามารถในการค้นหาแบบ fuzzy ของมันช่วยปรับปรุงประสบการณ์ผู้ใช้โดยคืนผลลัพธ์ที่เกี่ยวข้องแม้คำค้นจะมีการพิมพ์ผิด

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK):** เวอร์ชัน 8 หรือใหม่กว่า.  
- **IDE:** IntelliJ IDEA, Eclipse, หรือ editor ที่รองรับ Java ใด ๆ.  
- **GroupDocs.Search for Java library:** เพิ่มผ่าน Maven (แนะนำ) หรือดาวน์โหลดไฟล์ JAR.

## วิธีการตั้งค่า GroupDocs.Search สำหรับ Java?

เพื่อเริ่มต้น ให้เพิ่ม dependency ของ GroupDocs.Search ลงในไฟล์ build ของคุณ ตรวจสอบให้แน่ใจว่า URL ของ repository สามารถเข้าถึงได้ และตรวจสอบว่าเวอร์ชัน JDK ตรงตามข้อกำหนดขั้นต่ำ หลังจากไลบรารีถูกดึงมาแล้ว คุณสามารถ import คลาสต่าง ๆ ในโค้ดของคุณและสร้างโฟลเดอร์ดัชนีบนดิสก์ที่เก็บข้อมูลที่สามารถค้นหาได้ทั้งหมด

### การตั้งค่า Maven
Add the repository and dependency to your `pom.xml` file exactly as shown in the original guide.

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
หรือดาวน์โหลดไฟล์ JAR จากหน้าปล่อยอย่างเป็นทางการ:

[การปล่อย GroupDocs.Search สำหรับ Java](https://releases.groupdocs.com/search/java/)

[เอกสาร GroupDocs.Search](https://docs.groupdocs.com/search/java/)

## วิธีการสร้างดัชนี?
สร้างโฟลเดอร์ดัชนีแบบคงที่ที่ GroupDocs.Search จะเก็บข้อมูลที่แยกโทเคนไว้ โหลดดัชนีแรกของคุณด้วยบรรทัดโค้ดเดียว—`new Index("path/to/indexFolder")`. คลาส `Index` เป็นคอมโพเนนต์หลักที่แทนคอลเลกชันเอกสารที่สามารถค้นหาได้ในหน่วยความจำและบนดิสก์

```java
   import com.groupdocs.search.*;

   String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/SearchResults";
   Index index = new Index(indexFolder);
   ```

## วิธีการเพิ่มเอกสารลงในดัชนี?
ใช้เมธอด `add` ของอินสแตนซ์ `Index` เพื่อชี้ไปยังโฟลเดอร์ที่มีไฟล์ต้นฉบับของคุณ เอนจินจะสแกนรูปแบบที่รองรับแบบเรียกซ้ำ ดึงเนื้อหาข้อความออกมา และอัปเดตโครงสร้างภายใน การเรียกเดียวนี้จัดการชุดข้อมูลขนาดใหญ่ได้อย่างมีประสิทธิภาพโดยไม่ต้องประมวลผลไฟล์ทีละไฟล์

```java
   String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentFolder);
   ```

## วิธีการกำหนดค่าการค้นหา Fuzzy ใน Java?
คลาส `FuzzySearchOptions` กำหนดพารามิเตอร์เช่นระยะทางการแก้ไขและความยาวพรีฟิกซ์ที่ควบคุมระดับการทนต่อการสะกดผิด `SearchOptions` รวมการตั้งค่าทั้งหมดในช่วงเวลาการค้นหา รวมถึงตัวเลือก fuzzy, ขีดจำกัดผลลัพธ์, และการไฮไลท์ เปิดการจับคู่ fuzzy โดยตั้งค่า `FuzzySearchOptions` บนวัตถุ `SearchOptions` นี้บอกเอ็นจินให้พิจารณาคำที่อยู่ในระยะทางการแก้ไขที่กำหนด ทำให้การค้นทนต่อการสะกดผิด

```java
  String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/SearchResults";
  Index index = new Index(indexFolder);
  ```

## วิธีการดำเนินการค้นหา?
เรียกเมธอด `search` บนวัตถุ `Index` โดยให้สตริงคำค้นและ `SearchOptions` ที่กำหนดไว้ เอ็นจินจะประมวลผลคำขอ ใช้การจับคู่ fuzzy หากเปิดใช้งาน และจัดอันดับผลลัพธ์ตามคะแนนความเกี่ยวข้อง การดำเนินการเสร็จเร็วแม้บนดัชนีขนาดใหญ่เพราะการค้นหาทำบนโครงสร้างโทเคนที่สร้างไว้ล่วงหน้า เมธอดจะคืนคอลเลกชัน `SearchResult` ที่มีเอกสารที่ตรงกัน, จำนวนการพบ, และสแนปช็อตที่ไฮไลท์

```java
  String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
  index.add(documentFolder);
  ```

## วิธีการประมวลผลและแสดงผลลัพธ์การค้นหา?
`SearchResult` เป็นคอลเลกชันที่เก็บอ็อบเจ็กต์ `SearchResultItem` แต่ละรายการอธิบายเอกสารที่ตรงกัน, จำนวนการพบ, และสแนปช็อตที่ไฮไลท์ วนลูปผ่านรายการ `SearchResult` แล้วพิมพ์เส้นทางของเอกสาร, จำนวนการเกิดขึ้น, และวลีที่ตรงกัน ลูปง่าย ๆ นี้ช่วยให้คุณสร้างตาราง UI, บันทึก, หรือการตอบสนอง API ที่แสดงเหตุผลว่าทำไมเอกสารจึงตรงกัน

```java
  import com.groupdocs.search.options.*;

  SearchOptions options = new SearchOptions();
  options.getFuzzySearch().setEnabled(true);
  options.getFuzzySearch().setFuzzyAlgorithm(new TableDiscreteFunction(3));
  ```

## การใช้งานจริง
1. **Legal Document Management:** ค้นหาข้อหรือฝ่ายต่าง ๆ ในสัญญานับพันภายในไม่กี่วินาที.  
2. **Academic Research:** ดึงเอกสารที่เกี่ยวข้องแม้คำค้นจะสะกดผิด.  
3. **Enterprise Content Management:** ให้พลังกับพอร์ทัลภายในด้วยการค้นหาเร็วและทนต่อการพิมพ์ผิดทั่วทั้งรายงาน, อีเมล, และงานนำเสนอ.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Index Refresh:** เรียกใช้ `add` หรือ `update` ใหม่ทุกครั้งที่ไฟล์ต้นทางเปลี่ยนแปลงเพื่อให้ผลลัพธ์เป็นปัจจุบัน.  
- **Memory Management:** GroupDocs.Search สตรีมไฟล์ขนาดใหญ่ ทำให้การใช้หน่วยความจำต่ำแม้สำหรับ PDF ขนาด 500 หน้า.  
- **Chunked Indexing:** แบ่งคอร์ปัสขนาดมหาศาลเป็นหลายโฟลเดอร์ดัชนีเพื่อประมวลผลแบบขนานและลดความหน่วงของคำค้น.

## คำถามที่พบบ่อย

**Q: What is fuzzy search Java and why is it useful?**  
A: Fuzzy search Java enables approximate string matching, allowing queries to return results despite typos or alternate spellings, which improves end‑user experience.

**Q: How do I update my index after adding new files?**  
A: Call `index.add("new/files/folder")` again; the library intelligently merges new content without rebuilding the entire index.

**Q: Can GroupDocs.Search handle password‑protected PDFs?**  
A: Yes—provide the password in the `DocumentLoadOptions` when adding the file, and the engine will decrypt and index the content.

**Q: Is there a limit to the number of documents I can index?**  
A: The library scales to millions of files; performance depends on hardware and storage, not a hard‑coded limit.

**Q: Where can I find more advanced examples?**  
A: Visit the official documentation for deeper topics like custom analyzers and result ranking.

## สรุป
คุณได้เรียนรู้ **how to search documents** ด้วย GroupDocs.Search สำหรับ Java ตั้งแต่การสร้างดัชนีจนถึงการเปิดใช้งาน fuzzy search Java และการประมวลผลผลลัพธ์แล้ว นำขั้นตอนเหล่านี้ไปใช้เพื่อมอบประสบการณ์การค้นหาเร็วและทนต่อการพิมพ์ผิดในแอปพลิเคชัน Java ใด ๆ

---

**อัปเดตล่าสุด:** 2026-05-28  
**ทดสอบกับ:** GroupDocs.Search 23.10 for Java  
**ผู้เขียน:** GroupDocs  

```java
  String query = "water OR \"Lorem ipsum\"";
  SearchResult result = index.search(query, options);
  ```

```java
  for (int i = 0; i < result.getDocumentCount(); i++) {
      FoundDocument document = result.getFoundDocument(i);
      System.out.println("\tDocument: " + document.getDocumentInfo().getFilePath());
      System.out.println("\tOccurrences: " + document.getOccurrenceCount());

      for (FoundDocumentField field : document.getFoundFields()) {
          System.out.println("\t\tField: " + field.getFieldName());
          if (field.getTerms() != null) {
              for (int k = 0; k < field.getTerms().length; k++) {
                  System.out.println("\t\t\t" + field.getTerms()[k] + " - " + field.getTermsOccurrences()[k]);
              }
          }
      }
  }
  ```

## บทเรียนที่เกี่ยวข้อง
- [สร้างดัชนีเอกสารด้วย GroupDocs.Search สำหรับ Java](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [ดำเนินการค้นหาแบบเต็มข้อความใน Java ด้วย GroupDocs.Search: คู่มือเชิงลึก](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [วิธีเพิ่มเอกสารลงในดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
---
date: '2026-05-28'
description: เรียนรู้วิธีการค้นหาวลีด้วย wildcard patterns โดยใช้ GroupDocs.Search
  for Java. รวมถึงการสร้าง search index, การเพิ่ม documents, และการดำเนินการ exact
  phrase และ wildcard queries.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: วิธีการค้นหาวลีด้วย wildcards ใน GroupDocs.Search for Java
type: docs
url: /th/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# วิธีการค้นหาวลีด้วยไวล์การ์ดใน GroupDocs.Search for Java

ในแอปพลิเคชันที่เน้นเอกสารสมัยใหม่ การ **how to search phrase** อย่างรวดเร็วและแม่นยำเป็นปัจจัยสำคัญต่อประสบการณ์ผู้ใช้ ไม่ว่าคุณจะสร้างฐานความรู้ แคตาล็อกอีคอมเมิร์ซ หรือคลังข้อมูลที่ขับเคลื่อนด้วยการปฏิบัติตามกฎ ความสามารถในการค้นหาวลีที่ตรงกันอย่างแม่นยำ—หรือรูปแบบที่ยืดหยุ่นของมัน—ช่วยให้ผู้ใช้ทำงานได้อย่างมีประสิทธิภาพและลดภาระการสนับสนุน บทเรียนนี้จะพาคุณผ่านการติดตั้ง **GroupDocs.Search for Java**, การสร้างดัชนีการค้นหา, การโหลดเอกสาร, และการรันทั้งการค้นหาวลีที่ตรงและการค้นหาที่เพิ่มไวล์การ์ด, ทั้งหมดด้วยโค้ดสแนปช็อตที่ชัดเจนและพร้อมใช้งานในสภาพแวดล้อมการผลิต

## คำตอบด่วน
- **อะไรคือประโยชน์หลักของการค้นหาวลี?** การจับคู่ที่แม่นยำของลำดับคำและระยะห่าง, รับประกันว่าจะคืนเอกสารที่มีลำดับที่ตรงกันเท่านั้น.  
- **สามารถใช้ไวล์การ์ดภายในวลีได้หรือไม่?** ใช่—ไวล์การ์ดช่วยให้คุณข้ามหรือแทนที่คำในขณะที่ยังคงรักษาลำดับโดยรวม.  
- **ต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการทดสอบ; จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **ควรใช้เวอร์ชัน Maven ใด?** เวอร์ชันล่าสุดของ GroupDocs.Search for Java (เช่น 25.4 ณ เวลาที่เขียน).  
- **วิธีนี้เหมาะกับชุดเอกสารขนาดใหญ่หรือไม่?** แน่นอน—GroupDocs.Search สามารถจัดการคอลเลกชันหลายแสนเอกสารพร้อมความหน่วงของการค้นหาแบบย่อยวินาทีเมื่อดัชนีได้รับการปรับให้เหมาะสม.

## “how to search phrase” คืออะไร?
**การค้นหาวลีหมายถึงการมองหาลำดับคำเฉพาะในเอกสาร.**  
เมื่อคุณดำเนินการค้นหาวลี, เอนจินจะตรวจสอบว่าคำปรากฏในลำดับที่ตรงกันและอยู่ในระยะห่างที่กำหนด, ทำให้ผลลัพธ์ที่ไม่เกี่ยวข้องที่มีคำเดียวกันในบริบทอื่นถูกกรองออก. สิ่งนี้ทำให้การค้นหาวลีเหมาะสำหรับการค้นหาข้อกฎหมาย, รหัสสินค้า, หรือข้อความใด ๆ ที่ลำดับมีความสำคัญ.

## ทำไมต้องใช้ GroupDocs.Search สำหรับการค้นหาวลีและไวล์การ์ด?
GroupDocs.Search ให้ **การทำดัชนีความเร็วสูงถึง 1 ล้านเอกสารพร้อมการตอบสนองของการค้นหาแบบย่อยวินาที** บนฮาร์ดแวร์เซิร์ฟเวอร์ทั่วไป. ภาษาคำค้นของมันรองรับวลีที่ตรง, ไวล์การ์ดแบบง่าย `*` และ `?`, และแพทเทิร์นขั้นสูงเช่นช่วงตัวเลข (`*2~5`). ไลบรารีนี้รวมเข้ากับแอปพลิเคชัน Java ใด ๆ ผ่าน Maven หรือการดาวน์โหลด JAR โดยตรง, และทำงานบน Java 8+ โดยไม่ต้องใช้บริการภายนอก.

## ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า (แนะนำ Java 11 LTS).  
- Maven 3 หรือใหม่กว่า (หากคุณต้องการการจัดการ dependencies).  
- ความคุ้นเคยพื้นฐานกับโครงสร้างโปรเจกต์ Java และแนวคิดเชิงวัตถุ.  

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การใช้ Maven
เพิ่ม repository อย่างเป็นทางการและ dependency ของ GroupDocs.Search ไปยังไฟล์ `pom.xml` ของคุณ:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### ดาวน์โหลดโดยตรง
หากต้องการ, ดาวน์โหลด JAR ล่าสุดจากหน้า release อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
- **Free Trial:** เหมาะสำหรับการทดลองอย่างรวดเร็ว; จำกัดที่ข้อมูลที่ทำดัชนี 100 MB.  
- **Temporary License:** ขอคีย์การประเมินผล 30‑วันจากพอร์ทัลของ GroupDocs.  
- **Full License:** จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิตและความจุการทำดัชนีไม่จำกัด.

## การเริ่มต้นและตั้งค่าเบื้องต้น
สร้างโฟลเดอร์ที่จะเก็บไฟล์ดัชนีและสร้างอ็อบเจกต์ `Index`. คลาส `Index` แทนดัชนีที่สามารถค้นหาได้ที่เก็บบนดิสก์และให้เมธอดสำหรับเพิ่ม, อัปเดต, และค้นหาเอกสาร.

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

เพิ่มเอกสารที่คุณต้องการให้สามารถค้นหาได้:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## วิธีการค้นหาวลีด้วยไวล์การ์ดใน GroupDocs.Search
ส่วนนี้จะแสดงระดับการค้นหาวลีสามระดับ—การจับคู่ที่ตรง, ไวล์การ์ดแบบง่าย, และแพทเทิร์นไวล์การ์ดขั้นสูง—โดยสาธิตวิธีสร้างดัชนี, เพิ่มเอกสาร, และดำเนินการแต่ละประเภทของคำค้นด้วยโค้ด Java ที่กระชับ. ตัวอย่างจะแสดงทั้งคำค้นแบบข้อความและการสร้างคำค้นแบบอ็อบเจกต์, ช่วยให้นักพัฒนานำความสามารถการค้นหาที่ยืดหยุ่นเข้าสู่แอปพลิเคชันของตนได้.

### การค้นหาวลีแบบง่าย

#### ภาพรวม
ใช้วิธีนี้เมื่อคุณต้องการ **exact match** ของลำดับคำ, เช่น ข้อกฎหมายหรือหมายเลขรุ่นสินค้า.

#### คำตอบโดยตรง
โหลดดัชนี, เรียก `search` ด้วยวลีที่อยู่ในเครื่องหมายคำพูด (เช่น `"quick brown fox"`), และเอนจินจะคืนเอกสารที่มีลำดับที่ตรงกันเท่านั้น, รักษาลำดับคำและช่องว่าง. คำค้นทำงานในระดับมิลลิวินาทีแม้กับดัชนีที่มีไฟล์หลายแสนไฟล์.

#### ขั้นตอน 1: สร้างดัชนี
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### ขั้นตอน 2: เพิ่มเอกสารลงในดัชนี
```java
Index index = new Index(indexFolder);
```

#### ขั้นตอน 3: ค้นหาวลีเฉพาะ (รูปแบบข้อความ)
```java
index.add(documentsFolder);
```

#### ขั้นตอน 4: คำถามแบบอ็อบเจกต์ (ค้นหาวลีที่ตรงกัน)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### การค้นหาวลีด้วยไวล์การ์ด

#### ภาพรวม
ไวล์การ์ด (`*` สำหรับอักขระจำนวนใดก็ได้, `?` สำหรับอักขระเดียว) ให้คุณ **skip variable words** ในขณะที่ยังคงบังคับลำดับโดยรอบ.

#### คำตอบโดยตรง
ใส่โทเคนไวล์การ์ด (`*`) ภายในวลีที่อยู่ในเครื่องหมายคำพูด—เช่น `"quick * fox"`—เพื่อจับคำใดก็ได้ระหว่าง *quick* และ *fox*. เอนจินจะขยายไวล์การ์ดในเวลาคำค้น, สแกนเฉพาะเทอมที่ทำดัชนีที่ตรงกับแพทเทิร์น, ทำให้ประสิทธิภาพเทียบเท่ากับการค้นหาวลีธรรมดา.

#### ขั้นตอน 1: สร้างดัชนี
*(เช่นเดียวกับการค้นหาวลีแบบง่าย.)*

#### ขั้นตอน 2: เพิ่มเอกสารลงในดัชนี
*(เช่นเดียวกับข้างต้น.)*

#### ขั้นตอน 3: ค้นหารูปแบบข้อความด้วยไวล์การ์ด
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### ขั้นตอน 4: คำถามแบบอ็อบเจกต์ด้วยไวล์การ์ด (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### การค้นหาไวล์การ์ดขั้นสูง

#### ภาพรวม
รวมช่วงตัวเลข, ตัวอักษรทางเลือก, และแพทเทิร์นคล้าย regex เพื่อ **sophisticated matching**, เช่นหมายเลขเวอร์ชันหรือรหัสสินค้า.

#### คำตอบโดยตรง
ใช้ไวยากรณ์ไวล์การ์ดขยาย `*min~max` เพื่อกำหนดช่วงระยะห่างของคำที่อนุญาต, หรือ `?` เพื่อจับอักขระเดียว. ตัวอย่างเช่น `"error *2~5 code"` จะพบคำ *error* ตามด้วยคำสองถึงห้าคำแล้วตามด้วย *code*. ความแม่นยำนี้ลดผลบวกเท็จในขณะที่ยังคงให้ความยืดหยุ่น.

#### ขั้นตอน 1: สร้างดัชนี
*(ทำซ้ำเพื่อความชัดเจน.)*

#### ขั้นตอน 2: เพิ่มเอกสารลงในดัชนี
*(ทำซ้ำ.)*

#### ขั้นตอน 3: ค้นหารูปแบบข้อความด้วยแพทเทิร์นไวล์การ์ดซับซ้อน
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### ขั้นตอน 4: คำถามแบบอ็อบเจกต์ด้วยไวล์การ์ดขั้นสูง
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## การประยุกต์ใช้งานจริง
- **Content Management Systems:** ผู้แก้ไขสามารถค้นหาข้อความที่ตรงหรือส่วนที่ยืดหยุ่นได้โดยไม่ต้องสแกนหลายร้อยหน้าโดยมือ.  
- **E‑commerce Catalogs:** ผู้ซื้อสามารถค้นหาผลิตภัณฑ์แม้จะละคำอธิบายหรือใช้คำพ้องความหมาย, ขอบคุณความทนทานของไวล์การ์ด.  
- **Legal & Compliance:** แยกภาษาสัญญาที่อาจปรากฏด้วยความแตกต่างเล็กน้อยในหลายสัญญาได้อย่างรวดเร็ว.  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Create Search Index** เพียงครั้งเดียวต่อชุดเอกสารที่คงที่; ใช้ `Index` ตัวเดียวสำหรับทุกคำค้น.  
- **Add Documents Incrementally** เมื่อไฟล์ใหม่เข้ามา—หลีกเลี่ยงการสร้างดัชนีใหม่ทั้งหมดเพื่อรักษาการใช้ CPU ต่ำ.  
- **Design Precise Wildcard Patterns**; แพทเทิร์นกว้าง (`*`) จะเพิ่มจำนวนการขยายเทอมและอาจทำให้โหลด CPU เพิ่มขึ้น.  
- **Call `index.optimize()`** เป็นระยะ (หากรองรับ) เพื่อบีบอัดดัชนีและควบคุมการใช้หน่วยความจำ.  

## ปัญหาและวิธีแก้ไขทั่วไป
| Issue | Solution |
|-------|----------|
| No results returned for a wildcard query | Verify the wildcard syntax (`*min~max`) and ensure the target words exist within the defined distance. |
| Index becomes stale after file updates | Use `index.add(updatedFolder)` or the incremental update API to refresh only changed files. |
| High memory consumption on large datasets | Increase JVM heap (`-Xmx4g` or higher) and consider splitting the index into multiple shards for parallel processing. |

## คำถามที่พบบ่อย

**Q: What is the difference between a wildcard and a phrase search?**  
A: การค้นหาวลีต้องการลำดับคำและช่องว่างที่ตรงกัน, ในขณะที่ไวล์การ์ดอนุญาตให้คุณแทนที่หรือข้ามคำภายในลำดับนั้น, ให้การจับคู่ที่ยืดหยุ่น.

**Q: Can I use wildcards with numeric data in searches?**  
A: ใช่—พารามิเตอร์ช่วงไวล์การ์ด (`*min~max`) ทำงานกับตัวเลขเช่นกันกับคำ, ทำให้สามารถค้นหาเช่น `"version *1~3"` ได้.

**Q: How should I handle very large document collections?**  
A: รักษาดัชนีให้ปรับให้เหมาะสม, ทำการอัปเดตแบบเพิ่มส่วน, และออกแบบแพทเทิร์นไวล์การ์ดที่เฉพาะเจาะจงเพื่อจำกัดการขยายเทอม. GroupDocs.Search สามารถทำดัชนี 1 million เอกสารพร้อมความหน่วงของการค้นหาต่ำกว่า 200 ms บนฮาร์ดแวร์มาตรฐาน.

**Q: Is GroupDocs.Search suitable for real‑time search scenarios?**  
A: แน่นอน—เมื่อดัชนีถูกสร้าง, คำค้นทำงานในระดับมิลลิวินาที, ทำให้เหมาะกับกล่องค้นหาแบบโต้ตอบและฟีเจอร์ auto‑complete.

**Q: Can I integrate this library into an existing Java project?**  
A: ใช่. เพิ่ม dependency ของ Maven หรือ JAR, สร้างอ็อบเจกต์ `Index` ตามที่แสดง, แล้วคุณพร้อมใช้คำค้นโดยไม่ต้องแก้ไขโค้ดเดิม.

---

**อัปเดตล่าสุด:** 2026-05-28  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## บทเรียนที่เกี่ยวข้อง

- [สร้างดัชนีการค้นหา Java – บทเรียน GroupDocs.Search](/search/java/)
- [เพิ่มเอกสารลงในดัชนี – บทเรียน GroupDocs.Search Java](/search/java/document-management/)
- [สร้างดัชนีการค้นหา - บทเรียน GroupDocs.Search Java](/search/java/advanced-features/)
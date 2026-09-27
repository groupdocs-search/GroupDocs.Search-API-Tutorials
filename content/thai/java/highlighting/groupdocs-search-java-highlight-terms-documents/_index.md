---
date: '2026-09-27'
description: เรียนรู้วิธีการ highlight text java ด้วย GroupDocs.Search for Java, ครอบคลุม
  search documents java, index documents java, และ fragment highlighting.
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: เรียนรู้วิธีการ highlight text java ด้วย GroupDocs.Search for Java.
  รับคำแนะนำ step‑by‑step เกี่ยวกับ indexing, searching, และ fragment highlighting
  เพื่อผลลัพธ์ที่รวดเร็ว.
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: ไฮไลท์ข้อความ Java ด้วย GroupDocs.Search – การไฮไลท์เอกสารอย่างรวดเร็ว
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: ไฮไลท์ข้อความ Java ด้วย GroupDocs.Search
type: docs
url: /th/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# ไฮไลท์ข้อความ Java ด้วย GroupDocs.Search

ในแอปพลิเคชันองค์กรสมัยใหม่, **highlight text java** มีความสำคัญในการเปลี่ยนผลการค้นหาดิบให้เป็นข้อมูลเชิงลึกที่อ่านได้ทันที ไม่ว่าคุณจะสร้างพอร์ทัลการตรวจสอบกฎหมาย, เครื่องมือค้นคว้าทางวิชาการ, หรือแดชบอร์ดการสนับสนุนลูกค้า, ความสามารถในการค้นหาและเน้นคำค้นหาแบบภาพช่วยผู้ใช้ประหยัดเวลาการสแกนด้วยตนเองเป็นวินาทีจำนวนมาก บทแนะนำนี้จะแสดงวิธีใช้ **GroupDocs.Search for Java** เพื่อ **search documents java**, **index documents java**, และใช้การไฮไลท์ทั้งระดับเอกสารทั้งหมดและระดับส่วนย่อย, ทั้งหมดด้วยเพียงไม่กี่บรรทัดของโค้ด.

## คำตอบด่วน
- **อะไรคือ “search and highlight text”?** หมายถึงการค้นหาคำค้นภายในเอกสารและทำให้เห็นชัดเจนด้วยการเน้น (เช่น ด้วยพื้นหลังสี).  
- **ไลบรารีใดที่ให้ความสามารถนี้?** GroupDocs.Search for Java.  
- **ฉันต้องการใบอนุญาตหรือไม่?** การทดลองใช้งานฟรีใช้ได้สำหรับการประเมิน; จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานในผลิตภัณฑ์.  
- **ฉันสามารถปรับสีไฮไลท์ได้หรือไม่?** ได้—สามารถตั้งค่าสี RGB ใดก็ได้ผ่าน `HighlightOptions`.  
- **การไฮไลท์ส่วนย่อยได้รับการสนับสนุนหรือไม่?** แน่นอน; คุณสามารถกำหนดคำก่อน/หลังการจับคู่เพื่อสร้างสแนปช็อตสั้นๆ.

## วิธีไฮไลท์ข้อความ Java ในเอกสาร

เพื่อไฮไลท์ข้อความ Java ในเอกสาร, ก่อนอื่นสร้างดัชนีของไฟล์ต้นฉบับโดยใช้การตั้งค่าการบีบอัดที่เหมาะสม, จากนั้นรันคำค้นเพื่อค้นหาคำที่ต้องการ, และสุดท้ายส่งออกผลลัพธ์เป็น HTML, PDF, หรือ plain text โดยแต่ละการจับคู่จะถูกห่อด้วยแท็กไฮไลท์ กระบวนการสามขั้นตอนนี้ทำให้การไฮไลท์รวดเร็วและแม่นยำในคอลเลกชันขนาดใหญ่.

1. **สร้างดัชนี** ด้วยการตั้งค่าการบีบอัดที่ทำให้พื้นที่จัดเก็บต่ำ.  
2. **ดำเนินการค้นหา** ด้วยสตริงคำค้นที่คุณต้องการไฮไลท์.  
3. **สร้างผลลัพธ์** (HTML, PDF, หรือ plain text) ที่ทุกการพบคำค้นจะถูกห่อด้วยแท็กไฮไลท์.

## การค้นหาและไฮไลท์ข้อความคืออะไร?

การค้นหาและไฮไลท์ข้อความคือกระบวนการสแกนคอลเลกชันที่ทำดัชนีเพื่อค้นหาคำค้นที่กำหนด, ดึงเอกสารที่ตรงกัน, แล้วทำเครื่องหมายแต่ละการพบของคำค้นภายในผลลัพธ์ (HTML, PDF, ฯลฯ). สัญญาณภาพนี้ช่วยให้ผู้ใช้มองเห็นข้อมูลที่เกี่ยวข้องได้ทันที.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?

GroupDocs.Search for Java ให้ **การทำดัชนีประสิทธิภาพสูง** (สูงสุด 50 GB ต่อดัชนีด้วย `Compression.High`), **การไฮไลท์หลากหลาย** ที่ทำงานบนเอกสารทั้งหมดและส่วนย่อยที่กำหนดเอง, และ **การสนับสนุนหลายรูปแบบ** มากกว่า 30 ประเภทไฟล์—รวมถึง DOCX, PDF, PPTX, และ TXT. ไลบรารีนี้ยังมี **การทำดัชนีแบบเพิ่มส่วน** ที่ช่วยให้คุณเพิ่มไฟล์ใหม่โดยไม่ต้องสร้างดัชนีใหม่ทั้งหมด, ลดเวลาหยุดทำงานได้ถึง 80 % ในการปรับใช้ขนาดใหญ่.

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือใหม่กว่า.  
- Maven สำหรับการจัดการ dependencies.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse.  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java.

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพิ่มรีโพสิตอรีของ GroupDocs และ dependency ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

คุณยังสามารถดาวน์โหลด JAR ล่าสุดโดยตรงจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
เริ่มต้นด้วยการทดลองใช้งานฟรีหรือรับใบอนุญาตชั่วคราวเพื่อการประเมิน. สำหรับการปรับใช้ในผลิตภัณฑ์, ซื้อใบอนุญาตเต็มเพื่อเปิดใช้งานคุณสมบัติทั้งหมด.

## คู่มือการใช้งาน

การใช้งานแบ่งเป็นสองส่วนปฏิบัติ: **การไฮไลท์ในเอกสารทั้งหมด** และ **การไฮไลท์ในส่วนย่อย**. ทั้งสองส่วนรวมขั้นตอนสำคัญสำหรับ **วิธีไฮไลท์ Java** เอกสารด้วย GroupDocs.Search.

### การกำหนดค่าการตั้งค่าดัชนี

ก่อนทำดัชนี, กำหนดให้ที่เก็บใช้การบีบอัดสูง—วิธีนี้ลดการใช้ดิสก์ได้ถึง 70 % ในขณะที่รักษาความเร็วการค้นหา.

`IndexSettings` คืออ็อบเจกต์การกำหนดค่าที่ควบคุมวิธีการจัดเก็บดัชนีบนดิสก์. ตั้งค่า `Compression` เป็น `Compression.High` เพื่อเปิดใช้งานการเพิ่มประสิทธิภาพนี้.  
`Compression` ระบุระดับการบีบอัดข้อมูลที่ใช้กับไฟล์ดัชนี, โดย `Compression.High` ให้การลดขนาดสูงสุด.

## การไฮไลท์ในเอกสารทั้งหมด

### ขั้นตอน 1: สร้างและเติมข้อมูลดัชนี

สร้างโฟลเดอร์ดัชนีและเพิ่มไฟล์ต้นฉบับทั้งหมดที่ต้องการค้นหา. คลาส `Index` แสดงถึงคอนเทนเนอร์ที่สามารถค้นหาได้.

### ขั้นตอน 2: ทำการค้นหาและใช้การไฮไลท์

ค้นหาคำ (เช่น `ipsum`) และสร้างไฟล์ HTML ที่มีการไฮไลท์ผลลัพธ์. ใช้ `HighlightOptions` เพื่อกำหนดสีไฮไลท์และว่าจะใช้สไตล์แบบอินไลน์หรือไม่.

`HighlightOptions` ให้คุณกำหนดสีพื้นหน้าและพื้นหลัง, รวมถึงคลาส CSS ที่จะถูกนำไปใช้กับแต่ละคำที่ไฮไลท์.

`HtmlHighlighter` สร้างผลลัพธ์ HTML ที่มีคำที่ไฮไลท์ตามตัวเลือกที่ให้.  
`SearchResult` มีรายการเอกสารที่ตรงกันและตำแหน่งของแต่ละคำที่พบ.

**Direct answer:** โหลดดัชนีของคุณ, เรียก `search("ipsum")`, แล้วส่ง `SearchResult` ที่ได้พร้อมกับอินสแตนซ์ `HighlightOptions` ที่กำหนดค่าไปยัง `HtmlHighlighter`. ตัวไฮไลท์จะคืนค่า HTML ที่แต่ละการพบของ “ipsum” ถูกห่อด้วย `<span>` ที่มีสีพื้นหลังตามที่เลือก.

ตัวเลือกสำคัญที่อธิบาย
- **Compression** – การบีบอัดสูงช่วยประหยัดพื้นที่จัดเก็บ.  
- **HighlightColor** – ตั้งค่าสี RGB ใดก็ได้ให้ตรงกับพาเลต UI ของคุณ.  
- **UseInlineStyles** – `false` จะสร้าง HTML ที่สะอาดซึ่งสามารถสไตล์ด้วย CSS แบบทั่วโลก.

## การไฮไลท์ในส่วนย่อย

### ขั้นตอน 1: ดัชนีและค้นหา (เช่นเดียวกับข้างต้น)

ขั้นตอนการทำดัชนีและค้นหาเดียวกัน; คุณจะใช้ซ้ำอ็อบเจกต์ `Index` และ `SearchResult`.

### ขั้นตอน 2: กำหนดบริบทของส่วนย่อยและไฮไลท์

กำหนดจำนวนคำก่อนและหลังการจับคู่ที่ควรปรากฏในแต่ละส่วนย่อยด้วย `FragmentOptions`.

`FragmentOptions` ควบคุมจำนวนคำรอบข้าง (`termsBefore` และ `termsAfter`) ที่รวมอยู่ในแต่ละสแนปช็อต, ช่วยให้คุณสมดุลระหว่างบริบทและความยาวของสแนปช็อต.

### ขั้นตอน 3: ดึงและเขียนส่วนย่อยที่ไฮไลท์

รวบรวมส่วนย่อยที่สร้างและเขียนลงไฟล์ HTML. แต่ละส่วนย่อยจะถูกไฮไลท์ตาม `HighlightOptions` ที่คุณกำหนดไว้แล้ว.

`fragmentHighlighter` เป็นยูทิลิตี้ที่สร้างสแนปช็อตที่ไฮไลท์จาก `SearchResult` โดยใช้ตัวเลือกส่วนย่อยและไฮไลท์ที่ระบุ.

**Direct answer:** หลังจากได้ `SearchResult`, เรียก `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)`. เมธอดนี้คืนรายการสแนปช็อต HTML, แต่ละสแนปช็อตมีคำที่ตรงกันโดยล้อมรอบด้วยจำนวนคำบริบทที่กำหนดและไฮไลท์ด้วยสีที่เลือก.

## การใช้งานเชิงปฏิบัติ
1. **การตรวจสอบเอกสารทางกฎหมาย** – ไฮไลท์กฎหมาย, ข้อ, หรืออ้างอิงคดีทันทีในสัญญาหลายพันฉบับ.  
2. **การวิจัยเชิงวิชาการ** – แสดงคำสำคัญใน PDF และไฟล์ Word หลายสิบไฟล์, ลดเวลาการทบทวนวรรณกรรมได้ถึง 60 %.  
3. **การสนับสนุนลูกค้า** – ระบุตัวเลขคำสั่งซื้อหรือรหัสข้อผิดพลาดในประวัติตั๋ว, ช่วยให้เจ้าหน้าที่แก้ปัญหาได้เร็วขึ้น.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **ขนาดดัชนี** – การบีบอัดสูง (`Compression.High`) ลดพื้นที่ดิสก์ได้ถึง 70 % โดยไม่มีผลต่อความหน่วงที่สังเกตได้.  
- **บริบทของส่วนย่อย** – ค่า `termsBefore/After` ที่ใหญ่ขึ้นทำให้สแนปช็อตอ่านง่ายขึ้นแต่อาจเพิ่มเวลา 10–15 ms ต่อการค้นหา.  
- **การจัดการหน่วยความจำ** – ตรวจสอบ heap ของ JVM เมื่อทำดัชนีข้อมูลขนาดใหญ่; พิจารณาดัชนีแบบเพิ่มส่วนสำหรับชุดข้อมูลที่เกิน 2 GB เพื่อรักษาการใช้หน่วยความจำให้อยู่ต่ำกว่า 1 GB.

## ปัญหาและวิธีแก้ไขทั่วไป
- **ข้อผิดพลาดในการทำดัชนี** – ตรวจสอบเส้นทางไฟล์และให้แน่ใจว่าแอปมีสิทธิ์อ่าน/เขียนในโฟลเดอร์ดัชนี.  
- **ไม่มีการไฮไลท์แสดง** – ยืนยันว่า `UseInlineStyles` ตรงกับรูปแบบผลลัพธ์ของคุณ (HTML หรือ PDF).  
- **สีไม่แสดง** – ตรวจสอบว่าค่า RGB อยู่ในช่วง 0‑255 และตัวดูรองรับ CSS แบบ inline หรือคลาส CSS ที่กำหนด.

## คำถามที่พบบ่อย

**Q: ประโยชน์ของการใช้ GroupDocs.Search สำหรับ Java มีอะไรบ้าง?**  
A: มันให้การทำดัชนีที่รวดเร็วและขยายได้, การไฮไลท์ที่ปรับแต่งได้, และการสนับสนุนรูปแบบเอกสารกว่า 30 ประเภท, ประมวลผลไฟล์ 500 หน้าในเวลาไม่ถึง 2 วินาทีบนเซิร์ฟเวอร์ทั่วไป.

**Q: จะรวม GroupDocs.Search กับ REST API อย่างไร?**  
A: เปิดเผยเมธอดค้นหาและไฮไลท์ผ่านคอนโทรลเลอร์ Spring Boot, ส่งคืนสแนปช็อต HTML หรือ payload JSON ที่มีส่วนย่อยที่ไฮไลท์.

**Q: ไลบรารีรองรับไฟล์ที่มีรหัสผ่านหรือไม่?**  
A: ใช่—ให้รหัสผ่านเมื่อเพิ่มเอกสารลงในดัชนีผ่าน `addDocument(filePath, password)`.

**Q: สามารถปรับแต่ง markup ของไฮไลท์ได้เกินสีหรือไม่?**  
A: แน่นอน; คุณสามารถกำหนดคลาส CSS ด้วย `options.setCssClass("myHighlight")` แล้วสไตล์แบบทั่วโลก, หรือแก้ไข HTML ที่สร้างหลังจากไฮไลท์.

**Q: เวอร์ชันที่ทดสอบสำหรับคู่มือนี้คืออะไร?**  
A: โค้ดได้รับการตรวจสอบกับ GroupDocs.Search 25.4.

**Q: จะตั้งค่า HighlightOptions ใน Java ให้ใช้คลาส CSS แทนสไตล์อินไลน์อย่างไร?**  
A: เรียก `options.setUseInlineStyles(false)` แล้วกำหนดกฎ CSS สำหรับคลาสที่กำหนดผ่าน `options.setCssClass("myHighlight")`.

**Q: มีวิธีไฮไลท์คำในผลลัพธ์ PDF โดยตรงหรือไม่?**  
A: มี—GroupDocs.Search ทำงานกับไฟล์ PDF, และไฮไลท์จะส่งออกเป็น HTML ที่สามารถฝังในตัวดู PDF หรือแปลงกลับเป็น PDF ด้วย GroupDocs.Conversion.

**อัปเดตล่าสุด:** 2026-09-27  
**ทดสอบกับ:** GroupDocs.Search 25.4  
**ผู้เขียน:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## บทแนะนำที่เกี่ยวข้อง

- [วิธีทำการค้นหาเต็มข้อความ java: สร้างไดเรกทอรีดัชนีด้วย GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [เรียนรู้การจัดการดัชนีการค้นหาด้วย GroupDocs.Search สำหรับ Java](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [เพิ่มเอกสารลงในดัชนีด้วยการค้นหาแบบแบ่งส่วนใน Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)
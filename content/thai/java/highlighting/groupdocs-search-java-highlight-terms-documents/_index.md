---
date: '2025-12-26'
description: เรียนรู้วิธีการค้นหาและไฮไลท์ข้อความในเอกสารโดยใช้ GroupDocs.Search สำหรับ
  Java. สำรวจเทคนิคการไฮไลท์ทั้งเอกสารเต็มและส่วนย่อย.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: ค้นหาและไฮไลท์ข้อความด้วย GroupDocs.Search สำหรับ Java
type: docs
url: /th/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# ค้นหาและไฮไลท์ข้อความในเอกสารด้วย GroupDocs.Search สำหรับ Java

ในยุคดิจิทัลปัจจุบัน การ **ค้นหาและไฮไลท์ข้อความ** ในคอลเลกชันเอกสารขนาดใหญ่เป็นความต้องการทั่วไป ไม่ว่าคุณจะกำลังสร้างเครื่องมือรีวิวกฎหมาย, พอร์ทัลการวิจัยทางวิชาการ, หรือแดชบอร์ดสนับสนุนลูกค้า การสามารถค้นหาและเน้นคำสำคัญได้ทันทีช่วยปรับปรุงการใช้งานอย่างมาก ในคู่มือฉบับครอบคลุมนี้ คุณจะได้เรียนรู้วิธีการทำ **ค้นหาและไฮไลท์ข้อความ** ด้วย GroupDocs.Search สำหรับ Java—ครอบคลุมทั้งการไฮไลท์เอกสารทั้งหมดและการไฮไลท์ระดับส่วนย่อยเพื่อให้ได้บริบทที่เน้น

## คำตอบอย่างรวดเร็ว
- **อะไรคือความหมายของ “search and highlight text”?** หมายถึงการค้นหาคำค้นในเอกสารและทำให้เห็นชัดเจนด้วยการเน้นสี (เช่น การใช้สีพื้นหลัง).
- **ไลบรารีใดที่ให้ความสามารถนี้?** GroupDocs.Search for Java.
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.
- **ฉันสามารถปรับสีไฮไลท์ได้หรือไม่?** ได้—สามารถตั้งค่าสี RGB ใดก็ได้ผ่าน `HighlightOptions`.
- **การไฮไลท์ส่วนย่อยได้รับการสนับสนุนหรือไม่?** แน่นอน; คุณสามารถกำหนดคำก่อน/หลังการจับคู่เพื่อสร้างสแนปช็อตสั้น ๆ.

## การค้นหาและไฮไลท์ข้อความคืออะไร?
การค้นหาและไฮไลท์ข้อความเป็นกระบวนการสแกนดัชนีเอกสารตามคำค้นที่กำหนด, ดึงเอกสารที่ตรงกัน, แล้วทำเครื่องหมายแต่ละตำแหน่งของคำค้นภายในผลลัพธ์เอกสาร (HTML, PDF, ฯลฯ). สัญญาณภาพนี้ช่วยให้ผู้ใช้ปลายทางพบข้อมูลที่เกี่ยวข้องได้ทันที.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
- **การทำดัชนีที่มีประสิทธิภาพสูง** พร้อมการบีบอัดที่กำหนดค่าได้.
- **API การไฮไลท์ที่หลากหลาย** ทำงานบนเอกสารทั้งหมดและส่วนย่อยที่กำหนดเอง.
- **การสนับสนุนหลายรูปแบบ** (DOCX, PDF, PPTX, TXT, และอื่น ๆ).
- **การผสานรวม Maven อย่างง่าย** และ API ที่ชัดเจนสำหรับ Java.

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือใหม่กว่า.  
- Maven สำหรับการจัดการ dependencies.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse.  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java.

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพิ่มรีโพสิตอรีของ GroupDocs และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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

คุณยังสามารถดาวน์โหลด JAR ล่าสุดโดยตรงจากเว็บไซต์อย่างเป็นทางการ: [การปล่อย GroupDocs.Search สำหรับ Java](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
เริ่มต้นด้วยการทดลองใช้ฟรีหรือรับไลเซนส์ชั่วคราวสำหรับการประเมิน. สำหรับการใช้งานในสภาพแวดล้อมการผลิต, ซื้อไลเซนส์เต็มเพื่อเปิดใช้งานคุณสมบัติทั้งหมด.

## คู่มือการใช้งาน

การนำไปใช้จะแบ่งเป็นสองส่วนปฏิบัติ: **การไฮไลท์ในเอกสารทั้งหมด** และ **การไฮไลท์ในส่วนย่อย**. ทั้งสองส่วนรวมขั้นตอนสำคัญสำหรับ **วิธีการไฮไลท์เอกสาร Java** ด้วย GroupDocs.Search.

### การกำหนดค่าการตั้งค่าดัชนี
ก่อนทำการทำดัชนี, กำหนดค่าที่เก็บข้อมูลให้ใช้การบีบอัดสูง—ซึ่งช่วยลดการใช้ดิสก์ขณะยังคงความเร็วในการค้นหา.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### การไฮไลท์ในเอกสารทั้งหมด

#### ขั้นตอน 1: สร้างและเติมข้อมูลดัชนี
สร้างโฟลเดอร์ดัชนีและเพิ่มไฟล์ต้นฉบับทั้งหมดที่คุณต้องการค้นหา.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### ขั้นตอน 2: ทำการค้นหาและใช้การไฮไลท์
ค้นหาคำ (เช่น `ipsum`) และสร้างไฟล์ HTML ที่มีการไฮไลท์ผลลัพธ์ที่ตรงกัน.

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

**อธิบายตัวเลือกสำคัญ**
- **Compression** – การบีบอัดสูงช่วยประหยัดพื้นที่จัดเก็บ.  
- **HighlightColor** – ตั้งค่าสี RGB ใดก็ได้ให้ตรงกับพาเลต UI ของคุณ.  
- **UseInlineStyles** – `false` จะสร้าง HTML ที่สะอาดและสามารถสไตล์ด้วย CSS อย่างทั่วโลก.

### การไฮไลท์ในส่วนย่อย

#### ขั้นตอน 1: ทำดัชนีและค้นหา (เช่นเดียวกับข้างบน)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### ขั้นตอน 2: กำหนดบริบทของส่วนย่อยและทำการไฮไลท์
ระบุจำนวนคำก่อนและหลังการจับคู่ที่ควรปรากฏในแต่ละส่วนย่อย.

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

#### ขั้นตอน 3: ดึงและเขียนส่วนย่อยที่ไฮไลท์
รวบรวมส่วนย่อยที่สร้างขึ้นและเขียนลงไฟล์ HTML.

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

## การประยุกต์ใช้งานจริง
1. **การตรวจสอบเอกสารทางกฎหมาย** – ไฮไลท์กฎหมาย, ข้อความ, หรือการอ้างอิงคดีโดยทันที.  
2. **การวิจัยทางวิชาการ** – แสดงคำศัพท์สำคัญในหลายสิบไฟล์ PDF และ Word.  
3. **การสนับสนุนลูกค้า** – ระบุตัวเลขคำสั่งซื้อหรือรหัสข้อผิดพลาดในประวัติตั๋ว.

## การพิจารณาประสิทธิภาพ
- **ขนาดดัชนี** – การบีบอัดสูง (`Compression.High`) ลดพื้นที่ดิสก์.  
- **บริบทของส่วนย่อย** – ค่า `termsBefore/After` ที่ใหญ่ขึ้นเพิ่มความแม่นยำแต่อาจส่งผลต่อความเร็ว.  
- **การจัดการหน่วยความจำ** – ตรวจสอบ heap ของ JVM เมื่อทำดัชนีข้อมูลจำนวนมาก; พิจารณาการทำดัชนีแบบเพิ่มขั้นสำหรับชุดข้อมูลขนาดใหญ่มาก.

## ปัญหาทั่วไปและวิธีแก้
- **ข้อผิดพลาดการทำดัชนี** – ตรวจสอบเส้นทางไฟล์และให้แน่ใจว่าแอปพลิเคชันมีสิทธิ์อ่าน/เขียน.  
- **ไม่มีการไฮไลท์แสดง** – ยืนยันว่า `UseInlineStyles` ตรงกับรูปแบบผลลัพธ์ของคุณ (HTML vs. PDF).  
- **สีไม่ถูกนำไปใช้** – ตรวจสอบว่าค่า RGB อยู่ในช่วง 0‑255 และตัวดู HTML รองรับสไตล์นั้น.

## คำถามที่พบบ่อย

**Q: ประโยชน์ของการใช้ GroupDocs.Search สำหรับ Java คืออะไร?**  
A: มันให้การทำดัชนีที่เร็วและขยายได้, การไฮไลท์ที่ปรับแต่งได้, และการสนับสนุนหลายรูปแบบเอกสาร.

**Q: ฉันจะรวม GroupDocs.Search กับ REST API อย่างไร?**  
A: เปิดเผยเมธอดการค้นหาและไฮไลท์ผ่านคอนโทรลเลอร์ Spring Boot, ส่งคืน HTML หรือ JSON payloads.

**Q: ไลบรารีนี้รองรับไฟล์ที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: ใช่—ให้รหัสผ่านเมื่อเพิ่มเอกสารลงในดัชนี.

**Q: ฉันสามารถปรับแต่ง markup ของการไฮไลท์นอกเหนือจากสีได้หรือไม่?**  
A: แน่นอน; คุณสามารถแทรกคลาส CSS ผ่าน `HighlightOptions` หรือแก้ไข HTML หลังการสร้าง.

**Q: เวอร์ชันที่ทดสอบสำหรับคู่มือนี้คืออะไร?**  
A: โค้ดได้รับการตรวจสอบกับ GroupDocs.Search 25.4.

---

**อัปเดตล่าสุด:** 2025-12-26  
**ทดสอบด้วย:** GroupDocs.Search 25.4  
**ผู้เขียน:** GroupDocs
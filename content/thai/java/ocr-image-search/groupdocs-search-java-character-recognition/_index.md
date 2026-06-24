---
date: '2026-03-17'
description: เรียนรู้วิธีสร้างดัชนีด้วย GroupDocs.Search สำหรับ Java, กำหนดค่าตัวอักษรปกติและผสม,
  และเพิ่มประสิทธิภาพการค้นหาสำหรับหมายเลขคดีทางกฎหมายและภาพ OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: วิธีสร้างดัชนีด้วยการจดจำตัวอักษรใน Java
type: docs
url: /th/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

:** By aligning the index’s character set with the OCR engine’s output, you reduce false negatives and improve overall search relevance.

Translate.

Then footer:

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

Translate labels but keep dates.

Now produce final markdown with translations.

Be careful to preserve all markdown formatting exactly.

Let's craft final answer.# วิธีสร้างดัชนีด้วยการรับรู้ตัวอักษรโดยใช้ GroupDocs.Search สำหรับ Java

ในแอปพลิเคชันที่มีเอกสารจำนวนมากในยุคปัจจุบัน, **วิธีสร้างดัชนี** ที่เคารพความละเอียดของข้อความของคุณ—เช่น เครื่องหมายขีดกลาง, เครื่องหมายขีดล่าง, หรือสัญลักษณ์เฉพาะของภาษา—เป็นสิ่งสำคัญสำหรับการดึงข้อมูลที่เร็วและแม่นยำ ในบทแนะนำนี้เราจะอธิบายการกำหนดค่าการรับรู้ตัวอักษรใน **GroupDocs.Search for Java**, ครอบคลุมทั้งตัวอักษรปกติ (letters, digits, underscores) และตัวอักษรผสม (เช่น hyphens) เมื่อเสร็จสิ้นคุณจะสามารถปรับดัชนีให้ตรงกับความต้องการของสถานการณ์ OCR หรือการค้นหาภาพของคุณ ไม่ว่าจะเป็นการทำดัชนีหมายเลขคดีทางกฎหมาย, ที่เก็บซอร์สโค้ด, หรือ PDF หลายภาษา

## คำตอบอย่างรวดเร็ว
- **What does “create custom search index” mean?** หมายถึงการกำหนดค่าดัชนีให้จัดการสัญลักษณ์เฉพาะเป็นตัวอักษรหรืออักขระผสม แทนที่จะละเลยมัน.  
- **Which library is used?** GroupDocs.Search for Java (v25.4 at the time of writing).  
- **Do I need a license?** การทดลองใช้ฟรีทำงานได้สำหรับการพัฒนา; จำเป็นต้องมีใบอนุญาตแบบชำระเงินสำหรับการใช้งานจริง.  
- **Can I index both PDFs and images?** ใช่—GroupDocs.Search รองรับ OCR บนรูปภาพและ PDF เมื่อกำหนดค่าอย่างถูกต้อง.  
- **Is Maven required?** Maven เป็นวิธีที่แนะนำสำหรับการจัดการ dependencies, แต่คุณก็สามารถใช้ Gradle หรือ JARs แบบแมนนวลได้.  

## ดัชนีการค้นหาแบบกำหนดเองคืออะไร?
ดัชนีการค้นหาแบบกำหนดเองให้คุณกำหนดวิธีที่เครื่องมือค้นหาแปลความหมายของตัวอักษร โดยค่าเริ่มต้นหลายสัญลักษณ์จะถูกละเลย ซึ่งอาจทำให้พลาดการจับคู่สำหรับสิ่งเช่นหมายเลขคดี (`2023-AB-456`) หรือโค้ดสแนปเพต (`my_variable`) การปรับพจนานุกรมอัลฟาเบตทำให้คุณควบคุมได้เต็มที่ว่าตัวเครื่องมือจะถือว่าอะไรเป็นข้อความที่สามารถค้นหาได้

## ทำไมต้องกำหนดค่าตัวอักษรปกติและตัวอักษรผสมสำหรับหมายเลขคดีทางกฎหมาย?
- **Regular characters** (letters, digits, underscores) จะถูกแยกเป็นโทเคน ทำให้การค้นหาแบบตรงกับตัวระบุเป็นไปได้อย่างแม่นยำ.  
- **Blended characters** (hyphens, slashes) จะทำให้โทเคนที่เกี่ยวข้องอยู่ด้วยกัน ป้องกันการแยกส่วนที่ไม่ต้องการของหมายเลขคดี, รหัสสินค้า, หรือเส้นทางไฟล์.  
- การกำหนดค่านี้ **optimizes search index** ประสิทธิภาพโดยลดการแยกโทเคนและเพิ่มความเกี่ยวข้องสำหรับเนื้อหา OCR  

## ข้อกำหนดเบื้องต้น
- **JDK 8** หรือใหม่กว่า ต้องติดตั้งไว้.  
- **Maven** สำหรับการจัดการ dependencies.  
- เข้าถึง **GroupDocs.Search for Java** library (ดาวน์โหลดผ่าน Maven หรือเว็บไซต์ทางการ).  

### ไลบรารีและ dependencies ที่จำเป็น
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ (ตามตัวอย่างด้านล่าง) ส่วน XML ต้องคงไว้โดยไม่เปลี่ยนแปลง

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

คุณสามารถดาวน์โหลด JAR ล่าสุดได้จาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
- **Free Trial** – เหมาะสำหรับการทดลองในขั้นต้น.  
- **Temporary License** – มีประโยชน์สำหรับวงจรการพัฒนาที่ยาวนาน.  
- **Production License** – จำเป็นสำหรับการใช้งานเชิงพาณิชย์.  

รับใบอนุญาตจากพอร์ทัลอย่างเป็นทางการ: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### การเริ่มต้นพื้นฐาน
โค้ดตัวอย่างด้านล่างแสดงวิธีการสร้างดัชนีเปล่าแบบขั้นต่ำ เก็บไว้ตามเดิม; เราจะต่อยอดจากนี้ในภายหลัง

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การติดตั้งผ่าน Maven
การกำหนดค่า Maven จากส่วน *ข้อกำหนดเบื้องต้น* คือทั้งหมดที่คุณต้องการ หลังจากเพิ่มแล้วให้รัน `mvn clean install` เพื่อดึงไบนารี

### ความต้องการการตั้งค่าสภาพแวดล้อม
- ตรวจสอบให้แน่ใจว่า **index folder** และ **document folder** มีอยู่บนดิสก์.  
- ใช้เส้นทางแบบ absolute หรือกำหนดค่า IDE ของคุณให้แก้ไขเส้นทาง relative อย่างถูกต้อง.  

## คู่มือการใช้งาน

ด้านล่างเราจะอธิบายสองฟีเจอร์ที่แตกต่างกัน: **regular characters** และ **blended characters** แต่ละฟีเจอร์ทำตามรูปแบบเดียวกัน—กำหนดเส้นทาง, สร้างดัชนี, ตั้งค่าพจนานุกรมอักขระ, และสุดท้ายทำการทำดัชนีเอกสารของคุณ

### ฟีเจอร์ 1 – ตัวอักษรปกติ

#### ภาพรวม
ตัวอักษรปกติจะถูกจัดการเป็นโทเคนอิสระ เหมาะเมื่อคุณต้องการให้ตัวเลข, ตัวอักษร, และเครื่องหมายขีดล่างสามารถค้นหาได้อย่างตรงตามที่ปรากฏ

#### การดำเนินการขั้นตอนต่อขั้นตอน

**1️⃣ Set Up Paths**  
กำหนดตำแหน่งที่ดัชนีจะถูกเก็บและตำแหน่งที่เอกสารต้นทางของคุณอยู่

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
สร้างอินสแตนซ์ของดัชนีและล้างการกำหนดค่าอัลฟาเบตที่มีอยู่ก่อนหน้า

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
สร้างอาร์เรย์ของอักขระที่รวมตัวเลข, ตัวอักษรละติน, และเครื่องหมายขีดล่าง

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
เพิ่มไฟล์ทั้งหมดจากโฟลเดอร์ต้นทางเข้าสู่ดัชนีที่กำหนดค่าใหม่

```java
index.add(documentFolder);
```

### ฟีเจอร์ 2 – ตัวอักษรผสม

#### ภาพรวม
ตัวอักษรผสม (เช่น hyphens) มักเชื่อมคำสองคำ การทำเครื่องหมายเป็น *blended* จะบอกเครื่องมือให้เก็บโทเคนรอบข้างไว้ด้วยกันระหว่างการทำดัชนี

#### การดำเนินการขั้นตอนต่อขั้นตอน

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
ที่นี่เราบอกพจนานุกรมให้ถือว่า hyphen เป็นอักขระผสม

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## การประยุกต์ใช้งานจริง

### กรณีการใช้งาน 1 – การจัดการเอกสารทางกฎหมาย
ไฟล์กฎหมายมักมีหมายเลขคดีเช่น `2023-AB-456` การกำหนดค่าเครื่องหมายขีดล่างและ hyphens ทำให้การค้นหาสามารถคืนผลลัพธ์ที่ตรงกันโดยไม่แยกตัวระบุ ช่วยให้คุณ **search legal case numbers** ได้อย่างมีประสิทธิภาพ

### กรณีการใช้งาน 2 – ที่เก็บซอร์สโค้ด
นักพัฒนาต้องการค้นหาโค้ดสแนปเพตที่เครื่องหมายขีดล่าง (`my_variable`) และ hyphens (`my-function`) มีความหมาย การรับรู้ตัวอักษรแบบกำหนดเองทำให้เครื่องมือค้นหาเคารพสัญลักษณ์เหล่านี้

### กรณีการใช้งาน 3 – ชุดข้อมูลหลายภาษา
เมื่อทำงานกับภาษาที่ใช้อัลฟาเบตเพิ่มเติม คุณสามารถ **extend Unicode character set** เพื่อรวมช่วงอักขระเหล่านั้นได้ รับประกันผลการค้นหาข้ามภาษาอย่างแม่นยำ

### กรณีการใช้งาน 4 – ดัชนี PDF รูปภาพ
หากคุณทำดัชนี PDF สแกนหรือไฟล์รูปภาพ ผลลัพธ์ OCR มักมีอักขระผสม การกำหนดค่าตัวอักษรปกติและผสมอย่างเหมาะสม **optimizes search index** ประสิทธิภาพสำหรับเนื้อหาที่มาจากภาพ

## ข้อควรพิจารณาด้านประสิทธิภาพ

- **Resource Management** – ตรวจสอบการใช้ heap; ดัชนีขนาดใหญ่จะได้ประโยชน์จากการ commit แบบ incremental.  
- **Garbage Collection** – ปล่อยออบเจ็กต์ `Index` เมื่อเสร็จเพื่อให้ JVM คืนหน่วยความจำ.  
- **Index Optimization** – เรียก `index.optimize()` อย่างสม่ำเสมอ (ถ้ามี) เพื่อบีบอัดดัชนีและเพิ่มความเร็วของการ query.  

## สรุป

คุณได้เรียนรู้ **วิธีสร้างดัชนี** ที่แยกแยะระหว่างตัวอักษรปกติและตัวอักษรผสมโดยใช้ GroupDocs.Search for Java การควบคุมในระดับละเอียดนี้ทำให้คุณสร้างโซลูชันการค้นหาที่รับรู้ OCR, มีประสิทธิภาพสูง และปรับให้เหมาะกับสภาพแวดล้อมทางกฎหมาย, การพัฒนา, หรือหลายภาษา

### ขั้นตอนต่อไป
- ทดลองเพิ่มช่วง Unicode เพิ่มเติมสำหรับอักษรที่ไม่ใช่ละติน.  
- ผสานการกำหนดค่าตัวอักษรกับฟีเจอร์อื่นของ GroupDocs.Search เช่น stemming หรือ synonyms.  
- รวมดัชนีเข้ากับ REST API เพื่อเปิดเผยความสามารถการค้นหาให้กับแอปพลิเคชัน front‑end.

## คำถามที่พบบ่อย

**Q:** *What is the purpose of `CharacterType.Letter`?*  
**A:** มันบอกดัชนีให้ถือว่าอักขระที่ระบุเป็นตัวอักษรปกติ ดังนั้นจะถูกแยกเป็นโทเคนแยกกันระหว่างการทำดัชนี

**Q:** *Can I mix regular and blended characters in the same index?*  
**A:** ได้—แค่เรียก `setRange` สำหรับแต่ละประเภท; พจนานุกรมจะจัดการการกำหนดค่าทั้งสองพร้อมกัน

**Q:** *Do I need to rebuild the index after changing the alphabet?*  
**A:** แน่นอน. การเปลี่ยนแปลงพจนานุกรมอักขระมีผลต่อการแยกโทเคน ดังนั้นคุณต้องทำการทำดัชนีใหม่ของเอกสารเพื่อให้กฎใหม่มีผล

**Q:** *Is there a limit to the number of custom characters I can define?*  
**A:** ไลบรารีรองรับช่วง Unicode ทั้งหมด; ประสิทธิภาพอาจลดลงหากคุณเพิ่มชุดอักขระที่ใหญ่มากเกินไป ดังนั้นควรจำกัดไว้ที่อักขระที่คุณต้องการใช้จริง

**Q:** *How does this affect OCR accuracy?*  
**A:** การทำให้ชุดอักขระของดัชนีสอดคล้องกับผลลัพธ์ของ OCR ช่วยลด false negatives และปรับปรุงความเกี่ยวข้องของการค้นหาโดยรวม

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
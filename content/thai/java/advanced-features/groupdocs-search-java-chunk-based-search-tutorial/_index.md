---
date: '2025-12-19'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและเปิดใช้งานการค้นหาแบบแบ่งส่วนใน Java
  ด้วย GroupDocs.Search เพื่อเพิ่มประสิทธิภาพสำหรับชุดเอกสารขนาดใหญ่.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: เพิ่มเอกสารลงในดัชนีด้วยการค้นหาแบบแบ่งส่วนใน Java
type: docs
url: /th/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# เพิ่มเอกสารลงในดัชนีด้วยการค้นหาแบบชั้นส่วนใน Java

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน ความสามารถในการ **เพิ่มเอกสารลงในดัชนี** อย่างรวดเร็วและจากนั้นทำการค้นหาแบบชั้นส่วนเป็นสิ่งสำคัญสำหรับแอปพลิเคชันใด ๆ ที่จัดการกับคอลเลกชันไฟล์ขนาดใหญ่ ไม่ว่าคุณจะทำงานกับสัญญากฎหมาย, คลังข้อมูลศูนย์ช่วยเหลือลูกค้า, หรือห้องสมุดการวิจัยขนาดมหาศาล บทเรียนนี้จะแสดงให้คุณเห็นขั้นตอนการตั้งค่า GroupDocs.Search สำหรับ Java เพื่อให้คุณสามารถทำดัชนีเอกสารได้อย่างมีประสิทธิภาพและดึงข้อมูลที่เกี่ยวข้องออกมาเป็นชั้นส่วนย่อย ๆ

## สิ่งที่คุณจะได้เรียนรู้
- วิธีสร้างดัชนีการค้นหาในโฟลเดอร์ที่ระบุ  
- ขั้นตอนการ **เพิ่มเอกสารลงในดัชนี** จากหลายตำแหน่ง  
- การกำหนดค่าตัวเลือกการค้นหาเพื่อเปิดใช้งานการค้นหาแบบชั้นส่วน  
- การทำการค้นหาแบบชั้นส่วนครั้งแรกและต่อเนื่อง  
- สถานการณ์จริงที่การค้นหาเอกสารแบบชั้นส่วนทำให้ประโยชน์สูงสุด

## คำตอบอย่างรวดเร็ว
- **ขั้นตอนแรกคืออะไร?** สร้างโฟลเดอร์ดัชนีการค้นหา  
- **จะรวมไฟล์หลายไฟล์ได้อย่างไร?** ใช้ `index.add()` สำหรับแต่ละโฟลเดอร์เอกสาร  
- **ตัวเลือกใดที่เปิดใช้งานการค้นหาแบบชั้นส่วน?** `options.setChunkSearch(true)`  
- **สามารถค้นหาต่อหลังจากชั้นแรกได้หรือไม่?** ได้, เรียก `index.searchNext()` พร้อมกับโทเคน  
- **ต้องมีลิขสิทธิ์หรือไม่?** ลิขสิทธิ์ทดลองหรือชั่วคราวใช้ได้สำหรับการพัฒนา; ต้องมีลิขสิทธิ์เต็มสำหรับการใช้งานในผลิตภัณฑ์

## ข้อกำหนดเบื้องต้น
เพื่อทำตามคู่มือนี้ โปรดตรวจสอบว่าคุณมี:

- **ไลบรารีที่ต้องการ**: GroupDocs.Search for Java 25.4 หรือใหม่กว่า  
- **การตั้งค่าสภาพแวดล้อม**: ติดตั้ง Java Development Kit (JDK) ที่เข้ากันได้  
- **ความรู้เบื้องต้น**: ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และ Maven

## การตั้งค่า GroupDocs.Search สำหรับ Java
เริ่มต้นโดยรวม GroupDocs.Search เข้าในโครงการของคุณผ่าน Maven:

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

หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### การรับลิขสิทธิ์
เพื่อทดลองใช้ GroupDocs.Search:

- **ทดลองฟรี** – ทดสอบคุณสมบัติหลักโดยไม่ต้องผูกมัด  
- **ลิขสิทธิ์ชั่วคราว** – เข้าถึงแบบขยายสำหรับการพัฒนา  
- **ซื้อ** – ลิขสิทธิ์เต็มสำหรับการใช้งานในผลิตภัณฑ์

### การเริ่มต้นและการตั้งค่าเบื้องต้น
สร้างดัชนีในโฟลเดอร์ที่คุณต้องการให้ข้อมูลที่สามารถค้นหาได้อยู่:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## วิธีเพิ่มเอกสารลงในดัชนี
เมื่อดัชนีมีอยู่แล้ว ขั้นตอนต่อไปที่สมเหตุสมผลคือการ **เพิ่มเอกสารลงในดัชนี** จากตำแหน่งที่ไฟล์ของคุณถูกจัดเก็บ

### 1. การสร้างดัชนี
**ภาพรวม**: ตั้งค่าไดเรกทอรีสำหรับดัชนีการค้นหา

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. การเพิ่มเอกสารลงในดัชนี
**ภาพรวม**: ดึงไฟล์จากหลายโฟลเดอร์ต้นทาง

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. การกำหนดค่าตัวเลือกการค้นหาเพื่อการค้นหาแบบชั้นส่วน
เปิดใช้งานการค้นหาแบบชั้นส่วนโดยปรับแต่งอ็อบเจ็กต์ options

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. การทำการค้นหาแบบชั้นส่วนครั้งแรก
รันคิวรีแรกโดยใช้ตัวเลือกที่เปิดใช้งานชั้นส่วน

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. การทำการค้นหาแบบชั้นส่วนต่อเนื่อง
วนลูปผ่านชั้นส่วนที่เหลือจนกว่าการค้นหาจะเสร็จสมบูรณ์

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## ทำไมต้องใช้การค้นหาแบบชั้นส่วน?
การค้นหาแบบชั้นส่วนจะแบ่งคอลเลกชันเอกสารขนาดมหาศาลออกเป็นชิ้นส่วนที่จัดการได้ ลดความกดดันของหน่วยความจำและเร่งความเร็วในการตอบสนอง โดยเฉพาะอย่างยิ่งจะเป็นประโยชน์เมื่อ:

1. **ทีมกฎหมาย** ต้องค้นหาข้อความเฉพาะในสัญญานับพันฉบับ  
2. **พอร์ทัลศูนย์ช่วยเหลือลูกค้า** ต้องแสดงบทความฐานความรู้ที่เกี่ยวข้องโดยทันที  
3. **นักวิจัย** ต้องคัดกรองข้อมูลชุดใหญ่โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ

## พิจารณาด้านประสิทธิภาพ
- **การจัดการหน่วยความจำ** – จัดสรรพื้นที่ heap เพียงพอ (`-Xmx`) สำหรับดัชนีขนาดใหญ่  
- **การตรวจสอบทรัพยากร** – คอยดูการใช้ CPU ระหว่างการทำดัชนีและการค้นหา  
- **การบำรุงรักษาดัชนี** – สร้างหรือทำความสะอาดดัชนีเป็นระยะเพื่อกำจัดข้อมูลที่ล้าสมัย

## ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| `OutOfMemoryError` ระหว่างการทำดัชนี | ขนาด heap ต่ำเกินไป | เพิ่มขนาด heap ของ JVM (`-Xmx2g` หรือมากกว่า) |
| ไม่ได้ผลลัพธ์ใด ๆ | โทเคนชั้นส่วนไม่ได้รับการประมวลผล | ตรวจสอบให้แน่ใจว่า loop `while` ทำงานจนกว่า `getNextChunkSearchToken()` จะเป็น `null` |
| การค้นหาช้า | ดัชนีไม่ได้ทำให้เป็นออพติไมซ์ | เรียก `index.optimize()` หลังจากการเพิ่มข้อมูลเป็นกลุ่ม |

## คำถามที่พบบ่อย

**ถาม: การค้นหาแบบชั้นส่วนคืออะไร?**  
ตอบ: การค้นหาแบบชั้นส่วนจะแบ่งชุดข้อมูลออกเป็นชิ้นย่อย ๆ ทำให้สามารถสืบค้นข้อมูลจำนวนมากได้อย่างมีประสิทธิภาพโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ

**ถาม: จะอัปเดตดัชนีด้วยไฟล์ใหม่อย่างไร?**  
ตอบ: เพียงเรียก `index.add()` พร้อมเส้นทางไปยังเอกสารใหม่; ดัชนีจะรวมไฟล์เหล่านั้นโดยอัตโนมัติ

**ถาม: GroupDocs.Search รองรับรูปแบบไฟล์ต่าง ๆ หรือไม่?**  
ตอบ: รองรับ PDF, DOCX, XLSX, PPTX และรูปแบบไฟล์ทั่วไปอื่น ๆ มากมาย

**ถาม: จุดคอขวดด้านประสิทธิภาพที่พบบ่อยคืออะไร?**  
ตอบ: ข้อจำกัดของหน่วยความจำและดัชนีที่ไม่ได้ทำให้เป็นออพติไมซ์เป็นสาเหตุหลัก; ควรจัดสรร heap เพียงพอและทำให้ดัชนีเป็นออพติไมซ์เป็นประจำ

**ถาม: จะหาเอกสารอธิบายรายละเอียดเพิ่มเติมได้ที่ไหน?**  
ตอบ: เยี่ยมชม [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) อย่างเป็นทางการเพื่อดูคู่มือเชิงลึกและอ้างอิง API

## แหล่งข้อมูล
- **เอกสาร**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **อ้างอิง API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **ดาวน์โหลด**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **สนับสนุนฟรี**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ลิขสิทธิ์ชั่วคราว**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**อัปเดตล่าสุด:** 2025-12-19  
**ทดสอบกับ:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

---
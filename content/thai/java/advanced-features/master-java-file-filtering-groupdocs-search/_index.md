---
date: '2026-02-21'
description: เรียนรู้วิธีการใช้ตัวกรองนามสกุลไฟล์ Java ด้วย GroupDocs.Search สำหรับ
  Java ซึ่งครอบคลุมตัวดำเนินการเชิงตรรกะ, วันที่สร้าง/แก้ไข, และตัวกรองเส้นทาง
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: ตัวกรองส่วนขยายไฟล์ Java ด้วย GroupDocs.Search – คู่มือ
type: docs
url: /th/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# เชี่ยวชาญการใช้ตัวกรองส่วนขยายไฟล์ java กับ GroupDocs.Search

การจัดการคลังเอกสารที่เพิ่มขึ้นอย่างต่อเนื่องอาจทำให้รู้สึกหนักหน่วงได้อย่างรวดเร็ว โดยเฉพาะเมื่อคุณต้องทำดัชนีเฉพาะประเภทไฟล์บางประเภท **ตัวกรองส่วนขยายไฟล์ java** ช่วยให้คุณบอก GroupDocs.Search ว่าต้องรวมหรือยกเว้นส่วนขยายใดบ้าง ทำให้คุณควบคุมขั้นตอนการทำดัชนีได้อย่างแม่นยำ ในคู่มือนี้เราจะอธิบายวิธีตั้งค่า GroupDocs.Search สำหรับ Java และแสดงวิธีผสานการกรองส่วนขยายไฟล์กับตัวดำเนินการตรรกะ AND, OR, และ NOT รวมถึงตัวกรองช่วงวันที่และเส้นทางไฟล์

## คำตอบสั้น ๆ
- **java file extension filter คืออะไร?** การกำหนดค่าที่บอก GroupDocs.Search ว่าส่วนขยายไฟล์ใดจะรวมหรือยกเว้นระหว่างการทำดัชนี  
- **ไลบรารีใดให้ฟีเจอร์นี้?** GroupDocs.Search for Java  
- **ต้องมีลิขสิทธิ์หรือไม่?** สามารถใช้รุ่นทดลองฟรีเพื่อประเมินผลได้; ต้องมีลิขสิทธิ์เต็มเพื่อใช้งานในสภาพแวดล้อมการผลิต  
- **สามารถผสานตัวกรองได้หรือไม่?** ได้ – คุณสามารถเชื่อมต่อการกรองส่วนขยาย, วันที่, ขนาด, และเส้นทางด้วยตรรกะ AND, OR, NOT  
- **รองรับ Maven หรือไม่?** แน่นอน – เพียงเพิ่ม dependency ของ GroupDocs.Search ลงใน `pom.xml` ของคุณ  

## java file extension filter คืออะไร?
**java file extension filter** คือชุดกฎที่ประเมินส่วนขยายของแต่ละไฟล์ก่อนส่งไปยังเครื่องยนต์ทำดัชนี โดยการระบุส่วนขยายเช่น `.txt`, `.pdf`, หรือ `.epub` คุณสามารถ **รวมไฟล์ตามส่วนขยาย** หรือ **ยกเว้นไฟล์ตามส่วนขยาย** เพื่อให้ดัชนีของคุณโฟกัสและผลการค้นหาเป็นประโยชน์มากขึ้น  

## ทำไมต้องใช้การกรองส่วนขยายไฟล์กับ GroupDocs.Search?
- **ประสิทธิภาพ:** การข้ามไฟล์ที่ไม่ต้องการช่วยลด I/O และเร่งความเร็วการทำดัชนี  
- **ประหยัดพื้นที่จัดเก็บ:** เก็บเฉพาะเอกสารที่เกี่ยวข้องในดัชนี ลดการใช้ดิสก์  
- **การปฏิบัติตามกฎ:** ป้องกันการทำดัชนีไฟล์ที่เป็นความลับหรือไม่รองรับโดยบังเอิญ  
- **ความยืดหยุ่น:** ผสานกับฟีเจอร์ **date range filter java** เพื่อกำหนดไฟล์ที่สร้างหรือแก้ไขในช่วงเวลาที่กำหนด  

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมีสิ่งต่อไปนี้แล้ว:

### ไลบรารีและ dependency ที่จำเป็น
- **GroupDocs.Search for Java**: เวอร์ชัน 25.4 หรือใหม่กว่า  
- **Java Development Kit (JDK)**: เวอร์ชันที่เข้ากันได้  

### การตั้งค่าสภาพแวดล้อม
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse หรือ IDE ที่รองรับ Maven ใด ๆ  

### ความรู้เบื้องต้นที่ต้องมี
- การเขียนโปรแกรม Java ขั้นพื้นฐาน  
- ความคุ้นเคยกับการทำ I/O ของไฟล์ใน Java  
- ความเข้าใจเกี่ยวกับ regular expressions และการจัดการ date‑time  

## การตั้งค่า GroupDocs.Search สำหรับ Java
เพื่อเริ่มใช้ GroupDocs.Search คุณต้องเพิ่มมันเป็น dependency ในโปรเจกต์ของคุณ

### การกำหนดค่า Maven
เพิ่ม repository และ dependency ด้านล่างนี้ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

#### การรับลิขสิทธิ์
1. **Free Trial** – ทดลองใช้ฟีเจอร์โดยไม่เสียค่าใช้จ่าย  
2. **Temporary License** – รับฟังก์ชันเต็มสำหรับระยะเวลาจำกัด  
3. **Purchase** – ซื้อไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต  

### การเริ่มต้นและตั้งค่าเบื้องต้น
เมื่อเพิ่มไลบรารีแล้ว ให้เริ่มต้นสภาพแวดล้อมการทำดัชนีของคุณ:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## คู่มือการใช้งาน
ต่อไปนี้เป็นการเจาะลึกแต่ละประเภทของตัวกรอง พร้อมอธิบาย **เหตุผลที่สำคัญ** และให้โค้ดขั้นตอน‑โดย‑ขั้นตอนที่คุณสามารถคัดลอกไปใช้ในโปรเจกต์ได้

### การกรองส่วนขยายไฟล์
กรองไฟล์ตามส่วนขยายระหว่างทำดัชนี เหมาะอย่างยิ่งเมื่อคุณต้องการประมวลผล e‑books (`.fb2`, `.epub`) และไฟล์ข้อความธรรมดา (`.txt`)

#### ภาพรวม
ใช้ `DocumentFilter.createFileExtension` เพื่อกำหนด whitelist ของส่วนขยาย

#### ขั้นตอนการทำงาน
1. **สร้างตัวกรอง**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **เริ่มต้น Index และเพิ่มเอกสาร**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรอง Logical NOT
ยกเว้นส่วนขยายเฉพาะ เช่น หน้าเว็บและ PDF เมื่อไม่ต้องการในสถานการณ์การค้นหาของคุณ

#### ขั้นตอนการทำงาน
1. **สร้างตัวกรองการยกเว้น**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **นำไปใช้กับ Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **เพิ่มเอกสาร**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรอง Logical AND
รวมเงื่อนไขหลายอย่าง – วันที่สร้าง, ส่วนขยาย, และขนาดไฟล์ – เพื่อให้ **เฉพาะไฟล์ที่ตรงตามทุกเงื่อนไข** เท่านั้นที่ถูกทำดัชนี

#### ภาพรวม
`DocumentFilter.createAnd` รวมตัวกรองหลายตัวเป็นกฎเดียว

#### ขั้นตอนการทำงาน
1. **กำหนดตัวกรอง**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **ผสานตัวกรอง**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **ทำดัชนีเอกสาร**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรอง Logical OR
รวมไฟล์ที่ตรงกับ **เงื่อนไขใดเงื่อนไขหนึ่ง** – มีประโยชน์เมื่อคุณต้องการจับไฟล์ข้อความขนาดเล็กและไฟล์ที่ไม่ใช่ข้อความขนาดใหญ่พร้อมกัน

#### ขั้นตอนการทำงาน
1. **กำหนดตัวกรอง**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **ผสานตัวกรองด้วยเงื่อนไขตรรกะ**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **สรุปตัวกรอง OR**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรองช่วงเวลาการสร้าง (Creation Time Filters)
กำหนดไฟล์ที่สร้างในช่วงเวลาที่ระบุ – ตัวอย่างคลาสสิกของ **date range filter java**

#### ขั้นตอนการทำงาน
1. **กำหนดตัวกรองช่วงวันที่**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **ทำดัชนีเอกสาร**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรองช่วงเวลาการแก้ไข (Modification Time Filters)
ยกเว้นไฟล์ที่ถูกแก้ไขหลังจากวันที่ตัดขาดที่กำหนด

#### ขั้นตอนการทำงาน
1. **กำหนดตัวกรอง**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **ทำดัชนีเอกสาร**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### การกรองเส้นทางไฟล์ (File Path Filtering)
จำกัดการทำดัชนีให้กับไฟล์ที่อยู่ในโฟลเดอร์เฉพาะหรือที่ตรงกับรูปแบบ – เหมาะสำหรับ **include files by extension** ภายในโครงสร้างไดเรกทอรีที่กำหนด

#### ขั้นตอนการทำงาน
1. **กำหนดตัวกรองเส้นทางไฟล์**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **เริ่มต้น Index และเพิ่มเอกสาร**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## ข้อผิดพลาดทั่วไป & เคล็ดลับ

- **ห้ามผสมเส้นทางแบบ absolute กับ relative** ในการตั้งค่าตัวกรองเดียวกัน – จะทำให้ไฟล์ถูกยกเว้นโดยไม่คาดคิด  
- **รีเซ็ต `IndexSettings`** เมื่อ **สลับชุดตัวกรอง**; มิฉะนั้นตัวกรองก่อนหน้าอาจคงอยู่  
- **ผสานขอบเขตความยาวสูงสุดกับตัวกรองส่วนขยาย** สำหรับคอลเลกชันขนาดใหญ่เพื่อควบคุมการใช้หน่วยความจำให้ต่ำลง  
- **เปิดใช้งาน logging** (`LoggingOptions.setEnabled(true)`) เพื่อดูเหตุผลที่ไฟล์ถูกปฏิเสธ  

## คำถามที่พบบ่อย

**Q: สามารถเปลี่ยนเกณฑ์การกรองหลังจากสร้างดัชนีแล้วได้หรือไม่?**  
A: ได้. ให้สร้างดัชนีใหม่ด้วย `DocumentFilter` ใหม่หรือใช้การทำดัชนีแบบ incremental พร้อมตั้งค่าอัปเดต  

**Q: ตัวกรองส่วนขยายไฟล์ java ทำงานกับไฟล์บีบอัด (เช่น ZIP) หรือไม่?**  
A: GroupDocs.Search สามารถทำดัชนีรูปแบบไฟล์บีบอัดที่รองรับได้ แต่ตัวกรองส่วนขยายจะใช้กับไฟล์บีบอัดเอง ไม่ได้ใช้กับไฟล์ภายใน ใช้ตัวกรองแบบซ้อนกันสำหรับการควบคุมระดับลึก  

**Q: จะดีบักเหตุผลที่ไฟล์ใดไฟล์หนึ่งถูกยกเว้นอย่างไร?**  
A: เปิด logging ของไลบรารี (`LoggingOptions.setEnabled(true)`) แล้วตรวจสอบ log – จะบอกว่า **ตัวกรองใดที่ปฏิเสธไฟล์นั้น**  

**Q: สามารถผสาน java file extension filter กับตัวกรอง regex แบบกำหนดเองได้หรือไม่?**  
A: แน่นอน. ใส่ตัวกรอง regex ภายใน `DocumentFilter.createAnd()` ร่วมกับตัวกรองส่วนขยาย  

**Q: การเพิ่มตัวกรองหลายตัวมีผลต่อประสิทธิภาพอย่างไร?**  
A: แต่ละตัวกรองเพิ่มภาระการประมวลผลเล็กน้อยระหว่างทำดัชนี แต่การลดปริมาณข้อมูลที่ทำดัชนีมักจะชดเชยค่าใช้จ่ายนั้นได้ ทดสอบกับตัวอย่างที่เป็นตัวแทนเพื่อหาจุดสมดุลที่เหมาะสม  

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
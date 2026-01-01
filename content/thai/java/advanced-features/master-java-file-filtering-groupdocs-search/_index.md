---
date: '2025-12-19'
description: เรียนรู้วิธีการใช้งานตัวกรองนามสกุลไฟล์ Java ด้วย GroupDocs.Search สำหรับ
  Java รวมถึงการใช้ตัวดำเนินการตรรกะ, วันที่สร้าง/แก้ไข, และตัวกรองเส้นทาง.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: ตัวกรองส่วนขยายไฟล์ Java ด้วย GroupDocs.Search – คู่มือ
type: docs
url: /th/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# เชี่ยวชาญการกรองส่วนขยายไฟล์ java ด้วย GroupDocs.Search

การจัดการคลังเอกสารที่เพิ่มขึ้นอย่างต่อเนื่องอาจทำให้รู้สึกท่วมท้นได้อย่างรวดเร็ว ไม่ว่าคุณจะต้องการทำดัชนีเฉพาะประเภทเอกสารบางประเภทหรือยกเว้นไฟล์ที่ไม่เกี่ยวข้อง **java file extension filter** จะให้การควบคุมระดับละเอียดว่าข้อมูลใดจะถูกประมวลผล ในคู่มือนี้เราจะพาคุณผ่านการตั้งค่า GroupDocs.Search สำหรับ Java และแสดงวิธีการผสานการกรองส่วนขยายไฟล์กับตัวดำเนินการ AND, OR, และ NOT รวมถึงการกรองช่วงวันที่และเส้นทางไฟล์

## คำตอบอย่างรวดเร็ว
- **java file extension filter คืออะไร?** การกำหนดค่าที่บอก GroupDocs.Search ว่าจะรวมหรือยกเว้นส่วนขยายไฟล์ใดระหว่างการทำดัชนี  
- **ไลบรารีใดให้ฟีเจอร์นี้?** GroupDocs.Search for Java  
- **ต้องการไลเซนส์หรือไม่?** สามารถใช้รุ่นทดลองฟรีเพื่อประเมินผล; ต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง  
- **สามารถผสานฟิลเตอร์ได้หรือไม่?** ได้ – คุณสามารถต่อเชื่อมฟิลเตอร์ส่วนขยาย, วันที่, ขนาด, และเส้นทางด้วยตรรกะ AND, OR, NOT  
- **รองรับ Maven หรือไม่?** แน่นอน – เพิ่ม dependency ของ GroupDocs.Search ลงใน `pom.xml` ของคุณ  

## บทนำ

กำลังประสบปัญหาในการจัดการคลังไฟล์ที่เพิ่มขึ้นอย่างมีประสิทธิภาพหรือไม่? ไม่ว่าคุณจะต้องการจัดระเบียบเอกสารตามประเภทหรือกรองไฟล์ที่ไม่จำเป็นระหว่างการทำดัชนี งานนี้อาจดูน่ากลัวหากไม่มีเครื่องมือที่เหมาะสม **GroupDocs.Search for Java** เป็นไลบรารีการค้นหาขั้นสูงที่ทำให้ความท้าทายเหล่านี้ง่ายขึ้นด้วยความสามารถในการกรองไฟล์ที่ทรงพลัง บทแนะนำนี้จะสอนคุณวิธีการใช้เทคนิคการกรองไฟล์ .NET ผ่าน GroupDocs.Search โดยเน้นที่ Logical AND, OR, และ NOT Filters  

### สิ่งที่คุณจะได้เรียนรู้
- การตั้งค่า GroupDocs.Search ในสภาพแวดล้อม Java ของคุณ  
- การใช้งานฟิลเตอร์ต่าง ๆ: File Extension, Logical Operators (AND, OR, NOT), Creation Time, Modification Time, File Path, และ Length  
- การประยุกต์ใช้ฟิลเตอร์เหล่านี้ในโลกจริงเพื่อการจัดการเอกสารที่มีประสิทธิภาพ  
- เคล็ดลับการเพิ่มประสิทธิภาพสำหรับงานทำดัชนีขนาดใหญ่  

พร้อมที่จะเปิดศักยภาพเต็มรูปแบบของการกรองไฟล์ใน Java หรือยัง? มาเริ่มต้นด้วยข้อกำหนดเบื้องต้นกันก่อน  

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้ครบแล้ว:

### ไลบรารีและ Dependencies ที่จำเป็น
- **GroupDocs.Search for Java**: เวอร์ชัน 25.4 หรือใหม่กว่า  
- **Java Development Kit (JDK)**: ตรวจสอบให้แน่ใจว่ามีเวอร์ชันที่เข้ากันได้ติดตั้งอยู่ในระบบของคุณ  

### การตั้งค่าสภาพแวดล้อม
- Integrated Development Environment (IDE): ใช้ IntelliJ IDEA, Eclipse หรือ IDE ใดก็ได้ที่รองรับโครงการ Maven  

### ความรู้พื้นฐานที่ต้องมี
- ความเข้าใจพื้นฐานของการเขียนโปรแกรม Java  
- ความคุ้นเคยกับการทำงาน I/O ของไฟล์ใน Java  
- ความเข้าใจเกี่ยวกับ regular expressions และการจัดการวัน‑เวลา  

## การตั้งค่า GroupDocs.Search สำหรับ Java
เพื่อเริ่มใช้ GroupDocs.Search คุณต้องเพิ่มเป็น dependency ในโครงการของคุณ ด้านล่างนี้คือวิธีทำ:

### การกำหนดค่า Maven
เพิ่ม repository และ dependency ต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)  

#### การรับไลเซนส์
1. **Free Trial**: เริ่มต้นด้วยรุ่นทดลองฟรีเพื่อสำรวจฟีเจอร์ของ GroupDocs.Search  
2. **Temporary License**: ขอรับไลเซนส์ชั่วคราวเพื่อเข้าถึงฟังก์ชันเต็มโดยไม่มีข้อจำกัด  
3. **Purchase**: สำหรับการใช้งานระยะยาว ให้ซื้อสมาชิกแบบสมัครสมาชิก  

### การเริ่มต้นพื้นฐานและการตั้งค่า
เมื่อเพิ่มไลบรารีแล้ว ให้ทำการเริ่มต้นสภาพแวดล้อมการทำดัชนีของคุณ:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## คู่มือการนำไปใช้
ต่อไปนี้เป็นวิธีการนำฟีเจอร์การกรองไฟล์ต่าง ๆ ไปใช้ด้วย GroupDocs.Search  

### การกรองตามส่วนขยายไฟล์
กรองไฟล์ตามส่วนขยายระหว่างการทำดัชนี ฟีเจอร์นี้มีประโยชน์เมื่อคุณต้องการประมวลผลเฉพาะประเภทเอกสารเช่น FB2, EPUB, และ TXT  

#### ภาพรวม
กรองเอกสารตามส่วนขยายไฟล์โดยใช้การกำหนดค่าฟิลเตอร์แบบกำหนดเอง  

#### ขั้นตอนการทำงาน
1. **สร้างฟิลเตอร์**:
    
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

### ฟิลเตอร์ Logical NOT
ยกเว้นส่วนขยายไฟล์เฉพาะระหว่างการทำดัชนี เช่น HTM, HTML, และ PDF  

#### ขั้นตอนการทำงาน
1. **สร้างฟิลเตอร์ยกเว้น**:
    
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

### ฟิลเตอร์ Logical AND
รวมหลายเงื่อนไขเพื่อรวมเฉพาะไฟล์ที่ตรงตามเงื่อนไขทั้งหมดที่กำหนด  

#### ภาพรวม
ใช้การดำเนินการ Logical AND เพื่อกรองไฟล์ตามเวลาสร้าง, ส่วนขยายไฟล์, และความยาว  

#### ขั้นตอนการทำงาน
1. **กำหนดฟิลเตอร์**:
    
    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **รวมฟิลเตอร์**:
    
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

### ฟิลเตอร์ Logical OR
รวมไฟล์ที่ตรงตามเงื่อนไขใดเงื่อนไขหนึ่งโดยใช้การดำเนินการ Logical OR  

#### ขั้นตอนการทำงาน
1. **กำหนดฟิลเตอร์**:
    
    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **รวมฟิลเตอร์ด้วยเงื่อนไข Logical**:
    
    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **สรุปฟิลเตอร์ OR**:
    
    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ฟิลเตอร์เวลาสร้าง (Creation Time)
กรองไฟล์ตามเวลาสร้างเพื่อรวมเฉพาะไฟล์ที่อยู่ในช่วงวันที่ที่กำหนด  

#### ขั้นตอนการทำงาน
1. **กำหนดฟิลเตอร์ช่วงวันที่**:
    
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

### ฟิลเตอร์เวลาแก้ไข (Modification Time)
ยกเว้นไฟล์ที่ถูกแก้ไขหลังจากวันที่เฉพาะ  

#### ขั้นตอนการทำงาน
1. **กำหนดฟิลเตอร์**:
    
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

### ฟิลเตอร์เส้นทางไฟล์ (File Path)
กรองไฟล์ตามเส้นทางไฟล์เพื่อรวมเฉพาะไฟล์ที่อยู่ในไดเรกทอรีที่กำหนด  

#### ขั้นตอนการทำงาน
1. **กำหนดฟิลเตอร์เส้นทางไฟล์**:
    
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

- **ห้ามผสานเส้นทางแบบ absolute และ relative** ในการกำหนดค่าฟิลเตอร์เดียวกัน – จะทำให้เกิดการยกเว้นที่ไม่คาดคิด  
- **อย่าลืมรีเซ็ต `IndexSettings`** เมื่อสลับจากชุดฟิลเตอร์หนึ่งไปยังอีกชุดหนึ่ง; มิฉะนั้นฟิลเตอร์ก่อนหน้าจะยังคงมีผลอยู่  
- **คอลเลกชันไฟล์ขนาดใหญ่** จะได้ประโยชน์จากการรวมขอบเขตความยาวสูงสุดกับฟิลเตอร์ส่วนขยายเพื่อรักษาการใช้หน่วยความจำให้ต่ำลง  

## คำถามที่พบบ่อย

**Q: สามารถเปลี่ยนเกณฑ์การกรองหลังจากสร้างดัชนีแล้วได้หรือไม่?**  
A: ได้ คุณสามารถสร้างดัชนีใหม่ด้วย `DocumentFilter` ใหม่หรือใช้การทำดัชนีแบบ incremental พร้อมตั้งค่าอัปเดต  

**Q: ฟิลเตอร์ java file extension filter ทำงานกับไฟล์บีบอัด (เช่น ZIP) หรือไม่?**  
A: GroupDocs.Search สามารถทำดัชนีรูปแบบไฟล์บีบอัดที่รองรับได้ แต่ฟิลเตอร์ส่วนขยายจะใช้กับไฟล์บีบอัดเอง ไม่ได้ใช้กับไฟล์ภายใน หากต้องการกรองไฟล์ภายในให้ใช้ฟิลเตอร์ซ้อนกัน  

**Q: จะดีบักว่าทำไมไฟล์ใดไฟล์หนึ่งถึงถูกยกเว้นได้อย่างไร?**  
A: เปิดการบันทึกของไลบรารี (`LoggingOptions.setEnabled(true)`) แล้วตรวจสอบ log ที่สร้างขึ้น – จะบอกรายละเอียดว่าฟิลเตอร์ใดบล็อกไฟล์นั้น  

**Q: สามารถผสาน java file extension filter กับฟิลเตอร์ regex ที่กำหนดเองได้หรือไม่?**  
A: แน่นอน คุณสามารถห่อฟิลเตอร์ regex ไว้ภายใน `DocumentFilter.createAnd()` พร้อมกับฟิลเตอร์ส่วนขยาย  

**Q: การเพิ่มฟิลเตอร์หลายตัวจะส่งผลต่อประสิทธิภาพอย่างไร?**  
A: ฟิลเตอร์แต่ละตัวจะเพิ่มภาระเล็กน้อยในระหว่างทำดัชนี แต่ประโยชน์จากการลดขนาดดัชนีมักจะชดเชยค่าใช้จ่ายนี้ได้ ทดสอบกับชุดตัวอย่างเพื่อหาจุดสมดุลที่เหมาะสม  

---

**อัปเดตล่าสุด:** 2025-12-19  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs
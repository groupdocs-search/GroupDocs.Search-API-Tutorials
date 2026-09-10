---
date: '2026-09-06'
description: เรียนรู้วิธีกรองส่วนขยายไฟล์ java โดยใช้ GroupDocs.Search สำหรับ Java
  ครอบคลุมตัวดำเนินการตรรกะ AND, OR, NOT, ตัวกรองช่วงวันที่ และตัวกรองเส้นทาง
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: กรองส่วนขยายไฟล์ java ด้วย GroupDocs.Search. เรียนรู้การรวมตัวกรองส่วนขยาย,
  ช่วงวันที่, และเส้นทางด้วยตัวดำเนินการตรรกะใน Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: กรองส่วนขยายไฟล์ java ด้วย GroupDocs.Search – คู่มือครบถ้วน
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: วิธีกรองส่วนขยายไฟล์ java ด้วย GroupDocs.Search
type: docs
url: /th/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# กรองนามสกุลไฟล์ java ด้วย GroupDocs.Search

ในบทแนะนำเชิงลึกนี้คุณจะได้เรียนรู้วิธี **filter file extensions java** เมื่อทำการจัดทำดัชนีเอกสารด้วย GroupDocs.Search. เมื่อจบคู่มือคุณจะสามารถรวมเฉพาะประเภทไฟล์ที่ต้องการ, ยกเว้นรูปแบบที่ไม่ต้องการ, และรวมกฎเหล่านั้นกับตัวกรองช่วงวันที่และเส้นทางโดยใช้ตัวดำเนินการตรรกะ AND, OR, และ NOT. วิธีนี้ทำให้ดัชนีของคุณเบาลง, เร่งความเร็วการค้นหา, และช่วยให้คุณปฏิบัติตามนโยบายการจัดการข้อมูล.

## คำตอบด่วน
- **java file extension filter คืออะไร?** เป็นกฎที่บอก GroupDocs.Search ว่านามสกุลไฟล์ใดจะรวมหรือยกเว้นในระหว่างการจัดทำดัชนี.  
- **ไลบรารีใดที่ให้คุณลักษณะนี้?** GroupDocs.Search for Java.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ฉันสามารถรวมตัวกรองได้หรือไม่?** ใช่ – คุณสามารถเชื่อมต่อตัวกรองนามสกุล, วันที่, ขนาด, และเส้นทางด้วยตรรกะ AND, OR, NOT.  
- **มันเข้ากันได้กับ Maven หรือไม่?** แน่นอน – เพิ่ม dependency ของ GroupDocs.Search ไปยัง `pom.xml` ของคุณ.

## java file extension filter คืออะไร?
A **java file extension filter** เป็นชุดกฎที่ประเมินนามสกุลของแต่ละไฟล์ก่อนที่จะส่งไปยังเครื่องมือจัดทำดัชนี. โดยระบุนามสกุลเช่น `.txt`, `.pdf`, หรือ `.epub`, คุณสามารถ **include files by extension** หรือ **exclude files by extension** เพื่อให้ดัชนีของคุณมีความมุ่งหมายและผลการค้นหาเกี่ยวข้อง.

## ทำไมต้องใช้การกรองนามสกุลไฟล์กับ GroupDocs.Search?
การกรองนามสกุลไฟล์ช่วยปรับปรุงประสิทธิภาพการจัดทำดัชนีโดยการยกเว้นรูปแบบที่ไม่เกี่ยวข้อง, ลดความต้องการพื้นที่จัดเก็บ, และช่วยให้ปฏิบัติตามกฎระเบียบโดยป้องกันเนื้อหาที่ไม่ต้องการเข้าสู่ดัชนี. นอกจากนี้ยังทำให้การตอบสนองคำค้นเร็วขึ้นเนื่องจากเครื่องมือค้นหาประมวลผลชุดข้อมูลที่เล็กลงและมีความเกี่ยวข้องมากขึ้น.

- **ประสิทธิภาพ:** การข้ามไฟล์ที่ไม่ต้องการลด I/O และเร่งความเร็วการจัดทำดัชนีได้ถึง 40 % ในคลังข้อมูลขนาดใหญ่.  
- **การประหยัดพื้นที่จัดเก็บ:** เอกสารที่เกี่ยวข้องเท่านั้นที่ถูกเก็บในดัชนี, ลดการใช้ดิสก์โดยเฉลี่ย 30 %.  
- **การปฏิบัติตาม:** ป้องกันการจัดทำดัชนีโดยบังเอิญของไฟล์ที่เป็นความลับหรือไม่รองรับ.  
- **ความยืดหยุ่น:** รวมกับคุณลักษณะ **date range filter java** เพื่อกำหนดเป้าหมายไฟล์ที่สร้างหรือแก้ไขในช่วงเวลาที่กำหนด.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

### ไลบรารีและ dependencies ที่จำเป็น
- **GroupDocs.Search for Java** – เวอร์ชัน 25.4 หรือใหม่กว่า (รองรับรูปแบบอินพุตกว่า 60 ประเภท).  
- **Java Development Kit (JDK)** – เวอร์ชันที่เข้ากันได้ใดก็ได้ (8 หรือใหม่กว่า).

### การตั้งค่าสภาพแวดล้อม
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse, หรือ IDE ที่เข้ากันได้กับ Maven ใดก็ได้.

### ความรู้เบื้องต้นที่จำเป็น
- พื้นฐานการเขียนโปรแกรม Java.  
- คุ้นเคยกับการทำงาน I/O ของไฟล์ใน Java.  
- เข้าใจ regular expressions และการจัดการวันที่‑เวลา.

## การตั้งค่า GroupDocs.Search สำหรับ Java
เพื่อเริ่มใช้ GroupDocs.Search, คุณต้องเพิ่มเป็น dependency ในโปรเจกต์ของคุณ.

### การกำหนดค่า Maven
เพิ่ม repository และการกำหนดค่า dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

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
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### การรับไลเซนส์
1. **Free trial** – สำรวจคุณลักษณะโดยไม่เสียค่าใช้จ่าย.  
2. **Temporary license** – รับฟังก์ชันเต็มในช่วงเวลาจำกัด.  
3. **Purchase** – ได้รับไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมจริง.

### การเริ่มต้นและตั้งค่าพื้นฐาน
เมื่อเพิ่มไลบรารีแล้ว, เริ่มต้นสภาพแวดล้อมการจัดทำดัชนีของคุณ. คลาส `IndexSettings` เก็บตัวเลือกการกำหนดค่าทั้งหมด, รวมถึงตัวกรอง.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## คู่มือการใช้งาน
ต่อไปนี้เราจะเจาะลึกแต่ละประเภทของตัวกรอง, อธิบาย **ทำไมจึงสำคัญ** และให้คำแนะนำทีละขั้นตอนที่คุณสามารถคัดลอกไปยังโปรเจกต์ของคุณ.

### การกรองนามสกุลไฟล์
กรองไฟล์ตามนามสกุลของพวกมันระหว่างการจัดทำดัชนี. เหมาะอย่างยิ่งเมื่อคุณต้องการประมวลผล e‑books (`.fb2`, `.epub`) และไฟล์ข้อความธรรมดา (`.txt`).

#### ภาพรวม
`DocumentFilter.createFileExtension` สร้าง whitelist ของนามสกุล.

#### ขั้นตอนการใช้งาน
1. **Create filter** – กำหนดนามสกุลที่คุณต้องการเก็บ.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – ใช้ตัวกรองเมื่อสร้าง `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรอง Logical NOT
ยกเว้นนามสกุลเฉพาะ, เช่น หน้าเว็บและ PDF, เมื่อไม่จำเป็นสำหรับสถานการณ์การค้นหาของคุณ.

#### ขั้นตอนการใช้งาน
1. **Create exclusion filter** – ระบุนามสกุลที่ต้องการปฏิเสธ.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – รวมตัวกรอง NOT กับกฎอื่น ๆ.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – เฉพาะไฟล์ที่ผ่านตัวกรองรวมจะถูกจัดทำดัชนี.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรอง Logical AND
รวมหลายเงื่อนไข—วันที่สร้าง, นามสกุล, และขนาดไฟล์—เพื่อให้ **เฉพาะไฟล์ที่ตรงตามทุกเกณฑ์** ถูกจัดทำดัชนี.

#### ภาพรวม
`DocumentFilter.createAnd` รวมหลายตัวกรองเป็นกฎเดียว.

#### ขั้นตอนการใช้งาน
1. **Define filters** – สร้างตัวกรองแยกสำหรับแต่ละเงื่อนไข.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – ใช้ตัวดำเนินการ AND เพื่อให้ต้องเป็นทุกเงื่อนไข.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – ส่งตัวกรองรวมไปยัง pipeline การจัดทำดัชนี.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรอง Logical OR
รวมไฟล์ที่ตรงกับ **เงื่อนไขใดก็ได้** ที่ระบุ—เป็นประโยชน์เมื่อคุณต้องการจับไฟล์ข้อความขนาดเล็กและไฟล์ที่ไม่ใช่ข้อความขนาดใหญ่.

#### ขั้นตอนการใช้งาน
1. **Define filters** – สร้างตัวกรองแยกสำหรับแต่ละเงื่อนไขทางเลือก.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – ใช้ตัวดำเนินการ OR.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – แนบตัวกรองรวมไปยังการกำหนดค่าดัชนี.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรองเวลาการสร้าง
กำหนดเป้าหมายไฟล์ที่สร้างในช่วงเวลาที่กำหนด—เป็นสถานการณ์ **date range filter java** คลาสสิก.

#### ขั้นตอนการใช้งาน
1. **Define date‑range filter** – ระบุวันที่เริ่มต้นและสิ้นสุด.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – เฉพาะไฟล์ที่มีเวลาสร้างอยู่ในช่วงที่กำหนดจะถูกจัดทำดัชนี.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### ตัวกรองเวลาการแก้ไข
ยกเว้นไฟล์ที่ถูกแก้ไขหลังจากวันที่ตัดขาดที่กำหนด.

#### ขั้นตอนการใช้งาน
1. **Define filter** – ตั้งค่า timestamp การแก้ไขสูงสุด.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – ไฟล์ที่ใหม่กว่าตัดขาดจะถูกละเว้น.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### การกรองเส้นทางไฟล์
จำกัดการจัดทำดัชนีให้กับไฟล์ที่อยู่ในโฟลเดอร์เฉพาะหรือที่ตรงกับรูปแบบ—เหมาะสำหรับ **include files by extension** ภายในโครงสร้างไดเรกทอรีที่กำหนด.

#### ขั้นตอนการใช้งาน
1. **Define file‑path filter** – ใช้รูปแบบ glob หรือ regex เพื่อจับคู่ไดเรกทอรี.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – ใช้ตัวกรองเส้นทางร่วมกับกฎอื่น ๆ.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## ข้อผิดพลาดทั่วไปและเคล็ดลับ
- **ห้ามผสานเส้นทางแบบ absolute และ relative** ในการกำหนดค่าตัวกรองเดียวกัน – อาจทำให้เกิดการยกเว้นที่ไม่คาดคิด.  
- **รีเซ็ต `IndexSettings`** เมื่อสลับชุดตัวกรอง; มิฉะนั้นตัวกรองก่อนหน้าจะคงอยู่.  
- **รวมขอบเขตความยาวสูงสุดกับตัวกรองนามสกุล** สำหรับคอลเลกชันขนาดใหญ่เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- LoggingOptions ควบคุมการกำหนดค่าการบันทึกสำหรับ GroupDocs.Search.  
- **เปิดใช้งานการบันทึก** (`LoggingOptions.setEnabled(true)`) เพื่อดูเหตุผลที่ไฟล์ถูกปฏิเสธ.  

## คำถามที่พบบ่อย
**Q: ฉันสามารถเปลี่ยนเกณฑ์ตัวกรองหลังจากสร้างดัชนีแล้วหรือไม่?**  
A: ใช่. สร้างดัชนีใหม่ด้วย `DocumentFilter` ใหม่หรือใช้การจัดทำดัชนีแบบเพิ่มส่วนโดยใช้การตั้งค่าอัปเดต.

**Q: ตัวกรอง java file extension ทำงานกับไฟล์บีบอัด (เช่น ZIP) หรือไม่?**  
A: GroupDocs.Search สามารถจัดทำดัชนีรูปแบบไฟล์บีบอัดที่รองรับได้, แต่ตัวกรองนามสกุลจะใช้กับไฟล์บีบอัดเอง, ไม่ใช่ไฟล์ภายใน. ใช้ตัวกรองซ้อนกันสำหรับการควบคุมที่ลึกขึ้น.

**Q: ฉันจะดีบักเหตุผลที่ไฟล์ใดไฟล์หนึ่งถูกยกเว้นอย่างไร?**  
A: เปิดการบันทึกของไลบรารี (`LoggingOptions.setEnabled(true)`) และตรวจสอบบันทึก – จะรายงานว่าตัวกรองใดปฏิเสธไฟล์แต่ละไฟล์.

**Q: สามารถรวมตัวกรอง java file extension กับตัวกรอง regex แบบกำหนดเองได้หรือไม่?**  
A: แน่นอน. ห่อหุ้มตัวกรอง regex ภายใน `DocumentFilter.createAnd()` ร่วมกับตัวกรองนามสกุล.

**Q: การเพิ่มตัวกรองหลายตัวมีผลต่อประสิทธิภาพอย่างไร?**  
A: แต่ละตัวกรองเพิ่มภาระเล็กน้อยระหว่างการจัดทำดัชนี, แต่การลดข้อมูลที่จัดทำดัชนีมักจะชดเชยค่าใช้จ่ายนั้น. ทดสอบด้วยตัวอย่างที่เป็นตัวแทนเพื่อหาสมดุลที่เหมาะที่สุด.

---

**อัปเดตล่าสุด:** 2026-09-06  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [รูปแบบวันที่แบบกำหนดเอง Java | การค้นหาช่วงวันที่ด้วย GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: การค้นหา Boolean ขั้นสูงด้วย GroupDocs.Search for Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [เพิ่มประสิทธิภาพการค้นหาด้วยเทคนิคการจัดทำดัชนีขั้นสูงใน GroupDocs.Search for Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


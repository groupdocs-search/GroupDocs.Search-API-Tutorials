---
date: '2026-01-08'
description: เรียนรู้วิธีการไฮไลท์ผลการค้นหาใน Java ด้วย GroupDocs.Search ในแอปพลิเคชัน
  Java, ตั้งค่าการค้นหาที่สามารถขยายได้, การปรับใช้บนเครือข่าย, และการไฮไลท์ผลลัพธ์.
keywords:
- GroupDocs.Search Java
- distributed searching Java
- highlight search results Java
title: ไฮไลท์ผลการค้นหาใน Java ด้วย GroupDocs.Search
type: docs
url: /th/java/licensing-configuration/groupdocs-search-java-implementation/
weight: 1
---

# ไฮไลท์ผลการค้นหา Java ด้วย GroupDocs.Search

หากคุณรู้สึกเหนื่อยกับการคัดกรองเอกสารจำนวนมากด้วยตนเอง, **highlight search results java** ให้วิธีที่เร็วและเชื่อถือได้ในการดึงข้อมูลที่คุณต้องการออกมา ในบทเรียนนี้เราจะอธิบายขั้นตอนการตั้งค่าเครือข่ายการค้นหาที่กระจาย, การทำดัชนีไฟล์ของคุณ, การรันคิวรี, และสุดท้ายการไฮไลท์ผลลัพธ์โดยตรงในเอกสาร เมื่อเสร็จสิ้นคุณจะมีโซลูชันพร้อมใช้งานในระดับผลิตที่สามารถขยายขนาดได้หลายโหนดและทำให้คำที่เกี่ยวข้องเด่นชัดทันที

## คำตอบสั้น
- **“highlight search results java” หมายถึงอะไร?** หมายถึงการทำเครื่องหมายคำสำคัญที่พบในเอกสารโดยใช้ไลบรารี Java เช่น GroupDocs.Search  
- **ฉันสามารถไฮไลท์หลายคำในเอกสารเดียวได้หรือไม่?** ได้ – ใช้ `HighlightOptions` เพื่อกำหนดจำนวนคำก่อน/หลังแต่ละผลลัพธ์ที่จะแสดง  
- **ต้องมีลิขสิทธิ์เพื่อรันตัวอย่างนี้หรือไม่?** ลิขสิทธิ์ทดลองหรือชั่วคราวใช้ได้สำหรับการทดสอบ; ต้องมีลิขสิทธิ์เต็มสำหรับการใช้งานในผลิตภัณฑ์  
- **ต้องใช้ Java เวอร์ชันใด?** Java 8 หรือใหม่กว่า  
- **วิธีนี้เหมาะกับคอลเลกชันเอกสารขนาดใหญ่หรือไม่?** แน่นอน – เครือข่ายการค้นหาจะกระจายการทำดัชนีและโหลดคิวรีไปยังหลายโหนด

## Highlight Search Results Java คืออะไร?
**Highlight search results java** คือกระบวนการรับคิวรีการค้นหา, หาชิ้นส่วนที่ตรงกันในเอกสารของคุณ, และทำให้ชิ้นส่วนนั้นเด่นชัด (เช่น การล้อมรอบด้วยเครื่องหมายหรือการคืนค่าเป็นสแนปช็อตที่ไฮไลท์) ทำให้ผู้ใช้เห็นบริบทของแต่ละผลลัพธ์โดยไม่ต้องเปิดไฟล์ทั้งหมด

## ทำไมต้องใช้ GroupDocs.Search สำหรับการไฮไลท์?
GroupDocs.Search มีเอนจินประสิทธิภาพสูงที่พร้อมใช้งาน รองรับรูปแบบไฟล์หลายสิบประเภท, การทำดัชนีแบบกระจาย, และไฮไลท์ชิ้นส่วนในตัว ช่วยให้คุณไม่ต้องเขียนพาร์เซอร์หรือจัดการโครงสร้างพื้นฐานการค้นหาเอง สามารถมุ่งเน้นที่ประสบการณ์ผู้ใช้ที่ราบรื่นได้

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 8+** – ตรวจสอบว่า `java -version` แสดง 1.8 หรือสูงกว่า  
- **Maven** – สำหรับการจัดการ dependencies  
- **GroupDocs.Search for Java 25.4** – เวอร์ชันที่ใช้ในคู่มือนี้ทั้งหมด  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse** (ไม่บังคับแต่แนะนำ)  
- ความรู้พื้นฐานเกี่ยวกับ Java และแนวคิดเครือข่าย

## การตั้งค่า GroupDocs.Search for Java

คุณสามารถเพิ่มไลบรารีเข้ามาในโปรเจกต์ได้ทั้งผ่าน Maven หรือดาวน์โหลด JAR โดยตรง

### การตั้งค่า Maven
เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณ:

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
หรือดาวน์โหลด JAR ล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### ขั้นตอนการรับลิขสิทธิ์
- **Free Trial:** เริ่มต้นด้วยการทดลองเพื่อสำรวจฟีเจอร์หลัก  
- **Temporary License:** รับลิขสิทธิ์ทดสอบระยะยาวจาก [this page](https://purchase.groupdocs.com/temporary-license/)  
- **Purchase:** ซื้อลิขสิทธิ์เต็มสำหรับการใช้งานในผลิตภัณฑ์

### การเริ่มต้นและตั้งค่าเบื้องต้น
สร้างอินสแตนซ์ `Index` ที่ชี้ไปยังโฟลเดอร์ที่เก็บดัชนีการค้นหา:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an instance of Index
        Index index = new Index("path/to/index/directory");
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## คู่มือการทำงาน

### วิธีไฮไลท์ผลการค้นหา Java ในเครือข่ายกระจาย

#### การกำหนดค่าเครือข่ายการค้นหา
แรกเริ่มกำหนดตำแหน่งที่เก็บเอกสารและพอร์ตที่เครือข่ายจะใช้

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/HighlightingResultsInNetwork/";
int basePort = 49116; // Change if port is busy

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **`basePath`** – โฟลเดอร์รากที่มีไฟล์ที่คุณต้องการทำดัชนี  
- **`basePort`** – พอร์ต TCP สำหรับการสื่อสารระหว่างโหนด; เลือกพอร์ตที่ยังไม่ได้ใช้

#### การปรับใช้โหนดเครือข่ายการค้นหา
ปรับใช้โหนดหนึ่งหรือหลายโหนดตามการกำหนดค่า โหนดแรกจะเป็น master

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```

- **`nodes`** – อาเรย์ของโหนดที่กำลังทำงานทั้งหมด  
- **`masterNode`** – ประสานงานการทำดัชนีและการกระจายคิวรี

#### การสมัครรับเหตุการณ์โหนดเครือข่ายการค้นหา
แนบ listener ไปยัง master node เพื่อรับการแจ้งเตือนแบบเรียลไทม์ (เช่น เมื่อการทำดัชนีเสร็จสิ้น)

```java
import com.groupdocs.search.scaling.events.*;

SearchNetworkNodeEvents.subscribe(masterNode);
```

#### การทำดัชนีไดเรกทอรีในโหนดเครือข่าย
ชี้โหนดไปยังโฟลเดอร์ที่คุณต้องการทำดัชนี คลาสช่วยเหลือ `Utils.DocumentsPath` จะชี้ไปยังโฟลเดอร์ข้อมูลตัวอย่าง

```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.options.*;

IndexingDocuments.addDirectories(masterNode, Utils.DocumentsPath);
```

#### การค้นหาข้อความข้ามโหนดเครือข่าย
รันคิวรีกับ **ทั้งหมด** ของโหนดและดึงเอกสารที่ตรงกัน

```java
import java.util.ArrayList;
import com.groupdocs.search.scaling.results.*;

ArrayList<NetworkFoundDocument> documents = TextSearchInNetwork.searchAll(masterNode, "ipsum", false);
highlightInDocument(masterNode, documents.get(0), 3); // Highlight results from the first found document.
```

- แทนที่ `"ipsum"` ด้วยคำที่คุณต้องการค้นหา  
- เมธอด `highlightInDocument` (แสดงต่อไป) จะทำการไฮไลท์

#### ไฮไลท์หลายคำในเอกสาร – Highlighting Search Results
เมธอดต่อไปนี้สาธิตวิธีไฮไลท์ชิ้นส่วนรอบแต่ละผลลัพธ์ รวมถึงการควบคุมจำนวนคำรอบ ๆ ผลลัพธ์ เพื่อสนองต่อคีย์เวิร์ดรอง **highlight multiple terms document**

```java
import com.groupdocs.search.highlighters.*;
import com.groupdocs.search.options.*;

public static void highlightInDocument(
    SearchNetworkNode node,
    NetworkFoundDocument document,
    int maxFragments) {
    
    Searcher searcher = node.getSearcher();
    FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.PlainText);

    HighlightOptions options = new HighlightOptions();
    options.setTermsAfter(5);
    options.setTermsBefore(5);
    options.setTermsTotal(15);

    searcher.highlight(document, highlighter, options); // Perform highlighting on the document.

    FragmentContainer[] result = highlighter.getResult();
    for (FragmentContainer container : result) {
        if (container.getCount() == 0) continue;

        String[] fragments = container.getFragments();
        int count = Math.min(fragments.length, maxFragments);
        for (int j = 0; j < count; j++) {
            // Print each fragment within the specified limit.
        }
    }
}
```

- **`OutputFormat.PlainText`** – คืนสแนปช็อตเป็นข้อความธรรม HTML เพื่อ UI ที่สวยงามกว่า  
- **`HighlightOptions`** – ควบคุมจำนวนคำก่อน/หลังแต่ละผลลัพธ์ (`setTermsBefore`, `setTermsAfter`)  
- **`maxFragments`** – จำกัดจำนวนสแนปช็อตที่แสดงต่อเอกสาร

#### ปิดโหนดเครือข่าย
เมื่อทำงานเสร็จ ให้ปิดทุกโหนดเพื่อคืนทรัพยากร

```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## การประยุกต์ใช้งานจริง

- **Enterprise Document Management:** รวมศูนย์ไฟล์องค์กรและให้พนักงานค้นหาสัญญาหรือระเบียบที่เกี่ยวข้องได้ทันที  
- **Legal Case Files:** ไฮไลท์คำสำคัญทางกฎหมายในเอกสารคดีอย่างรวดเร็ว  
- **R&D Knowledge Bases:** นักวิจัยค้นหาสิทธิบัตรหรือบทความเทคนิคและเห็นส่วนที่ไฮไลท์  
- **E‑commerce Catalogs:** ผู้ซื้อค้นหาผลิตภัณฑ์ด้วยคีย์เวิร์ดและเห็นผลลัพธ์ที่ไฮไลท์ในคำอธิบายสินค้า  
- **Library Systems:** ผู้ใช้ค้นหาผ่านหนังสือหลายพันเล่มและดูข้อความที่ไฮไลท์โดยไม่ต้องเปิดไฟล์ทั้งหมด

## พิจารณาด้านประสิทธิภาพ

- **รักษาดัชนีให้สด:** ทำดัชนีไฟล์ที่เปลี่ยนแปลงทุกคืนหรือใช้การอัปเดตแบบ incremental  
- **ใช้หลายโหนด:** กระจายการทำดัชนีและโหลดคิวรีเพื่อหลีกเลี่ยงคอขวด  
- **ปรับ `HighlightOptions`:** ลด `termsBefore/After` เพื่อลดการใช้หน่วยความจำในเอกสารขนาดใหญ่มาก  

## ปัญหาที่พบบ่อยและการแก้ไข

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|-------|-------------------|--------|
| ไม่มีผลลัพธ์คืนค่า | ดัชนียังไม่ได้สร้างหรือชี้ไปยังโฟลเดอร์ผิด | ตรวจสอบ `Utils.DocumentsPath` และรัน `IndexingDocuments.addDirectories` อีกครั้ง |
| ผลลัพธ์ไฮไลท์เป็นค่าว่าง | `HighlightOptions` ตั้งค่าต่ำเกินไปหรือเอกสารมีปัญหา encoding | เพิ่มค่า `termsTotal` หรือยืนยันว่าเอกสารรองรับ encoding |
| เกิดข้อผิดพลาดพอร์ตซ้ำ | `basePort` ถูกใช้งานอยู่แล้ว | เลือกพอร์ตอื่น (เช่น 49117) |
| เกิดข้อยกเว้นลิขสิทธิ์ | ไฟล์ลิขสิทธิ์หายหรือหมดอายุ | วางไฟล์ `GroupDocs.Search.lic` ที่เป็นไฟล์ลิขสิทธิ์ที่ถูกต้องในโฟลเดอร์รากของแอปพลิเคชัน |

## คำถามที่พบบ่อย

**Q: สามารถปรับใช้หลายโหนดเครือข่ายการค้นหาเพื่อทำ load balancing ได้หรือไม่?**  
A: ได้, การปรับใช้หลายโหนดช่วยกระจายการทำดัชนีและคิวรี ทำให้ระบบขยายตัวและตอบสนองเร็วขึ้น  

**Q: วิธีไฮไลท์หลายคำค้นหาในเอกสารเดียว?**  
A: ส่งรายการคำไปยังเมธอด `highlight` และตั้งค่า `HighlightOptions` ให้แสดงคำรอบ ๆ แต่ละผลลัพธ์  

**Q: สามารถสมัครรับเหตุการณ์การค้นหาแบบเรียลไทม์ได้หรือไม่?**  
A: แน่นอน ใช้ `SearchNetworkNodeEvents.subscribe(masterNode)` เพื่อรับ callback สำหรับความคืบหน้าการทำดัชนี, การรันคิวรี, และข้อผิดพลาด  

**Q: GroupDocs.Search รองรับรูปแบบไฟล์ใดบ้างสำหรับการทำดัชนีและไฮไลท์?**  
A: รองรับมากกว่า 50 รูปแบบ รวมถึง DOCX, PDF, HTML, TXT, PPTX ฯลฯ  

**Q: จะเพิ่มความเร็วการค้นหาในคอลเลกชันขนาดใหญ่อย่างไร?**  
A: อัปเดตดัชนีเป็นประจำ, กระจายดัชนีไปยังหลายโหนด, และปรับ `HighlightOptions` เพื่อลดขนาดชิ้นส่วน  

## สรุป
ตามคู่มือนี้คุณจะได้ตั้งค่าระบบ **highlight search results java** ด้วย GroupDocs.Search ที่พร้อมใช้งานในระดับผลิต สามารถขยายโซลูชันข้ามเครือข่าย, ทำดัชนีไฟล์ที่รองรับ, รันคิวรีอย่างรวดเร็ว, และคืนสแนปช็อตที่ไฮไลท์เพื่อช่วยผู้ใช้ค้นหาข้อมูลที่ต้องการได้อย่างแม่นยำ ต่อไปลองผสานผลลัพธ์เข้ากับ UI เว็บ, เพิ่ม faceted search, หรือรวมกับ OCR สำหรับ PDF ที่สแกน

---

**อัปเดตล่าสุด:** 2026-01-08  
**ทดสอบกับ:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs  

---
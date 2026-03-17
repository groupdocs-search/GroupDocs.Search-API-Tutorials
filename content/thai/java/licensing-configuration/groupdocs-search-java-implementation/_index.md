---
date: '2026-03-17'
description: เรียนรู้วิธีไฮไลท์ผลการค้นหาใน Java ด้วย GroupDocs.Search, ตั้งค่าเครือข่ายการค้นหาที่สามารถขยายได้,
  ทำการทำดัชนีเอกสาร, รันคำค้น, และแสดงส่วนข้อความที่ไฮไลท์.
keywords:
- GroupDocs.Search Java
- distributed searching Java
- highlight search results Java
title: วิธีไฮไลท์ผลการค้นหาใน Java ด้วย GroupDocs.Search
type: docs
url: /th/java/licensing-configuration/groupdocs-search-java-implementation/
weight: 1
---

# ไฮไลท์ผลการค้นหา Java ด้วย GroupDocs.Search

หากคุณรู้สึกเหนื่อยกับการคัดกรองเอกสารจำนวนมากด้วยตนเอง, **highlight search results java** ให้วิธีที่เร็วและเชื่อถือได้ในการดึงข้อมูลที่ต้องการออกมา ในบทเรียนนี้เราจะอธิบายการตั้งค่าเครือข่ายการค้นหาแบบกระจาย, การทำดัชนีไฟล์ของคุณ, การรันคิวรี, และสุดท้ายการไฮไลท์ผลที่ตรงกันโดยตรงในเอกสาร เมื่อเสร็จสิ้นคุณจะได้โซลูชันพร้อมใช้งานในระดับผลิตที่สามารถขยายได้หลายโหนดและทำให้คำที่เกี่ยวข้องเด่นชัดทันที

## คำตอบอย่างรวดเร็ว
- **What does “highlight search results java” mean?** หมายถึงการทำเครื่องหมายคีย์เวิร์ดที่พบในเอกสารโดยอัตโนมัติเมื่อใช้ไลบรารี Java เช่น GroupDocs.Search  
- **Can I highlight multiple terms in the same document?** ใช่ – ใช้ `HighlightOptions` เพื่อกำหนดจำนวนคำก่อน/หลังแต่ละผลลัพธ์ที่จะแสดง  
- **Do I need a license to run this example?** สามารถใช้การทดลองหรือไลเซนส์ชั่วคราวสำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานในผลิตภัณฑ์  
- **Which Java version is required?** Java 8 หรือใหม่กว่า  
- **Is this approach suitable for large document collections?** แน่นอน – เครือข่ายการค้นหาจะกระจายการทำดัชนีและโหลดคิวรีไปยังโหนดหลายตัว  

## Highlight Search Results Java คืออะไร?
**Highlight search results java** คือกระบวนการรับคิวรีการค้นหา, ค้นหาชิ้นส่วนที่ตรงกันในเอกสารของคุณ, และทำให้ชิ้นส่วนนั้นเด่นชัด (เช่นโดยใส่เครื่องหมายรอบหรือส่งกลับเป็นสแนปช็อตที่ไฮไลท์) ทำให้ผู้ใช้เห็นบริบทของแต่ละผลลัพธ์โดยไม่ต้องเปิดไฟล์ทั้งหมด

## ทำไม Highlight Search Results Java ถึงสำคัญ
การใช้ **highlight search results java** ปรับปรุงประสบการณ์ผู้ใช้โดยแสดงตำแหน่งที่คำปรากฏอย่างชัดเจน, ลดเวลาที่ใช้เปิดไฟล์ที่ไม่เกี่ยวข้อง, และช่วยทีมปฏิบัติตามกฎระเบียบค้นหาข้อมูลที่อ่อนไหวได้อย่างรวดเร็ว เมื่อรวมกับเครือข่ายการค้นหาแบบกระจาย โซลูชันจะตอบสนองได้ดีแม้ฐานข้อมูลเอกสารจะเติบโตเป็นล้านเอกสาร

## ทำไมต้องใช้ GroupDocs.Search สำหรับการไฮไลท์?
GroupDocs.Search มีเอนจินประสิทธิภาพสูงที่พร้อมใช้งาน รองรับไฟล์หลายสิบรูปแบบ, การทำดัชนีแบบกระจาย, และไฮไลท์ชิ้นส่วนในตัว ช่วยให้คุณไม่ต้องเขียนพาร์เซอร์หรือจัดการโครงสร้างพื้นฐานการค้นหาแบบระดับล่าง สามารถมุ่งเน้นที่การมอบประสบการณ์ผู้ใช้ที่ราบรื่นได้เลย

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 8+** – ตรวจสอบว่า `java -version` แสดง 1.8 หรือสูงกว่า  
- **Maven** – สำหรับการจัดการ dependencies  
- **GroupDocs.Search for Java 25.4** – เวอร์ชันที่ใช้ในคู่มือนี้ทั้งหมด  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse** (ไม่บังคับแต่แนะนำ)  
- ความรู้พื้นฐานเกี่ยวกับ Java และแนวคิดเครือข่าย  

## การตั้งค่า GroupDocs.Search for Java

คุณสามารถนำไลบรารีเข้ามาในโปรเจกต์ได้ทั้งผ่าน Maven หรือดาวน์โหลดไฟล์ JAR โดยตรง

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
หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### ขั้นตอนการรับไลเซนส์
- **Free Trial:** เริ่มต้นด้วยการทดลองเพื่อสำรวจฟีเจอร์หลัก  
- **Temporary License:** รับไลเซนส์ทดสอบระยะยาวจาก [this page](https://purchase.groupdocs.com/temporary-license/)  
- **Purchase:** ซื้อไลเซนส์เต็มสำหรับการใช้งานในผลิตภัณฑ์  

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

## คู่มือการใช้งาน

### วิธีไฮไลท์ผลการค้นหา Java ในเครือข่ายแบบกระจาย

#### การกำหนดค่าเครือข่ายการค้นหา
ก่อนอื่นกำหนดตำแหน่งที่เก็บเอกสารและพอร์ตที่เครือข่ายจะใช้

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/HighlightingResultsInNetwork/";
int basePort = 49116; // Change if port is busy

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **`basePath`** – โฟลเดอร์รากที่บรรจุไฟล์ที่ต้องการทำดัชนี  
- **`basePort`** – พอร์ต TCP สำหรับการสื่อสารระหว่างโหนด; เลือกพอร์ตที่ยังไม่ได้ใช้  

#### การปรับใช้โหนดเครือข่ายการค้นหา
ปรับใช้โหนดหนึ่งหรือหลายโหนดตามการกำหนดค่า โหนดแรกจะเป็น master

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```

- **`nodes`** – อาร์เรย์ของโหนดที่กำลังทำงานทั้งหมด  
- **`masterNode`** – ประสานงานการทำดัชนีและการกระจายคิวรี  

#### การสมัครรับเหตุการณ์โหนดเครือข่ายการค้นหา
แนบ listener ไปยัง master node เพื่อรับการแจ้งเตือนแบบเรียลไทม์ (เช่นเมื่อการทำดัชนีเสร็จ)

```java
import com.groupdocs.search.scaling.events.*;

SearchNetworkNodeEvents.subscribe(masterNode);
```

#### การทำดัชนีไดเรกทอรีในโหนดเครือข่าย
ชี้โหนดไปยังโฟลเดอร์ที่ต้องการทำดัชนี คลาสช่วย `Utils.DocumentsPath` จะชี้ไปยังโฟลเดอร์ข้อมูลตัวอย่าง

```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.options.*;

IndexingDocuments.addDirectories(masterNode, Utils.DocumentsPath);
```

#### การค้นหาข้อความข้ามโหนดเครือข่าย
รันคิวรีบน **all** โหนดและดึงเอกสารที่ตรงกัน

```java
import java.util.ArrayList;
import com.groupdocs.search.scaling.results.*;

ArrayList<NetworkFoundDocument> documents = TextSearchInNetwork.searchAll(masterNode, "ipsum", false);
highlightInDocument(masterNode, documents.get(0), 3); // Highlight results from the first found document.
```

- แทนที่ `"ipsum"` ด้วยคำที่คุณต้องการค้นหา  
- เมธอด `highlightInDocument` (แสดงต่อไป) จะทำการไฮไลท์  

#### ไฮไลท์หลายคำในเอกสาร – Highlighting Search Results
เมธอดต่อไปนี้สาธิตวิธีไฮไลท์ชิ้นส่วนรอบแต่ละผลลัพธ์ และแสดงวิธีควบคุมจำนวนคำรอบผลลัพธ์ เพื่อตอบสนองคีย์เวิร์ดรอง **highlight multiple terms document**

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

- **`OutputFormat.PlainText`** – คืนสแนปช็อตเป็นข้อความธรรมดา; สามารถสลับเป็น HTML เพื่อ UI ที่สวยงามกว่าได้  
- **`HighlightOptions`** – ควบคุมจำนวนคำก่อน/หลังแต่ละผลลัพธ์ที่รวม (`setTermsBefore`, `setTermsAfter`)  
- **`maxFragments`** – จำกัดจำนวนสแนปช็อตที่แสดงต่อเอกสาร  

#### ปิดโหนดเครือข่าย
เมื่อทำงานเสร็จ ให้ปิดทุกโหนดเพื่อคืนทรัพยากร

```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## การประยุกต์ใช้ในทางปฏิบัติ

- **Enterprise Document Management:** รวมศูนย์ไฟล์องค์กรและให้พนักงานค้นหาสัญญาหรือนโยบายที่เกี่ยวข้องได้ทันที  
- **Legal Case Files:** ค้นหาเอกสารอ้างอิงโดยไฮไลท์คำสำคัญทางกฎหมายได้อย่างรวดเร็ว  
- **R&D Knowledge Bases:** นักวิจัยสามารถค้นหาสิทธิบัตรหรือเอกสารเทคนิคและดูส่วนที่ไฮไลท์ได้  
- **E‑commerce Catalogs:** ช่วยให้ผู้ซื้อค้นหาผลิตภัณฑ์ด้วยคีย์เวิร์ดและเห็นผลลัพธ์ที่ไฮไลท์ในคำอธิบายสินค้า  
- **Library Systems:** ผู้ใช้สามารถค้นหาผ่านหนังสือหลายพันเล่มและดูข้อความที่ไฮไลท์โดยไม่ต้องเปิดไฟล์แต่ละไฟล์  

## พิจารณาด้านประสิทธิภาพ

- **Keep indexes fresh:** ทำการทำดัชนีไฟล์ที่เปลี่ยนแปลงทุกคืนหรือใช้การอัปเดตแบบ incremental  
- **Leverage multiple nodes:** กระจายการทำดัชนีและโหลดคิวรีเพื่อหลีกเลี่ยงคอขวด  
- **Tune `HighlightOptions`:** ลดค่า `termsBefore/After` จะช่วยลดการใช้หน่วยความจำสำหรับเอกสารขนาดใหญ่มาก  

## ปัญหาทั่วไป & การแก้ไขข้อผิดพลาด

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| No results returned | Index not built or pointing to wrong folder | Verify `Utils.DocumentsPath` and run `IndexingDocuments.addDirectories` again |
| Highlight output is empty | `HighlightOptions` limits too low or document encoding issue | Increase `termsTotal` or ensure the document’s encoding is supported |
| Port conflict error | `basePort` already in use | Choose a different port number (e.g., 49117) |
| License exception | Missing or expired license file | Place a valid `GroupDocs.Search.lic` file in the application root |

## คำถามที่พบบ่อย

**Q: Can I deploy multiple search network nodes for load balancing?**  
A: ใช่, การปรับใช้หลายโหนดจะกระจายการทำดัชนีและงานคิวรี ทำให้ระบบขยายตัวได้ดีและตอบสนองเร็วขึ้น  

**Q: How do I highlight multiple search terms in the same document?**  
A: ส่งรายการคำไปยังเมธอด `highlight` และกำหนด `HighlightOptions` ให้แสดงคำรอบแต่ละผลลัพธ์  

**Q: Is it possible to subscribe to real‑time search events?**  
A: แน่นอน ใช้ `SearchNetworkNodeEvents.subscribe(masterNode)` เพื่อรับ callback สำหรับความคืบหน้าการทำดัชนี, การรันคิวรี, และข้อผิดพลาด  

**Q: Which file formats does GroupDocs.Search support for indexing and highlighting?**  
A: รองรับกว่า 50 รูปแบบ รวมถึง DOCX, PDF, HTML, TXT, PPTX และอื่น ๆ  

**Q: How can I improve search speed on very large collections?**  
A: อัปเดตดัชนีเป็นประจำ, กระจายดัชนีไปยังโหนดหลายตัว, และปรับ `HighlightOptions` เพื่อลดขนาดชิ้นส่วนที่แสดง  

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs
---
date: '2026-07-07'
description: เรียนรู้วิธีลบดัชนี, ทำการค้นหาข้อความเต็มรูปแบบด้วย Java, และเพิ่มประสิทธิภาพการค้นหาโดยใช้
  GroupDocs.Search for Java. คู่มือขั้นตอนโดยละเอียดพร้อมการตั้งค่าเครือข่ายและการทำดัชนี
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: วิธีลบดัชนีและทำการค้นหาข้อความเต็มรูปแบบด้วย Java โดยใช้ GroupDocs.Search.
  ปฏิบัติตามคู่มือนี้เพื่อตั้งค่าเครือข่ายการค้นหา, สร้างดัชนีที่สามารถค้นหาได้, และเพิ่มประสิทธิภาพการค้นหา
og_title: วิธีลบดัชนีและทำการค้นหาข้อความด้วย GroupDocs.Search for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: วิธีลบดัชนีและทำการค้นหาข้อความด้วย GroupDocs.Search for Java
type: docs
url: /th/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# วิธีลบดัชนีและทำการค้นหาข้อความด้วย GroupDocs.Search สำหรับ Java

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **how to delete index** อย่างรวดเร็วพร้อมยังคงมอบความสามารถในการค้นหาแบบเต็มข้อความด้วย Java ที่เร็วเหมือนสายฟ้าเป็นข้อได้เปรียบในการแข่งขัน ไม่ว่าคุณจะสร้างฐานความรู้ภายใน, คลังข้อมูลคดีกฎหมาย, หรือแคตาล็อกสินค้าของอีคอมเมิร์ซ, เครือข่ายการค้นหาที่ปรับแต่งอย่างดีสามารถปรับปรุงความพึงพอใจของผู้ใช้ได้อย่างมาก ในคู่มือนี้คุณจะได้เรียนรู้วิธี **set up a search network**, **create a searchable index**, **optimize search performance**, และ **delete documents from the index** เมื่อจำเป็น — ทั้งหมดนี้โดยใช้ GroupDocs.Search สำหรับ Java.

## คำตอบสั้น
- **วัตถุประสงค์หลักของ GroupDocs.Search สำหรับ Java คืออะไร?** It provides full‑text search across 50+ document formats, enabling rapid keyword retrieval.  
- **ฉันจะทำการค้นหาข้อความในสภาพแวดล้อมแบบกระจายได้อย่างไร?** Deploy a search network, index documents on a master node, then query any node.  
- **ฉันสามารถลบเอกสารออกจากดัชนีโดยไม่ต้องสร้างดัชนีใหม่ได้หรือไม่?** Yes, use the Delete API to remove selected files, effectively *how to delete index* without full re‑indexing.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 or higher.  
- **ต้องการใบอนุญาตสำหรับการใช้งานในโปรดักชันหรือไม่?** A valid GroupDocs.Search license is required; a free trial is available.

## การ “perform text search” คืออะไร?
การทำการค้นหาข้อความหมายถึงการสอบถามดัชนีเต็มข้อความเพื่อดึงเอกสารที่มีคีย์เวิร์ดหรือวลีที่ระบุ GroupDocs.Search สร้างดัชนีแบบกลับด้านที่ทำให้การค้นหาเหล่านี้เร็วมาก แม้จะมีไฟล์หลายพันไฟล์

## ทำไมต้องตั้งค่าเครือข่ายการค้นหา?
เครือข่ายการค้นหาจะแจกจ่ายภาระการทำดัชนีและการสอบถามไปยังหลายโหนด, ทำให้คุณสามารถ **optimize search performance**, ขยายแนวนอน, และรักษาความพร้อมใช้งานสูง สถาปัตยกรรมนี้เหมาะสำหรับคลังเอกสารระดับองค์กรที่ความหน่วงและอัตราการผ่านข้อมูลเป็นสิ่งสำคัญ.

## วิธีการนำไปใช้และปรับแต่งเครือข่ายการค้นหาด้วย GroupDocs.Search สำหรับ Java
โหลดการกำหนดค่าของคุณ, เริ่มโหนดหลัก, แล้วเพิ่มโหนดทำงานที่ใช้เส้นทางฐานและพอร์ตเดียวกัน การปรับใช้เครือข่ายแบบนี้ทำให้โหนดใดก็สามารถจัดการการทำดัชนีหรือการสอบถาม, ให้เวลาตอบสนองที่สม่ำเสมอแม้จำนวนเอกสารจะเพิ่มเป็นหลายแสน.

### ภาพรวมขั้นตอนต่อขั้นตอน
1. **กำหนดการกำหนดค่าพื้นฐาน** ที่รวมถึงไดเรกทอรีที่ใช้ร่วมกันและพอร์ต TCP.  
2. **เริ่มโหนดหลัก** เพื่อจัดการดัชนีและประสานงานโหนดทำงาน.  
3. **เพิ่มโหนดทำงาน** ที่เชื่อมต่อกับโหนดหลัก, ทำให้สามารถทำดัชนีและการค้นหาแบบขนานได้.  
4. **ตรวจสอบการใช้ทรัพยากร** และปรับแต่งการตั้งค่า JVM heap เพื่อให้ความหน่วงต่ำ.

## วิธีลบดัชนีใน GroupDocs.Search สำหรับ Java
`SearchNode` แสดงถึงโหนดในเครือข่าย GroupDocs.Search ที่จัดการการทำดัชนีและการดำเนินการสอบถาม เมธอด `delete` จะลบเอกสารที่ระบุออกจากดัชนี.

### ขั้นตอนการลบโดยตรง
- เรียกเมธอด `delete` บนอินสแตนซ์ `SearchNode`.  
- ระบุอาร์เรย์ของเส้นทางไฟล์แบบสัมพันธ์.  
- คอมมิตการเปลี่ยนแปลง; ดัชนีจะรีเฟรชทันทีและการค้นหาต่อไปจะไม่แสดงไฟล์ที่ถูกลบ.

## เครือข่ายการค้นหาคืออะไร?
A **search network** คือคลัสเตอร์ของโหนดที่เชื่อมต่อกันซึ่งใช้คลังดัชนีร่วมกัน, ทำให้สามารถทำดัชนีและการดำเนินการสอบถามแบบกระจายได้ มันช่วยให้สามารถขยายแนวนอนและมีความทนต่อข้อผิดพลาดสำหรับคอลเลกชันเอกสารขนาดใหญ่.

## วิธีสร้างดัชนีที่สามารถค้นหาได้ (index documents java)
เมธอด `add` ทำการทำดัชนีเอกสารเข้าสู่ดัชนีการค้นหา เพิ่มเอกสารไปยังโหนดหลักโดยใช้เมธอด `add`; เครือข่ายจะกระจายการเปลี่ยนแปลงไปยังโหนดทำงานทั้งหมด วิธีนี้ทำให้ทุกโหนดสามารถให้บริการสอบถามต่อดัชนีล่าสุดโดยไม่ต้องมีขั้นตอนซิงโครไนซ์เพิ่มเติม.

### การกระทำสำคัญ
- ชี้โหนดหลักไปยังโฟลเดอร์ที่มีไฟล์ต้นฉบับ.  
- เรียกใช้รูทีนการทำดัชนี; เครือข่ายจะประมวลผลแต่ละไฟล์และอัปเดตดัชนีแบบกลับด้าน.  
- ตรวจสอบว่ามีไฟล์ดัชนีปรากฏในไดเรกทอรีจัดเก็บที่กำหนด.

## วิธีลบไฟล์ที่ทำดัชนีแล้ว (remove indexed files)
เมื่อเอกสารถูกทำให้ล้าสมัย, เรียก API `delete` พร้อมเส้นทางของไฟล์ ระบบจะลบรายการของไฟล์จากดัชนีแบบกลับด้าน, ปลดปล่อยพื้นที่จัดเก็บและป้องกันผลลัพธ์ที่ล้าสมัย.

## การตั้งค่า GroupDocs.Search สำหรับ Java
เพื่อเริ่มต้น, ผสานรวม GroupDocs.Search เข้ากับโครงการ Java ของคุณโดยใช้การตั้งค่าดังต่อไปนี้:

### การตั้งค่า Maven
Add the repository and dependency to your `pom.xml` file:

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
หรือคุณสามารถ [download the latest version directly from GroupDocs](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
GroupDocs มีการทดลองใช้งานฟรี, ซึ่งช่วยให้คุณประเมินคุณสมบัติก่อนซื้อ คุณสามารถรับใบอนุญาตชั่วคราวโดยทำตามขั้นตอนใน [purchase page](https://purchase.groupdocs.com/temporary-license/). สิ่งนี้จะเปิดใช้งานฟังก์ชันเต็มในช่วงการทดสอบของคุณ.

### การเริ่มต้นและตั้งค่าพื้นฐาน
Initialize GroupDocs.Search in your Java application with:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## คู่มือการใช้งาน

### การกำหนดค่าเครือข่ายการค้นหา
**Overview:** สร้างเส้นทางฐานและพอร์ตสำหรับเครือข่ายการค้นหาของคุณ, ทำให้โหนดสื่อสารได้อย่างมีประสิทธิภาพ.

#### ขั้นตอนที่ 1: กำหนดการกำหนดค่าพื้นฐาน
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath`: เส้นทางไดเรกทอรีสำหรับการดำเนินการของเครือข่าย.  
  - `basePort`: หมายเลขพอร์ตที่ใช้โดยเครือข่ายการค้นหา.

#### ขั้นตอนที่ 2: การแก้ไขปัญหา
ตรวจสอบให้แน่ใจว่าพอร์ตที่ระบุไม่ได้ถูกบล็อกโดยการตั้งค่าไฟร์วอลล์หรือถูกใช้งานโดยแอปพลิเคชันอื่น ปรับเปลี่ยนตามจำเป็นเพื่อหลีกเลี่ยงความขัดแย้ง.

### การปรับใช้โหนดเครือข่ายการค้นหา
**Overview:** ใช้การกำหนดค่าของคุณ, ปรับใช้โหนดทั่วเครือข่ายเพื่อทำดัชนีและการค้นหาแบบกระจาย.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port:** ค่าต่าง ๆ เหล่านี้ควรตรงกับที่ใช้ในการกำหนดค่าเริ่มต้นของคุณเพื่อให้สอดคล้องกัน.

### การทำดัชนีเอกสาร (`create searchable index`)
**Overview:** เพิ่มเอกสารเข้าสู่ดัชนีการค้นหาอย่างมีประสิทธิภาพโดยใช้โหนดหลัก.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode`: โหนดหลักที่จัดการการทำดัชนีเอกสาร.  
  - `documentsPath`: เส้นทางไปยังไดเรกทอรีที่มีเอกสาร.

#### เคล็ดลับการแก้ไขปัญหา
ตรวจสอบว่าเส้นทางเอกสารของคุณถูกต้องและเข้าถึงได้ ตรวจสอบให้แน่ใจว่ามีสิทธิ์อ่านจากไดเรกทอรีเหล่านี้.

### การค้นหาข้อความในเครือข่าย (`perform text search`)
**Overview:** ทำการค้นหาข้อความอย่างครอบคลุมทั่วเครือข่ายที่ทำดัชนีของคุณ.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query`: ข้อความที่คุณกำลังค้นหา.  
  - `masterNode`: โหนดที่ทำการค้นหา.

### การลบเอกสารจากดัชนี (`delete documents index`)
**Overview:** ลบเอกสารเฉพาะจากดัชนีของคุณโดยใช้เส้นทางไฟล์ของพวกมัน.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Method Purpose:**  
  - `node`: โหนดเป้าหมายสำหรับการดำเนินการลบ.  
  - `filePaths`: เส้นทางของเอกสารที่จะลบออกจากดัชนี.

#### การแก้ไขปัญหา
ตรวจสอบว่าเส้นทางไฟล์แม่นยำและไฟล์มีอยู่ในไดเรกทอรีของคุณ หากปัญหายังคงอยู่, ตรวจสอบสิทธิ์เครือข่ายและการเชื่อมต่อ.

## การประยุกต์ใช้งานจริง
1. **Enterprise Document Management:** ปรับปรุงการดึงข้อมูลความรู้ภายใน.  
2. **Legal Case Analysis:** ค้นหาไฟล์คดีที่เกี่ยวข้องอย่างรวดเร็วในหลายคลังข้อมูล.  
3. **E‑commerce Platforms:** เพิ่มความเร็วการค้นหาผลิตภัณฑ์โดยทำดัชนีคำอธิบายและรีวิว.  
4. **Academic Research:** ค้นหาห้องสมุดดิจิทัลขนาดใหญ่ของเอกสารและวิทยานิพนธ์อย่างมีประสิทธิภาพ.  
5. **Customer Support Systems:** ลดเวลาตอบสนองโดยทำให้เจ้าหน้าที่สามารถค้นหาตั๋วเก่าได้ทันที.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Optimize Indexing Speed:** เพิ่มเอกสารใหม่อย่างต่อเนื่องในช่วงเวลาที่ไม่มีการใช้งานหนักเพื่อให้ความหน่วงต่ำ.  
- **Resource Usage Guidelines:** ตรวจสอบ CPU และหน่วยความจำ, โดยเฉพาะเมื่อขยายจำนวนโหนด.  
- **Java Memory Management:** ปรับแต่งการตั้งค่า JVM heap ตามภาระงานของคุณ (เช่น `-Xmx2g` สำหรับดัชนีขนาดกลาง).

## สรุป
โดยทำตามคู่มือนี้คุณได้เรียนรู้วิธี **set up a search network**, **create a searchable index**, **perform text search**, และ **delete documents index** ด้วย GroupDocs.Search สำหรับ Java ความสามารถเหล่านี้ทำให้การดึงเอกสารที่เร็วและเชื่อถือได้ในสภาพแวดล้อมแบบกระจาย.

**ขั้นตอนต่อไป**
- ทดลองกำหนดค่าโหนดต่าง ๆ เพื่อหาสมดุลที่เหมาะสมสำหรับภาระงานของคุณ.  
- ศึกษาตัวเลือกการทำดัชนีขั้นสูงเช่นตัววิเคราะห์แบบกำหนดเองและการปรับความเกี่ยวข้อง.  
- สำรวจการผสานรวมกับผลิตภัณฑ์ GroupDocs อื่น ๆ เพื่อการประมวลผลเอกสารแบบครบวงจร.

## คำถามที่พบบ่อย

**Q: การใช้งานหลักของ GroupDocs.Search สำหรับ Java คืออะไร?**  
A: It provides full‑text search across many document formats, allowing you to **perform text search** in large repositories.

**Q: ฉันจะปรับปรุงความเร็วการค้นหาในเครือข่ายขนาดใหญ่ได้อย่างไร?**  
A: Deploy additional nodes, tune the JVM heap, and schedule indexing during low‑traffic periods to **optimize search performance**.

**Q: สามารถลบเอกสารเดียวโดยไม่ต้องทำดัชนีใหม่ทั้งหมดได้หรือไม่?**  
A: Yes, use the **delete documents index** API as shown in the code example to remove specific files.

**Q: ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?**  
A: A free trial license is sufficient for testing; a commercial license is required for production deployments.

**Q: ฉันสามารถทำดัชนี PDFs, Word files, และอีเมลพร้อมกันได้หรือไม่?**  
A: Absolutely—GroupDocs.Search supports a wide range of formats out of the box.

---

**อัปเดตล่าสุด:** 2026-07-07  
**ทดสอบด้วย:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [วิธีทำดัชนีข้อความใน Java ด้วย GroupDocs.Search Guide](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [เพิ่มประสิทธิภาพการค้นหาด้วยเทคนิคการทำดัชนีขั้นสูงใน GroupDocs.Search สำหรับ Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [ปรับปรุงประสิทธิภาพการสอบถามด้วย GroupDocs.Search Java: ปรับดัชนีและการค้นหา](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
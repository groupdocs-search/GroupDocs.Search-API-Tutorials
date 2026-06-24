---
date: '2026-05-17'
description: เรียนรู้วิธีกำหนดค่าพอร์ตฐาน groupdocs สำหรับเครือข่าย Java ที่สามารถขยายได้ของ
  GroupDocs.Search, ปรับปรุงความเร็วการดึงข้อมูล, และตั้งค่าระบบหลายโหนด.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: กำหนดค่าพอร์ตฐาน groupdocs ในเครือข่าย Java Search
type: docs
url: /th/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# กำหนดค่าพอร์ตฐาน groupdocs ในเครือข่ายการค้นหา Java

ในแอปพลิเคชันสมัยใหม่ที่มีข้อมูลจำนวนมาก, **configure base port groupdocs** เป็นขั้นตอนแรกในการสร้างโครงสร้างพื้นฐานการค้นหาที่เร็วและเชื่อถือได้ ไม่ว่าคุณจะทำการจัดทำดัชนี PDF จำนวนพันไฟล์หรือขยายไปหลายเซิร์ฟเวอร์ การกำหนดพอร์ตและไดเรกทอรีที่ไม่ซ้ำกันจะป้องกันความขัดแย้งระหว่างโหนดและทำให้คลัสเตอร์ทำงานได้อย่างมีสุขภาพดี บทแนะนำนี้จะพาคุณผ่านข้อกำหนดเบื้องต้น การติดตั้ง และการกำหนดค่าหลายโหนดอย่างสมบูรณ์โดยใช้ GroupDocs.Search สำหรับ Java เพื่อให้คุณสามารถเปิดใช้งานเครือข่ายการค้นหาที่ขยายได้จริงในวันนี้.

## คำตอบด่วน
- **วัตถุประสงค์หลักคืออะไร?** เพื่อกำหนดพอร์ตและไดเรกทอรีฐานที่ไม่ซ้ำกันสำหรับแต่ละโหนดการค้นหา เพื่อลดความขัดแย้ง.  
- **ฉันต้องการใบอนุญาตหรือไม่?** ใช่ – จำเป็นต้องมีใบอนุญาตทดลองหรือเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** Java 8 หรือสูงกว่า (แนะนำ Java 11+).  
- **ฉันสามารถรันบนเซิร์ฟเวอร์คลาวด์ได้หรือไม่?** แน่นอน – เพียงเปิดพอร์ตที่เลือกในกลุ่มความปลอดภัยของคลาวด์ของคุณ.  
- **ฉันสามารถเพิ่มโหนดได้กี่โหนด?** ไม่มีขีดจำกัดที่แน่นอน; คุณถูกจำกัดโดยฮาร์ดแวร์และความจุของเครือข่ายเท่านั้น.

## “configure base port groupdocs” คืออะไร?

**Configure base port groupdocs** คือกระบวนการกำหนดพอร์ต TCP เริ่มต้นที่แต่ละโหนดการค้นหาจะใช้และเพิ่มขึ้นสำหรับโหนดต่อไป ขั้นตอนง่ายนี้จะขจัดข้อผิดพลาด “port already in use” ที่น่ากลัวและวางพื้นฐานสำหรับคลัสเตอร์การค้นหาที่ขยายได้แนวนอนอย่างสะอาด ทำให้แต่ละโหนดสื่อสารผ่านจุดสิ้นสุดที่แตกต่างกัน.

## ทำไมต้องใช้ GroupDocs.Search สำหรับเครือข่ายที่ขยายได้?

GroupDocs.Search มอบ **high‑performance indexing** (สูงสุด 50 GB/นาทีบนเซิร์ฟเวอร์ 8‑core มาตรฐาน) และรองรับ **50+ file formats** รวมถึง PDF, DOCX, PPTX, และ HTML สถาปัตยกรรมโมดูลาร์ของมันทำให้คุณสามารถผสานรวม indexers, searchers, shards, และ extractors ข้ามโหนดได้ ให้การขยายตัวเชิงเส้นเมื่อคุณเพิ่มฮาร์ดแวร์ ไลบรารียังมีตัวเลือกการบีบอัดในตัวที่ลดการใช้ดิสก์ได้ถึง 70 % ในขณะที่รักษาความหน่วงของการค้นหาให้อยู่ต่ำกว่า 200 ms สำหรับงานทั่วไป.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK)** 8 หรือใหม่กว่า (แนะนำ Java 11+ สำหรับการจัดการหน่วยความจำที่ดีกว่า).  
- **IDE** เช่น IntelliJ IDEA หรือ Eclipse.  
- **GroupDocs.Search for Java** library (เวอร์ชัน 25.4 หรือใหม่กว่า) ติดตั้งผ่าน Maven หรือดาวน์โหลดด้วยตนเอง.  
- ความรู้พื้นฐานด้านเครือข่าย (พอร์ต TCP, localhost vs. โฮสต์ระยะไกล).  
- ใบอนุญาต **GroupDocs.Search** ที่ถูกต้อง (ทดลองหรือเต็ม).

## การตั้งค่า GroupDocs.Search สำหรับ Java

### คำแนะนำการติดตั้ง

การตั้งค่า Maven:

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

ดาวน์โหลดโดยตรง:

หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต

- **Free Trial** – เริ่มทดสอบทันที.  
- **Temporary License** – รับการทดลองใช้งานต่ออายุที่ [Temporary License](https://purchase.groupdocs.com/temporary-license).  
- **Full Purchase** – จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

### การเริ่มต้นและตั้งค่าพื้นฐาน

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## คู่มือการนำไปใช้

### วิธีการกำหนดค่าพอร์ตฐาน groupdocs?

เพื่อกำหนดค่าพอร์ตฐาน ให้แก้ไขไฟล์การกำหนดค่าเครือข่ายหรือกำหนดค่า `basePort` ผ่านโปรแกรมเป็นค่าที่สูงและยังไม่ได้ใช้ เช่น 49100 สำหรับแต่ละโหนดต่อไปให้เพิ่มหมายเลขพอร์ตหนึ่ง (หรือเพิ่มตามค่าออฟเซ็ตคงที่) เพื่อให้แต่ละโหนดผูกกับจุดสิ้นสุด TCP ของตนเอง ลดข้อผิดพลาดการชนของพอร์ตและทำให้กฎไฟร์วอลล์ง่ายขึ้น.

#### การตั้งค่า Base Paths

ก่อนเขียนโค้ดใด ๆ ให้กำหนดโครงสร้างโฟลเดอร์ที่สอดคล้องกัน ตัวอย่างเช่น สร้างไดเรกทอรีแยกสำหรับ indexers (`Indexer0`), searchers (`Searcher0`), และ extractors (`Extractor0`). โครงสร้างนี้ทำให้แต่ละโหนดสามารถค้นหาไฟล์ของตนได้อย่างรวดเร็ว.

- **Why**: โครงสร้างไดเรกทอรีที่คาดเดาได้ช่วยป้องกันข้อผิดพลาด “file not found” เมื่อโหนดเริ่มทำงานบนเครื่องต่าง ๆ.

#### การกำหนดค่าพอร์ตฐาน

เลือกพอร์ตเริ่มต้นที่สูงเพื่อหลีกเลี่ยงการชนกับบริการทั่วไป (HTTP 80, SSH 22, เป็นต้น) เพิ่มหมายเลขพอร์ตสำหรับแต่ละโหนดใหม่ที่คุณเพิ่ม.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: การเริ่มที่พอร์ตสูง (เช่น 49100) ลดความเสี่ยงของการชนกับบริการที่มีอยู่และทำให้การสร้างกฎไฟร์วอลล์ง่ายขึ้น.

#### กำหนดที่อยู่โฮสต์

ในระหว่างการพัฒนา `localhost` ทำงานได้ดี สำหรับการผลิต ให้เปลี่ยนเป็นที่อยู่ IP ของเซิร์ฟเวอร์หรือชื่อ DNS เพื่อให้โหนดระยะไกลสามารถเชื่อมต่อกันได้.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: การใช้ที่อยู่โฮสต์จริงทำให้การสื่อสารระหว่างเครื่องเป็นไปได้ ซึ่งจำเป็นสำหรับคลัสเตอร์บนคลาวด์หรือในสถานที่.

#### สร้างการกำหนดค่าเครือข่าย

คลาส `NetworkConfig` รวมตัวเลือกเครือข่ายทั้งหมด—พอร์ตฐาน, โฮสต์, และการตั้งค่า SSL ทางเลือก—ไว้ในอ็อบเจ็กต์เดียวที่เครื่องมือ Search ใช้งาน.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Why**: การรวมศูนย์ตัวเลือกเหล่านี้ทำให้การกำหนดค่าสามารถนำกลับมาใช้ใหม่และง่ายต่อการบำรุงรักษาในหลายโหนด.

#### เพิ่มโหนด

`SearchNode` แสดงถึงโหนดแต่ละตัวในคลัสเตอร์ GroupDocs.Search ที่ทำหน้าที่เฉพาะเช่นการจัดทำดัชนีหรือการค้นหา สร้างอินสแตนซ์ `SearchNode` สำหรับแต่ละบทบาท (indexer, searcher, extractor) และลงทะเบียนกับ `SearchEngine` การกระจายหน้าที่ไปยังโหนดช่วยเพิ่มการทำงานแบบขนานและความทนทานต่อข้อผิดพลาด.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Why**: การแบ่งงานไปยังโหนดเฉพาะทำให้ลดการแย่งทรัพยากรและทำให้แต่ละเครื่องเชี่ยวชาญในงานเดียว เพิ่มประสิทธิภาพโดยรวม.

#### สรุปการกำหนดค่า

หลังจากเพิ่มโหนดทั้งหมดแล้ว เรียก `engine.start()` เพื่อเปิดเครือข่าย เครื่องมือจะผูกแต่ละโหนดกับพอร์ตที่กำหนดโดยอัตโนมัติและตรวจสอบการเชื่อมต่อ.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### ปัญหาและวิธีแก้ทั่วไป

- **Port Conflicts** – เพิ่ม `basePort` สำหรับแต่ละโหนดใหม่เสมอ ตรวจสอบพอร์ตที่เปิดด้วย `netstat` หรือเครื่องมือตรวจสอบเครือข่ายของระบบปฏิบัติการของคุณ.  
- **Missing Directories** – ตรวจสอบให้แน่ใจว่าโฟลเดอร์ทั้งหมด (`Indexer0`, `Searcher0`, เป็นต้น) มีอยู่และกระบวนการ Java มีสิทธิ์อ่าน/เขียน.  
- **Network Reachability** – เมื่อย้ายไปสู่การตั้งค่าหลายเครื่อง ให้เปลี่ยน `127.0.0.1` เป็น IP ของโฮสต์จริงและเปิดพอร์ตที่เลือกในไฟร์วอลล์.  

## การประยุกต์ใช้งานจริง

| สถานการณ์ | ประโยชน์ของการกำหนดค่าพอร์ตฐาน groupdocs |
|----------|--------------------------------------------|
| การจัดการเอกสารระดับองค์กร | การขยายตัวอย่างต่อเนื่องทั่วแผนกโดยไม่มีการหยุดทำงาน |
| แพลตฟอร์ม CMS ขนาดใหญ่ | การดึงข้อมูลที่เร็วขึ้นเนื่องจากดัชนีถูกกระจาย |
| การจัดการคดีกฎหมาย | การสกัด PDF แบบขนานลดความหน่วงของการค้นหา |

## การพิจารณาด้านประสิทธิภาพ

- **Monitor CPU/Memory** – ใช้ JMX ของ Java หรือเครื่องมือ profiling เพื่อติดตามการใช้เธรด.  
- **Adjust Compression** – `Compression.High` ประหยัดพื้นที่ดิสก์แต่อาจเพิ่มภาระ CPU; ทดสอบทั้ง `High` และ `Normal` เพื่อหาจุดที่เหมาะสม.  
- **Regular Updates** – เวอร์ชันใหม่ของ GroupDocs.Search มักมีแพตช์ประสิทธิภาพ; ควรอัปเดตไลบรารีให้เป็นเวอร์ชันล่าสุด.

## สรุป

คุณได้เรียนรู้วิธี **configure base port groupdocs** และตั้งค่าเครือข่ายการค้นหาหลายโหนดโดยใช้ GroupDocs.Search สำหรับ Java แล้ว ทดลองเพิ่มโหนดเพิ่มเติม ปรับแต่งการตั้งค่าดัชนี และผสานเครือข่ายเข้ากับแอปพลิเคชันที่มีอยู่ของคุณเพื่อโซลูชันการค้นหาที่ขยายได้จริง.

## คำถามที่พบบ่อย

**Q: จุดประสงค์ของการปิดการใช้งาน stop words ในการจัดทำดัชนีคืออะไร?**  
A: การปิดการใช้งาน stop words สามารถปรับปรุงความแม่นยำของการค้นหาโดยคงคำทั่วไปที่อาจสำคัญในโดเมนเฉพาะ.

**Q: ฉันจะจัดการกับความขัดแย้งของพอร์ตเมื่อเพิ่มหลายโหนดอย่างไร?**  
A: เริ่มด้วย `basePort` ที่สูง (เช่น 49100) และเพิ่มค่าตามโหนดต่อไป เพื่อให้แต่ละโหนดมีจุดสิ้นสุด TCP ที่ไม่ซ้ำกัน.

**Q: ฉันสามารถใช้การตั้งค่านี้สำหรับแอปพลิเคชันบนคลาวด์ได้หรือไม่?**  
A: ใช่—เพียงตรวจสอบให้แน่ใจว่าพอร์ตที่เลือกเปิดอยู่ในกลุ่มความปลอดภัยของคลาวด์และเปลี่ยน `127.0.0.1` เป็น IP สาธารณะหรือส่วนตัวที่เหมาะสม.

**Q: ความแตกต่างระหว่าง NormalIndex กับประเภทดัชนีอื่นคืออะไร?**  
A: `NormalIndex` ให้สมดุลระหว่างความเร็วและการใช้หน่วยความจำ ในขณะที่ดัชนีพิเศษ (เช่น `FastIndex`) มุ่งเน้นสถานการณ์ประสิทธิภาพเฉพาะ.

**Q: มีขีดจำกัดจำนวนโหนดที่ฉันสามารถเพิ่มได้หรือไม่?**  
A: โดยเทคนิคไม่มี; ขีดจำกัดขึ้นอยู่กับทรัพยากรฮาร์ดแวร์และแบนด์วิดท์ของเครือข่าย.

---

**อัปเดตล่าสุด:** 2026-05-17  
**ทดสอบกับ:** GroupDocs.Search Java 25.4  
**ผู้เขียน:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## บทแนะนำที่เกี่ยวข้อง

- [วิธีกำหนดค่าเครือข่ายการค้นหา .NET ด้วย GroupDocs.Search และ Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [วิธีนำเครือข่ายการค้นหาไปใช้กับ GroupDocs.Search ใน .NET สำหรับระบบจัดการเอกสาร](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [การปรับใช้โหนดเครือข่ายการค้นหาใน .NET ด้วย GroupDocs เพื่อการจัดทำดัชนีและการดึงข้อมูลเอกสารอย่างมีประสิทธิภาพ](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
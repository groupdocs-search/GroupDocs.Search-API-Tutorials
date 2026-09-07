---
date: '2026-06-27'
description: เรียนรู้วิธีกำหนดค่าการค้นหาแบบกระจายและปรับใช้เครือข่ายการค้นหาที่มีประสิทธิภาพโดยใช้
  GroupDocs.Search for Java เพื่อเพิ่มประสิทธิภาพและความสามารถในการขยายตัว
keywords:
- configure distributed search
- add documents to index
- GroupDocs.Search Java network
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Learn how to configure distributed search and deploy a powerful search
    network using GroupDocs.Search for Java, improving performance and scalability.
  headline: Configure Distributed Search with GroupDocs.Search Java Network
  type: TechArticle
- description: Learn how to configure distributed search and deploy a powerful search
    network using GroupDocs.Search for Java, improving performance and scalability.
  name: Configure Distributed Search with GroupDocs.Search Java Network
  steps:
  - name: '**Large‑Scale Enterprise Systems** – Index millions of contracts, policies,
      and reports while maintaining sub‑second query responses.'
    text: '**Large‑Scale Enterprise Systems** – Index millions of contracts, policies,
      and reports while maintaining sub‑second query responses.'
  - name: '**Content Management Platforms** – Serve thousands of concurrent users
      searching across multimedia assets without bottlenecks.'
    text: '**Content Management Platforms** – Serve thousands of concurrent users
      searching across multimedia assets without bottlenecks.'
  - name: '**E‑commerce Websites** – Accelerate product searches and faceted navigation
      on catalogs containing millions of SKUs.'
    text: '**E‑commerce Websites** – Accelerate product searches and faceted navigation
      on catalogs containing millions of SKUs.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search for Java is a high‑performance library that indexes and
      searches text across more than 50 document formats, providing fast, scalable
      full‑text search for Java applications.
    question: What is GroupDocs.Search for Java?
  - answer: Visit the [GroupDocs's licensing page](https://purchase.groupdocs.com/temporary-license/)
      to request a free trial or purchase a full license for production use.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes, you can **add documents to index** at any time using the `IndexManager.addDocument()`
      method; the changes propagate automatically across the cluster. **IndexManager.addDocument()**
      adds a new document to the index and propagates it across the network.
    question: Can I add new documents after the network is deployed?
  - answer: Typical issues include mismatched base paths, port conflicts, and insufficient
      file‑system permissions. Double‑check each node’s configuration and ensure all
      directories are accessible.
    question: What are common pitfalls when configuring nodes?
  - answer: Absolutely. GroupDocs.Search offers real‑time indexing APIs that immediately
      make newly added documents searchable across all nodes without downtime.
    question: Does the network support real‑time indexing?
  type: FAQPage
title: กำหนดค่าการค้นหาแบบกระจายด้วย GroupDocs.Search Java Network
type: docs
url: /th/java/search-network/deploy-groupdocs-search-java-network/
weight: 1
---

# กำหนดค่าการค้นหาแบบกระจายด้วย GroupDocs.Search Java Network

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **configure distributed search** มีความสำคัญสำหรับการจัดการคอลเลกชันเอกสารขนาดมหาศาลพร้อมรักษาเวลาในการตอบสนองให้ต่ำอยู่. บทแนะนำนี้จะพาคุณผ่านการตั้งค่าเครือข่าย GroupDocs.Search for Java ที่แข็งแกร่ง, แสดงวิธี **deploy search across multiple nodes**, **add documents to index**, และ **configure TCP settings** เพื่อการสื่อสารที่เชื่อถือได้. เมื่อเสร็จสิ้น, คุณจะมีโซลูชันการค้นหาที่สามารถขยายได้พร้อมใช้งานในสภาพแวดล้อมการผลิตและเข้าใจอย่างชัดเจนว่าทำไมสถาปัตยกรรมนี้จึงเหนือกว่าการตั้งค่าแบบโหนดเดียว.

## คำตอบสั้น
- **configure distributed search คืออะไร?** เป็นกระบวนการเชื่อมต่อโหนดการค้นหาอิสระหลายโหนดเพื่อให้พวกมันทำการจัดทำดัชนีและตอบคำถามร่วมกัน, ส่งมอบอัตราการทำงานที่สูงขึ้นและความทนทานต่อข้อผิดพลาด.  
- **ควรใช้โหนดกี่โหนด?** โดยทั่วไป 3‑5 โหนดให้สมดุลที่ดีระหว่างประสิทธิภาพและความทนทานต่อข้อผิดพลาดสำหรับภาระงานระดับองค์กรส่วนใหญ่.  
- **ต้องการใบอนุญาตหรือไม่?** ใช่ – จำเป็นต้องมีใบอนุญาตชั่วคราวหรือเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิตของ GroupDocs.Search.  
- **ควรใช้พอร์ตใด?** เลือกพอร์ตที่ว่างบนเซิร์ฟเวอร์ของคุณ; ตัวอย่างใช้พอร์ต 49136‑49139, แต่ช่วงพอร์ตที่เปิดอยู่ใดก็ได้ก็ทำงานได้.  
- **สามารถเพิ่มเอกสารใหม่หลังการปรับใช้ได้หรือไม่?** แน่นอน – คุณสามารถ **add documents to index** ได้ตลอดเวลาโดยไม่ต้องรีสตาร์ทเครือข่าย.

## configure distributed search คืออะไร?
การกำหนดสถาปัตยกรรมการค้นหาแบบกระจายหมายถึงการเชื่อมต่อโหนดการค้นหาอิสระหลายโหนดเพื่อให้พวกมันแบ่งงานจัดทำดัชนีและตอบคำถามร่วมกัน. สิ่งนี้ช่วยลดภาระบนเครื่องเดียว, ปรับปรุงอัตราการทำงานและความน่าเชื่อถือ, และให้ความซ้ำซ้อนในตัวสำหรับความทนทานต่อข้อผิดพลาด.

## ทำไมต้องใช้ GroupDocs.Search for Java?
GroupDocs.Search for Java ให้ **high‑performance indexing** (สูงสุด 1 GB/s บนฮาร์ดแวร์สมัยใหม่) และ **scalable architecture** ที่รองรับคลัสเตอร์ที่มี 10+ โหนด. มันเข้าใจ **50+ document formats** โดยเนทีฟ—รวมถึง PDF, DOCX, XLSX, PPTX, และไฟล์อีเมล—ทำให้คุณสามารถจัดทำดัชนีเนื้อหาธุรกิจใดก็ได้โดยไม่ต้องใช้ตัวแปลงเพิ่มเติม. คลาส `TcpSettings` ที่มีในตัวช่วยให้คุณปรับแต่ง latency, throughput, และช่วง keep‑alive อย่างละเอียด, เพื่อให้การสื่อสารระหว่างโหนดเชื่อถือได้แม้ข้ามขอบเขตศูนย์ข้อมูล. **TcpSettings** กำหนดพารามิเตอร์การสื่อสาร TCP ระดับต่ำระหว่างโหนด.

## ข้อกำหนดเบื้องต้น

### ไลบรารีและการพึ่งพาที่จำเป็น
คุณจะต้องใช้ **GroupDocs.Search for Java** เวอร์ชัน 25.4 หรือใหม่กว่า. ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณมี Java ติดตั้งอยู่.

### ความต้องการการตั้งค่าสภาพแวดล้อม
- ชุดพัฒนา Java (JDK) รุ่น 11 หรือใหม่กว่า.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse เพื่อการจัดการโครงการที่สะดวก.

### ความรู้เบื้องต้นที่จำเป็น
ทักษะการเขียนโปรแกรม Java เบื้องต้นและความเข้าใจทั่วไปเกี่ยวกับการกำหนดค่าเครือข่ายจะช่วยให้คุณทำตามขั้นตอนได้อย่างราบรื่น.

## การตั้งค่า GroupDocs.Search for Java
เพื่อเริ่มต้น, เพิ่ม GroupDocs.Search for Java ลงในโครงการของคุณ. คุณสามารถทำได้ผ่าน Maven หรือโดยการดาวน์โหลดไลบรารีโดยตรง.

**Maven Setup**  
เพิ่ม repository และการกำหนด dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

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

**Direct Download**  
หรืออีกทางเลือกหนึ่ง, ดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
เพื่อใช้ GroupDocs.Search อย่างเต็มที่, คุณสามารถรับใบอนุญาตชั่วคราวหรือซื้อใบอนุญาตได้. เยี่ยมชม [GroupDocs's licensing page](https://purchase.groupdocs.com/temporary-license/) เพื่อดูข้อมูลเพิ่มเติมเกี่ยวกับการขอทดลองใช้ฟรีหรือใบอนุญาตเต็ม. คุณอาจใช้ [GroupDocs licensing page](https://purchase.groupdocs.com/temporary-license/) สำหรับวัตถุประสงค์เดียวกัน.

### การเริ่มต้นและการตั้งค่าพื้นฐาน
มาลองเริ่มต้น GroupDocs.Search ในแอปพลิเคชัน Java ของคุณ:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        // Add documents to the index
        index.add("YOUR_DOCUMENT_DIRECTORY");
    }
}
```

## คู่มือการนำไปใช้
ในส่วนนี้, เราจะพาคุณผ่านการกำหนดค่าและการปรับใช้เครือข่ายการค้นหาโดยใช้ GroupDocs.Search for Java.

### วิธีการกำหนดค่า distributed search ด้วย GroupDocs.Search?
โหลดการกำหนดค่าเครือข่าย, กำหนดเส้นทางฐาน, และตั้งค่าพารามิเตอร์ TCP เพียงไม่กี่บรรทัดของโค้ด. รูปแบบการตอบโดยตรงนี้แสดงขั้นตอนสำคัญก่อนการอธิบายรายละเอียดใด ๆ.

แรก, สร้างอ็อบเจ็กต์ `SearchNetworkConfig`, ระบุไดเรกทอรีฐานที่ใช้ร่วมกัน, และกำหนดพอร์ต TCP ที่แตกต่างสำหรับแต่ละโหนด. **SearchNetworkConfig** กำหนดการตั้งค่าสำหรับคลัสเตอร์การค้นหาแบบกระจาย, เช่นไดเรกทอรีฐานและพอร์ตของโหนด. จากนั้น, สร้างอินสแตนซ์ของ `TcpSettings`—คลาสที่ควบคุมเวลาเชื่อมต่อของซ็อกเก็ต, ขนาดบัฟเฟอร์, และพฤติกรรม keep‑alive. สุดท้าย, เรียก `NetworkManager.deploy(config)` เพื่อเปิดคลัสเตอร์. **NetworkManager** จัดการการปรับใช้และการจัดการโหนดการค้นหาในคลัสเตอร์.

#### การกำหนดค่าเครือข่าย
คลาส `TcpSettings` เป็นศูนย์กลางการกำหนดค่าสำหรับการสื่อสารระดับ TCP ระหว่างโหนดทั้งหมด. มันให้คุณตั้งค่า timeout การเชื่อมต่อ, ขนาดบัฟเฟอร์อ่าน/เขียน, และว่าจะใช้ Nagle’s algorithm หรือไม่.

```java
Configuration configuration = ConfiguringSearchNetwork.configure("YOUR_DOCUMENT_DIRECTORY", 49136);
```

#### การปรับใช้โหนด
ปรับใช้แต่ละโหนดโดยระบุรหัสประจำตัวที่ไม่ซ้ำและการกำหนดค่าที่ได้กำหนดไว้ก่อนหน้า. ขั้นตอนการปรับใช้จะลงทะเบียนโหนดกับคลัสเตอร์โดยอัตโนมัติ, เปิดซ็อกเก็ตที่รับฟัง, และเริ่มเธรดการจัดทำดัชนีเบื้องหลัง.

```java
public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
    // Define timeouts for sending and receiving data over the network.
    int sendTimeout = 3000;
    int receiveTimeout = 3000;

    // Create and start three nodes that can run on separate servers or together.
    SearchNetworkNode node1 = new SearchNetworkNode(
        1,
        basePath + "Node1",
        new TcpSettings(basePort + 1, sendTimeout, receiveTimeout)
    );
    node1.start();

    SearchNetworkNode node2 = new SearchNetworkNode(
        2,
        basePath + "Node2",
        new TcpSettings(basePort + 2, sendTimeout, receiveTimeout)
    );
    node2.start();

    SearchNetworkNode node3 = new SearchNetworkNode(
        3,
        basePath + "Node3",
        new TcpSettings(basePort + 3, sendTimeout, receiveTimeout)
    );
    node3.start();

    // Create and configure the main configuration node.
    SearchNetworkNode node0 = new SearchNetworkNode(
        0,
        basePath + "Node0",
        new TcpSettings(basePort, sendTimeout, receiveTimeout),
        new ConsoleLogger(),
        configuration
    );

    // Add an event handler to notify when the configuration is complete.
    node0.getEvents().ConfigurationCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            // Event handling logic here (e.g., logging)
        }
    });

    // Configure all nodes in the network using the main configuration node.
    node0.configureAllNodes();

    // Start the search network by launching all configured nodes.
    node0.start();

    // Return an array of all deployed nodes.
    return new SearchNetworkNode[] {node0, node1, node2, node3};
}
```

## ปัญหาทั่วไปและวิธีแก้
- **Directory Access Errors** – ตรวจสอบให้แน่ใจว่าไดเรกทอรีฐานของทุกโหนดมีอยู่และกระบวนการ Java มีสิทธิ์อ่าน/เขียน.  
- **Port Conflicts** – ยืนยันว่าพอร์ตที่เลือก (เช่น 49136‑49139) ไม่ถูกใช้โดยบริการอื่น; คุณสามารถรัน `netstat -an` เพื่อตรวจสอบ.  
- **Timeouts on Slow Networks** – เพิ่มค่า `TcpSettings.setConnectionTimeout()` หากคุณพบการตัดการเชื่อมต่อบ่อยในสภาพแวดล้อมที่มี latency สูง.  
- **Index Corruption** – ทำการสำรองโฟลเดอร์ดัชนีเป็นประจำและเปิดใช้งาน `NetworkManager.enableAutoRecovery()` เพื่อสร้าง shard ที่เสียหายใหม่โดยอัตโนมัติ.

## การประยุกต์ใช้ในเชิงปฏิบัติ
การปรับใช้เครือข่ายการค้นหาแบบกระจายสามารถเป็นประโยชน์ในหลายสถานการณ์:

1. **Large‑Scale Enterprise Systems** – จัดทำดัชนีสัญญา, นโยบาย, และรายงานนับล้านรายการพร้อมรักษาการตอบสนองของคำค้นให้ต่ำกว่า 1 วินาที.  
2. **Content Management Platforms** – ให้บริการผู้ใช้หลายพันคนที่ทำการค้นหาข้ามสินทรัพย์มัลติมีเดียโดยไม่มีคอขวด.  
3. **E‑commerce Websites** – เร่งการค้นหาผลิตภัณฑ์และการนำทางแบบ faceted บนแคตาล็อกที่มีสินค้าล้าน SKU.

## การพิจารณาด้านประสิทธิภาพ
เพื่อให้สภาพแวดล้อม **configure distributed search** ของคุณทำงานอย่างมีประสิทธิภาพ:

- **Index Size Management** – GroupDocs.Search สามารถจัดการดัชนีที่เกิน 100 GB; อย่างไรก็ตาม, ควรตรวจสอบ I/O ของดิสก์และพิจารณา sharding คอลเลกชันขนาดใหญ่ข้ามหลายโหนด.  
- **Resource Tuning** – ใช้แฟล็กการปรับแต่งหน่วยความจำของ Java (`-Xmx8g -Xms4g`) ตามภาระงานของคุณ, และปรับ `TcpSettings.setReadBufferSize()` สำหรับเครือข่ายที่มี throughput สูง.  
- **Health Monitoring** – ใช้ `NetworkHealthMonitor` ที่มีในตัวเพื่อติดตาม CPU, หน่วยความจำ, และ latency ของเครือข่ายต่อโหนด, และตั้งการแจ้งเตือนสำหรับเกณฑ์ที่คุณกำหนด.

## สรุป
โดยทำตามบทแนะนำนี้, คุณได้เรียนรู้วิธี **configure distributed search** และปรับใช้เครือข่าย GroupDocs.Search Java ที่สามารถขยายได้. โซลูชันนี้สามารถปรับปรุงความเร็วและความน่าเชื่อถือของฟีเจอร์การค้นหาในแอปพลิเคชันของคุณอย่างมหาศาล, โดยเฉพาะเมื่อจัดการกับคอลเลกชันเอกสารขนาดใหญ่และหลากหลาย.

### ขั้นตอนต่อไป
สำรวจความสามารถขั้นสูงเช่นตัววิเคราะห์แบบกำหนดเอง, การจัดการคำพ้อง, และการจัดทำดัชนีแบบเรียลไทม์เพื่อปรับปรุงประสบการณ์การค้นหาของคุณต่อไป. คุณอาจรวมเครือข่ายกับชั้น API แบบ RESTful เพื่อเปิดเผยฟังก์ชันการค้นหาให้กับไคลเอนต์ภายนอก.

### เรียกร้องให้ดำเนินการ
เริ่มนำโซลูชันที่แข็งแกร่งนี้ไปใช้ในโครงการของคุณวันนี้และสัมผัสการเพิ่มประสิทธิภาพด้วยตนเอง!

## คำถามที่พบบ่อย

**Q: GroupDocs.Search for Java คืออะไร?**  
A: GroupDocs.Search for Java เป็นไลบรารีประสิทธิภาพสูงที่จัดทำดัชนีและค้นหาข้อความในรูปแบบเอกสารมากกว่า 50 แบบ, ให้การค้นหาแบบเต็มข้อความที่เร็วและสามารถขยายได้สำหรับแอปพลิเคชัน Java.

**Q: ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Search อย่างไร?**  
A: เยี่ยมชม [GroupDocs's licensing page](https://purchase.groupdocs.com/temporary-license/) เพื่อขอทดลองใช้ฟรีหรือซื้อใบอนุญาตเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

**Q: ฉันสามารถเพิ่มเอกสารใหม่หลังจากที่เครือข่ายถูกปรับใช้ได้หรือไม่?**  
A: ใช่, คุณสามารถ **add documents to index** ได้ตลอดเวลาโดยใช้เมธอด `IndexManager.addDocument()`; การเปลี่ยนแปลงจะกระจายโดยอัตโนมัติทั่วคลัสเตอร์. **IndexManager.addDocument()** เพิ่มเอกสารใหม่ลงในดัชนีและกระจายไปทั่วเครือข่าย.

**Q: ปัญหาที่พบบ่อยเมื่อกำหนดค่าโหนดคืออะไร?**  
A: ปัญหาที่พบบ่อยรวมถึงเส้นทางฐานที่ไม่ตรงกัน, ความขัดแย้งของพอร์ต, และสิทธิ์ระบบไฟล์ที่ไม่เพียงพอ. ตรวจสอบการกำหนดค่าแต่ละโหนดอีกครั้งและให้แน่ใจว่าไดเรกทอรีทั้งหมดเข้าถึงได้.

**Q: เครือข่ายสนับสนุนการจัดทำดัชนีแบบเรียลไทม์หรือไม่?**  
A: แน่นอน. GroupDocs.Search มี API การจัดทำดัชนีแบบเรียลไทม์ที่ทำให้เอกสารที่เพิ่มใหม่สามารถค้นหาได้ทันทีทั่วทุกโหนดโดยไม่มีเวลาหยุดทำงาน.

---

**อัปเดตล่าสุด:** 2026-06-27  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## บทแนะนำที่เกี่ยวข้อง

- [บทแนะนำและตัวอย่างของ GroupDocs.Search for Java](/search/net/)
- [ปรับใช้โหนดเครือข่ายการค้นหาใน .NET ด้วย GroupDocs เพื่อการจัดทำดัชนีและการดึงข้อมูลเอกสารที่มีประสิทธิภาพ](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [บทแนะนำการเพิ่มประสิทธิภาพการค้นหาสำหรับ GroupDocs.Search .NET](/search/net/performance-optimization/)
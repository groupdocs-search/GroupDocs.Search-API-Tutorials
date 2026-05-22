---
date: '2026-05-22'
description: เรียนรู้วิธีเพิ่มเอกสารลงในดัชนีและสร้างเครือข่ายการค้นหาที่ปรับขนาดได้โดยใช้
  GroupDocs.Search for Java รองรับการค้นหาข้ามหลายเซิร์ฟเวอร์
keywords:
- build scalable search network
- add documents to index
- search across multiple servers
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  headline: Build Scalable Search Network – Index Docs with GroupDocs Java
  type: TechArticle
- description: Learn how to add documents to index and build scalable search network
    using GroupDocs.Search for Java. Supports search across multiple servers.
  name: Build Scalable Search Network – Index Docs with GroupDocs Java
  steps:
  - name: Define Base Path and Port
    text: The `SearchNetworkNode` class represents a single node that participates
      in the distributed index.
  - name: Configure the Network
    text: '`NetworkConfiguration` holds the common settings (base path, ports, replication
      factor) that every node reads at startup.'
  - name: Deploy Nodes Using Configuration
    text: '`SearchNetworkNode` instances are started with the same configuration file,
      allowing them to discover each other via the defined base port range.'
  - name: Define Subscription Method
    text: '`NodeEventListener` is an interface you implement to receive callbacks
      for indexing progress, errors, and node health changes.'
  - name: Use Subscription Method
    text: Register your listener with each node so that you get real‑time feedback
      during large batch operations.
  type: HowTo
- questions:
  - answer: Change the `basePort` variable in your configuration code to an available
      port.
    question: How do I handle port conflicts when deploying nodes?
  - answer: Yes, it supports real‑time indexing with appropriate configurations.
    question: Can GroupDocs.Search be used for real‑time indexing?
  - answer: Network connectivity and incorrect path settings are frequent culprits.
      Ensure all paths and ports are correctly configured.
    question: What are some common issues during node deployment?
  - answer: Absolutely. You can call `index.add(...)` on any node, and the network
      will distribute the new workload automatically.
    question: Is it possible to add documents to index after the network is running?
  - answer: A temporary trial license is sufficient for testing; a commercial license
      is required for production use.
    question: Do I need a license for development testing?
  type: FAQPage
title: สร้างเครือข่ายการค้นหาที่ปรับขนาดได้ – ทำดัชนีเอกสารด้วย GroupDocs Java
type: docs
url: /th/java/search-network/scalable-search-groupdocs-java/
weight: 1
---

# สร้างเครือข่ายการค้นหาที่ขยายได้ – ดัชนีเอกสารด้วย GroupDocs.Java

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีการเพิ่มเอกสารลงในดัชนี** และ **สร้างเครือข่ายการค้นหาที่ขยายได้** ด้วย GroupDocs.Search สำหรับ Java เราจะอธิบายการกำหนดค่าเครือข่ายการค้นหา การปรับใช้โหนด และการจัดการเหตุการณ์เพื่อให้แอปพลิเคชันของคุณสามารถประมวลผลคอลเลกชันเอกสารขนาดใหญ่ได้อย่างมีประสิทธิภาพบนหลายเซิร์ฟเวอร์

## คำตอบด่วน
- **อะไรหมายถึง “add documents to index”?** หมายถึงการใส่ไฟล์ลงในดัชนีที่สามารถค้นหาได้เพื่อให้สามารถสืบค้นได้อย่างรวดเร็ว.  
- **ไลบรารีใดที่ให้ความสามารถนี้?** GroupDocs.Search for Java.  
- **ฉันต้องการไลเซนส์หรือไม่?** มีไลเซนส์ทดลองชั่วคราว; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถขยายแนวนอนได้หรือไม่?** ได้ — โดยการปรับใช้หลายอินสแตนซ์ของ SearchNetworkNode.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 หรือสูงกว่า.

## การเพิ่มเอกสารลงในดัชนีคืออะไร?
โหลดไฟล์ต้นทางของคุณ (PDF, DOCX, PPTX ฯลฯ) เข้าไปในเอนจิน GroupDocs.Search ซึ่งจะสกัดข้อความ สร้างตารางความถี่ของคำ และจัดเก็บไว้ในไฟล์ดัชนี ดัชนีที่ได้ทำให้การค้นหาคำสำคัญในระดับต่ำกว่าหนึ่งวินาทีเป็นไปได้แม้กับคอลเลกชันหลายร้อยหน้า

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java ในสภาพแวดล้อมเครือข่าย?
กระจายภาระงานการทำดัชนีและการค้นหาไปยังหลายโหนด ลดความหน่วงของการสืบค้นโดยประมวลผลใกล้แหล่งข้อมูล และเพิ่มหรือลบโหนดได้โดยไม่มีเวลาหยุดทำงาน สถาปัตยกรรมนี้ทำให้คุณ **ค้นหาข้ามหลายเซิร์ฟเวอร์** พร้อมรักษาประสิทธิภาพให้คงที่

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** ติดตั้งแล้ว.  
- **Maven** สำหรับการจัดการ dependencies.  
- ความคุ้นเคยพื้นฐานกับ Java และโครงสร้างโครงการ Maven.  

### ไลบรารีที่จำเป็น, เวอร์ชัน, และ Dependencies
เพื่อทำให้ GroupDocs.Search for Java ทำงานได้ ให้เพิ่มสิ่งต่อไปนี้ในโครงการ Maven ของคุณ:

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

หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/). คุณยังสามารถพบเวอร์ชันได้ที่ [GroupDocs Search Java releases](https://releases.groupdocs.com/search/java/).

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- JDK 8 หรือสูงกว่า ติดตั้งบนระบบของคุณ.  
- Maven ติดตั้งและกำหนดค่าไว้หากใช้โครงการ Maven.

### ความรู้เบื้องต้นที่จำเป็น
- ความเข้าใจพื้นฐานของการเขียนโปรแกรม Java.  
- ความคุ้นเคยกับการจัดการ dependencies ใน Maven.

## การตั้งค่า GroupDocs.Search สำหรับ Java
1. **Maven Setup**: เพิ่ม repository และ dependency ตามที่แสดงด้านบนในไฟล์ `pom.xml` ของคุณ.  
2. **Direct Download**: หรือคุณสามารถดาวน์โหลดไลบรารีจาก [GroupDocs Search Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
- รับไลเซนส์ทดลองฟรีหรือชั่วคราวโดยเยี่ยมชม [GroupDocs website](https://purchase.groupdocs.com/temporary-license).  
- สำหรับการเข้าถึงเต็มรูปแบบและการสนับสนุน พิจารณาซื้อไลเซนส์เชิงพาณิชย์.

### การเริ่มต้นพื้นฐาน
Initialize GroupDocs.Search in your Java application:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index/directory");

        // Add documents to the index
        index.add("path/to/documents");
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## วิธีเพิ่มเอกสารลงในดัชนีในเครือข่ายการค้นหา?
โหลดเอกสารของคุณผ่านโหนดใดก็ได้ในเครือข่าย; เฟรมเวิร์กจะกระจายภาระงานการทำดัชนีโดยอัตโนมัติ ปรับสมดุลโหลด และอัปเดตดัชนีที่แชร์แบบเรียลไทม์ แต่ละโหนดจะประมวลผลไฟล์ที่มอบหมาย สกัดข้อความ และเขียนการเปลี่ยนแปลงแบบเพิ่มขึ้นไปยังดัชนีศูนย์กลาง เพื่อให้เนื้อหาใหม่ที่เพิ่มเข้ามาสามารถค้นหาได้ทั่วทุกโหนดโดยทันที

### ฟีเจอร์ 1: กำหนดค่า Search Network
#### ภาพรวม
การกำหนดค่าเครือข่ายการค้นหาต้องตั้งค่าโหนดเพื่อจัดการและกระจายงานค้นหาอย่างมีประสิทธิภาพ.

##### ขั้นตอนที่ 1: กำหนด Base Path และ Port
คลาส `SearchNetworkNode` แสดงถึงโหนดเดียวที่เข้าร่วมในดัชนีแบบกระจาย.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SearchNetworkNodeEvents/";
int basePort = 49140; // Change if necessary due to busy port issues
```

##### ขั้นตอนที่ 2: กำหนดค่า Network
`NetworkConfiguration` เก็บการตั้งค่าทั่วไป (base path, ports, replication factor) ที่ทุกโหนดอ่านเมื่อเริ่มต้น.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.scaling.configuring.*;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

### ฟีเจอร์ 2: ปรับใช้โหนด Search Network
#### ภาพรวม
ปรับใช้โหนดเพื่อกระจายและจัดการการดำเนินการค้นหาผ่านเครือข่ายของคุณ.

##### ขั้นตอนที่ 1: ปรับใช้โหนดโดยใช้การกำหนดค่า
อินสแตนซ์ของ `SearchNetworkNode` จะเริ่มด้วยไฟล์การกำหนดค่าเดียวกัน ทำให้พวกมันค้นหาและเชื่อมต่อกันผ่านช่วงพอร์ตฐานที่กำหนด.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
```

### ฟีเจอร์ 3: สมัครรับเหตุการณ์ของโหนด
#### ภาพรวม
การสมัครรับเหตุการณ์ของโหนดทำให้คุณสามารถตรวจสอบและตอบสนองต่อการกระทำต่าง ๆ ภายในเครือข่ายการค้นหา.

##### ขั้นตอนที่ 1: กำหนดวิธีการสมัครรับ
`NodeEventListener` เป็นอินเทอร์เฟซที่คุณต้องทำการ implement เพื่อรับ callback สำหรับความคืบหน้าการทำดัชนี, ข้อผิดพลาด, และการเปลี่ยนแปลงสถานะสุขภาพของโหนด.

```java
import com.groupdocs.search.events.*;
import com.groupdocs.search.scaling.events.*;

public static void subscribe(SearchNetworkNode node) {
    // Subscribe to IndexingCompleted event
    node.getEvents().IndexingCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            System.out.println("Indexing completed.");
        }
    });

    // Additional events can be subscribed similarly...
}
```

##### ขั้นตอนที่ 2: ใช้วิธีการสมัครรับ
ลงทะเบียน listener ของคุณกับแต่ละโหนดเพื่อรับฟีดแบ็กแบบเรียลไทม์ระหว่างการดำเนินการแบบแบชขนาดใหญ่.

```java
SearchNetworkNode masterNode = nodes[0];
subscribe(masterNode);
```

### ปิดโหนด
ควรปิดโหนดอย่างสุภาพเสมอเพื่อทำการ flush การเขียนที่ค้างอยู่และปล่อย socket ของเครือข่าย.

```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## การประยุกต์ใช้งานจริง
1. **Enterprise Search Solutions** – ปรับใช้เครือข่ายการค้นหาเพื่อจัดการการค้นหาเอกสารขนาดใหญ่ข้ามหลายเซิร์ฟเวอร์.  
2. **E‑commerce Platforms** – ปรับปรุงความสามารถการค้นหาผลิตภัณฑ์โดยกระจายงานทำดัชนีไปยังหลายโหนด.  
3. **Content Management Systems (CMS)** – ปรับปรุงประสิทธิภาพของการดึงและอัปเดตเนื้อหาในสภาพแวดล้อม CMS.  

## พิจารณาด้านประสิทธิภาพ
- ปรับการปรับใช้โหนดให้เหมาะสมตามทรัพยากรของระบบของคุณ.  
- ตรวจสอบการใช้หน่วยความจำเป็นประจำเพื่อป้องกันการรั่วไหล โดยเฉพาะเมื่อจัดการชุดข้อมูลขนาดใหญ่.  
- ใช้การตั้งค่าการกำหนดค่าเพื่อปรับจูนการทำดัชนีและการค้นหาให้มีประสิทธิภาพดียิ่งขึ้น.  

## ปัญหาที่พบบ่อยและวิธีแก้ไข
| ปัญหา | สาเหตุทั่วไป | วิธีแก้ |
|-------|---------------|--------|
| การชนของพอร์ต | `basePort` ถูกใช้แล้ว | เปลี่ยน `basePort` เป็นหมายเลขที่ใช้ได้ |
| โหนดไม่สามารถเข้าถึงได้ | ไฟร์วอลล์หรือกฎเครือข่าย | เปิดพอร์ตที่จำเป็นและตรวจสอบการเชื่อมต่อ |
| ดัชนีไม่อัปเดต | เส้นทางเอกสารไม่ถูกต้อง | ตรวจสอบว่า `basePath` ชี้ไปยังไดเรกทอรีที่ถูกต้อง |
| การใช้หน่วยความจำสูง | การทำดัชนีเป็นแบชขนาดใหญ่ | ทำดัชนีเอกสารเป็นแบชเล็กลงหรือเพิ่มขนาด heap |

## คำถามที่พบบ่อย
**Q: ฉันจะจัดการกับการชนของพอร์ตเมื่อปรับใช้โหนดอย่างไร?**  
A: เปลี่ยนตัวแปร `basePort` ในโค้ดการกำหนดค่าของคุณเป็นพอร์ตที่ใช้ได้.

**Q: GroupDocs.Search สามารถใช้สำหรับการทำดัชนีแบบเรียลไทม์ได้หรือไม่?**  
A: ได้, รองรับการทำดัชนีแบบเรียลไทม์ด้วยการกำหนดค่าที่เหมาะสม.

**Q: ปัญหาที่พบบ่อยระหว่างการปรับใช้โหนดมีอะไรบ้าง?**  
A: การเชื่อมต่อเครือข่ายและการตั้งค่าเส้นทางที่ไม่ถูกต้องเป็นสาเหตุบ่อย ตรวจสอบให้แน่ใจว่าเส้นทางและพอร์ตทั้งหมดกำหนดค่าอย่างถูกต้อง.

**Q: สามารถเพิ่มเอกสารลงในดัชนีหลังจากเครือข่ายทำงานแล้วได้หรือไม่?**  
A: แน่นอน คุณสามารถเรียก `index.add(...)` บนโหนดใดก็ได้ และเครือข่ายจะกระจายภาระงานใหม่โดยอัตโนมัติ.

**Q: ฉันต้องการไลเซนส์สำหรับการทดสอบการพัฒนาหรือไม่?**  
A: ไลเซนส์ทดลองชั่วคราวเพียงพอสำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## แหล่งข้อมูล
- **Documentation**: [GroupDocs Search Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Latest Release](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

โดยทำตามคำแนะนำนี้ คุณจะสามารถ **เพิ่มเอกสารลงในดัชนี** และจัดการเครือข่ายการค้นหาที่แข็งแกร่งและ **สร้างเครือข่ายการค้นหาที่ขยายได้** ด้วย GroupDocs.Search สำหรับ Java ขอให้เขียนโค้ดอย่างสนุก!

---

**อัปเดตล่าสุด:** 2026-05-22  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง
- [Search Network Tutorials for GroupDocs.Search .NET](/search/net/search-network/)
- [How to Configure a .NET Search Network Using GroupDocs.Search and Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Deploy a Search Network Node in .NET using GroupDocs for Efficient Document Indexing and Retrieval](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
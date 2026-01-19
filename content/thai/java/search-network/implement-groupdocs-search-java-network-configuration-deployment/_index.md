---
date: '2026-01-19'
description: เรียนรู้วิธีกำหนดค่าเครือข่ายและปรับใช้ GroupDocs.Search สำหรับ Java
  รวมถึงการทำดัชนี การค้นหารูปภาพ การปรับใช้โหนด และการสมัครรับเหตุการณ์
keywords:
- GroupDocs.Search Java Network
- Java-based document search network
- configuring and deploying GroupDocs.Search
title: 'วิธีกำหนดค่าเครือข่าย: คู่มือการกำหนดค่าและการปรับใช้ GroupDocs.Search Java'
type: docs
url: /th/java/search-network/implement-groupdocs-search-java-network-configuration-deployment/
weight: 1
---

# วิธีตั้งค่าเครือข บทนำ
ในยุใหญ่เป็นทักษะสำคัญสำหรับองค์กรใด ๆ โซลูชันแบบดั้งเดิมมักเจอขีดจำกัดด้านประสิทธิภาพเมื่อชุดข้อมูลเพิ่มขึ้น แต่ **GroupDocs.Search for Java** ให้พื้นฐานที่สามารถขยายได้และมีประสิทธิภาพสูง ในบทเรียนนี้เราจะพาคุณผ่านทุกขั้นตอนที่จำเป็นในการตั้งค่าเครือขายะการค้น does GroupDocs.Search use by default?** ตัวอย่างใช้พอร์ต **49120** แต่คุณสามารถเลือกพอร์ตว่างใดก็ได้  
- **Can I add or remove nodes without downtime?** ใช่—โหนดสามารถปรับใช้หรือถอดออกได้แบบไดนามิก  
- **Do I need a license for production?** จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต; มีใบอนุญาตทดลองสำหรับการประเมินผล  
- **Is image search supported out of the box?** ใช่—GroupDocs.Search มีการเปรียบเทียบแฮชของภาพในตัว  

## Search Network คืออะไร?
Search Network คือการรวบรวมของอินสแตนซ์ **เวลาในการตอบสน่งให้ต่ำ

## ทำไมต้องใช้ GroupDocs.Search for Java?
- **Scalability:** เพิ่มโหนดเมื่อคลังข้อมูลของคุณเติบโต  
- **Performance:** การทำดัชนีและการประมวลผลการค้นหาแบบขนานช่วยลดความหน่วง  
- **Flexibility:** รองรับข้อความ, PDF, ไฟล์ Office, และการค้นหาภาพ  
- **Event‑Driven Management:** การตรวจสอบแบบเรียลไทม์ผ่านการสมัครรับเหตุการณ์  

## ข้อกำหนดเบื้องต้น
- **JDK 8+** ติดตั้งแล้ว  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**  
- Maven สำหรับการจัดการ dependencies  
- ความรู้พื้นฐานเกี่ยวกับ Java และแนวคิดเครือข่าย  

### ไลบรารีและ dependencies ที่จำเป็น
Add the GroupDocs repository and dependency to your `pom.xml`:

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

หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## การตั้งค่า GroupDocs.Search for Java
### การติดตั้งผ่าน Maven
ส่วนโค้ด Maven ด้านบนจะดึงไลบรารีเข้ามาในโปรเจกต์ของคุณโดยอัตโนมัติ

### การรับใบอนุญาต
- **Free Trial** – ทดลองใช้คุณลักษณะหลัก  
- **Temporary License** – ระยะเวลาการทดสอบต่อเนื่อง  
- **Full License** – พร้อมใช้งานในสภาพแวดล้อมการผลิต, ไม่จำกัดการใช้  

### Basic Initialization and Setup
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an instance of Index with the path to store index data.
        String indexPath = "path/to/index";
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## คู่มือการใช้งาน
ต่อไปเราจะเจาะลึกแต่ละงานหลักโดยใช้โค้ดสแนปช็อตที่ชัดเจนและเป็นขั้นตอน

### วิธีการปรับใช้โหนดใน Search Network
การปรับใช้หลายโหนงานและเพิ่มความทนทานต่อข้อผิดพลาด

```java
public class SearchNetworkDeployment {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Change if necessary.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        System.out.println("Deployed " + nodes.length + " search network nodes.");
    }
}
```

**คำอธิบคุณ  
- `basePort` คือ **search network port** ที่แต่ละโหนดฟัง; ปรับเพื่อหลีกเลี่ยงการชนกัน  
- เมธอดนี้คืนค่าอาร์เรย์ของอ็อบเจกต์ `SearchNetworkNode` ที่แสดงถึงแต่ละโหนดที่ทำงานอยู่  

### วิธีการสมัครรับเหตุการณ์
การสมัครรับเหตุการณ์ให้ข้อมูลเชิงลึกแบบเรียลไทม์เกี่ยวกับสุขภาพของโหนด, ความคืบหน้าการทำดัชนี, และข้อผิดพลาด

```java
public class NodeEventSubscription {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Adjust if needed.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

        SearchNetworkEvents.subscribe(nodes[0]);
        
        System.out.println("Subscribed to events for the master node.");
    }
}
```

**คำอธิบาย:**  
- `nodes[0]` ถือเป็น **master node**; คุณยังสามารถสมัครรับเหตุการณ์ของแต่ละ worker node แยกกันได้  

### วิธีการทำดัชนีเอกสาร
การทำดัชนีที่มีประสิทธิภาพเป็นกระดูกสันหลังของผลลัพธ์การค้นหาที่รวดเร็ว

```java
public class DocumentIndexing {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Change if there is a conflict.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

        IndexingDocuments.addDirectories(nodes[0], "YOUR_DOCUMENT_DIRECTORY");
        
        System.out.println("Added directories to master node's index.");
    }
}
```

**คำอธิบาย:**  
- `addDirectories` บอก master node ว่าโฟลเดอร์ใดบ้างที่จะสแกนและทำดัชนี  
- เมื่อทำดัชนีเสร็จแล้ว โหนดทั้งหมดสามารถสืบค้นดัชนีที่แชร์ได้  

### วิธีการทำการค้นหาภาพ
GroupDocs.Search รองรับการเปรียบเทียบแฮชของภาพ ทำให้คุณสามารถค้นหาสินทรัพย์ที่มีลักษณะภาพคล้ายกัน

```java
public class ImageSearch {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY";
        int basePort = 49120; // Modify if needed.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

        SearchImage searchImage = SearchImage.create("YOUR_DOCUMENT_DIRECTORY/ic_arrow_back_black_18dp.png");

        imageSearch(nodes[0], searchImage, 8);
    }
}
```

**คำอธิบาย:**  
- `SearchImage.create` โหลดภาพอ้างอิง  
- `imageSearch` ทำการค้นหาบนโหนดที่เลือก โดยอนุญาตความแตกต่างของแฮชสูงสุด **8** (ปรับให้เข้มงวดหรือผ่อนคลายตามต้องการ)  

### วิธีการกำหนดค่าพอร์ตเครือข่าย
หากสภาพแวดล้อมของคุณใช้พอร์ต **49120** อยู่แล้ว คุณสามารถเปลี่ยนเป็นพอร์ต TCP ว่างใดก็ได้:

```java
int customPort = 50000; // Example of a custom port.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, customPort);
```

ตรวจสอบให้แน่ใจว่าพอร์ตที่เลือกเปิดอยู่ในไฟร์วอลล์และไม่ได้ถูกใช้โดยบริการอื่น  

## ปัญหาทั่วไปและการแก้ไขปัญหา
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|---------------|-----|
| โหนดไม่สามารถเริ่มทำงานได้ | การชนกันของพอร์ต | เลือก `basePort` ที่แตกต่างและอัปเดตกฎไฟร์วอลล์ |
| การทำดัชนีช้า | แบนด์วิดท์ I/O ไม่เพียงพอ | ใช้ที่เก็บข้อมูล SSD และเปิดใช้งานการทำดัชนีแบบเพิ่มส่วน |
| การสมัครรับเหตุการณ์ไม่ทำงาน | การลงทะเบียนตัวจัดการเหตุการณ์หายไป | ตรวจสอบให้แน่ใจว่าได้เรียก `SearchNetworkEvents.subscribe(node)` ก่อนเริ่มทำดัชนีใด ๆ |
| การค้นหาภาพไม่ให้ผลลัพธ์ | ความแตกต่างของแฮชต่ำเกินไป | เพิ่มความแตกต่างของแฮชที่อนุญาต (เช่น จาก 4 เป็น 8) |

## คำถามที่พบบ่อย

**Q: ฉันจะเพิ่มประสิทธิภาพการทำดัชนีในเครือข่าย GroupDocs.Search อย่างไร?**  
A: ใช้การทำดัชนีแบบเพิ่มส่วน, เก็บดัชนีบน SSD ที่เร็ว, และจัดสรรหน่วยความจำ heap เพียงพอให้กับ JVM  

**Q: ฉันสามารถเพิ่มหรือถอดโหนดออกโดยไม่ต้องรีสตาร์ทเครือข่ายการค้นหาทั้งหมดได้หรือไม่?**  
A: ใช่—โหนดสามารถปรับใช้หรือถอดออกได้แบบไดนามิก หลังจากเพิ่มโหนด ให้เรียก `SearchNetworkDeployment.deploy` อีกครั้งเพื่อรีเฟรชมุมมองคลัสเตอร์  

**Q: การสมัครรับเหตุการณ์ช่วยปรับปรุงการจัดการเครือข่ายอย่างไร?**  
A: เหตุการณ์ที่สมัครรับจะให้การแจ้งเตือนแบบเรียลไทม์สำหรับการเปลี่ยนแปลงสถานะของโหนด, ความคืบหน้าการทำดัชนี, และข้อผิดพลาด, ช่วยให้แก้ปัญหาเชิงรุกได้  

**Q: สามารถค้นหาหลายรูปแบบเอกสารพร้อมกันได้หรือไม่?**  
A: แน่นอน. GroupDocs.Search รองรับ PDF, Word, Excel, PowerPoint, ภาพ, และรูปแบบอื่น ๆ มากมายในการค้นหาเดียว  

**Q: ข้อมูลในเครือข่าย GroupDocs.Search มีความปลอดภัยแค่ไหน?**  
A: ความปลอดภัยขึ้นอยู่กับโครงสร้างพื้นฐานของคุณ. ใช้ SSL/TLS สำหรับการสื่อสารระหว่างโหนด, จำกัดการเข้าถึงเครือข่าย, และปฏิบัติตามแนวทางปฏิบัติที่ดีที่สุดสำหรับการปกป้องข้อมูล  

---

**อัปเดตล่าสุด:** 2026-01-19  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs
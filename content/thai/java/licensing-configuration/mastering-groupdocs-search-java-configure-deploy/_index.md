---
date: '2026-05-02'
description: เรียนรู้วิธีกำหนดค่าการค้นหาและเปิดใช้งานการอัปเดตการค้นหาแบบเรียลไทม์โดยใช้
  GroupDocs.Search สำหรับ Java คู่มือแบบขั้นตอนต่อขั้นตอนเกี่ยวกับการตั้งค่าเครือข่าย
  การปรับใช้โหนด และการทำดัชนี
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: วิธีกำหนดค่าการค้นหาด้วย GroupDocs.Search ใน Java - คู่มือการกำหนดค่าและการปรับใช้
type: docs
url: /th/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# วิธีการกำหนดค่าการค้นหาด้วย GroupDocs.Search ใน Java

ในโลกดิจิทัลที่เคลื่อนที่อย่างรวดเร็วในทุกวันนี้ การ **วิธีการกำหนดค่าการค้นหา** อย่างมีประสิทธิภาพสามารถทำให้ความสำเร็จของโครงการสำเร็จหรือพังได้ ไม่ว่าคุณจะจัดการกับสัญญาหลายพันฉบับ งานวิจัย หรือรายงานภายใน เครือข่ายการค้นหาที่ออกแบบอย่างดีจะช่วยให้คุณค้นหาเอกสารที่ต้องการได้ในไม่กี่วินาที บทเรียนนี้จะพาคุณผ่านการกำหนดค่าเครือข่ายการค้นหา การปรับใช้โหนด และการเปิดใช้งาน **การอัปเดตการค้นหาแบบเรียลไทม์** ด้วย GroupDocs.Search สำหรับ Java.

## คำตอบสั้น
- **วัตถุประสงค์หลักของเครือข่ายการค้นหาคืออะไร?** เพื่อกระจายการทำดัชนีและการประมวลผลคำค้นหาผ่านหลายโหนดเพื่อความสามารถในการขยายและความเร็ว  
- **เวอร์ชันของไลบรารีที่ต้องการคืออะไร?** GroupDocs.Search for Java v25.4 หรือใหม่กว่า  
- **ฉันต้องการใบอนุญาตหรือไม่?** การทดลองใช้งานฟรีใช้ได้สำหรับการประเมิน; จำเป็นต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานจริง  
- **การอัปเดตแบบเรียลไทม์จัดการอย่างไร?** โดยการสมัครรับเหตุการณ์ของโหนดที่เกิดขึ้นเมื่อมีการเปลี่ยนแปลงการทำดัชนี  
- **ฉันสามารถเพิ่มโฟลเดอร์เอกสารใหม่ได้ทันทีหรือไม่?** ได้—ใช้เมธอด `addDirectories` ของ indexer  

## “วิธีการกำหนดค่าการค้นหา” คืออะไรในบริบทของ GroupDocs?
การกำหนดค่าการค้นหาหมายถึงการตั้งค่า **เครือข่ายการค้นหา** ที่รู้ว่ามีเอกสารของคุณอยู่ที่ไหน โหนดสื่อสารกันอย่างไร และการทำดัชนีถูกประสานกันอย่างไร เมื่อเครือข่ายถูกกำหนดค่าแล้ว คุณสามารถเพิ่มหรือเอาโหนดออกได้โดยไม่มีการหยุดทำงาน ทำให้เข้าถึงผลการค้นหาที่อัปเดตอยู่เสมอได้อย่างต่อเนื่อง.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
- **Scalability:** แจกจ่ายภาระงานไปยังเครื่องหลายเครื่อง  
- **Real‑time updates:** แสดงไฟล์ที่ทำดัชนีใหม่ทันทีทั่วเครือข่าย  
- **Ease of integration:** การตั้งค่า Maven อย่างง่ายและ API ของ Java ที่ชัดเจน  
- **Enterprise‑ready:** รองรับคอร์ปัสขนาดใหญ่และสถานการณ์การค้นหาที่ซับซ้อน  

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** installed.  
- **Maven** สำหรับการจัดการ dependencies.  
- ความคุ้นเคยพื้นฐานกับ Java, Maven, และแนวคิดการค้นหา.  

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การพึ่งพา Maven
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

**Direct Download:** คุณยังสามารถดาวน์โหลดไลบรารีได้จาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
- **Free Trial:** รับใบอนุญาตทดลองเพื่อสำรวจคุณสมบัติทั้งหมด.  
- **Temporary License:** ขอใบอนุญาตชั่วคราวสำหรับช่วงเวลาการประเมินที่ยาวนานขึ้น.  
- **Commercial License:** จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  

### การเริ่มต้นพื้นฐาน
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## วิธีการกำหนดค่าเครือข่ายการค้นหาใน Java

### ขั้นตอนที่ 1: นำเข้าแพ็กเกจที่จำเป็น
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### ขั้นตอนที่ 2: กำหนดค่าเครือข่าย
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameters:** `basePath` ชี้ไปยังโฟลเดอร์เอกสารของคุณ; `basePort` คือพอร์ต TCP ที่ใช้สำหรับการสื่อสารระหว่างโหนด.  

## การปรับใช้โหนดเครือข่ายการค้นหา

### ขั้นตอนที่ 1: นำเข้าแพ็กเกจการปรับใช้
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### ขั้นตอนที่ 2: ปรับใช้โหนด
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Node:** ประสานการค้นหาและการทำดัชนีทั่วทุกโหนด คุณสามารถ **configure master node** การตั้งค่า เช่น การจัดสรร shard และการตรวจสอบสุขภาพ.  

## การสมัครรับเหตุการณ์โหนดสำหรับการอัปเดตการค้นหาแบบเรียลไทม์

### ขั้นตอนที่ 1: นำเข้าแพ็กเกจเหตุการณ์
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### ขั้นตอนที่ 2: สมัครรับเหตุการณ์ของ Master Node
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Event Handling:** เปิดใช้งาน **real time search updates** ทุกครั้งที่มีการเพิ่ม, อัปเดต หรือเอาเอกสารออก.  

## การเพิ่มไดเรกทอรีสำหรับการทำดัชนี

### ขั้นตอนที่ 1: นำเข้าแพ็กเกจ Indexer
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### ขั้นตอนที่ 2: เพิ่มไดเรกทอรีเอกสาร
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dynamic Indexing:** ใช้เมธอด `addDirectories` เพื่อ **add directories to index** อย่างทันทีโดยไม่ต้องรีสตาร์ทเครือข่าย.  

## การดึงเอกสารที่ทำดัชนี

### ขั้นตอนที่ 1: นำเข้าแพ็กเกจ Searcher
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### ขั้นตอนที่ 2: ดึงข้อมูลเอกสาร
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Shard Management:** จัดการชุดข้อมูลขนาดใหญ่อย่างมีประสิทธิภาพโดยกระจายเอกสารไปยัง shard ต่างๆ เพื่อ **optimize shard size** ให้ตรวจสอบสถิติ shard และปรับการตั้งค่า `shardSize` ในการปล่อยเวอร์ชันต่อไป.  

## ทำไมเรื่องนี้ถึงสำคัญสำหรับโครงการของคุณ
เครือข่ายการค้นหาที่กำหนดค่าอย่างเหมาะสมจะขจัดคอขวด ลดความหน่วงเวลา และทำให้ผู้ใช้เห็นเวอร์ชันล่าสุดของเอกสารเสมอ การอัปเดตแบบเรียลไทม์และความสามารถในการ **add directories to index** โดยไม่ต้องหยุดทำงานเป็นคุณค่าที่สำคัญสำหรับบริษัทกฎหมาย สถาบันวิจัย และองค์กรใดๆ ที่ต้องจัดการกับคอลเลกชันเอกสารที่เปลี่ยนแปลงตลอดเวลา.  

## การประยุกต์ใช้งานจริง
1. **Enterprise Document Management:** ศูนย์กลางการค้นหาผ่านไฟล์หลายล้านไฟล์.  
2. **Legal Firms:** ค้นหาไฟล์คดี, สัญญา, และหลักฐานได้อย่างรวดเร็ว.  
3. **Academic Research:** ทำดัชนีนิตยสารและเอกสารวิจัยเพื่อการดึงข้อมูลทันที.  

## พิจารณาด้านประสิทธิภาพ
- **Optimize Indexing:** กำหนดเวลาการรีเฟรชดัชนีเป็นประจำและลบข้อมูลที่ล้าสมัย.  
- **Memory Management:** ตรวจสอบ heap ของ JVM โดยเฉพาะเมื่อจัดการกับ shard ขนาดใหญ่.  
- **Scalability Planning:** เพิ่มโหนดเมื่อคอร์ปัสของคุณขยาย; เครือข่ายจะปรับสมดุลโหลดอัตโนมัติ.  
- **Optimize shard size:** shard ขนาดเล็กช่วยลด latency ของการค้นหา, ส่วน shard ขนาดใหญ่ลด overhead. ปรับตามฮาร์ดแวร์และรูปแบบการค้นหาของคุณ.  

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| โหนดไม่สามารถเชื่อมต่อ | ขัดแย้งพอร์ตหรือไฟร์วอลล์ | ตรวจสอบให้แน่ใจว่า `basePort` เปิดอยู่และไม่ได้ใช้โดยบริการอื่น |
| ดัชนีไม่อัปเดต | ไม่มีการสมัครรับเหตุการณ์ | เรียก `SearchNetworkNodeEvents.subscribe(masterNode)` หลังการปรับใช้ |
| ข้อผิดพลาด Out‑of‑memory | โหลด shard ขนาดใหญ่จำนวนมาก | ลดขนาด shard หรือเพิ่ม heap ของ JVM (`-Xmx` flag) |

## คำถามที่พบบ่อย

**Q: ฉันสามารถเพิ่มไดเรกทอรีใหม่หลังจากเครือข่ายทำงานแล้วหรือไม่?**  
A: ใช่—ใช้เมธอด `indexer.addDirectories()`; เหตุการณ์ที่สมัครรับจะกระจายการอัปเดตแบบเรียลไทม์  

**Q: ฉันจะตรวจสอบสุขภาพของโหนดได้อย่างไร?**  
A: แต่ละ `SearchNetworkNode` มี API สถานะ; ผสานรวมกับเครื่องมือมอนิเตอร์ที่คุณเลือกใช้  

**Q: สามารถรัน master node บนเครื่องแยกต่างหากได้หรือไม่?**  
A: แน่นอน เพียงตรวจสอบให้โหนดทั้งหมดใช้ `basePort` เดียวกันและสามารถเชื่อมต่อกันผ่านเครือข่ายได้  

**Q: รองรับรูปแบบไฟล์อะไรบ้าง?**  
A: GroupDocs.Search รองรับ PDFs, Word, Excel, PowerPoint, plain text และรูปแบบอื่น ๆ มากมายโดยอัตโนมัติ  

**Q: จำเป็นต้องรีสตาร์ทเครือข่ายหลังจากเพิ่มโหนดใหม่หรือไม่?**  
A: ไม่—โหนดสามารถเพิ่มหรือเอาออกได้แบบไดนามิก; master node จะปรับสมดุล shard โดยอัตโนมัติ  

## สรุป
ตอนนี้คุณรู้แล้วว่า **วิธีการกำหนดค่าการค้นหา** ด้วย GroupDocs.Search สำหรับ Java คุณสามารถสร้างโซลูชันการค้นหาเอกสารที่เร็ว, สามารถขยายได้, และเชื่อถือได้ ซึ่งสอดคล้องกับการเติบโตขององค์กรของคุณ นำรูปแบบเหล่านี้ไปใช้เพื่อสร้างประสบการณ์การค้นหาแบบเรียลไทม์และกระจายสำหรับทุกอุตสาหกรรม.

---

**อัปเดตล่าสุด:** 2026-05-02  
**ทดสอบด้วย:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs
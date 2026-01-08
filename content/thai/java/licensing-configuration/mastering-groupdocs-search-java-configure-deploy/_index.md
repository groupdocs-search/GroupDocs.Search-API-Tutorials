---
date: '2026-01-08'
description: เรียนรู้วิธีกำหนดค่าการค้นหาและเปิดใช้งานการอัปเดตการค้นหาแบบเรียลไทม์ด้วย
  GroupDocs.Search สำหรับ Java คู่มือแบบขั้นตอนต่อขั้นตอนเกี่ยวกับการตั้งค่าเครือข่าย
  การปรับใช้โหนด และการทำดัชนี
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'วิธีกำหนดค่าการค้นหาด้วย GroupDocs.Search ใน Java: คู่มือการกำหนดค่าและการปรับใช้'
type: docs
url: /th/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# วิธีกำหนดค่าการค้นหาด้วย GroupDocs.Search ใน Java

ในโลกดิจิทัลที่เคลื่อนที่อย่างรวดเร็วในทุกวันนี้ การ **กำหนดค่าการค้นหา** อย่างมีประสิทธิภาพสามารถทำให้โครงการประสบความสำเร็จหรือไม่สำเร็จได้ ไม่ว่าคุณจะต้องจัดการกับสัญญานับพัน, เอกสารวิจัย, หรือรายงานภายใน, เครือข่ายการค้นหาที่ออกแบบอย่างดีจะช่วยให้คุณค้นหาเอกสารที่ต้องการได้ในไม่กี่วินาที บทแนะนำนี้จะพาคุณผ่านการกำหนดค่าเครือข่ายการค้นหา, การปรับใช้โหนด, และการเปิดใช้งาน **การอัปเดตการค้นหาแบบเรียลไทม์** ด้วย GroupDocs.Search สำหรับ Java.

## คำตอบด่วน
- **วัตถุประสงค์หลักของเครือข่ายการค้นหาคืออะไร?** เพื่อกระจายการทำดัชนีและการประมวลผลคำค้นหาไปยังหลายโหนดเพื่อความสามารถในการขยายและความเร็ว.  
- **ต้องการเวอร์ชันของไลบรารีใด?** GroupDocs.Search for Java v25.4 หรือใหม่กว่า.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **การอัปเดตแบบเรียลไทม์จัดการอย่างไร?** โดยการสมัครรับเหตุการณ์ของโหนดที่เกิดขึ้นเมื่อมีการเปลี่ยนแปลงการทำดัชนี.  
- **ฉันสามารถเพิ่มโฟลเดอร์เอกสารใหม่ได้ในขณะทำงานหรือไม่?** ได้—ใช้เมธอด `addDirectories` ของ indexer.

## “การกำหนดค่าการค้นหา” คืออะไรในบริบทของ GroupDocs?
การกำหนดค่าการค้นหาหมายถึงการตั้งค่า **เครือข่ายการค้นหา** ที่ทราบตำแหน่งที่เอกสารของคุณอยู่, วิธีที่โหนดสื่อสารกัน, และวิธีการประสานงานการทำดัชนี เมื่อเครือข่ายถูกกำหนดค่าแล้ว, คุณสามารถเพิ่มหรือเอาโหนดออกได้โดยไม่มีการหยุดทำงาน, ทำให้เข้าถึงผลการค้นหาที่อัปเดตอยู่เสมอ.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
- **Scalability (ความสามารถในการขยาย):** กระจายภาระงานไปยังหลายเครื่อง.  
- **Real‑time updates (การอัปเดตแบบเรียลไทม์):** แสดงไฟล์ที่ทำดัชนีใหม่ทันทีทั่วเครือข่าย.  
- **Ease of integration (ความง่ายในการรวมระบบ):** การตั้งค่า Maven อย่างง่ายและ Java APIs ที่ชัดเจน.  
- **Enterprise‑ready (พร้อมใช้งานในระดับองค์กร):** จัดการกับคอร์ปัสขนาดใหญ่และสถานการณ์การค้นหาที่ซับซ้อน.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** ติดตั้งแล้ว.  
- **Maven** สำหรับการจัดการ dependencies.  
- ความคุ้นเคยพื้นฐานกับ Java, Maven, และแนวคิดการค้นหา.

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การกำหนดค่า Maven Dependency
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

### การรับไลเซนส์
- **Free Trial:** รับไลเซนส์ทดลองเพื่อสำรวจคุณสมบัติทั้งหมด.  
- **Temporary License:** ขอไลเซนส์ชั่วคราวสำหรับช่วงการประเมินที่ยาวนานขึ้น.  
- **Commercial License:** จำเป็นสำหรับการปรับใช้ในสภาพแวดล้อมการผลิต.

### การเริ่มต้นพื้นฐาน
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## วิธีกำหนดค่าเครือข่ายการค้นหาใน Java

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
- **Parameters (พารามิเตอร์):** `basePath` ชี้ไปยังโฟลเดอร์เอกสารของคุณ; `basePort` คือพอร์ต TCP ที่ใช้สำหรับการสื่อสารระหว่างโหนด.

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
- **Master Node (โหนดหลัก):** ประสานการค้นหาและการทำดัชนีทั่วทุกโหนด.

## การสมัครรับเหตุการณ์โหนดสำหรับการอัปเดตการค้นหาแบบเรียลไทม์

### ขั้นตอนที่ 1: นำเข้าแพ็กเกจเหตุการณ์
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### ขั้นตอนที่ 2: สมัครรับเหตุการณ์จากโหนดหลัก
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Event Handling (การจัดการเหตุการณ์):** เปิดใช้งาน **การอัปเดตการค้นหาแบบเรียลไทม์** ทุกครั้งที่มีการเพิ่ม, ปรับปรุง, หรือเอาเอกสารออก.

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
- **Dynamic Indexing (การทำดัชนีแบบไดนามิก):** เพิ่มโฟลเดอร์ได้ตามต้องการ; เครือข่ายจะทำดัชนีโดยอัตโนมัติ.

## การดึงเอกสารที่ทำดัชนีแล้ว

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
- **Shard Management (การจัดการชาร์ด):** จัดการชุดข้อมูลขนาดใหญ่อย่างมีประสิทธิภาพโดยการกระจายเอกสารไปยังชาร์ดต่าง ๆ.

## การประยุกต์ใช้งานจริง
1. **Enterprise Document Management (การจัดการเอกสารระดับองค์กร):** รวมศูนย์การค้นหาผ่านไฟล์หลายล้านไฟล์.  
2. **Legal Firms (สำนักงานกฎหมาย):** ค้นหาไฟล์คดี, สัญญา, และหลักฐานได้อย่างรวดเร็ว.  
3. **Academic Research (การวิจัยเชิงวิชาการ):** ทำดัชนีนิตยสารและเอกสารเพื่อการดึงข้อมูลทันที.

## พิจารณาด้านประสิทธิภาพ
- **Optimize Indexing (เพิ่มประสิทธิภาพการทำดัชนี):** กำหนดเวลาการรีเฟรชดัชนีเป็นประจำและลบข้อมูลที่ล้าสมัย.  
- **Memory Management (การจัดการหน่วยความจำ):** ตรวจสอบ heap ของ JVM โดยเฉพาะเมื่อจัดการชาร์ดขนาดใหญ่.  
- **Scalability Planning (การวางแผนขยายขนาด):** เพิ่มโหนดเมื่อคอร์ปัสของคุณเติบโต; เครือข่ายจะปรับสมดุลโหลดโดยอัตโนมัติ.

## ปัญหาทั่วไปและวิธีแก้

| Issue (ปัญหา) | Cause (สาเหตุ) | Fix (วิธีแก้) |
|-------|-------|-----|
| Nodes cannot connect | Port conflict or firewall | Ensure `basePort` is open and not used by other services |
| Index not updating | Event subscription missing | Call `SearchNetworkNodeEvents.subscribe(masterNode)` after deployment |
| Out‑of‑memory errors | Too many large shards loaded | Reduce shard size or increase JVM heap (`-Xmx` flag) |

## คำถามที่พบบ่อย

**Q: ฉันสามารถเพิ่มไดเรกทอรีใหม่หลังจากเครือข่ายทำงานแล้วได้หรือไม่?**  
A: ได้—ใช้เมธอด `indexer.addDirectories()`; เหตุการณ์ที่สมัครรับจะกระจายการอัปเดตแบบเรียลไทม์.

**Q: ฉันจะตรวจสอบสุขภาพของโหนดได้อย่างไร?**  
A: แต่ละ `SearchNetworkNode` มี API สถานะ; สามารถรวมเข้ากับเครื่องมือมอนิเตอร์ที่คุณเลือกใช้ได้.

**Q: สามารถรันโหนดหลักบนเครื่องแยกต่างหากได้หรือไม่?**  
A: ได้แน่นอน เพียงให้แน่ใจว่าโหนดทั้งหมดใช้ `basePort` เดียวกันและสามารถเชื่อมต่อกันผ่านเครือข่ายได้.

**Q: รองรับรูปแบบไฟล์อะไรบ้าง?**  
A: GroupDocs.Search รองรับ PDF, Word, Excel, PowerPoint, plain text และรูปแบบอื่น ๆ อีกหลายประเภทโดยไม่ต้องตั้งค่าเพิ่มเติม.

**Q: จำเป็นต้องรีสตาร์ทเครือข่ายหลังจากเพิ่มโหนดใหม่หรือไม่?**  
A: ไม่จำเป็น—โหนดสามารถเพิ่มหรือเอาออกได้แบบไดนามิก; โหนดหลักจะทำการปรับสมดุลชาร์ดโดยอัตโนมัติ.

## สรุป
คุณได้เข้าใจอย่างครบถ้วนและเป็นขั้นตอนเกี่ยวกับ **การกำหนดค่าการค้นหา** ด้วย GroupDocs.Search สำหรับ Java ตั้งแต่การตั้งค่าเริ่มต้นจนถึงการอัปเดตแบบเรียลไทม์และการทำดัชนีแบบกระจาย ใช้รูปแบบเหล่านี้เพื่อสร้างโซลูชันการค้นหาเอกสารที่เร็ว, ขยายได้, และเชื่อถือได้สำหรับทุกอุตสาหกรรม.

---

**Last Updated:** 2026-01-08  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs
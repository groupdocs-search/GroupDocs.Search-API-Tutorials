---
date: '2026-05-17'
description: เรียนรู้วิธีเพิ่มการพึ่งพา groupdocs Maven, ตั้งค่า Java search network,
  และเพิ่ม directories ไปยัง index เพื่อการ document retrieval ที่เร็วและสามารถขยายได้
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: วิธีเพิ่มการพึ่งพา GroupDocs Maven สำหรับ Search Network
type: docs
url: /th/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# วิธีเพิ่มการพึ่งพา Maven ของ GroupDocs สำหรับเครือข่ายการค้นหา

ในคู่มือฉบับครอบคลุมนี้คุณจะได้ค้นพบ **วิธีเพิ่มการพึ่งพา Maven ของ GroupDocs** การกำหนดค่าเครือข่ายการค้นหา Java ที่แข็งแกร่งด้วย GroupDocs.Search และการทำให้ชาร์ดของคุณซิงโครไนซ์ ไม่ว่าคุณจะทำการจัดทำดัชนีเอกสารกฎหมาย รายงานการเงิน หรืองานวิจัยทางวิชาการ ขั้นตอนต่อไปนี้จะช่วยคุณสร้างดัชนีที่ค้นหาได้ แจกจ่ายภาระการค้นหาข้ามโหนด และรักษาความสอดคล้องของข้อมูลด้วยความพยายามเพียงเล็กน้อย

## คำตอบสั้น
- **อะไรคือการพึ่งพา Maven ของ GroupDocs?** Maven artifact ที่บรรจุไลบรารี GroupDocs.Search สำหรับโครงการ Java  
- **ทำไมต้องใช้เครือข่ายการค้นหา?** มันกระจายการทำดัชนีและภาระการค้นหาข้ามหลายโหนด เพิ่มความเร็วและความน่าเชื่อถือ  
- **ฉันจะเพิ่มไดเรกทอรีเพื่อทำดัชนีอย่างไร?** ใช้ `IndexingDocuments.addDirectories` บนโหนดหลัก  
- **จะซิงโครไนซ์ชาร์ดอย่างไร?** เรียก `SynchronizeOptions` บน `Indexer` ของแต่ละโหนด  
- **ฉันต้องมีไลเซนส์หรือไม่?** ใช่ ต้องมีไลเซนส์ทดลองหรือเชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์

## GroupDocs Maven Dependency คืออะไร?

`GroupDocs Maven dependency` เป็น Maven artifact ที่บรรจุไลบรารี GroupDocs.Search สำหรับโครงการ Java  
มันให้คลาสที่จำเป็นทั้งหมดเพื่อสร้างดัชนีที่ค้นหาได้ จัดการโหนดเครือข่าย และดำเนินการค้นหาอย่างรวดเร็ว และ Maven จะดึง dependencies แบบทรานซิทีฟโดยอัตโนมัติ ทำให้คุณได้เครื่องมือค้นหาที่พร้อมใช้งานด้วยเพียงไม่กี่บรรทัดใน `pom.xml` ของคุณ

## วิธีเพิ่ม GroupDocs Maven Dependency

เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ แล้วรัน `mvn clean install`; Maven จะดาวน์โหลด JAR `groupdocs-search` และไลบรารีที่จำเป็น ทำให้ API พร้อมใช้งานในโปรเจกต์ของคุณ หลังจากการสร้างสำเร็จคุณสามารถเริ่มใช้คลาส `com.groupdocs.search` ได้ทันที

### การกำหนดค่า Maven

เพิ่ม repository และ dependency ลงใน `pom.xml` ของคุณ:

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

> **เคล็ดลับ:** คอยอัปเดตหมายเลขเวอร์ชันโดยตรวจสอบหน้าปล่อยเวอร์ชันอย่างเป็นทางการ

คุณยังสามารถดาวน์โหลด JAR โดยตรงจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

## ทำไมต้องใช้เครือข่ายการค้นหา?

เครือข่ายการค้นหาช่วยให้การขยายแนวนอนโดยการแบ่งดัชนีเป็นชาร์ดที่อยู่บนโหนดแยกต่างหาก GroupDocs.Search สามารถจัดการ **รูปแบบไฟล์กว่า 50** และประมวลผล **เอกสารหลายร้อยหน้า** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ให้การตอบสนองการค้นหาในระดับวินาทีแม้ว่าปริมาณข้อมูลจะเพิ่มขึ้น

## ข้อกำหนดเบื้องต้น

- **JDK** (เวอร์ชัน 11 หรือใหม่กว่า) ติดตั้งแล้ว  
- IDE เช่น IntelliJ IDEA หรือ Eclipse  
- ความรู้พื้นฐานของ Java, ความคุ้นเคยกับ Maven, และความเข้าใจเรื่องโหนดเครือข่าย  
- ไลเซนส์ GroupDocs.Search ที่ถูกต้อง (ทดลองฟรีหรือเชิงพาณิชย์)

## การเริ่มต้นและตั้งค่าพื้นฐาน

เริ่มต้นด้วยการสร้างไดเรกทอรีดัชนี:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

ขั้นตอนง่าย ๆ นี้เตรียมสภาพแวดล้อมสำหรับการกำหนดค่าเครือข่ายต่อไป

## คู่มือการใช้งาน

### ฟีเจอร์ 1: การกำหนดค่าเครือข่ายการค้นหา

#### ภาพรวม

การกำหนดค่าเครือข่ายการค้นหากำหนดเส้นทางไฟล์และพอร์ตที่โหนดจะใช้สื่อสารกัน

##### ตั้งค่าเส้นทางและพอร์ต

Configuration เป็นคลาสที่เก็บเส้นทางเครือข่าย, พอร์ต, และการตั้งค่าอื่น ๆ สำหรับคลัสเตอร์การค้นหา  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
อ็อบเจกต์ `configuration` ตอนนี้มีการตั้งค่าที่จำเป็นทั้งหมดสำหรับเครือข่ายการค้นหาของคุณ

### ฟีเจอร์ 2: การปรับใช้โหนดเครือข่ายการค้นหา

#### ภาพรวม

ปรับใช้โหนดเพื่อกระจายภาระงานข้ามเครือข่ายของคุณ โหนดหลักจะจัดการการดำเนินการและเหตุการณ์ต่าง ๆ

##### โค้ดการปรับใช้

SearchNetworkNode แสดงถึงโหนดในเครือข่ายการค้นหาที่สามารถทำหน้าที่เป็นโหนดหลักหรือโหนดทำงาน  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### ฟีเจอร์ 3: การสมัครรับเหตุการณ์โหนดเครือข่ายการค้นหา

#### ภาพรวม

การฟังเหตุการณ์ช่วยให้จัดการการเปลี่ยนแปลงหรืออัปเดตในเครือข่ายของคุณได้แบบไดนามิก

##### การทำงานของการสมัครรับ

SearchNetworkNodeEvents ให้ฮุคเหตุการณ์สำหรับวงจรชีวิตของโหนดและการทำดัชนี  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### ฟีเจอร์ 4: การเพิ่มไดเรกทอรีไปยังดัชนี

#### ภาพรวม

การเพิ่มไดเรกทอรีเป็นขั้นตอนหลักที่ทำให้เอกสารของคุณสามารถค้นหาได้

##### การเพิ่มเอกสาร

`IndexingDocuments.addDirectories` เพิ่มเส้นทางโฟลเดอร์ไปยังดัชนีเพื่อประมวลผล  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### ฟีเจอร์ 5: การซิงโครไนซ์ชาร์ดในโหนดเครือข่ายการค้นหา

#### ภาพรวม

การซิงโครไนซ์ทำให้ข้อมูลสอดคล้องกันทั่วทุกชาร์ด

##### โค้ดการซิงโครไนซ์

`SynchronizeOptions` กำหนดวิธีการซิงโครไนซ์ชาร์ดระหว่างโหนด  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### ฟีเจอร์ 6: การปิดโหนดเครือข่ายการค้นหา

#### ภาพรวม

การปิดโหนดอย่างถูกต้องจะปล่อยทรัพยากรและป้องกันการรั่วไหลของหน่วยความจำ

##### การปิดโหนด

`close()` ปล่อยทรัพยากรและปิดการทำงานของโหนดเครือข่ายการค้นหา  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## การประยุกต์ใช้งานจริง

1. **การจัดการเอกสารทางกฎหมาย** – ดึงไฟล์คดีและอ้างอิงได้อย่างรวดเร็ว  
2. **การบันทึกข้อมูลการเงิน** – เข้าถึงใบแจ้งหนี้และร่องรอยการตรวจสอบในไม่กี่วินาที  
3. **การวิจัยทางวิชาการ** – ค้นหาผ่านงานวิจัยหลายพันฉบับเพื่อหาการอ้างอิงที่เกี่ยวข้อง

## ข้อพิจารณาด้านประสิทธิภาพ

- **เพิ่มประสิทธิภาพคำค้น** – เขียนคำค้นให้กระชับเพื่อลดเวลาตอบสนอง  
- **การจัดการหน่วยความจำ** – ตรวจสอบการใช้ heap ของ JVM; พิจารณาการปรับแต่ง GC สำหรับดัชนีขนาดใหญ่  
- **กลยุทธ์การขยาย** – เพิ่มโหนดตามปริมาณข้อมูลและภาระการค้นหาอย่างสัดส่วน

## ปัญหาที่พบบ่อยและวิธีแก้ไข

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|----------|
| โหนดไม่สามารถเชื่อมต่อได้ | ขัดแย้งพอร์ต | เปลี่ยน `basePort` เป็นค่าที่ไม่ได้ใช้ |
| ดัชนีไม่อัปเดต | ไม่มีการสมัครรับเหตุการณ์ | ตรวจสอบให้แน่ใจว่าได้เรียก `SearchNetworkNodeEvents.subscribe(masterNode)` |
| ความหน่วงสูง | ชาร์ดไม่เพียงพอ | เพิ่มจำนวนโหนดและปรับสมดุลการกระจายเอกสาร |

## คำถามที่พบบ่อย

**Q: ประโยชน์หลักของการใช้ GroupDocs.Search คืออะไร?**  
A: มันให้ความสามารถในการค้นหาอย่างรวดเร็วและขยายได้บนชุดเอกสารขนาดใหญ่โดยต้องการการกำหนดค่าต่ำสุด

**Q: ฉันสามารถปรับแต่งการกำหนดค่าโหนดในเครือข่ายการค้นหาได้หรือไม่?**  
A: ได้ คุณสามารถตั้งค่าเส้นทาง, พอร์ต, และตัวเลือกอื่น ๆ ผ่านอ็อบเจกต์ `Configuration`

**Q: ฉันจะเพิ่มไดเรกทอรีไปยังดัชนีหลังจากเครือข่ายทำงานแล้วอย่างไร?**  
A: เรียก `IndexingDocuments.addDirectories(masterNode, "path")` ทุกครั้งที่ต้องทำดัชนีโฟลเดอร์ใหม่

**Q: จะซิงโครไนซ์ชาร์ดเมื่อโหนดใหม่เข้าร่วมเครือข่ายอย่างไร?**  
A: ใช้เมธอด `synchronizeShards` ที่แสดงด้านบนบนโหนดที่เพิ่มใหม่

**Q: ฉันต้องมีไลเซนส์สำหรับการพัฒนาหรือไม่?**  
A: ไลเซนส์ทดลองฟรีเพียงพอสำหรับการทดสอบ; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์

## สรุป

โดยทำตามคู่มือนี้คุณจะรู้วิธี **เพิ่มการพึ่งพา Maven ของ GroupDocs**, กำหนดค่าเครือข่ายการค้นหาหลายโหนด, ทำดัชนีไดเรกทอรี, และซิงโครไนซ์ชาร์ด ขั้นตอนเหล่านี้เป็นพื้นฐานสำหรับโซลูชันการค้นหาเอกสารที่มีประสิทธิภาพสูงและสามารถเติบโตตามความต้องการขององค์กรของคุณ

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [Tutorials and Examples of GroupDocs.Search for Java](/search/net/)  
- [Configuring GroupDocs.Search Network in .NET: A Comprehensive Guide](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)  
- [How to Implement a Search Network with GroupDocs.Search in .NET for Document Management Systems](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
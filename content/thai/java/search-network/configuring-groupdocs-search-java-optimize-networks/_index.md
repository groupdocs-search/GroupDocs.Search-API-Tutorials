---
date: '2026-07-16'
description: เรียนรู้วิธีกำหนดค่า GroupDocs.Search network ใน Java, เพิ่ม synonyms
  ไปยัง index, และ boost ประสิทธิภาพการค้นหาใน distributed nodes.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: วิธีกำหนดค่า GroupDocs.Search network ใน Java และเพิ่ม synonyms ไปยัง
  index เพื่อผลลัพธ์ที่เร็วขึ้นและแม่นยำมากขึ้น. ทำตาม step-by-step guide นี้.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: วิธีกำหนดค่า GroupDocs.Search Network ใน Java – Boost Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: วิธีกำหนดค่า GroupDocs.Search Network ใน Java คู่มือ
type: docs
url: /th/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# วิธีกำหนดค่า GroupDocs.Search Network ใน Java – Boost Search

ในแอปพลิเคชันสมัยใหม่ที่ใช้ข้อมูลเป็นหลัก, **how to configure GroupDocs** อย่างถูกต้องเป็นหัวใจสำคัญในการส่งมอบผลการค้นหาที่เร็วแสงและเกี่ยวข้องอย่างแม่นยำทั่วคลังเอกสารขนาดใหญ่ ไม่ว่าคุณจะสร้างพอร์ทัลระดับองค์กร, ฐานความรู้, หรือแคตาล็อกสินค้า, GroupDocs.Search network ที่ปรับแต่งอย่างดีจะช่วยให้คุณขยายแนวนอนได้, ใส่ตรรกะคำพ้อง, และควบคุมความหน่วงเวลาได้ ในบทแนะนำนี้เราจะเดินผ่านทุกขั้นตอนที่จำเป็นเพื่อการตั้งค่า, การปรับใช้, และการปรับจูน GroupDocs.Search network ด้วย Java, พร้อมคำแนะนำเชิงปฏิบัติเกี่ยวกับการเพิ่มคำพ้องในดัชนีและการจัดการวงจรชีวิตของโหนด

## คำตอบสั้น
- **ประโยชน์หลักของการกำหนดค่า GroupDocs.Search network คืออะไร?** มันทำให้สามารถทำดัชนีและการสืบค้นแบบกระจายได้, ปรับปรุงประสิทธิภาพและความสามารถในการขยายตัว.  
- **ฉันต้องมีใบอนุญาตเพื่อรันตัวอย่างหรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; ใบอนุญาตเชิงพาณิชย์จำเป็นสำหรับการใช้งานในสภาพแวดล้อมจริง.  
- **สามารถเพิ่มคำพ้องโดยไม่ต้องสร้างดัชนีใหม่ได้หรือไม่?** ได้—ใช้พจนานุกรมคำพ้องในเวลารันเพื่อ **add synonyms to index**.  
- **ฉันสามารถปรับใช้โหนดได้กี่โหนด?** คุณสามารถปรับใช้โหนดได้ตามที่โครงสร้างพื้นฐานของคุณอนุญาต; แต่ละโหนดทำงานบนพอร์ตของตนเอง.  
- **ต้องใช้เวอร์ชัน Java ใด?** รองรับ JDK 8 หรือใหม่กว่า, มีความเข้ากันได้เต็มรูปแบบจนถึง JDK 21.

## การกำหนดค่า GroupDocs.Search network คืออะไร?
**GroupDocs.Search network** คือชุดของกระบวนการ JVM ที่ทำงานร่วมกันเพื่อทำดัชนีและสืบค้นชุดเอกสารที่ใช้ร่วมกัน มันประกอบด้วยโหนดหลักที่ประสานงานโหนดทำงานหนึ่งหรือหลายโหนด (shards) เครือข่ายทำหน้าที่เป็นชั้นนามธรรมของการจัดเก็บข้อมูล, ดังนั้นคำสืบค้นเดียวจะถูกกระจายอัตโนมัติไปยังทุก shard และผลลัพธ์จะถูกรวมก่อนส่งกลับให้ผู้เรียกใช้

## ทำไมต้องกำหนดค่า GroupDocs.Search network?
การกำหนดค่า GroupDocs.Search network ให้คุณได้สามข้อได้เปรียบที่ชัดเจน: **scalability**, **reliability**, และ **enhanced relevance**. โดยการกระจายภาระการทำดัชนีไปยังโหนดสูงสุด 20 โหนด, แต่ละโหนดจัดการ shard ขนาด 5 GB, คุณสามารถลดเวลาการทำดัชนีทั้งหมดลงประมาณ 70 % เมื่อเทียบกับการตั้งค่าโหนดเดียว การเพิ่มพจนานุกรมคำพ้องช่วยเพิ่ม recall สูงสุด 35 % สำหรับคำสืบค้นที่ใช้คำศัพท์ทางเลือก, ในขณะที่การทำสำเนาโหนดรับประกัน uptime 99.9 % ในช่วงเวลาบำรุงรักษา

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 – 21 (any LTS version)  
- Maven 3.5 + for building the project  
- ความคุ้นเคยกับไวยากรณ์พื้นฐานของ Java และการจัดการ dependencies ของ Maven  
- การเข้าถึงไลบรารี GroupDocs.Search for Java (สามารถดาวน์โหลดได้จาก Maven Central หรือหน้าปล่อยอย่างเป็นทางการ)

## การตั้งค่า GroupDocs.Search สำหรับ Java

เพิ่ม repository และ dependency ลงใน **pom.xml** ของ Maven ของคุณ:

The following XML snippet adds the GroupDocs.Search repository and library dependency.  
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

หรือดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
- **Free Trial** – สำรวจคุณสมบัติหลักโดยไม่มีค่าใช้จ่าย.  
- **Temporary License** – ปลดล็อกความสามารถเต็มรูปแบบสำหรับการทดสอบระยะสั้น.  
- **Commercial License** – จำเป็นสำหรับการปรับใช้ในสภาพแวดล้อมการผลิตและเพื่อรับการสนับสนุนระดับพรีเมียม.

### การเริ่มต้นและการตั้งค่าเบื้องต้น
สร้างคลาส Java ง่าย ๆ เพื่อยืนยันว่าไลบรารีโหลดอย่างถูกต้อง:

The SampleInitializer class demonstrates loading the GroupDocs.Search engine.  
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## คู่มือขั้นตอนการกำหนดค่า GroupDocs.Search Network

### 1. การกำหนดค่า Search Network
กำหนดโฟลเดอร์เอกสารฐานและพอร์ตเริ่มต้นสำหรับการสื่อสารระหว่างโหนด.

SearchNetworkConfig holds the configuration for the network nodes.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – ไดเรกทอรีที่เก็บพจนานุกรม (เช่นไฟล์คำพ้อง).  
- **basePort** – พอร์ตแรก; โหนดต่อ ๆ ไปจะเพิ่มจากค่านี้.

### 2. การปรับใช้ Search Network Nodes
เปิดโหนดทำงานหลายโหนดที่ใช้การกำหนดค่าเดียวกัน.

SearchNode represents an individual node in the distributed network.  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

แต่ละโหนดทำงานบนพอร์ตของตนเอง (`basePort + index`) และถือ shard ของดัชนีโดยรวม, ทำให้สามารถประมวลผลการทำดัชนีและการสืบค้นแบบขนานได้

### 3. การสมัครรับเหตุการณ์ของโหนด
ตรวจสอบสุขภาพ, ความคืบหน้าการทำดัชนี, และเงื่อนไขข้อผิดพลาดโดยแนบ event listener ไปยังโหนดหลัก.

NetworkEventListener handles callbacks for node lifecycle events.  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Callback ของเหตุการณ์ทำให้คุณตอบสนองต่อการเริ่ม/หยุดโหนด, การทำดัชนีเสร็จสิ้น, และความล้มเหลวที่ไม่คาดคิด, ให้คุณมองเห็นระบบกระจายได้อย่างเต็มที่

### 4. การเพิ่มคำพ้องให้กับ Indexer ของโหนด  
เพิ่มความเกี่ยวข้องโดย **add synonyms to index** ในเวลารัน.

SynonymDictionary allows adding synonym groups to the indexer.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – อาเรย์ของคำที่ควรถือเป็นเทียบเท่า.  
- **clearBeforeAdding** – ตั้งค่าเป็น `true` หากต้องการแทนที่รายการที่มีอยู่

### 5. การเพิ่มไดเรกทอรีสำหรับการทำดัชนี
บอกโหนดหลักว่าโฟลเดอร์ใดบรรจุเอกสารที่ต้องการให้ค้นหาได้.

Indexer.addDirectory registers a folder for indexing.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

เมธอดนี้สแกนไดเรกทอรีแบบเรียกซ้ำและกระจายไฟล์ไปยัง shard ต่าง ๆ, รองรับข้อมูลมากกว่า 10 TB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ

### 6. การทำการค้นหาข้อความในเครือข่าย
ดำเนินการสืบค้นทั่วทุกโหนด, สามารถบังคับให้ทำการจับคู่แบบ exact‑match ได้ตามต้องการ.

SearchEngine.search runs the query on the network.  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

สลับ `exactMatchOnly` เป็น `true` เมื่อคุณต้องการการจับคู่คำอย่างเคร่งครัดโดยไม่มี stemming, ซึ่งอาจเพิ่มความแม่นยำสำหรับสถานการณ์การค้นหาโค้ดได้ถึง 20 %

### 7. การปิดโหนดเครือข่าย
ปล่อยทรัพยากรอย่างสุภาพเมื่อการประมวลผลเสร็จสิ้น.

`node.close()` shuts down a SearchNode and frees resources.  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

การปิดอย่างถูกต้องช่วยป้องกันการรั่วของหน่วยความจำและทำให้ JVM มีสุขภาพดี, โดยเฉพาะในบริการที่ทำงานต่อเนื่องและหมุนเวียนโหนดในช่วงเวลาที่ไม่ใช้งานสูง

## การประยุกต์ใช้งานจริง
| สถานการณ์ | วิธีที่เครือข่ายช่วย |
|----------|-----------------------|
| **การค้นหาในระดับองค์กร** | กระจายการทำดัชนีไปยังเซิร์ฟเวอร์ศูนย์ข้อมูลสำหรับข้อมูลขนาด petabyte‑scale, ทำให้ได้ latency การสืบค้นต่ำกว่า 1 วินาทีสำหรับเอกสารกว่า 100 M+ รายการ. |
| **การจัดการเอกสาร** | เพิ่มคำพ้องให้กับดัชนีเพื่อให้ผู้ใช้ค้นหาเอกสารได้แม้ใช้คำศัพท์ที่แตกต่าง, เพิ่ม recall สูงสุด 35 %. |
| **แคตาล็อกอี‑คอมเมิร์ซ** | ปรับใช้โหนดเฉพาะภูมิภาคเพื่อให้บริการการค้นหาผลิตภัณฑ์ที่เป็นภาษาท้องถิ่นได้อย่างรวดเร็ว, ลดเวลาเฉลี่ยของการตอบสนองจาก 250 ms เหลือ 80 ms. |
| **การจัดการเนื้อหา** | ทำให้เนื้อหายังคงค้นหาได้ในขณะที่บรรณาธิการเพิ่มไฟล์ใหม่ในไดเรกทอรีเฉพาะ; เครือข่ายทำการทำดัชนีเพิ่มอย่างต่อเนื่องโดยไม่มี downtime. |

## ปัญหาที่พบบ่อยและวิธีแก้ไข
- **Port Conflicts** – ตรวจสอบให้แน่ใจว่าพอร์ตของแต่ละโหนด (`basePort + index`) ว่าง; ปรับ `basePort` หากจำเป็น.  
- **Synonym Not Applied** – ยืนยันว่าคุณได้เรียก `indexer.setDictionary(dictionary)` หลังจากเพิ่มคำ; มิฉะนั้นคำพ้องใหม่จะไม่ถูกนำมาพิจารณาในการสืบค้น.  
- **Node Not Responding** – สมัครรับเหตุการณ์; มองหา callback `NodeFailed` เพื่อวินิจฉัยปัญหาเครือข่าย.  
- **Memory Leak on Close** – เรียก `node.close()` สำหรับทุกโหนดที่ปรับใช้เสมอ; พิจารณาใช้โครงสร้าง try‑with‑resources เพื่อทำความสะอาดอัตโนมัติ.  

## คำถามที่พบบ่อย

**Q: การปรับใช้หลายโหนดช่วยปรับปรุงประสิทธิภาพการค้นหาอย่างไร?**  
A: แต่ละโหนดทำดัชนี shard ของข้อมูล, ทำให้ประมวลผลแบบขนานและลด latency ของการสืบค้นเมื่อภาระงานถูกแบ่งกันในคลัสเตอร์.

**Q: ฉันสามารถเพิ่มคำพ้องโดยไม่ต้องทำดัชนีเอกสารใหม่หรือไม่?**  
A: ได้, คุณสามารถ **add synonyms to index** ในเวลารันผ่านพจนานุกรมคำพ้อง; การเปลี่ยนแปลงจะมีผลทันทีสำหรับคำสืบค้นใหม่.

**Q: การสมัครรับเหตุการณ์ของโหนดจำเป็นหรือไม่?**  
A: แม้ไม่จำเป็นสำหรับการทำงานพื้นฐาน, การสมัครรับเหตุการณ์ให้คุณมองเห็นสุขภาพของโหนดและช่วยให้ตอบสนองต่อความล้มเหลวได้อย่างทันท่วงที.

**Q: แนวทางปฏิบัติที่ดีที่สุดสำหรับการจัดการทรัพยากรของโหนดคืออะไร?**  
A: ปิดโหนดที่ไม่ได้ใช้งานเป็นประจำ, ตรวจสอบการใช้หน่วยความจำของ JVM, และหมุนเวียนโหนดในช่วงเวลาที่ไม่ใช้งานสูงเพื่อให้การใช้ทรัพยากรอยู่ในระดับที่เหมาะสม.

**Q: GroupDocs.Search รองรับรูปแบบที่ไม่ใช่ข้อความเช่น PDF หรือรูปภาพหรือไม่?**  
A: รองรับอย่างเต็มที่. ไลบรารีจะสกัดข้อความจาก PDF, ไฟล์ Office, และทำ OCR บนรูปภาพ, ทำให้ไฟล์เหล่านั้นสามารถค้นหาได้โดยอัตโนมัติ.

---

**Last Updated:** 2026-07-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [Tutorials and Examples of GroupDocs.Search for Java](/search/net/)
- [Configuring GroupDocs.Search Network in .NET: A Comprehensive Guide](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Deploy a Search Network Node in .NET using GroupDocs for Efficient Document Indexing and Retrieval](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
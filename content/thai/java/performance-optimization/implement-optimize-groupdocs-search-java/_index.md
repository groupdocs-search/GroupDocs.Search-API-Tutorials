---
date: '2026-01-16'
description: เรียนรู้วิธีการทำการค้นหาข้อความและเพิ่มประสิทธิภาพการค้นหาโดยใช้ GroupDocs.Search
  สำหรับ Java รวมถึงขั้นตอนการตั้งค่าเครือข่ายการค้นหา การสร้างดัชนีที่สามารถค้นหาได้
  และการลบดัชนีเอกสาร
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: ดำเนินการค้นหาข้อความด้วย GroupDocs.Search สำหรับ Java
type: docs
url: /th/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Perform Text Search with GroupDocs.Search for Java
## Performance Optimization
## How to Implement and Optimize a Search Network with GroupDocs.Search for Java

### Introduction
ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน ความสามารถในการ **perform text search** อย่างรวดเร็วในคอลเลกชันเอกสารขนาดมหาศาลเป็นข้อได้เปรียบในการแข่งขัน ไม่ว่าคุณจะสร้างฐานความรู้ภายใน, คลังข้อมูลคดีกฎหมาย, หรือแคตาล็อกสินค้าสำหรับอี‑คอมเมิร์ซ เครือข่ายการค้นหาที่ปรับแต่งอย่างดีสามารถปรับปรุงความพึงพอใจของผู้ใช้ได้อย่างมาก ในคู่มือนี้คุณจะได้เรียนรู้วิธี **set up search network**, **create searchable index**, **optimize search performance**, และแม้กระทั่ง **delete documents index** เมื่อจำเป็น—ทั้งหมดโดยใช้ GroupDocs.Search สำหรับ Java.

**What You'll Learn**
- Configuring a search network with GroupDocs.Search  
- Deploying nodes within the network  
- Indexing documents efficiently (`index documents java`)  
- Performing text searches across your network (`perform text search`)  
- Deleting specific documents from the index (`delete documents index`)  

มาดำดิ่งเข้าไปว่าคุณสามารถใช้คุณลักษณะเหล่านี้เพื่อสร้างประสบการณ์การค้นหาที่เพิ่มประสิทธิภาพได้อย่างไร

## Quick Answers
- **What is the main purpose of GroupDocs.Search for Java?** It provides full‑text search across many document formats.  
- **How do I perform text search in a distributed environment?** Deploy a search network, index documents on a master node, then query any node.  
- **Can I delete documents from the index without rebuilding it?** Yes, use the Delete API to remove selected files.  
- **What Java version is required?** JDK 8 or higher.  
- **Is a license needed for production?** A valid GroupDocs.Search license is required; a free trial is available.

## What is “perform text search”?
การทำการค้นหาข้อความหมายถึงการสอบถามดัชนีข้อความเต็มเพื่อดึงเอกสารที่มีคีย์เวิร์ดหรือวลีที่ระบุ GroupDocs.Search สร้างดัชนีแบบย้อนกลับซึ่งทำให้การค้นหาเหล่านี้เร็วมาก แม้จะมีไฟล์หลายพันไฟล์

## Why set up a search network?
เครือข่ายการค้นหาจะแบ่งการทำดัชนีและภาระการสอบถามไปยังหลายโหนด ทำให้คุณสามารถ **optimize search performance**, ขยายแนวนอน, และรักษาความพร้อมใช้งานสูง สถาปัตยกรรมนี้เหมาะสำหรับคลังเอกสารระดับองค์กรที่ความหน่วงและอัตราการผ่านข้อมูลเป็นสิ่งสำคัญ

### Prerequisites
- **Required Libraries:** GroupDocs.Search for Java version 25.4 (latest).  
- **Environment:** Java JDK 8+, Maven.  
- **Knowledge:** ความรู้พื้นฐานการเขียนโปรแกรม Java และความคุ้นเคยกับแนวคิดเครือข่าย

### Setting Up GroupDocs.Search for Java
เพื่อเริ่มต้น, ผสานรวม GroupDocs.Search เข้ากับโครงการ Java ของคุณโดยใช้การตั้งค่าดังต่อไปนี้:

#### Maven Setup
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

#### Direct Download
Alternatively, you can [download the latest version directly from GroupDocs](https://releases.groupdocs.com/search/java/).

#### License Acquisition
GroupDocs มีการทดลองใช้ฟรี ซึ่งช่วยให้คุณประเมินคุณลักษณะก่อนการซื้อ คุณสามารถรับใบอนุญาตชั่วคราวโดยทำตามขั้นตอนใน [purchase page](https://purchase.groupdocs.com/temporary-license/) ของพวกเขา สิ่งนี้จะเปิดใช้งานฟังก์ชันเต็มในช่วงการทดสอบของคุณ.

#### Basic Initialization and Setup
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

### Implementation Guide

#### Configuring the Search Network
**Overview:** สร้าง base path และ port สำหรับเครือข่ายการค้นหาของคุณ เพื่อให้โหนดสื่อสารได้อย่างมีประสิทธิภาพ.

##### Step 1: Define Base Configuration
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath`: เส้นทางไดเรกทอรีสำหรับการดำเนินการเครือข่าย.  
  - `basePort`: หมายเลขพอร์ตที่ใช้โดยเครือข่ายการค้นหา.

##### Step 2: Troubleshooting
ตรวจสอบให้แน่ใจว่าพอร์ตที่ระบุไม่ได้ถูกบล็อกโดยการตั้งค่าไฟร์วอลล์หรือใช้งานโดยแอปพลิเคชันอื่น ปรับเปลี่ยนตามความจำเป็นเพื่อหลีกเลี่ยงความขัดแย้ง.

#### Deploying Search Network Nodes
**Overview:** Using your configuration, deploy nodes across your network for distributed indexing and searching.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port:** ค่าต่าง ๆ นี้ควรตรงกับที่ใช้ในการกำหนดค่าเริ่มต้นเพื่อความสอดคล้อง.

#### Indexing Documents (`create searchable index`)
**Overview:** Add documents to the search index efficiently using a master node.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode`: โหนดหลักที่จัดการการทำดัชนีเอกสาร.  
  - `documentsPath`: เส้นทางไปยังไดเรกทอรีที่มีเอกสาร.

##### Troubleshooting Tips
ตรวจสอบว่าเส้นทางเอกสารของคุณถูกต้องและเข้าถึงได้ ตรวจสอบสิทธิ์ให้อนุญาตการอ่านจากไดเรกทอรีเหล่านี้.

#### Searching Text in Network (`perform text search`)
**Overview:** Perform comprehensive text searches across your indexed network.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query`: ข้อความที่คุณกำลังค้นหา.  
  - `masterNode`: โหนดที่ทำการค้นหา.

#### Deleting Documents from Index (`delete documents index`)
**Overview:** Remove specific documents from your index using their file paths.

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

##### Troubleshooting
ตรวจสอบว่าเส้นทางไฟล์แม่นยำและไฟล์มีอยู่ในไดเรกทอรีของคุณ หากปัญหายังคงอยู่ ให้ตรวจสอบสิทธิ์เครือข่ายและการเชื่อมต่อ.

### Practical Applications
1. **Enterprise Document Management:** ปรับปรุงการดึงข้อมูลความรู้ภายใน.  
2. **Legal Case Analysis:** ค้นหาไฟล์คดีที่เกี่ยวข้องอย่างรวดเร็วในหลายคลังข้อมูล.  
3. **E‑commerce Platforms:** เพิ่มความเร็วการค้นหาผลิตภัณฑ์โดยทำดัชนีคำอธิบายและรีวิว.  
4. **Academic Research:** ค้นหาห้องสมุดดิจิทัลขนาดใหญ่ของเอกสารและวิทยานิพนธ์อย่างมีประสิทธิภาพ.  
5. **Customer Support Systems:** ลดเวลาตอบสนองโดยให้เจ้าหน้าที่ค้นหาตั๋วเก่าได้ทันที.

### Performance Considerations
- **Optimize Indexing Speed:** เพิ่มเอกสารใหม่อย่างต่อเนื่องในช่วงเวลาที่ไม่มีการใช้งานหนักเพื่อรักษาความหน่วงต่ำ.  
- **Resource Usage Guidelines:** ตรวจสอบการใช้ CPU และหน่วยความจำ โดยเฉพาะเมื่อขยายจำนวนโหนด.  
- **Java Memory Management:** ปรับตั้งค่า heap ของ JVM ตามภาระงานของคุณ (เช่น `-Xmx2g` สำหรับดัชนีขนาดกลาง).

### Conclusion
โดยทำตามคู่มือนี้คุณได้เรียนรู้วิธี **set up search network**, **create searchable index**, **perform text search**, และ **delete documents index** ด้วยการใช้ GroupDocs.Search สำหรับ Java ความสามารถเหล่านี้ทำให้การดึงเอกสารที่เร็วและเชื่อถือได้ในสภาพแวดล้อมแบบกระจาย

**Next Steps**
- ทดลองใช้การกำหนดค่าโหนดต่าง ๆ เพื่อค้นหาความสมดุลที่เหมาะสมที่สุดสำหรับภาระงานของคุณ.  
- ศึกษาเพิ่มเติมเกี่ยวกับตัวเลือกการทำดัชนีขั้นสูง เช่น ตัววิเคราะห์แบบกำหนดเองและการปรับความเกี่ยวข้อง.  
- สำรวจการบูรณาการกับผลิตภัณฑ์ GroupDocs อื่น ๆ เพื่อการประมวลผลเอกสารแบบครบวงจร.

## Frequently Asked Questions

**Q: What is the primary use case for GroupDocs.Search for Java?**  
A: มันให้การค้นหาข้อความเต็มรูปแบบในหลายรูปแบบเอกสาร ทำให้คุณสามารถ **perform text search** ในคลังข้อมูลขนาดใหญ่ได้.

**Q: How can I improve search speed in a large network?**  
A: ปรับใช้โหนดเพิ่มเติม, ปรับจูน heap ของ JVM, และกำหนดเวลาการทำดัชนีในช่วงที่มีการใช้งานน้อยเพื่อ **optimize search performance**.

**Q: Is it possible to delete a single document without re‑indexing the whole collection?**  
A: ได้, ใช้ API **delete documents index** ตามตัวอย่างโค้ดเพื่อเอาไฟล์เฉพาะออก.

**Q: Do I need a license for development?**  
A: ใบอนุญาตทดลองใช้ฟรีเพียงพอสำหรับการทดสอบ; ต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.

**Q: Can I index PDFs, Word files, and emails together?**  
A: แน่นอน—GroupDocs.Search รองรับรูปแบบไฟล์หลากหลายตั้งแต่แรก.

---

**อัปเดตล่าสุด:** 2026-01-16  
**ทดสอบกับ:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs
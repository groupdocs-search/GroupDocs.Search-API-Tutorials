---
date: '2026-09-27'
description: เรียนรู้วิธีการใช้งานการค้นหาแบบเต็มข้อความ java ด้วย GroupDocs.Search
  for Java, เพิ่มไฟล์เพื่อค้นหา, กำหนดค่าไดเรกทอรี, และเปิดใช้งานการทำดัชนีแบบเรียลไทม์
keywords:
- java full text search
- event driven indexing
- java search engine
- add files to search
- real time indexing java
lastmod: '2026-09-27'
og_description: ใช้งานการค้นหาแบบเต็มข้อความ java ด้วย GroupDocs.Search. เรียนรู้การเพิ่มไฟล์,
  กำหนดค่า nodes, และเปิดใช้งานการทำดัชนีแบบเรียลไทม์ภายในไม่กี่นาที.
og_image_alt: Guide to setting up java full text search with GroupDocs.Search
og_title: วิธีการใช้งานการค้นหาแบบเต็มข้อความ java ด้วย GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to implement java full text search using GroupDocs.Search
    for Java, add files to search, configure directories, and enable real time indexing.
  headline: How to implement java full text search with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: Yes. The library works with any Java runtime, and you can point `basePath`
      to a network‑mounted folder or a cloud storage mount.
    question: Can I use GroupDocs.Search on a cloud‑based Java application?
  - answer: Subscribe to node events (see Feature 3) and call `addFiles` or `addDirectories`
      again for the modified paths.
    question: How do I update the index when a file changes?
  - answer: Practically, the limit is defined by your hardware and network bandwidth.
      The API imposes no hard cap.
    question: Is there a limit to the number of nodes I can deploy?
  - answer: No. Adding files triggers indexing automatically; you only need to commit
      if you defer the operation.
    question: Do I need to restart nodes after adding new files?
  - answer: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, and many image types—over
      50 formats in total.
    question: Which document formats are supported out of the box?
  type: FAQPage
tags:
- java full text search
- GroupDocs.Search
- search indexing
title: วิธีการใช้งานการค้นหาแบบเต็มข้อความ java ด้วย GroupDocs.Search
type: docs
url: /th/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# วิธีการใช้งานการค้นหาข้อความเต็มใน Java ด้วย GroupDocs.Search

ในยุคของแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูล **java full text search** มีความสำคัญต่อการเปลี่ยนคอลเลกชันเอกสารขนาดมหาศาลให้กลายเป็นฐานความรู้ที่สามารถค้นหาได้ทันที ไม่ว่าคุณจะสร้างพอร์ทัลระดับองค์กรหรือยูทิลิตี้เดสก์ท็อปแบบเบา ๆ เครือข่ายการค้นหาที่กำหนดค่าอย่างดีสามารถลดระยะเวลาการตอบสนองจากวินาทีเป็นมิลลิวินาทีและทำให้ผลลัพธ์ยังคงเกี่ยวข้องเมื่อข้อมูลเพิ่มขึ้น คำแนะนำนี้จะพาคุณผ่านการปรับใช้ **GroupDocs.Search for Java**, การเพิ่มไฟล์เพื่อค้นหา, การกำหนดค่าไดเรกทอรีบนโหนด, และการเปิดใช้งานการทำดัชนีแบบเรียลไทม์เพื่อให้ดัชนีของคุณสดใหม่โดยไม่ต้องแทรกแซงด้วยมือ

> **ทำไมเรื่องนี้ถึงสำคัญ:** ดัชนีการค้นหาข้อความเต็มใน Java ลดระยะเวลาการตอบสนอง, สามารถขยายตามปริมาณข้อมูล, และนำความสามารถเต็มรูปแบบของการค้นหาข้อความมาสู่โซลูชันที่ใช้ Java — พอร์ทัลเว็บ, แอปเดสก์ท็อป, หรือไมโครเซอร์วิสบนคลาวด์

## คำตอบอย่างรวดเร็ว
- **วัตถุประสงค์หลักของ GroupDocs.Search คืออะไร?** มันให้เครื่องมือค้นหา java ที่สามารถขยายได้, ทำการสร้างดัชนีและค้นหาเอกสารทั่วเครือข่ายแบบกระจาย  
- **ควรใช้เวอร์ชันใด?** แนะนำให้ใช้รุ่นเสถียรล่าสุด (เช่น 25.4) สำหรับโครงการใหม่  
- **ต้องการไลเซนส์หรือไม่?** มีการทดลองใช้งานฟรี 30 วัน; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต  
- **สามารถเพิ่มไฟล์และไดเรกทอรีทั้งหมดได้หรือไม่?** ได้ – ใช้ตัวช่วย `addFiles` และ `addDirectories` เพื่อดึงข้อมูลเข้า  
- **ต้องการ Java เวอร์ชันใด?** Java 8 หรือสูงกว่า, พร้อม Maven สำหรับการจัดการ dependencies  
- **การทำดัชนีแบบเรียลไทม์ใน java ทำงานอย่างไร?** โดยการสมัครรับเหตุการณ์ของโหนดคุณสามารถกระตุ้นการทำดัชนีอัตโนมัติเมื่อไฟล์มีการเปลี่ยนแปลง  

## “สร้างดัชนีที่ค้นหาได้ใน Java” คืออะไร?
การสร้างดัชนีที่ค้นหาได้ใน Java หมายถึงการสร้างโครงสร้างข้อมูลที่แมพคำค้นหาไปยังเอกสารที่มีคำนั้นอยู่, ทำให้สามารถทำการค้นหาเต็มข้อความได้อย่างรวดเร็ว **GroupDocs.Search for Java** จะดูแลการทำงานหนักเหล่านั้น, ให้คุณมุ่งเน้นที่การป้อนเอกสารและปรับแต่งพฤติกรรมการค้นหา

## ทำไมต้องใช้ GroupDocs.Search for Java?
GroupDocs.Search มอบเครื่องมือค้นหา java ที่สามารถขยายแนวนอนได้, รองรับรูปแบบไฟล์เข้าและออกกว่า 50 ประเภท, และมีการทำดัชนีแบบอีเวนต์‑ดริเวน การปรับใช้หลายโหนดช่วยกระจายภาระการทำดัชนี, ในขณะที่การตรวจสอบสุขภาพในตัวทำให้เครือข่ายเชื่อถือได้ นอกจากนี้ยังมี RESTful APIs และตัววิเคราะห์ที่ปรับแต่งได้สำหรับการปรับความเกี่ยวข้องอย่างละเอียด

## ข้อกำหนดเบื้องต้น
- **JDK 8+** ติดตั้งบนเครื่องพัฒนา  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**  
- ความรู้พื้นฐานของ **Java** และ **Maven**  
- การเข้าถึงไลบรารี **GroupDocs.Search for Java** (ดาวน์โหลดหรือใช้ Maven)

## การตั้งค่า GroupDocs.Search for Java

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

> **เคล็ดลับ:** ตรวจสอบหน้า releases อย่างเป็นทางการเพื่อให้เวอร์ชันเป็นปัจจุบันเสมอ

คุณยังสามารถดาวน์โหลด JAR โดยตรงจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การจัดหาไลเซนส์
- **ทดลองใช้ฟรี:** การประเมินผล 30 วัน  
- **ไลเซนส์ชั่วคราว:** ขอสำหรับการทดสอบระยะยาว  
- **การซื้อ:** จำเป็นสำหรับการปรับใช้ในสภาพแวดล้อมการผลิต

### การเริ่มต้นพื้นฐาน
สร้างอ็อบเจ็กต์การกำหนดค่าที่ชี้ไปยังโฟลเดอร์ที่ไฟล์ดัชนีจะถูกจัดเก็บและกำหนดพอร์ตสื่อสารฐาน:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## วิธีสร้างดัชนีที่ค้นหาได้ใน Java ด้วย GroupDocs.Search?
โหลดอ็อบเจ็กต์ `SearchConfiguration`, เริ่ม `SearchNetworkNode`, และเรียก `node.getIndexer().addFiles(...)` เพื่อเติมดัชนี รูปแบบบรรทัดเดียวนี้จะเปิดเครือข่ายการค้นหาข้อความเต็มใน java ที่ทำงานเต็มรูปแบบ, พร้อมรับคำค้นทันที คุณสามารถขยายโดยเพิ่มโหนดเพิ่มเติมที่ใช้เส้นทางฐานและช่วงพอร์ตเดียวกัน

### ฟีเจอร์ 1 – การกำหนดค่าและตั้งค่าเครือข่าย
คลาส `SearchConfiguration` เก็บการตั้งค่าทั้งหมดที่จำเป็นสำหรับการสตาร์ทโหนด

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – ไดเรกทอรีที่ข้อมูลดัชนีจะถูกบันทึก  
- **`basePort`** – พอร์ตเริ่มต้น; โหนดแต่ละตัวจะเพิ่มจากค่านี้

### ฟีเจอร์ 2 – การปรับใช้โหนดเครือข่ายการค้นหา
`SearchNetworkNode` แทนบริการทำดัชนีแต่ละตัวที่สามารถรันบนเครื่องใดก็ได้

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

`SearchNetworkNode` เป็นคอมโพเนนต์รันไทม์หลักที่โฮสต์ดัชนี, ประมวลเหตุการณ์เพิ่ม/ลบ, และตอบสนองต่อคำค้น การปรับใช้หลายโหนดทำให้คุณ **สร้างการค้นหาข้อความเต็มใน java** เป็นคลัสเตอร์ที่ขยายแนวนอนได้

### ฟีเจอร์ 3 – การสมัครรับเหตุการณ์ของโหนด
การอัปเดตแบบเรียลไทม์ทำให้ดัชนีสอดคล้องกับการเปลี่ยนแปลงของระบบไฟล์

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

โดยการฟังเหตุการณ์, คุณสามารถกระตุ้นการทำดัชนีใหม่อัตโนมัติเมื่อไฟล์ใหม่เข้ามา, ทำให้ได้ **การทำดัชนีแบบอีเวนต์‑ดริเวน** โดยไม่ต้องใช้สคริปต์มือ

### ฟีเจอร์ 4 – การเพิ่มไดเรกทอรีไปยังโหนดเครือข่าย
ใช้ตัวช่วยนี้เพื่อ **เพิ่มไดเรกทอรีไปยังโหนด**, รวบรวมเอกสารที่รองรับทั้งหมดแบบเรียกซ้ำ

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

เมธอด `DirectoryAdder.addDirectories(node, path)` จะเดินทางผ่านโครงสร้างโฟลเดอร์และเรียก `addFiles` สำหรับไฟล์ที่รองรับแต่ละไฟล์, ทำให้การนำเข้าจำนวนมากง่ายขึ้น

### ฟีเจอร์ 5 – การเพิ่มไฟล์ไปยังโหนดเครือข่าย
เมื่อคุณต้องการควบคุมอย่างละเอียด, **เพิ่มไฟล์ไปยังการค้นหา** ทีละไฟล์:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

`addFiles` เป็นเมธอดที่รับรายการเส้นทางไฟล์หรือสตรีม, ทำให้คุณสามารถทำดัชนีเอกสารจากคลาวด์สตอเรจ, แคชชั่วคราว, หรือสตรีมในหน่วยความจำได้

## กรณีการใช้งานทั่วไป
- **พอร์ทัลเอกสารระดับองค์กร** ที่ต้องการการค้นหาแบบทันทีในหลายพันไฟล์ PDF และ Office  
- **แพลตฟอร์ม e‑discovery ทางกฎหมาย** ที่หลักฐานใหม่ถูกเพิ่มอย่างต่อเนื่องและต้องค้นหาได้แบบเรียลไทม์  
- **ระบบจัดการเนื้อหา** ที่เก็บรูปภาพ, งานนำเสนอ, และสเปรดชีต พร้อมต้องการการค้นหาเต็มข้อความ

## ปัญหาทั่วไป & วิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|-----|
| **ไม่มีเอกสารปรากฏในผลการค้นหา** | ดัชนียังไม่ได้คอมมิท | เรียก `node.getIndexer().commit()` หลังจากเพิ่มไฟล์ |
| **ข้อผิดพลาดพอร์ตซ้ำกัน** | บริการอื่นใช้ `basePort` | เลือก `basePort` อื่นหรือยืนยันพอร์ตว่าง |
| **รูปแบบไฟล์ไม่รองรับ** | ไลบรารีไม่มี parser | ตรวจสอบให้แน่ใจว่าส่วนขยายไฟล์รองรับหรือเพิ่มตัวแยกข้อมูลแบบกำหนดเอง |

## เคล็ดลับการแก้ไขปัญหา
- **ตรวจสอบสุขภาพโหนด:** ใช้ endpoint ตรวจสอบสุขภาพในตัว (`http://localhost:{port}/health`) เพื่อยืนยันว่าโหนดแต่ละตัวทำงานอยู่  
- **ตรวจสอบการใช้หน่วยความจำ:** ชุดเอกสารขนาดใหญ่สามารถทำให้หน่วยความจำพุ่งสูง; ทำดัชนีเป็นชิ้นเล็กและเรียก `commit()` อย่างสม่ำเสมอ  
- **ตรวจสอบบันทึก:** GroupDocs.Search จะเขียนบันทึกรายละเอียดลงในโฟลเดอร์ `basePath` — ตรวจสอบเพื่อหาข้อผิดพลาดการแปลงหรือการหมดเวลาเครือข่าย

## คำถามที่พบบ่อย

**Q: สามารถใช้ GroupDocs.Search บนแอปพลิเคชัน Java ที่ทำงานบนคลาวด์ได้หรือไม่?**  
A: ได้. ไลบรารีทำงานกับ runtime ของ Java ใดก็ได้, และคุณสามารถชี้ `basePath` ไปยังโฟลเดอร์ที่เมานท์บนเครือข่ายหรือที่เก็บข้อมูลบนคลาวด์ได้

**Q: จะอัปเดตดัชนีเมื่อไฟล์มีการเปลี่ยนแปลงอย่างไร?**  
A: สมัครรับเหตุการณ์ของโหนด (ดูฟีเจอร์ 3) และเรียก `addFiles` หรือ `addDirectories` อีกครั้งสำหรับเส้นทางที่แก้ไข

**Q: มีขีดจำกัดจำนวนโหนดที่สามารถปรับใช้ได้หรือไม่?**  
A: โดยปฏิบัติ ขีดจำกัดขึ้นอยู่กับฮาร์ดแวร์และแบนด์วิดท์ของเครือข่าย. API ไม่ได้กำหนดขีดจำกัดคงที่

**Q: จำเป็นต้องรีสตาร์ทโหนดหลังจากเพิ่มไฟล์ใหม่หรือไม่?**  
A: ไม่จำเป็น. การเพิ่มไฟล์จะกระตุ้นการทำดัชนีโดยอัตโนมัติ; เพียงแค่คอมมิทหากคุณเลื่อนการดำเนินการ

**Q: รองรับรูปแบบเอกสารใดบ้างโดยอัตโนมัติ?**  
A: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, และหลายรูปแบบภาพ — มากกว่า 50 รูปแบบทั้งหมด

**Q: จะเปิดใช้งานการทำดัชนีแบบเรียลไทม์สำหรับโฟลเดอร์ที่รับอัปโหลดต่อเนื่องอย่างไร?**  
A: สร้างตัวตรวจจับระบบไฟล์ (เช่น `java.nio.file.WatchService`) ที่เรียก `DirectoryAdder.addDirectories(node, path)` ทุกครั้งที่ตรวจพบไฟล์ใหม่

---

**อัปเดตล่าสุด:** 2026-09-27  
**ทดสอบกับ:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [How to implement java full text search: create index directory with GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Implement Full Text Search Java Groupdocs Search](/search/java/searching/implement-full-text-search-java-groupdocs-search/)
- [How to Configure Search with GroupDocs.Search in Java - Configuration & Deployment Guide](/search/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/)

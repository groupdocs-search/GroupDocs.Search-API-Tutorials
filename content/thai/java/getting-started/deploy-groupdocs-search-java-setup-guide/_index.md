---
date: '2026-02-27'
description: เรียนรู้วิธีสร้างดัชนีที่สามารถค้นหาได้ใน Java ด้วย GroupDocs.Search
  for Java, เพิ่มไฟล์เพื่อค้นหา, เพิ่มไดเรกทอรีไปยังโหนด, และเปิดใช้งานการทำดัชนีแบบเรียลไทม์ใน
  Java.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: สร้างดัชนีที่ค้นหาได้ด้วย Java – ปรับใช้ GroupDocs.Search สำหรับ Java
type: docs
url: /th/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# สร้างดัชนีที่ค้นหาได้ใน Java – ปรับใช้ GroupDocs.Search สำหรับ Java

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, แอปพลิเคชัน **creating a searchable index java** จำเป็นต้องจัดการกับคอลเลกชันเอกสารขนาดใหญ่อย่างมีประสิทธิภาพ ไม่ว่าคุณจะสร้างบริการค้นหาระดับองค์กรหรือโครงการขนาดเล็ก เครือข่ายการค้นหาที่กำหนดค่าอย่างดีสามารถปรับปรุงความเร็วและความเกี่ยวข้องของการดึงข้อมูลได้อย่างมาก ในคู่มือนี้เราจะพาคุณผ่านกระบวนการทั้งหมดในการตั้งค่า **GroupDocs.Search for Java**, ตั้งแต่การเพิ่มไฟล์เพื่อค้นหาไปจนถึงการเพิ่มไดเรกทอรีไปยังโหนด, เพื่อให้คุณเริ่มทำดัชนีเอกสารของคุณได้ทันที.

> **Why this matters:** ดัชนีที่ค้นหาได้ช่วยลดความหน่วงของการสอบถามจากวินาทีเป็นมิลลิวินาที, สามารถขยายตามการเติบโตของข้อมูลของคุณ, และทำให้คุณเพิ่มความสามารถในการค้นหาแบบเต็มข้อความที่ทรงพลังให้กับโซลูชันที่ใช้ Java—ไม่ว่าจะเป็นพอร์ทัลเว็บ, แอปพลิเคชันเดสก์ท็อป, หรือไมโครเซอร์วิสบนคลาวด์.

## คำตอบด่วน
- **What is the primary purpose of GroupDocs.Search?** มันให้เครื่องยนต์ที่สามารถขยายได้, พัฒนาโดย Java สำหรับการทำดัชนีและการค้นหาเอกสารผ่านเครือข่ายแบบกระจาย.  
- **Which version should I use?** แนะนำให้ใช้เวอร์ชันที่เสถียรล่าสุด (เช่น 25.4) สำหรับโครงการใหม่.  
- **Do I need a license?** มีการทดลองใช้ฟรี 30 วัน; จำเป็นต้องมีใบอนุญาตถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **Can I add both files and whole directories?** ได้ – ใช้ตัวช่วย `addFiles` และ `addDirectories` เพื่อดึงข้อมูล.  
- **What Java version is required?** Java 8 หรือสูงกว่า, พร้อมกับ Maven สำหรับการจัดการ dependencies.  
- **How does real time indexing java work?** โดยการสมัครรับเหตุการณ์ของโหนดคุณสามารถเรียกทำการทำดัชนีใหม่อัตโนมัติเมื่อไฟล์มีการเปลี่ยนแปลง.

## “create searchable index java” คืออะไร?
การสร้างดัชนีที่ค้นหาได้ใน Java หมายถึงการสร้างโครงสร้างข้อมูลที่แมพคำค้นไปยังเอกสารที่มีคำนั้น, ทำให้สามารถทำการสอบถามแบบเต็มข้อความได้อย่างรวดเร็ว GroupDocs.Search จัดการส่วนที่ซับซ้อนให้, ทำให้คุณสามารถมุ่งเน้นที่การป้อนเอกสารและปรับแต่งพฤติกรรมการค้นหา.

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
- **Scalable network architecture** – ปรับใช้หลายโหนดที่แบ่งภาระการทำดัชนี.  
- **Rich document format support** – รองรับ PDF, Word, Excel, PowerPoint, รูปภาพ, และอื่น ๆ.  
- **Event‑driven updates** – สมัครรับเหตุการณ์ของโหนดเพื่อให้ดัชนีอัปเดตแบบเรียลไทม์.  
- **Simple Maven integration** – เพิ่มไม่กี่บรรทัดใน `pom.xml` แล้วเริ่มทำดัชนี.

## การทำดัชนีแบบเรียลไทม์ใน Java ด้วย GroupDocs.Search
GroupDocs.Search จะส่งเหตุการณ์ทุกครั้งที่ไฟล์ถูกเพิ่ม, อัปเดต, หรือถูกลบ. โดยการจัดการเหตุการณ์เหล่านี้คุณสามารถเรียก `addFiles` หรือ `addDirectories` โดยอัตโนมัติ, ทำให้ดัชนีคงความสอดคล้องโดยไม่ต้องทำด้วยมือ วิธีนี้เหมาะสำหรับระบบจัดการเอกสาร, พอร์ทัลเนื้อหา, และแอปพลิเคชันใด ๆ ที่ข้อมูลเปลี่ยนแปลงบ่อย.

## ข้อกำหนดเบื้องต้น
- **JDK 8+** ติดตั้งบนเครื่องพัฒนาของคุณ.  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**.  
- ความรู้พื้นฐานของ **Java** และ **Maven**.  
- การเข้าถึงไลบรารี **GroupDocs.Search for Java** (ดาวน์โหลดหรือใช้ Maven).

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การพึ่งพา Maven
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

> **Pro tip:** ควรอัปเดตหมายเลขเวอร์ชันให้เป็นปัจจุบันโดยตรวจสอบหน้าการปล่อยเวอร์ชันอย่างเป็นทางการ.

คุณยังสามารถดาวน์โหลดไฟล์ JAR โดยตรงจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับใบอนุญาต
- **Free Trial:** การประเมินผล 30 วัน.  
- **Temporary License:** ขอเพื่อการทดสอบต่อเนื่อง.  
- **Purchase:** จำเป็นสำหรับการปรับใช้ในสภาพแวดล้อมการผลิต.

### การเริ่มต้นพื้นฐาน
สร้างอ็อบเจกต์การกำหนดค่าที่ชี้ไปยังโฟลเดอร์ที่ไฟล์ดัชนีจะถูกจัดเก็บและกำหนดพอร์ตการสื่อสารพื้นฐาน:

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
ต่อไปนี้เราจะแยกคุณลักษณะหลักที่คุณต้องการเพื่อ **add files to search** และ **add directories to node**, พร้อมกับการปรับใช้เครือข่ายที่สามารถขยายได้.

### คุณลักษณะ 1 – การกำหนดค่าและการตั้งค่าเครือข่าย
การกำหนดค่าเครือข่ายการค้นหาเป็นขั้นตอนแรกในการสร้างดัชนีที่ค้นหาได้.

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

- **`basePath`** – โฟลเดอร์ที่ข้อมูลดัชนีจะถูกบันทึก.  
- **`basePort`** – พอร์ตเริ่มต้น; แต่ละโหนดจะเพิ่มค่าจากพอร์ตนี้.

### คุณลักษณะ 2 – การปรับใช้โหนดเครือข่ายการค้นหา
การปรับใช้โหนดจะกระจายภาระการทำดัชนีไปยังหลายเครื่องหรือหลายกระบวนการ.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

แต่ละ `SearchNetworkNode` ทำงานเป็นบริการทำดัชนีของตนเอง, ทำให้คุณสามารถ **create a searchable index java** ที่ขยายแนวนอนได้.

### คุณลักษณะ 3 – การสมัครรับเหตุการณ์ของโหนด
การอัปเดตแบบเรียลไทม์ทำให้ดัชนีสอดคล้องกับการเปลี่ยนแปลงของระบบไฟล์.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

โดยการฟังเหตุการณ์, คุณสามารถเรียกทำการทำดัชนีใหม่โดยอัตโนมัติเมื่อไฟล์ใหม่เข้ามา.

### คุณลักษณะ 4 – การเพิ่มไดเรกทอรีไปยังโหนดเครือข่าย
ใช้ตัวช่วยนี้เพื่อ **add directories to node**, เก็บรวบรวมเอกสารที่รองรับทั้งหมดอย่างเรียกซ้ำ.

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

### คุณลักษณะ 5 – การเพิ่มไฟล์ไปยังโหนดเครือข่าย
เมื่อคุณต้องการการควบคุมในระดับละเอียด, **add files to search** ทีละไฟล์:

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

วิธีนี้ให้ความยืดหยุ่นในการทำดัชนีไฟล์ที่มาจากสตรีม, ที่เก็บข้อมูลบนคลาวด์, หรือที่ตั้งชั่วคราว.

## กรณีการใช้งานทั่วไป
- **Enterprise document portals** ที่ต้องการการค้นหาแบบทันทีในหลายพันไฟล์ PDF และไฟล์ Office.  
- **Legal e‑discovery platforms** ที่หลักฐานใหม่ถูกเพิ่มอย่างต่อเนื่องและต้องสามารถค้นหาได้แบบเรียลไทม์.  
- **Content management systems** ที่เก็บรูปภาพ, งานนำเสนอ, และสเปรดชีตและต้องการการค้นหาแบบเต็มข้อความ.

## ปัญหาทั่วไปและวิธีแก้
| Issue | Reason | Fix |
|-------|--------|-----|
| **No documents appear in search results** | ดัชนียังไม่ได้ commit | เรียก `node.getIndexer().commit()` หลังจากเพิ่มไฟล์. |
| **Port conflict error** | บริการอื่นใช้ `basePort` | เลือก `basePort` อื่นหรือยืนยันว่าพอร์ตว่าง. |
| **Unsupported file format** | ไลบรารีไม่มี parser | ตรวจสอบให้แน่ใจว่าส่วนขยายไฟล์ได้รับการสนับสนุนหรือเพิ่ม extractor แบบกำหนดเอง. |

## เคล็ดลับการแก้ไขปัญหา
- **Verify node health:** ใช้ endpoint ตรวจสอบสุขภาพในตัว (`http://localhost:{port}/health`) เพื่อยืนยันว่าแต่ละโหนดกำลังทำงาน.  
- **Monitor memory usage:** ชุดเอกสารขนาดใหญ่สามารถทำให้หน่วยความจำพุ่งสูง; พิจารณาทำดัชนีเป็นชิ้นย่อยและเรียก `commit()` เป็นระยะ.  
- **Check logs:** GroupDocs.Search จะเขียนบันทึกรายละเอียดไปยังโฟลเดอร์ `basePath`—ตรวจสอบเพื่อหาข้อผิดพลาดการแปลงหรือการหมดเวลาเครือข่าย.

## คำถามที่พบบ่อย

**Q: Can I use GroupDocs.Search on a cloud‑based Java application?**  
A: ใช่. ไลบรารีทำงานกับ Java runtime ใดก็ได้, และคุณสามารถชี้ `basePath` ไปยังโฟลเดอร์ที่เมานท์บนเครือข่ายหรือที่เก็บข้อมูลบนคลาวด์ที่เมานท์ไว้ในเครื่อง.

**Q: How do I update the index when a file changes?**  
A: สมัครรับเหตุการณ์ของโหนด (ดูคุณลักษณะ 3) และเรียก `addFiles` หรือ `addDirectories` อีกครั้งสำหรับเส้นทางที่แก้ไข.

**Q: Is there a limit to the number of nodes I can deploy?**  
A: โดยปฏิบัติ ขีดจำกัดขึ้นอยู่กับฮาร์ดแวร์และแบนด์วิธของเครือข่ายของคุณ. API เองไม่มีการจำกัดแบบตายตัว.

**Q: Do I need to restart nodes after adding new files?**  
A: ไม่. การเพิ่มไฟล์จะทำให้การทำดัชนีทำงานโดยอัตโนมัติ; คุณเพียงต้อง commit หากคุณเลื่อนการดำเนินการ.

**Q: Which document formats are supported out of the box?**  
A: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, และหลายประเภทของรูปภาพ. ดูเอกสารอย่างเป็นทางการสำหรับรายการเต็ม.

**Q: How can I enable real time indexing java for a folder that receives uploads continuously?**  
A: Implement ตัวตรวจจับระบบไฟล์ (เช่น `java.nio.file.WatchService`) ที่เรียก `DirectoryAdder.addDirectories(node, path)` ทุกครั้งที่ตรวจพบไฟล์ใหม่.

---

**อัปเดตล่าสุด:** 2026-02-27  
**ทดสอบด้วย:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs
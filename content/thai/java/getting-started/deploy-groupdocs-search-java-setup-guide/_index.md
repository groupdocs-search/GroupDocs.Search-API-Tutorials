---
date: '2025-12-26'
description: เรียนรู้วิธีสร้างดัชนีที่ค้นหาได้ด้วย Java โดยใช้ GroupDocs.Search for
  Java, เพิ่มไฟล์เพื่อการค้นหาและเพิ่มไดเรกทอรีลงในโหนด
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: สร้างดัชนีที่ค้นหาได้ใน Java – ปรับใช้ GroupDocs.Search สำหรับ Java
type: docs
url: /th/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# สร้างดัชนีที่ค้นหาได้ด้วย Java – ปรับใช้ GroupDocs.Search for Java

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **การสร้างดัชนีที่ค้นหาได้ด้วย Java** แอปพลิเคชันต้องจัดการกับคอลเลกชันเอกสารขนาดใหญ่อย่างมีประสิทธิภาพ ไม่ว่าคุณจะสร้างบริการค้นหาระดับองค์กรหรือโครงการขนาดเล็ก, เครือข่ายการค้นหาที่กำหนดค่าอย่างดีสามารถปรับปรุงความเร็วและความเกี่ยวข้องของการดึงข้อมูลได้อย่างมาก ในคู่มือนี้เราจะพาคุณผ่านกระบวนการตั้งค่า **GroupDocs.Search for Java** ตั้งแต่การเพิ่มไฟล์เพื่อค้นหาไปจนถึงการเพิ่มไดเรกทอรีไปยังโหนด, เพื่อให้คุณเริ่มทำดัชนีเอกสารของคุณได้ทันที

## คำตอบสั้น ๆ
- **วัตถุประสงค์หลักของ GroupDocs.Search คืออะไร?** ให้เครื่องมือค้นหาขนาดใหญ่ที่ทำงานบน Java สำหรับการทำดัชนีและค้นหาเอกสารในเครือข่ายกระจาย  
- **ควรใช้เวอร์ชันใด?** แนะนำให้ใช้รุ่นเสถียรล่าสุด (เช่น 25.4) สำหรับโครงการใหม่  
- **ต้องการไลเซนส์หรือไม่?** มีการทดลองใช้ฟรี 30 วัน; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต  
- **สามารถเพิ่มไฟล์และไดเรกทอรีทั้งหมดได้หรือไม่?** ได้ – ใช้ตัวช่วย `addFiles` และ `addDirectories` เพื่อดึงข้อมูลเข้า  
- **ต้องการ Java เวอร์ชันใด?** Java 8 หรือสูงกว่า, พร้อม Maven สำหรับการจัดการ dependencies  

## “create searchable index java” คืออะไร?
การสร้างดัชนีที่ค้นหาได้ใน Java หมายถึงการสร้างโครงสร้างข้อมูลที่แมปคำกับเอกสารที่มีคำนั้นอยู่, ทำให้สามารถทำการค้นหาแบบเต็มข้อความได้อย่างรวดเร็ว GroupDocs.Search ทำหน้าที่จัดการส่วนที่ซับซ้อน, ให้คุณโฟกัสที่การป้อนเอกสารและปรับแต่งพฤติกรรมการค้นหา

## ทำไมต้องใช้ GroupDocs.Search for Java?
- **สถาปัตยกรรมเครือข่ายที่ขยายได้** – ปรับใช้หลายโหนดที่แบ่งภาระการทำดัชนีร่วมกัน  
- **รองรับรูปแบบเอกสารหลากหลาย** – PDF, Word, Excel, PowerPoint, รูปภาพ, และอื่น ๆ  
- **อัปเดตแบบเหตุการณ์** – สมัครรับเหตุการณ์ของโหนดเพื่อให้ดัชนีอัปเดตแบบเรียลไทม์  
- **รวมกับ Maven อย่างง่าย** – เพิ่มไม่กี่บรรทัดใน `pom.xml` แล้วเริ่มทำดัชนี  

## ข้อกำหนดเบื้องต้น
- **JDK 8+** ติดตั้งบนเครื่องพัฒนาของคุณ  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**  
- ความรู้พื้นฐานเกี่ยวกับ **Java** และ **Maven**  
- การเข้าถึงไลบรารี **GroupDocs.Search for Java** (ดาวน์โหลดหรือใช้ Maven)

## การตั้งค่า GroupDocs.Search for Java

### Dependency ของ Maven
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

> **เคล็ดลับ:** ตรวจสอบหน้า releases อย่างเป็นทางการเพื่อให้เวอร์ชันเป็นปัจจุบันอยู่เสมอ

คุณยังสามารถดาวน์โหลด JAR โดยตรงจากเว็บไซต์อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### การจัดหาไลเซนส์
- **ทดลองใช้ฟรี:** การประเมินผล 30 วัน  
- **ไลเซนส์ชั่วคราว:** ขอเพื่อการทดสอบต่อเนื่อง  
- **ซื้อไลเซนส์:** จำเป็นสำหรับการปรับใช้ในสภาพแวดล้อมการผลิต

### การเริ่มต้นพื้นฐาน
สร้างอ็อบเจ็กต์การกำหนดค่าที่ชี้ไปยังโฟลเดอร์ที่เก็บไฟล์ดัชนีและกำหนดพอร์ตการสื่อสารพื้นฐาน:

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

## วิธีสร้าง searchable index java ด้วย GroupDocs.Search?

ต่อไปนี้เป็นการแยกคุณลักษณะหลักที่คุณต้อง **add files to search** และ **add directories to node** พร้อมกับการปรับใช้เครือข่ายที่ขยายได้

### คุณลักษณะ 1 – การกำหนดค่าและตั้งค่าเครือข่าย
การกำหนดค่าเครือข่ายการค้นหาเป็นขั้นตอนแรกในการสร้าง searchable index

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

- **`basePath`** – ไดเรกทอรีที่ข้อมูลดัชนีจะถูกบันทึกไว้  
- **`basePort`** – พอร์ตเริ่มต้น; โหนดแต่ละตัวจะเพิ่มค่าจากพอร์ตนี้

### คุณลักษณะ 2 – การปรับใช้โหนดเครือข่ายการค้นหา
การปรับใช้โหนดช่วยกระจายภาระการทำดัชนีไปยังเครื่องหรือกระบวนการหลายเครื่อง

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

แต่ละ `SearchNetworkNode` ทำงานเป็นบริการทำดัชนีของตนเอง, ทำให้คุณ **create a searchable index java** ที่สามารถขยายแนวนอนได้

### คุณลักษณะ 3 – การสมัครรับเหตุการณ์ของโหนด
การอัปเดตแบบเรียลไทม์ทำให้ดัชนีสอดคล้องกับการเปลี่ยนแปลงของระบบไฟล์

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

โดยการฟังเหตุการณ์, คุณสามารถเรียกทำการ re‑index อัตโนมัติเมื่อมีไฟล์ใหม่เข้ามา

### คุณลักษณะ 4 – การเพิ่มไดเรกทอรีไปยังโหนดเครือข่าย
ใช้ตัวช่วยนี้เพื่อ **add directories to node**, รวบรวมเอกสารที่รองรับทั้งหมดแบบเรียกซ้ำ

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
เมื่อคุณต้องการควบคุมอย่างละเอียด, **add files to search** ทีละไฟล์:

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

วิธีนี้ให้ความยืดหยุ่นในการทำดัชนีไฟล์จากสตรีม, ที่เก็บบนคลาวด์, หรือตำแหน่งชั่วคราว

## ปัญหาทั่วไป & วิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **ไม่มีเอกสารปรากฏในผลการค้นหา** | ดัชนียังไม่ได้ commit | เรียก `node.getIndexer().commit()` หลังจากเพิ่มไฟล์ |
| **เกิดข้อผิดพลาดพอร์ตซ้ำ** | บริการอื่นใช้ `basePort` | เลือก `basePort` อื่นหรือยืนยันว่าพอร์ตว่าง |
| **รูปแบบไฟล์ไม่รองรับ** | ไลบรารีไม่มี parser | ตรวจสอบให้แน่ใจว่ามีส่วนขยายไฟล์ที่รองรับหรือเพิ่ม extractor แบบกำหนดเอง |

## คำถามที่พบบ่อย

**ถาม: สามารถใช้ GroupDocs.Search ในแอปพลิเคชัน Java บนคลาวด์ได้หรือไม่?**  
ตอบ: ใช่. ไลบรารีทำงานกับ Java runtime ใดก็ได้, และคุณสามารถชี้ `basePath` ไปยังโฟลเดอร์ที่เมานท์บนเครือข่ายหรือที่เก็บบนคลาวด์ที่เมานท์ไว้ในเครื่อง

**ถาม: จะอัปเดตดัชนีเมื่อไฟล์มีการเปลี่ยนแปลงอย่างไร?**  
ตอบ: สมัครรับเหตุการณ์ของโหนด (ดูคุณลักษณะ 3) แล้วเรียก `addFiles` หรือ `addDirectories` อีกครั้งสำหรับเส้นทางที่แก้ไข

**ถาม: มีขีดจำกัดจำนวนโหนดที่สามารถปรับใช้ได้หรือไม่?**  
ตอบ: โดยหลักการ ขีดจำกัดขึ้นอยู่กับฮาร์ดแวร์และแบนด์วิธของเครือข่ายของคุณเอง API เองไม่มีการกำหนดขีดจำกัดคงที่

**ถาม: จำเป็นต้องรีสตาร์ทโหนดหลังจากเพิ่มไฟล์ใหม่หรือไม่?**  
ตอบ: ไม่จำเป็น. การเพิ่มไฟล์จะทำการทำดัชนีโดยอัตโนมัติ; เพียงแค่ commit หากคุณเลิกทำการ commit ไปก่อนหน้า

**ถาม: มีการรองรับรูปแบบเอกสารใดบ้างโดยตรง?**  
ตอบ: PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML, และหลายรูปแบบภาพ ดูเอกสารอย่างเป็นทางการสำหรับรายการเต็ม

---

**อัปเดตล่าสุด:** 2025-12-26  
**ทดสอบกับ:** GroupDocs.Search for Java 25.4  
**ผู้เขียน:** GroupDocs
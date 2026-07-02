---
date: '2026-01-16'
description: เรียนรู้วิธีกำหนดค่าเครือข่ายการค้นหา GroupDocs ใน Java และเพิ่มคำพ้องความหมายลงในดัชนีเพื่อเพิ่มประสิทธิภาพการค้นหา.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: กำหนดค่า GroupDocs.Search Network ใน Java – เพิ่มประสิทธิภาพการค้นหา
type: docs
url: /th/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# กำหนดค่า GroupDocs.Search Network ใน Java - Boost Search

แอปพลิเคชันที่อุดมด้วยข้อมูลในปัจจุบัน **กำหนดค่าเครือข่ายการค้นหา groupdocs** เป็นขั้นตอนสำคัญในการให้ผลลัพธ์ที่เร็วและนำไปสู่ประสิทธิภาพในเอกสารขนาดใหญ่สำหรับสร้างระบบแบบทั้งหมดหรือขยายความเข้มข้นของพลังงานแล้วนั้น GroupDocs.Search network มอบสเกลองค์กรที่เพิ่มคำร้องให้และรักษาความสดใหม่ให้ต่ำในซีรีย์นี้ตรวจสอบและปรับจูน GroupDocs.Search network ด้วย Java เคล็ดลับเพิ่มเติมคำพ้องลงไปที่ดัชนีและการจัดการระบบใน

## คำตอบด่วน
- **ประโยชน์หลักของการกำหนดค่าเครือข่าย GroupDocs.Search คืออะไร**ช่วยให้สามารถจัดทำดัชนีและการสืบค้นแบบกระจาย ปรับปรุงประสิทธิภาพและความสามารถในการปรับขนาด
- **ฉันจำเป็นต้องมีใบอนุญาตเพื่อเรียกใช้ตัวอย่างหรือไม่**การทดลองใช้ฟรีใช้งานได้เพื่อการพัฒนา ต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการผลิต
- **สามารถเพิ่มคำพ้องความหมายโดยไม่ต้องสร้างดัชนีใหม่ได้หรือไม่**ใช่—ใช้พจนานุกรมคำพ้องความหมายในขณะรันไทม์เพื่อ **เพิ่มคำพ้องความหมายในดัชนี**
- **ฉันสามารถปรับใช้โหนดได้กี่โหนด?** คุณสามารถปรับใช้โหนดได้มากเท่าที่โครงสร้างพื้นฐานของคุณอนุญาต โดยแต่ละโหนดจะทำงานบนพอร์ตของตัวเอง

## การกำหนดค่าเครือข่าย GroupDocs.Search คืออะไร?

การกำหนดค่าเครือข่าย GroupDocs.Search หมายถึงการกำหนดโครงสร้างโฟลเดอร์ พอร์ต และการตั้งค่าโหนดที่ช่วยให้ JVM หลายอินสแตนซ์ทำงานร่วมกันในการจัดทำดัชนีและการค้นหา การตั้งค่านี้จะสร้างโหนดหลักที่ประสานงานกับโหนดรอง (ชาร์ด) และรับประกันว่าการค้นหาจะถูกดำเนินการทั่วทั้งชุดข้อมูล

## เหตุใดจึงต้องกำหนดค่าเครือข่าย GroupDocs.Search?
- **ความสามารถในการขยายขนาด** – กระจายภาระการจัดทำดัชนีไปยังเครื่องหลายเครื่อง
- **ความน่าเชื่อถือ** – สามารถเพิ่มหรือลบโหนดได้โดยไม่ต้องหยุดการทำงาน
- **ความเกี่ยวข้องของการค้นหา** – เพิ่มคำพ้องความหมายลงในดัชนีเพื่อผลลัพธ์ที่สมบูรณ์ยิ่งขึ้น
- **ประสิทธิภาพ** – การดำเนินการค้นหาแบบขนานช่วยลดเวลาตอบสนอง

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) เวอร์ชัน 8 หรือใหม่กว่า
- Maven สำหรับสร้างโปรเจ็กต์
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ของ Java
- การเข้าถึงไลบรารี GroupDocs.Search for Java (ดาวน์โหลดผ่าน Maven หรือหน้าดาวน์โหลดอย่างเป็นทางการ)

## การตั้งค่า GroupDocs.Search for Java

เพิ่ม repository และ dependency ลงในไฟล์ **pom.xml** ของ Maven:

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

หรืออีกทางเลือกหนึ่ง ดาวน์โหลดเวอร์ชันล่าสุดได้โดยตรงจาก [GroupDocs.Search สำหรับรุ่น Java](https://releases.groupdocs.com/search/java/)

### การขอรับใบอนุญาต
- **ทดลองใช้ฟรี** – สำรวจคุณสมบัติหลักได้โดยไม่มีค่าใช้จ่าย
- **ใบอนุญาตชั่วคราว** – ปลดล็อกความสามารถเต็มรูปแบบสำหรับการทดสอบระยะสั้น
- **ใบอนุญาตเชิงพาณิชย์** – จำเป็นสำหรับการใช้งานจริง

### การเริ่มต้นและการตั้งค่าพื้นฐาน
สร้างคลาส Java อย่างง่ายเพื่อตรวจสอบว่าไลบรารีโหลดได้อย่างถูกต้อง:

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

## คู่มือทีละขั้นตอนในการกำหนดค่าเครือข่าย GroupDocs.Search

### 1. การกำหนดค่าเครือข่ายการค้นหา
กำหนดโฟลเดอร์เอกสารหลักและพอร์ตเริ่มต้นสำหรับการสื่อสารของโหนด

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

- **basePath** – ตำแหน่งที่เก็บพจนานุกรม (เช่น ไฟล์คำพ้องความหมาย)
- **basePort** – พอร์ตแรก โหนดถัดไปจะเพิ่มค่าจากค่านี้

### 2. การติดตั้งโหนดเครือข่ายการค้นหา
สร้างโหนดผู้ปฏิบัติงานหลายโหนดที่มีการกำหนดค่าเดียวกัน

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

แต่ละโหนดทำงานบนพอร์ตของตัวเอง (basePort+index) และเก็บส่วนหนึ่งของดัชนีโดยรวมไว้

### 3. การสมัครรับเหตุการณ์ของโหนด
ตรวจสอบสถานะสุขภาพ ความคืบหน้าในการจัดทำดัชนี และสภาวะข้อผิดพลาดโดยการแนบตัวรับฟังเหตุการณ์เข้ากับโหนดหลัก

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

การเรียกกลับเหตุการณ์ช่วยให้คุณตอบสนองต่อการเริ่มต้น/หยุดโหนด การเสร็จสิ้นการจัดทำดัชนี และความล้มเหลวที่ไม่คาดคิด

### 4. การเพิ่มคำพ้องความหมายลงในตัวจัดทำดัชนีของโหนด
เพิ่มความเกี่ยวข้องโดย **เพิ่มคำพ้องความหมายลงในดัชนี** ในระหว่างการทำงาน

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

- **group** – อาร์เรย์ของคำที่ควรได้รับการพิจารณาว่าเทียบเท่ากัน
- **clearBeforeAdding** – ตั้งค่าเป็น `true` หากคุณต้องการแทนที่รายการที่มีอยู่

### 5. การเพิ่มไดเร็กทอรีสำหรับการจัดทำดัชนี
บอกโหนดหลักว่าโฟลเดอร์ใดมีเอกสารที่คุณต้องการให้ค้นหาได้

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

วิธีการนี้จะสแกนไดเร็กทอรีแบบเรียกซ้ำและกระจายไฟล์ไปยังชาร์ดต่างๆ

### 6. การค้นหาข้อความในเครือข่าย
ดำเนินการค้นหาในทุกโหนด โดยอาจบังคับให้ค้นหาแบบตรงกันทุกประการ

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

เปลี่ยน `exactMatchOnly` เป็น `true` เมื่อคุณต้องการการค้นหาแบบตรงตัวโดยไม่ตัดคำลงท้าย

### 7. การปิดโหนดเครือข่าย
ปล่อยทรัพยากรอย่างนุ่มนวลเมื่อการประมวลผลเสร็จสิ้น

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

การปิดระบบอย่างถูกต้องจะช่วยป้องกันการรั่วไหลของหน่วยความจำและรักษาสภาพการทำงานของ JVM ให้สมบูรณ์

## การประยุกต์ใช้งานจริง
| สถานการณ์ | เครือข่ายช่วยได้อย่างไร |

|----------|-----------------------|

| **การค้นหาระดับองค์กร** | กระจายการจัดทำดัชนีไปยังเซิร์ฟเวอร์ศูนย์ข้อมูลสำหรับคลังข้อมูลขนาดเพตาไบต์ |
| **การจัดการเอกสาร** | เพิ่มคำพ้องความหมายลงในดัชนีเพื่อให้ผู้ใช้สามารถค้นหาเอกสารได้แม้จะมีคำศัพท์ที่หลากหลาย |
| **แคตตาล็อกอีคอมเมิร์ซ** | ปรับใช้โหนดเฉพาะภูมิภาคเพื่อให้บริการการค้นหาสินค้าในพื้นที่ได้อย่างรวดเร็ว |
| **การจัดการเนื้อหา** | ทำให้เนื้อหาสามารถค้นหาได้ในขณะที่บรรณาธิการเพิ่มไฟล์ใหม่ลงในไดเร็กทอรีเฉพาะ |

## ปัญหาและวิธีแก้ไขทั่วไป
- **ความขัดแย้งของพอร์ต** – ตรวจสอบให้แน่ใจว่าพอร์ตของแต่ละโหนด (basePort+index) ว่าง ปรับ `basePort` หากจำเป็น

- **ไม่ได้ใช้คำพ้องความหมาย** – ตรวจสอบว่าคุณเรียกใช้ `indexer.setDictionary(dictionary)` หลังจากเพิ่มคำศัพท์แล้ว - **โหนดไม่ตอบสนอง** – สมัครรับเหตุการณ์ ตรวจสอบการเรียกกลับ `NodeFailed` เพื่อวินิจฉัยปัญหาเครือข่าย

- **หน่วยความจำรั่วไหลเมื่อปิด** – เรียกใช้ `node.close()` ทุกครั้งสำหรับทุกโหนดที่ใช้งาน

## คำถามที่พบบ่อย

**ถาม: การใช้งานหลายโหนดช่วยปรับปรุงประสิทธิภาพการค้นหาได้อย่างไร?**
ตอบ: แต่ละโหนดจะจัดทำดัชนีข้อมูลส่วนหนึ่ง ทำให้สามารถประมวลผลแบบขนานและลดความหน่วงของคิวรี เนื่องจากมีการแบ่งงานกัน

**ถาม: ฉันสามารถเพิ่มคำพ้องความหมายโดยไม่ต้องจัดทำดัชนีเอกสารที่มีอยู่ใหม่ได้หรือไม่?**
ตอบ: ได้ คุณสามารถ **เพิ่มคำพ้องความหมายลงในดัชนี** ได้ในขณะทำงานผ่านพจนานุกรมคำพ้องความหมาย การเปลี่ยนแปลงจะมีผลทันทีสำหรับคิวรีใหม่

**ถาม: การสมัครรับเหตุการณ์ของโหนดเป็นสิ่งจำเป็นหรือไม่?**
ตอบ: แม้ว่าจะไม่จำเป็นสำหรับการทำงานพื้นฐาน แต่การสมัครรับเหตุการณ์จะช่วยให้คุณมองเห็นสถานะของโหนดและช่วยให้คุณตอบสนองต่อความล้มเหลวได้อย่างรวดเร็ว


**ถาม: แนวทางปฏิบัติที่ดีที่สุดสำหรับการจัดการทรัพยากรโหนดคืออะไร?**
ตอบ: ปิดโหนดที่ไม่ได้ใช้งานเป็นประจำ ตรวจสอบการใช้งานหน่วยความจำ JVM และรีไซเคิลโหนดในช่วงเวลาที่ไม่ใช่ช่วงเวลาที่มีการใช้งานสูงสุด เพื่อให้การใช้ทรัพยากรอยู่ในระดับที่เหมาะสมที่สุด

**ถาม: GroupDocs.Search รองรับรูปแบบที่ไม่ใช่ข้อความ เช่น PDF หรือรูปภาพหรือไม่?**
ตอบ: ได้อย่างแน่นอน ไลบรารีนี้สามารถดึงข้อความจาก PDF ไฟล์ Office และยังทำการ OCR บนรูปภาพ ทำให้สามารถค้นหาได้ทันที

---

**อัปเดตล่าสุด:** 2026-01-16
**ทดสอบกับ:** GroupDocs.Search 25.4 สำหรับ Java
**ผู้เขียน:** GroupDocs
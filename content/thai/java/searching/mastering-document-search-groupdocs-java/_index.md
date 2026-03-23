---
date: '2026-03-23'
description: เรียนรู้วิธีสร้างดัชนีการค้นหาใน Java ด้วย GroupDocs.Search และสร้างเครือข่ายการค้นหาเอกสารที่มีประสิทธิภาพสำหรับแอปพลิเคชัน
  Java.
keywords:
- GroupDocs.Search Java
- document search network
- Java document retrieval
title: สร้างดัชนีการค้นหา Java ด้วย GroupDocs.Search – คู่มือ
type: docs
url: /th/java/searching/mastering-document-search-groupdocs-java/
weight: 1
---

# สร้างดัชนีการค้นหา Java ด้วย GroupDocs.Search – คู่มือ

คุณกำลังประสบปัญหาในการจัดการคอลเลกชันเอกสารขนาดใหญ่อย่างมีประสิทธิภาพหรือไม่? การค้นหาผ่านไฟล์จำนวนมากอาจเป็นเรื่องยากโดยไม่มีเครื่องมือที่เหมาะสม **Creating a search index java** ด้วย GroupDocs.Search สำหรับ Java จะมอบวิธีที่แข็งแกร่งและขยายได้ในการทำดัชนีและดึงเอกสาร เปลี่ยนคลังข้อมูลที่วุ่นวายให้เป็นฐานความรู้ที่สามารถค้นหาได้ ในคู่มือนี้เราจะพาคุณผ่านทุกขั้นตอน—ตั้งแต่การกำหนดค่าเครือข่าย การปรับใช้โหนด และการดึงเนื้อหาเอกสารเฉพาะ—เพื่อให้คุณเริ่มใช้งานได้อย่างรวดเร็ว

## คำตอบด่วน
- **วัตถุประสงค์หลักของ GroupDocs.Search คืออะไร?** มันให้การทำดัชนีที่เร็วและขยายได้พร้อมการค้นหาแบบเต็มข้อความสำหรับคอลเลกชันเอกสารขนาดใหญ่ใน Java.  
- **ต้องการเวอร์ชัน Java ใด?** Java 8 หรือสูงกว่าแนะนำ.  
- **ฉันต้องการใบอนุญาตเพื่อทดลองใช้งานหรือไม่?** ใช่ — รับใบอนุญาตชั่วคราวเพื่อเปิดใช้งานคุณสมบัติทั้งหมดในช่วงการประเมินผล.  
- **ฉันสามารถขยายเครือข่ายการค้นหาได้หรือไม่?** แน่นอน; คุณสามารถปรับใช้หลายโหนดเพื่อกระจายภาระการทำดัชนีและการค้นหา.  
- **ฉันจะดึงข้อความจากเอกสารเฉพาะได้อย่างไร?** ใช้ `searcher.getDocumentText()` หลังจากค้นหาเอกสารโดยใช้เส้นทางหรือเมตาดาต้า.

## “create search index java” คืออะไร?
การสร้างดัชนีการค้นหาใน Java หมายถึงการสร้างโครงสร้างข้อมูลที่แมพคำและวลีไปยังเอกสารที่มีคำเหล่านั้น GroupDocs.Search ทำงานอัตโนมัติในกระบวนการนี้ จัดการการแยกคำ การจัดเก็บ และการค้นหาอย่างรวดเร็ว เพื่อให้คุณมุ่งเน้นที่ตรรกะธุรกิจแทนรายละเอียดการทำดัชนีระดับต่ำ

## ทำไมต้องใช้ GroupDocs.Search สำหรับ Java?
- **Performance:** อัลกอริธึมที่ปรับแต่งให้ทำงานส่งมอบผลการค้นหาแบบใกล้เคียงเรียลไทม์แม้กับไฟล์หลายล้านไฟล์.  
- **Scalability:** ปรับใช้เครือข่ายการค้นหาด้วยหลายโหนดเพื่อสมดุลภาระ.  
- **Flexibility:** รองรับหลายสิบรูปแบบเอกสารโดยไม่ต้องตั้งค่าเพิ่มเติม (PDF, DOCX, TXT, ฯลฯ).  
- **Ease of Integration:** การตั้งค่า Maven ง่ายและ API ของ Java ชัดเจนทำให้เป็นมิตรต่อผู้พัฒนา.

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่ม, โปรดตรวจสอบว่าคุณได้ปฏิบัติตามข้อกำหนดต่อไปนี้แล้ว:

### ไลบรารีและการพึ่งพาที่จำเป็น
เพื่อใช้ GroupDocs.Search ใน Java, ตั้งค่าโปรเจกต์ของคุณด้วยการพึ่งพา Maven. รวมรีโพซิทอรีของ GroupDocs และการพึ่งพาในไฟล์ `pom.xml` ของคุณ:

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

### ความต้องการการตั้งค่าสภาพแวดล้อม
ตรวจสอบว่าคุณได้ติดตั้ง JDK ที่เข้ากันได้ (แนะนำ Java 8 หรือสูงกว่า). สภาพแวดล้อมการพัฒนาของคุณควรสนับสนุนโปรเจกต์ Maven.

### ความรู้เบื้องต้นที่จำเป็น
ความคุ้นเคยกับการเขียนโปรแกรม Java และความรู้พื้นฐานเกี่ยวกับการตั้งค่าโปรเจกต์ Maven จะเป็นประโยชน์ในการทำตามได้อย่างมีประสิทธิภาพ

## การตั้งค่า GroupDocs.Search สำหรับ Java

การตั้งค่าโปรเจกต์ Java ของคุณด้วย GroupDocs.Search มีขั้นตอนสำคัญไม่กี่ขั้นตอน:

1. **Maven Setup**: เพิ่มรีโพซิทอรีและการพึ่งพาที่จำเป็นในไฟล์ `pom.xml` ของคุณตามที่แสดงด้านบน.  
2. **License Acquisition**: รับใบอนุญาตชั่วคราวเพื่อสำรวจคุณสมบัติทั้งหมดของ GroupDocs.Search โดยไม่มีข้อจำกัดใด ๆ. เยี่ยมชม [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) สำหรับรายละเอียดเพิ่มเติม.

### การเริ่มต้นพื้นฐาน

เพื่อเริ่มต้น GroupDocs.Search ในแอปพลิเคชัน Java ของคุณ, เริ่มด้วยการตั้งค่าการกำหนดค่าเบื้องต้น:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an index
        Index index = new Index("YOUR_INDEX_DIRECTORY");
        
        // Add documents to the index
        index.add("YOUR_DOCUMENT_DIRECTORY");

        System.out.println("Indexing completed.");
    }
}
```

แทนที่ `"YOUR_INDEX_DIRECTORY"` และ `"YOUR_DOCUMENT_DIRECTORY"` ด้วยไดเรกทอรีจริงของคุณ การตั้งค่าง่าย ๆ นี้จะเริ่มต้นดัชนีและเพิ่มเอกสาร, เตรียมคุณสำหรับการทำงานที่ซับซ้อนมากขึ้น.

## คู่มือการนำไปใช้

เราจะแบ่งการนำไปใช้เป็นสามคุณลักษณะหลัก: การตั้งค่าการกำหนดค่า, การปรับใช้เครือข่ายการค้นหา, และการดึงเอกสารจากเครือข่าย

### คุณลักษณะ 1: การตั้งค่าการกำหนดค่า

#### ภาพรวม
คุณลักษณะนี้แสดงการกำหนดค่าเครือข่ายการค้นหาด้วยฐานเส้นทางและพอร์ต. เป็นสิ่งสำคัญสำหรับการตั้งค่าสภาพแวดล้อมการทำดัชนีของคุณ.

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigurationSetup {
    public static void main(String[] args) {
        String basePath = "YOUR_DOCUMENT_DIRECTORY"; // Set your document directory here
        int basePort = 49108; // Port number for the configuration
        
        // Configure the search network with provided path and port.
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
    }
}
```

**Explanation**: เมธอด `ConfiguringSearchNetwork.configure` ตั้งค่าสภาพแวดล้อมของคุณโดยใช้ไดเรกทอรีเอกสารที่ระบุและพอร์ต. ปรับแต่งพารามิเตอร์เหล่านี้ตามความต้องการของโปรเจกต์ของคุณ.

### คุณลักษณะ 2: การปรับใช้เครือข่ายการค้นหา

#### ภาพรวม
การปรับใช้เครือข่ายการค้นหาต้องเริ่มต้นโหนดที่รับผิดชอบการทำดัชนีเอกสารและการดึงข้อมูล.

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.*;

public class SearchNetworkDeploymentFeature {
    public static void main(String[] args) {
        String basePath = "YOUR_DOCUMENT_DIRECTORY"; // Set your document directory here
        int basePort = 49108; // Port number for deployment
        
        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Deploy the search network using given path and port.
        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
    }
}
```

**Explanation**: เมธอด `deploy` เริ่มต้นโหนดตามการกำหนดค่าของคุณ. แต่ละโหนดสามารถจัดการส่วนของกระบวนการทำดัชนีได้อย่างอิสระ, ทำให้สามารถขยายได้.

### คุณลักษณะ 3: การดึงเอกสารจากเครือข่าย

#### ภาพรวม
ดึงเอกสารจากเครือข่ายการค้นหาที่ตรงกับเกณฑ์ข้อความที่ระบุ.

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.*;
import java.util.ArrayList;
import java.util.Arrays;

public class NetworkDocumentRetrievalFeature {
    public static void main(String[] args) {
        // Assuming masterNode is already initialized and contains documents.
        SearchNetworkNode masterNode = null;  // Placeholder: Initialize your search network node here
        String containsInPath = "English.txt";
        
        getDocumentText(masterNode, containsInPath);
    }

    public static void getDocumentText(SearchNetworkNode node, String containsInPath) {
        Searcher searcher = node.getSearcher();
        ArrayList<NetworkDocumentInfo> documents = new ArrayList<>();
        int[] shardIndices = node.getShardIndices();

        for (int i = 0; i < shardIndices.length; i++) {
            int shardIndex = shardIndices[i];
            NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);
            documents.addAll(Arrays.asList(infos));

            for (NetworkDocumentInfo info : infos) {
                NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
                documents.addAll(Arrays.asList(items));
            }
        }

        for (NetworkDocumentInfo document : documents) {
            if (document.getDocumentInfo().toString().contains(containsInPath)) {
                StringOutputAdapter outputAdapter = new StringOutputAdapter(OutputFormat.PlainText);
                searcher.getDocumentText(document, outputAdapter);

                System.out.println(outputAdapter.getResult());
                break;
            }
        }
    }
}
```

**Explanation**: คุณลักษณะนี้วนลูปผ่าน shard เพื่อค้นหาเอกสารที่มีข้อความที่ระบุ. เมธอด `searcher.getDocumentText` จะดึงและแสดงเนื้อหาที่ตรงกัน.

## การประยุกต์ใช้งานจริง

- **Enterprise Document Management** – ปรับปรุงการดึงเอกสารในองค์กรขนาดใหญ่, เพิ่มประสิทธิภาพการทำงาน.  
- **Legal Document Search** – ค้นหาข้อความกฎหมายที่เกี่ยวข้องได้อย่างรวดเร็วในไฟล์คดีหรือห้องสมุดกฎหมายจำนวนมาก.  
- **Library Cataloging Systems** – ทำให้การค้นหารายการแคตาล็อกของหนังสือ, วารสาร, และสื่ออื่น ๆ มีประสิทธิภาพ.

## การพิจารณาประสิทธิภาพ

เพื่อเพิ่มประสิทธิภาพการใช้งาน GroupDocs.Search ของคุณ:

- **Resource Management** – ตรวจสอบการใช้หน่วยความจำเพื่อป้องกันคอขวดระหว่างการทำดัชนี.  
- **Scalability** – ใช้หลายโหนดเพื่อกระจายภาระและเพิ่มประสิทธิภาพ.  
- **Index Optimization** – ปรับปรุงและเพิ่มประสิทธิภาพดัชนีอย่างสม่ำเสมอเพื่อผลการค้นหาเร็วขึ้น.

## ปัญหาทั่วไปและวิธีแก้

| Issue | Cause | Solution |
|-------|-------|----------|
| **ข้อผิดพลาด Out‑of‑Memory ระหว่างการทำดัชนี** | ไฟล์ขนาดใหญ่ถูกโหลดทั้งหมดพร้อมกัน | เปิดใช้งานการทำดัชนีแบบเพิ่มขั้นหรือเพิ่มขนาด heap ของ JVM (`-Xmx`). |
| **การค้นหาไม่คืนผลลัพธ์** | ดัชนีไม่ได้รับการรีเฟรชหลังจากเพิ่มเอกสาร | เรียก `index.update()` หรือรีสตาร์ทโหนดเพื่อโหลดดัชนีใหม่. |
| **ข้อขัดแย้งพอร์ตเมื่อปรับใช้โหนด** | บริการอื่นใช้พอร์ตเดียวกัน | เลือกค่ `basePort` ที่ไม่ได้ใช้หรือปรับกฎไฟร์วอลล์. |

## คำถามที่พบบ่อย

**Q: ฉันจะสร้างดัชนีการค้นหา java อย่างโปรแกรมได้อย่างไร?**  
A: ใช้คลาส `Index` เพื่อชี้ไปยังไดเรกทอรี, จากนั้นเรียก `index.add("<document_folder>")`. นี้จะสร้างดัชนีที่สามารถค้นหาได้บนดิสก์.

**Q: ฉันสามารถเพิ่มเอกสารใหม่ลงในดัชนีที่มีอยู่โดยไม่ต้องสร้างใหม่ทั้งหมดได้หรือไม่?**  
A: ใช่ — เพียงเรียก `index.add("<new_document_folder>")` บนอินสแตนซ์ `Index` ที่มีอยู่; ไลบรารีจะทำการรวมไฟล์ใหม่.

**Q: ฟอร์แมตใดบ้างที่รองรับโดยไม่ต้องตั้งค่าเพิ่มเติม?**  
A: GroupDocs.Search รองรับมากกว่า 50 ฟอร์แมต, รวมถึง PDF, DOCX, TXT, PPTX, และหลายประเภทของรูปภาพ.

**Q: สามารถค้นหาข้ามหลายโหนดพร้อมกันได้หรือไม่?**  
A: แน่นอน. เมื่อคุณปรับใช้เครือข่ายการค้นหา, แต่ละโหนดจะแบ่งปันข้อมูล shard ของตน, ทำให้การสอบถามเดียวสามารถกระจายไปยังทุกโหนดได้.

**Q: ฉันจะทำให้เครือข่ายการค้นหามีความปลอดภัยได้อย่างไร?**  
A: ใช้ TLS/SSL สำหรับการสื่อสารระหว่างโหนดและบังคับใช้โทเค็นการยืนยันตัวตนเมื่อเปิดเผย API การค้นหา.

## คำถามที่พบบ่อย

**1. ข้อกำหนดเบื้องต้นที่สำคัญสำหรับการใช้งาน GroupDocs.Search ใน Java คืออะไร?**  
Java 8+, การตั้งค่า Maven, การพึ่งพา GroupDocs.Search, และใบอนุญาตที่ถูกต้องเป็นข้อกำหนดที่จำเป็น.

**2. ฉันจะกำหนดค่าเครือข่ายการค้นหาใน Java ด้วย GroupDocs.Search อย่างไร?**  
ใช้ `ConfiguringSearchNetwork.configure()` พร้อมเส้นทางเอกสารและพอร์ตของคุณเพื่อกำหนดสภาพแวดล้อม.

**3. ฉันสามารถปรับใช้หลายโหนดเพื่อขยายเครือข่ายการค้นหาได้หรือไม่?**  
ได้, การปรับใช้หลายโหนดด้วย `SearchNetworkDeployment.deploy()` จะเพิ่มความสามารถในการขยายและการกระจายภาระ.

**4. เครือข่ายการค้นหามีประสิทธิภาพอย่างไรกับคอลเลกชันเอกสารขนาดใหญ่?**  
ด้วยการปรับใช้โหนดที่เหมาะสมและการปรับปรุงดัชนี, มันจัดการคอลเลกชันขนาดใหญ่ได้อย่างมีประสิทธิภาพ, ให้การดึงข้อมูลที่รวดเร็ว.

**5. ฉันจะดึงเนื้อหาเอกสารเฉพาะที่มีข้อความบางอย่างได้อย่างไร?**  
ใช้ `searcher.getDocumentText()` ภายในโหนดเครือข่ายของคุณเพื่อดึงและแสดงเนื้อหาที่ตรงกับเกณฑ์ของคุณ.

## สรุป

โดยทำตามบทแนะนำนี้ คุณจะรู้วิธี **create search index java** ด้วย GroupDocs.Search, ตั้งค่าเครือข่ายการค้นหาที่สามารถขยายได้, และดึงเนื้อหาเอกสารตามต้องการ. นำรูปแบบเหล่านี้ไปใช้ในแอปพลิเคชันของคุณเพื่อมอบประสบการณ์การค้นหาที่เร็วและเชื่อถือได้สำหรับผู้ใช้ที่จัดการห้องสมุดเอกสารขนาดมหาศาล.

---

**อัปเดตล่าสุด:** 2026-03-23  
**ทดสอบด้วย:** GroupDocs.Search 25.4  
**ผู้เขียน:** GroupDocs
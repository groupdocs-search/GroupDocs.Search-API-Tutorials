---
date: '2026-07-02'
description: เรียนรู้วิธีรับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Search, เพิ่ม directories
  ไปยัง index, และเพิ่ม custom document attributes ขณะจัดการ Java search network nodes.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: รับใบอนุญาตชั่วคราว GroupDocs – Master Search Nodes (Java)
type: docs
url: /th/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# รับใบอนุญาตชั่วคราว GroupDocs – โหนดการค้นหาหลัก (Java)

ในคู่มือฉบับเต็มนี้คุณจะ **รับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Search** ตั้งค่าเครือข่ายการค้นหาหลายโหนด และเรียนรู้วิธี **เพิ่มไดเรกทอรีเพื่อทำดัชนี** และ **เพิ่มแอตทริบิวต์เอกสารแบบกำหนดเอง** ด้วย Java ไม่ว่าคุณจะสร้างระบบจัดการเอกสารระดับองค์กรหรือแคตาล็อกสินค้าที่ค้นหาได้ การเชี่ยวชาญขั้นตอนเหล่านี้จะทำให้คุณประเมินแพลตฟอร์มโดยไม่มีข้อจำกัดและขยายความสามารถในการค้นหาได้อย่างรวดเร็ว

## คำตอบอย่างรวดเร็ว
- **ขั้นตอนแรกในการเริ่มใช้ GroupDocs.Search คืออะไร?** รับใบอนุญาตชั่วคราวจากพอร์ทัลของ GroupDocs.  
- **รีโพซิทอรี Maven ใดที่โฮสต์ไลบรารี?** `https://releases.groupdocs.com/search/java/`.  
- **ฉันจะเพิ่มไดเรกทอรีเพื่อทำดัชนีได้อย่างไร?** เรียกเมธอด `addDirectoriesToIndex` บนโหนดหลัก.  
- **ฉันสามารถเพิ่มแอตทริบิวต์เอกสารแบบกำหนดเองได้หรือไม่?** ได้—เรียก `addAttribute` พร้อมคีย์เอกสารและชื่อแอตทริบิวต์.  
- **ฉันจะปิดโหนดอย่างปลอดภัยได้อย่างไร?** เรียก `closeNodes` เพื่อปล่อยทรัพยากร.

## ใบอนุญาตชั่วคราวคืออะไรและทำไมต้องใช้?
ใบอนุญาตชั่วคราวช่วยให้คุณประเมิน GroupDocs.Search ได้โดยไม่มีข้อจำกัดในการใช้งาน เหมาะสำหรับการพัฒนา การทดสอบ หรือโครงการพิสูจน์แนวคิดก่อนตัดสินใจซื้อเต็มรูปแบบ ใบอนุญาตให้เข้าถึงฟีเจอร์ทั้งหมดเป็นระยะเวลาจำกัด ช่วยให้คุณวัดประสิทธิภาพ ทดสอบจุดเชื่อมต่อ และตรวจสอบว่าโซลูชันตอบสนองความต้องการของคุณหรือไม่โดยไม่ต้องผูกมัดทางการเงิน

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

### ไลบรารีและการพึ่งพาที่จำเป็น
เพื่อทำงานกับ GroupDocs.Search สำหรับ Java ให้เพิ่มการพึ่งพา Maven ที่จำเป็น:
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
คุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การตั้งค่าสภาพแวดล้อม
- ตรวจสอบว่าคุณมี JDK ที่เข้ากันได้ติดตั้งอยู่ (Java 8 หรือใหม่กว่า).  
- ตั้งค่า IDE ของคุณให้รองรับโครงการ Maven.

### ความรู้พื้นฐานที่ต้องมี
ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และการจัดการโครงการ Maven จะเป็นประโยชน์ หากคุณยังใหม่กับแนวคิดเหล่านี้ ควรสำรวจแหล่งข้อมูลเบื้องต้นเพื่อเริ่มต้น

## วิธีรับใบอนุญาตชั่วคราว
ใบอนุญาตชั่วคราวจะได้รับโดยการเยี่ยมชมพอร์ทัลของ GroupDocs, กรอกแบบฟอร์มคำขอสั้น ๆ และวางไฟล์ `.lic` ที่ได้รับลงในโฟลเดอร์ `resources` ของโครงการของคุณ จากนั้นให้เริ่มต้นใบอนุญาตด้วยไม่กี่บรรทัดของโค้ด (ดูตัวอย่างด้านล่าง) สำหรับแบบฟอร์มคำขอ ให้ใช้หน้าทางการ: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## การตั้งค่า GroupDocs.Search สำหรับ Java

### ข้อมูลการติดตั้ง
เพื่อเริ่มใช้ GroupDocs.Search สำหรับ Java ในโครงการของคุณ ให้ทำตามขั้นตอน Maven ด้านบนหรือดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจากหน้าปล่อยอย่างเป็นทางการ

#### ขั้นตอนการรับใบอนุญาต
1. **Free Trial** – สำรวจฟีเจอร์ต่าง ๆ โดยไม่มีข้อผูกมัด.  
2. **Temporary License** – รับคีย์ระยะสั้นสำหรับการทดสอบ (ดูส่วนที่กล่าวถึงข้างต้น).  
3. **Purchase** – สำหรับการใช้งานในสภาพแวดล้อมการผลิต ให้ซื้อใบอนุญาตเต็มจาก **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### การเริ่มต้นและตั้งค่าพื้นฐาน
เริ่มต้นโครงการของคุณด้วย GroupDocs.Search ดังนี้:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
ขั้นตอนการเริ่มต้นนี้สำคัญเพื่อให้ทุกคอมโพเนนต์ทำงานร่วมกันอย่างราบรื่นภายในเครือข่ายการค้นหาของคุณ

## คู่มือการนำไปใช้
ต่อไปนี้เป็นการแบ่งกระบวนการเป็นส่วนย่อย ๆ ที่แต่ละส่วนมุ่งเน้นฟีเจอร์เฉพาะของการปรับใช้และจัดการโหนดเครือข่ายการค้นหา

### ฟีเจอร์ 1: การตั้งค่าการกำหนดค่า
**ภาพรวม:** การตั้งค่าการกำหนดค่าสำหรับเครือข่ายการค้นหาของคุณเป็นขั้นตอนแรกในการปรับใช้โหนด การตั้งค่านี้รวมถึงการระบุเส้นทางและพอร์ตที่สำคัญสำหรับการปรับใช้โหนด

#### ขั้นตอนการนำไปใช้:
##### ขั้นตอนที่ 1: กำหนด Base Path และ Port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### ขั้นตอนที่ 2: กำหนดค่า Search Network
ฟังก์ชัน `configureSearchNetwork` เตรียมอ็อบเจกต์การกำหนดค่าที่จำเป็นสำหรับการปรับใช้โหนด  
`Configuration` เป็นคลาสที่เก็บการตั้งค่าต่าง ๆ เช่น โฟลเดอร์ดัชนี, พอร์ตเครือข่าย, และบทบาทของโหนด  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **พารามิเตอร์:** Base path และ port ถูกใช้เพื่อค้นหาแหล่งข้อมูลและสร้างช่องทางการสื่อสาร.  
- **ค่าที่คืนกลับ:** อ็อบเจกต์ `Configuration` ที่กำหนดค่าแล้วตามความต้องการของการปรับใช้ของคุณ.

### ฟีเจอร์ 2: การปรับใช้เครือข่ายการค้นหา
**ภาพรวม:** การปรับใช้โหนดเป็นสิ่งจำเป็นสำหรับการขยายความสามารถในการค้นหาของคุณไปยังสภาพแวดล้อมหรือส่วนข้อมูลต่าง ๆ

#### ขั้นตอนการนำไปใช้:
##### ขั้นตอนที่ 1: ปรับใช้โหนด
ฟังก์ชัน `deploySearchNetwork` เริ่มต้นและคืนค่าอาร์เรย์ของโหนดเครือข่ายการค้นหา  
`SearchNetworkNodes` แทนแต่ละอินสแตนซ์ของโหนดที่เข้าร่วมคลัสเตอร์การค้นหาแบบกระจาย  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **พารามิเตอร์:** Base path, port, และ configuration ถูกใช้เพื่อกำหนดสภาพแวดล้อมการปรับใช้.  
- **ค่าที่คืนกลับ:** อาร์เรย์ที่บรรจุ `SearchNetworkNodes` ที่ถูกเริ่มต้นแล้ว.

### ฟีเจอร์ 3: การสมัครรับเหตุการณ์เครือข่าย
**ภาพรวม:** การตรวจสอบกิจกรรมของเครือข่ายการค้นหาของคุณเป็นสิ่งสำคัญเพื่อรักษาประสิทธิภาพและความน่าเชื่อถือสูงสุด

#### ขั้นตอนการนำไปใช้:
##### ขั้นตอนที่ 1: สมัครรับเหตุการณ์ของโหนดหลัก
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **วัตถุประสงค์:** ขั้นตอนนี้ทำให้คุณได้รับการแจ้งเตือนเมื่อเกิดเหตุการณ์หรือการเปลี่ยนแปลงสำคัญภายในเครือข่ายการค้นหา

### ฟีเจอร์ 4: การทำดัชนีเอกสาร
**ภาพรวม:** การเพิ่มไดเรกทอรีที่มีเอกสารเพื่อทำดัชนีช่วยให้การดึงข้อมูลมีประสิทธิภาพทั่วเครือข่ายของคุณ

#### วิธีเพิ่มไดเรกทอรีเพื่อทำดัชนี
`addDirectoriesToIndex` เป็นเมธอดช่วยเหลือที่ลงทะเบียนเส้นทางโฟลเดอร์สำหรับทำดัชนีบนโหนดหลัก  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **วัตถุประสงค์:** ช่วยให้เข้าถึงและค้นหาเอกสารทั้งหมดในไดเรกทอรีที่ระบุได้อย่างรวดเร็ว

### ฟีเจอร์ 5: การเพิ่มแอตทริบิวต์ให้กับเอกสาร
**ภาพรวม:** แอตทริบิวต์แบบกำหนดเองช่วยเสริมเมตาดาต้าเอกสาร ทำให้การค้นหามีความยืดหยุ่นและให้ข้อมูลมากขึ้น

#### วิธีเพิ่มแอตทริบิวต์เอกสารแบบกำหนดเอง
`addAttribute` เพิ่มแอตทริบิวต์เมตาดาต้าแบบกำหนดเองให้กับเอกสารที่ระบุในดัชนี  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **พารามิเตอร์:** ระบุโหนด, คีย์เอกสาร, และแอตทริบิวต์ที่จะเพิ่ม.  
- **วัตถุประสงค์:** ขยายความสามารถในการค้นหาโดยเพิ่มเมตาดาต้าเพิ่มเติมให้กับเอกสาร

### ฟีเจอร์ 6: การดึงเอกสารที่ทำดัชนีแล้ว
**ภาพรวม:** ดึงและแสดงรายการเอกสารที่ทำดัชนีอย่างมีประสิทธิภาพเพื่อให้มั่นใจว่าข้อมูลครบถ้วนและถูกต้อง

#### ขั้นตอนการนำไปใช้:
##### ขั้นตอนที่ 1: ดึงเอกสารที่ทำดัชนี
```java
getIndexedDocuments(nodes[0]);
```  
- **วัตถุประสงค์:** ตรวจสอบว่าการทำดัชนีของเอกสารทั้งหมดที่จำเป็นในเครือข่ายการค้นหาของคุณสำเร็จแล้ว

### ฟีเจอร์ 7: การปิดโหนดเครือข่าย
**ภาพรวม:** การปิดโหนดอย่างถูกต้องเป็นสิ่งสำคัญสำหรับการจัดการทรัพยากรและป้องกันการรั่วไหลของหน่วยความจำ

#### ขั้นตอนการนำไปใช้:
##### ขั้นตอนที่ 1: ปิดโหนดทั้งหมด
`closeNodes` ปิดการทำงานของโหนดการค้นหาที่ใช้งานอยู่ทั้งหมดและปล่อยทรัพยากรที่จัดสรรไว้  
```java
closeNodes(nodes);
```  
- **วัตถุประสงค์:** ปล่อยทรัพยากรที่โหนดแต่ละตัวครอบครองอยู่ เพื่อให้กระบวนการปิดทำงานอย่างสะอาด

## ทำไมต้องใช้ใบอนุญาตชั่วคราวสำหรับ GroupDocs.Search?
ใบอนุญาตชั่วคราวให้ **การเข้าถึงฟีเจอร์เต็มรูปแบบเป็นเวลา 30 วัน** และรองรับเอกสารทำดัชนีสูงสุด **50,000 เอกสาร** โดยไม่มีการจำกัดประสิทธิภาพ สิ่งนี้ช่วยให้คุณวัดความเร็วการทำดัชนี, ความหน่วงของการค้นหา, และความสามารถในการขยายตัวบนข้อมูลจริงก่อนตัดสินใจซื้อใบอนุญาตการผลิต อีกทั้งยังลบลายน้ำการประเมินผลออก ทำให้คุณเห็นภาพความสามารถของผลิตภัณฑ์อย่างแท้จริง

## กรณีการใช้งานทั่วไป
1. **Enterprise Document Management** – ทำดัชนีไฟล์ภายในหลายล้านไฟล์ข้ามแผนก เพื่อให้ค้นหาแบบเต็มข้อความได้ทันที.  
2. **E‑commerce Platforms** – สร้างแคตาล็อกสินค้าที่ค้นหาได้ซึ่งครอบคลุมคลังสินค้าหลายแห่งและฟีดจากบุคคลที่สาม.  
3. **Legal Firms** – จัดระเบียบไฟล์คดี, สัญญา, และหลักฐานด้วยเมตาดาต้าแบบกำหนดเองเพื่อการดึงข้อมูลอย่างรวดเร็ว.

ความเป็นไปได้ในการบูรณาการกับระบบอื่น ๆ รวมถึงแพลตฟอร์ม CRM, ระบบจัดการเนื้อหา (CMS), และเครื่องมือวิเคราะห์ข้อมูล โดยใช้คุณสมบัติการทำดัชนีและการค้นหาที่แข็งแกร่งของ GroupDocs.Search สำหรับ Java

## พิจารณาด้านประสิทธิภาพ
เพื่อเพิ่มประสิทธิภาพเมื่อใช้ GroupDocs.Search สำหรับ Java:
- **Optimize Configuration** – ปรับแต่งการตั้งค่าให้สอดคล้องกับสภาพแวดล้อมการปรับใช้ของคุณ.  
- **Monitor Resource Usage** – ตรวจสอบ CPU, หน่วยความจำ, และ I/O อย่างสม่ำเสมอเพื่อป้องกันคอขวดหรือการรั่วไหลของหน่วยความจำ.  
- **Follow Best Practices** – ปฏิบัติตามแนวทางการจัดการหน่วยความจำของ Java เพื่อให้ใช้ทรัพยากรระบบอย่างมีประสิทธิภาพ.

## คำถามที่พบบ่อย

**Q: ใบอนุญาตชั่วคราวมีอายุการใช้งานนานแค่ไหน?**  
A: ใบอนุญาตชั่วคราวมักมีอายุ 30 วัน ให้คุณมีเวลาพอเพียงในการประเมินผลิตภัณฑ์.

**Q: ฉันสามารถเปลี่ยนจากใบอนุญาตชั่วคราวเป็นใบอนุญาตเต็มได้โดยไม่ต้องติดตั้งใหม่หรือไม่?**  
A: ได้—เพียงแทนที่ไฟล์ใบอนุญาตชั่วคราวด้วยไฟล์ใบอนุญาตเต็มและรีสตาร์ทแอปพลิเคชันของคุณ.

**Q: ฉันต้องทำการทำดัชนีเอกสารใหม่หลังจากใช้ใบอนุญาตใหม่หรือไม่?**  
A: ไม่จำเป็น ดัชนียังคงอยู่; ใบอนุญาตมีผลต่อสิทธิ์การใช้งานเท่านั้น.

**Q: จะเกิดอะไรขึ้นหากฉันลืมปิดโหนด?**  
A: ทรัพยากรที่ไม่ได้ปล่อยอาจทำให้เกิดการรั่วไหลของหน่วยความจำ; ควรเรียก `closeNodes` ทุกครั้งเมื่อปิดระบบ.

**Q: สามารถเพิ่มแอตทริบิวต์แบบกำหนดเองได้มากกว่าหนึ่งรายการต่อเอกสารหรือไม่?**  
A: แน่นอน—เรียก `addAttribute` หลายครั้งพร้อมชื่อแอตทริบิวต์ที่แตกต่างกัน.

**Last Updated:** 2026-07-02  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs

## บทเรียนที่เกี่ยวข้อง

- [Deploy a Search Network Node in .NET using GroupDocs for Efficient Document Indexing and Retrieval](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [How to Implement a Search Network with GroupDocs.Search in .NET for Document Management Systems](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configuring Aspose.Search Network & Adding Document Attributes with GroupDocs.Redaction for .NET: A Comprehensive Guide](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
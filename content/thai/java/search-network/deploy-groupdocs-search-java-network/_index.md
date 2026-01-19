---
date: '2026-01-19'
description: เรียนรู้วิธีกำหนดค่าการค้นหาแบบกระจายและปรับใช้เครือข่ายการค้นหาที่มีประสิทธิภาพโดยใช้
  GroupDocs.Search สำหรับ Java เพื่อเพิ่มประสิทธิภาพและความสามารถในการขยายตัว
keywords:
- GroupDocs.Search Java network
- search performance enhancement
- distributed search architecture
title: ตั้งค่าการค้นหาแบบกระจายด้วย GroupDocs.Search Java Network
type: docs
url: /th/java/search-network/deploy-groupdocs-search-java-network/
weight: 1
---

สนทแนะนำนี้จะพาคุณสดงวิธี **how to deploy search** บนหลายโหนด การเพิ่มเอกสารลงในดัชนี และ **configure TCP settings** เพื่อการสื่อสารที่เชื่อถือได้ เมื่อเสร็จสิ้น คุณจะมีโซลูชันการค้นหาที่สามารถขยายได้พร้อมใช้งานในสภาพแวดล้อมการผลิต

## คำตอบอย่างรวดเร็ว
- **What is configure distributed search?** เป็นกระบวนการตั้งค่าโหนดการค้นหาหลายโหนดที่ทำงานร่วมกันเพื่อทำการจัดทำดัชนีและสอบถามข้อมูลอย่างมีประสิทธิภาพ  
- **How many nodes are recommended?** โดยทั่วไป 3‑5 โหนดให้สมดุลที่ดีระหว่างประสิทธิภาพและความทนต่อข้อผิดพลาด  
- **Do I need a license?** ใช่ – จำเป็นต้องมีใบอนุญาตชั่วคราวหรือเต็มรูปแบบสำหรับการใช้งานในสภาพแวดล้อมการผลิต  
- **Which ports should I use?** เลือกพอร์ตที่ว่างอยู่บนเซิร์ฟเวอร์ของคุณ; ตัวอย่างใช้พอร์ต 49136‑49139  
- **Can I add new documents after deployment?** แน่นอน – คุณสามารถ **add documents to index** ได้ตลอดเวลาโดยไม่ต้องรีสตาร์ทเครือข่าย

## configure distributed search คืออะไร?
การกำหนดค่าโครงสร้างการค้นหาแบบกระจายหมายถึงการเชื่อมต่อโหนดการค้นหาหลายโหนดที่ทำงานอิสระให้ร่วมกันแบ่งงานจัดทำดัชนีและตอบคำถามร่วมกัน สิ่งนี้ช่วยลดภาระบนเครื่องเดียวและเพิ่มอัตราการทำงานรวมทั้งความน่าเชื่อถือ

## ทำไมต้องใช้ GroupDocs.Search for Java?
- **High performance** – การทำงานแบบเนทีฟของ Java ปรับแต่งความเร็วการทำดัชนีให้สูงสุด  
- **Scalable design** – สามารถเพิ่มหรือลบโหนดได้โดยไม่ต้องทำการกำหนดค่าใหม่อย่างใหญ่โต  
- **Rich document support** – รองรับไฟล์ PDF, Word, อีเมลและรูปแบบอื่น ๆ มากมาย  
- **Simple TCP communication** – `TcpSettings` ที่มาพร้อมในตัวช่วยให้คุณปรับแต่งความหน่วงของเครือข่ายได้ละเอียด

## ข้อกำหนดเบื้องต้น

### ไลบรารีและการพึ่งพาที่จำเป็น
คุณจะต้องใช้ **GroupDocs.Search for Java** เวอร์ชัน 25.4 หรือใหม่กว่า ตรวจสอบให้แน่ใจว่ามี Java ติดตั้งในสภาพแวดล้อมการพัฒนาของคุณ

### ความต้องการการตั้งค่าสภาพแวดล้อม
- ติดตั้ง Java Development Kit (JDK) บนเครื่องของคุณ  
- มี IDE เช่น IntelliJ IDEA หรือ Eclipse  

### ความรู้เบื้องต้นที่จำเป็น
ทักษะการเขียนโปรแกรม Java เบื้องต้นและความเข้าใจทั่วไปเกี่ยวกับการกำหนดค่าเครือข่ายจะช่วยให้คุณทำตามขั้นตอนได้อย่างราบรื่น

## การตั้งค่า GroupDocs.Search for Java
เพื่อเริ่มต้น ให้เพิ่ม GroupDocs.Search for Java ลงในโปรเจกต์ของคุณ คุณสามารถทำได้ง่าย ๆ ผ่าน Maven หรือโดยการดาวน์โหลดไลบรารีโดยตรง

**Maven Setup**  
เพิ่ม repository และการกำหนด dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

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

**Direct Download**  
หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดจาก [การปล่อย GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)

### การรับใบอนุญาต
เพื่อใช้ GroupDocs.Search อย่างเต็มที่ คุณสามารถขอรับใบอนุญาตชั่วคราวหรือซื้อใบอนุญาตได้ เยี่ยมชม [หน้าลิขสิทธิ์ของ GroupDocs](https://purchase.groupdocs.com/temporary-license/) เพื่อดูข้อมูลเพิ่มเติมเกี่ยวกับการรับทดลองใช้ฟรีหรือใบอนุญาตเต็มรูปแบบ

### การเริ่มต้นและการตั้งค่าเบื้องต้น
มาทำการเริ่มต้น GroupDocs.Search ในแอปพลิเคชัน Java ของคุณ:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        // Add documents to the index
        index.add("YOUR_DOCUMENT_DIRECTORY");
    }
}
```

## คู่มือการใช้งาน
ในส่วนนี้ เราจะพาคุณผ่านขั้นตอนการกำหนดค่าและการปรับใช้เครือข่ายการค้นหาโดยใช้ GroupDocs.Search for Java

### วิธีการ configure distributed search ด้วย GroupDocs.Search
การปรับใช้หลายโหนดในสถาปัตยกรรมการค้นหาของคุณช่วยให้ทำการจัดทำดัชนีและการค้นหาแบบกระจายได้ ส่งผลให้ประสิทธิภาพและความสามารถในการขยายเพิ่มขึ้น คู่มือนี้จะแสดงวิธีการกำหนดค่าโหนดเหล่านี้อย่างมีประสิทธิภาพ

#### การกำหนดค่าเครือข่าย
เริ่มต้นด้วยการตั้งค่าการกำหนดค่าพร้อมฐานพาธและพอร์ต ขั้นตอนนี้ยัง **configures TCP settings** ที่กำหนดวิธีการสื่อสารระหว่างโหนด:

```java
Configuration configuration = ConfiguringSearchNetwork.configure("YOUR_DOCUMENT_DIRECTORY", 49136);
```

#### การปรับใช้โหนด
ต่อไป ปรับใช้โหนดเครือข่ายการค้นหาโดยใช้การตั้งค่าที่กำหนดไว้:

```java
public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
    // Define timeouts for sending and receiving data over the network.
    int sendTimeout = 3000;
    int receiveTimeout = 3000;

    // Create and start three nodes that can run on separate servers or together.
    SearchNetworkNode node1 = new SearchNetworkNode(
        1,
        basePath + "Node1",
        new TcpSettings(basePort + 1, sendTimeout, receiveTimeout)
    );
    node1.start();

    SearchNetworkNode node2 = new SearchNetworkNode(
        2,
        basePath + "Node2",
        new TcpSettings(basePort + 2, sendTimeout, receiveTimeout)
    );
    node2.start();

    SearchNetworkNode node3 = new SearchNetworkNode(
        3,
        basePath + "Node3",
        new TcpSettings(basePort + 3, sendTimeout, receiveTimeout)
    );
    node3.start();

    // Create and configure the main configuration node.
    SearchNetworkNode node0 = new SearchNetworkNode(
        0,
        basePath + "Node0",
        new TcpSettings(basePort, sendTimeout, receiveTimeout),
        new ConsoleLogger(),
        configuration
    );

    // Add an event handler to notify when the configuration is complete.
    node0.getEvents().ConfigurationCompleted.add(new EventHandler() {
        @Override
        public void invoke(Object s, EventArgs e) {
            // Event handling logic here (e.g., logging)
        }
    });

    // Configure all nodes in the network using the main configuration node.
    node0.configureAllNodes();

    // Start the search network by launching all configured nodes.
    node0.start();

    // Return an array of all deployed nodes.
    return new SearchNetworkNode[] {node0, node1, node2, node3};
}
```

### เคล็ดลับการแก้ไขปัญหา
- ตรวจสอบให้แน่ใจว่าไดเรกทอรีของแต่ละโหนดระบุอย่างถูกต้องและเข้าถึงได้  
- ตรวจสอบการกำหนดค่าเครือข่าย โดยเฉพาะการตั้งค่าพอร์ต เพื่อป้องกันความขัดแย้ง  
- ตรวจสอบบันทึก (logs) เพื่อหาข้อผิดพลาดหรือคำเตือนในการกำหนดค่า  

## การประยุกต์ใช้งานจริง
การปรับใช้เครือข่ายการค้นหาแบบกระจายสามารถเป็นประโยชน์ในหลายสถานการณ์:

1. **Large‑Scale Enterprise Systems** – ปรับปรุงการค้นหาในคลังเอกสารขนาดใหญ่ขององค์กร  
2. **Content Management Platforms** – เพิ่มประสิทธิภาพบนเว็บไซต์ที่มีการเข้าชมสูงและข้อมูลจำนวนมหาศาล  
3. **E‑commerce Websites** – เร่งการค้นหาผลิตภัณฑ์เพื่อประสบการณ์ลูกค้าที่ราบรื่น  

## การพิจารณาด้านประสิทธิภาพ
เพื่อให้สภาพแวดล้อม **configure distributed search** ของคุณทำงานอย่างมีประสิทธิภาพ:

- อัปเดตดัชนีเป็นประจำเพื่อสะท้อนการเปลี่ยนแปลงของข้อมูล  
- ตรวจสอบการใช้ CPU, หน่วยความจำและดิสก์; ปรับค่า timeout ของ `TcpSettings` หากจำเป็น  
- ใช้ flag การปรับจูนหน่วยความจำของ Java (`-Xmx`, `-Xms`) ตามภาระงาน  

## สรุป
โดยทำตามบทแนะนำนี้ คุณconfigure distributed search** และปรับใช้เครือข่าย GroupDocs.Search Java ที่สามารถขยายได้ โซลูชันนี้สามารถเพิ่มิเคชันของคุณอย่างมาก

### ขั้นตอนต่อไป
สำรวจคุณลักษณะดของคุณวันนี้และสัมผัสการเพิ่มประสิทธิภาพอย่างชัดเจน!

## ส่วนคำถามที่พบบ่อย
**Q1: GroupDocs.Search for Java คืออะไร?**  
A1: GroupDocs.Search for Java เป็นไลบรารีที่ทรงพลังสำหรับการค้นหาข้อความในรูปแบบเอกสารต่าง ๆ ทำให้สามารถจัดทำดัชนีและสอบถามข้อมูลได้อย่างมีประสิทธิภาพ

**Q2: ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ GroupDocs.Search ได้อย่างไร?**  
A2: เยี่ยมชม [หน้าลิขสิทธิ์ของ GroupDocs](https://purchase.groupdocs.com/temporary-license/) เพื่อรับการทดลองใช้งานฟรีหรือใบอนุญาตเต็มรูปแบบ

**Q3: การกำหนดค่าเครือข่ายนี้สามารถใช้กับประเภทเอกสารอื่นได้หรือไม่?**  
A3: ใช่, GroupDocs.Search รองรับรูปแบบเอกสารหลากหลาย ทำให้สามารถนำไปใช้กับกรณีการใช้งานต่าง ๆ ได้อย่างยืดหยุ่น

**Q4: ปัญหาที่พบบ่อยเมื่อปรับใช้โหนดมีอะไรบ้าง?**  
A4: ปัญหาที่พบบ่อยรวมถึงไดเรกทอรีที่กำหนดไม่ถูกต้อง, ความขัดแย้งของพอร์ต, และสิทธิ์การเข้าถึงที่ไม่เพียงพอ ตรวจสอบให้แน่ใจว่าการตั้งค่าทั้งหมดถูกต้องเพื่อหลีกเลี่ยงปัญหาเหล่านี้

---

**Last Updated:** 2026-01-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
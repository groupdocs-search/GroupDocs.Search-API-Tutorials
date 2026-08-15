---
date: '2026-08-15'
description: เรียนรู้วิธีปรับปรุงความหน่วงของการค้นหาโดยใช้คุณสมบัติการทำดัชนีขั้นสูงของ
  GroupDocs.Search สำหรับ Java รวมถึง cancellation, async operations, multithreading,
  และ metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: ปรับปรุงความหน่วงของการค้นหาโดยใช้ GroupDocs.Search สำหรับ Java ด้วยการใช้
  cancellation, asynchronous indexing, multithreading, และ metadata customization.
  เพิ่มประสิทธิภาพและลดการใช้ทรัพยากร.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: ปรับปรุงความหน่วงของการค้นหาโดยใช้การทำดัชนีขั้นสูงใน GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: ปรับปรุงความหน่วงของการค้นหาโดยใช้การทำดัชนีขั้นสูงใน GroupDocs
type: docs
url: /th/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# ปรับปรุงความหน่วงของการค้นหาด้วยการทำดัชนีขั้นสูงใน GroupDocs

ในสภาพแวดล้อมดิจิทัลที่เร็วแรงในปัจจุบัน, **improve search latency** มีความสำคัญสำหรับการส่งมอบผลลัพธ์ทันทีให้กับผู้ใช้ ไม่ว่าคุณจะสร้างเครื่องมือค้นหาแบบกำหนดเองหรือปรับปรุงระบบจัดการเอกสารที่มีอยู่ กลยุทธ์การทำดัชนีที่เหมาะสมสามารถลดความหน่วงอย่างมาก, ลดการใช้ทรัพยากร, และ **improve search latency** ในทุกด้าน ในบทแนะนำนี้เราจะพาไปดูคุณสมบัติที่ทรงพลังที่สุดของ GroupDocs.Search สำหรับ Java — การยกเลิก, การทำดัชนีแบบอะซิงโครนัส, การทำงานหลายเธรด, และการปรับแต่งเมตาดาต้า — เพื่อให้คุณสามารถ **add documents to index** ได้เร็วและมีประสิทธิภาพมากขึ้น.

**สิ่งที่คุณจะได้เรียนรู้**

- วิธียกเลิกการทำดัชนีหลังจากระยะเวลาที่กำหนด  
- การดำเนินการทำดัชนีแบบอะซิงโครนัสและการจัดการการเปลี่ยนแปลงสถานะ  
- การกำหนดค่าการทำงานหลายเธรดเพื่อการทำดัชนีที่เร็วขึ้น  
- ปรับแต่งตัวเลือกการทำดัชนีเมตาดาต้าเพื่อ **customize search metadata**  

ให้แน่ใจว่าคุณมีทุกอย่างที่ต้องการก่อนที่เราจะลงลึกไปในโค้ด.

## คำตอบอย่างรวดเร็ว
- **การยกเลิกทำอะไร?** มันหยุดการทำดัชนีหลังจากเวลาที่กำหนด, ปล่อย CPU และหน่วยความจำให้กับงานอื่น ๆ  
- **ฉันสามารถทำดัชนีเอกสารแบบอะซิงโครนัสได้หรือไม่?** ใช่ – เปิดใช้งานด้วย `options.setAsync(true)`  
- **ฉันสามารถใช้เธรดได้กี่ตัว?** จำนวนเต็มบวกใดก็ได้; 2‑4 เธรดเป็นค่าปกติสำหรับเซิร์ฟเวอร์ส่วนใหญ่  
- **การทำดัชนีเมตาดาต้าเป็นทางเลือกหรือไม่?** แน่นอน – คุณสามารถเปิดหรือปรับแต่งตามฟิลด์ได้  
- **ฉันต้องการไลเซนส์สำหรับคุณลักษณะเหล่านี้หรือไม่?** การทดลองใช้งานทำงานสำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง

## ข้อกำหนดเบื้องต้น

- **GroupDocs.Search library** – เวอร์ชัน 25.4 หรือใหม่กว่า.  
- **Java Development Environment** – JDK 8 หรือสูงกว่าแนะนำ.  
- ความคุ้นเคยพื้นฐานกับ Java และแนวคิดของการทำดัชนี

### การตั้งค่า GroupDocs.Search สำหรับ Java

#### การติดตั้ง Maven

เพิ่ม repository และ dependency ไปยังไฟล์ `pom.xml` ของคุณ:

การกำหนดค่า `pom.xml` บอก Maven ว่า artifacts ของ GroupDocs.Search ใดที่จะดาวน์โหลดและรวมในโปรเจกต์ของคุณ.

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

#### ดาวน์โหลดโดยตรง

หรือดาวน์โหลด JAR ล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License acquisition** – เริ่มต้นด้วยการทดลองฟรีหรือขอไลเซนส์ชั่วคราวเพื่อปลดล็อกชุดคุณลักษณะทั้งหมด.

### การเริ่มต้นและตั้งค่าเบื้องต้น

คลาส `SearchIndex` เป็นจุดเริ่มต้นที่แสดงถึงดัชนีที่สามารถค้นหาได้ซึ่งจัดเก็บบนดิสก์หรือในหน่วยความจำ.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## “optimize search performance” คืออะไรในบริบทนี้?

การปรับประสิทธิภาพการค้นหาหมายถึงการกำหนดค่ากระบวนการทำดัชนีให้ใช้ CPU, หน่วยความจำ, และเวลาในระดับที่เหมาะสมขณะส่งมอบผลลัพธ์ที่เกี่ยวข้องที่สุดโดยทันที การควบคุมการยกเลิก, การทำงานแบบอะซิงโครนัส, การทำงานหลายเธรด, และการจัดการเมตาดาต้าช่วยให้คุณมีอิทธิพลโดยตรงต่อความเร็วที่เอนจินสามารถ **add documents to index** และตอบสนองต่อคำค้นหา

## ทำไมต้องใช้คุณสมบัติการทำดัชนีขั้นสูง?

การทำดัชนีแบบอะซิงโครนัสและหลายเธรดทำให้แอปพลิเคชันของคุณตอบสนองได้ดีขึ้น, ในขณะที่การยกเลิกช่วยป้องกันกระบวนการทำงานที่ใช้เวลานานเกินไป ตัวเลือกเมตาดาต้าที่ปรับแต่งได้ช่วยให้คุณแสดงข้อมูลสำคัญที่สุด, ซึ่งโดยตรง **improve search latency** สำหรับผู้ใช้สุดท้าย นอกจากนี้คุณลักษณะเหล่านี้ยังลดการกระตุ้น CPU, ลดแรงกดดันหน่วยความจำ, และทำให้การขยายขนาดเป็นไปอย่างราบรื่นเมื่อจัดการกับปริมาณเอกสารจำนวนมาก

## วิธีปรับปรุงความหน่วงของการค้นดาด้วยการทำดัชนีขั้นสูง?

โหลดอินสแตนซ์ `SearchIndex` ของคุณ, กำหนดค่า `IndexingOptions` ด้วยการยกเลิก, การทำงานแบบอะซิงโครนัส, และการตั้งค่าเธรด, จากนั้นเรียก `index.add(document)` — การผสมผสานนี้ลดเวลาการทำดัชนีโดยรวมได้ถึง 60 % ในภาระงานทั่วไปและรับประกันว่างานที่ใช้เวลานานจะไม่บล็อกการทำงานอื่น ๆ คุณยังสามารถปรับขีดจำกัดการทำดัชนีเมตาดาต้าและตรวจสอบความคืบหน้าผ่านเหตุการณ์การเปลี่ยนแปลงสถานะเพื่อให้แน่ใจว่ากระบวนการอยู่ในขอบเขตของงบประมาณประสิทธิภาพ

## คู่มือการใช้งาน

### คุณสมบัติการยกเลิก

**Overview** – ยกเลิกการทำดัชนีหลังจากระยะเวลาที่กำหนดเพื่อหลีกเลี่ยงการใช้ทรัพยากรเกิน

#### ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อม

สร้างอินสแตนซ์ `SearchIndex` ที่ชี้ไปยังโฟลเดอร์ดัชนีของคุณ.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### ขั้นตอนที่ 2: สร้างตัวเลือกการทำดัชนีพร้อมการยกเลิก

`IndexingOptions` ให้คุณระบุพฤติกรรมของเครื่องมือทำดัชนี.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**จุดสำคัญ**

- `setCancellation()` เปิดใช้งานฟีเจอร์  
- `cancelAfter(int milliseconds)` กำหนดเวลาจำกัด (3 วินาทีในตัวอย่างนี้)

### คุณสมบัติแบบอะซิงโครนัส

**Overview** – รันการทำดัชนีบนเธรดพื้นหลังและฟังเหตุการณ์การเปลี่ยนแปลงสถานะ

#### ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อม

สร้างอินสแตนซ์ดัชนีและเตรียมคอลเลกชันเอกสาร.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### ขั้นตอนที่ 2: สมัครรับเหตุการณ์ status‑changed

เหตุการณ์ `StatusChanged` จะบอกคุณเมื่องานทำดัชนีเปลี่ยนสถานะ

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### ขั้นตอนที่ 3: กำหนดค่าตัวเลือกแบบอะซิงโครนัส

เปิดโหมด async เพื่อให้การเรียกคืนค่าโดยทันทีและการประมวลผลดำเนินต่อในพื้นหลัง.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### คุณสมบัติของเธรด

**Overview** – เร่งความเร็วการทำดัชนีโดยใช้หลายคอร์ของ CPU

#### ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อม

เตรียมดัชนีและตรวจสอบว่า JVM มีหน่วยความจำ heap เพียงพอ

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### ขั้นตอนที่ 2: กำหนดค่าการทำงานหลายเธรด

ตั้งจำนวนเธรดทำงาน; แต่ละเธรดจะประมวลผลส่วนย่อยของเอกสาร

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### คุณสมบัติของตัวเลือกการทำดัชนีเมตาดาต้า

**Overview** – ปรับแต่งให้ละเอียดว่าเมตาดาต้าเอกสารใดจะถูกทำดัชนีและเก็บอย่างไร

#### ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อม

โหลดเอกสารที่มีฟิลด์เมตาดาต้าเช่นผู้เขียน, ชื่อเรื่อง, และแท็กกำหนดเอง

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### ขั้นตอนที่ 2: กำหนดค่าตัวเลือกเมตาดาต้า

`MetadataIndexingOptions` ให้คุณเปิดหรือปิดฟิลด์เมตาดาต้าแต่ละฟิลด์และกำหนดขีดจำกัดขนาด

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## การประยุกต์ใช้ในทางปฏิบัติ

1. **Document management systems** – ใช้การทำดัชนีแบบอะซิงโครนัสเพื่อให้ UI ตอบสนองได้ขณะประมวลผลชุดใหญ่ในพื้นหลัง.  
2. **Content search engines** – ใช้การยกเลิกเพื่อป้องกันงานที่ใช้เวลานานเกินไปจากการกินทรัพยากรเซิร์ฟเวอร์ในช่วงเวลาที่มีการใช้งานสูง.  
3. **Large‑scale ingestion pipelines** – ใช้การทำงานหลายเธรดเพื่อ **add documents to index** ในระดับใหญ่, ลดเวลาการประมวลผลอย่างมหาศาล.  

## การพิจารณาด้านประสิทธิภาพ

- **Thread management** – ตรวจสอบการใช้ CPU; เธรดจำนวนมากเกินไปอาจทำให้เกิดค่าใช้จ่ายจากการสลับคอนเท็กซ์.  
- **Memory footprint** – ขีดจำกัดเมตาดาต้า (เช่น `setMaxBytesToIndexField`) ช่วยให้การใช้หน่วยความจำคาดเดาได้.  
- **Garbage collection** – ใช้แฟล็ก JVM ที่เหมาะสม (`-Xmx`, `-XX:+UseG1GC`) เมื่อทำดัชนีคอร์ปัสขนาดใหญ่.  

## ปัญหาทั่วไปและวิธีแก้ไข

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| การทำดัชนีไม่เคยเสร็จสิ้น | การตั้งค่าการยกเลิกต่ำเกินไป | เพิ่มค่าของ `cancelAfter` หรือเอาการยกเลิกออกสำหรับงานที่ยาว |
| ไม่มีการอัปเดตสถานะในโหมดอะซิงโครนัส | ตัวจัดการเหตุการณ์ไม่ได้เชื่อมต่ออย่างถูกต้อง | ตรวจสอบว่าได้เรียก `index.getEvents().StatusChanged.add(...)` ก่อน `index.add` |
| ข้อผิดพลาด Out‑of‑memory | จำนวนเธรดมากเกินไปหรือขีดจำกัดเมตาดาต้าสูง | ลดค่า `options.setThreads` และลดขีดจำกัดฟิลด์เมตาดาต้า |
| เมตาดาต้าขาดหายในผลลัพธ์ | การทำดัชนีเมตาดาต้าถูกปิด | ตรวจสอบว่า `options.getMetadataIndexingOptions()` ถูกกำหนดค่าและไม่ได้ตั้งค่าให้ละเว้นฟิลด์ |

## คำถามที่พบบ่อย

**Q: How do I obtain a temporary license for GroupDocs.Search?**  
A: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) and follow the on‑screen instructions.

**Q: Can I cancel an indexing operation midway through?**  
A: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()` programmatically.

**Q: What are some use cases for asynchronous indexing?**  
A: Real‑time document retrieval, background batch processing, and UI‑responsive applications benefit from async indexing.

**Q: Is it safe to increase the thread count on a shared server?**  
A: Increase gradually and monitor CPU load; on heavily shared environments, keep the thread count modest (2‑4).

**Q: How does metadata indexing affect search relevance?**  
A: Properly indexed metadata (author, creation date, tags) can be weighted higher in queries, improving result accuracy.

## สรุป

โดยการนำคุณลักษณะขั้นสูงของ GroupDocs.Search สำหรับ Java ไปใช้, คุณจะ **improve search latency** ในหลายสถานการณ์ — ตั้งแต่การรับเอกสารอย่างรวดเร็วจนถึงการควบคุมเมตาดาต้าอย่างละเอียด ทดลองปรับแต่งค่าต่าง ๆ, ตรวจสอบการใช้ทรัพยากร, และปรับให้เหมาะกับภาระงานของคุณเพื่อให้ได้ผลลัพธ์ที่ดีที่สุด.

---

**อัปเดตล่าสุด:** 2026-08-15  
**ทดสอบด้วย:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [ปรับปรุงประสิทธิภาพการค้นหาด้วย GroupDocs.Search Java: ปรับแต่งดัชนีและการค้นหา](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [วิธีเพิ่มเอกสารลงดัชนีด้วยการทำดัชนีเมตาดาต้าใน Java โดยใช้ GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [วิธีเพิ่มหลาย Alias และเพิ่มเอกสารลงดัชนีใน GroupDocs.Search สำหรับ Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
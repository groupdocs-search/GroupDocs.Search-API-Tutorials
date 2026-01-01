---
date: '2025-12-29'
description: เรียนรู้วิธีเพิ่มประสิทธิภาพการค้นหาโดยใช้คุณสมบัติการทำดัชนีขั้นสูงของ
  GroupDocs.Search สำหรับ Java รวมถึงการยกเลิก, การทำงานแบบอะซิงโครนัส, การทำงานหลายเธรด,
  และการปรับแต่งเมตาดาต้า.
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: เพิ่มประสิทธิภาพการค้นหาด้วยเทคนิคการทำดัชนีขั้นสูงใน GroupDocs.Search สำหรับ
  Java
type: docs
url: /th/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# ปรับประสิทธิภาพการค้นหาด้วยเทคนิคการทำดัชนีขั้นสูงใน GroupDocs.Search สำหรับ Java

ในสภาพแวดล้อมดิจิทัลที่เร็วเปรี้ยงพร่าในวันนี้, **optimizing search performance** มีความสำคัญต่อการให้ผลลัพธ์ทันทีแก่ผู้ใช้ ไม่ว่าคุณจะกำลังสร้างเครื่องมือค้นหาแบบกำหนดเองหรือปรับปรุงระบบจัดการเอกสารที่มีอยู่ กลยุทธ์การทำดัชนีที่เหมาะสมสามารถลดความหน่วงและการใช้ทรัพยากรได้อย่างมาก ในบทแนะนำนี้เราจะพาคุณไปสำรวจคุณลักษณะที่ทรงพลังที่สุดของ GroupDocs.Search สำหรับ Java—cancellation, asynchronous indexing, multi‑threading, และ metadata customization—เพื่อให้คุณสามารถ **add documents index** ได้เร็วและมีประสิทธิภาพมากขึ้น.

**What You’ll Learn**

- วิธียกเลิกการทำดัชนีหลังจากระยะเวลาที่กำหนด
- การทำดัชนีแบบอะซิงโครนัสและจัดการการเปลี่ยนแปลงสถานะ
- การกำหนดค่า multi‑threading เพื่อเร่งความเร็วการทำดัชนี
- การปรับแต่งตัวเลือกการทำดัชนีเมตาดาต้า

ให้แน่ใจว่าคุณมีทุกอย่างที่ต้องการก่อนที่เราจะลงลึกในโค้ด

## Prerequisites

- **GroupDocs.Search Library** – เวอร์ชัน 25.4 หรือใหม่กว่า  
- **Java Development Environment** – แนะนำให้ใช้ JDK 8 หรือสูงกว่า  
- ความคุ้นเคยพื้นฐานกับ Java และแนวคิดการทำดัชนี

### Setting Up GroupDocs.Search for Java

#### Maven Installation

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

Alternatively, download the latest JAR from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition** – เริ่มต้นด้วยการทดลองใช้ฟรีหรือขอรับใบอนุญาตชั่วคราวเพื่อเปิดใช้งานคุณสมบัติทั้งหมด

### Basic Initialization and Setup

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

## Quick Answers
- **What does cancellation do?** หยุดการทำดัชนีหลังจากเวลาที่กำหนดเพื่อปลดปล่อยทรัพยากร  
- **Can I index documents asynchronously?** ใช่ – ตั้งค่า `options.setAsync(true)`  
- **How many threads can I use?** จำนวนเต็มบวกใดก็ได้; ค่าที่นิยมใช้คือ 2‑4 สำหรับเซิร์ฟเวอร์ส่วนใหญ่  
- **Is metadata indexing optional?** แน่นอน – คุณสามารถเปิดหรือปรับจูนตามฟิลด์ได้  
- **Do I need a license for these features?** การทดลองใช้ทำงานได้สำหรับการทดสอบ; ต้องมีใบอนุญาตเต็มสำหรับการใช้งานจริง

## What Is “Optimize Search Performance” in This Context?

การปรับประสิทธิภาพการค้นหาหมายถึงการกำหนดค่ากระบวนการทำดัชนีให้ใช้ CPU, หน่วยความจำ, และเวลาในระดับที่เหมาะสมพร้อมกับให้ผลลัพธ์ที่เกี่ยวข้องที่สุดโดยทันที การควบคุม cancellation, การทำงานแบบ async, การใช้ threading, และการจัดการเมตาดาต้าช่วยให้คุณมีอิทธิพลโดยตรงต่อความเร็วที่ engine สามารถ **add documents index** และตอบสนองต่อคำค้นได้

## Why Use Advanced Indexing Features?

- **Reduced latency** – การทำดัชนีแบบอะซิงโครนัสและมัลติ‑เธรดทำให้แอปพลิเคชันของคุณตอบสนองได้ดีขึ้น  
- **Better resource management** – Cancellation ป้องกันกระบวนการที่ใช้ทรัพยากรเกินจำเป็น  
- **Tailored search relevance** – ตัวเลือกเมตาดาต้าช่วยให้คุณแสดงข้อมูลสำคัญที่สุดออกมา  

## Implementation Guide

### Cancellation Property

**Overview** – ยกเลิกการทำดัชนีหลังจากระยะเวลาที่กำหนดเพื่อหลีกเลี่ยงการใช้ทรัพยากรเกินขอบเขต

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Create Indexing Options with Cancellation

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

**Key Points**

- `setCancellation()` เปิดใช้งานฟีเจอร์นี้  
- `cancelAfter(int milliseconds)` กำหนดเวลา timeout (3 seconds ในตัวอย่างนี้)

### Asynchronous Property

**Overview** – ทำการทำดัชนีบนเธรดพื้นหลังและฟังการเปลี่ยนแปลงสถานะ

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Subscribe to Status Changed Event

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

#### Step 3: Configure Asynchronous Options

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Threads Property

**Overview** – เร่งความเร็วการทำดัชนีโดยใช้หลายคอร์ของ CPU

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metadata Indexing Options Property

**Overview** – ปรับจูนว่าเมตาดาต้าเอกสารใดบ้างที่จะทำดัชนีและวิธีการจัดเก็บ

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Metadata Options

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

## Practical Applications

1. **Document Management Systems** – ใช้การทำดัชนีแบบอะซิงโครนัสเพื่อให้ UI ตอบสนองได้ดีขณะประมวลผลชุดข้อมูลขนาดใหญ่ในพื้นหลัง  
2. **Content Search Engines** – ใช้ cancellation เพื่อป้องกันงานที่ใช้เวลานานเกินไปจากการกินทรัพยากรเซิร์ฟเวอร์ในช่วงเวลาที่มีการใช้งานสูงสุด  
3. **Large‑Scale Ingestion Pipelines** – ใช้มัลติ‑เธรดเพื่อ **add documents index** ในระดับใหญ่ ลดเวลาการประมวลผลอย่างมีนัยสำคัญ  

## Performance Considerations

- **Thread Management** – ตรวจสอบการใช้ CPU; จำนวนเธรดมากเกินไปอาจทำให้เกิด overhead จากการสลับคอนเท็กซ์  
- **Memory Footprint** – ขีดจำกัดเมตาดาต้า (เช่น `setMaxBytesToIndexField`) ช่วยให้การใช้หน่วยความจำคาดการณ์ได้  
- **Garbage Collection** – ใช้แฟล็ก JVM ที่เหมาะสม (`-Xmx`, `-XX:+UseG1GC`) เมื่อทำดัชนีข้อมูลขนาดมหาศาล  

## Common Issues and Solutions

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Indexing never finishes | Cancellation set too low | Increase `cancelAfter` value or remove cancellation for long jobs |
| No status updates in async mode | Event handler not attached correctly | Ensure `index.getEvents().StatusChanged.add(...)` is called before `index.add` |
| Out‑of‑memory errors | Too many threads or high metadata limits | Reduce `options.setThreads` and lower metadata field limits |
| Missing metadata in results | Metadata indexing disabled | Verify `options.getMetadataIndexingOptions()` is configured and not set to ignore fields |

## Frequently Asked Questions

**Q: How do I obtain a temporary license for GroupDocs.Search?**  
A: Visit [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/).

**Q: Can I cancel an indexing operation midway through?**  
A: Yes – use the cancellation property with `cancelAfter()` or call `Cancellation.cancel()` programmatically.

**Q: What are some use cases for asynchronous indexing?**  
A: Real‑time document retrieval, background batch processing, and UI‑responsive applications benefit from async indexing.

**Q: Is it safe to increase the thread count on a shared server?**  
A: Increase gradually and monitor CPU load; on heavily shared environments, keep the thread count modest (2‑4).

**Q: How does metadata indexing affect search relevance?**  
A: Properly indexed metadata (author, creation date, tags) can be weighted higher in queries, improving result accuracy.

## Conclusion

By embracing these advanced features of GroupDocs.Search for Java, you’ll **optimize search performance** across a variety of scenarios—from rapid document ingestion to fine‑grained metadata control. Experiment with different configurations, monitor resource usage, and tailor the settings to your specific workload to get the best results.

---

**Last Updated:** 2025-12-29  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---
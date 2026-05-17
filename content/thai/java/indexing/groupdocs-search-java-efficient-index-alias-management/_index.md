---
date: '2026-03-06'
description: เรียนรู้วิธีเพิ่มนามแฝงหลายรายการ, เพิ่มเอกสารลงในดัชนี, และจัดการดัชนีที่สามารถค้นหาได้อย่างมีประสิทธิภาพด้วย
  GroupDocs.Search สำหรับ Java.
keywords:
- GroupDocs.Search Java
- index management
- alias dictionary
title: วิธีเพิ่มนามแฝงหลายรายการและเพิ่มเอกสารลงในดัชนีใน GroupDocs.Search สำหรับ
  Java
type: docs
url: /th/java/indexing/groupdocs-search-java-efficient-index-alias-management/
weight: 1
---

# เพิ่มหลาย Alias และเพิ่มเอกสารลงในดัชนีใน GroupDocs.Search Java: คู่มือฉบับสมบูรณ์

ในโลกที่ขับเคลื่อนด้วยข้อมูลในวันนี้ การที่คุณสามารถ **เพิ่มหลาย alias** ขณะ **เพิ่มเอกสารลงในดัชนี** จะให้ข้อได้เปรียบด้านประสิทธิภาพที่ชัดเจนแก่โซลูชันการค้นหาของคุณ ไม่ว่าคุณจะทำการจัดทำดัชนีให้กับสัญญาหลายพันฉบับ, แคตตาล็อกสินค้า, หรือเอกสารวิจัย, GroupDocs.Search สำหรับ Java จะช่วยให้คุณ **สร้างโครงสร้างดัชนีที่สามารถค้นหาได้** และปรับแต่งการค้นหาโดยใช้พจนานุกรม alias — ทั้งหมดนี้ทำได้อย่างง่ายดายและรวดเร็ว

## คำตอบสั้น
- **ขั้นตอนแรกในการเริ่มใช้ GroupDocs.Search คืออะไร?** เพิ่ม dependency ของ Maven และเริ่มต้นอ็อบเจกต์ `Index`  
- **ฉันจะเพิ่มเอกสารลงในดัชนีอย่างไร?** เรียก `index.add("<folder_path>")` พร้อมกับโฟลเดอร์ที่บรรจุไฟล์ของคุณ  
- **ฉันสามารถสร้าง alias สำหรับการค้นหาที่ซับซ้อนได้หรือไม่?** ได้ — ใช้พจนานุกรม alias เพื่อแมปโทเคนสั้นให้เป็นนิพจน์การค้นหาเต็มรูปแบบ และคุณยังสามารถ **เพิ่มหลาย alias** พร้อมกันได้  
- **สามารถส่งออกและนำเข้าพจนานุกรม alias ได้หรือไม่?** แน่นอน — ใช้เมธอด `exportDictionary` และ `importDictionary`  
- **ต้องใช้เวอร์ชันใดของ GroupDocs.Search?** เวอร์ชัน 25.4 หรือใหม่กว่า (บทแนะนำนี้ใช้ 25.4)

## “เพิ่มเอกสารลงในดัชนี” คืออะไร?
การเพิ่มเอกสารลงในดัชนีหมายถึงการป้อนไฟล์ดิบ (PDF, DOCX, TXT ฯลฯ) ให้กับ GroupDocs.Search เพื่อให้ไลบรารีทำการวิเคราะห์เนื้อหาและสร้าง **ดัชนีที่สามารถค้นหาได้** เมื่อทำการจัดทำดัชนีแล้ว คุณสามารถรันการค้นหาแบบเต็มข้อความที่รวดเร็วบนเอกสารทั้งหมดได้

## ทำไมต้องจัดการ Alias?
Alias ช่วยให้คุณแทนที่ส่วนยาว ๆ ของนิพจน์การค้นหาที่ซ้ำกันด้วยโทเคนสั้น ๆ ที่จำง่าย (เช่น `@t` → `(gravida OR promotion)`) สิ่งนี้ไม่เพียงทำให้สตริงการค้นหาสั้นลง แต่ยังเพิ่มความอ่านง่าย, ความดูแลรักษา, และ **เพิ่มประสิทธิภาพการค้นหา** โดยเฉพาะเมื่อการค้นหามีความซับซ้อน

## วิธีเพิ่มหลาย Alias?
GroupDocs.Search มีเมธอด `addRange` ที่สะดวกซึ่งช่วยให้คุณแทรกคู่แทนที่ alias จำนวนมากพร้อมกัน การทำงานแบบ bulk นี้ช่วยลดภาระการประมวลผลเมื่อเทียบกับการเพิ่มแต่ละ alias ทีละรายการ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมี:

- **GroupDocs.Search for Java** ≥ 25.4  
- **JDK** (เวอร์ชันล่าสุดใดก็ได้, เช่น 11+)  
- IDE เช่น **IntelliJ IDEA** หรือ **Eclipse**  
- ความรู้พื้นฐานเกี่ยวกับ Java และ Maven  

## การตั้งค่า GroupDocs.Search for Java

### ใช้ Maven
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

### ดาวน์โหลดโดยตรง
หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจากเว็บไซต์ทางการได้ที่  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

#### ขั้นตอนการขอรับใบอนุญาต
1. **Free Trial** – ทดลองใช้ทุกฟีเจอร์โดยไม่มีข้อผูกมัด  
2. **Temporary License** – ขอคีย์ระยะสั้นเพื่อการประเมินผล  
3. **Full Purchase** – รับใบอนุญาตถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต  

### การเริ่มต้นและตั้งค่าพื้นฐาน

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        // Specify the directory to store indices
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
        
        // Create or open an index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup complete.");
    }
}
```

## คู่มือการใช้งาน

ด้านล่างเป็นขั้นตอนการทำงานของแต่ละฟีเจอร์ อ่านคำอธิบายก่อน แล้วคัดลอกโค้ดบล็อกที่ตรงกัน

### การสร้างหรือเปิด Index

**วิธีเพิ่มเอกสารลงในดัชนี – ขั้นแรกคุณต้องมีอินสแตนซ์ Index ที่ทำงานอยู่**

#### ขั้นตอน 1: นำเข้าคลาส Index
```java
import com.groupdocs.search.Index;
```

#### ขั้นตอน 2: กำหนดตำแหน่งที่ไฟล์ดัชนีจะถูกเก็บ
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/Indexes/Index";
```

#### ขั้นตอน 3: สร้างดัชนีใหม่หรือเปิดดัชนีที่มีอยู่
```java
Index index = new Index(indexFolder);
```

### การเพิ่มเอกสารลงใน Index

เมื่อดัชนีมีอยู่แล้ว ให้ **เพิ่มเอกสารลงในดัชนี** กันต่อ

#### ขั้นตอน 1: ระบุตำแหน่งโฟลเดอร์ต้นทางของคุณ
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/Documents";
```

#### ขั้นตอน 2: เพิ่มไฟล์ที่รองรับทุกประเภทจากโฟลเดอร์นั้น
```java
index.add(documentsFolder);
```

> **เคล็ดลับระดับมืออาชีพ:** รันขั้นตอนนี้ทุกครั้งที่มีไฟล์ใหม่เข้ามา GroupDocs.Search จะทำการจัดทำดัชนีเฉพาะเนื้อหาใหม่เท่านั้น, ไม่กระทบรายการที่มีอยู่แล้ว นี่คือแก่นของ **incremental indexing java**

### การจัดการพจนานุกรม Alias

Alias ช่วยให้คุณแมปโทเคนสั้นให้เป็นสตริงการค้นหาที่ซับซ้อน เราจะอธิบายการล้างรายการเก่า, การเพิ่ม alias เดียว, และ **การเพิ่มหลาย alias** แบบ bulk

#### ล้าง Alias ที่มีอยู่
```java
if (index.getDictionaries().getAliasDictionary().getCount() > 0) {
    index.getDictionaries().getAliasDictionary().clear();
}
```

#### เพิ่ม Alias เดียว
```java
index.getDictionaries().getAliasDictionary().add("t", "(gravida OR promotion)");
index.getDictionaries().getAliasDictionary().add("e", "(viverra OR farther)");
```

#### เพิ่มหลาย Alias
```java
AliasReplacementPair[] pairs = new AliasReplacementPair[] {
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};
index.getDictionaries().getAliasDictionary().addRange(pairs);
```

### การสืบค้นการแทนที่ Alias

คุณสามารถดึงข้อความเต็มของ alias ใด ๆ ที่ได้กำหนดไว้ได้ดังนี้:

```java
if (index.getDictionaries().getAliasDictionary().contains("e")) {
    String replacement = index.getDictionaries().getAliasDictionary().getText("e");
}
```

### การส่งออกและนำเข้าพจนานุกรม Alias

การส่งออกเป็นประโยชน์สำหรับการสำรองข้อมูลหรือแชร์ระหว่างสภาพแวดล้อม

#### ส่งออก Alias
```java
String fileName = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.getDictionaries().getAliasDictionary().exportDictionary(fileName);
```

#### นำเข้า Alias
```java
index.getDictionaries().getAliasDictionary().importDictionary(fileName);
```

### การค้นหาโดยใช้ Alias Query

เมื่อมี Alias อยู่แล้ว สตริงการค้นหาของคุณจะสะอาดและกระชับมากขึ้น:

```java
String query = "@t OR @e";
SearchResult result = index.search(query);
```

สัญลักษณ์ `@` บอก GroupDocs.Search ให้แทนที่โทเคนด้วยนิพจน์เต็มก่อนทำการค้นหา

## การประยุกต์ใช้งานจริง

| สถานการณ์ | Alias ช่วยอย่างไร |
|----------|-------------------|
| **การจัดการเอกสารทางกฎหมาย** | แมปหมายเลขคดี (`@case123`) ให้เป็นเงื่อนไข Boolean ที่ซับซ้อน, เร่งการดึงข้อมูล |
| **การค้นหาผลิตภัณฑ์ในอี‑คอมเมิร์ซ** | แทนที่การรวมคุณลักษณะทั่วไป (`@sale`) ด้วย `(discounted OR clearance)` |
| **ฐานข้อมูลวิจัย** | ใช้ `@year2020` เพื่อขยายเป็นตัวกรองช่วงวันที่บนเอกสารหลายฉบับ |

## พิจารณาด้านประสิทธิภาพ

- **Incremental Indexing:** เพิ่มเฉพาะไฟล์ใหม่หรือไฟล์ที่เปลี่ยนแปลง; หลีกเลี่ยงการทำดัชนีใหม่ทั้งหมด  
- **JVM Tuning:** จัดสรรหน่วยความจำ heap เพียงพอ (`-Xmx4g` สำหรับคอร์ปัสขนาดใหญ่)  
- **Batch Alias Updates:** ใช้ `addRange` เพื่อแทรกหลาย alias พร้อมกัน, ลดภาระการประมวลผล  
- **Optimize Search Performance:** ทำให้พจนานุกรม alias มีขนาดกะทัดรัดและใช้โทเคนอย่างชาญฉลาดเพื่อลดเวลาการพาร์สคำค้นหา

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | วิธีแก้ |
|-------|----------|
| ไฟล์ใหม่ไม่สามารถค้นหาได้ | รัน `index.add(newFolder)` อีกครั้ง; GroupDocs.Search จะทำการจัดทำดัชนีไฟล์ที่ยังไม่เคยเห็น |
| Alias ให้ผลลัพธ์ว่างเปล่า | ตรวจสอบว่าคีย์ alias (`@`) มีการใส่ prefix อย่างถูกต้องและพจนานุกรมมี token นั้นอยู่ |
| การใช้หน่วยความจำสูงขณะทำดัชนีแบบ bulk | เพิ่ม heap ของ JVM (`-Xmx`) และพิจารณาจัดทำดัชนีเป็น batch เล็ก ๆ |

## คำถามที่พบบ่อย

**ถาม: ประโยชน์หลักของการใช้ GroupDocs.Search for Java คืออะไร?**  
ตอบ: ให้ความสามารถในการจัดทำดัชนีและค้นหาแบบเต็มข้อความที่ทรงพลังและพร้อมใช้งาน, ช่วยให้คุณ **เพิ่มเอกสารลงในดัชนี** ได้อย่างรวดเร็วและค้นหาได้ด้วยประสิทธิภาพสูง

**ถาม: สามารถใช้ GroupDocs.Search ร่วมกับฐานข้อมูลได้หรือไม่?**  
ตอบ: ได้ — ดึงข้อมูลจากแหล่งใดก็ได้ (SQL, NoSQL, CSV) แล้วส่งต่อไปยังดัชนีโดยใช้เมธอด `add` เดียวกัน

**ถาม: Alias ช่วยเพิ่มประสิทธิภาพการค้นหาอย่างไร?**  
ตอบ: Alias ทำให้คุณเก็บตรรกะการค้นหาที่ซับซ้อนไว้ครั้งเดียวและเรียกใช้ด้วยโทเคนสั้น, ลดเวลาการพาร์สคำค้นหาและลดความผิดพลาดของมนุษย์เมื่อคุณ **search with aliases**

**ถาม: สามารถอัปเดต alias ที่มีอยู่โดยไม่ต้องสร้างพจนานุกรมใหม่ทั้งหมดได้หรือไม่?**  
ตอบ: แน่นอน — เรียก `add` ด้วยคีย์เดียวกัน; ไลบรารีจะเขียนทับค่าก่อนหน้า

**ถาม: ควรทำอย่างไรหากการค้นหาผลลัพธ์ไม่เป็นไปตามที่คาด?**  
ตอบ: ตรวจสอบว่าการกำหนดค่า alias ถูกต้อง, ทำการจัดทำดัชนีไฟล์ใหม่อีกครั้ง, และตรวจสอบการตั้งค่า analyzer สำหรับปัญหาการตัด token

---

**อัปเดตล่าสุด:** 2026-03-06  
**ทดสอบกับ:** GroupDocs.Search 25.4 for Java  
**ผู้เขียน:** GroupDocs  

---
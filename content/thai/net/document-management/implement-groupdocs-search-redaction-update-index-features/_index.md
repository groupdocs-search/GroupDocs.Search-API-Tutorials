---
date: '2026-06-07'
description: เรียนรู้วิธีอัปเดตดัชนีอย่างมีประสิทธิภาพด้วย GroupDocs.Search และ Redaction
  สำหรับ .NET เพื่อปรับปรุงระบบการจัดการเอกสารของคุณ
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: วิธีอัปเดตดัชนีด้วย GroupDocs.Search & Redaction (.NET)
type: docs
url: /th/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# วิธีอัปเดตดัชนีด้วย GroupDocs.Search & Redaction (.NET)

ในองค์กรสมัยใหม่ที่ขับเคลื่อนด้วยข้อมูล, **how to update index** อย่างรวดเร็วและเชื่อถือได้สามารถทำให้ประสบการณ์การค้นหาของคุณดีหรือแย่ได้ ไม่ว่าคุณจะจัดการกับสัญญาหลายพันฉบับหรือฐานความรู้ขนาดใหญ่ การทำให้ดัชนีการค้นหาเป็นไปตามการเปลี่ยนแปลงเอกสารล่าสุดเป็นสิ่งสำคัญสำหรับผลลัพธ์ที่เร็วและแม่นยำ บทแนะนำนี้จะพาคุณผ่านการใช้ GroupDocs.Search สำหรับ .NET ร่วมกับ GroupDocs.Redaction เพื่อ **update index** ไฟล์, จัดการดัชนีเวอร์ชัน, และปกป้องเนื้อหาที่ละเอียดอ่อน ทั้งหมดในโครงการ .NET ที่สะอาด

## คำตอบอย่างรวดเร็ว
- **What does “how to update index” mean?** เป็นกระบวนการแก้ไขดัชนีการค้นหาที่มีอยู่เพื่อให้เอกสารใหม่หรือที่เปลี่ยนแปลงสามารถค้นหาได้โดยไม่ต้องสร้างใหม่ตั้งแต่ต้น.  
- **Which libraries are required?** GroupDocs.Search และ GroupDocs.Redaction สำหรับ .NET (ทั้งสองสามารถติดตั้งได้ผ่าน NuGet).  
- **Do I need a license?** การทดลองใช้ฟรีทำงานได้สำหรับการทดสอบ; ใบอนุญาตการผลิตจะเปิดใช้งานฟังก์ชันเต็ม.  
- **Can I run this on .NET Core?** ใช่, ไลบรารีสนับสนุน .NET Framework 4.5+, .NET Core 3.1+, และ .NET 5/6+.  
- **What performance can I expect?** การอัปเดตดัชนีขนาด 1 GB ด้วย 2 เธรดจะเสร็จภายในน้อยกว่าหนึ่งนาทีบนเซิร์ฟเวอร์ 4‑คอร์ทั่วไป.

## “how to update index” คืออะไร?
**How to update index** หมายถึงเทคนิคการนำการเปลี่ยนแปลงแบบเพิ่มขั้นไปใช้กับดัชนีการค้นหาที่มีอยู่แทนการสร้างใหม่ทั้งหมด วิธีนี้ลดเวลาหยุดทำงาน, ประหยัดการใช้ CPU, และทำให้ผลการค้นหาของคุณสดใหม่เมื่อมีการเพิ่ม, แก้ไข หรือ ลบเอกสาร.

## ทำไมต้องใช้ GroupDocs.Search & Redaction สำหรับการอัปเดตดัชนี?
GroupDocs.Search รองรับ **50+ file formats** (PDF, DOCX, XLSX, PPTX, HTML, รูปภาพ ฯลฯ) และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ เมื่อรวมกับ GroupDocs.Redaction คุณสามารถลบหรือปิดบังข้อมูลที่ละเอียดอ่อนโดยอัตโนมัติก่อนทำดัชนี, ทำให้สอดคล้องกับข้อกำหนดและยังคงความเกี่ยวข้องของการค้นหา.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Search** – ติดตั้งผ่าน NuGet.  
- **GroupDocs.Redaction for .NET** – จำเป็นสำหรับความสามารถในการลบข้อมูล.  
- Visual Studio (หรือ IDE .NET ใดก็ได้) ที่ติดตั้ง .NET 6+ แล้ว.  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับแนวคิดการทำดัชนี.

### ไลบรารีและเวอร์ชันที่ต้องการ
- **GroupDocs.Search** – เวอร์ชันเสถียรล่าสุดจาก NuGet.  
- **GroupDocs.Redaction for .NET** – เวอร์ชันเสถียรล่าสุดจาก NuGet.

### ความต้องการการตั้งค่าสภาพแวดล้อม
- เครื่อง Windows หรือ Linux ที่ติดตั้ง .NET SDK.  
- เข้าถึงโฟลเดอร์ที่ไฟล์ดัชนีจะถูกจัดเก็บ.

### ความรู้พื้นฐานที่จำเป็น
- ความเข้าใจเกี่ยวกับการทำดัชนีเอกสารและพื้นฐานการค้นหา.  
- การรับรู้การจัดการวงจรชีวิตของเอกสารในระบบองค์กร.

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### ติดตั้งแพ็กจ์

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- ค้นหา “GroupDocs.Redaction” และติดตั้งเวอร์ชันล่าสุด.

### ขั้นตอนการรับใบอนุญาต
1. **Free Trial** – เริ่มต้นด้วยการทดลองเพื่อสำรวจคุณสมบัติทั้งหมด.  
2. **Temporary License** – ขอคีย์ชั่วคราวสำหรับการทดสอบต่อเนื่อง.  
3. **Purchase** – รับใบอนุญาตเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

### การเริ่มต้นและตั้งค่าเบื้องต้น
`Redactor` คือคลาสหลักที่ใช้ใช้กฎการลบข้อมูลกับเอกสาร.  
เพื่อเริ่มต้น, อ้างอิง namespace Redaction และสร้างอินสแตนซ์ของ `Redactor`:

```csharp
using GroupDocs.Redaction;
```

## คู่มือการใช้งาน

เราจะครอบคลุมสองความสามารถหลัก: การอัปเดตเอกสารที่ทำดัชนีและการควบคุมเวอร์ชันของดัชนี.

### วิธีอัปเดตดัชนีโดยใช้ GroupDocs.Search?
`Index` แสดงถึงคอลเลกชันที่สามารถค้นหาได้ที่เก็บบนดิสก์.  
`UpdateOptions` กำหนดวิธีการทำการอัปเดตแบบเพิ่มขั้น (เช่น จำนวนเธรด).  
`UpdateDocument` ใช้การเปลี่ยนแปลงกับเอกสารเดียว, และ `Commit` สรุปการอัปเดตที่ค้างอยู่ทั้งหมด.

**Direct answer (40‑70 words):**  
สร้างอ็อบเจกต์ `Index` ที่ชี้ไปยังโฟลเดอร์ดัชนีของคุณ, ใช้ `UpdateOptions` เพื่อระบุจำนวนเธรด, เรียก `UpdateDocument` สำหรับแต่ละไฟล์ที่เปลี่ยนแปลง, และสุดท้ายเรียก `Commit` เพื่อบันทึกการเปลี่ยนแปลง วิธีการเพิ่มขั้นนี้จะอัปเดตเฉพาะส่วนที่แก้ไข, ทำให้ดัชนีเป็นปัจจุบันโดยไม่ต้องสร้างใหม่ทั้งหมด.

#### ฟีเจอร์ 1: อัปเดตเอกสารที่ทำดัชนี

##### ภาพรวม
การอัปเดตเอกสารที่ทำดัชนีทำให้ผลการค้นหาของคุณสะท้อนเนื้อหาใหม่ล่าสุด, แม้ว่าเอกสารจะถูกแก้ไขหรือแทนที่.

##### ขั้นตอนที่ 1: สร้าง Index
คลาส `Index` เป็นอ็อบเจกต์ระดับบนสุดที่แสดงคอลเลกชันที่สามารถค้นหาได้บนดิสก์.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### ขั้นตอนที่ 2: เพิ่มเอกสารลงใน Index
เพิ่มไฟล์จากไดเรกทอรี; ไลบรารีจะดึงข้อความที่สามารถค้นหาได้โดยอัตโนมัติ.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### ขั้นตอนที่ 3: ค้นหาและอัปเดต
รันการค้นหา, แก้ไขไฟล์ต้นฉบับ, จากนั้นเรียก `UpdateDocument` ด้วย `UpdateOptions` เดียวกันที่ใช้ระหว่างการทำดัชนี.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**ทำไมวิธีนี้ถึงได้ผล:** โดยการตั้งค่า `Threads = 2`, การอัปเดตจะใช้สองคอร์ของ CPU, ลดเวลาการประมวลผลประมาณครึ่งหนึ่งบนเครื่องคอมพิวเตอร์ 4‑คอร์.

### วิธีจัดการควบคุมเวอร์ชันของดัชนี?
`IndexUpdater` คือคลาสยูทิลิตี้ที่อัปเกรดรูปแบบดัชนีเก่าให้เป็นเวอร์ชันล่าสุดที่ไลบรารีสนับสนุน.

**Direct answer (40‑70 words):**  
สร้างอินสแตนซ์ `IndexUpdater` ด้วยเส้นทางไปยังดัชนีที่มีอยู่, เรียก `CanUpdateVersion()` เพื่อตรวจสอบความเข้ากันได้, จากนั้นรัน `UpdateVersion()` หากจำเป็น หลังจากอัปเกรด, โหลดดัชนีใหม่ด้วยรูปแบบใหม่และทำการค้นหาเพื่อยืนยันว่าทุกอย่างทำงานได้ วิธีนี้ทำให้การย้ายเวอร์ชันระหว่างการปล่อยไลบรารีเป็นไปอย่างราบรื่น.

#### ฟีเจอร์ 2: ควบคุมเวอร์ชันของดัชนี

##### ภาพรวม
การควบคุมเวอร์ชันรับประกันว่าดัชนีเก่ายังคงสามารถค้นหาได้หลังจากอัปเกรดไลบรารี.

##### ขั้นตอนที่ 1: ตรวจสอบความเข้ากันได้
`IndexUpdater` ตรวจสอบว่าดัชนีปัจจุบันสามารถอัปเกรดเป็นรูปแบบล่าสุดได้หรือไม่.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### ขั้นตอนที่ 2: โหลดและค้นหา
หลังจากอัปเกรด, โหลดดัชนีที่รีเฟรชแล้วและดำเนินการค้นหาเพื่อยืนยันความสมบูรณ์.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**ทำไมวิธีนี้ถึงได้ผล:** ตัวตรวจสอบ `CanUpdateVersion` ป้องกันข้อยกเว้นในระหว่างทำงานที่เกิดจากสคีมาดัชนีที่ไม่ตรงกัน, ให้เส้นทางอัปเกรดที่ปลอดภัย.

## การประยุกต์ใช้งานจริง
สถานการณ์จริงที่ **how to update index** มีความสำคัญ:

1. **Legal Document Management** – รีอินเดกซ์สัญญาอย่างรวดเร็วหลังการแก้ไขพร้อมลบข้อมูลที่เป็นความลับ.  
2. **Corporate Archives** – ทำให้บันทึกประวัติศาสตร์สามารถค้นหาได้โดยไม่ต้องประมวลผลไฟล์หลายล้านไฟล์ใหม่.  
3. **Content Management Systems (CMS)** – ส่งการอัปเดตแบบเพิ่มขั้นไปยังดัชนีการค้นหาเมื่อผู้เขียนเผยแพร่บทความใหม่.

## การพิจารณาประสิทธิภาพ
- **Threading Options:** ปรับ `UpdateOptions.Threads` ตามจำนวนคอร์ของ CPU; เธรดมากขึ้นเพิ่มอัตราการทำงานแต่ใช้หน่วยความจำมากขึ้น.  
- **Resource Usage:** ตรวจสอบ RAM; ไลบรารีสตรีมไฟล์, ดังนั้นการกระโดดของหน่วยความจำจึงน้อยแม้สำหรับ PDF 500 หน้า.  
- **Best Practices:** กำหนดเวลาการอัปเดตแบบเพิ่มขั้นเป็นประจำและทำความสะอาดเวอร์ชันดัชนีที่ล้าสมัยเพื่อรักษาประสิทธิภาพที่ดีที่สุด.

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **Index not found** | เส้นทางโฟลเดอร์ผิด | ตรวจสอบให้แน่ใจว่า constructor ของ `Index` ชี้ไปยังไดเรกทอรีที่ถูกต้อง. |
| **Version mismatch error** | ใช้ดัชนีเก่ากับไลบรารีใหม่ | รันกระบวนการ `IndexUpdater` ก่อนทำดัชนีปกติ. |
| **Redaction not applied** | กฎการลบข้อมูลโหลดหลังจากทำดัชนี | ใช้การลบข้อมูล **ก่อน** เพิ่มเอกสารลงในดัชนี. |

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง `UpdateDocument` กับ `Rebuild` คืออะไร?**  
A: `UpdateDocument` แก้ไขเฉพาะไฟล์ที่เปลี่ยนแปลง, ในขณะที่ `Rebuild` สร้างดัชนีทั้งหมดใหม่จากศูนย์, ใช้เวลและทรัพยากรมากกว่า.

**Q: สามารถอัปเดตหลายเอกสารพร้อมกันได้หรือไม่?**  
A: ใช่, ตั้งค่า `UpdateOptions.Threads` เป็นจำนวนคอร์ที่ต้องการใช้; ไลบรารีจัดการการประมวลผลแบบขนานภายใน.

**Q: GroupDocs.Search รองรับ PDF ที่เข้ารหัสหรือไม่?**  
A: แน่นอน. ให้รหัสผ่านผ่าน `SearchOptions.Password` เมื่อโหลดเอกสาร.

**Q: จะตรวจสอบว่าการลบข้อมูลสำเร็จก่อนทำดัชนีอย่างไร?**  
A: เรียก `Redactor.Apply()` และตรวจสอบขนาดไฟล์ผลลัพธ์; ขนาดที่ลดลงมักบ่งชี้ว่าการลบข้อมูลสำเร็จ.

**Q: .NET เวอร์ชันใดที่รองรับอย่างเป็นทางการ?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, และ .NET 6+.

## สรุป
คุณมีคู่มือครบถ้วนและพร้อมใช้งานในสภาพแวดล้อมการผลิตเกี่ยวกับ **how to update index** ด้วย GroupDocs.Search และวิธีทำให้ดัชนีเหล่านั้นเข้ากันได้กับเวอร์ชันของ GroupDocs.Redaction สำหรับ .NET. ด้วยการทำตามขั้นตอนข้างต้น, คุณสามารถรับประกันว่าชั้นการค้นหาของคุณจะเร็ว, แม่นยำ, และสอดคล้องกับกฎระเบียบความเป็นส่วนตัวของข้อมูล.

**ขั้นตอนต่อไป:**  
- ทดลองตั้งค่า `Threads` ต่าง ๆ เพื่อหาค่าที่เหมาะสมกับฮาร์ดแวร์ของคุณ.  
- สำรวจรูปแบบการลบข้อมูลขั้นสูง (เช่น การลบ SSN ด้วย regex) ก่อนทำดัชนี.  
- ผสานรวมกระบวนการอัปเดตดัชนีเข้าสู่ pipeline CI/CD ของคุณเพื่อการจัดการเอกสารอัตโนมัติเต็มรูปแบบ.

---

**อัปเดตล่าสุด:** 2026-06-07  
**ทดสอบกับ:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**ผู้เขียน:** GroupDocs  

## แหล่งข้อมูล
- [เอกสาร](https://docs.groupdocs.com/search/net/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

## บทแนะนำที่เกี่ยวข้อง
- [เชี่ยวชาญ GroupDocs.Redaction .NET: การสร้างดัชนีอย่างมีประสิทธิภาพและการจัดการ Alias สำหรับการค้นหาเอกสารขั้นสูง](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [ใช้งานการค้นหา Synonym กับ GroupDocs.Redaction .NET เพื่อการจัดการเอกสารที่ดีขึ้น](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [เชี่ยวชาญ GroupDocs Search และ Redaction ใน .NET: การจัดการเอกสารขั้นสูง](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
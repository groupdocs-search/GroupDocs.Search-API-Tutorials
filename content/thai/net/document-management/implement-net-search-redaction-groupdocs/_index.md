---
date: '2026-06-12'
description: เรียนรู้วิธีการค้นหาและลบข้อมูลในเอกสารด้วย .NET ด้วย GroupDocs.Search
  และ GroupDocs.Redaction เพื่อเพิ่มประสิทธิภาพการค้นหาและจัดการข้อผิดพลาดในการทำดัชนี
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: วิธีการค้นหาและลบข้อมูลในเอกสารด้วย .NET โดยใช้ GroupDocs.Search และ GroupDocs.Redaction
type: docs
url: /th/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# ค้นหาและทำการลบข้อมูลในเอกสารด้วย .NET ด้วย GroupDocs.Search & GroupDocs.Redaction

ในสภาพแวดล้อมองค์กรสมัยใหม่ ความสามารถในการ **search and redact** มีความสำคัญต่อการปกป้องข้อมูลที่เป็นความลับในขณะที่ทำให้เอกสารค้นหาได้ง่าย การสอนนี้จะพาคุณผ่านการสร้างโซลูชัน .NET ที่แข็งแกร่งโดยผสาน GroupDocs.Search สำหรับการค้นหาแบบเต็มข้อความที่รวดเร็วกับ GroupDocs.Redaction เพื่อการลบข้อมูลที่เป็นความลับอย่างปลอดภัย เมื่อจบคุณจะรู้วิธีตั้งค่าห้องสมุด สร้างตัวแบ่งข้อความแบบกำหนดเอง รันการค้นหาประสิทธิภาพสูง และทำการลบข้อมูลอย่างปลอดภัย

## คำตอบด่วน
- **“search and redact” หมายความว่าอะไร?** หมายถึงการค้นหาข้อความในเอกสารและทำการปิดบังอย่างถาวร  
- **ต้องใช้ห้องสมุดอะไรบ้าง?** GroupDocs.Search และ GroupDocs.Redaction สำหรับ .NET  
- **ฉันสามารถจัดการเนื้อหาหลายภาษาได้หรือไม่?** ได้—ใช้ตัวแบ่งข้อความแบบกำหนดเองเพื่อแยกคำอย่างถูกต้อง  
- **จะเพิ่มความเร็วการค้นหาอย่างไร?** ทำการสร้างดัชนีครั้งเดียว ใช้ดัชนีซ้ำ และเปิดการตั้งค่า `optimize search performance`  
- **ถ้าการสร้างดัชนีล้มเหลวจะทำอย่างไร?** ปฏิบัติตามแนวทาง “handle indexing errors” ในส่วนการแก้ไขปัญหา

## “search and redact” คืออะไร?

“search and redact” คือกระบวนการค้นหาคำหรือวลีเฉพาะในชุดเอกสารแล้วทำการบังหรือเอาออกอย่างถาวรเพื่อปกป้องความเป็นส่วนตัวหรือให้เป็นไปตามข้อกำหนดด้านกฎระเบียบ มันรวมการค้นหาแบบเต็มข้อความเพื่อหาข้อมูลที่สำคัญกับเครื่องมือการลบที่แทนที่เนื้อหาโดยยังคงรักษาโครงสร้างต้นฉบับของเอกสารไว้

## ทำไมต้องใช้ GroupDocs.Search และ GroupDocs.Redaction ร่วมกัน?

GroupDocs.Search รองรับ **ไฟล์รูปแบบกว่า 50** ชนิดและสามารถสร้างดัชนี **กว่า 100,000 เอกสาร** ในเวลาน้อยกว่านาทีบนเซิร์ฟเวอร์มาตรฐาน ในขณะที่ GroupDocs.Redaction สามารถทำการลบข้อมูลใน **PDF, DOCX, PPTX และอื่น ๆ** โดยไม่ทำให้รูปแบบต้นฉบับเปลี่ยนแปลง การผสานสองเครื่องมือนี้ให้คุณได้โซลูชันแบบสแต็กเดียวที่ **เพิ่มประสิทธิภาพการค้นหา** และ **จัดการข้อผิดพลาดการสร้างดัชนี** อย่างราบรื่น

## ข้อกำหนดเบื้องต้น

- Visual Studio 2022 หรือใหม่กว่า พร้อมสนับสนุน .NET 6+  
- แพ็กเกจ NuGet: **GroupDocs.Search** และ **GroupDocs.Redaction** (เวอร์ชันเสถียรล่าสุด)  
- ใบอนุญาต GroupDocs ที่ถูกต้อง (ทดลองหรือซื้อ)

### ห้องสมุดที่ต้องการ
- **GroupDocs.Search** – ให้บริการการสร้างดัชนี การสืบค้น และการแบ่งส่วนข้อความแบบกำหนดเอง  
- **GroupDocs.Redaction** – ให้บริการการลบข้อความ รูปภาพ และเมทาดาท้าในรูปแบบที่รองรับ

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
ตรวจสอบให้เครื่องพัฒนาของคุณมีสิทธิ์เขียนไปยังโฟลเดอร์ที่เก็บดัชนี

### ความรู้เบื้องต้นที่ต้องมี
- ความคุ้นเคยกับ C# และโครงสร้างโปรเจกต์ .NET  
- ความเข้าใจพื้นฐานเกี่ยวกับแนวคิดการประมวลผลเอกสาร (ไม่บังคับแต่เป็นประโยชน์)

## จะติดตั้ง GroupDocs.Redaction สำหรับ .NET อย่างไร?

คุณสามารถเพิ่มแพ็กเกจ Redaction ไปยังโปรเจกต์ของคุณได้โดยใช้ .NET CLI หรือ NuGet Package Manager คำสั่งจะดาวน์โหลดเวอร์ชันเสถียรล่าสุดและลงทะเบียนในไฟล์โปรเจกต์ของคุณ ทำให้ API พร้อมใช้งานทันที  

```bash
dotnet add package GroupDocs.Redaction
```  

## จะขอรับใบอนุญาตสำหรับ GroupDocs อย่างไร?

GroupDocs มีตัวเลือกใบอนุญาตสามแบบ: ทดลองฟรีเพื่อประเมินผล, ใบอนุญาตชั่วคราวสำหรับการทดสอบการพัฒนาต่อเนื่อง, และใบอนุญาตเชิงพาณิชย์เต็มรูปแบบสำหรับการใช้งานในผลิตภัณฑ์ การทดลองให้ฟังก์ชันจำกัด ส่วนคีย์ชั่วคราวขยายระยะเวลาการประเมินผล ส่วนใบอนุญาตที่ซื้อจะปลดล็อกคุณสมบัติทั้งหมดและรับการสนับสนุนระดับพรีเมียม

## จะเริ่มต้นใช้งาน GroupDocs.Redaction ในแอปพลิเคชันของฉันอย่างไร?

คลาส `Redaction` เป็นจุดเริ่มต้นหลักสำหรับการทำลบข้อมูลในเอกสารที่รองรับ มันโหลดไฟล์ เตรียมวัตถุการลบ และดำเนินการลบข้อมูล ส่งคืนเอกสารที่แก้ไขแล้วโดยยังคงรักษาเลย์เอาต์เดิม คุณยังสามารถกำหนดตัวเลือกการลบเช่น สี, การซ้อนทับ, และการลบเมทาดาท้าเพื่อให้สอดคล้องกับข้อกำหนดการปฏิบัติตาม  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## จะตั้งค่าดัชนีโดยใช้ GroupDocs.Search อย่างไร?

คลาส `Index` แทนที่คลังข้อมูลที่สามารถค้นหาได้ซึ่งจัดเก็บบนดิสก์ มันจัดการการสร้าง, การอัปเดต, และการสืบค้นดัชนี ทำให้คุณสามารถเพิ่มเอกสาร, สร้างดัชนีใหม่, และดำเนินการค้นหาเร็ว ๆ ในคอลเลกชันขนาดใหญ่ โฟลเดอร์ดัชนีสามารถวางบนที่จัดเก็บภายในเครื่องหรือเครือข่าย และคุณสามารถกำหนดการบีบอัดและการเข้ารหัสเพื่อปกป้องข้อมูลที่ถูกจัดทำดัชนี  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## ตัวแบ่งข้อความแบบกำหนดเองคืออะไรและทำไมต้องใช้?

ตัวแบ่งข้อความแบบกำหนดเองกำหนดวิธีที่ข้อความดิบจะแบ่งเป็นโทเคนที่สามารถค้นหาได้ โดยการปรับกฎการแบ่งส่วนให้เหมาะกับภาษา หรือโดเมนเฉพาะ คุณจะเพิ่มความแม่นยำของการทำโทเคนไลเซชัน ส่งผลให้การเรียกค้นมีการเรียกคืนและความเกี่ยวข้องที่สูงขึ้น สิ่งนี้มีประโยชน์อย่างยิ่งกับภาษาที่มีขอบเขตคำซับซ้อน เช่น ญี่ปุ่นหรืออาหรับ ซึ่งตัวแบ่งคำเริ่มต้นอาจแยกคำผิด  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## จะทำการค้นหาแบบเต็มข้อความด้วยตัวแบ่งแบบกำหนดเองอย่างไร?

อ็อบเจ็กต์ `SearchQuery` จะบรรจุคำค้นของผู้ใช้และทำงานร่วมกับตัวแบ่งข้อความแบบกำหนดเองเพื่อค้นหาตรงกัน มันรองรับการค้นหาแบบ fuzzy, คำวลี, และการให้คะแนนน้ำหนัก ส่งคืนชุดผลลัพธ์ที่มี ID ของเอกสาร, ตำแหน่งที่พบ, และคะแนนความเกี่ยวข้อง คุณยังสามารถใช้ฟิลเตอร์เช่น ประเภทไฟล์ หรือช่วงวันที่เพื่อจำกัดผลลัพธ์ให้แม่นยำยิ่งขึ้น  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## จะทำการลบข้อมูลหลังจากพบข้อความที่เป็นความลับอย่างไร?

API `Redaction` ให้คุณแทนที่หรือเอาข้อความ, รูปภาพ, และเมทาดาท้าออกจากเอกสารที่รองรับ หลังจากระบุคำที่เป็นความลับแล้ว คุณสร้างวัตถุการลบ, นำไปใช้, และบันทึกไฟล์ที่ลบแล้ว เพื่อให้ข้อมูลลับถูกซ่อนอย่างถาวร ตัวเลือกการลบรวมถึงการซ้อนกล่องสีดำ, ใช้สีกำหนดเอง, หรือการลบวัตถุทั้งหมดโดยยังคงโครงสร้างเอกสาร  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## ปัญหาทั่วไปและวิธีจัดการข้อผิดพลาดการสร้างดัชนี

- **Index Not Found:** ตรวจสอบว่าเส้นทางดัชนีมีอยู่และแอปพลิเคชันมีสิทธิ์อ่าน/เขียน  
- **Search Returns No Results:** รันกระบวนการสร้างดัชนีใหม่และตรวจสอบว่าตัวแบ่งข้อความแบบกำหนดเองได้ลงทะเบียนอย่างถูกต้อง  
- **Redaction Fails on Certain Formats:** ยืนยันว่าประเภทไฟล์ได้รับการสนับสนุน; สำหรับ PDF ให้ใช้เวอร์ชัน Redaction ล่าสุดเพื่อรองรับฟีเจอร์ PDF 2.0

## การประยุกต์ใช้งานจริง

1. **การจัดการเอกสารทางกฎหมาย:** ค้นหาสัญญาสำหรับ “non‑disclosure” และลบข้อกำหนดโดยอัตโนมัติก่อนแชร์ภายนอก  
2. **การวิจัยเชิงวิชาการ:** ค้นหาข้อมูลที่ยังไม่ได้ตีพิมพ์ในต้นฉบับและซ่อนเพื่อกระบวนการตรวจสอบโดยผู้เชี่ยวชาญ  
3. **สัญญาทางธุรกิจ:** ประมวลผลเป็นชุดพัน ๆ ข้อตกลง ลบข้อมูลส่วนบุคคลขณะยังคงรักษาภาษาเชิงกฎหมายไว้

## จะเพิ่มประสิทธิภาพการค้นหาสำหรับชุดเอกสารขนาดใหญ่ได้อย่างไร?

เพื่อให้ได้ประสิทธิภาพสูงสุด ให้สร้างดัชนีเอกสารเพียงครั้งเดียวและใช้ดัชนีเดียวกันสำหรับการสืบค้นต่อไป เปิดการประมวลผลแบบขนาน, ตั้งค่าการแคช, และปรับจูนการตั้งค่าดัชนีเพื่อลดความหน่วงและเพิ่มอัตราผ่านข้อมูลบนเซิร์ฟเวอร์หลายคอร์ นอกจากนี้ให้ตั้งค่าสถานะ `EnableMemoryMapping` เพื่อให้ดัชนีถูกแมปเป็นหน่วยความจำ ซึ่งช่วยเร่งการอ่านสำหรับชุดข้อมูลขนาดใหญ่

## จะจัดการหน่วยความจำ .NET เมื่อทำงานกับไฟล์ขนาดใหญ่อย่างไร?

การจัดการหน่วยความจำอย่างมีประสิทธิภาพเป็นสิ่งสำคัญเมื่อจัดการเอกสารขนาดใหญ่ ห่อ `Index` และ `Redaction` ด้วยคำสั่ง `using` เพื่อให้แน่ใจว่ามีการทำลายวัตถุอย่างกำหนด และประมวลผลไฟล์เป็นสตรีมแทนการโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ การตรวจสอบคอนเตอร์ประสิทธิภาพช่วยให้ตรวจจับการพุ่งของหน่วยความจำได้เร็ว ทำให้คุณปรับขนาดชุดข้อมูลหรือเปิดการปรับจูนการเก็บขยะได้ตามต้องการ

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถใช้ GroupDocs.Search กับเมทาดาท้าที่ไม่ใช่ข้อความได้หรือไม่?**  
ตอบ: ได้—ฟิลด์เมทาดาท้าสามารถทำดัชนีพร้อมกับเนื้อหาเอกสาร ทำให้สามารถค้นหาแบบ “author:JohnDoe” ได้

**ถาม: GroupDocs.Redaction รองรับการลบข้อมูลแบบเรียลไทม์ใน Web API หรือไม่?**  
ตอบ: รองรับ; คุณสามารถเรียก API Redaction แบบซิงโครนัสสำหรับไฟล์ขนาดเล็กหรือคิวงานขนาดใหญ่เพื่อประมวลผลแบบอะซิงโครนัส

**ถาม: จะทำอย่างไรถ้าดัชนีเสียหาย?**  
ตอบ: ลบโฟลเดอร์ดัชนีที่เสียและสร้างดัชนีใหม่ด้วยขั้นตอนเดิม; ไลบรารีจะบันทึกข้อความข้อผิดพลาดโดยละเอียดเพื่อช่วยระบุสาเหตุ

**ถาม: สามารถดูตัวอย่างเอกสารที่ลบแล้วก่อนบันทึกได้หรือไม่?**  
ตอบ: แน่นอน—เรียก `redaction.Apply()` พร้อมแฟล็ก `preview` เพื่อสร้างเวอร์ชันชั่วคราวสำหรับตรวจสอบ

**ถาม: .NET เวอร์ชันใดที่รองรับอย่างเป็นทางการ?**  
ตอบ: GroupDocs.Search และ GroupDocs.Redaction รองรับ .NET 6, .NET 5, .NET Core 3.1, และ .NET Framework 4.6.2+

## แหล่งข้อมูล

- **เอกสาร:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)  
- **อ้างอิง API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **ดาวน์โหลด:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **สนับสนุนฟรี:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ใบอนุญาตชั่วคราว:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-06-12  
**ทดสอบกับ:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**ผู้เขียน:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## บทเรียนที่เกี่ยวข้อง

- [เชี่ยวชาญ GroupDocs Search และ Redaction ใน .NET: การจัดการเอกสารขั้นสูง](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)  
- [นำ GroupDocs.Search & Redaction ไปใช้: การอัปเดตและจัดการดัชนีเอกสารใน .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)  
- [เพิ่มประสิทธิภาพการทำดัชนีเอกสารใน .NET ด้วย GroupDocs.Redaction: การยกเลิก, Async, และ Threads](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
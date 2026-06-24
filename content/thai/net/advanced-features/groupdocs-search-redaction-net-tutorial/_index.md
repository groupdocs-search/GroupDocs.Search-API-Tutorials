---
date: '2026-04-04'
description: เรียนรู้วิธีการค้นหาเอกสารทางกฎหมายและจัดการดัชนีโดยใช้ GroupDocs.Search
  และรวมการทำลบข้อมูลสำหรับบันทึกทางการแพทย์ด้วย GroupDocs.Redaction ใน .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: ค้นหาเอกสารทางกฎหมายด้วย GroupDocs Search & Redaction สำหรับ .NET
type: docs
url: /th/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# ค้นหาเอกสารทางกฎหมายด้วย GroupDocs Search & Redaction ใน .NET

ในสภาพแวดล้อมที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน การ **ค้นหาเอกสารทางกฎหมาย** อย่างรวดเร็วและปลอดภัยเป็นความต้องการสำคัญสำหรับทุกองค์กร ไม่ว่าคุณจะจัดการสัญญา การยื่นฟ้องศาล หรือรายงานการปฏิบัติตามกฎระเบียบ GroupDocs.Search จะให้ดัชนีที่เร็วและขยายได้ ในขณะที่ GroupDocs.Redaction ทำให้ข้อมูลที่ละเอียดอ่อนถูกซ่อนอยู่ บทแนะนำนี้จะพาคุณผ่านการตั้งค่าดัชนีที่สามารถค้นหาได้ การเพิ่มเอกสารจากหลายโฟลเดอร์ และการกำหนดค่าการลบข้อมูลเพื่อให้คุณสามารถค้นบันทึกทางการแพทย์และไฟล์ที่เป็นความลับได้อย่างปลอดภัย.

## คำตอบอย่างรวดเร็ว
- **GroupDocs.Search ทำอะไร?** มันสร้างดัชนีที่สามารถค้นหาแบบเต็มข้อความสำหรับรูปแบบเอกสารที่หลากหลาย.  
- **ฉันสามารถลบข้อมูลก่อนการค้นหาได้หรือไม่?** ได้ – ใช้ GroupDocs.Redaction เพื่อซ่อนหรือเอาข้อมูลที่ละเอียดอ่อนออก.  
- **ฉันจะเพิ่มเอกสารลงในดัชนีอย่างไร?** เรียก `index.Add("folderPath")` สำหรับแต่ละโฟลเดอร์ที่คุณต้องการรวม.  
- **ประเภทไฟล์ที่รองรับคืออะไร?** PDF, DOCX, PPTX, TXT และอื่น ๆ อีกมาก.  
- **ฉันต้องการไลเซนส์สำหรับการใช้งานจริงหรือไม่?** มีการทดลองใช้ชั่วคราว; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้เชิงพาณิชย์.

## ข้อกำหนดเบื้องต้น
เพื่อทำตามบทแนะนำนี้ ให้แน่ใจว่าคุณมี:
- .NET Core SDK (3.1 หรือใหม่กว่า) ติดตั้งแล้ว.
- Visual Studio Code, Visual Studio หรือ IDE อื่นที่รองรับ .NET.
- ความคุ้นเคยพื้นฐานกับการเขียนโปรแกรม C#.

### การรับไลเซนส์
คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรีของทั้งสองไลบรารี สำหรับการใช้งานต่อเนื่อง ให้พิจารณาได้รับไลเซนส์ชั่วคราวหรือซื้อจาก [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## การติดตั้งแพ็กเกจที่จำเป็น

**การติดตั้ง GroupDocs.Search:**  
ใช้ **.NET CLI**, รัน:
```bash
dotnet add package GroupDocs.Search
```
หรือใช้ Package Manager Console ใน Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**การติดตั้ง GroupDocs.Redaction:**  
- ใช้ .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- หรือ ผ่าน Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

เยี่ยมชม UI ของ NuGet Package Manager และค้นหา "GroupDocs.Redaction" เพื่อติดตั้งหากคุณต้องการใช้ GUI.

## กำหนดค่าการลบข้อมูล
ก่อนที่คุณจะเริ่มลบข้อมูล คุณอาจต้องการปรับพฤติกรรมของ redactor (เช่น ตั้งค่าสีการลบหรือกำหนดรูปแบบที่กำหนดเอง) โค้ดตัวอย่างต่อไปนี้แสดงการเริ่มต้นพื้นฐาน:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **เคล็ดลับ:** ปรับ `redactorSettings` ให้ตรงกับนโยบายการปฏิบัติตามขององค์กรของคุณ (เช่น แทนที่ข้อความด้วยกล่องสีดำ, ใช้ OCR ก่อนการลบข้อมูล, เป็นต้น).

## คู่มือการใช้งาน

### วิธีการค้นหาเอกสารทางกฎหมาย?
การสร้างดัชนีที่สามารถค้นหาได้เป็นพื้นฐานสำหรับการดึงข้อมูลเอกสารทางกฎหมายอย่างรวดเร็ว GroupDocs.Search ให้คุณชี้ไปยังโฟลเดอร์ใดก็ได้ สร้างดัชนี แล้วดำเนินการค้นหาที่ซับซ้อนในหลายพันไฟล์.

### วิธีการเพิ่มเอกสารลงในดัชนี
การเพิ่มเอกสารเป็นเรื่องง่าย—เพียงแค่ชี้ไลบรารีไปยังไดเรกทอรีที่เก็บไฟล์ของคุณ คุณสามารถเพิ่มหลายโฟลเดอร์ได้ ซึ่งสะดวกเมื่อคอลเลกชันทางกฎหมายของคุณกระจายอยู่หลายที่.

#### การสร้างและจัดการดัชนี
**ภาพรวม:**  
การสร้างดัชนีเป็นขั้นตอนแรกสู่การดำเนินการค้นหาเอกสารอย่างมีประสิทธิภาพ GroupDocs.Search อนุญาตให้คุณสร้างดัชนีที่สามารถค้นหาได้ในไดเรกทอรีใดก็ได้ตามที่คุณเลือก ทำให้ดึงเอกสารได้อย่างรวดเร็ว.

##### ขั้นตอนที่ 1: สร้างดัชนี
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*คำอธิบาย:* `Index` เริ่มต้นดัชนีการค้นหาในไดเรกทอรีที่ระบุ ตรวจสอบให้แน่ใจว่าเส้นทางสะท้อนโครงสร้างโฟลเดอร์ของโครงการของคุณ.

##### ขั้นตอนที่ 2: เพิ่มเอกสารลงในดัชนี
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*คำอธิบาย:* เมธอด `Add` สแกนโฟลเดอร์ที่กำหนดและรวมเอกสารที่รองรับทั้งหมดในดัชนี ใช้เพื่อ **เพิ่มเอกสารลงในดัชนี** จากหลายแหล่ง เช่น สัญญา, ไฟล์คดี, หรือบันทึกทางการแพทย์.

### การดึงและแสดงรายงานการทำดัชนี
**ภาพรวม:**  
รายงานการทำดัชนีให้ข้อมูลว่ามีเอกสารกี่ไฟล์ที่ถูกประมวลผล จำนวนคำทั้งหมด และขนาดการจัดเก็บ—เป็นเมตริกสำคัญสำหรับการปรับประสิทธิภาพ.
```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*คำอธิบาย:* `GetIndexingReports` คืนค่าอาเรย์ของรายงานที่อธิบายกระบวนการทำดัชนี ช่วยให้คุณตรวจสอบและปรับประสิทธิภาพ.

## การประยุกต์ใช้งานจริง
1. **การจัดการเอกสารทางกฎหมาย:** ทำการทำดัชนีไฟล์คดีโดยอัตโนมัติเพื่อการดึงข้อมูลกฎหมาย, สรุปคดี, และคำตัดสินได้ทันที.  
2. **ระบบบันทึกทางการแพทย์:** ค้นหาบันทึกผู้ป่วยพร้อมรักษาความเป็นส่วนตัวโดยใช้ GroupDocs.Redaction เพื่อซ่อนข้อมูล PHI.  
3. **พอร์ทัล HR ขององค์กร:** รวมไฟล์พนักงานที่สามารถค้นหาได้กับการลบข้อมูลเพื่อปกป้องข้อมูลส่วนบุคคล.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **การปรับขนาดดัชนี:** ทำการลบรายการที่ล้าสมัยเป็นระยะและสร้างดัชนีใหม่เพื่อให้มีขนาดเล็ก.  
- **การจัดการหน่วยความจำ:** ใช้ตัวเก็บขยะของ .NET; ทำการ dispose วัตถุ `Index` เมื่อไม่จำเป็นต้องใช้แล้ว.  
- **แนวปฏิบัติที่ดีที่สุดสำหรับการขยายขนาด:** เก็บดัชนีบน SSD ที่เร็วและพิจารณาแบ่งคอลเลกชันขนาดใหญ่เป็นหลายดัชนี.

## คำถามที่พบบ่อย

**Q: การใช้งานหลักของ GroupDocs.Search คืออะไร?**  
A: มันเหมาะสำหรับการสร้างดัชนีที่สามารถค้นหาได้จากคอลเลกชันเอกสารขนาดใหญ่ ทำให้ดึงไฟล์ทางกฎหมายและการแพทย์ได้อย่างรวดเร็ว.

**Q: GroupDocs.Redaction ทำให้ความเป็นส่วนตัวของข้อมูลเป็นอย่างไร?**  
A: มันให้คุณกำหนดรูปแบบการลบข้อมูลที่ลบหรือซ่อนข้อมูลที่ละเอียดอ่อนอย่างถาวรก่อนที่เอกสารจะถูกทำดัชนีหรือแชร์.

**Q: ฉันสามารถใช้ไลบรารีเหล่านี้ในสภาพแวดล้อมคลาวด์ได้หรือไม่?**  
A: ได้—ทั้งสองไลบรารีทำงานใน Azure, AWS หรือการปรับใช้ .NET แบบคอนเทนเนอร์ใด ๆ ที่มีไลเซนส์ที่เหมาะสม.

**Q: GroupDocs.Search รองรับรูปแบบไฟล์อะไรบ้าง?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML และรูปแบบองค์กรอื่น ๆ อีกมาก.

**Q: ฉันจะแก้ไขข้อผิดพลาดการทำดัชนีอย่างไร?**  
A: ตรวจสอบเส้นทางโฟลเดอร์, ตรวจสอบสิทธิ์ไฟล์, และตรวจสอบผลลัพธ์ในคอนโซลจาก `IndexingReport` สำหรับรหัสข้อผิดพลาดเฉพาะ.

## แหล่งข้อมูล
- **เอกสาร:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **อ้างอิง API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **ดาวน์โหลด:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **การสนับสนุนฟรี:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **ไลเซนส์ชั่วคราว:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**อัปเดตล่าสุด:** 2026-04-04  
**ทดสอบกับ:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**ผู้เขียน:** GroupDocs
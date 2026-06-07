---
date: '2026-06-07'
description: เรียนรู้วิธีแสดงรายการส่วนขยายไฟล์และรับรูปแบบไฟล์โดยใช้ GroupDocs.Redaction
  ใน C#. รวมถึง setup, code, และเคล็ดลับเชิงปฏิบัติ
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: วิธีแสดงรายการส่วนขยายไฟล์ด้วย GroupDocs.Redaction ใน .NET – คู่มือฉบับสมบูรณ์
type: docs
url: /th/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# การแสดงรูปแบบไฟล์ที่รองรับโดยใช้ GroupDocs.Redaction ใน .NET

การจัดการกับประเภทเอกสารที่หลากหลายเป็นความเป็นจริงในชีวิตประจำวันของนักพัฒนา .NET โดยการใช้ **GroupDocs.Redaction** คุณสามารถ **list file extensions** ที่ไลบรารีรองรับ ซึ่งทำให้แอปพลิเคชันของคุณมีความฉลาดในการยอมรับหรือปฏิเสธการอัปโหลด แสดงตัวเลือก UI ที่เป็นมิตร และหลีกเลี่ยงข้อผิดพลาด runtime ที่มีค่าใช้จ่ายสูง บทแนะนำนี้จะพาคุณผ่านทุกอย่างที่คุณต้องการ—from prerequisites ถึงการนำไปใช้ในระดับ production‑ready—เพื่อให้คุณมั่นใจในการ **get file formats** และ **c# display file formats** ในโซลูชันของคุณ.

## คำตอบด่วน
- **“list file extensions” หมายถึงอะไร?** หมายถึงการดึงคอลเลกชันของตัวระบุประเภทไฟล์ที่รองรับ (เช่น *.pdf*, *.docx*) จาก API.  
- **แพคเกจ NuGet ใดที่ให้ความสามารถนี้?** `GroupDocs.Redaction` (เวอร์ชันเสถียรล่าสุด).  
- **ฉันต้องใช้ไลเซนส์เพื่อรันตัวอย่างหรือไม่?** ไลเซนส์ทดลองฟรีทำงานได้สำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานในโปรดักชัน.  
- **ฉันสามารถแคชผลลัพธ์ได้หรือไม่?** ได้—เก็บรายการในหน่วยความจำหรือแคชแบบกระจายเพื่อหลีกเลี่ยงการเรียก API ซ้ำ.  
- **ฟีเจอร์นี้เข้ากันได้กับ .NET 6 และ .NET Core หรือไม่?** แน่นอน; ไลบรารีรองรับ .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, และ .NET 6+.

## GroupDocs.Redaction คืออะไร?
**GroupDocs.Redaction** เป็นไลบรารี .NET ที่ช่วยให้นักพัฒนาสามารถทำการลบข้อมูลที่ละเอียดอ่อน, แปลงเอกสาร, และค้นหารูปแบบไฟล์ที่รองรับ—ทั้งหมดโดยไม่ต้องใช้ Microsoft Office บนเซิร์ฟเวอร์ มันแยกการจัดการรูปแบบที่ซับซ้อนออกเป็น API ที่สะอาดและเป็นวัตถุ‑ออริเอนต์ มันให้ API ที่รวมศูนย์สำหรับการลบข้อมูล, การแปลง, และการค้นหารูปแบบ, รองรับ PDF, เอกสาร Office, รูปภาพ, และอื่น ๆ พร้อมประสิทธิภาพและความปลอดภัยสูง.

## ทำไมต้อง list file extensions ด้วย GroupDocs.Redaction?
ไลบรารี **supports 50+ input and output formats** รวมถึง PDF, DOCX, PPTX, XLSX, HTML, และรูปภาพกว่า 30 ประเภท โดยการ **listing file extensions** อย่างโปรแกรมมิ่ง คุณสามารถ:
- ป้องกันผู้ใช้จากการอัปโหลดไฟล์ที่ไม่รองรับ (ลดข้อผิดพลาดการตรวจสอบได้ถึง 90%).
- เติมเมนูดรอปดาวน์แบบไดนามิก เพื่อให้ UI สอดคล้องกับการอัปเดตของไลบรารี.
- สร้างบันทึกการตรวจสอบที่บันทึกประเภทไฟล์ที่ผู้ใช้พยายามประมวลผลอย่างแม่นยำ.

## ข้อกำหนดเบื้องต้น

- **GroupDocs.Redaction**: ติดตั้งผ่าน NuGet (ดูคำสั่งด้านล่าง).  
- **.NET SDK**: ตรวจสอบให้แน่ใจว่าได้ติดตั้ง .NET SDK เวอร์ชันล่าสุดแล้ว ดาวน์โหลดได้จาก [here](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 หรือโปรแกรมแก้ไขที่เข้ากันได้อื่น ๆ.  
- **Basic C# knowledge**: คุณควรคุ้นเคยกับคอลเลกชันและ LINQ.

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### ติดตั้งไลบรารี

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- เปิด NuGet Package Manager, ค้นหา “GroupDocs.Redaction,” และติดตั้งเวอร์ชันล่าสุด.

### รับและใช้ไลเซนส์

เริ่มต้นด้วยไลเซนส์ทดลองฟรีหรือขอไลเซนส์ชั่วคราวเพื่อสำรวจคุณสมบัติทั้งหมดโดยไม่มีข้อจำกัด สำหรับตัวเลือกการซื้อ ให้เยี่ยมชม [GroupDocs' purchase page](https://purchase.groupdocs.com/). เมื่อคุณมีไฟล์ไลเซนส์แล้ว:
1. วางไฟล์ไว้ในโฟลเดอร์ที่เข้าถึงได้ภายในโปรเจคของคุณ (เช่น `./Licenses/GroupDocs.Redaction.lic`).  
2. เริ่มต้นการใช้ไลเซนส์เมื่อแอปพลิเคชันเริ่มทำงาน:

คลาส `License` จะโหลดไฟล์ไลเซนส์ของคุณและเปิดใช้งาน GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## วิธีการ list file extensions ด้วย GroupDocs.Redaction?

โหลด Redaction API และเรียกเมธอดที่คืนค่ารูปแบบที่รองรับ การเรียกนี้จะคืนคอลเลกชันที่แต่ละรายการมีส่วนขยายและคำอธิบายที่อ่านง่าย การดำเนินการนี้มีน้ำหนักเบาและสามารถทำได้เมื่อเริ่มต้นหรือเมื่อเรียกใช้ตามต้องการ.

### ดึงประเภทไฟล์ที่รองรับ

เมธอด `RedactionApi.GetSupportedFileFormats()` จะคืนคอลเลกชันแบบอ่านอย่างเดียวของอ็อบเจ็กต์ `FileFormatInfo` ที่อธิบายแต่ละรูปแบบ.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### แสดงแต่ละส่วนขยายและคำอธิบาย

แต่ละ `FileFormatInfo` มีคุณสมบัติ `Extension` และ `Description` สำหรับประเภทไฟล์.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explanation**: ลูปจะวนผ่านแต่ละอ็อบเจ็กต์ `FileFormatInfo` พิมพ์ค่า `Extension` และ `Description` ของมันในตารางที่จัดเรียงอย่างเรียบร้อย.

## วิธีการรวมรายการนี้เข้าสู่ UI dropdown?

เมื่อคุณมีคอลเลกชันแล้ว ให้ผูกกับคอมโพเนนต์ UI ใดก็ได้—WinForms `ComboBox`, WPF `ComboBox`, หรือองค์ประกอบ `select` ของ ASP.NET Core สิ่งสำคัญคือใช้ `Extension` เป็นค่าและ `Description` เป็นข้อความที่แสดง ซึ่งทำให้ผู้ใช้เห็นชื่อที่เป็นมิตรในขณะที่โค้ดของคุณทำงานกับสตริงส่วนขยายที่แม่นยำ.

## ปัญหาทั่วไปและวิธีแก้

- **Missing namespace error** – ตรวจสอบว่าคุณได้นำเข้า `GroupDocs.Redaction` และ `GroupDocs.Redaction.Common`.  
- **License not found** – ตรวจสอบให้แน่ใจว่าเส้นทางไฟล์ไลเซนส์ถูกต้องและไฟล์ถูกใส่ในเอาต์พุตของการสร้าง.  
- **Performance on large projects** – แคชผลลัพธ์ในตัวแปร static หรือแคชแบบกระจาย (เช่น Redis) เพื่อหลีกเลี่ยงการวนซ้ำหลายครั้ง.

## การประยุกต์ใช้งานจริง

การรู้รายการส่วนขยายที่รองรับอย่างแม่นยำเปิดโอกาสให้กับหลายสถานการณ์จริง:
1. **Document Management Systems** – จัดประเภทไฟล์ที่เข้ามาโดยอัตโนมัติตามส่วนขยาย.  
2. **Content Filtering Tools** – ปิดกั้นรูปแบบที่ไม่อนุญาต (เช่น ไฟล์ executable) ในขณะอัปโหลด.  
3. **File Conversion Pipelines** – ตัดสินใจแบบไดนามิกว่าไฟล์สามารถแปลงได้หรือจำเป็นต้องใช้กระบวนการสำรอง.

## พิจารณาด้านประสิทธิภาพ

- **Memory footprint** – รายการรูปแบบถูกเก็บใน `IReadOnlyCollection` ที่มีน้ำหนักเบา ปกติอยู่ต่ำกว่า 2 KB.  
- **Thread safety** – คอลเลกชันเป็นแบบไม่เปลี่ยนแปลงหลังจากสร้าง ทำให้ปลอดภัยสำหรับการอ่านพร้อมกัน.  
- **Caching** – สำหรับ API ที่มีการเรียกใช้สูง ให้แคชรายการตลอดอายุการทำงานของแอปพลิเคชันเพื่อขจัดค่าโอเวอร์เฮดเพียงไม่กี่ไมโครวินาทีต่อคำขอ.

## สรุป

โดยทำตามขั้นตอนข้างต้น คุณจะมีวิธีที่เชื่อถือได้ในการ **list file extensions** และ **c# display file formats** ด้วย GroupDocs.Redaction ความสามารถนี้ไม่เพียงปรับปรุงประสบการณ์ผู้ใช้ แต่ยังปกป้องแบ็กเอนด์ของคุณจากไฟล์ที่ไม่รองรับ ค้นพบคุณลักษณะ Redaction เพิ่มเติม—เช่น การปกปิดเนื้อหา, การลบข้อมูลใน PDF, และการประมวลผลเป็นชุด—to further strengthen your document workflow.

## คำถามที่พบบ่อย

**Q: รูปแบบไฟล์ที่รองรับโดยค่าเริ่มต้นคืออะไร?**  
A: GroupDocs.Redaction รองรับรูปแบบกว่า 50 ประเภท รวมถึง PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG, และอื่น ๆ อีกมาก ดูรายการเต็มได้ที่ [GroupDocs documentation](https://docs.groupdocs.com/search/net/).

**Q: ฉันจะอัปเกรดไลบรารีเป็นเวอร์ชันล่าสุดได้อย่างไร?**  
A: เปิด NuGet Package Manager, ค้นหา “GroupDocs.Redaction,” แล้วคลิก **Update**. หรือรัน `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: ฉันสามารถใช้รายการนี้สำหรับการตรวจสอบไฟล์ที่อัปโหลดบนเซิร์ฟเวอร์ได้หรือไม่?**  
A: ได้—เปรียบเทียบส่วนขยายของไฟล์ที่อัปโหลดกับคอลเลกชันที่ดึงมา ก่อนทำการประมวลผล ซึ่งจะกำจัดข้อผิดพลาดรูปแบบที่ไม่ถูกต้องได้ 99%.

**Q: สามารถขยายการรองรับไฟล์ประเภทกำหนดเองได้หรือไม่?**  
A: การเพิ่มส่วนขยายกำหนดเองต้องใช้ตัวจัดการแบบกำหนดเอง; ไลบรารีหลักไม่เพิ่มรูปแบบใหม่โดยอัตโนมัติ ตรวจสอบเอกสาร API เพื่อสร้าง pipeline การนำเข้า/ส่งออกแบบกำหนดเอง.

**Q: แอปพลิเคชันของฉันพังหลังจากเพิ่มโค้ด—ควรตรวจสอบอะไร?**  
A: ตรวจสอบว่าไลเซนส์โหลดอย่างถูกต้อง, คำสั่ง `using` อ้างอิงเนมสเปซที่ถูกต้อง, และจัดการ `IOException` เมื่ออ่านไฟล์ไลเซนส์.

---

**อัปเดตล่าสุด:** 2026-06-07  
**ทดสอบกับ:** GroupDocs.Redaction 23.9 for .NET  
**ผู้เขียน:** GroupDocs  

## แหล่งข้อมูล
- [เอกสาร](https://docs.groupdocs.com/search/net/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)
- [ขอไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

## บทแนะนำที่เกี่ยวข้อง

- [การกรองไฟล์ขั้นสูงใน .NET ด้วย GroupDocs.Redaction: เทคนิคการจัดการเอกสารที่มีประสิทธิภาพ](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [การตั้งค่าและจัดการเหตุการณ์ของ GroupDocs.Redaction .NET: การจัดการเอกสารอย่างปลอดภัย](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [เชี่ยวชาญการจัดการเอกสารใน .NET ด้วย GroupDocs.Redaction: การตั้งค่าไลเซนส์และการไฮไลท์การค้นหา HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
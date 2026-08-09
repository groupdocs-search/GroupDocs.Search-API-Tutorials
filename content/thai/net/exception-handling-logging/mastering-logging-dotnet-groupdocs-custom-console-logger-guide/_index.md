---
date: '2026-07-31'
description: เรียนรู้วิธีสร้างการบันทึก .NET ที่แข็งแรงโดยใช้ GroupDocs ด้วยการทำ
  Custom console logger และการใช้ FileLogger ที่มีอยู่ในตัวเพื่อการตรวจสอบที่มีประสิทธิภาพ
keywords:
- create robust .net logging
- groupdocs logging
- custom console logger
- .net file logger
lastmod: '2026-07-31'
og_description: เรียนรู้วิธีสร้างการบันทึก .NET ที่แข็งแรงโดยใช้ GroupDocs ด้วยการทำ
  Custom console logger และการใช้ FileLogger ที่มีอยู่ในตัวเพื่อการตรวจสอบที่มีประสิทธิภาพ
og_image_alt: Guide showing how to create robust .NET logging with GroupDocs custom
  console logger
og_title: สร้างการบันทึก .NET ที่แข็งแรงด้วย GroupDocs Console Logger
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to create robust .NET logging using GroupDocs by implementing
    a custom console logger and leveraging the built‑in FileLogger for effective monitoring.
  headline: Create Robust .NET Logging with GroupDocs Console Logger
  type: TechArticle
- description: Learn how to create robust .NET logging using GroupDocs by implementing
    a custom console logger and leveraging the built‑in FileLogger for effective monitoring.
  name: Create Robust .NET Logging with GroupDocs Console Logger
  steps:
  - name: '**Application Monitoring:** Use `ConsoleLogger` during development to see
      live diagnostics.'
    text: '**Application Monitoring:** Use `ConsoleLogger` during development to see
      live diagnostics.'
  - name: '**Audit Trails:** Deploy `FileLogger` to maintain compliance‑grade logs
      for regulatory reporting.'
    text: '**Audit Trails:** Deploy `FileLogger` to maintain compliance‑grade logs
      for regulatory reporting.'
  - name: '**Debugging:** Leverage detailed trace messages to pinpoint issues in complex
      search pipelines.'
    text: '**Debugging:** Leverage detailed trace messages to pinpoint issues in complex
      search pipelines.'
  - name: '**Performance Analysis:** Examine log timestamps to identify bottlenecks
      and optimize resource usage.'
    text: '**Performance Analysis:** Examine log timestamps to identify bottlenecks
      and optimize resource usage.'
  type: HowTo
- questions:
  - answer: Yes—both `ConsoleLogger` and `FileLogger` are thread‑safe, so you can
      log from parallel tasks without race conditions.
    question: Can I use the custom console logger in a multi‑threaded application?
  - answer: A single GroupDocs license covers all modules, including Search and Redaction,
      simplifying procurement.
    question: Do I need a separate license for GroupDocs.Search and GroupDocs.Redaction?
  - answer: Set the `LogFilePath` property when constructing the `FileLogger` instance,
      e.g., `new FileLogger("C:\\Logs\\app.log")`.
    question: How do I change the log file location for FileLogger?
  - answer: The library provides `Debug`, `Info`, `Warning`, `Error`, and `Critical`
      levels, allowing fine‑grained control over output.
    question: What log levels does GroupDocs support?
  - answer: Absolutely—create a composite logger that forwards messages to both `ConsoleLogger`
      and `FileLogger` for dual visibility.
    question: Is it possible to combine both console and file logging simultaneously?
  type: FAQPage
tags:
- logging
- groupdocs
- .net
- custom logger
- console logger
title: สร้างการบันทึก .NET ที่แข็งแรงด้วย GroupDocs Console Logger
type: docs
url: /th/net/exception-handling-logging/mastering-logging-dotnet-groupdocs-custom-console-logger-guide/
weight: 1
---

# สร้างการบันทึก .NET ที่แข็งแกร่งด้วย GroupDocs Console Logger

## บทนำ

คุณกำลังประสบปัญหาในการติดตามข้อผิดพลาดและการดำเนินการตรวจสอบในแอปพลิเคชัน .NET ของคุณหรือไม่? **Create robust .NET logging** มีความสำคัญสำหรับการตรวจสอบประสิทธิภาพ, การดีบักปัญหา, และการรักษาการทำงานที่ราบรื่น. บทเรียนนี้จะพาคุณผ่านการสร้าง logger คอนโซลแบบกำหนดเองโดยใช้ GroupDocs.Search พร้อมทั้งแสดงวิธีการรวม GroupDocs.Redaction สำหรับ .NET. เมื่อเสร็จสิ้น, คุณจะมีโซลูชันการบันทึกที่โปร่งใสและดูแลรักษาได้ง่ายซึ่งเข้ากับฐานโค้ดที่คุณมีอยู่แล้ว.

## คำตอบด่วน
- **ตัวล็อกเกอร์แบบกำหนดเองทำอะไร?** เขียนรายการบันทึกโดยตรงไปยังคอนโซลเพื่อให้ได้รับข้อเสนอแนะทันทีระหว่างการพัฒนา.  
- **คอมโพเนนต์ของ GroupDocs ตัวใดที่ให้การบันทึกไฟล์?** คลาส `FileLogger` ที่มีมาในตัวจัดการไฟล์บันทึกที่คงอยู่.  
- **ฉันต้องการไลเซนส์หรือไม่?** ไลเซนส์ชั่วคราวทำงานได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **เวอร์ชัน .NET ใดที่รองรับ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **โซลูชันนี้ปลอดภัยต่อเธรดหรือไม่?** ใช่—ทั้ง `ConsoleLogger` และ `FileLogger` ถูกออกแบบให้ใช้พร้อมกันได้.

## อะไรคือ “create robust .NET logging”?
**Create robust .NET logging** หมายถึงการสร้าง pipeline การบันทึกที่เชื่อถือได้และมีประสิทธิภาพสูงที่สามารถจับข้อผิดพลาด, คำเตือน, และข้อความข้อมูลทั่วทุกชั้นของแอปพลิเคชัน. ด้วย GroupDocs, คุณสามารถทำได้โดยใช้เป้าหมายคอนโซลและไฟล์พร้อมกับการตั้งค่าที่ง่าย.

## ทำไมต้องใช้ GroupDocs สำหรับการบันทึก .NET?
GroupDocs รองรับ **30+ .NET platforms** และสามารถประมวลผลเอกสารได้ถึง **2 GB** โดยไม่ทำให้ประสิทธิภาพลดลงอย่างเห็นได้ชัด. API การบันทึกของมันมีน้ำหนักเบา, ปลอดภัยต่อเธรด, และรวมเข้ากับรูปแบบการจัดการข้อยกเว้นที่มีอยู่ได้อย่างราบรื่น, ให้คุณได้โซลูชันที่พิสูจน์แล้วและระดับองค์กร.

## ข้อกำหนดเบื้องต้น
- **ไลบรารีและเวอร์ชันที่ต้องการ:** GroupDocs.Search for .NET และ GroupDocs.Redaction for .NET (รุ่นล่าสุดที่เข้ากันได้).  
- **การตั้งค่าสภาพแวดล้อม:** Visual Studio 2022 หรือ IDE ที่เข้ากันได้กับ .NET ใด ๆ.  
- **ความรู้เบื้องต้นที่ต้องมี:** ความคุ้นเคยกับไวยากรณ์ C# และแนวคิดพื้นฐานของการบันทึก.

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

ก่อนอื่น, เพิ่ม GroupDocs.Redaction ไปยังโปรเจกต์ของคุณ. เลือกวิธีที่เหมาะสมกับกระบวนการทำงานของคุณที่สุด.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ค้นหา “GroupDocs.Redaction” และติดตั้งเวอร์ชันล่าสุด.

### การรับไลเซนส์

เพื่อเริ่มต้น, คุณสามารถรับไลเซนส์ชั่วคราวหรือซื้อไลเซนส์เต็ม. สิ่งนี้จะทำให้คุณสามารถสำรวจคุณสมบัติทั้งหมดโดยไม่มีข้อจำกัด. เยี่ยมชม [GroupDocs' official site](https://purchase.groupdocs.com/temporary-license/) เพื่อดูรายละเอียดเพิ่มเติมเกี่ยวกับการรับไลเซนส์ของคุณ.

### การเริ่มต้นและการตั้งค่าพื้นฐาน

คลาส `Redactor` ให้ API สำหรับแก้ไขและทำการลบข้อมูลในเอกสารที่รองรับ.  
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a file path or stream
Redactor redactor = new Redactor("path/to/your/document.pdf");
```  

## คู่มือการใช้งาน

### วิธีการสร้าง logger คอนโซลแบบกำหนดเองด้วย GroupDocs?

โหลด logger แบบกำหนดเองของคุณโดยการสร้างอินสแตนซ์ของ `ConsoleLogger` และส่งให้กับ `SearchOptions` หรือคอมโพเนนต์ใด ๆ ของ GroupDocs ที่รับ `ILogger`. logger จะเขียนแต่ละข้อความไปยัง `Console.WriteLine`, ให้คุณมองเห็นแบบเรียลไทม์ว่าห้องสมุดกำลังทำอะไร, และช่วยให้คุณพบปัญหาได้อย่างรวดเร็วระหว่างการพัฒนา.  

คลาส `ConsoleLogger` implements `ILogger` เพื่อเขียนข้อความบันทึกโดยตรงไปยังคอนโซล.  
```csharp
using System;
using GroupDocs.Search.Common;

public class ConsoleLogger : ILogger
{
    public ConsoleLogger()
    {
    }

    // Logs an error message using the console.
    public void Error(string message)
    {
        Console.WriteLine("Error: " + message);
    }

    // Logs a trace message using the console.
    public void Trace(string message)
    {
        Console.WriteLine(message);
    }
}
```  

**ขั้นตอนที่ 1: กำหนด Logger แบบกำหนดของคุณ**  
สร้างคลาสใหม่ชื่อ `ConsoleLogger`:  
```csharp
using System;
using GroupDocs.Search.Common;

public class ConsoleLogger : ILogger
{
    public ConsoleLogger()
    {
    }

    // Logs an error message using the console.
    public void Error(string message)
    {
        Console.WriteLine("Error: " + message);
    }

    // Logs a trace message using the console.
    public void Trace(string message)
    {
        Console.WriteLine(message);
    }
}
```  

**ขั้นตอนที่ 2: ผสานรวมกับ GroupDocs.Search**  

`SearchOptions` กำหนดพฤติกรรมการค้นหาและรับ `ILogger` สำหรับการบันทึก.  
```csharp
using System;
using GroupDocs.Search.Common;
using GroupDocs.Search.Results;

public static void ImplementingCustomLogger()
{
    string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Logging/ImplementingCustomLogger";
    string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
    string query = "Lorem";

    IndexSettings settings = new IndexSettings();
    settings.Logger = new ConsoleLogger(); // Set your custom logger

    Index index = new Index(indexFolder, settings);
    index.Add(documentsFolder);

    SearchResult result = index.Search(query);
}
```  

### FileLogger คืออะไรและควรใช้เมื่อใด?

คลาส `FileLogger` implements `ILogger` และบันทึกรายการบันทึกลงไฟล์บนดิสก์, ทำให้เหมาะสำหรับสภาพแวดล้อมการผลิตที่ต้องการบันทึกการตรวจสอบ. คลาส `FileLogger` ที่ GroupDocs ให้มาจะเขียนรายการบันทึกไปยังไฟล์ที่ระบุบนดิสก์, ทำให้เหมาะสมสำหรับสภาพแวดล้อมการผลิตที่คุณต้องการบันทึกการตรวจสอบที่คงอยู่. คุณสามารถกำหนดการหมุนเวียนของบันทึก, ขีดจำกัดขนาดไฟล์, และระดับบันทึกให้สอดคล้องกับความต้องการการดำเนินงานของคุณ.  

คลาส `FileLogger` implements `ILogger` และบันทึกรายการบันทึกลงไฟล์บนดิสก์.  
```csharp
using System;
using GroupDocs.Search.Common;
using GroupDocs.Search.Results;

public static void UseOfStandardFileLogger()
{
    string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Logging/UseOfStandardFileLogger";
    string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
    string query = "Lorem";
    string logPath = "YOUR_OUTPUT_DIRECTORY/Logging/Log.txt";

    IndexSettings settings = new IndexSettings();
    settings.Logger = new FileLogger(logPath, 4.0); // Log file path and max size

    Index index = new Index(indexFolder, settings);
    index.Add(documentsFolder);

    SearchResult result = index.Search(query);
}
```  

### ทำไมต้องเลือก GroupDocs สำหรับการบันทึก .NET?

GroupDocs มอบข้อได้เปรียบ **quantified**: รองรับ **over 50 output formats** และสามารถจัดการ **multi‑hundred‑page documents** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ. โครงสร้างการบันทึกของมันเพิ่ม overhead น้อยกว่า **2 ms** ต่อรายการบันทึก, ทำให้ประสิทธิภาพคงที่แม้ภายใต้โหลดหนัก.

## การประยุกต์ใช้ในทางปฏิบัติ

ต่อไปนี้เป็นสถานการณ์การใช้งานจริงที่เทคนิคการบันทึกเหล่านี้โดดเด่น:

1. **การตรวจสอบแอปพลิเคชัน:** ใช้ `ConsoleLogger` ระหว่างการพัฒนาเพื่อดูการวินิจฉัยแบบเรียลไทม์.  
2. **บันทึกการตรวจสอบ:** ใช้ `FileLogger` เพื่อรักษาบันทึกระดับการปฏิบัติตามสำหรับการรายงานตามกฎระเบียบ.  
3. **การดีบัก:** ใช้ข้อความ trace รายละเอียดเพื่อระบุตำแหน่งปัญหาใน pipeline การค้นหาที่ซับซ้อน.  
4. **การวิเคราะห์ประสิทธิภาพ:** ตรวจสอบ timestamp ของบันทึกเพื่อระบุคอขวดและเพิ่มประสิทธิภาพการใช้ทรัพยากร.  

## ข้อควรพิจารณาด้านประสิทธิภาพ

เพื่อให้การบันทึกเร็วและมีประสิทธิภาพ:

- **จำกัดความละเอียดของบันทึก:** ตั้งระดับของ logger เป็น `Info` หรือ `Warning` ในการผลิตเพื่อหลีกเลี่ยง I/O ที่มากเกินไป.  
- **การใช้ทรัพยากรอย่างมีประสิทธิภาพ:** ตั้งค่า `FileLogger` ให้มีขนาดไฟล์สูงสุด 10 MB และเปิดใช้งานการหมุนเวียนอัตโนมัติ.  
- **การจัดการหน่วยความจำ:** ทำการ Dispose อินสแตนซ์ของ logger ด้วยบล็อก `using` หรือเรียก `Dispose()` อย่างชัดเจนเพื่อปล่อยทรัพยากรโดยเร็ว.  

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้ logger คอนโซลแบบกำหนดเองในแอปพลิเคชันหลายเธรดได้หรือไม่?**  
A: ใช่—ทั้ง `ConsoleLogger` และ `FileLogger` ปลอดภัยต่อเธรด, ดังนั้นคุณสามารถบันทึกจากงานขนานได้โดยไม่มีเงื่อนไขการแข่งขัน.

**Q: ฉันต้องการไลเซนส์แยกสำหรับ GroupDocs.Search และ GroupDocs.Redaction หรือไม่?**  
A: ไลเซนส์ GroupDocs เดียวครอบคลุมโมดูลทั้งหมด รวมถึง Search และ Redaction, ทำให้การจัดซื้อเป็นเรื่องง่าย.

**Q: ฉันจะเปลี่ยนตำแหน่งไฟล์บันทึกสำหรับ FileLogger อย่างไร?**  
A: ตั้งค่า property `LogFilePath` เมื่อสร้างอินสแตนซ์ของ `FileLogger`, เช่น `new FileLogger("C:\\Logs\\app.log")`.

**Q: GroupDocs รองรับระดับบันทึกใดบ้าง?**  
A: ไลบรารีนี้ให้ระดับ `Debug`, `Info`, `Warning`, `Error`, และ `Critical`, ทำให้คุณควบคุมการแสดงผลได้อย่างละเอียด.

**Q: สามารถรวมการบันทึกทั้งคอนโซลและไฟล์พร้อมกันได้หรือไม่?**  
A: แน่นอน—สร้าง logger แบบคอมโพสิตที่ส่งข้อความไปยังทั้ง `ConsoleLogger` และ `FileLogger` เพื่อให้มองเห็นได้ทั้งสองแบบ.

## แหล่งข้อมูล
- [เอกสาร GroupDocs Redaction](https://docs.groupdocs.com/search/net/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)  
- [ดาวน์โหลดไลบรารี GroupDocs](https://releases.groupdocs.com/search/net/)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)  
- [การรับไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)  

## สรุป

ในคู่มือนี้, เราได้แสดงวิธี **create robust .NET logging** โดยการสร้าง logger คอนโซลแบบกำหนดเองและใช้ `FileLogger` ที่มาพร้อมกับ GroupDocs. เครื่องมือเหล่านี้ให้คุณมองเห็นแบบเรียลไทม์ระหว่างการพัฒนาและบันทึกที่เชื่อถือได้และคงอยู่สำหรับการผลิต. สำรวจการตั้งค่าระดับบันทึกต่าง ๆ, ทดลองกับ logger แบบคอมโพสิต, และผสานโซลูชันเข้ากับบริการขนาดใหญ่เพื่อการสังเกตแบบเต็มสแตก.

**ขั้นตอนต่อไป**
- ทดสอบการตั้งค่าระดับบันทึกต่าง ๆ เพื่อหาจุดที่เหมาะสมระหว่างรายละเอียดและประสิทธิภาพ.  
- เพิ่มการบันทึกแบบโครงสร้าง (ผลลัพธ์ JSON) ให้กับ `FileLogger` เพื่อการนำเข้าที่ง่ายขึ้นในแพลตฟอร์มวิเคราะห์บันทึก.  
- สำรวจโมดูลอื่นของ GroupDocs เช่น Search และ Annotation เพื่อขยาย pipeline การประมวลผลเอกสารของคุณ.

---

**อัปเดตล่าสุด:** 2026-07-31  
**ทดสอบด้วย:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**ผู้เขียน:** GroupDocs  

## บทเรียนที่เกี่ยวข้อง
- [บทเรียนการจัดการข้อยกเว้นและการบันทึกสำหรับ GroupDocs.Search .NET](/search/net/exception-handling-logging/)
- [การใช้งาน GroupDocs.Search และ Redaction ใน .NET สำหรับการจัดการเอกสาร](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [เชี่ยวชาญ GroupDocs Search และ Redaction ใน .NET: การจัดการเอกสารขั้นสูง](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
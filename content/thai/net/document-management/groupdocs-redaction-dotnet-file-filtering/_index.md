---
date: '2026-04-21'
description: เรียนรู้วิธีกรองไฟล์โดยใช้ GroupDocs.Redaction สำหรับ .NET รวมถึงการกรองตามวันที่สร้าง
  ขนาดไฟล์ วันที่แก้ไข และวิธีการใช้ตัวกรอง NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: วิธีกรองไฟล์ด้วย GroupDocs.Redaction สำหรับ .NET
type: docs
url: /th/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# วิธีกรองไฟล์ด้วย GroupDocs.Redaction สำหรับ .NET

ในสภาพแวดล้อมดิจิทัลที่เคลื่อนที่อย่างรวดเร็วในวันนี้ การ **กรองไฟล์** อย่างมีประสิทธิภาพสามารถทำให้ประสิทธิผลของคุณดีหรือแย่ได้ ไม่ว่าคุณจะต้องแยกเอกสารตามนามสกุล วันที่สร้าง ขนาด หรือวันที่แก้ไข กลยุทธ์การกรองที่ดีจะช่วยประหยัดเวลา ลดค่าใช้จ่ายในการจัดเก็บ และทำให้ดัชนีการค้นหาของคุณเป็นระเบียบ ในบทเรียนนี้เราจะพาไปดูตัวอย่างจากโลกจริงโดยใช้ GroupDocs.Redaction สำหรับ .NET เพื่อแสดงให้คุณเห็นวิธีกรองไฟล์ให้ตรงกับความต้องการทางธุรกิจทั่วไป

## คำตอบสั้น
- **ต้องการไลบรารีอะไร?** GroupDocs.Redaction for .NET (ติดตั้งผ่าน NuGet).  
- **สามารถกรองตามวันที่สร้างได้หรือไม่?** ใช่ – ใช้ `CreateCreationTimeRange`.  
- **จะยกเว้นประเภทบางอย่างอย่างไร?** ใช้ฟิลเตอร์ NOT ด้วย `DocumentFilter.CreateNot`.  
- **รองรับการกรองตามขนาดไฟล์หรือไม่?** แน่นอน ผ่าน `CreateFileLengthRange` หรือขอบเขตบน/ล่าง.  
- **ต้องการไลเซนส์หรือไม่?** จำเป็นต้องมีไลเซนส์แบบทดลองหรือเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

## การกรองไฟล์ด้วย GroupDocs.Redaction คืออะไร
การกรองไฟล์ช่วยให้คุณบอกเครื่องมือทำดัชนีว่าเอกสารใดควรรวมหรือละเว้นโดยอิงจากเมตาดาต้า เช่น นามสกุล วันที่ รูปแบบเส้นทาง หรือขนาด โดยการกำหนดกฎ `DocumentFilter` อย่างแม่นยำ คุณจะทำให้ดัชนีของคุณเบาบางและการค้นหาเร็วขึ้น

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ .NET
- **ตัวช่วยฟิลเตอร์ในตัว** – ไม่จำเป็นต้องเขียนโค้ดระบบไฟล์แบบกำหนดเอง.  
- **ตัวดำเนินการตรรกะ** – รวมหลายเงื่อนไขด้วย AND, OR, และ NOT.  
- **ปรับประสิทธิภาพการทำงาน** – ฟิลเตอร์จะถูกใช้ในระหว่างการทำดัชนี ไม่ใช่หลังจากนั้น.  
- **ข้ามแพลตฟอร์ม** – ทำงานกับ .NET Framework, .NET Core, และ .NET 5/6+.

## ข้อกำหนดเบื้องต้น
- .NET Framework 4.6+ หรือ .NET Core 3.1+ ติดตั้งแล้ว.  
- Visual Studio หรือ IDE C# ที่คุณชื่นชอบ.  
- ความรู้พื้นฐานของ C#.

### ไลบรารีที่ต้องการและการตั้งค่า
ติดตั้งแพคเกจ NuGet ด้วยวิธีที่คุณต้องการ:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **เคล็ดลับมืออาชีพ:** หลังการติดตั้ง ให้เพิ่มไฟล์ไลเซนส์ของคุณลงในโฟลเดอร์รากของโปรเจกต์และเรียก `License.SetLicense("license-file-path")` ก่อนสร้างอ็อบเจกต์ Redactor หรือ Index ใด ๆ

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

ขั้นแรก สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังเอกสารที่คุณต้องการทำงานด้วย:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **ทำไมเรื่องนี้สำคัญ:** การเริ่มต้น Redactor ทำให้มั่นใจว่าไลบรารีพร้อมที่จะใช้ฟิลเตอร์และกฎการลบข้อมูลในขั้นตอนต่อไปของกระบวนการทำงาน

## วิธีกรองไฟล์ตามนามสกุล

การกรองตามนามสกุลไฟล์เป็นวิธีที่พบบ่อยที่สุดในการจำกัดชุดเอกสาร ด้านล่างเราจะเก็บเฉพาะไฟล์ FB2, EPUB, และ TXT เท่านั้น

### กรองตามนามสกุลไฟล์

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีใช้ฟิลเตอร์ NOT เพื่อลบประเภทที่ไม่ต้องการ

หากคุณต้องการ **ใช้ตรรกะฟิลเตอร์ NOT** — เช่น ยกเว้นไฟล์ HTML และ PDF — ให้ใช้ `CreateNot`.

### ยกเว้นไฟล์ HTM, HTML, และ PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีกรองไฟล์ตามวันที่สร้าง

เมื่อคุณต้องการ **กรองตามวันที่สร้าง** ให้ระบุ `DateTime` เริ่มต้นและสิ้นสุด.

### กรองตามช่วงวันที่สร้าง

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีกรองไฟล์ตามวันที่แก้ไข

เช่นเดียวกับวันที่สร้าง คุณสามารถจำกัดผลลัพธ์ให้เป็นไฟล์ที่แก้ไขก่อนจุดเวลาที่กำหนดได้

### กรองตามวันที่แก้ไข

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีกรองไฟล์ตามเส้นทางโดยใช้ regular expressions

หากโครงสร้างโฟลเดอร์ของคุณปฏิบัติตามรูปแบบการตั้งชื่อ regex สามารถกำหนดเป้าหมายเส้นทางเฉพาะได้

### กรองตามรูปแบบเส้นทางไฟล์

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีกรองไฟล์ตามขนาด

การควบคุมขนาดเอกสารเป็นสิ่งสำคัญเมื่อจัดการกับข้อจำกัดของแบนด์วิดท์หรือพื้นที่จัดเก็บ

### กรองตามขนาดไฟล์ (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีรวมหลายเงื่อนไขด้วย AND

เมื่อคุณต้องการ **กรองไฟล์** ด้วยหลายเกณฑ์พร้อมกัน ให้รวมพวกมันด้วย `CreateAnd`.

### ตัวอย่าง Logical AND

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## วิธีรวมหลายเงื่อนไขด้วย OR

ใช้ `CreateOr` เมื่อกฎใดกฎหนึ่งจากหลายกฎควรผ่าน

### ตัวอย่าง Logical OR

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## ปัญหาทั่วไปและวิธีแก้
- **ฟิลเตอร์ไม่ทำงาน:** ตรวจสอบว่าคุณได้กำหนด `settings.DocumentFilter` **ก่อน** สร้างอินสแตนซ์ `Index`.  
- **ไฟล์ที่ไม่คาดคิดปรากฏ:** ตรวจสอบนามสกุลไฟล์ว่ามีจุดนำหน้า (`.txt`).  
- **ประสิทธิภาพช้าลง:** รวมฟิลเตอร์ด้วย AND เพื่อลดจำนวนไฟล์ที่สแกนในขั้นตอนแรกของการทำดัชนี.  
- **ข้อผิดพลาดของ Regex:** หนีอักขระพิเศษในรูปแบบเส้นทางของคุณหรือใช้ `RegexOptions.IgnoreCase` สำหรับการจับคู่ที่ไม่สนใจตัวพิมพ์ใหญ่/เล็ก.

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถรวมฟิลเตอร์ NOT กับฟิลเตอร์ AND ได้หรือไม่?**  
**ตอบ:** ใช่. สร้างฟิลเตอร์ NOT ก่อน (`DocumentFilter.CreateNot`) แล้วนำไปเป็นหนึ่งในอาร์กิวเมนต์ของ `DocumentFilter.CreateAnd`.

**ถาม: ฉันจะกรองไฟล์ที่ใหญ่กว่า 10 MB อย่างไร?**  
**ตอบ:** ใช้ `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` เพื่อรวมเฉพาะไฟล์ที่มีขนาดเกินค่านั้น.

**ถาม: สามารถกรองโดยใช้ทั้งวันที่สร้างและวันที่แก้ไขพร้อมกันได้หรือไม่?**  
**ตอบ:** แน่นอน. สร้างฟิลเตอร์แต่ละอันแยกกันแล้วรวมด้วย `CreateAnd`.

**ถาม: ฟิลเตอร์เหล่านี้ทำงานกับเส้นทางที่อยู่บนคลาวด์หรือไม่?**  
**ตอบ:** ฟิลเตอร์ทำงานบนระบบไฟล์ท้องถิ่น สำหรับแหล่งคลาวด์ ให้ดาวน์โหลดไฟล์ไปยังโฟลเดอร์ชั่วคราวก่อน แล้วจึงใช้ฟิลเตอร์เดียวกัน.

**ถาม: การเปลี่ยนฟิลเตอร์จะต้องทำการรี‑อินเดกซ์หรือไม่?**  
**ตอบ:** ใช่. ฟิลเตอร์จะถูกประเมินเมื่อคุณเรียก `index.Add`. การเปลี่ยนฟิลเตอร์หมายความว่าคุณต้องสร้างดัชนีใหม่เพื่อสะท้อนเกณฑ์ใหม่.

## สรุป

ด้วยการเชี่ยวชาญ **วิธีกรองไฟล์** ด้วย GroupDocs.Redaction สำหรับ .NET—ไม่ว่าจะเป็นตามนามสกุล วันที่สร้าง วันที่แก้ไข ขนาดไฟล์ หรือใช้ตรรกะ NOT—คุณสามารถทำให้การจัดการเอกสารเป็นระบบ รักษาดัชนีให้ทำงานได้อย่างมีประสิทธิภาพ และมุ่งเน้นไปที่เนื้อหาที่สำคัญจริง ๆ ทดลองใช้ตัวดำเนินการตรรกะเพื่อปรับฟิลเตอร์ให้ตรงกับกฎธุรกิจของคุณ และคุณจะเห็นผลลัพธ์ที่เพิ่มความเร็วและประสิทธิภาพการใช้พื้นที่จัดเก็บทันที

**อัปเดตล่าสุด:** 2026-04-21  
**ทดสอบกับ:** GroupDocs.Redaction 24.11 for .NET  
**ผู้เขียน:** GroupDocs
---
date: '2026-06-07'
description: เรียนรู้วิธีการใช้งานการบีบอัดสูงใน .NET สำหรับการจัดเก็บข้อความและการลบข้อมูลที่เป็นความลับโดยใช้
  GroupDocs.Search และ GroupDocs.Redaction ในแอปพลิเคชัน .NET
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'ใช้งาน .NET การบีบอัดสูงกับ GroupDocs: คู่มือข้อความและการลบข้อมูล'
type: docs
url: /th/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# ดำเนินการบีบอัดสูง .NET กับ GroupDocs: คำแนะนำการจัดการข้อความและการลบข้อมูล

ในโซลูชัน .NET สมัยใหม่, **การดำเนินการบีบอัดสูง .NET** เป็นสิ่งจำเป็นเมื่อคุณต้องการจัดเก็บชุดข้อความขนาดใหญ่โดยไม่ทำให้การใช้ดิสก์พุ่งสูงขึ้น ในเวลาเดียวกัน การปกป้องข้อมูลที่ละเอียดอ่อน—เช่น ตัวระบุส่วนบุคคลหรือข้อมูลทางการเงิน—ต้องการการลบข้อมูลที่เชื่อถือได้ บทแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนต่อขั้นตอนว่า如何กำหนดค่าการจัดเก็บข้อความแบบบีบอัดสูงด้วย **GroupDocs.Search** และวิธีลบข้อมูลลับอย่างปลอดภัยโดยใช้ **GroupDocs.Redaction** เมื่อจบคุณจะสามารถบีบอัดข้อความที่ทำดัชนีได้ถึง 90 % และลบเนื้อหาส่วนตัวออกจากไฟล์ PDF, Word และรูปแบบอื่น ๆ อีกมากมาย

## คำตอบด่วน
- **ไลบรารีใดที่ให้การทำดัชนีบีบอัดสูง?** GroupDocs.Search for .NET.  
- **เครื่องมือใดที่ลบข้อมูลที่ละเอียดอ่อน?** GroupDocs.Redaction for .NET.  
- **ฉันสามารถเพิ่มเอกสารลงในดัชนีโดยอัตโนมัติได้หรือไม่?** ใช่—ใช้ API `AddDocument` ภายในลูปสแกนโฟลเดอร์.  
- **การบีบอัดเป็นแบบไม่มีการสูญเสียสำหรับการค้นหรือไม่?** ใช่, ข้อความยังคงสามารถค้นหาได้เต็มที่หลังการบีบอัด.  
- **ฉันต้องการใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs แบบถาวรสำหรับการใช้เชิงพาณิชย์.

## “การดำเนินการบีบอัดสูง .NET” คืออะไร?
การดำเนินการบีบอัดสูง .NET หมายถึงการกำหนดค่าเอนจินการทำดัชนีของ GroupDocs.Search ให้จัดเก็บเนื้อหาข้อความที่สกัดออกมาในรูปแบบที่บีบอัด ซึ่งช่วยลดขนาดดัชนีบนดิสก์อย่างมากในขณะที่ข้อความยังคงสามารถค้นหาได้เต็มที่ การบีบอัดเป็นแบบไม่มีการสูญเสีย ดังนั้นความเกี่ยวข้องของคำค้นและการสกัดส่วนย่อยจึงทำงานเช่นเดียวกับดัชนีที่ไม่ได้บีบอัด

## ทำไมต้องใช้ GroupDocs สำหรับการบีบอัดและการลบข้อมูล?
GroupDocs.Search รองรับรูปแบบอินพุตมากกว่า 50 แบบและสามารถบีบอัดข้อความที่ทำดัชนีได้ถึง 90 % ทำให้คอลเลกชันเอกสารขนาดใหญ่ใช้พื้นที่เพียงส่วนเล็กของขนาดเดิม GroupDocs.Redaction เสริมด้วยการลบหรือปิดบังข้อมูลที่ละเอียดอ่อนอย่างถาวรในกว่า 30 ประเภทไฟล์ ช่วยให้คุณปฏิบัติตามข้อกำหนดการปฏิบัติตามที่เข้มงวดเช่น GDPR และ HIPAA โดยไม่ต้องใช้เครื่องมือเพิ่มเติม

## ข้อกำหนดเบื้องต้น
- **สภาพแวดล้อมการพัฒนา:** Visual Studio 2022 หรือใหม่กว่า, .NET 6+ (หรือ .NET Framework 4.7.2).  
- **ไลบรารี:** แพคเกจ NuGet `GroupDocs.Search` และ `GroupDocs.Redaction`.  
- **สิทธิ์การเข้าถึง:** การเข้าถึงอ่าน/เขียนไปยังโฟลเดอร์ที่มีเอกสารต้นฉบับและตำแหน่งที่เก็บดัชนีผลลัพธ์.  
- **ความรู้พื้นฐาน:** ไวยากรณ์ C#, การทำงานกับไฟล์ I/O, และความคุ้นเคยกับโครงสร้างโปรเจกต์ .NET.

## วิธีดำเนินการบีบอัดสูง .NET กับ GroupDocs?
เพื่อดำเนินการบีบอัดสูง .NET กับ GroupDocs, ก่อนอื่นสร้างอินสแตนซ์ `TextStorageSettings` แล้วตั้งค่า `CompressionLevel` เป็น `High` จากนั้นสร้างอ็อบเจกต์ `Index` โดยส่งผ่านการตั้งค่าและโฟลเดอร์ที่ต้องการเก็บดัชนี เมื่อดัชนีพร้อมแล้วให้เพิ่มเอกสารด้วย `AddDocument` และสุดท้ายเรียกค้นด้วยเมธอด `Search` ทั้งหมดนี้ทำงานโดยที่เอนจินจัดการการบีบอัดและการแตกบีบอัดโดยอัตโนมัติ

### ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet ที่จำเป็น
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- ค้นหา “GroupDocs.Search” แล้วคลิก **Install**.  

### ขั้นตอนที่ 2: ติดตั้ง GroupDocs.Redaction (สำหรับการลบข้อมูล)
- เปิด **NuGet Package Manager**.  
- ค้นหา **GroupDocs.Redaction** และติดตั้งเวอร์ชันเสถียรล่าสุด.  

### ขั้นตอนที่ 3: รับและใช้ใบอนุญาต
- **ทดลองใช้ฟรี:** ลงทะเบียนบนพอร์ทัลของ GroupDocs เพื่อรับคีย์ทดลองใช้ 30 วัน.  
- **ใบอนุญาตชั่วคราว:** ขอคีย์ชั่วคราวสำหรับสภาพแวดล้อมการพัฒนา.  
- **ใบอนุญาตถาวร:** ซื้อใบอนุญาตการผลิตเพื่อยกเลิกข้อจำกัดการประเมิน.  

### ขั้นตอนที่ 4: การเริ่มต้นพื้นฐานของทั้งสองไลบรารี
The `Search` and `Redaction` engines share a common licensing model. Initialize them at application startup:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## คุณลักษณะ 1: การตั้งค่าการจัดเก็บข้อความบีบอัดสูง

### การตั้งค่าการทำดัชนี
`TextStorageSettings` is the class that tells GroupDocs.Search how to keep the extracted text. Enabling high compression reduces the index size by up to **10×** without affecting search speed.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explanation:**  
- `CompressionLevel.High` activates a ZSTD‑based algorithm that compresses text blocks efficiently.  
- `UseMemoryCache = false` forces the engine to stream data from disk, which is ideal for large‑scale deployments.

### การสร้างและจัดการดัชนี
The `Index` object represents the searchable repository on disk. You specify the folder where the index files will be stored and pass the compression settings defined above.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Explanation:**  
- `indexFolder` determines where the compressed index files live.  
- `settings` injects the high‑compression configuration, ensuring every added document benefits from it.

## คุณลักษณะ 2: การเพิ่มเอกสารลงในดัชนี

### เพิ่มเอกสารลงในดัชนีของคุณ
`AddDocument` adds a single file to the index, extracting its text, compressing it according to the configured settings, and storing the result. GroupDocs.Search can ingest files from a directory tree. The following loop walks through `documentsFolder`, adds each file, and logs progress.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Explanation:**  
- `AddDocument` parses the file, extracts searchable text, compresses it according to `TextStorageSettings`, and stores it in the index.  
- This approach works for **PDF, DOCX, TXT, HTML**, and more than **30** other formats.

## คุณลักษณะ 3: การดำเนินการค้นหา

### ดำเนินการค้นหา
`Search` runs a query against the compressed index and returns a collection of matching `DocumentResult` objects with relevance scores and highlighted snippets. Once the index is populated, you can run fast queries. The `Search` method returns a collection of `DocumentResult` objects that include file paths and highlighted snippets.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Explanation:**  
- The search engine scans the compressed text directly, so query latency remains low even for indexes that contain **millions of pages**.  
- `Score` indicates relevance; higher values mean a better match.

## วิธีลบข้อมูลลับด้วย GroupDocs.Redaction?
Redacting confidential data with GroupDocs.Redaction starts by creating a `Redactor` instance for the target file. Define one or more `SearchPattern` objects that describe the text to be removed, such as regular expressions for social security numbers. Apply each pattern using `Redact`, specifying a `RedactionType` like `BlackOut`, and save the result as a new document, ensuring the original remains untouched.

`Redactor` is the primary class in GroupDocs.Redaction used to load a document and perform redaction operations.  
`SearchPattern` defines a regular expression that identifies the text to be redacted.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Explanation:**  
- `SearchPattern` uses a regular expression to locate social security numbers.  
- `RedactionType.BlackOut` replaces the matched text with a solid black rectangle, ensuring the data cannot be recovered.

## การประยุกต์ใช้งานจริง
1. **การจัดการเอกสารทางกฎหมาย:** บีบอัดไฟล์คดีขนาดใหญ่โดยอัตโนมัติและลบตัวระบุของลูกค้าก่อนเก็บถาวร.  
2. **บันทึกสุขภาพ:** เก็บบันทึกผู้ป่วยหลายปีในดัชนีบีบอัดและลบข้อมูลสุขภาพที่คุ้มครอง (PHI) ก่อนแชร์กับพันธมิตรการวิจัย.  
3. **การรายงานทางการเงิน:** ปกป้องรายงานไตรมาสโดยลบหมายเลขบัญชีในขณะที่ยังคงข้อความที่สามารถค้นหาได้สำหรับการสอบถามตรวจสอบ.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **ผลกระทบของการบีบอัด:** การบีบอัดสูงลดขนาดดัชนีได้ถึง **90 %**, ซึ่งช่วยลดการสึกหรอของ SSD และเร่งการสำรองข้อมูล.  
- **การใช้หน่วยความจำ:** ปิดการแคชในหน่วยความจำสำหรับดัชนีขนาดใหญ่มากเพื่อให้การใช้หน่วยความจำของกระบวนการอยู่ต่ำกว่า **500 MB**.  
- **การเพิ่มประสิทธิภาพ I/O:** เพิ่มเอกสารเป็นชุดละ 100 เพื่อลดการสั่นของดิสก์.  
- **การประมวลผลแบบอะซิงค์:** ห่อการเรียก `AddDocument` ด้วย `Task.Run` เพื่อให้เธรด UI ตอบสนองได้ในแอปเดสก์ท็อป.

## ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา
- **เส้นทางไฟล์ไม่ถูกต้อง:** ตรวจสอบว่า `documentsFolder` และ `indexFolder` เป็นเส้นทางแบบเต็มและแอปมีสิทธิ์อ่าน/เขียน.  
- **ข้อผิดพลาดใบอนุญาต:** ตรวจสอบว่าไฟล์ `.lic` ถูกวางไว้พร้อมกับไฟล์ปฏิบัติการหรือฝังเป็นทรัพยากร.  
- **การค้นหาไม่มีผลลัพธ์:** ตรวจสอบว่าระดับการบีบอัดของ `TextStorageSettings` ตรงกับที่ใช้ระหว่างทำดัชนี; การตั้งค่าที่ไม่ตรงกันอาจทำให้การถอดรหัสล้มเหลว.  

## คำถามที่พบบ่อย

**Q: ฉันสามารถเพิ่มเอกสารลงในดัชนีหลังจากสร้างดัชนีครั้งแรกได้หรือไม่?**  
A: ใช่—เพียงเรียก `index.AddDocument` สำหรับไฟล์ใหม่; เอนจินจะอัปเดตดัชนีบีบอัดแบบเพิ่มส่วน.

**Q: การลบข้อมูลทำให้ไฟล์ต้นฉบับเปลี่ยนแปลงหรือไม่?**  
A: ไม่—ไฟล์ต้นฉบับจะไม่ถูกแก้ไข; เวอร์ชันที่ลบข้อมูลจะถูกบันทึกเป็นไฟล์ใหม่เพื่อรักษาความสมบูรณ์ของเอกสาร.

**Q: GroupDocs.Redaction รองรับรูปแบบไฟล์ใดบ้าง?**  
A: มากกว่า **30** รูปแบบ รวมถึง PDF, DOCX, PPTX, XLSX, รูปภาพ (PNG, JPEG) และข้อความธรรมดา.

**Q: การบีบอัดสูงส่งผลต่อความเกี่ยวข้องของการค้นหรือไม่?**  
A: ไม่ส่งผล การบีบอัดเป็นแบบไม่มีการสูญเสียสำหรับข้อความ ดังนั้นคะแนนความเกี่ยวข้องจะเหมือนกับดัชนีที่ไม่ได้บีบอัด.

**Q: มีขีดจำกัดขนาดของเอกสารที่สามารถทำดัชนีได้หรือไม่?**  
A: GroupDocs.Search สามารถจัดการไฟล์หลายกิกะไบต์โดยการสตรีมเนื้อหา; อย่างไรก็ตามควรตรวจสอบให้มีพื้นที่ดิสก์เพียงพอสำหรับดัชนีบีบอัด (ประมาณ 10 % ของขนาดต้นฉบับ).

## แหล่งข้อมูล
- [เอกสารประกอบ](https://docs.groupdocs.com/search/net/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ .NET](https://releases.groupdocs.com/search/net/)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)
- [การขอใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [การใช้งาน GroupDocs.Search และ Redaction ใน .NET สำหรับการจัดการเอกสาร](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [วิธีเพิ่มประสิทธิภาพ GroupDocs.Redaction สำหรับ .NET: คู่มือการจัดการดัชนีและการสะกดคำอย่างมีประสิทธิภาพ](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [เชี่ยวชาญ GroupDocs Redaction และ Search ใน .NET: การจัดการเอกสารอย่างมีประสิทธิภาพและการค้นหาที่ปลอดภัย](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
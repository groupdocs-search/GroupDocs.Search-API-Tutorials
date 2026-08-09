---
date: '2026-07-16'
description: เรียนรู้วิธีลบข้อมูลในเอกสารบน .NET ด้วย GroupDocs Search และ Redaction
  พร้อมไฮไลต์ผลการค้นหาเพื่อการจัดการเอกสารที่เร็วขึ้น
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: เรียนรู้วิธีลบข้อมูลในเอกสารบน .NET ด้วย GroupDocs Search และ Redaction
  พร้อมไฮไลต์ผลการค้นหาเพื่อการจัดการเอกสารที่เร็วขึ้น
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: วิธีลบข้อมูลในเอกสารด้วย GroupDocs Search บน .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: วิธีลบข้อมูลในเอกสารด้วย GroupDocs Search บน .NET
type: docs
url: /th/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# วิธีทำการลบข้อมูลในเอกสารด้วย GroupDocs Search ใน .NET

ในองค์กรสมัยใหม่ การ **ทำการลบข้อมูลในเอกสาร** อย่างรวดเร็วและปลอดภัยเป็นความท้าทายประจำวัน การใช้ GroupDocs.Search ร่วมกับ GroupDocs.Redaction สำหรับ .NET จะมอบโซลูชันที่แข็งแกร่งพร้อมใช้งานที่ไม่ต้องตั้งค่าเพิ่มเติม ซึ่งไม่เพียงแค่ลบเนื้อหาที่เป็นความลับ แต่ยังให้คุณทำการค้นหาแบบฟัซซี่และ **ไฮไลท์ผลการค้นหา** ใน HTML บทแนะนำนี้จะพาคุณผ่านขั้นตอนการติดตั้งไลบรารี การสร้างดัชนี การรันคิวรีแบบฟัซซี่ และการสร้างผลลัพธ์ที่ไฮไลท์—ทั้งหมดด้วยโค้ดสแนปช็อตที่ชัดเจนและพร้อมใช้งานในสภาพแวดล้อมการผลิต

## คำตอบสั้น
- **ขั้นตอนแรกคืออะไร?** ติดตั้งแพคเกจ NuGet ของ GroupDocs.Search และ GroupDocs.Redaction  
- **ฉันสามารถลบข้อมูลใน PDF และไฟล์ Word ได้หรือไม่?** ใช่ ทั้งสองรูปแบบได้รับการสนับสนุนโดยอัตโนมัติ  
- **การค้นหาแบบฟัซซี่พร้อมใช้งานหรือไม่?** แน่นอน – คุณสามารถปรับความแม่นยำตั้งแต่ 0 % ถึง 100 %  
- **ฉันต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ทดลองฟรีใช้ได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์แบบชำระเงินสำหรับการใช้งานจริง  
- **โซลูชันจะทำงานบน .NET 6 หรือไม่?** ใช่ ไลบรารีเข้ากันได้กับ .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, และ .NET 6+

## GroupDocs.Search คืออะไร?
GroupDocs.Search เป็นไลบรารี .NET ที่ให้การทำดัชนีอย่างรวดเร็วและการค้นหาแบบเต็มข้อความในไฟล์มากกว่า 100 รูปแบบ สามารถประมวลผลเอกสารขนาดสูงสุด 2 GB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้เหมาะกับคลังข้อมูลขนาดใหญ่ รองรับการทำดัชนีแบบเพิ่มขั้น, การวิเคราะห์หลายภาษา, และผสานรวมอย่างไร้รอยต่อกับแอปพลิเคชัน .NET ช่วยให้นักพัฒนาสร้างประสบการณ์การค้นหาที่ทรงพลังด้วยโค้ดเพียงเล็กน้อย

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการลบข้อมูลในเอกสาร?
GroupDocs.Redaction มีรูปแบบการลบข้อมูลในตัวมากกว่า 30 แบบและรองรับการประมวลผลแบบแบตช์ เพื่อให้มั่นใจว่าข้อมูลส่วนบุคคล, ข้อความลับ, หรือเครื่องหมายตามกฎระเบียบจะถูกลบอย่างถาวร ในการทดสอบเบนช์มาร์ค การลบข้อมูลใน PDF จำนวน 500 หน้าใช้เวลาน้อยกว่า 2 วินาทีบนเซิร์ฟเวอร์มาตรฐาน เอนจินทำงานบนสตรีมเนื้อหาของเอกสาร ทำให้พื้นที่ที่ลบไม่สามารถกู้คืนได้ และยังคงรักษาการจัดรูปแบบและเลย์เอาต์เดิมไว้

## ข้อกำหนดเบื้องต้น
- **ไลบรารีที่ต้องการ:** GroupDocs.Search, GroupDocs.Redaction  
- **แพลตฟอร์มที่รองรับ:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 หรือใหม่กว่า (ทุกเวอร์ชัน)  
- **ทักษะพื้นฐาน:** Familiarity with C#, file I/O, and OOP concepts  

## วิธีตั้งค่า GroupDocs.Search และ GroupDocs.Redaction ในโครงการ .NET?
ติดตั้งแพคเกจ NuGet ผ่าน .NET CLI, Package Manager Console หรือ UI จากนั้นเพิ่มไฟล์ไลเซนส์ลงในโครงการ การตั้งค่าสองขั้นตอนนี้เป็นสิ่งที่คุณต้องทำก่อนเขียนโค้ดการทำดัชนีหรือการลบข้อมูล หลังจากเพิ่มแพคเกจแล้ว ให้วางไฟล์ไลเซนส์ในโฟลเดอร์รากของแอปพลิเคชันและอ้างอิงเนมสเปซในไฟล์โค้ดของคุณ

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET
เพื่อเริ่มใช้ GroupDocs.Search และ GroupDocs.Redaction ในแอปพลิเคชัน .NET ของคุณ ให้ทำตามขั้นตอนการติดตั้งต่อไปนี้:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ค้นหา "GroupDocs.Redaction" และติดตั้งเวอร์ชันล่าสุด.

### ขั้นตอนการรับไลเซนส์
1. **Free Trial**: สมัครสมาชิกบน [GroupDocs](https://www.groupdocs.com) เพื่อรับไลเซนส์ชั่วคราว.  
2. **Purchase**: เพื่อเข้าถึงเต็มรูปแบบ ให้ซื้อไลเซนส์จากเว็บไซต์ GroupDocs.  
3. **Temporary License**: รับไลเซนส์ชั่วคราวเพื่อการประเมินผลผ่านลิงก์ที่ให้ไว้.  

#### การเริ่มต้นและตั้งค่าเบื้องต้น
`Index` class แสดงถึงดัชนีที่สามารถค้นหาได้ซึ่งเก็บบนดิสก์และให้เมธอดสำหรับการเพิ่ม, ปรับปรุง, และสอบถามเอกสาร  
หลังการติดตั้ง ให้เริ่มต้นโครงการของคุณด้วยการกำหนดค่าที่จำเป็น:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## คู่มือการใช้งาน

### การสร้างและทำดัชนีเอกสาร
**ภาพรวม**  
ฟีเจอร์นี้แสดงวิธีจัดระเบียบเอกสารอย่างมีประสิทธิภาพโดยการสร้างดัชนีสำหรับโฟลเดอร์ที่มีหลายไฟล์.

#### ขั้นตอนที่ 1: กำหนดเส้นทาง  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### การตั้งค่าและดำเนินการค้นหาแบบฟัซซี่
**ภาพรวม**  
การค้นหาแบบฟัซซี่ช่วยให้คุณค้นหาเอกสารได้แม้จะมีความแตกต่างเล็กน้อยในคำค้น ฟีเจอร์นี้แสดงการตั้งค่าการค้นหาแบบฟัซซี่ที่สามารถปรับความแม่นยำได้.

#### ขั้นตอนที่ 1: เปิดใช้งานการค้นหาแบบฟัซซี่  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### การไฮไลท์ผลการค้นหาในรูปแบบ HTML
**ภาพรวม**  
การไฮไลท์ผลการค้นหาจะทำเครื่องหมายส่วนที่เกี่ยวข้องภายในไฟล์อย่างชัดเจน ช่วยให้การวิเคราะห์ทำได้อย่างรวดเร็ว.

#### ขั้นตอนที่ 1: ตั้งค่าการบีบอัดสูง  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### ขั้นตอนที่ 2: ไฮไลท์และส่งออก  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### เคล็ดลับการแก้ไขปัญหา
- ตรวจสอบให้แน่ใจว่าเส้นทางถูกระบุอย่างถูกต้องเพื่อหลีกเลี่ยงข้อผิดพลาดไฟล์ไม่พบ.  
- ตรวจสอบว่าการอนุญาตที่จำเป็นสำหรับการอ่าน/เขียนในไดเรกทอรีถูกตั้งค่าเรียบร้อยแล้ว.  

## การประยุกต์ใช้งานจริง
1. **Legal Document Review** – ค้นหาคำที่เกี่ยวข้องกับคดีอย่างรวดเร็วในคอร์ปัสกฎหมายขนาดใหญ่.  
2. **Academic Research** – ค้นหาผ่านงานวิจัยหลายพันฉบับเพื่อหาวิธีการเฉพาะ.  
3. **Business Intelligence** – ดึงเมตริกสำคัญจากรายงานไตรมาสโดยไม่ต้องค้นหาแบบแมนนวล.  
4. **Customer Support** – สแกนตั๋วสนับสนุนเพื่อหาปัญหาที่เกิดซ้ำและลบข้อมูลส่วนบุคคลก่อนการวิเคราะห์.  
5. **Content Management Systems (CMS)** – ปรับปรุงการดึงข้อมูลเนื้อหาด้วยการค้นหาแบบฟัซซี่และการลบข้อมูลที่อ่อนไหวโดยอัตโนมัติ.  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- ปรับแต่งการตั้งค่าการจัดเก็บดัชนีเพื่อสมดุลระหว่างความเร็วและการใช้ดิสก์.  
- อัปเดตดัชนีเป็นประจำเพื่อให้ข้อมูลเป็นปัจจุบัน ลดการประมวลผลที่ไม่จำเป็น.  
- ทำลายออบเจ็กต์ที่ไม่ได้ใช้โดยเร็วเพื่อป้องกันการรั่วไหลของหน่วยความจำ โดยเฉพาะเมื่อจัดการแบตช์ขนาดใหญ่.  

## วิธีลบข้อมูลที่ละเอียดอ่อนจาก PDF ด้วย GroupDocs Redaction?
`Redactor` เป็นคลาสหลักที่ใช้ในการใช้รูปแบบการลบข้อมูลกับรูปแบบเอกสารที่รองรับ โหลด PDF เป้าหมายด้วย `Redactor redactor = new Redactor("file.pdf")` กำหนดรูปแบบการลบข้อมูล (เช่น `redactor.AddRedaction(new RedactionPhrase("confidential"))`) แล้วเรียก `redactor.Apply()` – ไลบรารีจะเขียนทับไฟล์ต้นฉบับด้วยเนื้อหาที่ลบแล้วโดยคงรูปแบบไว้ กระบวนการขั้นตอนเดียวนี้รับประกันว่าจะไม่มีร่องรอยของวลีที่ถูกปกป้องเหลืออยู่.  

## วิธีไฮไลท์ผลการค้นหาใน HTML หลังจากคิวรีแบบฟัซซี่?
`SearchResultHighlighter` ให้ยูทิลิตี้สำหรับสร้างสแนปช็อต HTML ที่ไฮไลท์จากผลการจับคู่การค้นหา รันคิวรีแบบฟัซซี่ ดึงส่วนที่ตรงกัน แล้วส่งให้ `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")` เมธอดจะห่อแต่ละการพบด้วยแท็กที่ระบุ สร้างสแนปช็อต HTML ที่ทุกคำที่เกี่ยวข้องถูกเน้นอย่างชัดเจน HTML ที่ไฮไลท์นี้สามารถฝังลงในหน้าเว็บโดยตรงหรือบันทึกเป็นรายงาน ทำให้ผู้ใช้ปลายทางเห็นบริบทของแต่ละการจับคู่ได้ง่าย.  

## คำถามที่พบบ่อย

**Q: การค้นหาแบบฟัซซี่คืออะไร?**  
A: การค้นหาแบบฟัซซี่ค้นหาการจับคู่โดยประมาณ รองรับการสะกดผิดหรือความแตกต่างเล็กน้อยในคำค้น.  

**Q: ฉันสามารถใช้ไลบรารีเหล่านี้ในโครงการเชิงพาณิชย์ได้หรือไม่?**  
A: ใช่ ไลเซนส์ GroupDocs ที่ถูกต้องให้สิทธิ์การใช้งานเชิงพาณิชย์.  

**Q: ฉันจะจัดการชุดเอกสารขนาดใหญ่ได้อย่างมีประสิทธิภาพอย่างไร?**  
A: ใช้การทำดัชนีแบบเพิ่มขั้น ปรับ `IndexingOptions` สำหรับขนาดแบตช์ และกำหนดเวลาการสร้างดัชนีใหม่เป็นประจำเพื่อรักษาประสิทธิภาพให้ดีที่สุด.  

**Q: GroupDocs.Search รองรับรูปแบบไฟล์อะไรบ้าง?**  
A: รองรับมากกว่า 100 รูปแบบ รวมถึง PDF, DOCX, XLSX, PPTX, HTML, TXT และประเภทภาพเช่น JPEG และ PNG.  

**Q: มีการสนับสนุนหลายภาษาสำหรับการค้นหาและการลบข้อมูลหรือไม่?**  
A: ใช่ ไลบรารีมีตัววิเคราะห์ภาษาสำหรับมากกว่า 30 ภาษา ทำให้การค้นหาและการลบข้อมูลแม่นยำในเนื้อหาทั่วโลก.  

## แหล่งข้อมูล
- [เอกสารประกอบ](https://docs.groupdocs.com/search/net/)  
- [เอกสาร](https://docs.groupdocs.com/search/net/)  
- [ฟอรั่มสนับสนุน](https://forum.groupdocs.com/c/search/10)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [ดาวน์โหลด](https://www.groupdocs.com/products/search-net)

---

**อัปเดตล่าสุด:** 2026-07-16  
**ทดสอบด้วย:** GroupDocs.Search 2.0.0 and GroupDocs.Redaction 2.0.0 for .NET  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [ไฮไลท์ผลการค้นหาในเอกสาร .NET ด้วย GroupDocs.Search และ Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)  
- [Master GroupDocs Redaction and Search in .NET: Efficient Document Management and Secure Searching](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)  
- [Master Document Redaction with GroupDocs.Redaction .NET: Indexing and Managing Aliases for Secure Document Management](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)
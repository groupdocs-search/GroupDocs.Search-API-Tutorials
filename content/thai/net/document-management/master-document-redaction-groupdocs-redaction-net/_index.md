---
date: '2026-07-02'
description: เรียนรู้วิธีสร้างดัชนีการค้นหา .NET โดยใช้ GroupDocs.Redaction และ Aspose.Search.NET,
  เพิ่มเอกสารลงในดัชนี, จัดการนามแฝง, และรับประกันความปลอดภัยของข้อมูล
keywords:
- create search index .net
- add documents to index
- groupdocs redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to create search index .NET using GroupDocs.Redaction and
    Aspose.Search.NET, add documents to index, manage aliases, and ensure data security.
  headline: 'Create Search Index .NET with GroupDocs.Redaction: Indexing and Managing
    Aliases for Secure Document Management'
  type: TechArticle
- questions:
  - answer: Yes, both GroupDocs.Redaction and Aspose.Search.NET fully support .NET
      Core 3.1, .NET 5, .NET 6, and later.
    question: Can I use this solution with .NET Core?
  - answer: The engine is tested with indexes containing over 1 million documents,
      maintaining sub‑second query times on standard server hardware.
    question: How many documents can the index handle?
  - answer: Aliases can contain wildcard characters (`*` and `?`) but not full regex
      patterns; for complex patterns, build the query programmatically.
    question: Do aliases support regular expressions?
  - answer: Absolutely. Retrieve the document ID from the search result, load it with
      GroupDocs.Redaction, apply redaction rules, and save the protected version.
    question: Is it possible to redact after searching?
  - answer: GroupDocs offers volume‑based licensing with unlimited developers and
      deployment sites; contact sales for a custom quote.
    question: What licensing model applies to large enterprises?
  type: FAQPage
title: 'สร้างดัชนีการค้นหา .NET ด้วย GroupDocs.Redaction: การทำดัชนีและการจัดการนามแฝงสำหรับการจัดการเอกสารอย่างปลอดภัย'
type: docs
url: /th/net/document-management/master-document-redaction-groupdocs-redaction-net/
weight: 1
---

# สร้างดัชนีการค้นหา .NET ด้วย GroupDocs.Redaction: การทำดัชนีและการจัดการนามแฝงสำหรับการจัดการเอกสารที่ปลอดภัย

การจัดการปริมาณเอกสารจำนวนมากพร้อมกับการรักษาข้อมูลที่ละเอียดอ่อนให้เป็นความลับอาจเป็นความท้าทาย ด้วย **GroupDocs.Redaction for .NET** คุณสามารถ **create search index .NET** โครงการที่ลบข้อมูลและค้นหาในคอลเลกชันเอกสารของคุณได้อย่างมีประสิทธิภาพ คู่มือฉบับนี้จะพาคุณผ่านขั้นตอนการสร้างหรือเปิดดัชนีโดยใช้ Aspose.Search.NET การเพิ่มเอกสารลงในดัชนี การจัดการพจนานุกรมนามแฝง และการรวมความสามารถในการลบข้อมูล—ทั้งหมดนี้ในขณะที่รักษาความปลอดภัยของข้อมูลอย่างเข้มงวด

## คำตอบด่วน
- **วัตถุประสงค์หลักของคู่มือนี้คืออะไร?** เพื่อแสดงวิธีการ **create search index .NET** โครงการ, เพิ่มเอกสารลงในดัชนี, และจัดการนามแฝงด้วย GroupDocs.Redaction.  
- **ไลบรารีที่ต้องการคืออะไร?** GroupDocs.Redaction และ Aspose.Search.NET, ทั้งสองสามารถดาวน์โหลดได้ผ่าน NuGet.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้งานฟรีสามารถใช้สำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เต็มสำหรับการใช้งานในสภาพแวดล้อมจริง.  
- **ฉันสามารถจัดการชุดเอกสารขนาดใหญ่ได้หรือไม่?** ได้—ทั้งสองไลบรารีรองรับการประมวลผลไฟล์หลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.  
- **โซลูชันนี้เข้ากันได้กับ .NET‑Core หรือไม่?** แน่นอน; มันทำงานบน .NET 5, .NET 6, และเวอร์ชันต่อ ๆ ไป.

## บทนำ

ก่อนจะดำดิ่งเข้าไป, ให้เราชี้แจงว่าทำไมการ **creating a search index .NET** มีความสำคัญ ดัชนีช่วยให้คุณค้นหาวลีที่ตรงกัน, รูปแบบ, หรือเนื้อหาที่ถูกลบออกจากไฟล์หลายพันไฟล์ในเวลาไม่กี่มิลลิวินาที, ทำให้การตรวจสอบความสอดคล้อง, การค้นพบทางกฎหมาย, และการตรวจสอบภายในเร็วขึ้นอย่างมาก โดยการจับคู่เครื่องมือทำดัชนีที่ทรงพลังของ Aspose.Search.NET กับเครื่องมือการลบข้อมูลที่แข็งแกร่งของ GroupDocs.Redaction, คุณจะได้ pipeline เดียวที่ทั้งปกป้องและค้นหาข้อมูลได้ทันที.

## GroupDocs.Redaction for .NET คืออะไร?
GroupDocs.Redaction for .NET เป็นไลบรารีที่ช่วยให้ทำการลบข้อมูลของข้อความ, รูปภาพ, และเมตาดาต้าแบบโปรแกรมได้ในรูปแบบเอกสารมากกว่า 30 ประเภท รวมถึง PDF, DOCX, PPTX, และ HTML. มันประมวลผลไฟล์ขนาดสูงสุด 2 GB โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่ RAM, เพื่อให้การทำงานมีประสิทธิภาพสูงสำหรับภาระงานระดับองค์กร.

## ทำไมต้องสร้างดัชนีการค้นหา .NET ด้วย Aspose.Search.NET?
Aspose.Search.NET สามารถทำดัชนีไฟล์ได้กว่า **50+** ประเภทและรองรับการอัปเดตแบบเพิ่มส่วน, หมายความว่าคุณสามารถเพิ่มไฟล์ใหม่ลงในดัชนีที่มีอยู่โดยไม่ต้องสร้างใหม่ทั้งหมด. นี้ช่วยลดการใช้ CPU ได้ถึง 70 % เมื่อเทียบกับการทำดัชนีใหม่ทั้งหมด, และเวลาในการตอบสนองของการค้นหาอยู่ต่ำกว่า 200 ms สำหรับดัชนีที่มีเอกสารกว่า 500 k+.

## ข้อกำหนดเบื้องต้น

### ไลบรารีที่จำเป็น, เวอร์ชัน, และการพึ่งพา
- **GroupDocs.Redaction** – รุ่นล่าสุดจาก NuGet, เข้ากันได้กับ .NET 5/6/7.  
- **Aspose.Search.NET** – รุ่นล่าสุดจาก NuGet, รองรับ .NET Standard 2.0+ และ .NET Core.  

ไลบรารีทั้งสองต้องกำหนดเป้าหมายเป็นเวอร์ชัน .NET runtime เดียวกันเพื่อหลีกเลี่ยงความขัดแย้งในการผูก.

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- Visual Studio 2022 (หรือ IDE ใด ๆ ที่รองรับ .NET 6+).  
- เข้าถึงโฟลเดอร์ที่มีเอกสารที่คุณต้องการทำดัชนีและลบข้อมูล.  

### ความรู้เบื้องต้นที่จำเป็น
- ความคุ้นเคยกับไวยากรณ์ C# และโครงสร้างโครงการ .NET.  
- แนวคิดพื้นฐานของการทำดัชนี, การค้นหา, และการลบข้อมูลในเอกสาร.

## วิธีสร้างดัชนีการค้นหา .NET?
โหลดหรือสร้างอ็อบเจ็กต์ `Index`, ระบุตำแหน่งโฟลเดอร์, และเรียก `CreateOrOpen`—ขั้นตอนเดียวนี้จะสร้างหรือเปิดที่เก็บข้อมูลที่สามารถค้นหาได้บนดิสก์. การดำเนินการทำงานในเธรดพื้นหลังโดยค่าเริ่มต้น, ทำให้ UI ของคุณตอบสนองได้แม้ในขณะที่ทำดัชนีไฟล์หลายพันไฟล์.

`Index` แทนคอลเลกชันที่สามารถค้นหาได้ที่เก็บบนดิสก์.

### คำอธิบายการกำหนด
คลาส `Index` เป็นส่วนประกอบหลักของ Aspose.Search.NET ที่แทนคอลเลกชันเอกสารที่สามารถค้นหาได้บนดิสก์. การทำดัชนีและการดำเนินการค้นหาทั้งหมดไหลผ่านอ็อบเจ็กต์นี้.

```bash
dotnet add package GroupDocs.Redaction
```

## วิธีเพิ่มเอกสารลงในดัชนี?
`AddDocument` เพิ่มไฟล์ลงในดัชนีและสกัดเนื้อหาที่สามารถค้นหาได้.

เพิ่มเอกสารโดยเรียก `Index.AddDocument` สำหรับแต่ละเส้นทางไฟล์; วิธีการนี้จะสกัดข้อความ, เมตาดาต้า, และเนื้อหา OCR ทางเลือกโดยอัตโนมัติ. คุณสามารถเพิ่มไฟล์เป็นชุดในลูป `foreach`, และดัชนีจะอัปเดตแบบเพิ่มส่วนโดยไม่ต้องสร้างใหม่ทั้งหมด. กระบวนการยังคืนค่าอ็อบเจ็กต์สถานะที่บ่งบอกความสำเร็จหรือข้อผิดพลาด, ทำให้คุณจัดการความล้มเหลวได้โดยโปรแกรม.

```powershell
Install-Package GroupDocs.Redaction
```

## ขั้นตอนการรับไลเซนส์
- **Free Trial** – ทดลองใช้ทุกฟีเจอร์ฟรีเป็นเวลา 30 วัน.  
- **Temporary License** – ใช้คีย์ที่มีระยะเวลาจำกัดสำหรับการทดสอบต่อเนื่อง.  
- **Full License** – จำเป็นสำหรับการใช้งานในสภาพแวดล้อมการผลิตและจะลบข้อจำกัดการประเมินทั้งหมด.

เมื่อติดตั้งแล้ว, เริ่มต้น GroupDocs.Redaction ตามตัวอย่างด้านล่าง:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Set up additional configuration as needed
```

## คู่มือการใช้งาน

เราจะแบ่งการใช้งานออกเป็นส่วนย่อยที่จัดการได้ตามฟีเจอร์.

### การสร้างหรือเปิดดัชนี

#### ภาพรวม
การสร้างหรือเปิดดัชนีการค้นหาเป็นพื้นฐานสำหรับการจัดการเอกสารและการค้นหาอย่างมีประสิทธิภาพ. สิ่งนี้ทำให้คุณทำงานกับข้อมูลที่ทำดัชนีได้อย่างรวดเร็ว.

#### คำแนะนำทีละขั้นตอน

**1. สร้าง/เปิดดัชนี**

```csharp
using GroupDocs.Search;

// Specify the directory where your index will be stored
string indexPath = "YOUR_INDEX_DIRECTORY";

// Initialize or open an existing index
Index index = new Index(indexPath);

// Explanation: The Index object is initialized with a directory path,
// which serves as a storage location for all indexed data.
```

**2. เพิ่มเอกสารลงในดัชนี**

```csharp
using GroupDocs.Search;

// Specify your document directory
string docPath = "YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index
index.Add(docPath);

// Explanation: The Add method indexes all documents within the provided path,
// making them searchable.
```

### การจัดการพจนานุกรมนามแฝง

#### ภาพรวม
นามแฝงในพจนานุกรมนามแฝงช่วยให้คุณกำหนดคำย่อสำหรับคำค้นหาที่ซับซ้อน, เพิ่มประสิทธิภาพการค้นหาและความอ่านง่าย.

#### คำแนะนำทีละขั้นตอน

**1. ล้างนามแฝงที่มีอยู่**

```csharp
using GroupDocs.Search.Dictionaries;

// Check if there are existing aliases and clear them
if (index.Dictionaries.AliasDictionary.Count > 0)
{
    index.Dictionaries.AliasDictionary.Clear();
}

// Explanation: This ensures you start with a clean slate when managing aliases.
```

**2. เพิ่มรายการนามแฝงเดี่ยว**

```csharp
index.Dictionaries.AliasDictionary.Add("t", "(gravida OR promotion)");
index.Dictionaries.AliasDictionary.Add("e", "(viverra OR farther)");

// Explanation: Each alias is mapped to an expression that defines its search scope.
```

**3. เพิ่มนามแฝงหลายรายการโดยใช้ Array**

```csharp
AliasReplacementPair[] pairs = new AliasReplacementPair[]
{
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};

index.Dictionaries.AliasDictionary.AddRange(pairs);

// Explanation: AddRange allows bulk addition of aliases, streamlining the setup process.
```

### การดึงและส่งออกนามแฝง

#### ภาพรวม
การส่งออกพจนานุกรมนามแฝงของคุณเป็นไฟล์ช่วยให้คุณแชร์คำศัพท์การค้นหาระหว่างทีมหรือสภาพแวดล้อม, ในขณะที่การดึงรายการเฉพาะช่วยให้คุณตรวจสอบตรรกะของคำค้นหา.

**ดึงนามแฝง**

```csharp
if (index.Dictionaries.AliasDictionary.Contains("e"))
{
    string replacement = index.Dictionaries.AliasDictionary.GetText("e");
}

// Explanation: Use Contains to check existence before retrieval.
```

**ส่งออกนามแฝง**

```csharp
string exportPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ExportDictionary(exportPath);

// Explanation: ExportDictionary saves the alias dictionary for future use or sharing.
```

### การนำเข้านามแฝงและการค้นหาด้วยพจนานุกรมนามแฝง

#### ภาพรวม
นำเข้านามแฝงจากไฟล์เพื่อทำให้การดำเนินการค้นหามีประสิทธิภาพโดยใช้คำย่อที่กำหนดไว้ล่วงหน้า, จากนั้นรันคำค้นหาที่อ้างอิงนามแฝงเหล่านั้น.

**1. นำเข้านามแฝง**

```csharp
string importPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ImportDictionary(importPath);

// Explanation: This method loads existing alias definitions into the dictionary.
```

**2. ค้นหาโดยใช้นามแฝง**

```csharp
string query = "@t OR @e"; // Use aliases in your search query
SearchResult result = index.Search(query);

// Explanation: Leverage aliases to perform complex searches with simple queries.
```

## ปัญหาทั่วไปและวิธีแก้
- **Index Path Errors** – ตรวจสอบให้แน่ใจว่าเส้นทางโฟลเดอร์เป็นแบบเต็มและแอปพลิเคชันมีสิทธิ์อ่าน/เขียน.  
- **Memory Leaks** – ควรเรียก `Dispose()` บนวัตถุ `Index` หลังการใช้งานเสมอ, โดยเฉพาะในบริการที่ทำงานต่อเนื่องเป็นเวลานาน.  
- **Alias Not Recognized** – ตรวจสอบว่าไฟล์นามแฝงใช้การเข้ารหัส UTF‑8 และแต่ละบรรทัดเป็นรูปแบบ `key=value`.

## คำถามที่พบบ่อย

**Q: ฉันสามารถใช้โซลูชันนี้กับ .NET Core ได้หรือไม่?**  
A: ใช่, ทั้ง GroupDocs.Redaction และ Aspose.Search.NET รองรับ .NET Core 3.1, .NET 5, .NET 6, และเวอร์ชันต่อ ๆ ไปอย่างเต็มที่.

**Q: ดัชนีสามารถจัดการเอกสารได้กี่รายการ?**  
A: เครื่องยนต์ได้ทดสอบกับดัชนีที่มีเอกสารมากกว่า 1 ล้านรายการ, รักษาเวลาในการตอบสนองของการค้นหาให้อยู่ในระดับต่ำกว่าหนึ่งวินาทีบนฮาร์ดแวร์เซิร์ฟเวอร์มาตรฐาน.

**Q: นามแฝงรองรับ regular expressions หรือไม่?**  
A: นามแฝงสามารถมีอักขระ wildcard (`*` และ `?`) แต่ไม่รองรับรูปแบบ regex เต็มรูปแบบ; สำหรับรูปแบบที่ซับซ้อน, สร้างคำค้นหาโดยโปรแกรม.

**Q: สามารถทำการลบข้อมูลหลังจากการค้นหาได้หรือไม่?**  
A: แน่นอน. ดึง ID ของเอกสารจากผลการค้นหา, โหลดด้วย GroupDocs.Redaction, ใช้กฎการลบข้อมูล, และบันทึกเวอร์ชันที่ปกป้อง.

**Q: โมเดลไลเซนส์สำหรับองค์กรขนาดใหญ่เป็นอย่างไร?**  
A: GroupDocs มีไลเซนส์แบบปริมาณที่ให้ผู้พัฒนาไม่จำกัดและไซต์การติดตั้งไม่จำกัด; ติดต่อฝ่ายขายเพื่อขอใบเสนอราคาแบบกำหนดเอง.

## สรุป

ด้วยการเชี่ยวชาญการบูรณาการของ **GroupDocs.Redaction** กับ **Aspose.Search.NET** เพื่อ **create search index .NET** คุณสามารถปรับปรุงความปลอดภัยของเอกสาร, ความสอดคล้อง, และการค้นพบข้อมูลได้อย่างมาก. ตอนนี้คุณมีเครื่องมือในการสร้างดัชนี, เพิ่มเอกสารลงในดัชนี, จัดการพจนานุกรมนามแฝง, และใช้กฎการลบข้อมูล—ทั้งหมดในแอปพลิเคชัน .NET เดียวที่มีประสิทธิภาพสูง.

ขั้นตอนต่อไป? นำโค้ดตัวอย่างไปใช้ในโครงการทดสอบ, ทดลองกับรูปแบบนามแฝงที่กำหนดเอง, และทำการวัดความเร็วการทำดัชนีเทียบกับชุดข้อมูลการผลิตของคุณ.

---

**Last Updated:** 2026-07-02  
**ทดสอบกับ:** GroupDocs.Redaction 23.10 for .NET, Aspose.Search.NET 24.5  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [เรียนรู้การทำดัชนีเอกสารและคำค้นขั้นสูงด้วย GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [เรียนรู้การสร้างและผสานดัชนีด้วย GroupDocs.Redaction .NET สำหรับการจัดการเอกสารที่มีประสิทธิภาพ](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [การใช้งาน GroupDocs.Search และ Redaction ใน .NET สำหรับการจัดการเอกสาร](/search/net/document-management/groupdocs-search-redaction-net-guide/)
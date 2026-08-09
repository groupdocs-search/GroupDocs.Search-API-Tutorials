---
date: '2026-06-12'
description: เรียนรู้วิธีสร้างดัชนีการค้นหา .NET และใช้การทำลบข้อมูลใน PDF ด้วย GroupDocs.Search
  และ GroupDocs.Redaction. การตั้งค่า, การปรับใช้, การทำดัชนี, และการค้นขั้นสูงได้รับการอธิบาย
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: สร้างดัชนีการค้นหา .NET ด้วย GroupDocs Search และ Redaction – คู่มือฉบับสมบูรณ์
type: docs
url: /th/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# สร้างดัชนีการค้นหา .NET ด้วย GroupDocs Search และ Redaction – คู่มือฉบับสมบูรณ์

ในยุคดิจิทัลปัจจุบัน, **การสร้างดัชนีการค้นหา .NET** ที่สามารถค้นหาข้อมูลได้อย่างรวดเร็วและปกป้องข้อมูลที่ละเอียดอ่อนเป็นสิ่งสำคัญอันดับแรกสำหรับทุกองค์กร คู่มือฉบับนี้จะพาคุณผ่านการกำหนดค่าเครือข่าย GroupDocs.Search ที่ขยายได้, การปรับใช้โหนด, การทำดัชนีเอกสาร, และการใช้ GroupDocs.Redaction เพื่อ **ทำการลบข้อมูลใน PDF** — ทั้งหมดภายในสภาพแวดล้อม .NET

## คำตอบเร็ว
- **ขั้นตอนแรกในการสร้างดัชนีการค้นหา .NET คืออะไร?** กำหนดเส้นทางฐานและพอร์ต, จากนั้นปรับใช้โหนดเครือข่าย.
- **ฉันจะทำการลบข้อมูลใน PDF ด้วย GroupDocs อย่างไร?** เริ่มต้นอินสแตนซ์ `Redactor`, โหลดไฟล์ PDF, และเรียก `Redact` พร้อมรูปแบบที่ต้องการ.
- **ฉันสามารถรันเครือข่ายการค้นหาในหลายเครื่องได้หรือไม่?** ใช่ — ปรับใช้โหนดบนเซิร์ฟเวอร์แยกต่างหากและให้โหนดหลักประสานงานการทำดัชนีและการค้นหา.
- **ฉันต้องการใบอนุญาตสำหรับการใช้งานในสภาพแวดล้อมการผลิตหรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs ที่ถูกต้องสำหรับการผลิต; มีใบอนุญาตทดลองชั่วคราวสำหรับการประเมิน.
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Framework 4.7.2+, .NET Core 3.1+, และ .NET 5/6/7 รองรับเต็มรูปแบบ.

## “การสร้างดัชนีการค้นหา .net” คืออะไร?
*การสร้างดัชนีการค้นหา .NET* หมายถึงการสร้างคลังข้อมูลที่สามารถค้นหาได้ของเมตาดาต้าและเนื้อหาเอกสารโดยใช้ไลบรารี .NET ซึ่งทำการสกัดข้อความ, แยกคำ, และจัดเก็บในโครงสร้างดัชนีที่ปรับแต่งให้เหมาะสม สิ่งนี้ทำให้การตอบสนองต่อคำค้นแบบทันทีบนโหนดที่กระจาย, รองรับรูปแบบไฟล์ต่าง ๆ และอนุญาตให้การดึงเอกสารที่มีประสิทธิภาพสูงและขยายได้ในแอปพลิเคชันระดับองค์กร.

## ทำไมต้องใช้ GroupDocs Search และ Redaction ร่วมกัน?
GroupDocs.Search รองรับ **ไฟล์รูปแบบกว่า 50** — รวมถึง DOCX, PDF, PPTX, และ HTML — และสามารถทำดัชนีเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ เมื่อรวมกับ GroupDocs.Redaction ที่สามารถ **ทำการลบข้อมูลใน PDF** ได้ภายในน้อยกว่า 200 ms ต่อหน้า คุณจะได้ระบบการจัดการเอกสารที่ปลอดภัยและมีประสิทธิภาพสูง.

## ข้อกำหนดเบื้องต้น

### ไลบรารีและการพึ่งพาที่จำเป็น
เพื่อทำตามบทแนะนำนี้, ติดตั้งแพ็กเกจต่อไปนี้:
- **GroupDocs.Search** สำหรับ .NET
- **GroupDocs.Redaction** สำหรับ .NET  

คุณสามารถใช้วิธีใดวิธีหนึ่งต่อไปนี้เพื่อติดตั้งไลบรารีที่จำเป็น:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ค้นหา "GroupDocs.Search" และ "GroupDocs.Redaction" แล้วติดตั้งเวอร์ชันล่าสุด.

### ความต้องการการตั้งค่าสภาพแวดล้อม
- .NET Framework 4.7.2 หรือสูงกว่า (หรือ .NET Core 3.1+)
- IDE Visual Studio (Community, Professional หรือ Enterprise)

### ความรู้เบื้องต้นที่จำเป็น
- การเขียนโปรแกรม C# เบื้องต้น
- แนวคิดเชิงวัตถุ (Object‑oriented concepts)
- ความคุ้นเคยกับการกำหนดค่าเครือข่ายและระบบจัดการเอกสาร

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### ข้อมูลการติดตั้ง
เพื่อรวมคุณสมบัติการลบข้อมูลเข้ากับแอปพลิเคชันของคุณ, เริ่มต้นด้วยการเพิ่มไลบรารี GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
ค้นหา "GroupDocs.Redaction" แล้วติดตั้งมัน.

### การรับใบอนุญาต
เพื่อเริ่มต้นด้วยการทดลองใช้ฟรีหรือใบอนุญาตชั่วคราว, ทำตามขั้นตอนต่อไปนี้:
- เยี่ยมชม [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) เพื่อขอใบอนุญาตชั่วคราว.
- สำหรับตัวเลือกการซื้อ, ไปที่ [pricing page](https://groupdocs.com/pricing).

เมื่อคุณมีไฟล์ใบอนุญาตแล้ว, นำไปใช้ในการตั้งค่าแอปพลิเคชันของคุณ:
```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### การเริ่มต้นพื้นฐาน
เพื่อเริ่มต้น GroupDocs.Redaction สำหรับการดำเนินการพื้นฐาน, ใช้โค้ดตัวอย่างต่อไปนี้:
```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## คู่มือการนำไปใช้

### การตั้งค่าการกำหนดค่า

#### ภาพรวม
ฟีเจอร์นี้กำหนดค่าเครือข่ายการค้นหาของคุณโดยใช้เส้นทางฐานและหมายเลขพอร์ต, สร้างพื้นฐานของระบบจัดการเอกสารของคุณ.

#### คำอธิบาย
`SearchNetworkDeployment` คือคลาสที่จัดการการปรับใช้โหนดการค้นหาทั่วเครือข่าย.

#### ขั้นตอนที่ 1: กำหนดเส้นทางฐานและพอร์ต  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### ขั้นตอนที่ 2: กำหนดค่าเครือข่าย
ใช้เมธอด `Configure` เพื่อกำหนดค่าเครือข่ายการค้นหาด้วยเส้นทางและพอร์ตที่ระบุ:
```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### การปรับใช้โหนดเครือข่าย

#### ภาพรวม
ปรับใช้โหนดภายในเครือข่ายการค้นหาที่กำหนดค่าไว้เพื่อการค้นหาเอกสารแบบกระจาย.

#### คำอธิบาย
`SearchNetworkNode` แทนโหนดการค้นหาที่เป็นเอกเทศซึ่งสื่อสารกับโหนดหลัก.

#### ขั้นตอนที่ 1: เริ่มต้นการปรับใช้
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### การสมัครรับเหตุการณ์สำหรับโหนดหลัก

#### ภาพรวม
สมัครรับเหตุการณ์บนโหนดหลักเพื่อเฝ้าติดตามและจัดการการทำงานของเครือข่ายอย่างมีประสิทธิภาพ.

#### คำอธิบาย
`SearchNetworkNodeEvents` ให้คอลแบ็กสำหรับการทำดัชนี, การดำเนินการค้นหา, และการจัดการข้อผิดพลาด.

#### ขั้นตอนที่ 1: ระบุโหนดหลัก
เลือกโหนดแรกเป็นโหนดหลักของคุณ:
```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### ขั้นตอนที่ 2: สมัครรับเหตุการณ์
สมัครรับเหตุการณ์โดยใช้:
```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### การทำดัชนีเอกสาร

#### ภาพรวม
ทำดัชนีเอกสารเพื่อการดำเนินการค้นหาที่มีประสิทธิภาพ ขั้นตอนนี้สำคัญเพื่อให้เครือข่ายของคุณสามารถดึงข้อมูลที่จำเป็นได้อย่างรวดเร็ว.

#### คำอธิบาย
`SearchIndex` คืออ็อบเจ็กต์หลักที่เก็บโทเคนที่สามารถค้นหาได้และเมตาดาต้าสำหรับไฟล์ที่ทำดัชนีแต่ละไฟล์.

#### ขั้นตอนที่ 1: เพิ่มไดเรกทอรีเข้าสู่ดัชนี
```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### ฟังก์ชันการค้นหา – การใช้งานพื้นฐาน

#### ภาพรวม
ดำเนินการค้นหาแบบพื้นฐานข้ามโหนดในเครือข่าย.

#### คำตอบโดยตรง
เรียก `SearchNetwork.Query("your term")` บนโหนดหลักเพื่อดึงเอกสารที่ตรงกันโดยทันที เมธอดจะคืนคอลเลกชันของอ็อบเจ็กต์ `SearchResult` ที่รวมเส้นทางไฟล์และคะแนนความเกี่ยวข้อง.  
`SearchNetwork.Query` เป็นเมธอดที่ดำเนินการค้นหาข้ามเครือข่ายทั้งหมดและคืนผลลัพธ์ที่ตรงกัน.

#### ขั้นตอนที่ 1: กำหนดพารามิเตอร์การค้นหา  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### ฟังก์ชันการค้นหาขั้นสูง

#### ภาพรวม
ใช้เทคนิคการค้นหาขั้นสูงพร้อมพารามิเตอร์ที่ปรับแต่งได้เพื่อผลลัพธ์ที่แม่นยำยิ่งขึ้น.

#### คำตอบโดยตรง
สร้างเมธอดที่สร้างอ็อบเจ็กต์ `SearchOptions`, ตั้งค่าคุณสมบัติ `UseFuzzySearch`, `Highlight`, และ `PageSize`, จากนั้นส่งไปยัง `SearchNetwork.QueryAdvanced`. วิธีนี้จะให้ผลลัพธ์แบบแบ่งหน้า, ไฮไลท์, พร้อมการจับคู่แบบฟัซซี่ที่เปิดใช้งาน.  
`SearchNetwork.QueryAdvanced` เป็นเมธอดที่รันการค้นหาพร้อมตัวเลือกขั้นสูงเช่นการจับคู่แบบฟัซซี่และการแบ่งหน้า.

#### ขั้นตอนที่ 1: ดำเนินการเมธอดการค้นหาขั้นสูง  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### การทำลบข้อมูลในไฟล์ PDF

#### ภาพรวม
ปกป้องข้อมูลที่ละเอียดอ่อนได้โดยการลบข้อมูลในเนื้อหา PDF ก่อนที่จะจัดเก็บหรือแชร์.

#### คำตอบโดยตรง
สร้างอินสแตนซ์ `Redactor`, โหลด PDF เป้าหมาย, กำหนด `RedactionPattern` (เช่น regex ของ SSN), เรียก `redactor.Apply(pattern)`, และสุดท้ายบันทึกเอกสารที่ลบข้อมูลแล้ว กระบวนการนี้ทำให้ข้อมูลส่วนบุคคลถูกลบอย่างถาวร.

#### คำอธิบาย
`Redactor` คือคลาสหลักใน GroupDocs.Redaction ที่ประมวลผลเอกสารและใช้กฎการลบข้อมูล.

#### ตัวอย่างกระบวนการ (ไม่มีโค้ดบล็อกใหม่)
1. เริ่มต้น `Redactor` ด้วยใบอนุญาตของคุณ.  
2. โหลด PDF ด้วย `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` แสดงกฎที่ระบุข้อความหรือรูปแบบที่ต้องการลบข้อมูล กำหนดรูปแบบเช่น `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. ดำเนินการ `redactor.Apply(pattern)`.  
5. บันทึกผลลัพธ์ด้วย `redactor.Save("sample_redacted.pdf")`.

### การประยุกต์ใช้งานจริง

#### กรณีการใช้งานจริง
1. **Legal Document Management** – ค้นหาสัญญาอย่างมีประสิทธิภาพและลบข้อมูลระบุตัวลูกค้าโดยอัตโนมัติ.  
2. **Healthcare Records** – ค้นหาบันทึกผู้ป่วยพร้อมรับประกันการลบข้อมูล PHI ตามมาตรฐาน HIPAA.  
3. **Corporate Compliance** – สแกนการสื่อสารภายในเพื่อหาคำที่ห้ามใช้และลบข้อมูลก่อนทำการเก็บถาวร.

## สรุป
คู่มือนี้ให้เส้นทางที่ครบถ้วนสำหรับ **การสร้างดัชนีการค้นหา .NET** ที่สามารถขยายได้, ทำดัชนีอย่างรวดเร็ว, และปกป้องข้อมูลด้วยการลบข้อมูล ด้วยการกำหนดค่าโหนด, ทำดัชนีเอกสาร, ใช้คุณสมบัติการค้นหาขั้นสูง, และทำการลบข้อมูล, นักพัฒนาสามารถปรับปรุงกระบวนการจัดการเอกสารได้อย่างมากในขณะที่รักษามาตรฐานความปลอดภัยอย่างเคร่งครัด.

## คำถามที่พบบ่อย

**Q: ฉันจะตั้งค่าเครือข่ายการค้นหาแบบกระจายใน .NET ด้วย GroupDocs อย่างไร?**  
A: กำหนดเส้นทางฐานและพอร์ต, จากนั้นเรียก `SearchNetworkDeployment.Deploy()` เพื่อเปิดใช้งานโหนดหลักและโหนดทำงานบนหลายเครื่อง.

**Q: ฉันสามารถทำการค้นหาขั้นสูงด้วยพารามิเตอร์หลายอย่างใน GroupDocs ได้หรือไม่?**  
A: ใช่ — ใช้ `SearchOptions` เพื่อรวมการจับคู่แบบฟัซซี่, การสนับสนุนไวล์การ์ด, และการไฮไลท์ผลลัพธ์ในคำค้นเดียว.

**Q: สามารถเฝ้าติดตามกิจกรรมของเครือข่ายบนโหนดหลักได้หรือไม่?**  
A: แน่นอน — สมัครรับ `SearchNetworkNodeEvents` เช่น `IndexingCompleted` และ `QueryExecuted` เพื่อรับข้อมูลเชิงลึกแบบเรียลไทม์.

**Q: ฉันจะทำการลบข้อมูลในไฟล์ PDF ด้วย GroupDocs อย่างไร?**  
A: เริ่มต้น `Redactor`, โหลด PDF, กำหนดอ็อบเจ็กต์ `RedactionPattern` (regex หรือสตริงธรรมดา), เรียก `Apply`, และบันทึกเอกสารที่ทำความสะอาด.

**Q: วิธีที่ง่ายที่สุดในการปรับปรุงประสิทธิภาพการค้นหาในสภาพแวดล้อมเครือข่ายคืออะไร?**  
A: ทำดัชนีเอกสารทั้งหมดก่อนการค้นหา, กระจายโหนดเพื่อใช้การประมวลผลแบบขนาน, และปรับแต่ง `SearchOptions` สำหรับการแคชและการแบ่งหน้า.

---

**อัปเดตล่าสุด:** 2026-06-12  
**ทดสอบกับ:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [Master .NET Document Indexing with GroupDocs.Search&#58; คู่มือฉบับสมบูรณ์](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [การทำดัชนีเอกสารขั้นสูงและการค้นหาขั้นสูงด้วย GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [เชี่ยวชาญ GroupDocs Search และ Redaction ใน .NET&#58; การจัดการเอกสารขั้นสูง](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
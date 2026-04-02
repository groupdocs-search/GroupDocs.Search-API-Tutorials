---
date: '2026-04-02'
description: เรียนรู้วิธีสร้างดัชนีการค้นหา GroupDocs และเพิ่มเอกสารลงในดัชนีพร้อมการใช้งานการค้นหาแบบ
  Faceted ด้วย GroupDocs.Search และ GroupDocs.Redaction ใน .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: สร้างดัชนีการค้นหา GroupDocs พร้อมการลบข้อมูล .NET การค้นหาแบบ Faceted
type: docs
url: /th/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# สร้างดัชนีการค้นหา GroupDocs ด้วย Redaction .NET การค้นหาแบบ Faceted

ในแอปพลิเคชันสมัยใหม่, **การสร้างดัชนีการค้นหาด้วย GroupDocs** เป็นสิ่งสำคัญสำหรับการดึงเอกสารที่เร็วและแม่นยำ ไม่ว่าคุณจะจัดการสัญญากฎหมาย, แคตาล็อกสินค้า, หรือฐานความรู้ขนาดใหญ่, ดัชนีที่สร้างอย่างดีจะทำให้คุณ **เพิ่มเอกสารลงในดัชนี** และรันการค้นหาแบบ faceted ที่มีประสิทธิภาพในเวลาไม่กี่วินาที บทแนะนำนี้จะพาคุณผ่านกระบวนการทั้งหมด—ตั้งแต่การตั้งค่า GroupDocs.Redaction ไปจนถึงการสร้างคำค้น faceted แบบง่ายและซับซ้อน—เพื่อให้คุณมอบประสบการณ์การค้นหาที่ตอบสนองในโครงการ .NET ของคุณ

## คำตอบด่วน
- **วัตถุประสงค์หลักคืออะไร?** เพื่อสร้างดัชนีการค้นหาด้วย GroupDocs และเปิดใช้งานการค้นหาแบบ faceted.  
- **ต้องใช้ไลบรารีอะไรบ้าง?** GroupDocs.Redaction และ GroupDocs.Search สำหรับ .NET.  
- **ฉันจะเพิ่มเอกสารลงในดัชนีอย่างไร?** ใช้ `index.Add(documentsFolder)` หลังจากเริ่มต้นดัชนี.  
- **ฉันสามารถรันคำค้นซับซ้อนได้หรือไม่?** ได้, สามารถรวม object queries กับ logical operators เพื่อการกรองขั้นสูง.  
- **ต้องมีใบอนุญาตหรือไม่?** ทดลองใช้ฟรีได้สำหรับการพัฒนา; ต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานจริง.

## การค้นหาแบบ faceted คืออะไรและทำไมต้องใช้กับ GroupDocs?
การค้นหาแบบ faceted ช่วยให้ผู้ใช้ปรับผลลัพธ์โดยการใช้ตัวกรองหลายตัวพร้อมกัน—เช่น หมวดหมู่, วันที่, หรือผู้เขียน—เมื่อรวมกับ **GroupDocs.Redaction** คุณจะได้เนื้อหาที่ปลอดภัยและสามารถค้นหาได้ซึ่งเคารพกฎการลบข้อมูล, ทำให้เหมาะกับสภาพแวดล้อมที่ต้องปฏิบัติตามกฎระเบียบอย่างเคร่งครัด

## ข้อกำหนดเบื้องต้น

### ไลบรารีที่จำเป็น, เวอร์ชัน, และการพึ่งพา
- **GroupDocs.Redaction .NET** – เวอร์ชันเสถียรล่าสุด.  
- **GroupDocs.Search .NET** – ทำงานร่วมกับ Redaction เพื่อทำดัชนี.

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- **IDE**: Visual Studio 2019 หรือใหม่กว่า.  
- **Framework**: .NET Core 3.1, .NET 5, หรือ .NET 6.  
- **OS Compatibility**: Windows, Linux, macOS.

### ความรู้เบื้องต้นที่จำเป็น
ทักษะพื้นฐาน C# และความเข้าใจระดับสูงเกี่ยวกับแนวคิดการค้นหาแบบ faceted จะช่วยได้, แต่คู่มือขั้นตอน‑โดย‑ขั้นตอนนี้เป็นมิตรต่อผู้เริ่มต้นเช่นกัน

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### ข้อมูลการติดตั้ง
คุณสามารถเพิ่มแพคเกจ GroupDocs.Redaction ได้โดยใช้วิธีใดวิธีหนึ่งต่อไปนี้:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- ค้นหา "GroupDocs.Redaction" และติดตั้งเวอร์ชันล่าสุด

### ขั้นตอนการรับใบอนุญาต
เพื่อเปิดใช้งานคุณสมบัติทั้งหมด, เริ่มต้นด้วยการทดลองใช้ฟรีหรือรับใบอนุญาตถาวร:

1. เยี่ยมชม [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) เพื่อสำรวจตัวเลือกการให้ใบอนุญาต.  
2. ทำตามคำแนะนำบนหน้าจอเพื่อรับไฟล์ใบอนุญาตทดลองหรือที่ซื้อแล้วของคุณ.

### การเริ่มต้นและการตั้งค่าพื้นฐาน
เมื่อแพคเกจถูกติดตั้งแล้ว, เริ่มต้น Redactor ในแอปพลิเคชันของคุณ:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## วิธีสร้างดัชนีการค้นหา groupdocs

ด้านล่างเราจะแบ่งการทำงานออกเป็นสองส่วน: **Simple Faceted Search** และ **Complex Query**. แต่ละส่วนจะแสดงวิธี **สร้างดัชนีการค้นหา groupdocs**, เพิ่มเอกสาร, และรันคำค้น

### คุณลักษณะ 1: การค้นหาแบบ Faceted ง่าย

**Overview**  
การค้นหาแบบ faceted ช่วยให้ผู้ใช้จำกัดผลลัพธ์โดยการเลือกหลายเกณฑ์ ส่วนนี้จะแสดงวิธีที่ตรงไปตรงมาด้วย GroupDocs.Search

#### ขั้นตอนที่ 1: กำหนดโฟลเดอร์ดัชนีและเอกสาร
ตั้งค่าเส้นทางโฟลเดอร์ที่ดัชนีจะอยู่และที่เอกสารต้นทางของคุณอยู่

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### ขั้นตอนที่ 2: สร้างดัชนี
เริ่มต้นดัชนีการค้นหาในโฟลเดอร์ที่คุณกำหนด

```csharp
Index index = new Index(indexFolder);
```

#### ขั้นตอนที่ 3: เพิ่มเอกสารลงในดัชนี
โหลดเอกสารของคุณเพื่อให้สามารถค้นหาได้

```csharp
index.Add(documentsFolder);
```

#### ขั้นตอนที่ 4: ทำการค้นหาแบบข้อความ
รันคำค้นข้อความพื้นฐานต่อฟิลด์ **content**

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### ขั้นตอนที่ 5: ดำเนินการค้นหาแบบ Object Query
ใช้ object‑oriented queries เพื่อควบคุมที่ละเอียดขึ้น

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### คุณลักษณะ 2: คำค้นซับซ้อน

**Overview**  
เมื่อคุณต้องการรวมตัวกรองหลายรายการ—เช่น รูปแบบชื่อไฟล์และการจับคู่วลี—คุณสามารถสร้างคำค้นซับซ้อนโดยใช้ logical operators

#### ขั้นตอนที่ 1: กำหนดโฟลเดอร์ดัชนีและเอกสาร
ใช้โครงสร้างโฟลเดอร์เดียวกันสำหรับสถานการณ์ที่ซับซ้อนมากขึ้น

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### ขั้นตอนที่ 2: สร้างดัชนีและเพิ่มเอกสาร (ดูขั้นตอนที่ 2‑3 จากตัวอย่างแบบง่าย; เหมือนเดิม)

#### ขั้นตอนที่ 3: ดำเนินการค้นหาแบบข้อความ
รันคำค้นข้อความแบบผสมที่รวมเกณฑ์ชื่อไฟล์และเนื้อหา

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### ขั้นตอนที่ 4: สร้างและดำเนินการ Object Queries
สร้างตรรกะเดียวกันโดยโปรแกรม

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

ดำเนินการต่อโดยรวมวลี, ช่วงค่า, และตัวดำเนินการบูลีนเพื่อให้ตรงกับกฎธุรกิจของคุณอย่างแม่นยำ

## การประยุกต์ใช้งานจริง

1. **E‑Commerce Platforms** – กรองสินค้าตามหมวดหมู่, ราคา, และคะแนน.  
2. **Document Management Systems** – ค้นหาสัญญาตามผู้เขียน, วันที่, หรือระดับความลับ.  
3. **Content Portals** – ให้ผู้อ่านเจาะลึกตามแท็ก, หัวข้อ, และวันที่เผยแพร่.

## ข้อควรพิจารณาด้านประสิทธิภาพ

- **Index Refresh**: ทำการทำดัชนีใหม่อย่างสม่ำเสมอสำหรับไฟล์ที่เพิ่มหรืออัปเดตเพื่อให้การค้นหาเร็ว.  
- **Memory Management**: ปล่อยวัตถุ `Index` เมื่อเสร็จ, โดยเฉพาะกับชุดข้อมูลขนาดใหญ่.  
- **Asynchronous Indexing**: ใช้ `Task.Run` หรือบริการพื้นหลังเพื่อหลีกเลี่ยงการหยุดทำงานของ UI ระหว่างการทำดัชนีหนัก.

## ปัญหาทั่วไปและวิธีแก้

| Issue | Solution |
|-------|----------|
| **Index not found** | ตรวจสอบเส้นทาง `indexFolder` และให้แน่ใจว่าโฟลเดอร์มีสิทธิ์เขียน. |
| **No results returned** | ตรวจสอบว่าฟิลด์ที่คุณค้นหา (เช่น `Content`, `Filename`) ถูกทำดัชนีแล้ว. |
| **Out‑of‑memory errors** | ประมวลผลเอกสารเป็นชุดและพิจารณาเพิ่มขนาด heap ของ .NET GC. |

## คำถามที่พบบ่อย

**Q: การค้นหาแบบ faceted คืออะไร?**  
A: การค้นหาแบบ faceted อนุญาตให้ผู้ใช้ปรับผลลัพธ์โดยใช้ตัวกรองหลายตัวที่เป็นอิสระ เช่น หมวดหมู่, วันที่, หรือผู้เขียน.

**Q: ฉันจะจัดการกับชุดข้อมูลขนาดใหญ่ด้วย GroupDocs.Search อย่างไร?**  
A: ใช้การทำดัชนีแบบเพิ่มขั้น, การประมวลผลเป็นชุด, และการทำงานแบบอะซิงโครนัสเพื่อรักษาการใช้หน่วยความจำให้ต่ำและประสิทธิภาพสูง.

**Q: ฉันสามารถผสานฟังก์ชันของ GroupDocs เข้ากับแอป .NET ที่มีอยู่ได้หรือไม่?**  
A: ได้, ไลบรารีออกแบบมาเพื่อการผสานที่ราบรื่นกับโครงการ .NET ใด ๆ.

**Q: ปัญหาที่พบบ่อยของการค้นหาแบบ faceted มีอะไรบ้าง?**  
A: ไวยากรณ์คำค้นที่ซับซ้อนและการทำให้แน่ใจว่าฟิลด์ที่เกี่ยวข้องทั้งหมดถูกทำดัชนีเป็นความท้าทายทั่วไป; การทดสอบอย่างละเอียดและการบำรุงรักษาดัชนีช่วยลดปัญหาเหล่านี้.

**Q: ฉันจะขอใบอนุญาตชั่วคราวสำหรับ GroupDocs อย่างไร?**  
A: เยี่ยมชม [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) เพื่อสมัครใบอนุญาตทดลองที่เปิดใช้งานฟังก์ชันเต็มในช่วงการประเมิน.

## แหล่งข้อมูล
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Last Updated:** 2026-04-02  
**Tested With:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Author:** GroupDocs
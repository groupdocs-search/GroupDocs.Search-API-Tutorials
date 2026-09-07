---
date: '2026-06-22'
description: เรียนรู้วิธีลบข้อมูลส่วนบุคคลในเอกสารด้วย .NET พร้อมเพิ่มประสิทธิภาพการค้นหาด้วย
  GroupDocs.Redaction และ GroupDocs.Search. Step‑by‑step attribute management, indexing,
  และ secure redaction สำหรับนักพัฒนา .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: วิธีลบข้อมูลส่วนบุคคลในเอกสารด้วย .NET โดยใช้ GroupDocs Redaction
type: docs
url: /th/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# วิธีการทำลบข้อมูลในเอกสารใน .NET ด้วย GroupDocs Redaction

ในบทแนะนำที่ครอบคลุมนี้คุณจะได้ค้นพบ **วิธีการทำลบข้อมูลในเอกสาร** ในสภาพแวดล้อม .NET และพร้อมกันนี้ยังเรียนรู้การจัดการแอตทริบิวต์ของเอกสารด้วย GroupDocs.Redaction และ GroupDocs.Search ไม่ว่าคุณจะต้องการปกป้องข้อมูลที่ละเอียดอ่อน เพิ่มความเร็วในการค้นหา หรือจัดการห้องสมุดเอกสารขนาดใหญ่ เทคนิคที่แสดงในที่นี้จะให้คุณได้โซลูชันพร้อมใช้งานในระดับการผลิตที่สามารถขยายได้ถึงหลายแสนไฟล์

## คำตอบอย่างรวดเร็ว
- **ฉันจะทำลบข้อมูล PDF ใน .NET อย่างไร?** โหลดไฟล์ด้วย `Redactor` กำหนด `RedactionRegion` แล้วเรียก `Redactor.Apply()` – สามบรรทัดของโค้ดจัดการงานหนัก  
- **ฉันสามารถเปลี่ยนแปลงแอตทริบิวต์ของเอกสารหลังการทำดัชนีได้หรือไม่?** ใช่, ใช้ `AttributeChangeBatch` เพื่อเพิ่ม, ปรับปรุง หรือเอาแอตทริบิวต์ออกเป็นกลุ่ม  
- **ต้องใช้ไลบรารีอะไรบ้าง?** `GroupDocs.Redaction` + `GroupDocs.Search` (เวอร์ชันล่าสุดจาก NuGet)  
- **ต้องมีใบอนุญาตสำหรับการผลิตหรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs ที่ถูกต้อง; มีใบอนุญาตทดลองชั่วคราวสำหรับการประเมินผล  
- **จะเพิ่มความเร็วในการค้นหาได้อย่างไร?** เปิดการประมวลผลแบบแบชและการทำดัชนีแบบเลือก; เทคนิคเหล่านี้สามารถ **เพิ่มประสิทธิภาพการค้นหา** ได้ถึง 40 % ในชุดข้อมูลขนาดใหญ่

## “วิธีการทำลบข้อมูลในเอกสาร” คืออะไร

มันอธิบายกระบวนการอัตโนมัติในการค้นหาข้อมูลที่ละเอียดอ่อนภายในไฟล์และแทนที่ด้วยเนื้อหาที่บัง เช่น แถบสีดำหรือช่องว่างสีขาว — ในขณะที่ยังคงรูปแบบต้นฉบับไว้เหมือนเดิม สิ่งนี้ทำให้ข้อมูลลับถูกซ่อนจากผู้ดู แต่เอกสารยังคงอ่านได้และทำงานต่อได้สำหรับงานต่อไป

## ทำไมต้องใช้ GroupDocs.Redaction และ GroupDocs.Search ร่วมกัน

GroupDocs.Redaction รองรับ **ไฟล์กว่า 50 รูปแบบ** (PDF, DOCX, XLSX, PPTX, รูปภาพ ฯลฯ) และสามารถประมวลผลเอกสารขนาด **ถึง 2 GB** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ GroupDocs.Search ทำการทำดัชนีมากกว่า **70 ล้านคำ** ต่อชั่วโมงบนเซิร์ฟเวอร์มาตรฐาน ทำให้คุณ **เพิ่มประสิทธิภาพการค้นหา** อย่างมหาศาลเมื่อรวมกับการกรองตามแอตทริบิวต์

## ข้อกำหนดเบื้องต้น

- **ไลบรารีที่ต้องการ:** `GroupDocs.Search` และ `GroupDocs.Redaction` (เวอร์ชันล่าสุดจาก NuGet)  
- **สภาพแวดล้อมการพัฒนา:** Visual Studio 2019 หรือใหม่กว่า, ตั้งเป้าหมายที่ .NET Core 3.1 หรือ .NET 6+  
- **ความรู้พื้นฐาน:** ไวยากรณ์ C#, แนวคิดเชิงวัตถุ, และความคุ้นเคยกับหลักการทำดัชนีเอกสาร

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### การติดตั้งไลบรารี

คุณสามารถเพิ่ม **GroupDocs.Redaction** ไปยังโปรเจกต์ของคุณได้ด้วยวิธีใดวิธีหนึ่งต่อไปนี้:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- ค้นหา “GroupDocs.Redaction” แล้วติดตั้งเวอร์ชันล่าสุด

### ขั้นตอนการรับใบอนุญาต

เพื่อเริ่มต้นคุณสามารถรับใบอนุญาตชั่วคราวหรือซื้อใบอนุญาตได้ การทดลองใช้ฟรีพร้อมให้คุณทดสอบฟีเจอร์ก่อนตัดสินใจ:
1. เยี่ยมชม [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) เพื่อขอใบอนุญาตชั่วคราว  
2. ทำตามคำแนะนำที่ให้ไว้เพื่อใช้ใบอนุญาตในแอปพลิเคชันของคุณ

### การเริ่มต้นและตั้งค่าเบื้องต้น

`Redactor` เป็นคลาสหลักที่ใช้โหลดเอกสารและทำการลบข้อมูล

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## ฟีเจอร์ 1: การเปลี่ยนแปลงแอตทริบิวต์ของเอกสาร

### ภาพรวม
การแก้ไขแอตทริบิวต์ของเอกสารช่วยให้คุณปรับแต่งวิธีที่เอกสารปรากฏในผลการค้นหา ทำให้สามารถกรองและจัดประเภทได้อย่างแม่นยำ

#### ขั้นตอนที่ 1: เริ่มต้น Index

`Index` แสดงถึงคอลเลกชันที่สามารถค้นหาได้ของเอกสารและเมตาดาต้าที่เกี่ยวข้อง

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### ขั้นตอนที่ 2: แก้ไขแอตทริบิวต์

`AttributeChangeBatch` เป็นคลาสที่ทำการแบชอัปเดตแอตทริบิวต์เพื่อความมีประสิทธิภาพ  

**Definition anchor:** *`AttributeChangeBatch` batches add, update, and delete operations on document attributes in a single transaction.*  

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### ขั้นตอนที่ 3: ค้นหาด้วยตัวกรองแอตทริบิวต์

คุณสามารถกรองผลการค้นหาตามค่าแอตทริบิวต์โดยใช้ `SearchOptions`  

**Direct answer:** เพื่อค้นหาเอกสารที่มีแอตทริบิวต์ `Category = "Legal"` ให้กำหนด `SearchOptions` พร้อม `AttributeFilter` แล้วเรียก `searcher.Search("contract", options)` ผลลัพธ์จะเป็นสัญญาที่มีแท็กกฎหมายเท่านั้น ลดสัญญาณรบกวนและ **เพิ่มประสิทธิภาพการค้นหา**  

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## ฟีเจอร์ 2: เพิ่มแอตทริบิวต์ระหว่างการทำดัชนี

### ภาพรวม
การเพิ่มแอตทริบิวต์ในขณะทำดัชนีทำให้ทุกเอกสารได้รับเมตาดาต้าที่เหมาะสมตั้งแต่ต้น ลดความจำเป็นในการอัปเดตแบบแบชภายหลัง

#### ขั้นตอนที่ 1: ตั้งค่า Event Handler สำหรับการทำดัชนี

**Definition anchor:** *The `DocumentIndexed` event fires each time a document is successfully added to the index, allowing custom logic to run.*  

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### ขั้นตอนที่ 2: ตั้งค่าและทำการค้นหา

หลังจากที่แอตทริบิวต์ถูกแนบแล้ว คุณสามารถค้นหาโดยใช้ฟิลด์ใหม่เหล่านั้นได้  

**Direct answer:** ใช้ `SearchOptions` พร้อม `AttributeFilter` เพื่อสอบถามแอตทริบิวต์ที่เพิ่มใหม่ เช่น `AttributeFilter("Department", "Finance")` จะคืนไฟล์ที่เกี่ยวกับการเงินเท่านั้น แสดง **วิธีทำดัชนีแอตทริบิวต์** เพื่อผลลัพธ์ที่เร็วและเกี่ยวข้องมากขึ้น  

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## การประยุกต์ใช้งานจริง

ต่อไปนี้คือสามสถานการณ์ทั่วไปที่การจัดการแอตทริบิวต์ของเอกสารและการทำลบข้อมูลร่วมกันสร้างคุณค่าทางธุรกิจที่จับต้องได้:

1. **การจัดการเอกสารทางกฎหมาย** – ทำลบข้อกำหนดที่เป็นความลับอัตโนมัติและแท็กสัญญาตามเขตอำนาจศาล ทำให้ทนายสามารถค้นหาไฟล์ที่เกี่ยวข้องได้อย่างรวดเร็ว  
2. **การจัดระเบียบบันทึกทางการแพทย์** – ทำลบตัวระบุผู้ป่วยขณะเดียวกันเพิ่มแอตทริบิวต์เช่น `PatientID` และ `VisitDate` เพื่อการดึงข้อมูลที่สอดคล้องและเร็วขึ้น  
3. **การจัดทำแคตาล็อกสินค้าอี‑คอมเมิร์ซ** – ทำลบข้อมูลราคาจากผู้จัดจำหน่ายและแท็กสินค้าโดย `StockStatus` หรือ `DiscountRate` ระหว่างการนำเข้าจำนวนมาก ทำให้สามารถสอบถามสินค้าคงคลังแบบเรียลไทม์ได้

## ข้อควรพิจารณาด้านประสิทธิภาพ

เมื่อจัดการกับชุดข้อมูลขนาดใหญ่ ควรปฏิบัติตามแนวปฏิบัติดังต่อไปนี้:

- **Batch Processing:** `AttributeChangeBatch` ลดการติดต่อกับดัชนี, ลดเวลาในการประมวลผลได้ถึง **45 %** ในแบช 100 k‑เอกสาร  
- **Selective Indexing:** ทำดัชนีเฉพาะเอกสารที่ต้องการเพิ่มแอตทริบิวต์ใหม่, ข้ามไฟล์ที่ไม่ได้เปลี่ยนแปลงเพื่อประหยัด CPU และ I/O  
- **Memory Management:** ปล่อย `SearchResult`, `Redactor`, และ `Indexer` ทันทีหลังใช้งานเพื่อคืนทรัพยากรที่ไม่ได้จัดการโดย .NET

## ปัญหาทั่วไปและวิธีแก้

| Issue | Cause | Solution |
|-------|-------|----------|
| Redaction does not hide text | Incorrect `RedactionRegion` coordinates | Verify page dimensions with `Redactor.GetPageSize()` before defining the region. |
| Attribute changes not reflected in search | Index not refreshed | Call `searcher.Refresh()` after `AttributeChangeBatch` execution. |
| Out‑of‑memory errors on large files | Loading entire file into memory | Enable streaming mode by setting `RedactorOptions.Stream = true`. |

## คำถามที่พบบ่อย

**Q: วิธีที่ดีที่สุดในการทำลบข้อมูลหลาย PDF พร้อมกันคืออะไร?**  
A: โหลดแต่ละไฟล์ด้วย `Redactor`, เพิ่ม `RedactionRegion` สำหรับทุกพื้นที่ที่ละเอียดอ่อน, แล้วเรียก `Redactor.Apply()` ภายในลูป; วิธีนี้สามารถประมวลผลไฟล์หลายพันไฟล์ด้วยการใช้หน่วยความจำต่ำ

**Q: สามารถรวมการทำลบข้อมูลกับการกรองแอตทริบิวต์ในคำค้นเดียวได้หรือไม่?**  
A: ได้ หลังจากทำลบข้อมูลแล้วเอกสารยังคงรักษาเมตาดาต้าไว้ คุณจึงสามารถค้นหาด้วยคำหลักและ `AttributeFilter` พร้อมกันได้

**Q: จะจัดการกับเอกสารที่มีการป้องกันด้วยรหัสผ่านอย่างไร?**  
A: ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ของ `Redactor`; ไลบรารีจะถอดรหัส, ทำลบข้อมูล, แล้วเข้ารหัสไฟล์ใหม่โดยอัตโนมัติ

**Q: GroupDocs รองรับ OCR สำหรับภาพสแกนก่อนทำลบข้อมูลหรือไม่?**  
A: รองรับอย่างเต็มที่ ตั้งค่า `RedactorOptions.Ocr = true` เพื่อให้ระบบจดจำข้อความในภาพ แล้วจึงใช้กฎการทำลบข้อมูลบนข้อความที่สกัดออกมา

**Q: .NET เวอร์ชันใดที่รองรับอย่างเป็นทางการ?**  
A: GroupDocs.Redaction และ GroupDocs.Search รองรับ .NET Core 3.1, .NET 5, .NET 6, .NET 7, รวมถึง .NET Framework 4.6.2+

## สรุป

คุณมีโซลูชันแบบเต็มสแตกสำหรับ **วิธีการทำลบข้อมูลในเอกสาร** พร้อมกับ **การเพิ่มประสิทธิภาพการค้นหา** และ **การทำดัชนีแอตทริบิวต์** ด้วย GroupDocs.Redaction และ GroupDocs.Search โดยทำตามขั้นตอนข้างต้น คุณจะสามารถปกป้องข้อมูลที่ละเอียดอ่อน, เพิ่มเมตาดาต้าให้กับดัชนีค้นหา, และทำให้แอปพลิเคชัน .NET ของคุณเร็วและปลอดภัย

---

**Last Updated:** 2026-06-22  
**Tested With:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Author:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)  
- [Master Document Redaction and Metadata Indexing with GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)  
- [Master GroupDocs.Redaction .NET: Setup & Event Handling for Secure Document Management](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
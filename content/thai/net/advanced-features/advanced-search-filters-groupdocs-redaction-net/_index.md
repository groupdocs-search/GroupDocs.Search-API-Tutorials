---
date: '2026-04-02'
description: เรียนรู้วิธีกรองตามนามสกุลไฟล์และค้นหาเฉพาะไฟล์ txt ด้วย GroupDocs.Redaction
  สำหรับ .NET—เพิ่มประสิทธิภาพการจัดการเอกสาร
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: กรองตามนามสกุลไฟล์ใน .NET ด้วย GroupDocs.Redaction
type: docs
url: /th/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# กรองตามนามสกุลไฟล์ใน .NET ด้วย GroupDocs.Redaction

การค้นหาผ่านคอลเลกชันไฟล์ขนาดใหญ่สามารถทำให้รู้สึกหนักหน่วงได้ โดยเฉพาะเมื่อคุณต้องการผลลัพธ์จากประเภทไฟล์ที่ระบุเท่านั้น ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีกรองตามนามสกุลไฟล์** ด้วย GroupDocs.Redaction สำหรับ .NET ซึ่งช่วยให้คุณค้นหาเฉพาะไฟล์ txt หรือส่วนขยายอื่นที่คุณเลือก เราจะอธิบายขั้นตอนการตั้งค่าตัวกรองทั้งแบบตามประเภทไฟล์และตามเส้นทาง เพื่อให้คุณสามารถค้นหาเอกสารที่ต้องการได้อย่างรวดเร็ว

## คำตอบสั้น
- **อะไรคือการ “filter by file extension” ทำ?** It limits a search to documents that match a given file extension (e.g., *.txt).  
- **ทำไมต้องใช้ GroupDocs.Redaction สำหรับเรื่องนี้?** It provides built‑in filtering APIs that are fast and easy to integrate.  
- **ฉันต้องการไลเซนส์หรือไม่?** A free trial works for testing; a paid license is required for production.  
- **เวอร์ชัน .NET ใดที่รองรับ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **ฉันสามารถรวมตัวกรองตามประเภทไฟล์และเส้นทางได้หรือไม่?** Yes—apply multiple filters for highly precise searches.  

## สิ่งที่คุณจะได้เรียนรู้
- วิธี **filter by file extension** เพื่อให้ค้นหาเฉพาะไฟล์ข้อความเท่านั้น.  
- วิธีตั้งค่า **file path filters** เพื่อจำกัดผลลัพธ์ให้กับโฟลเดอร์หรือรูปแบบการตั้งชื่อเฉพาะ.  
- เคล็ดลับในการทำให้ดัชนีของคุณเร็วและใช้หน่วยความจำน้อย.

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

- **GroupDocs.Redaction Library** ที่ติดตั้งและเข้ากันได้กับโครงการ .NET ของคุณ.  
- สภาพแวดล้อมการพัฒนา เช่น Visual Studio หรือ VS Code.  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับโครงสร้างโครงการ .NET.

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

ขั้นแรก ให้เพิ่มไลบรารีลงในโครงการของคุณ.

**ใช้ .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**ใช้ Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

หรือค้นหา “GroupDocs.Redaction” ใน UI ของ NuGet Package Manager แล้วติดตั้งเวอร์ชันล่าสุด.

### การรับไลเซนส์

คุณสามารถเริ่มต้นด้วยการทดลองใช้งานฟรีหรือขอไลเซนส์ชั่วคราว สำหรับโครงการระยะยาว ให้ซื้อไลเซนส์จากเว็บไซต์ทางการ.

### การเริ่มต้นพื้นฐาน

หลังจากแพ็กเกจถูกติดตั้งแล้ว ให้สร้าง Index ที่จะเก็บอ้างอิงเอกสารของคุณ:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## คู่มือการใช้งาน

### ฟีเจอร์ 1: ตั้งค่าตัวกรองสำหรับเอกสารข้อความ (.txt)

#### วิธีกรองตามนามสกุลไฟล์สำหรับเอกสารข้อความ

1. **กำหนดดัชนีและโฟลเดอร์เอกสาร**  
   กำหนดเส้นทางที่ไฟล์ต้นฉบับของคุณอยู่:  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **สร้าง Index**  
   โหลดไฟล์ทั้งหมดจากโฟลเดอร์ต้นฉบับเข้าสู่ Index:  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **กำหนดค่า Search Options ด้วยตัวกรองนามสกุลไฟล์**  
   บอกให้เอนจินพิจารณาเฉพาะไฟล์ *.txt เท่านั้น:  

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **ดำเนินการค้นหา**  
   รันคิวรี; ตัวกรองจะทำให้ไฟล์ที่ไม่ใช่ข้อความถูกละเว้น:  

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explanation*: เมธอด `Search` จะคืนผลลัพธ์ที่ตรงกับตัวกรอง, ลดสัญญาณรบกวนอย่างมากและปรับปรุงประสิทธิภาพ.

### ฟีเจอร์ 2: ตัวกรอง FilePath

#### ทำไมต้องใช้ตัวกรอง file path?

บางครั้งคุณอาจต้องจำกัดการค้นหาให้กับโฟลเดอร์ของแผนกเฉพาะหรือชุดไฟล์ที่มีรูปแบบการตั้งชื่อเดียวกัน ตัวกรองเส้นทางทำให้คุณทำเช่นนั้นได้.

1. **กำหนดดัชนีและโฟลเดอร์เอกสาร**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **สร้าง Index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **กำหนดค่า Search Options ด้วย regular expression ที่อิงตามเส้นทาง**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   regular expression นี้จะจับคู่กับไฟล์ใด ๆ ที่เส้นทางเต็มของไฟล์มีคำว่า “Lorem”, ทำให้คุณสามารถกำหนดเป้าหมายไปยังโฟลเดอร์ย่อยเฉพาะ.

4. **ดำเนินการค้นหาตามเส้นทาง**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## การประยุกต์ใช้งานจริง
- **Legal Document Management** – ค้นหาสัญญาที่เกี่ยวข้องที่เก็บเป็นไฟล์ข้อความธรรมดาได้อย่างรวดเร็ว.  
- **Academic Research** – ดึงเฉพาะบันทึกการวิจัย *.txt ที่อยู่ในโฟลเดอร์โครงการเฉพาะ.  
- **Corporate Reporting** – กรองรายงานภายในตามเส้นทางแผนก (เช่น `/Finance/2025/`).  

## พิจารณาด้านประสิทธิภาพ
- ทำการ Index เฉพาะประเภทเอกสารที่คุณต้องการจริง ๆ; ไฟล์ที่ไม่จำเป็นจะเพิ่มขนาด Index และเวลาในการค้นหา.  
- รักษา Index ให้เป็นปัจจุบันด้วยงานที่กำหนดเวลาเรียก `index.Add()` สำหรับไฟล์ใหม่หรือที่เปลี่ยนแปลง.  
- ใช้ regular expression อย่างง่าย; รูปแบบที่ซับซ้อนเกินไปอาจทำให้เครื่องมือค้นช้าลง.  
- ทำการ Dispose วัตถุ `Index` เมื่อไม่ต้องการใช้งานแล้วเพื่อคืนหน่วยความจำ.

## สรุป
ตอนนี้คุณรู้วิธี **filter by file extension** และใช้ **file path filters** ด้วย GroupDocs.Redaction สำหรับ .NET เทคนิคเหล่านี้ให้การควบคุมที่ละเอียดต่อคอลเลกชันเอกสารขนาดใหญ่ ทำให้การค้นหาเร็วขึ้นและมีความเกี่ยวข้องมากขึ้น ต่อไปลองผสานหลายตัวกรองเข้าด้วยกันหรือรวมการค้นหาเข้าไปในกระบวนการทำงานของแอปพลิเคชันที่ใหญ่ขึ้น.

## ส่วนคำถามที่พบบ่อย

**Q1: ฉันสามารถกรองเอกสารที่ไม่ใช่ไฟล์ข้อความได้หรือไม่?**  
A1: ได้, GroupDocs.Redaction รองรับหลายรูปแบบ. เปลี่ยนอาร์กิวเมนต์ใน `CreateFileExtension` เป็นนามสกุลที่ต้องการ (เช่น ".pdf").

**Q2: ฉันจะอัปเดต Index การค้นหาเป็นประจำอย่างไร?**  
A2: กำหนดบริการพื้นหลังหรือ cron job ที่เรียก `index.Add()` บนไดเรกทอรีที่คุณต้องการให้เป็นปัจจุบัน.

**Q3: การกรองตามเส้นทางไฟล์มีผลต่อประสิทธิภาพหรือไม่?**  
A3: regular expression ที่ปรับให้เหมาะสมจะมีผลกระทบน้อยที่สุด, แต่ควรทำการ benchmark ด้วยชุดข้อมูลของคุณเองเสมอ.

**Q4: ฉันสามารถรวมหลายตัวกรองเพื่อการค้นหาที่ละเอียดขึ้นได้หรือไม่?**  
A4: แน่นอน. คุณสามารถต่อเชื่อมตัวกรองหรือสร้างตัวกรองเชิงรวมเพื่อกำหนดเป้าหมายทั้งประเภทไฟล์และเส้นทางพร้อมกัน.

**Q5: ฉันจะหาแหล่งข้อมูลเพิ่มเติมเกี่ยวกับ GroupDocs.Redaction ได้จากที่ไหน?**  
A5: เยี่ยมชมเอกสารอย่างเป็นทางการที่ [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) เพื่อดูคู่มือโดยละเอียดและอ้างอิง API.

## คำถามที่พบบ่อย

**Q: `SearchDocumentFilter` ทำงานกับไฟล์ที่เข้ารหัสหรือไม่?**  
A: ตัวกรองทำงานบนเมตาดาต้าไฟล์, ดังนั้นไฟล์ที่เข้ารหัสยังคงถูก Index หากคุณให้ข้อมูลการถอดรหัสที่จำเป็นในระหว่างการ Index.

**Q: ฉันสามารถใช้ไวล์การ์ดแทน regular expression สำหรับการกรองเส้นทางได้หรือไม่?**  
A: API ปัจจุบันต้องการ regular expression, แต่คุณสามารถจำลองไวล์การ์ดแบบง่าย (เช่น `.*` สำหรับอักขระใด ๆ) ได้.

**Q: Index สามารถมีขนาดใหญ่เท่าไหร่ก่อนที่ต้องพิจารณา sharding?**  
A: Index ขนาดหลายร้อยกิกะไบต์อาจได้ประโยชน์จากการแยกเป็นหลาย Index เชิงตรรกะ; ทดสอบประสิทธิภาพเมื่อคอลเลกชันของคุณเติบโต.

**Q: มีเมธอดในตัวสำหรับลบเอกสารออกจาก Index หรือไม่?**  
A: มี—เรียก `index.Delete(documentId)` หรือ `index.DeleteAll()` เพื่อจัดการรายการที่ล้าสมัย.

**Q: มีวิธีดูตัวอย่างผลการค้นหาก่อนโหลดเอกสารเต็มหรือไม่?**  
A: วัตถุ `SearchResult` มีข้อมูล snippet ที่คุณสามารถแสดงใน UI โดยไม่ต้องเปิดไฟล์ทั้งหมด.

## แหล่งข้อมูล
- **เอกสาร**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **อ้างอิง API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **ดาวน์โหลด**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **สนับสนุนฟรี**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **ไลเซนส์ชั่วคราว**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**อัปเดตล่าสุด:** 2026-04-02  
**ทดสอบกับ:** GroupDocs.Redaction 23.12 for .NET  
**ผู้เขียน:** GroupDocs
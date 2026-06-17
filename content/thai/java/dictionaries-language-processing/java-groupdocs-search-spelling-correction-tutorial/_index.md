---
date: '2026-02-21'
description: เรียนรู้วิธีเปิดใช้งานการแก้ไขการสะกดใน Java ด้วย GroupDocs.Search, เพิ่มเอกสารลงในดัชนี,
  และตั้งค่าจำนวนข้อผิดพลาดสูงสุดเพื่อความแม่นยำในการค้นหาที่ดียิ่งขึ้น.
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: วิธีเปิดใช้งานการตรวจสอบการสะกดใน Java ด้วย GroupDocs.Search
type: docs
url: /th/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

" maybe keep as is? Should translate: "อัปเดตล่าสุด". "Tested With" -> "ทดสอบด้วย". "Author" -> "ผู้เขียน". Keep bold.

So:

---
**อัปเดตล่าสุด:** 2026-02-21  
**ทดสอบด้วย:** GroupDocs.Search 25.4  
**ผู้เขียน:** GroupDocs

Now ensure we didn't miss any markdown formatting.

Check headings: #, ##, ###.

Check code block placeholders remain unchanged.

Check tables: we changed header row.

Check bullet lists: use dash.

Check bold formatting: keep **.

Check italic? None.

Check *Tip:* keep as is.

Check *Why ...* keep.

Now produce final content.# วิธีเปิดใช้งานการสะกดคำใน Java ด้วย GroupDocs.Search

ผลการค้นหาที่แม่นยำเป็นสิ่งสำคัญสำหรับแอปพลิเคชันสมัยใหม่ทุกประเภท ในบทเรียนนี้คุณจะได้เรียนรู้ **วิธีเปิดใช้งานการสะกดคำ** ใน Java ด้วย GroupDocs.Search เพื่อให้ผู้ใช้ได้รับผลลัพธ์ที่ถูกต้องแม้จะพิมพ์คำค้นผิด เราจะอธิบายขั้นตอนการสร้างดัชนี, **การเพิ่มเอกสารลงในดัชนี**, การกำหนดค่าตัวเลือกการสะกดคำ, และการทำการค้นหาที่แก้ไขข้อผิดพลาดโดยอัตโนมัติ

## Quick Answers
- **“how to enable spelling” หมายถึงอะไร?** มันเปิดใช้งานตัวตรวจสอบการสะกดคำในตัวที่แก้ไขการพิมพ์ผิดของผู้ใช้ระหว่างการค้นหา.  
- **ไลบรารีใดที่ให้ฟีเจอร์นี้?** GroupDocs.Search for Java.  
- **ฉันต้องการไลเซนส์หรือไม่?** ไลเซนส์ทดลองฟรีใช้ได้สำหรับการประเมิน; ต้องมีไลเซนส์เต็มสำหรับการใช้งานจริง.  
- **ฉันสามารถควบคุมระดับความทนทานได้หรือไม่?** ได้ – ใช้ `setMaxMistakeCount` เพื่อกำหนดจำนวนการพิมพ์ผิดที่อนุญาต.  
- **เหมาะกับดัชนีขนาดใหญ่หรือไม่?** แน่นอน – เครื่องยนต์ได้รับการปรับให้ทำงานอย่างมีประสิทธิภาพสูงสำหรับการทำดัชนีและการค้นหา.

## “how to enable spelling” คืออะไรใน GroupDocs.Search?
การเปิดใช้งานการสะกดคำบอกให้เครื่องมือค้นหาค้นหาคำที่ใกล้เคียงและถูกต้องที่สุดเมื่อคำค้นมีข้อผิดพลาด ฟีเจอร์นี้ช่วยปรับปรุงประสบการณ์ผู้ใช้อย่างมากโดยให้ผลลัพธ์ที่เกี่ยวข้องแม้กับอินพุตที่สะกดผิด

## ทำไมต้องเปิดใช้งานการแก้ไขการสะกดคำในแอปพลิเคชัน Java?
- **เพิ่มความพึงพอใจของผู้ใช้** – ผู้ใช้ไม่จำเป็นต้องพิมพ์อย่างสมบูรณ์แบบ.  
- **ลดอัตราการตีกลับ** – ผลลัพธ์ที่แม่นยำมากขึ้นทำให้ผู้เข้าชมอยู่ในเว็บไซต์นานขึ้น.  
- **ทำงานได้ในหลายโดเมน** – ตั้งแต่แคตาล็อกห้องสมุดจนถึงการค้นหาผลิตภัณฑ์ในอีคอมเมิร์ซ.

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java Development Kit (JDK) แล้ว  
- ความรู้พื้นฐานเกี่ยวกับ Java และ Maven  
- เข้าใจแนวคิดการทำดัชนี  
- มีไลเซนส์ทดลองหรือไลเซนส์ของ GroupDocs.Search  

### การตั้งค่า GroupDocs.Search สำหรับ Java
ผสานรวมไลบรารีเข้ากับโปรเจกต์ Maven ของคุณ

**Maven Setup**  
Add the repository and dependency to your `pom.xml` file:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

**Direct Download**  
หรือดาวน์โหลดเวอร์ชันล่าสุดจาก [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### การรับไลเซนส์
รับไลเซนส์ทดลองฟรีเพื่อการประเมินผล สำหรับการใช้งานจริง ให้ซื้อไลเซนส์เต็มหรือขอคีย์ชั่วคราวจากเว็บไซต์อย่างเป็นทางการ

## วิธีเพิ่มเอกสารลงในดัชนี
การสร้างดัชนีเป็นพื้นฐานสำหรับแอปพลิเคชันที่มีการค้นหาใด ๆ ด้านล่างเป็นตัวอย่างขั้นพื้นฐานที่ **เพิ่มเอกสารลงในดัชนี** จากโฟลเดอร์

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

*Tip:* ตรวจสอบให้แน่ใจว่าเส้นทางถูกต้องและแอปพลิเคชันมีสิทธิ์เขียนไปยังโฟลเดอร์ดัชนี.

## วิธีกำหนดค่าการแก้ไขการสะกดคำ (set max mistake count)
คุณสามารถปรับแต่งตัวตรวจสอบการสะกดคำโดยเปิดใช้งานและกำหนดระดับความทนทานต่อข้อผิดพลาด

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

*Why `setMaxMistakeCount` matters:* มันกำหนดจำนวนการพิมพ์ผิดที่เครื่องยนต์จะยอมรับ ปรับค่าตามรูปแบบข้อผิดพลาดทั่วไปของโดเมนของคุณ.

## วิธีทำการค้นหาที่แก้ไขการสะกดคำ
เมื่อดัชนีพร้อมและตั้งค่าตัวเลือกการสะกดคำแล้ว ให้เรียกใช้คำค้นที่อาจมีข้อผิดพลาด

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

`search()` จะคืนค่า `SearchResult` ที่มีคำที่แก้ไขแล้วและเอกสารที่เกี่ยวข้องที่สุด.

## การใช้งานเชิงปฏิบัติ
1. **ระบบห้องสมุด:** แก้ไขชื่อหนังสือหรือชื่อผู้เขียนที่สะกดผิด.  
2. **แพลตฟอร์มอีคอมเมิร์ซ:** แก้ไขการพิมพ์ผิดของผู้ใช้ในการค้นหาผลิตภัณฑ์เพื่อเพิ่มอัตราการแปลง.  
3. **ระบบจัดการเนื้อหา:** ปรับปรุงการดึงบทความสำหรับทีมบรรณาธิการ.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **รักษาดัชนีให้เป็นปัจจุบัน** – ทำการทำดัชนีใหม่สำหรับไฟล์ที่เพิ่มหรือเปลี่ยนแปลงเป็นประจำ.  
- **ปรับตั้งค่าหน่วยความจำ JVM** – จัดสรร heap เพียงพอสำหรับดัชนีขนาดใหญ่.  
- **ตรวจสอบการใช้ทรัพยากร** – ปรับค่า flag ของ garbage‑collector หากจำเป็น.

## ปัญหาทั่วไปและการแก้ไขปัญหา
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ไข |
|---------|--------------|-----|
| ไม่มีผลลัพธ์หลังจากเปิดใช้งานการสะกดคำ | เส้นทางโฟลเดอร์ดัชนีผิดหรือว่างเปล่า | ตรวจสอบว่า `indexFolder` ชี้ไปยังดัชนีที่ถูกต้องและว่า `index.add()` ทำงานสำเร็จ |
| ตัวตรวจสอบการสะกดคำไม่แก้ไขการพิมพ์ผิดที่ชัดเจน | `setMaxMistakeCount` ตั้งค่าต่ำเกินไป | เพิ่มจำนวนเป็น 2 หรือ 3 เพื่อให้แก้ไขได้ยืดหยุ่นมากขึ้น |
| แอปพลิเคชันพังเมื่อจัดการชุดเอกสารขนาดใหญ่ | หน่วยความจำ JVM ไม่เพียงพอ | เพิ่มตัวเลือก `-Xmx` (เช่น `-Xmx4g`) |

## คำถามที่พบบ่อย

**Q: GroupDocs.Search คืออะไร?**  
A: เป็นไลบรารี Java ที่ให้การทำดัชนีที่รวดเร็ว, ฟีเจอร์การค้นหาขั้นสูง, และการแก้ไขการสะกดคำในตัว.

**Q: ฉันจะได้รับไลเซนส์สำหรับ GroupDocs.Search อย่างไร?**  
A: เยี่ยมชมเว็บไซต์อย่างเป็นทางการเพื่อดาวน์โหลดไลเซนส์ทดลองฟรีหรือซื้อไลเซนส์เต็ม.

**Q: ฉันสามารถผสานรวม GroupDocs.Search กับเฟรมเวิร์ก Java อื่น ๆ ได้หรือไม่?**  
A: ได้, มันทำงานร่วมกับ Spring, Jakarta EE, และแอปพลิเคชัน Java มาตรฐานใด ๆ.

**Q: ปัญหาทั่วไปเมื่อตั้งค่าดัชนีคืออะไร?**  
A: เส้นทางโฟลเดอร์ไม่ถูกต้อง, สิทธิ์ไฟล์ไม่เพียงพอ, หรือการพึ่งพาที่หายไปใน `pom.xml`.

**Q: การแก้ไขการสะกดคำช่วยปรับปรุงผลการค้นหาอย่างไร?**  
A: มันจะเขียนคำค้นที่สะกดผิดใหม่เป็นคำที่ใกล้เคียงและถูกต้องที่สุดโดยอัตโนมัติ, ให้ผลลัพธ์ที่เกี่ยวข้องมากขึ้น.

## แหล่งข้อมูลเพิ่มเติม
- [เอกสาร](https://docs.groupdocs.com/search/java/)
- [อ้างอิง API](https://reference.groupdocs.com/search/java)
- [ดาวน์โหลด](https://releases.groupdocs.com/search/java/)
- [Repository บน GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/search/10)
- [ไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-02-21  
**ทดสอบด้วย:** GroupDocs.Search 25.4  
**ผู้เขียน:** GroupDocs
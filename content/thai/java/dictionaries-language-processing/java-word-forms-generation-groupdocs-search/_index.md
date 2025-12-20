---
date: '2025-12-20'
description: เรียนรู้วิธีสร้างผู้ให้บริการรูปแบบคำใน Java ด้วย GroupDocs.Search สร้างรูปแบบเอกพจน์และพหูพจน์สำหรับการค้นหา
  การวิเคราะห์ข้อความ และอื่น ๆ
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: สร้าง Word Forms Provider ใน Java ด้วย GroupDocs.Search API
type: docs
url: /th/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# สร้าง Word Forms Provider ใน Java ด้วย GroupDocs.Search API

การแปลงคำจากรูปเอกพจน์เป็นพหูพจน์—หรือในทางกลับกัน—เป็นอุปสรรคที่พบบ่อยเมื่อสร้างแอปพลิเคชันที่รับรู้ภาษา ในคู่มือนี้คุณจะ **สร้าง word forms provider** ด้วย GroupDocs.Search Java API ซึ่งจะทำให้เครื่องมือค้นหาหรือเครื่องมือวิเคราะห์ข้อความของคุณสามารถเข้าใจและจับคู่รูปแบบคำที่แตกต่างกันได้โดยอัตโนมัติ

ไม่ว่าคุณจะกำลังพัฒนา search engine, ระบบจัดการเนื้อหา (CMS) หรือแอปพลิเคชัน Java ใด ๆ ที่ประมวลผลภาษาธรรมชาติ การเชี่ยวชาญการสร้างรูปแบบคำจะทำให้ผลลัพธ์แม่นยำยิ่งขึ้นและผู้ใช้พึงพอใจมากขึ้น มาดูกันว่าต้องเตรียมอะไรบ้างก่อนเริ่ม

## คำตอบสั้น

- **Word forms provider ทำอะไร?** มันสร้างรูปแบบทางเลือก (เอกพจน์, พหูพจน์ ฯลฯ) ของคำที่กำหนดเพื่อให้การค้นหาสามารถจับคู่ทุกรูปแบบได้  
- **ต้องใช้ไลบรารีใด?** GroupDocs.Search สำหรับ Java (เวอร์ชัน 25.4 หรือใหม่กว่า)  
- **ต้องมีไลเซนส์หรือไม่?** สามารถใช้ trial ฟรีเพื่อประเมินผล; ต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง  
- **รองรับ Java เวอร์ชันใด?** JDK 8 หรือสูงกว่า  
- **ต้องเขียนโค้ดกี่บรรทัด?** ประมาณ 30 บรรทัดสำหรับการทำ provider อย่างง่าย

## “Create Word Forms Provider” คืออะไร?

**Create word forms provider** เป็นคอมโพเนนต์คลาสที่กำหนดเองซึ่ง implements `IWordFormsProvider` มันรับคำและคืนอาร์เรย์ของรูปแบบที่เป็นไปได้—เช่น เอกพจน์, พหูพจน์ หรือรูปแบบทางภาษาต่าง ๆ—ตามกฎที่คุณกำหนด ซึ่งทำให้ดัชนีการค้นหาสามารถถือว่า “cat” และ “cats” เท่ากันได้ เพิ่มความครอบคลุมโดยไม่ลดความแม่นยำ

## ทำไมต้องใช้ GroupDocs.Search สำหรับการสร้างรูปแบบคำ?

- **ขยายได้ในตัว:** คุณสามารถต่อ provider ของคุณเข้าไปใน pipeline การทำดัชนีได้โดยตรง  
- **ประสิทธิภาพสูง:** ไลบรารีจัดการดัชนีขนาดใหญ่ได้อย่างมีประสิทธิภาพ และคุณสามารถแคชผลลัพธ์เพื่อความเร็วเพิ่มขึ้น  
- **รองรับหลายภาษา:** แม้ว่าตัวอย่างนี้จะเน้น Java แนวคิดเดียวกันยังใช้ได้กับ .NET และแพลตฟอร์มอื่น ๆ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะทำ **create word forms provider** ให้แน่ใจว่าคุณมี:

- **Maven** ติดตั้งอยู่และมี JDK 8 หรือใหม่กว่าในเครื่องของคุณ  
- ความคุ้นเคยพื้นฐานกับการพัฒนา Java และการตั้งค่า `pom.xml` ของ Maven  
- การเข้าถึงไลบรารี GroupDocs.Search Java (เวอร์ชัน 25.4 หรือใหม่กว่า)

## การตั้งค่า GroupDocs.Search สำหรับ Java

### การกำหนดค่า Maven

เพิ่ม repository และ dependency ลงในไฟล์ `pom.xml` ของคุณตามตัวอย่างด้านล่างโดยตรง:

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

### ดาวน์โหลดโดยตรง

หรือคุณสามารถดาวน์โหลด JAR ล่าสุดจากหน้า releases อย่างเป็นทางการ: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### ขั้นตอนการรับไลเซนส์

เพื่อใช้ GroupDocs.Search โดยไม่มีข้อจำกัด:

1. **Free Trial:** สมัครเพื่อทดลองใช้ฟีเจอร์หลัก  
2. **Temporary License:** ขอคีย์ชั่วคราวสำหรับการทดสอบต่อเนื่อง  
3. **Purchase:** ซื้อไลเซนส์เชิงพาณิชย์เพื่อใช้งานใน production อย่างไม่มีข้อจำกัด

### การเริ่มต้นและการตั้งค่าเบื้องต้น

โค้ดตัวอย่างต่อไปนี้แสดงวิธีสร้างดัชนี—จุดเริ่มต้นสำหรับการเพิ่มเอกสารและตรรกะการสร้างรูปแบบคำ:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## คู่มือการทำงาน

ต่อไปนี้เป็นขั้นตอนการ **create word forms provider** ที่จัดการการแปลงเอกพจน์‑พหูพจน์อย่างง่าย

### การ Implement SimpleWordFormsProvider

#### ภาพรวม

Provider ที่กำหนดเองของเราจะ:

- ลบ “es” หรือ “s” ที่ต่อท้ายเพื่อคาดเดารูปเอกพจน์  
- แปลง “y” ที่ต่อท้ายเป็น “is” เพื่อสร้างรูปพหูพจน์ (เช่น “city” → “citis”)  
- เพิ่ม “s” และ “es” เพื่อสร้างตัวเลือกพหูพจน์พื้นฐาน

#### ขั้นตอน 1 – สร้างโครงสร้างคลาส

เริ่มด้วยการกำหนดคลาสที่ implements `IWordFormsProvider` คงไว้ซึ่งคำสั่ง import ตามเดิม:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### ขั้นตอน 2 – Implement `getWordForms`

เพิ่มเมธอดที่สร้างรายการรูปแบบที่เป็นไปได้ บล็อกนี้เป็นตรรกะหลัก; คุณสามารถขยายต่อไปเพื่อรองรับกฎที่ซับซ้อนกว่า

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### คำอธิบายตรรกะ

- **Singularization:** ตรวจจับ suffix พหูพจน์ทั่วไป (`es`, `s`) แล้วลบออกเพื่อประมาณคำฐาน  
- **Pluralization:** จัดการคำนามที่ลงท้ายด้วย `y` โดยเปลี่ยนเป็น `is` ซึ่งเป็นกฎง่ายที่ใช้ได้กับหลายคำภาษาอังกฤษ  
- **Suffix Appending:** เพิ่ม `s` และ `es` เพื่อครอบคลุมรูปพหูพจน์ปกติที่อาจไม่ถูกตรวจจับโดยการตรวจสอบก่อนหน้า

#### เคล็ดลับการแก้ไขปัญหา

- **Case Sensitivity:** เมธอดใช้ `toLowerCase()` สำหรับการเปรียบเทียบ ทำให้ “Cats” และ “cats” ทำงานเหมือนกัน  
- **Edge Cases:** คำที่สั้นกว่าความยาวของ suffix จะถูกละเว้นเพื่อหลีกเลี่ยงการคืนสตริงว่าง  
- **Performance:** สำหรับพจนานุกรมขนาดใหญ่ ควรแคชผลลัพธ์ใน `ConcurrentHashMap`

## การประยุกต์ใช้งานจริง

การ Implement **create word forms provider** สามารถเพิ่มประสิทธิภาพในหลายสถานการณ์จริง:

1. **Search Engines:** ผู้ใช้พิมพ์ “mouse” ควรพบเอกสารที่มี “mice” ด้วย Provider สามารถสร้างรูปแบบที่ไม่ปกติเช่นนี้ได้  
2. **Text Analysis Tools:** การวิเคราะห์อารมณ์หรือการสกัดเอนทิตี้ทำได้แม่นยำขึ้นเมื่อรับรู้รูปแบบคำทั้งหมด  
3. **Content Management Systems:** การสร้างแท็กอัตโนมัติสามารถรวมคำพหูพจน์เป็นส่วนหนึ่งของ synonym ทำให้ SEO และการเชื่อมโยงภายในดีขึ้น

## พิจารณาด้านประสิทธิภาพ

เมื่อใส่ Provider เข้าไปในระบบ production ควรคำนึงถึง:

- **Cache รูปแบบที่ใช้บ่อย:** เก็บผลลัพธ์ในหน่วยความจำเพื่อหลีกเลี่ยงการคำนวณซ้ำ  
- **ตรวจสอบ JVM Heap:** ดัชนีขนาดใหญ่เพิ่มความกดดันของหน่วยความจำ; ปรับ `-Xmx` ให้เหมาะสม  
- **ใช้ Collection ที่มีประสิทธิภาพ:** `ArrayList` เหมาะกับชุดเล็ก ๆ แต่หากต้องจัดการหลายพันรูปแบบ ควรพิจารณา `HashSet` เพื่อลบซ้ำอย่างรวดเร็ว

**Best Practices**

- อัปเดตไลบรารีให้เป็นเวอร์ชันล่าสุดเพื่อรับประโยชน์จากแพตช์ประสิทธิภาพ  
- ทำ profiling ให้ Provider ด้วยโหลดการค้นหาจริงเพื่อหาจุดคอขวดตั้งแต่แรก  

## สรุป

คุณได้เรียนรู้วิธี **create word forms provider** ด้วย GroupDocs.Search สำหรับ Java แล้ว Component ขนาดเล็กนี้สามารถปรับปรุงความเกี่ยวข้องของผลการค้นหาและความแม่นยำของการวิเคราะห์ภาษาในหลายแอปพลิเคชันได้อย่างมีนัยสำคัญ  

**ขั้นตอนต่อไป:**  
- ทดลองใช้กฎทางภาษาที่ซับซ้อนขึ้น (เช่น พหูพจน์ที่ไม่เป็นระเบียบ, stemming)  
- ผสาน Provider เข้าไปใน pipeline การทำดัชนีและวัดผลการเพิ่ม recall  
- สำรวจฟีเจอร์อื่นของ GroupDocs.Search เช่น synonym dictionaries และ custom analyzers  

**Call to Action:** ลองเพิ่ม `SimpleWordFormsProvider` ลงในโปรเจกต์ของคุณวันนี้และดูว่ามันทำให้ประสบการณ์การค้นหาของคุณดีขึ้นแค่ไหน!

## FAQ Section

**1. GroupDocs.Search for Java คืออะไร?**  
เป็นไลบรารีที่ทรงพลังให้บริการ full‑text search, indexing, และฟีเจอร์ด้านภาษาต่าง ๆ รวมถึงความสามารถในการต่อ custom word‑form providers

**2. SimpleWordFormsProvider ทำงานอย่างไร?**  
มันสร้างรูปแบบทางเลือกโดยใช้กฎพื้นฐานที่อิง suffix (ลบ “s/es”, แปลง “y” เป็น “is”, และเพิ่ม “s/es”)

**3. สามารถปรับแต่งกฎการสร้างรูปแบบคำได้หรือไม่?**  
ได้เลย แก้ไขเมธอด `getWordForms` เพื่อเพิ่มรูปแบบที่ไม่เป็นระเบียบ, กฎตาม locale, หรือเชื่อมต่อกับพจนานุกรมภายนอก

**4. มีการใช้งานทั่วไปของฟีเจอร์นี้บ้าง?**  
Search engines, pipelines การวิเคราะห์ข้อความ, และแพลตฟอร์ม CMS ต่าง ๆ จะได้ประโยชน์จากการรับรู้รูปแบบเอกพจน์/พหูพจน์

**5. ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งาน production หรือไม่?**  
ใช่—แม้ trial จะให้คุณสำรวจ API ได้ แต่ไลเซนส์ที่ซื้อจะลบข้อจำกัดการใช้งานและให้การสนับสนุน

---

**Last Updated:** 2025-12-20  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs
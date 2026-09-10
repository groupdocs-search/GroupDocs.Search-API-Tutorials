---
date: '2026-09-06'
description: GroupDocs.Search for Java का उपयोग करके फ़ाइल एक्सटेंशन java को फ़िल्टर
  करना सीखें, जिसमें logical AND, OR, NOT operators, date range filters, और path filters
  शामिल हैं।
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: GroupDocs.Search का उपयोग करके फ़ाइल एक्सटेंशन java को फ़िल्टर करें।
  Java में logical operators के साथ extension, date range, और path filters को combine
  करना सीखें।
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: GroupDocs.Search के साथ फ़ाइल एक्सटेंशन java को फ़िल्टर करें – Complete
  Guide
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: GroupDocs.Search के साथ फ़ाइल एक्सटेंशन java को फ़िल्टर करने का तरीका
type: docs
url: /hi/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search के साथ जावा फ़ाइल एक्सटेंशन फ़िल्टर

इस व्यापक ट्यूटोरियल में आप सीखेंगे कि GroupDocs.Search के साथ दस्तावेज़ों को इंडेक्स करते समय **जावा फ़ाइल एक्सटेंशन फ़िल्टर** कैसे किया जाता है। गाइड के अंत तक आप केवल आवश्यक फ़ाइल प्रकारों को शामिल कर पाएँगे, अनचाहे फ़ॉर्मेट को बाहर रख पाएँगे, और तिथि‑रेंज और पाथ फ़िल्टर के साथ इन नियमों को लॉजिकल AND, OR, और NOT ऑपरेटरों का उपयोग करके संयोजित कर पाएँगे। यह तरीका आपके इंडेक्स को हल्का रखता है, खोज को तेज़ करता है, और डेटा‑हैंडलिंग नीतियों के अनुपालन में मदद करता है।

## त्वरित उत्तर
- **जावा फ़ाइल एक्सटेंशन फ़िल्टर क्या है?** यह एक नियम है जो GroupDocs.Search को बताता है कि इंडेक्सिंग के दौरान किन फ़ाइल एक्सटेंशन को शामिल या बाहर किया जाए।  
- **यह सुविधा कौन सी लाइब्रेरी प्रदान करती है?** GroupDocs.Search for Java.  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं फ़िल्टर को संयोजित कर सकता हूँ?** हाँ – आप एक्सटेंशन, तिथि, आकार, और पाथ फ़िल्टर को AND, OR, NOT लॉजिक के साथ जोड़ सकते हैं।  
- **क्या यह Maven‑संगत है?** बिल्कुल – अपने `pom.xml` में GroupDocs.Search निर्भरता जोड़ें।

## जावा फ़ाइल एक्सटेंशन फ़िल्टर क्या है?
एक **जावा फ़ाइल एक्सटेंशन फ़िल्टर** नियमों का सेट है जो प्रत्येक फ़ाइल के एक्सटेंशन का मूल्यांकन करता है इससे पहले कि वह इंडेक्सिंग इंजन को भेजी जाए। `.txt`, `.pdf`, या `.epub` जैसे एक्सटेंशन निर्दिष्ट करके आप **एक्सटेंशन द्वारा फ़ाइलें शामिल** कर सकते हैं या **एक्सटेंशन द्वारा फ़ाइलें बाहर** रख सकते हैं ताकि आपका इंडेक्स केंद्रित रहे और खोज परिणाम प्रासंगिक हों।

## GroupDocs.Search के साथ फ़ाइल‑एक्सटेंशन फ़िल्टरिंग क्यों उपयोग करें?
फ़ाइल‑एक्सटेंशन फ़िल्टरिंग अप्रासंगिक फ़ॉर्मेट को बाहर रखकर इंडेक्सिंग दक्षता को बढ़ाती है, स्टोरेज की आवश्यकता को कम करती है, और अनचाहे कंटेंट को इंडेक्स में प्रवेश करने से रोककर अनुपालन नियमों को पूरा करने में मदद करती है। यह तेज़ क्वेरी प्रतिक्रियाओं को भी सक्षम बनाती है क्योंकि सर्च इंजन एक छोटे, अधिक प्रासंगिक डेटासेट को प्रोसेस करता है।

- **प्रदर्शन:** अनावश्यक फ़ाइलों को छोड़ने से I/O कम होता है और बड़े रिपॉज़िटरीज़ पर इंडेक्सिंग 40 % तक तेज़ हो जाती है।  
- **स्टोरेज बचत:** केवल प्रासंगिक दस्तावेज़ इंडेक्स में संग्रहीत होते हैं, जिससे डिस्क उपयोग औसतन 30 % तक घटता है।  
- **अनुपालन:** गोपनीय या असमर्थित फ़ाइल प्रकारों के आकस्मिक इंडेक्सिंग को रोकें।  
- **लचीलापन:** **date range filter java** सुविधाओं के साथ संयोजित करके विशिष्ट अवधि में बनाई या संशोधित फ़ाइलों को लक्षित करें।

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

### आवश्यक लाइब्रेरी और निर्भरताएँ
- **GroupDocs.Search for Java** – संस्करण 25.4 या बाद का (60+ इनपुट फ़ॉर्मेट का समर्थन करता है)।  
- **Java Development Kit (JDK)** – कोई भी संगत संस्करण (8 या नया)।

### पर्यावरण सेटअप
- एकीकृत विकास वातावरण (IDE): IntelliJ IDEA, Eclipse, या कोई भी Maven‑संगत IDE।

### ज्ञान पूर्वापेक्षाएँ
- बुनियादी Java प्रोग्रामिंग।  
- Java में फ़ाइल I/O की परिचितता।  
- रेगुलर एक्सप्रेशन और तिथि‑समय हैंडलिंग की समझ।

## GroupDocs.Search के लिए Java सेटअप
GroupDocs.Search का उपयोग शुरू करने के लिए, आपको इसे अपने प्रोजेक्ट में एक निर्भरता के रूप में शामिल करना होगा।

### Maven कॉन्फ़िगरेशन
`pom.xml` फ़ाइल में निम्नलिखित रिपॉज़िटरी और निर्भरता कॉन्फ़िगरेशन जोड़ें:

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

### प्रत्यक्ष डाउनलोड
वैकल्पिक रूप से, नवीनतम संस्करण सीधे [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

#### लाइसेंस प्राप्ति
1. **Free trial** – बिना लागत के सुविधाओं का अन्वेषण करें।  
2. **Temporary license** – सीमित अवधि के लिए पूर्ण कार्यक्षमता प्राप्त करें।  
3. **Purchase** – उत्पादन उपयोग के लिए स्थायी लाइसेंस प्राप्त करें।

### बुनियादी प्रारंभिककरण और सेटअप
लाइब्रेरी जोड़ने के बाद, अपने इंडेक्सिंग पर्यावरण को प्रारंभ करें। `IndexSettings` क्लास सभी कॉन्फ़िगरेशन विकल्पों को रखती है, जिसमें फ़िल्टर भी शामिल हैं।

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## कार्यान्वयन गाइड
नीचे हम प्रत्येक फ़िल्टर प्रकार में गहराई से देखते हैं, **क्यों यह महत्वपूर्ण है** समझाते हैं और चरण‑दर‑चरण निर्देश प्रदान करते हैं जिन्हें आप अपने प्रोजेक्ट में कॉपी कर सकते हैं।

### फ़ाइल एक्सटेंशन फ़िल्टरिंग
इंडेक्सिंग के दौरान फ़ाइलों को उनके एक्सटेंशन के आधार पर फ़िल्टर करें। यह तब आदर्श है जब आप केवल ई‑बुक्स (`.fb2`, `.epub`) और साधारण‑टेक्स्ट फ़ाइलें (`.txt`) प्रोसेस करना चाहते हैं।

#### अवलोकन
`DocumentFilter.createFileExtension` एक्सटेंशन की व्हाइटलिस्ट बनाता है।

#### कार्यान्वयन चरण
1. **फ़िल्टर बनाएं** – उन एक्सटेंशन को परिभाषित करें जिन्हें आप रखना चाहते हैं।

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **इंडेक्स प्रारंभ करें और दस्तावेज़ जोड़ें** – `IndexSettings` बनाते समय फ़िल्टर लागू करें।

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### लॉजिकल NOT फ़िल्टर
विशिष्ट एक्सटेंशन, जैसे वेब पेज और PDFs, को बाहर रखें जब वे आपके खोज परिदृश्य के लिए आवश्यक न हों।

#### कार्यान्वयन चरण
1. **बहिष्करण फ़िल्टर बनाएं** – बाहर करने के लिए एक्सटेंशन निर्दिष्ट करें।

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **इंडेक्स सेटिंग्स पर लागू करें** – NOT फ़िल्टर को अन्य नियमों के साथ संयोजित करें।

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **दस्तावेज़ जोड़ें** – केवल वे फ़ाइलें जो संयुक्त फ़िल्टर को पास करती हैं, इंडेक्स की जाती हैं।

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### लॉजिकल AND फ़िल्टर
कई शर्तों—निर्माण तिथि, एक्सटेंशन, और फ़ाइल आकार—को मिलाकर **सभी मानदंडों को पूरा करने वाली फ़ाइलें** ही इंडेक्स की जाती हैं।

#### अवलोकन
`DocumentFilter.createAnd` कई फ़िल्टर को एक नियम में मिलाता है।

#### कार्यान्वयन चरण
1. **फ़िल्टर परिभाषित करें** – प्रत्येक शर्त के लिए व्यक्तिगत फ़िल्टर बनाएं।

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **फ़िल्टर संयोजित करें** – सभी शर्तों को आवश्यक बनाने के लिए AND ऑपरेटर का उपयोग करें।

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **दस्तावेज़ इंडेक्स करें** – संयुक्त फ़िल्टर को इंडेक्सिंग पाइपलाइन में फीड करें।

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### लॉजिकल OR फ़िल्टर
फ़ाइलें शामिल करें जो निर्दिष्ट शर्तों में **किसी भी** को पूरा करती हों—जब आप छोटे टेक्स्ट फ़ाइलें और बड़े गैर‑टेक्स्ट फ़ाइलें दोनों को कैप्चर करना चाहते हैं तो उपयोगी।

#### कार्यान्वयन चरण
1. **फ़िल्टर परिभाषित करें** – प्रत्येक वैकल्पिक शर्त के लिए अलग-अलग फ़िल्टर बनाएं।

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **लॉजिकल शर्तों के साथ फ़िल्टर संयोजित करें** – OR ऑपरेटर का उपयोग करें।

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **OR फ़िल्टर को अंतिम रूप दें** – संयुक्त फ़िल्टर को इंडेक्स कॉन्फ़िगरेशन से जोड़ें।

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### निर्माण समय फ़िल्टर
एक विशिष्ट अवधि में बनाई गई फ़ाइलों को लक्षित करें—एक क्लासिक **date range filter java** परिदृश्य।

#### कार्यान्वयन चरण
1. **date‑range फ़िल्टर परिभाषित करें** – प्रारंभ और समाप्ति तिथियां निर्दिष्ट करें।

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **दस्तावेज़ इंडेक्स करें** – केवल वे फ़ाइलें जिनके निर्माण टाइमस्टैम्प रेंज के भीतर हैं, इंडेक्स की जाती हैं।

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### संशोधन समय फ़िल्टर
उन फ़ाइलों को बाहर रखें जो किसी निश्चित कटऑफ़ तिथि के बाद संशोधित हुई हैं।

#### कार्यान्वयन चरण
1. **फ़िल्टर परिभाषित करें** – अधिकतम संशोधन टाइमस्टैम्प सेट करें।

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **दस्तावेज़ इंडेक्स करें** – कटऑफ़ से नई फ़ाइलें अनदेखी की जाती हैं।

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### फ़ाइल पाथ फ़िल्टरिंग
इंडेक्सिंग को उन फ़ाइलों तक सीमित करें जो विशेष फ़ोल्डरों में स्थित हैं या किसी पैटर्न से मेल खाती हैं—विशिष्ट डायरेक्टरी पदानुक्रम में **include files by extension** के लिए आदर्श।

#### कार्यान्वयन चरण
1. **फ़ाइल‑पाथ फ़िल्टर परिभाषित करें** – डायरेक्टरी मिलाने के लिए ग्लॉब या रेगेक्स पैटर्न का उपयोग करें।

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **इंडेक्स प्रारंभ करें और दस्तावेज़ जोड़ें** – पाथ फ़िल्टर को अन्य नियमों के साथ लागू करें।

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## सामान्य कठिनाइयाँ और सुझाव

- **कभी भी एक ही फ़िल्टर कॉन्फ़िगरेशन में पूर्ण (absolute) और सापेक्ष (relative) पाथ को मिलाएँ नहीं** – इससे अप्रत्याशित बहिष्कार हो सकते हैं।  
- फ़िल्टर सेट बदलते समय `IndexSettings` को **रीसेट** करें; अन्यथा पिछले फ़िल्टर बने रह सकते हैं।  
- बड़े संग्रहों के लिए मेमोरी उपयोग कम रखने हेतु **लंबाई की ऊपरी सीमा को एक्सटेंशन फ़िल्टर के साथ संयोजित** करें।  
- LoggingOptions GroupDocs.Search के लॉगिंग कॉन्फ़िगरेशन को नियंत्रित करता है।  
- **लॉगिंग सक्षम करें** (`LoggingOptions.setEnabled(true)`) ताकि यह देखा जा सके कि कोई फ़ाइल क्यों अस्वीकार हुई।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं इंडेक्स बन जाने के बाद फ़िल्टर मानदंड बदल सकता हूँ?**  
A: हाँ। नया `DocumentFilter` के साथ इंडेक्स को पुनः बनाएं या अपडेटेड सेटिंग्स के साथ इंक्रीमेंटल इंडेक्सिंग का उपयोग करें।

**Q: क्या जावा फ़ाइल एक्सटेंशन फ़िल्टर संकुचित अभिलेखों (जैसे, ZIP) पर काम करता है?**  
A: GroupDocs.Search समर्थित अभिलेख फ़ॉर्मेट को इंडेक्स कर सकता है, लेकिन एक्सटेंशन फ़िल्टर अभिलेख स्वयं पर लागू होता है, अंदर की फ़ाइलों पर नहीं। गहरी नियंत्रण के लिए नेस्टेड फ़िल्टर का उपयोग करें।

**Q: मैं कैसे डिबग करूँ कि कोई विशेष फ़ाइल क्यों बाहर रखी गई?**  
A: लाइब्रेरी की लॉगिंग सक्षम करें (`LoggingOptions.setEnabled(true)`) और लॉग देखें – यह बताता है कि कौन सा फ़िल्टर प्रत्येक फ़ाइल को अस्वीकार करता है।

**Q: क्या जावा फ़ाइल एक्सटेंशन फ़िल्टर को कस्टम रेगेक्स फ़िल्टर के साथ संयोजित करना संभव है?**  
A: बिल्कुल। `DocumentFilter.createAnd()` के भीतर एक्सटेंशन फ़िल्टर के साथ रेगेक्स फ़िल्टर को रैप करें।

**Q: कई फ़िल्टर जोड़ने का प्रदर्शन पर क्या प्रभाव पड़ता है?**  
A: प्रत्येक फ़िल्टर इंडेक्सिंग के दौरान थोड़ा ओवरहेड जोड़ता है, लेकिन इंडेक्स किए गए डेटा की कमी आमतौर पर लागत से अधिक होती है। इष्टतम संतुलन खोजने के लिए प्रतिनिधि नमूने के साथ परीक्षण करें।

---

**अंतिम अपडेट:** 2026-09-06  
**परीक्षण किया गया:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [कस्टम डेट फॉर्मेट जावा | ग्रुपडॉक्स के साथ डेट रेंज सर्च](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: ग्रुपडॉक्स.Search for Java के साथ बूलियन सर्च में महारत](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [ग्रुपडॉक्स.Search for Java में उन्नत इंडेक्सिंग तकनीकों के साथ सर्च प्रदर्शन को अनुकूलित करें](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


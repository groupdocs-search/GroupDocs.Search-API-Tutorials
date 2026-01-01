---
date: '2025-12-19'
description: GroupDocs.Search for Java का उपयोग करके जावा फ़ाइल एक्सटेंशन फ़िल्टर
  को लागू करना सीखें, जिसमें लॉजिकल ऑपरेटर्स, निर्माण/संशोधन तिथियां और पाथ फ़िल्टर
  शामिल हैं।
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: GroupDocs.Search के साथ जावा फ़ाइल एक्सटेंशन फ़िल्टर – गाइड
type: docs
url: /hi/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search के साथ java फ़ाइल एक्सटेंशन फ़िल्टर में महारत हासिल करना

दस्तावेज़ों के बढ़ते रिपॉज़िटरी को प्रबंधित करना जल्दी ही भारी लग सकता है। चाहे आपको केवल विशिष्ट दस्तावेज़ प्रकारों को इंडेक्स करना हो या अप्रासंगिक फ़ाइलों को बाहर रखना हो, एक **java फ़ाइल एक्सटेंशन फ़िल्टर** आपको प्रोसेस होने वाली फ़ाइलों पर सूक्ष्म नियंत्रण देता है। इस गाइड में हम GroupDocs.Search for Java को सेट अप करने की प्रक्रिया दिखाएंगे और यह बताएँगे कि फ़ाइल‑एक्सटेंशन फ़िल्टरिंग को लॉजिकल AND, OR, और NOT ऑपरेटर्स के साथ, साथ ही डेट‑रेंज और पाथ फ़िल्टर के साथ कैसे संयोजित किया जाए।

## त्वरित उत्तर
- **java फ़ाइल एक्सटेंशन फ़िल्टर क्या है?** एक कॉन्फ़िगरेशन जो GroupDocs.Search को बताता है कि इंडेक्सिंग के दौरान कौन से फ़ाइल एक्सटेंशन को शामिल या बाहर किया जाए।  
- **यह सुविधा कौन सी लाइब्रेरी प्रदान करती है?** GroupDocs.Search for Java।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं फ़िल्टरों को संयोजित कर सकता हूँ?** हाँ – आप एक्सटेंशन, डेट, साइज, और पाथ फ़िल्टर को AND, OR, NOT लॉजिक के साथ चेन कर सकते हैं।  
- **क्या यह Maven‑संगत है?** बिल्कुल – अपने `pom.xml` में GroupDocs.Search डिपेंडेंसी जोड़ें।  

## परिचय

फ़ाइलों के बढ़ते रिपॉज़िटरी को प्रभावी ढंग से प्रबंधित करने में संघर्ष हो रहा है? चाहे आपको दस्तावेज़ों को प्रकार के अनुसार व्यवस्थित करना हो या इंडेक्सिंग के दौरान अनावश्यक फ़ाइलों को फ़िल्टर करना हो, सही टूल्स के बिना यह कार्य कठिन हो सकता है। **GroupDocs.Search for Java** एक उन्नत सर्च लाइब्रेरी है जो शक्तिशाली फ़ाइल फ़िल्टरिंग क्षमताओं के माध्यम से इन चुनौतियों को सरल बनाती है। यह ट्यूटोरियल आपको GroupDocs.Search का उपयोग करके .NET फ़ाइल फ़िल्टरिंग तकनीकों को लागू करने में मार्गदर्शन करेगा, जिसमें लॉजिकल AND, OR, और NOT फ़िल्टरों पर ध्यान केंद्रित किया गया है।

### आप क्या सीखेंगे
- अपने Java वातावरण में GroupDocs.Search सेट अप करना  
- विभिन्न फ़िल्टरों को लागू करना: फ़ाइल एक्सटेंशन, लॉजिकल ऑपरेटर्स (AND, OR, NOT), निर्माण समय, संशोधन समय, फ़ाइल पाथ, और लंबाई  
- प्रभावी दस्तावेज़ प्रबंधन के लिए इन फ़िल्टरों के वास्तविक‑दुनिया अनुप्रयोग  
- बड़े‑पैमाने पर इंडेक्सिंग कार्यों के लिए प्रदर्शन अनुकूलन टिप्स  

Java में फ़ाइल फ़िल्टरिंग की पूरी क्षमता को अनलॉक करने के लिए तैयार हैं? चलिए पहले आवश्यकताओं में डुबकी लगाते हैं।

## आवश्यकताएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

### आवश्यक लाइब्रेरी और डिपेंडेंसीज़
- **GroupDocs.Search for Java**: संस्करण 25.4 या बाद का  
- **Java Development Kit (JDK)**: सुनिश्चित करें कि आपके सिस्टम पर संगत संस्करण स्थापित है  

### पर्यावरण सेटअप
- इंटीग्रेटेड डेवलपमेंट एनवायरनमेंट (IDE): IntelliJ IDEA, Eclipse, या कोई भी पसंदीदा IDE उपयोग करें जो Maven प्रोजेक्ट्स को सपोर्ट करता हो।  

### ज्ञान आवश्यकताएँ
- Java प्रोग्रामिंग की बुनियादी समझ  
- Java में फ़ाइल I/O ऑपरेशन्स की परिचितता  
- रेगुलर एक्सप्रेशन्स और डेट‑टाइम मैनिपुलेशन की समझ  

## GroupDocs.Search for Java सेट अप करना
GroupDocs.Search का उपयोग शुरू करने के लिए, आपको इसे अपने प्रोजेक्ट में एक डिपेंडेंसी के रूप में शामिल करना होगा। यह रहा तरीका:

### Maven कॉन्फ़िगरेशन
`pom.xml` फ़ाइल में निम्नलिखित रिपॉज़िटरी और डिपेंडेंसी कॉन्फ़िगरेशन जोड़ें:

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

### सीधे डाउनलोड
वैकल्पिक रूप से, नवीनतम संस्करण सीधे [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

#### लाइसेंस प्राप्ति
1. **Free Trial**: GroupDocs.Search की सुविधाओं को खोजने के लिए फ्री ट्रायल से शुरू करें।  
2. **Temporary License**: बिना सीमाओं के पूरी कार्यक्षमता तक पहुंचने के लिए एक अस्थायी लाइसेंस के लिए आवेदन करें।  
3. **Purchase**: दीर्घकालिक उपयोग के लिए, एक सब्सक्रिप्शन खरीदें।  

### बुनियादी इनिशियलाइज़ेशन और सेटअप
लाइब्रेरी जोड़ने के बाद, अपने इंडेक्सिंग वातावरण को इनिशियलाइज़ करें:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## कार्यान्वयन गाइड
अब, चलिए GroupDocs.Search का उपयोग करके विभिन्न फ़ाइल फ़िल्टरिंग सुविधाओं को लागू करने के तरीकों को देखें।

### फ़ाइल एक्सटेंशन फ़िल्टरिंग
इंडेक्सिंग के दौरान फ़ाइलों को उनके एक्सटेंशन के आधार पर फ़िल्टर करें। यह सुविधा केवल विशिष्ट दस्तावेज़ प्रकारों जैसे FB2, EPUB, और TXT को प्रोसेस करने में उपयोगी है।

#### अवलोकन
कस्टम फ़िल्टर कॉन्फ़िगरेशन का उपयोग करके फ़ाइल एक्सटेंशन के आधार पर दस्तावेज़ फ़िल्टर करें।

#### कार्यान्वयन चरण
1. **फ़िल्टर बनाएं**:

```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **इंडेक्स इनिशियलाइज़ करें और दस्तावेज़ जोड़ें**:

```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### लॉजिकल NOT फ़िल्टर
इंडेक्सिंग के दौरान विशिष्ट फ़ाइल एक्सटेंशन जैसे HTM, HTML, और PDF को बाहर रखें।

#### कार्यान्वयन चरण
1. **बहिष्करण फ़िल्टर बनाएं**:

```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **इंडेक्स सेटिंग्स पर लागू करें**:

```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **दस्तावेज़ जोड़ें**:

```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### लॉजिकल AND फ़िल्टर
कई मानदंडों को संयोजित करके केवल उन फ़ाइलों को शामिल करें जो सभी निर्दिष्ट शर्तों को पूरा करती हैं।

#### अवलोकन
फ़ाइलों को निर्माण समय, फ़ाइल एक्सटेंशन, और लंबाई के आधार पर फ़िल्टर करने के लिए लॉजिकल AND ऑपरेशन का उपयोग करें।

#### कार्यान्वयन चरण
1. **फ़िल्टर परिभाषित करें**:

```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **फ़िल्टर संयोजित करें**:

```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **दस्तावेज़ इंडेक्स करें**:

```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### लॉजिकल OR फ़िल्टर
लॉजिकल OR ऑपरेशन्स का उपयोग करके उन फ़ाइलों को शामिल करें जो निर्दिष्ट मानदंडों में से किसी एक को पूरा करती हैं।

#### कार्यान्वयन चरण
1. **फ़िल्टर परिभाषित करें**:

```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **लॉजिकल शर्तों के साथ फ़िल्टर संयोजित करें**:

```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **OR फ़िल्टर को अंतिम रूप दें**:

```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### निर्माण समय फ़िल्टर
फ़ाइलों को उनके निर्माण समय के आधार पर फ़िल्टर करें ताकि केवल निर्दिष्ट डेट रेंज के भीतर वाली फ़ाइलें शामिल हों।

#### कार्यान्वयन चरण
1. **डेट रेंज फ़िल्टर परिभाषित करें**:

```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **दस्तावेज़ इंडेक्स करें**:

```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### संशोधन समय फ़िल्टर
निर्दिष्ट तिथि के बाद संशोधित हुई फ़ाइलों को बाहर रखें।

#### कार्यान्वयन चरण
1. **फ़िल्टर परिभाषित करें**:

```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **दस्तावेज़ इंडेक्स करें**:

```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### फ़ाइल पाथ फ़िल्टरिंग
फ़ाइलों को उनके पाथ के आधार पर फ़िल्टर करें ताकि केवल विशिष्ट डायरेक्टरी में स्थित फ़ाइलें शामिल हों।

#### कार्यान्वयन चरण
1. **फ़ाइल पाथ फ़िल्टर परिभाषित करें**:

```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **इंडेक्स इनिशियलाइज़ करें और दस्तावेज़ जोड़ें**:

```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## सामान्य कठिनाइयाँ और टिप्स
- **कभी भी एक ही फ़िल्टर कॉन्फ़िगरेशन में एब्सोल्यूट और रिलेटिव पाथ को मिलाएँ नहीं** – इससे अप्रत्याशित बहिष्करण हो सकते हैं।  
- **जब आप एक फ़िल्टर सेट से दूसरे में स्विच करते हैं तो `IndexSettings` को रीसेट करना याद रखें**; अन्यथा पहले के फ़िल्टर बने रह सकते हैं।  
- **बड़ी फ़ाइल संग्रह** मेमोरी उपयोग को कम रखने के लिए लंबाई की ऊपरी सीमा को एक्सटेंशन फ़िल्टर के साथ संयोजित करने से लाभ मिलता है।  

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं इंडेक्स बन जाने के बाद फ़िल्टर मानदंड बदल सकता हूँ?**  
A: हाँ। आप नए `DocumentFilter` के साथ इंडेक्स को पुनः बनाकर या अपडेटेड सेटिंग्स के साथ इंक्रीमेंटल इंडेक्सिंग का उपयोग करके बदल सकते हैं।

**Q: क्या java फ़ाइल एक्सटेंशन फ़िल्टर संकुचित आर्काइव (जैसे ZIP) पर काम करता है?**  
A: GroupDocs.Search समर्थित आर्काइव फ़ॉर्मेट को इंडेक्स कर सकता है, लेकिन एक्सटेंशन फ़िल्टर आर्काइव स्वयं पर लागू होता है, न कि अंदर की फ़ाइलों पर। आवश्यकता होने पर नेस्टेड फ़िल्टर का उपयोग करें।

**Q: मैं कैसे डिबग करूँ कि कोई विशेष फ़ाइल क्यों बाहर रखी गई?**  
A: लाइब्रेरी की लॉगिंग को सक्षम करें (`LoggingOptions.setEnabled(true)` सेट करके) और उत्पन्न लॉग की जाँच करें – यह बताता है कि कौन सा फ़िल्टर प्रत्येक फ़ाइल को अस्वीकार कर रहा है।

**Q: क्या java फ़ाइल एक्सटेंशन फ़िल्टर को कस्टम रेगेक्स फ़िल्टरों के साथ संयोजित करना संभव है?**  
A: बिल्कुल। आप रेगेक्स फ़िल्टर को `DocumentFilter.createAnd()` के भीतर एक्सटेंशन फ़िल्टर के साथ रैप कर सकते हैं।

**Q: कई फ़िल्टर जोड़ने का प्रदर्शन पर क्या प्रभाव पड़ता है?**  
A: प्रत्येक अतिरिक्त फ़िल्टर इंडेक्सिंग के दौरान थोड़ा ओवरहेड जोड़ता है, लेकिन इंडेक्स आकार में कमी का लाभ आमतौर पर लागत से अधिक होता है। इष्टतम संतुलन खोजने के लिए एक सैंपल सेट के साथ परीक्षण करें।

---

**अंतिम अपडेट:** 2025-12-19  
**परीक्षण किया गया:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs
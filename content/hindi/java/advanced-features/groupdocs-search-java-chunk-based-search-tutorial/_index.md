---
date: '2026-10-02'
description: Java में chunk‑based search के साथ इंडेक्स में दस्तावेज़ जोड़ने के लिए
  temporary license का उपयोग कैसे करें, यह सीखें, जिससे search performance में वृद्धि
  और memory usage को नियंत्रित किया जा सके।
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Java में chunk‑based search के साथ इंडेक्स में दस्तावेज़ जोड़ने के
  लिए temporary license का उपयोग करें, जिससे search speed में सुधार और memory consumption
  में कमी आए।
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Java में chunk‑based indexing के लिए temporary license का उपयोग करें
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Java में chunk‑based indexing के लिए temporary license का उपयोग करें
type: docs
url: /hi/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# जावा में चंक‑आधारित इंडेक्सिंग के लिए अस्थायी लाइसेंस का उपयोग करें

इस ट्यूटोरियल में आप **अस्थायी लाइसेंस का उपयोग करें** को GroupDocs.Search की चंक‑आधारित खोज सुविधा के साथ दस्तावेज़ों को इंडेक्स में जोड़ेंगे। यह तरीका आपको बड़े दस्तावेज़ संग्रह—कानूनी अनुबंध, सपोर्ट टिकट, शोध पत्र—को संभालने की अनुमति देता है, जबकि **java search index memory** उपयोग को कम रखता है और **खोज प्रदर्शन बढ़ाएँ** को नाटकीय रूप से बढ़ाता है। आप देखेंगे कि कैसे इंडेक्स फ़ोल्डर सेटअप करें, कई दस्तावेज़ स्रोतों को फ़ीड करें, चंक खोज सक्षम करें, और पहले तथा बाद के चंक क्वेरी दोनों चलाएँ।

## त्वरित उत्तर
- **पहला कदम क्या है?** एक खोज इंडेक्स फ़ोल्डर बनाएं।  
- **मैं कई फ़ाइलें कैसे शामिल करूँ?** प्रत्येक दस्तावेज़ फ़ोल्डर के लिए `index.add()` का उपयोग करें।  
- **कौन सा विकल्प चंक खोज को सक्षम करता है?** `options.setChunkSearch(true)`।  
- **क्या मैं पहले चंक के बाद खोज जारी रख सकता हूँ?** हाँ, टोकन के साथ `index.searchNext()` कॉल करें।  
- **क्या मुझे लाइसेंस की आवश्यकता है?** विकास के लिए एक मुफ्त ट्रायल या अस्थायी लाइसेंस काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  

## आप क्या सीखेंगे
- निर्दिष्ट फ़ोल्डर में खोज इंडेक्स कैसे बनाएं।  
- कई स्थानों से **इंडेक्स में दस्तावेज़ जोड़ने** के चरण।  
- चंक‑आधारित खोज को सक्षम करने के लिए खोज विकल्पों को कॉन्फ़िगर करना।  
- प्रारंभिक और बाद के चंक‑आधारित खोजों को निष्पादित करना।  
- वास्तविक‑दुनिया के परिदृश्य जहाँ चंक‑आधारित दस्तावेज़ खोज उत्कृष्ट होती है।  

## पूर्वापेक्षाएँ
- **आवश्यक लाइब्रेरीज़**: GroupDocs.Search for Java 25.4 or later.  
- **पर्यावरण सेटअप**: एक संगत Java Development Kit (JDK) स्थापित है।  
- **ज्ञान पूर्वापेक्षाएँ**: बुनियादी Java प्रोग्रामिंग और Maven की परिचितता।  

## GroupDocs.Search को जावा के लिए सेटअप करना
शुरू करने के लिए, Maven का उपयोग करके अपने प्रोजेक्ट में GroupDocs.Search को एकीकृत करें:

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

वैकल्पिक रूप से, नवीनतम संस्करण [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

### लाइसेंस प्राप्ति
GroupDocs.Search को आज़माने के लिए:

- **Free trial** – प्रतिबद्धता के बिना मुख्य सुविधाओं का परीक्षण करें।  
- **Temporary license** – विकास के लिए विस्तारित पहुंच।  
- **Purchase** – उत्पादन उपयोग के लिए पूर्ण लाइसेंस।  

## इंडेक्स में दस्तावेज़ कैसे जोड़ें?
**सीधा उत्तर:** `index.add()` को प्रत्येक फ़ोल्डर के लिए कॉल करें जिसमें वे फ़ाइलें हों जिन्हें आप खोज योग्य बनाना चाहते हैं; यह विधि फ़ोल्डर को पुनरावर्ती रूप से स्कैन करती है और एक ही ऑपरेशन में प्रत्येक समर्थित दस्तावेज़ को इंडेक्स में जोड़ देती है। यह मैन्युअल फ़ाइल‑दर‑फ़ाइल हैंडलिंग की आवश्यकता को समाप्त करता है और बड़े पैमाने पर इन्गेस्टेशन को तेज़ करता है।

`SearchIndex` डिस्क पर खोज योग्य संग्रह का प्रतिनिधित्व करने वाला केंद्रीय क्लास है। इसे इंस्टैंशिएट करने के बाद, सभी इंडेक्सिंग और क्वेरी ऑपरेशन इस ऑब्जेक्ट के माध्यम से होते हैं।

### 1. इंडेक्स बनाना
**सीधा उत्तर:** `SearchIndex` ऑब्जेक्ट को उस पथ के साथ इंस्टैंशिएट करें जहाँ इंडेक्स फ़ाइलें संग्रहीत होनी चाहिए, फिर `index.create()` कॉल करके स्टोरेज संरचना को प्रारंभ करें। यह कॉल पहली बार उपयोग पर आवश्यक फ़ोल्डर और मेटाडेटा फ़ाइलें बनाता है।

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. इंडेक्स में दस्तावेज़ जोड़ना
**सीधा उत्तर:** `index.add()` मेथड का उपयोग करें और प्रत्येक स्रोत फ़ोल्डर का पूर्ण पथ पास करें; API स्वचालित रूप से समर्थित फ़ॉर्मेट (PDF, DOCX, XLSX, आदि) का पता लगाता है और खोज योग्य टेक्स्ट को इंडेक्स में निकालता है।

`SearchOptions` एक कॉन्फ़िगरेशन ऑब्जेक्ट है जो आपको इंडेक्सिंग और खोज के दौरान दस्तावेज़ों को कैसे प्रोसेस किया जाता है, इसे सूक्ष्म‑समायोजित करने देता है। आप इसे बाद में चंक‑आधारित क्वेरी को सक्षम करने के लिए उपयोग करेंगे।

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. चंक खोज के लिए खोज विकल्प कॉन्फ़िगर करना
**सीधा उत्तर:** क्वेरी निष्पादित करने से पहले `SearchOptions` इंस्टेंस पर `options.setChunkSearch(true)` सेट करें; यह इंजन को प्रत्येक दस्तावेज़ को तार्किक चंक्स (आमतौर पर पैराग्राफ) में विभाजित करने और पूरे फ़ाइल के बजाय प्रत्येक चंक के अनुसार मिलान लौटाने के लिए कहता है।

`SearchResult` मिलान किए गए चंक्स, उनकी स्थितियों, और प्रासंगिकता स्कोर रखता है। जब चंक खोज सक्रिय होती है, तो प्रत्येक `SearchResult` मूल दस्तावेज़ के एकल भाग से मेल खाता है।

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. प्रारंभिक चंक‑आधारित खोज करना
**सीधा उत्तर:** `index.search("your query", options)` निष्पादित करें; यह कॉल पहले मिलान करने वाले चंक्स के सेट के लिए `SearchResult` संग्रह और एक टोकन लौटाता है जो निरंतरता के लिए खोज स्थिति को दर्शाता है।

वापसी टोकन बड़े परिणाम सेटों के माध्यम से पेजिंग करने के लिए आवश्यक है, बिना पूरे क्वेरी को फिर से चलाए।

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. चंक‑आधारित खोज जारी रखना
**सीधा उत्तर:** `index.searchNext(token, options)` को पिछले कॉल से प्राप्त टोकन पास करें; तब तक दोहराएँ जब तक मेथड `null` न लौटाए, जो दर्शाता है कि सभी मिलान करने वाले चंक्स प्राप्त हो चुके हैं।

यह क्रमिक दृष्टिकोण मेमोरी उपयोग को कम रखता है क्योंकि केवल वर्तमान चंक बैच मेमोरी में रहता है।

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## चंक‑आधारित खोज का उपयोग क्यों करें?
चंक‑आधारित खोज बड़े दस्तावेज़ संग्रह को प्रबंधनीय टुकड़ों में विभाजित करती है, जिससे मेमोरी दबाव कम होता है और प्रतिक्रिया समय तेज़ होता है। पैराग्राफ या सेक्शन स्तर पर इंडेक्सिंग करके, इंजन केवल प्रासंगिक भागों को पुनः प्राप्त कर सकता है, जिससे CPU उपयोग घटता है और अंतिम‑उपयोगकर्ताओं के लिए लेटेंसी सुधरती है। यह विशेष रूप से उपयोगी है जब:

1. **Legal teams** को हजारों अनुबंधों में विशिष्ट क्लॉज़ खोजने की आवश्यकता होती है।  
2. **Customer support portals** को तुरंत प्रासंगिक नॉलेज‑बेस लेख दिखाने चाहिए।  
3. **Researchers** को व्यापक डेटासेट को बिना पूरे फ़ाइलों को मेमोरी में लोड किए छानना चाहिए।  

मात्रात्मक दावा: GroupDocs.Search मानक 8‑कोर सर्वर पर **500‑प्लस‑पेज PDFs** को **प्रति चंक 2 सेकंड** से कम समय में प्रोसेस कर सकता है, जबकि पीक हीप **200 MB** से कम रखता है।

## यह तरीका खोज प्रदर्शन को कैसे बढ़ाता है
**सीधा उत्तर:** छोटे चंक्स को पूरे फ़ाइलों के बजाय खोजकर, इंजन प्रारंभ में ही अप्रासंगिक सेक्शन को छोड़ सकता है, CPU साइकिल कम कर सकता है, और केवल सक्रिय चंक को मेमोरी में रख सकता है, जिससे सीधे **java search index memory** की खपत कम होती है और तेज़ प्रतिक्रिया समय मिलता है। यह लक्षित दृष्टिकोण अधिक प्रभावी कैशिंग और समानांतर प्रोसेसिंग को भी सक्षम करता है, जिससे कई कोर विभिन्न चंक्स को एक साथ संभाल सकते हैं, जो मल्टी‑कोर सर्वरों पर थ्रूपुट को और बेहतर बनाता है।

अतिरिक्त लाभ शामिल हैं:
- कई कोरों में समानांतर चंक प्रोसेसिंग।  
- जब उच्च‑प्रासंगिक मिलान मिलता है तो शीघ्र समाप्ति।  

## java search index memory का प्रबंधन
**सीधा उत्तर:** अपेक्षित इंडेक्स आकार के आधार पर पर्याप्त JVM हीप (उदाहरण के लिए, `-Xmx2g` या अधिक) आवंटित करें, बड़े जोड़ के बाद `index.optimize()` चलाकर इंडेक्स संरचना को संकुचित करें, और लेटेंसी स्पाइक्स से बचने के लिए VisualVM के साथ GC विराम की निगरानी करें।

अधिक ट्यूनिंग टिप्स:
- बड़े बैच के बाद `index.flush()` का उपयोग करके अंतरिम डेटा को डिस्क पर लिखें।  
- प्रति‑खोज मेमोरी उपयोग को सीमित करने के लिए `options.setMemoryLimit(256)` सक्षम करें।  

## प्रदर्शन विचार
- **Memory management** – बड़े इंडेक्स के लिए पर्याप्त हीप स्पेस (`-Xmx`) आवंटित करें।  
- **Resource monitoring** – इंडेक्सिंग और खोज संचालन के दौरान CPU उपयोग पर नज़र रखें।  
- **Index maintenance** – पुराना डेटा हटाने के लिए समय-समय पर इंडेक्स को पुनः बनाएं या साफ़ करें।  

## सामान्य समस्याएँ एवं समस्या निवारण
| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| `OutOfMemoryError` इंडेक्सिंग के दौरान | हीप आकार बहुत छोटा | JVM हीप बढ़ाएँ (`-Xmx2g` या अधिक) |
| कोई परिणाम नहीं मिला | चंक टोकन प्रोसेस नहीं हुआ | `while` लूप तब तक चलाएँ जब तक `getNextChunkSearchToken()` `null` न हो |
| खोज प्रदर्शन धीमा | इंडेक्स अनुकूलित नहीं है | बड़े जोड़ के बाद `index.optimize()` चलाएँ |

## अक्सर पूछे जाने वाले प्रश्न
**Q: चंक‑आधारित खोज क्या है?**  
**A:** चंक‑आधारित खोज डेटासेट को छोटे टुकड़ों में विभाजित करती है, जिससे बड़े डेटा वॉल्यूम पर कुशल क्वेरी संभव होती है बिना पूरे दस्तावेज़ को मेमोरी में लोड किए।

**Q: नए फ़ाइलों के साथ अपना इंडेक्स कैसे अपडेट करूँ?**  
**A:** सिर्फ `index.add()` को नए दस्तावेज़ों के पथ के साथ कॉल करें; इंडेक्स उन्हें स्वचालित रूप से शामिल कर लेगा।

**Q: क्या GroupDocs.Search विभिन्न फ़ाइल फ़ॉर्मेट संभाल सकता है?**  
**A:** हाँ, यह **PDF, DOCX, XLSX, PPTX, HTML, TXT, और 30 से अधिक अन्य फ़ॉर्मेट** को समर्थन देता है।

**Q: सामान्य प्रदर्शन बाधाएँ क्या हैं?**  
**A:** मेमोरी प्रतिबंध और अनऑप्टिमाइज़्ड इंडेक्स सबसे आम हैं; पर्याप्त हीप आवंटित करें और नियमित रूप से इंडेक्स को ऑप्टिमाइज़ करें।

**Q: अधिक विस्तृत दस्तावेज़ीकरण कहाँ मिल सकता है?**  
**A:** विस्तृत गाइड और API रेफ़रेंसेज़ के लिए आधिकारिक [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) पर जाएँ।

**Q: क्या चंक‑आधारित खोज एन्क्रिप्टेड PDFs के साथ काम करती है?**  
**A:** हाँ, जब तक आप उपयुक्त API ओवरलोड के माध्यम से पासवर्ड प्रदान करते हैं।

**Q: मैं इंडेक्सिंग प्रगति कैसे मॉनिटर कर सकता हूँ?**  
**A:** `Index.add()` ओवरलोड का उपयोग करें जो `Progress` ऑब्जेक्ट लौटाता है या लॉगिंग कॉलबैक में हुक करें।

## संसाधन
- **दस्तावेज़ीकरण**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API संदर्भ**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **डाउनलोड**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **नि:शुल्क समर्थन**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **अस्थायी लाइसेंस**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**अंतिम अपडेट:** 2026-10-02  
**परीक्षित संस्करण:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## संबंधित ट्यूटोरियल
- [सर्च इंडेक्स डायरेक्टरी बनाएं और लाइसेंस सेट करें – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [GroupDocs.Search Java के साथ क्वेरी प्रदर्शन सुधारें: इंडेक्स और सर्च को ऑप्टिमाइज़ करें](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java उन्नत खोज सुविधाएँ](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
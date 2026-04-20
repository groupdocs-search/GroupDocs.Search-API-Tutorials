---
date: '2026-01-16'
description: GroupDocs.Search for Java का उपयोग करके टेक्स्ट खोज कैसे करें और खोज
  प्रदर्शन को अनुकूलित करें, सीखें। इसमें खोज नेटवर्क सेटअप करने, खोज योग्य इंडेक्स
  बनाने और दस्तावेज़ इंडेक्स को हटाने के चरण शामिल हैं।
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: GroupDocs.Search for Java के साथ टेक्स्ट खोज करें
type: docs
url: /hi/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Perform Text Search with GroupDocs.Search for Java
## Performance Optimization

## How to Implement and Optimize a Search Network with GroupDocs.Search for Java

### Introduction
आज के डेटा‑ड्रिवेन विश्व में, बड़े दस्तावेज़ संग्रहों में **टेक्स्ट सर्च** को तेज़ी से करने की क्षमता एक प्रतिस्पर्धात्मक लाभ है। चाहे आप एक आंतरिक नॉलेज बेस, एक लीगल‑केस रिपॉज़िटरी, या एक ई‑कॉमर्स प्रोडक्ट कैटलॉग बना रहे हों, एक अच्छी तरह ट्यून किया गया सर्च नेटवर्क उपयोगकर्ता संतुष्टि को काफी बढ़ा सकता है। इस गाइड में आप सीखेंगे कि **सर्च नेटवर्क सेट अप** कैसे करें, **सर्चेबल इंडेक्स बनाएं**, **सर्च परफ़ॉर्मेंस ऑप्टिमाइज़** करें, और आवश्यकता पड़ने पर **डॉक्यूमेंट्स इंडेक्स डिलीट** कैसे करें—सब GroupDocs.Search for Java का उपयोग करके।

**What You'll Learn**
- GroupDocs.Search के साथ सर्च नेटवर्क को कॉन्फ़िगर करना  
- नेटवर्क के भीतर नोड्स को डिप्लॉय करना  
- दस्तावेज़ों को प्रभावी रूप से इंडेक्स करना (`index documents java`)  
- नेटवर्क में टेक्स्ट सर्च करना (`perform text search`)  
- इंडेक्स से विशिष्ट दस्तावेज़ हटाना (`delete documents index`)  

आइए देखें कि आप इन फीचर्स का उपयोग करके एक ऑप्टिमाइज़्ड सर्च एक्सपीरियंस कैसे बना सकते हैं।

## Quick Answers
- **GroupDocs.Search for Java का मुख्य उद्देश्य क्या है?** यह कई दस्तावेज़ फ़ॉर्मेट्स में फुल‑टेक्स्ट सर्च प्रदान करता है।  
- **डिस्ट्रिब्यूटेड एनवायरनमेंट में टेक्स्ट सर्च कैसे करें?** एक सर्च नेटवर्क डिप्लॉय करें, मास्टर नोड पर दस्तावेज़ों को इंडेक्स करें, फिर किसी भी नोड से क्वेरी करें।  
- **क्या मैं इंडेक्स को रीबिल्ड किए बिना दस्तावेज़ डिलीट कर सकता हूँ?** हाँ, Delete API का उपयोग करके चयनित फ़ाइलें हटाएँ।  
- **कौन सा Java संस्करण आवश्यक है?** JDK 8 या उससे ऊपर।  
- **प्रोडक्शन के लिए लाइसेंस चाहिए?** एक वैध GroupDocs.Search लाइसेंस आवश्यक है; एक फ्री ट्रायल उपलब्ध है।

## What is “perform text search”?
टेक्स्ट सर्च करने का मतलब है फुल‑टेक्स्ट इंडेक्स को क्वेरी करके उन दस्तावेज़ों को प्राप्त करना जिनमें निर्दिष्ट कीवर्ड या फ़्रेज़ मौजूद हैं। GroupDocs.Search एक इनवर्टेड इंडेक्स बनाता है जो हजारों फ़ाइलों में भी लुक‑अप को अत्यंत तेज़ बनाता है।

## Why set up a search network?
एक सर्च नेटवर्क इंडेक्सिंग और क्वेरी वर्कलोड को कई नोड्स में वितरित करता है, जिससे आप **सर्च परफ़ॉर्मेंस ऑप्टिमाइज़** कर सकते हैं, हॉरिज़ॉन्टली स्केल कर सकते हैं, और हाई अवेलेबिलिटी बनाए रख सकते हैं। यह आर्किटेक्चर एंटरप्राइज़‑लेवल दस्तावेज़ रिपॉज़िटरी के लिए आदर्श है जहाँ लेटेंसी और थ्रूपुट महत्वपूर्ण होते हैं।

### Prerequisites
- **Required Libraries:** GroupDocs.Search for Java version 25.4 (latest).  
- **Environment:** Java JDK 8+, Maven.  
- **Knowledge:** बेसिक Java प्रोग्रामिंग और नेटवर्क कॉन्सेप्ट्स की समझ।

### Setting Up GroupDocs.Search for Java
शुरू करने के लिए, अपने Java प्रोजेक्ट में GroupDocs.Search को नीचे दिए गए सेटअप के साथ इंटीग्रेट करें:

#### Maven Setup
`pom.xml` फ़ाइल में रेपो और डिपेंडेंसी जोड़ें:

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

#### Direct Download
वैकल्पिक रूप से, आप [GroupDocs से सीधे नवीनतम संस्करण डाउनलोड कर सकते हैं](https://releases.groupdocs.com/search/java/)।

#### License Acquisition
GroupDocs एक फ्री ट्रायल प्रदान करता है, जिससे आप खरीदने से पहले फीचर्स का मूल्यांकन कर सकते हैं। आप उनके [purchase पेज](https://purchase.groupdocs.com/temporary-license/) पर दिए गए चरणों का पालन करके एक टेम्पररी लाइसेंस प्राप्त कर सकते हैं। यह आपके टेस्टिंग फेज़ में पूरी फ़ंक्शनैलिटी सक्षम करेगा।

#### Basic Initialization and Setup
अपने Java एप्लिकेशन में GroupDocs.Search को इनिशियलाइज़ करें:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

### Implementation Guide

#### Configuring the Search Network
**Overview:** सर्च नेटवर्क के लिए बेस पाथ और पोर्ट सेट करें, जिससे नोड्स प्रभावी रूप से कम्यूनिकेट कर सकें।

##### Step 1: Define Base Configuration

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath`: नेटवर्क ऑपरेशन्स के लिए डायरेक्टरी पाथ।  
  - `basePort`: सर्च नेटवर्क द्वारा उपयोग किया जाने वाला पोर्ट नंबर।

##### Step 2: Troubleshooting
सुनिश्चित करें कि आपका निर्दिष्ट पोर्ट फ़ायरवॉल सेटिंग्स द्वारा ब्लॉक नहीं है या किसी अन्य एप्लिकेशन द्वारा उपयोग नहीं हो रहा है। टकराव से बचने के लिए आवश्यकतानुसार समायोजित करें।

#### Deploying Search Network Nodes
**Overview:** अपनी कॉन्फ़िगरेशन का उपयोग करके नेटवर्क में नोड्स डिप्लॉय करें, जिससे डिस्ट्रिब्यूटेड इंडेक्सिंग और सर्च संभव हो।

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port:** ये वैल्यूज़ आपके प्रारंभिक कॉन्फ़िगरेशन में उपयोग किए गए मानों से मेल खानी चाहिए ताकि कंसिस्टेंसी बनी रहे।

#### Indexing Documents (`create searchable index`)
**Overview:** मास्टर नोड का उपयोग करके दस्तावेज़ों को सर्च इंडेक्स में प्रभावी रूप से जोड़ें।

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode`: दस्तावेज़ इंडेक्सिंग को मैनेज करने वाला प्राइमरी नोड।  
  - `documentsPath`: दस्तावेज़ों वाले डायरेक्टरी का पाथ।

##### Troubleshooting Tips
सुनिश्चित करें कि आपके दस्तावेज़ पाथ सही और एक्सेसिबल हैं। डायरेक्टरीज़ से पढ़ने की अनुमति भी चेक करें।

#### Searching Text in Network (`perform text search`)
**Overview:** अपने इंडेक्स किए हुए नेटवर्क में व्यापक टेक्स्ट सर्च करें।

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query`: वह टेक्स्ट जिसे आप सर्च कर रहे हैं।  
  - `masterNode`: सर्च करने वाला नोड।

#### Deleting Documents from Index (`delete documents index`)
**Overview:** फ़ाइल पाथ्स के आधार पर इंडेक्स से विशिष्ट दस्तावेज़ हटाएँ।

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Method Purpose:**  
  - `node`: डिलीशन ऑपरेशन के लिए टार्गेट नोड।  
  - `filePaths`: इंडेक्स से हटाए जाने वाले दस्तावेज़ों के पाथ्स।

##### Troubleshooting
फ़ाइल पाथ्स सटीक हों और फ़ाइलें आपके डायरेक्टरी में मौजूद हों, यह सुनिश्चित करें। यदि समस्या बनी रहे तो नेटवर्क परमिशन और कनेक्टिविटी चेक करें।

### Practical Applications
1. **Enterprise Document Management:** आंतरिक नॉलेज रिट्रीवल को सुव्यवस्थित करें।  
2. **Legal Case Analysis:** कई रिपॉज़िटरीज़ में संबंधित केस फ़ाइलें जल्दी खोजें।  
3. **E‑commerce Platforms:** प्रोडक्ट डिस्क्रिप्शन और रिव्यूज़ को इंडेक्स करके सर्च स्पीड बढ़ाएँ।  
4. **Academic Research:** पेपर और थिसिस की बड़ी डिजिटल लाइब्रेरीज़ को प्रभावी रूप से सर्च करें।  
5. **Customer Support Systems:** एजेंट्स को पिछले टिकट्स तुरंत सर्च करने की सुविधा देकर रिस्पॉन्स टाइम घटाएँ।

### Performance Considerations
- **Optimize Indexing Speed:** ऑफ‑पीक घंटों में क्रमिक रूप से नए दस्तावेज़ जोड़ें ताकि लेटेंसी कम रहे।  
- **Resource Usage Guidelines:** नोड्स की संख्या बढ़ाने पर CPU और मेमोरी मॉनिटर करें।  
- **Java Memory Management:** वर्कलोड के आधार पर JVM हीप सेटिंग्स ट्यून करें (उदा., `-Xmx2g` मिडियम‑साइज़ इंडेक्स के लिए)।

### Conclusion
इस गाइड को फॉलो करके आपने **सर्च नेटवर्क सेट अप**, **सर्चेबल इंडेक्स बनाना**, **टेक्स्ट सर्च करना**, और **डॉक्यूमेंट्स इंडेक्स डिलीट** करना सीख लिया है, सभी GroupDocs.Search for Java का उपयोग करके। ये क्षमताएँ डिस्ट्रिब्यूटेड एनवायरनमेंट में तेज़ और भरोसेमंद डॉक्यूमेंट रिट्रीवल को संभव बनाती हैं।

**Next Steps**
- विभिन्न नोड कॉन्फ़िगरेशन के साथ प्रयोग करें ताकि आपके वर्कलोड के लिए इष्टतम बैलेंस मिल सके।  
- कस्टम एनालाइज़र और रिलिवेंस ट्यूनिंग जैसे एडवांस्ड इंडेक्सिंग ऑप्शन्स में गहराई से जाएँ।  
- एंड‑टू‑एंड डॉक्यूमेंट प्रोसेसिंग के लिए अन्य GroupDocs प्रोडक्ट्स के साथ इंटीग्रेशन एक्सप्लोर करें।

## Frequently Asked Questions

**Q: GroupDocs.Search for Java का मुख्य उपयोग केस क्या है?**  
A: यह कई दस्तावेज़ फ़ॉर्मेट्स में फुल‑टेक्स्ट सर्च प्रदान करता है, जिससे आप बड़े रिपॉज़िटरीज़ में **टेक्स्ट सर्च** कर सकते हैं।

**Q: बड़े नेटवर्क में सर्च स्पीड कैसे बढ़ाएँ?**  
A: अतिरिक्त नोड्स डिप्लॉय करें, JVM हीप ट्यून करें, और कम ट्रैफ़िक वाले समय में इंडेक्सिंग शेड्यूल करें ताकि **सर्च परफ़ॉर्मेंस ऑप्टिमाइज़** हो सके।

**Q: क्या पूरी कलेक्शन को री‑इंडेक्स किए बिना एकल दस्तावेज़ डिलीट किया जा सकता है?**  
A: हाँ, कोड उदाहरण में दिखाए गए **delete documents index** API का उपयोग करके विशिष्ट फ़ाइलें हटाएँ।

**Q: डेवलपमेंट के लिए लाइसेंस चाहिए?**  
A: टेस्टिंग के लिए फ्री ट्रायल लाइसेंस पर्याप्त है; प्रोडक्शन डिप्लॉयमेंट के लिए कमर्शियल लाइसेंस आवश्यक है।

**Q: क्या मैं PDFs, Word फ़ाइलें और ईमेल्स को एक साथ इंडेक्स कर सकता हूँ?**  
A: बिलकुल—GroupDocs.Search आउट‑ऑफ़‑द‑बॉक्स कई फ़ॉर्मेट्स को सपोर्ट करता है।

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs
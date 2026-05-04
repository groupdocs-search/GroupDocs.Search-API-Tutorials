---
date: '2026-01-21'
description: GroupDocs Maven निर्भरता को जोड़ना, Java सर्च नेटवर्क को कॉन्फ़िगर और
  सिंक्रनाइज़ करना, तथा GroupDocs.Search के साथ इंडेक्स करने के लिए डायरेक्टरी जोड़ना
  सीखें।
keywords:
- Java Search Network Configuration
- GroupDocs.Search for Java
- Document Indexing and Retrieval
title: GroupDocs Maven निर्भरता – जावा सर्च नेटवर्क सिंक
type: docs
url: /hi/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# GroupDocs Maven Dependency: जावा सर्च नेटवर्क्स को कॉन्फ़िगर करना और सिंक्रनाइज़ करना

इस व्यापक गाइड में कुशलता से सिंक रखनेड़ी इंटीग्रेट करके आप एक शक्तिशाली इंडेक्सिंग इंजन प्राप्त करते हैं जो कई नोड्स में स्केल करता है। यह ट्यूटोरियल आपको डिपेंडेंसी सेट अप करने, नेटवर्क नोड्स डिप्लॉय करने, इंडेक्स में डायरेक्टरी जोड़ने और इष्टतम प्रदर्शन के लिए शार्ड्स को सिंक्रनाइज़ करने की प्रक्रिया दिखाता है।

### Quick Answers
- **GroupDocs Maven Dependency क्या है?** एक Maven आर्टिफैक्ट जो GroupDocs.Search लाइब्रेरी को आपके जावा प्रोजेक्ट में लाता है।  
- **सर्च नेटवर्क क्यों उपयोग करें?** यह इंडेक्सिंग और क्वेरी लोड को कई नोड्स में वितरित करता है, जिससे गति और विश्वसनीयता बढ़ती है।  
- **इंडेक्स में डायरेक्टरी कैसे जोड़ें?** मास्टर नोड उपयोग करें।  
- **शार्ड लाइसेंस चाहिए?** हाँ, प्रोडक्शन उपयोग के लिए ट्रायल या कमर्शियल लाइसेंस आवश्यक है।

## What is the GroupDocs Maven Dependency?

GroupDocs Maven Dependency (`com.groupdocs:groupdocs-search`) वह पैकेज है जिसमें सभी क्लासेज़ शामिल हैं जो सर्चेबल इंडेक्स बनाने, नेटवर्क नोड्स को मैनेज करने और तेज़ क्वेरीज़ करने के लिए आवश्यक हैं। इसे अपने `pom.xml` में जोड़ने से Maven सही बाइनरीज़ और ट्रांज़िटिव डिपेंडेंसीज़ को पुल करता है।

## How to Add the GroupDocs Maven Dependency

### Maven Configuration

अपने `pom.xml` में रिपॉज़िटरी और डिपेंडेंसी जोड़ें:

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

> **Pro tip:** आधिकारिक रिलीज़ पेज पर जाकर संस्करण संख्या को हमेशा अपडेट रखें।

आप आधिकारिक साइट से सीधे JAR भी डाउनलोड कर सकते हैं: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)।

## Prerequisites

- **JDK** (11 या नया) स्थापित हो।  
- IntelliJ IDEA या Eclipse जैसे IDE।  
- बेसिक जावा नॉलेज, Maven की समझ, और नेटवर्क नोड कॉन्सेप्ट्स की जानकारी।  
- वैध GroupDocs.Search लाइसेंस (फ्री ट्रायल या कमर्शियल)।

## Basic Initialization and Setup

इंडेक्स डायरेक्टरी बनाकर शुरू करें:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

यह सरल कदम अगले नेटवर्क कॉन्फ़िगरेशन के लिए वातावरण तैयार करता है।

## Implementation Guide

### Feature 1: Configuration of Search Network

#### Overview

सर्च नेटवर्क को कॉन्फ़िगर करने से फ़ाइल पाथ्स और पोर्ट्स सेट होते हैं जो नोड्स संचार के लिए उपयोग करेंगे।

##### Set Up Paths and Ports
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
`configuration` ऑब्जेक्ट अब आपके सर्च नेटवर्क के सभी आवश्यक सेटिंग्स रखता है।

### Feature 2: Deploying Search Network Nodes

#### Overview

वर्कलोड को अपने नेटवर्क में वितरित करने के लिए नोड्स डिप्लॉय करें। मास्टर नोड ऑपरेशन्स और इवेंट्स को मैनेज करता है।

##### Deployment Code
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Feature 3: Subscribing to Search Network Node Events

#### Overview

इवेंट्स को सुनने से नेटवर्क में बदलाव या अपडेट को डायनामिक रूप से हैंडल किया जा सकता है।

##### Subscription Implementation
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Feature 4: Adding Directories to Index

#### Overview

डायरेक्टरी जोड़ना वह मुख्य कदम है जिससे आपके दस्तावेज़ सर्चेबल बनते हैं।

##### Document Addition
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Feature 5: Synchronizing Shards in Search Network Node

#### Overview

सिंक्रनाइज़ेशन सभी शार्ड्स में डेटा कंसिस्टेंसी सुनिश्चित करता है।

##### Synchronization Code
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Feature 6: Closing Search Network Nodes

#### Overview

नोड्स को सही तरीके से बंद करने से रिसोर्सेज़ रिलीज़ होते हैं और मेमोरी लीक्स रोकते हैं।

##### Node Closure
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Practical Applications

1. **Legal Document Management** – केस फ़ाइल्स और प्रीसिडेंट्स को जल्दी से रिट्रीव करें।  
2. **Financial Record Keeping** – स्टेटमेंट्स और ऑडिट ट्रेल्स को सेकंड्स में एक्सेस करें।  
3. **Academic Research** – हजारों पेपरों में खोज कर प्रासंगिक सिटेशन्स खोजें।

## Performance Considerations

- **Optimize Queries** – रिस्पॉन्स टाइम कम करने के लिए संक्षिप्त क्वेरीज़ लिखें।  
- **Memory Management** – JVM हीप उपयोग मॉनिटर करें; बड़े इंडेक्स के लिए GC ट्यूनिंग पर विचार करें।  
- **Scaling Strategy** –ोड के अनुसार नोड्स को प्रोप to connect | Port conflict | `basePort` को किसी अनयूज़्ड वैल्यू में बदलें |
| Index not updating | Event subscription missing | सुनिश्चित करें कि `SearchNetworkNodeEvents.subscribe(masterNode)` कॉल किया गया है |
| High latency | Insufficient shards | नोड्स की संख्या बढ़ाएँ और डॉक्यूमेंट डिस्ट्रिब्यूशन बैलेंस करें |

## Frequently Asked Questions

**Q: GroupDocs.Search उपयोग करने का मुख्य लाभ क्या है?**  
A: यह बड़े दस्तावेज़ सेट्स में तेज़, स्केलेबल सर्च क्षमताएँ प्रदान करता है, जिसमें न्यूनतम कॉन्फ़िगरेशन की आवश्यकता होती है।

**Q: क्या सर्च नेटवर्क में नोड कॉन्फ़िगरेशन कस्टमाइज़ कर सकते हैं?**  
A: हाँ, आप `Configuration` ऑब्जेक्ट के माध्यम से कस्टम पाथ्स, पोर्ट्स और अन्य विकल्प सेट कर सकते हैं।

**Q: नेटवर्क चल रहा हो तो डायरेक्टरी कैसे जोड़ें?**  
A: जब भी नई फ़ोल्डर इंडेक्स करनी हो, `IndexingDocuments.addDirectories(masterNode, "path")` कॉल करें।

**Q: नया नोड जुड़ने पर शार्ड्स को कैसे सिंक करें?**  
A: ऊपर दिखाए गए `synchronizeShards` मेथड को नए जोड़े गए नोड पर उपयोग करें।

**Q: विकास के लिए लाइसेंस चाहिए?**  
A: टेस्टिंग के लिए फ्री ट्रायल लाइसेंस पर्याप्त है; प्रोडक्शन के लिए कमर्शियल लाइसेंस आवश्यक है।

## Conclusion

इस गाइड को फॉलो करके आप अब **GroupDocs Maven Dependency को जोड़ना**, मल्टी‑नोड सर्च नेटवर्क कॉन्फ़िगर करना, डायरेक्टरीज़ को इंडेक्स करना और शार्ड्स को सिंक्रनाइज़ रखना जानते हैं। ये कदम एक हाई‑परफ़ॉर्मेंस डॉक्यूमेंट सर्च सॉल्यूशन की नींव रखते हैं, जो आपके संगठन की जरूरतों के साथ बढ़ सकता है।

---

**Last Updated:** 2026-01-21  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs
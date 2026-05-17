---
date: '2026-05-17'
description: जानें कि groupdocs Maven dependency कैसे जोड़ें, Java search network
  सेट अप करें, और तेज़, स्केलेबल दस्तावेज़ पुनर्प्राप्ति के लिए इंडेक्स में डायरेक्टरीज़
  कैसे जोड़ें।
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Search Network के लिए GroupDocs Maven Dependency कैसे जोड़ें
type: docs
url: /hi/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# समूहडॉक्स Maven निर्भरता को सर्च नेटवर्क के लिए कैसे जोड़ें

इस व्यापक गाइड में आप **groupdocs Maven निर्भरता को कैसे जोड़ें**, GroupDocs.Search का उपयोग करके एक मजबूत जावा सर्च नेटवर्क को कॉन्फ़िगर करना, और अपने शार्ड्स को सिंक्रनाइज़ रखना सीखेंगे। चाहे आप कानूनी दस्तावेज़, वित्तीय विवरण, या शैक्षणिक पेपर को इंडेक्स कर रहे हों, नीचे दिए गए चरण आपको खोज योग्य इंडेक्स बनाने, क्वेरी लोड को नोड्स में वितरित करने, और न्यूनतम प्रयास से डेटा संगतता बनाए रखने में मदद करेंगे।

## त्वरित उत्तर
- **GroupDocs Maven निर्भरता क्या है?** एक Maven आर्टिफैक्ट जो जावा प्रोजेक्ट्स के लिए GroupDocs.Search लाइब्रेरी को बंडल करता है।  
- **सर्च नेटवर्क का उपयोग क्यों करें?** यह इंडेक्सिंग और क्वेरी लोड को कई नोड्स में वितरित करता है, जिससे गति और विश्वसनीयता में सुधार होता है।  
- **इंडेक्स में डायरेक्टरी कैसे जोड़ें?** मास्टर नोड पर `IndexingDocuments.addDirectories` का उपयोग करें।  
- **शार्ड्स को सिंक कैसे करें?** प्रत्येक नोड के `Indexer` पर `SynchronizeOptions` को कॉल करें।  
- **क्या मुझे लाइसेंस चाहिए?** हाँ, प्रोडक्शन उपयोग के लिए एक ट्रायल या कमर्शियल लाइसेंस आवश्यक है।

## GroupDocs Maven निर्भरता क्या है?

`GroupDocs Maven dependency` एक Maven आर्टिफैक्ट है जो जावा प्रोजेक्ट्स के लिए GroupDocs.Search लाइब्रेरी को बंडल करता है।  
यह खोज योग्य इंडेक्स बनाने, नेटवर्क नोड्स को प्रबंधित करने, और तेज़ क्वेरीज़ निष्पादित करने के लिए सभी आवश्यक क्लासेस प्रदान करता है, और Maven स्वचालित रूप से ट्रांज़िटिव डिपेंडेंसियों को हल करता है, जिससे आपके `pom.xml` में कुछ ही लाइनों से एक तैयार‑से‑उपयोग खोज इंजन मिल जाता है।

## GroupDocs Maven निर्भरता को कैसे जोड़ें

अपने `pom.xml` में रिपॉज़िटरी और निर्भरता प्रविष्टियाँ जोड़ें, फिर `mvn clean install` चलाएँ; Maven `groupdocs-search` JAR और उसकी आवश्यक लाइब्रेरीज़ डाउनलोड करता है, जिससे API आपके प्रोजेक्ट में उपलब्ध हो जाता है। बिल्ड सफल होने के बाद आप तुरंत `com.groupdocs.search` क्लासेज़ का उपयोग शुरू कर सकते हैं।

### Maven कॉन्फ़िगरेशन

अपने `pom.xml` में रिपॉज़िटरी और निर्भरता जोड़ें:

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

> **Pro tip:** आधिकारिक रिलीज़ पेज की जाँच करके संस्करण संख्या को अद्यतन रखें।

आप आधिकारिक साइट से JAR सीधे डाउनलोड भी कर सकते हैं: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## सर्च नेटवर्क का उपयोग क्यों करें?

सर्च नेटवर्क इंडेक्स को शार्ड्स में विभाजित करके अलग-अलग नोड्स पर रखकर क्षैतिज स्केलिंग सक्षम करता है। GroupDocs.Search **50+ इनपुट फॉर्मैट्स** को संभाल सकता है और **सैकड़ों पृष्ठों वाले दस्तावेज़** को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस करता है, जिससे डेटा की मात्रा बढ़ने पर भी सब‑सेकंड क्वेरी प्रतिक्रियाएँ मिलती हैं।

## पूर्वापेक्षाएँ

- **JDK** (11 या नया) स्थापित होना चाहिए।  
- IntelliJ IDEA या Eclipse जैसे IDE।  
- बेसिक जावा ज्ञान, Maven की परिचितता, और नेटवर्क नोड अवधारणाओं की समझ।  
- एक वैध GroupDocs.Search लाइसेंस (फ्री ट्रायल या कमर्शियल)।

## बुनियादी इनिशियलाइज़ेशन और सेटअप

एक इंडेक्स डायरेक्टरी बनाकर शुरू करें:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

यह सरल चरण बाद के नेटवर्क कॉन्फ़िगरेशन के लिए वातावरण तैयार करता है।

## इम्प्लीमेंटेशन गाइड

### फीचर 1: सर्च नेटवर्क की कॉन्फ़िगरेशन

#### अवलोकन

सर्च नेटवर्क को कॉन्फ़िगर करने से फ़ाइल पाथ और पोर्ट सेट होते हैं जो नोड्स संवाद करने के लिए उपयोग करेंगे।

##### पाथ्स और पोर्ट्स सेट करें

Configuration एक क्लास है जो सर्च क्लस्टर के नेटवर्क पाथ्स, पोर्ट्स और अन्य सेटिंग्स को रखती है।  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
`configuration` ऑब्जेक्ट अब आपके सर्च नेटवर्क के सभी आवश्यक सेटिंग्स रखता है।

### फीचर 2: सर्च नेटवर्क नोड्स की डिप्लॉयमेंट

#### अवलोकन

वर्कलोड को अपने नेटवर्क में वितरित करने के लिए नोड्स को डिप्लॉय करें। मास्टर नोड ऑपरेशन्स और इवेंट्स को प्रबंधित करता है।

##### डिप्लॉयमेंट कोड

SearchNetworkNode सर्च नेटवर्क में एक नोड को दर्शाता है जो मास्टर या वर्कर के रूप में कार्य कर सकता है।  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### फीचर 3: सर्च नेटवर्क नोड इवेंट्स की सब्सक्रिप्शन

#### अवलोकन

इवेंट्स को सुनना आपके नेटवर्क में बदलाव या अपडेट को डायनामिक रूप से हैंडल करने की अनुमति देता है।

##### सब्सक्रिप्शन इम्प्लीमेंटेशन

SearchNetworkNodeEvents नोड लाइफ़साइकल और इंडेक्सिंग एक्शन के लिए इवेंट हुक प्रदान करता है।  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### फीचर 4: इंडेक्स में डायरेक्टरी जोड़ना

#### अवलोकन

डायरेक्टरी जोड़ना वह मुख्य कदम है जो आपके दस्तावेज़ों को खोज योग्य बनाता है।

##### दस्तावेज़ जोड़ना

`IndexingDocuments.addDirectories` प्रोसेसिंग के लिए फ़ोल्डर पाथ्स को इंडेक्स में जोड़ता है।  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### फीचर 5: सर्च नेटवर्क नोड में शार्ड्स का सिंक्रनाइज़ेशन

#### अवलोकन

सिंक्रनाइज़ेशन सभी शार्ड्स में डेटा संगति सुनिश्चित करता है।

##### सिंक्रनाइज़ेशन कोड

`SynchronizeOptions` यह कॉन्फ़िगर करता है कि शार्ड्स नोड्स के बीच कैसे सिंक्रनाइज़ किए जाएँ।  
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

### फीचर 6: सर्च नेटवर्क नोड्स को बंद करना

#### अवलोकन

नोड्स को सही ढंग से बंद करने से संसाधन मुक्त होते हैं और मेमोरी लीक से बचाव होता है।

##### नोड क्लोजर

`close()` संसाधनों को मुक्त करता है और सर्च नेटवर्क नोड को शटडाउन करता है।  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## व्यावहारिक अनुप्रयोग

1. **लीगल डॉक्यूमेंट मैनेजमेंट** – केस फ़ाइलें और प्रीसिडेंट्स जल्दी से प्राप्त करें।  
2. **फ़ाइनेंशियल रिकॉर्ड कीपिंग** – सेकंडों में स्टेटमेंट्स और ऑडिट ट्रेल्स तक पहुँचें।  
3. **अकादमिक रिसर्च** – हजारों पेपर में खोज कर प्रासंगिक सिटेशन खोजें।

## प्रदर्शन विचार

- **क्वेरीज़ को ऑप्टिमाइज़ करें** – प्रतिक्रिया समय कम करने के लिए संक्षिप्त क्वेरी लिखें।  
- **मेमोरी मैनेजमेंट** – JVM हीप उपयोग की निगरानी करें; बड़े इंडेक्स के लिए GC ट्यूनिंग पर विचार करें।  
- **स्केलिंग स्ट्रैटेजी** – डेटा वॉल्यूम और क्वेरी लोड के अनुसार नोड्स जोड़ें।

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|-------|----------|
| नोड्स कनेक्ट नहीं हो पा रहे हैं | पोर्ट कॉन्फ्लिक्ट | `basePort` को एक अप्रयुक्त मान में बदलें |
| इंडेक्स अपडेट नहीं हो रहा | इवेंट सब्सक्रिप्शन गायब | `SearchNetworkNodeEvents.subscribe(masterNode)` कॉल किया गया है यह सुनिश्चित करें |
| उच्च लेटेंसी | अपर्याप्त शार्ड्स | नोड्स की संख्या बढ़ाएँ और दस्तावेज़ वितरण को संतुलित करें |

## अक्सर पूछे जाने वाले प्रश्न

**Q:** GroupDocs.Search का उपयोग करने का मुख्य लाभ क्या है?  
**A:** यह बड़े दस्तावेज़ सेटों में तेज़, स्केलेबल सर्च क्षमताएँ न्यूनतम कॉन्फ़िगरेशन के साथ प्रदान करता है।

**Q:** क्या मैं सर्च नेटवर्क में नोड कॉन्फ़िगरेशन को कस्टमाइज़ कर सकता हूँ?  
**A:** हाँ, आप `Configuration` ऑब्जेक्ट के माध्यम से कस्टम पाथ्स, पोर्ट्स, और अन्य विकल्प सेट कर सकते हैं।

**Q:** नेटवर्क चलने के बाद मैं इंडेक्स में डायरेक्टरी कैसे जोड़ूँ?  
**A:** जब भी आपको नई फ़ोल्डर इंडेक्स करने की आवश्यकता हो, `IndexingDocuments.addDirectories(masterNode, "path")` कॉल करें।

**Q:** जब नया नोड नेटवर्क में जुड़ता है तो शार्ड्स को कैसे सिंक करें?  
**A:** ऊपर दिखाए गए `synchronizeShards` मेथड को नए जोड़े गए नोड पर उपयोग करें।

**Q:** विकास के लिए मुझे लाइसेंस चाहिए?  
**A:** परीक्षण के लिए एक फ्री ट्रायल लाइसेंस पर्याप्त है; प्रोडक्शन के लिए एक कमर्शियल लाइसेंस आवश्यक है।

## निष्कर्ष

इस गाइड का पालन करके अब आप जानते हैं कि **groupdocs Maven निर्भरता को कैसे जोड़ें**, मल्टी‑नोड सर्च नेटवर्क को कॉन्फ़िगर करें, डायरेक्टरी को इंडेक्स करें, और शार्ड्स को सिंक्रनाइज़ रखें। ये चरण एक हाई‑परफ़ॉर्मेंस डॉक्यूमेंट सर्च सॉल्यूशन की नींव रखते हैं जो आपके संगठन की जरूरतों के साथ बढ़ सकता है।

---

**अंतिम अपडेट:** 2026-05-17  
**परीक्षित संस्करण:** GroupDocs.Search 25.4  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल्स

- [GroupDocs.Search for Java के ट्यूटोरियल्स और उदाहरण](/search/net/)
- [GroupDocs.Search नेटवर्क को .NET में कॉन्फ़िगर करना: एक व्यापक गाइड](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [डॉक्यूमेंट मैनेजमेंट सिस्टम्स के लिए .NET में GroupDocs.Search के साथ सर्च नेटवर्क कैसे लागू करें](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
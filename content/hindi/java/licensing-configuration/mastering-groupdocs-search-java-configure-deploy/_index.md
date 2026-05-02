---
date: '2026-05-02'
description: GroupDocs.Search for Java का उपयोग करके खोज को कॉन्फ़िगर करना और वास्तविक‑समय
  खोज अपडेट सक्षम करना सीखें। नेटवर्क सेटअप, नोड डिप्लॉयमेंट और इंडेक्सिंग पर चरण‑दर‑चरण
  गाइड।
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: Java में GroupDocs.Search के साथ खोज को कैसे कॉन्फ़िगर करें - कॉन्फ़िगरेशन
  और डिप्लॉयमेंट गाइड
type: docs
url: /hi/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# GroupDocs.Search के साथ Java में खोज को कॉन्फ़िगर कैसे करें

आज के तेज़ गति वाले डिजिटल संसार में, **how to configure search** को कुशलतापूर्वक कॉन्फ़िगर करना प्रोजेक्ट की सफलता को बना या बिगाड़ सकता है। चाहे आप हजारों अनुबंधों, शोध पत्रों, या आंतरिक रिपोर्टों को संभाल रहे हों, एक अच्छी तरह से डिज़ाइन किया गया सर्च नेटवर्क आपको सेकंडों में सही दस्तावेज़ खोजने में मदद करता है। यह ट्यूटोरियल आपको सर्च नेटवर्क को कॉन्फ़िगर करने, नोड्स को डिप्लॉय करने, और GroupDocs.Search for Java के साथ **real time search updates** सक्षम करने के चरण दिखाता है।

## त्वरित उत्तर
- **search network का मुख्य उद्देश्य क्या है?** स्केलेबिलिटी और गति के लिए कई नोड्स में इंडेक्सिंग और क्वेरी प्रोसेसिंग को वितरित करना।  
- **कौन सा लाइब्रेरी संस्करण आवश्यक है?** GroupDocs.Search for Java v25.4 या नया।  
- **क्या मुझे लाइसेंस की आवश्यकता है?** मूल्यांकन के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **real time updates कैसे संभाले जाते हैं?** इंडेक्सिंग परिवर्तन पर फायर होने वाले नोड इवेंट्स को सब्सक्राइब करके।  
- **क्या मैं नई दस्तावेज़ फ़ोल्डर तुरंत जोड़ सकता हूँ?** हाँ—इंडेक्सर की `addDirectories` मेथड का उपयोग करें।

## GroupDocs संदर्भ में “how to configure search” क्या है?
खोज को कॉन्फ़िगर करना मतलब एक **search network** सेट अप करना है जो जानता है कि आपके दस्तावेज़ कहाँ हैं, नोड्स कैसे संचार करते हैं, और इंडेक्सिंग कैसे समन्वित होती है। एक बार नेटवर्क कॉन्फ़िगर हो जाने पर, आप नोड्स को बिना डाउनटाइम के जोड़ या हटा सकते हैं, जिससे निरंतर अद्यतन खोज परिणामों तक पहुँच सुनिश्चित होती है।

## GroupDocs.Search for Java का उपयोग क्यों करें?
- **Scalability:** कई मशीनों में कार्यभार वितरित करें।  
- **Real‑time updates:** नेटवर्क में नई इंडेक्स की गई फ़ाइलों को तुरंत प्रतिबिंबित करें।  
- **Ease of integration:** सरल Maven सेटअप और स्पष्ट Java APIs।  
- **Enterprise‑ready:** बड़े कॉर्पोरा और जटिल क्वेरी परिदृश्यों को संभालता है।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK) 8+** स्थापित है।  
- **Maven** निर्भरता प्रबंधन के लिए।  
- Java, Maven, और खोज अवधारणाओं की बुनियादी परिचितता।

## GroupDocs.Search for Java सेट अप करना

### Maven निर्भरता
`pom.xml` में रिपॉज़िटरी और निर्भरता जोड़ें:

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

**Direct Download:** आप लाइब्रेरी को यहाँ से भी प्राप्त कर सकते हैं: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### लाइसेंस प्राप्ति
- **Free Trial:** सभी फीचर्स को एक्सप्लोर करने के लिए ट्रायल लाइसेंस प्राप्त करें।  
- **Temporary License:** विस्तारित मूल्यांकन अवधि के लिए अनुरोध करें।  
- **Commercial License:** उत्पादन डिप्लॉयमेंट के लिए आवश्यक।

### बेसिक इनिशियलाइज़ेशन
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Java में search network को कॉन्फ़िगर कैसे करें

### चरण 1: आवश्यक पैकेज इम्पोर्ट करें
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### चरण 2: नेटवर्क कॉन्फ़िगर करें
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameters:** `basePath` आपके दस्तावेज़ फ़ोल्डर की ओर इशारा करता है; `basePort` नोड संचार के लिए उपयोग किया जाने वाला TCP पोर्ट है।

## सर्च नेटवर्क नोड्स को डिप्लॉय करना

### चरण 1: डिप्लॉयमेंट पैकेज इम्पोर्ट करें
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### चरण 2: नोड्स डिप्लॉय करें
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Node:** सभी नोड्स में खोज और इंडेक्सिंग का समन्वय करता है। आप शार्ड आवंटन और हेल्थ चेक जैसे सेटिंग्स को **configure master node** कर सकते हैं।

## रियल‑टाइम सर्च अपडेट्स के लिए नोड इवेंट्स को सब्सक्राइब करना

### चरण 1: इवेंट पैकेज इम्पोर्ट करें
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### चरण 2: मास्टर नोड इवेंट्स को सब्सक्राइब करें
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Event Handling:** जब भी दस्तावेज़ जोड़े, अपडेट या हटाए जाएँ, **real time search updates** सक्षम करता है।

## इंडेक्सिंग के लिए डायरेक्टरीज़ जोड़ना

### चरण 1: इंडेक्सर पैकेज इम्पोर्ट करें
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### चरण 2: दस्तावेज़ डायरेक्टरीज़ जोड़ें
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dynamic Indexing:** नेटवर्क को रीस्टार्ट किए बिना फ़्लाई पर **add directories to index** करने के लिए `addDirectories` मेथड का उपयोग करें।

## इंडेक्स किए गए दस्तावेज़ प्राप्त करना

### चरण 1: सर्चर पैकेज इम्पोर्ट करें
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### चरण 2: दस्तावेज़ जानकारी प्राप्त करें
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Shard Management:** दस्तावेज़ों को शार्ड्स में वितरित करके बड़े डेटासेट को कुशलतापूर्वक संभालता है। **optimize shard size** करने के लिए, शार्ड आँकड़े मॉनिटर करें और भविष्य के रिलीज़ में `shardSize` कॉन्फ़िगरेशन को समायोजित करें।

## आपके प्रोजेक्ट के लिए यह क्यों महत्वपूर्ण है
एक सही तरीके से कॉन्फ़िगर किया गया सर्च नेटवर्क बॉटलनेक्स को समाप्त करता है, लेटेंसी को कम करता है, और सुनिश्चित करता है कि उपयोगकर्ता हमेशा दस्तावेज़ का नवीनतम संस्करण देखें। रियल‑टाइम अपडेट्स और **add directories to index** करने की क्षमता बिना डाउनटाइम के विशेष रूप से कानूनी फर्मों, शोध संस्थानों, और उन सभी संगठनों के लिए मूल्यवान है जो लगातार बदलते दस्तावेज़ संग्रहों से निपटते हैं।

## व्यावहारिक अनुप्रयोग
1. **Enterprise Document Management:** लाखों फ़ाइलों में खोज को केंद्रीकृत करें।  
2. **Legal Firms:** केस फ़ाइलें, अनुबंध, और साक्ष्य जल्दी खोजें।  
3. **Academic Research:** जर्नल और पेपर को इंडेक्स करके तुरंत प्राप्त करें।

## प्रदर्शन संबंधी विचार
- **Optimize Indexing:** नियमित रूप से इंडेक्स रीफ़्रेश शेड्यूल करें और पुराना डेटा हटाएँ।  
- **Memory Management:** JVM हीप मॉनिटर करें, विशेषकर बड़े शार्ड्स को संभालते समय।  
- **Scalability Planning:** जैसे-जैसे आपका कॉर्पस बढ़े, नोड्स जोड़ें; नेटवर्क स्वचालित रूप से लोड संतुलित करता है।  
- **Optimize shard size:** छोटे शार्ड्स क्वेरी लेटेंसी को सुधारते हैं, जबकि बड़े शार्ड्स ओवरहेड को कम करते हैं। अपने हार्डवेयर और क्वेरी पैटर्न के आधार पर ट्यून करें।

## सामान्य समस्याएँ और समाधान
| समस्या | कारण | समाधान |
|-------|-------|-----|
| नोड्स कनेक्ट नहीं हो पा रहे हैं | पोर्ट कॉन्फ्लिक्ट या फ़ायरवॉल | `basePort` खुला हो और अन्य सेवाओं द्वारा उपयोग न किया गया हो, यह सुनिश्चित करें |
| इंडेक्स अपडेट नहीं हो रहा | इवेंट सब्सक्रिप्शन गायब | डिप्लॉयमेंट के बाद `SearchNetworkNodeEvents.subscribe(masterNode)` कॉल करें |
| आउट‑ऑफ़‑मेमोरी त्रुटियाँ | बहुत अधिक बड़े शार्ड्स लोड हुए | शार्ड आकार घटाएँ या JVM हीप बढ़ाएँ (`-Xmx` फ़्लैग) |

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं नेटवर्क चलने के बाद नई डायरेक्टरीज़ जोड़ सकता हूँ?**  
A: हाँ—`indexer.addDirectories()` मेथड का उपयोग करें; सब्सक्राइब किए गए इवेंट्स रियल‑टाइम में अपडेट्स को प्रसारित करेंगे।

**Q: मैं नोड हेल्थ कैसे मॉनिटर करूँ?**  
A: प्रत्येक `SearchNetworkNode` स्टेटस APIs प्रदान करता है; इसे अपनी पसंद के मॉनिटरिंग टूल के साथ इंटीग्रेट करें।

**Q: क्या मास्टर नोड को अलग मशीन पर चलाना संभव है?**  
A: बिल्कुल। बस यह सुनिश्चित करें कि सभी नोड्स समान `basePort` साझा करें और नेटवर्क पर एक-दूसरे तक पहुँच सकें।

**Q: कौन से फ़ाइल फ़ॉर्मेट समर्थित हैं?**  
A: GroupDocs.Search PDFs, Word, Excel, PowerPoint, plain text, और कई अन्य फ़ॉर्मेट्स को बॉक्स से ही सपोर्ट करता है।

**Q: क्या नया नोड जोड़ने के बाद नेटवर्क को रीस्टार्ट करना पड़ेगा?**  
A: नहीं—नोड्स को डायनामिक रूप से जोड़ा या हटाया जा सकता है; मास्टर नोड स्वचालित रूप से शार्ड्स को रीबैलेंस करेगा।

## निष्कर्ष
अब जब आप GroupDocs.Search for Java का उपयोग करके **how to configure search** जानते हैं, तो आप तेज़, स्केलेबल, और विश्वसनीय दस्तावेज़ खोज समाधान बना सकते हैं जो आपके संगठन की वृद्धि के साथ तालमेल रखते हैं। इन पैटर्न को लागू करके किसी भी उद्योग के लिए रियल‑टाइम, वितरित सर्च अनुभव बना सकते हैं।

---

**अंतिम अपडेट:** 2026-05-02  
**परीक्षित संस्करण:** GroupDocs.Search for Java 25.4  
**लेखक:** GroupDocs
---
date: '2026-01-16'
description: जावा में ग्रुपडॉक्स सर्च नेटवर्क को कॉन्फ़िगर करना सीखें और बेहतर खोज
  दक्षता के लिए इंडेक्स में समानार्थक शब्द जोड़ें।
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Java में GroupDocs.Search नेटवर्क को कॉन्फ़िगर करें – सर्च को बूस्ट करें
type: docs
url: /hi/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# जावा में GroupDocs.Search नेटवर्क को कॉन्फ़िगर करें – सर्च को बूस्ट करें

आज के डेटा‑ड्रिवन एप्लिकेशनों में, **configure groupdocs search network** तेज़ और सटीक परिणाम बड़े दस्तावेज़ संग्रहों में प्रदान करने का मुख्य कदम है। चाहे आप एंटरप्राइज़‑वाइड सर्च पोर्टल बना रहे हों या मौजूदा समाधान को विस्तारित कर रहे हों, एक अच्छी तरह से कॉन्फ़िगर किया गया GroupDocs.Search नेटवर्क आपको क्षैतिज रूप से स्केल करने, समानार्थी शब्द समर्थन जोड़ने, और लेटेंसी कम रखने की अनुमति देता है। इस ट्यूटोरियल में आप जावा का उपयोग करके GroupDocs.Search नेटवर्क को सेट अप, डिप्लॉय और फाइन‑ट्यून करना सीखेंगे, साथ ही इंडेक्स में समानार्थी शब्द जोड़ने और नोड लाइफ़साइकल प्रबंधन के व्यावहारिक टिप्स भी प्राप्त करेंगे।

## त्वरित उत्तर

- **GroupDocs.Search नेटवर्क को कॉन्फ़िगर करने का मुख्य लाभ क्या है?** यह वितरित इंडेक्सिंग और क्वेरींग को सक्षम करता है, जिससे प्रदर्शन और स्केलेबिलिटी में सुधार होता है।  
- **उदाहरण चलाने के लिए मुझे लाइसेंस चाहिए?** डेवलपमेंट के लिए फ्री ट्रायल काम करता है; प्रोडक्शन के लिए कमर्शियल लाइसेंस आवश्यक है।  
- **क्या इंडेक्स को रीबिल्ड किए बिना समानार्थी शब्द जोड़े जा सकते हैं?** हाँ—रनटाइम पर सिंनोनिम डिक्शनरी का उपयोग करके **add synonyms to index**।  
- **मैं कितने नोड्स डिप्लॉय कर सकता हूँ?** आप अपनी इन्फ्रास्ट्रक्चर की अनुमति के अनुसार जितने चाहें नोड्स डिप्लॉय कर सकते हैं; प्रत्येक नोड अपना पोर्ट उपयोग करता है।  

## GroupDocs.Search नेटवर्क को कॉन्फ़िगर करना क्या है?

GroupDocs.Search नेटवर्क को कॉन्फ़िगर करना मतलब फ़ोल्डर संरचना, पोर्ट्स, और नोड सेटिंग्स को परिभाषित करना है जिससे कई JVM इंस्टेंस इंडेक्सिंग और सर्चिंग में सहयोग कर सकें। यह सेटअप एक मास्टर‑नोड बनाता है जो वर्कर्स (शार्ड्स) को समन्वयित करता है और सुनिश्चित करता है कि क्वेरीज़ पूरे डेटासेट पर निष्पादित हों।

## GroupDocs.Search नेटवर्क को कॉन्फ़िगर क्यों करें?

- **Scalability** – इंडेक्सिंग लोड को कई मशीनों में वितरित करें।  
- **Reliability** – नोड्स को बिना डाउntime के जोड़ा या हटाया जा सकता है।  
- **Search relevance** – बेहतर परिणामों के लिए इंडेक्स में समानार्थी शब्द जोड़ें।  
- **Performance** – समानांतर क्वेरी निष्पादन से प्रतिक्रिया समय घटता है।  

## पूर्वापेक्षाएँ

- Java Development Kit (JDK) 8 या उससे नया  
- प्रोजेक्ट बनाने के लिए Maven  
- Java सिंटैक्स की बुनियादी जानकारी  
- GroupDocs.Search for Java लाइब्रेरी तक पहुंच (Maven या आधिकारिक रिलीज़ पेज से डाउनलोड किया गया)  

## जावा के लिए GroupDocs.Search सेट अप करना

अपने Maven **pom.xml** में रिपॉज़िटरी और डिपेंडेंसी जोड़ें:

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

वैकल्पिक रूप से, नवीनतम संस्करण सीधे [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

### लाइसेंस प्राप्ति
- **Free Trial** – बिना लागत के कोर फीचर्स का अन्वेषण करें।  
- **Temporary License** – अल्पकालिक परीक्षण के लिए पूरी क्षमताओं को अनलॉक करें।  
- **Commercial License** – प्रोडक्शन डिप्लॉयमेंट के लिए आवश्यक है।  

### बेसिक इनिशियलाइज़ेशन और सेटअप
लाइब्रेरी सही ढंग से लोड होती है यह सत्यापित करने के लिए एक सरल जावा क्लास बनाएं:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## GroupDocs.Search नेटवर्क को कॉन्फ़िगर करने के लिए चरण‑दर‑चरण गाइड

### 1. सर्च नेटवर्क को कॉन्फ़िगर करना
नोड संचार के लिए बेस डॉक्यूमेंट फ़ोल्डर और प्रारंभिक पोर्ट को परिभाषित करें।

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – जहाँ डिक्शनरी (जैसे, synonym फ़ाइलें) स्थित हैं।  
- **basePort** – पहला पोर्ट; बाद के नोड्स इस मान से बढ़ते हैं।  

### 2. सर्च नेटवर्क नोड्स को डिप्लॉय करना
एक ही कॉन्फ़िगरेशन को साझा करने वाले कई वर्कर नोड्स को स्पिन अप करें।

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

प्रत्येक नोड अपना पोर्ट (basePort + index) पर चलता है और समग्र इंडेक्स का एक शार्ड रखता है।

### 3. नोड इवेंट्स की सदस्यता लेना
मास्टर नोड पर इवेंट लिस्नर जोड़कर स्वास्थ्य, इंडेक्सिंग प्रगति, और त्रुटि स्थितियों की निगरानी करें।

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

इवेंट कॉलबैक्स आपको नोड शुरू/बंद, इंडेक्सिंग पूर्णता, और अप्रत्याशित विफलताओं पर प्रतिक्रिया देने की अनुमति देते हैं।

### 4. नोड के इंडेक्सर में समानार्थी शब्द जोड़ना  
रनटाइम पर **add synonyms to index** करके प्रासंगिकता बढ़ाएँ।

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – शब्दों का एरे जो समान माना जाना चाहिए।  
- **clearBeforeAdding** – यदि आप मौजूदा एंट्रीज़ को बदलना चाहते हैं तो इसे `true` सेट करें।  

### 5. इंडेक्सिंग के लिए डायरेक्टरी जोड़ना
मास्टर नोड को बताएं कि कौन से फ़ोल्डर में वे दस्तावेज़ हैं जिन्हें आप सर्चेबल बनाना चाहते हैं।

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

यह मेथड डायरेक्टरी को रीकर्सिवली स्कैन करता है और फ़ को शार्ड्स में वितरित करता है।

### 6. नेटवर्क में टेक्स्ट सर्च करना
सभी नोड्स पर एक क्वेरी निष्पादित करें, वैकल्पिक रूप से एक्सैक्ट‑मैच व्यवहार को मजबूर करें।

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

जब आपको स्टेमिंग के बिना सख्त टर्म मिलान चाहिए तो `exactMatchOnly` को `true` पर सेट करें।

### 7. नेटवर्क नोड्स को बंद करना
प्रोसेसिंग पूर्ण होने पर संसाधनों को सुगमता से रिलीज़ करें।

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

सही शटडाउन मेमोरी लीक को रोकता है और JVM को स्वस्थ रखता है।

## व्यावहारिक अनुप्रयोग

| Scenario | How the network helps |
|----------|----------------|
| **एंटरप्राइज़ सर्च** | डेटा‑सेंटर सर्वरों में इंडेक्सिंग वितरित करें ताकि पेटाबाइट‑स्केल कॉर्पोरा को संभाला जा सके। |
| **दस्तावेज़ प्रबंधन** | इंडेक्स में समानार्थी शब्द जोड़ें ताकि उपयोगकर्ता विभिन्न शब्दावली के बावजूद दस्तावेज़ खोज सकें। |
| **ई‑कॉमर्स कैटलॉग** | क्षेत्र‑विशिष्ट नोड्स को डिप्लॉय करें ताकि स्थानीयकृत प्रोडक्ट सर्च तेज़ी से सर्व किया जा सके। |
| **सामग्री प्रबंधन** | संपादक जब विशिष्ट डायरेक्टरी में नई फ़ाइलें जोड़ते हैं, तब भी सामग्री को सर्चेबल रखें। |

## सामान्य समस्याएँ और समाधान

- **Port Conflicts** – सुनिश्चित करें कि प्रत्येक नोड का पोर्ट (basePort + index) मुक्त है; आवश्यकता पड़ने पर `basePort` को समायोजित करें।  
- **Synonym Not Applied** – शब्द जोड़ने के बाद आपने `indexer.setDictionary(dictionary)` कॉल किया है यह जांचें।  
- **Node Not Responding** – इवेंट्स की सदस्यता लें; नेटवर्क समस्याओं का निदान करने के लिए `NodeFailed` कॉलबैक्स देखें।  
- **Memory Leak on Close** – प्रत्येक डिप्लॉय किए गए नोड के लिए हमेशा `node.close()` को कॉल करें।  

## अक्सर पूछे जाने वाले प्रश्न

**Q: कई नोड्स को डिप्लॉय करने से सर्च प्रदर्शन कैसे सुधरता है?**  
A: प्रत्येक नोड डेटा का एक शार्ड इंडेक्स करता है, जिससे समानांतर प्रोसेसिंग संभव होती है और कार्यभार साझा होने से क्वेरी लेटेंसी घटती है।

**Q: क्या मैं मौजूदा दस्तावेज़ों को पुनः‑इंडेक्स किए बिना समानार्थी शब्द जोड़ सकता हूँ?**  
A: हाँ, आप रनटाइम पर सिंनोनिम डिक्शनरी के माध्यम से **add synonyms to index** कर सकते हैं; परिवर्तन तुरंत नए क्वेरीज़ के लिए प्रभावी हो जाते हैं।

**Q: नोड इवेंट्स की सदस्यता लेना अनिवार्य है?**  
A: बेसिक ऑपरेशन के लिए आवश्यक नहीं है, लेकिन इवेंट सब्सक्रिप्शन आपको नोड स्वास्थ्य की दृश्यता देता है और विफलताओं पर तुरंत प्रतिक्रिया करने में मदद करता है।

**Q: नोड संसाधनों के प्रबंधन के लिए सर्वोत्तम प्रथाएँ क्या हैं?**  
A: नियमित रूप से निष्क्रिय नोड्स को बंद करें, JVM मेमोरी उपयोग की निगरानी करें, और ऑफ‑पीक घंटों में नोड्स को रीसायकल करें ताकि संसाधन खपत अनुकूल रहे।

**Q: क्या GroupDocs.Search PDFs या इमेजेज़ जैसे नॉन‑टेक्स्ट फॉर्मैट्स को सपोर्ट करता है?**  
A: बिल्कुल। लाइब्रेरी PDFs, Office फ़ाइलों से टेक्स्ट निकालती है, और इमेजेज़ पर OCR भी करती है, जिससे वे बॉक्स से बाहर सर्चेबल बन जाते हैं।

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
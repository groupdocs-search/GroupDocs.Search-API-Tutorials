---
date: '2026-03-01'
description: GroupDocs.Search for Java की उन्नत इंडेक्सिंग सुविधाओं का उपयोग करके
  खोज प्रदर्शन को अनुकूलित करना और खोज लेटेंसी को सुधारना सीखें, जिसमें रद्दीकरण,
  असिंक्रोनस ऑपरेशन्स, मल्टी‑थ्रेडिंग और मेटाडेटा कस्टमाइज़ेशन शामिल हैं।
keywords:
- GroupDocs.Search Java
- advanced indexing features
- asynchronous operations
title: GroupDocs.Search for Java में उन्नत अनुक्रमण तकनीकों के साथ खोज प्रदर्शन को
  अनुकूलित करें
type: docs
url: /hi/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# GroupDocs.Search for Java में उन्नत इंडेक्सिंग तकनीकों के साथ खोज प्रदर्शन को अनुकूलित करें

आज के तेज़ गति वाले डिजिटल माहौल में, **search performance को अनुकूलित करना** उपयोगकर्ताओं को तुरंत परिणाम देने के लिए आवश्यक है। चाहे आप एक कस्टम सर्च इंजन बना रहे हों या मौजूदा दस्तावेज़ प्रबंधन प्रणाली को बेहतर बना रहे हों, सही इंडेक्सिंग रणनीति लेटेंसी को काफी कम कर सकती है, संसाधन उपयोग को घटा सकती है, और **search latency को सुधारना**। इस ट्यूटोरियल में हम GroupDocs.Search for Java की सबसे शक्तिशाली सुविधाओं—cancellation, asynchronous indexing, multi‑threading, और metadata customization—पर चर्चा करेंगे, ताकि आप **दस्तावेज़ इंडेक्स जोड़ें** को तेज़ और अधिक कुशलता से कर सकें।

**आप क्या सीखेंगे**

- निर्दिष्ट समय के बाद इंडेक्सिंग ऑपरेशन को कैसे रद्द करें  
- असिंक्रोनस इंडेक्सिंग ऑपरेशन्स को निष्पादित करना और स्थिति परिवर्तन को संभालना  
- तेज़ इंडेक्सिंग के लिए मल्टी‑थ्रेडिंग को कॉन्फ़िगर करना  
- मेटाडेटा इंडेक्सिंग विकल्पों को कस्टमाइज़ करना  

आइए कोड में डुबकी लगाने से पहले सुनिश्चित करें कि आपके पास सभी आवश्यक चीज़ें हैं।

## आवश्यकताएँ

- **GroupDocs.Search Library** – संस्करण 25.4 या बाद का।  
- **Java Development Environment** – JDK 8 या उससे ऊपर की सिफ़ारिश की जाती है।  
- Java और इंडेक्सिंग की अवधारणा की बुनियादी परिचितता।

### GroupDocs.Search for Java को सेट अप करना

#### Maven इंस्टॉलेशन

`pom.xml` फ़ाइल में रिपॉजिटरी और डिपेंडेंसी जोड़ें:

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

#### डायरेक्ट डाउनलोड

वैकल्पिक रूप से, नवीनतम JAR को [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

**License Acquisition** – मुफ्त ट्रायल से शुरू करें या पूर्ण फीचर सेट को अनलॉक करने के लिए एक टेम्पररी लाइसेंस का अनुरोध करें।

### बेसिक इनिशियलाइज़ेशन और सेटअप

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## त्वरित उत्तर
- **रद्दीकरण क्या करता है?** सेट समय के बाद इंडेक्सिंग को रोकता है ताकि संसाधन मुक्त हो सकें।  
- **क्या मैं दस्तावेज़ों को असिंक्रोनस रूप से इंडेक्स कर सकता हूँ?** हाँ – `options.setAsync(true)` सेट करें।  
- **मैं कितनी थ्रेड्स का उपयोग कर सकता हूँ?** कोई भी सकारात्मक पूर्णांक; अधिकांश सर्वरों के लिए सामान्य मान 2‑4 हैं।  
- **क्या मेटाडेटा इंडेक्सिंग वैकल्पिक है?** बिल्कुल – आप इसे प्रत्येक फ़ील्ड के अनुसार सक्षम या फाइन‑ट्यून कर सकते हैं।  
- **क्या इन सुविधाओं के लिए लाइसेंस चाहिए?** परीक्षण के लिए ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।

## इस संदर्भ में “search performance को अनुकूलित करना” क्या है?

search performance को अनुकूलित करना का मतलब है इंडेक्सिंग प्रक्रिया को इस तरह कॉन्फ़िगर करना कि वह सही मात्रा में CPU, मेमोरी और समय का उपयोग करे जबकि तुरंत सबसे प्रासंगिक परिणाम प्रदान करे। रद्दीकरण, async निष्पादन, थ्रेडिंग, और मेटाडेटा हैंडलिंग को नियंत्रित करके आप सीधे यह प्रभावित करते हैं कि इंजन **दस्तावेज़ इंडेक्स जोड़ें** को कितनी तेज़ी से कर सकता है और क्वेरीज़ का उत्तर दे सकता है।

## उन्नत इंडेक्सिंग सुविधाओं का उपयोग क्यों करें?

- **कम हुई लेटेंसी** – असिंक्रोनस और मल्टी‑थ्रेडेड इंडेक्सिंग आपके एप्लिकेशन को प्रतिक्रियाशील रखती है।  
- **बेहतर संसाधन प्रबंधन** – रद्दीकरण अनियंत्रित प्रक्रियाओं को रोकता है।  
- **कस्टम खोज प्रासंगिकता** – मेटाडेटा विकल्प आपको सबसे महत्वपूर्ण जानकारी को उजागर करने देते हैं।  

## उन्नत इंडेक्सिंग के साथ search latency को कैसे सुधारें?

जब आपको **search latency को सुधारना** हो, तो उन सुविधाओं को मिलाकर देखें जिनका हम यहाँ अन्वेषण करेंगे: लंबे‑चलने वाले जॉब्स को रद्द करें, बैकग्राउंड में इंडेक्सिंग चलाएँ, और कार्य को कई CPU कोरों में वितरित करें। यह बहु‑आधारित दृष्टिकोण अक्सर सबसे बड़े गति लाभ देता है।

## इम्प्लीमेंटेशन गाइड

### रद्दीकरण प्रॉपर्टी

**Overview** – निर्दिष्ट अवधि के बाद इंडेक्सिंग को रद्द करके संसाधनों की अधिक खपत से बचें।

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Create Indexing Options with Cancellation

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Key Points**

- `setCancellation()` फ़ीचर को सक्रिय करता है।  
- `cancelAfter(int milliseconds)` टाइमआउट निर्धारित करता है (इस उदाहरण में 3 सेकंड)।

### असिंक्रोनस प्रॉपर्टी

**Overview** – बैकग्राउंड थ्रेड पर इंडेक्सिंग चलाएँ और स्थिति परिवर्तन को सुनें।

#### Step 1: Set Up the Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Subscribe to Status Changed Event

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Step 3: Configure Asynchronous Options

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### थ्रेड्स प्रॉपर्टी

**Overview** – कई CPU कोरों का उपयोग करके इंडेक्सिंग को तेज़ करें।

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Multi‑threading

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### मेटाडेटा इंडेक्सिंग विकल्प प्रॉपर्टी

**Overview** – यह तय करें कि कौन सा दस्तावेज़ मेटाडेटा इंडेक्स किया जाए और वह कैसे संग्रहीत हो।

#### Step 1: Set Up Environment

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Step 2: Configure Metadata Options

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## व्यावहारिक अनुप्रयोग

1. **Document Management Systems** – असिंक्रोनस इंडेक्सिंग का उपयोग करें ताकि बैकग्राउंड में बड़े बैच प्रोसेस होते समय UI प्रतिक्रियाशील रहे।  
2. **Content Search Engines** – पिक ट्रैफ़िक के दौरान लंबे समय तक चलने वाले जॉब्स को सर्वर संसाधनों को हॉग करने से रोकने के लिए रद्दीकरण लागू करें।  
3. **Large‑Scale Ingestion Pipelines** – स्केल पर **add documents index** करने के लिए मल्टी‑थ्रेडिंग का उपयोग करें, जिससे प्रोसेसिंग समय काफी घटे।  

## प्रदर्शन विचार

- **Thread Management** – CPU उपयोग की निगरानी करें; बहुत अधिक थ्रेड्स से कॉन्टेक्स्ट‑स्विच ओवरहेड हो सकता है।  
- **Memory Footprint** – मेटाडेटा लिमिट्स (जैसे `setMaxBytesToIndexField`) मेमोरी उपयोग को पूर्वानुमेय रखने में मदद करती हैं।  
- **Garbage Collection** – बड़े कॉर्पोरा को इंडेक्स करते समय उपयुक्त JVM फ़्लैग्स (`-Xmx`, `-XX:+UseG1GC`) का उपयोग करें।  

## सामान्य समस्याएँ और समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| इंडेक्सिंग कभी समाप्त नहीं होती | रद्दीकरण बहुत कम सेट किया गया | `cancelAfter` मान बढ़ाएँ या लंबे जॉब्स के लिए रद्दीकरण हटाएँ |
| असिंक्रोनस मोड में कोई स्थिति अपडेट नहीं | इवेंट हैंडलर सही ढंग से संलग्न नहीं है | सुनिश्चित करें कि `index.getEvents().StatusChanged.add(...)` को `index.add` से पहले कॉल किया गया है |
| आउट‑ऑफ़‑मेमोरी त्रुटियाँ | बहुत अधिक थ्रेड्स या उच्च मेटाडेटा लिमिट्स | `options.setThreads` को कम करें और मेटाडेटा फ़ील्ड लिमिट्स घटाएँ |
| परिणामों में मेटाडेटा गायब | मेटाडेटा इंडेक्सिंग अक्षम | सुनिश्चित करें कि `options.getMetadataIndexingOptions()` कॉन्फ़िगर किया गया है और फ़ील्ड्स को इग्नोर करने के लिए सेट नहीं है |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न:** मैं GroupDocs.Search के लिए टेम्पररी लाइसेंस कैसे प्राप्त करूँ?  
**उत्तर:** [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) पर जाएँ।

**प्रश्न:** क्या मैं इंडेक्सिंग ऑपरेशन को बीच में रद्द कर सकता हूँ?  
**उत्तर:** हाँ – `cancelAfter()` के साथ रद्दीकरण प्रॉपर्टी का उपयोग करें या प्रोग्रामेटिक रूप से `Cancellation.cancel()` कॉल करें।

**प्रश्न:** असिंक्रोनस इंडेक्सिंग के कुछ उपयोग केस क्या हैं?  
**उत्तर:** रियल‑टाइम दस्तावेज़ पुनःप्राप्ति, बैकग्राउंड बैच प्रोसेसिंग, और UI‑प्रतिक्रियाशील एप्लिकेशन असिंक्रोनस इंडेक्सिंग से लाभान्वित होते हैं।

**प्रश्न:** साझा सर्वर पर थ्रेड काउंट बढ़ाना सुरक्षित है?  
**उत्तर:** धीरे‑धीरे बढ़ाएँ और CPU लोड की निगरानी करें; अत्यधिक साझा वातावरण में थ्रेड काउंट को मध्यम रखें (2‑4)।

**प्रश्न:** मेटाडेटा इंडेक्सिंग खोज प्रासंगिकता को कैसे प्रभावित करती है?  
**उत्तर:** सही तरीके से इंडेक्स किया गया मेटाडेटा (लेखक, निर्माण तिथि, टैग) क्वेरी में अधिक वज़न पा सकता है, जिससे परिणाम की सटीकता बढ़ती है।

## निष्कर्ष

इन उन्नत GroupDocs.Search for Java सुविधाओं को अपनाकर आप विभिन्न परिदृश्यों में **search performance को अनुकूलित** कर सकते हैं—तेज़ दस्तावेज़ इनजेशन से लेकर फाइन‑ग्रेन मेटाडेटा नियंत्रण तक। विभिन्न कॉन्फ़िगरेशन के साथ प्रयोग करें, संसाधन उपयोग की निगरानी करें, और अपने वर्कलोड के अनुसार सेटिंग्स को अनुकूलित करें ताकि सर्वोत्तम परिणाम प्राप्त हों।

---

**अंतिम अपडेट:** 2026-03-01  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
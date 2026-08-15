---
date: '2026-08-15'
description: GroupDocs.Search for Java की advanced indexing सुविधाओं का उपयोग करके
  search latency को कैसे सुधारें, सीखें, जिसमें cancellation, async operations, multithreading,
  और metadata customization शामिल हैं।
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: GroupDocs.Search for Java का उपयोग करके cancellation, asynchronous
  indexing, multithreading, और metadata customization के माध्यम से search latency
  में सुधार करें। प्रदर्शन को बढ़ाएँ और संसाधन उपयोग को कम करें।
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: GroupDocs में advanced indexing के साथ search latency में सुधार करें
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: GroupDocs में advanced indexing के साथ search latency में सुधार करें
type: docs
url: /hi/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# उन्नत अनुक्रमण के साथ GroupDocs में खोज विलंबता में सुधार करें

आज के तेज़ गति वाले डिजिटल माहौल में, **search latency में सुधार** उपयोगकर्ताओं को तुरंत परिणाम प्रदान करने के लिए आवश्यक है। चाहे आप एक कस्टम सर्च इंजन बना रहे हों या मौजूदा दस्तावेज़ प्रबंधन प्रणाली को बेहतर बना रहे हों, सही अनुक्रमण रणनीति विलंबता को काफी हद तक घटा सकती है, संसाधन खपत को कम कर सकती है, और **search latency में सुधार** पूरे सिस्टम में कर सकती है। इस ट्यूटोरियल में हम GroupDocs.Search for Java की सबसे शक्तिशाली सुविधाओं—रद्दीकरण, असिंक्रोनस अनुक्रमण, मल्टीथ्रेडिंग, और मेटाडेटा कस्टमाइज़ेशन—पर चर्चा करेंगे, ताकि आप **दस्तावेज़ों को index में जोड़ें** तेज़ और अधिक कुशल बना सकें।

**आप क्या सीखेंगे**

- एक निर्दिष्ट समय के बाद अनुक्रमण ऑपरेशन को रद्द करने का तरीका  
- असिंक्रोनस अनुक्रमण ऑपरेशन्स करना और स्थिति परिवर्तन को संभालना  
- तेज़ अनुक्रमण के लिए मल्टीथ्रेडिंग को कॉन्फ़िगर करना  
- metadata अनुक्रमण विकल्पों को कस्टमाइज़ करना ताकि **search metadata को कस्टमाइज़ करें**  

कोड में डुबकी लगाने से पहले सुनिश्चित करें कि आपके पास सभी आवश्यक चीज़ें हैं।

## त्वरित उत्तर
- **रद्दीकरण क्या करता है?** यह सेट टाइमआउट के बाद अनुक्रमण को रोक देता है, जिससे CPU और मेमोरी अन्य कार्यों के लिए मुक्त हो जाती है।  
- **क्या मैं दस्तावेज़ों को असिंक्रोनस रूप से अनुक्रमित कर सकता हूँ?** हाँ – इसे `options.setAsync(true)` से सक्षम करें।  
- **मैं कितनी थ्रेड्स का उपयोग कर सकता हूँ?** कोई भी सकारात्मक पूर्णांक; अधिकांश सर्वरों के लिए 2‑4 थ्रेड्स सामान्य हैं।  
- **क्या metadata अनुक्रमण वैकल्पिक है?** बिल्कुल – आप इसे प्रत्येक फ़ील्ड के अनुसार सक्षम या फाइन‑ट्यून कर सकते हैं।  
- **क्या इन सुविधाओं के लिए लाइसेंस आवश्यक है?** परीक्षण के लिए ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।

## पूर्वापेक्षाएँ

- **GroupDocs.Search लाइब्रेरी** – संस्करण 25.4 या बाद का।  
- **Java विकास वातावरण** – JDK 8 या उससे ऊपर की सिफ़ारिश की जाती है।  
- Java और अनुक्रमण की अवधारणा की बुनियादी परिचितता।

### GroupDocs.Search for Java सेटअप करना

#### Maven इंस्टॉलेशन

`pom.xml` फ़ाइल में रिपॉज़िटरी और डिपेंडेंसी जोड़ें:

`pom.xml` कॉन्फ़िगरेशन Maven को बताता है कि कौन से GroupDocs.Search आर्टिफैक्ट डाउनलोड करके आपके प्रोजेक्ट में शामिल करने हैं।

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

#### प्रत्यक्ष डाउनलोड

वैकल्पिक रूप से, नवीनतम JAR को [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

**लाइसेंस प्राप्ति** – पूर्ण फीचर सेट अनलॉक करने के लिए मुफ्त ट्रायल से शुरू करें या अस्थायी लाइसेंस का अनुरोध करें।

### बुनियादी इनिशियलाइज़ेशन और सेटअप

`SearchIndex` क्लास वह एंट्री पॉइंट है जो डिस्क या मेमोरी में संग्रहीत खोज योग्य अनुक्रमण को दर्शाता है।

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

## इस संदर्भ में “search प्रदर्शन को अनुकूलित करना” क्या है?

search प्रदर्शन को अनुकूलित करने का मतलब है अनुक्रमण प्रक्रिया को इस तरह कॉन्फ़िगर करना कि वह सही मात्रा में CPU, मेमोरी और समय का उपयोग करे, जबकि तुरंत सबसे प्रासंगिक परिणाम प्रदान करे। रद्दीकरण, असिंक्रोनस निष्पादन, थ्रेडिंग, और metadata हैंडलिंग को नियंत्रित करके, आप सीधे यह प्रभावित करते हैं कि इंजन कितनी जल्दी **दस्तावेज़ों को index में जोड़ सके** और क्वेरीज़ का जवाब दे सके।

## उन्नत अनुक्रमण सुविधाओं का उपयोग क्यों करें?

असिंक्रोनस और मल्टीथ्रेडेड अनुक्रमण आपके एप्लिकेशन को प्रतिक्रियाशील रखता है, जबकि रद्दीकरण अनियंत्रित प्रक्रियाओं को रोकता है। फाइन‑ट्यून्ड metadata विकल्प आपको सबसे महत्वपूर्ण जानकारी को उजागर करने देते हैं, जो सीधे अंत उपयोगकर्ताओं के लिए **search latency में सुधार** करता है। अतिरिक्त रूप से, ये सुविधाएँ CPU स्पाइक्स को कम करती हैं, मेमोरी दबाव घटाती हैं, और बड़े दस्तावेज़ वॉल्यूम को संभालते समय सुगम स्केलिंग को सक्षम करती हैं।

## उन्नत अनुक्रमण के साथ search latency कैसे सुधारें?

`SearchIndex` इंस्टेंस लोड करें, `IndexingOptions` को रद्दीकरण, असिंक्रोनस, और थ्रेड सेटिंग्स के साथ कॉन्फ़िगर करें, फिर `index.add(document)` कॉल करें — यह संयोजन सामान्य वर्कलोड पर कुल अनुक्रमण समय को 60 % तक कम करता है और सुनिश्चित करता है कि लंबी चलने वाली जॉब्स अन्य ऑपरेशन्स को ब्लॉक न करें। आप metadata अनुक्रमण सीमाओं को भी समायोजित कर सकते हैं और स्टेटस‑चेंज्ड इवेंट्स के माध्यम से प्रगति की निगरानी कर सकते हैं ताकि पाइपलाइन प्रदर्शन बजट के भीतर रहे।

## कार्यान्वयन गाइड

### रद्दीकरण प्रॉपर्टी

**अवलोकन** – संसाधनों के अधिक उपयोग से बचने के लिए निर्दिष्ट अवधि के बाद अनुक्रमण रद्द करें।

#### चरण 1: पर्यावरण सेट अप करें

`SearchIndex` इंस्टेंस बनाएं जो आपके index फ़ोल्डर की ओर इशारा करता हो।

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### चरण 2: रद्दीकरण के साथ अनुक्रमण विकल्प बनाएं

`IndexingOptions` आपको अनुक्रमण इंजन के व्यवहार को निर्दिष्ट करने की अनुमति देता है।

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

**Key points**

- `setCancellation()` फीचर को सक्रिय करता है।  
- `cancelAfter(int milliseconds)` टाइमआउट निर्धारित करता है (इस उदाहरण में 3 सेकंड)।  

### असिंक्रोनस प्रॉपर्टी

**अवलोकन** – बैकग्राउंड थ्रेड पर अनुक्रमण चलाएँ और स्थिति परिवर्तन को सुनें।

#### चरण 1: पर्यावरण सेट अप करें

इंडेक्स को इंस्टैंशिएट करें और दस्तावेज़ संग्रह तैयार करें।

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### चरण 2: status‑changed इवेंट को सब्सक्राइब करें

`StatusChanged` इवेंट आपको सूचित करता है जब अनुक्रमण जॉब स्थितियों के बीच बदलता है।

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

#### चरण 3: असिंक्रोनस विकल्प कॉन्फ़िगर करें

async मोड सक्षम करें ताकि कॉल तुरंत रिटर्न हो और प्रोसेसिंग बैकग्राउंड में जारी रहे।

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### थ्रेड्स प्रॉपर्टी

**अवलोकन** – कई CPU कोर का उपयोग करके अनुक्रमण को तेज़ करें।

#### चरण 1: पर्यावरण सेट अप करें

इंडेक्स तैयार करें और सुनिश्चित करें कि JVM में पर्याप्त हीप मेमोरी हो।

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### चरण 2: मल्टीथ्रेडिंग कॉन्फ़िगर करें

वर्कर थ्रेड्स की संख्या सेट करें; प्रत्येक थ्रेड दस्तावेज़ों के एक उपसमुच्चय को प्रोसेस करता है।

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Metadata अनुक्रमण विकल्प प्रॉपर्टी

**अवलोकन** – यह फाइन‑ट्यून करें कि कौन सा दस्तावेज़ metadata अनुक्रमित होता है और कैसे संग्रहीत किया जाता है।

#### चरण 1: पर्यावरण सेट अप करें

ऐसे दस्तावेज़ को लोड करें जिसमें author, title, और कस्टम टैग जैसे metadata फ़ील्ड हों।

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### चरण 2: metadata विकल्प कॉन्फ़िगर करें

`MetadataIndexingOptions` आपको व्यक्तिगत metadata फ़ील्ड को सक्षम या अक्षम करने और आकार सीमाएँ निर्धारित करने की अनुमति देता है।

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

1. **डॉक्यूमेंट मैनेजमेंट सिस्टम** – असिंक्रोनस अनुक्रमण का उपयोग करें ताकि बड़े बैच बैकग्राउंड में प्रोसेस होते समय UI प्रतिक्रियाशील बना रहे।  
2. **कंटेंट सर्च इंजन** – रद्दीकरण लागू करें ताकि पीक ट्रैफ़िक के दौरान लंबी चलने वाली जॉब्स सर्वर संसाधनों को हॉग न करें।  
3. **विस्तृत स्केल इन्जेशन पाइपलाइन** – स्केल पर **दस्तावेज़ों को index में जोड़ने** के लिए मल्टीथ्रेडिंग का उपयोग करें, जिससे प्रोसेसिंग समय में नाटकीय कमी आए।  

## प्रदर्शन विचार

- **थ्रेड प्रबंधन** – CPU उपयोग की निगरानी करें; बहुत अधिक थ्रेड्स कंटेक्स्ट‑स्विच ओवरहेड का कारण बन सकते हैं।  
- **मेमोरी फुटप्रिंट** – Metadata सीमाएँ (जैसे `setMaxBytesToIndexField`) मेमोरी उपयोग को पूर्वानुमानित रखती हैं।  
- **गार्बेज कलेक्शन** – बड़े कॉर्पोरा को अनुक्रमित करते समय उपयुक्त JVM फ़्लैग्स (`-Xmx`, `-XX:+UseG1GC`) का उपयोग करें।  

## सामान्य समस्याएँ और समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| अनुक्रमण कभी समाप्त नहीं होता | रद्दीकरण बहुत कम सेट किया गया | `cancelAfter` मान बढ़ाएँ या लंबी जॉब्स के लिए रद्दीकरण हटाएँ |
| असिंक्रोनस मोड में कोई स्थिति अपडेट नहीं | इवेंट हैंडलर सही तरीके से संलग्न नहीं है | `index.getEvents().StatusChanged.add(...)` को `index.add` से पहले कॉल किया गया है, यह सुनिश्चित करें |
| आउट‑ऑफ़‑मेमारी त्रुटियाँ | बहुत अधिक थ्रेड्स या उच्च metadata सीमाएँ | `options.setThreads` को कम करें और metadata फ़ील्ड सीमाओं को घटाएँ |
| परिणामों में metadata गायब | metadata अनुक्रमण अक्षम है | `options.getMetadataIndexingOptions()` कॉन्फ़िगर है और फ़ील्ड्स को इग्नोर करने के लिए सेट नहीं है, यह सत्यापित करें |

## अक्सर पूछे जाने वाले प्रश्न

**प्र: मैं GroupDocs.Search के लिए अस्थायी लाइसेंस कैसे प्राप्त करूँ?**  
उ: [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) पर जाएँ और स्क्रीन पर दिए गए निर्देशों का पालन करें।

**प्र: क्या मैं अनुक्रमण ऑपरेशन को बीच में रद्द कर सकता हूँ?**  
उ: हाँ – `cancelAfter()` के साथ रद्दीकरण प्रॉपर्टी का उपयोग करें या प्रोग्रामेटिक रूप से `Cancellation.cancel()` को कॉल करें।

**प्र: असिंक्रोनस अनुक्रमण के कुछ उपयोग केस क्या हैं?**  
उ: रीयल‑टाइम दस्तावेज़ पुनर्प्राप्ति, बैकग्राउंड बैच प्रोसेसिंग, और UI‑प्रतिक्रियाशील एप्लिकेशन असिंक्रोनस अनुक्रमण से लाभान्वित होते हैं।

**प्र: साझा सर्वर पर थ्रेड काउंट बढ़ाना सुरक्षित है?**  
उ: धीरे‑धीरे बढ़ाएँ और CPU लोड की निगरानी करें; अत्यधिक साझा वातावरण में थ्रेड काउंट को मध्यम रखें (2‑4)।

**प्र: metadata अनुक्रमण search प्रासंगिकता को कैसे प्रभावित करता है?**  
उ: सही तरीके से अनुक्रमित metadata (author, creation date, tags) को क्वेरी में अधिक वेट दिया जा सकता है, जिससे परिणाम की सटीकता बढ़ती है।

## निष्कर्ष

GroupDocs.Search for Java की इन उन्नत सुविधाओं को अपनाकर, आप विभिन्न परिदृश्यों में **search latency में सुधार** करेंगे—तेज़ दस्तावेज़ इन्जेशन से लेकर फाइन‑ग्रेन्ड metadata नियंत्रण तक। विभिन्न कॉन्फ़िगरेशन के साथ प्रयोग करें, संसाधन उपयोग की निगरानी करें, और अपने विशिष्ट वर्कलोड के अनुसार सेटिंग्स को अनुकूलित करें ताकि सर्वोत्तम परिणाम मिलें।

---

**अंतिम अपडेट:** 2026-08-15  
**परीक्षण किया गया:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [GroupDocs.Search Java के साथ क्वेरी प्रदर्शन सुधारें: इंडेक्स और सर्च को अनुकूलित करें](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs.Search का उपयोग करके Java में Metadata Indexing के साथ दस्तावेज़ों को index में कैसे जोड़ें](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [GroupDocs.Search for Java में कई एलियास जोड़ना और दस्तावेज़ों को index में कैसे जोड़ें](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
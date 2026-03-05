---
date: '2026-02-16'
description: GroupDocs.Search के साथ जावा में बूलियन ऑपरेटर्स का उपयोग करके सर्च इंडेक्स
  बनाना, जावा में कंटेंट सर्च और फ़ैसिटेड क्वेरीज़ करना सीखें, जिससे प्रदर्शन और उपयोगकर्ता
  अनुभव में सुधार हो।
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: बूलियन ऑपरेटर्स जावा – सर्च इंडेक्स बनाएं और फ़ैसिटेड खोज
type: docs
url: /hi/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean Operators Java – सर्च इंडेक्स बनाएं & फ़ेसटेड सर्च

Java में एक शक्तिशाली **search experience** लागू करना भारी लग सकता है, विशेषकर जब आपको **create a search index Java** बनाना पड़े जो **boolean operators Java** को फ़ेसटेड और जटिल क्वेरीज़ के लिए सपोर्ट करता हो। इस ट्यूटोरियल में हम **GroupDocs.Search for Java** सेट अप करना, एक इंडेक्स बनाना, दस्तावेज़ जोड़ना, और सरल फ़ेसटेड सर्च तथा जटिल मल्टी‑क्राइटेरिया क्वेरीज़ जो Boolean लॉजिक का उपयोग करती हैं, को कवर करेंगे। अंत तक आप **content search Java**, **filename search Java**, और **update index java** ऑपरेशन्स को समझेंगे जिससे आपका डेटा हमेशा ताज़ा रहे।

## Quick Answers
- **What is a faceted search?** पूर्वनिर्धारित श्रेणियों जैसे फ़ाइल प्रकार या तिथि द्वारा परिणाम फ़िल्टर करने का तरीका।  
- **How do I create a search index Java?** एक `Index` ऑब्जेक्ट को फ़ोल्डर की ओर इशारा करके इनिशियलाइज़ करें और दस्तावेज़ जोड़ें।  
- **Can I combine multiple criteria with boolean operators?** हाँ—ऑब्जेक्ट‑बेस्ड क्वेरीज़ या टेक्स्ट क्वेरी में Boolean ऑपरेटर्स का उपयोग करें।  
- **Do I need a license?** विकास के लिए फ्री ट्रायल काम करता है; एक कमर्शियल लाइसेंस सीमाओं को हटाता है।  
- **Which IDE works best?** कोई भी Java IDE (IntelliJ IDEA, Eclipse, NetBeans) ठीक रहेगा।

## What is “create search index java”?
Java में सर्च इंडेक्स बनाना मतलब एक सर्चेबल डेटा स्ट्रक्चर तैयार करना है जो दस्तावेज़ मेटाडेटा और कंटेंट को स्टोर करता है, जिससे उपयोगकर्ता क्वेरीज़ के आधार पर तेज़ रिट्रीवल संभव हो। GroupDocs.Search के साथ, इंडेक्स डिस्क पर रहता है, इसे क्रमिक रूप से अपडेट किया जा सकता है, और यह फ़ेसटिंग, **boolean operators Java**, और जटिल Boolean लॉजिक जैसी उन्नत सुविधाओं को सपोर्ट करता है।

## Why use GroupDocs.Search for faceted and complex queries?
- **Out‑of‑the‑box faceting** – फ़ाइल नाम, आकार, या कस्टम मेटाडेटा जैसे फ़ील्ड द्वारा फ़िल्टर करें।  
- **Rich query language** – टेक्स्ट, फ़्रेज़, और फ़ील्ड क्वेरीज़ को AND/OR/NOT ऑपरेटर्स के साथ मिलाएँ (यह **boolean operators java** का मूल है)।  
- **Scalable performance** – लाखों दस्तावेज़ों को इंडेक्स करें और लेटेंसी कम रखें।  
- **Pure Java** – कोई नेटिव डिपेंडेंसी नहीं, JDK 8+ चलाने वाले किसी भी प्लेटफ़ॉर्म पर काम करता है।  
- **Easy index maintenance** – फ़ाइलें जोड़ने या हटाने के बाद `index.update()` कॉल करके **update index java** करें।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

- **JDK 8 or newer** इंस्टॉल और आपके IDE में कॉन्फ़िगर किया हुआ।  
- **Maven** (या Gradle) डिपेंडेंसी मैनेजमेंट के लिए।  
- **GroupDocs.Search for Java** ≥ 25.4।  
- Java OOP कॉन्सेप्ट्स और Maven प्रोजेक्ट स्ट्रक्चर की बेसिक समझ।

## Setting Up GroupDocs.Search for Java

### Maven Setup
`pom.xml` फ़ाइल में रिपॉज़िटरी और डिपेंडेंसी जोड़ें:

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

### Direct Download
वैकल्पिक रूप से, आधिकारिक रिलीज़ पेज से नवीनतम JAR डाउनलोड करें:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### License Acquisition
पूरा फ़ंक्शनैलिटी अनलॉक करने के लिए:

1. **Free trial** – विकास और टेस्टिंग के लिए परफेक्ट।  
2. **Temporary evaluation license** – ट्रायल लिमिट्स को बढ़ाता है।  
3. **Commercial license** – प्रोडक्शन उपयोग के लिए सभी प्रतिबंध हटाता है।

### Basic Initialization and Setup
नीचे दिया गया स्निपेट दिखाता है कि **create a search index Java** कैसे बनाते हैं `Index` क्लास को इंस्टैंशिएट करके:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

इंडेक्स तैयार होने के बाद, हम वास्तविक‑दुनिया की फ़ेसटेड और जटिल क्वेरीज़ की ओर बढ़ सकते हैं।

## How to use boolean operators java – Simple Faceted Search

फ़ेसटेड सर्च उपयोगकर्ताओं को पूर्वनिर्धारित श्रेणियों (फ़ेसेट) से मान चुनकर परिणाम संकीर्ण करने देता है। नीचे स्टेप‑बाय‑स्टेप प्रक्रिया दी गई है।

### Step 1: Create an Index
पहले, `Index` को उस फ़ोल्डर की ओर पॉइंट करें जहाँ इंडेक्स फ़ाइलें स्टोर होंगी।

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Step 2: Add Documents to the Index
GroupDocs.Search को बताएं कि आपके स्रोत दस्तावेज़ कहाँ स्थित हैं। सभी सपोर्टेड फ़ाइल प्रकार (PDF, DOCX, TXT, आदि) स्वचालित रूप से इंडेक्स हो जाएंगे।

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Step 3: Perform a Search in the Content Field with a Text Query
एक तेज़ टेक्स्ट क्वेरी `content` फ़ील्ड द्वारा फ़िल्टर करती है। सिंटैक्स `content: Pellentesque` परिणामों को उन दस्तावेज़ों तक सीमित करता है जिनके बॉडी टेक्स्ट में *Pellentesque* शब्द मौजूद है।

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Step 4: Perform a Search Using an Object Query
ऑब्जेक्ट‑बेस्ड क्वेरीज़ आपको फाइन‑ग्रेन कंट्रोल देती हैं। यहाँ हम एक वर्ड क्वेरी बनाते हैं, उसे फ़ील्ड क्वेरी में रैप करते हैं, और उसे एक्सीक्यूट करते हैं।

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## How to use boolean operators java – Complex Query Search

जटिल क्वेरीज़ कई फ़ील्ड, Boolean ऑपरेटर्स, और फ़्रेज़ सर्च को मिलाती हैं। यह e‑commerce फ़िल्टर या लीगल डॉक्यूमेंट रिसर्च जैसे परिदृश्यों के लिए आदर्श है।

### Step 1: Create an Index for Complex Queries
एक ही फ़ोल्डर स्ट्रक्चर को पुनः उपयोग करें; आप इंडेक्स को सरल और जटिल दोनों परिदृश्यों में शेयर कर सकते हैं।

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Step 2: Perform a Search with a Text Query
नीचे दिया गया क्वेरी फ़ाइलों को *lorem* **and** *ipsum* **or** कंटेंट में दो सटीक फ़्रेज़ में से किसी एक को खोजता है।

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Step 3: Perform a Search with an Object Query
ऑब्जेक्ट‑बेस्ड निर्माण टेक्स्ट क्वेरी को प्रतिबिंबित करता है लेकिन टाइप सेफ़्टी और IDE असिस्टेंस देता है।

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Practical Applications of Faceted & Complex Searches

| Scenario | How Faceting Helps | Example Query |
|----------|-------------------|---------------|
| **E‑commerce catalog** | श्रेणी, कीमत, ब्रांड द्वारा फ़िल्टर करें | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | केस नंबर, जुरिस्डिक्शन द्वारा संकीर्ण करें | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | लेखक, प्रकाशन वर्ष, कीवर्ड को मिलाएँ | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | फ़ाइल प्रकार और विभाग द्वारा खोजें | `filetype: pdf AND department: HR` |

इन उदाहरणों से स्पष्ट होता है कि **boolean operators java** और **filename search java** तकनीकों में महारत हासिल करना किसी भी डेटा‑इंटेंसिव एप्लिकेशन के लिए गेम‑चेंजर क्यों है।

## Common Pitfalls & Troubleshooting

- **Empty results** – सुनिश्चित करें कि दस्तावेज़ सफलतापूर्वक जोड़े गए हैं (`index.getDocumentCount()` मदद कर सकता है)।  
- **Stale index** – फ़ाइलें जोड़ने या हटाने के बाद `index.update()` कॉल करके **update index java** करें और इंडेक्स को सिंक रखें।  
- **Incorrect field names** – टाइपो से बचने के लिए `CommonFieldNames` कॉन्स्टैंट्स (`Content`, `FileName`, आदि) का उपयोग करें।  
- **Performance bottlenecks** – बड़े कलेक्शन के लिए `index.setCacheSize()` सक्षम करें या इंडेक्स फ़ोल्डर के लिए समर्पित SSD उपयोग करें।  
- **Missing highlights** – **highlight search results java** करने के लिए `SearchResult.getFragments()` के माध्यम से मैच्ड फ्रैगमेंट्स प्राप्त करें (यहाँ नहीं दिखाया गया लेकिन API में उपलब्ध है)।  

## Frequently Asked Questions

**Q: क्या मैं GroupDocs.Search को Spring Boot के साथ उपयोग कर सकता हूँ?**  
A: बिल्कुल। Maven डिपेंडेंसी जोड़ें, इंडेक्स को Spring bean के रूप में कॉन्फ़िगर करें, और जहाँ भी सर्च क्षमता चाहिए वहाँ इन्जेक्ट करें।

**Q: क्या लाइब्रेरी कस्टम मेटाडेटा फ़ील्ड्स को सपोर्ट करती है?**  
A: हाँ – आप इंडेक्सिंग के दौरान यूज़र‑डिफाइंड फ़ील्ड्स जोड़ सकते हैं और उन पर फ़ेसट कर सकते हैं।

**Q: इंडेक्स कितना बड़ा हो सकता है?**  
A: इंडेक्स डिस्क‑बेस्ड है और लाखों दस्तावेज़ संभाल सकता है; बस पर्याप्त स्टोरेज रखें और कैश सेटिंग्स मॉनिटर करें।

**Q: क्या परिणामों को रिलिवेंस के आधार पर रैंक किया जा सकता है?**  
A: GroupDocs.Search स्वचालित रूप से मैचेस को स्कोर करता है; आप स्कोर `SearchResult.getDocument(i).getScore()` से प्राप्त कर सकते हैं।

**Q: यदि मैं एन्क्रिप्टेड PDFs को इंडेक्स करता हूँ तो क्या होगा?**  
A: दस्तावेज़ जोड़ते समय पासवर्ड प्रदान करें: `index.add(filePath, password)`।

## Conclusion

अब आप **create a search index Java** को GroupDocs.Search के साथ सहजता से बना सकते हैं, दस्तावेज़ जोड़ सकते हैं, और सरल फ़ेसटेड क्वेरीज़ तथा **boolean operators java** का उपयोग करके जटिल Boolean सर्च तैयार कर सकते हैं। ये क्षमताएँ आपको e‑commerce प्लेटफ़ॉर्म से लेकर एंटरप्राइज़ नॉलेज बेस तक विभिन्न अनुप्रयोगों में तेज़, सटीक, और उपयोगकर्ता‑मित्र सर्च एक्सपीरियंस प्रदान करने में सक्षम बनाती हैं।

अगला कदम उठाने के लिए तैयार हैं? **GroupDocs.Search** की उन्नत सुविधाओं जैसे **highlighting**, **suggestions**, और **real‑time indexing** का अन्वेषण करें ताकि आपके एप्लिकेशन की सर्च पावर और भी बढ़े।

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
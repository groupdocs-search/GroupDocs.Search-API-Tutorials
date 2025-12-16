---
date: '2025-12-16'
description: GroupDocs.Search का उपयोग करके जावा में सर्च इंडेक्स बनाना और फेशेटेड
  तथा जटिल खोजों को लागू करना सीखें, जिससे खोज प्रदर्शन और उपयोगकर्ता अनुभव में सुधार
  हो।
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: सर्च इंडेक्स जावा बनाएं – फ़ैसिटेड और जटिल खोजें
type: docs
url: /hi/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# खोज इंडेक्स जावा बनाएं – फेस्डेड और जटिल खोजें

जावा में एक शक्तिशाली **search experience** लागू करना भारी लग सकता है, विशेष रूप से जब आपको बड़े दस्तावेज़ संग्रह को संभालने वाले **create search index Java** प्रोजेक्ट्स बनाने की आवश्यकता हो। सौभाग्य से, **GroupDocs.Search for Java** एक समृद्ध API प्रदान करता है जो आपको कुछ ही कोड लाइनों के साथ फेस्डेड और जटिल क्वेरीज़ बनाने देता है। इस ट्यूटोरियल में आप लाइब्रेरी सेटअप करना, **create a search index Java** बनाना, दस्तावेज़ जोड़ना, और सरल फेस्डेड खोजों तथा परिष्कृत मल्टी‑क्राइटेरिया क्वेरीज़ चलाना सीखेंगे।

## त्वरित उत्तर
- **What is a faceted search?** पूर्वनिर्धारित श्रेणियों (जैसे, फ़ाइल प्रकार, तिथि) द्वारा परिणामों को फ़िल्टर करने का तरीका।  
- **How do I create a search index Java?** एक फ़ोल्डर की ओर इशारा करने वाले `Index` ऑब्जेक्ट को इनिशियलाइज़ करें और दस्तावेज़ जोड़ें।  
- **Can I combine multiple criteria?** हाँ—ऑब्जेक्ट‑आधारित क्वेरीज़ या टेक्स्ट क्वेरी में Boolean ऑपरेटर्स का उपयोग करें।  
- **Do I need a license?** विकास के लिए एक फ्री ट्रायल काम करता है; एक कमर्शियल लाइसेंस सीमाओं को हटा देता है।  
- **Which IDE works best?** कोई भी Java IDE (IntelliJ IDEA, Eclipse, NetBeans) ठीक काम करता है।

## “create search index java” क्या है?
जावा में एक सर्च इंडेक्स बनाना एक सर्चेबल डेटा स्ट्रक्चर तैयार करना है जो दस्तावेज़ मेटाडेटा और सामग्री को संग्रहीत करता है, जिससे उपयोगकर्ता क्वेरीज़ के आधार पर तेज़ पुनर्प्राप्ति संभव होती है। GroupDocs.Search के साथ, इंडेक्स डिस्क पर रहता है, क्रमिक रूप से अपडेट किया जा सकता है, और फेस्डिंग तथा जटिल Boolean लॉजिक जैसी उन्नत सुविधाओं का समर्थन करता है।

## फेस्डेड और जटिल क्वेरीज़ के लिए GroupDocs.Search क्यों उपयोग करें?
- **Out‑of‑the‑box faceting** – फ़ाइल नाम, आकार, या कस्टम मेटाडेटा जैसे फ़ील्ड्स द्वारा फ़िल्टर करें।  
- **Rich query language** – AND/OR/NOT ऑपरेटर्स का उपयोग करके टेक्स्ट, फ़्रेज़, और फ़ील्ड क्वेरीज़ को मिलाएँ।  
- **Scalable performance** – मिलियन दस्तावेज़ों को इंडेक्स करता है जबकि सर्च लेटेंसी कम रखता है।  
- **Pure Java** – कोई नेटिव डिपेंडेंसी नहीं, वह किसी भी प्लेटफ़ॉर्म पर चलता है जो JDK 8+ चलाता है।

## आवश्यकताएँ
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

- **JDK 8 or newer** आपके IDE में इंस्टॉल और कॉन्फ़िगर किया हुआ।  
- **Maven** (या Gradle) डिपेंडेंसी मैनेजमेंट के लिए।  
- **GroupDocs.Search for Java** ≥ 25.4।  
- जावा OOP अवधारणाओं और Maven प्रोजेक्ट स्ट्रक्चर की बुनियादी परिचितता।

## GroupDocs.Search for Java सेटअप करना

### Maven सेटअप
Add the repository and dependency to your `pom.xml` file:

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

### डायरेक्ट डाउनलोड
वैकल्पिक रूप से, आधिकारिक रिलीज़ पेज से नवीनतम JAR डाउनलोड करें:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### लाइसेंस प्राप्ति
पूर्ण कार्यक्षमता अनलॉक करने के लिए:

1. **Free trial** – विकास और परीक्षण के लिए उपयुक्त।  
2. **Temporary evaluation license** – ट्रायल सीमाओं को बढ़ाता है।  
3. **Commercial license** – प्रोडक्शन उपयोग के लिए सभी प्रतिबंध हटाता है।

### बेसिक इनिशियलाइज़ेशन और सेटअप
निम्नलिखित स्निपेट दिखाता है कि कैसे `Index` क्लास को इंस्टैंसिएट करके **create a search index Java** किया जाता है:

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

इंडेक्स तैयार होने के बाद, हम वास्तविक-विश्व फेस्डेड और जटिल क्वेरीज़ की ओर बढ़ सकते हैं।

## कैसे create search index java – सरल फेस्डेड सर्च

फेस्डेड सर्च उपयोगकर्ताओं को पूर्वनिर्धारित श्रेणियों (facets) से मान चुनकर परिणामों को संकीर्ण करने देता है। नीचे चरण‑दर‑चरण walkthrough दिया गया है।

### चरण 1: इंडेक्स बनाएं
पहले, `Index` को उस फ़ोल्डर की ओर इशारा करें जहाँ इंडेक्स फ़ाइलें संग्रहीत होंगी।

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### चरण 2: इंडेक्स में दस्तावेज़ जोड़ें
GroupDocs.Search को बताएं कि आपके स्रोत दस्तावेज़ कहाँ स्थित हैं। सभी समर्थित फ़ाइल प्रकार (PDF, DOCX, TXT, आदि) स्वचालित रूप से इंडेक्स किए जाएंगे।

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### चरण 3: टेक्स्ट क्वेरी के साथ कंटेंट फ़ील्ड में खोज करें
एक त्वरित टेक्स्ट क्वेरी `content` फ़ील्ड द्वारा फ़िल्टर करती है। सिंटैक्स `content: Pellentesque` परिणामों को उन दस्तावेज़ों तक सीमित करता है जिनके बॉडी टेक्स्ट में शब्द *Pellentesque* मौजूद है।

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### चरण 4: ऑब्जेक्ट क्वेरी का उपयोग करके खोज करें
ऑब्जेक्ट‑आधारित क्वेरीज़ आपको सूक्ष्म नियंत्रण देती हैं। यहाँ हम एक शब्द क्वेरी बनाते हैं, उसे फ़ील्ड क्वेरी में लपेटते हैं, और उसे निष्पादित करते हैं।

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## कैसे create search index java – जटिल क्वेरी सर्च

जटिल क्वेरीज़ कई फ़ील्ड्स, Boolean ऑपरेटर्स, और फ़्रेज़ सर्च को मिलाती हैं। यह e‑commerce फ़िल्टर या कानूनी दस्तावेज़ शोध जैसे परिदृश्यों के लिए आदर्श है।

### चरण 1: जटिल क्वेरीज़ के लिए इंडेक्स बनाएं
एक ही फ़ोल्डर संरचना का पुन: उपयोग करें; आप इंडेक्स को सरल और जटिल दोनों परिदृश्यों में साझा कर सकते हैं।

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### चरण 2: टेक्स्ट क्वेरी के साथ खोज करें
निम्नलिखित क्वेरी उन फ़ाइलों को खोजती है जिनका नाम *lorem* **और** *ipsum* **या** कंटेंट में दो सटीक फ़्रेज़ में से कोई एक हो।

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

### चरण 3: ऑब्जेक्ट क्वेरी के साथ खोज करें
ऑब्जेक्ट‑आधारित निर्माण टेक्स्टुअल क्वेरी को प्रतिबिंबित करता है लेकिन टाइप सेफ़्टी और IDE सहायता प्रदान करता है।

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

## फेस्डेड और जटिल खोजों के व्यावहारिक अनुप्रयोग

| परिदृश्य | फेस्डिंग कैसे मदद करता है | उदाहरण क्वेरी |
|----------|---------------------------|---------------|
| **E‑commerce catalog** | श्रेणी, कीमत, ब्रांड द्वारा फ़िल्टर | `category: Electronics AND price:[100 TO 500]` |
| **Legal document repository** | केस नंबर, अधिकार क्षेत्र द्वारा संकीर्ण | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Research archives** | लेखक, प्रकाशन वर्ष, कीवर्ड्स को मिलाएँ | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | फ़ाइल प्रकार और विभाग द्वारा खोजें | `filetype: pdf AND department: HR` |

ये उदाहरण दर्शाते हैं कि क्यों **create search index java** तकनीकों में महारत हासिल करना किसी भी डेटा‑गहन एप्लिकेशन के लिए गेम‑चेंजर है।

## सामान्य समस्याएँ और ट्रबलशूटिंग
- **Empty results** – सुनिश्चित करें कि दस्तावेज़ सफलतापूर्वक जोड़े गए हैं (`index.getDocumentCount()` मदद कर सकता है)।  
- **Stale index** – फ़ाइलें जोड़ने या हटाने के बाद, इंडेक्स को सिंक में रखने के लिए `index.update()` कॉल करें।  
- **Incorrect field names** – टाइपो से बचने के लिए `CommonFieldNames` कॉन्स्टेंट्स (`Content`, `FileName`, आदि) का उपयोग करें।  
- **Performance bottlenecks** – बड़े संग्रह के लिए, `index.setCacheSize()` सक्षम करने या इंडेक्स फ़ोल्डर के लिए समर्पित SSD उपयोग करने पर विचार करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं GroupDocs.Search को Spring Boot के साथ उपयोग कर सकता हूँ?**  
A: बिल्कुल। केवल Maven डिपेंडेंसी जोड़ें, इंडेक्स को Spring bean के रूप में कॉन्फ़िगर करें, और जहाँ आवश्यक हो वहाँ इंजेक्ट करें।

**Q: क्या लाइब्रेरी कस्टम मेटाडेटा फ़ील्ड्स का समर्थन करती है?**  
A: हाँ – आप इंडेक्सिंग के दौरान यूज़र‑डिफाइंड फ़ील्ड्स जोड़ सकते हैं और फिर उन पर फेस्डिंग कर सकते हैं।

**Q: इंडेक्स कितना बड़ा हो सकता है?**  
A: इंडेक्स डिस्क‑आधारित है और मिलियन दस्तावेज़ संभाल सकता है; बस पर्याप्त स्टोरेज सुनिश्चित करें और कैश सेटिंग्स की निगरानी करें।

**Q: क्या परिणामों को प्रासंगिकता के आधार पर रैंक करने का कोई तरीका है?**  
A: GroupDocs.Search स्वचालित रूप से मैचों को स्कोर देता है; आप स्कोर `SearchResult.getDocument(i).getScore()` के माध्यम से प्राप्त कर सकते हैं।

**Q: यदि मैं एन्क्रिप्टेड PDFs को इंडेक्स करता हूँ क्या होता है?**  
A: दस्तावेज़ जोड़ते समय पासवर्ड प्रदान करें: `index.add(filePath, password)`।

## निष्कर्ष

अब तक आपको GroupDocs.Search के साथ **create a search index Java** बनाने, दस्तावेज़ जोड़ने, और सरल फेस्डेड क्वेरीज़ तथा परिष्कृत Boolean खोजें बनाने में सहज महसूस होना चाहिए। ये क्षमताएँ आपको तेज़, सटीक, और उपयोगकर्ता‑मित्रवत सर्च अनुभव विभिन्न प्रकार के अनुप्रयोगों में प्रदान करने में सक्षम बनाती हैं—e‑commerce प्लेटफ़ॉर्म से लेकर एंटरप्राइज़ नॉलेज बेस तक।

अगले कदम के लिए तैयार हैं? **GroupDocs.Search** की उन्नत सुविधाओं जैसे **highlighting**, **suggestions**, और **real‑time indexing** को एक्सप्लोर करें ताकि आपके एप्लिकेशन की सर्च शक्ति और बढ़े।

**अंतिम अपडेट:** 2025-12-16  
**परीक्षित संस्करण:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs
---
date: '2026-07-21'
description: Create Boolean Query Java ट्यूटोरियल दिखाता है कि GroupDocs.Search for
  Java का उपयोग करके boolean AND, OR, NOT खोजों को कैसे लागू किया जाए, दस्तावेज़ों
  को एक index में जोड़ा जाए, और दस्तावेज़ पुनर्प्राप्ति को boost किया जाए।
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Create Boolean Query Java ट्यूटोरियल चरण‑दर‑चरण समझाता है कि GroupDocs.Search
  for Java के साथ AND, OR, NOT क्वेरीज़ कैसे बनाएं, दस्तावेज़ों को एक index में जोड़ें,
  और retrieval performance को सुधारें।
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – GroupDocs.Search के साथ Boolean खोजों में महारत
  हासिल करें
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Create Boolean Query Java: GroupDocs.Search for Java के साथ Boolean खोजों
  में महारत हासिल करें'
type: docs
url: /hi/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# बूलियन क्वेरी जावा बनाएं: GroupDocs.Search for Java के साथ बूलियन खोज में महारत हासिल करें

दस्तावेज़ों के बड़े संग्रह को खोजने का काम अक्सर सुई को घास के ढेर में खोजने जैसा महसूस हो सकता है। **Create Boolean Query Java** आपको इंजन को ठीक वही बताने देता है जो आपको चाहिए—ऐसे दस्तावेज़ जो *दोनों* शब्दों को शामिल करते हैं, *किसी* एक शब्द को, या अनचाहे शब्दों को *बहिष्कृत* करते हैं। इस गाइड में हम **GroupDocs.Search for Java** को सेटअप करने, दस्तावेज़ों को इंडेक्स में जोड़ने, और शक्तिशाली बूलियन क्वेरीज़ बनाने के चरणों से गुजरेंगे जो आपके **document retrieval java** कार्यप्रवाह को बढ़ाएंगी। अंत तक आप कुछ ही पंक्तियों में जावा में बूलियन क्वेरीज़ बनाने वाला साफ़, रखरखाव योग्य कोड लिख पाएँगे।

## त्वरित उत्तर
- **बूलियन AND क्वेरी क्या है?** केवल उन दस्तावेज़ों को लौटाता है जो *सभी* निर्दिष्ट शब्दों को शामिल करते हैं।  
- **OR, AND से कैसे अलग है?** OR उन दस्तावेज़ों से मेल खाता है जिनमें *कोई भी* शब्द हो, जिससे परिणाम सेट विस्तृत होता है।  
- **NOT का उपयोग कब करना चाहिए?** अनचाहे शब्दों वाले दस्तावेज़ों को फ़िल्टर करने के लिए NOT का उपयोग करें।  
- **क्या मुझे लाइसेंस चाहिए?** परीक्षण के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **कौन सा जावा संस्करण आवश्यक है?** Java 8+ समर्थित है; JDK 11+ की सलाह दी जाती है।  

## **create boolean query java** क्या है?
`create boolean query java` जावा में एक खोज क्वेरी बनाने को दर्शाता है जो AND, OR, और NOT जैसे लॉजिकल ऑपरेटर्स को GroupDocs.Search API का उपयोग करके संयोजित करता है। इन ऑपरेटर्स को जोड़कर आप यह सटीक रूप से नियंत्रित कर सकते हैं कि कौन से दस्तावेज़ मेल खाते हैं, जिससे उन्नत फ़िल्टरिंग, प्रासंगिकता ट्यूनिंग, और जटिल खोज परिदृश्य संभव होते हैं।

## GroupDocs.Search for Java का उपयोग क्यों करें?
- **उच्च प्रदर्शन** बड़े दस्तावेज़ सेटों पर – यह मानक सर्वर पर एक मिनट से कम समय में 500 GB टेक्स्ट को इंडेक्स और खोज सकता है।  
- **समृद्ध API** जो टेक्स्ट‑आधारित और ऑब्जेक्ट‑आधारित दोनों क्वेरीज़ का समर्थन करता है, जिससे आप अपनी आर्किटेक्चर के अनुकूल शैली चुन सकते हैं।  
- **इन‑बिल्ट भाषा समर्थन** 30+ भाषाओं में स्टेमिंग, स्टॉप‑वर्ड्स, और फज़ी मैचिंग के लिए।  
- **आसान एकीकरण** Maven या सीधे JAR डाउनलोड के साथ, शुरू करने के लिए केवल कुछ पंक्तियों के कोड की आवश्यकता होती है।  

## पूर्वापेक्षाएँ
- **GroupDocs.Search for Java** (v25.4 या बाद का) – नीचे दिए गए डाउनलोड लिंक को देखें।  
- JDK 8+ स्थापित और आपके IDE (IntelliJ IDEA, Eclipse, आदि) में कॉन्फ़िगर किया हुआ।  
- बुनियादी जावा ज्ञान और निर्भरता प्रबंधन के लिए Maven।  

## GroupDocs.Search for Java सेटअप करना

### Maven सेटअप
अपने `pom.xml` में रिपॉजिटरी और निर्भरता जोड़ें:

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

### प्रत्यक्ष डाउनलोड
वैकल्पिक रूप से, आधिकारिक साइट से नवीनतम JAR डाउनलोड करें: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### लाइसेंस प्राप्ति
सभी सुविधाओं को अन्वेषण करने के लिए एक मुफ्त ट्रायल लाइसेंस से शुरू करें। उत्पादन उपयोग के लिए, पूर्ण कार्यक्षमता को अनलॉक करने हेतु एक व्यावसायिक लाइसेंस खरीदें।

### बुनियादी आरंभिककरण और सेटअप
एक इंडेक्स फ़ोल्डर बनाएं और `Index` ऑब्जेक्ट को इंस्टैंशिएट करें:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## आप बूलियन क्वेरी जावा कैसे बनाते हैं?
`Index` क्लास डिस्क पर संग्रहीत दस्तावेज़ों के खोज योग्य संग्रह को दर्शाता है। एक `BooleanQuery` कई सब‑क्वेरीज़ को लॉजिकल ऑपरेटर्स के साथ संयोजित करता है। `createAndQuery`, `createOrQuery`, और `createNotQuery` क्रमशः AND, OR, और NOT सब‑क्वेरीज़ बनाते हैं। एक `Index` इंस्टेंस लोड या बनाएं, दस्तावेज़ जोड़ें, फिर `createAndQuery`, `createOrQuery`, या `createNotQuery` का उपयोग करके `BooleanQuery` ऑब्जेक्ट बनाएं। मिलते-जुलते दस्तावेज़ प्राप्त करने के लिए `index.search(query)` को कॉल करें। यह पैटर्न सरल और जटिल दोनों परिदृश्यों में काम करता है और केवल तीन लॉजिकल चरणों की आवश्यकता होती है: इंडेक्स आरंभिककरण, दस्तावेज़ जोड़ना, और क्वेरी निष्पादन।

## बूलियन AND खोज

### अवलोकन
एक AND क्वेरी परिणामों को संकीर्ण करती है, जिससे प्रासंगिकता बढ़ती है जब आपको कई मानदंडों से मेल खाने वाले दस्तावेज़ चाहिए।

### कार्यान्वयन चरण
1. **इंडेक्स आरंभ करें** – यह AND परिदृश्य के लिए **इंडेक्स में दस्तावेज़ जोड़ें** को भी दर्शाता है।

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी खोज निष्पादित करें** – साधारण स्ट्रिंग सिंटैक्स का उपयोग करके।

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी खोज निष्पादित करें** – प्रोग्रामेटिक रूप से क्वेरी बनाते समय उपयोगी (**search with and java**)।

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## बूलियन OR खोज

### अवलोकन
एक OR क्वेरी अन्वेषणात्मक खोजों के लिए आदर्श है जहाँ आप कई कीवर्ड में से कम से कम एक को शामिल करने वाले दस्तावेज़ों को पकड़ना चाहते हैं (**search with or java**)।

### कार्यान्वयन चरण
1. **इंडेक्स आरंभ करें**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी खोज निष्पादित करें**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी खोज निष्पादित करें**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## बूलियन NOT खोज

### अवलोकन
एक NOT क्वेरी आपको अप्रासंगिक दस्तावेज़ों को हटाने में मदद करती है, जैसे प्रतिस्पर्धी के ब्रांड नाम को फ़िल्टर करना (**boolean search examples java**)।

### कार्यान्वयन चरण
1. **इंडेक्स आरंभ करें**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी खोज निष्पादित करें**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी खोज निष्पादित करें**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## जटिल बूलियन क्वेरीज़

### अवलोकन
जटिल क्वेरीज़ आपको वास्तविक‑दुनिया की खोज परिदृश्यों को मॉडल करने देती हैं, जैसे “ऐसे खेल लेख खोजें जो अनुकूल हों लेकिन किसी विशिष्ट एथलीट का उल्लेख न हो”।

### कार्यान्वयन चरण
1. **इंडेक्स आरंभ करें**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी खोज निष्पादित करें**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी खोज निष्पादित करें**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## **java boolean and or** क्वेरीज़ के व्यावहारिक अनुप्रयोग
- **डॉक्यूमेंट मैनेजमेंट सिस्टम** – ऐसे अनुबंध खोजें जो दोनों “confidential” **AND** “renewal” शामिल करते हों।  
- **लीगल रिसर्च** – केस लॉ को **AND**/ **OR** से फ़िल्टर करें और पुरानी विधियों को **NOT** से बाहर रखें।  
- **कस्टमर सपोर्ट** – ऐसे टिकट प्राप्त करें जिनमें “login” **AND** “error” उल्लेख हो लेकिन “resolved” न हो।  
- **कंटेंट क्यूरेशन** – न्यूज़लेटर के लिए “cloud” **OR** “serverless” के बारे में ब्लॉग पोस्ट एकत्र करें।  

## सामान्य समस्याएँ और ट्रबलशूटिंग
- **इंडेक्स रीफ़्रेश का अभाव** – नए दस्तावेज़ जोड़ने के बाद, उन्हें खोज योग्य बनाने के लिए `index.update()` कॉल करें।  
- **ऑपरेटर स्पेसिंग गलत** – GroupDocs.Search ऑपरेटर्स (`AND`, `OR`, `NOT`) के चारों ओर स्पेस की अपेक्षा करता है।  
- **केस सेंसिटिविटी** – क्वेरीज़ डिफ़ॉल्ट रूप से केस‑इनसेंसिटिव होती हैं, लेकिन कस्टम एनालाइज़र इस पर प्रभाव डाल सकते हैं।  
- **बड़े परिणाम सेट** – मेमोरी ओवरलोड से बचने के लिए पेजिनेशन (`search(query, 0, 100)`) का उपयोग करें।  

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं AND क्वेरी में दो से अधिक शब्दों को जोड़ सकता हूँ?**  
A: बिल्कुल। आप कई `createWordQuery` ऑब्जेक्ट्स को `createAndQuery` से जोड़ सकते हैं, या टेक्स्ट क्वेरी में बस `"term1 AND term2 AND term3"` लिख सकते हैं।

**Q: क्या GroupDocs.Search वाइल्डकार्ड या फज़ी खोजों का समर्थन करता है?**  
A: हाँ। वाइल्डकार्ड के लिए `*` जोड़ें (उदा., `promot*`) या फज़ी मैचिंग के लिए `~` उपयोग करें (उदा., `comfort~`)।

**Q: मैं खोज को विशिष्ट फ़ाइल प्रकारों तक कैसे सीमित करूँ?**  
`FileTypeQuery` खोज परिणामों को PDF या DOCX जैसे विशिष्ट फ़ाइल फ़ॉर्मेट तक सीमित करता है।  
A: `FileTypeQuery` क्लास का उपयोग करके परिणामों को PDF, DOCX आदि तक सीमित करें, और इसे अपनी बूलियन क्वेरी के साथ संयोजित करें।

**Q: इंडेक्सिंग प्रदर्शन की निगरानी का सबसे अच्छा तरीका क्या है?**  
A: बिल्ट‑इन लॉगर को सक्षम करें (`index.getLogger().setLevel(Level.INFO)`) और प्रत्येक `add` ऑपरेशन के बाद टाइमिंग मेट्रिक्स की समीक्षा करें।

**Q: क्या कुछ शब्दों की प्रासंगिकता बढ़ाने का कोई तरीका है?**  
`BoostQuery` खोज क्वेरी में निर्दिष्ट शब्दों के प्रासंगिकता स्कोर को बढ़ाता है।  
A: हाँ। महत्वपूर्ण शब्दों को `BoostQuery` से घेरें ताकि स्कोरिंग एल्गोरिद्म में उनका वजन बढ़े।

---

**अंतिम अपडेट:** 2026-07-21  
**परीक्षित संस्करण:** GroupDocs.Search 25.4 (Java)  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल्स

- [बूलियन ऑपरेटर जावा – सर्च इंडेक्स बनाएं और फैसेटेड सर्च](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [GroupDocs.Search Java में महारत: कुशल दस्तावेज़ खोज और इंडेक्स प्रबंधन](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - GroupDocs.Search Java में महारत – सर्च इंडेक्स बनाएं और प्रबंधित करें](/search/java/indexing/groupdocs-search-java-create-index-guide/)
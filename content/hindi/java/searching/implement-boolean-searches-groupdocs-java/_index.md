---
date: '2026-01-29'
description: GroupDocs.Search for Java का उपयोग करके जावा बूलियन AND OR क्वेरीज़ को
  लागू करना सीखें, दस्तावेज़ों को इंडेक्स में जोड़ें और दस्तावेज़ पुनर्प्राप्ति को
  बेहतर बनाएं।
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'जावा बूलियन एंड ऑर: GroupDocs.Search for Java के साथ बूलियन खोजों में माहिर
  बनें'
type: docs
url: /hi/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: GroupDocs.Search for Java के साथ बूलियन खोजों में महारत हासिल करें

दस्तावेज़ों के बड़े संग्रह को खोजने का काम अक्सर सुई को घास के ढेर में खोजने जैसा लगता है। **java boolean and or** क्वेरीज़ के साथ आप इंजन को ठीक‑ठीक बता सकते हैं कि आपको क्या चाहिए—ऐसे दस्तावेज़ जो *दोनों* शब्दों को शामिल करते हों, *किसी* एक शब्द को, या अनचाहे शब्दों को **exclude** करें। इस गाइड में हम **GroupDocs.Search for Java** को सेट‑अप करेंगे, इंडेक्स में दस्तावेज़ जोड़ेंगे, और शक्तिशाली बूलियन क्वेरीज़ बनाएँगे जो आपके **document retrieval java** वर्कफ़्लो को तेज़ बनाएँगी।

## त्वरित उत्तर
- **बूलियन AND क्वेरी क्या है?** केवल उन दस्तावेज़ों को लौटाती है जिनमें *सभी* निर्दिष्ट शब्द मौजूद हों।  
- **OR, AND से कैसे अलग है?** OR उन दस्तावेज़ों को मिलाता है जिनमें *कोई भी* शब्द हो, जिससे परिणाम सेट विस्तृत हो जाता है।  
- **NOT कब उपयोग करें?** उन दस्तावेज़ों को फ़िल्टर करने के लिए NOT का प्रयोग करें जिनमें अनचाहे शब्द हों।  
- **क्या लाइसेंस चाहिए?** परीक्षण के लिए एक फ्री ट्रायल काम करता है; उत्पादन के लिए एक कमर्शियल लाइसेंस आवश्यक है।  
- **कौन सा Java संस्करण आवश्यक है?** Java 8+ समर्थित है; JDK 11+ की सलाह दी जाती है।

## **java boolean and or** क्या है?
एक **java boolean and or** क्वेरी लॉजिकल ऑपरेटर (AND, OR, NOT) को मिलाकर खोज परिणामों को परिष्कृत करती है। क्वेरी को इस तरह संरचित करके आप GroupDocs.Search को ठीक‑ठीक बता सकते हैं कि शब्द आपस में कैसे जुड़े हैं, जिससे पुनःप्राप्ति प्रक्रिया पर सटीक नियंत्रण मिलता है।

## GroupDocs.Search for Java क्यों उपयोग करें?
- **उच्च प्रदर्शन** बड़े दस्तावेज़ सेटों पर।  
- **समृद्ध API** जो टेक्स्ट‑आधारित और ऑब्जेक्ट‑आधारित दोनों क्वेरीज़ का समर्थन करता है।  
- **इन‑बिल्ट भाषा समर्थन** स्टेमिंग, स्टॉप‑वर्ड्स, और फज़ी मैचिंग के लिए।  
- **Maven या सीधे JAR डाउनलोड** के साथ आसान इंटीग्रेशन।

## पूर्वापेक्षाएँ
शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हों:

- **GroupDocs.Search for Java** (v25.4 या बाद का) – नीचे दिए गए डाउनलोड लिंक को देखें।  
- JDK 8+ इंस्टॉल हो और आपके IDE (IntelliJ IDEA, Eclipse, आदि) में कॉन्फ़िगर हो।  
- बेसिक Java ज्ञान और Maven के साथ डिपेंडेंसी मैनेजमेंट।

## GroupDocs.Search for Java सेट‑अप करना

### Maven सेटअप
`pom.xml` में रिपॉज़िटरी और डिपेंडेंसी जोड़ें:

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

### सीधे डाउनलोड
वैकल्पिक रूप से, आधिकारिक साइट से नवीनतम JAR डाउनलोड करें: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)।

### लाइसेंस प्राप्त करना
सभी फीचर एक्सप्लोर करने के लिए एक फ्री ट्रायल लाइसेंस से शुरू करें। उत्पादन उपयोग के लिए, पूर्ण कार्यक्षमता अनलॉक करने हेतु कमर्शियल लाइसेंस खरीदें।

### बेसिक इनिशियलाइज़ेशन और सेटअप
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

## java boolean and or: बूलियन खोजों को लागू करना

नीचे हम **AND**, **OR**, **NOT**, और **जटिल** क्वेरीज़ को कवर करेंगे। प्रत्येक सेक्शन में एक प्लेन‑टेक्स्ट क्वेरी और समकक्ष ऑब्जेक्ट‑बेस्ड क्वेरी दोनों दिखाए गए हैं, ताकि आप अपनी कोडबेस के अनुसार उपयुक्त शैली चुन सकें।

### बूलियन AND सर्च
**AND** के साथ शब्दों को मिलाकर केवल उन दस्तावेज़ों को प्राप्त करें जिनमें *सभी* कीवर्ड हों।

#### अवलोकन
AND क्वेरी परिणामों को संकीर्ण करती है, जिससे प्रासंगिकता बढ़ती है जब आपको कई मानदंडों से मेल खाने वाले दस्तावेज़ चाहिए हों।

#### कार्यान्वयन चरण

1. **इंडेक्स इनिशियलाइज़ करें** – यह **add documents to index** को भी दर्शाता है, जो AND परिदृश्य के लिए आवश्यक है।

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी सर्च चलाएँ** – प्लेन स्ट्रिंग सिंटैक्स का उपयोग करके।

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी सर्च चलाएँ** – प्रोग्रामेटिक रूप से क्वेरी बनाने के लिए उपयोगी (**search with and java**)।

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### बूलियन OR सर्च
**OR** का उपयोग करके परिणामों को विस्तृत करें, यानी आपूर्ति किए गए किसी भी शब्द से मेल खाने वाले दस्तावेज़ मिलें।

#### अवलोकन
OR क्वेरी अन्वेषणात्मक खोजों के लिए आदर्श है जहाँ आप कई कीवर्ड में से कम से कम एक वाले दस्तावेज़ पकड़ना चाहते हैं (**search with or java**)।

#### कार्यान्वयन चरण

1. **इंडेक्स इनिशियलाइज़ करें**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी सर्च चलाएँ**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी सर्च चलाएँ**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### बूलियन NOT सर्च
**NOT** के साथ अनचाहे शब्दों को बाहर रखें और परिणामों से शोर को फ़िल्टर करें।

#### अवलोकन
NOT क्वेरी आपको अप्रासंगिक दस्तावेज़ हटाने में मदद करती है, जैसे किसी प्रतिस्पर्धी के ब्रांड नाम को फ़िल्टर करना (**boolean search examples java**)।

#### कार्यान्वयन चरण

1. **इंडेक्स इनिशियलाइज़ करें**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी सर्च चलाएँ**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी सर्च चलाएँ**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### जटिल बूलियन क्वेरीज़
**AND**, **OR**, और **NOT** को मिलाकर अत्यधिक विशिष्ट पुनःप्राप्ति आवश्यकताओं के लिए जटिल खोज लॉजिक बनाएं।

#### अवलोकन
जटिल क्वेरी वास्तविक‑विश्व खोज परिदृश्यों को मॉडल करती हैं, जैसे “ऐसे खेल लेख खोजें जो सकारात्मक हों लेकिन किसी विशेष एथलीट का उल्लेख न हो”।

#### कार्यान्वयन चरण

1. **इंडेक्स इनिशियलाइज़ करें**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **दस्तावेज़ इंडेक्स करें**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **टेक्स्ट क्वेरी सर्च चलाएँ**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **ऑब्जेक्ट क्वेरी सर्च चलाएँ**

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

## java boolean and or क्वेरीज़ के व्यावहारिक उपयोग
- **डॉक्यूमेंट मैनेजमेंट सिस्टम** – ऐसे कॉन्ट्रैक्ट खोजें जिनमें “confidential” **AND** “renewal” दोनों हों।  
- **लीगल रिसर्च** – केस लॉ को **AND**/**OR** से फ़िल्टर करें और पुरानी विधियों को **NOT** से बाहर रखें।  
- **कस्टमर सपोर्ट** – ऐसे टिकट प्राप्त करें जिनमें “login” **AND** “error” हो, लेकिन “resolved” न हो।  
- **कंटेंट क्यूरेशन** – न्यूज़लेटर के लिए “cloud” **OR** “serverless” वाले ब्लॉग पोस्ट इकट्ठा करें।

## सामान्य गलतियाँ एवं ट्रबलशूटिंग
- **इंडेक्स रिफ्रेश भूल जाना** – नए दस्तावेज़ जोड़ने के बाद `index.update()` कॉल करें ताकि वे सर्चेबल बनें।  
- **ऑपरेटर स्पेसिंग गलत** – GroupDocs.Search ऑपरेटरों (`AND`, `OR`, `NOT`) के चारों ओर स्पेस की अपेक्षा करता है।  
- **केस सेंसिटिविटी** – डिफ़ॉल्ट रूप से क्वेरी केस‑इन्सेंसिटिव होती है, लेकिन कस्टम एनालाइज़र इसको बदल सकते हैं।  
- **बड़े परिणाम सेट** – मेमोरी ओवरलोड से बचने के लिए पेजिनेशन (`search(query, 0, 100)`) उपयोग करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं AND क्वेरी में दो से अधिक शब्द जोड़ सकता हूँ?**  
उत्तर: बिल्कुल। आप कई `createWordQuery` ऑब्जेक्ट को `createAndQuery` से चेन कर सकते हैं, या प्लेन टेक्स्ट में `"term1 AND term2 AND term3"` लिख सकते हैं।

**प्रश्न: क्या GroupDocs.Search वाइल्डकार्ड या फज़ी सर्च को सपोर्ट करता है?**  
उत्तर: हाँ। वाइल्डकार्ड के लिए `*` जोड़ें (जैसे `promot*`) या फज़ी मैचिंग के लिए `~` उपयोग करें (जैसे `comfort~`)।

**प्रश्न: मैं सर्च को विशिष्ट फ़ाइल प्रकारों तक कैसे सीमित करूँ?**  
उत्तर: `FileTypeQuery` क्लास का उपयोग करके परिणामों को PDFs, DOCX आदि तक सीमित करें, और इसे अपनी बूलियन क्वेरी के साथ मिलाएँ।

**प्रश्न: इंडेक्सिंग प्रदर्शन की निगरानी का सबसे अच्छा तरीका क्या है?**  
उत्तर: बिल्ट‑इन लॉगर को सक्षम करें (`index.getLogger().setLevel(Level.INFO)`) और प्रत्येक `add` ऑपरेशन के बाद टाइमिंग मेट्रिक्स देखें।

**प्रश्न: क्या कुछ शब्दों की प्रासंगिकता बढ़ाने का तरीका है?**  
उत्तर: हाँ। महत्वपूर्ण शब्दों को `BoostQuery` में रैप करें ताकि स्कोरिंग एल्गोरिद्म में उनका वज़न बढ़े।

---

**अंतिम अपडेट:** 2026-01-29  
**टेस्टेड विद:** GroupDocs.Search 25.4 (Java)  
**लेखक:** GroupDocs
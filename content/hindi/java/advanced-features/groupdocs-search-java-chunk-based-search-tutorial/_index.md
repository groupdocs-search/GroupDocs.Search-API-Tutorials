---
date: '2026-02-21'
description: GroupDocs.Search का उपयोग करके जावा में चंक‑आधारित खोज के साथ दस्तावेज़ों
  को इंडेक्स में जोड़ना और खोज प्रदर्शन बढ़ाना सीखें, बड़े दस्तावेज़ सेटों के लिए
  जावा सर्च इंडेक्स मेमोरी को अनुकूलित करें।
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: जावा में चंक‑आधारित खोज के साथ दस्तावेज़ को इंडेक्स में जोड़ें
type: docs
url: /hi/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Java में chunk‑based खोज के साथ दस्तावेज़ को इंडेक्स में जोड़ें

आधुनिक अनुप्रयोगों में जहाँ **इंडेक्स में दस्तावेज़ जोड़ना** तेज़ी से आवश्यक होता है और फिर तेज़, chunk‑आधारित क्वेरीज़ करनी होती हैं, आपको एक ऐसा समाधान चाहिए जो मेमोरी को अधिक न खींचे और स्केलेबल हो। यह ट्यूटोरियल आपको GroupDocs.Search for Java सेटअप करने, कई दस्तावेज़ फ़ोल्डरों को जोड़ने, और इंजन को **खोज प्रदर्शन बढ़ाने** के लिए कॉन्फ़िगर करने के चरण दिखाता है, जबकि **java search index memory** उपयोग को नियंत्रित रखता है। चाहे आप कानूनी अनुबंधों, सपोर्ट टिकटों या शोध पत्रों को इंडेक्स कर रहे हों, नीचे दिए गए चरण एक प्रोडक्शन‑रेडी इम्प्लीमेंटेशन प्रदान करेंगे।

## त्वरित उत्तर
- **पहला कदम क्या है?** एक सर्च इंडेक्स फ़ोल्डर बनाएं।  
- **मैं कई फ़ाइलें कैसे शामिल करूँ?** प्रत्येक दस्तावेज़ फ़ोल्डर के लिए `index.add()` उपयोग करें।  
- **कौन सा विकल्प chunk खोज को सक्षम करता है?** `options.setChunkSearch(true)`।  
- **क्या मैं पहले chunk के बाद भी खोज जारी रख सकता हूँ?** हाँ, टोकन के साथ `index.searchNext()` कॉल करें।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक फ्री ट्रायल या टेम्पररी लाइसेंस काम करता है; प्रोडक्शन के लिए पूर्ण लाइसेंस आवश्यक है।  

## आप क्या सीखेंगे
- निर्दिष्ट फ़ोल्डर में सर्च इंडेक्स कैसे बनाएं।  
- कई स्थानों से **इंडेक्स में दस्तावेज़ जोड़ना** के चरण।  
- chunk‑आधारित खोज को सक्षम करने के लिए सर्च विकल्पों का कॉन्फ़िगरेशन।  
- प्रारंभिक और बाद की chunk‑आधारित खोजें कैसे करें।  
- वास्तविक दुनिया के परिदृश्य जहाँ chunk‑आधारित दस्तावेज़ खोज चमकती है।  

## पूर्वापेक्षाएँ
इस गाइड को फॉलो करने के लिए सुनिश्चित करें कि आपके पास है:

- **आवश्यक लाइब्रेरीज़**: GroupDocs.Search for Java 25.4 या बाद का संस्करण।  
- **पर्यावरण सेटअप**: संगत Java Development Kit (JDK) स्थापित हो।  
- **ज्ञान की पूर्वापेक्षाएँ**: बेसिक Java प्रोग्रामिंग और Maven की समझ।  

## GroupDocs.Search for Java सेटअप करना
शुरू करने के लिए, Maven का उपयोग करके GroupDocs.Search को अपने प्रोजेक्ट में इंटीग्रेट करें:

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

वैकल्पिक रूप से, नवीनतम संस्करण [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

### लाइसेंस प्राप्त करना
GroupDocs.Search को आज़माने के लिए:

- **फ्री ट्रायल** – बिना प्रतिबद्धता के कोर फीचर्स टेस्ट करें।  
- **टेम्पररी लाइसेंस** – विकास के लिए विस्तारित एक्सेस।  
- **पर्चेज** – प्रोडक्शन उपयोग के लिए पूर्ण लाइसेंस।  

### बेसिक इनिशियलाइज़ेशन और सेटअप
उस फ़ोल्डर में एक इंडेक्स बनाएं जहाँ आप सर्चेबल डेटा रखना चाहते हैं:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## इंडेक्स में दस्तावेज़ कैसे जोड़ें
अब जब इंडेक्स मौजूद है, अगला तार्किक कदम है **इंडेक्स में दस्तावेज़ जोड़ना** उन स्थानों से जहाँ आपकी फ़ाइलें संग्रहीत हैं।

### 1. इंडेक्स बनाना
**सारांश**: सर्च इंडेक्स के लिए एक डायरेक्टरी सेट अप करें।

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. इंडेक्स में दस्तावेज़ जोड़ना
**सारांश**: कई स्रोत फ़ोल्डरों से फ़ाइलें लाएँ।

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Chunk खोज के लिए सर्च विकल्प कॉन्फ़िगर करना
विकल्प ऑब्जेक्ट को ट्यून करके chunk‑आधारित खोज सक्षम करें।

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. प्रारंभिक Chunk‑आधारित खोज करना
chunk‑सक्षम विकल्पों के साथ पहली क्वेरी चलाएँ।

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Chunk‑आधारित खोज जारी रखना
जब तक खोज पूरी नहीं होती, शेष chunks पर इटरेट करें।

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Chunk‑आधारित खोज क्यों उपयोग करें?
Chunk‑आधारित खोज बड़े दस्तावेज़ संग्रह को प्रबंधनीय टुकड़ों में विभाजित करती है, जिससे मेमोरी दबाव कम होता है और प्रतिक्रिया समय तेज़ हो जाता है। यह विशेष रूप से उपयोगी है जब:

1. **कानूनी टीमों** को हजारों अनुबंधों में विशिष्ट क्लॉज़ खोजने होते हैं।  
2. **कस्टमर सपोर्ट पोर्टल** को तुरंत प्रासंगिक नॉलेज‑बेस लेख दिखाने होते हैं।  
3. **शोधकर्ता** बड़े डेटा सेट को बिना पूरे फ़ाइलों को मेमोरी में लोड किए प्रोसेस करना चाहते हैं।  

## यह तरीका **खोज प्रदर्शन को कैसे बढ़ाता है**
छोटे chunks को खोजकर, इंजन:

- अप्रासंगिक सेक्शन को जल्दी स्किप कर CPU साइकिल बचाता है।  
- केवल सक्रिय chunk को मेमोरी में रखता है, जिससे **java search index memory** की खपत सीधे घटती है।  
- मल्टी‑कोर मशीनों पर chunk प्रोसेसिंग को पैरललाइज़ करके तेज़ परिणाम देता है।  

## **java search index memory** का प्रबंधन
जबकि chunk‑आधारित खोज पहले से ही मेमोरी फुटप्रिंट घटाती है, आप JVM को और ट्यून कर सकते हैं:

- इंडेक्स आकार के आधार पर पर्याप्त हीप अलोकेट करें (`-Xmx2g` या अधिक)।  
- बल्क एडिशन के बाद `index.optimize()` चलाकर इंडेक्स संरचना को कॉम्प्रेस करें।  
- VisualVM जैसे टूल्स से GC पॉज़ मॉनिटर करें ताकि लेटेंसी स्पाइक्स न आएँ।  

## प्रदर्शन संबंधी विचार
- **मेमोरी मैनेजमेंट** – बड़े इंडेक्स के लिए पर्याप्त हीप स्पेस (`-Xmx`) अलोकेट करें।  
- **रिसोर्स मॉनिटरिंग** – इंडेक्सिंग और सर्च ऑपरेशन्स के दौरान CPU उपयोग पर नज़र रखें।  
- **इंडेक्स मेंटेनेंस** – समय‑समय पर इंडेक्स को रीबिल्ड या क्लीन करें ताकि पुराना डेटा हटाया जा सके।  

## सामान्य pitfalls & ट्रबलशूटिंग
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Chunk‑आधारित खोज क्या है?**  
**उत्तर:** Chunk‑आधारित खोज डेटा सेट को छोटे टुकड़ों में विभाजित करती है, जिससे बड़े वॉल्यूम पर प्रभावी क्वेरी संभव हो जाती है बिना पूरे दस्तावेज़ को मेमोरी में लोड किए।

**प्रश्न: मैं अपने इंडेक्स को नई फ़ाइलों के साथ कैसे अपडेट करूँ?**  
**उत्तर:** बस `index.add()` को नई दस्तावेज़ों के पाथ के साथ कॉल करें; इंडेक्स स्वचालित रूप से उन्हें शामिल कर लेगा।

**प्रश्न: क्या GroupDocs.Search विभिन्न फ़ाइल फ़ॉर्मेट्स को संभाल सकता है?**  
**उत्तर:** हाँ, यह PDFs, DOCX, XLSX, PPTX और कई अन्य सामान्य फ़ॉर्मेट्स को सपोर्ट करता है।

**प्रश्न: सामान्य प्रदर्शन बाधाएँ क्या हैं?**  
**उत्तर:** मेमोरी सीमाएँ और अनऑप्टिमाइज़्ड इंडेक्स सबसे आम हैं; पर्याप्त हीप अलोकेट करें और नियमित रूप से इंडेक्स को ऑप्टिमाइज़ करें।

**प्रश्न: अधिक विस्तृत दस्तावेज़ीकरण कहाँ मिल सकता है?**  
**उत्तर:** आधिकारिक [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) पर विस्तृत गाइड और API रेफ़रेंसेज़ देखें।

**प्रश्न: क्या Chunk‑आधारित खोज एन्क्रिप्टेड PDFs के साथ काम करती है?**  
**उत्तर:** हाँ, जब तक आप उपयुक्त API ओवरलोड के माध्यम से पासवर्ड प्रदान करें।

**प्रश्न: मैं इंडेक्सिंग प्रोग्रेस को कैसे मॉनिटर करूँ?**  
**उत्तर:** `Index.add()` के उस ओवरलोड का उपयोग करें जो `Progress` ऑब्जेक्ट रिटर्न करता है या लॉगिंग कॉलबैक में हुक करें।

## संसाधन
- **डॉक्यूमेंटेशन**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API रेफ़रेंस**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **डाउनलोड**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **फ्री सपोर्ट**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **टेम्पररी लाइसेंस**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**अंतिम अपडेट:** 2026-02-21  
**टेस्टेड विथ:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs  

---
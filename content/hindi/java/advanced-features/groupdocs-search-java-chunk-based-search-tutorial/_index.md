---
date: '2025-12-19'
description: GroupDocs.Search का उपयोग करके जावा में दस्तावेज़ों को इंडेक्स में जोड़ना
  और चंक-आधारित खोज को सक्षम करना सीखें, जिससे बड़े दस्तावेज़ सेटों के लिए प्रदर्शन
  में सुधार हो।
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: जावा में चंक‑आधारित खोज के साथ दस्तावेज़ को इंडेक्स में जोड़ें
type: docs
url: /hi/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Java में chunk‑आधारित खोज के साथ इंडेक्स में दस्तावेज़ जोड़ें

आज के डेटा‑ड्रिवेन विश्व में, **add documents to index** को जल्दी से करना और फिर chunk‑based खोज करना किसी भी एप्लिकेशन के लिए आवश्यक है जो बड़ी फ़ाइल संग्रहों को संभालता है। चाहे आप कानूनी अनुबंधों, ग्राहक सहायता अभिलेखों, या विशाल शोध पुस्तकालयों से निपट रहे हों, यह ट्यूटोरियल आपको दिखाता है कि GroupDocs.Search for Java को कैसे सेट अप करें ताकि आप दस्तावेज़ों को प्रभावी ढंग से इंडेक्स कर सकें और बाइट‑साइज़्ड chunks में प्रासंगिक जानकारी प्राप्त कर सकें।

## आप क्या सीखेंगे
- निर्दिष्ट फ़ोल्डर में खोज इंडेक्स कैसे बनाएं।  
- कई स्थानों से **add documents to index** करने के चरण।  
- chunk‑based खोज को सक्षम करने के लिए खोज विकल्पों को कॉन्फ़िगर करना।  
- प्रारंभिक और बाद के chunk‑based खोजें करना।  
- वास्तविक‑दुनिया के परिदृश्य जहाँ chunk‑based दस्तावेज़ खोज चमकती है।

## त्वरित उत्तर
- **पहला कदम क्या है?** एक खोज इंडेक्स फ़ोल्डर बनाएं।  
- **मैं कई फ़ाइलें कैसे शामिल करूँ?** प्रत्येक दस्तावेज़ फ़ोल्डर के लिए `index.add()` का उपयोग करें।  
- **कौन सा विकल्प chunk खोज को सक्षम करता है?** `options.setChunkSearch(true)`।  
- **क्या मैं पहले chunk के बाद खोज जारी रख सकता हूँ?** हाँ, टोकन के साथ `index.searchNext()` को कॉल करें।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक फ्री ट्रायल या टेम्पररी लाइसेंस काम करता है; प्रोडक्शन के लिए पूर्ण लाइसेंस आवश्यक है।

## पूर्वापेक्षाएँ
- **आवश्यक लाइब्रेरीज़**: GroupDocs.Search for Java 25.4 या बाद का संस्करण।  
- **पर्यावरण सेटअप**: संगत Java Development Kit (JDK) स्थापित हो।  
- **ज्ञान पूर्वापेक्षाएँ**: बुनियादी Java प्रोग्रामिंग और Maven की परिचितता।

## GroupDocs.Search for Java सेटअप करना
शुरू करने के लिए, Maven का उपयोग करके अपने प्रोजेक्ट में GroupDocs.Search को इंटीग्रेट करें:

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

वैकल्पिक रूप से, नवीनतम संस्करण को यहाँ से डाउनलोड करें: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)।

### लाइसेंस प्राप्त करना
GroupDocs.Search को आज़माने के लिए:

- **Free Trial** – बिना प्रतिबद्धता के मुख्य सुविधाओं का परीक्षण करें।  
- **Temporary License** – विकास के लिए विस्तारित एक्सेस।  
- **Purchase** – प्रोडक्शन उपयोग के लिए पूर्ण लाइसेंस।

### बुनियादी इनिशियलाइज़ेशन और सेटअप
जिस फ़ोल्डर में आप खोज योग्य डेटा रखना चाहते हैं, वहाँ एक इंडेक्स बनाएं:

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
अब जबकि इंडेक्स मौजूद है, अगला तार्किक कदम है **add documents to index** को उन स्थानों से जोड़ना जहाँ आपकी फ़ाइलें संग्रहीत हैं।

### 1. इंडेक्स बनाना
**Overview**: खोज इंडेक्स के लिए एक डायरेक्टरी सेट अप करें।

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. इंडेक्स में दस्तावेज़ जोड़ना
**Overview**: कई स्रोत फ़ोल्डरों से फ़ाइलें लाएँ।

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

### 3. Chunk खोज के लिए खोज विकल्प कॉन्फ़िगर करना
विकल्प ऑब्जेक्ट को समायोजित करके chunk‑based खोज को सक्षम करें।

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. प्रारंभिक Chunk‑Based खोज करना
Chunk‑enabled विकल्पों का उपयोग करके पहला क्वेरी चलाएँ।

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Chunk‑Based खोज जारी रखना
जब तक खोज पूरी न हो जाए, शेष chunks पर इटरेट करें।

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Chunk‑Based खोज का उपयोग क्यों करें?
Chunk‑based खोज बड़े दस्तावेज़ संग्रहों को प्रबंधनीय टुकड़ों में विभाजित करती है, जिससे मेमोरी दबाव कम होता है और प्रतिक्रिया समय तेज़ हो जाता है। यह विशेष रूप से लाभदायक है जब:

1. **Legal teams** को हजारों अनुबंधों में विशिष्ट क्लॉज़ खोजने की आवश्यकता होती है।  
2. **Customer support portals** को तुरंत प्रासंगिक नॉलेज‑बेस लेख दिखाने चाहिए।  
3. **Researchers** को पूरी फ़ाइलें मेमोरी में लोड किए बिना बड़े डेटासेट को छानना पड़ता है।

## प्रदर्शन संबंधी विचार
- **Memory Management** – बड़े इंडेक्स के लिए पर्याप्त हीप स्पेस (`-Xmx`) आवंटित करें।  
- **Resource Monitoring** – इंडेक्सिंग और खोज संचालन के दौरान CPU उपयोग पर नज़र रखें।  
- **Index Maintenance** – समय-समय पर इंडेक्स को पुनर्निर्मित या साफ़ करें ताकि पुराना डेटा हटाया जा सके।

## सामान्य समस्याएँ और ट्रबलशूटिंग
| Issue | क्यों होता है | समाधान |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | हीप आकार बहुत छोटा | JVM हीप बढ़ाएँ (`-Xmx2g` या अधिक) |
| No results returned | Chunk टोकन प्रोसेस नहीं हुआ | सुनिश्चित करें कि `while` लूप `getNextChunkSearchToken()` `null` होने तक चले |
| Slow search performance | इंडेक्स अनऑप्टिमाइज़्ड | बल्क एडिशन के बाद `index.optimize()` चलाएँ |

## अक्सर पूछे जाने वाले प्रश्न

**Q: Chunk‑based खोज क्या है?**  
A: Chunk‑based खोज डेटा सेट को छोटे टुकड़ों में विभाजित करती है, जिससे बड़े डेटा वॉल्यूम पर प्रभावी क्वेरी संभव हो जाती है बिना पूरे दस्तावेज़ को मेमोरी में लोड किए।

**Q: मैं अपने इंडेक्स को नई फ़ाइलों से कैसे अपडेट करूँ?**  
A: बस `index.add()` को नई दस्तावेज़ों के पाथ के साथ कॉल करें; इंडेक्स उन्हें स्वचालित रूप से शामिल कर लेगा।

**Q: क्या GroupDocs.Search विभिन्न फ़ाइल फ़ॉर्मेट संभाल सकता है?**  
A: हाँ, यह PDFs, DOCX, XLSX, PPTX, और कई अन्य सामान्य फ़ॉर्मेट को सपोर्ट करता है।

**Q: सामान्य प्रदर्शन बाधाएँ क्या हैं?**  
A: मेमोरी प्रतिबंध और अनऑप्टिमाइज़्ड इंडेक्स सबसे आम हैं; पर्याप्त हीप आवंटित करें और नियमित रूप से इंडेक्स को ऑप्टिमाइज़ करें।

**Q: अधिक विस्तृत दस्तावेज़ीकरण कहाँ मिल सकता है?**  
A: आधिकारिक [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) पर गहन गाइड और API रेफ़रेंस देखें।

## संसाधन
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API रेफ़रेंस**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **डाउनलोड**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **नि:शुल्क समर्थन**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **टेम्पररी लाइसेंस**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**अंतिम अपडेट:** 2025-12-19  
**परीक्षित संस्करण:** GroupDocs.Search 25.4 for Java  
**लेखक:** GroupDocs  

---
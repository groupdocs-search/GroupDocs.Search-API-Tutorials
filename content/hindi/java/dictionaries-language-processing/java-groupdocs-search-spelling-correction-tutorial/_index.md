---
date: '2026-02-21'
description: जावा में GroupDocs.Search का उपयोग करके वर्तनी सुधार को सक्षम करना सीखें,
  दस्तावेज़ों को इंडेक्स में जोड़ें, और बेहतर खोज सटीकता के लिए अधिकतम त्रुटि संख्या
  सेट करें।
keywords:
- spelling correction Java
- GroupDocs.Search tutorial
- Java search functionality
title: GroupDocs.Search के साथ जावा में स्पेलिंग कैसे सक्षम करें
type: docs
url: /hi/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

CODE_BLOCK_0}}; keep unchanged.

Also there is a table; translate column headers and rows.

Let's write final output.

# Java में GroupDocs.Search का उपयोग करके वर्तनी सक्षम कैसे करें

सटीक खोज परिणाम किसी भी आधुनिक एप्लिकेशन के लिए आवश्यक होते हैं। इस ट्यूटोरियल में आप **Java में वर्तनी सुधार को सक्षम करने** का तरीका सीखेंगे, जिससे उपयोगकर्ता टाइपो करने पर भी सही परिणाम प्राप्त कर सकें। हम इंडेक्स बनाना, **इंडेक्स में दस्तावेज़ जोड़ना**, वर्तनी विकल्पों को कॉन्फ़िगर करना, और स्वचालित रूप से त्रुटियों को सुधारने वाली खोज चलाना दिखाएंगे।

## त्वरित उत्तर
- **“वर्तनी सक्षम करने” का क्या अर्थ है?** यह बिल्ट‑इन स्पेल‑चेकर को सक्रिय करता है जो खोज के दौरान उपयोगकर्ता की टाइपो को सुधारता है।  
- **कौन सी लाइब्रेरी यह सुविधा प्रदान करती है?** GroupDocs.Search for Java।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल लाइसेंस काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं सहनशीलता को नियंत्रित कर सकता हूँ?** हाँ – `setMaxMistakeCount` का उपयोग करके आप कितनी टाइपो की अनुमति देना चाहते हैं, निर्धारित कर सकते हैं।  
- **क्या यह बड़े इंडेक्स के लिए उपयुक्त है?** बिल्कुल – इंजन उच्च‑प्रदर्शन इंडेक्सिंग और सर्च के लिए अनुकूलित है।

## GroupDocs.Search में “वर्तनी सक्षम करने” क्या है?
वर्तनी को सक्षम करने से सर्च इंजन को त्रुटिपूर्ण क्वेरी में सबसे निकटतम सही शब्द खोजने की अनुमति मिलती है। यह सुविधा उपयोगकर्ता अनुभव को काफी बेहतर बनाती है, क्योंकि गलत वर्तनी वाले इनपुट पर भी प्रासंगिक परिणाम मिलते हैं।

## Java एप्लिकेशन में वर्तनी सुधार को क्यों सक्षम करें?
- **उपयोगकर्ता संतुष्टि बढ़ती है** – उपयोगकर्ताओं को पूरी तरह सही टाइप करने की जरूरत नहीं।  
- **बाउंस रेट कम होता है** – अधिक सटीक परिणाम विज़िटर को व्यस्त रखते हैं।  
- **विभिन्न डोमेनों में काम करता है** – लाइब्रेरी कैटलॉग से लेकर ई‑कॉमर्स प्रोडक्ट सर्च तक।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) स्थापित हो।  
- बेसिक Java और Maven का ज्ञान।  
- इंडेक्सिंग अवधारणाओं की समझ।  
- GroupDocs.Search का ट्रायल या लाइसेंस्ड की।

### Java के लिए GroupDocs.Search सेट अप करना
अपने Maven प्रोजेक्ट में लाइब्रेरी को इंटीग्रेट करें।

**Maven सेटअप**  
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

**डायरेक्ट डाउनलोड**  
वैकल्पिक रूप से, नवीनतम संस्करण [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से डाउनलोड करें।

### लाइसेंस प्राप्त करना
मूल्यांकन के लिए एक फ्री ट्रायल लाइसेंस प्राप्त करें। उत्पादन उपयोग के लिए पूर्ण लाइसेंस खरीदें या आधिकारिक साइट से अस्थायी कुंजी अनुरोध करें।

## इंडेक्स में दस्तावेज़ कैसे जोड़ें
इंडेक्स बनाना किसी भी सर्च‑सक्षम एप्लिकेशन की नींव है। नीचे एक न्यूनतम उदाहरण है जो **फ़ोल्डर से दस्तावेज़ों को इंडेक्स में जोड़ता** है।

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

*टिप:* सुनिश्चित करें कि पाथ सही हैं और एप्लिकेशन को इंडेक्स फ़ोल्डर पर लिखने की अनुमति है।

## वर्तनी सुधार को कॉन्फ़िगर करना (अधिकतम त्रुटि संख्या सेट करें)
स्पेल‑चेकर को सक्षम करके और त्रुटियों के लिए सहनशीलता सेट करके आप इसे फाइन‑ट्यून कर सकते हैं।

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

*`setMaxMistakeCount` क्यों महत्वपूर्ण है:* यह निर्धारित करता है कि इंजन कितनी टाइपो को सहन करेगा। अपने डोमेन के सामान्य त्रुटि पैटर्न के आधार पर इस मान को समायोजित करें।

## वर्तनी‑सुधारित खोज कैसे करें
इंडेक्स तैयार और वर्तनी विकल्प कॉन्फ़िगर होने के बाद, ऐसी क्वेरी चलाएँ जिसमें त्रुटियाँ हो सकती हैं।

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

`search()` कॉल एक `SearchResult` लौटाता है जिसमें सुधारे गए शब्द और सबसे प्रासंगिक दस्तावेज़ शामिल होते हैं।

## व्यावहारिक अनुप्रयोग
1. **लाइब्रेरी सिस्टम:** पुस्तक शीर्षक या लेखक नाम में टाइपो को सुधारें।  
2. **ई‑कॉमर्स प्लेटफ़ॉर्म:** उत्पाद खोज में उपयोगकर्ता की टाइपो को ठीक करके रूपांतरण बढ़ाएँ।  
3. **कंटेंट मैनेजमेंट सिस्टम:** संपादकीय स्टाफ के लिए लेख पुनर्प्राप्ति को बेहतर बनाएं।

## प्रदर्शन संबंधी विचार
- **इंडेक्स को अद्यतन रखें** – नई या बदलती फ़ाइलों को नियमित रूप से पुनः‑इंडेक्स करें।  
- **JVM मेमोरी सेटिंग्स ट्यून करें** – बड़े इंडेक्स के लिए पर्याप्त हीप आवंटित करें।  
- **संसाधन उपयोग की निगरानी करें** – आवश्यक होने पर गार्बेज‑कलेक्टर फ़्लैग्स समायोजित करें।

## सामान्य समस्याएँ एवं ट्रबलशूटिंग
| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| वर्तनी सक्षम करने के बाद कोई परिणाम नहीं मिल रहा | इंडेक्स फ़ोल्डर पाथ गलत या खाली है | सुनिश्चित करें `indexFolder` वैध इंडेक्स की ओर इशारा कर रहा है और `index.add()` सफल हुआ है |
| स्पेल‑चेकर स्पष्ट टाइपो को नहीं सुधार रहा | `setMaxMistakeCount` बहुत कम सेट है | अधिक सहनशीलता के लिए काउंट को 2 या 3 तक बढ़ाएँ |
| बड़े दस्तावेज़ सेट पर एप्लिकेशन क्रैश हो रहा है | JVM हीप अपर्याप्त है | `-Xmx` विकल्प बढ़ाएँ (उदा., `-Xmx4g`) |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: GroupDocs.Search क्या है?**  
**उत्तर:** यह एक Java लाइब्रेरी है जो तेज़ इंडेक्सिंग, उन्नत खोज सुविधाएँ, और बिल्ट‑इन वर्तनी सुधार प्रदान करती है।

**प्रश्न: मैं GroupDocs.Search के लिए लाइसेंस कैसे प्राप्त करूँ?**  
**उत्तर:** आधिकारिक साइट पर जाकर फ्री ट्रायल डाउनलोड करें या पूर्ण लाइसेंस खरीदें।

**प्रश्न: क्या मैं GroupDocs.Search को अन्य Java फ्रेमवर्क के साथ इंटीग्रेट कर सकता हूँ?**  
**उत्तर:** हाँ, यह Spring, Jakarta EE, और किसी भी मानक Java एप्लिकेशन के साथ काम करता है।

**प्रश्न: इंडेक्स सेट अप करते समय आम समस्याएँ क्या हैं?**  
**उत्तर:** गलत फ़ोल्डर पाथ, अपर्याप्त फ़ाइल अनुमतियाँ, या `pom.xml` में डिपेंडेंसी की कमी।

**प्रश्न: स्पेल‑करेक्शन खोज परिणामों को कैसे बेहतर बनाता है?**  
**उत्तर:** यह स्वचालित रूप से गलत वर्तनी वाले क्वेरी को सबसे निकटतम सही शब्दों में बदल देता है, जिससे अधिक प्रासंगिक हिट्स मिलते हैं।

## अतिरिक्त संसाधन
- [Documentation](https://docs.groupdocs.com/search/java/)  
- [API Reference](https://reference.groupdocs.com/search/java)  
- [Download](https://releases.groupdocs.com/search/java/)  
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**अंतिम अपडेट:** 2026-02-21  
**परीक्षित संस्करण:** GroupDocs.Search 25.4  
**लेखक:** GroupDocs
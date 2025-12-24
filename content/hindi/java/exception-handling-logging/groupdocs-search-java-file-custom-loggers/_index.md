---
date: '2025-12-24'
description: GroupDocs.Search for Java के साथ लॉग फ़ाइल का आकार सीमित करना और कंसोल
  लॉगर जावा का उपयोग करना सीखें। यह गाइड लॉगिंग कॉन्फ़िगरेशन, समस्या निवारण टिप्स,
  और प्रदर्शन अनुकूलन को कवर करता है।
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: GroupDocs.Search Java लॉगर्स के साथ लॉग फ़ाइल का आकार सीमित करें
type: docs
url: /hi/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search Java लॉगर्स के साथ लॉग फ़ाइल आकार सीमित करें

बड़ी दस्तावेज़ संग्रहों को प्रबंधित करते समय प्रभावी लॉगिंग आवश्यक है, विशेष रूप से जब आपको **लॉग फ़ाइल आकार सीमित** करना हो ताकि स्टोरेज नियंत्रण में रहे। **GroupDocs.Search for Java** अपनी शक्तिशाली खोज क्षमताओं के माध्यम से लॉग को संभालने के लिए मजबूत समाधान प्रदान करता है। यह ट्यूटोरियल आपको GroupDocs.Search का उपयोग करके फ़ाइल और कस्टम लॉगर्स को लागू करने में मार्गदर्शन करता है, जिससे आपके एप्लिकेशन की इवेंट ट्रैकिंग और डिबगिंग क्षमता बढ़ती है।

## Quick Answers
- **“limit log file size” का क्या अर्थ है?** यह लॉग फ़ाइल के अधिकतम आकार को सीमित करता है, जिससे डिस्क पर अनियंत्रित वृद्धि नहीं होती।  
- **कौन सा लॉगर आपको लॉग फ़ाइल आकार सीमित करने देता है?** बिल्ट‑इन `FileLogger` एक अधिकतम आकार पैरामीटर स्वीकार करता है।  
- **मैं console logger java का उपयोग कैसे करूँ?** `ConsoleLogger` का इंस्टैंस बनाएँ और इसे `IndexSettings` पर सेट करें।  
- **क्या GroupDocs.Search के लिए लाइसेंस आवश्यक है?** मूल्यांकन के लिए ट्रायल काम करता है; उत्पादन के लिए व्यावसायिक लाइसेंस आवश्यक है।  
- **पहला कदम क्या है?** अपने Maven प्रोजेक्ट में GroupDocs.Search डिपेंडेंसी जोड़ें।

## What is limit log file size?
लॉग फ़ाइल आकार को सीमित करने का अर्थ है लॉगर को इस प्रकार कॉन्फ़िगर करना कि जब फ़ाइल एक पूर्वनिर्धारित सीमा (जैसे, 4 MB) तक पहुँच जाए, तो वह बढ़ना बंद कर दे या रोल ओवर हो जाए। इससे आपके एप्लिकेशन की स्टोरेज फ़ुटप्रिंट पूर्वानुमानित रहती है और प्रदर्शन में गिरावट से बचा जा सकता है।

## Why use file and custom loggers with GroupDocs.Search?
- **ऑडिटेबिलिटी:** इंडेक्सिंग और सर्च इवेंट्स का स्थायी रिकॉर्ड रखें।  
- **डिबगिंग:** संक्षिप्त लॉग की समीक्षा करके समस्याओं को जल्दी पहचानें।  
- **लचीलापन:** स्थायी फ़ाइल लॉग और त्वरित कंसोल आउटुट (`use console logger java`) में से चुनें।  

## Prerequisites
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 या नया, IDE (IntelliJ IDEA, Eclipse, आदि)।  
- बुनियादी Java और Maven ज्ञान।  

## Setting Up GroupDocs.Search for Java

नीचे दिए गए तरीकों में से किसी एक का उपयोग करके लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें।

**Maven Setup:**

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

**Direct Download:**  
आधिकारिक साइट से नवीनतम JAR डाउनलोड करें: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)।

### License Acquisition
ट्रायल प्राप्त करें या [licensing page](https://purchase.groupdocs.com/temporary-license/) के माध्यम से लाइसेंस खरीदें।

## How to limit log file size with File Logger
नीचे चरण‑दर‑चरण गाइड दिया गया है जो दिखाता है कि `FileLogger` को कैसे कॉन्फ़िगर करें ताकि लॉग फ़ाइल आपके निर्दिष्ट आकार से कभी अधिक न हो।

### 1️⃣ Import Necessary Packages
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Set Up Index Settings with File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Create or Load the Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Add Documents to the Index
```java
index.add(documentsFolder);
```

### 5️⃣ Perform a Search Query
```java
SearchResult result = index.search(query);
```

**मुख्य बिंदु:** `FileLogger` कंस्ट्रक्टर का दूसरा आर्ग्यूमेंट (`4.0`) मेगाबाइट में अधिकतम लॉग फ़ाइल आकार निर्धारित करता है, जो सीधे **limit log file size** आवश्यकता को पूरा करता है।

## How to use console logger java
यदि आप टर्मिनल में तुरंत फीडबैक चाहते हैं, तो फ़ाइल लॉगर को कंसोल लॉगर से बदलें।

### 1️⃣ Import the Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Set Up Index Settings with Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Create or Load the Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Add Documents and Perform a Search
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**टिप:** कंसोल लॉगर विकास के दौरान आदर्श है क्योंकि यह प्रत्येक लॉग एंट्री को तुरंत प्रिंट करता है, जिससे आप यह सत्यापित कर सकते हैं कि इंडेक्सिंग और सर्चिंग अपेक्षित रूप से कार्य कर रहे हैं।

## Practical Applications
- **डॉक्यूमेंट मैनेजमेंट सिस्टम:** प्रत्येक इंडेक्स किए गए दस्तावेज़ का ऑडिट ट्रेल रखें।  
- **एंटरप्राइज़ सर्च इंजन:** क्वेरी प्रदर्शन और त्रुटि दरों को रियल‑टाइम में मॉनिटर करें।  
- **लीगल एवं कंप्लायंस सॉफ्टवेयर:** नियामक रिपोर्टिंग के लिए सर्च टर्म्स रिकॉर्ड करें।  

## Performance Considerations
- **लॉग आकार:** लॉग फ़ाइल आकार सीमित करके आप अत्यधिक डिस्क उपयोग से बचते हैं जो आपके एप्लिकेशन को धीमा कर सकता है।  
- **असिंक्रोनस लॉगिंग:** यदि आपको उच्च थ्रूपुट चाहिए, तो लॉगर को असिंक्रोनस कतार में रैप करने पर विचार करें (इस गाइड के दायरे से बाहर)।  
- **मेमोरी मैनेजमेंट:** जब बड़े `Index` ऑब्जेक्ट्स की आवश्यकता न रहे तो उन्हें रिलीज़ करें ताकि JVM फ़ुटप्रिंट कम रहे।  

## Common Issues & Solutions
- **लॉग पाथ उपलब्ध नहीं:** सुनिश्चित करें कि डायरेक्टरी मौजूद है और एप्लिकेशन को लिखने की अनुमति है।  
- **लॉगर फायर नहीं हो रहा:** `Index` ऑब्जेक्ट बनाने *से पहले* `settings.setLogger(...)` कॉल करें।  
- **कंसोल आउटपुट नहीं दिख रहा:** पुष्टि करें कि आप एप्लिकेशन को ऐसे टर्मिनल में चला रहे हैं जो `System.out` दिखाता है।  

## Frequently Asked Questions

**Q: `FileLogger` के दूसरे पैरामीटर का क्या नियंत्रण है?**  
A: यह लॉग फ़ाइल का अधिकतम आकार मेगाबाइट में सेट करता है, जिससे आप लॉग फ़ाइल आकार सीमित कर सकते हैं।

**Q: क्या मैं फ़ाइल और कंसोल लॉगर्स को संयोजित कर सकता हूँ?**  
A: हाँ, एक कस्टम लॉगर बनाकर जो संदेशों को दोनों गंतव्यों पर फॉरवर्ड करता है।

**Q: प्रारंभिक निर्माण के बाद इंडेक्स में दस्तावेज़ कैसे जोड़ें?**  
A: किसी भी समय `index.add(pathToNewDocs)` कॉल करें; लॉगर ऑपरेशन को रिकॉर्ड करेगा।

**Q: क्या `ConsoleLogger` थ्रेड‑सेफ़ है?**  
A: यह सीधे `System.out` में लिखता है, जिसे JVM द्वारा सिंक्रनाइज़ किया गया है, इसलिए अधिकांश उपयोग मामलों में यह सुरक्षित है।

**Q: क्या लॉग फ़ाइल आकार सीमित करने से संग्रहीत जानकारी की मात्रा प्रभावित होगी?**  
A: जब आकार सीमा पहुँच जाती है, तो नई एंट्रीज़ को त्यागा जा सकता है या फ़ाइल रोल ओवर हो सकती है, यह लॉगर इम्प्लीमेंटेशन पर निर्भर करता है।

## Resources
- [डॉक्यूमेंटेशन](https://docs.groupdocs.com/search/java/)
- [API रेफ़रेंस](https://reference.groupdocs.com/search/java/)

---

**अंतिम अद्यतन:** 2025-12-24  
**परीक्षित संस्करण:** GroupDocs.Search for Java 25.4  
**लेखक:** GroupDocs
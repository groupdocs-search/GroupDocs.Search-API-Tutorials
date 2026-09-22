---
date: '2026-09-21'
description: GroupDocs.Search for Java में लॉगर बनाना, अधिकतम लॉग आकार सेट करना और
  कंसोल लॉगर का उपयोग करना सीखें।
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: GroupDocs.Search for Java में लॉगर बनाना, अधिकतम लॉग आकार सेट करना
  और कंसोल लॉगर का उपयोग करना सीखें। चरण‑दर‑चरण निर्देश और सर्वोत्तम‑प्रैक्टिस टिप्स
  का पालन करें।
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: GroupDocs.Search में लॉगर कैसे बनाएं और लॉग आकार सीमित करें
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: GroupDocs.Search for Java में लॉगर कैसे बनाएं और लॉग आकार सीमित करें
type: docs
url: /hi/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search for Java में लॉगर कैसे बनाएं और लॉग फ़ाइल आकार को सीमित करें

इस ट्यूटोरियल में आप GroupDocs.Search के लिए **लॉगर कैसे बनाएं** कार्यान्वयन, अधिकतम लॉग फ़ाइल आकार को कॉन्फ़िगर करना, और फ़ाइल‑आधारित तथा कंसोल लॉगिंग के बीच स्विच करना सीखेंगे। उचित लॉग प्रबंधन बड़े इंडेक्सिंग कार्यों के दौरान डिस्क भरने से रोकता है, समस्या निवारण में सुधार करता है, और विकास के दौरान त्वरित प्रतिक्रिया देता है। हम Maven सेटअप से शुरू करेंगे, लॉगर कॉन्फ़िगरेशन को चरण‑दर‑चरण देखेंगे, और एक सरल सर्च क्वेरी के साथ समाप्त करेंगे जो कार्रवाई में लॉगर को दर्शाता है।

## त्वरित उत्तर
- **“limit log file size” क्या मतलब है?** यह लॉग फ़ाइल के अधिकतम आकार को सीमित करता है, जिससे डिस्क पर अनियंत्रित वृद्धि नहीं होती।  
- **कौन सा लॉगर आपको लॉग फ़ाइल आकार सीमित करने देता है?** बिल्ट‑इन `FileLogger` एक अधिकतम‑आकार पैरामीटर स्वीकार करता है।  
- **मैं console logger java कैसे उपयोग करूँ?** `ConsoleLogger` को इंस्टैंसिएट करें और इसे `IndexSettings` पर सेट करें।  
- **क्या मुझे GroupDocs.Search के लिए लाइसेंस चाहिए?** मूल्यांकन के लिए ट्रायल काम करता है; उत्पादन के लिए व्यावसायिक लाइसेंस आवश्यक है।  
- **पहला कदम क्या है?** अपने Maven प्रोजेक्ट में GroupDocs.Search डिपेंडेंसी जोड़ें।  

## लॉग फ़ाइल आकार को सीमित करना क्या है?
The **limit log file size** सेटिंग लॉगर को बताती है कि फ़ाइल एक निर्धारित सीमा (उदाहरण के लिए, 4 MB) तक पहुँचने पर नई प्रविष्टियाँ लिखना बंद कर दे। जब सीमा पहुँच जाती है, तो लॉगर या तो आगे के संदेशों को त्याग देता है या नई फ़ाइल में रोल ओवर करता है, जिससे डिस्क उपयोग पूर्वानुमानित रहता है।

## GroupDocs.Search के साथ फ़ाइल और कस्टम लॉगर क्यों उपयोग करें?
फ़ाइल और कस्टम लॉगर आपको ऑडिटेबिलिटी, डिबगिंग अंतर्दृष्टि, और लचीलापन प्रदान करते हैं। उत्पादन वातावरण में, फ़ाइल लॉग प्रत्येक इंडेक्सिंग और सर्च ऑपरेशन का स्थायी रिकॉर्ड देते हैं, जबकि कंसोल लॉग विकास के दौरान त्वरित प्रतिक्रिया प्रदान करते हैं। ये लॉग टीमों को प्रदर्शन की निगरानी, त्रुटियों का पता लगाने, और विस्तृत गतिविधि ट्रेल को संरक्षित करके अनुपालन आवश्यकताओं को पूरा करने में मदद करते हैं।

## पूर्वापेक्षाएँ
- GroupDocs.Search for Java ≥ 25.4।  
- JDK 8 या नया, साथ में IntelliJ IDEA या Eclipse जैसा IDE।  
- Maven और Java प्रोग्रामिंग की बुनियादी परिचितता।  

## GroupDocs.Search for Java सेटअप करना

नीचे दिए गए तरीकों में से किसी एक का उपयोग करके लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें।

**Maven सेटअप:**  

```text
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
```

**सीधा डाउनलोड:**  
आधिकारिक साइट से नवीनतम JAR डाउनलोड करें: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### लाइसेंस प्राप्ति
ट्रायल प्राप्त करें या [licensing page](https://purchase.groupdocs.com/temporary-license/) के माध्यम से लाइसेंस खरीदें।

## GroupDocs.Search के लिए कस्टम लॉगर कैसे बनाएं
कस्टम लॉगर बनाना सरल है क्योंकि GroupDocs.Search `ILogger` इंटरफ़ेस पर निर्भर करता है। इस इंटरफ़ेस को लागू करके—या प्रदान किए गए `FileLogger` या `ConsoleLogger` को विस्तारित करके—आप रिमोट फ़ॉरवर्डिंग या लॉग रोटेशन जैसी अतिरिक्त व्यवहार जोड़ सकते हैं। आप प्रारंभिक लॉजिक भी जोड़ सकते हैं, जैसे नेटवर्क कनेक्शन खोलना, और लॉगर के शटडाउन मेथड में संसाधनों को बंद करना सुनिश्चित कर सकते हैं। यह दृष्टिकोण आपको ELK या Splunk जैसे मॉनिटरिंग प्लेटफ़ॉर्म के साथ एकीकृत करने देता है।

### परिभाषा एंकर
`ILogger` GroupDocs.Search में मुख्य लॉगिंग अनुबंध है; कोई भी क्लास जो उसके `log(Level, String)` मेथड को लागू करती है, लॉगर बन सकती है।

### उदाहरण दृष्टिकोण (कोई कोड ब्लॉक नहीं)
1. `ILogger` को लागू करने वाली क्लास बनाएं।  
2. `log` मेथड को ओवरराइड करके संदेशों को अपनी चुनी हुई गंतव्य (फ़ाइल, डेटाबेस, HTTP एन्डपॉइंट) पर लिखें।  
3. इंडेक्स कॉन्फ़िगरेशन में, `settings.setLogger(new YourCustomLogger())` कॉल करें।  

## File Logger के साथ लॉग फ़ाइल आकार को कैसे सीमित करें
`FileLogger` क्लास लॉग प्रविष्टियों को डिस्क पर फ़ाइल में लिखता है और अधिकतम आकार तर्क स्वीकार करता है। आकार सीमा निर्दिष्ट करके, लॉगर स्वचालित रूप से नई प्रविष्टियों को जोड़ना बंद कर देता है या सीमा पहुँचने पर नई फ़ाइल बनाता है, जिससे अनियंत्रित डिस्क वृद्धि नहीं होती। यह व्यवहार सुनिश्चित करता है कि लॉगिंग इंडेक्सिंग प्रदर्शन में बाधा न डाले और घटनाओं का संक्षिप्त रिकॉर्ड रखे।

### परिभाषा एंकर
`FileLogger` एक बिल्ट‑इन लॉगर है जो संदेशों को टेक्स्ट फ़ाइल में सहेजता है और कॉन्फ़िगर करने योग्य अधिकतम फ़ाइल आकार का समर्थन करता है।

### चरण‑दर‑चरण गाइड
1️⃣ **आवश्यक पैकेज इम्पोर्ट करें**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **File Logger के साथ इंडेक्स सेटिंग्स सेट करें**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **इंडेक्स बनाएं या लोड करें**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **इंडेक्स में दस्तावेज़ जोड़ें**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **एक सर्च क्वेरी निष्पादित करें**  
```text
```java
SearchResult result = index.search(query);
```
```

**मुख्य बिंदु:** `FileLogger` कंस्ट्रक्टर का दूसरा तर्क (`4.0`) मेगाबाइट में **set max log size** को परिभाषित करता है, जो सीधे **limit log file size** आवश्यकता को संबोधित करता है।

## console logger java कैसे उपयोग करें
जब आपको लॉग इवेंट्स की त्वरित दृश्यता चाहिए, तो `ConsoleLogger` प्रत्येक संदेश को `System.out` पर लिखता है। यह लॉगर हल्का और थ्रेड‑सेफ है, जिससे यह विकास और डिबगिंग सत्रों के लिए उपयुक्त है। यह इंडेक्सिंग प्रगति, सर्च क्वेरी, और त्रुटि स्थितियों पर तुरंत प्रतिक्रिया प्रदान करता है, बिना फ़ाइल I/O की आवश्यकता के, जिससे आवर्ती परीक्षण तेज़ हो सकता है।

### परिभाषा एंकर
`ConsoleLogger` एक हल्का लॉगर है जो लॉग प्रविष्टियों को मानक कंसोल स्ट्रीम पर आउटपुट करता है, जिससे यह डिबगिंग सत्रों के लिए आदर्श बनता है।

### कॉन्फ़िगरेशन चरण
1️⃣ **कंसोल लॉगर इम्पोर्ट करें**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Console Logger के साथ इंडेक्स सेटिंग्स सेट करें**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **इंडेक्स बनाएं या लोड करें**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **दस्तावेज़ जोड़ें और सर्च निष्पादित करें**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**टिप:** कंसोल लॉगर विकास के दौरान आदर्श है क्योंकि यह प्रत्येक लॉग प्रव entry को तुरंत प्रिंट करता है, जिससे आप सत्यापित कर सकते हैं कि इंडेक्सिंग और सर्च अपेक्षित रूप से कार्य कर रहे हैं।

## व्यावहारिक अनुप्रयोग
1. **डॉक्यूमेंट मैनेजमेंट सिस्टम:** प्रत्येक इंडेक्स किए गए दस्तावेज़ का ऑडिट ट्रेल रखें, जिससे अनुपालन आवश्यकताओं को पूरा किया जा सके।  
2. **एंटरप्राइज़ सर्च इंजन:** रीयल‑टाइम में क्वेरी प्रदर्शन और त्रुटि दरों की निगरानी करें, जिससे तेज़ SLA अनुपालन जांच संभव हो।  
3. **लीगल एवं अनुपालन सॉफ़्टवेयर:** नियामक रिपोर्टिंग के लिए सर्च टर्म और टाइमस्टैम्प रिकॉर्ड करें, और लॉग को निर्धारित रखरखाव अवधि तक बनाए रखें।  

## प्रदर्शन संबंधी विचार
- **लॉग आकार:** **set max log size** द्वारा, आप अत्यधिक डिस्क उपयोग से बचते हैं जो अन्यथा JVM के गार्बेज कलेक्टर को धीमा कर सकता है।  
- **असिंक्रोनस लॉगिंग:** उच्च‑थ्रूपुट परिदृश्यों के लिए, अपने लॉगर को असिंक्रोनस कतार में रैप करें ताकि I/O को इंडेक्सिंग थ्रेड से अलग किया जा सके (इस गाइड के दायरे से बाहर)।  
- **मेमोरी प्रबंधन:** जब बड़े `Index` ऑब्जेक्ट की आवश्यकता न रहे, तो `index.close()` के साथ उन्हें रिलीज़ करें ताकि JVM का फुटप्रिंट कम रहे।  

## सामान्य समस्याएँ एवं समाधान
- **लॉग पाथ उपलब्ध नहीं:** सुनिश्चित करें कि डायरेक्टरी मौजूद है और एप्लिकेशन के पास JVM चलाने वाले उपयोगकर्ता खाते के लिए लिखने की अनुमति है।  
- **लॉगर नहीं चल रहा:** `Index` ऑब्जेक्ट बनाने *से पहले* `settings.setLogger(...)` कॉल करें; अन्यथा डिफ़ॉल्ट लॉगर उपयोग होगा।  
- **कंसोल आउटपुट नहीं दिख रहा:** सुनिश्चित करें कि आप एप्लिकेशन को ऐसे टर्मिनल में चला रहे हैं जो `System.out` दिखाता है, और कोई लॉगिंग फ्रेमवर्क (जैसे SLF4J) आउटपुट को इंटरसेप्ट नहीं कर रहा है।  

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: `FileLogger` के दूसरे पैरामीटर का नियंत्रण क्या है?**  
उत्तर: यह लॉग फ़ाइल का अधिकतम आकार मेगाबाइट में सेट करता है, जिससे आप **set max log size** कर सकते हैं और अनियंत्रित वृद्धि को रोक सकते हैं।

**प्रश्न: क्या मैं फ़ाइल और कंसोल लॉगर को संयोजित कर सकता हूँ?**  
उत्तर: हाँ। एक कस्टम लॉगर बनाएं जो प्रत्येक `log` कॉल को दोनों `FileLogger` और `ConsoleLogger` को फॉरवर्ड करे, फिर उस कॉम्पोजिट लॉगर को `IndexSettings` के साथ रजिस्टर करें।

**प्रश्न: प्रारंभिक निर्माण के बाद इंडेक्स में दस्तावेज़ कैसे जोड़ें?**  
उत्तर: कभी भी `index.add(pathToNewDocs)` कॉल करें; कॉन्फ़िगर किया गया लॉगर स्वचालित रूप से जोड़ने को रिकॉर्ड करेगा।

**प्रश्न: क्या `ConsoleLogger` थ्रेड‑सेफ़ है?**  
उत्तर: यह सीधे `System.out` पर लिखता है, जिसे JVM आंतरिक रूप से सिंक्रनाइज़ करता है, जिससे यह सामान्य मल्टी‑थ्रेडेड उपयोग मामलों के लिए सुरक्षित है।

**प्रश्न: क्या लॉग फ़ाइल आकार को सीमित करने से संग्रहीत जानकारी की मात्रा प्रभावित होगी?**  
उत्तर: एक बार आकार सीमा पहुँचने पर, नई प्रविष्टियों को या तो त्याग दिया जाता है या लॉगर नई फ़ाइल में रोल ओवर करता है, यह आपके द्वारा चुनी गई कार्यान्वयन पर निर्भर करता है।

## संसाधन
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**अंतिम अपडेट:** 2026-09-21  
**परीक्षण किया गया:** GroupDocs.Search for Java 25.4  
**लेखक:** GroupDocs  

---

## संबंधित ट्यूटोरियल

- [लॉगिंग कैसे लागू करें - एक्सेप्शन हैंडलिंग और लॉगिंग ट्यूटोरियल्स for GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [GroupDocs.Search के साथ जावा में असिंक्रोनस लॉगिंग लागू करें – कस्टम लॉगर गाइड](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [जावा में सर्च इंडेक्स बनाएं – GroupDocs.Search ट्यूटोरियल्स](/search/java/indexing/)
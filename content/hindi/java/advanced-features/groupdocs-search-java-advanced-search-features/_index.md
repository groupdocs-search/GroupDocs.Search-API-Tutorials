---
date: '2025-12-16'
description: GroupDocs.Search for Java का उपयोग करके डेट रेंज सर्च और फेसेटेड सर्च
  जैसी अन्य उन्नत खोज सुविधाओं को कैसे लागू करें, साथ ही त्रुटि संभालना और प्रदर्शन
  अनुकूलन सीखें।
keywords:
- GroupDocs.Search Java
- advanced search features Java
- Java indexing errors
title: 'GroupDocs.Search Java - तारीख सीमा खोज और उन्नत सुविधाएँ'
type: docs
url: /hi/java/advanced-features/groupdocs-search-java-advanced-search-features/
weight: 1
---

# GroupDocs.Search Java में महारत: डेट रेंज सर्च और उन्नत सुविधाएँ

आज के डेटा‑ड्रिवन एप्लिकेशन्स में, **date range search** एक मुख्य क्षमता है जो आपको समय अवधि के आधार पर दस्तावेज़ों को फ़िल्टर करने की अनुमति देती है, जिससे प्रासंगिकता और गति में उल्लेखनीय सुधार होता है। चाहे आप एक अनुपालन पोर्टल, एक ई‑कॉमर्स कैटलॉग, या एक कंटेंट‑मैनेजमेंट सिस्टम बना रहे हों, date range search को अन्य शक्तिशाली क्वेरी प्रकारों के साथ महारत हासिल करने से आपका समाधान लचीला और मजबूत दोनों बन जाएगा। यह गाइड आपको एरर हैंडलिंग, विभिन्न क्वेरी प्रकारों और प्रदर्शन टिप्स के माध्यम से ले जाता है, सभी वास्तविक Java कोड के साथ जिसे आप कॉपी‑पेस्ट कर सकते हैं।

## त्वरित उत्तर
- **date range search क्या है?** निर्दिष्ट प्रारंभ‑से‑समाप्त अंतराल के भीतर तिथियों वाले दस्तावेज़ों को फ़िल्टर करना।  
- **कौन सी लाइब्रेरी यह प्रदान करती है?** GroupDocs.Search for Java.  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक मुफ्त ट्रायल काम करता है; व्यावसायिक उपयोग के लिए एक प्रोडक्शन लाइसेंस आवश्यक है।  
- **क्या मैं इसे अन्य क्वेरीज़ के साथ मिला सकता हूँ?** हाँ—date ranges को boolean, faceted, या regex क्वेरीज़ के साथ मिलाएँ।  
- **क्या यह बड़े डेटासेट्स के लिए तेज़ है?** सही तरीके से इंडेक्स किए जाने पर, सर्च मिलियन रिकॉर्ड्स पर भी सब‑सेकंड समय में चलती है।

## date range search क्या है?
date range search आपको उन दस्तावेज़ों को खोजने में मदद करता है जिनमें दो सीमाओं के बीच की तिथियां होती हैं, जैसे “2023‑01‑01 ~~ 2023‑12‑31”. यह रिपोर्ट, ऑडिट लॉग, और किसी भी स्थिति में आवश्यक है जहाँ समय‑आधारित फ़िल्टरिंग महत्वपूर्ण होती है।

## GroupDocs.Search for Java का उपयोग क्यों करें?
GroupDocs.Search कई क्वेरी प्रकारों—simple, wildcard, faceted, numeric, date range, regex, boolean, और phrase—के लिए एकीकृत API प्रदान करता है, जिससे आप कई लाइब्रेरीज़ को संभाले बिना परिष्कृत सर्च अनुभव बना सकते हैं। इसका इवेंट‑ड्रिवन एरर हैंडलिंग भी आपके इंडेक्सिंग पाइपलाइन को लचीला बनाता है।

## पूर्वापेक्षाएँ
- **GroupDocs.Search Java library** (v25.4 या नया)।  
- **Java Development Kit (JDK)** आपके प्रोजेक्ट के साथ संगत।  
- निर्भरता प्रबंधन के लिए Maven (या मैन्युअल डाउनलोड)।

### आवश्यक लाइब्रेरी और पर्यावरण सेटअप
अपने `pom.xml` में GroupDocs रिपॉजिटरी और डिपेंडेंसी जोड़ें:

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

### वैकल्पिक सेटअप
डायरेक्ट डाउनलोड के लिए, देखें [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### लाइसेंसिंग और प्रारंभिक सेटअप
एक मुफ्त ट्रायल या अस्थायी लाइसेंस से शुरू करें:
- विवरण के लिए देखें [GroupDocs License Options](https://purchase.groupdocs.com/temporary-license/)।

अब चलिए वह इंडेक्स फ़ोल्डर बनाते हैं जो आपके सर्चेबल डेटा को रखेगा।

## GroupDocs.Search for Java सेटअप करना

### बेसिक इनिशियलाइज़ेशन
पहले, एक `Index` ऑब्जेक्ट बनाएं जो डिस्क पर एक फ़ोल्डर की ओर इशारा करता है:

```java
import com.groupdocs.search.*;

// Initialize Index
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\BasicUsage\\BuildSearchQuery";
Index index = new Index(indexFolder);
```

अब आपके पास सभी सर्च ऑपरेशन्स के लिए एक गेटवे है।

## इम्प्लीमेंटेशन गाइड

### फीचर 1: इंडेक्सिंग में एरर हैंडलिंग
#### इंडेक्सिंग एरर को कैसे कैप्चर करें (Java)

```java
import com.groupdocs.search.events.*;

index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
    @Override
    public void invoke(Object sender, IndexErrorEventArgs args) {
        System.out.println(args.getMessage()); // Output the error message
    }
});

// Add documents to the index
index.add("YOUR_DOCUMENT_DIRECTORY");
```

*क्यों महत्वपूर्ण है*: `ErrorOccurred` को सुनकर, आप समस्याओं को लॉग कर सकते हैं, फेल हुए फ़ाइलों को रीट्राई कर सकते हैं, या उपयोगकर्ताओं को अलर्ट कर सकते हैं बिना पूरे प्रोसेस को क्रैश किए।

### फीचर 2: सिम्पल सर्च क्वेरी
#### सिम्पल सर्च क्या है?

```java
import com.groupdocs.search.*;

String query = "volutpat";
SearchResult result = index.search(query);
```

*परिणाम*: वह सभी दस्तावेज़ लौटाता है जिनमें शब्द **volutpat** शामिल है।

### फीचर 3: वाइल्डकार्ड सर्च क्वेरी
#### वाइल्डकार्ड सर्च कैसे काम करता है?

```java
String query = "?ffect";
SearchResult result = index.search(query);
```

*परिणाम*: **affect** और **effect** दोनों से मेल खाता है, जो `?` प्लेसहोल्डर की शक्ति दर्शाता है।

### फीचर 4: फेसेटेड सर्च क्वेरी
#### Java में फेसेटेड सर्च कैसे करें

```java
String query = "Content: magna";
SearchResult result = index.search(query);
```

*परिणाम*: सर्च को **Content** फ़ील्ड तक सीमित करता है, जो श्रेणी या लेखक जैसे मेटाडाटा द्वारा फ़िल्टर करने के लिए आदर्श है।

### फीचर 5: न्यूमेरिक रेंज सर्च क्वेरी
#### न्यूमेरिक रेंज कैसे सर्च करें

```java
String query = "2000 ~~ 3000";
SearchResult result = index.search(query);
```

*परिणाम*: उन दस्तावेज़ों को प्राप्त करता है जहाँ संख्यात्मक मान 2000 और 3000 के बीच होते हैं।

### फीचर 6: डेट रेंज सर्च क्वेरी
#### डेट रेंज सर्च कैसे निष्पादित करें

```java
import com.groupdocs.search.options.*;
import java.util.*;

String query = "daterange(2000-01-01 ~~ 2001-06-15)";
SearchOptions options = new SearchOptions();

options.getDateFormats().clear();
DateFormatElement[] elements = {
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

SearchResult result = index.search(query, options);
```

*व्याख्या*: `SearchOptions` को कस्टमाइज़ करके, आप इंजन को **MM/DD/YYYY** फॉर्मेट में तिथियों को पहचानने के लिए कहते हैं, फिर 1 जनवरी 2000 से 15 जून 2001 के बीच सभी रिकॉर्ड्स को प्राप्त करते हैं।

### फीचर 7: रेगुलर एक्सप्रेशन सर्च क्वेरी
#### Java में रेगेक्स सर्च कैसे चलाएँ

```java
String query = "^(.)\\1{2,}";
SearchResult result = index.search(query);
```

*परिणाम*: तीन या अधिक समान अक्षरों की श्रृंखला खोजता है (जैसे “aaa”, “111”).

### फीचर 8: बूलियन सर्च क्वेरी
#### Java में बूलियन सर्च के साथ शर्तों को कैसे मिलाएँ

```java
String query = "justo AND NOT 3456";
SearchResult result = index.search(query);
```

*परिणाम*: उन दस्तावेज़ों को लौटाता है जिनमें **justo** है लेकिन उन सभी को बाहर रखता है जिनमें **3456** भी है।

### फीचर 9: कॉम्प्लेक्स बूलियन सर्च क्वेरी
#### उन्नत बूलियन क्वेरी कैसे बनाएँ

```java
String query = "FileName: Engl?(1~3) OR Content: (3456 AND consequat)";
SearchResult result = index.search(query);
```

*परिणाम*: फ़ाइल नामों को “English” के समान खोजता है (1‑3 अक्षर के अंतर की अनुमति) **या** ऐसी सामग्री जो दोनों **3456** और **consequat** शामिल करती है।

### फीचर 10: फ्रेज़ सर्च क्वेरी
#### सटीक वाक्यांश कैसे खोजें

```java
String query = "\"ipsum dolor sit amet\"";
SearchResult result = index.search(query);
```

*परिणाम*: केवल उन दस्तावेज़ों को प्राप्त करता है जिनमें सटीक वाक्यांश **ipsum dolor sit amet** है।

## व्यावहारिक अनुप्रयोग
1. **E‑commerce Platforms** – आकार, रंग और ब्रांड के आधार पर उत्पादों को फ़िल्टर करने के लिए faceted search Java का उपयोग करें।  
2. **Content Management Systems** – उन्नत संपादकीय टूल्स को शक्ति देने के लिए boolean search Java को phrase search के साथ मिलाएँ।  
3. **Data Analysis Tools** – समय‑आधारित रिपोर्ट और डैशबोर्ड बनाने के लिए date range search का उपयोग करें।

## सामान्य समस्याएँ और समाधान
- **date range search के लिए कोई परिणाम नहीं** – सुनिश्चित करें कि आपके दस्तावेज़ों में तिथि फॉर्मेट आपके द्वारा जोड़े गए कस्टम `DateFormat` से मेल खाता है।  
- **Regex क्वेरीज़ बहुत अधिक हिट्स देती हैं** – पैटर्न को परिष्कृत करें या अतिरिक्त फ़ील्ड क्वालिफायर के साथ सर्च स्कोप को सीमित करें।  
- **इंडेक्सिंग एरर कैप्चर नहीं हो रहे** – सुनिश्चित करें कि इवेंट हैंडलर `index.add(...)` को कॉल करने **से पहले** जुड़ा हो।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं date range search को अन्य क्वेरी प्रकारों के साथ मिला सकता हूँ?**  
A: बिल्कुल। आप एक date range क्लॉज़ को बूलियन ऑपरेटर्स, फेसेटेड फ़िल्टर या रेगेक्स पैटर्न के साथ एक ही क्वेरी स्ट्रिंग में मिला सकते हैं।

**Q: तिथि फॉर्मेट बदलने के बाद क्या मुझे इंडेक्स को पुनः बनाना चाहिए?**  
A: हाँ। इंडेक्स टोकनाइज़्ड टर्म्स को संग्रहीत करता है; केवल `SearchOptions` को अपडेट करने से मौजूदा डेटा पुनः‑टोकनाइज़ नहीं होगा। फॉर्मेट बदलने के बाद दस्तावेज़ों को पुनः‑इंडेक्स करें।

**Q: GroupDocs.Search बड़े इंडेक्स को कैसे संभालता है?**  
A: यह इन्क्रीमेंटल इंडेक्सिंग और ऑन‑डिस्क स्टोरेज का उपयोग करता है, जिससे आप मिलियन दस्तावेज़ों तक स्केल कर सकते हैं जबकि मेमोरी उपयोग कम रहता है।

**Q: वाइल्डकार्ड अक्षरों की संख्या पर कोई सीमा है?**  
A: वाइल्डकार्ड को प्रभावी ढंग से प्रोसेस किया जाता है, लेकिन कई लीडिंग वाइल्डकार्ड (जैसे `*term`) का उपयोग प्रदर्शन को घटा सकता है। प्रीफ़िक्स या सफ़िक्स वाइल्डकार्ड को प्राथमिकता दें।

**Q: प्रोडक्शन के लिए कौन सा लाइसेंस मॉडल अनुशंसित है?**  
A: GroupDocs का परपेचुअल या सब्सक्रिप्शन लाइसेंस आपको अपडेट, सपोर्ट और ट्रायल सीमाओं के बिना डिप्लॉय करने की क्षमता देता है।

## निष्कर्ष
**date range search** और GroupDocs.Search for Java द्वारा प्रदान किए गए उन्नत क्वेरी प्रकारों के पूर्ण सेट में महारत हासिल करके, आप अत्यधिक प्रतिक्रियाशील, फीचर‑रिच सर्च अनुभव बना सकते हैं। मजबूत एरर हैंडलिंग लागू करें, अपने इंडेक्स को फाइन‑ट्यून करें, और क्वेरीज़ को मिलाकर लगभग किसी भी रिट्रीवल परिदृश्य को पूरा करें। आज ही प्रयोग शुरू करें और अपने एप्लिकेशन की डेटा‑एक्सेस क्षमताओं को ऊँचा उठाएँ।

---

**अंतिम अपडेट:** 2025-12-16  
**परीक्षित संस्करण:** GroupDocs.Search 25.4 (Java)  
**लेखक:** GroupDocs
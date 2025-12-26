---
date: '2025-12-26'
description: GroupDocs.Search for Java का उपयोग करके दस्तावेज़ों में टेक्स्ट को खोजने
  और हाइलाइट करने के तरीके सीखें। पूर्ण‑दस्तावेज़ और अंश हाइलाइटिंग की तकनीकों का
  अन्वेषण करें।
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: GroupDocs.Search for Java के साथ टेक्स्ट को खोजें और हाइलाइट करें
type: docs
url: /hi/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# GroupDocs.Search for Java का उपयोग करके दस्तावेज़ों में टेक्स्ट खोजें और हाइलाइट करें

आज के डिजिटल युग में, **search and highlight text** को बड़े दस्तावेज़ संग्रह में खोजना एक सामान्य आवश्यकता बन गई है। चाहे आप एक कानूनी रिव्यू टूल, शैक्षणिक शोध पोर्टल, या ग्राहक‑सपोर्ट डैशबोर्ड बना रहे हों, प्रमुख शब्दों को तुरंत खोजने और उन्हें उजागर करने की क्षमता उपयोगिता को काफी बढ़ा देती है। इस व्यापक गाइड में, आप जानेंगे कि **search and highlight text** को GroupDocs.Search for Java के साथ कैसे लागू किया जाए—पूरे दस्तावेज़ के हाइलाइटिंग और फ्रैगमेंट‑लेवल हाइलाइटिंग दोनों को कवर करते हुए।

## Quick Answers
- **What does “search and highlight text” mean?** यह दस्तावेज़ में क्वेरी शब्दों को ढूँढ़ने और उन्हें दृश्य रूप से (जैसे बैकग्राउंड रंग) उजागर करने को कहते हैं।  
- **Which library provides this capability?** GroupDocs.Search for Java।  
- **Do I need a license?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **Can I customize highlight colors?** हाँ—किसी भी RGB रंग को `HighlightOptions` के माध्यम से सेट किया जा सकता है।  
- **Is fragment highlighting supported?** बिल्कुल; आप मैच से पहले/बाद के शब्दों को निर्धारित करके संक्षिप्त स्निपेट बना सकते हैं।

## What Is Search and Highlight Text?
Search and highlight text वह प्रक्रिया है जिसमें किसी क्वेरी के लिए दस्तावेज़ इंडेक्स को स्कैन किया जाता है, मिलते‑जुलते दस्तावेज़ प्राप्त किए जाते हैं, और फिर क्वेरी शब्द की प्रत्येक उपस्थिति को दस्तावेज़ आउटपुट (HTML, PDF, आदि) में चिह्नित किया जाता है। यह दृश्य संकेत उपयोगकर्ताओं को प्रासंगिक जानकारी तुरंत पहचानने में मदद करता है।

## Why Use GroupDocs.Search for Java?
- **High‑performance indexing** के साथ कॉन्फ़िगरेबल कम्प्रेशन।  
- **Rich highlighting API** जो पूरे दस्तावेज़ और कस्टम फ्रैगमेंट दोनों पर काम करता है।  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT, और अधिक)।  
- **Easy Maven integration** और स्पष्ट Java‑centric API।

## Prerequisites
- Java Development Kit (JDK) 8 या नया।  
- निर्भरता प्रबंधन के लिए Maven।  
- IntelliJ IDEA या Eclipse जैसे IDE।  
- Java सिंटैक्स की बुनियादी समझ।

## Setting Up GroupDocs.Search for Java

`pom.xml` में GroupDocs रिपॉजिटरी और डिपेंडेंसी जोड़ें:

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

आप आधिकारिक साइट से नवीनतम JAR भी डाउनलोड कर सकते हैं: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)।

### License Acquisition
फ्री ट्रायल से शुरू करें या मूल्यांकन के लिए एक अस्थायी लाइसेंस प्राप्त करें। उत्पादन परिनियोजन के लिए सभी सुविधाओं को अनलॉक करने हेतु पूर्ण लाइसेंस खरीदें।

## Implementation Guide

इम्प्लीमेंटेशन दो व्यावहारिक भागों में विभाजित है: **पूरे दस्तावेज़ में हाइलाइटिंग** और **फ्रैगमेंट में हाइलाइटिंग**। दोनों भागों में GroupDocs.Search का उपयोग करके **Java दस्तावेज़ों को कैसे हाइलाइट करें** के आवश्यक चरण शामिल हैं।

### Configuring Index Settings
इंडेक्सिंग से पहले, स्टोरेज को हाई कम्प्रेशन पर सेट करें—यह डिस्क उपयोग को कम करता है जबकि सर्च स्पीड बरकरार रखता है।

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Highlighting in Entire Documents

#### Step 1: Create and Populate the Index
एक इंडेक्स फ़ोल्डर बनाएं और सभी स्रोत फ़ाइलें जोड़ें जिन्हें आप सर्च करना चाहते हैं।

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Step 2: Perform Search and Apply Highlighting
शब्द (जैसे `ipsum`) को सर्च करें और हाइलाइटेड मैचों के साथ एक HTML फ़ाइल जनरेट करें।

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Key options explained**
- **Compression** – हाई कम्प्रेशन स्टोरेज बचाता है।  
- **HighlightColor** – किसी भी RGB वैल्यू को आपके UI पैलेट के अनुसार सेट करें।  
- **UseInlineStyles** – `false` सेट करने पर साफ़ HTML बनता है जिसे आप ग्लोबली CSS से स्टाइल कर सकते हैं।

### Highlighting in Fragments

#### Step 1: Index and Search (same as above)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Step 2: Define Fragment Context and Highlight
प्रत्येक फ्रैगमेंट में मैच से पहले और बाद में कितने शब्द दिखाने हैं, यह निर्धारित करें।

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Step 3: Retrieve and Write Highlighted Fragments
जनरेट किए गए फ्रैगमेंट को इकट्ठा करें और उन्हें एक HTML फ़ाइल में लिखें।

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Practical Applications
1. **Legal Document Review** – statutes, clauses, या case references को तुरंत हाइलाइट करें।  
2. **Academic Research** – दर्जनों PDF और Word फ़ाइलों में प्रमुख शब्दावली को उजागर करें।  
3. **Customer Support** – टिकट इतिहास में ऑर्डर नंबर या एरर कोड को pinpoint करें।

## Performance Considerations
- **Index Size** – हाई कम्प्रेशन (`Compression.High`) डिस्क फुटप्रिंट को घटाता है।  
- **Fragment Context** – बड़े `termsBefore/After` मान सटीकता बढ़ाते हैं लेकिन गति पर असर डाल सकते हैं।  
- **Memory Management** – बड़े कॉर्पस को इंडेक्स करते समय JVM हीप मॉनिटर करें; बहुत बड़े सेट के लिए इन्क्रिमेंटल इंडेक्सिंग पर विचार करें।

## Common Issues and Solutions
- **Indexing Errors** – फ़ाइल पाथ की जाँच करें और सुनिश्चित करें कि एप्लिकेशन के पास पढ़ने/लिखने की अनुमति है।  
- **No Highlights Appear** – पुष्टि करें कि `UseInlineStyles` आपके आउटपुट फॉर्मेट (HTML बनाम PDF) से मेल खाता है।  
- **Color Not Applied** – सुनिश्चित करें कि RGB वैल्यू 0‑255 रेंज में हैं और HTML व्यूअर स्टाइल को सपोर्ट करता है।

## Frequently Asked Questions

**Q: What are the benefits of using GroupDocs.Search for Java?**  
A: यह तेज़, स्केलेबल इंडेक्सिंग, कस्टमाइज़ेबल हाइलाइटिंग, और कई दस्तावेज़ फ़ॉर्मेट का समर्थन प्रदान करता है।

**Q: How can I integrate GroupDocs.Search with a REST API?**  
A: Spring Boot कंट्रोलर्स के माध्यम से सर्च और हाइलाइट मेथड्स को एक्सपोज़ करें, और HTML या JSON पेलोड रिटर्न करें।

**Q: Does the library handle password‑protected files?**  
A: हाँ—डॉक्यूमेंट को इंडेक्स में जोड़ते समय पासवर्ड प्रदान करें।

**Q: Can I customize the highlight markup beyond color?**  
A: बिल्कुल; आप `HighlightOptions` के ज़रिए CSS क्लासेज़ इन्जेक्ट कर सकते हैं या जनरेटेड HTML को बाद में मॉडिफ़ाई कर सकते हैं।

**Q: What version was tested for this guide?**  
A: कोड को GroupDocs.Search 25.4 के साथ वैलिडेट किया गया था।

---

**Last Updated:** 2025-12-26  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs
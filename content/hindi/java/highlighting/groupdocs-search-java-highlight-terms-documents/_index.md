---
date: '2026-09-27'
description: GroupDocs.Search for Java का उपयोग करके टेक्स्ट जावा को highlight करना
  सीखें, जिसमें search documents java, index documents java, और fragment highlighting
  शामिल हैं।
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: GroupDocs.Search for Java का उपयोग करके टेक्स्ट जावा को highlight
  करना सीखें। तेज़ परिणामों के लिए indexing, searching, और fragment highlighting पर
  step‑by‑step मार्गदर्शन प्राप्त करें।
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: GroupDocs.Search के साथ Highlight text java – Fast document highlighting
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: GroupDocs.Search के साथ जावा टेक्स्ट को highlight करें
type: docs
url: /hi/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# GroupDocs.Search के साथ टेक्स्ट हाइलाइट करें java

आधुनिक एंटरप्राइज़ एप्लिकेशन्स में, **जावा में टेक्स्ट हाइलाइट** कच्चे खोज परिणामों को तुरंत पढ़ने योग्य अंतर्दृष्टियों में बदलने के लिए आवश्यक है। चाहे आप एक कानूनी‑समीक्षा पोर्टल, एक शैक्षणिक शोध इंजन, या ग्राहक‑समर्थन डैशबोर्ड बना रहे हों, क्वेरी शब्दों को खोजने और दृश्य रूप से उजागर करने से उपयोगकर्ताओं को मैन्युअल स्कैनिंग में अनगिनत सेकंड बचते हैं। यह ट्यूटोरियल दिखाता है कि **GroupDocs.Search for Java** का उपयोग करके **जावा में दस्तावेज़ खोजें**, **जावा में दस्तावेज़ इंडेक्स करें**, और पूर्ण‑दस्तावेज़ तथा फ्रैगमेंट‑स्तर दोनों हाइलाइटिंग कैसे लागू करें, केवल कुछ कोड लाइनों के साथ।

## त्वरित उत्तर
- **“search and highlight text” क्या मतलब है?** इसका मतलब है दस्तावेज़ के भीतर क्वेरी शब्दों को ढूँढना और उन्हें दृश्य रूप से उजागर करना (उदाहरण के लिए, रंगीन पृष्ठभूमि के साथ)।  
- **कौन सी लाइब्रेरी यह क्षमता प्रदान करती है?** GroupDocs.Search for Java.  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; उत्पादन उपयोग के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं हाइलाइट रंग कस्टमाइज़ कर सकता हूँ?** हाँ—कोई भी RGB रंग `HighlightOptions` के माध्यम से सेट किया जा सकता है।  
- **क्या फ्रैगमेंट हाइलाइटिंग समर्थित है?** बिल्कुल; आप मैच से पहले/बाद के शब्दों को परिभाषित करके संक्षिप्त स्निपेट बना सकते हैं।

## जावा में दस्तावेज़ों में टेक्स्ट हाइलाइट कैसे करें

दस्तावेज़ों में जावा में टेक्स्ट हाइलाइट करने के लिए, पहले उपयुक्त संपीड़न सेटिंग्स का उपयोग करके स्रोत फ़ाइलों का इंडेक्स बनाएं, फिर वांछित शब्दों को खोजने के लिए एक खोज क्वेरी चलाएँ, और अंत में परिणामों को HTML, PDF, या साधारण टेक्स्ट में निर्यात करें, जहाँ प्रत्येक मिलान को हाइलाइट टैग में लपेटा गया हो। यह तीन‑स्टेप प्रक्रिया बड़े संग्रहों में तेज़ और सटीक हाइलाइटिंग सुनिश्चित करती है।

1. **एक इंडेक्स बनाएं** ऐसी संपीड़न सेटिंग्स के साथ जो स्टोरेज फुटप्रिंट को कम रखती हैं।  
2. **एक खोज चलाएँ** उस क्वेरी स्ट्रिंग का उपयोग करके जिसे आप हाइलाइट करना चाहते हैं।  
3. **आउटपुट जनरेट करें** (HTML, PDF, या साधारण टेक्स्ट) जहाँ क्वेरी शब्द की हर घटना हाइलाइट टैग में लिपटी हो।

## खोज और टेक्स्ट हाइलाइट क्या है?

खोज और टेक्स्ट हाइलाइट वह प्रक्रिया है जिसमें एक इंडेक्स्ड संग्रह को दिए गए क्वेरी के लिए स्कैन किया जाता है, मिलते‑जुलते दस्तावेज़ प्राप्त किए जाते हैं, और फिर आउटपुट (HTML, PDF, आदि) में क्वेरी शब्द की प्रत्येक घटना को चिह्नित किया जाता है। यह दृश्य संकेत उपयोगकर्ताओं को प्रासंगिक जानकारी तुरंत पहचानने में मदद करता है।

## GroupDocs.Search for Java का उपयोग क्यों करें?

GroupDocs.Search for Java **उच्च‑प्रदर्शन इंडेक्सिंग** ( `Compression.High` के साथ प्रति इंडेक्स 50 GB तक), **समृद्ध हाइलाइटिंग** जो पूरे दस्तावेज़ और कस्टम फ्रैगमेंट दोनों पर काम करती है, और **क्रॉस‑फ़ॉर्मेट समर्थन** 30 से अधिक फ़ाइल प्रकारों के लिए—जैसे DOCX, PDF, PPTX, और TXT—प्रदान करता है। लाइब्रेरी **इन्क्रिमेंटल इंडेक्सिंग** भी देती है, जिससे आप पूरे इंडेक्स को फिर से बनाये बिना नई फ़ाइलें जोड़ सकते हैं, जिससे बड़े‑पैमाने पर डिप्लॉयमेंट में डाउनटाइम 80 % तक घट जाता है।

## आवश्यकताएँ
- Java Development Kit (JDK) 8 या नया।  
- निर्भरता प्रबंधन के लिए Maven।  
- IntelliJ IDEA या Eclipse जैसे IDE।  
- Java सिंटैक्स की बुनियादी समझ।

## GroupDocs.Search for Java सेटअप करना

`pom.xml` में GroupDocs रिपॉजिटरी और डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

आप आधिकारिक साइट से नवीनतम JAR भी सीधे डाउनलोड कर सकते हैं: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### लाइसेंस प्राप्ति
फ़्री ट्रायल से शुरू करें या मूल्यांकन के लिए एक अस्थायी लाइसेंस प्राप्त करें। उत्पादन डिप्लॉयमेंट के लिए सभी सुविधाओं को अनलॉक करने हेतु पूर्ण लाइसेंस खरीदें।

## कार्यान्वयन गाइड

कार्यान्वयन दो व्यावहारिक भागों में विभाजित है: **पूरे दस्तावेज़ों में हाइलाइटिंग** और **फ्रैगमेंट में हाइलाइटिंग**। दोनों भागों में **जावा दस्तावेज़ों को हाइलाइट करने** के आवश्यक चरण शामिल हैं, GroupDocs.Search का उपयोग करके।

### इंडेक्स सेटिंग्स कॉन्फ़िगर करना

इंडेक्सिंग से पहले, स्टोरेज को हाई कॉम्प्रेशन पर सेट करें—यह डिस्क उपयोग को 70 % तक घटाता है जबकि खोज गति बरकरार रखता है।

`IndexSettings` वह कॉन्फ़िगरेशन ऑब्जेक्ट है जो नियंत्रित करता है कि इंडेक्स डिस्क पर कैसे संग्रहीत होता है। `Compression` को `Compression.High` पर सेट करें ताकि यह ऑप्टिमाइज़ेशन सक्षम हो सके।  
`Compression` इंडेक्स फ़ाइलों पर लागू डेटा संपीड़न स्तर को निर्दिष्ट करता है, जहाँ `Compression.High` अधिकतम आकार कमी प्रदान करता है।

## पूरे दस्तावेज़ों में हाइलाइटिंग

### चरण 1: इंडेक्स बनाएं और भरें

एक इंडेक्स फ़ोल्डर बनाएं और सभी स्रोत फ़ाइलें जोड़ें जिन्हें आप खोजना चाहते हैं। `Index` क्लास खोज योग्य कंटेनर का प्रतिनिधित्व करती है।

### चरण 2: खोज करें और हाइलाइटिंग लागू करें

शब्द (उदाहरण के लिए `ipsum`) को खोजें और हाइलाइटेड मैचों के साथ एक HTML फ़ाइल जनरेट करें। हाइलाइट रंग और इनलाइन स्टाइल उपयोग को निर्दिष्ट करने के लिए `HighlightOptions` का उपयोग करें।

`HighlightOptions` आपको फ़ोरग्राउंड और बैकग्राउंड रंग, साथ ही प्रत्येक हाइलाइटेड शब्द पर लागू होने वाली CSS क्लास निर्धारित करने की अनुमति देता है।

`HtmlHighlighter` प्रदान किए गए विकल्पों के आधार पर हाइलाइटेड शब्दों के साथ HTML आउटपुट जनरेट करता है।  
`SearchResult` मिलते हुए दस्तावेज़ों की सूची और प्रत्येक पाए गए शब्द की स्थितियों को रखता है।

**सीधा उत्तर:** अपना इंडेक्स लोड करें, `search("ipsum")` कॉल करें, और प्राप्त `SearchResult` को कॉन्फ़िगर किए गए `HighlightOptions` इंस्टेंस के साथ `HtmlHighlighter` को पास करें। हाईलाइटर HTML लौटाता है जहाँ “ipsum” की प्रत्येक घटना चुने हुए बैकग्राउंड रंग के साथ `<span>` में लिपटी होती है।

मुख्य विकल्पों की व्याख्या  
- **Compression** – हाई कॉम्प्रेशन स्टोरेज बचाता है।  
- **HighlightColor** – अपनी UI पैलेट से मेल खाने के लिए कोई भी RGB मान सेट करें।  
- **UseInlineStyles** – `false` सेट करने पर साफ़ HTML बनता है जिसे आप ग्लोबली CSS से स्टाइल कर सकते हैं।  

## फ्रैगमेंट में हाइलाइटिंग

### चरण 1: इंडेक्स और खोज (ऊपर जैसा ही)

उसी इंडेक्स और खोज चरणों का उपयोग करें; आप `Index` और `SearchResult` ऑब्जेक्ट्स को पुन: उपयोग करेंगे।

### चरण 2: फ्रैगमेंट कॉन्टेक्स्ट निर्धारित करें और हाइलाइट करें

`FragmentOptions` के साथ निर्धारित करें कि प्रत्येक फ्रैगमेंट में मैच से पहले और बाद में कितने शब्द दिखाने हैं।

`FragmentOptions` प्रत्येक स्निपेट में शामिल आसपास के शब्दों (`termsBefore` और `termsAfter`) की संख्या को नियंत्रित करता है, जिससे आप कॉन्टेक्स्ट और स्निपेट लंबाई के बीच संतुलन बना सकते हैं।

### चरण 3: हाइलाइटेड फ्रैगमेंट प्राप्त करें और लिखें

जनरेट किए गए फ्रैगमेंट एकत्र करें और उन्हें HTML फ़ाइल में लिखें। प्रत्येक फ्रैगमेंट पहले से ही आपके कॉन्फ़िगर किए गए `HighlightOptions` के अनुसार हाइलाइटेड होता है।

`fragmentHighlighter` एक यूटिलिटी है जो `SearchResult` से निर्दिष्ट फ्रैगमेंट और हाइलाइट विकल्पों का उपयोग करके हाइलाइटेड स्निपेट बनाती है।

**सीधा उत्तर:** `SearchResult` प्राप्त करने के बाद, `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)` कॉल करें। यह मेथड HTML स्निपेट्स की सूची लौटाता है, जहाँ प्रत्येक में कॉन्फ़िगर किए गए कॉन्टेक्स्ट शब्दों के साथ मिलते शब्द को हाइलाइट किया गया होता है।

## व्यावहारिक अनुप्रयोग
1. **कानूनी दस्तावेज़ समीक्षा** – हजारों कॉन्ट्रैक्ट्स में कानून, क्लॉज़ या केस रेफ़रेंस को तुरंत हाइलाइट करें।  
2. **शैक्षणिक शोध** – दर्जनों PDF और Word फ़ाइलों में प्रमुख शब्दावली को उजागर करें, जिससे साहित्य‑समीक्षा समय 60 % तक घटे।  
3. **ग्राहक समर्थन** – टिकट इतिहास में ऑर्डर नंबर या एरर कोड को pinpoint करें, जिससे एजेंट तेज़ी से समस्या हल कर सकें।

## प्रदर्शन संबंधी विचार
- **इंडेक्स आकार** – हाई कॉम्प्रेशन (`Compression.High`) डिस्क फुटप्रिंट को 70 % तक घटाता है बिना उल्लेखनीय लेटेंसी प्रभाव के।  
- **फ्रैगमेंट कॉन्टेक्स्ट** – बड़े `termsBefore/After` मान स्निपेट पठनीयता बढ़ाते हैं लेकिन प्रति क्वेरी 10–15 ms अतिरिक्त ले सकते हैं।  
- **मेमोरी प्रबंधन** – बड़े कॉर्पोरा को इंडेक्स करते समय JVM हीप मॉनिटर करें; 2 GB से बड़े डेटा सेट के लिए इन्क्रिमेंटल इंडेक्सिंग अपनाएँ ताकि मेमोरी उपयोग 1 GB से नीचे रहे।

## सामान्य समस्याएँ और समाधान
- **इंडेक्सिंग त्रुटियाँ** – फ़ाइल पाथ सत्यापित करें और सुनिश्चित करें कि एप्लिकेशन को इंडेक्स फ़ोल्डर पर पढ़ने/लिखने की अनुमति है।  
- **हाइलाइट नहीं दिख रहा** – पुष्टि करें कि `UseInlineStyles` आपके आउटपुट फ़ॉर्मेट (HTML बनाम PDF) से मेल खाता है।  
- **रंग लागू नहीं हो रहा** – सुनिश्चित करें कि RGB मान 0‑255 रेंज में हैं और व्यूअर इनलाइन CSS या प्रदान की गई CSS क्लास को सम्मानित करता है।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: GroupDocs.Search for Java का उपयोग करने के क्या लाभ हैं?**  
उत्तर: यह तेज़, स्केलेबल इंडेक्सिंग, कस्टमाइज़ेबल हाइलाइटिंग, और 30+ दस्तावेज़ फ़ॉर्मेट समर्थन प्रदान करता है, सामान्य सर्वर पर 500‑पेज फ़ाइलों को 2 सेकंड से कम में प्रोसेस करता है।

**प्रश्न: मैं GroupDocs.Search को REST API के साथ कैसे इंटीग्रेट करूँ?**  
उत्तर: Spring Boot कंट्रोलर्स के माध्यम से खोज और हाइलाइट मेथड को एक्सपोज़ करें, HTML स्निपेट या JSON पेलोड लौटाएँ जिसमें हाइलाइटेड फ्रैगमेंट हों।

**प्रश्न: क्या लाइब्रेरी पासवर्ड‑प्रोटेक्टेड फ़ाइलों को संभालती है?**  
उत्तर: हाँ—`addDocument(filePath, password)` के माध्यम से दस्तावेज़ को इंडेक्स में जोड़ते समय पासवर्ड प्रदान करें।

**प्रश्न: क्या मैं हाइलाइट मार्कअप को रंग से आगे कस्टमाइज़ कर सकता हूँ?**  
उत्तर: बिल्कुल; `options.setCssClass("myHighlight")` के साथ CSS क्लास असाइन करें और उसे ग्लोबली स्टाइल करें, या हाइलाइटिंग के बाद जनरेटेड HTML को संशोधित करें।

**प्रश्न: इस गाइड के लिए किस संस्करण का परीक्षण किया गया?**  
उत्तर: कोड को GroupDocs.Search 25.4 के साथ वैध किया गया था।

**प्रश्न: हाइलाइट विकल्पों को इनलाइन स्टाइल के बजाय CSS क्लास उपयोग करने के लिए कैसे सेट करूँ?**  
उत्तर: `options.setUseInlineStyles(false)` कॉल करें और `options.setCssClass("myHighlight")` के माध्यम से क्लास परिभाषित करें।

**प्रश्न: क्या PDF आउटपुट में सीधे शब्दों को हाइलाइट करने का तरीका है?**  
उत्तर: हाँ—GroupDocs.Search PDF इनपुट को सपोर्ट करता है, और हाईलाइटर HTML आउटपुट देता है जिसे आप PDF व्यूअर में एम्बेड कर सकते हैं या GroupDocs.Conversion के माध्यम से PDF में पुनः परिवर्तित कर सकते हैं।

---

**अंतिम अपडेट:** 2026-09-27  
**परीक्षण किया गया:** GroupDocs.Search 25.4.  
**लेखक:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

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

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

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

## संबंधित ट्यूटोरियल

- [जावा फुल टेक्स्ट सर्च कैसे लागू करें: GroupDocs.Search के साथ इंडेक्स डायरेक्टरी बनाएं](/search/java/indexing/groupdocs-search-java-create-index/)
- [GroupDocs.Search for Java के साथ सर्च इंडेक्स को प्रबंधित करना सीखें](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [जावा में चंक-आधारित खोज के साथ दस्तावेज़ को इंडेक्स में जोड़ें](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)
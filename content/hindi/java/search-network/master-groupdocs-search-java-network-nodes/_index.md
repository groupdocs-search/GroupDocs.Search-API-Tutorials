---
date: '2026-07-02'
description: GroupDocs.Search के लिए temporary license प्राप्त करने, index में directories
  जोड़ने, और custom document attributes जोड़ने के बारे में सीखें, जबकि Java search
  network nodes का प्रबंधन करें।
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Temporary License प्राप्त करें GroupDocs – Master Search Nodes (Java)
type: docs
url: /hi/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# अस्थायी लाइसेंस प्राप्त करें GroupDocs – मास्टर सर्च नोड्स (Java)

इस व्यापक गाइड में आप **GroupDocs.Search के लिए एक अस्थायी लाइसेंस प्राप्त करेंगे**, एक मल्टी‑नोड सर्च नेटवर्क को कॉन्फ़िगर करेंगे, और Java का उपयोग करके **इंडेक्स करने के लिए डायरेक्टरी जोड़ना** और **कस्टम दस्तावेज़ एट्रिब्यूट जोड़ना** सीखेंगे। चाहे आप एंटरप्राइज़ दस्तावेज़‑प्रबंधन प्रणाली बना रहे हों या एक सर्चेबल प्रोडक्ट कैटलॉग, इन चरणों में निपुण होने से आप प्लेटफ़ॉर्म का बिना किसी प्रतिबंध के मूल्यांकन कर सकते हैं और अपनी सर्च क्षमताओं को जल्दी स्केल कर सकते हैं।

## त्वरित उत्तर
- **GroupDocs.Search का उपयोग शुरू करने के लिए पहला कदम क्या है?** GroupDocs पोर्टल से एक अस्थायी लाइसेंस प्राप्त करें।  
- **कौन सा Maven रिपॉज़िटरी लाइब्रेरी को होस्ट करता है?** `https://releases.groupdocs.com/search/java/`।  
- **इंडेक्स करने के लिए डायरेक्टरी कैसे जोड़ूँ?** मास्टर नोड पर `addDirectoriesToIndex` हेल्पर को कॉल करें।  
- **क्या मैं कस्टम दस्तावेज़ एट्रिब्यूट जोड़ सकता हूँ?** हाँ—`addAttribute` को दस्तावेज़ कुंजी और एट्रिब्यूट नाम के साथ invoke करें।  
- **नोड्स को साफ़ तरीके से कैसे बंद करूँ?** संसाधनों को रिलीज़ करने के लिए `closeNodes` invoke करें।

## अस्थायी लाइसेंस क्या है और मुझे इसकी आवश्यकता क्यों है?
एक अस्थायी लाइसेंस आपको GroupDocs.Search का मूल्यांकन बिना किसी प्रतिबंध के करने देता है। यह विकास, परीक्षण, या प्रूफ़‑ऑफ़‑कॉन्सेप्ट प्रोजेक्ट्स के लिए पूरी तरह उपयुक्त है, इससे पहले कि आप पूर्ण खरीदारी के लिए प्रतिबद्ध हों। लाइसेंस सीमित अवधि के लिए पूर्ण‑फ़ीचर एक्सेस प्रदान करता है, जिससे आप प्रदर्शन बेंचमार्क कर सकते हैं, इंटीग्रेशन पॉइंट्स का परीक्षण कर सकते हैं, और बिना वित्तीय प्रतिबद्धता के यह सुनिश्चित कर सकते हैं कि समाधान आपकी आवश्यकताओं को पूरा करता है।

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

### आवश्यक लाइब्रेरीज़ और निर्भरताएँ
Java के लिए GroupDocs.Search के साथ काम करने के लिए आवश्यक Maven निर्भरताएँ शामिल करें:
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
आप नवीनतम संस्करण सीधे [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) से भी डाउनलोड कर सकते हैं।

### पर्यावरण सेटअप
- सुनिश्चित करें कि आपके पास संगत JDK स्थापित है (Java 8 या बाद का)।  
- अपने IDE को Maven प्रोजेक्ट्स को सपोर्ट करने के लिए सेटअप करें।

### ज्ञान पूर्वापेक्षाएँ
Java प्रोग्रामिंग की बुनियादी समझ और Maven प्रोजेक्ट मैनेजमेंट से परिचित होना लाभदायक होगा। यदि आप इन अवधारणाओं में नए हैं, तो शुरू करने के लिए परिचयात्मक संसाधनों का अन्वेषण करने पर विचार करें।

## अस्थायी लाइसेंस कैसे प्राप्त करें
एक अस्थायी लाइसेंस GroupDocs पोर्टल पर जाकर, एक छोटा अनुरोध फ़ॉर्म भरकर, और प्राप्त `.lic` फ़ाइल को अपने प्रोजेक्ट के `resources` फ़ोल्डर में रखकर प्राप्त किया जाता है। फिर लाइसेंस को कुछ कोड लाइनों के साथ इनिशियलाइज़ करें (नीचे स्निपेट देखें)। अनुरोध फ़ॉर्म के लिए आधिकारिक पेज उपयोग करें: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)।

## GroupDocs.Search for Java सेटअप करना

### इंस्टॉलेशन जानकारी
अपने प्रोजेक्ट में GroupDocs.Search for Java का उपयोग शुरू करने के लिए, ऊपर दिए गए Maven चरणों का पालन करें या आधिकारिक रिलीज़ पेज से नवीनतम संस्करण सीधे डाउनलोड करें।

#### लाइसेंस प्राप्त करने के चरण
1. **Free Trial** – बिना किसी प्रतिबद्धता के फीचर्स का अन्वेषण करें।  
2. **Temporary License** – परीक्षण के लिए एक शॉर्ट‑टर्म की प्राप्त करें (ऊपर के सेक्शन देखें)।  
3. **Purchase** – प्रोडक्शन उपयोग के लिए, **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)** से पूर्ण लाइसेंस खरीदें।

### बुनियादी इनिशियलाइज़ेशन और सेटअप
GroupDocs.Search के साथ अपने प्रोजेक्ट को इस प्रकार इनिशियलाइज़ करें:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
यह इनिशियलाइज़ेशन चरण यह सुनिश्चित करने के लिए महत्वपूर्ण है कि सभी कॉम्पोनेन्ट्स आपके सर्च नेटवर्क में सहजता से कार्य करें।

## कार्यान्वयन गाइड
अब, प्रक्रिया को प्रबंधनीय सेक्शनों में विभाजित करते हैं, प्रत्येक सर्च नेटवर्क नोड्स को डिप्लॉय और मैनेज करने की विशिष्ट सुविधा पर केंद्रित है।

### फीचर 1: कॉन्फ़िगरेशन सेटअप
**Overview:** आपके सर्च नेटवर्क के लिए कॉन्फ़िगरेशन सेटअप करना नोड्स को डिप्लॉय करने का पहला कदम है। यह सेटअप नोड डिप्लॉयमेंट के लिए आवश्यक पाथ्स और पोर्ट्स को निर्दिष्ट करता है।

#### कार्यान्वयन चरण:
##### चरण 1: बेस पाथ और पोर्ट निर्धारित करें
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### चरण 2: सर्च नेटवर्क कॉन्फ़िगर करें
`configureSearchNetwork` फ़ंक्शन नोड्स को डिप्लॉय करने के लिए आवश्यक कॉन्फ़िगरेशन ऑब्जेक्ट तैयार करता है।  
`Configuration` एक क्लास है जो सभी सेटिंग्स जैसे इंडेक्स फ़ोल्डर, नेटवर्क पोर्ट्स, और नोड रोल्स को रखती है।  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameters:** बेस पाथ और पोर्ट संसाधनों को लोकेट करने और कम्युनिकेशन चैनल स्थापित करने के लिए उपयोग होते हैं।  
- **Return Value:** आपका डिप्लॉयमेंट आवश्यकताओं के अनुसार तैयार किया गया एक कॉन्फ़िगर किया गया `Configuration` ऑब्जेक्ट।

### फीचर 2: सर्च नेटवर्क डिप्लॉयमेंट
**Overview:** विभिन्न वातावरणों या डेटा सेगमेंट्स में अपनी सर्च क्षमताओं को स्केल करने के लिए नोड्स को डिप्लॉय करना आवश्यक है।

#### कार्यान्वयन चरण:
##### चरण 1: नोड्स डिप्लॉय करें
`deploySearchNetwork` फ़ंक्शन इनिशियलाइज़ करता है और सर्च नेटवर्क नोड्स की एक एरे रिटर्न करता है।  
`SearchNetworkNodes` प्रत्येक नोड इंस्टेंस को दर्शाता है जो वितरित सर्च क्लस्टर में भाग लेता है।  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameters:** बेस पाथ, पोर्ट, और कॉन्फ़िगरेशन डिप्लॉयमेंट पर्यावरण निर्धारित करने के लिए उपयोग होते हैं।  
- **Return Value:** इनिशियलाइज़्ड `SearchNetworkNodes` वाली एक एरे।

### फीचर 3: नेटवर्क इवेंट्स की सदस्यता लेना
**Overview:** आपके सर्च नेटवर्क की गतिविधियों की मॉनिटरिंग इष्टतम प्रदर्शन और विश्वसनीयता बनाए रखने के लिए महत्वपूर्ण है।

#### कार्यान्वयन चरण:
##### चरण 1: मास्टर नोड इवेंट्स की सदस्यता लें
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Purpose:** यह चरण सुनिश्चित करता है कि आपको सर्च नेटवर्क के भीतर महत्वपूर्ण इवेंट्स या बदलावों की सूचना मिलती रहे।

### फीचर 4: दस्तावेज़ों का इंडेक्सिंग
**Overview:** इंडेक्स करने के लिए दस्तावेज़ों वाली डायरेक्टरीज़ जोड़ने से आपके नेटवर्क में डेटा रिट्रीवल अधिक कुशल हो जाता है।

#### इंडेक्स में डायरेक्टरी कैसे जोड़ें
`addDirectoriesToIndex` एक हेल्पर मेथड है जो मास्टर नोड पर इंडेक्सिंग के लिए फ़ोल्डर पाथ्स को रजिस्टर करता है।  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Purpose:** निर्दिष्ट डायरेक्टरीज़ के भीतर सभी दस्तावेज़ों की तेज़ एक्सेस और सर्चेबिलिटी को सुविधाजनक बनाता है।

### फीचर 5: दस्तावेज़ों में एट्रिब्यूट जोड़ना
**Overview:** कस्टम एट्रिब्यूट दस्तावेज़ मेटाडेटा को बढ़ाते हैं, जिससे सर्च अधिक लचीला और जानकारीपूर्ण बनता है।

#### कस्टम दस्तावेज़ एट्रिब्यूट कैसे जोड़ें
`addAttribute` इंडेक्स में निर्दिष्ट दस्तावेज़ में एक कस्टम मेटाडेटा एट्रिब्यूट जोड़ता है।  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameters:** नोड, दस्तावेज़ कुंजी, और जोड़ने के लिए एट्रिब्यूट निर्दिष्ट करें।  
- **Purpose:** अतिरिक्त मेटाडेटा के साथ दस्तावेज़ों को समृद्ध करके सर्च फ़ंक्शनैलिटी का विस्तार करता है।

### फीचर 6: इंडेक्स किए गए दस्तावेज़ों को प्राप्त करना
**Overview:** डेटा की सटीकता और पूर्णता सुनिश्चित करने के लिए इंडेक्स किए गए दस्तावेज़ों को कुशलता से प्राप्त और सूचीबद्ध करें।

#### कार्यान्वयन चरण:
##### चरण 1: इंडेक्स किए गए दस्तावेज़ प्राप्त करें
```java
getIndexedDocuments(nodes[0]);
```  
- **Purpose:** आपके सर्च नेटवर्क के भीतर सभी आवश्यक दस्तावेज़ों के सफल इंडेक्सिंग को सत्यापित करता है।

### फीचर 7: नेटवर्क नोड्स को बंद करना
**Overview:** संसाधन प्रबंधन और मेमोरी लीक्स को रोकने के लिए नोड्स को सही तरीके से बंद करना महत्वपूर्ण है।

#### कार्यान्वयन चरण:
##### चरण 1: सभी नोड्स बंद करें
`closeNodes` सभी सक्रिय सर्च नोड्स को शटडाउन करता है और आवंटित संसाधनों को रिलीज़ करता है।  
```java
closeNodes(nodes);
```  
- **Purpose:** प्रत्येक नोड द्वारा कब्जा किए गए संसाधनों को रिलीज़ करता है, जिससे एक साफ़ शटडाउन प्रक्रिया सुनिश्चित होती है।

## GroupDocs.Search के लिए अस्थायी लाइसेंस क्यों उपयोग करें?
एक अस्थायी लाइसेंस **30 दिनों के लिए पूर्ण‑फ़ीचर एक्सेस** प्रदान करता है और **50,000 इंडेक्स किए गए दस्तावेज़** तक बिना प्रदर्शन थ्रॉटलिंग के सपोर्ट करता है। यह आपको वास्तविक डेटा पर इंडेक्सिंग स्पीड, क्वेरी लेटेंसी, और स्केलेबिलिटी को बेंचमार्क करने देता है, प्रोडक्शन लाइसेंस खरीदने से पहले। यह मूल्यांकन वाटरमार्क भी हटाता है, जिससे आपको अंतिम उत्पाद की क्षमताओं का सच्चा प्रतिनिधित्व मिलता है।

## सामान्य उपयोग केस
1. **Enterprise Document Management** – विभागों में लाखों आंतरिक फ़ाइलों को इंडेक्स करें, जिससे तुरंत फुल‑टेक्स्ट सर्च संभव हो।  
2. **E‑commerce Platforms** – कई वेयरहाउस और थर्ड‑पार्टी फ़ीड्स को कवर करने वाला सर्चेबल प्रोडक्ट कैटलॉग बनाएं।  
3. **Legal Firms** – केस फ़ाइलें, कॉन्ट्रैक्ट्स, और साक्ष्य को कस्टम मेटाडेटा के साथ व्यवस्थित करें, जिससे तेज़ रिट्रीवल संभव हो।

अन्य सिस्टम्स के साथ इंटीग्रेशन संभावनाओं में CRM प्लेटफ़ॉर्म, कंटेंट मैनेजमेंट सिस्टम (CMS), और डेटा एनालिटिक्स टूल्स शामिल हैं, जो GroupDocs.Search for Java द्वारा प्रदान किए गए मजबूत इंडेक्सिंग और सर्चिंग फीचर्स का लाभ उठाते हैं।

## प्रदर्शन संबंधी विचार
GroupDocs.Search for Java का उपयोग करते समय प्रदर्शन को अनुकूलित करने के लिए:
- **Optimize Configuration** – अपने विशिष्ट डिप्लॉयमेंट पर्यावरण से मेल खाने के लिए कॉन्फ़िगरेशन सेटिंग्स को अनुकूलित करें।  
- **Monitor Resource Usage** – नियमित रूप से CPU, मेमोरी, और I/O की जाँच करें ताकि बॉटलनेक्स या मेमोरी लीक्स से बचा जा सके।  
- **Follow Best Practices** – Java मेमोरी‑मैनेजमेंट गाइडलाइन्स का पालन करें, जिससे सिस्टम संसाधनों का कुशल उपयोग सुनिश्चित हो।

## अक्सर पूछे जाने वाले प्रश्न

**Q: अस्थायी लाइसेंस कितने समय तक वैध रहता है?**  
A: अस्थायी लाइसेंस आमतौर पर 30 दिनों के लिए वैध होते हैं, जिससे आपको उत्पाद का पर्याप्त समय तक मूल्यांकन करने का अवसर मिलता है।

**Q: क्या मैं अस्थायी लाइसेंस को पूर्ण लाइसेंस में बिना पुनः इंस्टॉल किए बदल सकता हूँ?**  
A: हाँ—अस्थायी लाइसेंस फ़ाइल को पूर्ण लाइसेंस फ़ाइल से बदलें और अपना एप्लिकेशन रीस्टार्ट करें।

**Q: नया लाइसेंस लागू करने के बाद क्या मुझे दस्तावेज़ों को पुनः‑इंडेक्स करना पड़ेगा?**  
A: नहीं, इंडेक्स वही रहता है; लाइसेंस केवल उपयोग अधिकारों को नियंत्रित करता है।

**Q: यदि मैं नोड्स को बंद करना भूल जाऊँ तो क्या होगा?**  
A: अनरिलीज़्ड रिसोर्सेज़ मेमोरी लीक्स का कारण बन सकते हैं; शटडाउन के दौरान हमेशा `closeNodes` invoke करें।

**Q: क्या एक दस्तावेज़ में एक से अधिक कस्टम एट्रिब्यूट जोड़ना संभव है?**  
A: बिल्कुल—विभिन्न एट्रिब्यूट नामों के साथ `addAttribute` को कई बार कॉल करें।

---

**अंतिम अपडेट:** 2026-07-02  
**टेस्टेड विथ:** GroupDocs.Search for Java 25.4  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल्स

- [Deploy a Search Network Node in .NET using GroupDocs for Efficient Document Indexing and Retrieval](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [How to Implement a Search Network with GroupDocs.Search in .NET for Document Management Systems](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configuring Aspose.Search Network & Adding Document Attributes with GroupDocs.Redaction for .NET: A Comprehensive Guide](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
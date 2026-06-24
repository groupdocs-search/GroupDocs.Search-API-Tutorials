---
date: '2026-04-21'
description: GroupDocs.Redaction for .NET का उपयोग करके फ़ाइलों को फ़िल्टर करना सीखें,
  जिसमें निर्माण तिथि, फ़ाइल आकार, संशोधन तिथि द्वारा फ़िल्टर करना और NOT फ़िल्टर
  कैसे लागू करें, शामिल है।
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: GroupDocs.Redaction for .NET के साथ फ़ाइलों को फ़िल्टर कैसे करें
type: docs
url: /hi/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# GroupDocs.Redaction for .NET के साथ फ़ाइलों को फ़िल्टर कैसे करें

आज के तेज़ गति वाले डिजिटल वातावरण में, **फ़ाइलों को फ़िल्टर करने का तरीका** प्रभावी ढंग से आपकी उत्पादकता को बढ़ा या घटा सकता है। चाहे आपको एक्सटेंशन, निर्माण तिथि, आकार, या संशोधन तिथि के आधार पर दस्तावेज़ अलग करने की आवश्यकता हो, एक ठोस फ़िल्टरिंग रणनीति समय बचाती है, स्टोरेज लागत कम करती है, और आपके सर्च इंडेक्स को व्यवस्थित रखती है। इस ट्यूटोरियल में हम GroupDocs.Redaction for .NET का उपयोग करके वास्तविक दुनिया के उदाहरणों के माध्यम से चलेंगे, जिससे आप देखेंगे कि सामान्य व्यावसायिक आवश्यकताओं को पूरा करने के लिए फ़ाइलों को कैसे फ़िल्टर किया जाता है।

## त्वरित उत्तर
- **मुझे कौन सी लाइब्रेरी चाहिए?** GroupDocs.Redaction for .NET (install via NuGet).  
- **क्या मैं निर्माण तिथि के आधार पर फ़िल्टर कर सकता हूँ?** Yes – use `CreateCreationTimeRange`.  
- **मैं कुछ प्रकारों को कैसे बाहर रखूँ?** Apply a NOT filter with `DocumentFilter.CreateNot`.  
- **क्या फ़ाइल आकार फ़िल्टरिंग समर्थित है?** Absolutely, via `CreateFileLengthRange` or upper/lower bounds.  
- **क्या मुझे लाइसेंस चाहिए?** A trial or full license is required for production use.

## GroupDocs.Redaction के साथ फ़ाइल फ़िल्टरिंग क्या है?
फ़ाइल फ़िल्टरिंग आपको इंडेक्सिंग इंजन को यह बताने देती है कि कौन से दस्तावेज़ मेटाडेटा जैसे एक्सटेंशन, तिथियों, पाथ पैटर्न या आकार के आधार पर शामिल या अनदेखा किए जाएँ। सटीक `DocumentFilter` नियमों को परिभाषित करके, आप अपना इंडेक्स हल्का और खोज तेज़ रख सकते हैं।

## .NET के लिए GroupDocs.Redaction का उपयोग क्यों करें?
- **निर्मित फ़िल्टर हेल्पर** – no need to write custom file‑system code.  
- **तार्किक ऑपरेटर** – combine multiple criteria with AND, OR, and NOT.  
- **प्रदर्शन‑ऑप्टिमाइज़्ड** – filters are applied during indexing, not after.  
- **क्रॉस‑प्लेटफ़ॉर्म** – works with .NET Framework, .NET Core, and .NET 5/6+.

## पूर्वापेक्षाएँ
- .NET Framework 4.6+ या .NET Core 3.1+ स्थापित हो।  
- Visual Studio या आपका पसंदीदा C# IDE।  
- बेसिक C# ज्ञान।  

### आवश्यक लाइब्रेरी और सेटअप
अपनी पसंदीदा विधि से NuGet पैकेज इंस्टॉल करें:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **प्रो टिप:** After installing, add your license file to the project root and call `License.SetLicense("license-file-path")` before creating any Redactor or Index objects.

## .NET के लिए GroupDocs.Redaction सेटअप करना

पहले, एक `Redactor` इंस्टेंस बनाएँ जो उस दस्तावेज़ की ओर इशारा करता है जिससे आप काम करना चाहते हैं:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **यह क्यों महत्वपूर्ण है:** Initializing the Redactor guarantees the library is ready to apply filters and redaction rules later in the workflow.

## एक्सटेंशन द्वारा फ़ाइलों को फ़िल्टर कैसे करें

फ़ाइल एक्सटेंशन द्वारा फ़िल्टर करना दस्तावेज़ सेट को संकीर्ण करने का सबसे सामान्य तरीका है। नीचे हम केवल FB2, EPUB, और TXT फ़ाइलें रखते हैं।

### फ़ाइल एक्सटेंशन द्वारा फ़िल्टर

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## अनचाहे प्रकारों को बाहर रखने के लिए NOT फ़िल्टर कैसे लागू करें

यदि आपको **NOT फ़िल्टर लागू करें** लॉजिक की आवश्यकता है—जैसे, HTML और PDF फ़ाइलें बाहर रखना—तो `CreateNot` का उपयोग करें।

### HTM, HTML, और PDF फ़ाइलें बाहर रखें

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## निर्माण तिथि द्वारा फ़ाइलों को फ़िल्टर कैसे करें

जब आपको **निर्माण तिथि द्वारा फ़िल्टर** करने की आवश्यकता हो, तो एक प्रारंभ और समाप्ति `DateTime` निर्दिष्ट करें।

### निर्माण तिथि रेंज द्वारा फ़िल्टर

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## संशोधन तिथि द्वारा फ़ाइलों को फ़िल्टर कैसे करें

निर्माण तिथियों के समान, आप परिणामों को किसी निश्चित बिंदु से पहले संशोधित फ़ाइलों तक सीमित कर सकते हैं।

### संशोधन तिथि द्वारा फ़िल्टर

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## नियमित अभिव्यक्तियों (regex) का उपयोग करके पाथ द्वारा फ़ाइलों को फ़िल्टर कैसे करें

यदि आपकी फ़ोल्डर संरचना नामकरण मानकों का पालन करती है, तो एक regex विशिष्ट पाथ को लक्षित कर सकता है।

### फ़ाइल पाथ पैटर्न द्वारा फ़िल्टर

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## फ़ाइल आकार द्वारा फ़ाइलों को फ़िल्टर कैसे करें

बैंडविड्थ या स्टोरेज सीमाओं से निपटते समय दस्तावेज़ आकार को नियंत्रित करना आवश्यक है।

### फ़ाइल आकार द्वारा फ़िल्टर (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## कई शर्तों को AND के साथ कैसे मिलाएँ

जब आपको कई मानदंडों का उपयोग करके **फ़ाइलों को फ़िल्टर करने का तरीका** चाहिए, तो उन्हें `CreateAnd` के साथ मिलाएँ।

### लॉजिकल AND उदाहरण

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## कई शर्तों को OR के साथ कैसे मिलाएँ

जब कई नियमों में से कोई भी पास हो, तो `CreateOr` का उपयोग करें।

### लॉजिकल OR उदाहरण

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## सामान्य समस्याएँ और समाधान
- **फ़िल्टर लागू नहीं हुआ:** Ensure you assign `settings.DocumentFilter` **before** creating the `Index` instance.  
- **अप्रत्याशित फ़ाइलें दिखाई देती हैं:** Double‑check file extensions include the leading dot (`.txt`).  
- **प्रदर्शन में गिरावट:** Combine filters with AND to reduce the number of files scanned early in the indexing pipeline.  
- **Regex त्रुटियाँ:** Escape special characters in your path pattern or use `RegexOptions.IgnoreCase` for case‑insensitive matches.

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं NOT फ़िल्टर को AND फ़िल्टर के साथ संयोजित कर सकता हूँ?**  
A: हाँ। पहले NOT फ़िल्टर बनाएँ (`DocumentFilter.CreateNot`) और फिर इसे `DocumentFilter.CreateAnd` के तर्कों में से एक के रूप में शामिल करें।

**Q: मैं 10 MB से बड़ी फ़ाइलों को कैसे फ़िल्टर करूँ?**  
A: केवल उन फ़ाइलों को शामिल करने के लिए `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` का उपयोग करें जो उस आकार से अधिक हैं।

**Q: क्या एक साथ निर्माण और संशोधन तिथियों दोनों द्वारा फ़िल्टर करना संभव है?**  
A: बिल्कुल। प्रत्येक फ़िल्टर को अलग-अलग बनाएँ और उन्हें `CreateAnd` के साथ मिलाएँ।

**Q: क्या ये फ़िल्टर क्लाउड स्टोरेज पाथ्स के साथ काम करते हैं?**  
A: फ़िल्टर स्थानीय फ़ाइल सिस्टम पर काम करते हैं। क्लाउड स्रोतों के लिए, पहले फ़ाइलों को एक अस्थायी फ़ोल्डर में डाउनलोड करें, फिर वही फ़िल्टर लागू करें।

**Q: फ़िल्टर बदलने से पुनः‑इंडेक्सिंग की आवश्यकता होगी?**  
A: हाँ। फ़िल्टर तब मूल्यांकित होते हैं जब आप `index.Add` कॉल करते हैं। फ़िल्टर बदलने का मतलब है कि आपको नई मानदंडों को प्रतिबिंबित करने के लिए इंडेक्स को पुनः बनाना होगा।

## निष्कर्ष

GroupDocs.Redaction for .NET के साथ **फ़ाइलों को फ़िल्टर करने का तरीका** में महारत हासिल करके—चाहे एक्सटेंशन, निर्माण तिथि, संशोधन तिथि, फ़ाइल आकार, या NOT लॉजिक का उपयोग करके—आप दस्तावेज़ प्रबंधन को सुव्यवस्थित कर सकते हैं, इंडेक्स को प्रदर्शनशील रख सकते हैं, और वास्तविक रूप से महत्वपूर्ण सामग्री पर ध्यान केंद्रित कर सकते हैं। लॉजिकल ऑपरेटरों के साथ प्रयोग करके फ़िल्टरिंग को अपने सटीक व्यावसायिक नियमों के अनुसार अनुकूलित करें, और आप गति और स्टोरेज दक्षता में तुरंत सुधार देखेंगे।

---

**अंतिम अपडेट:** 2026-04-21  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.11 for .NET  
**लेखक:** GroupDocs
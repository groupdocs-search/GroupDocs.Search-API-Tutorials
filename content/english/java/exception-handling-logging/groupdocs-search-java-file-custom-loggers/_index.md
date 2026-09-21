---
date: '2026-09-21'
description: Learn how to create logger, set max log size, and use console logger
  in GroupDocs.Search for Java.
images:
- /java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/og-image.png
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Learn how to create logger, set max log size, and use console logger
  in GroupDocs.Search for Java. Follow step‑by‑step instructions and best‑practice
  tips.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: How to create logger and limit log size in GroupDocs.Search
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
title: How to create logger and limit log size in GroupDocs.Search for Java
type: docs
url: /java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# How to create logger and limit log file size in GroupDocs.Search for Java

In this tutorial you’ll **how to create logger** implementations for GroupDocs.Search, configure a maximum log file size, and switch between file‑based and console logging. Proper log management prevents disks from filling up during large indexing jobs, improves troubleshooting, and gives you instant feedback when developing. We’ll start with Maven setup, walk through the logger configuration, and finish with a simple search query that demonstrates the logger in action.

## Quick answers
- **What does “limit log file size” mean?** It caps the maximum size of a log file, preventing uncontrolled growth on disk.  
- **Which logger lets you limit log file size?** The built‑in `FileLogger` accepts a max‑size parameter.  
- **How do I use console logger java?** Instantiate `ConsoleLogger` and set it on `IndexSettings`.  
- **Do I need a license for GroupDocs.Search?** A trial works for evaluation; a commercial license is required for production.  
- **What’s the first step?** Add the GroupDocs.Search dependency to your Maven project.  

## What is limit log file size?
The **limit log file size** setting tells the logger to stop writing new entries once the file reaches a defined threshold (for example, 4 MB). When the limit is hit, the logger either discards further messages or rolls over to a new file, keeping disk usage predictable.

## Why use file and custom loggers with GroupDocs.Search?
File and custom loggers give you auditability, debugging insight, and flexibility. In production environments, file logs provide a permanent record of every indexing and search operation, while console logs deliver instant feedback during development. These logs help teams monitor performance, trace errors, and satisfy compliance requirements by preserving a detailed activity trail.

## Prerequisites
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 or newer, with an IDE such as IntelliJ IDEA or Eclipse.  
- Basic familiarity with Maven and Java programming.  

## Setting up GroupDocs.Search for Java

Add the library to your project using one of the methods below.

**Maven setup:**  

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

**Direct download:**  
Download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License acquisition
Obtain a trial or purchase a license via the [licensing page](https://purchase.groupdocs.com/temporary-license/).

## How to create custom logger for GroupDocs.Search
Creating a custom logger is straightforward because GroupDocs.Search relies on the `ILogger` interface. By implementing this interface—or by extending the provided `FileLogger` or `ConsoleLogger`—you can inject additional behavior such as remote forwarding or log rotation. You can also add initialization logic, such as opening network connections, and ensure resources are closed in the logger’s shutdown method. This approach lets you integrate with monitoring platforms like ELK or Splunk.

### Definition anchor
`ILogger` is the core logging contract in GroupDocs.Search; any class that implements its `log(Level, String)` method can become a logger.

### Example approach (no code block)
1. Create a class that implements `ILogger`.  
2. Override the `log` method to write messages to your chosen destination (file, database, HTTP endpoint).  
3. In the index configuration, call `settings.setLogger(new YourCustomLogger())`.  

## How to limit log file size with File Logger
The `FileLogger` class writes log entries to a file on disk and accepts a maximum size argument. By specifying the size limit, the logger automatically stops adding new entries or creates a new file when the threshold is reached, preventing uncontrolled disk growth. This behavior ensures that logging does not interfere with indexing performance while keeping a concise record of events.

### Definition anchor
`FileLogger` is a built‑in logger that persists messages to a text file and supports a configurable maximum file size.

### Step‑by‑step guide
1️⃣ **Import necessary packages**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Set up index settings with File Logger**  
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

3️⃣ **Create or load the index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Add documents to the index**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Perform a search query**  
```text
```java
SearchResult result = index.search(query);
```
```

**Key point:** The `FileLogger` constructor’s second argument (`4.0`) defines the **set max log size** in megabytes, directly addressing the **limit log file size** requirement.

## How to use console logger java
When you need instant visibility of log events, the `ConsoleLogger` writes each message to `System.out`. This logger is lightweight and thread‑safe, making it suitable for development and debugging sessions. It provides immediate feedback on indexing progress, search queries, and error conditions without requiring file I/O, which can speed up iterative testing.

### Definition anchor
`ConsoleLogger` is a lightweight logger that outputs log entries to the standard console stream, making it ideal for debugging sessions.

### Configuration steps
1️⃣ **Import the console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Set up index settings with Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Create or load the index**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Add documents and perform a search**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Tip:** The console logger is ideal during development because it prints each log entry instantly, helping you verify that indexing and searching behave as expected.

## Practical applications
1. **Document management systems:** Keep audit trails of every document indexed, satisfying compliance requirements.  
2. **Enterprise search engines:** Monitor query performance and error rates in real time, enabling rapid SLA compliance checks.  
3. **Legal & compliance software:** Record search terms and timestamps for regulatory reporting, with logs retained for the mandated retention period.

## Performance considerations
- **Log size:** By **set max log size**, you avoid excessive disk usage that could otherwise slow down the JVM’s garbage collector.  
- **Asynchronous logging:** For high‑throughput scenarios, wrap your logger in an asynchronous queue to decouple I/O from the indexing thread (implementation outside the scope of this guide).  
- **Memory management:** Release large `Index` objects with `index.close()` when they are no longer needed to keep the JVM footprint low.

## Common issues & solutions
- **Log path not accessible:** Verify that the directory exists and that the application has write permissions for the user account running the JVM.  
- **Logger not firing:** Ensure you call `settings.setLogger(...)` *before* creating the `Index` object; otherwise the default logger is used.  
- **Console output missing:** Confirm you are running the application in a terminal that displays `System.out`, and that no logging framework (e.g., SLF4J) is intercepting the output.

## Frequently asked questions

**Q: What does the second parameter of `FileLogger` control?**  
A: It sets the maximum size of the log file in megabytes, allowing you to **set max log size** and prevent uncontrolled growth.

**Q: Can I combine file and console loggers?**  
A: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger` and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.

**Q: How do I add documents to the index after the initial creation?**  
A: Call `index.add(pathToNewDocs)` at any time; the configured logger will automatically record the addition.

**Q: Is `ConsoleLogger` thread‑safe?**  
A: It writes directly to `System.out`, which the JVM synchronizes internally, making it safe for typical multi‑threaded use cases.

**Q: Will limiting the log file size affect the amount of information stored?**  
A: Once the size limit is hit, new entries are either discarded or the logger rolls over to a new file, depending on the implementation you choose.

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-09-21  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

---

## Related Tutorials

- [How to Implement Logging - Exception Handling and Logging Tutorials for GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Implement Asynchronous Logging in Java with GroupDocs.Search – Custom Logger Guide](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Create Search Index Java – GroupDocs.Search Tutorials](/search/java/indexing/)
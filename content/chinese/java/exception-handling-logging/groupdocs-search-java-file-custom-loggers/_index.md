---
date: '2026-09-21'
description: 了解如何在 GroupDocs.Search for Java 中创建 logger、设置 max log size 并使用 console
  logger。
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: 了解如何在 GroupDocs.Search for Java 中创建 logger、设置 max log size 并使用 console
  logger。遵循逐步说明和最佳实践提示。
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: 如何在 GroupDocs.Search 中创建 logger 并限制 log size
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
title: 如何在 GroupDocs.Search for Java 中创建 logger 并限制 log size
type: docs
url: /zh/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# 如何创建日志记录器并限制 GroupDocs.Search for Java 中的日志文件大小

在本教程中，你将 **如何创建日志记录器** 实现用于 GroupDocs.Search，配置最大日志文件大小，并在基于文件和控制台的日志记录之间切换。适当的日志管理可防止在大型索引作业期间磁盘被填满，提升故障排查效率，并在开发时提供即时反馈。我们将从 Maven 设置开始，逐步演示日志记录器配置，最后通过一个简单的搜索查询展示日志记录器的实际效果。

## 快速答案
- **“limit log file size” 是什么意思？** 它限制日志文件的最大大小，防止磁盘上出现不受控制的增长。  
- **哪个日志记录器可以限制日志文件大小？** 内置的 `FileLogger` 接受最大大小参数。  
- **如何使用 console logger java？** 实例化 `ConsoleLogger` 并在 `IndexSettings` 上设置它。  
- **我需要 GroupDocs.Search 的许可证吗？** 试用版可用于评估；生产环境需要商业许可证。  
- **第一步是什么？** 将 GroupDocs.Search 依赖添加到你的 Maven 项目中。  

## 什么是限制日志文件大小？
**limit log file size** 设置告诉日志记录器在文件达到定义的阈值（例如 4 MB）后停止写入新条目。达到限制后，日志记录器要么丢弃后续消息，要么切换到新文件，从而保持磁盘使用可预测。

## 为什么在 GroupDocs.Search 中使用文件和自定义日志记录器？
文件和自定义日志记录器为你提供审计能力、调试洞察和灵活性。在生产环境中，文件日志提供每一次索引和搜索操作的永久记录，而控制台日志在开发期间提供即时反馈。这些日志帮助团队监控性能、追踪错误，并通过保留详细的活动轨迹满足合规要求。

## 前提条件
- GroupDocs.Search for Java ≥ 25.4。  
- JDK 8 或更高版本，配合 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 熟悉 Maven 和 Java 编程的基础知识。  

## 设置 GroupDocs.Search for Java

将库添加到项目中，可使用以下任一方法。

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
下载官方站点上的最新 JAR： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证
通过 [licensing page](https://purchase.groupdocs.com/temporary-license/) 获取试用或购买许可证。

## 如何为 GroupDocs.Search 创建自定义日志记录器
创建自定义日志记录器非常简单，因为 GroupDocs.Search 依赖于 `ILogger` 接口。实现该接口，或继承提供的 `FileLogger` 或 `ConsoleLogger`，即可注入远程转发或日志轮转等额外行为。你还可以添加初始化逻辑，例如打开网络连接，并在日志记录器的关闭方法中确保资源被释放。此方式让你能够与 ELK、Splunk 等监控平台集成。

### 定义锚点
`ILogger` 是 GroupDocs.Search 的核心日志契约；任何实现其 `log(Level, String)` 方法的类都可以成为日志记录器。

### 示例方法（无代码块）
1. 创建实现 `ILogger` 的类。  
2. 重写 `log` 方法，将消息写入你选择的目标（文件、数据库、HTTP 端点）。  
3. 在索引配置中，调用 `settings.setLogger(new YourCustomLogger())`。  

## 如何使用文件日志记录器限制日志文件大小
`FileLogger` 类将日志条目写入磁盘文件，并接受最大大小参数。通过指定大小限制，日志记录器在达到阈值时自动停止添加新条目或创建新文件，从而防止磁盘无序增长。这种行为确保日志记录不会干扰索引性能，同时保持事件记录的简洁。

### 定义锚点
`FileLogger` 是内置日志记录器，可将消息持久化到文本文件，并支持可配置的最大文件大小。

### 步骤指南
1️⃣ **导入必要的包**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **使用文件日志记录器设置索引设置**  
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

3️⃣ **创建或加载索引**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **向索引添加文档**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **执行搜索查询**  
```text
```java
SearchResult result = index.search(query);
```
```

**关键点：** `FileLogger` 构造函数的第二个参数 (`4.0`) 定义了以兆字节为单位的 **set max log size**，直接满足 **limit log file size** 的需求。

## 如何使用 console logger java
当需要即时可见的日志事件时，`ConsoleLogger` 将每条消息写入 `System.out`。该日志记录器轻量且线程安全，适合开发和调试阶段使用。它在不进行文件 I/O 的情况下即时反馈索引进度、搜索查询和错误情况，从而加快迭代测试速度。

### 定义锚点
`ConsoleLogger` 是一种轻量级日志记录器，将日志条目输出到标准控制台流，极其适合调试会话。

### 配置步骤
1️⃣ **导入控制台日志记录器**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **使用控制台日志记录器设置索引设置**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **创建或加载索引**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **添加文档并执行搜索**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**提示：** 控制台日志记录器在开发期间非常理想，因为它会即时打印每条日志，帮助你验证索引和搜索是否如预期运行。

## 实际应用
1. **文档管理系统：** 为每个已索引的文档保留审计轨迹，满足合规要求。  
2. **企业搜索引擎：** 实时监控查询性能和错误率，快速进行 SLA 合规检查。  
3. **法律与合规软件：** 记录搜索词和时间戳以供监管报告使用，日志保留符合规定的保存期限。  

## 性能考虑因素
- **日志大小：** 通过 **set max log size**，避免过度磁盘使用，否则可能减慢 JVM 垃圾回收器的速度。  
- **异步日志记录：** 对于高吞吐场景，可将日志记录器包装在异步队列中，以将 I/O 与索引线程解耦（本指南不涉及实现细节）。  
- **内存管理：** 当 `Index` 对象不再需要时，使用 `index.close()` 释放，以保持 JVM 占用低。  

## 常见问题与解决方案
- **日志路径不可访问：** 确认目录存在且运行 JVM 的用户账户拥有写入权限。  
- **日志记录器未触发：** 确保在创建 `Index` 对象 *之前* 调用 `settings.setLogger(...)`；否则会使用默认日志记录器。  
- **控制台输出缺失：** 确认在显示 `System.out` 的终端中运行应用，并且没有日志框架（如 SLF4J）拦截输出。  

## 常见问题

**Q: `FileLogger` 的第二个参数控制什么？**  
A: 它设置日志文件的最大大小（单位为兆字节），让你能够 **set max log size** 并防止不受控制的增长。

**Q: 我可以同时使用文件和控制台日志记录器吗？**  
A: 可以。创建一个自定义日志记录器，将每次 `log` 调用同时转发给 `FileLogger` 和 `ConsoleLogger`，然后在 `IndexSettings` 中注册该复合日志记录器。

**Q: 初始创建后，如何向索引添加文档？**  
A: 随时调用 `index.add(pathToNewDocs)`；已配置的日志记录器会自动记录此操作。

**Q: `ConsoleLogger` 是线程安全的吗？**  
A: 它直接写入 `System.out`，JVM 内部会同步该流，对典型的多线程使用场景是安全的。

**Q: 限制日志文件大小会影响存储的信息量吗？**  
A: 达到大小限制后，新条目要么被丢弃，要么根据所选实现切换到新文件。  

## 资源
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**最后更新：** 2026-09-21  
**已测试于：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs  

## 相关教程

- [如何实现日志记录 - GroupDocs.Search Java 的异常处理和日志记录教程](/search/java/exception-handling-logging/)
- [在 Java 中使用 GroupDocs.Search 实现异步日志记录 – 自定义日志记录器指南](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [创建搜索索引 Java – GroupDocs.Search 教程](/search/java/indexing/)
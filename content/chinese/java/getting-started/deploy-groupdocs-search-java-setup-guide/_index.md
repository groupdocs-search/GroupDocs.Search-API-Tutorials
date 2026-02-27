---
date: '2026-02-27'
description: 学习如何使用 GroupDocs.Search for Java 创建可搜索的索引，向搜索中添加文件，向节点添加目录，并启用实时索引。
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: 创建可搜索索引（Java）– 部署 GroupDocs.Search for Java
type: docs
url: /zh/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# 创建可搜索索引 Java – 部署 GroupDocs.Search for Java

在当今数据驱动的世界，**创建可搜索索引 java**的应用程序需要高效处理海量文档集合。无论您是构建企业级搜索服务还是较小的项目，良好配置的搜索网络都能显著提升检索速度和相关性。本指南将完整演示如何设置**GroupDocs.Search for Java**，包括将文件添加到搜索以及将目录添加到节点，让您立即开始对文档进行索引。

> **为什么重要：** 可搜索索引将查询延迟从秒级降低到毫秒级，能够随数据增长而扩展，并且让您能够为任何基于 Java 的解决方案添加强大的全文功能——无论是网页门户、桌面应用还是云微服务。

## 快速答复
- **GroupDocs.Search 的主要目的是什么？** 它提供了一个可扩展的基于 Java 的引擎，用于在分布式网络中对文档进行索引和搜索。  
- **我应该使用哪个版本？** 建议在新项目中使用最新的稳定版本（例如 25.4）。  
- **我需要许可证吗？** 提供 30 天免费试用；生产环境需要永久许可证。  
- **我可以同时添加文件和整个目录吗？** 可以——使用 `addFiles` 和 `addDirectories` 辅助方法来导入内容。  
- **需要哪个 Java 版本？** Java 8 或更高版本，并使用 Maven 管理依赖。  
- **实时索引 java 如何工作？** 通过订阅节点事件，您可以在文件更改时触发自动重新索引。

## 什么是“create searchable index java”？

在 Java 中创建可搜索索引意味着构建一种数据结构，将词项映射到包含这些词项的文档，从而实现快速的全文查询。GroupDocs.Search 抽象了繁重的工作，让您专注于提供文档和调优搜索行为。

## 为什么使用 GroupDocs.Search for Java？

- **可扩展的网络架构** – 部署多个节点共享索引工作负载。  
- **丰富的文档格式支持** – PDF、Word、Excel、PowerPoint、图像等。  
- **事件驱动的更新** – 订阅节点事件，以实时保持索引最新。  
- **简易的 Maven 集成** – 在 `pom.xml` 中添加几行代码即可开始索引。

## 使用 GroupDocs.Search 的实时索引 java

GroupDocs.Search 在文件被添加、更新或删除时会触发事件。通过处理这些事件，您可以自动调用 `addFiles` 或 `addDirectories`，确保索引保持同步，无需手动干预。这种方式非常适合文档管理系统、内容门户以及任何数据频繁变化的应用程序。

## 前置条件
- **JDK 8+** 已在开发机器上安装。  
- 如 **IntelliJ IDEA** 或 **Eclipse** 等 IDE。  
- 具备 **Java** 和 **Maven** 的基础知识。  
- 获取 **GroupDocs.Search for Java** 库（下载或通过 Maven）。

## 设置 GroupDocs.Search for Java

### Maven 依赖

将仓库和依赖添加到您的 `pom.xml` 中：

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

> **专业提示：** 通过检查官方发布页面，保持版本号为最新。

您也可以直接从官方网站下载 JAR 包： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证

- **免费试用：** 30 天评估。  
- **临时许可证：** 申请延长测试。  
- **购买：** 生产部署需要购买。

### 基本初始化

创建一个配置对象，指向存放索引文件的文件夹，并定义基础通信端口：

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## 如何使用 GroupDocs.Search 创建 searchable index java？

下面我们将分解您需要的核心功能，包含**将文件添加到搜索**和**将目录添加到节点**，并部署可扩展的网络。

### 功能 1 – 配置和网络设置

配置搜索网络是构建可搜索索引的第一步。

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- **`basePath`** – 索引数据将持久化的目录。  
- **`basePort`** – 起始端口；每个节点将在此值上递增。

### 功能 2 – 部署搜索网络节点

部署节点可将索引工作负载分布到多台机器或多个进程上。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

每个 `SearchNetworkNode` 运行自己的索引服务，使您能够**创建可搜索索引 java**，实现水平扩展。

### 功能 3 – 订阅节点事件

实时更新保持索引与文件系统更改同步。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

通过监听事件，您可以在新文件到达时自动触发重新索引。

### 功能 4 – 将目录添加到网络节点

使用此辅助方法**将目录添加到节点**，递归收集所有受支持的文档。

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### 功能 5 – 将文件添加到网络节点

当您需要细粒度控制时，可单独**将文件添加到搜索**：

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

此方法为您提供了将来自流、云存储或临时位置的文件进行索引的灵活性。

## 常见使用场景
- **企业文档门户**，需要在数千个 PDF 和 Office 文件中实现即时搜索。  
- **法律电子取证平台**，持续添加新证据并需实时可搜索。  
- **内容管理系统**，存储图像、演示文稿和电子表格，并需要全文检索。

## 常见问题与解决方案

| 问题 | 原因 | 解决方案 |
|-------|--------|-----|
| **搜索结果中未出现文档** | 索引未提交 | 在添加文件后调用 `node.getIndexer().commit()`。 |
| **端口冲突错误** | 其他服务使用了 `basePort` | 选择不同的 `basePort` 或检查空闲端口。 |
| **不支持的文件格式** | 库缺少解析器 | 确保文件扩展名受支持，或添加自定义提取器。 |

## 故障排除技巧
- **验证节点健康：** 使用内置的健康检查端点 (`http://localhost:{port}/health`) 确认每个节点正在运行。  
- **监控内存使用情况：** 大批量文档可能导致内存激增；考虑分批索引并定期调用 `commit()`。  
- **检查日志：** GroupDocs.Search 将详细日志写入 `basePath` 文件夹——检查其中的解析错误或网络超时。

## 常见问答

**Q: 我可以在基于云的 Java 应用程序上使用 GroupDocs.Search 吗？**  
A: 可以。该库适用于任何 Java 运行时，您可以将 `basePath` 指向网络挂载的文件夹或本地挂载的云存储。

**Q: 文件更改时如何更新索引？**  
A: 订阅节点事件（见功能 3），并对已修改的路径再次调用 `addFiles` 或 `addDirectories`。

**Q: 部署的节点数量是否有限制？**  
A: 实际上，限制取决于您的硬件和网络带宽。API 本身没有硬性上限。

**Q: 添加新文件后需要重启节点吗？**  
A: 不需要。添加文件会自动触发索引；如果您延迟提交操作，只需在需要时调用 commit。

**Q: 开箱即支持哪些文档格式？**  
A: PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、TXT、HTML 以及多种图像类型。完整列表请参阅官方文档。

**Q: 如何为持续接收上传的文件夹启用实时索引 java？**  
A: 实现文件系统监视器（例如 `java.nio.file.WatchService`），在检测到新文件时调用 `DirectoryAdder.addDirectories(node, path)`。

---

**最后更新：** 2026-02-27  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs
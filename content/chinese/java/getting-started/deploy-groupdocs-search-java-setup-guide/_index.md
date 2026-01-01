---
date: '2025-12-26'
description: 学习如何使用 GroupDocs.Search for Java 创建可搜索的 Java 索引，添加文件进行搜索并向节点添加目录。
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: 创建可搜索索引 Java – 部署 GroupDocs.Search for Java
type: docs
url: /zh/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# 创建可搜索索引 Java – 部署 GroupDocs.Search for Java

在当今数据驱动的世界，**创建可搜索索引 Java** 的应用需要高效地处理海量文档集合。无论您是在构建企业级搜索服务，还是一个小型项目，配置良好的搜索网络都能显著提升检索速度和相关性。在本指南中，我们将完整演示如何设置 **GroupDocs.Search for Java**，包括将文件添加到搜索、将目录添加到节点，让您立即开始为文档建立索引。

## 快速答疑
- **GroupDocs.Search 的主要用途是什么？** 它提供了一个可扩展的基于 Java 的引擎，用于在分布式网络中对文档进行索引和搜索。  
- **应该使用哪个版本？** 推荐使用最新的稳定版（例如 25.4）进行新项目开发。  
- **需要许可证吗？** 提供 30 天免费试用；正式生产环境必须使用永久许可证。  
- **可以同时添加文件和整个目录吗？** 可以 – 使用 `addFiles` 和 `addDirectories` 辅助方法导入内容。  
- **需要哪个 Java 版本？** Java 8 或更高版本，并使用 Maven 管理依赖。

## 什么是 “创建可搜索索引 Java”？
在 Java 中创建可搜索索引意味着构建一种数据结构，将词项映射到包含这些词项的文档，从而实现快速的全文查询。GroupDocs.Search 负责繁重的底层工作，让您专注于提供文档和调优搜索行为。

## 为什么使用 GroupDocs.Search for Java？
- **可扩展的网络架构** – 部署多个节点共享索引工作负载。  
- **丰富的文档格式支持** – PDF、Word、Excel、PowerPoint、图片等。  
- **事件驱动的更新** – 订阅节点事件，实现实时索引刷新。  
- **简易的 Maven 集成** – 在 `pom.xml` 中添加几行代码即可开始索引。

## 前置条件
- 已在开发机器上安装 **JDK 8+**。  
- 使用 **IntelliJ IDEA** 或 **Eclipse** 等 IDE。  
- 具备 **Java** 与 **Maven** 的基础知识。  
- 获取 **GroupDocs.Search for Java** 库（下载或通过 Maven）。

## 设置 GroupDocs.Search for Java

### Maven 依赖
在 `pom.xml` 中添加仓库和依赖：

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

> **小技巧：** 通过官方发布页面保持版本号为最新。

您也可以直接从官方网站下载 JAR 包：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 许可证获取
- **免费试用：** 30 天评估。  
- **临时许可证：** 用于延长测试。  
- **购买：** 生产部署必须购买。

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

## 如何使用 GroupDocs.Search 创建可搜索索引 Java？

下面我们分解实现 **将文件添加到搜索** 与 **将目录添加到节点** 的核心功能，同时演示如何部署可扩展的网络。

### 功能 1 – 配置与网络设置
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

- **`basePath`** – 索引数据持久化的目录。  
- **`basePort`** – 起始端口；每个节点将在此基础上递增。

### 功能 2 – 部署搜索网络节点
部署节点可将索引工作负载分布到多台机器或多个进程。

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

每个 `SearchNetworkNode` 都运行自己的索引服务，使您能够 **创建可搜索索引 Java** 并实现水平扩展。

### 功能 3 – 订阅节点事件
实时更新可保持索引与文件系统的同步。

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
使用此辅助方法 **将目录添加到节点**，递归收集所有受支持的文档。

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
当需要细粒度控制时，可单独 **将文件添加到搜索**：

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

该方法让您能够索引来自流、云存储或临时位置的文件。

## 常见问题与解决方案
| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **搜索结果中没有文档** | 索引未提交 | 在添加文件后调用 `node.getIndexer().commit()` |
| **端口冲突错误** | 其他服务占用了 `basePort` | 更换 `basePort` 或检查空闲端口 |
| **不支持的文件格式** | 库缺少相应解析器 | 确认文件扩展名受支持，或添加自定义提取器 |

## 常见问答

**问：我可以在基于云的 Java 应用中使用 GroupDocs.Search 吗？**  
答：可以。该库兼容任何 Java 运行时，您可以将 `basePath` 指向网络挂载文件夹或本地挂载的云存储。

**问：文件变更后如何更新索引？**  
答：订阅节点事件（见功能 3），对修改后的路径再次调用 `addFiles` 或 `addDirectories`。

**问：可以部署的节点数量有限制吗？**  
答：实际限制取决于硬件和网络带宽。API 本身没有硬性上限。

**问：添加新文件后需要重启节点吗？**  
答：不需要。添加文件会自动触发索引，只在您延迟提交时需要手动调用 commit。

**问：开箱即支持哪些文档格式？**  
答：PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、TXT、HTML 以及多种图片格式。完整列表请参阅官方文档。

---

**最后更新：** 2025-12-26  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs
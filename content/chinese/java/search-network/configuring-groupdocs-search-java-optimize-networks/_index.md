---
date: '2026-01-16'
description: 学习如何在 Java 中配置 GroupDocs 搜索网络，并向索引添加同义词以提升搜索效率。
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: 在 Java 中配置 GroupDocs.Search 网络 – 提升搜索
type: docs
url: /zh/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# 在 Java 中配置 GroupDocs.Search 网络 – 提升搜索

在当今数据驱动的应用程序中，**configure groupdocs search network** 是实现跨海量文档集合快速、精准结果的关键步骤。无论您是构建企业级搜索门户还是扩展现有解决方案，配置良好的 GroupDocs.Search 网络都能实现水平扩展、添加同义词支持，并保持低延迟。在本教程中，您将学习如何使用 Java 设置、部署和微调 GroupDocs.Search 网络，以及添加同义词到索引和管理节点生命周期的实用技巧。

## 快速答案
- **配置 GroupDocs.Search 网络的主要好处是什么？** 它实现了分布式索引和查询，提升了性能和可扩展性。  
- **运行示例是否需要许可证？** 免费试用可用于开发；生产环境需要商业许可证。  
- **可以在不重建索引的情况下添加同义词吗？** 可以——在运行时使用同义词字典来 **add synonyms to index**。  
- **我可以部署多少个节点？** 您可以根据基础设施的容量部署任意数量的节点；每个节点在独立的端口上运行。  

## 什么是配置 GroupDocs.Search 网络？
配置 GroupDocs.Search 网络是指定文件夹结构、端口和节点设置，使多个 JVM 实例能够协同进行索引和搜索。此设置会创建一个 master‑node（主节点），协调工作节点（shards）并确保查询在整个数据集上执行。

## 为什么要配置 GroupDocs.Search 网络？
- **可扩展性** – 将索引负载分布到多台机器上。  
- **可靠性** – 节点可以在不中断服务的情况下添加或移除。  
- **搜索相关性** – 添加同义词到索引以获得更丰富的结果。  
- **性能** – 并行查询执行可降低响应时间。  

## 前提条件
- Java Development Kit (JDK) 8 或更高  
- 用于构建项目的 Maven  
- 对 Java 语法的基本了解  
- 获取 GroupDocs.Search for Java 库（通过 Maven 或官方发布页面下载）  

## 为 Java 设置 GroupDocs.Search

将仓库和依赖添加到您的 Maven **pom.xml** 中：

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

或者，直接从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下载最新版本。

### 获取许可证
- **免费试用** – 免费探索核心功能。  
- **临时许可证** – 为短期测试解锁全部功能。  
- **商业许可证** – 生产部署时必需。  

### 基本初始化和设置
创建一个简单的 Java 类，以验证库是否正确加载：

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## 配置 GroupDocs.Search 网络的分步指南

### 1. 配置搜索网络
定义基础文档文件夹以及节点通信的起始端口。

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – 存放字典（例如同义词文件）的路径。  
- **basePort** – 第一个端口；后续节点在此基础上递增。  

### 2. 部署搜索网络节点
启动多个共享相同配置的工作节点。

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

每个节点在其独立的端口（basePort + index）上运行，并持有整体索引的一个 shard。  

### 3. 订阅节点事件
通过将事件监听器附加到 master node（主节点），监控健康状态、索引进度和错误情况。

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

事件回调使您能够对节点启动/停止、索引完成以及意外故障作出响应。  

### 4. 向节点的 Indexer 添加同义词  
通过在运行时 **add synonyms to index** 来提升相关性。

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – 应视为等价的词数组。  
- **clearBeforeAdding** – 如果想替换已有条目，请设为 `true`。  

### 5. 添加用于索引的目录
告诉 master node（主节点）哪些文件夹包含您希望可搜索的文档。

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

该方法递归扫描目录并将文件分配到各个 shard。  

### 6. 在网络中执行文本搜索
在所有节点上执行查询，可选地强制精确匹配行为。

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

当需要严格的词项匹配且不进行词干提取时，将 `exactMatchOnly` 切换为 `true`。  

### 7. 关闭网络节点
处理完成后优雅地释放资源。

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

正确的关闭可防止内存泄漏并保持 JVM 健康。  

## 实际应用
| 场景 | 网络如何帮助 |
|----------|-----------------------|
| **Enterprise Search** | 将索引分布到数据中心服务器，以支持 PB 级规模的语料库。 |
| **Document Management** | 添加同义词到索引，使用户即使使用不同术语也能找到文档。 |
| **E‑commerce Catalog** | 部署区域特定节点，以快速提供本地化的产品搜索。 |
| **Content Management** | 在编辑者向特定目录添加新文件时，保持内容可搜索。 |

## 常见问题与解决方案
- **端口冲突** – 确保每个节点的端口（basePort + index）是空闲的；如有需要，调整 `basePort`。  
- **同义词未生效** – 确认在添加词条后调用了 `indexer.setDictionary(dictionary)`。  
- **节点无响应** – 订阅事件；查找 `NodeFailed` 回调以诊断网络问题。  
- **关闭时内存泄漏** – 对每个已部署的节点始终调用 `node.close()`。  

## 常见问答

**Q: 部署多个节点如何提升搜索性能？**  
A: 每个节点对数据的一个 shard 进行索引，允许并行处理，并通过共享工作负载降低查询延迟。  

**Q: 能否在不重新索引现有文档的情况下添加同义词？**  
A: 可以，您可以在运行时通过同义词字典 **add synonyms to index**；更改会立即对新查询生效。  

**Q: 订阅节点事件是强制性要求吗？**  
A: 虽然基本操作不需要，但订阅事件可以让您了解节点健康状况，并帮助您及时对故障作出响应。  

**Q: 管理节点资源的最佳实践是什么？**  
A: 定期关闭空闲节点，监控 JVM 内存使用，并在非高峰时段回收节点，以保持资源消耗最佳。  

**Q: GroupDocs.Search 是否支持非文本格式，如 PDF 或图像？**  
A: 当然。该库可以从 PDF、Office 文件中提取文本，甚至对图像进行 OCR，使其开箱即用地可搜索。  

---

**最后更新：** 2026-01-16  
**测试环境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs
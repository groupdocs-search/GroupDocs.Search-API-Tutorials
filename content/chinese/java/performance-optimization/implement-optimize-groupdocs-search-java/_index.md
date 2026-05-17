---
date: '2026-01-16'
description: 学习如何使用 GroupDocs.Search for Java 执行文本搜索并优化搜索性能。包括设置搜索网络、创建可搜索索引以及删除文档索引的步骤。
keywords:
- GroupDocs.Search for Java
- search network optimization
- document indexing with GroupDocs
title: 使用 GroupDocs.Search for Java 执行文本搜索
type: docs
url: /zh/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# 使用 GroupDocs.Search for Java 执行文本搜索
## 性能优化

## 如何使用 GroupDocs.Search for Java 实现和优化搜索网络

### 介绍
在当今数据驱动的世界中，能够 **快速执行文本搜索** 并跨海量文档集合检索信息是一项竞争优势。无论您是在构建内部知识库、法律案件存储库，还是电子商务产品目录，经过精心调优的搜索网络都能显著提升用户满意度。在本指南中，您将学习如何 **设置搜索网络**、**创建可搜索索引**、**优化搜索性能**，以及在需要时 **删除文档索引**——全部使用 GroupDocs.Search for Java。

**您将学习**
- 使用 GroupDocs.Search 配置搜索网络  
- 在网络中部署节点  
- 高效索引文档 (`index documents java`)  
- 在网络中执行文本搜索 (`perform text search`)  
- 从索引中删除特定文档 (`delete documents index`)  

让我们深入了解如何利用这些功能创建优化的搜索体验。

## 快速答案
- **GroupDocs.Search for Java 的主要目的是什么？** 它提供跨多种文档格式的全文搜索。  
- **如何在分布式环境中执行文本搜索？** 部署搜索网络，在主节点上索引文档，然后在任意节点查询。  
- **是否可以在不重新构建索引的情况下删除文档？** 可以，使用 Delete API 删除选定文件。  
- **需要哪个 Java 版本？** JDK 8 或更高。  
- **生产环境是否需要许可证？** 需要有效的 GroupDocs.Search 许可证；提供免费试用。

## 什么是“perform text search”？
执行文本搜索意味着查询全文索引，以检索包含指定关键字或短语的文档。GroupDocs.Search 构建倒排索引，使这些查找即使在成千上万的文件中也极其快速。

## 为什么要设置搜索网络？
搜索网络将索引和查询工作负载分布到多个节点，帮助您 **优化搜索性能**、实现水平扩展，并保持高可用性。这种架构非常适合企业级文档库，在此类环境中延迟和吞吐量至关重要。

### 先决条件
- **必需库：** GroupDocs.Search for Java 版本 25.4（最新）。  
- **环境：** Java JDK 8+，Maven。  
- **知识：** 基础 Java 编程以及网络概念的了解。

### 设置 GroupDocs.Search for Java
首先，将 GroupDocs.Search 集成到您的 Java 项目中，使用以下设置：

#### Maven 设置
在 `pom.xml` 文件中添加仓库和依赖：

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

#### 直接下载
或者，您可以[直接从 GroupDocs 下载最新版本](https://releases.groupdocs.com/search/java/)。

#### 许可证获取
GroupDocs 提供免费试用，帮助您在购买前评估其功能。您可以通过其[购买页面](https://purchase.groupdocs.com/temporary-license/)获取临时许可证。这将在测试阶段启用全部功能。

#### 基本初始化和设置
在 Java 应用程序中初始化 GroupDocs.Search：

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

### 实现指南

#### 配置搜索网络
**概述：** 为搜索网络设定基础路径和端口，以便节点之间能够有效通信。

##### 步骤 1：定义基础配置

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **参数：**  
  - `basePath`：网络操作的目录路径。  
  - `basePort`：搜索网络使用的端口号。

##### 步骤 2：故障排除
确保您指定的端口未被防火墙阻塞或被其他应用占用。必要时进行调整，以避免冲突。

#### 部署搜索网络节点
**概述：** 使用上述配置，在网络中部署节点，实现分布式索引和搜索。

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **关键配置选项：**  
  - **Base Path & Port：** 这些值应与初始配置中的保持一致，以确保一致性。

#### 索引文档（`create searchable index`）
**概述：** 使用主节点高效地将文档添加到搜索索引中。

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **目的：**  
  - `masterNode`：负责文档索引的主节点。  
  - `documentsPath`：包含文档的目录路径。

##### 故障排除提示
验证文档路径是否正确且可访问。确保拥有读取这些目录的权限。

#### 在网络中搜索文本（`perform text search`）
**概述：** 在已索引的网络中执行全面的文本搜索。

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **参数：**  
  - `query`：您要搜索的文本。  
  - `masterNode`：执行搜索的节点。

#### 从索引中删除文档（`delete documents index`）
**概述：** 使用文件路径从索引中移除特定文档。

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **方法目的：**  
  - `node`：执行删除操作的目标节点。  
  - `filePaths`：要从索引中移除的文档路径。

##### 故障排除
确保文件路径精确且文件确实存在于目录中。如问题仍然存在，请检查网络权限和连通性。

### 实际应用
1. **企业文档管理：** 简化内部知识检索。  
2. **法律案件分析：** 快速定位多个存储库中的相关案件文件。  
3. **电子商务平台：** 通过索引描述和评论提升产品搜索速度。  
4. **学术研究：** 高效搜索大型数字图书馆中的论文和学位论文。  
5. **客户支持系统：** 让客服人员即时搜索历史工单，缩短响应时间。

### 性能考虑因素
- **优化索引速度：** 在非高峰时段增量添加新文档，以保持低延迟。  
- **资源使用指南：** 监控 CPU 和内存，尤其是在扩展节点数量时。  
- **Java 内存管理：** 根据工作负载调优 JVM 堆设置（例如，`-Xmx2g` 适用于中等规模索引）。

### 结论
通过本指南，您已学习如何 **设置搜索网络**、**创建可搜索索引**、**执行文本搜索**，以及使用 GroupDocs.Search for Java **删除文档索引**。这些功能使您能够在分布式环境中实现快速、可靠的文档检索。

**下一步**
- 试验不同的节点配置，以找到适合工作负载的最佳平衡。  
- 深入了解高级索引选项，如自定义分析器和相关性调优。  
- 探索与其他 GroupDocs 产品的集成，实现端到端的文档处理。

## 常见问题

**Q: GroupDocs.Search for Java 的主要使用场景是什么？**  
A: 它提供跨多种文档格式的全文搜索，使您能够在大型仓库中 **执行文本搜索**。

**Q: 如何提升大型网络的搜索速度？**  
A: 部署更多节点，调优 JVM 堆，并在低流量时段安排索引，以 **优化搜索性能**。

**Q: 是否可以在不重新索引整个集合的情况下删除单个文档？**  
A: 可以，使用示例代码中的 **delete documents index** API 删除特定文件。

**Q: 开发阶段是否需要许可证？**  
A: 免费试用许可证足以进行测试；生产部署需要商业许可证。

**Q: 能否同时索引 PDF、Word 文件和电子邮件？**  
A: 完全可以——GroupDocs.Search 开箱即支持多种格式。

---

**最后更新：** 2026-01-16  
**测试版本：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs
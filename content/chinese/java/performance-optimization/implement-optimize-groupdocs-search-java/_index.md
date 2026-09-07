---
date: '2026-07-07'
description: 了解如何使用 GroupDocs.Search for Java 删除索引、执行 Java 全文搜索，并优化搜索性能。提供网络设置和索引的分步指南。
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: 如何使用 GroupDocs.Search 删除索引并执行 Java 全文搜索。请按照本指南设置搜索网络、创建可搜索索引并优化搜索性能。
og_title: 如何使用 GroupDocs.Search for Java 删除索引并执行全文搜索
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: 如何使用 GroupDocs.Search for Java 删除索引并执行全文搜索
type: docs
url: /zh/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# 如何删除索引并使用 GroupDocs.Search for Java 执行文本搜索

在当今数据驱动的世界中，快速 **how to delete index** 同时提供闪电般的 Java 全文搜索能力是一项竞争优势。无论您是构建内部知识库、法律案件存储库，还是电子商务产品目录，经过良好调优的搜索网络都能显著提升用户满意度。在本指南中，您将学习如何 **设置搜索网络**、**创建可搜索索引**、**优化搜索性能**，以及在需要时 **从索引中删除文档**——全部使用 GroupDocs.Search for Java。

## 快速答案
- **What is the main purpose of GroupDocs.Search for Java?** 它提供跨 50 多种文档格式的全文搜索，实现快速关键字检索。  
- **How do I perform text search in a distributed environment?** 部署搜索网络，在主节点上建立文档索引，然后在任意节点进行查询。  
- **Can I delete documents from the index without rebuilding it?** 是的，使用 Delete API 删除选定文件，实际上可以 *how to delete index* 而无需完整重新索引。  
- **What Java version is required?** JDK 8 或更高版本。  
- **Is a license needed for production?** 需要有效的 GroupDocs.Search 许可证；提供免费试用版。

## 什么是“perform text search”？
执行文本搜索是指查询全文索引，以检索包含指定关键字或短语的文档。GroupDocs.Search 构建倒排索引，使这些查找即使在成千上万的文件中也极其快速。

## 为什么要设置搜索网络？
搜索网络将索引和查询工作负载分布在多个节点上，使您能够 **优化搜索性能**、水平扩展并保持高可用性。这种架构非常适合对延迟和吞吐量有要求的企业级文档库。

## 如何使用 GroupDocs.Search for Java 实现并优化搜索网络
加载配置，启动主节点，然后添加共享相同基础路径和端口的工作节点。以这种方式部署网络，使任何节点都能处理索引或查询请求，即使文档数量增长到数十万，也能提供一致的响应时间。

### 步骤概览
1. **定义基础配置** 包含共享目录和 TCP 端口。  
2. **启动主节点** 来管理索引并协调工作节点。  
3. **添加工作节点** 连接到主节点，实现并行索引和搜索。  
4. **监控资源使用情况** 并调优 JVM 堆设置，以保持低延迟。

## 如何在 GroupDocs.Search for Java 中删除索引
`SearchNode` 表示 GroupDocs.Search 网络中的一个节点，负责管理索引和查询操作。`delete` 方法从索引中删除指定的文档。

### 直接删除步骤
- 在 `SearchNode` 实例上调用 `delete` 方法。  
- 提供相对文件路径数组。  
- 提交更改；索引会立即刷新，后续搜索不再返回已删除的文件。

## 什么是搜索网络？
**搜索网络** 是一组相互连接的节点集群，共享公共索引库，支持分布式索引和查询执行。它实现了大规模文档集合的水平扩展和容错能力。

## 如何创建可搜索索引（index documents java）
`add` 方法将文档索引到搜索索引中。使用 `add` 方法将文档添加到主节点；网络会将更改传播到所有工作节点。这种方式确保每个节点都能针对最新索引提供查询，而无需额外的同步步骤。

### 关键操作
- 将主节点指向包含源文件的文件夹。  
- 调用索引例程；网络处理每个文件并更新倒排索引。  
- 验证索引文件是否出现在指定的存储目录中。

## 如何移除已索引文件（remove indexed files）
当文档过期时，使用其路径调用 `delete` API。系统会从倒排索引中移除该文件的条目，释放存储空间并防止出现陈旧结果。

## 设置 GroupDocs.Search for Java
首先，使用以下设置将 GroupDocs.Search 集成到您的 Java 项目中：

### Maven 设置
在 `pom.xml` 文件中添加仓库和依赖项：

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

### 直接下载
或者，您可以[直接从 GroupDocs 下载最新版本](https://releases.groupdocs.com/search/java/)。

### 获取许可证
GroupDocs 提供免费试用，允许您在购买前评估其功能。您可以通过其[购买页面](https://purchase.groupdocs.com/temporary-license/)的步骤获取临时许可证。这将在您的测试阶段启用全部功能。

### 基本初始化和设置
在您的 Java 应用程序中使用以下代码初始化 GroupDocs.Search：

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## 实施指南

### 配置搜索网络
**概述：** 为搜索网络建立基础路径和端口，使节点能够有效通信。

#### 步骤 1：定义基础配置
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

#### 步骤 2：故障排除
确保您指定的端口未被防火墙阻止或被其他应用占用。必要时进行调整以避免冲突。

### 部署搜索网络节点
**概述：** 使用您的配置，在网络中部署节点，实现分布式索引和搜索。

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **关键配置选项：**  
  - **Base Path & Port（基础路径和端口）：** 这些值应与初始配置中使用的保持一致，以确保一致性。

### 索引文档（`create searchable index`）
**概述：** 使用主节点高效地将文档添加到搜索索引中。

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **目的：**  
  - `masterNode`：管理文档索引的主节点。  
  - `documentsPath`：包含文档的目录路径。

#### 故障排除提示
验证文档路径是否正确且可访问。确保权限允许读取这些目录。

### 在网络中搜索文本（`perform text search`）
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

### 从索引中删除文档（`delete documents index`）
**概述：** 使用文件路径从索引中删除特定文档。

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

#### 故障排除
确保文件路径准确且文件存在于目录中。如果问题仍然存在，请检查网络权限和连通性。

## 实际应用
1. **企业文档管理：** 简化内部知识检索。  
2. **法律案件分析：** 快速定位跨多个存储库的相关案件文件。  
3. **电子商务平台：** 通过索引描述和评论提升产品搜索速度。  
4. **学术研究：** 高效搜索大型数字图书馆中的论文和论文集。  
5. **客户支持系统：** 通过让客服人员即时搜索过去的工单来降低响应时间。

## 性能考虑因素
- **优化索引速度：** 在非高峰时段增量添加新文档，以保持低延迟。  
- **资源使用指南：** 监控 CPU 和内存，特别是在扩展节点数量时。  
- **Java 内存管理：** 根据工作负载调优 JVM 堆设置（例如，中等规模索引使用 `-Xmx2g`）。

## 结论
通过本指南，您已经学习了如何使用 GroupDocs.Search for Java **设置搜索网络**、**创建可搜索索引**、**执行文本搜索**以及 **删除文档索引**。这些功能在分布式环境中实现快速、可靠的文档检索。

**下一步**  
- 试验不同的节点配置，以找到适合您工作负载的最佳平衡。  
- 深入了解高级索引选项，如自定义分析器和相关性调优。  
- 探索与其他 GroupDocs 产品的集成，实现端到端的文档处理。

## 常见问题

**Q: GroupDocs.Search for Java 的主要使用场景是什么？**  
A: 它提供跨多种文档格式的全文搜索，使您能够在大型仓库中 **perform text search**。

**Q: 如何在大型网络中提升搜索速度？**  
A: 部署额外节点，调优 JVM 堆，并在低流量时段安排索引，以 **optimize search performance**。

**Q: 是否可以在不重新索引整个集合的情况下删除单个文档？**  
A: 可以，使用代码示例中展示的 **delete documents index** API 删除特定文件。

**Q: 开发阶段需要许可证吗？**  
A: 免费试用许可证足以进行测试；生产部署需要商业许可证。

**Q: 我可以同时索引 PDF、Word 文件和电子邮件吗？**  
A: 当然——GroupDocs.Search 开箱即支持多种格式。

---

**最后更新：** 2026-07-07  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs

## 相关教程

- [如何在 Java 中使用 GroupDocs.Search 指南进行文本索引](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [使用高级索引技术优化 GroupDocs.Search for Java 的搜索性能](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [使用 GroupDocs.Search Java 改善查询性能：优化索引与搜索](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
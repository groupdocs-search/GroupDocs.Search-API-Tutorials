---
date: '2026-05-02'
description: 了解如何使用 GroupDocs.Search for Java 配置搜索并启用实时搜索更新。提供网络设置、节点部署和索引的逐步指南。
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: 如何在 Java 中使用 GroupDocs.Search 配置搜索 - 配置与部署指南
type: docs
url: /zh/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 配置搜索

在当今快速发展的数字世界中，**如何配置搜索**的效率可以决定项目的成败。无论您处理的是成千上万的合同、研究论文还是内部报告，一个设计良好的搜索网络都能让您在几秒钟内定位到正确的文档。本教程将指导您配置搜索网络、部署节点，并使用 GroupDocs.Search for Java 启用 **实时搜索更新**。

## 快速答案
- **搜索网络的主要目的是什么？** 将索引和查询处理分布在多个节点上，以实现可扩展性和速度。  
- **需要哪个库版本？** GroupDocs.Search for Java v25.4 或更高。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要商业许可证。  
- **实时更新如何处理？** 通过订阅在索引更改时触发的节点事件。  
- **我可以动态添加新的文档文件夹吗？** 是的——使用索引器的 `addDirectories` 方法。

## 在 GroupDocs 环境中，“如何配置搜索”是什么？
配置搜索意味着建立一个 **搜索网络**，该网络了解文档所在位置、节点之间的通信方式以及索引的协调方式。网络配置完成后，您可以在不中断服务的情况下添加或移除节点，确保持续访问最新的搜索结果。

## 为什么使用 GroupDocs.Search for Java？
- **可扩展性：** 将工作负载分布在多台机器上。  
- **实时更新：** 立即在网络中反映新索引的文件。  
- **易于集成：** 简单的 Maven 设置和清晰的 Java API。  
- **企业级：** 处理大型语料库和复杂查询场景。

## 前提条件
- **Java Development Kit (JDK) 8+** 已安装。  
- **Maven** 用于依赖管理。  
- 熟悉 Java、Maven 和搜索概念的基础知识。

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

**直接下载：** 您也可以从 [GroupDocs.Search for Java 发布](https://releases.groupdocs.com/search/java/) 获取该库。

### 获取许可证
- **免费试用：** 获取试用许可证以探索所有功能。  
- **临时许可证：** 请求延长评估期限。  
- **商业许可证：** 生产部署所需。  

### 基本初始化
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## 如何在 Java 中配置搜索网络

### 步骤 1：导入所需包
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### 步骤 2：配置网络
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **参数：** `basePath` 指向您的文档文件夹；`basePort` 是用于节点通信的 TCP 端口。

## 部署搜索网络节点

### 步骤 1：导入部署包
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### 步骤 2：部署节点
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **主节点：** 协调所有节点的搜索和索引。您可以 **配置主节点** 设置，例如分片分配和健康检查。

## 订阅节点事件以实现实时搜索更新

### 步骤 1：导入事件包
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 步骤 2：订阅主节点事件
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **事件处理：** 在文档被添加、更新或删除时启用 **实时搜索更新**。

## 添加目录进行索引

### 步骤 1：导入索引器包
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 步骤 2：添加文档目录
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **动态索引：** 使用 `addDirectories` 方法 **将目录添加到索引**，无需重启网络即可实现。

## 检索已索引的文档

### 步骤 1：导入搜索器包
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### 步骤 2：检索文档信息
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **分片管理：** 通过在分片之间分配文档，高效处理大型数据集。要 **优化分片大小**，请监控分片统计信息并在后续版本中调整 `shardSize` 配置。

## 为什么这对您的项目很重要
一个正确配置的搜索网络可以消除瓶颈，降低延迟，并确保用户始终看到文档的最新版本。实时更新以及 **将目录添加到索引** 而无需停机的能力，对律师事务所、研究机构以及任何处理不断变化文档集合的组织尤为有价值。

## 实际应用
1. **企业文档管理：** 在数百万文件中实现搜索集中化。  
2. **律师事务所：** 快速定位案件文件、合同和证据。  
3. **学术研究：** 索引期刊和论文，实现即时检索。

## 性能考虑
- **优化索引：** 安排定期的索引刷新并清除陈旧数据。  
- **内存管理：** 监控 JVM 堆，特别是在处理大型分片时。  
- **可扩展性规划：** 随着语料库增长添加节点；网络会自动平衡负载。  
- **优化分片大小：** 较小的分片可提升查询延迟，而较大的分片可降低开销。根据硬件和查询模式进行调优。

## 常见问题与解决方案
| 问题 | 原因 | 解决方案 |
|-------|-------|-----|
| 节点无法连接 | 端口冲突或防火墙 | 确保 `basePort` 已打开且未被其他服务占用 |
| 索引未更新 | 缺少事件订阅 | 部署后调用 `SearchNetworkNodeEvents.subscribe(masterNode)` |
| 内存不足错误 | 加载了过多的大型分片 | 减小分片大小或增加 JVM 堆（`-Xmx` 标志） |

## 常见问题

**问：网络运行后我可以添加新目录吗？**  
答：是的——使用 `indexer.addDirectories()` 方法；已订阅的事件将实时传播更新。

**问：如何监控节点健康？**  
答：每个 `SearchNetworkNode` 提供状态 API；可与您选择的监控工具集成。

**问：可以在单独的机器上运行主节点吗？**  
答：完全可以。只需确保所有节点使用相同的 `basePort` 并且能够在网络上相互访问。

**问：支持哪些文件格式？**  
答：GroupDocs.Search 开箱即支持 PDF、Word、Excel、PowerPoint、纯文本等多种格式。

**问：添加新节点后需要重启网络吗？**  
答：不需要——节点可以动态添加或移除；主节点会自动重新平衡分片。

## 结论
现在，您已经了解了使用 GroupDocs.Search for Java **如何配置搜索**，可以构建快速、可扩展且可靠的文档搜索解决方案，以跟上组织的增长步伐。将这些模式应用于任何行业，以创建实时、分布式的搜索体验。

---

**最后更新：** 2026-05-02  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs
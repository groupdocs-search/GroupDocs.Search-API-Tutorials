---
date: '2026-01-08'
description: 了解如何使用 GroupDocs.Search for Java 配置搜索并启用实时搜索更新。提供网络设置、节点部署和索引的逐步指南。
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 如何在 Java 中使用 GroupDocs.Search 配置搜索 - 配置与部署指南
type: docs
url: /zh/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Search 配置搜索

在当今快速发展的数字世界，**如何高效配置搜索** 能决定项目的成败。无论您处理的是成千上万份合同、研究论文还是内部报告，一个设计良好的搜索网络都能让您在几秒钟内定位到正确的文档。本教程将带您一步步配置搜索网络、部署节点，并使用 GroupDocs.Search for Java 实现 **实时搜索更新**。

## 快速回答
- **搜索网络的主要目的是什么？** 将索引和查询处理分布到多个节点，以实现可扩展性和速度。  
- **需要哪个库版本？** GroupDocs.Search for Java v25.4 或更高。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要商业许可证。  
- **实时更新是如何处理的？** 通过订阅在索引更改时触发的节点事件。  
- **可以动态添加新的文档文件夹吗？** 可以——使用索引器的 `addDirectories` 方法。

## 在 GroupDocs 环境中，“如何配置搜索”指的是什么？
配置搜索意味着建立一个 **搜索网络**，该网络了解文档所在位置、节点之间的通信方式以及索引的协调方式。网络配置完成后，您可以在不中断服务的情况下添加或移除节点，确保持续获取最新的搜索结果。

## 为什么要使用 GroupDocs.Search for Java？
- **可扩展性：** 将工作负载分布到多台机器。  
- **实时更新：** 新索引的文件会立即在网络中同步。  
- **易于集成：** 简单的 Maven 设置和清晰的 Java API。  
- **企业级：** 能处理大规模语料库和复杂查询场景。

## 前置条件
- 已安装 **Java Development Kit (JDK) 8+**。  
- 已安装 **Maven** 用于依赖管理。  
- 具备 Java、Maven 和搜索概念的基本了解。  

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

**直接下载：** 您也可以从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 获取库。

### 许可证获取
- **免费试用：** 获取试用许可证以探索全部功能。  
- **临时许可证：** 申请延长评估期。  
- **商业许可证：** 生产部署必须使用。

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
- **参数：** `basePath` 指向您的文档文件夹；`basePort` 是节点通信使用的 TCP 端口。

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
- **主节点：** 协调所有节点的搜索和索引工作。

## 订阅节点事件以实现实时搜索更新

### 步骤 1：导入事件包
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 步骤 2：订阅主节点事件
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **事件处理：** 当文档被添加、更新或删除时，启用 **实时搜索更新**。

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
- **动态索引：** 可随意添加文件夹，网络会自动进行索引。

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
- **分片管理：** 通过在分片之间分配文档，高效处理大规模数据集。

## 实际应用场景
1. **企业文档管理：** 在数百万文件中实现统一搜索。  
2. **律所：** 快速定位案件文件、合同和证据。  
3. **学术研究：** 索引期刊和论文，实现即时检索。

## 性能考虑因素
- **优化索引：** 定期安排索引刷新并清除陈旧数据。  
- **内存管理：** 监控 JVM 堆内存，尤其在处理大分片时。  
- **可扩展性规划：** 随着语料库增长添加节点，网络会自动负载均衡。

## 常见问题与解决方案
| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 节点无法连接 | 端口冲突或防火墙 | 确保 `basePort` 已打开且未被其他服务占用 |
| 索引未更新 | 缺少事件订阅 | 部署后调用 `SearchNetworkNodeEvents.subscribe(masterNode)` |
| 内存溢出错误 | 加载了过多大型分片 | 减小分片大小或增加 JVM 堆内存 (`-Xmx` 参数) |

## 常见问答

**问：网络运行后可以添加新目录吗？**  
答：可以——使用 `indexer.addDirectories()` 方法；已订阅的事件会实时传播更新。

**问：如何监控节点健康状态？**  
答：每个 `SearchNetworkNode` 都提供状态 API，可与您选择的监控工具集成。

**问：可以在不同机器上运行主节点吗？**  
答：完全可以。只需确保所有节点使用相同的 `basePort` 并能够相互网络访问。

**问：支持哪些文件格式？**  
答：GroupDocs.Search 开箱即支持 PDF、Word、Excel、PowerPoint、纯文本等多种格式。

**问：添加新节点后需要重启网络吗？**  
答：不需要——节点可以动态添加或移除，主节点会自动重新平衡分片。

## 结论
现在，您已经完整掌握了使用 GroupDocs.Search for Java **如何配置搜索** 的全部步骤，从初始设置到实时更新以及分布式索引。将这些模式应用于实际项目，可构建快速、可扩展且可靠的文档搜索解决方案，满足各行业需求。

---

**最后更新：** 2026-01-08  
**测试环境：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs
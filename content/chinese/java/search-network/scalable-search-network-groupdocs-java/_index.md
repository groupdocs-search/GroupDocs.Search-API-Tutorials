---
date: '2026-01-24'
description: 学习如何使用 GroupDocs.Search Java 配置基础端口 groupdocs，以实现可扩展的搜索网络，优化检索速度，并搭建多节点系统。
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: 在 Java Search Network 中配置基础端口 groupdocs
type: docs
url: /zh/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

配置建快速、可靠搜索基础设施的基础步骤。无论您处理成千上万的 PDF，还是在多台服务器上扩展，正确设置端口和路径可确保每个节点之间通信不冲突。本教程将逐步讲解所有细节——从先决条件到完整的多节点配置——帮助您自信地使用 GroupDocs.Search for Java 启动可扩展的搜索网络。

## 快速答案
- **主要目的是什么？** 为每个搜索节点设置唯一的端口和目录，防止冲突。
- **我需要许可证吗？** 是的，生产环境使用需要试用版或正式许可证。
- **支持哪个 Java 版本？** Java 8 或更高。
- **我可以在云服务器上运行吗？** 当然——只需确保在安全组中打开相应端口。
- **我可以添加多少节点？** 没有硬性限制；可根据硬件和网络情况添加任意数量的节点。

## 什么您为每个节点分配一个起始 TCP 端口（后续节点递增）。此简单步骤可消除恼人的 “端口已被占用” 错误，并为干净的水平可扩展搜索集选项 Intelli Java** 库（版本 25.4 或更高），通过 Maven 或手动下载安装。
- 基本的网络知识（TCP 端口、localhost 与远程主机）。

## 设置 GroupDocs.Search for Java

### 安装说明

**Maven 设置:**

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

**直接下载:**

另外，您可以从 [GroupDocs.Search for Java 发布](https://releases.groupdocs.com/search/java/) 下载最新版本。

### 获取许可证

- **免费试用** – 立即开始测试。
- **临时许可证** – 在 [临时许可证](https://purchase.groupdocs.com/temporary-license) 获取延长试用。
- **正式购买** – 生产部署所必需。

### 基本初始化和设置

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## 实施指南

### 如何配置基础端口 GroupDocs

#### 设置基础路径

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **原因**：一致的目录结构使每个节点能够明确定位其索引、分片或提取器文件。

#### 配置基础端口

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **原因**：从较高的端，可降低与常用服务冲突的概率。每增加一个节点，端口递增。

#### 定义主机地址

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **原因**：开发时使用 `localhost` 最为理想；生产环境请替换为服务器的 IP 或 DNS 名称。

#### 创建网络配置

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **原因**：这些选项在速度和存储效率之间取得平衡，为您提供轻量且强大的搜索索引。

#### 添加节点

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **原因**：在节点之间分配职责（索引 vs. 搜索，分片 vs. 提取）可提升并行性和容错能力。

#### 完成配置

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### 常见问题与解决方案
- **端口冲突** – 对每个新节点始终递增 `basePort`。可使用 `netstat` 或操作系统的端口监视器进行验证。
- **目录缺失** – 确保所有引用的文件夹（`Indexer0`、`Searcher0` 等）存在，并且 Java 进程拥有读写权限。
- **网络可达性** – 在迁移到多机器部署时，将 `127.0.0.1` 替换为实际主机 IP，并在防火墙中打开所选端口。

## 实际应用

| 场景                     | 配置基础端口 GroupDocs 的好处                         |
|--------------------------|------------------------------------------------------|
| 企业文档管理             | 跨部门无停机的无缝扩展                                 |
| 大型 CMS 平台            | 由于索引分布式，内容检索更快                           |
| 法律案件管理             | PDF 并行提取降低搜索延迟                               |

## 性能考虑
- **监控 CPU/内存** – 使用 Java 的 JMX 或分析工具监视线程使用情况。
 `Compression.High` 可节省磁盘空间，但可能增加 CPU 开销；请同时测试 `High` 和 `Normal`。
- **定期更新** – 新的 GroupDocs.Search 版本通常包含性能补丁。

## 结论

您已经学习了如何 **配置基础端口 GroupDocs** 并使用 GroupDocs.Search for Java 搭建多节点搜索网络。可尝试引设置，并将网络集成到现索引时禁用停用词的目的是什么？**  
答：禁用停用词可以通过保留在特定领域可能关键的常用词来提升搜索准确性。

**选端口，并将 `127.0.0.1` 替换为相应的公网或私网 IP。

**问：NormalIndex 与其他索引类型有什么区别？**  
答：`NormalIndex` 在速度和内存使用之间提供了平衡的折衷，而专用索引（如 `FastIndex`）针对特定的性能场景。

**问：我可以添加的节点数量是否有限制？**  
答：技术上没有限制；上限取决于您的硬件资源和网络带宽。

---

**最后更新：** 2026-01-24  
**测试环境：** GroupDocs.Search Java 25.4  
**作者：** GroupDocs
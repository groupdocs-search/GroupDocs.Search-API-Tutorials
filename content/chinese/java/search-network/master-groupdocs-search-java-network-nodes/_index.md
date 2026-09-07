---
date: '2026-07-02'
description: 了解如何为 GroupDocs.Search 获取临时许可证，向索引添加目录，并在管理 Java 搜索网络节点时添加自定义文档属性。
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: 获取临时许可证 GroupDocs – 主搜索节点 (Java)
type: docs
url: /zh/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# 获取临时许可证 GroupDocs – 主搜索节点 (Java)

在本综合指南中，您将**获取 GroupDocs.Search 的临时许可证**，配置多节点搜索网络，并学习如何使用 Java **将目录添加到索引**以及**添加自定义文档属性**。无论您是构建企业文档管理系统还是可搜索的产品目录，掌握这些步骤都能让您在不受限制的情况下评估平台，并快速扩展搜索能力。

## 快速答案
- **开始使用 GroupDocs.Search 的第一步是什么？** 从 GroupDocs 门户获取临时许可证。  
- **哪个 Maven 仓库托管该库？** `https://releases.groupdocs.com/search/java/`。  
- **如何将目录添加到索引？** 在主节点上调用 `addDirectoriesToIndex` 辅助方法。  
- **我可以添加自定义文档属性吗？** 可以——使用文档键和属性名称调用 `addAttribute`。  
- **如何干净地关闭节点？** 调用 `closeNodes` 释放资源。

## 什么是临时许可证以及为什么需要它？
临时许可证让您在没有任何评估限制的情况下评估 GroupDocs.Search。它非常适合在正式购买之前用于开发、测试或概念验证项目。该许可证在有限的时间内提供全部功能访问，使您能够对性能进行基准测试、测试集成点，并确保解决方案满足您的需求，而无需财务投入。

## 前置条件

在开始之前，请确保已具备以下前置条件：

### 必需的库和依赖项
要在 Java 中使用 GroupDocs.Search，请包含必要的 Maven 依赖：
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
您也可以直接从 [GroupDocs.Search for Java 发行版](https://releases.groupdocs.com/search/java/) 下载最新版本。

### 环境设置
- 确保已安装兼容的 JDK（Java 8 或更高版本）。  
- 将您的 IDE 设置为支持 Maven 项目。

### 知识前置条件
对 Java 编程的基本了解以及对 Maven 项目管理的熟悉将大有裨益。如果您对这些概念不熟悉，建议查阅入门资源以开始学习。

## 如何获取临时许可证
通过访问 GroupDocs 门户、填写简短的请求表单并将收到的 `.lic` 文件放入项目的 `resources` 文件夹，即可获取临时许可证。随后使用几行代码初始化许可证（见下方代码片段）。请求表单请使用官方页面：[GroupDocs 临时许可证](https://purchase.groupdocs.com/temporary-license/)。

## 设置 GroupDocs.Search for Java

### 安装信息
要在项目中开始使用 GroupDocs.Search for Java，请遵循上述 Maven 步骤，或直接从官方发行页面下载最新版本。

#### 许可证获取步骤
1. **免费试用** – 在无需任何承诺的情况下探索功能。  
2. **临时许可证** – 获取用于测试的短期密钥（参见上面的章节）。  
3. **购买** – 在生产环境中使用时，从 **[GroupDocs 购买页面](https://purchase.groupdocs.com/)** 购买完整许可证。

### 基本初始化和设置
按如下方式初始化项目以使用 GroupDocs.Search：
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
此初始化步骤对于确保所有组件在搜索网络中无缝运行至关重要。

## 实施指南
现在，让我们将过程拆分为可管理的章节，每个章节聚焦于部署和管理搜索网络节点的特定功能。

### 功能 1：配置设置
**概述：** 为搜索网络设置配置是部署节点的第一步。此设置涉及指定对节点部署至关重要的路径和端口。

#### 实施步骤：
##### 步骤 1：定义基础路径和端口
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### 步骤 2：配置搜索网络
`configureSearchNetwork` 函数准备部署节点所需的配置对象。  
`Configuration` 是一个类，保存所有设置，如索引文件夹、网络端口和节点角色。  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **参数：** 基础路径和端口用于定位资源并建立通信通道。  
- **返回值：** 一个针对您部署需求定制的已配置 `Configuration` 对象。

### 功能 2：搜索网络部署
**概述：** 部署节点对于在不同环境或数据分段中扩展搜索能力至关重要。

#### 实施步骤：
##### 步骤 1：部署节点
`deploySearchNetwork` 函数初始化并返回搜索网络节点数组。  
`SearchNetworkNodes` 表示参与分布式搜索集群的每个节点实例。  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **参数：** 基础路径、端口和配置用于确定部署环境。  
- **返回值：** 包含已初始化 `SearchNetworkNodes` 的数组。

### 功能 3：订阅网络事件
**概述：** 监控搜索网络的活动对于保持最佳性能和可靠性至关重要。

#### 实施步骤：
##### 步骤 1：订阅主节点事件
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **目的：** 此步骤确保您收到搜索网络中重要事件或变更的通知。

### 功能 4：文档索引
**概述：** 添加包含待索引文档的目录可实现网络内高效的数据检索。

#### 如何将目录添加到索引
`addDirectoriesToIndex` 是一个帮助方法，用于在主节点上注册用于索引的文件夹路径。  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **目的：** 促进对指定目录中所有文档的快速访问和可搜索性。

### 功能 5：为文档添加属性
**概述：** 自定义属性增强文档元数据，使搜索更灵活、信息更丰富。

#### 如何添加自定义文档属性
`addAttribute` 向索引中的指定文档添加自定义元数据属性。  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **参数：** 指定要添加的节点、文档键和属性。  
- **目的：** 通过为文档添加额外的元数据来扩展搜索功能。

### 功能 6：检索已索引文档
**概述：** 高效检索并列出已索引文档，以确保数据的准确性和完整性。

#### 实施步骤：
##### 步骤 1：获取已索引文档
```java
getIndexedDocuments(nodes[0]);
```  
- **目的：** 验证搜索网络中所有必要文档已成功索引。

### 功能 7：关闭网络节点
**概述：** 正确关闭节点对于资源管理和防止内存泄漏至关重要。

#### 实施步骤：
##### 步骤 1：关闭所有节点
`closeNodes` 关闭所有活动搜索节点并释放已分配的资源。  
```java
closeNodes(nodes);
```  
- **目的：** 释放每个节点占用的资源，确保干净的关闭过程。

## 为什么使用 GroupDocs.Search 的临时许可证？
临时许可证提供 **30 天的完整功能访问**，并支持最多 **50,000 个已索引文档**，且不受性能限制。这使您能够在购买正式许可证之前，在真实数据上对索引速度、查询延迟和可扩展性进行基准测试。它还会去除评估水印，真实呈现最终产品的能力。

## 常见使用场景
1. **企业文档管理** – 索引跨部门的数百万内部文件，实现即时全文搜索。  
2. **电子商务平台** – 构建跨多个仓库和第三方数据源的可搜索产品目录。  
3. **律师事务所** – 使用自定义元数据组织案件文件、合同和证据，以实现快速检索。

与其他系统的集成可能包括 CRM 平台、内容管理系统（CMS）和数据分析工具，利用 GroupDocs.Search for Java 提供的强大索引和搜索功能。

## 性能考虑因素
在使用 GroupDocs.Search for Java 时优化性能：
- **优化配置** – 根据具体部署环境定制配置设置。  
- **监控资源使用** – 定期检查 CPU、内存和 I/O，以防止瓶颈或内存泄漏。  
- **遵循最佳实践** – 遵守 Java 内存管理指南，确保系统资源的高效利用。

## 常见问题

**Q: 临时许可证的有效期是多久？**  
A: 临时许可证通常有效期为 30 天，足以让您充分评估产品。

**Q: 我可以在不重新安装的情况下从临时许可证切换到完整许可证吗？**  
A: 可以——用完整许可证文件替换临时许可证文件并重新启动应用程序。

**Q: 应用新许可证后需要重新索引文档吗？**  
A: 不需要，索引保持完整；许可证仅控制使用权限。

**Q: 如果忘记关闭节点会怎样？**  
A: 未释放的资源可能导致内存泄漏；在关闭时始终调用 `closeNodes`。

**Q: 是否可以为每个文档添加多个自定义属性？**  
A: 当然可以——使用不同的属性名多次调用 `addAttribute`。

---

**最后更新：** 2026-07-02  
**测试使用：** GroupDocs.Search for Java 25.4  
**作者：** GroupDocs

## 相关教程

- [在 .NET 中使用 GroupDocs 部署搜索网络节点，实现高效文档索引和检索](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [如何在 .NET 中使用 GroupDocs.Search 实现搜索网络，以用于文档管理系统](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [在 .NET 中配置 Aspose.Search 网络并使用 GroupDocs.Redaction 添加文档属性：完整指南](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
---
date: '2026-01-21'
description: 了解如何添加 GroupDocs Maven 依赖、配置并同步 Java 搜索网络，以及使用 GroupDocs.Search 将目录添加到索引中。
keywords:
- Java Search Network Configuration
- GroupDocs.Search for Java
- Document Indexing and Retrieval
title: GroupDocs Maven 依赖 – Java 搜索网络同步
type: docs
url: /zh/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# GroupDocs Maven 依赖：配置和同步 Java 搜索网络

在本综合指南中，您将了解 **如何将 GroupDocs Maven 依赖** 添加到项目中，然后使用 GroupDocs.Search 配置强大的 Java 搜索网络。无论您处理的是法律简报、财务报告还是学术论文，以下步骤都将帮助您高效地建立索引、搜索并保持分片同步。

## Introduction

管理和搜索海量文档集合是许多组织的日常挑战。通过集成 **GroupDocs Maven 依赖**，您可以获得一个强大的索引引擎，该引擎能够跨多个节点扩展。本教程将引导您完成依赖的设置、网络节点的部署、向索引添加目录以及同步分片以实现最佳性能的全过程。

### Quick Answers
- **What is the GroupDocs Maven dependency?** 一个 Maven 构件，将 GroupDocs.Search 库引入您的 Java 项目。  
- **Why use a search network?** 它将索引和查询负载分布到多个节点，提高速度和可靠性。  
- **How do I add directories to index?** 在主节点上使用 `IndexingDocuments.addDirectories`。  
- **How to sync shards?** 在每个节点的 `Indexer` 上调用 `SynchronizeOptions`。  
- **Do I need a license?** 是的，生产环境需要试用或商业许可证。

## What is the GroupDocs Maven Dependency?

GroupDocs Maven 依赖 (`com.groupdocs:groupdocs-search`) 包含构建可搜索索引、管理网络节点以及执行快速查询所需的所有类。将其添加到 `pom.xml` 可确保 Maven 拉取正确的二进制文件及其传递依赖。

## How to Add the GroupDocs Maven Dependency

### Maven Configuration

将仓库和依赖添加到您的 `pom.xml`：

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

> **Pro tip:** 通过检查官方发布页面，保持版本号为最新。

您也可以直接从官方网站下载 JAR：[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

## Prerequisites

- 已安装 **JDK**（11 或更高）。
- IDE，例如 IntelliJ IDEA 或 Eclipse。
- 基本的 Java 知识、Maven 使用经验以及对网络节点概念的了解。
- 有效的 GroupDocs.Search 许可证（免费试用或商业版）。

## Basic Initialization and Setup

首先创建一个索引目录：

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

此简单步骤为后续的网络配置做好准备。

## Implementation Guide

### Feature 1: Configuration of Search Network

#### Overview

配置搜索网络时，需要设置节点用于通信的文件路径和端口。

##### Set Up Paths and Ports
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
`configuration` 对象现在包含了搜索网络所需的全部设置。

### Feature 2: Deploying Search Network Nodes

#### Overview

部署节点以在网络中分配工作负载。主节点负责管理操作和事件。

##### Deployment Code
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Feature 3: Subscribing to Search Network Node Events

#### Overview

监听事件可动态处理网络中的变化或更新。

##### Subscription Implementation
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Feature 4: Adding Directories to Index

#### Overview

添加目录是使文档可搜索的核心步骤。

##### Document Addition
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Feature 5: Synchronizing Shards in Search Network Node

#### Overview

同步确保所有分片之间的数据一致性。

##### Synchronization Code
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Feature 6: Closing Search Network Nodes

#### Overview

正确关闭节点可释放资源并防止内存泄漏。

##### Node Closure
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Practical Applications

1. **Legal Document Management** – 快速检索案件文件和判例。  
2. **Financial Record Keeping** – 在几秒钟内访问对账单和审计轨迹。  
3. **Academic Research** – 在成千上万的论文中搜索以找到相关引用。

## Performance Considerations

- **Optimize Queries** – 编写简洁的查询以降低响应时间。  
-优 – 根据数据量和查询负载按比例添加节点。

## Common Issues and Solutions

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 节点连接失败 | 端口冲突 | 将 `basePort` 更改为未使用的值 |
| 索引未更新 | 缺少事件订阅 |(masterNode)` |
| 延迟高 | 分片不足 |可以通过 network引新文件夹时，调用 `IndexingDocuments.addDirectories(masterNode, "path")`。

**Q: How to sync shards when a new node joins the network?**  
A: 在新加入的节点上使用上文展示的 `synchronizeShards` 方法。

**Q: Do I need a license for development?**  
A: 测试阶段使用免费试用许可证即可，生产环境需要商业许可证。

## Conclusion

通过本指南，您现在已经了解如何 **添加 GroupDocs Maven 依赖**、配置多节点搜索网络、索引目录以及保持分片同步。这些步骤为构建高性能文档搜索解决方案奠定了基础，能够随组织需求的增长而扩展。

---

**Last Updated:** 2026-01-21  
**Tested With:** GroupDocs.Search 25.4  
**Author:** GroupDocs
---
date: '2026-01-16'
description: 学习如何使用 GroupDocs，并通过 GroupDocs.Search for Java 检索所有支持的文件格式来获取 Java 文件扩展名。非常适合集成文档处理库的开发者。
keywords:
- GroupDocs.Search for Java
- retrieve supported file formats
- Java document processing
title: 如何使用 GroupDocs 在 Java 中检索受支持的文件格式
type: docs
url: /zh/java/licensing-configuration/retrieve-supported-file-formats-groupdocs-search-java/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 检索受支持的文件格式

如果你想了解 **如何使用 GroupDocs** 来发现你的应用程序可以处理的确切文件类型，你来对地方了。在本教程中，我们将演示如何使用 GroupDocs.Search for Java 获取完整的受支持格式列表，从而能够自信地在 UI 中显示或验证文件扩展名。

## 快速回答
- **该功能做什么？** 返回 GroupDocs.Search 能够索引的所有文件扩展名。  
- **有什么用？** 让你能够动态告知用户支持的上传类型，避免出现不受支持文件的错误。  
- **需要许可证吗？** 免费试用可用于测试；正式生产环境需要完整许可证。  
- **需要哪个 Java 版本？** Java 8 或更高。  
- **需要额外配置吗？** 不需要——只需添加依赖并调用 API 即可。

## 什么是 GroupDocs.Search？
GroupDocs.Search 是一个 Java 库，提供对多种文档格式的快速全文搜索。它抽象了 PDF、Word、电子表格等多种类型的解析复杂性，提供了简洁的 API 用于索引和查询。

## 为什么要检索受支持的文件格式？
了解确切的扩展名列表可以帮助你：
- 构建仅允许受支持文件的动态上传组件。  
- 为最终用户生成准确的文档说明。  
- 减少因尝试索引不受支持格式而导致的运行时错误。

## 前置条件
- **Java Development Kit (JDK) 8+**  
- **Maven** 用于依赖管理  
- **IDE** 如 IntelliJ IDEA 或 Eclipse  

熟悉基本的 Java 与 Maven 概念会让操作更顺畅。

## 为 Java 设置 GroupDocs.Search

### Maven 配置
在 `pom.xml` 中添加 GroupDocs 仓库和依赖：

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
如果你愿意，也可以直接从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下载最新版本。

### 许可证获取步骤
- **免费试用** – 体验核心功能。  
- **临时许可证** – 在不受功能限制的情况下进行测试。  
- **完整许可证** – 解锁生产环境所需的全部功能。

#### 基本初始化与设置
添加依赖后，你可以创建索引并添加文档：

```java
import com.groupdocs.search.*;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an index in the specified folder
        Index index = new Index("path/to/index/folder");
        
        // Add documents to the index from a folder
        index.add("path/to/documents/folder");
    }
}
```

## 如何使用 GroupDocs 获取文件扩展名（Java）

### 检索受支持的文件格式
以下步骤展示了如何获取 GroupDocs.Search 支持的完整文件扩展名列表。

#### 步骤 1 – 导入所需类
```java
import com.groupdocs.search.results.FileType;
```

#### 步骤 2 – 获取受支持类型的集合
```java
Iterable<FileType> supportedFileTypes = FileType.getSupportedFileTypes();
```

#### 步骤 3 – 遍历并打印每种格式
```java
for (FileType fileType : supportedFileTypes) {
    System.out.println(fileType.getExtension() + " - " + fileType.getDescription());
}
```

运行此代码片段会输出类似 `pdf - Portable Document Format` 的行，为 UI 下拉框或验证逻辑提供即用的列表。

### 故障排除提示
- **类未找到** – 确认 Maven 依赖已正确解析。  
- **路径问题** – 确保索引文件夹路径存在且可写。  

## 实际应用场景
1. **文档管理系统** – 动态列出受支持的上传类型。  
2. **基于 Web 的文件上传** – 在客户端使用检索到的列表进行文件类型校验。  
3. **备份解决方案** – 在归档前过滤掉不受支持的文件。

## 性能考虑
- 如果需要频繁访问，可将检索到的列表存入内存；该调用本身开销很小。  
- 保持 GroupDocs.Search 库为最新版本，以获得性能改进。

## 常见问题与解决方案
| 问题 | 原因 | 解决方案 |
|------|------|----------|
| `FileType` 类缺失 | 未添加依赖 | 在添加依赖后重新运行 `mvn clean install` |
| 没有输出 | IDE 中抑制了 `System.out` | 检查控制台配置或在命令行运行 |

## 常见问答

**问：什么是 GroupDocs.Search？**  
答：它是一个 Java 库，能够在多种文档格式上实现全文搜索，无需单独的解析器。

**问：如何更新库的版本？**  
答：修改 `pom.xml` 中的 `<version>` 标签，然后运行 `mvn clean install`。

**问：我可以在非 Java 项目中使用此功能吗？**  
答：文中示例是针对 Java 的，但 GroupDocs 也提供 .NET、Python 等平台的类似功能。

**问：如果缺少需要的文件类型怎么办？**  
答：请联系 GroupDocs 支持，他们会在后续版本中持续添加新格式。

**问：生产环境是否需要商业许可证？**  
答：是的，完整许可证可去除试用限制并授予商业使用权。

## 资源
- [GroupDocs Search 文档](https://docs.groupdocs.com/search/java/)
- [API 参考](https://reference.groupdocs.com/search/java)
- [下载最新版本](https://releases.groupdocs.com/search/java/)
- [GitHub 仓库](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [免费支持论坛](https://forum.groupdocs.com/c/search/10)
- [临时许可证获取](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-01-16  
**测试环境：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs
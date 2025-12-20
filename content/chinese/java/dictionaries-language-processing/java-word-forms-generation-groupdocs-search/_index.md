---
date: '2025-12-20'
description: 学习如何使用 GroupDocs.Search 在 Java 中创建词形提供程序。生成单数和复数形式用于搜索、文本分析等。
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: 使用 GroupDocs.Search API 在 Java 中创建 Word 表单提供程序
type: docs
url: /zh/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# 使用 GroupDocs.Search API 在 Java 中创建词形提供程序

在构建语言感知的应用程序时，将单数词转换为复数——或相反——是一个常见的难题。在本指南中，您将使用 GroupDocs.Search Java API **创建词形提供程序**，为您的搜索引擎或文本分析工具提供自动理解和匹配不同词形变体的能力。

无论您是在开发搜索引擎、内容管理系统，还是任何处理自然语言的 Java 应用程序，掌握词形生成都能使您的结果更准确，提升用户满意度。让我们在开始之前先了解所需的前提条件。

## 快速答案
- **词形提供程序的作用是什么？** 它为给定的单词生成替代形式（单数、复数等），以便搜索能够匹配所有变体。  
- **需要哪个库？** GroupDocs.Search for Java（版本 25.4 或更高）。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要正式许可证。  
- **支持的 Java 版本是什么？** JDK 8 或更高。  
- **需要多少行代码？** 简单提供程序实现大约 30 行代码。

## 什么是 “创建词形提供程序” 功能？

一个 **创建词形提供程序** 组件是实现 `IWordFormsProvider` 接口的自定义类。它接收一个单词并返回一个可能形式的数组——单数、复数或其他语言变体——依据您定义的规则。这使得搜索索引能够将 “cat” 与 “cats” 视为等价，从而在不牺牲精确度的前提下提升召回率。

## 为什么使用 GroupDocs.Search 进行词形生成？

- **内置可扩展性：** 您可以将自定义提供程序直接插入索引管道。  
- **性能优化：** 该库高效处理大型索引，并且您可以缓存结果以提升速度。  
- **跨语言支持：** 虽然本教程聚焦于 Java，但相同概念同样适用于 .NET 和其他平台。

## 前提条件

在实现 **创建词形提供程序** 之前，请确保您已具备以下条件：

- 已安装 **Maven**，并在机器上配置了 JDK 8 或更高版本。  
- 对 Java 开发和 Maven 的 `pom.xml` 配置有基本了解。  
- 可获取 GroupDocs.Search Java 库（版本 25.4 或更高）。

## 为 Java 设置 GroupDocs.Search

### Maven 配置

将仓库和依赖项按以下示例添加到您的 `pom.xml` 文件中：

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

或者，从官方发布页面下载最新的 JAR 包： [GroupDocs.Search for Java 发布](https://releases.groupdocs.com/search/java/).

### 获取许可证的步骤

要在无使用限制的情况下使用 GroupDocs.Search：

1. **免费试用：** 注册试用以探索核心功能。  
2. **临时许可证：** 请求临时密钥以进行更长时间的测试。  
3. **购买：** 获取商业许可证，以在生产环境中无限制使用。

### 基本初始化和设置

以下代码片段演示如何创建索引——这是添加文档和词形逻辑的起点：

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## 实现指南

下面我们将逐步讲解如何 **创建词形提供程序**，以处理简单的单数到复数以及复数到单数的转换。

### 实现 SimpleWordFormsProvider

#### 概述

我们的自定义提供程序将：

- 去除结尾的 “es” 或 “s”，以猜测单数形式。  
- 将结尾的 “y” 改为 “is”，生成复数形式（例如 “city” → “citis”）。  
- 添加 “s” 和 “es” 以生成基本的复数候选词。

#### 步骤 1 – 创建类骨架

首先定义一个实现 `IWordFormsProvider` 的类。保持 import 语句不变：

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### 步骤 2 – 实现 `getWordForms`

添加构建可能形式列表的方法。此代码块包含核心逻辑，您可以随后扩展以覆盖更复杂的规则。

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### 逻辑说明

- **单数化：** 检测常见的复数后缀（`es`、`s`），并将其移除以近似得到词根。  
- **复数化：** 处理以 `y` 结尾的名词，将其替换为 `is`，这是一条适用于许多英语单词的简单规则。  
- **后缀添加：** 添加 `s` 和 `es`，以覆盖可能未被前述检查捕获的常规复数形式。

#### 故障排除提示

- **大小写敏感性：** 该方法使用 `toLowerCase()` 进行比较，确保 “Cats” 与 “cats” 表现一致。  
- **边缘情况：** 长度短于后缀的单词会被忽略，以避免返回空字符串。  
- **性能：** 对于大型词汇表，考虑将结果缓存到 `ConcurrentHashMap` 中。

## 实际应用

实现 **创建词形提供程序** 可以提升多个真实场景的效果：

1. **搜索引擎：** 用户输入 “mouse” 时也应能找到包含 “mice” 的文档。提供程序可以生成此类不规则形式。  
2. **文本分析工具：** 当所有词形变体都被识别时，情感或实体抽取的可靠性会提升。  
3. **内容管理系统：** 自动标签生成可以包含复数同义词，提升 SEO 和内部链接效果。

## 性能考虑

将提供程序嵌入生产系统时，请牢记以下提示：

- **缓存常用词形：** 将结果存入内存，以避免对同一单词重复计算。  
- **监控 JVM 堆内存：** 大型索引可能增加内存压力；相应地调优 `-Xmx` 参数。  
- **使用高效集合：** 对于小集合 `ArrayList` 足够，但对于成千上万的词形，考虑使用 `HashSet` 以快速去重。

**最佳实践**

- 保持库的最新版本，以获得性能补丁。  
- 使用真实查询负载对提供程序进行性能分析，及早发现瓶颈。

## 结论

您已经学习了如何使用 GroupDocs.Search for Java **创建词形提供程序**。这个轻量级组件可以显著提升搜索结果的相关性以及多种应用中的语言分析准确性。

**下一步：**

- 尝试更复杂的语言规则（不规则复数、词干提取）。  
- 将提供程序集成到索引管道中，并衡量召回率的提升。  
- 探索 GroupDocs.Search 的其他功能，如同义词词典和自定义分析器。

**行动号召：** 立即在您的项目中添加 `SimpleWordFormsProvider`，体验它如何提升搜索体验！

## 常见问题解答

**1. 什么是 GroupDocs.Search for Java？**  
它是一个强大的库，提供全文搜索、索引和语言特性——包括插入自定义词形提供程序的能力。

**2. SimpleWordFormsProvider 如何工作？**  
它通过应用简单的基于后缀的规则（移除 “s/es”，将 “y” 转换为 “is”，并添加 “s/es”）来生成替代形式。

**3. 我可以自定义词形生成规则吗？**  
当然可以。修改 `getWordForms` 方法，以加入不规则形式、特定语言规则或与外部词典的集成。

**4. 此功能的常见应用有哪些？**  
搜索引擎、文本分析流水线以及 CMS 平台都受益于对单数/复数变体的识别。

**5. 生产环境需要商业许可证吗？**  
是的——虽然试用版可以让您探索 API，但购买许可证后可解除使用限制并获得支持。

---

**最后更新：** 2025-12-20  
**测试环境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs
---
date: '2026-02-21'
description: 学习如何在 Java 中使用 GroupDocs.Search API 生成单复数形式。创建自定义词形提供程序，以实现精准搜索和文本分析。
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: 使用 GroupDocs.Search 在 Java 中生成单复数形式
type: docs
url: /zh/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

 placeholders to be kept unchanged. So we keep them as is.

We must translate all textual content, keep technical terms in English. Ensure headings same.

We need to translate step-by-step. Let's produce Chinese translation.

We need to keep code blocks placeholders unchanged.

Let's produce final markdown with Chinese translation.

Check each line.

Title: "# Generate Singular Plural Forms in Java with GroupDocs.Search" -> translate: "# 使用 GroupDocs.Search 在 Java 中生成单复数形式"

Similarly other headings.

Make sure to keep bullet points, code placeholders.

Let's write.

# 使用 GroupDocs.Search 在 Java 中生成单复数形式

如果您需要 **在 Java 中生成单复数形式**，自定义词形提供程序是让您的搜索或文本分析引擎理解每种词形变化的关键。在本教程中，我们将手把手教您使用 GroupDocs.Search Java API 构建这样一个提供程序，使您的应用能够自动匹配 “cat”、 “cats”、 “city” 和 “citis”，无需额外工作。

## 快速回答
- **词形提供程序的作用是什么？** 它为给定单词生成替代形式（单数、复数等），从而使搜索能够匹配所有变体。  
- **需要哪个库？** GroupDocs.Search for Java（版本 25.4 或更高）。  
- **需要许可证吗？** 免费试用可用于评估；生产环境需要正式许可证。  
- **支持的 Java 版本？** JDK 8 或更高。  
- **需要多少行代码？** 简单实现大约 30 行。

## “Create Word Forms Provider” 功能是什么？
**Create word forms provider** 组件是实现 `IWordFormsProvider` 接口的自定义类。它接收一个单词并返回可能的形式数组——单数、复数或其他语言学变体——依据您定义的规则。这样搜索索引就可以把 “cat” 与 “cats” 视为等价，提高召回率而不牺牲精确度。

## 为什么使用 GroupDocs.Search 进行词形生成？
- **内置可扩展性：** 可直接将自定义提供程序插入索引管道。  
- **性能优化：** 高效处理大规模索引，并可缓存结果以提升速度。  
- **跨语言支持：** 相关概念同样适用于 .NET 等其他平台。

## 前置条件
在实现 **create word forms provider** 之前，请确保您已具备：

- 已安装 **Maven**，并在机器上配置了 JDK 8 或更高版本。  
- 具备基本的 Java 开发和 Maven `pom.xml` 配置经验。  
- 获得 GroupDocs.Search Java 库（版本 25.4 或以上）的访问权限。  

## 为 Java 配置 GroupDocs.Search

### Maven 配置

在 `pom.xml` 文件中按如下方式添加仓库和依赖：

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

或者，从官方发布页面下载最新的 JAR 包： [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)。

### 获取许可证的步骤

1. **免费试用：** 注册试用以体验核心功能。  
2. **临时许可证：** 申请临时密钥以进行更长时间的测试。  
3. **购买：** 获取商业许可证以在生产环境中无限制使用。

### 基本初始化与设置

下面的代码片段演示了如何创建索引——这是添加文档和词形逻辑的起点：

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

下面我们将逐步说明如何 **create word forms provider**，实现简单的单数‑复数以及复数‑单数转换。

### 实现 SimpleWordFormsProvider

#### 概览
我们的自定义提供程序将：

- 去除结尾的 “es” 或 “s” 以猜测单数形式。  
- 将结尾的 “y” 替换为 “is” 生成复数形式（例如 “city” → “citis”）。  
- 添加 “s” 和 “es” 以生成基本的复数候选。

#### 第 1 步 – 创建类骨架

首先定义一个实现 `IWordFormsProvider` 的类。保持 import 语句不变：

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### 第 2 步 – 实现 `getWordForms`

添加构建可能形式列表的方法。此代码块包含核心逻辑，后续可扩展以覆盖更复杂的规则。

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
- **单数化：** 检测常见的复数后缀（`es`、`s`），并将其移除，以近似得到词根。  
- **复数化：** 处理以 `y` 结尾的名词，将其换成 `is`，这是一条对多数英文单词有效的简易规则。  
- **后缀追加：** 添加 `s` 与 `es`，覆盖可能未被前面检查捕获的常规复数形式。

#### 故障排查提示
- **大小写敏感：** 方法使用 `toLowerCase()` 进行比较，确保 “Cats” 与 “cats” 行为一致。  
- **边界情况：** 对长度小于后缀长度的单词直接忽略，以避免返回空字符串。  
- **性能：** 对于大词表，考虑在 `ConcurrentHashMap` 中缓存结果。

## 实际应用

实现 **create word forms provider** 可提升多个真实场景的效果：

1. **搜索引擎：** 用户输入 “mouse” 时也能找到包含 “mice” 的文档。提供程序可以生成此类不规则形式。  
2. **文本分析工具：** 在进行情感或实体抽取时，识别所有词形变体可提升可靠性。  
3. **内容管理系统：** 自动标签生成时加入复数同义词，可改善 SEO 与内部链接。

## 性能考虑

将提供程序嵌入生产系统时，请注意以下要点：

- **缓存常用词形：** 将结果存入内存，避免重复计算同一单词。  
- **监控 JVM 堆内存：** 大索引可能增加内存压力，需相应调节 `-Xmx` 参数。  
- **使用高效集合：** 小规模集合可使用 `ArrayList`，但若涉及数千种形式，建议使用 `HashSet` 快速去重。

**最佳实践**

- 保持库版本最新，以获得性能补丁。  
- 使用真实查询负载对提供程序进行性能分析，及早发现瓶颈。

## 结论

现在，您已经掌握了如何使用 GroupDocs.Search 通过自定义 `SimpleWordFormsProvider` 在 Java 中 **生成单复数形式**。这一轻量级组件能够显著提升搜索结果的相关性以及语言分析的准确性，适用于众多应用场景。

**后续步骤：**  
- 试验更复杂的语言规则（不规则复数、词干提取）。  
- 将提供程序集成到索引管道并衡量召回率提升。  
- 探索 GroupDocs.Search 的其他功能，如同义词词典和自定义分析器。

**行动号召：** 立即在您的项目中添加 `SimpleWordFormsProvider`，体验搜索体验的提升吧！

## FAQ 区

**1. 什么是 GroupDocs.Search for Java？**  
它是一款功能强大的库，提供全文搜索、索引以及语言学特性——包括插入自定义词形提供程序的能力。

**2. SimpleWordFormsProvider 如何工作？**  
它通过简单的后缀规则（去除 “s/es”、将 “y” 转为 “is”、以及追加 “s/es”）生成替代形式。

**3. 我可以自定义词形生成规则吗？**  
当然。修改 `getWordForms` 方法即可加入不规则形式、特定语言规则或外部词典的集成。

**4. 这个功能有哪些常见应用场景？**  
搜索引擎、文本分析流水线以及 CMS 平台都受益于对单复数变体的识别。

**5. 生产环境需要商业许可证吗？**  
是的——试用版可用于探索 API，正式生产需购买许可证以解除使用限制并获得技术支持。

---

**最后更新：** 2026-02-21  
**测试环境：** GroupDocs.Search 25.4 (Java)  
**作者：** GroupDocs  

---
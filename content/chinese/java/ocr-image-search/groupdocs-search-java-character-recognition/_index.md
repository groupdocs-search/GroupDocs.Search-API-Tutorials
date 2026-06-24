---
date: '2026-03-17'
description: 学习如何使用 GroupDocs.Search for Java 创建索引，配置常规和混合字符，并优化对法律案件编号和 OCR 图像的搜索。
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: 如何在 Java 中使用字符识别创建索引
type: docs
url: /zh/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# 使用 GroupDocs.Search for Java 创建带字符识别的索引

在现代文档密集的应用中，**如何创建索引**以尊重文本细微差别——例如连字符、下划线或特定语言符号——对于快速、准确的检索至关重要。在本教程中，我们将演示如何在 **GroupDocs.Search for Java** 中配置字符识别，涵盖普通字符（字母、数字、下划线）和混合字符（例如连字符）。完成后，您将能够定制索引，以满足 OCR 或图像搜索场景的精确需求，无论是索引法律案件编号、源代码仓库还是多语言 PDF。

## 快速回答
- **“创建自定义搜索索引”是什么意思？** 这意味着配置索引，使特定符号被视为字母或混合字符，而不是被忽略。  
- **使用的是哪个库？** GroupDocs.Search for Java（撰写时为 v25.4）。  
- **我需要许可证吗？** 开发阶段可使用免费试用版；生产环境需要付费许可证。  
- **我可以同时索引 PDF 和图像吗？** 可以——在正确配置后，GroupDocs.Search 支持对图像和 PDF 进行 OCR。  
- **是否必须使用 Maven？** 推荐使用 Maven 管理依赖，但也可以使用 Gradle 或手动 JAR。

## 什么是自定义搜索索引？
自定义搜索索引允许您定义搜索引擎如何解释字符。默认情况下，许多符号会被忽略，这可能导致诸如案件编号 (`2023-AB-456`) 或代码片段 (`my_variable`) 等匹配失败。调整字母表字典即可完全控制引擎将哪些字符视为可搜索文本。

## 为什么为法律案件编号配置普通字符和混合字符？
- **普通字符**（字母、数字、下划线）会被单独标记为词元，能够实现标识符的精确匹配搜索。  
- **混合字符**（连字符、斜杠）会将相关词元保持在一起，防止案件编号、产品代码或文件路径被不必要地拆分。  
- 此配置 **优化搜索索引** 性能，减少词元碎片化，并提升 OCR 生成内容的相关性。

## 前置条件
- **JDK 8** 或更高版本已安装。  
- **Maven** 用于依赖管理。  
- 已获取 **GroupDocs.Search for Java** 库（通过 Maven 或官方网站下载）。

### 必需的库和依赖项
将仓库和依赖项添加到您的 `pom.xml`（如下所示）。XML 块必须保持不变。

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

您也可以从 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 下载最新的 JAR 包。

### 许可证获取
- **免费试用** – 适合早期实验。  
- **临时许可证** – 适用于较长的开发周期。  
- **正式许可证** – 商业部署必需。  

从官方门户获取许可证： [GroupDocs](https://purchase.groupdocs.com/temporary-license/)。

### 基本初始化
下面的代码片段展示了创建空索引所需的最小代码。保持原样；后续我们将在此基础上构建。

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## 设置 GroupDocs.Search for Java

### 通过 Maven 安装
*Prerequisites* 部分的 Maven 配置即为全部所需。添加后运行 `mvn clean install` 拉取二进制文件。

### 环境设置要求
- 确保 **index folder** 和 **document folder** 已在磁盘上存在。  
- 使用绝对路径或在 IDE 中正确配置相对路径解析。

## 实现指南

下面我们将分别演示两大功能：**普通字符** 和 **混合字符**。每个功能遵循相同的步骤——定义路径、创建索引、设置字符字典，最后索引文档。

### 功能 1 – 普通字符

#### 概述
普通字符被视为独立的词元。当您希望数字、字母和下划线能够精确按原样搜索时，这种方式最为理想。

#### 步骤实现

**1️⃣ Set Up Paths**  
定义索引存放位置以及源文档所在目录。

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
实例化索引并清除任何预先存在的字母表配置。

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
构建一个字符数组，包含数字、拉丁字母以及下划线。

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
将源文件夹中的所有文件添加到新配置的索引中。

```java
index.add(documentFolder);
```

### 功能 2 – 混合字符

#### 概述
混合字符（如连字符）通常连接两个词。将其标记为 *混合* 可让引擎在索引时保持周围词元的整体性。

#### 步骤实现

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
这里我们告诉字典将连字符视为混合字符。

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## 实际应用

### 用例 1 – 法律文档管理
法律文件常包含类似 `2023-AB-456` 的案件编号。通过配置下划线和连字符，搜索能够返回完整匹配而不会拆分标识符，从而高效 **搜索法律案件编号**。

### 用例 2 – 源代码仓库
开发者需要搜索包含下划线 (`my_variable`) 和连字符 (`my-function`) 的代码片段。自定义字符识别确保搜索引擎尊重这些符号。

### 用例 3 – 多语言数据集
处理使用额外字母表的语言时，您可以 **扩展 Unicode 字符集** 以包含这些范围，确保跨语言搜索结果的准确性。

### 用例 4 – 索引 PDF 图像
如果索引的是扫描的 PDF 或图像文件，OCR 输出通常包含混合字符。正确配置普通字符和混合字符 **优化搜索索引** 在基于图像内容的场景下的性能。

## 性能考虑

- **资源管理** – 关注堆内存使用；大型索引受益于增量提交。  
- **垃圾回收** – 完成后释放 `Index` 对象，以便 JVM 回收内存。  
- **索引优化** – 定期调用 `index.optimize()`（若可用）以压缩索引并提升查询速度。  

## 结论

您现在已经了解 **如何创建索引**，并能够在 GroupDocs.Search for Java 中区分普通字符和混合字符。这种细粒度的控制使您能够构建面向 OCR、具备高性能的搜索解决方案，满足法律、开发或多语言环境的特定需求。

### 下一步
- 试验为非拉丁字母表添加额外的 Unicode 范围。  
- 将字符配置与 GroupDocs.Search 的其他功能（如词干提取或同义词）结合使用。  
- 将索引集成到 REST API 中，向前端应用提供搜索能力。

## 常见问题

**Q:** *`CharacterType.Letter` 的作用是什么？*  
**A:** 它告诉索引将提供的字符视为普通字母，从而在索引时将其单独标记为词元。

**Q:** *我可以在同一个索引中同时混合普通字符和混合字符吗？*  
**A:** 可以——只需分别调用 `setRange` 为每种类型设置，字典会同时处理这两种配置。

**Q:** *更改字母表后是否需要重新构建索引？*  
**A:** 必须。字符字典的更改会影响词元化，因此必须重新索引文档以应用新规则。

**Q:** *自定义字符的数量有限制吗？*  
**A:** 库支持完整的 Unicode 范围；如果添加极大量的字符可能会影响性能，建议仅定义实际需要的字符。

**Q:** *这会如何影响 OCR 准确性？*  
**A:** 通过使索引的字符集与 OCR 引擎的输出保持一致，可减少漏检并提升整体搜索相关性。

---

**最后更新：** 2026-03-17  
**已测试版本：** GroupDocs.Search 25.4 for Java  
**作者：** GroupDocs  

---
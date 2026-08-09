---
date: '2026-07-21'
description: Hướng dẫn tạo Truy Vấn Boolean Java trình bày cách thực hiện các tìm
  kiếm boolean AND, OR, NOT bằng GroupDocs.Search for Java, thêm tài liệu vào một
  chỉ mục và tăng cường việc truy xuất tài liệu.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: Hướng dẫn tạo Truy Vấn Boolean Java giải thích chi tiết cách xây dựng
  các truy vấn AND, OR, NOT với GroupDocs.Search for Java, thêm tài liệu vào một chỉ
  mục và cải thiện hiệu suất truy xuất.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Tạo Truy Vấn Boolean Java – Thành Thạo Tìm Kiếm Boolean với GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Tạo Truy Vấn Boolean Java: Thành Thạo Tìm Kiếm Boolean với GroupDocs.Search
  for Java'
type: docs
url: /vi/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Tạo Truy Vấn Boolean Java: Thành Thạo Tìm Kiếm Boolean với GroupDocs.Search cho Java

Tìm kiếm trong các bộ sưu tập tài liệu khổng lồ có thể giống như việc tìm kim trong đống cỏ khô. **Create Boolean Query Java** cho phép bạn chỉ định cho công cụ chính xác những gì bạn cần — các tài liệu chứa *cả* hai từ, *bất kỳ* từ nào, hoặc *loại bỏ* các từ không mong muốn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách thiết lập **GroupDocs.Search for Java**, thêm tài liệu vào chỉ mục, và tạo các truy vấn boolean mạnh mẽ giúp tăng hiệu suất **document retrieval java** của bạn. Khi hoàn thành, bạn sẽ có thể viết mã sạch, dễ bảo trì để tạo truy vấn boolean trong Java chỉ với vài dòng.

## Câu trả lời nhanh
- **What is a boolean AND query?** Trả về chỉ các tài liệu chứa *all* các thuật ngữ đã chỉ định.  
- **How does OR differ from AND?** OR khớp các tài liệu có *any* trong các thuật ngữ, mở rộng tập kết quả.  
- **When should I use NOT?** Sử dụng NOT để lọc ra các tài liệu chứa các từ không mong muốn.  
- **Do I need a license?** Bản dùng thử miễn phí đủ cho việc thử nghiệm; cần giấy phép thương mại cho môi trường sản xuất.  
- **Which Java version is required?** Hỗ trợ Java 8+; khuyến nghị JDK 11+.

## Cái gì là **create boolean query java**?
`create boolean query java` đề cập đến việc xây dựng một truy vấn tìm kiếm trong Java kết hợp các toán tử logic như AND, OR và NOT bằng API của GroupDocs.Search. Bằng cách ghép các toán tử này, bạn có thể kiểm soát chính xác các tài liệu khớp, cho phép lọc nâng cao, tinh chỉnh độ liên quan và các kịch bản tìm kiếm phức tạp.

## Tại sao nên sử dụng GroupDocs.Search cho Java?
- **High performance** trên các tập tài liệu lớn – có thể lập chỉ mục và tìm kiếm 500 GB văn bản trong chưa tới một phút trên máy chủ tiêu chuẩn.  
- **Rich API** hỗ trợ cả truy vấn dựa trên văn bản và dựa trên đối tượng, cho phép bạn chọn phong cách phù hợp với kiến trúc của mình.  
- **Built‑in language support** cho stemming, stop‑words và fuzzy matching trên hơn 30 ngôn ngữ.  
- **Easy integration** với Maven hoặc tải JAR trực tiếp, chỉ cần vài dòng mã để bắt đầu.

## Yêu cầu
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **GroupDocs.Search for Java** (v25.4 hoặc mới hơn) – xem liên kết tải xuống bên dưới.  
- JDK 8+ đã được cài đặt và cấu hình trong IDE (IntelliJ IDEA, Eclipse, v.v.).  
- Kiến thức cơ bản về Java và Maven để quản lý phụ thuộc.  

## Cài đặt GroupDocs.Search cho Java

### Cài đặt Maven
Thêm repository và dependency vào file `pom.xml` của bạn:

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

### Tải trực tiếp
Ngoài ra, tải JAR mới nhất từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Bắt đầu với giấy phép dùng thử miễn phí để khám phá mọi tính năng. Đối với môi trường sản xuất, mua giấy phép thương mại để mở khóa đầy đủ chức năng.

### Khởi tạo và Cài đặt Cơ bản
Tạo thư mục chỉ mục và khởi tạo đối tượng `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Làm thế nào để tạo boolean query java?
Lớp `Index` đại diện cho một tập hợp tài liệu có thể tìm kiếm được lưu trên đĩa. `BooleanQuery` kết hợp nhiều sub‑query với các toán tử logic. `createAndQuery`, `createOrQuery` và `createNotQuery` tạo các sub‑query AND, OR và NOT tương ứng. Tải hoặc tạo một thể hiện `Index`, thêm tài liệu, sau đó xây dựng đối tượng `BooleanQuery` bằng `createAndQuery`, `createOrQuery` hoặc `createNotQuery`. Gọi `index.search(query)` để lấy các tài liệu khớp. Mẫu này hoạt động cho cả kịch bản đơn giản và phức tạp, chỉ cần ba bước logic: khởi tạo chỉ mục, thêm tài liệu và thực thi truy vấn.

## Tìm Kiếm Boolean AND

### Tổng quan
Truy vấn AND thu hẹp kết quả, cải thiện độ liên quan khi bạn cần các tài liệu đáp ứng nhiều tiêu chí đồng thời.

### Các bước thực hiện

1. **Initialize Index** – this also demonstrates **add documents to index** for the AND scenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – using the plain string syntax.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – useful when building queries programmatically (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Tìm Kiếm Boolean OR

### Tổng quan
Truy vấn OR lý tưởng cho các tìm kiếm khám phá, khi bạn muốn nắm bắt các tài liệu chứa ít nhất một trong nhiều từ khóa (**search with or java**).

### Các bước thực hiện

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Tìm Kiếm Boolean NOT

### Tổng quan
Truy vấn NOT giúp bạn loại bỏ các tài liệu không liên quan, chẳng hạn lọc ra tên thương hiệu của đối thủ (**boolean search examples java**).

### Các bước thực hiện

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Truy Vấn Boolean Phức Tạp

### Tổng quan
Các truy vấn phức tạp cho phép mô hình hoá các kịch bản tìm kiếm thực tế, ví dụ “tìm các bài báo thể thao có xu hướng tích cực nhưng loại trừ bất kỳ đề cập nào đến các vận động viên cụ thể”.

### Các bước thực hiện

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Ứng dụng thực tế của các truy vấn **java boolean and or**
- **Document Management Systems** – locate contracts that contain both “confidential” **AND** “renewal”.  
- **Legal Research** – filter case law with **AND**/ **OR** while excluding outdated statutes using **NOT**.  
- **Customer Support** – retrieve tickets that mention “login” **AND** “error” but not “resolved”.  
- **Content Curation** – gather blog posts about “cloud” **OR** “serverless” for a newsletter.

## Những Cạm Bẫy Thường Gặp & Khắc Phục Sự Cố

- **Missing Index Refresh** – after adding new documents, call `index.update()` to ensure they are searchable.  
- **Incorrect Operator Spacing** – GroupDocs.Search expects spaces around operators (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – queries are case‑insensitive by default, but custom analyzers may affect this.  
- **Large Result Sets** – use pagination (`search(query, 0, 100)`) to avoid memory overload.  

## Câu Hỏi Thường Gặp

**Q: Can I combine more than two terms in an AND query?**  
A: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`, or simply write `"term1 AND term2 AND term3"` in the text query.

**Q: Does GroupDocs.Search support wildcard or fuzzy searches?**  
A: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching (e.g., `comfort~`).

**Q: How do I limit the search to specific file types?**  
`FileTypeQuery` limits search results to particular file formats such as PDF or DOCX.  
A: Use the `FileTypeQuery` class to restrict results to PDFs, DOCX, etc., and combine it with your boolean query.

**Q: What is the best way to monitor indexing performance?**  
A: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`) and review the timing metrics after each `add` operation.

**Q: Is there a way to boost the relevance of certain terms?**  
`BoostQuery` boosts the relevance score of specified terms in a search query.  
A: Yes. Wrap important words with `BoostQuery` to increase their weight in the scoring algorithm.

---

**Cập nhật lần cuối:** 2026-07-21  
**Kiểm tra với:** GroupDocs.Search 25.4 (Java)  
**Tác giả:** GroupDocs

## Hướng Dẫn Liên Quan

- [Boolean Operators Java – Create Search Index & Faceted Search](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java&#58; Efficient Document Search and Index Management](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Mastering GroupDocs.Search Java – Create and Manage a Search Index](/search/java/indexing/groupdocs-search-java-create-index-guide/)
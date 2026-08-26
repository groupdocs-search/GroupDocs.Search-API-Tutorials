---
date: '2026-08-26'
description: Tìm hiểu cách boolean operators Java cho phép bạn xây dựng một search
  index nhanh, thực hiện content search Java, và chạy các faceted query với GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Tìm hiểu cách boolean operators Java cho phép bạn xây dựng một search
  index nhanh, thực hiện content search Java, và thực thi faceted queries với GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – xây dựng search index và faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – tạo search index & faceted search
type: docs
url: /vi/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Toán tử Boolean Java – tạo chỉ mục tìm kiếm & tìm kiếm phân lớp

Việc triển khai một **search experience** mạnh mẽ trong Java có thể cảm thấy áp lực, đặc biệt khi bạn cần **create a search index Java** hỗ trợ **boolean operators Java** cho các truy vấn phân lớp và phức tạp. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách thiết lập **GroupDocs.Search for Java**, xây dựng một chỉ mục, thêm tài liệu, và tạo cả các tìm kiếm phân lớp đơn giản và các truy vấn đa tiêu chí tinh vi sử dụng logic Boolean. Khi hoàn thành, bạn sẽ hiểu cách tận dụng các thao tác **content search Java**, **filename search Java**, và thậm chí **update index Java** để giữ dữ liệu luôn mới.

## Câu trả lời nhanh
- **What is a faceted search?** Một cách để lọc kết quả theo các danh mục đã định trước như loại tệp hoặc ngày.  
- **How do I create a search index Java?** Khởi tạo một đối tượng `Index` trỏ tới một thư mục và thêm tài liệu.  
- **Can I combine multiple criteria with boolean operators?** Có—sử dụng các truy vấn dựa trên đối tượng hoặc các toán tử Boolean trong truy vấn văn bản.  
- **Do I need a license?** Một bản dùng thử miễn phí hoạt động cho việc phát triển; giấy phép thương mại loại bỏ các giới hạn.  
- **Which IDE works best?** Bất kỳ IDE Java nào (IntelliJ IDEA, Eclipse, NetBeans) đều hoạt động tốt.

## “create search index java” là gì?

Tạo một search index Java có nghĩa là xây dựng một cấu trúc dựa trên đĩa lưu trữ văn bản tài liệu và siêu dữ liệu, cho phép truy xuất ngay lập tức các tài liệu phù hợp thông qua các truy vấn. Chỉ mục ánh xạ các thuật ngữ tới định danh tài liệu, hỗ trợ tra cứu nhanh, và có thể được cập nhật một cách tăng dần khi các tệp thay đổi, cung cấp nền tảng cho các tính năng tìm kiếm mạnh mẽ.

## Tại sao nên sử dụng GroupDocs.Search cho các truy vấn phân lớp và phức tạp?

GroupDocs.Search for Java cung cấp tính năng faceting tích hợp, hỗ trợ truy vấn Boolean, và chỉ mục hiệu suất cao có thể xử lý tới 10 triệu tài liệu trong khi giữ độ trễ truy vấn dưới 200 ms trên phần cứng máy chủ tiêu chuẩn. Nó cung cấp các bộ lọc trường ngay từ đầu, một ngôn ngữ truy vấn phong phú, và khả năng tương thích thuần Java, làm cho nó trở thành lựa chọn lý tưởng cho các kịch bản tìm kiếm quy mô doanh nghiệp.

## Yêu cầu trước

- **JDK 8 hoặc mới hơn** đã được cài đặt và cấu hình trong IDE của bạn.  
- **Maven** (hoặc Gradle) để quản lý phụ thuộc.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Kiến thức cơ bản về các khái niệm OOP trong Java và cấu trúc dự án Maven.

## Cài đặt GroupDocs.Search cho Java

### Cấu hình Maven
Thêm kho lưu trữ và phụ thuộc vào tệp `pom.xml` của bạn:

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

### Tải xuống trực tiếp
Hoặc, tải JAR mới nhất từ trang phát hành chính thức:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Mua giấy phép
Để mở khóa đầy đủ chức năng:

1. **Free trial** – hoàn hảo cho việc phát triển và thử nghiệm.  
2. **Temporary evaluation license** – mở rộng giới hạn dùng thử.  
3. **Commercial license** – loại bỏ mọi hạn chế cho việc sử dụng trong môi trường sản xuất.

### Khởi tạo và cấu hình cơ bản
Lớp `Index` là thành phần cốt lõi đại diện cho một chỉ mục có thể tìm kiếm được lưu trên đĩa. Đoạn mã sau cho thấy cách **create a search index Java** bằng cách khởi tạo lớp `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Khi chỉ mục đã sẵn sàng, chúng ta có thể chuyển sang các truy vấn phân lớp và phức tạp trong thực tế.

## Cách sử dụng boolean operators java – Tìm kiếm phân lớp đơn giản

Tải chỉ mục của bạn, thêm tài liệu, và thực hiện một truy vấn trường; mẫu hai bước cho phép bạn lấy số lượng facet và kết quả đã lọc trong một lần gọi. Cách tiếp cận này cung cấp cho người dùng một cách trực quan để thu hẹp kết quả theo các danh mục như loại tệp, tác giả, hoặc siêu dữ liệu tùy chỉnh.

### Bước 1: Tạo chỉ mục
Đầu tiên, trỏ `Index` tới một thư mục nơi các tệp chỉ mục sẽ được lưu.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Bước 2: Thêm tài liệu vào chỉ mục
Cho GroupDocs.Search biết nơi các tài liệu nguồn của bạn nằm. Tất cả các loại tệp được hỗ trợ (PDF, DOCX, TXT, v.v.) sẽ được lập chỉ mục tự động.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Bước 3: Thực hiện tìm kiếm trong trường content bằng truy vấn văn bản
Một truy vấn văn bản nhanh lọc theo trường `content`. Cú pháp `content: Pellentesque` giới hạn kết quả chỉ các tài liệu chứa từ *Pellentesque* trong nội dung chính.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Bước 4: Thực hiện tìm kiếm bằng truy vấn đối tượng
Các truy vấn dựa trên đối tượng cung cấp cho bạn kiểm soát chi tiết. Ở đây chúng tôi xây dựng một truy vấn từ, bao bọc nó trong một truy vấn trường, và thực thi.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Cách sử dụng boolean operators java – Tìm kiếm truy vấn phức tạp

Để thực hiện một truy vấn phức tạp, kết hợp nhiều điều kiện trường với các toán tử AND/OR/NOT, và tùy chọn bao gồm các tìm kiếm cụm từ. Bạn có thể chỉ định mỗi điều kiện bằng các truy vấn trường, lồng chúng với các toán tử Boolean, và kiểm soát độ liên quan bằng việc tăng trọng số, cho phép bạn chỉ lấy các tài liệu có độ liên quan cao nhất đáp ứng tất cả các tiêu chí yêu cầu.

### Bước 1: Tạo chỉ mục cho truy vấn phức tạp
Tái sử dụng cùng cấu trúc thư mục; bạn có thể chia sẻ chỉ mục cho cả hai kịch bản đơn giản và phức tạp.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Bước 2: Thực hiện tìm kiếm bằng truy vấn văn bản
Truy vấn sau tìm các tệp có tên *lorem* **và** *ipsum* **hoặc** nội dung chứa một trong hai cụm từ chính xác.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Bước 3: Thực hiện tìm kiếm bằng truy vấn đối tượng
Cấu trúc dựa trên đối tượng phản ánh truy vấn văn bản nhưng cung cấp tính an toàn kiểu và hỗ trợ IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Ứng dụng thực tế của tìm kiếm phân lớp & phức tạp

| Kịch bản | Faceting giúp gì | Truy vấn mẫu |
|----------|-------------------|---------------|
| **Danh mục thương mại điện tử** | Lọc theo danh mục, giá, thương hiệu | `category: Electronics AND price:[100 TO 500]` |
| **Kho tài liệu pháp lý** | Thu hẹp theo số vụ, quyền tài phán | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Lưu trữ nghiên cứu** | Kết hợp tác giả, năm xuất bản, từ khóa | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Mạng nội bộ doanh nghiệp** | Tìm kiếm theo loại tệp và phòng ban | `filetype: pdf AND department: HR` |

These examples illustrate why mastering **boolean operators java** and **filename search java** techniques is a game‑changer for any data‑intensive application.

## Những lỗi thường gặp & khắc phục

Đối tượng `SearchResult` chứa các tài liệu khớp với truy vấn và cung cấp quyền truy cập vào điểm liên quan và các đoạn được đánh dấu.  
Lớp `CommonFieldNames` định nghĩa các tên trường chuẩn như `Content` và `FileName` được sử dụng trong toàn bộ API.

- **Empty results** – Kiểm tra xem các tài liệu đã được thêm thành công chưa (`index.getDocumentCount()` có thể giúp).  
- **Stale index** – Sau khi thêm hoặc xóa tệp, gọi `index.update()` để **update index java** và giữ chỉ mục đồng bộ.  
- **Incorrect field names** – Sử dụng hằng số `CommonFieldNames` (`Content`, `FileName`, v.v.) để tránh lỗi chính tả.  
- **Performance bottlenecks** – Đối với bộ sưu tập lớn, cân nhắc bật `index.setCacheSize()` hoặc sử dụng SSD riêng cho thư mục chỉ mục.  
- **Missing highlights** – Để **highlight search results java**, lấy các đoạn khớp qua `SearchResult.getFragments()` (không được hiển thị ở đây nhưng có trong API).  

## Câu hỏi thường gặp

**Q: Có thể sử dụng GroupDocs.Search với Spring Boot không?**  
A: Chắc chắn. Thêm phụ thuộc Maven, cấu hình chỉ mục như một Spring bean, và tiêm nó ở bất kỳ nơi nào bạn cần khả năng tìm kiếm.

**Q: Thư viện có hỗ trợ các trường siêu dữ liệu tùy chỉnh không?**  
A: Có – bạn có thể thêm các trường do người dùng định nghĩa trong quá trình lập chỉ mục và sau đó thực hiện faceting trên chúng.

**Q: Chỉ mục có thể lớn đến mức nào?**  
A: Chỉ mục dựa trên đĩa có thể xử lý tới 10 triệu tài liệu; chỉ cần đảm bảo đủ dung lượng lưu trữ và giám sát cài đặt bộ nhớ đệm.

**Q: Có cách nào để xếp hạng kết quả theo mức độ liên quan không?**  
A: GroupDocs.Search tự động chấm điểm các kết quả khớp; bạn có thể lấy điểm qua `SearchResult.getDocument(i).getScore()`.

**Q: Điều gì xảy ra nếu tôi lập chỉ mục các PDF được mã hóa?**  
A: Cung cấp mật khẩu khi thêm tài liệu: `index.add(filePath, password)`.

## Kết luận

Bây giờ bạn nên cảm thấy tự tin **creating a search index Java** với GroupDocs.Search, thêm tài liệu, và tạo cả các truy vấn faceted đơn giản và các tìm kiếm Boolean tinh vi bằng cách sử dụng **boolean operators java**. Những khả năng này cho phép bạn cung cấp trải nghiệm tìm kiếm nhanh, chính xác và thân thiện với người dùng trên nhiều loại ứng dụng—từ nền tảng thương mại điện tử đến các cơ sở tri thức doanh nghiệp.

Sẵn sàng cho bước tiếp theo? Khám phá các tính năng nâng cao của **GroupDocs.Search** như **highlighting**, **suggestions**, và **real‑time indexing** để tăng cường sức mạnh tìm kiếm cho ứng dụng của bạn.

---

**Cập nhật lần cuối:** 2026-08-26  
**Kiểm thử với:** GroupDocs.Search 25.4 for Java  
**Tác giả:** GroupDocs

## Các hướng dẫn liên quan

- [Wildcard Search Java với GroupDocs.Search – Tính năng nâng cao](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Cách cập nhật Index Java với GroupDocs.Search – Hướng dẫn toàn diện](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Cách triển khai tìm kiếm toàn văn java: tạo thư mục chỉ mục với GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
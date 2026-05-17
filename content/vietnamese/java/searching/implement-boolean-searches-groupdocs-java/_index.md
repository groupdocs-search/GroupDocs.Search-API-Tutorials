---
date: '2026-01-29'
description: Tìm hiểu cách triển khai các truy vấn boolean AND/OR trong Java bằng
  GroupDocs.Search for Java, thêm tài liệu vào chỉ mục và cải thiện việc truy xuất
  tài liệu.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: Thành thạo tìm kiếm Boolean với GroupDocs.Search cho
  Java'
type: docs
url: /vi/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Thành thạo tìm kiếm Boolean với GroupDocs.Search cho Java

Tìm kiếm trong các bộ sưu tập tài liệu khổng lồ có thể giống như việc tìm kim trong bãi cỏ khô. Với các truy vấn **java boolean and or** bạn có thể chỉ định cho engine chính xác những gì bạn cần — tài liệu chứa *cả* hai thuật ngữ, *bất kỳ* thuật ngữ nào, hoặc *loại bỏ* các từ không mong muốn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách thiết lập **GroupDocs.Search for Java**, thêm tài liệu vào chỉ mục, và tạo các truy vấn boolean mạnh mẽ giúp tăng hiệu suất **document retrieval java** của bạn.

## Câu trả lời nhanh
- **Truy vấn boolean AND là gì?** Trả về chỉ các tài liệu chứa *tất cả* các thuật ngữ đã chỉ định.  
- **OR khác gì so với AND?** OR khớp với các tài liệu có *bất kỳ* thuật ngữ nào, mở rộng tập kết quả.  
- **Khi nào nên dùng NOT?** Dùng NOT để lọc ra các tài liệu chứa các từ không mong muốn.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc thử nghiệm; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Yêu cầu phiên bản Java nào?** Hỗ trợ Java 8+; khuyến nghị JDK 11+.

## **java boolean and or** là gì?
Một truy vấn **java boolean and or** kết hợp các toán tử logic (AND, OR, NOT) để tinh chỉnh kết quả tìm kiếm. Bằng cách cấu trúc các truy vấn, bạn cho GroupDocs.Search biết chính xác cách các thuật ngữ liên quan với nhau, mang lại cho bạn khả năng kiểm soát chính xác quá trình truy xuất.

## Tại sao nên sử dụng GroupDocs.Search cho Java?
- **High performance** trên các bộ tài liệu lớn.  
- **Rich API** hỗ trợ cả truy vấn dựa trên văn bản và dựa trên đối tượng.  
- **Built‑in language support** cho stemming, stop‑words và fuzzy matching.  
- **Easy integration** với Maven hoặc tải JAR trực tiếp.

## Yêu cầu trước
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **GroupDocs.Search for Java** (v25.4 hoặc sau) – xem liên kết tải xuống bên dưới.  
- JDK 8+ đã được cài đặt và cấu hình trong IDE của bạn (IntelliJ IDEA, Eclipse, v.v.).  
- Kiến thức cơ bản về Java và Maven để quản lý phụ thuộc.  

## Cài đặt GroupDocs.Search cho Java

### Cấu hình Maven
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

### Tải xuống trực tiếp
Hoặc, tải JAR mới nhất từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Bắt đầu với giấy phép dùng thử miễn phí để khám phá tất cả các tính năng. Đối với môi trường sản xuất, mua giấy phép thương mại để mở khóa đầy đủ chức năng.

### Khởi tạo và Cấu hình Cơ bản
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

## java boolean and or: Triển khai tìm kiếm Boolean
Dưới đây chúng tôi sẽ giới thiệu các truy vấn **AND**, **OR**, **NOT**, và **complex**. Mỗi phần sẽ hiển thị cả truy vấn dạng văn bản thuần và truy vấn dựa trên đối tượng tương đương, để bạn có thể chọn phong cách phù hợp với mã nguồn của mình.

### Tìm kiếm Boolean AND
Kết hợp các thuật ngữ bằng **AND** để chỉ lấy các tài liệu chứa *tất cả* các từ khóa.

#### Tổng quan
Truy vấn AND thu hẹp kết quả, cải thiện độ liên quan khi bạn cần các tài liệu đáp ứng nhiều tiêu chí.

#### Các bước thực hiện
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

### Tìm kiếm Boolean OR
Sử dụng **OR** để mở rộng kết quả, khớp với bất kỳ thuật ngữ nào được cung cấp.

#### Tổng quan
Truy vấn OR là lựa chọn lý tưởng cho các tìm kiếm khám phá khi bạn muốn thu thập các tài liệu chứa ít nhất một trong nhiều từ khóa (**search with or java**).

#### Các bước thực hiện
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

### Tìm kiếm Boolean NOT
Loại bỏ các thuật ngữ không mong muốn bằng **NOT** để lọc bỏ nhiễu trong kết quả.

#### Tổng quan
Truy vấn NOT giúp bạn loại bỏ các tài liệu không liên quan, chẳng hạn lọc bỏ tên thương hiệu của đối thủ (**boolean search examples java**).

#### Các bước thực hiện
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

### Truy vấn Boolean phức tạp
Kết hợp **AND**, **OR**, và **NOT** để tạo ra logic tìm kiếm phức tạp cho các nhu cầu truy xuất rất cụ thể.

#### Tổng quan
Các truy vấn phức tạp cho phép bạn mô phỏng các kịch bản tìm kiếm thực tế, chẳng hạn “tìm các bài báo thể thao có nội dung tích cực nhưng loại bỏ mọi đề cập đến các vận động viên cụ thể”.

#### Các bước thực hiện
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

## Ứng dụng thực tế của các truy vấn java boolean and or
- **Document Management Systems** – locate contracts that contain both “confidential” **AND** “renewal”.  
- **Legal Research** – filter case law with **AND**/ **OR** while excluding outdated statutes using **NOT**.  
- **Customer Support** – retrieve tickets that mention “login” **AND** “error” but not “resolved”.  
- **Content Curation** – gather blog posts about “cloud” **OR** “serverless” for a newsletter.

## Những lỗi thường gặp & Khắc phục
- **Missing Index Refresh** – after adding new documents, call `index.update()` to ensure they are searchable.  
- **Incorrect Operator Spacing** – GroupDocs.Search expects spaces around operators (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – queries are case‑insensitive by default, but custom analyzers may affect this.  
- **Large Result Sets** – use pagination (`search(query, 0, 100)`) to avoid memory overload.

## Câu hỏi thường gặp

**Q: Có thể kết hợp hơn hai thuật ngữ trong một truy vấn AND không?**  
A: Chắc chắn. Bạn có thể nối chuỗi nhiều đối tượng `createWordQuery` bằng `createAndQuery`, hoặc đơn giản viết `"term1 AND term2 AND term3"` trong truy vấn văn bản.

**Q: GroupDocs.Search có hỗ trợ tìm kiếm wildcard hoặc fuzzy không?**  
A: Có. Thêm `*` để thực hiện wildcard (ví dụ `promot*`) hoặc dùng `~` cho fuzzy matching (ví dụ `comfort~`).

**Q: Làm sao để giới hạn tìm kiếm chỉ trong các loại tệp cụ thể?**  
A: Sử dụng lớp `FileTypeQuery` để hạn chế kết quả chỉ ở PDF, DOCX, v.v., và kết hợp nó với truy vấn boolean của bạn.

**Q: Cách tốt nhất để giám sát hiệu năng indexing là gì?**  
A: Bật logger tích hợp sẵn (`index.getLogger().setLevel(Level.INFO)`) và xem các chỉ số thời gian sau mỗi thao tác `add`.

**Q: Có cách nào tăng độ quan trọng của một số từ khóa không?**  
A: Có. Bao bọc các từ quan trọng bằng `BoostQuery` để tăng trọng số của chúng trong thuật toán tính điểm.

---

**Last Updated:** 2026-01-29  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs
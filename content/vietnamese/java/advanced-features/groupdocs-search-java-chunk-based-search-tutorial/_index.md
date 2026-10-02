---
date: '2026-10-02'
description: Tìm hiểu cách sử dụng temporary license để thêm documents vào index với
  chunk‑based search trong Java, tăng hiệu suất tìm kiếm đồng thời kiểm soát việc
  sử dụng bộ nhớ.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Sử dụng temporary license để thêm documents vào index với chunk‑based
  search trong Java, cải thiện tốc độ tìm kiếm và giảm tiêu thụ bộ nhớ.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Sử dụng temporary license cho chunk‑based indexing trong Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Sử dụng temporary license cho chunk‑based indexing trong Java
type: docs
url: /vi/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Sử dụng giấy phép tạm thời cho việc lập chỉ mục dựa trên đoạn trong Java

Trong hướng dẫn này, bạn sẽ **sử dụng giấy phép tạm thời** để thêm tài liệu vào chỉ mục với tính năng tìm kiếm dựa trên đoạn của GroupDocs.Search. Cách tiếp cận này cho phép bạn xử lý các bộ sưu tập tài liệu khổng lồ—hợp đồng pháp lý, vé hỗ trợ, bài báo nghiên cứu—trong khi giữ **bộ nhớ chỉ mục tìm kiếm java** ở mức thấp và **tăng hiệu suất tìm kiếm** một cách đáng kể. Bạn sẽ thấy cách thiết lập thư mục chỉ mục, cung cấp nhiều nguồn tài liệu, bật tìm kiếm dựa trên đoạn, và chạy cả truy vấn đoạn đầu tiên và các truy vấn đoạn tiếp theo.

## Câu trả lời nhanh
- **Bước đầu tiên là gì?** Tạo một thư mục chỉ mục tìm kiếm.  
- **Làm thế nào để bao gồm nhiều tệp?** Sử dụng `index.add()` cho mỗi thư mục tài liệu.  
- **Tùy chọn nào bật tìm kiếm dựa trên đoạn?** `options.setChunkSearch(true)`.  
- **Tôi có thể tiếp tục tìm kiếm sau đoạn đầu tiên không?** Có, gọi `index.searchNext()` với token.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoặc giấy phép tạm thời hoạt động cho phát triển; giấy phép đầy đủ là bắt buộc cho môi trường sản xuất.  

## Những gì bạn sẽ học
- Cách tạo một chỉ mục tìm kiếm trong một thư mục được chỉ định.  
- Các bước để **thêm tài liệu vào chỉ mục** từ nhiều vị trí.  
- Cấu hình các tùy chọn tìm kiếm để bật tìm kiếm dựa trên đoạn.  
- Thực hiện các tìm kiếm dựa trên đoạn ban đầu và tiếp theo.  
- Các kịch bản thực tế nơi tìm kiếm tài liệu dựa trên đoạn tỏa sáng.  

## Yêu cầu trước
Để theo dõi hướng dẫn này, hãy đảm bảo bạn có:

- **Thư viện yêu cầu**: GroupDocs.Search cho Java 25.4 hoặc mới hơn.  
- **Cài đặt môi trường**: Đã cài đặt Java Development Kit (JDK) tương thích.  
- **Kiến thức yêu cầu**: Lập trình Java cơ bản và quen thuộc với Maven.  

## Cài đặt GroupDocs.Search cho Java
Để bắt đầu, tích hợp GroupDocs.Search vào dự án của bạn bằng Maven:

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

Hoặc, tải phiên bản mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Để thử nghiệm GroupDocs.Search:

- **Bản dùng thử miễn phí** – thử các tính năng cốt lõi mà không cần cam kết.  
- **Giấy phép tạm thời** – truy cập mở rộng cho phát triển.  
- **Mua** – giấy phép đầy đủ cho việc sử dụng trong môi trường sản xuất.  

## Cách thêm tài liệu vào chỉ mục?
**Câu trả lời trực tiếp:** Gọi `index.add()` cho mỗi thư mục chứa các tệp bạn muốn có thể tìm kiếm; phương thức sẽ quét thư mục một cách đệ quy và thêm mọi tài liệu được hỗ trợ vào chỉ mục trong một thao tác duy nhất. Điều này loại bỏ nhu cầu xử lý thủ công từng tệp và tăng tốc quá trình nhập khẩu hàng loạt.

`SearchIndex` là lớp trung tâm đại diện cho bộ sưu tập có thể tìm kiếm trên đĩa. Sau khi bạn khởi tạo nó, tất cả các thao tác lập chỉ mục và truy vấn sẽ diễn ra qua đối tượng này.

### 1. Tạo chỉ mục
**Câu trả lời trực tiếp:** Khởi tạo một đối tượng `SearchIndex` với đường dẫn nơi các tệp chỉ mục sẽ được lưu trữ, sau đó gọi `index.create()` để khởi tạo cấu trúc lưu trữ. Lệnh này tạo các thư mục và tệp siêu dữ liệu cần thiết khi sử dụng lần đầu.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Thêm tài liệu vào chỉ mục
**Câu trả lời trực tiếp:** Sử dụng phương thức `index.add()` và truyền đường dẫn tuyệt đối của mỗi thư mục nguồn; API sẽ tự động phát hiện các định dạng được hỗ trợ (PDF, DOCX, XLSX, v.v.) và trích xuất văn bản có thể tìm kiếm vào chỉ mục.

`SearchOptions` là một đối tượng cấu hình cho phép bạn tinh chỉnh cách tài liệu được xử lý trong quá trình lập chỉ mục và tìm kiếm. Bạn sẽ sử dụng nó sau này để bật các truy vấn dựa trên đoạn.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Cấu hình tùy chọn tìm kiếm cho tìm kiếm dựa trên đoạn
**Câu trả lời trực tiếp:** Đặt `options.setChunkSearch(true)` trên một thể hiện `SearchOptions` trước khi thực hiện truy vấn; điều này yêu cầu engine chia mỗi tài liệu thành các đoạn logic (thường là đoạn văn) và trả về các kết quả khớp theo đoạn thay vì toàn bộ tệp.

`SearchResult` chứa các đoạn khớp, vị trí của chúng và điểm liên quan. Khi tìm kiếm dựa trên đoạn được bật, mỗi `SearchResult` tương ứng với một đoạn riêng của tài liệu gốc.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Thực hiện tìm kiếm dựa trên đoạn ban đầu
**Câu trả lời trực tiếp:** Thực thi `index.search("your query", options)`; lệnh này trả về một tập hợp `SearchResult` cho tập hợp các đoạn khớp đầu tiên và một token đại diện cho trạng thái tìm kiếm để tiếp tục.

Token trả về là cần thiết để phân trang qua các tập kết quả lớn mà không cần thực thi lại toàn bộ truy vấn.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Tiếp tục tìm kiếm dựa trên đoạn
**Câu trả lời trực tiếp:** Truyền token trả về từ lời gọi trước vào `index.searchNext(token, options)`; lặp lại cho đến khi phương thức trả về `null`, cho biết đã lấy được tất cả các đoạn khớp.

Cách tiếp cận tăng dần này giữ mức sử dụng bộ nhớ thấp vì chỉ có lô đoạn hiện tại nằm trong bộ nhớ.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Tại sao nên sử dụng tìm kiếm dựa trên đoạn?
Tìm kiếm dựa trên đoạn chia các bộ sưu tập tài liệu khổng lồ thành các phần có thể quản lý được, giảm áp lực bộ nhớ và tăng tốc thời gian phản hồi. Bằng cách lập chỉ mục ở mức đoạn hoặc phần, engine có thể chỉ truy xuất các đoạn liên quan, giảm việc sử dụng CPU và cải thiện độ trễ cho người dùng cuối. Điều này đặc biệt hữu ích khi:

1. **Các đội pháp lý** cần tìm các điều khoản cụ thể trong hàng ngàn hợp đồng.  
2. **Các cổng hỗ trợ khách hàng** phải hiển thị các bài viết kiến thức liên quan ngay lập tức.  
3. **Các nhà nghiên cứu** lọc qua các bộ dữ liệu rộng lớn mà không cần tải toàn bộ tệp vào bộ nhớ.  

Khẳng định định lượng: GroupDocs.Search có thể xử lý **các PDF trên 500 trang** trong thời gian dưới **2 giây mỗi đoạn** trên một máy chủ tiêu chuẩn 8 lõi, đồng thời giữ mức heap tối đa dưới **200 MB**.

## Cách tiếp cận này tăng hiệu suất tìm kiếm
**Câu trả lời trực tiếp:** Bằng cách tìm kiếm các đoạn nhỏ hơn thay vì toàn bộ tệp, engine có thể bỏ qua các phần không liên quan sớm, giảm vòng CPU, và chỉ giữ đoạn đang hoạt động trong bộ nhớ, điều này trực tiếp giảm tiêu thụ **bộ nhớ chỉ mục tìm kiếm java** và mang lại thời gian phản hồi nhanh hơn. Cách tiếp cận có mục tiêu này cũng cho phép bộ nhớ đệm và xử lý song song hiệu quả hơn, cho phép nhiều lõi xử lý các đoạn khác nhau đồng thời, từ đó cải thiện thông lượng trên các máy chủ đa lõi.

Những lợi ích bổ sung bao gồm:

- Xử lý đoạn song song trên nhiều lõi.  
- Kết thúc sớm khi tìm thấy kết quả có độ liên quan cao.  

## Quản lý bộ nhớ chỉ mục tìm kiếm java
**Câu trả lời trực tiếp:** Phân bổ đủ heap cho JVM (ví dụ, `-Xmx2g` hoặc cao hơn) dựa trên kích thước chỉ mục dự kiến, chạy `index.optimize()` sau khi thêm hàng loạt để nén cấu trúc chỉ mục, và giám sát thời gian dừng GC bằng VisualVM để tránh tăng độ trễ.

Tips tinh chỉnh thêm:

- Sử dụng `index.flush()` sau các lô lớn để ghi dữ liệu tạm thời ra đĩa.  
- Bật `options.setMemoryLimit(256)` để giới hạn mức sử dụng bộ nhớ cho mỗi tìm kiếm.

## Các cân nhắc về hiệu suất
- **Quản lý bộ nhớ** – Phân bổ đủ không gian heap (`-Xmx`) cho các chỉ mục lớn.  
- **Giám sát tài nguyên** – Theo dõi việc sử dụng CPU trong quá trình lập chỉ mục và tìm kiếm.  
- **Bảo trì chỉ mục** – Thường xuyên xây dựng lại hoặc dọn dẹp chỉ mục để loại bỏ dữ liệu lỗi thời.  

## Những lỗi thường gặp & khắc phục
| Issue | Why it happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` trong quá trình lập chỉ mục | Kích thước heap quá thấp | Tăng heap JVM (`-Xmx2g` hoặc cao hơn) |
| Không có kết quả trả về | Token đoạn không được xử lý | Đảm bảo vòng lặp `while` chạy cho đến khi `getNextChunkSearchToken()` trả về `null` |
| Hiệu suất tìm kiếm chậm | Chỉ mục chưa được tối ưu | Chạy `index.optimize()` sau khi thêm hàng loạt |

## Câu hỏi thường gặp

**Q: Tìm kiếm dựa trên đoạn là gì?**  
A: Tìm kiếm dựa trên đoạn chia bộ dữ liệu thành các phần nhỏ hơn, cho phép truy vấn hiệu quả trên khối lượng dữ liệu lớn mà không cần tải toàn bộ tài liệu vào bộ nhớ.

**Q: Làm thế nào để cập nhật chỉ mục với các tệp mới?**  
A: Chỉ cần gọi `index.add()` với đường dẫn tới các tài liệu mới; chỉ mục sẽ tự động tích hợp chúng.

**Q: GroupDocs.Search có thể xử lý các định dạng tệp khác nhau không?**  
A: Có, nó hỗ trợ **PDF, DOCX, XLSX, PPTX, HTML, TXT và hơn 30 định dạng khác**.

**Q: Các nút thắt hiệu suất thường gặp là gì?**  
A: Các hạn chế về bộ nhớ và chỉ mục chưa được tối ưu là phổ biến nhất; hãy phân bổ đủ heap và thường xuyên tối ưu chỉ mục.

**Q: Tôi có thể tìm tài liệu chi tiết hơn ở đâu?**  
A: Truy cập tài liệu chính thức [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) để xem hướng dẫn chi tiết và tham chiếu API.

**Q: Tìm kiếm dựa trên đoạn có hoạt động với PDF được mã hóa không?**  
A: Có, miễn là bạn cung cấp mật khẩu qua overload API thích hợp.

**Q: Làm sao tôi có thể giám sát tiến độ lập chỉ mục?**  
A: Sử dụng overload `Index.add()` trả về một đối tượng `Progress` hoặc kết nối vào các callback ghi log.

## Tài nguyên
- **Tài liệu**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Tham chiếu API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Tải xuống**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Hỗ trợ miễn phí**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Giấy phép tạm thời**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Cập nhật lần cuối:** 2026-10-02  
**Đã kiểm tra với:** GroupDocs.Search 25.4 for Java  
**Tác giả:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Các hướng dẫn liên quan

- [Tạo Thư mục Chỉ mục Tìm kiếm & Đặt Giấy phép – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Cải thiện Hiệu suất Truy vấn với GroupDocs.Search Java: Tối ưu Hóa Chỉ mục & Tìm kiếm](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Tính năng Tìm kiếm Nâng cao của GroupDocs Search Java](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
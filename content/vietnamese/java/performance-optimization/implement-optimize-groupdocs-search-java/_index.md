---
date: '2026-07-07'
description: Tìm hiểu cách xóa chỉ mục, thực hiện full text search Java, và tối ưu
  search performance bằng GroupDocs.Search for Java. Hướng dẫn từng bước với cài đặt
  mạng và lập chỉ mục.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Cách xóa chỉ mục và thực hiện full text search Java bằng GroupDocs.Search.
  Thực hiện theo hướng dẫn này để thiết lập search network, tạo searchable index,
  và tối ưu search performance.
og_title: Cách xóa chỉ mục và thực hiện tìm kiếm văn bản với GroupDocs.Search for
  Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Cách xóa chỉ mục và thực hiện tìm kiếm văn bản với GroupDocs.Search for Java
type: docs
url: /vi/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Cách Xóa Chỉ mục và Thực hiện Tìm kiếm Văn bản với GroupDocs.Search cho Java

Trong thế giới dựa trên dữ liệu ngày nay, **cách xóa chỉ mục** nhanh chóng đồng thời vẫn cung cấp khả năng tìm kiếm toàn văn nhanh như chớp trong Java là một lợi thế cạnh tranh. Cho dù bạn đang xây dựng một cơ sở tri thức nội bộ, một kho lưu trữ vụ kiện pháp lý, hoặc một danh mục sản phẩm thương mại điện tử, một mạng tìm kiếm được tối ưu tốt có thể cải thiện đáng kể sự hài lòng của người dùng. Trong hướng dẫn này, bạn sẽ học cách **thiết lập mạng tìm kiếm**, **tạo chỉ mục có thể tìm kiếm**, **tối ưu hiệu suất tìm kiếm**, và **xóa tài liệu khỏi chỉ mục** khi cần — tất cả đều sử dụng GroupDocs.Search cho Java.

## Câu trả lời nhanh
- **Mục đích chính của GroupDocs.Search cho Java là gì?** Nó cung cấp khả năng tìm kiếm toàn văn trên hơn 50 định dạng tài liệu, cho phép truy xuất từ khóa nhanh chóng.  
- **Làm thế nào để thực hiện tìm kiếm văn bản trong môi trường phân tán?** Triển khai một mạng tìm kiếm, lập chỉ mục tài liệu trên nút master, sau đó truy vấn bất kỳ nút nào.  
- **Tôi có thể xóa tài liệu khỏi chỉ mục mà không cần xây dựng lại không?** Có, sử dụng Delete API để loại bỏ các tệp đã chọn, thực tế là *how to delete index* mà không cần tái lập chỉ mục toàn bộ.  
- **Yêu cầu phiên bản Java nào?** JDK 8 hoặc cao hơn.  
- **Cần giấy phép cho môi trường sản xuất không?** Cần một giấy phép GroupDocs.Search hợp lệ; một bản dùng thử miễn phí có sẵn.

## “Thực hiện tìm kiếm văn bản” là gì?
Thực hiện tìm kiếm văn bản có nghĩa là truy vấn một chỉ mục toàn văn để lấy các tài liệu chứa các từ khóa hoặc cụm từ đã chỉ định. GroupDocs.Search xây dựng một chỉ mục đảo ngược giúp các truy vấn này cực kỳ nhanh chóng, ngay cả khi xử lý hàng ngàn tệp.

## Tại sao cần thiết lập mạng tìm kiếm?
Mạng tìm kiếm phân phối tải công việc lập chỉ mục và truy vấn trên nhiều nút, cho phép bạn **tối ưu hiệu suất tìm kiếm**, mở rộng theo chiều ngang và duy trì tính sẵn sàng cao. Kiến trúc này lý tưởng cho các kho lưu trữ tài liệu cấp doanh nghiệp, nơi độ trễ và thông lượng quan trọng.

## Cách triển khai và tối ưu mạng tìm kiếm với GroupDocs.Search cho Java
Tải cấu hình của bạn, khởi động một nút master, sau đó thêm các nút worker chia sẻ cùng đường dẫn cơ sở và cổng. Triển khai mạng theo cách này cho phép bất kỳ nút nào xử lý yêu cầu lập chỉ mục hoặc truy vấn, mang lại thời gian phản hồi nhất quán ngay cả khi số lượng tài liệu tăng lên hàng trăm ngàn.

### Tổng quan từng bước
1. **Xác định cấu hình cơ sở** bao gồm một thư mục chia sẻ và một cổng TCP.  
2. **Khởi động nút master** để quản lý chỉ mục và điều phối các nút worker.  
3. **Thêm các nút worker** kết nối tới master, cho phép lập chỉ mục và tìm kiếm song song.  
4. **Giám sát việc sử dụng tài nguyên** và tinh chỉnh cài đặt heap JVM để giữ độ trễ thấp.

## Cách xóa chỉ mục trong GroupDocs.Search cho Java
`SearchNode` đại diện cho một nút trong mạng GroupDocs.Search quản lý các hoạt động lập chỉ mục và truy vấn. Phương thức `delete` loại bỏ các tài liệu đã chỉ định khỏi chỉ mục.

### Các bước xóa trực tiếp
- Gọi phương thức `delete` trên thể hiện `SearchNode`.  
- Cung cấp một mảng các đường dẫn tệp tương đối.  
- Cam kết các thay đổi; chỉ mục được làm mới ngay lập tức và các tìm kiếm tiếp theo sẽ không trả về các tệp đã bị xóa.

## Mạng tìm kiếm là gì?
Một **mạng tìm kiếm** là một cụm các nút kết nối với nhau chia sẻ một kho lưu trữ chỉ mục chung, cho phép lập chỉ mục và thực thi truy vấn phân tán. Nó cho phép mở rộng theo chiều ngang và chịu lỗi cho các bộ sưu tập tài liệu quy mô lớn.

## Cách tạo chỉ mục có thể tìm kiếm (index documents java)
Phương thức `add` lập chỉ mục một tài liệu vào chỉ mục tìm kiếm. Thêm tài liệu vào nút master bằng phương thức `add`; mạng sẽ truyền các thay đổi tới tất cả các nút worker. Cách tiếp cận này đảm bảo mỗi nút có thể phục vụ các truy vấn dựa trên chỉ mục mới nhất mà không cần các bước đồng bộ bổ sung.

### Các hành động chính
- Chỉ định nút master tới thư mục chứa các tệp nguồn.  
- Gọi quy trình lập chỉ mục; mạng sẽ xử lý mỗi tệp và cập nhật chỉ mục đảo ngược.  
- Xác minh rằng các tệp chỉ mục xuất hiện trong thư mục lưu trữ được chỉ định.

## Cách loại bỏ các tệp đã lập chỉ mục (remove indexed files)
Khi một tài liệu trở nên lỗi thời, gọi API `delete` với đường dẫn của nó. Hệ thống sẽ loại bỏ các mục nhập của tệp khỏi chỉ mục đảo ngược, giải phóng không gian lưu trữ và ngăn ngừa kết quả lỗi thời.

## Cài đặt GroupDocs.Search cho Java
Để bắt đầu, tích hợp GroupDocs.Search vào dự án Java của bạn bằng cách sử dụng cấu hình sau:

### Cấu hình Maven
Add the repository and dependency to your `pom.xml` file:

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
Ngoài ra, bạn có thể [tải phiên bản mới nhất trực tiếp từ GroupDocs](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
GroupDocs cung cấp bản dùng thử miễn phí, cho phép bạn đánh giá các tính năng trước khi mua. Bạn có thể nhận giấy phép tạm thời bằng cách làm theo các bước trên [trang mua hàng](https://purchase.groupdocs.com/temporary-license/). Điều này sẽ kích hoạt đầy đủ chức năng trong giai đoạn thử nghiệm của bạn.

### Khởi tạo và cấu hình cơ bản
Initialize GroupDocs.Search in your Java application with:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Hướng dẫn triển khai

### Cấu hình mạng tìm kiếm
**Tổng quan:** Thiết lập đường dẫn cơ sở và cổng cho mạng tìm kiếm của bạn, cho phép các nút giao tiếp hiệu quả.

#### Bước 1: Xác định cấu hình cơ sở
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Tham số:**  
  - `basePath`: Đường dẫn thư mục cho các hoạt động mạng.  
  - `basePort`: Số cổng được mạng tìm kiếm sử dụng.

#### Bước 2: Khắc phục sự cố
Đảm bảo rằng cổng bạn chỉ định không bị chặn bởi tường lửa hoặc đang được một ứng dụng khác sử dụng. Điều chỉnh khi cần thiết để tránh xung đột.

### Triển khai các nút mạng tìm kiếm
**Tổng quan:** Sử dụng cấu hình của bạn, triển khai các nút trên mạng để thực hiện lập chỉ mục và tìm kiếm phân tán.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Các tùy chọn cấu hình chính:**  
  - **Base Path & Port:** Các giá trị này phải khớp với những gì đã dùng trong cấu hình ban đầu để đảm bảo tính nhất quán.

### Lập chỉ mục tài liệu (`create searchable index`)
**Tổng quan:** Thêm tài liệu vào chỉ mục tìm kiếm một cách hiệu quả bằng nút master.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Mục đích:**  
  - `masterNode`: Nút chính quản lý việc lập chỉ mục tài liệu.  
  - `documentsPath`: Đường dẫn tới thư mục chứa các tài liệu.

#### Mẹo khắc phục sự cố
Xác minh rằng các đường dẫn tài liệu của bạn là đúng và có thể truy cập. Đảm bảo quyền cho phép đọc từ các thư mục này.

### Tìm kiếm văn bản trong mạng (`perform text search`)
**Tổng quan:** Thực hiện các tìm kiếm văn bản toàn diện trên mạng đã lập chỉ mục của bạn.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Tham số:**  
  - `query`: Văn bản bạn đang tìm kiếm.  
  - `masterNode`: Nút thực hiện tìm kiếm.

### Xóa tài liệu khỏi chỉ mục (`delete documents index`)
**Tổng quan:** Loại bỏ các tài liệu cụ thể khỏi chỉ mục của bạn bằng cách sử dụng đường dẫn tệp của chúng.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Mục đích phương thức:**  
  - `node`: Nút mục tiêu cho các thao tác xóa.  
  - `filePaths`: Đường dẫn của các tài liệu sẽ được loại bỏ khỏi chỉ mục.

#### Khắc phục sự cố
Đảm bảo các đường dẫn tệp chính xác và các tệp tồn tại trong thư mục của bạn. Nếu vấn đề vẫn tiếp diễn, kiểm tra quyền mạng và kết nối.

## Ứng dụng thực tiễn
1. **Quản lý tài liệu doanh nghiệp:** Tinh giản việc truy xuất kiến thức nội bộ.  
2. **Phân tích vụ kiện pháp lý:** Nhanh chóng tìm vị trí các tệp vụ kiện liên quan trên nhiều kho lưu trữ.  
3. **Nền tảng thương mại điện tử:** Tăng tốc độ tìm kiếm sản phẩm bằng cách lập chỉ mục mô tả và đánh giá.  
4. **Nghiên cứu học thuật:** Tìm kiếm hiệu quả các thư viện số lớn gồm các bài báo và luận văn.  
5. **Hệ thống hỗ trợ khách hàng:** Giảm thời gian phản hồi bằng cách cho phép nhân viên tìm kiếm các vé hỗ trợ cũ ngay lập tức.

## Các cân nhắc về hiệu năng
- **Tối ưu tốc độ lập chỉ mục:** Thêm tài liệu mới một cách gia tăng trong giờ thấp điểm để giữ độ trễ thấp.  
- **Hướng dẫn sử dụng tài nguyên:** Giám sát CPU và bộ nhớ, đặc biệt khi mở rộng số lượng nút.  
- **Quản lý bộ nhớ Java:** Tinh chỉnh cài đặt heap JVM dựa trên khối lượng công việc của bạn (ví dụ, `-Xmx2g` cho chỉ mục kích thước trung bình).

## Kết luận
Bằng cách làm theo hướng dẫn này, bạn đã học cách **thiết lập mạng tìm kiếm**, **tạo chỉ mục có thể tìm kiếm**, **thực hiện tìm kiếm văn bản**, và **xóa tài liệu khỏi chỉ mục** bằng cách sử dụng GroupDocs.Search cho Java. Những khả năng này cho phép truy xuất tài liệu nhanh chóng và đáng tin cậy trong môi trường phân tán.

**Các bước tiếp theo**
- Thử nghiệm các cấu hình nút khác nhau để tìm cân bằng tối ưu cho khối lượng công việc của bạn.  
- Tìm hiểu sâu hơn các tùy chọn lập chỉ mục nâng cao như bộ phân tích tùy chỉnh và điều chỉnh độ liên quan.  
- Khám phá việc tích hợp với các sản phẩm GroupDocs khác để xử lý tài liệu từ đầu đến cuối.

## Câu hỏi thường gặp

**Q: Trường hợp sử dụng chính của GroupDocs.Search cho Java là gì?**  
A: Nó cung cấp tìm kiếm toàn văn trên nhiều định dạng tài liệu, cho phép bạn **thực hiện tìm kiếm văn bản** trong các kho lưu trữ lớn.

**Q: Làm thế nào tôi có thể cải thiện tốc độ tìm kiếm trong một mạng lớn?**  
A: Triển khai thêm các nút, tinh chỉnh heap JVM, và lên lịch lập chỉ mục trong thời gian ít lưu lượng để **tối ưu hiệu suất tìm kiếm**.

**Q: Có thể xóa một tài liệu duy nhất mà không cần tái lập chỉ mục toàn bộ bộ sưu tập không?**  
A: Có, sử dụng API **delete documents index** như trong ví dụ mã để loại bỏ các tệp cụ thể.

**Q: Tôi có cần giấy phép cho việc phát triển không?**  
A: Giấy phép dùng thử miễn phí đủ cho việc thử nghiệm; giấy phép thương mại cần thiết cho triển khai sản xuất.

**Q: Tôi có thể lập chỉ mục PDF, Word và email cùng lúc không?**  
A: Chắc chắn—GroupDocs.Search hỗ trợ đa dạng các định dạng ngay từ đầu.

---

**Cập nhật lần cuối:** 2026-07-07  
**Kiểm tra với:** GroupDocs.Search for Java 25.4  
**Tác giả:** GroupDocs

## Các hướng dẫn liên quan

- [Cách lập chỉ mục văn bản trong Java với hướng dẫn GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Tối ưu hiệu suất tìm kiếm với kỹ thuật lập chỉ mục nâng cao trong GroupDocs.Search cho Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Cải thiện hiệu suất truy vấn với GroupDocs.Search Java: Tối ưu chỉ mục & tìm kiếm](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
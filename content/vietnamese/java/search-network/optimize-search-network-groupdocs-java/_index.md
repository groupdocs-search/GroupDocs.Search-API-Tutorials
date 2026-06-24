---
date: '2026-05-17'
description: Tìm hiểu cách cấu hình search network java, tối ưu hóa shards, thực hiện
  text search và xử lý port conflicts với GroupDocs.Search cho Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Cách Tối Ưu Hóa Shards trong GroupDocs.Search cho Java: Hướng Dẫn Toàn Diện'
type: docs
url: /vi/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Cách Tối Ưu Hóa Shard trong GroupDocs.Search cho Java: Hướng Dẫn Toàn Diện

Efficient document searching is essential for developers and businesses that manage large data sets or need fast internal retrieval. In this tutorial you’ll learn **how to configure search network java**, how to index and query documents, and the exact steps to **optimize shards** for peak performance. We’ll also cover real‑world use cases, common pitfalls, and practical tips to keep your search nodes running smoothly.

## Câu trả lời nhanh
- **What is shard optimization?** Nó tái tổ chức dữ liệu chỉ mục để tăng tốc truy vấn và giảm chi phí lưu trữ.  
- **How to configure a search network?** Xác định thư mục cơ sở và cổng, sau đó triển khai các nút bằng API được cung cấp.  
- **How to perform text search?** Sử dụng `TextSearchInNetwork.searchAll` với chuỗi truy vấn của bạn.  
- **How to index documents in Java?** Thêm các thư mục tài liệu vào nút master bằng `IndexingDocuments.addDirectories`.  
- **How to handle port conflicts?** Thay đổi biến `basePort` sang một cổng chưa được sử dụng trên máy của bạn.

## Cách Cấu Hình Mạng Tìm Kiếm
`Configuration` lưu trữ tất cả các cài đặt cần thiết để khởi chạy một mạng GroupDocs.Search, chẳng hạn như vị trí thư mục chỉ mục và cổng giao tiếp.  
`SearchNetwork` điều phối các nút, xử lý việc lập chỉ mục và phân phối truy vấn.

Tải cấu hình tìm kiếm của bạn, đặt đường dẫn cơ sở tài liệu, chọn một cổng trống và khởi động mạng — tất cả trong vài dòng mã. Câu trả lời trực tiếp này giải thích toàn bộ quy trình trong dưới 70 từ: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`.** Mạng sẽ tự động khởi tạo một nút master và bất kỳ nút worker cần thiết nào, sẵn sàng nhận yêu cầu lập chỉ mục.

### Định Nghĩa Anchor
`Configuration` là lớp cốt lõi lưu trữ tất cả các cài đặt cần thiết để khởi chạy một mạng GroupDocs.Search, chẳng hạn như vị trí thư mục chỉ mục và cổng giao tiếp.

Để tránh lỗi “port already in use” đáng sợ, trước tiên hãy xác minh rằng cổng đã chọn đang trống (ví dụ, sử dụng `netstat` hoặc một kiểm tra socket đơn giản) trước khi khởi tạo mạng.

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

## Cách Lập Chỉ Mục Tài Liệu Java
`IndexingDocuments` là một lớp tiện ích giúp đơn giản hoá việc thêm nhiều thư mục vào một nút tìm kiếm và kích hoạt quy trình lập chỉ mục.

Thêm các thư mục tài liệu của bạn vào nút master, sau đó để trình lập chỉ mục quét chúng. **Direct answer:** Gọi `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` và sau đó gọi `masterNode.index()`; engine sẽ tạo các shard có thể tìm kiếm cho mỗi thư mục bạn cung cấp. Cách tiếp cận này mở rộng theo chiều ngang — thêm nhiều nút, và cùng một phương thức sẽ tự động phân phối khối lượng công việc.

### Định Nghĩa Anchor
`IndexingDocuments` là một lớp tiện ích giúp đơn giản hoá việc thêm nhiều thư mục vào một nút tìm kiếm và kích hoạt quy trình lập chỉ mục.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Cách Thực Hiện Tìm Kiếm Văn Bản
`TextSearchInNetwork` cung cấp các phương thức tĩnh hỗ trợ phát một truy vấn văn bản tới mọi nút trong mạng và tổng hợp kết quả.  
`SearchResult` bao gồm ID của tài liệu khớp, đoạn trích và điểm liên quan.

Chạy một truy vấn trên tất cả các shard bằng một lần gọi phương thức. **Direct answer:** Sử dụng `TextSearchInNetwork.searchAll("your query", searchNetwork)`; phương thức này trả về một tập hợp các đối tượng `SearchResult` chứa ID tài liệu, đoạn trích và điểm liên quan. Bạn có thể lọc kết quả thêm theo ngôn ngữ, loại tệp hoặc siêu dữ liệu tùy chỉnh mà không cần viết mã bổ sung.

### Định Nghĩa Anchor
`TextSearchInNetwork` cung cấp các phương thức tĩnh hỗ trợ phát một truy vấn văn bản tới mọi nút trong mạng và tổng hợp kết quả.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Cách Xử Lý Xung Đột Cổng
Nếu cổng mặc định (`49132`) đã được chiếm dụng, chỉ cần chọn một cổng trống khác và cập nhật trường `basePort` trước khi khởi động mạng. **Direct answer:** Thay đổi `int basePort = 49132;` thành một giá trị chưa được sử dụng như `49133`, biên dịch lại và khởi động lại; mạng sẽ liên kết với cổng mới mà không ảnh hưởng đến các nút hiện có.

Mẹo: Giữ một tệp cấu hình nhỏ (ví dụ, `search-config.properties`) để bạn có thể thay đổi cổng mà không cần biên dịch lại.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Yêu Cầu Trước
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có các yêu cầu sau:

### Thư Viện, Phiên Bản và Phụ Thuộc Yêu Cầu
Để triển khai giải pháp này, bao gồm thư viện GroupDocs.Search bằng Maven bằng cách thêm cấu hình sau vào tệp `pom.xml` của bạn:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Hoặc tải phiên bản mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Yêu Cầu Thiết Lập Môi Trường
- Java Development Kit (JDK) 8 hoặc mới hơn.  
- Quyền mạng cho phép liên kết tới `basePort` đã chọn.  
- Không gian đĩa đủ cho các tệp chỉ mục (mỗi shard có thể chiếm ~10 MB cho 1.000 tài liệu).

### Kiến Thức Yêu Cầu
Kiến thức cơ bản về Java, lập trình hướng đối tượng và xử lý ngoại lệ sẽ giúp bạn theo dõi các ví dụ một cách suôn sẻ.

## Cài Đặt GroupDocs.Search cho Java
Để bắt đầu sử dụng GroupDocs.Search trong dự án của bạn, làm theo các bước sau:

1. **Add the Dependency**: Như đã trình bày ở trên, thêm phụ thuộc Maven cần thiết vào dự án của bạn hoặc tải trực tiếp từ trang phát hành.  
2. **License Acquisition**:  
   - **Free trial** – không cần khóa giấy phép, nhưng việc sử dụng bị giới hạn 500 tài liệu mỗi ngày.  
   - **Temporary license** – yêu cầu khóa dùng thử 30 ngày từ [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – mua giấy phép sản xuất để truy cập không giới hạn và hỗ trợ ưu tiên.  
3. **Basic Initialization and Setup**:  
   Khởi tạo cấu hình bằng lớp `Configuration`, thiết lập đường dẫn cơ sở cho tài liệu và chỉ định số cổng:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Hướng Dẫn Triển Khai
Bây giờ chúng ta sẽ khám phá việc triển khai các tính năng chính bằng GroupDocs.Search Java.

### Tính Năng: Cấu Hình Mạng Tìm Kiếm
**Overview**: Thiết lập một mạng tìm kiếm bao gồm việc xác định thư mục tài liệu của bạn và cấu hình nó với một cổng cụ thể để giao tiếp giữa các nút.

#### Bước 1: Xác Định Thư Mục Tài Liệu và Cổng
`DocumentDirectory` là một đối tượng đơn giản giữ đường dẫn tuyệt đối của thư mục bạn muốn lập chỉ mục. Cung cấp một hoặc nhiều đường dẫn cho cấu hình.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Bước 2: Cấu Hình Mạng Tìm Kiếm
Tạo đối tượng cấu hình bằng cách sử dụng các đường dẫn đã định nghĩa:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Tính Năng: Triển Khai Các Nút Mạng Tìm Kiếm
**Overview**: Triển khai các nút để xử lý tìm kiếm tài liệu một cách hiệu quả trên mạng của bạn.

#### Bước 1: Triển Khai Các Nút Sử Dụng Cấu Hình
Triển khai các nút mạng tìm kiếm và xác định nút master để quản lý tập trung:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Tính Năng: Đăng Ký Sự Kiện Nút Mạng
**Overview**: Giám sát mạng tìm kiếm của bạn bằng cách đăng ký các sự kiện thông báo các thay đổi hoặc hành động quan trọng.

#### Bước 1: Đăng Ký Sự Kiện Nút Master
`SearchNetworkEventListener` cho phép bạn phản hồi khi hoàn thành lập chỉ mục, lỗi nút, hoặc tối ưu hoá shard.

CODE_BLOCK_PLACEHOLDER_9_END

### Tính Năng: Lập Chỉ Mục Tài Liệu trong Các Nút Mạng
**Overview**: Thêm các thư mục chứa tài liệu vào quá trình lập chỉ mục để tìm kiếm hiệu quả.

#### Bước 1: Thêm Thư Mục Tài Liệu vào Quy Trình Lập Chỉ Mục
Cung cấp danh sách các đường dẫn thư mục cho nút master; engine sẽ tạo một shard riêng cho mỗi thư mục, cho phép thực thi truy vấn song song.

CODE_BLOCK_PLACEHOLDER_10_END

### Tính Năng: Tìm Kiếm Văn Bản trong Các Nút Mạng
**Overview**: Thực hiện tìm kiếm văn bản trên tất cả tài liệu đã lập chỉ mục trong mạng tìm kiếm của bạn.

#### Bước 1: Thực Hiện Tìm Kiếm Văn Bản
Gọi phương thức tĩnh trợ giúp để chạy một truy vấn và lấy các tài liệu khớp cùng điểm liên quan.

CODE_BLOCK_PLACEHOLDER_11_END

### Tính Năng: Tối Ưu Hóa Shard
**Overview**: Cải thiện hiệu năng bằng cách tối ưu hoá shard trong bộ lập chỉ mục của nút mạng tìm kiếm của bạn.

#### Bước 1: Tối Ưu Hoá Shard của Bộ Lập Chỉ Mục
Tối ưu hoá shard để cải thiện hiệu quả tìm kiếm (đây là nơi **how to optimize shards** thực sự quan trọng):

CODE_BLOCK_PLACEHOLDER_12_END

## Ứng Dụng Thực Tiễn
GroupDocs.Search cho Java có thể được áp dụng trong nhiều kịch bản thực tế, mỗi trường hợp đều hưởng lợi từ việc tối ưu hoá shard:

1. **Enterprise Document Management** – Xử lý các kho lưu trữ hơn 10 TB với thời gian truy vấn dưới giây sau khi tối ưu hoá shard.  
2. **E‑commerce Platforms** – Hỗ trợ tìm kiếm sản phẩm trên 1 triệu SKU, giảm độ trễ lên tới 45 % khi shard được tối ưu hoá.  
3. **Legal Firms** – Truy xuất hồ sơ vụ án từ kho 200 GB trong vòng dưới 200 ms.  
4. **Library Systems** – Hỗ trợ tìm kiếm danh mục cho 500 nghìn sách kỹ thuật số với việc sử dụng bộ nhớ hiệu quả.  
5. **Content Management Systems (CMS)** – Cho phép khám phá nội dung ngay lập tức cho các triển khai đa site với hơn 2 triệu trang.

## Các Yếu Tố Hiệu Suất
Để đảm bảo hiệu suất tối ưu cho triển khai GroupDocs.Search của bạn:

- **Regularly optimize shards** – Chạy `optimizeShards()` sau mỗi 10 GB dữ liệu mới giảm thời gian phản hồi truy vấn từ 30‑50 %.  
- **Monitor memory usage** – Giữ heap JVM dưới 75 % RAM vật lý; bật G1GC cho các chỉ mục lớn.  
- **Use incremental indexing** – Chỉ thêm các tệp đã thay đổi để tránh lập chỉ mục toàn bộ.  
- **Leverage multi‑node scaling** – Thêm các nút worker để phân phối shard; mỗi nút bổ sung có thể cải thiện thông lượng khoảng ~20 % cho tải công việc đọc nặng.

## Các Vấn Đề Thường Gặp và Giải Pháp
| Vấn đề | Triệu chứng | Giải pháp |
|-------|-------------|-----------|
| Xung đột cổng khi khởi động | `java.net.BindException: Address already in use` | Thay đổi `basePort` thành một giá trị chưa được sử dụng; xác minh bằng `netstat -ano`. |
| Lỗi thiếu bộ nhớ trong quá trình tối ưu hoá | `java.lang.OutOfMemoryError: Java heap space` | Tăng cờ JVM `-Xmx` hoặc chạy tối ưu hoá trên một nút chuyên dụng có RAM nhiều hơn. |
| Thiếu tài liệu trong kết quả tìm kiếm | Không có kết quả nào được trả về sau khi lập chỉ mục | Đảm bảo các thư mục được thêm đúng cách qua `IndexingDocuments.addDirectories` và `masterNode.index()` đã hoàn thành mà không có ngoại lệ. |
| Shard lỗi thời sau xóa hàng loạt | Các tệp đã xóa vẫn xuất hiện | Chạy `optimizeShards()` để hợp nhất các segment và loại bỏ tombstones. |

## Câu Hỏi Thường Gặp

**Q: Tối ưu hoá shard ảnh hưởng như thế nào đến tốc độ truy vấn?**  
A: Tối ưu hoá shard làm nén chỉ mục, giảm I/O đĩa, và thường mang lại tốc độ phản hồi truy vấn nhanh hơn 30‑50 % cho các bộ dữ liệu lớn.

**Q: Có an toàn khi chạy `optimizeShards` trên một nút đang hoạt động không?**  
A: Có, thao tác này được thiết kế để chạy mà không gây downtime, nhưng nên lên lịch trong thời gian ít lưu lượng cho các chỉ mục lớn hơn 20 GB.

**Q: Tôi có thể tùy chỉnh `OptimizeOptions` không?**  
A: Chắc chắn. Bạn có thể đặt các tham số như `maxSegmentSize` hoặc `mergeFactor` để tinh chỉnh quá trình tối ưu hoá.

**Q: Tôi nên làm gì nếu gặp `IOException` trong quá trình tối ưu hoá?**  
A: Kiểm tra quyền hệ thống tệp, đảm bảo đủ không gian đĩa trống, và xác nhận không có tiến trình nào khác đang khóa các tệp chỉ mục.

**Q: Tối ưu hoá shard có khôi phục không gian tài liệu đã xóa không?**  
A: Có, bộ tối ưu hoá sẽ hợp nhất các segment và loại bỏ tombstones, giải phóng không gian chiếm bởi các tài liệu đã xóa.

## Kết Luận
Bằng cách làm theo hướng dẫn toàn diện này, bạn hiện đã biết cách **configure search network java**, lập chỉ mục tài liệu, chạy truy vấn văn bản, và quan trọng nhất, **optimize shards** để duy trì hiệu năng tìm kiếm sắc bén. Áp dụng các mẫu này cho bất kỳ giải pháp tìm kiếm doanh nghiệp dựa trên Java nào, và bạn sẽ thấy cải thiện đáng đo lường về độ trễ, khả năng mở rộng và sử dụng tài nguyên. Đối với các bước tiếp theo, khám phá các tính năng nâng cao như bộ phân tích tùy chỉnh, tìm kiếm phân lớp, và tích hợp với các nhà cung cấp lưu trữ đám mây.

---

**Cập nhật lần cuối:** 2026-05-17  
**Được kiểm tra với:** GroupDocs.Search 25.4 for Java  
**Tác giả:** GroupDocs

## Các Hướng Dẫn Liên Quan

- [Cấu hình Mạng GroupDocs.Search trong .NET: Hướng Dẫn Toàn Diện](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Lập chỉ mục tài liệu .NET Master với GroupDocs.Search: Hướng Dẫn Toàn Diện](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Hướng dẫn và ví dụ về GroupDocs.Search cho Java](/search/net/)
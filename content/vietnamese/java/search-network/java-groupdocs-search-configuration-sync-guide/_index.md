---
date: '2026-05-17'
description: Tìm hiểu cách thêm phụ thuộc groupdocs Maven, thiết lập mạng tìm kiếm
  Java và thêm thư mục vào chỉ mục để truy xuất tài liệu nhanh chóng, mở rộng được.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Cách Thêm Phụ Thuộc GroupDocs Maven cho Mạng Tìm Kiếm
type: docs
url: /vi/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Cách Thêm Phụ Thuộc Maven của GroupDocs cho Mạng Tìm Kiếm

Trong hướng dẫn toàn diện này, bạn sẽ khám phá **how to add groupdocs Maven dependency**, cấu hình một mạng tìm kiếm Java mạnh mẽ bằng cách sử dụng GroupDocs.Search, và giữ cho các shard của bạn được đồng bộ. Cho dù bạn đang lập chỉ mục các bản tóm tắt pháp lý, báo cáo tài chính, hay các bài báo học thuật, các bước dưới đây sẽ giúp bạn tạo các chỉ mục có thể tìm kiếm, phân phối tải truy vấn qua các nút, và duy trì tính nhất quán dữ liệu với ít công sức.

## Câu Trả Lời Nhanh
- **What is the GroupDocs Maven dependency?** Một artifact Maven chứa thư viện GroupDocs.Search cho các dự án Java.  
- **Why use a search network?** Nó phân phối tải lập chỉ mục và truy vấn qua nhiều nút, cải thiện tốc độ và độ tin cậy.  
- **How do I add directories to index?** Sử dụng `IndexingDocuments.addDirectories` trên nút master.  
- **How to sync shards?** Gọi `SynchronizeOptions` trên `Indexer` của mỗi nút.  
- **Do I need a license?** Có, cần có giấy phép dùng thử hoặc thương mại cho môi trường sản xuất.

## Phụ Thuộc Maven của GroupDocs là gì?
`GroupDocs Maven dependency` là một artifact Maven chứa thư viện GroupDocs.Search cho các dự án Java.  
Nó cung cấp tất cả các lớp cần thiết để tạo các chỉ mục có thể tìm kiếm, quản lý các nút mạng, và thực thi các truy vấn nhanh, và Maven tự động giải quyết các phụ thuộc truyền thống, mang đến cho bạn một công cụ tìm kiếm sẵn sàng sử dụng chỉ với vài dòng trong `pom.xml`.

## Cách Thêm Phụ Thuộc Maven của GroupDocs
Thêm các mục repository và dependency vào `pom.xml` của bạn, sau đó chạy `mvn clean install`; Maven sẽ tải về JAR `groupdocs-search` và các thư viện cần thiết, làm cho API sẵn sàng trong dự án của bạn. Sau khi quá trình build thành công, bạn có thể bắt đầu sử dụng các lớp `com.groupdocs.search` ngay lập tức.

### Cấu Hình Maven
Thêm repository và dependency vào `pom.xml` của bạn:

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

> **Pro tip:** Giữ cho số phiên bản luôn cập nhật bằng cách kiểm tra trang phát hành chính thức.

Bạn cũng có thể tải JAR trực tiếp từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Tại Sao Nên Sử Dụng Mạng Tìm Kiếm?
Mạng tìm kiếm cho phép mở rộng ngang bằng cách phân chia chỉ mục thành các shard nằm trên các nút riêng biệt. GroupDocs.Search có thể xử lý **hơn 50 định dạng đầu vào** và xử lý **các tài liệu hàng trăm trang** mà không cần tải toàn bộ tệp vào bộ nhớ, cung cấp phản hồi truy vấn dưới một giây ngay cả khi khối lượng dữ liệu tăng lên.

## Yêu Cầu Trước
- **JDK** (11 hoặc mới hơn) đã được cài đặt.  
- Một IDE như IntelliJ IDEA hoặc Eclipse.  
- Kiến thức cơ bản về Java, quen thuộc với Maven, và hiểu biết về các khái niệm nút mạng.  
- Giấy phép GroupDocs.Search hợp lệ (bản dùng thử miễn phí hoặc thương mại).

## Khởi Tạo và Cấu Hình Cơ Bản
Bắt đầu bằng việc tạo một thư mục chỉ mục:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Bước đơn giản này chuẩn bị môi trường cho cấu hình mạng tiếp theo.

## Hướng Dẫn Triển Khai

### Tính Năng 1: Cấu Hình Mạng Tìm Kiếm
#### Tổng Quan
Cấu hình mạng tìm kiếm đặt các đường dẫn tệp và cổng mà các nút sẽ sử dụng để giao tiếp.

##### Thiết Lập Đường Dẫn và Cổng
Configuration là một lớp chứa các đường dẫn mạng, cổng và các cài đặt khác cho cụm tìm kiếm.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
Đối tượng `configuration` hiện đã chứa tất cả các cài đặt cần thiết cho mạng tìm kiếm của bạn.

### Tính Năng 2: Triển Khai Các Nút Mạng Tìm Kiếm
#### Tổng Quan
Triển khai các nút để phân phối khối lượng công việc qua mạng của bạn. Nút master quản lý các hoạt động và sự kiện.

##### Mã Triển Khai
SearchNetworkNode đại diện cho một nút trong mạng tìm kiếm có thể hoạt động như master hoặc worker.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Tính Năng 3: Đăng Ký Sự Kiện Nút Mạng Tìm Kiếm
#### Tổng Quan
Lắng nghe các sự kiện cho phép xử lý động các thay đổi hoặc cập nhật trong mạng của bạn.

##### Triển Khai Đăng Ký
SearchNetworkNodeEvents cung cấp các hook sự kiện cho vòng đời nút và các hành động lập chỉ mục.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Tính Năng 4: Thêm Thư Mục Vào Chỉ Mục
#### Tổng Quan
Thêm thư mục là bước cốt lõi giúp tài liệu của bạn có thể tìm kiếm được.

##### Thêm Tài Liệu
`IndexingDocuments.addDirectories` thêm các đường dẫn thư mục vào chỉ mục để xử lý.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Tính Năng 5: Đồng Bộ Hóa Shard trong Nút Mạng Tìm Kiếm
#### Tổng Quan
Đồng bộ hóa đảm bảo tính nhất quán dữ liệu trên tất cả các shard.

##### Mã Đồng Bộ
`SynchronizeOptions` cấu hình cách các shard được đồng bộ trên các nút.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Tính Năng 6: Đóng Các Nút Mạng Tìm Kiếm
#### Tổng Quan
Đóng đúng cách các nút sẽ giải phóng tài nguyên và ngăn ngừa rò rỉ bộ nhớ.

##### Đóng Nút
`close()` giải phóng tài nguyên và tắt nút mạng tìm kiếm.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Ứng Dụng Thực Tế
1. **Legal Document Management** – Nhanh chóng truy xuất hồ sơ vụ án và tiền lệ.  
2. **Financial Record Keeping** – Truy cập báo cáo và dấu vết kiểm toán trong vài giây.  
3. **Academic Research** – Tìm kiếm qua hàng ngàn bài báo để tìm các trích dẫn liên quan.

## Các Yếu Tố Hiệu Suất
- **Optimize Queries** – Viết các truy vấn ngắn gọn để giảm thời gian phản hồi.  
- **Memory Management** – Giám sát việc sử dụng heap của JVM; cân nhắc tinh chỉnh GC cho các chỉ mục lớn.  
- **Scaling Strategy** – Thêm các nút tỷ lệ với khối lượng dữ liệu và tải truy vấn.

## Các Vấn Đề Thường Gặp và Giải Pháp
| Vấn Đề | Nguyên Nhân | Giải Pháp |
|-------|-------|----------|
| Các nút không kết nối được | Xung đột cổng | Thay đổi `basePort` thành giá trị chưa được sử dụng |
| Chỉ mục không cập nhật | Thiếu đăng ký sự kiện | Đảm bảo gọi `SearchNetworkNodeEvents.subscribe(masterNode)` |
| Độ trễ cao | Số shard không đủ | Tăng số lượng nút và cân bằng phân phối tài liệu |

## Câu Hỏi Thường Gặp
**Q: What is the primary benefit of using GroupDocs.Search?**  
A: Nó cung cấp khả năng tìm kiếm nhanh, mở rộng được trên các tập tài liệu lớn với cấu hình tối thiểu.

**Q: Can I customize node configurations in a search network?**  
A: Có, bạn có thể đặt các đường dẫn, cổng và các tùy chọn khác tùy chỉnh thông qua đối tượng `Configuration`.

**Q: How do I add directories to index after the network is running?**  
A: Gọi `IndexingDocuments.addDirectories(masterNode, "path")` bất cứ khi nào bạn cần lập chỉ mục các thư mục mới.

**Q: How to sync shards when a new node joins the network?**  
A: Sử dụng phương thức `synchronizeShards` được mô tả ở trên trên nút mới được thêm vào.

**Q: Do I need a license for development?**  
A: Giấy phép dùng thử miễn phí đủ cho việc thử nghiệm; giấy phép thương mại cần cho môi trường sản xuất.

## Kết Luận
Bằng cách làm theo hướng dẫn này, bạn đã biết cách **add groupdocs Maven dependency**, cấu hình một mạng tìm kiếm đa nút, lập chỉ mục các thư mục, và giữ các shard đồng bộ. Những bước này tạo nền tảng cho giải pháp tìm kiếm tài liệu hiệu suất cao có thể mở rộng cùng nhu cầu của tổ chức bạn.

---

**Cập Nhật Cuối Cùng:** 2026-05-17  
**Đã Kiểm Tra Với:** GroupDocs.Search 25.4  
**Tác Giả:** GroupDocs

## Hướng Dẫn Liên Quan
- [Hướng Dẫn và Ví Dụ về GroupDocs.Search cho Java](/search/net/)
- [Cấu Hình Mạng GroupDocs.Search trong .NET: Hướng Dẫn Toàn Diện](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Cách Triển Khai Mạng Tìm Kiếm với GroupDocs.Search trong .NET cho Hệ Thống Quản Lý Tài Liệu](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
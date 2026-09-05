---
date: '2026-05-17'
description: Tìm hiểu cách cấu hình cổng cơ bản groupdocs cho một mạng GroupDocs.Search
  Java có khả năng mở rộng, tối ưu tốc độ truy xuất và thiết lập hệ thống đa nút.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Cấu hình cổng cơ bản groupdocs trong Mạng Tìm kiếm Java
type: docs
url: /vi/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Cấu hình cổng cơ sở groupdocs trong Mạng Tìm kiếm Java

Trong các ứng dụng hiện đại, dữ liệu nặng, **configure base port groupdocs** là bước đầu tiên để xây dựng một hạ tầng tìm kiếm nhanh chóng và đáng tin cậy. Cho dù bạn đang lập chỉ mục hàng ngàn tệp PDF hoặc mở rộng trên nhiều máy chủ, việc gán các cổng và thư mục duy nhất ngăn ngừa xung đột giữa các nút và giữ cho cụm hoạt động khỏe mạnh. Hướng dẫn này sẽ đưa bạn qua các yêu cầu trước, cài đặt và cấu hình đa‑nút hoàn chỉnh bằng GroupDocs.Search cho Java, để bạn có thể khởi chạy một mạng tìm kiếm thực sự mở rộng ngay hôm nay.

## Câu trả lời nhanh
- **Mục đích chính là gì?** Để gán các cổng và thư mục cơ sở duy nhất cho mỗi nút tìm kiếm, loại bỏ xung đột.  
- **Tôi có cần giấy phép không?** Có – cần giấy phép dùng thử hoặc đầy đủ cho các triển khai sản xuất.  
- **Phiên bản Java nào được hỗ trợ?** Java 8 trở lên (khuyến nghị Java 11+).  
- **Tôi có thể chạy trên máy chủ đám mây không?** Chắc chắn – chỉ cần mở các cổng đã chọn trong nhóm bảo mật đám mây của bạn.  
- **Tôi có thể thêm bao nhiêu nút?** Không có giới hạn cứng; chỉ bị ràng buộc bởi phần cứng và khả năng mạng.

## “configure base port groupdocs” là gì?
**Configure base port groupdocs** là quá trình gán một cổng TCP khởi đầu cho mỗi nút tìm kiếm và tăng dần cho các nút tiếp theo. Bước đơn giản này loại bỏ các lỗi “cổng đã được sử dụng” đáng sợ và đặt nền tảng cho một cụm tìm kiếm sạch sẽ, có khả năng mở rộng theo chiều ngang, đảm bảo mỗi nút giao tiếp qua một điểm cuối riêng biệt.

## Tại sao sử dụng GroupDocs.Search cho một mạng lưới có khả năng mở rộng?
GroupDocs.Search cung cấp **đánh chỉ mục hiệu suất cao** (lên tới 50 GB/phút trên máy chủ 8‑core tiêu chuẩn) và hỗ trợ **hơn 50 định dạng tệp** bao gồm PDF, DOCX, PPTX và HTML. Kiến trúc mô-đun cho phép bạn kết hợp các bộ lập chỉ mục, công cụ tìm kiếm, shard và extractor trên các nút, cung cấp khả năng mở rộng tuyến tính khi bạn thêm phần cứng. Thư viện còn cung cấp các tùy chọn nén tích hợp giảm dung lượng đĩa lên tới 70 % trong khi giữ độ trễ truy vấn dưới 200 ms cho các khối lượng công việc điển hình.

## Yêu cầu trước
- **Bộ công cụ phát triển Java (JDK)** 8 hoặc mới hơn (khuyến nghị Java 11+ để thu gom rác tốt hơn).  
- **IDE** như IntelliJ IDEA hoặc Eclipse.  
- **Thư viện GroupDocs.Search for Java** (phiên bản 25.4 hoặc mới hơn) được cài đặt qua Maven hoặc tải xuống thủ công.  
- Kiến thức cơ bản về mạng (cổng TCP, localhost so với máy chủ từ xa).  
- Giấy phép **GroupDocs.Search** hợp lệ (dùng thử hoặc đầy đủ).

## Cài đặt GroupDocs.Search cho Java

### Hướng dẫn cài đặt

**Maven Setup:**

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

**Direct Download:**

Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Đăng ký giấy phép

- **Dùng thử miễn phí** – bắt đầu kiểm tra ngay lập tức.  
- **Giấy phép tạm thời** – nhận bản dùng thử mở rộng tại [Temporary License](https://purchase.groupdocs.com/temporary-license).  
- **Mua đầy đủ** – cần thiết cho triển khai sản xuất.

### Khởi tạo và Cài đặt Cơ bản

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Hướng dẫn triển khai

### Cách cấu hình base port groupdocs?

Để cấu hình cổng cơ sở, chỉnh sửa tệp cấu hình mạng hoặc thiết lập thuộc tính `basePort` trong mã nguồn thành một giá trị cao, chưa được sử dụng như 49100. Đối với mỗi nút tiếp theo, tăng số cổng lên một (hoặc một khoảng cố định) để mỗi nút gắn vào điểm cuối TCP riêng, loại bỏ lỗi xung đột cổng và đơn giản hoá quy tắc tường lửa.

#### Thiết lập Đường dẫn Cơ sở

Trước khi viết bất kỳ mã nào, hãy quyết định một bố cục thư mục nhất quán. Ví dụ, tạo các thư mục riêng cho các bộ lập chỉ mục (`Indexer0`), công cụ tìm kiếm (`Searcher0`) và extractor (`Extractor0`). Cấu trúc này cho phép mỗi nút nhanh chóng giải quyết các tệp của mình.

- **Tại sao**: Cấu trúc thư mục dự đoán được ngăn ngừa lỗi “file not found” khi các nút khởi động trên các máy khác nhau.

#### Cấu hình Cổng Cơ sở

Chọn một cổng khởi đầu cao để tránh xung đột với các dịch vụ phổ biến (HTTP 80, SSH 22, v.v.). Tăng số cổng cho mỗi nút mới bạn thêm.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Tại sao**: Bắt đầu ở một cổng cao (ví dụ 49100) giảm khả năng trùng lặp với các dịch vụ hiện có và đơn giản hoá việc tạo quy tắc tường lửa.

#### Xác định Địa chỉ Máy chủ

Trong quá trình phát triển, `localhost` hoạt động tốt. Đối với môi trường sản xuất, thay thế bằng địa chỉ IP của máy chủ hoặc tên DNS để các nút từ xa có thể kết nối với nhau.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Tại sao**: Sử dụng địa chỉ máy chủ thực tế cho phép giao tiếp giữa các máy, điều này thiết yếu cho các cụm đám mây hoặc on‑premise.

#### Tạo Cấu hình Mạng

Lớp `NetworkConfig` gom tất cả các tùy chọn mạng — cổng cơ sở, máy chủ và các thiết lập SSL tùy chọn — vào một đối tượng duy nhất mà công cụ tìm kiếm sử dụng.

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Tại sao**: Trung tâm hoá các tùy chọn này làm cho cấu hình có thể tái sử dụng và dễ bảo trì hơn trên nhiều nút.

#### Thêm Nút

`SearchNode` đại diện cho một nút riêng lẻ trong cụm GroupDocs.Search thực hiện một chức năng cụ thể như lập chỉ mục hoặc tìm kiếm. Tạo một `SearchNode` cho mỗi vai trò (indexer, searcher, extractor) và đăng ký nó với `SearchEngine`. Phân phối trách nhiệm trên các nút cải thiện tính song song và khả năng chịu lỗi.

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Tại sao**: Phân chia công việc trên các nút chuyên dụng giảm sự cạnh tranh và cho phép mỗi máy tập trung vào một nhiệm vụ duy nhất, tăng năng suất tổng thể.

#### Hoàn thiện Cấu hình

Sau khi thêm tất cả các nút, gọi `engine.start()` để khởi động mạng. Engine sẽ tự động gán mỗi nút vào cổng đã chỉ định và xác minh kết nối.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Các vấn đề thường gặp & Giải pháp

- **Xung đột Cổng** – Luôn tăng `basePort` cho mỗi nút mới. Kiểm tra các cổng mở bằng `netstat` hoặc công cụ giám sát mạng của hệ điều hành.  
- **Thiếu Thư mục** – Đảm bảo mọi thư mục (`Indexer0`, `Searcher0`, v.v.) tồn tại và tiến trình Java có quyền đọc/ghi.  
- **Khả năng tiếp cận Mạng** – Khi chuyển sang cấu hình đa máy, thay `127.0.0.1` bằng IP máy chủ thực tế và mở các cổng đã chọn trong tường lửa.  

## Ứng dụng Thực tiễn

| Kịch bản | Lợi ích của việc cấu hình base port groupdocs |
|----------|-----------------------------------------------|
| Quản lý tài liệu doanh nghiệp | Mở rộng liền mạch giữa các phòng ban mà không có thời gian chết |
| Nền tảng CMS lớn | Truy xuất nội dung nhanh hơn khi chỉ mục được phân phối |
| Quản lý vụ kiện pháp lý | Trích xuất PDF song song giảm độ trễ tìm kiếm |

## Các yếu tố về Hiệu năng

- **Giám sát CPU/Bộ nhớ** – Sử dụng JMX của Java hoặc công cụ profiling để theo dõi việc sử dụng luồng.  
- **Điều chỉnh Nén** – `Compression.High` tiết kiệm không gian đĩa nhưng có thể tăng tải CPU; thử cả `High` và `Normal` để tìm điểm cân bằng.  
- **Cập nhật thường xuyên** – Các bản phát hành mới của GroupDocs.Search thường bao gồm các bản vá hiệu năng; giữ thư viện luôn cập nhật.

## Kết luận

Bạn đã học cách **configure base port groupdocs** và thiết lập một mạng tìm kiếm đa‑nút bằng GroupDocs.Search cho Java. Hãy thử nghiệm với các nút bổ sung, tinh chỉnh các thiết lập chỉ mục và tích hợp mạng vào các ứng dụng hiện có để có một giải pháp tìm kiếm thực sự mở rộng.

## Câu hỏi thường gặp

**Hỏi: Mục đích của việc tắt stop words trong quá trình lập chỉ mục là gì?**  
**Đáp:** Tắt stop words có thể cải thiện độ chính xác tìm kiếm bằng cách giữ lại các từ phổ biến có thể quan trọng trong các lĩnh vực chuyên biệt.

**Hỏi: Làm thế nào để xử lý xung đột cổng khi thêm nhiều nút?**  
**Đáp:** Bắt đầu với một `basePort` cao (ví dụ 49100) và tăng dần cho mỗi nút tiếp theo, đảm bảo mỗi nút có một điểm cuối TCP duy nhất.

**Hỏi: Tôi có thể sử dụng cấu hình này cho các ứng dụng dựa trên đám mây không?**  
**Đáp:** Có—chỉ cần đảm bảo các cổng đã chọn được mở trong nhóm bảo mật đám mây và thay `127.0.0.1` bằng IP công cộng hoặc riêng phù hợp.

**Hỏi: Sự khác biệt giữa NormalIndex và các loại chỉ mục khác là gì?**  
**Đáp:** `NormalIndex` cung cấp cân bằng giữa tốc độ và việc sử dụng bộ nhớ, trong khi các chỉ mục chuyên biệt (ví dụ `FastIndex`) nhắm vào các kịch bản hiệu năng đặc thù.

**Hỏi: Có giới hạn số lượng nút tôi có thể thêm không?**  
**Đáp:** Về mặt kỹ thuật không có; giới hạn chỉ phụ thuộc vào tài nguyên phần cứng và băng thông mạng của bạn.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## Hướng dẫn liên quan

- [Cách cấu hình mạng tìm kiếm .NET bằng GroupDocs.Search và Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Cách triển khai mạng tìm kiếm với GroupDocs.Search trong .NET cho Hệ thống Quản lý Tài liệu](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Triển khai nút mạng tìm kiếm trong .NET sử dụng GroupDocs để Lập chỉ mục và Truy xuất Tài liệu Hiệu quả](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
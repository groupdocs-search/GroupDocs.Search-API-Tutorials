---
date: '2026-01-24'
description: Tìm hiểu cách cấu hình base port groupdocs cho các mạng tìm kiếm có khả
  năng mở rộng bằng cách sử dụng GroupDocs.Search Java, tối ưu tốc độ truy xuất và
  thiết lập hệ thống đa nút.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Cấu hình cổng cơ bản groupdocs trong Java Search Network
type: docs
url: /vi/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Cấu hình cổng cơ bản groupdocs trong Mạng Tìm kiếm Java

Trong các ứng dụng hiện đại, dữ liệu nặng, **cấu hình cổng cơ bản groupdocs** là bước nền tảng để xây dựng một hạ tầng tìm kiếm nhanh chóng và đáng tin cậy. Cho dù bạn đang xử lý hàng ngàn tệp PDF hay mở rộng trên nhiều máy chủ, việc thiết lập bảo mỗi chi tiết — từ các yêu cầu trước đột.
- **Có cần giấy phép không?** Có, cần giấy phép dùng thử hoặc đầy đủ cho môi trường sản xuất.
- **Phiên bản Java nào được hỗ trợ?** Java 8 hoặc cao hơn.
- **Có thể chạy trên máy chủ đám mây không?** Chắc chắn — chỉ cần đảm bảo các cổng được mở trong nhóm bảo mật của bạn.
- **Có thể thêm bao nhiêu nút?** Không có giới hạn cứng; thêm bao nhiêu tùy thuộc vào phần cứng và mạng của bạn.

## “Cấu hình cổng cơ bản groupdocs” là gì?
Khi bạn **cấu hình cổng cơ bản groupdocs**, bạn chỉ định một cổng TCP khởi đầu mà mỗi nút sẽ sử dụng (và tăng dần cho các nút tiếp theo). Bước đơn giản này loại bỏ các lỗi “cổng đã được sử dụng” đáng sợ và tạo nền tảng cho một cụm tìm kiếm mở rộng theo chiều ngang sạch sẽ.

## Tại sao sử dụng GroupDocs.Search cho một mạng có khả năng mở rộng?
- **Hiệu năng cao** – thuật toán lập chỉ mục và tìm kiếm được tối ưu.
- **Kiến trúc linh hoạt** – bạn có thể kết hợp các bộ lập chỉ mục, bộ tìm kiếm, shard và extractor trên các nút khác nhau.
- **Dễ tích hợp** – hoạt động với bất kỳ ứng dụng Java nào, trên máy chủ nội bộ hoặc đám mây.
- **Giấy phép mạnh mẽ** – các tùy chọn dùng thử cho phép bạn kiểm tra trước khi cam kết.

## Các yêu cầu trước
- **Java Development Kit (JDK)** 8 hoặc mới hơn.
- **IDE** như IntelliJ IDEA hoặc Eclipse.
- Thư viện **GroupDocs.Search for Java** (phiên bản 25.4 trở lên) được cài đặt qua Maven hoặc tải về thủ công.
- Kiến thức cơ bản về mạng (cổng TCP, localhost vs. máy chủ từ xa).

## Cài đặt GroupDocs.Search cho Java

### Hướng dẫn cài đặt

**Cài đặt Maven:**

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

**Tải trực tiếp:**

Ngoài ra, tải phiên bản mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Mua giấy phép

- **Dùng thử miễn phí** – bắt đầu kiểm tra ngay lập tức.
- **Giấy phép tạm thời** – nhận bản dùng thử mở rộng tại [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Mua bản đầy đủ** – bắt buộc cho các triển khai sản xuất.

### Khởi tạo và thiết lập cơ bản

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

### Cách cấu hình cổng cơ bản groupdocs

#### Thiết lập đường dẫn cơ bản

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Tại sao**: Cấu trúc thư mục nhất quán cho phép mỗi nút tìm thấy các tệp chỉ mục, shard hoặc extractor mà không gây nhầm lẫn.

#### Cấu hình cổng cơ bản

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Tại sao**: Bắt đầu từ một số cổng cao (ví dụ: 49100) sẽ giảm khả năng trùng với các dịch vụ phổ biến. Tăng cổng cho mỗi nút bổ sung.

#### Định nghĩa địa chỉ máy chủ

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Tại sao**: Sử dụng `localhost` là lý tưởng cho môi trường phát triển; thay thế bằng địa chỉ IP hoặc tên DNS của máy chủ khi đưa vào sản xuất.

#### Tạo cấu hình mạng

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

- **Tại sao**: Các tùy chọn này cân bằng tốc độ và hiệu quả lưu trữ, mang lại một chỉ mục tìm kiếm gọn nhẹ nhưng mạnh mẽ.

#### Thêm nút

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

- **Tại sao**: Phân chia trách nhiệm giữa các nút (lập chỉ mục vs. tìm kiếm, shard vs. extractor) cải thiện tính song song và khả năng chịu lỗi.

#### Hoàn thiện cấu hình

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Các vấn đề thường gặp & Giải pháp

- **Xung đột cổng** – Luôn tăng `basePort` cho mỗi nút mới. Kiểm tra bằng `netstat` hoặc công cụ giám sát cổng của hệ điều hành.
- **Thiếu thư mục** – Đảm bảo mọi thư mục được tham chiếu (`Indexer0`, `Searcher0`, …) tồn tại và quá trình Java có quyền đọc/ghi.
- **Khả năng tiếp cận mạng** – Khi chuyển sang môi trường đa máy, thay `127.0.0.1` bằng IP thực tế của máy chủ và mở các cổng đã chọn trong tường lửa.

## Ứng dụng thực tiễn

| Kịch bản | Lợi ích của việc cấu hình cổng cơ bản GroupDocs |
|----------|--------------------------------------------|
| Quản lý tài liệu doanh nghiệp | Mở rộng liền mạch giữa các phòng ban mà không gây downtime |
| Nền tảng CMS lớn | Truy xuất nội dung nhanh hơn nhờ chỉ mục được phân phối |
| Quản lý hồ sơ pháp lý | Trích xuất PDF song song giảm độ trễ tìm kiếm |

## Các cân nhắc về hiệu năng

- **Giám sát CPU/Bộ nhớ** – Sử dụng JMX của Java hoặc công cụ profiling để theo dõi việc sử dụng luồng.
- **Điều chỉnh nén** – `Compression.High` tiết kiệm không gian đĩa nhưng có thể tăng tải CPU; thử cả `High` và `Normal`.
- **Cập nhật thường xuyên** – Các bản phát hành mới của GroupDocs.Search thường bao gồm các bản vá hiệu năng.

## Kết luận

Bạn đã học cách **cấu hình cổng cơ bản groupdocs** và thiết lập một mạng tìm kiếm đa‑nút bằng GroupDocs.Search cho Java. Thử nghiệm với các nút bổ sung, tinh chỉnh cài đặt chỉ mục và tích hợp mạng vào các ứng dụng hiện có để có giải pháp tìm kiếm thực sự mở rộng.

## Câu hỏi thường gặp

**H: Mục đích của việc tắt stop words trong quá trình lập chỉ mục là gì?**  
Đ: Tắt stop words có thể cải thiện độ chính xác tìm kiếm bằng cách giữ lại các từ phổ biến có thể quan trọng trong các lĩnh vực chuyên biệt.

**H: Làm sao xử lý xung đột cổng khi thêm nhiều nút?**  
Đ: Bắt đầu với một `basePort` cao (ví dụ: 49100) và tăng dần cho mỗi nút tiếp theo, đảm bảo mỗi nút có một endpoint TCP duy nhất.

**H: Tôi có thể dùng cấu hình này cho các ứng dụng đám mây không?**  
Đ: Có — chỉ cần mở các cổng đã chọn trong nhóm bảo mật đám mây và thay `127.0.0.1` bằng IP công cộng hoặc riêng phù hợp.

**H: Sự khác biệt giữa NormalIndex và các loại chỉ mục khác là gì?**  
Đ: `NormalIndex` cung cấp sự cân bằng giữa tốc độ và việc sử dụng bộ nhớ, trong khi các chỉ mục chuyên biệt (ví dụ: `FastIndex`) nhắm vào các kịch bản hiệu năng đặc thù.

**H: Có giới hạn số lượng nút có thể thêm không?**  
Đ: Về mặt kỹ thuật không; giới hạn phụ thuộc vào tài nguyên phần cứng và băng thông mạng của bạn.

---

**Cập nhật lần cuối:** 2026-01-24  
**Đã kiểm tra với:** GroupDocs.Search Java 25.4  
**Tác giả:** GroupDocs
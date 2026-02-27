---
date: '2026-01-08'
description: Tìm hiểu cách cấu hình tìm kiếm và bật cập nhật tìm kiếm thời gian thực
  bằng GroupDocs.Search cho Java. Hướng dẫn từng bước về thiết lập mạng, triển khai
  nút và lập chỉ mục.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Cách cấu hình tìm kiếm với GroupDocs.Search trong Java - Hướng dẫn cấu hình
  và triển khai'
type: docs
url: /vi/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Cách tìm kiếm cấu hình GroupDocs.Search trong Java

Trong thế giới kỹ thuật số ngày này, **cách cấu hình tìm kiếm** hiệu quả có thể quyết định thành công hay thất bại của một dự án. Dù bạn đang xử lý hàng ngàn hợp đồng, bài báo nghiên cứu, hay báo cáo nội bộ, một mạng lưới tìm kiếm được thiết kế tốt cho phép bạn tìm thấy tài liệu đúng trong vài giây. Hướng dẫn này sẽ hướng dẫn bạn cấu hình mạng tìm kiếm, phát triển các nút và bật **cập nhật tìm kiếm thời gian thực** với GroupDocs.Search cho Java.

## Trả lời nhanh
- **Mục đích chính của tìm kiếm mạng mạng là gì?** Để phân phối công việc thiết lập chỉ mục và xử lý truy vấn trên nhiều nút nhằm tăng khả năng mở rộng và tốc độ.
- **Phiên bản thư viện nào được yêu cầu?**GroupDocs.SearchchoJavav25.4hoặc mới hơn.
- **Tôi có cần giấy phép không?**Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép thương mại được bắt buộc cho môi trường sản xuất.
- **Thời gian cập nhật được thực thi như thế nào?**Đăng ký nút sự kiện được kích hoạt khi thay đổi chỉ mục cài đặt.
- **Tôi có thể bổ sung thêm các tài liệu thư mục mới ngay lập tức không?**Có— sử dụng phương thức `addDirectories` của người lập chỉ mục.

## “Tìm kiếm cấu hình” trong ngữ cảnh GroupDocs là gì?
Cấu hình tìm kiếm có nghĩa là thiết lập một **tìm kiếm mạng** biết vị trí tài liệu của bạn, giao tiếp các nút tiếp theo và cách thiết lập chỉ mục được phân phối hợp lý. Khi mạng đã được cấu hình, bạn có thể thêm hoặc loại bỏ các nút mà không gây chết thời gian, đảm bảo truy cập liên tục vào kết quả tìm kiếm cập nhật.

## Tại sao nên sử dụng GroupDocs.Search cho Java?
- **Khả năng mở rộng:** Phân phối khối lượng công việc trên nhiều máy.
- **Thực hiện cập nhật thời gian:** Ngay lập tức phản ánh các tệp mới được thiết lập chỉ mục trên toàn mạng.
- **Dễ dàng tích hợp:** Cài đặt Maven đơn giản và API Java rõ ràng.
- **Sẵn sàng cho doanh nghiệp:** Xử lý dữ liệu lớn và các truy vấn phức tạp.

## Điều kiện tiên quyết
- **Bộ công cụ phát triển Java (JDK)8+** đã được cài đặt.
- **Maven** để quản lý phụ thuộc.
- Kiến trúc cơ bản về Java, Maven và các khái niệm tìm kiếm.

## Thiết lập GroupDocs.Tìm kiếm Java

### Phụ thuộc Maven
Thêm kho lưu trữ và phần phụ thuộc vào `pom.xml` của bạn:

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

**Tải trực tiếp:** Bạn cũng có thể lấy thư viện từ [GroupDocs.Search for Java Releases](https://releases.groupdocs.com/search/java/).

### Mua lại giấy phép
- **Bản dùng thử:** Đã nhận giấy phép dùng thử để khám phá tất cả các tính năng.
- **Giấy phép tạm thời:** Yêu cầu để kéo dài thời gian đánh giá dài.
- **Giấy phép thương mại:** Cần thiết cho phát triển khai sản xuất.

### Khởi tạo cơ bản
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Cách cấu hình tìm kiếm mạng trong Java

### Bước 1: Nhập các gói cần thiết
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Bước 2: Cấu hình Mạng
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Tham số:** `basePath` chỉ tới thư mục tài liệu của bạn; `basePort` là cổng TCP được sử dụng cho giao tiếp giữa các nút.

## Triển khai các Nút Mạng Tìm kiếm

### Bước 1: Nhập Gói Triển khai
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Bước 2: Triển khai các Nút
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Nút Master:** Điều phối tìm kiếm và lập chỉ mục trên tất cả các nút.

## Đăng ký nhận Sự kiện Nút để cập nhật tìm kiếm theo thời gian thực

### Bước 1: Nhập Gói Sự kiện
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Bước 2: Đăng ký nhận Sự kiện Nút Chính
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Xử lý sự kiện:** Cho phép **cập nhật tìm kiếm thời gian thực** mỗi khi tài liệu được thêm, cập nhật hoặc xóa.

## Thêm Thư mục để Lập chỉ mục

### Bước 1: Nhập Gói Lập chỉ mục
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Bước 2: Thêm Thư mục Tài liệu
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Lập chỉ mục động:** Thêm bao nhiêu thư mục tùy ý; mạng lưới sẽ tự động lập chỉ mục chúng.

## Truy xuất Tài liệu đã được Lập chỉ mục

### Bước 1: Nhập Gói Tìm kiếm
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Bước 2: Truy xuất Thông tin Tài liệu
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **Quản lý phân đoạn:** Xử lý hiệu quả các dữ liệu lớn bằng cách phân phối tài liệu qua các phân đoạn.

## Ứng dụng thực tế
1. **Quản lý tài sản doanh nghiệp:** Tập trung tìm kiếm trên hàng triệu tệp.
2. **Công pháp luật:** Nhanh chóng tìm thấy hồ sơ dịch vụ, hợp đồng và bằng chứng.
3. **Nghiên cứu học thuật:** Lập chỉ mục các tạp chí và bài báo để truy xuất ngay lập tức.

## Cân nhắc về hiệu suất
- **Mục ưu tiên cài đặt:** Lên lịch làm mới chỉ mục thường xuyên và xóa dữ liệu cũ.
- **Quản lý bộ nhớ:** Giám sát JVM heap, đặc biệt khi xử lý các phân đoạn lớn.
- **Mở rộng kế hoạch:** Thêm nút khi dữ liệu của bạn tăng lên; Tải xuống cân bằng mạng lưới.

## Các vấn đề thường gặp & Giải pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------|------|
| Các nút không thể kết nối | Cổng xung đột hoặc tường lửa | Đảm bảo `basePort` được mở và không có dịch vụ nào khác được sử dụng |
| Mục không được cập nhật | Missing sự kiện đăng ký | Gọi `SearchNetworkNodeEvents.subscribe(masterNode)` sau khi phát triển khai |
| Lỗi hết bộ nhớ | Quá nhiều phân đoạn được tải xuống | Phân đoạn kích thước nhỏ hoặc JVM heap tăng (cờ `-Xmx`) |

## Câu hỏi thường gặp

**H: Tôi có thể thêm thư mục mới sau khi mạng lưới đang chạy?**
Đ: Có—sử dụng phương thức `indexer.addDirectories()`; các sự kiện đã đăng ký sẽ truyền tải bản cập nhật theo thời gian thực.

**H: Làm thế nào tôi có thể giám sát nút trạng thái?**
Đ: Mỗi `SearchNetworkNode` cung cấp trạng thái API; hợp nhất với giám sát công cụ mà bạn chọn.

**H: Có thể chạy nút master trên máy chủ đặc biệt không?**
Đ: Chắc chắn. Chỉ cần đảm bảo tất cả các nút dùng chung `basePort` và có thể kết nối với nhau qua mạng.

**H: Những định dạng tệp nào được hỗ trợ?**
Đ: GroupDocs.Search hỗ trợ PDF, Word, Excel, PowerPoint, văn bản thuần và nhiều định dạng khác ngay từ đầu.

**H: Tôi cần khởi động lại mạng sau khi thêm nút mới không?**
Đ: Không—các nút có thể được thêm hoặc loại bỏ một cách động; nút master sẽ tự động cân bằng lại các phân đoạn.

## Phần kết luận
Bạn đã hiểu đầy đủ từng bước về **cách tìm kiếm cấu hình** bằng GroupDocs.Search cho Java, từ cài đặt ban đầu đến bản cập nhật thời gian thực và cài đặt phân mục chỉ mục. Áp dụng các mẫu này để xây dựng các giải pháp tìm kiếm tài liệu nhanh chóng, mở rộng và đáng tin cậy cho bất kỳ chuyên ngành nào.

---

**Cập nhật lần cuối:** 2026-01-08
**Kiểm tra với:** GroupDocs.Search for Java25.4
**Tác giả:** GroupDocs
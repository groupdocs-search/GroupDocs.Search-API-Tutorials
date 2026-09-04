---
date: '2026-05-02'
description: Tìm hiểu cách cấu hình tìm kiếm và bật cập nhật tìm kiếm thời gian thực
  bằng GroupDocs.Search cho Java. Hướng dẫn từng bước về thiết lập mạng, triển khai
  nút và lập chỉ mục.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: Cách cấu hình tìm kiếm với GroupDocs.Search trong Java - Hướng dẫn cấu hình
  và triển khai
type: docs
url: /vi/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Cách cấu hình tìm kiếm với GroupDocs.Search trong Java

Trong thế giới kỹ thuật số ngày nay, **cách cấu hình tìm kiếm** một cách hiệu quả có thể quyết định thành công hay thất bại của dự án. Dù bạn đang xử lý hàng ngàn hợp đồng, bài báo nghiên cứu hay báo cáo nội bộ, một mạng tìm kiếm được thiết kế tốt cho phép bạn tìm đúng tài liệu trong vài giây. Hướng dẫn này sẽ đưa bạn qua quá trình cấu hình mạng tìm kiếm, triển khai các nút và bật **cập nhật tìm kiếm thời gian thực** với GroupDocs.Search cho Java.

## Câu trả lời nhanh
- **Mục đích chính của mạng tìm kiếm là gì?** Để phân phối việc lập chỉ mục và xử lý truy vấn trên nhiều nút nhằm tăng khả năng mở rộng và tốc độ.  
- **Phiên bản thư viện nào được yêu cầu?** GroupDocs.Search for Java v25.4 hoặc mới hơn.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Cập nhật thời gian thực được xử lý như thế nào?** Bằng cách đăng ký các sự kiện nút xảy ra khi có thay đổi lập chỉ mục.  
- **Tôi có thể thêm thư mục tài liệu mới ngay lập tức không?** Có — sử dụng phương thức `addDirectories` của indexer.

## “cách cấu hình tìm kiếm” là gì trong ngữ cảnh GroupDocs?
Cấu hình tìm kiếm có nghĩa là thiết lập một **mạng tìm kiếm** biết vị trí tài liệu của bạn, cách các nút giao tiếp và cách lập chỉ mục được phối hợp. Khi mạng đã được cấu hình, bạn có thể thêm hoặc loại bỏ các nút mà không gây downtime, đảm bảo truy cập liên tục tới kết quả tìm kiếm luôn cập nhật.

## Tại sao nên sử dụng GroupDocs.Search cho Java?
- **Scalability:** Phân phối tải công việc trên nhiều máy.  
- **Real‑time updates:** Ngay lập tức phản ánh các tệp mới được lập chỉ mục trên toàn mạng.  
- **Ease of integration:** Cài đặt Maven đơn giản và API Java rõ ràng.  
- **Enterprise‑ready:** Xử lý tập dữ liệu lớn và các kịch bản truy vấn phức tạp.

## Yêu cầu trước
- **Java Development Kit (JDK) 8+** đã được cài đặt.  
- **Maven** để quản lý phụ thuộc.  
- Hiểu biết cơ bản về Java, Maven và các khái niệm tìm kiếm.  

## Cài đặt GroupDocs.Search cho Java

### Phụ thuộc Maven
Thêm repository và phụ thuộc vào file `pom.xml` của bạn:

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

**Direct Download:** Bạn cũng có thể lấy thư viện từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Mua giấy phép
- **Free Trial:** Nhận giấy phép dùng thử để khám phá tất cả các tính năng.  
- **Temporary License:** Yêu cầu để kéo dài thời gian đánh giá.  
- **Commercial License:** Cần thiết cho các triển khai sản xuất.

### Khởi tạo cơ bản
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Cách cấu hình mạng tìm kiếm trong Java

### Bước 1: Nhập các gói cần thiết
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Bước 2: Cấu hình mạng
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Parameters:** `basePath` chỉ tới thư mục tài liệu của bạn; `basePort` là cổng TCP dùng cho giao tiếp giữa các nút.

## Triển khai các nút mạng tìm kiếm

### Bước 1: Nhập gói triển khai
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Bước 2: Triển khai các nút
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Master Node:** Điều phối tìm kiếm và lập chỉ mục trên tất cả các nút. Bạn có thể **configure master node** các thiết lập như phân bổ shard và kiểm tra sức khỏe.

## Đăng ký sự kiện nút để cập nhật tìm kiếm thời gian thực

### Bước 1: Nhập gói sự kiện
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Bước 2: Đăng ký sự kiện nút chính
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Event Handling:** Cho phép **cập nhật tìm kiếm thời gian thực** mỗi khi tài liệu được thêm, cập nhật hoặc xóa.

## Thêm thư mục để lập chỉ mục

### Bước 1: Nhập gói Indexer
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Bước 2: Thêm thư mục tài liệu
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Dynamic Indexing:** Sử dụng phương thức `addDirectories` để **add directories to index** ngay lập tức mà không cần khởi động lại mạng.

## Lấy tài liệu đã lập chỉ mục

### Bước 1: Nhập gói Searcher
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Bước 2: Lấy thông tin tài liệu
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
- **Shard Management:** Xử lý hiệu quả các bộ dữ liệu lớn bằng cách phân phối tài liệu qua các shard. Để **optimize shard size**, theo dõi thống kê shard và điều chỉnh cấu hình `shardSize` trong các phiên bản tương lai.

## Tại sao điều này quan trọng đối với dự án của bạn
Một mạng tìm kiếm được cấu hình đúng loại bỏ các nút thắt cổ chai, giảm độ trễ và đảm bảo người dùng luôn thấy phiên bản tài liệu mới nhất. Các cập nhật thời gian thực và khả năng **add directories to index** mà không cần downtime đặc biệt hữu ích cho các công ty luật, viện nghiên cứu và bất kỳ tổ chức nào làm việc với bộ sưu tập tài liệu luôn thay đổi.

## Ứng dụng thực tiễn
1. **Enterprise Document Management:** Tập trung tìm kiếm trên hàng triệu tệp.  
2. **Legal Firms:** Nhanh chóng tìm kiếm hồ sơ vụ án, hợp đồng và bằng chứng.  
3. **Academic Research:** Lập chỉ mục các tạp chí và bài báo để truy xuất ngay lập tức.

## Các yếu tố cần cân nhắc về hiệu năng
- **Optimize Indexing:** Lên lịch làm mới chỉ mục thường xuyên và xóa dữ liệu cũ.  
- **Memory Management:** Giám sát heap JVM, đặc biệt khi xử lý các shard lớn.  
- **Scalability Planning:** Thêm nút khi tập dữ liệu tăng; mạng tự động cân bằng tải.  
- **Optimize shard size:** Shard nhỏ hơn cải thiện độ trễ truy vấn, trong khi shard lớn hơn giảm chi phí quản lý. Điều chỉnh dựa trên phần cứng và mẫu truy vấn của bạn.

## Các vấn đề thường gặp & Giải pháp
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| Các nút không thể kết nối | Xung đột cổng hoặc tường lửa | Đảm bảo `basePort` được mở và không bị dịch vụ khác sử dụng |
| Chỉ mục không được cập nhật | Thiếu đăng ký sự kiện | Gọi `SearchNetworkNodeEvents.subscribe(masterNode)` sau khi triển khai |
| Lỗi hết bộ nhớ | Quá nhiều shard lớn được tải | Giảm kích thước shard hoặc tăng bộ nhớ heap JVM (`-Xmx` flag) |

## Câu hỏi thường gặp

**Q: Tôi có thể thêm thư mục mới sau khi mạng đang chạy không?**  
A: Có — sử dụng phương thức `indexer.addDirectories()`; các sự kiện đã đăng ký sẽ truyền các cập nhật theo thời gian thực.

**Q: Làm sao để giám sát sức khỏe của nút?**  
A: Mỗi `SearchNetworkNode` cung cấp API trạng thái; tích hợp với công cụ giám sát bạn lựa chọn.

**Q: Có thể chạy nút chính trên máy riêng biệt không?**  
A: Hoàn toàn có thể. Chỉ cần đảm bảo mọi nút cùng sử dụng `basePort` và có thể kết nối với nhau qua mạng.

**Q: Những định dạng tệp nào được hỗ trợ?**  
A: GroupDocs.Search hỗ trợ PDF, Word, Excel, PowerPoint, văn bản thuần và nhiều định dạng khác ngay từ đầu.

**Q: Tôi có cần khởi động lại mạng sau khi thêm nút mới không?**  
A: Không — các nút có thể được thêm hoặc loại bỏ một cách động; nút chính sẽ tự động cân bằng lại các shard.

## Kết luận
Bây giờ bạn đã biết **cách cấu hình tìm kiếm** bằng GroupDocs.Search cho Java, bạn có thể xây dựng các giải pháp tìm kiếm tài liệu nhanh, mở rộng và đáng tin cậy, đáp ứng tốc độ phát triển của tổ chức. Áp dụng các mẫu này để tạo trải nghiệm tìm kiếm phân tán thời gian thực cho bất kỳ ngành nào.

---

**Cập nhật lần cuối:** 2026-05-02  
**Đã kiểm tra với:** GroupDocs.Search for Java 25.4  
**Tác giả:** GroupDocs
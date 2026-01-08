---
date: '2026-01-08'
description: Tìm hiểu cách cấu hình tìm kiếm và bật cập nhật tìm kiếm thời gian thực
  bằng GroupDocs.Search cho Java. Hướng dẫn từng bước về thiết lập mạng, triển khai
  nút và lập chỉ mục.
keywords:
- GroupDocs.Search for Java
- configure search network in Java
- deploying nodes in search network
title: 'Cách cấu hình tìm kiếm với GroupDocs.Search trong Java: Hướng dẫn cấu hình
  và triển khai'
type: docs
url: /vi/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Cách cấu hình tìm kiếm với GroupDocs.Search trong Java

Trong thế giới kỹ thuật số ngày nay, **cách cấu hình tìm kiếm** hiệu quả có thể quyết định thành công hay thất bại của một dự án. Dù bạn đang xử lý hàng ngàn hợp đồng, bài báo nghiên cứu, hay báo cáo nội bộ, một mạng lưới tìm kiếm được thiết kế tốt cho phép bạn tìm đúng tài liệu trong vài giây. Hướng dẫn này sẽ hướng dẫn bạn cấu hình mạng lưới tìm kiếm, triển khai các nút, và bật **cập nhật tìm kiếm thời gian thực** với GroupDocs.Search cho Java.

## Quick Answers
- **Mục đích chính của một mạng lưới tìm kiếm là gì?** Để phân phối việc lập chỉ mục và xử lý truy vấn trên nhiều nút nhằm tăng khả năng mở rộng và tốc độ.  
- **Phiên bản thư viện nào được yêu cầu?** GroupDocs.Search cho Java v25.4 hoặc mới hơn.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép thương mại là bắt buộc cho môi trường sản xuất.  
- **Cập nhật thời gian thực được xử lý như thế nào?** Bằng cách đăng ký các sự kiện nút được kích hoạt khi có thay đổi lập chỉ mục.  
- **Tôi có thể thêm các thư mục tài liệu mới ngay lập tức không?** Có—sử dụng phương thức `addDirectories` của indexer.

## “Cách cấu hình tìm kiếm” trong ngữ cảnh GroupDocs là gì?
Cấu hình tìm kiếm có nghĩa là thiết lập một **mạng lưới tìm kiếm** biết vị trí tài liệu của bạn, cách các nút giao tiếp, và cách lập chỉ mục được phối hợp. Khi mạng lưới đã được cấu hình, bạn có thể thêm hoặc loại bỏ các nút mà không gây thời gian chết, đảm bảo truy cập liên tục vào kết quả tìm kiếm luôn cập nhật.

## Why use GroupDocs.Search for Java?
- **Khả năng mở rộng:** Phân phối khối lượng công việc trên nhiều máy.  
- **Cập nhật thời gian thực:** Ngay lập tức phản ánh các tệp mới được lập chỉ mục trên toàn mạng.  
- **Dễ dàng tích hợp:** Cài đặt Maven đơn giản và API Java rõ ràng.  
- **Sẵn sàng cho doanh nghiệp:** Xử lý tập dữ liệu lớn và các kịch bản truy vấn phức tạp.

## Prerequisites
- **Java Development Kit (JDK) 8+** đã được cài đặt.  
- **Maven** để quản lý phụ thuộc.  
- Kiến thức cơ bản về Java, Maven và các khái niệm tìm kiếm.  

## Setting Up GroupDocs.Search for Java

### Maven Dependency
Add the repository and dependency to your `pom.xml`:

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

**Tải trực tiếp:** Bạn cũng có thể lấy thư viện từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Bản dùng thử:** Nhận giấy phép dùng thử để khám phá tất cả các tính năng.  
- **Giấy phép tạm thời:** Yêu cầu để kéo dài thời gian đánh giá.  
- **Giấy phép thương mại:** Cần thiết cho triển khai sản xuất.

### Basic Initialization
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Cách cấu hình mạng lưới tìm kiếm trong Java

### Step 1: Import Required Packages
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### Step 2: Configure the Network
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **Tham số:** `basePath` chỉ tới thư mục tài liệu của bạn; `basePort` là cổng TCP được sử dụng cho giao tiếp giữa các nút.

## Deploying Search Network Nodes

### Step 1: Import Deployment Package
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### Step 2: Deploy Nodes
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **Nút Master:** Điều phối tìm kiếm và lập chỉ mục trên tất cả các nút.

## Subscribing to Node Events for Real Time Search Updates

### Step 1: Import Event Package
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### Step 2: Subscribe to Master Node Events
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **Xử lý sự kiện:** Cho phép **cập nhật tìm kiếm thời gian thực** mỗi khi tài liệu được thêm, cập nhật hoặc xóa.

## Adding Directories for Indexing

### Step 1: Import Indexer Package
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### Step 2: Add Document Directories
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **Lập chỉ mục động:** Thêm bao nhiêu thư mục tùy ý; mạng lưới sẽ tự động lập chỉ mục chúng.

## Retrieving Indexed Documents

### Step 1: Import Searcher Package
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### Step 2: Retrieve Document Information
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
- **Quản lý shard:** Xử lý hiệu quả các tập dữ liệu lớn bằng cách phân phối tài liệu qua các shard.

## Practical Applications
1. **Quản lý tài liệu doanh nghiệp:** Tập trung tìm kiếm trên hàng triệu tệp.  
2. **Công ty luật:** Nhanh chóng tìm thấy hồ sơ vụ án, hợp đồng và bằng chứng.  
3. **Nghiên cứu học thuật:** Lập chỉ mục các tạp chí và bài báo để truy xuất ngay lập tức.

## Performance Considerations
- **Tối ưu hoá lập chỉ mục:** Lên lịch làm mới chỉ mục thường xuyên và xóa dữ liệu cũ.  
- **Quản lý bộ nhớ:** Giám sát heap JVM, đặc biệt khi xử lý các shard lớn.  
- **Kế hoạch mở rộng:** Thêm nút khi tập dữ liệu của bạn tăng; mạng lưới tự cân bằng tải.

## Common Issues & Solutions
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------|-----|
| Các nút không thể kết nối | Xung đột cổng hoặc tường lửa | Đảm bảo `basePort` được mở và không bị dịch vụ khác sử dụng |
| Chỉ mục không cập nhật | Thiếu đăng ký sự kiện | Gọi `SearchNetworkNodeEvents.subscribe(masterNode)` sau khi triển khai |
| Lỗi hết bộ nhớ | Quá nhiều shard lớn được tải | Giảm kích thước shard hoặc tăng heap JVM (`-Xmx` flag) |

## Frequently Asked Questions

**H: Tôi có thể thêm thư mục mới sau khi mạng lưới đang chạy không?**  
Đ: Có—sử dụng phương thức `indexer.addDirectories()`; các sự kiện đã đăng ký sẽ truyền cập nhật theo thời gian thực.

**H: Làm thế nào tôi có thể giám sát tình trạng nút?**  
Đ: Mỗi `SearchNetworkNode` cung cấp API trạng thái; tích hợp với công cụ giám sát bạn chọn.

**H: Có thể chạy nút master trên máy riêng biệt không?**  
Đ: Chắc chắn. Chỉ cần đảm bảo tất cả các nút dùng cùng `basePort` và có thể kết nối với nhau qua mạng.

**H: Những định dạng tệp nào được hỗ trợ?**  
Đ: GroupDocs.Search hỗ trợ PDF, Word, Excel, PowerPoint, văn bản thuần và nhiều định dạng khác ngay từ đầu.

**H: Tôi có cần khởi động lại mạng lưới sau khi thêm nút mới không?**  
Đ: Không—các nút có thể được thêm hoặc loại bỏ một cách động; nút master sẽ tự động cân bằng lại các shard.

## Conclusion
Bạn đã có hiểu biết đầy đủ, từng bước về **cách cấu hình tìm kiếm** bằng GroupDocs.Search cho Java, từ cài đặt ban đầu đến cập nhật thời gian thực và lập chỉ mục phân tán. Áp dụng các mẫu này để xây dựng các giải pháp tìm kiếm tài liệu nhanh, mở rộng và đáng tin cậy cho bất kỳ ngành nào.

---

**Cập nhật lần cuối:** 2026-01-08  
**Kiểm tra với:** GroupDocs.Search for Java 25.4  
**Tác giả:** GroupDocs
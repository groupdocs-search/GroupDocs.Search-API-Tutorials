---
date: '2025-12-26'
description: Học cách tạo chỉ mục tìm kiếm Java với GroupDocs.Search cho Java, thêm
  tệp để tìm kiếm và thêm thư mục vào node.
keywords:
- GroupDocs.Search for Java
- deploy GroupDocs.Search
- Java search network setup
title: Tạo chỉ mục tìm kiếm Java – Triển khai GroupDocs.Search cho Java
type: docs
url: /vi/java/getting-started/deploy-groupdocs-search-java-setup-guide/
weight: 1
---

# Tạo Chỉ mục Tìm kiếm Java – Triển khai GroupDocs.Search cho Java

Trong thế giới dựa trên dữ liệu ngày nay, các ứng dụng **creating a searchable index java** cần xử lý các bộ sưu tập tài liệu khổng lồ một cách hiệu quả. Dù bạn đang xây dựng một dịch vụ tìm kiếm cấp doanh nghiệp hay một dự án nhỏ hơn, một mạng lưới tìm kiếm được cấu hình tốt có thể cải thiện đáng kể tốc độ truy xuất và độ liên quan. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quá trình thiết lập **GroupDocs.Search cho Java**, từ việc thêm tệp để tìm kiếm đến việc thêm thư mục vào node, để bạn có thể bắt đầu lập chỉ mục tài liệu ngay lập tức.

## Câu trả lời nhanh
- **Mục đích chính của GroupDocs.Search là gì?** Nó cung cấp một engine có khả năng mở rộng, dựa trên Java, để lập chỉ mục và tìm kiếm tài liệu trên một mạng lưới phân tán.  
- **Tôi nên sử dụng phiên bản nào?** Phiên bản ổn định mới nhất (ví dụ: 25.4) được khuyến nghị cho các dự án mới.  
- **Tôi có cần giấy phép không?** Một bản dùng thử miễn phí 30 ngày có sẵn; giấy phép vĩnh viễn là bắt buộc cho việc sử dụng trong môi trường sản xuất.  
- **Tôi có thể thêm cả tệp và toàn bộ thư mục không?** Có – sử dụng các hàm trợ giúp `addFiles` và `addDirectories` để nhập nội dung.  
- **Yêu cầu phiên bản Java nào?** Java 8 hoặc cao hơn, cùng Maven để quản lý phụ thuộc.

## “create searchable index java” là gì?
Việc tạo một chỉ mục tìm kiếm trong Java có nghĩa là xây dựng một cấu trúc dữ liệu ánh xạ các thuật ngữ tới các tài liệu chứa chúng, cho phép truy vấn toàn văn nhanh chóng. GroupDocs.Search trừu tượng hoá các công việc nặng, cho phép bạn tập trung vào việc cung cấp tài liệu và tinh chỉnh hành vi tìm kiếm.

## Tại sao nên sử dụng GroupDocs.Search cho Java?
- **Kiến trúc mạng có khả năng mở rộng** – Triển khai nhiều node chia sẻ khối lượng công việc lập chỉ mục.  
- **Hỗ trợ đa dạng định dạng tài liệu** – PDF, Word, Excel, PowerPoint, hình ảnh và hơn nữa.  
- **Cập nhật dựa trên sự kiện** – Đăng ký các sự kiện node để giữ chỉ mục luôn mới theo thời gian thực.  
- **Tích hợp Maven đơn giản** – Thêm vài dòng vào `pom.xml` và bắt đầu lập chỉ mục.

## Yêu cầu trước
- **JDK 8+** được cài đặt trên máy phát triển của bạn.  
- Một IDE như **IntelliJ IDEA** hoặc **Eclipse**.  
- Kiến thức cơ bản về **Java** và **Maven**.  
- Truy cập vào thư viện **GroupDocs.Search cho Java** (tải xuống hoặc Maven).

## Cài đặt GroupDocs.Search cho Java

### Phụ thuộc Maven
Thêm kho và phụ thuộc vào `pom.xml` của bạn:

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

> **Mẹo chuyên nghiệp:** Giữ phiên bản luôn cập nhật bằng cách kiểm tra trang phát hành chính thức.

Bạn cũng có thể tải JAR trực tiếp từ trang chính thức: [phiên bản GroupDocs.Search cho Java](https://releases.groupdocs.com/search/java/).

### Đăng ký giấy phép
- **Dùng thử miễn phí:** Đánh giá 30 ngày.  
- **Giấy phép tạm thời:** Yêu cầu để kéo dài thời gian thử nghiệm.  
- **Mua bản quyền:** Yêu cầu cho triển khai trong môi trường sản xuất.

### Khởi tạo cơ bản
Tạo một đối tượng cấu hình trỏ tới thư mục nơi các tệp chỉ mục sẽ được lưu và định nghĩa cổng giao tiếp cơ bản:

```java
import com.groupdocs.search.Configuration;

class InitializeSearch {
    public static void main(String[] args) {
        String basePath = "your/base/path";
        int basePort = 8080;
        
        Configuration config = new ConfiguringSearchNetwork().configure(basePath, basePort);
        // Use this configuration for subsequent operations
    }
}
```

## Cách tạo searchable index java với GroupDocs.Search?

Dưới đây chúng tôi sẽ phân tích các tính năng cốt lõi mà bạn cần để **thêm tệp để tìm kiếm** và **thêm thư mục vào node**, đồng thời triển khai một mạng lưới có khả năng mở rộng.

### Tính năng 1 – Cấu hình và Thiết lập Mạng
Cấu hình mạng tìm kiếm là bước đầu tiên hướng tới việc xây dựng một chỉ mục tìm kiếm.

```java
import com.groupdocs.search.Configuration;
import com.groupdocs.search.scaling.*;

class ConfiguringSearchNetwork {
    public static Configuration configure(String basePath, int basePort) {
        // Configure the search network with specified base path and port
        return new Configuration(basePath, basePort);
    }
}
```

- `basePath` – Thư mục nơi dữ liệu chỉ mục sẽ được lưu trữ.  
- `basePort` – Cổng khởi đầu; mỗi node sẽ tăng từ giá trị này.

### Tính năng 2 – Triển khai các Node Mạng Tìm kiếm
Triển khai các node phân phối khối lượng công việc lập chỉ mục trên nhiều máy hoặc quy trình.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkDeployment {
    public static SearchNetworkNode[] deploy(String basePath, int basePort, Configuration configuration) {
        // Deploy nodes based on the provided configuration
        return new SearchNetworkNode[]{new SearchNetworkNode()};
    }
}
```

Mỗi `SearchNetworkNode` chạy dịch vụ lập chỉ mục riêng, cho phép bạn **create a searchable index java** mở rộng theo chiều ngang.

### Tính năng 3 – Đăng ký các Sự kiện Node
Cập nhật thời gian thực giữ cho chỉ mục đồng bộ với các thay đổi của hệ thống tệp.

```java
import com.groupdocs.search.scaling.*;

class SearchNetworkNodeEvents {
    public static void subscribe(SearchNetworkNode node) {
        // Logic to subscribe to the specified node's events
    }
}
```

Bằng cách lắng nghe các sự kiện, bạn có thể tự động kích hoạt việc lập chỉ mục lại khi có tệp mới xuất hiện.

### Tính năng 4 – Thêm Thư mục vào Node Mạng
Sử dụng trợ giúp này để **add directories to node**, thu thập đệ quy tất cả các tài liệu được hỗ trợ.

```java
import java.io.File;
import java.util.ArrayList;

class DirectoryAdder {
    public static void addDirectories(SearchNetworkNode node, String... directoryPaths) {
        ArrayList<String> files = new ArrayList<>();
        for (String directoryPath : directoryPaths) {
            final File folder = new File(directoryPath);
            listFiles(folder, files);
        }
        addFiles(node, files.toArray(new String[0]));
    }

    private static void listFiles(final File folder, ArrayList<String> list) {
        for (final File fileEntry : folder.listFiles()) {
            if (fileEntry.isDirectory()) {
                listFiles(fileEntry, list);
            } else {
                list.add(fileEntry.getPath());
            }
        }
    }
}
```

### Tính năng 5 – Thêm Tệp vào Node Mạng
Khi bạn cần kiểm soát chi tiết, **add files to search** từng tệp một:

```java
import com.groupdocs.search.Document;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Date;
import org.apache.commons.io.FilenameUtils;
import com.groupdocs.search.Indexer;
import com.groupdocs.search.options.*;

class FileAdder {
    public static void addFiles(SearchNetworkNode node, String... filePaths) {
        try {
            InputStream[] streams = new FileInputStream[filePaths.length];
            Document[] documents = new Document[filePaths.length];
            for (int i = 0; i < filePaths.length; i++) {
                String filePath = filePaths[i];
                InputStream stream = new FileInputStream(filePath);
                streams[i] = stream;
                
                // Create a document from the input stream
                String fileName = FilenameUtils.getName(filePath);
                String extension = "." + FilenameUtils.getExtension(filePath);
                Document document = Document.createFromStream(
                    fileName,
                    new Date(),
                    extension,
                    stream);
                documents[i] = document;
            }

            // Initialize the indexer and configure options
            Indexer indexer = node.getIndexer();
            IndexingOptions options = new IndexingOptions();
            options.setUseRawTextExtraction(false);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

Phương pháp này cung cấp cho bạn tính linh hoạt để lập chỉ mục các tệp đến từ luồng, lưu trữ đám mây hoặc vị trí tạm thời.

## Các vấn đề thường gặp & Giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|------------|----------|
| **Không có tài liệu nào xuất hiện trong kết quả tìm kiếm** | Chỉ mục chưa được commit | Gọi `node.getIndexer().commit()` sau khi thêm tệp. |
| **Lỗi xung đột cổng** | Dịch vụ khác đang sử dụng `basePort` | Chọn một `basePort` khác hoặc kiểm tra các cổng còn trống. |
| **Định dạng tệp không được hỗ trợ** | Thư viện thiếu bộ phân tích | Đảm bảo phần mở rộng tệp được hỗ trợ hoặc thêm bộ trích xuất tùy chỉnh. |

## Câu hỏi thường gặp

**Hỏi: Tôi có thể sử dụng GroupDocs.Search trên một ứng dụng Java dựa trên đám mây không?**  
**Đáp:** Có. Thư viện hoạt động với bất kỳ môi trường Java nào, và bạn có thể chỉ định `basePath` tới một thư mục được gắn mạng hoặc lưu trữ đám mây được gắn cục bộ.

**Hỏi: Làm thế nào để cập nhật chỉ mục khi một tệp thay đổi?**  
**Đáp:** Đăng ký các sự kiện node (xem Tính năng 3) và gọi lại `addFiles` hoặc `addDirectories` cho các đường dẫn đã sửa đổi.

**Hỏi: Có giới hạn số lượng node tôi có thể triển khai không?**  
**Đáp:** Thực tế, giới hạn được xác định bởi phần cứng và băng thông mạng của bạn. API không áp đặt bất kỳ giới hạn cứng nào.

**Hỏi: Tôi có cần khởi động lại các node sau khi thêm tệp mới không?**  
**Đáp:** Không. Việc thêm tệp sẽ tự động kích hoạt quá trình lập chỉ mục; bạn chỉ cần commit nếu hoãn thao tác.

**Hỏi: Những định dạng tài liệu nào được hỗ trợ ngay lập tức?**  
**Đáp:** PDFs, DOC/DOCX, XLS/XLSX, PPT/PPTX, TXT, HTML và nhiều loại hình ảnh. Xem tài liệu chính thức để biết danh sách đầy đủ.

---

**Cập nhật lần cuối:** 2025-12-26  
**Đã kiểm tra với:** GroupDocs.Search cho Java 25.4  
**Tác giả:** GroupDocs
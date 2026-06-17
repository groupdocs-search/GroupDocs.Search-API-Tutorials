---
date: '2026-02-24'
description: Tìm hiểu cách tạo logger tùy chỉnh, đặt kích thước log tối đa và cấu
  hình logger console hoặc file trong GroupDocs.Search cho Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Cách tạo logger tùy chỉnh và giới hạn kích thước tệp log với GroupDocs.Search
  Java
type: docs
url: /vi/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Giới hạn kích thước tệp log với Trình ghi Log của GroupDocs.Search Java

Trong hướng dẫn này, bạn sẽ **tạo các triển khai logger tùy chỉnh** và học cách **giới hạn kích thước tệp log** khi sử dụng GroupDocs.Search cho Java. Kiểm soát sự tăng trưởng của log là rất quan trọng đối với việc lập chỉ mục tài liệu quy mô lớn, và các logger tích hợp sẵn cho phép bạn **đặt kích thước log tối đa**, **quay lại log file**, hoặc chuyển sang **sử dụng console logger** để nhận phản hồi ngay lập tức. Hãy cùng đi qua toàn bộ quá trình thiết lập, từ cấu hình Maven đến chạy truy vấn tìm kiếm, và xem cách **thêm tài liệu vào chỉ mục** với logger đã được cấu hình.

## Câu trả lời nhanh
- **What does “limit log file size” mean?** Nó giới hạn kích thước tối đa của tệp log, ngăn chặn việc tăng trưởng không kiểm soát trên đĩa.  
- **Which logger lets you limit log file size?** Logger tích hợp `FileLogger` chấp nhận tham số kích thước tối đa.  
- **How do I use console logger java?** Tạo một thể hiện của `ConsoleLogger` và đặt nó vào `IndexSettings`.  
- **Do I need a license for GroupDocs.Search?** Bản dùng thử đủ cho việc đánh giá; cần giấy phép thương mại cho môi trường sản xuất.  
- **What’s the first step?** Thêm phụ thuộc GroupDocs.Search vào dự án Maven của bạn.  

## Giới hạn kích thước tệp log là gì?
Giới hạn kích thước tệp log có nghĩa là cấu hình logger sao cho khi tệp đạt đến ngưỡng đã định (ví dụ, 4 MB), nó sẽ ngừng tăng kích thước hoặc quay lại (roll over). Điều này giúp dung lượng lưu trữ của ứng dụng dự đoán được và tránh suy giảm hiệu năng.

## Tại sao sử dụng logger file và tùy chỉnh với GroupDocs.Search?
- **Auditability:** Giữ bản ghi vĩnh viễn về các sự kiện lập chỉ mục và tìm kiếm.  
- **Debugging:** Nhanh chóng xác định vấn đề bằng cách xem lại các log ngắn gọn.  
- **Flexibility:** Lựa chọn giữa log file bền vững và đầu ra console ngay lập tức (`use console logger`).  

## Yêu cầu trước
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 hoặc mới hơn, IDE (IntelliJ IDEA, Eclipse, v.v.).  
- Kiến thức cơ bản về Java và Maven.  

## Cài đặt GroupDocs.Search cho Java

Thêm thư viện vào dự án của bạn bằng một trong các phương pháp dưới đây.

**Cấu hình Maven:**

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
Tải JAR mới nhất từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Nhận bản dùng thử hoặc mua giấy phép qua [trang cấp phép](https://purchase.groupdocs.com/temporary-license/).

## Cách tạo logger tùy chỉnh cho GroupDocs.Search
GroupDocs.Search cho phép bạn gắn bất kỳ triển khai nào của giao diện `ILogger`. Bằng cách mở rộng `FileLogger` hoặc `ConsoleLogger`, bạn có thể thêm hành vi bổ sung—như quay lại (roll over) tệp log hoặc chuyển tiếp tin nhắn tới dịch vụ giám sát từ xa. Sự linh hoạt này là lý do nhiều nhóm **tạo logger tùy chỉnh** để đáp ứng nhu cầu vận hành của họ.

## Cách giới hạn kích thước tệp log bằng File Logger
Dưới đây là hướng dẫn từng bước cho thấy cách **cấu hình file logger** để tệp log không bao giờ vượt quá kích thước bạn chỉ định.

### 1️⃣ Nhập các gói cần thiết
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Thiết lập Index Settings với File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ Tạo hoặc tải Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Thêm tài liệu vào Index
```java
index.add(documentsFolder);
```

### 5️⃣ Thực hiện truy vấn tìm kiếm
```java
SearchResult result = index.search(query);
```

**Điểm chính:** Tham số thứ hai của hàm khởi tạo `FileLogger` (`4.0`) xác định **set max log size** tính bằng megabyte, trực tiếp đáp ứng yêu cầu **giới hạn kích thước tệp log**.

## Cách sử dụng console logger java
Nếu bạn muốn phản hồi ngay lập tức trong terminal, hãy thay logger file bằng console logger.

### 1️⃣ Nhập Console Logger
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Thiết lập Index Settings với Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ Tạo hoặc tải Index
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Thêm tài liệu và thực hiện tìm kiếm
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Mẹo:** Console logger là lựa chọn lý tưởng trong quá trình phát triển vì nó in mỗi mục log ngay lập tức, giúp bạn xác minh việc lập chỉ mục và tìm kiếm hoạt động như mong đợi.

## Ứng dụng thực tiễn
1. **Document Management Systems:** Giữ lại các bản ghi audit cho mọi tài liệu đã được lập chỉ mục.  
2. **Enterprise Search Engines:** Giám sát hiệu suất truy vấn và tỷ lệ lỗi trong thời gian thực.  
3. **Legal & Compliance Software:** Ghi lại các từ khóa tìm kiếm cho báo cáo quy định.  

## Các cân nhắc về hiệu năng
- **Log Size:** Bằng cách **set max log size**, bạn tránh việc sử dụng đĩa quá mức có thể làm chậm ứng dụng.  
- **Asynchronous Logging:** Nếu cần thông lượng cao hơn, hãy cân nhắc bọc logger trong một hàng đợi async (ngoài phạm vi của hướng dẫn này).  
- **Memory Management:** Giải phóng các đối tượng `Index` lớn khi không còn cần thiết để giảm footprint của JVM.  

## Các vấn đề thường gặp & Giải pháp
- **Log path not accessible:** Kiểm tra thư mục tồn tại và ứng dụng có quyền ghi.  
- **Logger not firing:** Đảm bảo bạn gọi `settings.setLogger(...)` *trước* khi tạo đối tượng `Index`.  
- **Console output missing:** Xác nhận bạn đang chạy ứng dụng trong terminal hiển thị `System.out`.  

## Câu hỏi thường gặp

**Q: What does the second parameter of `FileLogger` control?**  
A: Nó đặt kích thước tối đa của tệp log tính bằng megabyte, cho phép bạn **set max log size**.

**Q: Can I combine file and console loggers?**  
A: Có, bằng cách tạo một logger tùy chỉnh chuyển tiếp tin nhắn tới cả hai đích.

**Q: How do I add documents to index after the initial creation?**  
A: Gọi `index.add(pathToNewDocs)` bất kỳ lúc nào; logger sẽ ghi lại thao tác.

**Q: Is `ConsoleLogger` thread‑safe?**  
A: Nó ghi trực tiếp vào `System.out`, được JVM đồng bộ, nên an toàn cho hầu hết các trường hợp sử dụng.

**Q: Will limiting the log file size affect the amount of information stored?**  
A: Khi đạt giới hạn kích thước, các mục mới có thể bị loại bỏ hoặc tệp có thể **roll over log file**, tùy thuộc vào triển khai logger.

## Tài nguyên
- [Tài liệu](https://docs.groupdocs.com/search/java/)
- [Tham chiếu API](https://reference.groupdocs.com/search/java/)

---

**Cập nhật lần cuối:** 2026-02-24  
**Được kiểm tra với:** GroupDocs.Search for Java 25.4  
**Tác giả:** GroupDocs  

---
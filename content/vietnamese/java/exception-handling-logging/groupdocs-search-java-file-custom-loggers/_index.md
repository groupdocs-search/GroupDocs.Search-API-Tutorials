---
date: '2025-12-24'
description: Tìm hiểu cách giới hạn kích thước tệp log và sử dụng console logger Java
  với GroupDocs.Search cho Java. Hướng dẫn này bao gồm cấu hình ghi log, mẹo khắc
  phục sự cố và tối ưu hiệu suất.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Giới hạn kích thước tệp log với các Logger Java của GroupDocs.Search
type: docs
url: /vi/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Giới hạn kích thước tệp log với GroupDocs.Search Java Loggers

Ghi log hiệu quả là cần thiết khi quản lý các bộ sưu tập tài liệu lớn, đặc biệt khi bạn cần **giới hạn kích thước tệp log** để kiểm soát dung lượng lưu trữ. **GroupDocs.Search for Java** cung cấp các giải pháp mạnh mẽ để xử lý log thông qua khả năng tìm kiếm mạnh mẽ của nó. Hướng dẫn này chỉ cho bạn cách triển khai file logger và custom logger bằng GroupDocs.Search, nâng cao khả năng theo dõi sự kiện và gỡ lỗi của ứng dụng.

## Trả lời nhanh
- **“Giới hạn kích thước tệp log” có nghĩa là gì?** Nó đặt giới hạn tối đa cho kích thước của một tệp log, ngăn chặn việc tăng trưởng không kiểm soát trên đĩa.  
- **Logger nào cho phép bạn giới hạn kích thước tệp log?** `FileLogger` tích hợp sẵn chấp nhận tham số max‑size.  
- **Làm sao để sử dụng console logger java?** Tạo một instance của `ConsoleLogger` và đặt nó vào `IndexSettings`.  
- **Tôi có cần giấy phép cho GroupDocs.Search không?** Bản dùng thử đủ cho việc đánh giá; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Bước đầu tiên là gì?** Thêm dependency GroupDocs.Search vào dự án Maven của bạn.

## “Giới hạn kích thước tệp log” là gì?
Giới hạn kích thước tệp log có nghĩa là cấu hình logger sao cho khi tệp đạt tới một ngưỡng đã định (ví dụ: 4 MB), nó sẽ ngừng tăng trưởng hoặc chuyển sang tệp mới. Điều này giúp dung lượng lưu trữ của ứng dụng dự đoán được và tránh suy giảm hiệu năng.

## Tại sao nên dùng file và custom logger với GroupDocs.Search?
- **Khả năng kiểm toán:** Lưu lại bản ghi vĩnh viễn của các sự kiện lập chỉ mục và tìm kiếm.  
- **Gỡ lỗi:** Nhanh chóng xác định vấn đề bằng cách xem các log ngắn gọn.  
- **Linh hoạt:** Chọn giữa log tệp bền vững và đầu ra console ngay lập tức (`use console logger java`).  

## Điều kiện tiên quyết
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 hoặc mới hơn, IDE (IntelliJ IDEA, Eclipse, …).  
- Kiến thức cơ bản về Java và Maven.  

## Cài đặt GroupDocs.Search for Java

Thêm thư viện vào dự án của bạn bằng một trong các cách dưới đây.

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
Tải JAR mới nhất từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Mua giấy phép
Lấy bản dùng thử hoặc mua giấy phép qua [trang cấp phép](https://purchase.groupdocs.com/temporary-license/).

## Cách giới hạn kích thước tệp log với File Logger
Dưới đây là hướng dẫn từng bước để cấu hình `FileLogger` sao cho tệp log không bao giờ vượt quá kích thước bạn chỉ định.

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

**Điểm quan trọng:** Tham số thứ hai (`4.0`) của hàm khởi tạo `FileLogger` xác định kích thước tối đa của tệp log tính bằng megabyte, trực tiếp đáp ứng yêu cầu **giới hạn kích thước tệp log**.

## Cách sử dụng console logger java
Nếu bạn muốn nhận phản hồi ngay trong terminal, hãy thay thế file logger bằng console logger.

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

**Mẹo:** Console logger rất hữu ích trong quá trình phát triển vì nó in mỗi mục log ngay lập tức, giúp bạn xác minh rằng quá trình lập chỉ mục và tìm kiếm hoạt động như mong đợi.

## Ứng dụng thực tiễn
1. **Hệ thống quản lý tài liệu:** Lưu lại các bản ghi kiểm toán cho mọi tài liệu được lập chỉ mục.  
2. **Công cụ tìm kiếm doanh nghiệp:** Giám sát hiệu suất truy vấn và tỷ lệ lỗi trong thời gian thực.  
3. **Phần mềm pháp lý & tuân thủ:** Ghi lại các từ khóa tìm kiếm cho báo cáo quy định.

## Các cân nhắc về hiệu năng
- **Kích thước log:** Bằng cách giới hạn kích thước tệp log, bạn tránh việc tiêu tốn quá nhiều dung lượng đĩa có thể làm chậm ứng dụng.  
- **Ghi log bất đồng bộ:** Nếu cần thông lượng cao hơn, hãy cân nhắc bọc logger trong một hàng đợi async (không nằm trong phạm vi của hướng dẫn này).  
- **Quản lý bộ nhớ:** Giải phóng các đối tượng `Index` lớn khi không còn cần thiết để giảm footprint của JVM.

## Các vấn đề thường gặp & Giải pháp
- **Đường dẫn log không truy cập được:** Kiểm tra thư mục tồn tại và ứng dụng có quyền ghi.  
- **Logger không hoạt động:** Đảm bảo bạn gọi `settings.setLogger(...)` *trước* khi tạo đối tượng `Index`.  
- **Không có đầu ra console:** Xác nhận bạn đang chạy ứng dụng trong terminal hiển thị `System.out`.

## Câu hỏi thường gặp

**Hỏi: Tham số thứ hai của `FileLogger` điều khiển gì?**  
Đáp: Nó đặt kích thước tối đa của tệp log tính bằng megabyte, cho phép bạn giới hạn kích thước tệp log.

**Hỏi: Tôi có thể kết hợp file và console logger không?**  
Đáp: Có, bằng cách tạo một custom logger chuyển tiếp thông điệp tới cả hai đích.

**Hỏi: Làm sao thêm tài liệu vào index sau khi đã tạo lần đầu?**  
Đáp: Gọi `index.add(pathToNewDocs)` bất kỳ lúc nào; logger sẽ ghi lại thao tác này.

**Hỏi: `ConsoleLogger` có an toàn đa luồng không?**  
Đáp: Nó ghi trực tiếp vào `System.out`, được JVM đồng bộ hoá, nên an toàn cho hầu hết các trường hợp sử dụng.

**Hỏi: Giới hạn kích thước tệp log có ảnh hưởng tới lượng thông tin được lưu không?**  
Đáp: Khi đạt giới hạn, các mục mới có thể bị bỏ qua hoặc tệp sẽ chuyển sang tệp mới, tùy vào cách triển khai của logger.

## Tài nguyên
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Cập nhật lần cuối:** 2025-12-24  
**Kiểm thử với:** GroupDocs.Search for Java 25.4  
**Tác giả:** GroupDocs
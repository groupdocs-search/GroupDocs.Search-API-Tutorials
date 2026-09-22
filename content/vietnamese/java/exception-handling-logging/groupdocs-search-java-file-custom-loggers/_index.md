---
date: '2026-09-21'
description: Tìm hiểu cách tạo logger, đặt kích thước log tối đa và sử dụng console
  logger trong GroupDocs.Search cho Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Tìm hiểu cách tạo logger, đặt kích thước log tối đa và sử dụng console
  logger trong GroupDocs.Search cho Java. Thực hiện theo hướng dẫn từng bước và các
  mẹo thực hành tốt nhất.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Cách tạo logger và giới hạn kích thước log trong GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: Cách tạo logger và giới hạn kích thước log trong GroupDocs.Search cho Java
type: docs
url: /vi/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Cách tạo logger và giới hạn kích thước tệp log trong GroupDocs.Search cho Java

Trong hướng dẫn này, bạn sẽ **cách tạo logger** cho GroupDocs.Search, cấu hình kích thước tối đa của tệp log và chuyển đổi giữa ghi log dạng tệp và console. Quản lý log đúng cách ngăn đĩa bị đầy trong các công việc lập chỉ mục lớn, cải thiện việc khắc phục sự cố và cung cấp phản hồi ngay lập tức khi phát triển. Chúng tôi sẽ bắt đầu với thiết lập Maven, đi qua cấu hình logger, và kết thúc bằng một truy vấn tìm kiếm đơn giản minh họa logger đang hoạt động.

## Câu trả lời nhanh
- **“Giới hạn kích thước tệp log” có nghĩa là gì?** Nó giới hạn kích thước tối đa của một tệp log, ngăn việc tăng trưởng không kiểm soát trên đĩa.  
- **Logger nào cho phép bạn giới hạn kích thước tệp log?** Logger tích hợp sẵn `FileLogger` chấp nhận tham số kích thước tối đa.  
- **Làm thế nào để sử dụng console logger java?** Tạo một thể hiện của `ConsoleLogger` và đặt nó vào `IndexSettings`.  
- **Tôi có cần giấy phép cho GroupDocs.Search không?** Bản dùng thử hoạt động cho việc đánh giá; giấy phép thương mại là bắt buộc cho môi trường sản xuất.  
- **Bước đầu tiên là gì?** Thêm phụ thuộc GroupDocs.Search vào dự án Maven của bạn.  

## Giới hạn kích thước tệp log là gì?
Cài đặt **giới hạn kích thước tệp log** cho logger dừng ghi các mục mới khi tệp đạt ngưỡng đã định (ví dụ, 4 MB). Khi đạt giới hạn, logger hoặc loại bỏ các tin nhắn tiếp theo hoặc chuyển sang tệp mới, giữ cho việc sử dụng đĩa dự đoán được.

## Tại sao nên sử dụng logger dạng tệp và tùy chỉnh với GroupDocs.Search?
Logger dạng tệp và tùy chỉnh cung cấp khả năng kiểm toán, hiểu biết gỡ lỗi và tính linh hoạt. Trong môi trường sản xuất, log tệp cung cấp bản ghi vĩnh viễn của mọi hoạt động lập chỉ mục và tìm kiếm, trong khi log console cung cấp phản hồi ngay lập tức trong quá trình phát triển. Những log này giúp các nhóm giám sát hiệu năng, truy vết lỗi và đáp ứng yêu cầu tuân thủ bằng cách lưu giữ chi tiết hoạt động.

## Yêu cầu trước
- GroupDocs.Search cho Java ≥ 25.4.  
- JDK 8 hoặc mới hơn, cùng một IDE như IntelliJ IDEA hoặc Eclipse.  
- Kiến thức cơ bản về Maven và lập trình Java.  

## Thiết lập GroupDocs.Search cho Java

Thêm thư viện vào dự án của bạn bằng một trong các phương pháp dưới đây.

**Cài đặt Maven:**  

```text
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
```

**Tải trực tiếp:**  
Tải JAR mới nhất từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Nhận bản dùng thử hoặc mua giấy phép qua [trang cấp phép](https://purchase.groupdocs.com/temporary-license/).

## Cách tạo logger tùy chỉnh cho GroupDocs.Search
Tạo một logger tùy chỉnh là rất đơn giản vì GroupDocs.Search dựa trên giao diện `ILogger`. Bằng cách triển khai giao diện này—hoặc mở rộng `FileLogger` hoặc `ConsoleLogger` đã cung cấp—bạn có thể chèn hành vi bổ sung như chuyển tiếp từ xa hoặc quay vòng log. Bạn cũng có thể thêm logic khởi tạo, chẳng hạn mở kết nối mạng, và đảm bảo tài nguyên được đóng trong phương thức tắt của logger. Cách tiếp cận này cho phép bạn tích hợp với các nền tảng giám sát như ELK hoặc Splunk.

### Định nghĩa anchor
`ILogger` là hợp đồng ghi log cốt lõi trong GroupDocs.Search; bất kỳ lớp nào triển khai phương thức `log(Level, String)` của nó đều có thể trở thành một logger.

### Ví dụ tiếp cận (không có khối mã)
1. Tạo một lớp triển khai `ILogger`.  
2. Ghi đè phương thức `log` để ghi thông điệp tới đích bạn chọn (tệp, cơ sở dữ liệu, endpoint HTTP).  
3. Trong cấu hình chỉ mục, gọi `settings.setLogger(new YourCustomLogger())`.  

## Cách giới hạn kích thước tệp log với File Logger
`FileLogger` ghi các mục log vào tệp trên đĩa và chấp nhận tham số kích thước tối đa. Bằng cách chỉ định giới hạn kích thước, logger tự động ngừng thêm mục mới hoặc tạo tệp mới khi đạt ngưỡng, ngăn việc tăng trưởng đĩa không kiểm soát. Hành vi này đảm bảo việc ghi log không ảnh hưởng đến hiệu năng lập chỉ mục đồng thời giữ bản ghi ngắn gọn các sự kiện.

### Định nghĩa anchor
`FileLogger` là logger tích hợp sẵn ghi các tin nhắn vào tệp văn bản và hỗ trợ kích thước tệp tối đa có thể cấu hình.

### Hướng dẫn từng bước
1️⃣ **Nhập các gói cần thiết**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Cấu hình cài đặt chỉ mục với File Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **Tạo hoặc tải chỉ mục**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Thêm tài liệu vào chỉ mục**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Thực hiện truy vấn tìm kiếm**  
```text
```java
SearchResult result = index.search(query);
```
```

**Điểm chính:** Tham số thứ hai của hàm khởi tạo `FileLogger` (`4.0`) định nghĩa **đặt kích thước log tối đa** tính bằng megabyte, trực tiếp đáp ứng yêu cầu **giới hạn kích thước tệp log**.

## Cách sử dụng console logger java
Khi bạn cần nhìn thấy các sự kiện log ngay lập tức, `ConsoleLogger` ghi mỗi thông điệp vào `System.out`. Logger này nhẹ và an toàn đa luồng, phù hợp cho các phiên phát triển và gỡ lỗi. Nó cung cấp phản hồi tức thời về tiến độ lập chỉ mục, truy vấn tìm kiếm và các điều kiện lỗi mà không cần I/O tệp, giúp tăng tốc kiểm thử lặp lại.

### Định nghĩa anchor
`ConsoleLogger` là logger nhẹ xuất các mục log ra luồng console tiêu chuẩn, lý tưởng cho các phiên gỡ lỗi.

### Các bước cấu hình
1️⃣ **Nhập console logger**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Cấu hình cài đặt chỉ mục với Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Tạo hoặc tải chỉ mục**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Thêm tài liệu và thực hiện tìm kiếm**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Mẹo:** Console logger lý tưởng trong quá trình phát triển vì nó in mỗi mục log ngay lập tức, giúp bạn xác nhận rằng việc lập chỉ mục và tìm kiếm hoạt động như mong đợi.

## Ứng dụng thực tiễn
1. **Hệ thống quản lý tài liệu:** Giữ nhật ký kiểm toán của mọi tài liệu được lập chỉ mục, đáp ứng yêu cầu tuân thủ.  
2. **Công cụ tìm kiếm doanh nghiệp:** Giám sát hiệu năng truy vấn và tỷ lệ lỗi theo thời gian thực, cho phép kiểm tra SLA nhanh chóng.  
3. **Phần mềm pháp lý & tuân thủ:** Ghi lại các từ khóa tìm kiếm và thời gian cho báo cáo quy định, với log được lưu trữ trong thời gian bảo lưu bắt buộc.

## Các cân nhắc về hiệu năng
- **Kích thước log:** Bằng cách **đặt kích thước log tối đa**, bạn tránh việc sử dụng đĩa quá mức có thể làm chậm bộ thu gom rác của JVM.  
- **Logging bất đồng bộ:** Đối với các kịch bản tải cao, bạn có thể bọc logger trong một hàng đợi bất đồng bộ để tách I/O ra khỏi luồng lập chỉ mục (triển khai ngoài phạm vi hướng dẫn này).  
- **Quản lý bộ nhớ:** Giải phóng các đối tượng `Index` lớn bằng `index.close()` khi không còn cần thiết để giảm footprint của JVM.

## Các vấn đề thường gặp & giải pháp
- **Đường dẫn log không truy cập được:** Kiểm tra thư mục tồn tại và ứng dụng có quyền ghi cho tài khoản người dùng chạy JVM.  
- **Logger không hoạt động:** Đảm bảo bạn gọi `settings.setLogger(...)` *trước* khi tạo đối tượng `Index`; nếu không, logger mặc định sẽ được sử dụng.  
- **Không có output console:** Xác nhận bạn chạy ứng dụng trong terminal hiển thị `System.out`, và không có framework logging (ví dụ, SLF4J) chặn output.

## Câu hỏi thường gặp

**Q: Tham số thứ hai của `FileLogger` điều khiển gì?**  
A: Nó đặt kích thước tối đa của tệp log tính bằng megabyte, cho phép bạn **đặt kích thước log tối đa** và ngăn việc tăng trưởng không kiểm soát.

**Q: Tôi có thể kết hợp file logger và console logger không?**  
A: Có. Tạo một logger tùy chỉnh chuyển tiếp mỗi lời gọi `log` tới cả `FileLogger` và `ConsoleLogger`, sau đó đăng ký logger tổng hợp này với `IndexSettings`.

**Q: Làm thế nào để thêm tài liệu vào chỉ mục sau khi tạo ban đầu?**  
A: Gọi `index.add(pathToNewDocs)` bất kỳ lúc nào; logger đã cấu hình sẽ tự động ghi lại việc thêm.

**Q: `ConsoleLogger` có an toàn đa luồng không?**  
A: Nó ghi trực tiếp vào `System.out`, JVM đồng bộ hoá nội bộ, nên an toàn cho các trường hợp đa luồng thông thường.

**Q: Giới hạn kích thước tệp log có ảnh hưởng đến lượng thông tin được lưu không?**  
A: Khi đạt giới hạn kích thước, các mục mới sẽ bị loại bỏ hoặc logger sẽ chuyển sang tệp mới, tùy thuộc vào cách triển khai bạn chọn.

## Tài nguyên
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Cập nhật lần cuối:** 2026-09-21  
**Kiểm tra với:** GroupDocs.Search cho Java 25.4  
**Tác giả:** GroupDocs  

---

## Các hướng dẫn liên quan

- [Cách triển khai Logging - Hướng dẫn Xử lý ngoại lệ và Logging cho GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Triển khai Logging bất đồng bộ trong Java với GroupDocs.Search – Hướng dẫn Logger tùy chỉnh](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Tạo chỉ mục tìm kiếm Java – Hướng dẫn GroupDocs.Search](/search/java/indexing/)
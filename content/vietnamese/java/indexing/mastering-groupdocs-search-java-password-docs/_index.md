---
date: '2026-10-28'
description: Tìm hiểu cách tìm kiếm nhiều loại tệp và tạo một chỉ mục có thể tìm kiếm
  cho các tài liệu được bảo vệ bằng mật khẩu trong Java bằng cách sử dụng GroupDocs.Search.
  Hướng dẫn từng bước kèm mã nguồn, mẹo và thủ thuật tối ưu hiệu năng.
keywords:
- search multiple file types
- build searchable index
- password protected document indexing java
- groupdocs.search java api
lastmod: '2026-10-28'
og_description: Tìm hiểu cách tìm kiếm nhiều loại tệp và tạo một chỉ mục có thể tìm
  kiếm cho các tài liệu được bảo vệ bằng mật khẩu trong Java bằng cách sử dụng GroupDocs.Search.
  Hướng dẫn từng bước kèm mã nguồn, mẹo và thủ thuật tối ưu hiệu năng.
og_image_alt: Guide showing Java code to search multiple file types and index password‑protected
  documents with GroupDocs.Search
og_title: Cách tìm kiếm nhiều loại tệp và lập chỉ mục tài liệu trong Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-28'
  description: Learn how to search multiple file types and build a searchable index
    for password‑protected documents in Java using GroupDocs.Search. Step‑by‑step
    guide with code, tips, and performance tricks.
  headline: How to search multiple file types and index docs in Java
  type: TechArticle
- questions:
  - answer: GroupDocs.Search supports 120+ formats including PDF, DOCX, XLSX, PPTX,
      and common image types. Install format plugins if required.
    question: How do I handle different file formats?
  - answer: The document is skipped and a warning is logged; verify your password
      dictionary or event handler.
    question: What happens if a password is wrong?
  - answer: Yes, but they must be downloaded to a local temporary folder first because
      the engine works with file‑system paths.
    question: Can I index files stored in the cloud?
  - answer: Adjust scoring with `IndexOptions`, add synonyms, and use advanced query
      syntax such as `field:term~` for fuzzy matching. `IndexOptions` is a configuration
      object that controls scoring and indexing behavior.
    question: How can I improve search relevance?
  - answer: Review the log output; common causes are missing passwords, corrupted
      files, or unsupported formats.
    question: What should I do if indexing fails for some files?
  type: FAQPage
tags:
- search multiple file types
- GroupDocs.Search
- Java indexing
- password‑protected docs
- document search
title: Cách tìm kiếm nhiều loại tệp và lập chỉ mục tài liệu trong Java
type: docs
url: /vi/java/indexing/mastering-groupdocs-search-java-password-docs/
weight: 1
---

# Cách tìm kiếm nhiều loại tệp và lập chỉ mục tài liệu trong Java

Trong các doanh nghiệp hiện đại, bạn thường cần **tìm kiếm nhiều loại tệp** đồng thời giữ các tệp bí mật được khóa bằng mật khẩu. Hướng dẫn này cho bạn cách xây dựng một chỉ mục có thể tìm kiếm cho các tài liệu được bảo vệ bằng mật khẩu trong Java bằng cách sử dụng GroupDocs.Search. Bạn sẽ thấy cách cấu hình từ điển mật khẩu, xử lý các sự kiện yêu cầu mật khẩu, và tối ưu hiệu năng cho các lô lớn — tất cả mà không cần viết mã giải mã tùy chỉnh.

## Câu trả lời nhanh
- **Nội dung của hướng dẫn này là gì?** Lập chỉ mục các tài liệu được bảo vệ bằng mật khẩu với từ điển mật khẩu và một bộ lắng nghe sự kiện.  
- **Thư viện nào được yêu cầu?** GroupDocs.Search for Java (phiên bản mới nhất).  
- **Tôi có cần giấy phép không?** Một giấy phép dùng thử miễn phí tạm thời có sẵn để đánh giá.  
- **Tôi có thể lập chỉ mục các loại tệp khác không?** Có, GroupDocs.Search hỗ trợ hơn 120 định dạng bao gồm PDF, DOCX, XLSX, PPTX và hình ảnh.  
- **Phiên bản Java nào cần thiết?** JDK 8 hoặc mới hơn.  

## “create document index java” là gì?
`create document index java` đề cập đến quá trình xây dựng một cấu trúc dữ liệu có thể tìm kiếm mà ánh xạ các thuật ngữ tới vị trí của các tệp được quản lý bởi Java. Với GroupDocs.Search, engine tự động trích xuất văn bản từ các định dạng được hỗ trợ — bao gồm PDF được mã hóa, tài liệu Office và hình ảnh — để bạn có thể thực hiện tìm kiếm toàn văn mà không cần viết bất kỳ mã giải mã nào. Cách tiếp cận này đơn giản hoá việc triển khai tìm kiếm đồng thời bảo vệ bảo mật tài liệu.

## Tại sao sử dụng GroupDocs.Search cho các tệp được bảo vệ bằng mật khẩu?
GroupDocs.Search cung cấp cơ chế mở khóa không cần can thiệp, áp dụng mật khẩu từ một từ điển hoặc bộ xử lý sự kiện, cho phép bạn lập chỉ mục các tệp được mã hóa trong một lần duy nhất. Nó xử lý lên tới 2 triệu tài liệu mỗi giờ trên máy chủ tiêu chuẩn 8‑core, hỗ trợ hơn 120 loại tệp, và cung cấp ngôn ngữ truy vấn phong phú với các toán tử Boolean, wildcard và fuzzy — tất cả đều cần thiết để xây dựng một chỉ mục có thể tìm kiếm bao phủ nội dung đa dạng.

## Yêu cầu trước
- Java Development Kit (JDK) 8+ đã được cài đặt và thêm vào `PATH` của bạn.  
- Một IDE như IntelliJ IDEA hoặc Eclipse.  
- Maven để quản lý phụ thuộc.  
- GroupDocs.Search for Java – thêm thư viện qua Maven (xem phần thiết lập).  

## Cài đặt GroupDocs.Search cho java

### Sử dụng Maven
Thêm repository và dependency vào tệp `pom.xml` của bạn:

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

### Tải trực tiếp
Hoặc, bạn có thể tải phiên bản mới nhất trực tiếp từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

Để bắt đầu với giấy phép dùng thử, truy cập [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) và làm theo hướng dẫn để nhận bản dùng thử miễn phí.

## Cách lập chỉ mục tài liệu với từ điển mật khẩu

Bạn có thể **xây dựng một chỉ mục có thể tìm kiếm** bằng cách cung cấp một từ điển ánh xạ đường dẫn tệp tới mật khẩu của chúng. Engine sẽ tự động lấy mật khẩu đúng trong quá trình lập chỉ mục.

### Tổng quan
Lưu mật khẩu tài liệu trong một bản đồ key‑value đơn giản để engine lập chỉ mục có thể mở khóa các tệp khi cần.

### Bước 1: xác định chỉ mục và thư mục tài liệu
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordDictionary";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Bước 2: tạo chỉ mục
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Bước 3: thêm mật khẩu tài liệu
```java
// Add passwords for specific files using their absolute paths
String path1 = new File(documentsFolder + "/English.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path1, "123456");

String path2 = new File(documentsFolder + "/SampleDocument.docx").getAbsolutePath();
index.getDictionaries().getDocumentPasswords().add(path2, "123456");
```

### Bước 4: lập chỉ mục tài liệu
```java
// Automatically retrieve passwords from the dictionary during indexing
index.add(documentsFolder);
```

### Bước 5: tìm kiếm trong chỉ mục
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

**Mẹo:** Đối với các kịch bản sản xuất, tải mật khẩu từ một kho bảo mật (ví dụ, Azure Key Vault hoặc AWS Secrets Manager) thay vì mã cứng.

#### Khắc phục sự cố
- Xác minh rằng mỗi mật khẩu khớp với mật khẩu bảo vệ thực tế của tệp.  
- Kiểm tra lại đường dẫn tệp; một đường dẫn không đúng sẽ gây ra `FileNotFoundException`.

## Cách lập chỉ mục tài liệu với bộ lắng nghe sự kiện yêu cầu mật khẩu?

Bạn có thể cung cấp mật khẩu chỉ khi engine phát sinh sự kiện yêu cầu mật khẩu, giữ thông tin đăng nhập ra khỏi bộ nhớ và cho phép giải quyết mật khẩu động.

Khi engine lập chỉ mục gặp một tệp được mã hóa, nó sẽ kích hoạt một callback nơi bạn có thể tra cứu mật khẩu từ kho bảo mật hoặc tính toán ngay lập tức. Phương pháp này giảm bề mặt tấn công so với việc lưu tất cả mật khẩu trong một từ điển.

### Tổng quan
Cung cấp mật khẩu ngay lập tức qua một callback sự kiện, giữ kho thông tin đăng nhập của bạn được cô lập.

### Bước 1: xác định chỉ mục và thư mục tài liệu
```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/IndexUsingPasswordEvent";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Path to password‑protected documents
```

### Bước 2: tạo chỉ mục
```java
// Initialize the Index object in the specified directory
Index index = new Index(indexFolder);
```

### Bước 3: đăng ký sự kiện yêu cầu mật khẩu
```java
index.getEvents().PasswordRequired.add(new EventHandler<PasswordRequiredEventArgs>() {
    @Override
    public void invoke(Object sender, PasswordRequiredEventArgs args) {
        // Provide password for DOCX files when needed
        if (args.getDocumentFullPath().endsWith(".docx")) {
            args.setPassword("123456");
        }
    }
});
```

### Bước 4: lập chỉ mục tài liệu
```java
// The event handler will supply passwords as required during indexing
index.add(documentsFolder);
```

### Bước 5: tìm kiếm trong chỉ mục
```java
String query = "sample OR increasing";
SearchResult result = index.search(query);

// Handle search results (e.g., display or process them)
```

#### Khắc phục sự cố
- Đảm bảo bộ xử lý sự kiện bao phủ tất cả các phần mở rộng tệp bạn cần lập chỉ mục.  
- Kiểm tra với một vài tệp mẫu trước để xác nhận mật khẩu đã được áp dụng.

## Ứng dụng thực tiễn

1. **Enterprise document management** – tự động lập chỉ mục các hợp đồng bí mật, tệp HR và báo cáo tài chính trong khi giữ chúng được mã hóa khi lưu trữ.  
2. **Legal archives** – nhanh chóng truy xuất các tệp vụ án mà không lộ nội dung nhạy cảm.  
3. **Healthcare records** – lập chỉ mục các PDF và tài liệu Word của bệnh nhân đồng thời tuân thủ yêu cầu HIPAA.  

## Các cân nhắc về hiệu năng

- **Memory allocation** – cấp phát đủ bộ nhớ heap (`-Xmx2g` hoặc cao hơn) cho các lô lớn.  
- **Parallel indexing** – sử dụng `index.addAsync(...)` hoặc chạy nhiều luồng lập chỉ mục để đạt tới **2 triệu tài liệu mỗi giờ** trên máy 8‑core. `index.addAsync(...)` là một phương thức que các tài liệu để lập chỉ mục bất đồng bộ.  
- **Index maintenance** – định kỳ gọi `index.optimize()` để nén chỉ mục và cải thiện tốc độ truy vấn.  

## Các vấn đề thường gặp và giải pháp

- **Wrong password** – tài liệu bị bỏ qua và một cảnh báo được ghi lại. Kiểm tra lại nguồn mật khẩu của bạn.  
- **Unsupported format** – cài đặt các plugin định dạng cần thiết hoặc chuyển đổi tệp sang loại được hỗ trợ trước khi lập chỉ mục.  
- **Large files** – tăng kích thước heap và cân nhắc lập chỉ mục chúng trong các lô nhỏ hơn để tránh `OutOfMemoryError`.  

## Câu hỏi thường gặp

**Q: Làm thế nào để tôi xử lý các định dạng tệp khác nhau?**  
A: GroupDocs.Search hỗ trợ hơn 120 định dạng bao gồm PDF, DOCX, XLSX, PPTX và các loại hình ảnh phổ biến. Cài đặt plugin định dạng nếu cần.

**Q: Điều gì xảy ra nếu mật khẩu sai?**  
A: Tài liệu bị bỏ qua và một cảnh báo được ghi lại; xác minh từ điển mật khẩu hoặc bộ xử lý sự kiện của bạn.

**Q: Tôi có thể lập chỉ mục các tệp lưu trữ trên đám mây không?**  
A: Có, nhưng chúng phải được tải xuống một thư mục tạm thời cục bộ trước vì engine làm việc với các đường dẫn hệ thống tệp.

**Q: Làm thế nào tôi có thể cải thiện độ liên quan của tìm kiếm?**  
A: Điều chỉnh điểm số với `IndexOptions`, thêm đồng nghĩa, và sử dụng cú pháp truy vấn nâng cao như `field:term~` cho khớp fuzzy. `IndexOptions` là một đối tượng cấu hình kiểm soát điểm số và hành vi lập chỉ mục.

**Q: Tôi nên làm gì nếu việc lập chỉ mục thất bại đối với một số tệp?**  
A: Xem lại đầu ra log; các nguyên nhân phổ biến là thiếu mật khẩu, tệp bị hỏng, hoặc định dạng không được hỗ trợ.

## Tài nguyên
- [Tài liệu GroupDocs.Search](https://docs.groupdocs.com/search/java/)
- [Tham chiếu API](https://reference.groupdocs.com/search/java)
- [Tải xuống GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [Kho lưu trữ GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Diễn đàn hỗ trợ miễn phí](https://forum.groupdocs.com/c/search/10)
- [Thông tin giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)

Bằng cách làm theo hướng dẫn này, bạn hiện đã biết **cách tìm kiếm nhiều loại tệp** và **lập chỉ mục các tài liệu được bảo vệ bằng mật khẩu** trong Java, nâng cao cả bảo mật và khả năng khám phá trong các ứng dụng của bạn.

---

**Cập nhật lần cuối:** 2026-10-28  
**Kiểm thử với:** GroupDocs.Search 25.4 cho Java  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Cách lập chỉ mục tài liệu được bảo vệ bằng mật khẩu trong Java bằng GroupDocs.Search](/search/java/indexing/mastering-groupdocs-search-java-password-docs/)
- [Cải thiện hiệu năng truy vấn với GroupDocs.Search Java: Tối ưu chỉ mục & tìm kiếm](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
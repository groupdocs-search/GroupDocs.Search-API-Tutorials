---
date: '2025-12-19'
description: Tìm hiểu cách thêm tài liệu vào chỉ mục và bật tìm kiếm dựa trên đoạn
  trong Java bằng GroupDocs.Search, nâng cao hiệu suất cho các bộ tài liệu lớn.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Thêm tài liệu vào chỉ mục bằng tìm kiếm dựa trên đoạn trong Java
type: docs
url: /vi/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Thêm tài liệu vào chỉ mục với tìm kiếm dựa trên đoạn trong Java

Trong thế giới dữ liệu ngày nay, khả năng **add documents to index** nhanh chóng và sau đó thực hiện tìm kiếm dựa trên đoạn là điều thiết yếu cho bất kỳ ứng dụng nào xử lý các bộ sưu tập tệp lớn. Dù bạn đang làm việc với hợp đồng pháp lý, kho lưu trữ hỗ trợ khách hàng, hay thư viện nghiên cứu khổng lồ, hướng dẫn này sẽ chỉ cho bạn cách thiết lập GroupDocs.Search cho Java để có thể lập chỉ mục tài liệu một cách hiệu quả và truy xuất thông tin liên quan theo các đoạn nhỏ.

## Những gì bạn sẽ học
- Cách tạo một chỉ mục tìm kiếm trong thư mục được chỉ định.  
- Các bước **add documents to index** từ nhiều vị trí.  
- Cấu hình tùy chọn tìm kiếm để bật tìm kiếm dựa trên đoạn.  
- Thực hiện tìm kiếm dựa trên đoạn ban đầu và các lần tiếp theo.  
- Các kịch bản thực tế mà tìm kiếm tài liệu dựa trên đoạn tỏa sáng.

## Câu trả lời nhanh
- **Bước đầu tiên là gì?** Tạo thư mục chỉ mục tìm kiếm.  
- **Làm sao để bao gồm nhiều tệp?** Sử dụng `index.add()` cho mỗi thư mục tài liệu.  
- **Tùy chọn nào bật tìm kiếm dựa trên đoạn?** `options.setChunkSearch(true)`.  
- **Có thể tiếp tục tìm kiếm sau đoạn đầu tiên không?** Có, gọi `index.searchNext()` kèm token.  
- **Cần giấy phép không?** Bản dùng thử miễn phí hoặc giấy phép tạm thời đủ cho phát triển; giấy phép đầy đủ cần cho môi trường sản xuất.

## Điều kiện tiên quyết
Để làm theo hướng dẫn này, hãy đảm bảo bạn có:

- **Thư viện yêu cầu**: GroupDocs.Search cho Java 25.4 hoặc mới hơn.  
- **Cài đặt môi trường**: JDK tương thích đã được cài đặt.  
- **Kiến thức nền**: Lập trình Java cơ bản và quen thuộc với Maven.

## Cài đặt GroupDocs.Search cho Java
Để bắt đầu, tích hợp GroupDocs.Search vào dự án của bạn bằng Maven:

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

Hoặc tải phiên bản mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Để thử nghiệm GroupDocs.Search:

- **Dùng thử miễn phí** – kiểm tra các tính năng cốt lõi mà không ràng buộc.  
- **Giấy phép tạm thời** – quyền truy cập mở rộng cho phát triển.  
- **Mua bản quyền** – giấy phép đầy đủ cho môi trường sản xuất.

### Khởi tạo và cấu hình cơ bản
Tạo một chỉ mục trong thư mục nơi bạn muốn lưu trữ dữ liệu có thể tìm kiếm:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Cách add documents to index
Bây giờ chỉ mục đã tồn tại, bước tiếp theo hợp lý là **add documents to index** từ các vị trí lưu trữ tệp của bạn.

### 1. Tạo chỉ mục
**Tổng quan**: Thiết lập thư mục cho chỉ mục tìm kiếm.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Thêm tài liệu vào chỉ mục
**Tổng quan**: Kéo các tệp từ nhiều thư mục nguồn.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Cấu hình tùy chọn tìm kiếm cho Chunk Search
Bật tìm kiếm dựa trên đoạn bằng cách điều chỉnh đối tượng options.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Thực hiện tìm kiếm dựa trên đoạn ban đầu
Chạy truy vấn đầu tiên sử dụng các tùy chọn đã bật chunk.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Tiếp tục tìm kiếm dựa trên đoạn
Lặp lại qua các đoạn còn lại cho đến khi quá trình tìm kiếm hoàn tất.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tại sao nên dùng tìm kiếm dựa trên đoạn?
Tìm kiếm dựa trên đoạn chia các bộ sưu tập tài liệu khổng lồ thành các phần quản lý được, giảm áp lực bộ nhớ và tăng tốc thời gian phản hồi. Điều này đặc biệt hữu ích khi:

1. **Các đội pháp lý** cần tìm các điều khoản cụ thể trong hàng ngàn hợp đồng.  
2. **Cổng hỗ trợ khách hàng** phải nhanh chóng hiển thị các bài viết kiến thức liên quan.  
3. **Các nhà nghiên cứu** lọc qua dữ liệu khổng lồ mà không cần tải toàn bộ tệp vào bộ nhớ.

## Các lưu ý về hiệu năng
- **Quản lý bộ nhớ** – Phân bổ đủ không gian heap (`-Xmx`) cho các chỉ mục lớn.  
- **Giám sát tài nguyên** – Theo dõi mức sử dụng CPU trong quá trình lập chỉ mục và tìm kiếm.  
- **Bảo trì chỉ mục** – Định kỳ xây dựng lại hoặc dọn dẹp chỉ mục để loại bỏ dữ liệu lỗi thời.

## Những lỗi thường gặp & Khắc phục
| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| `OutOfMemoryError` khi lập chỉ mục | Heap quá nhỏ | Tăng kích thước heap JVM (`-Xmx2g` hoặc lớn hơn) |
| Không có kết quả trả về | Token chunk không được xử lý | Đảm bảo vòng lặp `while` chạy tới khi `getNextChunkSearchToken()` trả về `null` |
| Tìm kiếm chậm | Chỉ mục chưa được tối ưu | Chạy `index.optimize()` sau khi thêm hàng loạt tài liệu |

## Câu hỏi thường gặp

**H: Tìm kiếm dựa trên đoạn là gì?**  
Đ: Tìm kiếm dựa trên đoạn chia bộ dữ liệu thành các phần nhỏ hơn, cho phép thực hiện truy vấn hiệu quả trên khối lượng dữ liệu lớn mà không cần tải toàn bộ tài liệu vào bộ nhớ.

**H: Làm sao cập nhật chỉ mục với các tệp mới?**  
Đ: Chỉ cần gọi `index.add()` với đường dẫn tới các tài liệu mới; chỉ mục sẽ tự động tích hợp chúng.

**H: GroupDocs.Search có hỗ trợ các định dạng tệp khác nhau không?**  
Đ: Có, nó hỗ trợ PDF, DOCX, XLSX, PPTX và nhiều định dạng phổ biến khác.

**H: Những nút thắt hiệu năng thường gặp là gì?**  
Đ: Hạn chế bộ nhớ và chỉ mục chưa được tối ưu là hai nguyên nhân chính; hãy cấp đủ heap và thường xuyên tối ưu chỉ mục.

**H: Tôi có thể tìm tài liệu chi tiết hơn ở đâu?**  
Đ: Truy cập [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) để xem các hướng dẫn sâu và tham chiếu API.

## Tài nguyên
- **Tài liệu**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Tham chiếu API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Tải xuống**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Hỗ trợ miễn phí**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Giấy phép tạm thời**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Cập nhật lần cuối:** 2025-12-19  
**Đã kiểm tra với:** GroupDocs.Search 25.4 cho Java  
**Tác giả:** GroupDocs
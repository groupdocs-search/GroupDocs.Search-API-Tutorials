---
date: '2026-02-21'
description: Tìm hiểu cách thêm tài liệu vào chỉ mục và tăng hiệu suất tìm kiếm bằng
  phương pháp tìm kiếm dựa trên khối trong Java sử dụng GroupDocs.Search, tối ưu bộ
  nhớ chỉ mục tìm kiếm Java cho các bộ tài liệu lớn.
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

Trong các ứng dụng hiện đại cần **thêm tài liệu vào chỉ mục** nhanh chóng và sau đó thực hiện các truy vấn nhanh, dựa trên đoạn, bạn sẽ muốn một giải pháp mở rộng mà không làm tăng quá mức bộ nhớ. Hướng dẫn này sẽ chỉ cho bạn cách thiết lập GroupDocs.Search cho Java, thêm nhiều thư mục tài liệu, và cấu hình engine để **tăng hiệu suất tìm kiếm** đồng thời giữ **java search index memory** ở mức kiểm soát. Dù bạn đang lập chỉ mục các hợp đồng pháp lý, vé hỗ trợ, hay các bài báo nghiên cứu, các bước dưới đây sẽ cung cấp cho bạn một triển khai sẵn sàng cho môi trường sản xuất.

## Câu trả lời nhanh
- **Bước đầu tiên là gì?** Tạo một thư mục chỉ mục tìm kiếm.  
- **Làm sao để bao gồm nhiều tệp?** Sử dụng `index.add()` cho mỗi thư mục tài liệu.  
- **Tùy chọn nào bật tìm kiếm dựa trên đoạn?** `options.setChunkSearch(true)`.  
- **Tôi có thể tiếp tục tìm kiếm sau đoạn đầu tiên không?** Có, gọi `index.searchNext()` với token.  
- **Có cần giấy phép không?** Bản dùng thử miễn phí hoặc giấy phép tạm thời hoạt động cho phát triển; giấy phép đầy đủ cần thiết cho môi trường sản xuất.  

## Những gì bạn sẽ học
- Cách tạo một chỉ mục tìm kiếm trong thư mục được chỉ định.  
- Các bước **thêm tài liệu vào chỉ mục** từ nhiều vị trí.  
- Cấu hình các tùy chọn tìm kiếm để bật tìm kiếm dựa trên đoạn.  
- Thực hiện các tìm kiếm dựa trên đoạn ban đầu và tiếp theo.  
- Các kịch bản thực tế mà tìm kiếm tài liệu dựa trên đoạn tỏa sáng.  

## Tiền đề
Để làm theo hướng dẫn này, hãy đảm bảo bạn có:

- **Thư viện yêu cầu**: GroupDocs.Search cho Java 25.4 hoặc mới hơn.  
- **Cài đặt môi trường**: JDK (Java Development Kit) tương thích đã được cài đặt.  
- **Kiến thức nền**: Lập trình Java cơ bản và quen thuộc với Maven.

## Thiết lập GroupDocs.Search cho Java
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

Hoặc tải phiên bản mới nhất từ [bản phát hành GroupDocs.Search cho Java](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Để thử nghiệm GroupDocs.Search:

- **Bản dùng thử** – kiểm tra các tính năng cốt lõi mà không cam kết.  
- **Giấy phép tạm thời** – truy cập mở rộng cho phát triển.  
- **Mua bản quyền** – giấy phép đầy đủ cho việc sử dụng trong sản xuất.

### Khởi tạo và cài đặt cơ bản
Tạo một chỉ mục trong thư mục nơi bạn muốn dữ liệu có thể tìm kiếm được lưu trữ:

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

## Cách thêm tài liệu vào chỉ mục
Bây giờ chỉ mục đã tồn tại, bước tiếp theo hợp lý là **thêm tài liệu vào chỉ mục** từ các vị trí lưu trữ tệp của bạn.

### 1. Tạo chỉ mục
**Tổng quan**: Thiết lập một thư mục cho chỉ mục tìm kiếm.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Thêm tài liệu vào chỉ mục
**Tổng quan**: Kéo các tệp từ một số thư mục nguồn.

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

### 3. Cấu hình tùy chọn tìm kiếm cho tìm kiếm dựa trên đoạn
Bật tìm kiếm dựa trên đoạn bằng cách điều chỉnh đối tượng options.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Thực hiện tìm kiếm dựa trên đoạn ban đầu
Chạy truy vấn đầu tiên bằng các tùy chọn đã bật đoạn.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Tiếp tục tìm kiếm dựa trên đoạn
Lặp lại qua các đoạn còn lại cho đến khi tìm kiếm hoàn tất.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Tại sao nên dùng tìm kiếm dựa trên đoạn?
Tìm kiếm dựa trên đoạn chia các bộ sưu tập tài liệu khổng lồ thành các phần có thể quản lý được, giảm áp lực bộ nhớ và tăng tốc thời gian phản hồi. Điều này đặc biệt có lợi khi:

1. **Các nhóm pháp lý** cần xác định các điều khoản cụ thể trong hàng ngàn hợp đồng.  
2. **Cổng hỗ trợ khách hàng** phải hiển thị ngay các bài viết kiến thức liên quan.  
3. **Các nhà nghiên cứu** lọc qua các tập dữ liệu lớn mà không cần tải toàn bộ tệp vào bộ nhớ.

## Cách tiếp cận này **tăng hiệu suất tìm kiếm**
Bằng cách tìm kiếm các đoạn nhỏ hơn thay vì toàn bộ tệp, engine có thể:

- Bỏ qua các phần không liên quan sớm, giảm vòng CPU.  
- Giữ chỉ đoạn đang hoạt động trong bộ nhớ, trực tiếp hạ thấp mức tiêu thụ **java search index memory**.  
- Xử lý song song các đoạn trên máy đa lõi để có kết quả nhanh hơn.

## Quản lý **java search index memory**
Mặc dù tìm kiếm dựa trên đoạn đã giảm đáng kể dung lượng bộ nhớ, bạn vẫn có thể tinh chỉnh JVM thêm:

- Phân bổ heap đủ (`-Xmx2g` hoặc cao hơn) tùy theo kích thước chỉ mục.  
- Sử dụng `index.optimize()` sau khi thêm hàng loạt để nén cấu trúc chỉ mục.  
- Giám sát các pause của GC bằng các công cụ như VisualVM để tránh tăng độ trễ.

## Các cân nhắc về hiệu suất
- **Quản lý bộ nhớ** – Phân bổ đủ không gian heap (`-Xmx`) cho các chỉ mục lớn.  
- **Giám sát tài nguyên** – Theo dõi mức sử dụng CPU trong quá trình lập chỉ mục và tìm kiếm.  
- **Bảo trì chỉ mục** – Thường xuyên xây dựng lại hoặc dọn dẹp chỉ mục để loại bỏ dữ liệu cũ.

## Những lỗi thường gặp & Khắc phục
| Vấn đề | Nguyên nhân | Giải pháp |
|-------|----------------|-----|
| `OutOfMemoryError` khi lập chỉ mục | Kích thước heap quá thấp | Tăng heap JVM (`-Xmx2g` hoặc cao hơn) |
| Không có kết quả trả về | Token đoạn không được xử lý | Đảm bảo vòng `while` chạy tới khi `getNextChunkSearchToken()` trả về `null` |
| Hiệu suất tìm kiếm chậm | Chỉ mục chưa được tối ưu | Chạy `index.optimize()` sau khi thêm hàng loạt |

## Câu hỏi thường gặp

**H: Tìm kiếm dựa trên đoạn là gì?**  
Đ: Tìm kiếm dựa trên đoạn chia bộ dữ liệu thành các phần nhỏ hơn, cho phép truy vấn hiệu quả trên khối lượng dữ liệu lớn mà không cần tải toàn bộ tài liệu vào bộ nhớ.

**H: Làm sao cập nhật chỉ mục với các tệp mới?**  
Đ: Chỉ cần gọi `index.add()` với đường dẫn tới các tài liệu mới; chỉ mục sẽ tự động tích hợp chúng.

**H: GroupDocs.Search có hỗ trợ các định dạng tệp khác nhau không?**  
Đ: Có, nó hỗ trợ PDF, DOCX, XLSX, PPTX và nhiều định dạng phổ biến khác.

**H: Các nút thắt hiệu suất thường gặp là gì?**  
Đ: Hạn chế bộ nhớ và chỉ mục chưa được tối ưu là những nguyên nhân phổ biến; hãy phân bổ heap đủ và thường xuyên tối ưu chỉ mục.

**H: Tôi có thể tìm tài liệu hướng dẫn chi tiết ở đâu?**  
Đ: Truy cập [tài liệu chính thức của GroupDocs.Search](https://docs.groupdocs.com/search/java/) để xem các hướng dẫn sâu và tham chiếu API.

**H: Tìm kiếm dựa trên đoạn có hoạt động với PDF được mã hóa không?**  
Đ: Có, miễn là bạn cung cấp mật khẩu qua overload API thích hợp.

**H: Làm sao theo dõi tiến độ lập chỉ mục?**  
Đ: Sử dụng overload `Index.add()` trả về đối tượng `Progress` hoặc gắn vào các callback ghi log.

## Tài nguyên
- **Tài liệu**: [GroupDocs.Search cho Java Docs](https://docs.groupdocs.com/search/java/)  
- **Tham chiếu API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Tải xuống**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [Repository GroupDocs.Search trên GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Hỗ trợ miễn phí**: [Diễn đàn GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Giấy phép tạm thời**: [Nhận giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license)

---

**Cập nhật lần cuối:** 2026-02-21  
**Kiểm tra với:** GroupDocs.Search 25.4 cho Java  
**Tác giả:** GroupDocs  

---
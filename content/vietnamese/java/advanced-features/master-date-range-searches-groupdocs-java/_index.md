---
date: '2025-12-18'
description: Tìm hiểu cách triển khai tìm kiếm Java với định dạng ngày tùy chỉnh bằng
  GroupDocs.Search, bao gồm các truy vấn phạm vi ngày, mẫu tùy chỉnh và mẹo hiệu năng.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Định dạng ngày tùy chỉnh Java: Tìm kiếm phạm vi ngày với GroupDocs'
type: docs
url: /vi/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Định dạng ngày tùy chỉnh Java: Tìm kiếm khoảng ngày với GroupDocs

Việc tìm kiếm tài liệu theo ngày là một yêu cầu thường gặp—cho dù bạn đang xây dựng hệ thống lưu trữ, công cụ báo cáo tài chính, hoặc cổng thông tin quản lý nội dung. Trong hướng dẫn này, bạn sẽ học các kỹ thuật **custom date format java** bằng cách sử dụng GroupDocs.Search, bao gồm các truy vấn khoảng ngày, định nghĩa mẫu tùy chỉnh, và các mẹo để **optimize search performance**. Khi hoàn thành, bạn sẽ có thể cho phép người dùng truy xuất các bản ghi nằm trong bất kỳ khoảng thời gian nào, bất kể định dạng họ sử dụng.

## Câu trả lời nhanh
- **Lớp chính để tạo chỉ mục là gì?** `Index` từ gói `com.groupdocs.search`.  
- **Làm thế nào để định nghĩa mẫu ngày tùy chỉnh?** Sử dụng `DateFormat` với các đối tượng `DateFormatElement` và một ký tự phân tách.  
- **Tôi có thể tìm kiếm bằng truy vấn dạng văn bản không?** Có, cú pháp `daterange(start ~~ end)` hoạt động trực tiếp trong chuỗi truy vấn.  
- **Các tọa độ Maven cần thiết là gì?** `com.groupdocs:groupdocs-search:25.4` (hoặc mới hơn).  
- **Tôi có cần giấy phép cho việc phát triển không?** Bản dùng thử miễn phí hoặc giấy phép tạm thời đủ cho việc thử nghiệm; giấy phép thương mại cần thiết cho môi trường sản xuất.

## **custom date format java** là gì?
Một **custom date format java** cho biết GroupDocs.Search cách diễn giải các chuỗi ngày không tuân theo mẫu ISO mặc định (YYYY‑MM‑DD). Bằng cách định nghĩa mẫu riêng của bạn—chẳng hạn `MM/dd/yyyy` hoặc `dd‑MM‑yyyy`—bạn cho phép engine nhận diện các ngày được nhúng trong tài liệu sử dụng định dạng khu vực hoặc định dạng cũ.

## Tại sao nên sử dụng GroupDocs.Search cho các truy vấn khoảng ngày?
- **Tốc độ:** Tạo chỉ mục tích hợp giúp tra cứu O(log n).  
- **Linh hoạt:** Hỗ trợ tạo truy vấn dựa trên văn bản và dựa trên đối tượng.  
- **Hỗ trợ đa định dạng:** Xử lý PDF, Word, Excel, văn bản thuần và hơn thế nữa mà không cần mã bổ sung.  

## Cách **search documents by date** với GroupDocs.Search
Dưới đây bạn sẽ tìm thấy hướng dẫn từng bước giúp bạn thiết lập thư viện, tạo chỉ mục cho các tệp và thực hiện cả tìm kiếm khoảng ngày đơn giản và nâng cao.

### Yêu cầu trước
- Java 8 hoặc mới hơn đã được cài đặt.  
- Maven để quản lý phụ thuộc.  
- Có quyền truy cập vào giấy phép GroupDocs.Search (bản dùng thử hoặc tạm thời đủ cho việc phát triển).  

### Cài đặt GroupDocs.Search cho Java

#### Cài đặt bằng Maven
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

#### Tải trực tiếp
Hoặc, bạn có thể tải phiên bản mới nhất trực tiếp từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Khởi tạo và Cấu hình Cơ bản
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Tính năng 1: Tạo Truy vấn Tìm kiếm Khoảng ngày

### Sử dụng Truy vấn Dạng Văn bản
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Giải thích**: Cú pháp `daterange` yêu cầu ngày ở định dạng `YYYY‑MM‑DD`. Nó trả về tất cả các tài liệu có ngày đã được lập chỉ mục nằm trong khoảng thời gian này.

### Sử dụng Đối tượng Truy vấn
For programmatic control and custom parsing, build a `SearchQuery` object:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Giải thích**: `createDateRangeQuery` cho phép bạn cung cấp các đối tượng `java.util.Date`, mang lại sự linh hoạt hoàn toàn về múi giờ và xử lý theo vùng địa phương.

## Tính năng 2: Định nghĩa Mẫu **custom date format java**

### Đặt Định dạng Ngày Tùy chỉnh
Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Giải thích**: Bằng cách xóa các định dạng mặc định và thêm một `DateFormat` sử dụng `/` làm ký tự phân tách, engine hiện có thể hiểu các ngày viết dưới dạng `MM/dd/yyyy`. Điều này rất quan trọng cho việc **search documents by date** ở các khu vực ưu tiên ghi ngày theo thứ tự tháng‑đầu.

## Mẹo để **optimize search performance**
- **Index Incrementally**: Thêm các tệp mới vào chỉ mục hiện có thay vì xây dựng lại từ đầu.  
- **Prune Stale Data**: Thường xuyên loại bỏ các tài liệu không còn cần thiết.  
- **Adjust Memory Settings**: Tăng bộ nhớ heap JVM (`-Xmx`) khi làm việc với các chỉ mục lớn.  

## Các Vấn đề Thường gặp và Giải pháp
- **Date Parsing Errors**: Kiểm tra xem các chuỗi ngày trong tài liệu có khớp chính xác với mẫu tùy chỉnh bạn đã định nghĩa hay không.  
- **Missing Results**: Đảm bảo các trường đã lập chỉ mục chứa siêu dữ liệu ngày; nếu không, engine không thể khớp các truy vấn ngày.  
- **Index Access Exceptions**: Xác nhận rằng đường dẫn `indexFolder` có thể ghi được và không bị khóa bởi tiến trình khác.

## Ứng dụng Thực tiễn
1. **Archival Systems** – Truy xuất các bản ghi từ một khoảng thời gian lịch sử cụ thể.  
2. **Content Management** – Hỗ trợ các định dạng ngày khu vực như `dd/MM/yyyy` cho người dùng châu Âu.  
3. **Financial Software** – Lọc giao dịch theo quý tài chính hoặc năm một cách nhanh chóng.

## Kết luận
Bạn hiện đã có một bộ công cụ **custom date format java** hoàn chỉnh để xây dựng các tìm kiếm khoảng ngày mạnh mẽ với GroupDocs.Search. Áp dụng các mẫu này, tinh chỉnh hiệu suất, và ứng dụng của bạn sẽ cung cấp kết quả nhanh chóng, chính xác cho bất kỳ truy vấn thời gian nào.

## Câu hỏi Thường gặp

**Q: Sự khác biệt giữa truy vấn dạng văn bản và truy vấn dựa trên đối tượng là gì?**  
A: Dạng văn bản nhanh và dễ dùng nhưng giới hạn ở định dạng ISO mặc định; truy vấn dựa trên đối tượng cho phép bạn cung cấp các đối tượng `Date` và định dạng tùy chỉnh để có độ linh hoạt cao hơn.

**Q: Tôi có thể tìm kiếm nhiều khoảng ngày trong một truy vấn duy nhất không?**  
A: Có, kết hợp các mệnh đề `daterange` với các toán tử logic như `AND` hoặc `OR` để xây dựng truy vấn phức tạp.

**Q: Định dạng ngày tùy chỉnh có làm chậm quá trình tìm kiếm không?**  
A: Có một chút chi phí bổ sung cho việc phân tích, nhưng ảnh hưởng là không đáng kể đối với khối lượng công việc thông thường và được bù đắp bởi độ chính xác tăng lên.

**Q: GroupDocs.Search có phù hợp cho triển khai quy mô lớn không?**  
A: Chắc chắn. Với các chiến lược lập chỉ mục phù hợp và tinh chỉnh JVM, nó có thể mở rộng tới hàng triệu tài liệu.

**Q: Tôi có thể tìm thêm các ví dụ Java ở đâu?**  
A: Khám phá [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) để xem thêm các mẫu và triển khai các trường hợp sử dụng.

---

**Resources**

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)  

---

**Cập nhật lần cuối:** 2025-12-18  
**Kiểm thử với:** GroupDocs.Search Java 25.4  
**Tác giả:** GroupDocs  

---
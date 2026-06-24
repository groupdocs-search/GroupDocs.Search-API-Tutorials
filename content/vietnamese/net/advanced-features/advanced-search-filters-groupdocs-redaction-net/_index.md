---
date: '2026-04-02'
description: Tìm hiểu cách lọc theo phần mở rộng tệp và chỉ tìm các tệp txt bằng GroupDocs.Redaction
  cho .NET—nâng cao hiệu quả quản lý tài liệu.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Lọc theo phần mở rộng tệp trong .NET bằng GroupDocs.Redaction
type: docs
url: /vi/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Lọc theo phần mở rộng tệp trong .NET bằng GroupDocs.Redaction

Việc tìm kiếm trong một bộ sưu tập tệp lớn có thể gây choáng ngợp, đặc biệt khi bạn chỉ cần kết quả từ các loại tệp cụ thể. Trong hướng dẫn này, bạn sẽ khám phá **cách lọc theo phần mở rộng tệp** với GroupDocs.Redaction cho .NET, cho phép bạn tìm kiếm chỉ các tệp txt hoặc bất kỳ phần mở rộng nào bạn chọn. Chúng tôi sẽ hướng dẫn cách thiết lập cả bộ lọc theo loại tệp và bộ lọc dựa trên đường dẫn, để bạn có thể nhanh chóng xác định chính xác các tài liệu cần thiết.

## Câu trả lời nhanh
- **What does “filter by file extension” do?** Nó giới hạn việc tìm kiếm chỉ các tài liệu có phần mở rộng tệp phù hợp (ví dụ, *.txt).  
- **Why use GroupDocs.Redaction for this?** Nó cung cấp các API lọc tích hợp sẵn, nhanh chóng và dễ tích hợp.  
- **Do I need a license?** Bản dùng thử miễn phí đủ cho việc thử nghiệm; cần có giấy phép trả phí cho môi trường sản xuất.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Can I combine file‑type and path filters?** Có — áp dụng nhiều bộ lọc để tìm kiếm chính xác hơn.

## Những gì bạn sẽ học
- Cách **filter by file extension** để chỉ tìm kiếm các tệp văn bản.  
- Cách thiết lập **file path filters** để thu hẹp kết quả vào các thư mục hoặc mẫu đặt tên cụ thể.  
- Mẹo để giữ chỉ mục của bạn nhanh và tiết kiệm bộ nhớ.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **GroupDocs.Redaction Library** đã được cài đặt và tương thích với dự án .NET của bạn.  
- Một môi trường phát triển như Visual Studio hoặc VS Code.  
- Kiến thức cơ bản về C# và quen thuộc với cấu trúc dự án .NET.

## Cài đặt GroupDocs.Redaction cho .NET

Đầu tiên, thêm thư viện vào dự án của bạn.

**Sử dụng .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Sử dụng Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Hoặc tìm “GroupDocs.Redaction” trong giao diện NuGet Package Manager và cài đặt phiên bản mới nhất.

### Nhận giấy phép

Bạn có thể bắt đầu với bản dùng thử miễn phí hoặc yêu cầu giấy phép tạm thời. Đối với các dự án dài hạn, mua giấy phép từ trang chính thức.

### Khởi tạo cơ bản

Sau khi gói đã được cài đặt, tạo một chỉ mục để lưu trữ các tham chiếu tới tài liệu của bạn:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Hướng dẫn triển khai

### Tính năng 1: Đặt bộ lọc cho tài liệu văn bản (.txt)

#### Cách lọc theo phần mở rộng tệp cho tài liệu văn bản

1. **Xác định chỉ mục và thư mục tài liệu**  
   Đặt các đường dẫn nơi các tệp nguồn của bạn nằm:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Tạo một Index**  
   Tải tất cả các tệp từ thư mục nguồn vào chỉ mục:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Cấu hình Search Options với bộ lọc phần mở rộng tệp**  
   Yêu cầu engine chỉ xem xét các tệp *.txt:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Thực hiện tìm kiếm**  
   Chạy một truy vấn; bộ lọc đảm bảo các tệp không phải văn bản bị bỏ qua:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Giải thích*: Phương thức `Search` trả về các kết quả phù hợp với bộ lọc, giảm đáng kể nhiễu và cải thiện hiệu suất.

### Tính năng 2: Bộ lọc FilePath

#### Tại sao sử dụng bộ lọc đường dẫn tệp?

Đôi khi bạn cần giới hạn tìm kiếm trong một thư mục bộ phận cụ thể hoặc một tập hợp các tệp có cùng quy tắc đặt tên. Bộ lọc đường dẫn cho phép bạn làm điều đó.

1. **Xác định chỉ mục và thư mục tài liệu**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Tạo một Index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Cấu hình Search Options với biểu thức chính quy dựa trên đường dẫn**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Biểu thức chính quy này khớp với bất kỳ tệp nào có đường dẫn đầy đủ chứa từ “Lorem”, cho phép bạn nhắm mục tiêu các thư mục con cụ thể.

4. **Thực thi tìm kiếm dựa trên đường dẫn**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Ứng dụng thực tế
- **Legal Document Management** – Nhanh chóng xác định các hợp đồng liên quan được lưu dưới dạng tệp văn bản thuần.  
- **Academic Research** – Lấy chỉ các ghi chú nghiên cứu *.txt thuộc một thư mục dự án cụ thể.  
- **Corporate Reporting** – Lọc báo cáo nội bộ theo đường dẫn bộ phận (ví dụ, `/Finance/2025/`).  

## Các cân nhắc về hiệu suất
- Chỉ lập chỉ mục các loại tài liệu bạn thực sự cần; các tệp không cần thiết làm tăng kích thước chỉ mục và thời gian tìm kiếm.  
- Giữ chỉ mục luôn cập nhật bằng công việc lên lịch gọi `index.Add()` cho các tệp mới hoặc đã thay đổi.  
- Sử dụng các biểu thức chính quy đơn giản; các mẫu quá phức tạp có thể làm chậm công cụ tìm kiếm.  
- Giải phóng các đối tượng `Index` khi không còn cần thiết để giải phóng bộ nhớ.

## Kết luận
Bạn hiện đã biết cách **filter by file extension** và áp dụng **file path filters** bằng GroupDocs.Redaction cho .NET. Những kỹ thuật này cung cấp cho bạn khả năng kiểm soát chi tiết các bộ sưu tập tài liệu lớn, làm cho việc tìm kiếm nhanh hơn và có liên quan hơn. Tiếp theo, hãy thử kết hợp nhiều bộ lọc hoặc tích hợp tìm kiếm vào quy trình làm việc của ứng dụng lớn hơn.

## Phần Câu hỏi thường gặp

**Q1: Tôi có thể lọc các tài liệu khác ngoài tệp văn bản không?**  
A1: Có, GroupDocs.Redaction hỗ trợ nhiều định dạng. Thay đổi đối số trong `CreateFileExtension` thành phần mở rộng mong muốn (ví dụ, ".pdf").

**Q2: Làm thế nào để tôi cập nhật chỉ mục tìm kiếm thường xuyên?**  
A2: Lên lịch một dịch vụ nền hoặc một cron job để chạy `index.Add()` trên các thư mục bạn muốn duy trì cập nhật.

**Q3: Có ảnh hưởng đến hiệu suất khi lọc theo đường dẫn tệp không?**  
A3: Các biểu thức chính quy được tối ưu đúng cách có ảnh hưởng tối thiểu, nhưng luôn thực hiện benchmark với bộ dữ liệu của bạn.

**Q4: Tôi có thể kết hợp nhiều bộ lọc để tìm kiếm chi tiết hơn không?**  
A4: Chắc chắn. Bạn có thể xâu chuỗi các bộ lọc hoặc tạo bộ lọc tổng hợp để đồng thời nhắm mục tiêu cả loại tệp và đường dẫn.

**Q5: Tôi có thể tìm thêm tài nguyên về GroupDocs.Redaction ở đâu?**  
A5: Tham khảo tài liệu chính thức tại [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) để có hướng dẫn chi tiết và tham chiếu API.

## Các câu hỏi thường gặp

**Q: `SearchDocumentFilter` có hoạt động với các tệp được mã hóa không?**  
A: Bộ lọc tự nó hoạt động trên siêu dữ liệu tệp, vì vậy các tệp được mã hóa vẫn sẽ được lập chỉ mục nếu bạn cung cấp thông tin xác thực giải mã cần thiết trong quá trình lập chỉ mục.

**Q: Tôi có thể sử dụng ký tự đại diện thay vì biểu thức chính quy cho việc lọc đường dẫn không?**  
A: API hiện tại yêu cầu một biểu thức chính quy, nhưng bạn có thể mô phỏng các ký tự đại diện đơn giản (ví dụ, `.*` cho bất kỳ ký tự nào).

**Q: Chỉ mục có thể lớn đến mức nào trước khi tôi cần xem xét sharding?**  
A: Các chỉ mục có kích thước hàng trăm gigabyte có thể hưởng lợi từ việc chia thành nhiều chỉ mục logic; hãy kiểm tra hiệu suất khi bộ sưu tập của bạn tăng lên.

**Q: Có các phương thức tích hợp để xóa tài liệu khỏi chỉ mục không?**  
A: Có — gọi `index.Delete(documentId)` hoặc `index.DeleteAll()` để quản lý các mục lỗi thời.

**Q: Có cách nào để xem trước kết quả tìm kiếm trước khi tải toàn bộ tài liệu không?**  
A: Đối tượng `SearchResult` bao gồm thông tin đoạn trích mà bạn có thể hiển thị trong UI mà không cần mở toàn bộ tệp.

## Tài nguyên
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Cập nhật lần cuối:** 2026-04-02  
**Được kiểm tra với:** GroupDocs.Redaction 23.12 for .NET  
**Tác giả:** GroupDocs
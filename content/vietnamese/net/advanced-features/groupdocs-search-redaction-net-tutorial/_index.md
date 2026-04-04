---
date: '2026-04-04'
description: Học cách tìm kiếm tài liệu pháp lý và quản lý chỉ mục bằng GroupDocs.Search,
  và tích hợp việc che dấu cho hồ sơ y tế bằng GroupDocs.Redaction trong .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Tìm kiếm tài liệu pháp lý với GroupDocs Search & Redaction cho .NET
type: docs
url: /vi/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Tìm kiếm tài liệu pháp lý với GroupDocs Search & Redaction trong .NET

Trong môi trường dựa trên dữ liệu ngày nay, **tìm kiếm tài liệu pháp lý** nhanh chóng và an toàn là một yêu cầu quan trọng đối với bất kỳ tổ chức nào. Cho dù bạn đang xử lý hợp đồng, hồ sơ tòa án, hoặc báo cáo tuân thủ, GroupDocs.Search cung cấp cho bạn một chỉ mục nhanh, có khả năng mở rộng, trong khi GroupDocs.Redaction đảm bảo thông tin nhạy cảm được ẩn. Hướng dẫn này sẽ chỉ cho bạn cách thiết lập một chỉ mục có thể tìm kiếm, thêm tài liệu từ nhiều thư mục, và cấu hình việc che dấu để bạn có thể an toàn tìm kiếm hồ sơ y tế và các tệp tin bảo mật khác.

## Câu trả lời nhanh
- **GroupDocs.Search làm gì?** Nó tạo một chỉ mục có thể tìm kiếm toàn văn cho một loạt các định dạng tài liệu.  
- **Tôi có thể che dấu thông tin trước khi tìm kiếm không?** Có – sử dụng GroupDocs.Redaction để che khuất hoặc loại bỏ dữ liệu nhạy cảm.  
- **Làm thế nào để thêm tài liệu vào chỉ mục?** Gọi `index.Add("folderPath")` cho mỗi thư mục bạn muốn bao gồm.  
- **Các loại tệp nào được hỗ trợ?** PDF, DOCX, PPTX, TXT và nhiều hơn nữa.  
- **Tôi có cần giấy phép cho môi trường sản xuất không?** Có sẵn bản dùng thử tạm thời; giấy phép vĩnh viễn là bắt buộc cho việc sử dụng thương mại.

## Yêu cầu trước
- .NET Core SDK (3.1 hoặc mới hơn) đã được cài đặt.
- Visual Studio Code, Visual Studio, hoặc IDE khác hỗ trợ .NET.
- Kiến thức cơ bản về lập trình C#.

### Nhận giấy phép
Bạn có thể bắt đầu với bản dùng thử miễn phí của cả hai thư viện. Đối với việc sử dụng kéo dài, hãy cân nhắc mua giấy phép tạm thời hoặc mua bản đầy đủ từ [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

## Cài đặt các gói cần thiết

**Cài đặt GroupDocs.Search:**  
Sử dụng **.NET CLI**, chạy:
```bash
dotnet add package GroupDocs.Search
```
Hoặc, sử dụng Package Manager Console trong Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**Cài đặt GroupDocs.Redaction:**  
- Sử dụng .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Hoặc, thông qua Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Truy cập giao diện NuGet Package Manager UI và tìm kiếm "GroupDocs.Redaction" để cài đặt nếu bạn thích giao diện đồ họa.

## Cấu hình cài đặt Redactor
Trước khi bạn bắt đầu che dấu, bạn có thể muốn điều chỉnh hành vi của redactor (ví dụ: đặt màu che dấu hoặc định nghĩa các mẫu tùy chỉnh). Đoạn mã sau đây hiển thị khởi tạo cơ bản:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Mẹo chuyên nghiệp:** Điều chỉnh `redactorSettings` để phù hợp với chính sách tuân thủ của tổ chức bạn (ví dụ: thay thế văn bản bằng các hộp đen, áp dụng OCR trước khi che dấu, v.v.).

## Hướng dẫn triển khai

### Cách tìm kiếm tài liệu pháp lý?
Tạo một chỉ mục có thể tìm kiếm là nền tảng cho việc truy xuất nhanh các tài liệu pháp lý. GroupDocs.Search cho phép bạn chỉ định bất kỳ thư mục nào, xây dựng một chỉ mục, và sau đó thực hiện các truy vấn phức tạp trên hàng ngàn tệp.

### Cách thêm tài liệu vào chỉ mục
Thêm tài liệu rất đơn giản—chỉ cần chỉ định thư viện tới các thư mục chứa tệp của bạn. Bạn có thể thêm nhiều thư mục, điều này hữu ích khi tập hợp pháp lý của bạn được phân tán ở các vị trí khác nhau.

#### Tạo và quản lý một chỉ mục
**Tổng quan:**  
Tạo một chỉ mục là bước đầu tiên hướng tới các hoạt động tìm kiếm tài liệu hiệu quả. GroupDocs.Search cho phép bạn tạo một chỉ mục có thể tìm kiếm trong bất kỳ thư mục nào bạn chọn, giúp truy xuất tài liệu nhanh chóng.

##### Bước 1: Tạo chỉ mục
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Giải thích:* `Index` khởi tạo một chỉ mục tìm kiếm tại thư mục được chỉ định. Đảm bảo đường dẫn phản ánh cấu trúc thư mục dự án của bạn.

##### Bước 2: Thêm tài liệu vào chỉ mục
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Giải thích:* Phương thức `Add` quét thư mục được cung cấp và bao gồm mọi tài liệu được hỗ trợ vào chỉ mục. Sử dụng điều này để **thêm tài liệu vào chỉ mục** từ nhiều nguồn, chẳng hạn như hợp đồng, hồ sơ vụ án, hoặc hồ sơ y tế.

### Lấy và hiển thị báo cáo lập chỉ mục
**Tổng quan:**  
Báo cáo lập chỉ mục cung cấp cho bạn cái nhìn về số lượng tài liệu đã được xử lý, tổng số từ, và kích thước lưu trữ—các chỉ số thiết yếu để tối ưu hiệu năng.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Giải thích:* `GetIndexingReports` trả về một mảng các báo cáo chi tiết quá trình lập chỉ mục, giúp bạn giám sát và tối ưu hiệu năng.

## Ứng dụng thực tiễn
1. **Quản lý tài liệu pháp lý:** Tự động lập chỉ mục các hồ sơ vụ án để truy xuất ngay lập tức các luật, bản tóm tắt và phán quyết.  
2. **Hệ thống hồ sơ y tế:** Tìm kiếm hồ sơ bệnh nhân trong khi bảo vệ quyền riêng tư bằng cách sử dụng GroupDocs.Redaction để che dấu PHI.  
3. **Cổng thông tin nhân sự doanh nghiệp:** Kết hợp các tệp nhân viên có thể tìm kiếm với việc che dấu để bảo vệ dữ liệu cá nhân.

## Các cân nhắc về hiệu năng
- **Tối ưu kích thước chỉ mục:** Thường xuyên loại bỏ các mục lỗi thời và xây dựng lại chỉ mục để giữ nó gọn nhẹ.  
- **Quản lý bộ nhớ:** Tận dụng bộ thu gom rác của .NET; giải phóng các đối tượng `Index` khi không còn cần thiết.  
- **Thực hành tốt về khả năng mở rộng:** Lưu trữ chỉ mục trên ổ SSD nhanh và cân nhắc phân chia các tập dữ liệu lớn thành nhiều chỉ mục.

## Câu hỏi thường gặp

**Q: Những mục đích chính của GroupDocs.Search là gì?**  
A: Nó lý tưởng để tạo các chỉ mục có thể tìm kiếm từ các bộ sưu tập tài liệu lớn, cho phép truy xuất nhanh các tệp pháp lý và y tế.

**Q: GroupDocs.Redaction đảm bảo bảo mật dữ liệu như thế nào?**  
A: Nó cho phép bạn định nghĩa các mẫu che dấu để loại bỏ hoặc che khuất vĩnh viễn thông tin nhạy cảm trước khi tài liệu được lập chỉ mục hoặc chia sẻ.

**Q: Tôi có thể sử dụng các thư viện này trong môi trường đám mây không?**  
A: Có—cả hai thư viện đều hoạt động trên Azure, AWS, hoặc bất kỳ triển khai .NET container nào với giấy phép phù hợp.

**Q: Các định dạng tệp nào được GroupDocs.Search hỗ trợ?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML và nhiều định dạng doanh nghiệp khác.

**Q: Làm thế nào để khắc phục lỗi lập chỉ mục?**  
A: Xác minh đường dẫn thư mục, kiểm tra quyền truy cập tệp, và xem lại đầu ra console từ `IndexingReport` để biết các mã lỗi cụ thể.

## Tài nguyên
- **Tài liệu:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **Tham chiếu API:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Tải xuống:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Hỗ trợ miễn phí:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Giấy phép tạm thời:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Cập nhật lần cuối:** 2026-04-04  
**Kiểm tra với:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Tác giả:** GroupDocs
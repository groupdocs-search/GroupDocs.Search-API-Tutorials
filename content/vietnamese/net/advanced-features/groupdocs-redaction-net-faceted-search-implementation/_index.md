---
date: '2026-04-02'
description: Tìm hiểu cách tạo chỉ mục tìm kiếm GroupDocs và thêm tài liệu vào chỉ
  mục trong khi triển khai tìm kiếm phân lớp bằng cách sử dụng GroupDocs.Search và
  GroupDocs.Redaction trong .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Tạo chỉ mục tìm kiếm GroupDocs với Redaction và Tìm kiếm phân lớp .NET
type: docs
url: /vi/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Tạo Chỉ mục Tìm kiếm GroupDocs với Redaction .NET Tìm kiếm Phân lớp

Trong các ứng dụng hiện đại, **việc tạo chỉ mục tìm kiếm với GroupDocs** là cần thiết để truy xuất tài liệu nhanh chóng và chính xác. Dù bạn đang xử lý hợp đồng pháp lý, danh mục sản phẩm, hay cơ sở kiến thức lớn, một chỉ mục được xây dựng tốt cho phép bạn **thêm tài liệu vào chỉ mục** và thực hiện các tìm kiếm phân lớp mạnh mẽ trong vài giây. Hướng dẫn này sẽ đưa bạn qua toàn bộ quá trình — từ việc thiết lập GroupDocs.Redaction đến việc tạo các truy vấn phân lớp đơn giản và phức tạp — để bạn có thể cung cấp trải nghiệm tìm kiếm đáp ứng trong các dự án .NET của mình.

## Câu trả lời nhanh
- **Mục đích chính là gì?** Để tạo một chỉ mục tìm kiếm với GroupDocs và bật tìm kiếm phân lớp.  
- **Các thư viện cần thiết là gì?** GroupDocs.Redaction và GroupDocs.Search cho .NET.  
- **Làm thế nào để thêm tài liệu vào chỉ mục?** Sử dụng `index.Add(documentsFolder)` sau khi khởi tạo chỉ mục.  
- **Tôi có thể chạy các truy vấn phức tạp không?** Có, kết hợp các truy vấn đối tượng với các toán tử logic để lọc nâng cao.  
- **Cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.

## Tìm kiếm phân lớp là gì và tại sao nên sử dụng với GroupDocs?
Tìm kiếm phân lớp cho phép người dùng tinh chỉnh kết quả bằng cách áp dụng nhiều bộ lọc—như danh mục, ngày, hoặc tác giả—cùng lúc. Khi kết hợp với **GroupDocs.Redaction**, bạn có được nội dung an toàn, có thể tìm kiếm được và tuân thủ các quy tắc che dấu, rất phù hợp cho các môi trường yêu cầu tuân thủ nghiêm ngặt.

## Các yêu cầu trước

### Thư viện, Phiên bản và Phụ thuộc cần thiết
- **GroupDocs.Redaction .NET** – phiên bản ổn định mới nhất.  
- **GroupDocs.Search .NET** – hoạt động liền mạch với Redaction để lập chỉ mục.

### Yêu cầu thiết lập môi trường
- **IDE**: Visual Studio 2019 hoặc mới hơn.  
- **Framework**: .NET Core 3.1, .NET 5, hoặc .NET 6.  
- **Tương thích hệ điều hành**: Windows, Linux, macOS.

### Kiến thức tiên quyết
Kỹ năng C# cơ bản và hiểu biết tổng quan về các khái niệm tìm kiếm phân lớp sẽ hữu ích, nhưng hướng dẫn từng bước cũng thân thiện với người mới bắt đầu.

## Thiết lập GroupDocs.Redaction cho .NET

### Thông tin Cài đặt
Bạn có thể thêm gói GroupDocs.Redaction bằng bất kỳ phương pháp sau:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Tìm kiếm "GroupDocs.Redaction" và cài đặt phiên bản mới nhất.

### Các bước nhận giấy phép
Để mở khóa tất cả tính năng, bắt đầu với bản dùng thử miễn phí hoặc nhận giấy phép vĩnh viễn:

1. Truy cập [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) để khám phá các tùy chọn cấp phép.  
2. Làm theo hướng dẫn trên màn hình để nhận tệp giấy phép dùng thử hoặc đã mua.

### Khởi tạo và Cấu hình Cơ bản
Sau khi gói được cài đặt, khởi tạo Redactor trong ứng dụng của bạn:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Cách tạo chỉ mục tìm kiếm groupdocs

Dưới đây chúng tôi chia triển khai thành hai phần: **Simple Faceted Search** và **Complex Query**. Mỗi phần cho thấy cách **tạo một chỉ mục tìm kiếm groupdocs**, thêm tài liệu và chạy các truy vấn.

### Tính năng 1: Tìm kiếm Phân lớp Đơn giản

**Tổng quan**  
Tìm kiếm phân lớp cho phép người dùng thu hẹp kết quả bằng cách chọn nhiều tiêu chí. Phần này trình bày cách tiếp cận đơn giản sử dụng GroupDocs.Search.

#### Bước 1: Xác định Thư mục Chỉ mục và Tài liệu
Thiết lập đường dẫn thư mục nơi chỉ mục sẽ được lưu và nơi tài liệu nguồn của bạn nằm.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Bước 2: Tạo Chỉ mục
Khởi tạo chỉ mục tìm kiếm trong thư mục bạn đã xác định.

```csharp
Index index = new Index(indexFolder);
```

#### Bước 3: Thêm Tài liệu vào Chỉ mục
Tải tài liệu của bạn để chúng có thể tìm kiếm được.

```csharp
index.Add(documentsFolder);
```

#### Bước 4: Thực hiện Tìm kiếm Truy vấn Văn bản
Chạy một truy vấn văn bản cơ bản trên trường **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Bước 5: Thực hiện Tìm kiếm Truy vấn Đối tượng
Sử dụng các truy vấn hướng đối tượng để kiểm soát chi tiết hơn.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Tính năng 2: Truy vấn Phức tạp

**Tổng quan**  
Khi bạn cần kết hợp nhiều bộ lọc—như mẫu tên tệp và khớp cụm từ—bạn có thể xây dựng một truy vấn phức tạp bằng cách sử dụng các toán tử logic.

#### Bước 1: Xác định Thư mục Chỉ mục và Tài liệu
Tái sử dụng cùng cấu trúc thư mục cho kịch bản nâng cao hơn.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Bước 2: Tạo Chỉ mục và Thêm Tài liệu
(Xem các bước 2‑3 từ ví dụ đơn giản; chúng vẫn giống như cũ.)

#### Bước 3: Thực hiện Tìm kiếm Truy vấn Văn bản
Chạy một truy vấn văn bản kết hợp mà pha trộn tiêu chí tên tệp và nội dung.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Bước 4: Xây dựng và Thực hiện Truy vấn Đối tượng
Xây dựng cùng logic này bằng mã.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Tiếp tục kết hợp các cụm từ, phạm vi và toán tử boolean để phù hợp với quy tắc kinh doanh chính xác của bạn.

## Ứng dụng Thực tiễn

1. **Nền tảng Thương mại điện tử** – Lọc sản phẩm theo danh mục, giá và đánh giá.  
2. **Hệ thống Quản lý Tài liệu** – Tìm hợp đồng theo tác giả, ngày hoặc mức độ bảo mật.  
3. **Cổng nội dung** – Cho phép người đọc lọc sâu theo thẻ, chủ đề và ngày xuất bản.

## Các yếu tố về Hiệu suất

- **Làm mới Chỉ mục**: Thường xuyên lập chỉ mục lại các tệp mới hoặc đã cập nhật để duy trì tốc độ tìm kiếm.  
- **Quản lý Bộ nhớ**: Giải phóng các đối tượng `Index` khi hoàn thành, đặc biệt với bộ dữ liệu lớn.  
- **Lập chỉ mục Bất đồng bộ**: Sử dụng `Task.Run` hoặc dịch vụ nền để tránh đóng băng giao diện người dùng trong quá trình lập chỉ mục nặng.

## Các vấn đề Thường gặp và Giải pháp

| Vấn đề | Giải pháp |
|-------|----------|
| **Không tìm thấy Chỉ mục** | Xác minh đường dẫn `indexFolder` và đảm bảo thư mục có quyền ghi. |
| **Không có kết quả trả về** | Kiểm tra các trường bạn truy vấn (ví dụ: `Content`, `Filename`) đã được lập chỉ mục. |
| **Lỗi hết bộ nhớ** | Xử lý tài liệu theo lô và cân nhắc tăng kích thước heap của .NET GC. |

## Câu hỏi Thường gặp

**Q: Tìm kiếm phân lớp là gì?**  
A: Tìm kiếm phân lớp cho phép người dùng tinh chỉnh kết quả bằng cách sử dụng nhiều bộ lọc độc lập như danh mục, ngày hoặc tác giả.

**Q: Làm thế nào để xử lý bộ dữ liệu lớn với GroupDocs.Search?**  
A: Sử dụng lập chỉ mục tăng dần, xử lý theo lô và các hoạt động bất đồng bộ để giữ mức sử dụng bộ nhớ thấp và hiệu suất cao.

**Q: Tôi có thể tích hợp các chức năng của GroupDocs vào các ứng dụng .NET hiện có không?**  
A: Có, các thư viện được thiết kế để tích hợp liền mạch với bất kỳ dự án .NET nào.

**Q: Một số vấn đề thường gặp với tìm kiếm phân lớp là gì?**  
A: Cú pháp truy vấn phức tạp và việc đảm bảo tất cả các trường liên quan được lập chỉ mục là những thách thức điển hình; việc kiểm tra kỹ lưỡng và bảo trì chỉ mục sẽ giảm thiểu chúng.

**Q: Làm thế nào để nhận giấy phép tạm thời cho GroupDocs?**  
A: Truy cập [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) để đăng ký giấy phép dùng thử mở khóa toàn bộ chức năng trong quá trình đánh giá.

## Tài nguyên
- **Tài liệu**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Tham khảo API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Cập nhật lần cuối:** 2026-04-02  
**Kiểm thử với:** GroupDocs.Redaction 23.12 cho .NET, GroupDocs.Search 23.12 cho .NET  
**Tác giả:** GroupDocs
---
date: '2026-04-21'
description: Tìm hiểu cách lọc tệp bằng GroupDocs.Redaction cho .NET, bao gồm lọc
  theo ngày tạo, kích thước tệp, ngày chỉnh sửa và cách áp dụng bộ lọc NOT.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Cách lọc tệp với GroupDocs.Redaction cho .NET
type: docs
url: /vi/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Cách lọc tệp với GroupDocs.Redaction cho .NET

Trong môi trường kỹ thuật số ngày càng nhanh chóng hiện nay, **cách lọc tệp** một cách hiệu quả có thể quyết định năng suất của bạn. Cho dù bạn cần tách riêng các tài liệu theo phần mở rộng, ngày tạo, kích thước hoặc ngày sửa đổi, một chiến lược lọc hợp lý sẽ tiết kiệm thời gian, giảm chi phí lưu trữ và giữ cho chỉ mục tìm kiếm của bạn gọn gàng. Trong hướng dẫn này, chúng tôi sẽ trình bày các ví dụ thực tế sử dụng GroupDocs.Redaction cho .NET, cho bạn thấy chính xác cách lọc tệp để đáp ứng các nhu cầu kinh doanh phổ biến.

## Câu trả lời nhanh
- **Thư viện tôi cần là gì?** GroupDocs.Redaction cho .NET (cài đặt qua NuGet).  
- **Tôi có thể lọc theo ngày tạo không?** Có – sử dụng `CreateCreationTimeRange`.  
- **Làm thế nào để loại trừ một số loại?** Áp dụng bộ lọc NOT với `DocumentFilter.CreateNot`.  
- **Có hỗ trợ lọc theo kích thước tệp không?** Chắc chắn, qua `CreateFileLengthRange` hoặc các giới hạn trên/dưới.  
- **Tôi có cần giấy phép không?** Cần giấy phép dùng thử hoặc đầy đủ cho môi trường sản xuất.

## Lọc tệp với GroupDocs.Redaction là gì?
Lọc tệp cho phép bạn chỉ định cho công cụ lập chỉ mục những tài liệu nào sẽ được bao gồm hoặc bỏ qua dựa trên siêu dữ liệu như phần mở rộng, ngày tháng, mẫu đường dẫn hoặc kích thước. Bằng cách định nghĩa các quy tắc `DocumentFilter` chính xác, bạn giữ cho chỉ mục của mình gọn nhẹ và các tìm kiếm nhanh chóng.

## Tại sao nên sử dụng GroupDocs.Redaction cho .NET?
- **Trợ giúp lọc tích hợp** – không cần viết mã hệ thống tệp tùy chỉnh.  
- **Toán tử logic** – kết hợp nhiều tiêu chí với AND, OR và NOT.  
- **Tối ưu hiệu năng** – bộ lọc được áp dụng trong quá trình lập chỉ mục, không phải sau đó.  
- **Đa nền tảng** – hoạt động với .NET Framework, .NET Core và .NET 5/6+.

## Yêu cầu trước
- .NET Framework 4.6+ hoặc .NET Core 3.1+ đã được cài đặt.  
- Visual Studio hoặc IDE C# ưa thích của bạn.  
- Kiến thức cơ bản về C#.

### Thư viện cần thiết & Cài đặt
Install the NuGet package using your preferred method:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Mẹo:** Sau khi cài đặt, thêm tệp giấy phép của bạn vào thư mục gốc của dự án và gọi `License.SetLicense("license-file-path")` trước khi tạo bất kỳ đối tượng Redactor hoặc Index nào.

## Cài đặt GroupDocs.Redaction cho .NET

First, create a `Redactor` instance that points to the document you want to work with:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Tại sao điều này quan trọng:** Khởi tạo Redactor đảm bảo thư viện sẵn sàng áp dụng bộ lọc và quy tắc che dấu sau này trong quy trình làm việc.

## Cách lọc tệp theo phần mở rộng

Lọc theo phần mở rộng tệp là cách phổ biến nhất để thu hẹp tập hợp tài liệu. Dưới đây chúng tôi chỉ giữ các tệp FB2, EPUB và TXT.

### Lọc theo phần mở rộng tệp

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách áp dụng bộ lọc NOT để loại trừ các loại không mong muốn

Nếu bạn cần **áp dụng bộ lọc NOT** — ví dụ, loại trừ các tệp HTML và PDF — hãy sử dụng `CreateNot`.

### Loại trừ các tệp HTM, HTML và PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách lọc tệp theo ngày tạo

Khi bạn cần **lọc theo ngày tạo**, hãy chỉ định `DateTime` bắt đầu và kết thúc.

### Lọc theo khoảng ngày tạo

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách lọc tệp theo ngày sửa đổi

Tương tự như ngày tạo, bạn có thể giới hạn kết quả cho các tệp đã sửa đổi trước một thời điểm nhất định.

### Lọc theo ngày sửa đổi

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách lọc tệp theo đường dẫn bằng biểu thức chính quy

Nếu cấu trúc thư mục của bạn tuân theo quy ước đặt tên, một regex có thể nhắm mục tiêu vào các đường dẫn cụ thể.

### Lọc theo mẫu đường dẫn tệp

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách lọc tệp theo kích thước

Kiểm soát kích thước tài liệu là điều cần thiết khi làm việc với giới hạn băng thông hoặc lưu trữ.

### Lọc theo kích thước tệp (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách kết hợp nhiều điều kiện với AND

Khi bạn cần **cách lọc tệp** bằng cách sử dụng nhiều tiêu chí cùng lúc, hãy kết hợp chúng với `CreateAnd`.

### Ví dụ AND logic

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Cách kết hợp nhiều điều kiện với OR

Sử dụng `CreateOr` khi bất kỳ một trong số các quy tắc nào cũng có thể đáp ứng.

### Ví dụ OR logic

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Các vấn đề thường gặp và giải pháp
- **Bộ lọc không được áp dụng:** Đảm bảo bạn gán `settings.DocumentFilter` **trước** khi tạo đối tượng `Index`.  
- **Các tệp không mong muốn xuất hiện:** Kiểm tra lại phần mở rộng tệp có bao gồm dấu chấm đầu (`.txt`).  
- **Giảm hiệu năng:** Kết hợp các bộ lọc với AND để giảm số lượng tệp được quét sớm trong quy trình lập chỉ mục.  
- **Lỗi regex:** Escape các ký tự đặc biệt trong mẫu đường dẫn của bạn hoặc sử dụng `RegexOptions.IgnoreCase` cho các khớp không phân biệt chữ hoa chữ thường.

## Câu hỏi thường gặp

**Q: Tôi có thể kết hợp bộ lọc NOT với bộ lọc AND không?**  
A: Có. Đầu tiên xây dựng bộ lọc NOT (`DocumentFilter.CreateNot`) rồi bao gồm nó như một trong các đối số cho `DocumentFilter.CreateAnd`.

**Q: Làm thế nào để lọc các tệp lớn hơn 10 MB?**  
A: Sử dụng `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` để chỉ bao gồm các tệp vượt quá kích thước đó.

**Q: Có thể lọc đồng thời theo ngày tạo và ngày sửa đổi không?**  
A: Chắc chắn. Tạo mỗi bộ lọc riêng biệt và kết hợp chúng với `CreateAnd`.

**Q: Các bộ lọc này có hoạt động với đường dẫn lưu trữ đám mây không?**  
A: Các bộ lọc hoạt động trên hệ thống tệp cục bộ. Đối với nguồn đám mây, tải tệp về một thư mục tạm trước, sau đó áp dụng các bộ lọc tương tự.

**Q: Thay đổi bộ lọc có yêu cầu tái lập chỉ mục không?**  
A: Có. Các bộ lọc được đánh giá khi bạn gọi `index.Add`. Thay đổi bộ lọc có nghĩa là bạn cần xây dựng lại chỉ mục để phản ánh tiêu chí mới.

## Kết luận

Bằng cách nắm vững **cách lọc tệp** với GroupDocs.Redaction cho .NET—cho dù là theo phần mở rộng, ngày tạo, ngày sửa đổi, kích thước tệp, hoặc sử dụng logic NOT—bạn có thể tối ưu hóa quản lý tài liệu, giữ cho chỉ mục hoạt động hiệu quả và tập trung vào nội dung thực sự quan trọng. Hãy thử nghiệm các toán tử logic để tùy chỉnh việc lọc theo quy tắc kinh doanh chính xác của bạn, và bạn sẽ thấy ngay lợi ích về tốc độ và hiệu quả lưu trữ.

---

**Cập nhật lần cuối:** 2026-04-21  
**Kiểm tra với:** GroupDocs.Redaction 24.11 cho .NET  
**Tác giả:** GroupDocs
---
date: '2026-06-12'
description: Tìm hiểu cách tìm kiếm và che đậy tài liệu trong .NET với GroupDocs.Search
  và GroupDocs.Redaction, tối ưu hiệu suất tìm kiếm và xử lý lỗi lập chỉ mục.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Cách Tìm Kiếm và Che Đậy Tài Liệu trong .NET Sử Dụng GroupDocs.Search và GroupDocs.Redaction
type: docs
url: /vi/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Tìm kiếm và Che dấu Tài liệu trong .NET với GroupDocs.Search & GroupDocs.Redaction

Trong môi trường doanh nghiệp hiện đại, khả năng **search and redact** là cần thiết để bảo vệ thông tin nhạy cảm đồng thời giữ cho tài liệu dễ dàng được tìm kiếm. Hướng dẫn này sẽ chỉ cho bạn cách xây dựng một giải pháp .NET mạnh mẽ kết hợp GroupDocs.Search để tìm kiếm toàn văn nhanh chóng với GroupDocs.Redaction để loại bỏ dữ liệu bí mật một cách an toàn. Khi kết thúc, bạn sẽ biết cách thiết lập các thư viện, tạo một bộ phân đoạn văn bản tùy chỉnh, thực hiện các tìm kiếm hiệu năng cao và áp dụng việc che dấu một cách an toàn.

## Câu trả lời nhanh
- **“search and redact” có nghĩa là gì?** Nó có nghĩa là tìm văn bản trong tài liệu và che dấu vĩnh viễn.  
- **Cần những thư viện nào?** GroupDocs.Search và GroupDocs.Redaction cho .NET.  
- **Tôi có thể xử lý nội dung đa ngôn ngữ không?** Có — sử dụng bộ phân đoạn văn bản tùy chỉnh để tách từ đúng cách.  
- **Làm thế nào để cải thiện tốc độ tìm kiếm?** Tạo chỉ mục một lần, tái sử dụng chỉ mục, và bật cài đặt `optimize search performance`.  
- **Nếu việc tạo chỉ mục thất bại thì sao?** Thực hiện theo hướng dẫn “handle indexing errors” trong phần khắc phục sự cố.  

## “search and redact” là gì?
Search and redact là quá trình xác định các thuật ngữ cụ thể trong một bộ sưu tập tài liệu và sau đó che dấu hoặc loại bỏ vĩnh viễn các thuật ngữ đó để bảo vệ quyền riêng tư hoặc đáp ứng các yêu cầu tuân thủ quy định. Nó kết hợp tìm kiếm toàn văn để tìm thông tin nhạy cảm với các công cụ che dấu thay thế nội dung trong khi giữ nguyên bố cục gốc của tài liệu.

## Tại sao nên sử dụng GroupDocs.Search và GroupDocs.Redaction cùng nhau?
GroupDocs.Search hỗ trợ **50+ file formats** và có thể lập chỉ mục **100,000+ documents** trong vòng chưa đầy một phút trên phần cứng máy chủ tiêu chuẩn, trong khi GroupDocs.Redaction có thể áp dụng việc che dấu cho **PDF, DOCX, PPTX và hơn nữa** mà không làm thay đổi bố cục gốc. Kết hợp chúng mang lại cho bạn một giải pháp duy nhất tối ưu hiệu năng tìm kiếm và xử lý lỗi lập chỉ mục một cách nhẹ nhàng.

## Yêu cầu trước

- Visual Studio 2022 hoặc phiên bản mới hơn với hỗ trợ .NET 6+.  
- Các gói NuGet: **GroupDocs.Search** và **GroupDocs.Redaction** (phiên bản ổn định mới nhất).  
- Giấy phép GroupDocs hợp lệ (bản dùng thử hoặc đã mua).  

### Thư viện yêu cầu
- **GroupDocs.Search** – Cung cấp khả năng lập chỉ mục, truy vấn và phân đoạn tùy chỉnh.  
- **GroupDocs.Redaction** – Cung cấp khả năng che dấu văn bản, hình ảnh và siêu dữ liệu trên các định dạng được hỗ trợ.  

### Yêu cầu thiết lập môi trường
Đảm bảo máy phát triển của bạn có quyền ghi vào thư mục nơi chỉ mục sẽ được lưu trữ.

### Kiến thức yêu cầu
- Quen thuộc với C# và cấu trúc dự án .NET.  
- Hiểu biết cơ bản về các khái niệm xử lý tài liệu (tùy chọn nhưng hữu ích).  

## Làm thế nào để cài đặt GroupDocs.Redaction cho .NET?
Bạn có thể thêm gói Redaction vào dự án của mình bằng .NET CLI hoặc NuGet Package Manager. Lệnh sẽ tải xuống phiên bản ổn định mới nhất và đăng ký nó trong tệp dự án, khiến API sẵn sàng sử dụng ngay lập tức.  

```bash
dotnet add package GroupDocs.Redaction
```  

## Làm thế nào để có được giấy phép cho GroupDocs?
GroupDocs cung cấp ba tùy chọn cấp phép: bản dùng thử miễn phí để đánh giá, giấy phép tạm thời cho việc thử nghiệm phát triển kéo dài, và giấy phép thương mại đầy đủ cho môi trường sản xuất. Bản dùng thử cung cấp chức năng hạn chế, trong khi khóa tạm thời kéo dài thời gian đánh giá, và giấy phép mua sẽ mở khóa tất cả các tính năng và hỗ trợ ưu tiên.  

## Làm thế nào để khởi tạo GroupDocs.Redaction trong Ứng dụng của tôi?
Lớp `Redaction` là điểm vào chính để áp dụng việc che dấu lên các tài liệu được hỗ trợ. Nó tải một tệp, chuẩn bị các đối tượng che dấu, và thực thi quá trình che dấu, trả về tài liệu đã được sửa đổi trong khi giữ nguyên bố cục gốc. Bạn cũng có thể cấu hình các tùy chọn che dấu như màu sắc, lớp phủ và loại bỏ siêu dữ liệu để đáp ứng các yêu cầu tuân thủ cụ thể.  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Làm thế nào để thiết lập một chỉ mục bằng GroupDocs.Search?
Lớp `Index` đại diện cho một kho lưu trữ có thể tìm kiếm được lưu trên đĩa. Nó quản lý việc tạo, cập nhật và truy vấn chỉ mục, cho phép bạn thêm tài liệu, xây dựng lại chỉ mục và thực hiện các tìm kiếm nhanh trên các bộ sưu tập lớn. Thư mục chỉ mục có thể nằm trên lưu trữ cục bộ hoặc mạng, và bạn có thể cấu hình các cài đặt nén và mã hóa để bảo vệ dữ liệu đã lập chỉ mục.  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Bộ phân đoạn văn bản tùy chỉnh là gì và tại sao tôi nên sử dụng nó?
Bộ phân đoạn văn bản tùy chỉnh xác định cách văn bản thô được chia thành các token có thể tìm kiếm. Bằng cách tùy chỉnh các quy tắc phân đoạn cho các ngôn ngữ hoặc lĩnh vực cụ thể, bạn cải thiện độ chính xác của việc tokenization, dẫn đến độ thu hồi và tính liên quan cao hơn trong kết quả tìm kiếm. Điều này đặc biệt hữu ích cho các ngôn ngữ có ranh giới từ phức tạp, như tiếng Nhật hoặc tiếng Ả Rập, nơi các bộ tokenizer mặc định có thể tách từ sai.  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Làm thế nào để thực hiện tìm kiếm toàn văn với bộ phân đoạn tùy chỉnh?
Đối tượng `SearchQuery` bao bọc truy vấn của người dùng và làm việc với bộ phân đoạn tùy chỉnh để tìm các kết quả phù hợp. Nó hỗ trợ khớp mờ, truy vấn cụm từ và trọng số, trả về tập kết quả bao gồm ID tài liệu, vị trí xuất hiện và điểm liên quan. Bạn cũng có thể áp dụng các bộ lọc như loại tệp hoặc khoảng thời gian để thu hẹp kết quả cho mục tiêu chính xác hơn.  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Làm thế nào để áp dụng việc che dấu sau khi tìm thấy văn bản nhạy cảm?
API `Redaction` cho phép bạn thay thế hoặc loại bỏ văn bản, hình ảnh và siêu dữ liệu trong các tài liệu được hỗ trợ. Sau khi xác định các thuật ngữ nhạy cảm, bạn tạo các đối tượng che dấu, áp dụng chúng và lưu tệp đã che dấu, đảm bảo thông tin bí mật bị ẩn vĩnh viễn. Các tùy chọn che dấu bao gồm phủ lên các hộp đen, áp dụng màu tùy chỉnh, hoặc loại bỏ toàn bộ đối tượng trong khi giữ nguyên cấu trúc tài liệu.  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Các vấn đề thường gặp và cách xử lý lỗi lập chỉ mục
- **Index Not Found:** Kiểm tra xem đường dẫn chỉ mục có tồn tại và ứng dụng có quyền đọc/ghi không.  
- **Search Returns No Results:** Chạy lại quá trình lập chỉ mục và đảm bảo bộ phân đoạn tùy chỉnh đã được đăng ký đúng.  
- **Redaction Fails on Certain Formats:** Xác nhận loại tệp được hỗ trợ; đối với PDF, sử dụng phiên bản Redaction mới nhất để xử lý các tính năng PDF 2.0.  

## Ứng dụng thực tiễn

1. **Legal Document Management:** Tìm kiếm hợp đồng cho “non‑disclosure” và tự động che dấu các điều khoản trước khi chia sẻ bên ngoài.  
2. **Academic Research:** Xác định dữ liệu chưa công bố trong bản thảo và ẩn nó cho quá trình phản biện đồng nghiệp.  
3. **Business Contracts:** Xử lý hàng nghìn hợp đồng theo lô, che dấu các thông tin nhận dạng cá nhân trong khi giữ nguyên ngôn ngữ pháp lý.  

## Làm thế nào để tối ưu hiệu năng tìm kiếm cho tập hợp tài liệu lớn?
Để tối đa hoá hiệu năng, lập chỉ mục tài liệu một lần và tái sử dụng cùng một chỉ mục cho các truy vấn tiếp theo. Bật xử lý song song, cấu hình bộ nhớ đệm và tinh chỉnh cài đặt chỉ mục để giảm độ trễ và cải thiện thông lượng trên máy chủ đa lõi. Ngoài ra, đặt cờ `EnableMemoryMapping` để cho phép chỉ mục được ánh xạ bộ nhớ, giúp tăng tốc các hoạt động đọc cho các bộ dữ liệu lớn.  

## Làm thế nào để quản lý bộ nhớ .NET khi làm việc với tệp lớn?
Quản lý bộ nhớ hiệu quả là rất quan trọng khi xử lý tài liệu lớn. Bao bọc các đối tượng `Index` và `Redaction` trong các câu lệnh `using` để đảm bảo việc giải phóng tài nguyên một cách quyết đoán, và xử lý tệp dưới dạng luồng thay vì tải toàn bộ tài liệu vào bộ nhớ. Giám sát các bộ đếm hiệu năng giúp phát hiện sớm các đợt tăng đột biến bộ nhớ, cho phép bạn điều chỉnh kích thước lô hoặc bật tinh chỉnh thu gom rác.  

## Câu hỏi thường gặp

**Q: Tôi có thể sử dụng GroupDocs.Search với siêu dữ liệu không phải văn bản không?**  
A: Có — các trường siêu dữ liệu có thể được lập chỉ mục cùng với nội dung tài liệu, cho phép tìm kiếm như “author:JohnDoe”.

**Q: GroupDocs.Redaction có hỗ trợ che dấu thời gian thực trong một web API không?**  
A: Có; bạn có thể gọi API Redaction đồng bộ cho các tệp nhỏ hoặc đưa các công việc lớn vào hàng đợi để xử lý bất đồng bộ.

**Q: Tôi nên làm gì nếu chỉ mục bị hỏng?**  
A: Xóa thư mục chỉ mục bị hỏng và xây dựng lại bằng cùng quy trình lập chỉ mục; thư viện sẽ ghi lại các thông báo lỗi chi tiết để giúp bạn xác định nguyên nhân.

**Q: Có thể xem trước tài liệu đã che dấu trước khi lưu không?**  
A: Chắc chắn — gọi `redaction.Apply()` với cờ `preview` để tạo một phiên bản tạm thời để xem xét.

**Q: Các phiên bản .NET nào được hỗ trợ chính thức?**  
A: GroupDocs.Search và GroupDocs.Redaction hỗ trợ .NET 6, .NET 5, .NET Core 3.1 và .NET Framework 4.6.2+.  

## Tài nguyên

- **Tài liệu:** [Tài liệu GroupDocs Redaction](https://docs.groupdocs.com/search/net/)  
- **Tham chiếu API:** [Tham chiếu API GroupDocs](https://reference.groupdocs.com/redaction/net)  
- **Tải xuống:** [Bản phát hành GroupDocs](https://releases.groupdocs.com/search/net/)  
- **Hỗ trợ miễn phí:** [Diễn đàn GroupDocs](https://forum.groupdocs.com/c/search/10)  
- **Giấy phép tạm thời:** [Giấy phép tạm thời GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Cập nhật lần cuối:** 2026-06-12  
**Đã kiểm tra với:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 cho .NET  
**Tác giả:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Hướng dẫn liên quan

- [Làm chủ GroupDocs Search và Redaction trong .NET: Quản lý tài liệu nâng cao](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)  
- [Triển khai GroupDocs.Search & Redaction: Cập nhật và Quản lý Chỉ mục Tài liệu trong .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)  
- [Tối ưu hoá việc lập chỉ mục tài liệu trong .NET với GroupDocs.Redaction: Hủy, Bất đồng bộ và Luồng](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
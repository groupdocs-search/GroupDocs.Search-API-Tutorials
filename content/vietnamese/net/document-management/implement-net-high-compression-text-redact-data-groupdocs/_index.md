---
date: '2026-06-07'
description: Tìm hiểu cách triển khai nén cao .NET cho việc lưu trữ văn bản và che
  dấu dữ liệu bí mật bằng cách sử dụng GroupDocs.Search và GroupDocs.Redaction trong
  các ứng dụng .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Triển khai nén cao .NET với GroupDocs: Hướng dẫn Văn bản & Che dấu'
type: docs
url: /vi/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Triển khai Nén Cao .NET với GroupDocs: Hướng dẫn Văn bản & Che dấu

Trong các giải pháp .NET hiện đại, **implement high compression .net** là cần thiết khi bạn cần lưu trữ các bộ sưu tập văn bản khổng lồ mà không làm tăng đáng kể việc sử dụng đĩa. Đồng thời, bảo vệ thông tin nhạy cảm—như định danh cá nhân hoặc số liệu tài chính—đòi hỏi việc che dấu đáng tin cậy. Hướng dẫn này sẽ chỉ cho bạn, từng bước, cách cấu hình lưu trữ văn bản nén cao với **GroupDocs.Search** và cách an toàn che dấu dữ liệu bí mật bằng **GroupDocs.Redaction**. Khi kết thúc, bạn sẽ có thể nén văn bản đã lập chỉ mục lên tới 90 % và loại bỏ nội dung riêng tư khỏi PDF, tệp Word và nhiều định dạng khác.

## Câu trả lời nhanh
- **What library provides high‑compression indexing?** Thư viện nào cung cấp lập chỉ mục nén cao? GroupDocs.Search for .NET.  
- **Which tool redacts sensitive data?** Công cụ nào che dấu dữ liệu nhạy cảm? GroupDocs.Redaction for .NET.  
- **Can I add documents to index automatically?** Tôi có thể tự động thêm tài liệu vào chỉ mục không? Có—sử dụng API `AddDocument` trong vòng lặp quét thư mục.  
- **Is compression lossless for search?** Việc nén có mất dữ liệu cho tìm kiếm không? Có, văn bản vẫn hoàn toàn có thể tìm kiếm được sau khi nén.  
- **Do I need a license for production?** Tôi có cần giấy phép cho môi trường sản xuất không? Cần một giấy phép GroupDocs vĩnh viễn cho việc sử dụng thương mại.

## “implement high compression .net” là gì?
Implement high compression .net có nghĩa là cấu hình động cơ lập chỉ mục GroupDocs.Search để lưu trữ nội dung văn bản đã trích xuất ở dạng nén. Điều này giảm đáng kể kích thước chỉ mục trên đĩa trong khi vẫn giữ văn bản có thể tìm kiếm đầy đủ. Việc nén là không mất dữ liệu, vì vậy độ liên quan của truy vấn và việc trích đoạn hoạt động chính xác như với chỉ mục không nén.

## Tại sao nên sử dụng GroupDocs cho nén và che dấu?
GroupDocs.Search hỗ trợ hơn năm mươi định dạng đầu vào và có thể nén văn bản đã lập chỉ mục lên tới chín mươi phần trăm, cho phép các bộ sưu tập tài liệu lớn chỉ chiếm một phần nhỏ kích thước gốc. GroupDocs.Redaction bổ trợ bằng cách xóa vĩnh viễn hoặc che dấu thông tin nhạy cảm trên hơn ba mươi loại tệp, giúp bạn đáp ứng các quy định tuân thủ nghiêm ngặt như GDPR và HIPAA mà không cần công cụ bổ sung.

## Yêu cầu trước
- **Development environment:** Môi trường phát triển: Visual Studio 2022 hoặc mới hơn, .NET 6+ (hoặc .NET Framework 4.7.2).  
- **Libraries:** Thư viện: `GroupDocs.Search` và `GroupDocs.Redaction` NuGet packages.  
- **Permissions:** Quyền truy cập: Read/write access to the folders that contain source documents and the index output location.  
- **Basic knowledge:** Kiến thức cơ bản: C# syntax, file I/O, and familiarity with .NET project structure.

## Cách triển khai nén cao .NET với GroupDocs?
Để triển khai nén cao .NET với GroupDocs, đầu tiên tạo một thể hiện `TextStorageSettings` và đặt `CompressionLevel` của nó thành `High`. Sau đó khởi tạo một đối tượng `Index`, truyền các cài đặt và thư mục nơi chỉ mục sẽ được lưu trữ. Khi chỉ mục đã sẵn sàng, thêm tài liệu bằng `AddDocument`, và cuối cùng thực hiện tìm kiếm bằng phương thức `Search`, trong khi động cơ tự động xử lý nén và giải nén.

### Bước 1: Cài đặt các gói NuGet cần thiết
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Trình quản lý gói**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**Giao diện người dùng Trình quản lý Gói NuGet**  
- Tìm kiếm “GroupDocs.Search” và nhấn **Install**.  

### Bước 2: Cài đặt GroupDocs.Redaction (cho việc che dấu dữ liệu)
- Mở **NuGet Package Manager**.  
- Tìm kiếm **GroupDocs.Redaction** và cài đặt phiên bản ổn định mới nhất.  

### Bước 3: Nhận và áp dụng giấy phép
- **Free trial:** Dùng thử miễn phí: Register on the GroupDocs portal for a 30‑day trial key.  
- **Temporary license:** Giấy phép tạm thời: Request a temporary key for development environments.  
- **Permanent license:** Giấy phép vĩnh viễn: Purchase a production license to remove evaluation limitations.

### Bước 4: Khởi tạo cơ bản cho cả hai thư viện
Các động cơ `Search` và `Redaction` chia sẻ một mô hình cấp phép chung. Khởi tạo chúng khi ứng dụng khởi động:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Tính năng 1: Cài đặt Lưu trữ Văn bản Nén Cao

### Cấu hình Cài đặt Lập chỉ mục
`TextStorageSettings` là lớp cho phép GroupDocs.Search biết cách lưu trữ văn bản đã trích xuất. Kích hoạt nén cao giảm kích thước chỉ mục lên tới **10×** mà không ảnh hưởng đến tốc độ tìm kiếm.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Giải thích:**  
- `CompressionLevel.High` kích hoạt thuật toán dựa trên ZSTD nén các khối văn bản một cách hiệu quả.  
- `UseMemoryCache = false` buộc động cơ truyền dữ liệu từ đĩa, thích hợp cho triển khai quy mô lớn.

### Tạo và Quản lý Chỉ mục
Đối tượng `Index` đại diện cho kho lưu trữ có thể tìm kiếm trên đĩa. Bạn chỉ định thư mục nơi các tệp chỉ mục sẽ được lưu và truyền các cài đặt nén đã định nghĩa ở trên.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Giải thích:**  
- `indexFolder` xác định vị trí lưu trữ các tệp chỉ mục đã nén.  
- `settings` đưa vào cấu hình nén cao, đảm bảo mọi tài liệu được thêm vào đều hưởng lợi từ nó.

## Tính năng 2: Thêm Tài liệu vào Chỉ mục

### Thêm Tài liệu vào Chỉ mục của Bạn
`AddDocument` thêm một tệp duy nhất vào chỉ mục, trích xuất văn bản, nén theo cài đặt đã cấu hình và lưu kết quả. GroupDocs.Search có thể nhập các tệp từ cây thư mục. Vòng lặp dưới đây duyệt qua `documentsFolder`, thêm mỗi tệp và ghi lại tiến độ.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Giải thích:**  
- `AddDocument` phân tích tệp, trích xuất văn bản có thể tìm kiếm, nén theo `TextStorageSettings`, và lưu vào chỉ mục.  
- Cách tiếp cận này hoạt động cho **PDF, DOCX, TXT, HTML**, và hơn **30** định dạng khác.

## Tính năng 3: Thực hiện Truy vấn Tìm kiếm

### Thực hiện Tìm kiếm
`Search` thực hiện một truy vấn trên chỉ mục đã nén và trả về một tập hợp các đối tượng `DocumentResult` phù hợp kèm theo điểm liên quan và đoạn trích nổi bật. Khi chỉ mục đã được tạo, bạn có thể chạy các truy vấn nhanh. Phương thức `Search` trả về một tập hợp các đối tượng `DocumentResult` bao gồm đường dẫn tệp và đoạn trích nổi bật.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Giải thích:**  
- Động cơ tìm kiếm quét trực tiếp văn bản đã nén, vì vậy độ trễ truy vấn vẫn thấp ngay cả với các chỉ mục chứa **hàng triệu trang**.  
- `Score` cho biết mức độ liên quan; giá trị cao hơn nghĩa là kết quả phù hợp hơn.

## Cách che dấu dữ liệu bí mật với GroupDocs.Redaction?
Che dấu dữ liệu bí mật với GroupDocs.Redaction bắt đầu bằng việc tạo một thể hiện `Redactor` cho tệp mục tiêu. Định nghĩa một hoặc nhiều đối tượng `SearchPattern` mô tả văn bản cần loại bỏ, chẳng hạn như biểu thức chính quy cho số an sinh xã hội. Áp dụng mỗi mẫu bằng `Redact`, chỉ định `RedactionType` như `BlackOut`, và lưu kết quả dưới dạng tệp mới, đảm bảo tệp gốc không bị thay đổi.

`Redactor` là lớp chính trong GroupDocs.Redaction dùng để tải tài liệu và thực hiện các thao tác che dấu.  
`SearchPattern` định nghĩa một biểu thức chính quy xác định văn bản cần được che dấu.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Giải thích:**  
- `SearchPattern` sử dụng biểu thức chính quy để xác định số an sinh xã hội.  
- `RedactionType.BlackOut` thay thế văn bản khớp bằng một hình chữ nhật đen đặc, đảm bảo dữ liệu không thể khôi phục.

## Ứng dụng Thực tiễn
1. **Legal Document Management:** Quản lý Tài liệu Pháp lý: Tự động nén các hồ sơ vụ án khổng lồ và che dấu định danh khách hàng trước khi lưu trữ.  
2. **Healthcare Records:** Hồ sơ Y tế: Lưu trữ nhiều năm ghi chú bệnh nhân trong một chỉ mục nén và loại bỏ PHI (Thông tin Sức khỏe Bảo vệ) trước khi chia sẻ với các đối tác nghiên cứu.  
3. **Financial Reporting:** Báo cáo Tài chính: Bảo mật các báo cáo quý bằng cách che dấu số tài khoản trong khi vẫn giữ văn bản có thể tìm kiếm cho các truy vấn kiểm toán.

## Các cân nhắc về Hiệu suất
- **Compression impact:** Ảnh hưởng của nén: Nén cao giảm kích thước chỉ mục lên tới **90 %**, giúp giảm hao mòn SSD và tăng tốc các hoạt động sao lưu.  
- **Memory usage:** Sử dụng bộ nhớ: Vô hiệu hoá bộ nhớ đệm trong RAM cho các chỉ mục rất lớn để giữ dung lượng tiến trình dưới **500 MB**.  
- **I/O optimization:** Tối ưu I/O: Thêm tài liệu theo lô nhóm 100 để giảm thiểu việc đụng độ đĩa.  
- **Async processing:** Xử lý bất đồng bộ: Bao bọc các lời gọi `AddDocument` trong `Task.Run` để giữ cho các luồng UI phản hồi nhanh trong các ứng dụng desktop.

## Những Cạm Bẫy Thường Gặp & Khắc Phục Sự Cố
- **Incorrect file paths:** Đường dẫn tệp không đúng: Xác minh rằng `documentsFolder` và `indexFolder` là các đường dẫn tuyệt đối và ứng dụng có quyền đọc/ghi.  
- **License errors:** Lỗi giấy phép: Đảm bảo các tệp `.lic` được triển khai cùng với tệp thực thi hoặc được nhúng dưới dạng tài nguyên.  
- **Search returns no results:** Tìm kiếm không trả về kết quả: Kiểm tra mức nén `TextStorageSettings` có khớp với mức đã dùng khi lập chỉ mục; cài đặt không khớp có thể gây lỗi giải mã.

## Câu hỏi Thường gặp

**Q: Can I add documents to index after the initial build?**  
A: Yes—simply call `index.AddDocument` for new files; the engine updates the compressed index incrementally.  
=> **Q: Tôi có thể thêm tài liệu vào chỉ mục sau khi xây dựng ban đầu không?**  
A: Có—chỉ cần gọi `index.AddDocument` cho các tệp mới; động cơ sẽ cập nhật chỉ mục nén một cách tăng dần.

**Q: Does redaction alter the original file?**  
A: No—the original file remains untouched; the redacted version is saved as a new file, preserving document integrity.  
=> **Q: Che dấu có làm thay đổi tệp gốc không?**  
A: Không—tệp gốc vẫn không bị thay đổi; phiên bản đã che dấu được lưu dưới dạng tệp mới, bảo toàn tính toàn vẹn của tài liệu.

**Q: What formats does GroupDocs.Redaction support?**  
A: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG), and plain text.  
=> **Q: GroupDocs.Redaction hỗ trợ những định dạng nào?**  
A: Hơn **30** định dạng, bao gồm PDF, DOCX, PPTX, XLSX, hình ảnh (PNG, JPEG), và văn bản thuần.

**Q: How does high compression affect search relevance?**  
A: It does not. The compression is loss‑less for text, so relevance scores are identical to an uncompressed index.  
=> **Q: Nén cao ảnh hưởng như thế nào đến độ liên quan của tìm kiếm?**  
A: Không ảnh hưởng. Việc nén là không mất dữ liệu cho văn bản, vì vậy điểm liên quan giống hệt chỉ mục không nén.

**Q: Is there a limit to the size of documents I can index?**  
A: GroupDocs.Search can handle multi‑gigabyte files by streaming content; however, ensure sufficient disk space for the compressed index (approximately 10 % of the original size).  
=> **Q: Có giới hạn nào về kích thước tài liệu tôi có thể lập chỉ mục không?**  
A: GroupDocs.Search có thể xử lý các tệp đa gigabyte bằng cách truyền nội dung; tuy nhiên, hãy đảm bảo có đủ không gian đĩa cho chỉ mục nén (khoảng 10 % kích thước gốc).

## Tài nguyên
- [Tài liệu](https://docs.groupdocs.com/search/net/)
- [Tham chiếu API](https://reference.groupdocs.com/redaction/net)
- [Tải xuống GroupDocs.Redaction cho .NET](https://releases.groupdocs.com/search/net/)
- [Diễn đàn Hỗ trợ Miễn phí](https://forum.groupdocs.com/c/search/10)
- [Mua Giấy phép Tạm thời](https://purchase.groupdocs.com/temporary-license/)

---

**Cập nhật lần cuối:** 2026-06-07  
**Được kiểm tra với:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Tác giả:** GroupDocs

## Các hướng dẫn liên quan

- [Triển khai GroupDocs.Search và Redaction trong .NET cho Quản lý Tài liệu](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Cách Tối ưu GroupDocs.Redaction cho .NET: Hướng dẫn Quản lý Chỉ mục & Chính tả Hiệu quả](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Thành thạo GroupDocs Redaction và Search trong .NET: Quản lý Tài liệu Hiệu quả và Tìm kiếm Bảo mật](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
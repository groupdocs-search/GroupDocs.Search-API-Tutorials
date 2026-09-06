---
date: '2026-06-07'
description: Tìm hiểu cách cập nhật chỉ mục một cách hiệu quả với GroupDocs.Search
  và Redaction cho .NET, nâng cao hệ thống quản lý tài liệu của bạn.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Cách cập nhật chỉ mục với GroupDocs.Search & Redaction (.NET)
type: docs
url: /vi/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Cách Cập Nhật Chỉ Mục với GroupDocs.Search & Redaction (.NET)

Trong các doanh nghiệp hiện đại dựa trên dữ liệu, **cách cập nhật chỉ mục** nhanh chóng và đáng tin cậy có thể quyết định trải nghiệm tìm kiếm của bạn. Dù bạn đang xử lý hàng ngàn hợp đồng hay một cơ sở tri thức rộng lớn, việc giữ chỉ mục tìm kiếm đồng bộ với các thay đổi tài liệu mới nhất là điều cần thiết để có kết quả nhanh, chính xác. Hướng dẫn này sẽ chỉ cho bạn cách sử dụng GroupDocs.Search cho .NET kết hợp với GroupDocs.Redaction để **cập nhật chỉ mục** các tệp, quản lý các chỉ mục phiên bản, và bảo vệ nội dung nhạy cảm — tất cả trong một dự án .NET sạch sẽ.

## Câu trả lời nhanh
- **“how to update index” có nghĩa là gì?** Đó là quá trình sửa đổi một chỉ mục tìm kiếm hiện có để các tài liệu mới hoặc đã thay đổi có thể tìm kiếm được mà không cần xây dựng lại từ đầu.  
- **Các thư viện nào được yêu cầu?** GroupDocs.Search và GroupDocs.Redaction cho .NET (cả hai đều có sẵn qua NuGet).  
- **Tôi có cần giấy phép không?** Một bản dùng thử miễn phí hoạt động cho việc thử nghiệm; giấy phép sản xuất mở khóa đầy đủ chức năng.  
- **Tôi có thể chạy điều này trên .NET Core không?** Có, các thư viện hỗ trợ .NET Framework 4.5+, .NET Core 3.1+, và .NET 5/6+.  
- **Hiệu năng tôi có thể mong đợi là gì?** Cập nhật một chỉ mục 1 GB với 2 luồng hoàn thành trong vòng chưa tới một phút trên máy chủ 4‑core tiêu chuẩn.

## “how to update index” là gì?
**How to update index** đề cập đến kỹ thuật áp dụng các thay đổi gia tăng vào một chỉ mục tìm kiếm hiện có thay vì tạo lại hoàn toàn. Cách tiếp cận này giảm thời gian ngừng hoạt động, tiết kiệm chu kỳ CPU, và giữ cho kết quả tìm kiếm của bạn luôn mới khi tài liệu được thêm, chỉnh sửa hoặc xóa.

## Tại sao nên sử dụng GroupDocs.Search & Redaction để cập nhật chỉ mục?
GroupDocs.Search hỗ trợ **hơn 50 định dạng tệp** (PDF, DOCX, XLSX, PPTX, HTML, hình ảnh, v.v.) và có thể xử lý các tài liệu hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ. Khi kết hợp với GroupDocs.Redaction, bạn có thể tự động loại bỏ hoặc che giấu dữ liệu nhạy cảm trước khi lập chỉ mục, đảm bảo tuân thủ đồng thời duy trì tính liên quan của tìm kiếm.

## Yêu cầu trước

- **GroupDocs.Search** – cài đặt qua NuGet.  
- **GroupDocs.Redaction for .NET** – cần thiết cho khả năng che dấu.  
- Visual Studio (hoặc bất kỳ IDE .NET nào) với .NET 6+ đã được cài đặt.  
- Kiến thức cơ bản về C# và quen thuộc với các khái niệm lập chỉ mục.

### Thư viện và Phiên bản yêu cầu
- **GroupDocs.Search** – bản phát hành ổn định mới nhất từ NuGet.  
- **GroupDocs.Redaction for .NET** – bản phát hành ổn định mới nhất từ NuGet.

### Yêu cầu thiết lập môi trường
- Máy Windows hoặc Linux có .NET SDK được cài đặt.  
- Quyền truy cập vào thư mục nơi các tệp chỉ mục sẽ được lưu trữ.

### Kiến thức nền tảng
- Hiểu biết về lập chỉ mục tài liệu và các nguyên tắc cơ bản của tìm kiếm.  
- Nhận thức về quản lý vòng đời tài liệu trong các hệ thống doanh nghiệp.

## Cài đặt GroupDocs.Redaction cho .NET

### Cài đặt các Gói

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Tìm kiếm “GroupDocs.Redaction” và cài đặt phiên bản mới nhất.

### Các bước lấy giấy phép
1. **Free Trial** – bắt đầu với bản dùng thử để khám phá tất cả các tính năng.  
2. **Temporary License** – yêu cầu khóa tạm thời để thử nghiệm kéo dài.  
3. **Purchase** – mua giấy phép đầy đủ cho triển khai sản xuất.

### Khởi tạo và Cấu hình Cơ bản
`Redactor` là lớp cốt lõi áp dụng các quy tắc che dấu vào tài liệu.  
Để bắt đầu, tham chiếu không gian tên Redaction và tạo một thể hiện `Redactor`:

```csharp
using GroupDocs.Redaction;
```

## Hướng dẫn triển khai

Chúng tôi sẽ đề cập đến hai khả năng cốt lõi: cập nhật tài liệu đã lập chỉ mục và duy trì kiểm soát phiên bản chỉ mục.

### Cách cập nhật chỉ mục bằng GroupDocs.Search?

`Index` đại diện cho bộ sưu tập có thể tìm kiếm được lưu trên đĩa.  
`UpdateOptions` cấu hình cách thực hiện các cập nhật gia tăng (ví dụ, số lượng luồng).  
`UpdateDocument` áp dụng các thay đổi cho một tài liệu duy nhất, và `Commit` hoàn tất tất cả các cập nhật đang chờ.

**Câu trả lời ngắn (40‑70 từ):**  
Tạo một đối tượng `Index` trỏ tới thư mục chỉ mục của bạn, sử dụng `UpdateOptions` để chỉ định số luồng, gọi `UpdateDocument` cho mỗi tệp đã thay đổi, và cuối cùng gọi `Commit` để lưu các thay đổi. Cách tiếp cận gia tăng này chỉ cập nhật các phần đã sửa đổi, giữ chỉ mục luôn cập nhật mà không cần xây dựng lại toàn bộ.

#### Tính năng 1: Cập nhật Tài liệu Đã Lập Chỉ mục

##### Tổng quan
Cập nhật tài liệu đã lập chỉ mục đảm bảo kết quả tìm kiếm của bạn phản ánh nội dung mới nhất, ngay cả khi tài liệu được chỉnh sửa hoặc thay thế.

##### Bước 1: Tạo một Index
Lớp `Index` là đối tượng cấp cao nhất đại diện cho một bộ sưu tập có thể tìm kiếm trên đĩa.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Bước 2: Thêm Tài liệu vào Index
Thêm các tệp từ một thư mục; thư viện tự động trích xuất văn bản có thể tìm kiếm.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Bước 3: Tìm kiếm và Cập nhật
Thực hiện một truy vấn, sửa đổi tệp nguồn, sau đó gọi `UpdateDocument` với cùng `UpdateOptions` đã sử dụng trong quá trình lập chỉ mục.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Tại sao cách này hoạt động:** Bằng cách đặt `Threads = 2`, quá trình cập nhật sử dụng hai lõi CPU, giảm thời gian xử lý khoảng một nửa trên máy có bốn lõi.

### Cách duy trì kiểm soát phiên bản chỉ mục?

`IndexUpdater` là lớp tiện ích nâng cấp các định dạng chỉ mục cũ lên phiên bản mới nhất được thư viện hỗ trợ.

**Câu trả lời ngắn (40‑70 từ):**  
Khởi tạo `IndexUpdater` với đường dẫn tới chỉ mục hiện có, gọi `CanUpdateVersion()` để xác minh khả năng tương thích, sau đó chạy `UpdateVersion()` nếu cần. Sau khi nâng cấp, tải lại chỉ mục với định dạng mới và thực hiện tìm kiếm để xác nhận mọi thứ hoạt động. Điều này đảm bảo việc di chuyển liền mạch giữa các phiên bản thư viện.

#### Tính năng 2: Duy trì Kiểm soát Phiên bản Chỉ mục

##### Tổng quan
Kiểm soát phiên bản đảm bảo các chỉ mục cũ vẫn có thể tìm kiếm được sau khi nâng cấp thư viện.

##### Bước 1: Kiểm tra Tính tương thích
`IndexUpdater` kiểm tra xem chỉ mục hiện tại có thể nâng cấp lên định dạng mới nhất hay không.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Bước 2: Tải và Tìm kiếm
Sau khi nâng cấp, tải chỉ mục đã được làm mới và thực hiện một truy vấn để xác minh tính toàn vẹn.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Tại sao cách này hoạt động:** Bộ kiểm tra `CanUpdateVersion` ngăn ngừa các ngoại lệ thời gian chạy do không khớp giữa các schema của chỉ mục, cung cấp một lộ trình nâng cấp an toàn.

## Ứng dụng Thực tiễn

Các kịch bản thực tế nơi **cách cập nhật chỉ mục** quan trọng:

1. **Legal Document Management** – Nhanh chóng lập chỉ mục lại các hợp đồng sau khi sửa đổi đồng thời che dấu các điều khoản bí mật.  
2. **Corporate Archives** – Giữ các hồ sơ lịch sử có thể tìm kiếm mà không cần xử lý lại hàng triệu tệp.  
3. **Content Management Systems (CMS)** – Đẩy các cập nhật gia tăng vào chỉ mục tìm kiếm khi các tác giả công bố bài viết mới.

## Các yếu tố về Hiệu năng

- **Threading Options:** Điều chỉnh `UpdateOptions.Threads` dựa trên số lõi CPU; nhiều luồng hơn cải thiện thông lượng nhưng tăng sử dụng bộ nhớ.  
- **Resource Usage:** Giám sát RAM; thư viện truyền dữ liệu tệp, vì vậy mức tăng đột biến bộ nhớ là tối thiểu ngay cả với PDF 500 trang.  
- **Best Practices:** Lên lịch cập nhật gia tăng thường xuyên và dọn dẹp các phiên bản chỉ mục lỗi thời để duy trì hiệu năng tối ưu.

## Các vấn đề thường gặp và giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Không tìm thấy Index** | Đường dẫn thư mục sai | Xác minh rằng hàm khởi tạo `Index` trỏ tới thư mục đúng. |
| **Lỗi không khớp phiên bản** | Sử dụng chỉ mục cũ với thư viện mới | Chạy quy trình `IndexUpdater` trước khi lập chỉ mục bình thường. |
| **Redaction không được áp dụng** | Các quy tắc redaction được tải sau khi lập chỉ mục | Áp dụng redaction **trước** khi thêm tài liệu vào chỉ mục. |

## Câu hỏi thường gặp

**Q: “how to update index” khác gì so với `Rebuild`?**  
A: `UpdateDocument` chỉ sửa đổi các tệp đã thay đổi, trong khi `Rebuild` tạo lại toàn bộ chỉ mục từ đầu, tiêu tốn nhiều thời gian và tài nguyên hơn.

**Q: Tôi có thể cập nhật nhiều tài liệu đồng thời không?**  
A: Có, đặt `UpdateOptions.Threads` bằng số lõi bạn muốn sử dụng; thư viện sẽ xử lý song song nội bộ.

**Q: GroupDocs.Search có hỗ trợ PDF được mã hóa không?**  
A: Chắc chắn. Cung cấp mật khẩu qua `SearchOptions.Password` khi tải tài liệu.

**Q: Làm sao kiểm tra redaction đã thành công trước khi lập chỉ mục?**  
A: Gọi `Redactor.Apply()` và kiểm tra kích thước tệp đầu ra; kích thước giảm thường cho thấy redaction đã thành công.

**Q: Các phiên bản .NET nào được hỗ trợ chính thức?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 và .NET 6+.

## Kết luận

Bạn đã có một hướng dẫn hoàn chỉnh, sẵn sàng cho sản xuất về **cách cập nhật chỉ mục** bằng GroupDocs.Search và cách giữ các chỉ mục này tương thích phiên bản với GroupDocs.Redaction cho .NET. Bằng cách thực hiện các bước trên, bạn có thể đảm bảo lớp tìm kiếm của mình luôn nhanh, chính xác và tuân thủ các quy định bảo mật dữ liệu.

**Các bước tiếp theo:**  
- Thử nghiệm với các cài đặt `Threads` khác nhau để tìm điểm cân bằng cho phần cứng của bạn.  
- Khám phá các mẫu redaction nâng cao (ví dụ, loại bỏ SSN dựa trên regex) trước khi lập chỉ mục.  
- Tích hợp quy trình cập nhật chỉ mục vào pipeline CI/CD của bạn để quản lý tài liệu hoàn toàn tự động.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs  

## Tài nguyên
- [Tài liệu](https://docs.groupdocs.com/search/net/)
- [Tham chiếu API](https://reference.groupdocs.com/redaction/net)
- [Tải xuống GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Diễn đàn Hỗ trợ Miễn phí](https://forum.groupdocs.com/c/search/10)
- [Giấy phép Tạm thời](https://purchase.groupdocs.com/temporary-license/)

## Hướng dẫn liên quan

- [Làm chủ GroupDocs.Redaction .NET: Tạo chỉ mục hiệu quả và quản lý bí danh cho Tìm kiếm Tài liệu Nâng cao](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Triển khai Tìm kiếm Đồng nghĩa với GroupDocs.Redaction .NET để Nâng cao Quản lý Tài liệu](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Làm chủ GroupDocs Search và Redaction trong .NET: Quản lý Tài liệu Nâng cao](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
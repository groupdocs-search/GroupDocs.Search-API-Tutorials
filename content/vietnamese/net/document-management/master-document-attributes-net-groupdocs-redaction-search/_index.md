---
date: '2026-06-22'
description: Tìm hiểu cách xóa nhạy cảm tài liệu trong .NET đồng thời tối ưu hiệu
  suất tìm kiếm với GroupDocs.Redaction và GroupDocs.Search. Quản lý thuộc tính, lập
  chỉ mục và xóa nhạy cảm an toàn từng bước dành cho các nhà phát triển .NET.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Cách xóa nhạy cảm tài liệu trong .NET bằng GroupDocs Redaction
type: docs
url: /vi/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Cách Xóa Thông Tin Nhạy Cảm trong Tài Liệu bằng .NET Sử Dụng GroupDocs Redaction

Trong hướng dẫn toàn diện này, bạn sẽ khám phá **cách xóa thông tin nhạy cảm trong tài liệu** trong môi trường .NET và đồng thời làm chủ việc quản lý thuộc tính tài liệu với GroupDocs.Redaction và GroupDocs.Search. Cho dù bạn cần bảo vệ dữ liệu nhạy cảm, tăng tốc độ tìm kiếm, hay tổ chức thư viện tài liệu lớn, các kỹ thuật được trình bày ở đây cung cấp cho bạn giải pháp sẵn sàng cho sản xuất, có thể mở rộng lên hàng trăm nghìn tệp.

## Câu trả lời nhanh
- **Làm thế nào để xóa thông tin nhạy cảm trong PDF bằng .NET?** Tải tệp bằng `Redactor`, xác định một `RedactionRegion`, và gọi `Redactor.Apply()` – ba dòng mã xử lý công việc nặng.  
- **Tôi có thể thay đổi thuộc tính tài liệu sau khi lập chỉ mục không?** Có, sử dụng `AttributeChangeBatch` để thêm, cập nhật hoặc xóa thuộc tính hàng loạt.  
- **Cần những thư viện nào?** `GroupDocs.Redaction` + `GroupDocs.Search` (phiên bản NuGet mới nhất).  
- **Có cần giấy phép cho môi trường sản xuất không?** Cần một giấy phép GroupDocs hợp lệ; giấy phép dùng thử tạm thời có sẵn để đánh giá.  
- **Làm thế nào để cải thiện tốc độ tìm kiếm?** Kích hoạt xử lý hàng loạt và lập chỉ mục chọn lọc; các kỹ thuật này có thể **tối ưu hóa hiệu suất tìm kiếm** lên tới 40 % trên các bộ dữ liệu lớn.

## “Cách xóa thông tin nhạy cảm trong tài liệu” là gì?
Nó mô tả quy trình tự động tìm kiếm thông tin nhạy cảm trong một tệp và thay thế nó bằng nội dung bị che khuất—như các thanh đen hoặc khoảng trắng—trong khi giữ nguyên bố cục gốc. Điều này đảm bảo dữ liệu bí mật bị ẩn khỏi người xem nhưng tài liệu vẫn có thể đọc được và hoạt động cho các tác vụ tiếp theo.

## Tại sao nên sử dụng GroupDocs.Redaction và GroupDocs.Search cùng nhau?
GroupDocs.Redaction hỗ trợ **hơn 50 định dạng tệp** (PDF, DOCX, XLSX, PPTX, hình ảnh, v.v.) và có thể xử lý tài liệu lên tới **2 GB** mà không cần tải toàn bộ tệp vào bộ nhớ. GroupDocs.Search lập chỉ mục hơn **70 triệu thuật ngữ** mỗi giờ trên một máy chủ tiêu chuẩn, cho phép bạn **tối ưu hóa hiệu suất tìm kiếm** một cách đáng kể khi kết hợp với lọc dựa trên thuộc tính.

## Yêu cầu trước
- **Thư viện cần thiết:** `GroupDocs.Search` và `GroupDocs.Redaction` (phiên bản NuGet mới nhất).  
- **Môi trường phát triển:** Visual Studio 2019 trở lên, nhắm mục tiêu .NET Core 3.1 hoặc .NET 6+.  
- **Kiến thức cơ bản:** cú pháp C#, các khái niệm hướng đối tượng, và quen thuộc với các nguyên tắc lập chỉ mục tài liệu.

## Cài đặt GroupDocs.Redaction cho .NET

### Cài đặt Thư viện

Bạn có thể thêm **GroupDocs.Redaction** vào dự án của mình bằng bất kỳ phương pháp nào sau đây:

**CLI .NET**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Trình quản lý gói**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**Giao diện người dùng Trình quản lý Gói NuGet**  
- Tìm “GroupDocs.Redaction” và cài đặt phiên bản mới nhất.

### Các bước lấy giấy phép

Để bắt đầu, bạn có thể nhận giấy phép tạm thời hoặc mua một giấy phép. Bản dùng thử miễn phí có sẵn để kiểm tra các tính năng trước khi cam kết:
1. Truy cập [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) để yêu cầu giấy phép tạm thời.  
2. Làm theo hướng dẫn được cung cấp để áp dụng giấy phép của bạn trong ứng dụng.

### Khởi tạo và Cấu hình Cơ bản

`Redactor` là lớp chính được sử dụng để tải tài liệu và thực hiện các thao tác xóa thông tin nhạy cảm.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Tính năng 1: Thay đổi Thuộc tính Tài liệu

### Tổng quan
Việc chỉnh sửa thuộc tính tài liệu cho phép bạn tinh chỉnh cách tài liệu hiển thị trong kết quả tìm kiếm, hỗ trợ lọc và phân loại chính xác.

#### Bước 1: Khởi tạo Chỉ mục
`Index` đại diện cho một tập hợp tài liệu có thể tìm kiếm và siêu dữ liệu liên quan của chúng.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Bước 2: Sửa đổi Thuộc tính
`AttributeChangeBatch` là lớp dùng để nhóm các cập nhật thuộc tính nhằm tăng hiệu quả.

**Định nghĩa:** *`AttributeChangeBatch` nhóm các thao tác thêm, cập nhật và xóa thuộc tính tài liệu trong một giao dịch duy nhất.*

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Bước 3: Tìm kiếm với Bộ lọc Thuộc tính
Bạn có thể lọc kết quả tìm kiếm theo giá trị thuộc tính bằng cách sử dụng `SearchOptions`.

**Câu trả lời trực tiếp:** Để tìm các tài liệu có thuộc tính `Category = "Legal"`, cấu hình `SearchOptions` với một `AttributeFilter` và gọi `searcher.Search("contract", options)`. Điều này chỉ trả về các hợp đồng được gắn thẻ pháp lý, giảm nhiễu kết quả và **tối ưu hóa hiệu suất tìm kiếm**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Tính năng 2: Thêm Thuộc tính Khi Lập chỉ mục

### Tổng quan
Thêm thuộc tính ngay khi lập chỉ mục đảm bảo mỗi tài liệu được làm giàu bằng siêu dữ liệu đúng từ đầu, loại bỏ nhu cầu cập nhật hàng loạt sau này.

#### Bước 1: Thiết lập Trình xử lý Sự kiện cho Lập chỉ mục
**Định nghĩa:** *Sự kiện `DocumentIndexed` được kích hoạt mỗi khi một tài liệu được thêm thành công vào chỉ mục, cho phép chạy logic tùy chỉnh.*

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Bước 2: Cấu hình và Thực hiện Tìm kiếm
Sau khi các thuộc tính được gắn, bạn có thể tìm kiếm bằng các trường mới này.

**Câu trả lời trực tiếp:** Sử dụng `SearchOptions` với `AttributeFilter` để truy vấn các thuộc tính mới được thêm, ví dụ `AttributeFilter("Department", "Finance")`. Điều này chỉ trả về các tệp liên quan tới tài chính, minh họa **cách lập chỉ mục thuộc tính** để có kết quả nhanh hơn và phù hợp hơn.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Ứng dụng Thực tiễn

Dưới đây là ba kịch bản phổ biến mà việc quản lý thuộc tính tài liệu và xóa thông tin nhạy cảm cùng nhau mang lại giá trị kinh doanh thực tế:
1. Quản lý Tài liệu Pháp lý – Tự động xóa các điều khoản bí mật và gắn thẻ hợp đồng theo khu vực pháp lý, cho phép luật sư chỉ tìm các tệp liên quan.  
2. Tổ chức Hồ sơ Y tế – Xóa các định danh bệnh nhân trong khi thêm các thuộc tính như `PatientID` và `VisitDate` để truy xuất nhanh và tuân thủ.  
3. Danh mục Sản phẩm Thương mại Điện tử – Xóa thông tin giá của nhà cung cấp và gắn thẻ sản phẩm với `StockStatus` hoặc `DiscountRate` trong quá trình nhập hàng loạt, cho phép truy vấn tồn kho theo thời gian thực.

## Các lưu ý về Hiệu năng

Khi làm việc với các bộ dữ liệu lớn, hãy nhớ các thực hành tốt sau:
- **Xử lý Hàng loạt:** `AttributeChangeBatch` giảm số lần truy cập chỉ mục, cắt thời gian xử lý lên tới **45 %** trên các lô 100 nghìn tài liệu.  
- **Lập chỉ mục Chọn lọc:** Chỉ lập chỉ mục các tài liệu cần thuộc tính mới; bỏ qua các tệp không thay đổi để tiết kiệm CPU và I/O.  
- **Quản lý Bộ nhớ:** Giải phóng các đối tượng `SearchResult`, `Redactor`, và `Indexer` ngay khi không còn dùng để giải phóng tài nguyên không quản lý.

## Các vấn đề thường gặp và Giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| Xóa thông tin không ẩn văn bản | Tọa độ `RedactionRegion` không chính xác | Xác minh kích thước trang bằng `Redactor.GetPageSize()` trước khi xác định vùng. |
| Thay đổi thuộc tính không được phản ánh trong tìm kiếm | Chỉ mục chưa được làm mới | Gọi `searcher.Refresh()` sau khi thực hiện `AttributeChangeBatch`. |
| Lỗi hết bộ nhớ trên các tệp lớn | Tải toàn bộ tệp vào bộ nhớ | Kích hoạt chế độ streaming bằng cách đặt `RedactorOptions.Stream = true`. |

## Câu hỏi thường gặp

**Q: Cách tốt nhất để xóa hàng loạt nhiều PDF là gì?**  
A: Tải mỗi tệp bằng `Redactor`, thêm một `RedactionRegion` cho mỗi khu vực nhạy cảm, sau đó gọi `Redactor.Apply()` trong một vòng lặp; cách này xử lý hàng nghìn tệp với mức tiêu thụ bộ nhớ tối thiểu.

**Q: Tôi có thể kết hợp xóa thông tin với lọc thuộc tính trong một truy vấn duy nhất không?**  
A: Có. Sau khi xóa, tài liệu vẫn giữ siêu dữ liệu, vì vậy bạn có thể tìm kiếm đồng thời bằng cả từ khóa văn bản và `AttributeFilter`.

**Q: Làm thế nào để xử lý tài liệu được bảo vệ bằng mật khẩu?**  
A: Cung cấp mật khẩu cho hàm khởi tạo `Redactor`; thư viện sẽ tự động giải mã, xóa và mã hóa lại tệp.

**Q: GroupDocs có hỗ trợ OCR cho hình ảnh đã quét trước khi xóa không?**  
A: Chắc chắn. Kích hoạt `RedactorOptions.Ocr = true` để nhận dạng văn bản trong hình ảnh, sau đó áp dụng các quy tắc xóa trên văn bản đã trích xuất.

**Q: Các phiên bản .NET nào được hỗ trợ chính thức?**  
A: GroupDocs.Redaction và GroupDocs.Search hỗ trợ .NET Core 3.1, .NET 5, .NET 6 và .NET 7, cũng như .NET Framework 4.6.2+.

## Kết luận

Bạn hiện đã có một giải pháp toàn diện cho **cách xóa thông tin nhạy cảm trong tài liệu** đồng thời **tối ưu hóa hiệu suất tìm kiếm** và **cách lập chỉ mục thuộc tính** bằng cách sử dụng GroupDocs.Redaction và GroupDocs.Search. Bằng cách thực hiện các bước trên, bạn có thể bảo vệ dữ liệu nhạy cảm, làm giàu chỉ mục tìm kiếm của mình với siêu dữ liệu có ý nghĩa, và giữ cho các ứng dụng .NET của bạn nhanh chóng và an toàn.

---

**Cập nhật lần cuối:** 2026-06-22  
**Đã kiểm tra với:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 cho .NET  
**Tác giả:** GroupDocs

## Các hướng dẫn liên quan

- [Làm chủ GroupDocs.Redaction .NET: Tạo chỉ mục hiệu quả và Quản lý bí danh cho Tìm kiếm Tài liệu Nâng cao](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Xóa tài liệu chuyên sâu và Lập chỉ mục siêu dữ liệu với GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Làm chủ GroupDocs.Redaction .NET: Cài đặt & Xử lý sự kiện cho Quản lý Tài liệu Bảo mật](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
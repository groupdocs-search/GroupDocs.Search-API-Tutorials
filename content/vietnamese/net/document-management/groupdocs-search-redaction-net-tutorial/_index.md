---
date: '2026-06-12'
description: Tìm hiểu cách tạo chỉ mục tìm kiếm .NET và áp dụng redaction cho PDF
  bằng GroupDocs.Search và GroupDocs.Redaction. Hướng dẫn Setup, deployment, indexing
  và advanced search.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Tạo chỉ mục tìm kiếm .NET với GroupDocs Search và Redaction – Hướng dẫn toàn
  diện
type: docs
url: /vi/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Tạo Chỉ mục Tìm kiếm .NET với GroupDocs Search và Redaction – Hướng dẫn Toàn diện

Trong bối cảnh kỹ thuật số ngày nay, **tạo một giải pháp tạo chỉ mục tìm kiếm .NET** có khả năng định vị thông tin nhanh chóng và bảo vệ dữ liệu nhạy cảm là ưu tiên hàng đầu của bất kỳ tổ chức nào. Hướng dẫn này sẽ hướng dẫn bạn cấu hình một mạng GroupDocs.Search có khả năng mở rộng, triển khai các nút, lập chỉ mục tài liệu và sử dụng GroupDocs.Redaction để **áp dụng redaction cho PDF** — tất cả trong môi trường .NET.

## Câu trả lời nhanh
- **Bước đầu tiên để tạo chỉ mục tìm kiếm .NET là gì?** Xác định đường dẫn cơ sở và cổng, sau đó triển khai các nút mạng.  
- **Làm thế nào để áp dụng redaction cho PDF với GroupDocs?** Khởi tạo một thể hiện `Redactor`, tải PDF và gọi `Redact` với các mẫu mong muốn.  
- **Tôi có thể chạy mạng tìm kiếm trên nhiều máy không?** Có—triển khai các nút trên các máy chủ riêng biệt và để nút master điều phối việc lập chỉ mục và truy vấn.  
- **Tôi có cần giấy phép cho việc sử dụng trong môi trường sản xuất không?** Cần một giấy phép GroupDocs hợp lệ cho môi trường sản xuất; một giấy phép dùng thử tạm thời có sẵn để đánh giá.  
- **Các phiên bản .NET nào được hỗ trợ?** .NET Framework 4.7.2+, .NET Core 3.1+, và .NET 5/6/7 đều được hỗ trợ đầy đủ.

## “Tạo chỉ mục tìm kiếm .NET” là gì?
*Creating a search index .NET* đề cập đến việc xây dựng một kho lưu trữ có thể tìm kiếm được của siêu dữ liệu và nội dung tài liệu bằng các thư viện .NET, chúng trích xuất văn bản, tách từ khóa và lưu trữ chúng trong cấu trúc chỉ mục tối ưu. Điều này cho phép phản hồi truy vấn tức thì trên các nút phân tán, hỗ trợ nhiều định dạng tệp và cho phép truy xuất tài liệu quy mô lớn, hiệu suất cao trong các ứng dụng doanh nghiệp.

## Tại sao nên sử dụng GroupDocs Search và Redaction cùng nhau?
GroupDocs.Search hỗ trợ **hơn 50 định dạng tệp**—bao gồm DOCX, PDF, PPTX và HTML—và có thể lập chỉ mục các tài liệu hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ. Khi kết hợp với GroupDocs.Redaction, có thể **áp dụng redaction cho PDF** trong thời gian dưới 200 ms mỗi trang, bạn sẽ có một quy trình quản lý tài liệu an toàn, hiệu suất cao.

## Yêu cầu trước

### Thư viện & Phụ thuộc cần thiết
Để làm theo hướng dẫn này, cài đặt các gói sau:
- **GroupDocs.Search** cho .NET
- **GroupDocs.Redaction** cho .NET  

Bạn có thể sử dụng bất kỳ phương pháp nào sau đây để cài đặt các thư viện cần thiết:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Tìm kiếm "GroupDocs.Search" và "GroupDocs.Redaction" và cài đặt phiên bản mới nhất.

### Yêu cầu thiết lập môi trường
- .NET Framework 4.7.2 hoặc cao hơn (hoặc .NET Core 3.1+)
- Visual Studio IDE (Community, Professional, hoặc Enterprise)

### Kiến thức tiên quyết
- Lập trình C# cơ bản
- Các khái niệm hướng đối tượng
- Quen thuộc với cấu hình mạng và hệ thống quản lý tài liệu

## Cài đặt GroupDocs.Redaction cho .NET

### Thông tin Cài đặt
Để tích hợp các tính năng redaction vào ứng dụng của bạn, bắt đầu bằng cách thêm thư viện GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Tìm kiếm "GroupDocs.Redaction" và cài đặt nó.

### Nhận giấy phép
Để bắt đầu với bản dùng thử miễn phí hoặc giấy phép tạm thời, thực hiện các bước sau:
- Truy cập [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) để yêu cầu giấy phép tạm thời.  
- Đối với các tùy chọn mua, truy cập [trang giá](https://groupdocs.com/pricing) của họ.

Sau khi bạn có tệp giấy phép, áp dụng nó trong cấu hình ứng dụng của bạn:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Khởi tạo Cơ bản
Để khởi tạo GroupDocs.Redaction cho các thao tác cơ bản, sử dụng đoạn mã sau:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Hướng dẫn Triển khai

### Cấu hình Thiết lập

#### Tổng quan
Tính năng này cấu hình mạng tìm kiếm của bạn bằng cách sử dụng đường dẫn cơ sở và số cổng, tạo nền tảng cho hệ thống quản lý tài liệu của bạn.

#### Định nghĩa Anchor
`SearchNetworkDeployment` là lớp điều phối việc triển khai các nút tìm kiếm trên toàn mạng.

#### Bước 1: Xác định Đường dẫn Cơ sở và Cổng  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Bước 2: Cấu hình Mạng
Sử dụng phương thức `Configure` để thiết lập mạng tìm kiếm với đường dẫn và cổng đã chỉ định:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Triển khai Nút Mạng

#### Tổng quan
Triển khai các nút trong mạng tìm kiếm đã cấu hình để tìm kiếm tài liệu phân tán.

#### Định nghĩa Anchor
`SearchNetworkNode` đại diện cho một nút tìm kiếm riêng lẻ giao tiếp với nút master.

#### Bước 1: Khởi tạo Triển khai  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Đăng ký Sự kiện cho Nút Master

#### Tổng quan
Đăng ký các sự kiện trên nút master để giám sát và quản lý hoạt động mạng một cách hiệu quả.

#### Định nghĩa Anchor
`SearchNetworkNodeEvents` cung cấp các callback cho việc lập chỉ mục, thực thi truy vấn và xử lý lỗi.

#### Bước 1: Xác định Nút Master
Chọn nút đầu tiên làm master của bạn:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Bước 2: Đăng ký Sự kiện
Đăng ký các sự kiện bằng cách sử dụng:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Lập chỉ mục Tài liệu

#### Tổng quan
Lập chỉ mục tài liệu để thực hiện các thao tác tìm kiếm hiệu quả. Bước này quan trọng để đảm bảo mạng của bạn có thể nhanh chóng truy xuất dữ liệu cần thiết.

#### Định nghĩa Anchor
`SearchIndex` là đối tượng cốt lõi lưu trữ các token có thể tìm kiếm và siêu dữ liệu cho mỗi tệp đã lập chỉ mục.

#### Bước 1: Thêm Thư mục vào Chỉ mục
Chỉ định các thư mục chứa tài liệu của bạn:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Chức năng Tìm kiếm – Sử dụng Cơ bản

#### Tổng quan
Thực hiện các thao tác tìm kiếm cơ bản trên các nút trong mạng.

#### Trả lời Trực tiếp
Gọi `SearchNetwork.Query("your term")` trên nút master để lấy ngay các tài liệu phù hợp. Phương thức trả về một tập hợp các đối tượng `SearchResult` bao gồm đường dẫn tệp và điểm liên quan.  
`SearchNetwork.Query` là một phương thức thực hiện truy vấn tìm kiếm trên toàn mạng và trả về các kết quả phù hợp.

#### Bước 1: Xác định Tham số Tìm kiếm  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Chức năng Tìm kiếm Nâng cao

#### Tổng quan
Sử dụng các kỹ thuật tìm kiếm nâng cao với các tham số tùy chỉnh để có kết quả chính xác hơn.

#### Trả lời Trực tiếp
Triển khai một phương thức xây dựng đối tượng `SearchOptions`, thiết lập các thuộc tính `UseFuzzySearch`, `Highlight` và `PageSize`, sau đó truyền nó vào `SearchNetwork.QueryAdvanced`. Điều này sẽ tạo ra các kết quả có phân trang, được đánh dấu và bật tính năng khớp mờ.  
`SearchNetwork.QueryAdvanced` là một phương thức chạy truy vấn với các tùy chọn nâng cao như khớp mờ và phân trang.

#### Bước 1: Triển khai Phương thức Tìm kiếm Nâng cao  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Áp dụng Redaction cho Tệp PDF

#### Tổng quan
Bảo vệ thông tin nhạy cảm bằng cách redaction nội dung PDF trước khi lưu hoặc chia sẻ.

#### Trả lời Trực tiếp
Tạo một thể hiện `Redactor`, tải PDF mục tiêu, định nghĩa một `RedactionPattern` (ví dụ: regex SSN), gọi `redactor.Apply(pattern)`, và cuối cùng lưu tài liệu đã redaction. Quá trình này đảm bảo dữ liệu cá nhân bị xóa vĩnh viễn.

#### Định nghĩa Anchor
`Redactor` là lớp chính trong GroupDocs.Redaction xử lý tài liệu và áp dụng các quy tắc redaction.

#### Quy trình Ví dụ (không có khối mã mới)
1. Khởi tạo `Redactor` với giấy phép của bạn.  
2. Tải PDF bằng `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` đại diện cho một quy tắc chỉ định văn bản hoặc mẫu cần redaction. Định nghĩa các mẫu như `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Thực thi `redactor.Apply(pattern)`.  
5. Lưu kết quả bằng `redactor.Save("sample_redacted.pdf")`.

### Ứng dụng Thực tiễn

#### Các trường hợp sử dụng thực tế
1. **Quản lý Tài liệu Pháp lý** – Tìm kiếm hợp đồng hiệu quả và tự động redaction các định danh khách hàng.  
2. **Hồ sơ Y tế** – Tìm kiếm ghi chú bệnh nhân đồng thời đảm bảo redaction PHI tuân thủ HIPAA.  
3. **Tuân thủ Doanh nghiệp** – Quét các giao tiếp nội bộ để tìm các thuật ngữ bị cấm và redaction trước khi lưu trữ.

## Kết luận 
Hướng dẫn này cung cấp một lộ trình toàn diện cho **tạo chỉ mục tìm kiếm .NET** giải pháp có khả năng mở rộng, lập chỉ mục nhanh chóng và bảo vệ dữ liệu bằng redaction. Bằng cách cấu hình các nút, lập chỉ mục tài liệu, tận dụng các tính năng tìm kiếm nâng cao và áp dụng redaction, các nhà phát triển có thể cải thiện đáng kể quy trình quản lý tài liệu đồng thời duy trì các tiêu chuẩn bảo mật nghiêm ngặt.

## Câu hỏi thường gặp

**Q: Làm thế nào để thiết lập một mạng tìm kiếm phân tán trong .NET với GroupDocs?**  
A: Xác định đường dẫn cơ sở và cổng, sau đó gọi `SearchNetworkDeployment.Deploy()` để khởi chạy các nút master và worker trên các máy.

**Q: Tôi có thể thực hiện tìm kiếm nâng cao với nhiều tham số trong GroupDocs không?**  
A: Có—sử dụng `SearchOptions` để kết hợp khớp mờ, hỗ trợ ký tự đại diện và đánh dấu kết quả trong một truy vấn duy nhất.

**Q: Có thể giám sát hoạt động mạng trên nút master không?**  
A: Chắc chắn—đăng ký `SearchNetworkNodeEvents` như `IndexingCompleted` và `QueryExecuted` để có thông tin thời gian thực.

**Q: Làm thế nào để áp dụng redaction cho tệp PDF bằng GroupDocs?**  
A: Khởi tạo một `Redactor`, tải PDF, định nghĩa các đối tượng `RedactionPattern` (regex hoặc chuỗi nguyên mẫu), gọi `Apply`, và lưu tài liệu đã được làm sạch.

**Q: Cách dễ nhất để cải thiện hiệu suất tìm kiếm trong môi trường mạng là gì?**  
A: Lập chỉ mục đầy đủ bộ tài liệu của bạn trước khi truy vấn, phân phối các nút để sử dụng xử lý song song, và tinh chỉnh `SearchOptions` cho bộ nhớ đệm và phân trang.

---

**Last Updated:** 2026-06-12  
**Tested With:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Author:** GroupDocs

## Các hướng dẫn liên quan

- [Chỉ mục Tài liệu .NET Master với GroupDocs.Search&#58; Hướng dẫn Toàn diện](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Chỉ mục Tài liệu Master và Truy vấn Tìm kiếm Nâng cao với GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Làm chủ GroupDocs Search và Redaction trong .NET&#58; Quản lý Tài liệu Nâng cao](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
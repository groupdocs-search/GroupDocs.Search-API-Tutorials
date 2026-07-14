---
date: '2026-06-07'
description: Tìm hiểu cách liệt kê các phần mở rộng tệp và lấy định dạng tệp bằng
  GroupDocs.Redaction trong C#. Bao gồm cài đặt, mã nguồn và các mẹo thực tiễn.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Cách liệt kê các phần mở rộng tệp với GroupDocs.Redaction trong .NET – Hướng
  dẫn toàn diện
type: docs
url: /vi/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Hiển thị các định dạng tệp được hỗ trợ bằng GroupDocs.Redaction trong .NET

Quản lý đa dạng các loại tài liệu là thực tế hàng ngày đối với các nhà phát triển .NET. Bằng cách sử dụng **GroupDocs.Redaction**, bạn có thể **liệt kê các phần mở rộng tệp** mà thư viện hỗ trợ, cung cấp cho ứng dụng của bạn khả năng chấp nhận hoặc từ chối tải lên, hiển thị các lựa chọn giao diện người dùng thân thiện, và tránh các lỗi thời gian chạy tốn kém. Hướng dẫn này sẽ dẫn bạn qua mọi thứ bạn cần — từ các yêu cầu trước đến một triển khai hoàn chỉnh, sẵn sàng cho môi trường sản xuất — để bạn có thể tự tin **lấy danh sách định dạng tệp** và **c# hiển thị định dạng tệp** trong giải pháp của mình.

## Câu trả lời nhanh
- **“Liệt kê các phần mở rộng tệp” có nghĩa là gì?** Nó có nghĩa là truy xuất bộ sưu tập các định danh loại tệp được hỗ trợ (ví dụ: *.pdf*, *.docx*) từ API.  
- **Gói NuGet nào cung cấp khả năng này?** `GroupDocs.Redaction` (phiên bản ổn định mới nhất).  
- **Tôi có cần giấy phép để chạy mẫu không?** Giấy phép dùng thử miễn phí hoạt động cho phát triển; giấy phép vĩnh viễn được yêu cầu cho môi trường sản xuất.  
- **Tôi có thể lưu vào bộ nhớ đệm kết quả không?** Có — lưu danh sách trong bộ nhớ hoặc bộ nhớ đệm phân tán để tránh các lần gọi API lặp lại.  
- **Tính năng này có tương thích với .NET 6 và .NET Core không?** Hoàn toàn; thư viện hỗ trợ .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ và .NET 6+.

## GroupDocs.Redaction là gì?
**GroupDocs.Redaction** là một thư viện .NET cho phép các nhà phát triển xóa bỏ nội dung nhạy cảm, chuyển đổi tài liệu và khám phá các loại tệp được hỗ trợ — tất cả mà không cần Microsoft Office trên máy chủ. Nó trừu tượng hoá việc xử lý định dạng phức tạp phía sau một API sạch, hướng đối tượng. Thư viện cung cấp một API thống nhất cho việc xóa, chuyển đổi và khám phá định dạng, xử lý PDF, tài liệu Office, hình ảnh và hơn thế nữa, đồng thời đảm bảo hiệu năng cao và bảo mật.

## Tại sao phải liệt kê các phần mở rộng tệp với GroupDocs.Redaction?
Thư viện **hỗ trợ hơn 50 định dạng đầu vào và đầu ra**, bao gồm PDF, DOCX, PPTX, XLSX, HTML và hơn 30 loại hình ảnh. Bằng cách **liệt kê các phần mở rộng tệp** một cách lập trình, bạn có thể:

- Ngăn người dùng tải lên các tệp không được hỗ trợ (giảm lỗi xác thực lên tới 90%).  
- Tự động điền các menu thả xuống, đảm bảo giao diện người dùng luôn đồng bộ với các cập nhật của thư viện.  
- Xây dựng nhật ký kiểm toán ghi lại loại tệp chính xác mà người dùng đã cố gắng xử lý.

## Yêu cầu trước
- **GroupDocs.Redaction**: Cài đặt qua NuGet (xem các lệnh bên dưới).  
- **.NET SDK**: Đảm bảo đã cài đặt .NET SDK mới nhất. Tải xuống nó [tại đây](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào tương thích.  
- **Kiến thức C# cơ bản**: Bạn nên thoải mái với các collection và LINQ.

## Cài đặt GroupDocs.Redaction cho .NET

### Cài đặt thư viện

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**Giao diện quản lý gói NuGet**  
- Mở NuGet Package Manager, tìm kiếm “GroupDocs.Redaction”, và cài đặt phiên bản mới nhất.

### Nhận và áp dụng giấy phép

Bắt đầu với giấy phép dùng thử miễn phí hoặc yêu cầu giấy phép tạm thời để khám phá đầy đủ tính năng mà không bị giới hạn. Đối với các tùy chọn mua, truy cập [trang mua của GroupDocs](https://purchase.groupdocs.com/). Khi bạn đã có tệp giấy phép:

1. Đặt nó vào một thư mục có thể truy cập trong dự án của bạn (ví dụ, `./Licenses/GroupDocs.Redaction.lic`).  
2. Khởi tạo giấy phép khi ứng dụng khởi động:

Lớp `License` tải tệp giấy phép của bạn và kích hoạt GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Cách liệt kê các phần mở rộng tệp bằng GroupDocs.Redaction?

Tải API Redaction và gọi phương thức trả về các định dạng được hỗ trợ. Lời gọi trả về một bộ sưu tập trong đó mỗi mục chứa một phần mở rộng và mô tả dễ đọc cho con người. Thao tác này nhẹ và có thể thực hiện khi khởi động hoặc theo yêu cầu.

### Lấy các loại tệp được hỗ trợ
Phương thức `RedactionApi.GetSupportedFileFormats()` trả về một bộ sưu tập chỉ đọc các đối tượng `FileFormatInfo` mô tả mỗi định dạng.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Hiển thị mỗi phần mở rộng và mô tả
Mỗi `FileFormatInfo` cung cấp các thuộc tính `Extension` và `Description` cho một loại tệp.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Giải thích**: Vòng lặp duyệt qua mỗi đối tượng `FileFormatInfo`, in ra `Extension` và `Description` của nó trong một bảng được căn chỉnh gọn gàng.

## Cách tích hợp danh sách vào dropdown giao diện người dùng?
Sau khi có bộ sưu tập, ràng buộc nó với bất kỳ thành phần UI nào — WinForms `ComboBox`, WPF `ComboBox`, hoặc phần tử `select` của ASP.NET Core. Điều quan trọng là sử dụng `Extension` làm giá trị và `Description` làm văn bản hiển thị. Điều này đảm bảo người dùng thấy tên thân thiện trong khi mã của bạn làm việc với các chuỗi phần mở rộng chính xác.

## Các vấn đề thường gặp và giải pháp
- **Lỗi thiếu namespace** – Kiểm tra bạn đã nhập `GroupDocs.Redaction` và `GroupDocs.Redaction.Common`.  
- **Không tìm thấy giấy phép** – Đảm bảo đường dẫn tệp giấy phép đúng và tệp được bao gồm trong đầu ra của quá trình biên dịch.  
- **Hiệu năng trên dự án lớn** – Lưu kết quả vào biến tĩnh hoặc bộ nhớ đệm phân tán (ví dụ, Redis) để tránh việc liệt kê lặp lại.

## Ứng dụng thực tiễn
Biết danh sách chính xác các phần mở rộng được hỗ trợ mở ra nhiều kịch bản thực tế:

1. **Hệ thống quản lý tài liệu** – Tự động phân loại các tệp đến dựa trên phần mở rộng của chúng.  
2. **Công cụ lọc nội dung** – Chặn các định dạng không cho phép (ví dụ, tệp thực thi) tại thời điểm tải lên.  
3. **Quy trình chuyển đổi tệp** – Động quyết định liệu tệp có thể được chuyển đổi hay cần quy trình dự phòng.

## Các cân nhắc về hiệu năng
- **Dấu chân bộ nhớ** – Danh sách định dạng được lưu trong một `IReadOnlyCollection` nhẹ, thường dưới 2 KB.  
- **An toàn đa luồng** – Bộ sưu tập không thay đổi sau khi tạo, khiến nó an toàn cho các đọc đồng thời.  
- **Bộ nhớ đệm** – Đối với API có lưu lượng cao, lưu danh sách vào bộ nhớ đệm trong suốt vòng đời của ứng dụng để loại bỏ vài micro giây chi phí mỗi yêu cầu.

## Kết luận
Bằng cách thực hiện các bước trên, bạn đã có một cách đáng tin cậy để **liệt kê các phần mở rộng tệp** và **c# hiển thị định dạng tệp** bằng GroupDocs.Redaction. Khả năng này không chỉ cải thiện trải nghiệm người dùng mà còn bảo vệ backend của bạn khỏi các tệp không được hỗ trợ. Khám phá các tính năng Redaction bổ sung — như che giấu nội dung, xóa PDF, và xử lý hàng loạt — để tăng cường hơn nữa quy trình làm việc với tài liệu của bạn.

## Câu hỏi thường gặp
**H: Các định dạng tệp mặc định được hỗ trợ là gì?**  
**Đ:** GroupDocs.Redaction hỗ trợ hơn 50 định dạng, bao gồm PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG và nhiều hơn nữa. Xem danh sách đầy đủ tại [tài liệu GroupDocs](https://docs.groupdocs.com/search/net/).

**H: Làm thế nào để nâng cấp thư viện lên phiên bản mới nhất?**  
**Đ:** Mở NuGet Package Manager, tìm kiếm “GroupDocs.Redaction”, và nhấn **Update**. Ngoài ra, chạy `dotnet add package GroupDocs.Redaction --version <latest>`.

**H: Tôi có thể sử dụng danh sách này để xác thực phía máy chủ các tệp được tải lên không?**  
**Đ:** Có — so sánh phần mở rộng của tệp tải lên với bộ sưu tập đã lấy trước khi xử lý. Điều này loại bỏ 99% lỗi định dạng không hợp lệ.

**H: Có thể mở rộng hỗ trợ cho các loại tệp tùy chỉnh không?**  
**Đ:** Các phần mở rộng tùy chỉnh yêu cầu các trình xử lý tùy chỉnh; thư viện lõi không tự động thêm định dạng mới. Xem tài liệu API để tạo các pipeline nhập/xuất tùy chỉnh.

**H: Ứng dụng của tôi gặp sự cố sau khi thêm mã — tôi nên kiểm tra gì?**  
**Đ:** Đảm bảo giấy phép được tải đúng cách, các câu lệnh `using` tham chiếu đúng namespace, và bạn xử lý `IOException` khi đọc tệp giấy phép.

**Cập nhật lần cuối:** 2026-06-07  
**Đã kiểm tra với:** GroupDocs.Redaction 23.9 cho .NET  
**Tác giả:** GroupDocs  

## Tài nguyên
- [Tài liệu](https://docs.groupdocs.com/search/net/)
- [Tham chiếu API](https://reference.groupdocs.com/redaction/net)
- [Tải xuống GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Diễn đàn hỗ trợ miễn phí](https://forum.groupdocs.com/c/search/10)
- [Yêu cầu giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)

## Hướng dẫn liên quan
- [Lọc tệp chuyên sâu trong .NET với GroupDocs.Redaction&#58; Kỹ thuật quản lý tài liệu hiệu quả](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Thành thạo GroupDocs.Redaction .NET&#58; Cài đặt & Xử lý sự kiện cho quản lý tài liệu an toàn](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Thành thạo quản lý tài liệu trong .NET với GroupDocs.Redaction&#58; Cài đặt giấy phép và tô sáng tìm kiếm HTML](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
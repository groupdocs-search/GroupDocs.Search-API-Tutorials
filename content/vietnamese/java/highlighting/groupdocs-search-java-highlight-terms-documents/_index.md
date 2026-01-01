---
date: '2025-12-26'
description: Tìm hiểu cách tìm kiếm và đánh dấu văn bản trong tài liệu bằng GroupDocs.Search
  cho Java. Khám phá các kỹ thuật để đánh dấu toàn bộ tài liệu và các đoạn văn bản.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Tìm kiếm và làm nổi bật văn bản với GroupDocs.Search cho Java
type: docs
url: /vi/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Tìm kiếm và Đánh dấu Văn bản trong Tài liệu bằng GroupDocs.Search cho Java

Trong thời đại số hiện nay, **tìm kiếm và đánh dấu văn bản** trên các bộ sưu tập tài liệu khổng lồ là một yêu cầu phổ biến. Dù bạn đang xây dựng công cụ rà soát pháp lý, cổng thông tin nghiên cứu học thuật, hay bảng điều khiển hỗ trợ khách hàng, khả năng nhanh chóng xác định và nhấn mạnh các thuật ngữ quan trọng sẽ cải thiện đáng kể tính khả dụng. Trong hướng dẫn toàn diện này, bạn sẽ khám phá cách triển khai **tìm kiếm và đánh dấu văn bản** với GroupDocs.Search cho Java — bao gồm cả việc đánh dấu toàn bộ tài liệu và đánh dấu theo đoạn để cung cấp ngữ cảnh ngắn gọn.

## Câu trả lời nhanh
- **“Tìm kiếm và đánh dấu văn bản” có nghĩa là gì?** Nó đề cập đến việc xác định các thuật ngữ truy vấn trong tài liệu và làm nổi bật chúng một cách trực quan (ví dụ: bằng màu nền).  
- **Thư viện nào cung cấp khả năng này?** GroupDocs.Search cho Java.  
- **Có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; cần giấy phép đầy đủ cho môi trường sản xuất.  
- **Có thể tùy chỉnh màu đánh dấu không?** Có — bất kỳ màu RGB nào cũng có thể đặt qua `HighlightOptions`.  
- **Có hỗ trợ đánh dấu theo đoạn không?** Hoàn toàn có; bạn có thể định nghĩa các từ trước/sau kết quả khớp để tạo các đoạn trích ngắn gọn.

## Tìm kiếm và Đánh dấu Văn bản là gì?
Tìm kiếm và đánh dấu văn bản là quá trình quét chỉ mục tài liệu dựa trên một truy vấn cho trước, lấy ra các tài liệu phù hợp, và sau đó đánh dấu mỗi lần xuất hiện của từ khóa trong đầu ra tài liệu (HTML, PDF, v.v.). Dấu hiệu trực quan này giúp người dùng cuối nhanh chóng nhận ra thông tin liên quan.

## Tại sao nên dùng GroupDocs.Search cho Java?
- **Chỉ mục hiệu suất cao** với khả năng nén cấu hình được.  
- **API đánh dấu phong phú** hoạt động trên toàn bộ tài liệu và trên các đoạn tùy chỉnh.  
- **Hỗ trợ đa định dạng** (DOCX, PDF, PPTX, TXT và nhiều hơn nữa).  
- **Tích hợp Maven dễ dàng** và API rõ ràng, tập trung vào Java.

## Điều kiện tiên quyết
- Java Development Kit (JDK) 8 hoặc mới hơn.  
- Maven để quản lý phụ thuộc.  
- Một IDE như IntelliJ IDEA hoặc Eclipse.  
- Kiến thức cơ bản về cú pháp Java.

## Cài đặt GroupDocs.Search cho Java

Thêm kho lưu trữ và phụ thuộc GroupDocs vào file `pom.xml` của bạn:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

Bạn cũng có thể tải JAR mới nhất trực tiếp từ trang chính thức: [phiên bản GroupDocs.Search cho Java](https://releases.groupdocs.com/search/java/).

### Nhận Giấy phép
Bắt đầu với bản dùng thử miễn phí hoặc lấy giấy phép tạm thời để đánh giá. Đối với triển khai sản xuất, mua giấy phép đầy đủ để mở khóa tất cả các tính năng.

## Hướng dẫn Triển khai

Quy trình triển khai được chia thành hai phần thực tiễn: **đánh dấu toàn bộ tài liệu** và **đánh dấu trong các đoạn**. Cả hai phần đều bao gồm các bước cần thiết để **đánh dấu tài liệu Java** bằng GroupDocs.Search.

### Cấu hình Cài đặt Chỉ mục
Trước khi tạo chỉ mục, cấu hình lưu trữ để sử dụng nén cao — giúp giảm dung lượng đĩa đồng thời duy trì tốc độ tìm kiếm.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Đánh dấu Toàn bộ Tài liệu

#### Bước 1: Tạo và Điền Dữ liệu vào Chỉ mục
Tạo thư mục chỉ mục và thêm tất cả các tệp nguồn bạn muốn tìm kiếm.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Bước 2: Thực hiện Tìm kiếm và Áp dụng Đánh dấu
Tìm kiếm từ khóa (ví dụ: `ipsum`) và tạo file HTML với các kết quả đã được đánh dấu.

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

**Giải thích các tùy chọn chính**
- **Compression** – nén cao giúp tiết kiệm không gian lưu trữ.  
- **HighlightColor** – đặt bất kỳ giá trị RGB nào để phù hợp với bảng màu UI của bạn.  
- **UseInlineStyles** – `false` tạo HTML sạch, có thể được định dạng toàn cục bằng CSS.

### Đánh dấu Trong Các Đoạn

#### Bước 1: Chỉ mục và Tìm kiếm (giống như trên)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Bước 2: Định nghĩa Ngữ cảnh Đoạn và Đánh dấu
Xác định số lượng từ trước và sau kết quả khớp sẽ xuất hiện trong mỗi đoạn.

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

#### Bước 3: Lấy và Ghi Các Đoạn Đã Đánh dấu
Thu thập các đoạn đã tạo và ghi chúng vào một file HTML.

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Ứng dụng Thực tiễn
1. **Rà soát Tài liệu Pháp lý** – nhanh chóng đánh dấu các điều luật, điều khoản hoặc tham chiếu vụ án.  
2. **Nghiên cứu Học thuật** – hiển thị nhanh các thuật ngữ quan trọng trong hàng chục file PDF và Word.  
3. **Hỗ trợ Khách hàng** – xác định số đơn hàng hoặc mã lỗi trong lịch sử ticket.

## Các yếu tố về Hiệu suất
- **Kích thước Chỉ mục** – nén cao (`Compression.High`) giảm footprint trên đĩa.  
- **Ngữ cảnh Đoạn** – giá trị `termsBefore/After` lớn hơn tăng độ chính xác nhưng có thể ảnh hưởng tới tốc độ.  
- **Quản lý Bộ nhớ** – giám sát heap JVM khi chỉ mục khối lượng lớn; cân nhắc chỉ mục tăng dần cho các bộ dữ liệu rất lớn.

## Các vấn đề Thường gặp và Giải pháp
- **Lỗi Khi Chỉ mục** – kiểm tra lại đường dẫn tệp và đảm bảo ứng dụng có quyền đọc/ghi.  
- **Không Có Đánh dấu** – xác nhận `UseInlineStyles` phù hợp với định dạng đầu ra (HTML vs. PDF).  
- **Màu Không Áp dụng** – chắc chắn giá trị RGB nằm trong khoảng 0‑255 và trình xem HTML hỗ trợ kiểu dáng.

## Câu hỏi Thường gặp

**H: Lợi ích của việc sử dụng GroupDocs.Search cho Java là gì?**  
Đ: Nó cung cấp chỉ mục nhanh, mở rộng, khả năng tùy chỉnh đánh dấu và hỗ trợ nhiều định dạng tài liệu.

**H: Làm sao tích hợp GroupDocs.Search với API REST?**  
Đ: Phơi bày các phương thức tìm kiếm và đánh dấu qua các controller Spring Boot, trả về HTML hoặc payload JSON.

**H: Thư viện có xử lý các tệp được bảo vệ bằng mật khẩu không?**  
Đ: Có — cung cấp mật khẩu khi thêm tài liệu vào chỉ mục.

**H: Có thể tùy chỉnh markup đánh dấu ngoài màu sắc không?**  
Đ: Hoàn toàn có; bạn có thể chèn lớp CSS qua `HighlightOptions` hoặc chỉnh sửa HTML sau khi tạo.

**H: Phiên bản nào đã được kiểm thử cho hướng dẫn này?**  
Đ: Mã đã được xác thực với GroupDocs.Search 25.4.

---

**Cập nhật lần cuối:** 2025-12-26  
**Kiểm thử với:** GroupDocs.Search 25.4  
**Tác giả:** GroupDocs
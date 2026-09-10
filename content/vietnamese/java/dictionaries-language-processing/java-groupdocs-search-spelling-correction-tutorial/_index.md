---
date: '2026-09-02'
description: Tìm hiểu cách tạo search index java và bật spelling correction bằng cách
  sử dụng GroupDocs.Search. Thực hiện các hướng dẫn từng bước để thêm tài liệu, cấu
  hình max mistake count và cải thiện search accuracy.
keywords:
- create search index java
- spelling correction java
- GroupDocs.Search tutorial
lastmod: '2026-09-02'
og_description: Tìm hiểu cách tạo search index java và bật spelling correction bằng
  cách sử dụng GroupDocs.Search. Thực hiện các hướng dẫn từng bước để thêm tài liệu,
  cấu hình max mistake count và cải thiện search accuracy.
og_image_alt: Guide showing Java code that creates a search index and configures spelling
  correction with GroupDocs.Search
og_title: Cách tạo search index java và bật spelling
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  headline: How to create search index java and enable spelling
  type: TechArticle
- description: Learn how to create search index java and enable spelling correction
    using GroupDocs.Search. Follow step‑by‑step instructions to add documents, configure
    max mistake count, and improve search accuracy.
  name: How to create search index java and enable spelling
  steps:
  - name: '**Library systems** – automatically fix misspelled book titles or author
      names.'
    text: '**Library systems** – automatically fix misspelled book titles or author
      names.'
  - name: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
    text: '**E‑commerce platforms** – correct product name typos to increase conversion
      rates.'
  - name: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
    text: '**Content management** – help editorial staff locate articles even with
      imperfect keywords.'
  type: HowTo
- questions:
  - answer: GroupDocs.Search is a Java library that provides fast indexing, advanced
      query capabilities, and built‑in spelling correction for any Java application.
    question: What is GroupDocs.Search?
  - answer: Visit the official site to download a free trial or purchase a full license;
      a temporary key is also available for short‑term testing.
    question: How do I obtain a license for GroupDocs.Search?
  - answer: Yes, it works seamlessly with Spring, Jakarta EE, and any standard Java
      application.
    question: Can I integrate GroupDocs.Search with other Java frameworks?
  - answer: Incorrect folder paths, missing file permissions, or absent Maven dependencies
      are the typical culprits.
    question: What are common issues when setting up an index?
  - answer: It automatically rewrites misspelled queries to their closest correct
      terms, returning more relevant hits and reducing user frustration.
    question: How does spell correction improve search results?
  type: FAQPage
tags:
- create search index java
- GroupDocs.Search
- Java search
title: Cách tạo search index java và bật spelling
type: docs
url: /vi/java/dictionaries-language-processing/java-groupdocs-search-spelling-correction-tutorial/
weight: 1
---

# Cách tạo chỉ mục tìm kiếm java và bật chính tả

Trong các ứng dụng Java hiện đại, cung cấp kết quả tìm kiếm chính xác là một tính năng bắt buộc. Hướng dẫn này cho thấy **how to create search index java** và bật tính năng sửa lỗi chính tả với GroupDocs.Search, để người dùng nhận được các kết quả liên quan ngay cả khi họ gõ sai truy vấn. Bạn sẽ thấy cách thiết lập thư viện, thêm tài liệu, cấu hình số lượng lỗi tối đa, và thực hiện tìm kiếm chịu lỗi chính tả — tất cả mà không cần viết một dòng mã cấu hình bổ sung.

## Câu trả lời nhanh
- **Chức năng “enable spelling” là gì?** Nó kích hoạt bộ kiểm tra chính tả tích hợp, tự động viết lại các từ bị viết sai thành dạng đúng nhất có thể trong quá trình tìm kiếm.  
- **Thư viện nào cung cấp tính năng này?** GroupDocs.Search for Java.  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép đầy đủ là bắt buộc cho môi trường sản xuất.  
- **Tôi có thể kiểm soát mức độ chịu lỗi không?** Có – sử dụng `setMaxMistakeCount` để định nghĩa số lượng lỗi chính tả cho phép cho mỗi truy vấn.  
- **Có phù hợp với các chỉ mục lớn không?** Chắc chắn – engine xử lý các chỉ mục có hàng triệu bản ghi trong khi giữ độ trễ truy vấn dưới 100 ms trên phần cứng máy chủ tiêu chuẩn.

## GroupDocs.Search là gì?
GroupDocs.Search là một thư viện Java cung cấp khả năng lập chỉ mục toàn văn nhanh và các tính năng tìm kiếm nâng cao, bao gồm cả sửa lỗi chính tả tích hợp. Nó hỗ trợ hơn 50 định dạng đầu vào và có thể xử lý các tài liệu hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ.

## Tại sao bật tính năng sửa lỗi chính tả trong các ứng dụng Java?
- **Tăng sự hài lòng của người dùng** – khách truy cập nhận được kết quả chính xác ngay cả khi gõ không hoàn hảo.  
- **Giảm tỷ lệ thoát** – các kết quả chính xác giữ người dùng ở lại lâu hơn.  
- **Áp dụng đa lĩnh vực** – từ danh mục thư viện đến tìm kiếm sản phẩm thương mại điện tử, sửa lỗi chính tả cải thiện độ liên quan ở mọi nơi.

## Yêu cầu trước
- Java Development Kit (JDK) đã được cài đặt.  
- Kiến thức cơ bản về Java và Maven.  
- Hiểu biết về các khái niệm lập chỉ mục.  
- Một bản dùng thử hoặc khóa giấy phép GroupDocs.Search.

### Cài đặt GroupDocs.Search cho Java
Tích hợp thư viện vào dự án Maven của bạn.

**Cài đặt Maven**  
Thêm kho lưu trữ và phụ thuộc vào tệp `pom.xml` của bạn:

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

**Tải trực tiếp**  
Hoặc, tải phiên bản mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
Nhận giấy phép dùng thử miễn phí để đánh giá. Đối với môi trường sản xuất, mua giấy phép đầy đủ hoặc yêu cầu khóa tạm thời từ trang chính thức.

## Làm thế nào để tạo chỉ mục tìm kiếm trong Java?
`SearchIndex` là lớp chính đại diện cho một chỉ mục có thể tìm kiếm được lưu trên đĩa.  
Tạo một thể hiện `SearchIndex` trỏ tới một thư mục trên đĩa, sau đó thêm tài liệu từ thư mục nguồn. Engine xây dựng một chỉ mục đảo ngược giúp tra cứu nhanh. Bạn có thể gọi `index.add()` cho mỗi tệp; thư viện tự động trích xuất văn bản dựa trên loại tệp.

## Làm sao bật tính năng sửa lỗi chính tả?
`getSpellingOptions()` trả về đối tượng cấu hình chính tả cho chỉ mục, cho phép bạn bật hoặc điều chỉnh các tính năng kiểm tra chính tả.  
Bật tính năng chính tả bằng cách gọi `index.getSpellingOptions().setEnabled(true)`. Điều này yêu cầu engine phân tích các từ truy vấn và đề xuất các lựa chọn đã được sửa khi phát hiện sự không khớp. Tính năng này hoạt động ngay lập tức cho tất cả các ngôn ngữ được lập chỉ mục mà thư viện hỗ trợ.

## Cài đặt max mistake count là gì?
`setMaxMistakeCount` cấu hình số lượng chỉnh sửa ký tự tối đa mà bộ kiểm tra chính tả sẽ chịu được cho mỗi từ.  
`setMaxMistakeCount(int)` định nghĩa số lượng chỉnh sửa ký tự (chèn, xóa, thay thế) tối đa mà bộ kiểm tra chính tả sẽ chịu cho mỗi từ. Đặt giá trị **2** cho phép engine sửa các lỗi thường gặp gồm hai ký tự trong khi tránh các sửa chữa quá mức có thể trả về kết quả không liên quan.

## Cách thực hiện tìm kiếm có sửa lỗi chính tả
`search()` thực thi một truy vấn trên chỉ mục và trả về một đối tượng `SearchResult` chứa các kết quả khớp và bất kỳ từ nào đã được sửa.  
Thực hiện truy vấn tìm kiếm bằng phương thức `search()`. Nếu truy vấn chứa các từ bị viết sai, engine sẽ trả về một `SearchResult` bao gồm các từ đã được sửa và danh sách các tài liệu có liên quan nhất. Bạn có thể hiển thị cả truy vấn gốc và phiên bản đã sửa cho người dùng để minh bạch.  
`SearchResult` chứa danh sách các tài liệu khớp và thông tin về các sửa chữa truy vấn.

## Ứng dụng thực tiễn
1. **Hệ thống thư viện** – tự động sửa các tiêu đề sách hoặc tên tác giả bị viết sai.  
2. **Nền tảng thương mại điện tử** – sửa lỗi chính tả trong tên sản phẩm để tăng tỷ lệ chuyển đổi.  
3. **Quản lý nội dung** – giúp nhân viên biên tập tìm kiếm bài viết ngay cả khi từ khóa không hoàn hảo.

## Các cân nhắc về hiệu năng
- **Giữ chỉ mục luôn cập nhật** – lập chỉ mục lại các tệp mới hoặc đã thay đổi thường xuyên.  
- **Tinh chỉnh cài đặt bộ nhớ JVM** – cấp phát heap đủ cho các chỉ mục lớn (ví dụ, `-Xmx4g`).  
- **Giám sát sử dụng tài nguyên** – điều chỉnh các flag của garbage‑collector nếu bạn nhận thấy có độ trễ trong quá trình lập chỉ mục hàng loạt.

## Các vấn đề thường gặp & khắc phục
| Triệu chứng | Nguyên nhân khả dĩ | Cách khắc phục |
|------------|---------------------|----------------|
| Không có kết quả sau khi bật tính năng chính tả | Đường dẫn thư mục chỉ mục sai hoặc trống | Xác minh `indexFolder` trỏ tới một chỉ mục hợp lệ và `index.add()` đã thành công |
| Bộ kiểm tra chính tả không sửa các lỗi rõ ràng | `setMaxMistakeCount` được đặt quá thấp | Tăng số lượng lên 2 hoặc 3 để có độ chịu lỗi cao hơn |
| Ứng dụng bị sập khi xử lý tập tài liệu lớn | Heap JVM không đủ | Tăng tùy chọn `-Xmx` (ví dụ, `-Xmx4g`) |

## Câu hỏi thường gặp

**Q: GroupDocs.Search là gì?**  
A: GroupDocs.Search là một thư viện Java cung cấp khả năng lập chỉ mục nhanh, khả năng truy vấn nâng cao, và tính năng sửa lỗi chính tả tích hợp cho bất kỳ ứng dụng Java nào.

**Q: Làm sao tôi có thể lấy giấy phép cho GroupDocs.Search?**  
A: Truy cập trang chính thức để tải bản dùng thử miễn phí hoặc mua giấy phép đầy đủ; một khóa tạm thời cũng có sẵn cho việc thử nghiệm ngắn hạn.

**Q: Tôi có thể tích hợp GroupDocs.Search với các framework Java khác không?**  
A: Có, nó hoạt động liền mạch với Spring, Jakarta EE và bất kỳ ứng dụng Java tiêu chuẩn nào.

**Q: Những vấn đề thường gặp khi thiết lập chỉ mục là gì?**  
A: Các đường dẫn thư mục không đúng, thiếu quyền truy cập tệp, hoặc thiếu phụ thuộc Maven là những nguyên nhân thường gặp.

**Q: Sửa lỗi chính tả cải thiện kết quả tìm kiếm như thế nào?**  
A: Nó tự động viết lại các truy vấn bị viết sai thành các từ đúng nhất có thể, trả về các kết quả liên quan hơn và giảm sự bực bội của người dùng.

## Tài nguyên bổ sung
- [Tài liệu](https://docs.groupdocs.com/search/java/)
- [Tham khảo API](https://reference.groupdocs.com/search/java)
- [Tải xuống](https://releases.groupdocs.com/search/java/)
- [Kho GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Diễn đàn hỗ trợ miễn phí](https://forum.groupdocs.com/c/search/10)
- [Giấy phép tạm thời](https://purchase.groupdocs.com/temporary-license/)

---

**Cập nhật lần cuối:** 2026-09-02  
**Kiểm tra với:** GroupDocs.Search 25.4  
**Tác giả:** GroupDocs

```java
import com.groupdocs.search.*;

public class FeatureIndexAndAddDocuments {
    public static void main(String[] args) {
        // Define where the index will be stored
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        
        // Create an Index instance pointing to the specified folder
        Index index = new Index(indexFolder);
        
        // Specify the documents directory for indexing
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";  
        
        // Add documents from this directory to the index
        index.add(documentsFolder);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

public class FeatureSpellingCorrectionOptions {
    public static void main(String[] args) {
        // Instantiate SearchOptions
        SearchOptions options = new SearchOptions();
        
        // Enable spelling correction
        options.getSpellingCorrector().setEnabled(true);
        
        // Allow up to one mistake during search
        options.getSpellingCorrector().setMaxMistakeCount(1);
        
        // Return only the best results after correction
        options.getSpellingCorrector().setOnlyBestResults(true);
    }
}
```

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

public class FeatureSpellingCorrectionSearch {
    public static void main(String[] args) {
        // Create an index in the specified directory
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SpellChecking";
        Index index = new Index(indexFolder);
        
        // Define search options with spelling correction enabled
        SearchOptions options = new SearchOptions();
        options.getSpellingCorrector().setEnabled(true);
        options.getSpellingCorrector().setMaxMistakeCount(1);
        options.getSpellingCorrector().setOnlyBestResults(true);
        
        // Specify a misspelled search query
        String query = "houseohld";
        
        // Execute the spelling‑corrected search
        SearchResult result = index.search(query, options);
    }
}
```

## Hướng dẫn liên quan

- [Cách tạo chỉ mục tài liệu và thêm tài liệu bằng API GroupDocs.Search cho Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Xử lý ngôn ngữ Java – Tạo từ điển đồng nghĩa với GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Từ dừng trong tìm kiếm: Thêm tài liệu vào chỉ mục với GroupDocs.Search Java](/search/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/)
---
date: '2026-02-21'
description: Tìm hiểu cách tạo các dạng số ít và số nhiều trong Java bằng API GroupDocs.Search.
  Tạo một nhà cung cấp dạng từ tùy chỉnh để tìm kiếm chính xác và phân tích văn bản.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Tạo dạng số ít và số nhiều trong Java với GroupDocs.Search
type: docs
url: /vi/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

 keep.

"**Author:** GroupDocs" keep.

Now produce final markdown with translations.

Make sure to keep code block placeholders unchanged.

Let's craft final answer.# Tạo Dạng Số ít Số nhiều trong Java với GroupDocs.Search

Nếu bạn cần **tạo dạng số ít số nhiều trong Java**, một nhà cung cấp dạng từ tùy chỉnh là chìa khóa để giúp công cụ tìm kiếm hoặc phân tích văn bản của bạn hiểu mọi biến thể của một thuật ngữ. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn xây dựng một nhà cung cấp như vậy bằng API Java của GroupDocs.Search, để ứng dụng của bạn có thể tự động khớp “cat”, “cats”, “city”, và “citis” mà không cần nỗ lực thêm.

## Câu trả lời nhanh
- **Nhà cung cấp dạng từ làm gì?** Nó tạo ra các dạng thay thế (số ít, số nhiều, v.v.) của một từ cho trước để các tìm kiếm có thể khớp tất cả các biến thể.  
- **Thư viện nào cần thiết?** GroupDocs.Search cho Java (phiên bản 25.4 hoặc mới hơn).  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí hoạt động cho việc đánh giá; giấy phép vĩnh viễn cần thiết cho môi trường sản xuất.  
- **Phiên bản Java nào được hỗ trợ?** JDK 8 hoặc cao hơn.  
- **Cần bao nhiêu dòng mã?** Khoảng 30 dòng cho một triển khai nhà cung cấp đơn giản.

## Tính năng “Create Word Forms Provider” là gì?
Một thành phần **create word forms provider** là một lớp tùy chỉnh triển khai `IWordFormsProvider`. Nó nhận vào một từ và trả về một mảng các dạng có thể có — số ít, số nhiều, hoặc các biến thể ngôn ngữ khác — dựa trên các quy tắc bạn định nghĩa. Điều này cho phép chỉ mục tìm kiếm xem “cat” và “cats” là tương đương, cải thiện độ bao phủ mà không làm giảm độ chính xác.

## Tại sao nên dùng GroupDocs.Search để tạo dạng từ?
- **Mở rộng tích hợp:** Gắn nhà cung cấp của bạn trực tiếp vào quy trình lập chỉ mục.  
- **Tối ưu hiệu năng:** Xử lý các chỉ mục lớn một cách hiệu quả, và bạn có thể lưu cache kết quả để tăng tốc.  
- **Hỗ trợ đa ngôn ngữ:** Các khái niệm cũng áp dụng cho .NET và các nền tảng khác.

## Yêu cầu trước
Trước khi triển khai **create word forms provider**, hãy chắc chắn rằng bạn đã có:

- **Maven** được cài đặt và JDK 8 hoặc mới hơn được thiết lập trên máy của bạn.  
- Kiến thức cơ bản về phát triển Java và cấu hình `pom.xml` của Maven.  
- Truy cập vào thư viện GroupDocs.Search Java (phiên bản 25.4 hoặc sau).

## Cài đặt GroupDocs.Search cho Java

### Cấu hình Maven

Thêm kho và phụ thuộc vào tệp `pom.xml` của bạn chính xác như dưới đây:

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

### Tải trực tiếp

Ngoài ra, tải JAR mới nhất từ trang phát hành chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Các bước lấy giấy phép

1. **Dùng thử miễn phí:** Đăng ký để dùng thử và khám phá các tính năng cốt lõi.  
2. **Giấy phép tạm thời:** Yêu cầu khóa tạm thời để thử nghiệm kéo dài hơn.  
3. **Mua:** Nhận giấy phép thương mại để sử dụng không giới hạn trong môi trường sản xuất.

### Khởi tạo và cấu hình cơ bản

Đoạn mã sau minh họa cách tạo một chỉ mục — điểm khởi đầu để thêm tài liệu và logic dạng từ:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Hướng dẫn triển khai

Dưới đây chúng tôi sẽ hướng dẫn các bước để **create word forms provider** xử lý các chuyển đổi đơn giản từ số ít sang số nhiều và ngược lại.

### Triển khai SimpleWordFormsProvider

#### Tổng quan
Nhà cung cấp tùy chỉnh của chúng tôi sẽ:

- Loại bỏ hậu tố “es” hoặc “s” để suy đoán dạng số ít.  
- Đổi “y” cuối thành “is” để tạo dạng số nhiều (ví dụ, “city” → “citis”).  
- Thêm “s” và “es” để tạo các ứng cử số nhiều cơ bản.

#### Bước 1 – Tạo khung lớp

Bắt đầu bằng việc định nghĩa một lớp triển khai `IWordFormsProvider`. Giữ nguyên các câu lệnh import:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Bước 2 – Triển khai `getWordForms`

Thêm phương thức xây dựng danh sách các dạng có thể. Khối này chứa logic cốt lõi; bạn có thể mở rộng sau này để bao phủ các quy tắc phức tạp hơn.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Giải thích logic
- **Singularization:** Phát hiện các hậu tố số nhiều phổ biến (`es`, `s`) và loại bỏ chúng để xấp xỉ từ gốc.  
- **Pluralization:** Xử lý các danh từ kết thúc bằng `y` bằng cách thay thế bằng `is`, một quy tắc đơn giản hoạt động cho nhiều từ tiếng Anh.  
- **Suffix Appending:** Thêm `s` và `es` để bao phủ các dạng số nhiều chuẩn mà có thể không được các kiểm tra trước bắt gặp.

#### Mẹo khắc phục sự cố
- **Phân biệt chữ hoa/thường:** Phương thức sử dụng `toLowerCase()` để so sánh, đảm bảo “Cats” và “cats” hoạt động giống nhau.  
- **Trường hợp biên:** Các từ ngắn hơn độ dài hậu tố sẽ bị bỏ qua để tránh trả về chuỗi rỗng.  
- **Hiệu năng:** Đối với từ vựng lớn, cân nhắc lưu cache kết quả trong một `ConcurrentHashMap`.

## Ứng dụng thực tiễn

Triển khai **create word forms provider** có thể nâng cao một số kịch bản thực tế:

1. **Công cụ tìm kiếm:** Người dùng gõ “mouse” cũng nên tìm thấy các tài liệu chứa “mice”. Nhà cung cấp có thể tạo ra các dạng bất quy tắc như vậy.  
2. **Công cụ phân tích văn bản:** Phân tích cảm xúc hoặc trích xuất thực thể trở nên đáng tin cậy hơn khi tất cả các biến thể từ được nhận diện.  
3. **Hệ thống quản lý nội dung:** Tự động tạo thẻ có thể bao gồm các đồng nghĩa số nhiều, cải thiện SEO và liên kết nội bộ.

## Lưu ý về hiệu năng

Khi bạn nhúng nhà cung cấp vào hệ thống sản xuất, hãy ghi nhớ các lời khuyên sau:

- **Cache các dạng thường dùng:** Lưu kết quả trong bộ nhớ để tránh tính lại cùng một từ nhiều lần.  
- **Giám sát heap JVM:** Các chỉ mục lớn có thể tăng áp lực bộ nhớ; điều chỉnh `-Xmx` cho phù hợp.  
- **Sử dụng collection hiệu quả:** `ArrayList` phù hợp cho tập nhỏ, nhưng với hàng ngàn dạng, hãy cân nhắc `HashSet` để loại bỏ trùng lặp nhanh chóng.

**Best Practices**

- Giữ thư viện luôn cập nhật để hưởng lợi từ các bản vá hiệu năng.  
- Đánh giá nhà cung cấp với tải truy vấn thực tế để phát hiện các nút thắt sớm.

## Kết luận

Bạn đã học cách **tạo dạng số ít số nhiều trong Java** bằng một `SimpleWordFormsProvider` tùy chỉnh cùng GroupDocs.Search. Thành phần nhẹ này có thể cải thiện đáng kể độ liên quan của kết quả tìm kiếm và độ chính xác của phân tích ngôn ngữ trong nhiều ứng dụng.

**Bước tiếp theo:**  
- Thử nghiệm các quy tắc ngôn ngữ phức tạp hơn (số nhiều bất quy tắc, stemming).  
- Tích hợp nhà cung cấp vào quy trình lập chỉ mục và đo lường cải thiện độ bao phủ.  
- Khám phá các tính năng khác của GroupDocs.Search như từ điển đồng nghĩa và bộ phân tích tùy chỉnh.

**Kêu gọi hành động:** Hãy thêm `SimpleWordFormsProvider` vào dự án của bạn ngay hôm nay và xem nó làm phong phú trải nghiệm tìm kiếm như thế nào!

## Phần Câu hỏi thường gặp

**1. GroupDocs.Search cho Java là gì?**  
Đó là một thư viện mạnh mẽ cung cấp tìm kiếm toàn văn, lập chỉ mục và các tính năng ngôn ngữ — bao gồm khả năng gắn các nhà cung cấp dạng từ tùy chỉnh.

**2. SimpleWordFormsProvider hoạt động như thế nào?**  
Nó tạo ra các dạng thay thế bằng cách áp dụng các quy tắc dựa trên hậu tố đơn giản (loại bỏ “s/es”, chuyển “y” thành “is”, và thêm “s/es”).

**3. Tôi có thể tùy chỉnh các quy tắc tạo dạng từ không?**  
Chắc chắn. Sửa đổi phương thức `getWordForms` để bao gồm các dạng bất quy tắc, quy tắc đặc thù vùng miền, hoặc tích hợp với từ điển bên ngoài.

**4. Một số ứng dụng phổ biến cho tính năng này là gì?**  
Các công cụ tìm kiếm, pipeline phân tích văn bản và nền tảng CMS đều hưởng lợi từ việc nhận diện các biến thể số ít/số nhiều.

**5. Tôi có cần giấy phép thương mại cho việc sử dụng trong sản xuất không?**  
Có — trong khi bản dùng thử cho phép bạn khám phá API, giấy phép mua sẽ loại bỏ các giới hạn sử dụng và cung cấp hỗ trợ.

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs
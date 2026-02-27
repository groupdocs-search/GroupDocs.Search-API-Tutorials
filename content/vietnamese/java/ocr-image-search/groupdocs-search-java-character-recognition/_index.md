---
date: '2026-01-11'
description: Tìm hiểu cách tạo chỉ mục tìm kiếm tùy chỉnh bằng GroupDocs.Search cho
  Java, cấu hình các ký tự thường và hỗn hợp cho OCR và tìm kiếm hình ảnh nâng cao.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Tạo chỉ mục tìm kiếm tùy chỉnh với nhận dạng ký tự – GroupDocs.Search Java
type: docs
url: /vi/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Tạo chỉ mục tìm kiếm tùy chỉnh với nhận dạng ký tự bằng GroupDocs.Search cho Java

Trong các ứng dụng hiện đại có lượng tài liệu lớn, **việc tạo chỉ mục tìm kiếm tùy chỉnh** có khả năng hiểu các chi tiết tinh tế của văn bản—như dấu gạch ngang, dấu gạch dưới hoặc các ký hiệu đặc thù của ngôn ngữ—là điều cần thiết để truy xuất nhanh chóng và chính xác. Hướng dẫn này sẽ chỉ cho bạn cách cấu hình nhận dạng ký tự trong **GroupDocs.Search cho Java**, bao gồm cả ký tự thường (chữ cái, chữ số, dấu gạch dưới) và ký tự kết hợp (ví dụ: dấu gạch ngang). Khi hoàn thành, bạn sẽ có thể tùy chỉnh một chỉ mục phù hợp với nhu cầu chính xác của kịch bản OCR hoặc tìm kiếm hình ảnh.

## Câu trả lời nhanh
- **What does “create custom search index” mean?** Nó có nghĩa là cấu hình một chỉ mục để xử lý các ký hiệu cụ thể như là chữ cái hoặc ký tự kết hợp, thay vì bỏ qua chúng.  
- **Which library is used?** GroupDocs.Search for Java (v25.4 tại thời điểm viết).  
- **Do I need a license?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép trả phí cần thiết cho môi trường sản xuất.  
- **Can I index both PDFs and images?** Có—GroupDocs.Search hỗ trợ OCR trên hình ảnh và PDF khi được cấu hình đúng.  
- **Is Maven required?** Maven là cách được khuyến nghị để quản lý các phụ thuộc, nhưng bạn cũng có thể sử dụng Gradle hoặc các JAR thủ công.  

## Chỉ mục tìm kiếm tùy chỉnh là gì?
Một chỉ mục tìm kiếm tùy chỉnh cho phép bạn xác định cách công cụ tìm kiếm diễn giải các ký tự. Theo mặc định, nhiều ký hiệu bị bỏ qua, điều này có thể dẫn đến việc không khớp được các trường hợp như số vụ án (`ABC-123`) hoặc đoạn mã (`my_variable`). Việc điều chỉnh từ điển bảng chữ cái cho phép bạn kiểm soát hoàn toàn những gì công cụ coi là văn bản có thể tìm kiếm.

## Tại sao cần cấu hình ký tự thường và ký tự kết hợp?
- **Regular characters** (letters, digits, underscores) được xử lý như các token độc lập, cải thiện khả năng tìm kiếm khớp chính xác.  
- **Blended characters** (hyphens, slashes) nối các từ; việc cấu hình chúng ngăn ngừa việc tách token không mong muốn, điều này quan trọng đối với các tham chiếu pháp lý, mã sản phẩm hoặc việc lập chỉ mục mã nguồn.  

## Yêu cầu trước
- **JDK 8** hoặc phiên bản mới hơn đã được cài đặt.  
- **Maven** để quản lý phụ thuộc.  
- Truy cập vào thư viện **GroupDocs.Search for Java** (tải về qua Maven hoặc trang chính thức).  

### Thư viện và phụ thuộc cần thiết
Thêm các mục repository và dependency vào file `pom.xml` của bạn (như được hiển thị bên dưới). Khối XML phải được giữ nguyên.

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

Bạn cũng có thể tải các JAR mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Cách lấy giấy phép
- **Free Trial** – hoàn hảo cho việc thử nghiệm ban đầu.  
- **Temporary License** – hữu ích cho các chu kỳ phát triển dài hơn.  
- **Production License** – cần thiết cho triển khai thương mại.  

Nhận giấy phép từ cổng thông tin chính thức: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Khởi tạo cơ bản
Đoạn mã dưới đây hiển thị code tối thiểu cần thiết để khởi tạo một chỉ mục trống. Giữ nguyên như hiện tại; chúng ta sẽ xây dựng tiếp sau.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## Cài đặt GroupDocs.Search cho Java

### Cài đặt qua Maven
Cấu hình Maven từ phần *Prerequisites* là tất cả những gì bạn cần. Sau khi thêm, chạy `mvn clean install` để tải các binary.

### Yêu cầu thiết lập môi trường
- Đảm bảo **thư mục chỉ mục** và **thư mục tài liệu** tồn tại trên đĩa.  
- Sử dụng đường dẫn tuyệt đối hoặc cấu hình IDE của bạn để giải quyết đúng các đường dẫn tương đối.

## Hướng dẫn triển khai

Dưới đây chúng tôi sẽ hướng dẫn qua hai tính năng riêng biệt: **regular characters** và **blended characters**. Mỗi tính năng tuân theo cùng một mẫu—định nghĩa đường dẫn, tạo chỉ mục, thiết lập từ điển ký tự, và cuối cùng là lập chỉ mục cho tài liệu của bạn.

### Tính năng 1 – Ký tự thường

#### Tổng quan
Ký tự thường được xử lý như các token độc lập. Điều này lý tưởng khi bạn muốn các chữ số, chữ cái và dấu gạch dưới có thể tìm kiếm chính xác như chúng xuất hiện.

#### Triển khai từng bước

**1️⃣ Set Up Paths**  
Xác định nơi sẽ lưu trữ chỉ mục và nơi các tài liệu nguồn của bạn nằm.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  
Tạo một thể hiện của chỉ mục và xóa bất kỳ cấu hình bảng chữ cái nào đã tồn tại trước đó.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define Regular Characters**  
Xây dựng một mảng ký tự bao gồm các chữ số, chữ Latin và dấu gạch dưới.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index Documents**  
Thêm tất cả các tệp từ thư mục nguồn vào chỉ mục mới cấu hình.

```java
index.add(documentFolder);
```

### Tính năng 2 – Ký tự kết hợp

#### Tổng quan
Ký tự kết hợp (như dấu gạch ngang) thường nối hai từ. Đánh dấu chúng là *blended* sẽ yêu cầu engine giữ các token xung quanh lại với nhau trong quá trình lập chỉ mục.

#### Triển khai từng bước

**1️⃣ Set Up Paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and Configure Index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define Blended Characters**  
Ở đây chúng ta thông báo cho từ điển rằng dấu gạch ngang nên được xử lý như một ký tự kết hợp.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Ứng dụng thực tiễn

### Trường hợp sử dụng 1 – Quản lý tài liệu pháp lý
Các tài liệu pháp lý thường chứa các số vụ án như `2023-AB-456`. Bằng cách cấu hình dấu gạch dưới và dấu gạch ngang, việc tìm kiếm sẽ trả về các kết quả khớp chính xác mà không tách biệt định danh.

### Trường hợp sử dụng 2 – Kho mã nguồn
Các nhà phát triển cần tìm kiếm các đoạn mã nơi dấu gạch dưới (`my_variable`) và dấu gạch ngang (`my-function`) có ý nghĩa. Nhận dạng ký tự tùy chỉnh đảm bảo công cụ tìm kiếm tôn trọng các ký hiệu này.

### Trường hợp sử dụng 3 – Bộ dữ liệu đa ngôn ngữ
Khi làm việc với các ngôn ngữ sử dụng bảng chữ cái bổ sung, bạn có thể mở rộng tập ký tự thường để bao gồm các dải Unicode đó, đảm bảo kết quả tìm kiếm chính xác qua các ngôn ngữ.

## Các cân nhắc về hiệu năng

- **Resource Management** – Giám sát việc sử dụng heap; các chỉ mục lớn hưởng lợi từ các commit tăng dần.  
- **Garbage Collection** – Giải phóng các đối tượng `Index` khi hoàn thành để JVM thu hồi bộ nhớ.  
- **Index Optimization** – Thỉnh thoảng gọi `index.optimize()` (nếu có) để nén chỉ mục và cải thiện tốc độ truy vấn.  

## Kết luận

Bạn đã biết cách **tạo một chỉ mục tìm kiếm tùy chỉnh** phân biệt giữa ký tự thường và ký tự kết hợp bằng cách sử dụng GroupDocs.Search cho Java. Kiểm soát chi tiết này cho phép bạn xây dựng các giải pháp tìm kiếm hiệu suất cao, hỗ trợ OCR, phù hợp với môi trường pháp lý, phát triển hoặc đa ngôn ngữ.

**Next Steps**  
- Thử nghiệm các dải Unicode bổ sung cho các bảng chữ cái không phải Latin.  
- Kết hợp cấu hình ký tự với các tính năng khác của GroupDocs.Search như stemming hoặc synonyms.  
- Tích hợp chỉ mục vào một REST API để cung cấp khả năng tìm kiếm cho các ứng dụng front‑end.  

## Câu hỏi thường gặp

**Q:** *What is the purpose of `CharacterType.Letter`?*  
**A:** Nó cho phép chỉ mục xử lý các ký tự được cung cấp như là các chữ cái thường, vì vậy chúng được tách token riêng biệt trong quá trình lập chỉ mục.

**Q:** *Can I mix regular and blended characters in the same index?*  
**A:** Có—chỉ cần gọi `setRange` cho mỗi loại; từ điển sẽ xử lý cả hai cấu hình đồng thời.

**Q:** *Do I need to rebuild the index after changing the alphabet?*  
**A:** Chắc chắn. Các thay đổi trong từ điển ký tự ảnh hưởng đến việc tách token, vì vậy bạn phải lập chỉ mục lại các tài liệu để áp dụng các quy tắc mới.

**Q:** *Is there a limit to the number of custom characters I can define?*  
**A:** Thư viện hỗ trợ toàn bộ dải Unicode; hiệu năng có thể giảm nếu bạn thêm một tập hợp rất lớn, vì vậy hãy giới hạn chỉ những ký tự bạn thực sự cần.

**Q:** *How does this affect OCR accuracy?*  
**A:** Bằng cách đồng bộ bộ ký tự của chỉ mục với đầu ra của engine OCR, bạn giảm các kết quả âm tính giả và cải thiện độ liên quan chung của tìm kiếm.

---

**Last Updated:** 2026-01-11  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
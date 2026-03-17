---
date: '2026-03-17'
description: Tìm hiểu cách tạo chỉ mục với GroupDocs.Search cho Java, cấu hình ký
  tự thường và ký tự pha trộn, và tối ưu hóa tìm kiếm cho số vụ án pháp lý và hình
  ảnh OCR.
keywords:
- GroupDocs.Search Java
- Java OCR character recognition
- search library Java
title: Cách tạo chỉ mục bằng nhận dạng ký tự trong Java
type: docs
url: /vi/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# Cách Tạo Chỉ Mục với Nhận Diện Ký Tự bằng GroupDocs.Search cho Java

Trong các ứng dụng hiện đại có lượng tài liệu lớn, **cách tạo chỉ mục** đáp ứng các chi tiết tinh tế của văn bản—như dấu gạch nối, dấu gạch dưới hoặc các ký hiệu đặc thù của ngôn ngữ—là điều cần thiết để truy xuất nhanh chóng và chính xác. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cấu hình nhận diện ký tự trong **GroupDocs.Search cho Java**, bao gồm cả ký tự thường (chữ cái, chữ số, dấu gạch dưới) và ký tự pha trộn (ví dụ: dấu gạch nối). Khi kết thúc, bạn sẽ có thể tùy chỉnh một chỉ mục phù hợp với nhu cầu chính xác của kịch bản OCR hoặc tìm kiếm hình ảnh, dù bạn đang lập chỉ mục số vụ án pháp lý, kho mã nguồn, hay các tệp PDF đa ngôn ngữ.

## Câu trả lời nhanh
- **Câu hỏi “tạo chỉ mục tìm kiếm tùy chỉnh” có nghĩa là gì?** Nó có nghĩa là cấu hình một chỉ mục để xử lý các ký hiệu cụ thể như chữ cái hoặc ký tự pha trộn, thay vì bỏ qua chúng.  
- **Thư viện nào được sử dụng?** GroupDocs.Search cho Java (v25.4 tại thời điểm viết).  
- **Tôi có cần giấy phép không?** Bản dùng thử miễn phí đủ cho phát triển; giấy phép trả phí cần thiết cho môi trường sản xuất.  
- **Tôi có thể lập chỉ mục cả PDF và hình ảnh không?** Có — GroupDocs.Search hỗ trợ OCR trên hình ảnh và PDF khi được cấu hình đúng.  
- **Có bắt buộc phải dùng Maven không?** Maven là cách được khuyến nghị để quản lý phụ thuộc, nhưng bạn cũng có thể dùng Gradle hoặc các JAR thủ công.  

## Chỉ mục Tìm kiếm Tùy chỉnh là gì?
Một chỉ mục tìm kiếm tùy chỉnh cho phép bạn định nghĩa cách công cụ tìm kiếm diễn giải các ký tự. Theo mặc định, nhiều ký hiệu bị bỏ qua, điều này có thể dẫn đến việc không khớp được các trường hợp như số vụ án (`2023-AB-456`) hoặc đoạn mã (`my_variable`). Việc điều chỉnh từ điển bảng chữ cái cung cấp cho bạn toàn quyền kiểm soát những gì công cụ coi là văn bản có thể tìm kiếm.

## Tại sao cần cấu hình Ký tự Thường và Ký tự Pha trộn cho Số vụ án pháp lý?
- **Ký tự thường** (chữ cái, chữ số, dấu gạch dưới) được tách thành token riêng, cho phép tìm kiếm khớp chính xác các định danh.  
- **Ký tự pha trộn** (dấu gạch nối, dấu gạch chéo) giữ các token liên quan cùng nhau, ngăn ngừa việc tách không mong muốn các số vụ án, mã sản phẩm hoặc đường dẫn tệp.  
- Cấu hình này **tối ưu hiệu suất chỉ mục tìm kiếm** bằng cách giảm phân mảnh token và nâng cao độ liên quan cho nội dung được tạo ra bởi OCR.  

## Yêu cầu trước
- **JDK 8** trở lên đã được cài đặt.  
- **Maven** để quản lý phụ thuộc.  
- Truy cập vào thư viện **GroupDocs.Search cho Java** (tải qua Maven hoặc trang chính thức).  

### Thư viện và Phụ thuộc cần thiết
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
- **Bản dùng thử** – lý tưởng cho giai đoạn thử nghiệm ban đầu.  
- **Giấy phép tạm thời** – hữu ích cho chu kỳ phát triển dài hơn.  
- **Giấy phép sản xuất** – cần thiết cho triển khai thương mại.  

Nhận giấy phép từ cổng thông tin chính thức: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### Khởi tạo Cơ bản
Đoạn mã dưới đây hiển thị mã tối thiểu cần thiết để khởi tạo một chỉ mục rỗng. Giữ nguyên như hiện tại; chúng ta sẽ xây dựng tiếp ở phần sau.

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
Cấu hình Maven từ phần *Yêu cầu trước* là tất cả những gì bạn cần. Sau khi thêm, chạy `mvn clean install` để tải các binary.

### Yêu cầu Cài đặt Môi trường
- Đảm bảo **thư mục chỉ mục** và **thư mục tài liệu** tồn tại trên đĩa.  
- Sử dụng đường dẫn tuyệt đối hoặc cấu hình IDE để giải quyết đúng các đường dẫn tương đối.  

## Hướng dẫn Triển khai

Dưới đây chúng ta sẽ đi qua hai tính năng riêng biệt: **ký tự thường** và **ký tự pha trộn**. Mỗi tính năng tuân theo cùng một mẫu — xác định đường dẫn, tạo chỉ mục, thiết lập từ điển ký tự, và cuối cùng lập chỉ mục cho tài liệu của bạn.

### Tính năng 1 – Ký tự Thường

#### Tổng quan
Ký tự thường được xử lý như các token độc lập. Điều này lý tưởng khi bạn muốn các chữ số, chữ cái và dấu gạch dưới có thể tìm kiếm chính xác như chúng xuất hiện.

#### Triển khai Bước‑bước

**1️⃣ Set Up Paths**  
Xác định vị trí lưu trữ chỉ mục và nơi chứa các tài liệu nguồn của bạn.

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
Thêm tất cả các tệp từ thư mục nguồn vào chỉ mục vừa được cấu hình.

```java
index.add(documentFolder);
```

### Tính năng 2 – Ký tự Pha trộn

#### Tổng quan
Ký tự pha trộn (như dấu gạch nối) thường nối hai từ lại với nhau. Đánh dấu chúng là *pha trộn* sẽ khiến engine giữ các token xung quanh cùng nhau trong quá trình lập chỉ mục.

#### Triển khai Bước‑bước

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
Ở đây chúng ta thông báo cho từ điển rằng dấu gạch nối sẽ được xử lý như một ký tự pha trộn.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index Documents**  

```java
index.add(documentFolder);
```

## Ứng dụng Thực tiễn

### Trường hợp sử dụng 1 – Quản lý Tài liệu Pháp lý
Các tệp pháp lý thường chứa số vụ án như `2023-AB-456`. Bằng cách cấu hình dấu gạch dưới và dấu gạch nối, các tìm kiếm sẽ trả về kết quả khớp chính xác mà không tách rời định danh, giúp bạn **tìm kiếm số vụ án pháp lý** một cách hiệu quả.

### Trường hợp sử dụng 2 – Kho Mã Nguồn
Các nhà phát triển cần tìm kiếm các đoạn mã nơi dấu gạch dưới (`my_variable`) và dấu gạch nối (`my-function`) có ý nghĩa. Nhận diện ký tự tùy chỉnh đảm bảo công cụ tìm kiếm tôn trọng các ký hiệu này.

### Trường hợp sử dụng 3 – Bộ Dữ liệu Đa ngôn ngữ
Khi làm việc với các ngôn ngữ sử dụng bảng chữ cái bổ sung, bạn có thể **mở rộng bộ ký tự Unicode** để bao gồm các dải ký tự đó, đảm bảo kết quả tìm kiếm chính xác xuyên ngôn ngữ.

### Trường hợp sử dụng 4 – Lập chỉ mục hình ảnh PDF
Nếu bạn đang lập chỉ mục các PDF đã quét hoặc tệp hình ảnh, đầu ra OCR thường chứa các ký tự hỗn hợp. Cấu hình đúng các ký tự thường và pha trộn **tối ưu hiệu suất chỉ mục tìm kiếm** cho nội dung dựa trên hình ảnh.

## Các yếu tố về Hiệu suất

- **Quản lý tài nguyên** – Theo dõi việc sử dụng heap; các chỉ mục lớn sẽ hưởng lợi từ các commit tăng dần.  
- **Thu gom rác** – Giải phóng các đối tượng `Index` khi hoàn thành để JVM có thể thu hồi bộ nhớ.  
- **Tối ưu hoá chỉ mục** – Thỉnh thoảng gọi `index.optimize()` (nếu có) để nén chỉ mục và cải thiện tốc độ truy vấn.  

## Kết luận

Bây giờ bạn đã biết **cách tạo chỉ mục** phân biệt giữa ký tự thường và ký tự pha trộn bằng GroupDocs.Search cho Java. Kiểm soát chi tiết này cho phép bạn xây dựng các giải pháp tìm kiếm hiệu năng cao, nhận thức OCR, phù hợp với môi trường pháp lý, phát triển hoặc đa ngôn ngữ.

### Các bước tiếp theo
- Thử nghiệm các dải Unicode bổ sung cho các bảng chữ cái không phải Latin.  
- Kết hợp cấu hình ký tự với các tính năng khác của GroupDocs.Search như stemming hoặc synonyms.  
- Tích hợp chỉ mục vào một REST API để cung cấp khả năng tìm kiếm cho các ứng dụng front‑end.  

## Câu hỏi thường gặp

**Q:** *Mục đích của `CharacterType.Letter` là gì?*  
**A:** Nó cho biết chỉ mục sẽ xử lý các ký tự được cung cấp như là các chữ cái thường, vì vậy chúng sẽ được tách thành token riêng trong quá trình lập chỉ mục.

**Q:** *Tôi có thể kết hợp ký tự thường và ký tự pha trộn trong cùng một chỉ mục không?*  
**A:** Có — chỉ cần gọi `setRange` cho mỗi loại; từ điển sẽ xử lý đồng thời cả hai cấu hình.

**Q:** *Tôi có cần xây dựng lại chỉ mục sau khi thay đổi bảng chữ cái không?*  
**A:** Chắc chắn. Thay đổi từ điển ký tự ảnh hưởng đến việc tách token, vì vậy bạn phải lập chỉ mục lại các tài liệu để áp dụng các quy tắc mới.

**Q:** *Có giới hạn về số lượng ký tự tùy chỉnh tôi có thể định nghĩa không?*  
**A:** Thư viện hỗ trợ toàn bộ dải Unicode; hiệu suất có thể giảm nếu bạn thêm một tập ký tự quá lớn, vì vậy hãy giới hạn chỉ những ký tự thực sự cần thiết.

**Q:** *Điều này ảnh hưởng như thế nào đến độ chính xác của OCR?*  
**A:** Bằng cách đồng bộ bộ ký tự của chỉ mục với đầu ra của engine OCR, bạn giảm các kết quả âm tính giả và cải thiện độ liên quan chung của tìm kiếm.

---

**Last Updated:** 2026-03-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---
---
date: '2026-02-21'
description: Tìm hiểu cách triển khai bộ lọc phần mở rộng tệp Java bằng GroupDocs.Search
  cho Java, bao gồm các toán tử logic, ngày tạo/điều chỉnh và bộ lọc đường dẫn.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: Bộ lọc phần mở rộng tệp Java với GroupDocs.Search – Hướng dẫn
type: docs
url: /vi/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Làm chủ bộ lọc phần mở rộng tệp java với GroupDocs.Search

Quản lý một kho tài liệu ngày càng tăng có thể nhanh chóng trở nên quá tải, đặc biệt khi bạn chỉ cần lập chỉ mục các loại tệp nhất định. **The java file extension filter** cho phép bạn chỉ định cho GroupDocs.Search chính xác những phần mở rộng nào sẽ được bao gồm hoặc loại trừ, mang lại kiểm soát chính xác cho quy trình lập chỉ mục của bạn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách thiết lập GroupDocs.Search cho Java và chỉ cho bạn cách kết hợp bộ lọc phần mở rộng tệp với các toán tử logic AND, OR và NOT, cũng như bộ lọc phạm vi ngày và đường dẫn.

## Câu trả lời nhanh
- **What is the java file extension filter?** Một cấu hình cho phép GroupDocs.Search biết những phần mở rộng tệp nào sẽ được bao gồm hoặc loại trừ trong quá trình lập chỉ mục.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Bản dùng thử miễn phí đủ cho việc đánh giá; cần giấy phép đầy đủ cho môi trường sản xuất.  
- **Can I combine filters?** Có – bạn có thể nối chuỗi các bộ lọc extension, date, size và path với logic AND, OR, NOT.  
- **Is it Maven‑compatible?** Chắc chắn – thêm phụ thuộc GroupDocs.Search vào `pom.xml` của bạn.  

## Bộ lọc phần mở rộng tệp java là gì?
Một **java file extension filter** là một tập hợp quy tắc đánh giá phần mở rộng của mỗi tệp trước khi nó được gửi tới engine lập chỉ mục. Bằng cách chỉ định các phần mở rộng như `.txt`, `.pdf`, hoặc `.epub`, bạn có thể **include files by extension** hoặc **exclude files by extension** để giữ cho chỉ mục của bạn tập trung và kết quả tìm kiếm có liên quan.

## Tại sao nên sử dụng bộ lọc phần mở rộng tệp với GroupDocs.Search?
- **Performance:** Bỏ qua các tệp không cần thiết giảm I/O và tăng tốc độ lập chỉ mục.  
- **Storage savings:** Chỉ lưu các tài liệu liên quan trong chỉ mục, giảm sử dụng đĩa.  
- **Compliance:** Ngăn việc lập chỉ mục nhầm các tệp bí mật hoặc không được hỗ trợ.  
- **Flexibility:** Kết hợp với các tính năng **date range filter java** để nhắm mục tiêu các tệp được tạo hoặc sửa đổi trong khoảng thời gian cụ thể.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có những thứ sau:

### Thư viện và phụ thuộc cần thiết
- **GroupDocs.Search for Java**: Phiên bản 25.4 trở lên  
- **Java Development Kit (JDK)**: Đã cài đặt phiên bản tương thích  

### Cài đặt môi trường
- Môi trường phát triển tích hợp (IDE): IntelliJ IDEA, Eclipse, hoặc bất kỳ IDE nào tương thích với Maven.

### Kiến thức yêu cầu
- Lập trình Java cơ bản  
- Quen thuộc với I/O tệp trong Java  
- Hiểu về biểu thức chính quy và xử lý ngày‑giờ  

## Cài đặt GroupDocs.Search cho Java
Để bắt đầu sử dụng GroupDocs.Search, bạn cần đưa nó vào như một phụ thuộc trong dự án của mình.

### Cấu hình Maven
Thêm cấu hình repository và dependency sau vào tệp `pom.xml` của bạn:

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
Hoặc, tải phiên bản mới nhất trực tiếp từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Nhận giấy phép
1. **Free Trial** – khám phá các tính năng mà không tốn phí.  
2. **Temporary License** – nhận đầy đủ chức năng trong một thời gian giới hạn.  
3. **Purchase** – mua giấy phép vĩnh viễn cho việc sử dụng trong môi trường sản xuất.  

### Khởi tạo và cài đặt cơ bản
Sau khi thư viện đã được thêm, khởi tạo môi trường lập chỉ mục của bạn:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Hướng dẫn triển khai
Dưới đây chúng tôi sẽ đi sâu vào từng loại bộ lọc, giải thích **tại sao nó quan trọng** và cung cấp mã từng bước mà bạn có thể sao chép vào dự án của mình.

### Bộ lọc phần mở rộng tệp
Lọc các tệp theo phần mở rộng của chúng trong quá trình lập chỉ mục. Điều này rất phù hợp khi bạn chỉ muốn xử lý e‑book (`.fb2`, `.epub`) và các tệp văn bản thuần (`.txt`).

#### Tổng quan
Sử dụng `DocumentFilter.createFileExtension` để tạo danh sách trắng các phần mở rộng.

#### Các bước thực hiện
1. **Create Filter**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc NOT logic
Loại trừ các phần mở rộng cụ thể, chẳng hạn như các trang web và PDF, khi chúng không cần thiết cho kịch bản tìm kiếm của bạn.

#### Các bước thực hiện
1. **Create Exclusion Filter**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to Index Settings**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add Documents**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc AND logic
Kết hợp nhiều điều kiện—ngày tạo, phần mở rộng và kích thước tệp—để **chỉ các tệp đáp ứng mọi tiêu chí** được lập chỉ mục.

#### Tổng quan
`DocumentFilter.createAnd` hợp nhất nhiều bộ lọc thành một quy tắc duy nhất.

#### Các bước thực hiện
1. **Define Filters**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine Filters**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index Documents**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc OR logic
Bao gồm các tệp thỏa mãn **bất kỳ** điều kiện nào trong số đã chỉ định—hữu ích khi bạn muốn nắm bắt cả các tệp văn bản nhỏ và các tệp không phải văn bản lớn hơn.

#### Các bước thực hiện
1. **Define Filters**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine Filters with Logical Conditions**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR Filter**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc thời gian tạo
Nhắm mục tiêu các tệp được tạo trong một khoảng thời gian cụ thể—một kịch bản **date range filter java** điển hình.

#### Các bước thực hiện
1. **Define Date Range Filter**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index Documents**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc thời gian sửa đổi
Loại trừ các tệp đã được sửa đổi sau một ngày cắt cụ thể.

#### Các bước thực hiện
1. **Define Filter**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index Documents**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc đường dẫn tệp
Hạn chế việc lập chỉ mục các tệp nằm trong các thư mục cụ thể hoặc khớp với một mẫu—lý tưởng cho **include files by extension** trong một cấu trúc thư mục nhất định.

#### Các bước thực hiện
1. **Define File Path Filter**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize Index and Add Documents**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Những lỗi thường gặp & Mẹo
- **Never mix absolute and relative paths** trong cùng một cấu hình bộ lọc – có thể dẫn đến việc loại trừ không mong muốn.  
- **Reset the `IndexSettings`** khi chuyển đổi bộ lọc; nếu không các bộ lọc trước có thể vẫn tồn tại.  
- **Combine a length upper bound with an extension filter** cho các bộ sưu tập lớn để giảm mức sử dụng bộ nhớ.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) để xem lý do tại sao một tệp bị loại bỏ.  

## Câu hỏi thường gặp

**Q: Can I change the filter criteria after the index is created?**  
A: Có. Xây dựng lại chỉ mục với một `DocumentFilter` mới hoặc sử dụng lập chỉ mục tăng dần với các cài đặt đã cập nhật.

**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: GroupDocs.Search có thể lập chỉ mục các định dạng archive được hỗ trợ, nhưng bộ lọc phần mở rộng áp dụng cho chính archive, không phải các tệp bên trong. Sử dụng bộ lọc lồng nhau để kiểm soát sâu hơn.

**Q: How do I debug why a particular file was excluded?**  
A: Bật logging của thư viện (`LoggingOptions.setEnabled(true)`) và kiểm tra log – nó sẽ báo cáo bộ lọc nào đã từ chối mỗi tệp.

**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: Chắc chắn. Đặt một bộ lọc regex bên trong `DocumentFilter.createAnd()` cùng với bộ lọc phần mở rộng.

**Q: What performance impact does adding many filters have?**  
A: Mỗi bộ lọc thêm một mức overhead vừa phải trong quá trình lập chỉ mục, nhưng việc giảm dữ liệu được lập chỉ mục thường bù đắp chi phí. Kiểm tra với mẫu đại diện để tìm cân bằng tối ưu.

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
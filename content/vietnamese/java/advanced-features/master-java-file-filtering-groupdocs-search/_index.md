---
date: '2025-12-19'
description: Tìm hiểu cách triển khai bộ lọc phần mở rộng tệp Java bằng GroupDocs.Search
  cho Java, bao gồm các toán tử logic, ngày tạo/chỉnh sửa và bộ lọc đường dẫn.
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

Quản lý một kho tài liệu ngày càng tăng có thể nhanh chóng trở nên quá tải. Cho dù bạn cần lập chỉ mục chỉ các loại tài liệu cụ thể hoặc loại bỏ các tệp không liên quan, một **java file extension filter** cung cấp cho bạn khả năng kiểm soát chi tiết về những gì sẽ được xử lý. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách thiết lập GroupDocs.Search cho Java và chỉ cho bạn cách kết hợp bộ lọc phần mở rộng tệp với các toán tử logic AND, OR và NOT, cũng như bộ lọc phạm vi ngày và đường dẫn.

## Câu trả lời nhanh
- **What is the java file extension filter?** Cấu hình cho phép GroupDocs.Search biết những phần mở rộng tệp nào sẽ được bao gồm hoặc loại trừ khi lập chỉ mục.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Bản dùng thử miễn phí đủ cho việc đánh giá; cần có giấy phép đầy đủ cho môi trường sản xuất.  
- **Can I combine filters?** Có – bạn có thể xâu chuỗi các bộ lọc phần mở rộng, ngày, kích thước và đường dẫn với logic AND, OR, NOT.  
- **Is it Maven‑compatible?** Chắc chắn – thêm phụ thuộc GroupDocs.Search vào `pom.xml`.

## Giới thiệu

Bạn đang gặp khó khăn trong việc quản lý hiệu quả một kho tệp ngày càng tăng? Cho dù bạn cần sắp xếp tài liệu theo loại hoặc lọc bỏ các tệp không cần thiết khi lập chỉ mục, công việc này có thể trở nên khó khăn nếu không có công cụ phù hợp. **GroupDocs.Search for Java** là một thư viện tìm kiếm nâng cao giúp đơn giản hoá những thách thức này thông qua khả năng lọc tệp mạnh mẽ. Bài hướng dẫn này sẽ chỉ cho bạn cách triển khai các kỹ thuật lọc tệp .NET bằng GroupDocs.Search, tập trung vào các bộ lọc Logical AND, OR và NOT.

### Những gì bạn sẽ học
- Thiết lập GroupDocs.Search trong môi trường Java của bạn  
- Triển khai các bộ lọc khác nhau: File Extension, Logical Operators (AND, OR, NOT), Creation Time, Modification Time, File Path và Length  
- Ứng dụng thực tế của các bộ lọc này để quản lý tài liệu hiệu quả  
- Mẹo tối ưu hoá hiệu năng cho các nhiệm vụ lập chỉ mục quy mô lớn  

Sẵn sàng khai thác toàn bộ tiềm năng của việc lọc tệp trong Java? Hãy bắt đầu với các yêu cầu tiên quyết.

## Yêu cầu tiên quyết

Trước khi bắt đầu, hãy chắc chắn bạn có những thứ sau:

### Thư viện và phụ thuộc cần thiết
- **GroupDocs.Search for Java**: Phiên bản 25.4 trở lên  
- **Java Development Kit (JDK)**: Đảm bảo bạn đã cài đặt phiên bản tương thích trên hệ thống  

### Cài đặt môi trường
- Integrated Development Environment (IDE): Sử dụng IntelliJ IDEA, Eclipse, hoặc bất kỳ IDE nào bạn ưa thích hỗ trợ dự án Maven.

### Kiến thức tiên quyết
- Kiến thức cơ bản về lập trình Java  
- Quen thuộc với các thao tác I/O tệp trong Java  
- Hiểu biết về biểu thức chính quy và xử lý ngày‑giờ  

## Cài đặt GroupDocs.Search cho Java
Để bắt đầu sử dụng GroupDocs.Search, bạn cần thêm nó như một phụ thuộc trong dự án của mình. Đây là cách thực hiện:

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
1. **Free Trial**: Bắt đầu với bản dùng thử miễn phí để khám phá các tính năng của GroupDocs.Search.  
2. **Temporary License**: Yêu cầu giấy phép tạm thời để truy cập đầy đủ chức năng mà không bị giới hạn.  
3. **Purchase**: Đối với việc sử dụng lâu dài, mua gói đăng ký.  

### Khởi tạo và cài đặt cơ bản
Sau khi thư viện được thêm, khởi tạo môi trường lập chỉ mục của bạn:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Hướng dẫn triển khai
Bây giờ, chúng ta sẽ khám phá cách triển khai các tính năng lọc tệp khác nhau bằng GroupDocs.Search.

### Lọc theo phần mở rộng tệp
Lọc các tệp theo phần mở rộng của chúng trong quá trình lập chỉ mục. Tính năng này hữu ích cho việc xử lý chỉ các loại tài liệu cụ thể như FB2, EPUB và TXT.

#### Tổng quan
Lọc tài liệu dựa trên phần mở rộng tệp bằng cấu hình bộ lọc tùy chỉnh.

#### Các bước triển khai
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

### Bộ lọc Logical NOT
Loại bỏ các phần mở rộng tệp cụ thể trong quá trình lập chỉ mục, chẳng hạn HTM, HTML và PDF.

#### Các bước triển khai
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

### Bộ lọc Logical AND
Kết hợp nhiều tiêu chí để chỉ bao gồm các tệp đáp ứng tất cả các điều kiện đã chỉ định.

#### Tổng quan
Sử dụng các phép toán logical AND để lọc tệp dựa trên thời gian tạo, phần mở rộng tệp và độ dài.

#### Các bước triển khai
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

### Bộ lọc Logical OR
Bao gồm các tệp đáp ứng bất kỳ tiêu chí nào đã chỉ định bằng các phép toán logical OR.

#### Các bước triển khai
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
Lọc tệp dựa trên thời gian tạo của chúng để chỉ bao gồm những tệp nằm trong phạm vi ngày đã chỉ định.

#### Các bước triển khai
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
Loại bỏ các tệp đã được sửa đổi sau một ngày cụ thể.

#### Các bước triển khai
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

### Lọc theo đường dẫn tệp
Lọc tệp dựa trên đường dẫn tệp của chúng để chỉ bao gồm những tệp nằm trong các thư mục cụ thể.

#### Các bước triển khai
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
- **Never mix absolute and relative paths** trong cùng một cấu hình bộ lọc – điều này có thể dẫn đến việc loại trừ không mong muốn.  
- **Remember to reset the `IndexSettings`** khi bạn chuyển từ một bộ lọc sang bộ lọc khác; nếu không, các bộ lọc trước có thể vẫn còn hiệu lực.  
- **Large file collections** sẽ có lợi khi kết hợp giới hạn độ dài trên cùng với bộ lọc phần mở rộng để giảm thiểu việc sử dụng bộ nhớ.

## Câu hỏi thường gặp

**Q: Tôi có thể thay đổi tiêu chí bộ lọc sau khi đã tạo chỉ mục không?**  
A: Có. Bạn có thể xây dựng lại chỉ mục với một `DocumentFilter` mới hoặc sử dụng lập chỉ mục tăng dần với các cài đặt đã cập nhật.

**Q: Bộ lọc phần mở rộng tệp java có hoạt động trên các tệp nén (ví dụ: ZIP) không?**  
A: GroupDocs.Search có thể lập chỉ mục các định dạng lưu trữ được hỗ trợ, nhưng bộ lọc phần mở rộng chỉ áp dụng cho chính tệp lưu trữ, không phải các tệp bên trong. Sử dụng bộ lọc lồng nhau nếu cần.

**Q: Làm thế nào để tôi debug vì sao một tệp cụ thể bị loại bỏ?**  
A: Bật logging của thư viện (đặt `LoggingOptions.setEnabled(true)`) và kiểm tra log đã tạo – nó sẽ báo cáo bộ lọc nào đã từ chối mỗi tệp.

**Q: Có thể kết hợp bộ lọc phần mở rộng tệp java với bộ lọc regex tùy chỉnh không?**  
A: Chắc chắn. Bạn có thể bọc một bộ lọc regex bên trong `DocumentFilter.createAnd()` cùng với bộ lọc phần mở rộng.

**Q: Thêm nhiều bộ lọc sẽ ảnh hưởng đến hiệu năng như thế nào?**  
A: Mỗi bộ lọc bổ sung sẽ tạo ra một chút overhead trong quá trình lập chỉ mục, nhưng lợi ích của việc giảm kích thước chỉ mục thường vượt trội hơn chi phí. Hãy thử nghiệm với một bộ mẫu để tìm ra cân bằng tối ưu.

---

**Cập nhật lần cuối:** 2025-12-19  
**Được kiểm tra với:** GroupDocs.Search 25.4 for Java  
**Tác giả:** GroupDocs
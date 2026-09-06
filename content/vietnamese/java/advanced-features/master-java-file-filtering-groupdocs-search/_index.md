---
date: '2026-09-06'
description: Tìm hiểu cách lọc phần mở rộng tệp java bằng GroupDocs.Search cho Java,
  bao gồm các toán tử logic AND, OR, NOT, bộ lọc date range, và bộ lọc path.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Lọc phần mở rộng tệp java bằng GroupDocs.Search. Tìm hiểu cách kết
  hợp bộ lọc extension, date range và path với các toán tử logic trong Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Lọc phần mở rộng tệp java với GroupDocs.Search – Hướng dẫn đầy đủ
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Cách lọc phần mở rộng tệp java với GroupDocs.Search
type: docs
url: /vi/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Lọc phần mở rộng tệp java với GroupDocs.Search

Trong hướng dẫn toàn diện này, bạn sẽ học cách **filter file extensions java** khi lập chỉ mục tài liệu với GroupDocs.Search. Khi kết thúc hướng dẫn, bạn sẽ có thể chỉ bao gồm các loại tệp bạn cần, loại trừ các định dạng không mong muốn, và kết hợp các quy tắc này với bộ lọc phạm vi ngày và đường dẫn bằng các toán tử logic AND, OR và NOT. Cách tiếp cận này giúp chỉ mục của bạn gọn nhẹ, tăng tốc tìm kiếm và giúp bạn tuân thủ các chính sách xử lý dữ liệu.

## Câu trả lời nhanh
- **What is the java file extension filter?** Đây là một quy tắc cho GroupDocs.Search biết những phần mở rộng tệp nào sẽ được bao gồm hoặc loại trừ trong quá trình lập chỉ mục.  
- **Which library provides this feature?** GroupDocs.Search for Java.  
- **Do I need a license?** Bản dùng thử miễn phí đủ cho việc đánh giá; cần giấy phép đầy đủ cho môi trường sản xuất.  
- **Can I combine filters?** Có – bạn có thể nối chuỗi các bộ lọc phần mở rộng, ngày, kích thước và đường dẫn bằng logic AND, OR, NOT.  
- **Is it Maven‑compatible?** Chắc chắn – thêm phụ thuộc GroupDocs.Search vào file `pom.xml` của bạn.  

## Bộ lọc phần mở rộng tệp java là gì?
Một **java file extension filter** là một tập hợp quy tắc đánh giá phần mở rộng của mỗi tệp trước khi gửi tới engine lập chỉ mục. Bằng cách chỉ định các phần mở rộng như `.txt`, `.pdf`, hoặc `.epub`, bạn có thể **include files by extension** hoặc **exclude files by extension** để giữ cho chỉ mục của bạn tập trung và kết quả tìm kiếm có liên quan.

## Tại sao nên sử dụng lọc phần mở rộng tệp với GroupDocs.Search?
Lọc phần mở rộng tệp cải thiện hiệu suất lập chỉ mục bằng cách loại trừ các định dạng không liên quan, giảm yêu cầu lưu trữ, và giúp tuân thủ các quy tắc bằng cách ngăn nội dung không mong muốn vào chỉ mục. Nó cũng cho phép phản hồi truy vấn nhanh hơn vì công cụ tìm kiếm xử lý một tập dữ liệu nhỏ hơn, có liên quan hơn.

- **Performance:** Bỏ qua các tệp không mong muốn giảm I/O và tăng tốc lập chỉ mục lên tới 40 % trên các kho lưu trữ lớn.  
- **Storage savings:** Chỉ các tài liệu liên quan được lưu trong chỉ mục, giảm sử dụng đĩa trung bình 30 %.  
- **Compliance:** Ngăn ngừa việc lập chỉ mục nhầm các loại tệp bí mật hoặc không được hỗ trợ.  
- **Flexibility:** Kết hợp với các tính năng **date range filter java** để nhắm mục tiêu các tệp được tạo hoặc sửa đổi trong các khoảng thời gian cụ thể.  

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn có những thứ sau:

### Thư viện và phụ thuộc cần thiết
- **GroupDocs.Search for Java** – phiên bản 25.4 trở lên (hỗ trợ hơn 60 định dạng đầu vào).  
- **Java Development Kit (JDK)** – bất kỳ phiên bản tương thích nào (8 hoặc mới hơn).

### Cài đặt môi trường
- Môi trường phát triển tích hợp (IDE): IntelliJ IDEA, Eclipse, hoặc bất kỳ IDE nào tương thích với Maven.

### Kiến thức cần thiết
- Lập trình Java cơ bản.  
- Quen thuộc với I/O tệp trong Java.  
- Hiểu về biểu thức chính quy và xử lý ngày‑giờ.

## Cài đặt GroupDocs.Search cho Java
Để bắt đầu sử dụng GroupDocs.Search, bạn cần đưa nó vào như một phụ thuộc trong dự án của mình.

### Cấu hình Maven
Thêm cấu hình kho và phụ thuộc sau vào file `pom.xml` của bạn:

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
1. **Free trial** – khám phá các tính năng mà không tốn phí.  
2. **Temporary license** – nhận đầy đủ chức năng trong một thời gian giới hạn.  
3. **Purchase** – mua giấy phép vĩnh viễn cho môi trường sản xuất.

### Khởi tạo và cài đặt cơ bản
Sau khi thư viện được thêm, khởi tạo môi trường lập chỉ mục của bạn. Lớp `IndexSettings` chứa tất cả các tùy chọn cấu hình, bao gồm các bộ lọc.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Hướng dẫn triển khai
Dưới đây chúng tôi sẽ đi sâu vào từng loại bộ lọc, giải thích **tại sao nó quan trọng** và cung cấp hướng dẫn từng bước mà bạn có thể sao chép vào dự án của mình.

### Lọc phần mở rộng tệp
Lọc các tệp theo phần mở rộng của chúng trong quá trình lập chỉ mục. Điều này rất phù hợp khi bạn chỉ muốn xử lý e‑book (`.fb2`, `.epub`) và các tệp văn bản thuần (`.txt`).

#### Tổng quan
`DocumentFilter.createFileExtension` tạo danh sách trắng các phần mở rộng.

#### Các bước thực hiện
1. **Create filter** – xác định các phần mở rộng bạn muốn giữ lại.

```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – áp dụng bộ lọc khi tạo `IndexSettings`.

```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc NOT logic
Loại trừ các phần mở rộng cụ thể, chẳng hạn như trang web và PDF, khi chúng không cần thiết cho kịch bản tìm kiếm của bạn.

#### Các bước thực hiện
1. **Create exclusion filter** – chỉ định các phần mở rộng cần loại bỏ.

```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – kết hợp bộ lọc NOT với các quy tắc khác.

```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – chỉ các tệp vượt qua bộ lọc kết hợp mới được lập chỉ mục.

```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc AND logic
Kết hợp nhiều điều kiện—ngày tạo, phần mở rộng và kích thước tệp—để **chỉ các tệp đáp ứng tất cả tiêu chí** được lập chỉ mục.

#### Tổng quan
`DocumentFilter.createAnd` hợp nhất nhiều bộ lọc thành một quy tắc duy nhất.

#### Các bước thực hiện
1. **Define filters** – tạo các bộ lọc riêng cho mỗi điều kiện.

```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – sử dụng toán tử AND để yêu cầu tất cả các điều kiện.

```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – đưa bộ lọc kết hợp vào quy trình lập chỉ mục.

```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc OR logic
Bao gồm các tệp thỏa mãn **bất kỳ** điều kiện nào được chỉ định—hữu ích khi bạn muốn nắm bắt cả tệp văn bản nhỏ và tệp không phải văn bản lớn hơn.

#### Các bước thực hiện
1. **Define filters** – tạo các bộ lọc riêng cho mỗi điều kiện thay thế.

```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – sử dụng toán tử OR.

```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – gắn bộ lọc kết hợp vào cấu hình chỉ mục.

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
1. **Define date‑range filter** – chỉ định ngày bắt đầu và ngày kết thúc.

```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – chỉ các tệp có dấu thời gian tạo nằm trong khoảng sẽ được lập chỉ mục.

```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Bộ lọc thời gian sửa đổi
Loại trừ các tệp đã được sửa đổi sau một ngày cắt cụ thể.

#### Các bước thực hiện
1. **Define filter** – đặt dấu thời gian sửa đổi tối đa.

```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – các tệp mới hơn ngày cắt sẽ bị bỏ qua.

```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Lọc đường dẫn tệp
Hạn chế việc lập chỉ mục chỉ các tệp nằm trong các thư mục cụ thể hoặc khớp với một mẫu—lý tưởng cho **include files by extension** trong một cấu trúc thư mục nhất định.

#### Các bước thực hiện
1. **Define file‑path filter** – sử dụng mẫu glob hoặc regex để khớp thư mục.

```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – áp dụng bộ lọc đường dẫn cùng với các quy tắc khác.

```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Những lỗi thường gặp & mẹo
- **Never mix absolute and relative paths** trong cùng một cấu hình bộ lọc – có thể dẫn đến việc loại trừ không mong muốn.  
- **Reset the `IndexSettings`** khi chuyển bộ lọc; nếu không các bộ lọc trước có thể vẫn tồn tại.  
- **Combine a length upper bound with an extension filter** cho các bộ sưu tập lớn để giữ mức sử dụng bộ nhớ thấp.  
- LoggingOptions kiểm soát cấu hình ghi log cho GroupDocs.Search.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) để xem lý do một tệp bị từ chối.  

## Câu hỏi thường gặp

**Q: Can I change the filter criteria after the index is created?**  
A: Có. Tái tạo chỉ mục với một `DocumentFilter` mới hoặc sử dụng lập chỉ mục tăng dần với các thiết lập đã cập nhật.

**Q: Does the java file extension filter work on compressed archives (e.g., ZIP)?**  
A: GroupDocs.Search có thể lập chỉ mục các định dạng archive được hỗ trợ, nhưng bộ lọc phần mở rộng áp dụng cho chính archive, không phải các tệp bên trong. Sử dụng bộ lọc lồng nhau để kiểm soát sâu hơn.

**Q: How do I debug why a particular file was excluded?**  
A: Bật ghi log của thư viện (`LoggingOptions.setEnabled(true)`) và kiểm tra log – nó sẽ báo cáo bộ lọc nào đã từ chối mỗi tệp.

**Q: Is it possible to combine the java file extension filter with custom regex filters?**  
A: Chắc chắn. Đặt một bộ lọc regex bên trong `DocumentFilter.createAnd()` cùng với bộ lọc phần mở rộng.

**Q: What performance impact does adding many filters have?**  
A: Mỗi bộ lọc thêm một phần tải nhẹ trong quá trình lập chỉ mục, nhưng việc giảm dữ liệu được lập chỉ mục thường bù đắp chi phí. Kiểm thử với mẫu đại diện để tìm cân bằng tối ưu.

**Last Updated:** 2026-09-06  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Hướng dẫn liên quan

- [Định dạng ngày tùy chỉnh Java | Tìm kiếm theo phạm vi ngày với GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Nắm vững tìm kiếm Boolean với GroupDocs.Search cho Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Tối ưu hiệu suất tìm kiếm với kỹ thuật lập chỉ mục nâng cao trong GroupDocs.Search cho Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
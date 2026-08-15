---
date: '2026-08-15'
description: Tìm hiểu cách cải thiện độ trễ tìm kiếm bằng cách sử dụng các tính năng
  chỉ mục nâng cao của GroupDocs.Search for Java, bao gồm cancellation, async operations,
  multithreading và metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Cải thiện độ trễ tìm kiếm với GroupDocs.Search for Java bằng cách
  sử dụng cancellation, asynchronous indexing, multithreading và metadata customization.
  Tăng hiệu suất và giảm mức tiêu thụ tài nguyên.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Cải thiện độ trễ tìm kiếm với chỉ mục nâng cao trong GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Cải thiện độ trễ tìm kiếm với chỉ mục nâng cao trong GroupDocs
type: docs
url: /vi/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Cải thiện độ trễ tìm kiếm với việc lập chỉ mục nâng cao trong GroupDocs

Trong môi trường kỹ thuật số nhanh chóng ngày nay, **cải thiện độ trễ tìm kiếm** là điều thiết yếu để cung cấp kết quả ngay lập tức cho người dùng. Cho dù bạn đang xây dựng một công cụ tìm kiếm tùy chỉnh hay nâng cao hệ thống quản lý tài liệu hiện có, chiến lược lập chỉ mục phù hợp có thể giảm đáng kể độ trễ, giảm tiêu thụ tài nguyên, và **cải thiện độ trễ tìm kiếm** trên toàn bộ. Trong hướng dẫn này, chúng tôi sẽ khám phá các tính năng mạnh mẽ nhất của GroupDocs.Search cho Java—hủy bỏ, lập chỉ mục bất đồng bộ, đa luồng và tùy chỉnh siêu dữ liệu—để bạn có thể **thêm tài liệu vào chỉ mục** nhanh hơn và hiệu quả hơn.

**Bạn sẽ học gì**

- Cách hủy một thao tác lập chỉ mục sau một khoảng thời gian xác định  
- Thực hiện các thao tác lập chỉ mục bất đồng bộ và xử lý các thay đổi trạng thái  
- Cấu hình đa luồng để lập chỉ mục nhanh hơn  
- Tùy chỉnh các tùy chọn lập chỉ mục siêu dữ liệu để **tùy chỉnh siêu dữ liệu tìm kiếm**  

Hãy chắc chắn rằng bạn có mọi thứ cần thiết trước khi chúng ta đi sâu vào mã.

## Câu trả lời nhanh
- **Hủy bỏ làm gì?** Nó dừng việc lập chỉ mục sau một thời gian chờ đã định, giải phóng CPU và bộ nhớ cho các tác vụ khác.  
- **Tôi có thể lập chỉ mục tài liệu một cách bất đồng bộ không?** Có – bật nó bằng `options.setAsync(true)`.  
- **Tôi có thể sử dụng bao nhiêu luồng?** Bất kỳ số nguyên dương nào; 2‑4 luồng là điển hình cho hầu hết các máy chủ.  
- **Lập chỉ mục siêu dữ liệu có tùy chọn không?** Chắc chắn – bạn có thể bật hoặc tinh chỉnh nó cho từng trường.  
- **Tôi có cần giấy phép cho các tính năng này không?** Bản dùng thử hoạt động cho việc thử nghiệm; giấy phép đầy đủ là bắt buộc cho môi trường sản xuất.

## Yêu cầu trước

- **Thư viện GroupDocs.Search** – phiên bản 25.4 hoặc mới hơn.  
- **Môi trường phát triển Java** – JDK 8 hoặc cao hơn được khuyến nghị.  
- Kiến thức cơ bản về Java và khái niệm lập chỉ mục.

### Cài đặt GroupDocs.Search cho Java

#### Cài đặt Maven

Thêm kho lưu trữ và phụ thuộc vào tệp `pom.xml` của bạn:

Cấu hình `pom.xml` cho Maven chỉ ra các thành phần GroupDocs.Search cần tải xuống và bao gồm trong dự án của bạn.

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

#### Tải xuống trực tiếp

Hoặc, tải xuống JAR mới nhất từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**Mua giấy phép** – Bắt đầu với bản dùng thử miễn phí hoặc yêu cầu giấy phép tạm thời để mở khóa toàn bộ tính năng.

### Khởi tạo và cấu hình cơ bản

Lớp `SearchIndex` là điểm vào đại diện cho một chỉ mục có thể tìm kiếm được lưu trên đĩa hoặc trong bộ nhớ.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## “Tối ưu hiệu suất tìm kiếm” có nghĩa là gì trong ngữ cảnh này?

Tối ưu hiệu suất tìm kiếm có nghĩa là cấu hình quá trình lập chỉ mục sao cho tiêu thụ đúng mức CPU, bộ nhớ và thời gian trong khi cung cấp các kết quả liên quan nhất ngay lập tức. Bằng cách kiểm soát hủy bỏ, thực thi bất đồng bộ, đa luồng và xử lý siêu dữ liệu, bạn trực tiếp ảnh hưởng đến tốc độ mà engine có thể **thêm tài liệu vào chỉ mục** và phản hồi các truy vấn.

## Tại sao nên sử dụng các tính năng lập chỉ mục nâng cao?

Lập chỉ mục bất đồng bộ và đa luồng giữ cho ứng dụng của bạn phản hồi nhanh, trong khi hủy bỏ ngăn chặn các tiến trình chạy quá lâu. Các tùy chọn siêu dữ liệu được tinh chỉnh cho phép bạn hiển thị thông tin quan trọng nhất, điều này trực tiếp **cải thiện độ trễ tìm kiếm** cho người dùng cuối. Ngoài ra, các tính năng này giảm đỉnh CPU, giảm áp lực bộ nhớ và cho phép mở rộng mượt mà hơn khi xử lý khối lượng tài liệu lớn.

## Cách cải thiện độ trễ tìm kiếm với lập chỉ mục nâng cao?

Tải đối tượng `SearchIndex` của bạn, cấu hình `IndexingOptions` với các thiết lập hủy bỏ, bất đồng bộ và luồng, sau đó gọi `index.add(document)` — sự kết hợp này giảm thời gian lập chỉ mục tổng thể lên đến 60 % trong các khối lượng công việc điển hình và đảm bảo các công việc chạy lâu không chặn các thao tác khác. Bạn cũng có thể điều chỉnh giới hạn lập chỉ mục siêu dữ liệu và giám sát tiến độ qua các sự kiện thay đổi trạng thái để đảm bảo quy trình nằm trong ngân sách hiệu năng.

## Hướng dẫn triển khai

### Thuộc tính hủy bỏ

**Tổng quan** – Hủy lập chỉ mục sau một khoảng thời gian xác định để tránh tiêu thụ quá mức tài nguyên.

#### Bước 1: thiết lập môi trường

Tạo một đối tượng `SearchIndex` trỏ tới thư mục chỉ mục của bạn.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Bước 2: tạo tùy chọn lập chỉ mục với hủy bỏ

`IndexingOptions` cho phép bạn chỉ định cách mà engine lập chỉ mục hoạt động.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Các điểm chính**

- `setCancellation()` kích hoạt tính năng này.  
- `cancelAfter(int milliseconds)` xác định thời gian chờ (3 giây trong ví dụ này).

### Thuộc tính bất đồng bộ

**Tổng quan** – Chạy lập chỉ mục trên một luồng nền và lắng nghe các thay đổi trạng thái.

#### Bước 1: thiết lập môi trường

Tạo thể hiện của chỉ mục và chuẩn bị bộ sưu tập tài liệu.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Bước 2: đăng ký sự kiện status‑changed

Sự kiện `StatusChanged` thông báo cho bạn khi công việc lập chỉ mục chuyển đổi giữa các trạng thái.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Bước 3: cấu hình tùy chọn bất đồng bộ

Bật chế độ async để lời gọi trả về ngay lập tức và quá trình xử lý tiếp tục ở nền.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Thuộc tính luồng

**Tổng quan** – Tăng tốc độ lập chỉ mục bằng cách tận dụng nhiều lõi CPU.

#### Bước 1: thiết lập môi trường

Chuẩn bị chỉ mục và đảm bảo JVM có đủ bộ nhớ heap.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Bước 2: cấu hình đa luồng

Đặt số lượng luồng làm việc; mỗi luồng xử lý một phần tài liệu.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Thuộc tính tùy chọn lập chỉ mục siêu dữ liệu

**Tổng quan** – Tinh chỉnh siêu dữ liệu tài liệu nào sẽ được lập chỉ mục và cách lưu trữ chúng.

#### Bước 1: thiết lập môi trường

Tải một tài liệu chứa các trường siêu dữ liệu như tác giả, tiêu đề và thẻ tùy chỉnh.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Bước 2: cấu hình tùy chọn siêu dữ liệu

`MetadataIndexingOptions` cho phép bạn bật hoặc tắt các trường siêu dữ liệu riêng lẻ và xác định giới hạn kích thước.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Ứng dụng thực tiễn

1. **Hệ thống quản lý tài liệu** – Sử dụng lập chỉ mục bất đồng bộ để giữ giao diện người dùng phản hồi nhanh trong khi các lô lớn được xử lý ở nền.  
2. **Công cụ tìm kiếm nội dung** – Áp dụng hủy bỏ để ngăn các công việc chạy lâu chiếm dụng tài nguyên máy chủ trong thời gian tải cao.  
3. **Các pipeline thu thập dữ liệu quy mô lớn** – Tận dụng đa luồng để **thêm tài liệu vào chỉ mục** ở quy mô lớn, giảm thời gian xử lý đáng kể.  

## Các cân nhắc về hiệu năng

- **Quản lý luồng** – Giám sát việc sử dụng CPU; quá nhiều luồng có thể gây overhead chuyển ngữ cảnh.  
- **Dấu chân bộ nhớ** – Giới hạn siêu dữ liệu (ví dụ, `setMaxBytesToIndexField`) giữ việc sử dụng bộ nhớ dự đoán được.  
- **Thu gom rác** – Sử dụng các cờ JVM phù hợp (`-Xmx`, `-XX:+UseG1GC`) khi lập chỉ mục các tập dữ liệu khổng lồ.  

## Các vấn đề thường gặp và giải pháp

| Triệu chứng | Nguyên nhân có thể | Giải pháp |
|-------------|--------------------|-----------|
| Lập chỉ mục không bao giờ hoàn thành | Hủy bỏ được đặt quá thấp | Tăng giá trị `cancelAfter` hoặc loại bỏ hủy bỏ cho các công việc dài |
| Không có cập nhật trạng thái trong chế độ async | Trình xử lý sự kiện không được gắn đúng cách | Đảm bảo `index.getEvents().StatusChanged.add(...)` được gọi trước `index.add` |
| Lỗi hết bộ nhớ | Quá nhiều luồng hoặc giới hạn siêu dữ liệu cao | Giảm `options.setThreads` và hạ giới hạn trường siêu dữ liệu |
| Thiếu siêu dữ liệu trong kết quả | Lập chỉ mục siêu dữ liệu bị tắt | Xác minh `options.getMetadataIndexingOptions()` được cấu hình và không được đặt để bỏ qua các trường |

## Câu hỏi thường gặp

**Q: Làm thế nào tôi có thể nhận giấy phép tạm thời cho GroupDocs.Search?**  
A: Truy cập [trang giấy phép tạm thời của GroupDocs](https://purchase.groupdocs.com/temporary-license/) và làm theo hướng dẫn trên màn hình.

**Q: Tôi có thể hủy một thao tác lập chỉ mục giữa chừng không?**  
A: Có – sử dụng thuộc tính hủy bỏ với `cancelAfter()` hoặc gọi `Cancellation.cancel()` bằng chương trình.

**Q: Một số trường hợp sử dụng cho lập chỉ mục bất đồng bộ là gì?**  
A: Truy xuất tài liệu thời gian thực, xử lý batch nền, và các ứng dụng phản hồi UI nhanh đều hưởng lợi từ lập chỉ mục async.

**Q: Có an toàn khi tăng số lượng luồng trên máy chủ chia sẻ không?**  
A: Tăng dần và giám sát tải CPU; trên môi trường chia sẻ nặng, giữ số lượng luồng ở mức vừa phải (2‑4).

**Q: Lập chỉ mục siêu dữ liệu ảnh hưởng như thế nào đến độ liên quan của tìm kiếm?**  
A: Siêu dữ liệu được lập chỉ mục đúng (tác giả, ngày tạo, thẻ) có thể được gán trọng số cao hơn trong truy vấn, cải thiện độ chính xác kết quả.

## Kết luận

Bằng cách áp dụng các tính năng nâng cao này của GroupDocs.Search cho Java, bạn sẽ **cải thiện độ trễ tìm kiếm** trong nhiều kịch bản—từ việc nhập tài liệu nhanh chóng đến kiểm soát siêu dữ liệu chi tiết. Thử nghiệm với các cấu hình khác nhau, giám sát việc sử dụng tài nguyên, và tùy chỉnh các thiết lập cho khối lượng công việc cụ thể của bạn để đạt được kết quả tốt nhất.

---

**Cập nhật lần cuối:** 2026-08-15  
**Kiểm tra với:** GroupDocs.Search 25.4 cho Java  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Cải thiện hiệu suất truy vấn với GroupDocs.Search Java: Tối ưu chỉ mục & tìm kiếm](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Cách thêm tài liệu vào chỉ mục với Lập chỉ mục Siêu dữ liệu trong Java bằng GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Cách thêm nhiều bí danh và Thêm tài liệu vào chỉ mục trong GroupDocs.Search cho Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
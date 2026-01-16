---
date: '2026-01-16'
description: Tìm hiểu cách cấu hình mạng tìm kiếm GroupDocs trong Java và thêm các
  đồng nghĩa vào chỉ mục để nâng cao hiệu quả tìm kiếm.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Cấu hình GroupDocs.Search Network trong Java – Tăng tốc tìm kiếm
type: docs
url: /vi/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Cấu hình GroupDocs.Search Network trong Java – Tăng tốc tìm kiếm

Trong các ứng dụng dựa trên dữ liệu ngày nay, **configure groupdocs search network** là bước then chốt để cung cấp kết quả nhanh chóng và chính xác trên các bộ sưu tập tài liệu khổng lồ. Dù bạn đang xây dựng một cổng tìm kiếm toàn doanh nghiệp hay mở rộng một giải pháp hiện có, một GroupDocs.Search network được cấu hình tốt cho phép bạn mở rộng theo chiều ngang, thêm hỗ trợ đồng nghĩa, và giữ độ trễ thấp. Trong hướng dẫn này, bạn sẽ học cách thiết lập, triển khai và tinh chỉnh một GroupDocs.Search network bằng Java, cùng các mẹo thực tế để thêm đồng nghĩa vào chỉ mục và quản lý vòng đời node.

## Câu trả lời nhanh
- **Lợi ích chính của việc cấu hình GroupDocs.Search network là gì?** Nó cho phép lập chỉ mục và truy vấn phân tán, cải thiện hiệu năng và khả năng mở rộng.  
- **Tôi có cần giấy phép để chạy các ví dụ không?** Bản dùng thử miễn phí hoạt động cho phát triển; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Có thể thêm đồng nghĩa mà không phải xây dựng lại chỉ mục không?** Có—sử dụng từ điển đồng nghĩa tại thời gian chạy để **add synonyms to index**.  
- **Tôi có thể triển khai bao nhiêu node?** Bạn có thể triển khai bao nhiêu node tùy hạ tầng cho phép; mỗi node chạy trên một cổng riêng.  

## Cấu hình GroupDocs.Search network là gì?
Cấu hình một GroupDocs.Search network có nghĩa là xác định cấu trúc thư mục, các cổng và thiết lập node cho phép nhiều instance JVM hợp tác trong việc lập chỉ mục và tìm kiếm. Cấu hình này tạo ra một master‑node điều phối các worker (shards) và đảm bảo các truy vấn được thực thi trên toàn bộ dữ liệu.

## Tại sao nên cấu hình GroupDocs.Search network?
- **Scalability** – Phân phối tải lập chỉ mục trên nhiều máy.  
- **Reliability** – Các node có thể được thêm hoặc loại bỏ mà không gây gián đoạn.  
- **Search relevance** – Add synonyms to index để có kết quả phong phú hơn.  
- **Performance** – Thực thi truy vấn song song giảm thời gian phản hồi.  

## Yêu cầu trước
- Java Development Kit (JDK) 8 trở lên  
- Maven để xây dựng dự án  
- Kiến thức cơ bản về cú pháp Java  
- Truy cập thư viện GroupDocs.Search cho Java (tải về qua Maven hoặc trang phát hành chính thức)  

## Thiết lập GroupDocs.Search cho Java

Thêm repository và dependency vào **pom.xml** Maven của bạn:

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

Hoặc, tải phiên bản mới nhất trực tiếp từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
- **Free Trial** – Khám phá các tính năng cốt lõi mà không tốn phí.  
- **Temporary License** – Mở khóa đầy đủ khả năng cho việc thử nghiệm ngắn hạn.  
- **Commercial License** – Cần thiết cho triển khai sản xuất.  

### Khởi tạo và thiết lập cơ bản
Tạo một lớp Java đơn giản để kiểm tra thư viện tải đúng:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Hướng dẫn từng bước để cấu hình GroupDocs.Search Network

### 1. Cấu hình Search Network
Xác định thư mục tài liệu cơ bản và cổng bắt đầu cho giao tiếp node.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Nơi lưu trữ các từ điển (ví dụ: tệp đồng nghĩa).  
- **basePort** – Cổng đầu tiên; các node tiếp theo sẽ tăng dần từ giá trị này.  

### 2. Triển khai các node Search Network
Khởi động nhiều worker node chia sẻ cùng cấu hình.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Mỗi node chạy trên một cổng riêng (basePort + index) và giữ một shard của chỉ mục tổng thể.

### 3. Đăng ký sự kiện node
Giám sát sức khỏe, tiến độ lập chỉ mục và các điều kiện lỗi bằng cách gắn một event listener vào master node.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Các callback sự kiện cho phép bạn phản hồi khi node bắt đầu/dừng, hoàn thành lập chỉ mục và các lỗi bất ngờ.

### 4. Thêm đồng nghĩa vào Indexer của node  
Cải thiện độ liên quan bằng cách **add synonyms to index** tại thời gian chạy.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Mảng các thuật ngữ nên được coi là tương đương.  
- **clearBeforeAdding** – Đặt thành `true` nếu bạn muốn thay thế các mục hiện có.  

### 5. Thêm thư mục để lập chỉ mục
Cho master node biết các thư mục nào chứa tài liệu bạn muốn tìm kiếm.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Phương thức này quét thư mục một cách đệ quy và phân phối các tệp vào các shard.

### 6. Thực hiện tìm kiếm văn bản trong mạng
Thực thi truy vấn trên tất cả các node, tùy chọn buộc hành vi khớp chính xác.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Chuyển `exactMatchOnly` thành `true` khi bạn cần khớp chính xác các thuật ngữ mà không thực hiện stemming.

### 7. Đóng các node mạng
Giải phóng tài nguyên một cách nhẹ nhàng khi xử lý hoàn tất.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Tắt đúng cách ngăn ngừa rò rỉ bộ nhớ và giữ JVM ổn định.

## Ứng dụng thực tiễn
| Kịch bản | Cách mạng lưới hỗ trợ |
|----------|-----------------------|
| **Enterprise Search** | Phân phối lập chỉ mục trên các máy chủ trung tâm dữ liệu cho các kho dữ liệu quy mô petabyte. |
| **Document Management** | Add synonyms to index để người dùng có thể tìm tài liệu ngay cả khi thuật ngữ khác nhau. |
| **E‑commerce Catalog** | Triển khai các node riêng vùng để phục vụ tìm kiếm sản phẩm địa phương nhanh chóng. |
| **Content Management** | Giữ nội dung có thể tìm kiếm trong khi các biên tập viên thêm tệp mới vào các thư mục cụ thể. |

## Các vấn đề thường gặp & Giải pháp
- **Port Conflicts** – Đảm bảo cổng của mỗi node (basePort + index) không bị chiếm; điều chỉnh `basePort` nếu cần.  
- **Synonym Not Applied** – Xác nhận bạn đã gọi `indexer.setDictionary(dictionary)` sau khi thêm các thuật ngữ.  
- **Node Not Responding** – Đăng ký sự kiện; tìm các callback `NodeFailed` để chẩn đoán vấn đề mạng.  
- **Memory Leak on Close** – Luôn gọi `node.close()` cho mọi node đã triển khai.  

## Câu hỏi thường gặp

**Q: Triển khai nhiều node cải thiện hiệu năng tìm kiếm như thế nào?**  
A: Mỗi node lập chỉ mục một shard của dữ liệu, cho phép xử lý song song và giảm độ trễ truy vấn vì khối lượng công việc được chia sẻ.

**Q: Tôi có thể thêm đồng nghĩa mà không cần lập chỉ mục lại các tài liệu hiện có không?**  
A: Có, bạn có thể **add synonyms to index** tại thời gian chạy thông qua từ điển đồng nghĩa; các thay đổi có hiệu lực ngay lập tức cho các truy vấn mới.

**Q: Việc đăng ký sự kiện node có bắt buộc không?**  
A: Mặc dù không cần thiết cho hoạt động cơ bản, việc đăng ký sự kiện cung cấp khả năng quan sát sức khỏe node và giúp bạn phản hồi nhanh với các lỗi.

**Q: Các thực tiễn tốt nhất để quản lý tài nguyên node là gì?**  
A: Thường xuyên đóng các node không hoạt động, giám sát việc sử dụng bộ nhớ JVM, và tái sử dụng node vào giờ thấp điểm để duy trì tiêu thụ tài nguyên tối ưu.

**Q: GroupDocs.Search có hỗ trợ các định dạng không phải văn bản như PDF hoặc hình ảnh không?**  
A: Chắc chắn. Thư viện trích xuất văn bản từ PDF, các tệp Office, và thậm chí thực hiện OCR trên hình ảnh, cho phép chúng có thể tìm kiếm ngay từ đầu.

---

**Cập nhật lần cuối:** 2026-01-16  
**Kiểm tra với:** GroupDocs.Search 25.4 for Java  
**Tác giả:** GroupDocs
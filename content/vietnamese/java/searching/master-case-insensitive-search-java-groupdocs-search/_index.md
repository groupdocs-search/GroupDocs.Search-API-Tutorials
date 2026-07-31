---
date: '2026-07-31'
description: Tìm hiểu cách thực hiện tìm kiếm không phân biệt chữ hoa chữ thường trong
  Java bằng cách thêm tài liệu vào chỉ mục với GroupDocs.Search, sử dụng việc thay
  thế ký tự để chuẩn hoá văn bản trong quá trình lập chỉ mục.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Tìm kiếm không phân biệt chữ hoa chữ thường trong Java cho phép bạn
  thêm tài liệu vào chỉ mục và truy vấn chúng mà không lo về kiểu chữ. Hướng dẫn này
  cho thấy cách GroupDocs.Search chuẩn hoá văn bản trong quá trình lập chỉ mục để
  đạt kết quả nhanh chóng và đáng tin cậy.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Tìm kiếm Không phân biệt Chữ hoa Chữ thường Java – Lập chỉ mục Tài liệu
  với GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Thêm Tài liệu vào Chỉ mục để Tìm kiếm Không phân biệt chữ hoa chữ thường trong
  Java
type: docs
url: /vi/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# Thêm Tài liệu vào Chỉ mục để Tìm kiếm Không phân biệt chữ hoa/chữ thường trong Java

Khi bạn cần **case insensitive search java** có khả năng tìm thông tin một cách đáng tin cậy bất kể người dùng gõ như thế nào, chìa khóa là thêm tài liệu vào một chỉ mục trong khi chuẩn hoá văn bản. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách cấu hình GroupDocs.Search cho Java sao cho mỗi tài liệu bạn lập chỉ mục sẽ tự động được chuyển thành chữ thường (hoặc được biến đổi theo cách khác) trong quá trình lập chỉ mục, đảm bảo kết quả không phân biệt chữ hoa/chữ thường mà không cần logic bổ sung ở thời điểm truy vấn.

## Câu trả lời nhanh
- **What does “add documents to index” mean?** Điều này có nghĩa là tải các tệp nguồn vào một cấu trúc dữ liệu có thể tìm kiếm để chúng có thể được truy vấn sau này.  
- **Why use character replacement?** Lý do sử dụng việc thay thế ký tự? Nó chuẩn hoá mọi ký tự — thường là chuyển thành chữ thường — để các tìm kiếm tự động bỏ qua sự khác biệt về chữ hoa/chữ thường.  
- **Do I need a license?** Bạn có cần giấy phép không? Bản dùng thử miễn phí đủ cho phát triển; giấy phép đầy đủ cần thiết cho triển khai sản xuất.  
- **Which Java version is required?** Phiên bản Java nào được yêu cầu? Java 8 hoặc mới hơn; thư viện nhắm tới Java 11+ để đạt hiệu suất tối ưu.  
- **Can I switch to case‑sensitive search when needed?** Tôi có thể chuyển sang tìm kiếm phân biệt chữ hoa/chữ thường khi cần không? Có — các tùy chọn tìm kiếm cho phép bạn bật/tắt phân biệt chữ hoa/chữ thường cho từng truy vấn.  

## “add documents to index” là gì trong GroupDocs.Search?
Tải các tệp nguồn của bạn (PDF, DOCX, TXT, v.v.) vào một chỉ mục có thể tìm kiếm để công cụ có thể truy xuất chúng nhanh chóng. Thêm tài liệu vào chỉ mục sẽ phân tích mỗi tệp, trích xuất văn bản thuần và lưu trữ nó trong một cấu trúc dữ liệu được tối ưu hoá, cho phép tra cứu nhanh.

## Tại sao bật việc thay thế ký tự trong quá trình lập chỉ mục?
Việc thay thế ký tự chuyển đổi mỗi ký tự thành một tương đương đã được định sẵn — thường là chữ thường — trong khi chỉ mục được xây dựng. Điều này đảm bảo rằng các biến thể về viết hoa, dấu phụ, hoặc ký hiệu đặc thù theo vùng không ảnh hưởng đến kết quả tìm kiếm. Bằng cách chuẩn hoá văn bản tại thời điểm lập chỉ mục, công cụ có thể khớp các truy vấn với một tập token nhất quán, cung cấp hành vi không phân biệt chữ hoa/chữ thường nhanh chóng và đáng tin cậy mà không cần xử lý bổ sung cho mỗi lần tìm kiếm.

## Yêu cầu trước
- **GroupDocs.Search for Java** version 25.4 hoặc mới hơn (thư viện hỗ trợ hơn 30 định dạng tệp và có thể lập chỉ mục các tài liệu hàng trăm trang mà không cần tải toàn bộ tệp vào bộ nhớ).  
- **Java Development Kit (JDK)** 8 hoặc mới hơn đã được cài đặt.  
- Kiến thức cơ bản về **Maven** (hoặc khả năng thêm JAR thủ công).  

## Cài đặt GroupDocs.Search cho Java

### Cài đặt Maven
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Nếu bạn không muốn sử dụng Maven, tải JAR mới nhất từ trang chính thức: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nhận giấy phép
- **Free Trial** – tải giấy phép dùng thử để bắt đầu thử nghiệm.  
- **Temporary License** – yêu cầu giấy phép thử nghiệm mở rộng từ cổng thông tin GroupDocs.  
- **Full License** – mua giấy phép sản xuất khi bạn đã sẵn sàng triển khai.

### Khởi tạo cơ bản (Tạo chỉ mục)
The following snippet creates an index folder and enables character replacements:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Hướng dẫn triển khai

### Bật Thay thế Ký tự trong Cài đặt Chỉ mục
Kích hoạt tính năng này cho phép công cụ thay thế ký tự trong quá trình lập chỉ mục, đây là bước cốt lõi để đạt hành vi không phân biệt chữ hoa/chữ thường.

#### Bước 1: Cấu hình `IndexSettings`
`IndexSettings` là đối tượng cấu hình điều khiển cách chỉ mục lưu trữ và xử lý văn bản. Bằng cách đặt `useCharacterReplacements` thành **true**, bạn bật việc tự động chuyển thành chữ thường (hoặc bất kỳ ánh xạ tùy chỉnh nào bạn cung cấp).

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### Cấu hình Thay thế Ký tự
Ánh xạ mỗi ký tự tới phiên bản chữ thường tương ứng (hoặc bất kỳ ánh xạ tùy chỉnh nào bạn cần).

#### Bước 2: Định nghĩa và Thêm Các Cặp Thay thế
Từ điển thay thế chứa các cặp như `'A' → 'a'`, `'É' → 'e'`, v.v. Thêm các cặp này trước khi lập chỉ mục đảm bảo mọi token được chuẩn hoá.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### Lập chỉ mục Tài liệu
Bây giờ chỉ mục đã sẵn sàng, bạn có thể **add documents to index** từ bất kỳ thư mục nào.

#### Bước 3: Thêm Tài liệu để Lập chỉ mục
GroupDocs.Search sẽ quét thư mục mục tiêu, trích xuất văn bản từ mỗi loại tệp được hỗ trợ, áp dụng bản đồ thay thế và ghi các token vào bộ lưu trữ chỉ mục.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Thực hiện Tìm kiếm Phân biệt chữ hoa/chữ thường (Tùy chọn)

#### Bước 4: Thực hiện Tìm kiếm Phân biệt chữ hoa/chữ thường
`SearchOptions` cấu hình hành vi truy vấn, chẳng hạn như bật/tắt phân biệt chữ hoa/chữ thường, cho phép kiểm soát chi tiết cách thực hiện tìm kiếm.  
`SearchOptions.setUseCaseSensitiveSearch(true)` buộc công cụ coi ký tự hoa và thường là khác nhau trong một truy vấn cụ thể, ghi đè hành vi mặc định không phân biệt chữ hoa/chữ thường.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## Ứng dụng Thực tiễn
1. **Marketing Campaigns** – Chuẩn hoá tên sản phẩm để đội bán hàng có thể tìm tài nguyên mà không lo về chữ hoa/chữ thường.  
2. **Customer Support** – Cung cấp hộp tìm kiếm cho bộ phận hỗ trợ giúp trả về bài viết đúng bất kể người dùng gõ “login” hay “Login”.  
3. **E‑commerce Catalogs** – Đảm bảo khách hàng tìm thấy sản phẩm bất kể cách họ gõ tiêu đề, nâng cao tỷ lệ chuyển đổi.  

## Các yếu tố về hiệu suất
- **Organize Source Files** – Một cấu trúc thư mục gọn gàng giảm thời gian quét trong bước **add documents to index**.  
- **Monitor Memory** – Lập chỉ mục khối lượng lớn có thể tiêu tốn RAM đáng kể; xử lý tệp theo lô 500 – 1 000 mục giúp kiểm soát việc sử dụng heap.  
- **Asynchronous Indexing** – Khi được hỗ trợ, chạy việc lập chỉ mục trên luồng nền để giao diện người dùng phản hồi tốt và tránh chặn các thao tác của người dùng.  

## Các vấn đề thường gặp & Khắc phục

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| No results returned for a known term | Character replacements not enabled | Verify `settings.setUseCharacterReplacements(true)` and that the replacement map contains the needed characters. |
| Out‑of‑memory error during indexing | Indexing too many large files at once | Index in smaller batches or increase JVM heap (`-Xmx4g`). |
| Search returns case‑sensitive results unexpectedly | `SearchOptions.setUseCaseSensitiveSearch(true)` was set | Remove or set to `false` for default case‑insensitive behavior. |
| Index load time exceeds expectations | Inefficient folder layout or SSD not used | Re‑organize files, prune unused documents, and store the index on a fast SSD. |
| Special characters are ignored | Replacement map missing Unicode entries | Add mappings for characters like “é”, “ß”, “ø” to their desired equivalents. |

## Câu hỏi thường gặp

**Q: Làm thế nào để xử lý các ký tự đặc biệt (ví dụ: “é”, “ß”) trong quá trình lập chỉ mục?**  
A: Bao gồm các ký tự đó trong bản đồ thay thế của bạn, ánh xạ chúng tới các tương đương ASCII hoặc giữ nguyên tùy theo yêu cầu tìm kiếm.

**Q: Tôi có thể giới hạn việc thay thế ký tự cho một ngôn ngữ cụ thể không?**  
A: Có. Xây dựng một mảng thay thế tùy chỉnh chỉ chứa các ký tự cho ngôn ngữ mục tiêu trước khi thêm vào từ điển.

**Q: Tôi nên làm gì nếu việc tải chỉ mục mất nhiều thời gian?**  
A: Tối ưu hóa cấu trúc thư mục, loại bỏ các tệp không cần thiết và lưu chỉ mục trên SSD tốc độ cao. Lập chỉ mục tăng dần cũng giảm tải thời gian tải.

**Q: Có thể hoàn tác việc thay thế ký tự sau khi lập chỉ mục không?**  
A: Không. Các thay thế đã được nhúng vào dữ liệu đã lập chỉ mục; bạn phải xây dựng lại chỉ mục với cài đặt mới để thay đổi chúng.

**Q: Tôi có thể tìm tài liệu API chi tiết hơn ở đâu?**  
A: Tài liệu chính thức và tham chiếu API cung cấp chi tiết đầy đủ (xem phần Tài nguyên bên dưới).

## Tài nguyên
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Cập nhật lần cuối:** 2026-07-31  
**Kiểm tra với:** GroupDocs.Search 25.4 for Java  
**Tác giả:** GroupDocs  

## Hướng dẫn liên quan

- [Thay thế ký tự trong GroupDocs.Search Java: Hướng dẫn toàn diện để cải thiện tìm kiếm văn bản và lập chỉ mục](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [Thêm tài liệu vào chỉ mục: tìm kiếm Java phân biệt chữ hoa/chữ thường với GroupDocs](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [Cách Thêm Tài liệu vào Chỉ mục với GroupDocs.Search cho Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
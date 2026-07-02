---
date: '2026-07-02'
description: Tìm hiểu cách nhận giấy phép tạm thời cho GroupDocs.Search, thêm thư
  mục vào chỉ mục và thêm thuộc tính tài liệu tùy chỉnh khi quản lý các nút mạng tìm
  kiếm Java.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Nhận Giấy phép Tạm thời GroupDocs – Master Search Nodes (Java)
type: docs
url: /vi/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Nhận Giấy Phép Tạm Thời GroupDocs – Các Node Tìm Kiếm Chính (Java)

Trong hướng dẫn toàn diện này, bạn sẽ **nhận giấy phép tạm thời cho GroupDocs.Search**, cấu hình một mạng tìm kiếm đa‑node, và học cách **thêm thư mục vào chỉ mục** và **thêm thuộc tính tài liệu tùy chỉnh** bằng Java. Cho dù bạn đang xây dựng hệ thống quản lý tài liệu doanh nghiệp hoặc danh mục sản phẩm có thể tìm kiếm, việc nắm vững các bước này cho phép bạn đánh giá nền tảng mà không có hạn chế và mở rộng khả năng tìm kiếm nhanh chóng.

## Câu trả lời nhanh
- **Bước đầu tiên để bắt đầu sử dụng GroupDocs.Search là gì?** Nhận giấy phép tạm thời từ cổng GroupDocs.  
- **Kho Maven nào chứa thư viện?** `https://releases.groupdocs.com/search/java/`.  
- **Làm thế nào để thêm thư mục vào chỉ mục?** Gọi hàm `addDirectoriesToIndex` trên node chính.  
- **Tôi có thể thêm thuộc tính tài liệu tùy chỉnh không?** Có—gọi `addAttribute` với khóa tài liệu và tên thuộc tính.  
- **Làm thế nào để tắt các node một cách sạch sẽ?** Gọi `closeNodes` để giải phóng tài nguyên.

## Giấy phép tạm thời là gì và tại sao tôi cần nó?
Giấy phép tạm thời cho phép bạn đánh giá GroupDocs.Search mà không có bất kỳ giới hạn nào. Nó hoàn hảo cho việc phát triển, thử nghiệm, hoặc các dự án chứng minh khái niệm trước khi cam kết mua bản đầy đủ. Giấy phép cung cấp quyền truy cập đầy đủ tính năng trong một thời gian giới hạn, cho phép bạn đo hiệu năng, kiểm tra các điểm tích hợp, và đảm bảo giải pháp đáp ứng yêu cầu của bạn mà không cần cam kết tài chính.

## Yêu cầu trước
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

### Thư viện và phụ thuộc cần thiết
Để làm việc với GroupDocs.Search cho Java, bao gồm các phụ thuộc Maven cần thiết:
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
Bạn cũng có thể tải phiên bản mới nhất trực tiếp từ [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Cài đặt môi trường
- Đảm bảo bạn đã cài đặt JDK tương thích (Java 8 hoặc mới hơn).  
- Thiết lập IDE của bạn để hỗ trợ các dự án Maven.

### Yêu cầu kiến thức
Kiến thức cơ bản về lập trình Java và quen thuộc với quản lý dự án Maven sẽ rất hữu ích. Nếu bạn mới với những khái niệm này, hãy cân nhắc khám phá các tài nguyên giới thiệu để bắt đầu.

## Cách nhận giấy phép tạm thời
Giấy phép tạm thời được nhận bằng cách truy cập cổng GroupDocs, điền vào mẫu yêu cầu ngắn, và đặt tệp `.lic` nhận được vào thư mục `resources` của dự án. Sau đó khởi tạo giấy phép bằng vài dòng mã (xem đoạn mã dưới đây). Đối với mẫu yêu cầu, sử dụng trang chính thức: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Cài đặt GroupDocs.Search cho Java

### Thông tin cài đặt
Để bắt đầu sử dụng GroupDocs.Search cho Java trong dự án của bạn, hãy làm theo các bước Maven ở trên hoặc tải phiên bản mới nhất trực tiếp từ trang phát hành chính thức.

#### Các bước nhận giấy phép
1. **Free Trial** – Dùng thử miễn phí – Khám phá các tính năng mà không có bất kỳ cam kết nào.  
2. **Temporary License** – Giấy phép tạm thời – Nhận khóa ngắn hạn để thử nghiệm (xem phần ở trên).  
3. **Purchase** – Mua – Đối với sử dụng trong môi trường sản xuất, mua giấy phép đầy đủ từ **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Khởi tạo và cấu hình cơ bản
Khởi tạo dự án của bạn với GroupDocs.Search như sau:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Bước khởi tạo này rất quan trọng để đảm bảo tất cả các thành phần hoạt động liền mạch trong mạng tìm kiếm của bạn.

## Hướng dẫn triển khai
Bây giờ, chúng ta sẽ chia quy trình thành các phần dễ quản lý, mỗi phần tập trung vào một tính năng cụ thể của việc triển khai và quản lý các node trong mạng tìm kiếm.

### Tính năng 1: Cấu hình thiết lập
**Tổng quan:** Thiết lập cấu hình cho mạng tìm kiếm của bạn là bước đầu tiên trong việc triển khai các node. Cài đặt này bao gồm việc chỉ định các đường dẫn và cổng quan trọng cho việc triển khai node.

#### Các bước thực hiện:
##### Bước 1: Xác định Đường dẫn cơ sở và Cổng
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Bước 2: Cấu hình Mạng Tìm Kiếm
Hàm `configureSearchNetwork` chuẩn bị đối tượng cấu hình cần thiết cho việc triển khai các node.  
`Configuration` là một lớp chứa tất cả các thiết lập như thư mục chỉ mục, cổng mạng, và vai trò node.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Tham số:** Đường dẫn cơ sở và cổng được sử dụng để xác định tài nguyên và thiết lập kênh giao tiếp.  
- **Giá trị trả về:** Một đối tượng `Configuration` đã được cấu hình phù hợp với nhu cầu triển khai của bạn.

### Tính năng 2: Triển khai Mạng Tìm Kiếm
**Tổng quan:** Triển khai các node là cần thiết để mở rộng khả năng tìm kiếm của bạn trên các môi trường hoặc phân đoạn dữ liệu khác nhau.

#### Các bước thực hiện:
##### Bước 1: Triển khai Node
Hàm `deploySearchNetwork` khởi tạo và trả về một mảng các node trong mạng tìm kiếm.  
`SearchNetworkNodes` đại diện cho mỗi instance node tham gia vào cụm tìm kiếm phân tán.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Tham số:** Đường dẫn cơ sở, cổng và cấu hình được sử dụng để xác định môi trường triển khai.  
- **Giá trị trả về:** Một mảng chứa các `SearchNetworkNodes` đã được khởi tạo.

### Tính năng 3: Đăng ký sự kiện mạng
**Tổng quan:** Giám sát hoạt động của mạng tìm kiếm là quan trọng để duy trì hiệu năng và độ tin cậy tối ưu.

#### Các bước thực hiện:
##### Bước 1: Đăng ký sự kiện Node Master
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Mục đích:** Bước này đảm bảo bạn nhận được thông báo về các sự kiện hoặc thay đổi quan trọng trong mạng tìm kiếm của bạn.

### Tính năng 4: Đánh chỉ mục tài liệu
**Tổng quan:** Thêm các thư mục chứa tài liệu để được đánh chỉ mục cho phép truy xuất dữ liệu hiệu quả trên toàn mạng của bạn.

#### Cách thêm thư mục vào chỉ mục
`addDirectoriesToIndex` là một phương thức trợ giúp đăng ký các đường dẫn thư mục để đánh chỉ mục trên node master.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Mục đích:** Tạo điều kiện cho việc truy cập nhanh và khả năng tìm kiếm tất cả tài liệu trong các thư mục được chỉ định.

### Tính năng 5: Thêm thuộc tính vào tài liệu
**Tổng quan:** Các thuộc tính tùy chỉnh nâng cao siêu dữ liệu tài liệu, làm cho việc tìm kiếm linh hoạt và thông tin hơn.

#### Cách thêm thuộc tính tài liệu tùy chỉnh
`addAttribute` thêm một thuộc tính siêu dữ liệu tùy chỉnh vào tài liệu được chỉ định trong chỉ mục.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Tham số:** Xác định node, khóa tài liệu và thuộc tính cần thêm.  
- **Mục đích:** Mở rộng chức năng tìm kiếm bằng cách làm phong phú tài liệu với siêu dữ liệu bổ sung.

### Tính năng 6: Truy xuất tài liệu đã đánh chỉ mục
**Tổng quan:** Truy xuất và liệt kê tài liệu đã đánh chỉ mục một cách hiệu quả để đảm bảo độ chính xác và đầy đủ của dữ liệu.

#### Các bước thực hiện:
##### Bước 1: Lấy tài liệu đã đánh chỉ mục
```java
getIndexedDocuments(nodes[0]);
```  
- **Mục đích:** Xác nhận việc đánh chỉ mục thành công của tất cả tài liệu cần thiết trong mạng tìm kiếm của bạn.

### Tính năng 7: Đóng các node mạng
**Tổng quan:** Đóng các node đúng cách là quan trọng cho việc quản lý tài nguyên và ngăn ngừa rò rỉ bộ nhớ.

#### Các bước thực hiện:
##### Bước 1: Đóng tất cả các node
`closeNodes` tắt tất cả các node tìm kiếm đang hoạt động và giải phóng tài nguyên đã cấp phát.  
```java
closeNodes(nodes);
```  
- **Mục đích:** Giải phóng tài nguyên chiếm dụng bởi mỗi node, đảm bảo quá trình tắt máy sạch sẽ.

## Tại sao nên sử dụng giấy phép tạm thời cho GroupDocs.Search?
Giấy phép tạm thời cung cấp **quyền truy cập đầy đủ tính năng trong 30 ngày** và hỗ trợ lên tới **50.000 tài liệu đã đánh chỉ mục** mà không bị giảm hiệu năng. Điều này cho phép bạn đo tốc độ đánh chỉ mục, độ trễ truy vấn, và khả năng mở rộng trên dữ liệu thực tế trước khi mua giấy phép sản xuất. Nó cũng loại bỏ các dấu watermark đánh giá, mang lại cho bạn một hình ảnh thực tế về khả năng của sản phẩm cuối cùng.

## Các trường hợp sử dụng phổ biến
1. **Enterprise Document Management** – "Quản lý tài liệu doanh nghiệp" – Đánh chỉ mục hàng triệu tệp nội bộ trên các phòng ban, cho phép tìm kiếm toàn văn tức thời.  
2. **E‑commerce Platforms** – "Nền tảng thương mại điện tử" – Xây dựng danh mục sản phẩm có thể tìm kiếm bao phủ nhiều kho và nguồn dữ liệu bên thứ ba.  
3. **Legal Firms** – "Công ty luật" – Tổ chức hồ sơ vụ án, hợp đồng và bằng chứng với siêu dữ liệu tùy chỉnh để truy xuất nhanh.

Các khả năng tích hợp với hệ thống khác bao gồm nền tảng CRM, hệ thống quản lý nội dung (CMS), và công cụ phân tích dữ liệu, tận dụng các tính năng đánh chỉ mục và tìm kiếm mạnh mẽ do GroupDocs.Search cho Java cung cấp.

## Các lưu ý về hiệu năng
Để tối ưu hiệu năng khi sử dụng GroupDocs.Search cho Java:
- **Tối ưu cấu hình** – Điều chỉnh các thiết lập cấu hình để phù hợp với môi trường triển khai cụ thể của bạn.  
- **Giám sát việc sử dụng tài nguyên** – Thường xuyên kiểm tra CPU, bộ nhớ và I/O để ngăn ngừa tắc nghẽn hoặc rò rỉ bộ nhớ.  
- **Tuân thủ các thực tiễn tốt nhất** – Tuân thủ các hướng dẫn quản lý bộ nhớ của Java, đảm bảo sử dụng hiệu quả tài nguyên hệ thống.

## Câu hỏi thường gặp

**Q: Giấy phép tạm thời có thời hạn bao lâu?**  
A: Giấy phép tạm thời thường có hiệu lực trong 30 ngày, cung cấp cho bạn đủ thời gian để đánh giá sản phẩm.

**Q: Tôi có thể chuyển từ giấy phép tạm thời sang giấy phép đầy đủ mà không cài lại không?**  
A: Có—thay thế tệp giấy phép tạm thời bằng tệp giấy phép đầy đủ và khởi động lại ứng dụng của bạn.

**Q: Tôi có cần đánh chỉ mục lại tài liệu sau khi áp dụng giấy phép mới không?**  
A: Không, chỉ mục vẫn giữ nguyên; giấy phép chỉ điều chỉnh quyền sử dụng.

**Q: Điều gì sẽ xảy ra nếu tôi quên đóng các node?**  
A: Các tài nguyên chưa được giải phóng có thể gây rò rỉ bộ nhớ; luôn gọi `closeNodes` khi tắt hệ thống.

**Q: Có thể thêm hơn một thuộc tính tùy chỉnh cho mỗi tài liệu không?**  
A: Chắc chắn—gọi `addAttribute` nhiều lần với các tên thuộc tính khác nhau.

---

**Cập nhật lần cuối:** 2026-07-02  
**Được kiểm tra với:** GroupDocs.Search for Java 25.4  
**Tác giả:** GroupDocs

## Hướng dẫn liên quan

- [Triển khai Node Mạng Tìm Kiếm trong .NET sử dụng GroupDocs để Đánh chỉ mục và Truy xuất Tài liệu Hiệu quả](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Cách triển khai Mạng Tìm Kiếm với GroupDocs.Search trong .NET cho Hệ thống Quản lý Tài liệu](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Cấu hình Mạng Aspose.Search & Thêm Thuộc tính Tài liệu với GroupDocs.Redaction cho .NET: Hướng dẫn Toàn diện](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
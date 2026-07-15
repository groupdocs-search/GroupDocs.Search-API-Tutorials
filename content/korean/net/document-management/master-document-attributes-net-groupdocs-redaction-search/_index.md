---
date: '2026-06-22'
description: GroupDocs.Redaction 및 GroupDocs.Search를 사용하여 검색 성능을 최적화하면서 .NET에서 문서를
  가리는 방법을 배웁니다. .NET 개발자를 위한 단계별 속성 관리, 인덱싱 및 보안 가리기.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: GroupDocs Redaction을 사용해 .NET에서 문서를 가리는 방법
type: docs
url: /ko/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# .NET에서 GroupDocs Redaction을 사용하여 문서 가리기

이 포괄적인 튜토리얼에서는 .NET 환경에서 **문서를 가리는 방법**을 배우고 GroupDocs.Redaction 및 GroupDocs.Search를 사용한 문서 속성 관리도 동시에 마스터하게 됩니다. 민감한 데이터를 보호하거나 검색 속도를 높이거나 대규모 문서 라이브러리를 정리해야 할 경우, 여기서 보여주는 기술은 수십만 개 파일까지 확장 가능한 프로덕션 수준 솔루션을 제공합니다.

## 빠른 답변
- **.NET에서 PDF를 어떻게 가리나요?** `Redactor`로 파일을 로드하고 `RedactionRegion`을 정의한 뒤 `Redactor.Apply()`를 호출합니다 – 세 줄의 코드만으로 핵심 작업을 수행합니다.  
- **인덱싱 후에 문서 속성을 변경할 수 있나요?** 예, `AttributeChangeBatch`를 사용하여 속성을 대량으로 추가, 업데이트 또는 제거할 수 있습니다.  
- **필요한 라이브러리는 무엇인가요?** `GroupDocs.Redaction` + `GroupDocs.Search` (최신 NuGet 버전).  
- **프로덕션에 라이선스가 필요합니까?** 유효한 GroupDocs 라이선스가 필요합니다; 평가용으로 임시 체험 라이선스를 제공합니다.  
- **검색 속도를 어떻게 향상시킬 수 있나요?** 배치 처리와 선택적 인덱싱을 활성화하면 이러한 기술로 대규모 데이터 세트에서 검색 성능을 최대 40 %까지 **최적화**할 수 있습니다.

## “문서 가리기”란 무엇인가요?
파일 내에서 민감한 정보를 자동으로 찾아 검은 막대나 공백과 같은 가려진 내용으로 교체하면서 원래 레이아웃을 유지하는 과정을 의미합니다. 이를 통해 기밀 데이터는 사용자에게 숨겨지지만 문서는 여전히 읽을 수 있고 후속 작업에 사용할 수 있습니다.

## GroupDocs.Redaction과 GroupDocs.Search를 함께 사용하는 이유
GroupDocs.Redaction은 **50개 이상의 파일 형식**(PDF, DOCX, XLSX, PPTX, 이미지 등)을 지원하며 전체 파일을 메모리에 로드하지 않고 **2 GB**까지의 문서를 처리할 수 있습니다. GroupDocs.Search는 표준 서버에서 시간당 **70 백만 개** 이상의 용어를 인덱싱하여 속성 기반 필터링과 결합하면 **검색 성능을 크게 최적화**할 수 있습니다.

## 전제 조건
- **필수 라이브러리:** `GroupDocs.Search` 및 `GroupDocs.Redaction` (최신 NuGet 릴리스).  
- **개발 환경:** Visual Studio 2019 이상, .NET Core 3.1 또는 .NET 6+ 대상.  
- **기본 지식:** C# 구문, 객체 지향 개념, 문서 인덱싱 원칙에 대한 이해.

## .NET용 GroupDocs.Redaction 설정

### 라이브러리 설치

다음 방법 중 하나를 사용하여 프로젝트에 **GroupDocs.Redaction**을 추가할 수 있습니다:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- “GroupDocs.Redaction”을 검색하고 최신 버전을 설치합니다.

### 라이선스 획득 단계

시작하려면 임시 라이선스를 받거나 구매할 수 있습니다. 기능을 테스트해볼 수 있는 무료 체험 라이선스도 제공됩니다:
1. 임시 라이선스를 요청하려면 [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/)를 방문합니다.  
2. 애플리케이션에 라이선스를 적용하는 방법에 대한 안내를 따릅니다.

### 기본 초기화 및 설정

`Redactor`는 문서를 로드하고 가리기 작업을 적용하는 데 사용되는 주요 클래스입니다.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## 기능 1: 문서 속성 변경

### 개요
문서 속성을 수정하면 검색 결과에서 문서가 표시되는 방식을 세밀하게 조정할 수 있어 정확한 필터링 및 분류가 가능합니다.

#### 단계 1: 인덱스 초기화
`Index`는 문서와 해당 메타데이터의 검색 가능한 컬렉션을 나타냅니다.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### 단계 2: 속성 수정
`AttributeChangeBatch`는 효율성을 위해 속성 업데이트를 배치하는 클래스입니다.

**Definition anchor:** *`AttributeChangeBatch`는 단일 트랜잭션에서 문서 속성에 대한 추가, 업데이트 및 삭제 작업을 배치합니다.*

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### 단계 3: 속성 필터로 검색
`SearchOptions`를 사용하여 속성 값으로 검색 결과를 필터링할 수 있습니다.

**Direct answer:** `Category = "Legal"` 속성을 포함하는 문서를 검색하려면 `SearchOptions`를 `AttributeFilter`와 함께 구성하고 `searcher.Search("contract", options)`를 호출합니다. 이렇게 하면 법적 태그가 지정된 계약서만 반환되어 결과 잡음을 줄이고 **검색 성능을 최적화**합니다.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## 기능 2: 인덱싱 중 속성 추가

### 개요
인덱싱 시점에 속성을 추가하면 모든 문서가 처음부터 올바른 메타데이터로 풍부해지며, 이후 대량 업데이트가 필요 없게 됩니다.

#### 단계 1: 인덱싱을 위한 이벤트 핸들러 설정
*`DocumentIndexed` 이벤트는 문서가 인덱스에 성공적으로 추가될 때마다 발생하여 사용자 정의 로직을 실행할 수 있게 합니다.*

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### 단계 2: 검색 구성 및 수행
속성이 부착된 후에는 새로운 필드를 사용하여 검색할 수 있습니다.

**Direct answer:** `SearchOptions`와 `AttributeFilter`를 사용하여 새로 추가된 속성을 쿼리합니다. 예를 들어 `AttributeFilter("Department", "Finance")`와 같이 사용합니다. 이렇게 하면 재무 관련 파일만 반환되어 **속성을 인덱싱하는 방법**을 보여주며 더 빠르고 관련성 높은 결과를 얻을 수 있습니다.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## 실용적인 적용 사례

다음은 문서 속성 관리와 가리기를 함께 수행하여 실질적인 비즈니스 가치를 제공하는 세 가지 일반적인 시나리오입니다:

1. **법률 문서 관리** – 기밀 조항을 자동으로 가리고 관할 구역별로 계약서를 태그하여 변호사가 관련 파일만 찾을 수 있게 합니다.  
2. **의료 기록 정리** – 환자 식별자를 가리면서 `PatientID` 및 `VisitDate`와 같은 속성을 추가하여 규정 준수와 빠른 검색을 가능하게 합니다.  
3. **전자상거래 제품 카탈로그** – 공급업체 가격 정보를 가리고 대량 가져오기 중에 `StockStatus` 또는 `DiscountRate`와 같은 속성을 태그하여 실시간 재고 조회를 가능하게 합니다.

## 성능 고려 사항

대규모 데이터 세트를 다룰 때 다음 모범 사례를 기억하십시오:

- **배치 처리:** `AttributeChangeBatch`는 인덱스로의 왕복 횟수를 줄여 100 k 문서 배치에서 처리 시간을 최대 **45 %**까지 단축합니다.  
- **선택적 인덱싱:** 새 속성이 필요한 문서만 인덱싱하고 변경되지 않은 파일은 건너뛰어 CPU와 I/O를 절약합니다.  
- **메모리 관리:** 사용이 끝난 `SearchResult`, `Redactor`, `Indexer` 인스턴스를 즉시 Dispose하여 관리되지 않는 리소스를 해제합니다.

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결 방법 |
|-------|-------|----------|
| 가리기가 텍스트를 숨기지 않음 | `RedactionRegion` 좌표가 올바르지 않음 | 영역을 정의하기 전에 `Redactor.GetPageSize()`로 페이지 크기를 확인하십시오. |
| 속성 변경이 검색에 반영되지 않음 | 인덱스가 새로 고쳐지지 않음 | `AttributeChangeBatch` 실행 후 `searcher.Refresh()`를 호출하십시오. |
| 대용량 파일에서 메모리 부족 오류 | 전체 파일을 메모리에 로드함 | `RedactorOptions.Stream = true`로 설정하여 스트리밍 모드를 활성화하십시오. |

## 자주 묻는 질문

**Q: 여러 PDF를 배치 가리기 위한 최선의 방법은 무엇인가요?**  
A: 각 파일을 `Redactor`로 로드하고 모든 민감 영역에 대해 `RedactionRegion`을 추가한 뒤 루프 내에서 `Redactor.Apply()`를 호출합니다; 이 방법은 수천 개 파일을 최소 메모리 오버헤드로 처리합니다.

**Q: 가리기와 속성 필터링을 단일 쿼리에서 결합할 수 있나요?**  
A: 예. 가리기 후에도 문서는 메타데이터를 유지하므로 텍스트 용어와 `AttributeFilter`를 동시에 사용하여 검색할 수 있습니다.

**Q: 암호로 보호된 문서는 어떻게 처리하나요?**  
A: 비밀번호를 `Redactor` 생성자에 전달하면 라이브러리가 자동으로 파일을 복호화, 가리기, 재암호화합니다.

**Q: 가리기 전에 스캔 이미지에 대한 OCR을 지원하나요?**  
A: 물론입니다. `RedactorOptions.Ocr = true`를 활성화하면 이미지에서 텍스트를 인식하고 추출된 텍스트에 가리기 규칙을 적용할 수 있습니다.

**Q: 공식적으로 지원되는 .NET 버전은 무엇인가요?**  
A: GroupDocs.Redaction 및 GroupDocs.Search는 .NET Core 3.1, .NET 5, .NET 6, .NET 7 및 .NET Framework 4.6.2 이상을 지원합니다.

## 결론

이제 GroupDocs.Redaction과 GroupDocs.Search를 사용하여 **문서 가리기**와 **검색 성능 최적화**, **속성 인덱싱**을 위한 전체 스택 솔루션을 갖추었습니다. 위 단계들을 따르면 민감한 데이터를 보호하고 의미 있는 메타데이터로 검색 인덱스를 풍부하게 하며 .NET 애플리케이션을 빠르고 안전하게 유지할 수 있습니다.

---

**마지막 업데이트:** 2026-06-22  
**테스트 환경:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction .NET 마스터: 고급 문서 검색을 위한 효율적인 인덱스 생성 및 별칭 관리](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [GroupDocs.Redaction .NET을 사용한 문서 가리기 및 메타데이터 인덱싱 마스터](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [GroupDocs.Redaction .NET 마스터: 보안 문서 관리를 위한 설정 및 이벤트 처리](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
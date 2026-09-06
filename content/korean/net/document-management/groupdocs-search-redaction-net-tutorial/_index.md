---
date: '2026-06-12'
description: GroupDocs.Search와 GroupDocs.Redaction을 사용하여 .NET에서 검색 인덱스를 만들고 PDF에 레드액션을
  적용하는 방법을 배웁니다. 설정, 배포, 인덱싱 및 고급 검색에 대해 설명합니다.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: GroupDocs Search 및 Redaction을 사용하여 .NET에서 검색 인덱스 만들기 – 포괄적인 가이드
type: docs
url: /ko/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# 검색 인덱스 .NET 만들기 – GroupDocs Search 및 Redaction 종합 가이드

오늘날 디지털 환경에서 **검색 인덱스 .NET** 솔루션을 구축하여 정보를 빠르게 찾고 민감한 데이터를 보호하는 것은 모든 조직의 최우선 과제입니다. 이 튜토리얼에서는 확장 가능한 GroupDocs.Search 네트워크 구성, 노드 배포, 문서 인덱싱, 그리고 GroupDocs.Redaction을 사용하여 **PDF에 레드랙션 적용**을 .NET 환경 내에서 수행하는 방법을 단계별로 안내합니다.

## 빠른 답변
- **검색 인덱스 .NET을 만들기 위한 첫 번째 단계는 무엇인가요?** 기본 경로와 포트를 정의한 다음 네트워크 노드를 배포합니다.  
- **GroupDocs로 PDF에 레드랙션을 적용하려면 어떻게 하나요?** `Redactor` 인스턴스를 초기화하고 PDF를 로드한 뒤 원하는 패턴으로 `Redact`를 호출합니다.  
- **검색 네트워크를 여러 머신에서 실행할 수 있나요?** 예—노드를 별도 서버에 배포하고 마스터 노드가 인덱싱 및 쿼리를 조정하도록 합니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 프로덕션에는 유효한 GroupDocs 라이선스가 필요하며, 평가용으로 임시 체험 라이선스를 사용할 수 있습니다.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.7.2+, .NET Core 3.1+, 및 .NET 5/6/7이 완전히 지원됩니다.

## “검색 인덱스 .NET 만들기”란 무엇인가요?
*Creating a search index .NET*은 .NET 라이브러리를 사용하여 문서 메타데이터와 내용을 검색 가능한 저장소로 구축하는 것을 의미합니다. 이 라이브러리는 텍스트를 추출하고, 용어를 토큰화하며, 최적화된 인덱스 구조에 저장합니다. 이를 통해 분산된 노드 간에 즉시 쿼리 응답이 가능해지며, 다양한 파일 형식을 지원하고 기업 애플리케이션에서 확장 가능하고 고성능의 문서 검색을 제공합니다.

## GroupDocs Search와 Redaction을 함께 사용하는 이유는?
GroupDocs.Search는 **50개 이상의 파일 형식**(DOCX, PDF, PPTX, HTML 등)을 지원하며 전체 파일을 메모리에 로드하지 않고도 수백 페이지 문서를 인덱싱할 수 있습니다. 여기에 **PDF에 레드랙션을 적용**할 수 있는 GroupDocs.Redaction을 결합하면 페이지당 200 ms 미만으로 처리되는 안전하고 고성능의 문서 관리 파이프라인을 얻을 수 있습니다.

## 전제 조건

### 필수 라이브러리 및 종속성
이 튜토리얼을 따라하려면 다음 패키지를 설치하십시오:
- **GroupDocs.Search** for .NET
- **GroupDocs.Redaction** for .NET  

필요한 라이브러리를 설치하는 방법은 다음 중 하나를 사용할 수 있습니다:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Search for "GroupDocs.Search" and "GroupDocs.Redaction" and install the latest version.

### 환경 설정 요구 사항
- .NET Framework 4.7.2 이상 (또는 .NET Core 3.1+)
- Visual Studio IDE (Community, Professional, 또는 Enterprise)

### 지식 전제 조건
- 기본 C# 프로그래밍
- 객체 지향 개념
- 네트워크 구성 및 문서 관리 시스템에 대한 친숙함

## .NET용 GroupDocs.Redaction 설정

### 설치 정보
애플리케이션에 레드랙션 기능을 통합하려면 먼저 GroupDocs.Redaction 라이브러리를 추가하십시오:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Search for "GroupDocs.Redaction" and install it.

### 라이선스 획득
무료 체험 또는 임시 라이선스로 시작하려면 다음 단계를 따르세요:
- Visit the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) to request a temporary license.  
- For purchase options, navigate to their [pricing page](https://groupdocs.com/pricing).

라이선스 파일을 확보하면 애플리케이션 설정에 적용하십시오:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### 기본 초기화
기본 작업을 위해 GroupDocs.Redaction을 초기화하려면 다음 코드 스니펫을 사용하십시오:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## 구현 가이드

### 구성 설정

#### 개요
이 기능은 기본 경로와 포트 번호를 사용하여 검색 네트워크를 구성하며, 문서 관리 시스템의 기반을 형성합니다.

#### 정의 앵커
`SearchNetworkDeployment`는 네트워크 전반에 검색 노드 배치를 조정하는 클래스입니다.

#### 단계 1: 기본 경로와 포트 정의  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### 단계 2: 네트워크 구성
지정된 경로와 포트로 검색 네트워크를 설정하려면 `Configure` 메서드를 사용하십시오:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### 네트워크 노드 배포

#### 개요
구성된 검색 네트워크 내에 노드를 배포하여 분산 문서 검색을 수행합니다.

#### 정의 앵커
`SearchNetworkNode`는 마스터 노드와 통신하는 개별 검색 가능한 노드를 나타냅니다.

#### 단계 1: 배포 초기화  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### 마스터 노드 이벤트 구독

#### 개요
마스터 노드의 이벤트를 구독하여 네트워크 작업을 효과적으로 모니터링하고 관리합니다.

#### 정의 앵커
`SearchNetworkNodeEvents`는 인덱싱, 쿼리 실행 및 오류 처리를 위한 콜백을 제공합니다.

#### 단계 1: 마스터 노드 식별
첫 번째 노드를 마스터로 선택합니다:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### 단계 2: 이벤트 구독
다음과 같이 이벤트를 구독합니다:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### 문서 인덱싱

#### 개요
효율적인 검색 작업을 위해 문서를 인덱싱합니다. 이 단계는 네트워크가 필요한 데이터를 신속하게 검색할 수 있도록 보장하는 데 중요합니다.

#### 정의 앵커
`SearchIndex`는 각 인덱스된 파일에 대한 검색 가능한 토큰과 메타데이터를 저장하는 핵심 객체입니다.

#### 단계 1: 인덱스에 디렉터리 추가
문서가 들어 있는 디렉터리를 지정합니다:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### 검색 기능 – 기본 사용법

#### 개요
네트워크 내 노드들을 대상으로 기본 검색 작업을 수행합니다.

#### 직접 답변
마스터 노드에서 `SearchNetwork.Query("your term")`를 호출하면 일치하는 문서를 즉시 검색할 수 있습니다. 이 메서드는 파일 경로와 관련성 점수를 포함하는 `SearchResult` 객체 컬렉션을 반환합니다.

`SearchNetwork.Query`는 전체 네트워크에 걸쳐 검색 쿼리를 실행하고 일치하는 결과를 반환하는 메서드입니다.

#### 단계 1: 검색 매개변수 정의  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### 고급 검색 기능

#### 개요
맞춤형 매개변수를 사용하여 보다 정밀한 결과를 얻기 위해 고급 검색 기술을 활용합니다.

#### 직접 답변
`SearchOptions` 객체를 생성하고 `UseFuzzySearch`, `Highlight`, `PageSize` 속성을 설정한 뒤 `SearchNetwork.QueryAdvanced`에 전달하는 메서드를 구현합니다. 이렇게 하면 퍼지 매칭이 활성화된 페이지네이션 및 하이라이트된 결과를 얻을 수 있습니다.

`SearchNetwork.QueryAdvanced`는 퍼지 매칭 및 페이지네이션과 같은 고급 옵션을 사용해 쿼리를 실행하는 메서드입니다.

#### 단계 1: 고급 검색 메서드 구현  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### PDF 파일에 레드랙션 적용

#### 개요
PDF 내용을 저장하거나 공유하기 전에 레드랙션하여 민감한 정보를 보호합니다.

#### 직접 답변
`Redactor` 인스턴스를 생성하고 대상 PDF를 로드한 뒤 `RedactionPattern`(예: SSN 정규식)을 정의하고 `redactor.Apply(pattern)`을 호출한 후 레드랙션된 문서를 저장합니다. 이 과정은 개인 데이터를 영구적으로 제거함을 보장합니다.

#### 정의 앵커
`Redactor`는 문서를 처리하고 레드랙션 규칙을 적용하는 GroupDocs.Redaction의 주요 클래스입니다.

#### 예시 워크플로 (새 코드 블록 없음)  
1. 라이선스로 `Redactor`를 초기화합니다.  
2. `redactor.Load("sample.pdf")`를 사용해 PDF를 로드합니다.  
3. `RedactionPattern`은 레드랙션할 텍스트 또는 패턴을 지정하는 규칙을 나타냅니다. `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`와 같은 패턴을 정의합니다.  
4. `redactor.Apply(pattern)`를 실행합니다.  
5. `redactor.Save("sample_redacted.pdf")`로 출력물을 저장합니다.

### 실용적인 적용 사례

#### 실제 사용 사례
1. **법률 문서 관리** – 계약서를 효율적으로 검색하고 클라이언트 식별자를 자동으로 레드랙션합니다.  
2. **헬스케어 기록** – 환자 메모를 찾으면서 HIPAA 준수 PHI 레드랙션을 보장합니다.  
3. **기업 컴플라이언스** – 내부 커뮤니케이션에서 금지된 용어를 스캔하고 보관 전에 레드랙션합니다.

## 결론 
이 가이드는 **검색 인덱스 .NET 만들기** 솔루션을 확장 가능하고 빠르게 인덱싱하며 레드랙션을 통해 데이터를 보호하는 포괄적인 경로를 제공합니다. 노드 구성, 문서 인덱싱, 고급 검색 기능 활용 및 레드랙션 적용을 통해 개발자는 문서 관리 워크플로를 크게 개선하면서 엄격한 보안 표준을 유지할 수 있습니다.

## 자주 묻는 질문

**Q: .NET에서 GroupDocs를 사용해 분산 검색 네트워크를 설정하려면 어떻게 해야 하나요?**  
A: 기본 경로와 포트를 정의한 뒤 `SearchNetworkDeployment.Deploy()`를 호출하여 머신 전반에 마스터 및 워커 노드를 시작합니다.

**Q: GroupDocs에서 여러 매개변수를 사용한 고급 검색을 수행할 수 있나요?**  
A: 예—`SearchOptions`를 사용하여 퍼지 매칭, 와일드카드 지원 및 결과 하이라이트를 하나의 쿼리로 결합합니다.

**Q: 마스터 노드에서 네트워크 활동을 모니터링할 수 있나요?**  
A: 물론입니다—`IndexingCompleted`, `QueryExecuted`와 같은 `SearchNetworkNodeEvents`에 구독하여 실시간 인사이트를 얻을 수 있습니다.

**Q: GroupDocs를 사용해 PDF 파일에 레드랙션을 적용하려면 어떻게 해야 하나요?**  
A: `Redactor`를 초기화하고 PDF를 로드한 뒤 `RedactionPattern` 객체(정규식 또는 문자열)를 정의하고 `Apply`를 호출한 후 정제된 문서를 저장합니다.

**Q: 네트워크 환경에서 검색 성능을 향상시키는 가장 쉬운 방법은 무엇인가요?**  
A: 쿼리 전에 문서 세트를 완전히 인덱싱하고, 노드를 분산시켜 병렬 처리를 활용하며, 캐싱 및 페이지네이션을 위해 `SearchOptions`를 조정합니다.

---

**마지막 업데이트:** 2026-06-12  
**테스트 환경:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Search와 함께하는 마스터 .NET 문서 인덱싱 – 종합 가이드](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [GroupDocs.Redaction .NET와 함께하는 마스터 문서 인덱싱 및 고급 검색 쿼리](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [.NET에서 GroupDocs Search와 Redaction 마스터하기 – 고급 문서 관리](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
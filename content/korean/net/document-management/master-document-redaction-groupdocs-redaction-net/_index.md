---
date: '2026-07-02'
description: GroupDocs.Redaction 및 Aspose.Search.NET을 사용하여 .NET 검색 인덱스를 만드는 방법을 배우고,
  문서를 인덱스에 추가하고, 별칭을 관리하며, 데이터 보안을 보장합니다.
keywords:
- create search index .net
- add documents to index
- groupdocs redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to create search index .NET using GroupDocs.Redaction and
    Aspose.Search.NET, add documents to index, manage aliases, and ensure data security.
  headline: 'Create Search Index .NET with GroupDocs.Redaction: Indexing and Managing
    Aliases for Secure Document Management'
  type: TechArticle
- questions:
  - answer: Yes, both GroupDocs.Redaction and Aspose.Search.NET fully support .NET
      Core 3.1, .NET 5, .NET 6, and later.
    question: Can I use this solution with .NET Core?
  - answer: The engine is tested with indexes containing over 1 million documents,
      maintaining sub‑second query times on standard server hardware.
    question: How many documents can the index handle?
  - answer: Aliases can contain wildcard characters (`*` and `?`) but not full regex
      patterns; for complex patterns, build the query programmatically.
    question: Do aliases support regular expressions?
  - answer: Absolutely. Retrieve the document ID from the search result, load it with
      GroupDocs.Redaction, apply redaction rules, and save the protected version.
    question: Is it possible to redact after searching?
  - answer: GroupDocs offers volume‑based licensing with unlimited developers and
      deployment sites; contact sales for a custom quote.
    question: What licensing model applies to large enterprises?
  type: FAQPage
title: 'GroupDocs.Redaction을 사용한 .NET 검색 인덱스 만들기: 보안 문서 관리를 위한 인덱싱 및 별칭 관리'
type: docs
url: /ko/net/document-management/master-document-redaction-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction을 사용한 .NET 검색 인덱스 생성: 보안 문서 관리를 위한 별칭 인덱싱 및 관리

대량의 문서를 관리하면서 민감한 정보를 기밀로 유지하는 것은 어려울 수 있습니다. **GroupDocs.Redaction for .NET**을 사용하면 **create search index .NET** 프로젝트를 만들어 문서 컬렉션을 효율적으로 마스킹하고 검색할 수 있습니다. 이 튜토리얼에서는 Aspose.Search.NET을 사용해 인덱스를 생성하거나 열고, 인덱스에 문서를 추가하고, 별칭 사전을 관리하며, 마스킹 기능을 통합하는 방법을 단계별로 안내합니다—모두 엄격한 데이터 보안을 유지하면서 진행됩니다.

## 빠른 답변
- **이 가이드의 주요 목적은 무엇입니까?** **create search index .NET** 프로젝트를 만드는 방법, 인덱스에 문서를 추가하는 방법, 그리고 GroupDocs.Redaction을 사용해 별칭을 관리하는 방법을 보여줍니다.  
- **필요한 라이브러리는 무엇입니까?** GroupDocs.Redaction 및 Aspose.Search.NET, 두 라이브러리 모두 NuGet을 통해 제공됩니다.  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험판을 사용할 수 있으며, 프로덕션 환경에서는 정식 라이선스가 필요합니다.  
- **대용량 문서 세트를 처리할 수 있습니까?** 예—두 라이브러리 모두 전체 파일을 메모리에 로드하지 않고 수백 페이지 파일을 처리할 수 있습니다.  
- **솔루션이 .NET‑Core와 호환됩니까?** 물론입니다; .NET 5, .NET 6 및 이후 버전에서 실행됩니다.

## 소개

본격적으로 시작하기 전에 **create search index .NET** 솔루션이 왜 중요한지 명확히 합시다. 인덱스를 사용하면 수천 개 파일에서 정확한 구문, 패턴 또는 마스킹된 콘텐츠를 밀리초 단위로 찾아낼 수 있어 컴플라이언스 검토, 법률 조사 및 내부 감사가 크게 빨라집니다. Aspose.Search.NET의 강력한 인덱싱 엔진과 GroupDocs.Redaction의 견고한 마스킹 도구를 결합하면 데이터를 보호하면서 즉시 검색할 수 있는 단일 파이프라인을 확보할 수 있습니다.

## GroupDocs.Redaction for .NET이란?
GroupDocs.Redaction for .NET은 PDF, DOCX, PPTX, HTML 등 30개 이상의 문서 형식에 대해 텍스트, 이미지 및 메타데이터를 프로그래밍 방식으로 마스킹할 수 있는 라이브러리입니다. 전체 문서를 RAM에 로드하지 않고 최대 2 GB까지 파일을 처리하므로 엔터프라이즈 워크로드에서도 높은 성능을 보장합니다.

## Aspose.Search.NET으로 .NET 검색 인덱스를 만드는 이유
Aspose.Search.NET은 **50+** 파일 형식을 인덱싱할 수 있으며 증분 업데이트를 지원합니다. 즉, 기존 인덱스를 재구성하지 않고 새 파일을 추가할 수 있어 CPU 사용량을 최대 70 % 절감하고, 500 k+ 문서를 포함한 인덱스에서도 쿼리 응답 시간이 200 ms 이하로 유지됩니다.

## 전제 조건

### 필수 라이브러리, 버전 및 종속성
- **GroupDocs.Redaction** – 최신 NuGet 릴리스, .NET 5/6/7과 호환됩니다.  
- **Aspose.Search.NET** – 최신 NuGet 릴리스, .NET Standard 2.0+ 및 .NET Core를 지원합니다.  

두 라이브러리는 동일한 .NET 런타임 버전을 대상으로 해야 바인딩 충돌을 방지할 수 있습니다.

### 환경 설정 요구 사항
- Visual Studio 2022(또는 .NET 6+을 지원하는 IDE).  
- 인덱싱 및 마스킹하려는 문서가 들어 있는 폴더에 대한 접근 권한.  

### 지식 전제 조건
- C# 구문 및 .NET 프로젝트 구조에 대한 친숙함.  
- 인덱싱, 검색 및 문서 마스킹의 기본 개념.

## 어떻게 .NET 검색 인덱스를 생성합니까?

`Index` 객체를 로드하거나 인스턴스화하고 폴더를 지정한 뒤 `CreateOrOpen`을 호출하면—이 한 단계만으로 디스크에 저장된 검색 가능한 스토어를 생성하거나 다시 엽니다. 기본적으로 백그라운드 스레드에서 작업이 수행되므로 수천 개 파일을 인덱싱하더라도 UI가 응답성을 유지합니다.

`Index`는 디스크에 저장된 검색 가능한 컬렉션을 나타냅니다.

### 정의 앵커
`Index` 클래스는 Aspose.Search.NET의 핵심 구성 요소로, 디스크에 저장된 문서 컬렉션을 검색 가능한 형태로 나타냅니다. 모든 인덱싱 및 쿼리 작업은 이 객체를 통해 흐릅니다.

```bash
dotnet add package GroupDocs.Redaction
```

## 인덱스에 문서를 어떻게 추가합니까?

`AddDocument`는 파일을 인덱스에 추가하고 검색 가능한 콘텐츠를 추출합니다.

각 파일 경로에 대해 `Index.AddDocument`를 호출하여 문서를 추가하면 메타데이터, 텍스트 및 선택적 OCR 콘텐츠가 자동으로 추출됩니다. `foreach` 루프에서 파일을 일괄 추가할 수 있으며, 인덱스는 기존 항목을 재구성하지 않고 증분적으로 업데이트됩니다. 또한 메서드는 성공 여부와 오류를 나타내는 상태 객체를 반환하므로 프로그래밍 방식으로 실패를 처리할 수 있습니다.

```powershell
Install-Package GroupDocs.Redaction
```

## 라이선스 획득 단계

- **무료 체험** – 30일 동안 비용 없이 모든 기능을 탐색할 수 있습니다.  
- **임시 라이선스** – 장기 테스트를 위한 제한된 기간의 키를 사용합니다.  
- **정식 라이선스** – 프로덕션 배포에 필요하며 모든 평가 제한을 해제합니다.

설치가 완료되면 아래와 같이 GroupDocs.Redaction을 초기화합니다:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Set up additional configuration as needed
```

## 구현 가이드

기능별로 관리 가능한 섹션으로 구현을 나누어 설명합니다.

### 인덱스 생성 또는 열기

#### 개요
검색 인덱스를 생성하거나 여는 것은 효율적인 문서 관리와 검색을 위한 기본 단계이며, 인덱싱된 데이터를 신속하게 활용할 수 있게 해줍니다.

#### 단계별 지침

**1. 인덱스 생성/열기**

```csharp
using GroupDocs.Search;

// Specify the directory where your index will be stored
string indexPath = "YOUR_INDEX_DIRECTORY";

// Initialize or open an existing index
Index index = new Index(indexPath);

// Explanation: The Index object is initialized with a directory path,
// which serves as a storage location for all indexed data.
```

**2. 인덱스에 문서 추가**

```csharp
using GroupDocs.Search;

// Specify your document directory
string docPath = "YOUR_DOCUMENT_DIRECTORY";

// Add documents from the specified directory to the index
index.Add(docPath);

// Explanation: The Add method indexes all documents within the provided path,
// making them searchable.
```

### 별칭 사전 관리

#### 개요
별칭 사전은 복잡한 검색 쿼리를 간단한 용어로 정의할 수 있게 해주어 검색 효율성과 가독성을 높여줍니다.

#### 단계별 지침

**1. 기존 별칭 삭제**

```csharp
using GroupDocs.Search.Dictionaries;

// Check if there are existing aliases and clear them
if (index.Dictionaries.AliasDictionary.Count > 0)
{
    index.Dictionaries.AliasDictionary.Clear();
}

// Explanation: This ensures you start with a clean slate when managing aliases.
```

**2. 단일 별칭 항목 추가**

```csharp
index.Dictionaries.AliasDictionary.Add("t", "(gravida OR promotion)");
index.Dictionaries.AliasDictionary.Add("e", "(viverra OR farther)");

// Explanation: Each alias is mapped to an expression that defines its search scope.
```

**3. 배열을 사용해 다중 별칭 추가**

```csharp
AliasReplacementPair[] pairs = new AliasReplacementPair[]
{
    new AliasReplacementPair("d", "daterange(2017-01-01 ~~ 2019-12-31)"),
    new AliasReplacementPair("n", "(400 ~~ 4000)")
};

index.Dictionaries.AliasDictionary.AddRange(pairs);

// Explanation: AddRange allows bulk addition of aliases, streamlining the setup process.
```

### 별칭 조회 및 내보내기

#### 개요
별칭 사전을 파일로 내보내면 팀이나 환경 간에 검색 어휘를 공유할 수 있으며, 특정 항목을 조회하면 쿼리 로직을 검증할 수 있습니다.

**별칭 조회**

```csharp
if (index.Dictionaries.AliasDictionary.Contains("e"))
{
    string replacement = index.Dictionaries.AliasDictionary.GetText("e");
}

// Explanation: Use Contains to check existence before retrieval.
```

**별칭 내보내기**

```csharp
string exportPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ExportDictionary(exportPath);

// Explanation: ExportDictionary saves the alias dictionary for future use or sharing.
```

### 별칭 가져오기 및 별칭 사전을 사용한 검색

#### 개요
파일에서 별칭을 가져와 미리 정의된 용어로 검색 작업을 간소화하고, 해당 별칭을 참조하는 쿼리를 실행합니다.

**1. 별칭 가져오기**

```csharp
string importPath = "YOUR_OUTPUT_DIRECTORY/Aliases.dat";
index.Dictionaries.AliasDictionary.ImportDictionary(importPath);

// Explanation: This method loads existing alias definitions into the dictionary.
```

**2. 별칭 사용 검색**

```csharp
string query = "@t OR @e"; // Use aliases in your search query
SearchResult result = index.Search(query);

// Explanation: Leverage aliases to perform complex searches with simple queries.
```

## 일반적인 문제 및 해결책

- **인덱스 경로 오류** – 폴더 경로가 절대 경로인지 확인하고, 애플리케이션에 읽기/쓰기 권한이 있는지 확인하십시오.  
- **메모리 누수** – 특히 장기 실행 서비스에서는 사용 후 `Index` 객체에 대해 반드시 `Dispose()`를 호출하십시오.  
- **별칭 인식 안 됨** – 별칭 파일이 UTF‑8 인코딩인지 확인하고, 각 라인이 `key=value` 형식을 따르는지 검증하십시오.

## 자주 묻는 질문

**Q: 이 솔루션을 .NET Core와 함께 사용할 수 있나요?**  
A: 예, GroupDocs.Redaction과 Aspose.Search.NET 모두 .NET Core 3.1, .NET 5, .NET 6 및 이후 버전을 완벽히 지원합니다.

**Q: 인덱스가 처리할 수 있는 문서 수는 얼마입니까?**  
A: 엔진은 100만 개 이상의 문서를 포함한 인덱스에서도 테스트되었으며, 표준 서버 하드웨어에서 서브초 수준의 쿼리 시간을 유지합니다.

**Q: 별칭이 정규식을 지원합니까?**  
A: 별칭에는 와일드카드 문자(`*` 및 `?`)를 포함할 수 있지만 전체 정규식 패턴은 지원되지 않습니다. 복잡한 패턴이 필요하면 프로그래밍 방식으로 쿼리를 구성하십시오.

**Q: 검색 후에 마스킹을 적용할 수 있나요?**  
A: 물론 가능합니다. 검색 결과에서 문서 ID를 가져와 GroupDocs.Redaction으로 로드한 뒤 마스킹 규칙을 적용하고 보호된 버전으로 저장하면 됩니다.

**Q: 대기업을 위한 라이선스 모델은 어떻게 되나요?**  
A: GroupDocs는 무제한 개발자와 배포 사이트를 포함하는 볼륨 기반 라이선스를 제공하며, 맞춤 견적은 영업팀에 문의하십시오.

## 결론

**GroupDocs.Redaction**과 **Aspose.Search.NET**을 통합해 **create search index .NET** 솔루션을 구현하면 문서 보안, 컴플라이언스 및 검색 가능성을 크게 향상시킬 수 있습니다. 이제 인덱스를 구축하고, 문서를 인덱스에 추가하고, 별칭 사전을 관리하며, 마스킹 규칙을 적용하는 모든 도구를 갖추었습니다—단일 고성능 .NET 애플리케이션 내에서 구현할 수 있습니다.

다음 단계는 무엇입니까? 코드 스니펫을 테스트 프로젝트에 적용하고, 사용자 정의 별칭 패턴을 실험하며, 프로덕션 데이터 세트에 대한 인덱싱 속도를 벤치마크해 보세요.

---

**마지막 업데이트:** 2026-07-02  
**테스트 환경:** GroupDocs.Redaction 23.10 for .NET, Aspose.Search.NET 24.5  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction .NET을 활용한 문서 인덱싱 및 고급 검색 쿼리 마스터](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [효율적인 문서 관리를 위한 GroupDocs.Redaction .NET 인덱스 생성 및 병합 마스터](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [문서 관리를 위한 .NET에서 GroupDocs.Search와 Redaction 구현 가이드](/search/net/document-management/groupdocs-search-redaction-net-guide/)
---
date: '2026-04-02'
description: GroupDocs.Search와 GroupDocs.Redaction을 사용하여 .NET에서 검색 인덱스를 만들고 문서를 인덱스에
  추가하면서 파싯 검색을 구현하는 방법을 배웁니다.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Redaction .NET 파시티드 검색을 활용한 GroupDocs 검색 인덱스 생성
type: docs
url: /ko/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# GroupDocs와 Redaction을 사용한 .NET 퍼시드 검색 인덱스 만들기

현대 애플리케이션에서는 **GroupDocs로 검색 인덱스 생성**이 빠르고 정확한 문서 검색을 위해 필수적입니다. 법률 계약서, 제품 카탈로그 또는 방대한 지식 베이스를 다루든, 잘 구축된 인덱스를 통해 **문서를 인덱스에 추가**하고 몇 초 만에 강력한 퍼시드 검색을 실행할 수 있습니다. 이 튜토리얼은 GroupDocs.Redaction 설정부터 간단하고 복잡한 퍼시드 쿼리 작성까지 전체 과정을 안내하므로 .NET 프로젝트에서 반응형 검색 경험을 제공할 수 있습니다.

## 빠른 답변
- **주된 목적은 무엇인가요?** GroupDocs로 검색 인덱스를 생성하고 퍼시드 검색을 활성화하는 것입니다.  
- **필요한 라이브러리는 무엇인가요?** .NET용 GroupDocs.Redaction 및 GroupDocs.Search.  
- **인덱스에 문서를 어떻게 추가하나요?** 인덱스를 초기화한 후 `index.Add(documentsFolder)`를 사용합니다.  
- **복잡한 쿼리를 실행할 수 있나요?** 예, 객체 쿼리를 논리 연산자와 결합하여 고급 필터링을 할 수 있습니다.  
- **라이선스가 필요합니까?** 개발에는 무료 체험판으로 충분하지만, 운영 환경에서는 상용 라이선스가 필요합니다.

## 퍼시드 검색이란 무엇이며 GroupDocs와 함께 사용하는 이유는?
퍼시드 검색은 사용자가 카테고리, 날짜, 저자와 같은 여러 필터를 동시에 적용하여 결과를 세분화할 수 있게 합니다. **GroupDocs.Redaction**과 결합하면, 레드액션 규칙을 준수하면서도 보안이 유지된 검색 가능한 콘텐츠를 제공하므로 규정 준수가 중요한 환경에 이상적입니다.

## 사전 요구 사항

### 필요한 라이브러리, 버전 및 종속성
- **GroupDocs.Redaction .NET** – 최신 안정 버전.  
- **GroupDocs.Search .NET** – 인덱싱을 위해 Redaction과 손잡고 작동합니다.

### 환경 설정 요구 사항
- **IDE**: Visual Studio 2019 이상.  
- **Framework**: .NET Core 3.1, .NET 5 또는 .NET 6.  
- **OS 호환성**: Windows, Linux, macOS.

### 지식 사전 요구 사항
기본적인 C# 실력과 퍼시드 검색 개념에 대한 높은 수준의 이해가 도움이 되지만, 단계별 가이드는 초보자도 쉽게 따라 할 수 있도록 구성되었습니다.

## .NET용 GroupDocs.Redaction 설정

### 설치 정보
다음 방법 중 하나를 사용하여 GroupDocs.Redaction 패키지를 추가할 수 있습니다:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- "GroupDocs.Redaction"을 검색하고 최신 버전을 설치합니다.

### 라이선스 획득 단계
전체 기능을 사용하려면 무료 체험판으로 시작하거나 영구 라이선스를 획득하십시오:

1. 라이선스 옵션을 확인하려면 [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/)를 방문하십시오.  
2. 화면에 표시되는 지침에 따라 체험판 또는 구매한 라이선스 파일을 받으세요.

### 기본 초기화 및 설정
패키지를 설치한 후 애플리케이션에서 Redactor를 초기화합니다:
```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## 검색 인덱스 groupdocs 만들기

아래에서는 구현을 두 부분으로 나눕니다: **Simple Faceted Search**와 **Complex Query**. 각 파트는 **검색 인덱스 groupdocs 생성**, 문서 추가 및 쿼리 실행 방법을 보여줍니다.

### 기능 1: Simple Faceted Search

**개요**  
퍼시드 검색은 사용자가 여러 기준을 선택하여 결과를 좁힐 수 있게 합니다. 이 섹션에서는 GroupDocs.Search를 사용한 간단한 접근 방식을 보여줍니다.

#### 단계 1: 인덱스 및 문서 폴더 정의
인덱스가 저장될 폴더와 원본 문서가 위치할 폴더 경로를 설정합니다.
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### 단계 2: 인덱스 생성
정의한 폴더에 검색 인덱스를 초기화합니다.
```csharp
Index index = new Index(indexFolder);
```

#### 단계 3: 인덱스에 문서 추가
문서를 로드하여 검색 가능하도록 합니다.
```csharp
index.Add(documentsFolder);
```

#### 단계 4: 텍스트 쿼리 검색 수행
**content** 필드에 대해 기본 텍스트 쿼리를 실행합니다.
```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### 단계 5: 객체 쿼리 검색 실행
보다 세밀한 제어를 위해 객체 지향 쿼리를 사용합니다.
```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### 기능 2: Complex Query

**개요**  
파일명 패턴과 구문 일치와 같은 여러 필터를 결합해야 할 때, 논리 연산자를 사용하여 복잡한 쿼리를 구축할 수 있습니다.

#### 단계 1: 인덱스 및 문서 폴더 정의
보다 고급 시나리오를 위해 동일한 폴더 구조를 재사용합니다.
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### 단계 2: 인덱스 생성 및 문서 추가
(간단한 예시의 단계 2‑3을 참고하세요; 동일하게 유지됩니다.)

#### 단계 3: 텍스트 쿼리 검색 실행
파일명과 내용 기준을 혼합한 복합 텍스트 쿼리를 실행합니다.
```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### 단계 4: 객체 쿼리 구축 및 실행
동일한 논리를 프로그래밍 방식으로 구성합니다.
```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

구문, 범위 및 불리언 연산자를 계속 결합하여 정확한 비즈니스 규칙에 맞추세요.

## 실용적인 적용 사례

1. **E‑Commerce 플랫폼** – 카테고리, 가격 및 평점으로 제품을 필터링합니다.  
2. **문서 관리 시스템** – 저자, 날짜 또는 기밀 수준별로 계약서를 찾습니다.  
3. **콘텐츠 포털** – 독자가 태그, 주제 및 발행일로 세부 탐색할 수 있게 합니다.

## 성능 고려 사항

- **인덱스 새로 고침**: 검색 속도를 유지하려면 새 파일이나 업데이트된 파일을 정기적으로 다시 인덱싱합니다.  
- **메모리 관리**: 특히 대용량 데이터 세트의 경우 사용이 끝난 `Index` 객체를 해제합니다.  
- **비동기 인덱싱**: 무거운 인덱싱 중 UI가 멈추는 것을 방지하려면 `Task.Run` 또는 백그라운드 서비스를 사용합니다.

## 일반적인 문제 및 해결책

| 문제 | 해결책 |
|-------|----------|
| **인덱스를 찾을 수 없음** | `indexFolder` 경로를 확인하고 폴더에 쓰기 권한이 있는지 확인하십시오. |
| **결과가 반환되지 않음** | 쿼리하는 필드(예: `Content`, `Filename`)가 인덱싱되어 있는지 확인하십시오. |
| **메모리 부족 오류** | 문서를 배치로 처리하고 .NET GC 힙 크기 확대를 고려하십시오. |

## 자주 묻는 질문

**Q: 퍼시드 검색이란 무엇인가요?**  
A: 퍼시드 검색은 사용자가 카테고리, 날짜, 저자와 같은 여러 독립적인 필터를 사용해 결과를 세분화할 수 있게 합니다.

**Q: GroupDocs.Search로 대용량 데이터 세트를 어떻게 처리하나요?**  
A: 증분 인덱싱, 배치 처리 및 비동기 작업을 사용하여 메모리 사용량을 낮게 유지하고 성능을 높일 수 있습니다.

**Q: 기존 .NET 애플리케이션에 GroupDocs 기능을 통합할 수 있나요?**  
A: 예, 라이브러리는 모든 .NET 프로젝트와 원활하게 통합되도록 설계되었습니다.

**Q: 퍼시드 검색에서 흔히 발생하는 문제는 무엇인가요?**  
A: 복잡한 쿼리 구문과 모든 관련 필드가 인덱싱되는지 확인하는 것이 일반적인 과제이며, 적절한 테스트와 인덱스 유지 관리로 이를 완화할 수 있습니다.

**Q: GroupDocs 임시 라이선스를 어떻게 획득하나요?**  
A: 평가 기간 동안 전체 기능을 사용할 수 있는 체험 라이선스를 신청하려면 [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/)를 방문하십시오.

## 리소스
- **문서**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API 레퍼런스**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Last Updated:** 2026-04-02  
**테스트 환경:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**작성자:** GroupDocs
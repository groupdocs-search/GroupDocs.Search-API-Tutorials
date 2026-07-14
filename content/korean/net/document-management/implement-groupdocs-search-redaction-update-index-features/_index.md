---
date: '2026-06-07'
description: GroupDocs.Search 및 Redaction for .NET을 사용하여 인덱스를 효율적으로 업데이트하고 문서 관리 시스템을
  향상시키는 방법을 배웁니다.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: GroupDocs.Search 및 Redaction (.NET)으로 인덱스 업데이트하는 방법
type: docs
url: /ko/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# GroupDocs.Search 및 Redaction(.NET)으로 인덱스 업데이트 방법

현대의 데이터 중심 기업에서는 **how to update index**를 빠르고 신뢰성 있게 수행하는 것이 검색 경험을 좌우할 수 있습니다. 수천 개의 계약서나 방대한 지식 베이스를 다루든, 최신 문서 변경 사항과 검색 인덱스를 동기화하는 것은 빠르고 정확한 결과를 위해 필수적입니다. 이 튜토리얼에서는 .NET용 GroupDocs.Search와 GroupDocs.Redaction을 함께 사용하여 **update index** 파일을 업데이트하고, 버전 관리된 인덱스를 관리하며, 민감한 콘텐츠를 보호하는 방법을 깔끔한 .NET 프로젝트 내에서 안내합니다.

## 빠른 답변
- **“how to update index”는 무엇을 의미하나요?** 기존 검색 인덱스를 수정하여 새 문서나 변경된 문서가 처음부터 재구축하지 않고도 검색 가능하도록 하는 과정입니다.  
- **필요한 라이브러리는 무엇인가요?** .NET용 GroupDocs.Search 및 GroupDocs.Redaction (두 라이브러리 모두 NuGet을 통해 제공됩니다).  
- **라이선스가 필요합니까?** 무료 체험으로 테스트할 수 있으며, 프로덕션 라이선스를 구매하면 전체 기능을 사용할 수 있습니다.  
- **.NET Core에서 실행할 수 있나요?** 예, 라이브러리는 .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+를 지원합니다.  
- **성능은 어떨까요?** 2개의 스레드를 사용해 1 GB 인덱스를 업데이트하면 일반적인 4코어 서버에서 1분 이내에 완료됩니다.

## “how to update index”란 무엇인가요?
**How to update index**는 기존 검색 인덱스에 증분 변경을 적용하는 기술을 의미하며, 전체를 다시 생성하는 것이 아닙니다. 이 접근 방식은 다운타임을 줄이고 CPU 사용량을 절감하며, 문서가 추가, 편집 또는 삭제될 때 검색 결과를 최신 상태로 유지합니다.

## 인덱스 업데이트에 GroupDocs.Search 및 Redaction을 사용하는 이유는?
GroupDocs.Search는 **50개 이상의 파일 형식**(PDF, DOCX, XLSX, PPTX, HTML, 이미지 등)을 지원하며 전체 파일을 메모리에 로드하지 않고도 수백 페이지 문서를 처리할 수 있습니다. GroupDocs.Redaction과 결합하면 인덱싱 전에 민감한 데이터를 자동으로 제거하거나 마스킹하여 규정 준수를 보장하면서 검색 관련성을 유지할 수 있습니다.

## 사전 요구 사항
- **GroupDocs.Search** – NuGet을 통해 설치합니다.  
- **GroupDocs.Redaction for .NET** – 레드액션 기능에 필요합니다.  
- .NET 6+가 설치된 Visual Studio(또는 기타 .NET IDE).  
- 기본 C# 지식 및 인덱싱 개념에 대한 이해.

### 필요한 라이브러리 및 버전
- **GroupDocs.Search** – NuGet에서 최신 안정 버전을 사용합니다.  
- **GroupDocs.Redaction for .NET** – NuGet에서 최신 안정 버전을 사용합니다.

### 환경 설정 요구 사항
- .NET SDK가 설치된 Windows 또는 Linux 머신.  
- 인덱스 파일이 저장될 폴더에 대한 접근 권한.

### 지식 사전 요구 사항
- 문서 인덱싱 및 검색 기본 원리에 대한 이해.  
- 기업 시스템에서 문서 수명 주기 관리에 대한 인식.

## .NET용 GroupDocs.Redaction 설정

### 패키지 설치

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- “GroupDocs.Redaction”을 검색하고 최신 버전을 설치합니다.

### 라이선스 획득 단계
1. **Free Trial** – 모든 기능을 살펴볼 수 있는 체험판으로 시작합니다.  
2. **Temporary License** – 장기 테스트를 위한 임시 키를 요청합니다.  
3. **Purchase** – 프로덕션 배포를 위한 정식 라이선스를 획득합니다.

### 기본 초기화 및 설정
`Redactor`는 문서에 레드액션 규칙을 적용하는 핵심 클래스입니다.  
시작하려면 Redaction 네임스페이스를 참조하고 `Redactor` 인스턴스를 생성합니다:

```csharp
using GroupDocs.Redaction;
```

## 구현 가이드

우리는 두 가지 핵심 기능을 다룰 것입니다: 인덱싱된 문서 업데이트와 인덱스 버전 관리.

### GroupDocs.Search를 사용하여 인덱스를 업데이트하는 방법은?
`Index`는 디스크에 저장된 검색 가능한 컬렉션을 나타냅니다.  
`UpdateOptions`는 증분 업데이트 수행 방식을 구성합니다(예: 스레드 수).  
`UpdateDocument`는 단일 문서에 변경을 적용하고, `Commit`은 모든 보류 중인 업데이트를 최종 확정합니다.

**Direct answer (40‑70 words):** 인덱스 폴더를 가리키는 `Index` 객체를 생성하고, `UpdateOptions`로 스레드 수를 지정한 뒤, 변경된 각 파일에 대해 `UpdateDocument`를 호출하고 마지막으로 `Commit`을 실행하여 변경 사항을 영구 저장합니다. 이 증분 방식은 수정된 부분만 업데이트하여 전체 재구축 없이 인덱스를 최신 상태로 유지합니다.

#### 기능 1: 인덱싱된 문서 업데이트

##### 개요
인덱싱된 문서를 업데이트하면 문서가 편집되거나 교체될 때에도 검색 결과가 최신 콘텐츠를 반영합니다.

##### 단계 1: 인덱스 생성
`Index` 클래스는 디스크에 저장된 검색 가능한 컬렉션을 나타내는 최상위 객체입니다.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### 단계 2: 문서를 인덱스에 추가
디렉터리에서 파일을 추가하면 라이브러리가 자동으로 검색 가능한 텍스트를 추출합니다.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### 단계 3: 검색 및 업데이트
쿼리를 실행하고, 원본 파일을 수정한 뒤, 인덱싱 시 사용한 동일한 `UpdateOptions`와 함께 `UpdateDocument`를 호출합니다.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Why This Works:** `Threads = 2`로 설정하면 업데이트가 두 개의 CPU 코어를 활용하여 쿼드코어 머신에서 처리 시간을 약 절반으로 단축합니다.

### 인덱스 버전 관리를 유지하는 방법은?
`IndexUpdater`는 이전 인덱스 형식을 라이브러리가 지원하는 최신 버전으로 업그레이드하는 유틸리티 클래스입니다.

**Direct answer (40‑70 words):** 기존 인덱스 경로를 사용해 `IndexUpdater`를 인스턴스화하고, `CanUpdateVersion()`을 호출해 호환성을 확인한 뒤 필요하면 `UpdateVersion()`을 실행합니다. 업그레이드 후 새로운 형식으로 인덱스를 다시 로드하고 검색을 수행해 모든 것이 정상 작동하는지 확인합니다. 이를 통해 라이브러리 릴리스 간 원활한 마이그레이션을 보장합니다.

#### 기능 2: 인덱스 버전 관리 유지

##### 개요
버전 관리는 라이브러리 업그레이드 후에도 이전 인덱스를 검색 가능하도록 보장합니다.

##### 단계 1: 호환성 확인
`IndexUpdater`는 현재 인덱스를 최신 형식으로 업그레이드할 수 있는지 확인합니다.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### 단계 2: 로드 및 검색
업그레이드 후 새로 고친 인덱스를 로드하고 쿼리를 실행하여 무결성을 확인합니다.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Why This Works:** `CanUpdateVersion` 검사는 인덱스 스키마 불일치로 인한 런타임 예외를 방지하여 안전한 업그레이드 경로를 제공합니다.

## 실용적인 적용 사례

Real‑world scenarios where **how to update index** matters:

1. **Legal Document Management** – 계약서 수정 후 기밀 조항을 레드액션하면서 신속하게 재인덱싱합니다.  
2. **Corporate Archives** – 수백만 파일을 다시 처리하지 않고도 역사적 기록을 검색 가능하게 유지합니다.  
3. **Content Management Systems (CMS)** – 저자가 새 기사를 게시할 때 검색 인덱스에 증분 업데이트를 푸시합니다.

## 성능 고려 사항
- **Threading Options:** CPU 코어 수에 따라 `UpdateOptions.Threads`를 조정합니다; 스레드를 늘리면 처리량이 향상되지만 메모리 사용량도 증가합니다.  
- **Resource Usage:** RAM을 모니터링합니다; 라이브러리는 파일을 스트리밍하므로 500페이지 PDF에서도 메모리 급증이 최소화됩니다.  
- **Best Practices:** 정기적인 증분 업데이트를 예약하고, 오래된 인덱스 버전을 정리하여 최적의 성능을 유지합니다.

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결책 |
|-------|-------|----------|
| **Index not found** | 잘못된 폴더 경로 | `Index` 생성자가 올바른 디렉터리를 가리키는지 확인합니다. |
| **Version mismatch error** | 새 라이브러리와 함께 오래된 인덱스를 사용함 | `IndexUpdater` 흐름을 일반 인덱싱 전에 실행합니다. |
| **Redaction not applied** | 인덱싱 후 레드액션 규칙을 로드함 | 문서를 인덱스에 추가하기 **전에** 레드액션을 적용합니다. |

## 자주 묻는 질문

**Q: `UpdateDocument`와 `Rebuild`의 차이점은 무엇인가요?**  
A: `UpdateDocument`는 변경된 파일만 수정하고, `Rebuild`는 전체 인덱스를 처음부터 다시 생성하여 더 많은 시간과 자원을 소모합니다.

**Q: 여러 문서를 병렬로 업데이트할 수 있나요?**  
A: 예, 사용하려는 코어 수만큼 `UpdateOptions.Threads`를 설정하면 라이브러리가 내부적으로 병렬 처리를 수행합니다.

**Q: GroupDocs.Search가 암호화된 PDF를 지원하나요?**  
A: 물론 지원합니다. 문서를 로드할 때 `SearchOptions.Password`에 비밀번호를 제공하면 됩니다.

**Q: 인덱싱 전에 레드액션이 성공했는지 어떻게 확인하나요?**  
A: `Redactor.Apply()`를 호출하고 출력 파일 크기를 확인합니다; 파일 크기가 감소하면 레드액션이 성공했음을 나타냅니다.

**Q: 공식적으로 지원되는 .NET 버전은 무엇인가요?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, .NET 6+.

## 결론

이제 GroupDocs.Search를 사용하여 **how to update index**하는 방법과 .NET용 GroupDocs.Redaction으로 해당 인덱스를 버전 호환 상태로 유지하는 방법에 대한 완전하고 프로덕션 준비된 가이드를 보유하게 되었습니다. 위 단계들을 따르면 검색 레이어를 빠르고 정확하게 유지하면서 데이터 프라이버시 규정을 준수할 수 있습니다.

**다음 단계:**  
- 하드웨어에 맞는 최적의 `Threads` 설정을 실험해 보세요.  
- 인덱싱 전에 고급 레드액션 패턴(예: 정규식 기반 SSN 제거)을 탐색하세요.  
- 인덱스 업데이트 루틴을 CI/CD 파이프라인에 통합하여 문서 관리를 완전 자동화합니다.

---

**마지막 업데이트:** 2026-06-07  
**테스트 대상:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**작성자:** GroupDocs  

## 리소스
- [문서](https://docs.groupdocs.com/search/net/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction 다운로드](https://releases.groupdocs.com/search/net/)
- [무료 지원 포럼](https://forum.groupdocs.com/c/search/10)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

## 관련 튜토리얼
- [GroupDocs.Redaction .NET 마스터하기: 고급 문서 검색을 위한 효율적인 인덱스 생성 및 별칭 관리](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [GroupDocs.Redaction .NET으로 동의어 검색 구현하여 문서 관리 향상](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [.NET에서 GroupDocs Search와 Redaction 마스터하기: 고급 문서 관리](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
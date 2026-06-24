---
date: '2026-06-12'
description: GroupDocs.Search와 GroupDocs.Redaction을 활용하여 .NET에서 문서를 검색하고 레드액션하는 방법을
  배우고, 검색 성능을 최적화하며 인덱싱 오류를 처리하는 방법을 익히세요.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: .NET에서 GroupDocs.Search와 GroupDocs.Redaction을 사용해 문서를 검색하고 레드액션하는 방법
type: docs
url: /ko/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# .NET에서 GroupDocs.Search 및 GroupDocs.Redaction을 사용한 문서 검색 및 편집

현대 기업 환경에서는 **search and redact** 기능이 민감한 정보를 보호하면서 문서를 쉽게 검색할 수 있도록 하는 데 필수적입니다. 이 튜토리얼에서는 빠른 전체 텍스트 검색을 위한 GroupDocs.Search와 기밀 데이터를 안전하게 제거하는 GroupDocs.Redaction을 결합한 견고한 .NET 솔루션을 구축하는 과정을 안내합니다. 마지막까지 진행하면 라이브러리를 설정하고, 사용자 정의 텍스트 세그멘터를 만들고, 고성능 검색을 실행하며, 안전하게 편집을 적용하는 방법을 알게 됩니다.

## 빠른 답변
- **What does “search and redact” mean?** 문서에서 텍스트를 찾아 영구적으로 가리는 것을 의미합니다.  
- **Which libraries are required?** .NET용 GroupDocs.Search 및 GroupDocs.Redaction.  
- **Can I handle multilingual content?** 예—맞춤 텍스트 세그멘터를 사용하여 단어를 올바르게 분할합니다.  
- **How do I improve search speed?** 인덱스를 한 번 생성하고 재사용하며 `optimize search performance` 설정을 활성화합니다.  
- **What if indexing fails?** 문제 해결 섹션의 “handle indexing errors” 가이드라인을 따르세요.

## “search and redact”란 무엇인가요?
search and redact는 문서 컬렉션에서 특정 용어를 찾아 해당 용어를 영구적으로 가리거나 제거하여 프라이버시를 보호하거나 규제 준수를 충족하는 과정입니다. 전체 텍스트 검색으로 민감한 정보를 찾고, 문서의 원래 레이아웃을 유지하면서 내용을 교체하는 편집 도구를 결합합니다.

## GroupDocs.Search와 GroupDocs.Redaction을 함께 사용하는 이유는?
GroupDocs.Search는 **50개 이상의 파일 형식**을 지원하고 일반 서버 하드웨어에서 1분 미만에 **100,000개 이상의 문서**를 인덱싱할 수 있으며, GroupDocs.Redaction은 원본 레이아웃을 변경하지 않고 **PDF, DOCX, PPTX 등**에 편집을 적용할 수 있습니다. 두 제품을 결합하면 **검색 성능을 최적화**하고 **인덱싱 오류를** 원활하게 처리하는 단일 스택 솔루션을 제공합니다.

## 전제 조건

- Visual Studio 2022 이상 및 .NET 6+ 지원.  
- NuGet 패키지: **GroupDocs.Search** 및 **GroupDocs.Redaction** (최신 안정 버전).  
- 유효한 GroupDocs 라이선스(체험판 또는 구매).  

### 필수 라이브러리
- **GroupDocs.Search** – 인덱싱, 쿼리 및 맞춤 세그멘테이션 제공.  
- **GroupDocs.Redaction** – 지원되는 형식 전반에 걸쳐 텍스트, 이미지 및 메타데이터 편집 제공.

### 환경 설정 요구 사항
인덱스가 저장될 폴더에 대한 쓰기 권한이 개발 머신에 있는지 확인하십시오.

### 지식 전제 조건
- C# 및 .NET 프로젝트 구조에 대한 친숙함.  
- 문서 처리 개념에 대한 기본 이해(선택 사항이지만 도움이 됨).

## .NET용 GroupDocs.Redaction을 어떻게 설치하나요?
Redaction 패키지를 .NET CLI 또는 NuGet 패키지 관리자를 사용하여 프로젝트에 추가할 수 있습니다. 명령은 최신 안정 버전을 다운로드하고 프로젝트 파일에 등록하여 API를 즉시 사용할 수 있게 합니다.  

```bash
dotnet add package GroupDocs.Redaction
```  

## GroupDocs 라이선스를 어떻게 획득하나요?
GroupDocs는 세 가지 라이선스 옵션을 제공합니다: 평가용 무료 체험, 확장된 개발 테스트를 위한 임시 라이선스, 그리고 운영용 전체 상용 라이선스. 체험판은 제한된 기능을 제공하고, 임시 키는 평가 기간을 연장하며, 구매한 라이선스는 모든 기능과 우선 지원을 해제합니다.

## 애플리케이션에서 GroupDocs.Redaction을 어떻게 초기화하나요?
`Redaction` 클래스는 지원되는 문서에 편집을 적용하기 위한 주요 진입점입니다. 파일을 로드하고 편집 객체를 준비한 뒤 편집 프로세스를 실행하여 원본 레이아웃을 유지한 채 수정된 문서를 반환합니다. 색상, 오버레이, 메타데이터 제거와 같은 편집 옵션을 구성하여 특정 규정 요구 사항을 충족할 수 있습니다.  

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## GroupDocs.Search를 사용하여 인덱스를 어떻게 설정하나요?
`Index` 클래스는 디스크에 저장된 검색 가능한 저장소를 나타냅니다. 인덱스의 생성, 업데이트 및 쿼리를 관리하여 문서를 추가하고, 인덱스를 재구성하며, 대규모 컬렉션에서 빠른 검색을 실행할 수 있습니다. 인덱스 폴더는 로컬 또는 네트워크 스토리지에 위치할 수 있으며, 압축 및 암호화 설정을 구성하여 인덱스된 데이터를 보호할 수 있습니다.  

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## 맞춤 텍스트 세그멘터란 무엇이며 왜 사용해야 하나요?
맞춤 텍스트 세그멘터는 원시 텍스트를 검색 가능한 토큰으로 어떻게 분할할지를 결정합니다. 특정 언어나 도메인에 맞게 세그멘테이션 규칙을 조정하면 토큰화 정확도가 향상되어 검색 결과의 재현율과 관련성이 높아집니다. 이는 일본어 또는 아랍어와 같이 복잡한 단어 경계가 있는 언어에 특히 유용한데, 기본 토크나이저가 단어를 잘못 분할할 수 있기 때문입니다.  

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## 맞춤 세그멘터를 사용하여 전체 텍스트 검색을 어떻게 수행하나요?
`SearchQuery` 객체는 사용자의 쿼리를 캡슐화하고 맞춤 세그멘터와 함께 작동하여 일치 항목을 찾습니다. 퍼지 매칭, 구문 쿼리 및 가중치를 지원하며 문서 ID, 히트 위치 및 관련 점수를 포함한 결과 집합을 반환합니다. 파일 유형이나 날짜 범위와 같은 필터를 적용하여 결과를 보다 정확하게 좁힐 수도 있습니다.  

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## 민감한 텍스트를 찾은 후 편집을 어떻게 적용하나요?
`Redaction` API를 사용하면 지원되는 문서에서 텍스트, 이미지 및 메타데이터를 교체하거나 제거할 수 있습니다. 민감한 용어를 식별한 후 편집 객체를 생성하고 적용한 뒤 편집된 파일을 저장하여 기밀 정보가 영구적으로 숨겨지도록 합니다. 편집 옵션에는 검은 상자를 오버레이하거나 맞춤 색상을 적용하거나 문서 구조를 유지하면서 전체 객체를 제거하는 것이 포함됩니다.  

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## 일반적인 문제 및 인덱싱 오류 처리 방법
- **Index Not Found:** 인덱스 경로가 존재하고 애플리케이션에 읽기/쓰기 권한이 있는지 확인하십시오.  
- **Search Returns No Results:** 인덱싱 프로세스를 다시 실행하고 맞춤 세그멘터가 올바르게 등록되었는지 확인하십시오.  
- **Redaction Fails on Certain Formats:** 파일 형식이 지원되는지 확인하십시오; PDF의 경우 PDF 2.0 기능을 처리하려면 최신 Redaction 버전을 사용하십시오.

## 실용적인 적용 사례
1. **Legal Document Management:** 계약서에서 “non‑disclosure”를 검색하고 외부 공유 전에 조항을 자동으로 편집합니다.  
2. **Academic Research:** 원고에서 미공개 데이터를 찾아 동료 검토 과정에서 숨깁니다.  
3. **Business Contracts:** 수천 개의 계약서를 일괄 처리하여 개인 식별자를 편집하면서 법적 문구를 유지합니다.

## 대용량 문서 세트에 대한 검색 성능을 어떻게 최적화할 수 있나요?
성능을 극대화하려면 문서를 한 번 인덱싱하고 이후 쿼리에서 동일한 인덱스를 재사용하십시오. 병렬 처리를 활성화하고 캐시를 구성하며 인덱스 설정을 조정하여 다중 코어 서버에서 지연 시간을 줄이고 처리량을 향상시킵니다. 또한 `EnableMemoryMapping` 플래그를 설정하여 인덱스를 메모리 매핑하도록 하면 대규모 데이터셋의 읽기 작업이 빨라집니다.

## 대용량 파일 작업 시 .NET 메모리를 어떻게 관리하나요?
대용량 문서를 처리할 때 효율적인 메모리 관리가 중요합니다. `Index` 및 `Redaction` 객체를 `using` 문으로 감싸서 결정적인 해제를 보장하고, 전체 문서를 메모리에 로드하는 대신 스트림으로 파일을 처리하십시오. 성능 카운터를 모니터링하면 메모리 급증을 조기에 감지하여 배치 크기를 조정하거나 가비지 컬렉션 튜닝을 활성화할 수 있습니다.

## 자주 묻는 질문

**Q: GroupDocs.Search를 비텍스트 메타데이터와 함께 사용할 수 있나요?**  
A: 예—메타데이터 필드를 문서 내용과 함께 인덱싱할 수 있어 “author:JohnDoe”와 같은 검색이 가능합니다.

**Q: GroupDocs.Redaction이 웹 API에서 실시간 편집을 지원하나요?**  
A: 지원합니다; 작은 파일은 Redaction API를 동기식으로 호출하고, 큰 작업은 비동기 처리를 위해 큐에 넣을 수 있습니다.

**Q: 인덱스가 손상되면 어떻게 해야 하나요?**  
A: 손상된 인덱스 폴더를 삭제하고 동일한 인덱싱 루틴으로 재구축하십시오; 라이브러리는 원인을 정확히 파악할 수 있도록 상세 오류 메시지를 기록합니다.

**Q: 저장하기 전에 편집된 문서를 미리 볼 수 있나요?**  
A: 물론입니다—`preview` 플래그와 함께 `redaction.Apply()`를 호출하면 검토용 임시 버전을 생성합니다.

**Q: 공식적으로 지원되는 .NET 버전은 무엇인가요?**  
A: GroupDocs.Search와 GroupDocs.Redaction은 .NET 6, .NET 5, .NET Core 3.1 및 .NET Framework 4.6.2+를 지원합니다.

## 리소스

- **Documentation:** [GroupDocs Redaction 문서](https://docs.groupdocs.com/search/net/)
- **API Reference:** [GroupDocs API 레퍼런스](https://reference.groupdocs.com/redaction/net)
- **Download:** [GroupDocs 릴리스](https://releases.groupdocs.com/search/net/)
- **Free Support:** [GroupDocs 포럼](https://forum.groupdocs.com/c/search/10)
- **Temporary License:** [GroupDocs 임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-06-12  
**테스트 대상:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**작성자:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## 관련 튜토리얼

- [GroupDocs Search 및 Redaction 마스터하기 (.NET): 고급 문서 관리](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [GroupDocs.Search 및 Redaction 구현: .NET에서 문서 인덱스 업데이트 및 관리](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [GroupDocs.Redaction으로 .NET에서 문서 인덱싱 최적화: 취소, 비동기 및 스레드](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
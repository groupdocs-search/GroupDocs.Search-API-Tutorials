---
date: '2026-04-27'
description: GroupDocs.Search와 Redaction을 사용하여 .NET에서 민감한 데이터를 삭제하는 방법을 배우고, 대용량 문서를
  검색하기 위해 인덱스에 문서를 추가하는 방법을 알아보세요.
keywords:
- redact sensitive data
- add documents to index
- search large documents
title: GroupDocs.Search 및 .NET의 Redaction – 민감한 데이터 삭제
type: docs
url: /ko/net/document-management/groupdocs-search-redaction-net-guide/
weight: 1
---

# GroupDocs.Search 및 Redaction in .NET – 민감한 데이터 가리기

방대한 양의 문서를 관리하는 것은 어려울 수 있습니다, 특히 **민감한 데이터를 가리기** 하면서도 빠른 검색 기능을 제공해야 할 때 더욱 그렇습니다. 이 가이드에서는 GroupDocs.Search와 GroupDocs.Redaction을 설정하는 방법을 단계별로 안내하고, **문서를 인덱스에 추가**하는 방법, 효율적인 **대용량 문서 검색** 작업 수행 방법을 보여주며, 모든 것이 개인정보 보호 요구사항을 준수하도록 합니다.

## 빠른 답변
- **“민감한 데이터 가리기”가 무엇을 의미합니까?** 문서에서 기밀 정보를 영구적으로 제거하거나 가리는 것을 의미합니다.
- **필요한 라이브러리는 무엇입니까?** .NET용 GroupDocs.Search 및 GroupDocs.Redaction (NuGet을 통해 제공).
- **.NET 프로젝트를 자동으로 인덱싱할 수 있습니까?** 예 – 단계별 안내는 “How to index .NET” 섹션을 참조하십시오.
- **대용량 파일을 어떻게 처리합니까?** 데이터를 관리 가능한 조각으로 처리하기 위해 청크 기반 검색을 사용하십시오.
- **프로덕션에 라이선스가 필요합니까?** 프로덕션 사용을 위해 유효한 GroupDocs 라이선스가 필요합니다; 무료 체험판을 이용할 수 있습니다.

## 민감한 데이터 가리기란?
민감한 데이터를 가리는 것은 개인, 재무 또는 기밀 정보를 문서에서 영구적으로 제거하거나 가려서 무단 사용자가 복구하거나 볼 수 없도록 하는 과정입니다.

## 왜 GroupDocs.Search와 Redaction을 결합해야 할까요?
- **Speed:** 밀리초 단위로 결과를 반환하는 검색 가능한 인덱스를 구축합니다.  
- **Security:** 문서를 공유하거나 저장하기 전에 가리기 규칙을 적용합니다.  
- **Scalability:** 청크 검색을 통해 메모리를 소모하지 않고 테라바이트 규모의 텍스트를 처리할 수 있습니다.  
- **Compliance:** 기밀 데이터가 유출되지 않도록 함으로써 GDPR, HIPAA 및 기타 규정을 준수합니다.

## 전제 조건
- .NET 개발 환경 (Visual Studio 권장).
- 기본 C# 지식.
- 필요한 패키지를 설치하기 위한 NuGet 접근 권한.

## .NET용 GroupDocs.Redaction 설정

### .NET CLI를 통한 설치
```bash
dotnet add package GroupDocs.Redaction
```

### 패키지 관리자 설치
```powershell
Install-Package GroupDocs.Redaction
```

### NuGet 패키지 관리자 UI
**"GroupDocs.Redaction"**을 검색하고 최신 버전을 설치합니다.

### 라이선스 획득 단계
- **Free Trial:** 기능을 탐색하기 위해 무료 체험판으로 시작합니다.
- **Temporary License:** 장기 사용을 위해 임시 라이선스를 요청합니다.
- **Purchase:** 장기 프로덕션 사용을 위해 구매를 고려합니다.

### 기본 초기화 및 설정
```csharp
using GroupDocs.Redaction;

RedactorSettings settings = new RedactorSettings();
// Initialize with desired options or default ones
```

## 구현 가이드

### GroupDocs.Search를 사용하여 .NET 프로젝트 인덱싱하기
아래에서는 구현을 명확한 번호 단계로 나누어 쉽게 따라 할 수 있도록 합니다.

#### 단계 1: 인덱스 폴더 지정
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SearchByChunks";
```
*왜?* 전용 폴더를 정의하면 인덱스가 정리되고 원본 문서와 분리됩니다.

#### 단계 2: 인덱스 생성 및 구성
```csharp
Index index = new Index(indexFolder);
```
*목적:* 지정한 위치에 새로운 검색 가능한 인덱스를 생성합니다.

#### 단계 3: **문서를 인덱스에 추가**
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath1");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath3");
```
*설명:* 각 호출은 파일(또는 폴더)을 인덱스에 추가하여 해당 내용이 검색 가능하도록 합니다.

### 청크 검색을 사용한 대용량 문서 검색
청크 검색을 사용하면 대용량 파일을 작은 조각으로 나누어 메모리 사용량을 낮게 유지할 수 있습니다.

#### 단계 1: 검색 쿼리 정의
```csharp
string query = "invitation";
```
*목적:* 모든 인덱스된 파일에서 찾고자 하는 용어입니다.

#### 단계 2: 청크 검색 옵션 구성
```csharp
SearchOptions options = new SearchOptions();
options.IsChunkSearch = true;
```
*설명:* `IsChunkSearch`를 활성화하면 엔진이 데이터를 청크 단위로 처리하도록 지시합니다.

#### 단계 3: 초기 검색 실행
```csharp
SearchResult result = index.Search(query, options);
Console.WriteLine("Document count: " + result.DocumentCount);
Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
```
*결과:* 해당 용어가 포함된 문서 수와 전체 발생 횟수를 보여줍니다.

#### 단계 4: 이후 청크 계속 처리
```csharp
while (result.NextChunkSearchToken != null)
{
    result = index.SearchNext(result.NextChunkSearchToken);
    Console.WriteLine("Document count: " + result.DocumentCount);
    Console.WriteLine("Occurrence count: " + result.OccurrenceCount);
}
```
*왜 이 루프인가?* 전체 데이터셋이 처리될 때까지 모든 청크에서 결과를 가져오도록 보장합니다.

### GroupDocs.Redaction을 사용한 민감한 데이터 가리기
보호해야 할 정보를 찾은 후, 가리기 규칙을 적용합니다.

#### 단계 1: 가리기 설정 초기화
```csharp
RedactorSettings settings = new RedactorSettings();
```

#### 단계 2: 가리기 적용
`Redactor` 클래스를 사용하여(원본 코드를 그대로 유지하기 위해 여기서는 표시되지 않음) 마스킹하려는 패턴, 텍스트 또는 이미지를 정의합니다.  
*팁:* 실수로 데이터가 손실되는 것을 방지하기 위해 먼저 문서 복사본에서 가리기 규칙을 테스트하십시오.

## 실용적인 적용 사례
이 기능들은 다양한 산업에서 빛을 발합니다:

1. **Legal Document Management** – 사례 파일을 빠르게 검색하면서 클라이언트 기밀 정보를 가립니다.  
2. **Healthcare Data Handling** – 환자 PHI를 보호하면서 의료진이 관련 기록을 찾을 수 있도록 합니다.  
3. **Financial Auditing** – 방대한 거래 로그를 인덱싱하고 계좌 번호 또는 개인 식별자를 가립니다.

## 성능 고려 사항
- **Optimize Indexing:** 변경된 파일만 다시 인덱싱하여 불필요한 작업 없이 인덱스를 최신 상태로 유지합니다.
- **Manage Resources:** 서버 RAM에 따라 청크 크기(`options.ChunkSize`)를 조정합니다.
- **Async Operations:** 대량 배치의 경우 비동기 인덱싱을 사용하여 UI가 응답성을 유지하도록 합니다.

## 자주 묻는 질문

**Q: 대용량 파일을 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: 청크 기반 검색(`IsChunkSearch = true`)을 사용하여 데이터를 작은 조각으로 처리함으로써 메모리 부담을 줄입니다.

**Q: GroupDocs.Redaction이 암호화된 문서와 함께 사용할 수 있나요?**  
A: 예 – 먼저 파일을 복호화하고, 가리기를 적용한 뒤 필요하면 다시 암호화합니다.

**Q: 어떤 라이선스 옵션이 제공되나요?**  
A: 무료 체험판, 평가용 임시 라이선스, 그리고 프로덕션용 전체 상용 라이선스가 있습니다.

**Q: 인덱스 오류를 어떻게 해결할 수 있나요?**  
A: 인덱스 폴더 경로가 올바른지 확인하고, 애플리케이션에 읽기/쓰기 권한이 있는지 확인하며, 모든 문서 형식이 지원되는지 점검합니다.

**Q: 검색 쿼리를 더 커스터마이즈할 수 있나요?**  
A: 물론입니다. `SearchOptions` API를 사용하여 부울 연산자, 와일드카드, 근접 검색 등을 결합할 수 있습니다.

## 리소스
- **문서:** [GroupDocs Redaction .NET](https://docs.groupdocs.com/search/net/)  
- **API 레퍼런스:** [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net)  
- **다운로드:** [Latest Releases](https://releases.groupdocs.com/search/net/)  
- **무료 지원:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **임시 라이선스:** [Request Here](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-04-27  
**테스트 환경:** GroupDocs.Search 23.9 and GroupDocs.Redaction 23.9 for .NET  
**작성자:** GroupDocs
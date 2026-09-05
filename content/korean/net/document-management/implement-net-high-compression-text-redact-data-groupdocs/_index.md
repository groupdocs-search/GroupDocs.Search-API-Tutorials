---
date: '2026-06-07'
description: 고압축 .NET을 텍스트 저장에 구현하고, .NET 애플리케이션에서 GroupDocs.Search와 GroupDocs.Redaction을
  사용하여 기밀 데이터를 레다크션하는 방법을 배우세요.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: '고압축 .NET을 GroupDocs와 함께 구현: 텍스트 및 레다크션 가이드'
type: docs
url: /ko/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# GroupDocs와 함께 고압축 .NET 구현: 텍스트 및 레드랙션 가이드

현대 .NET 솔루션에서는 대용량 텍스트 컬렉션을 디스크 사용량을 크게 늘리지 않고 저장해야 할 때 **고압축 .NET 구현**이 필수적입니다. 동시에 개인 식별자나 재무 수치와 같은 민감한 정보를 보호하려면 신뢰할 수 있는 레드랙션이 필요합니다. 이 튜토리얼에서는 **GroupDocs.Search**를 사용하여 고압축 텍스트 저장소를 구성하는 방법과 **GroupDocs.Redaction**을 사용해 기밀 데이터를 안전하게 레드랙션하는 방법을 단계별로 보여줍니다. 최종적으로 색인된 텍스트를 최대 90 %까지 압축하고 PDF, Word 파일 및 기타 다양한 형식에서 개인 정보를 제거할 수 있게 됩니다.

## 빠른 답변
- **고압축 인덱싱을 제공하는 라이브러리는 무엇인가요?** GroupDocs.Search for .NET.  
- **민감한 데이터를 레드랙션하는 도구는 무엇인가요?** GroupDocs.Redaction for .NET.  
- **문서를 자동으로 인덱스에 추가할 수 있나요?** 예—`AddDocument` API를 폴더 스캔 루프 내에서 사용하세요.  
- **압축이 검색에 대해 무손실인가요?** 예, 압축 후에도 텍스트는 완전히 검색 가능합니다.  
- **프로덕션에 라이선스가 필요합니까?** 상업적 사용을 위해서는 영구적인 GroupDocs 라이선스가 필요합니다.

## “고압축 .NET 구현”이란 무엇인가요?
고압축 .NET 구현은 GroupDocs.Search 인덱싱 엔진을 구성하여 추출된 텍스트 콘텐츠를 압축된 형태로 저장하는 것을 의미합니다. 이를 통해 디스크상의 인덱스 크기가 크게 감소하면서도 텍스트는 완전히 검색 가능하게 유지됩니다. 압축은 무손실이며, 쿼리 관련성 및 스니펫 추출이 압축되지 않은 인덱스와 동일하게 작동합니다.

## 압축 및 레드랙션에 GroupDocs를 사용하는 이유는?
GroupDocs.Search는 50개가 넘는 입력 형식을 지원하며 색인된 텍스트를 최대 90 %까지 압축할 수 있어 대규모 문서 컬렉션이 원본 크기의 일부만 차지하도록 합니다. GroupDocs.Redaction은 30개가 넘는 파일 유형에서 민감한 정보를 영구적으로 삭제하거나 마스킹하여 GDPR 및 HIPAA와 같은 엄격한 규정 준수를 추가 도구 없이도 충족하도록 도와줍니다.

## 사전 요구 사항
- **개발 환경:** Visual Studio 2022 이상, .NET 6+ (또는 .NET Framework 4.7.2).  
- **라이브러리:** `GroupDocs.Search` 및 `GroupDocs.Redaction` NuGet 패키지.  
- **권한:** 소스 문서와 인덱스 출력 위치가 있는 폴더에 대한 읽기/쓰기 접근 권한.  
- **기본 지식:** C# 구문, 파일 I/O, .NET 프로젝트 구조에 대한 이해.

## GroupDocs와 함께 고압축 .NET을 구현하는 방법은?
GroupDocs를 사용하여 고압축 .NET을 구현하려면 먼저 `TextStorageSettings` 인스턴스를 생성하고 `CompressionLevel`을 `High`로 설정합니다. 그런 다음 `Index` 객체를 인스턴스화하고 설정과 인덱스가 저장될 폴더를 전달합니다. 인덱스가 준비되면 `AddDocument`를 사용해 문서를 추가하고, 마지막으로 `Search` 메서드로 검색을 실행하면 엔진이 압축 및 압축 해제를 자동으로 처리합니다.

### 단계 1: 필요한 NuGet 패키지 설치
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- “GroupDocs.Search”를 검색하고 **Install**을 클릭합니다.  

### 단계 2: GroupDocs.Redaction 설치 (데이터 레드랙션용)
- **NuGet Package Manager**를 엽니다.  
- **GroupDocs.Redaction**을 검색하고 최신 안정 버전을 설치합니다.  

### 단계 3: 라이선스 획득 및 적용
- **무료 체험:** GroupDocs 포털에 등록하여 30일 체험 키를 받습니다.  
- **임시 라이선스:** 개발 환경용 임시 키를 요청합니다.  
- **영구 라이선스:** 평가 제한을 제거하기 위해 프로덕션 라이선스를 구매합니다.

### 단계 4: 두 라이브러리 기본 초기화
`Search`와 `Redaction` 엔진은 공통 라이선스 모델을 공유합니다. 애플리케이션 시작 시 초기화합니다:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## 기능 1: 고압축 텍스트 저장 설정

### 인덱싱 구성 설정
`TextStorageSettings`는 GroupDocs.Search가 추출된 텍스트를 어떻게 보관할지 지정하는 클래스입니다. 고압축을 활성화하면 검색 속도에 영향을 주지 않으면서 인덱스 크기를 최대 **10배**까지 줄일 수 있습니다.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**설명:**  
- `CompressionLevel.High`는 텍스트 블록을 효율적으로 압축하는 ZSTD 기반 알고리즘을 활성화합니다.  
- `UseMemoryCache = false`는 엔진이 디스크에서 데이터를 스트리밍하도록 강제하여 대규모 배포에 적합합니다.

### 인덱스 생성 및 관리
`Index` 객체는 디스크상의 검색 가능한 저장소를 나타냅니다. 인덱스 파일이 저장될 폴더를 지정하고 위에서 정의한 압축 설정을 전달합니다.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**설명:**  
- `indexFolder`는 압축된 인덱스 파일이 위치할 경로를 결정합니다.  
- `settings`는 고압축 구성을 주입하여 추가되는 모든 문서가 이를 활용하도록 합니다.

## 기능 2: 문서를 인덱스에 추가하기

### 인덱스에 문서 추가
`AddDocument`는 단일 파일을 인덱스에 추가하고, 텍스트를 추출한 뒤 설정된 압축 방식으로 압축하여 결과를 저장합니다. GroupDocs.Search는 디렉터리 트리에서 파일을 가져올 수 있습니다. 다음 루프는 `documentsFolder`를 순회하면서 각 파일을 추가하고 진행 상황을 로그에 기록합니다.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**설명:**  
- `AddDocument`는 파일을 파싱하고 검색 가능한 텍스트를 추출한 뒤 `TextStorageSettings`에 따라 압축하고 인덱스에 저장합니다.  
- 이 방법은 **PDF, DOCX, TXT, HTML** 및 30개가 넘는 다른 형식에서도 작동합니다.

## 기능 3: 검색 쿼리 실행

### 검색 수행
`Search`는 압축된 인덱스에 대해 쿼리를 실행하고 관련성 점수와 강조된 스니펫을 포함한 일치하는 `DocumentResult` 객체 컬렉션을 반환합니다. 인덱스가 채워지면 빠른 쿼리를 실행할 수 있습니다. `Search` 메서드는 파일 경로와 강조된 스니펫을 포함하는 `DocumentResult` 객체 컬렉션을 반환합니다.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**설명:**  
- 검색 엔진은 압축된 텍스트를 직접 스캔하므로 **수백만 페이지**가 포함된 인덱스에서도 쿼리 지연 시간이 낮게 유지됩니다.  
- `Score`는 관련성을 나타내며 값이 높을수록 더 좋은 매치입니다.

## GroupDocs.Redaction으로 기밀 데이터 레드랙션하는 방법은?
GroupDocs.Redaction으로 기밀 데이터를 레드랙션하려면 먼저 대상 파일에 대한 `Redactor` 인스턴스를 생성합니다. 사회보장번호와 같은 텍스트를 제거하기 위한 정규식 등 하나 이상의 `SearchPattern` 객체를 정의합니다. 각 패턴을 `Redact`로 적용하고 `BlackOut`과 같은 `RedactionType`을 지정한 뒤 결과를 새 문서로 저장하여 원본 파일이 손상되지 않도록 합니다.

`Redactor`는 문서를 로드하고 레드랙션 작업을 수행하는 GroupDocs.Redaction의 주요 클래스입니다.  
`SearchPattern`은 레드랙션할 텍스트를 식별하는 정규식을 정의합니다.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**설명:**  
- `SearchPattern`은 정규식을 사용해 사회보장번호를 찾습니다.  
- `RedactionType.BlackOut`은 일치하는 텍스트를 검은 사각형으로 대체하여 데이터가 복구되지 않도록 합니다.

## 실용적인 적용 사례
1. **법률 문서 관리:** 대용량 사건 파일을 자동으로 압축하고 보관 전에 클라이언트 식별자를 레드랙션합니다.  
2. **헬스케어 기록:** 수년간의 환자 노트를 압축된 인덱스에 저장하고 연구 파트너와 공유하기 전에 PHI(보호된 건강 정보)를 제거합니다.  
3. **재무 보고:** 계좌 번호를 레드랙션하여 분기 보고서를 보호하면서도 감사 쿼리를 위한 검색 가능한 텍스트는 유지합니다.

## 성능 고려 사항
- **압축 영향:** 고압축은 인덱스 크기를 최대 **90 %**까지 줄여 SSD 마모를 감소시키고 백업 작업을 가속화합니다.  
- **메모리 사용량:** 매우 큰 인덱스의 경우 메모리 캐싱을 비활성화하여 프로세스 메모리 사용량을 **500 MB** 이하로 유지합니다.  
- **I/O 최적화:** 디스크 스래싱을 최소화하기 위해 문서 추가를 100개씩 배치합니다.  
- **비동기 처리:** 데스크톱 앱에서 UI 스레드가 응답하도록 `AddDocument` 호출을 `Task.Run`으로 래핑합니다.

## 일반적인 함정 및 문제 해결
- **잘못된 파일 경로:** `documentsFolder`와 `indexFolder`가 절대 경로인지, 애플리케이션에 읽기/쓰기 권한이 있는지 확인합니다.  
- **라이선스 오류:** `.lic` 파일이 실행 파일과 함께 배포되었거나 리소스로 포함되어 있는지 확인합니다.  
- **검색 결과 없음:** `TextStorageSettings` 압축 수준이 인덱싱 시 사용한 것과 일치하는지 확인합니다. 설정이 일치하지 않으면 역직렬화 오류가 발생할 수 있습니다.

## 자주 묻는 질문

**Q: 초기 구축 후에도 인덱스에 문서를 추가할 수 있나요?**  
A: 예—새 파일에 대해 `index.AddDocument`를 호출하면 엔진이 압축 인덱스를 점진적으로 업데이트합니다.

**Q: 레드랙션이 원본 파일을 변경합니까?**  
A: 아니요—원본 파일은 그대로 유지됩니다; 레드랙션된 버전은 새 파일로 저장되어 문서 무결성을 보존합니다.

**Q: GroupDocs.Redaction이 지원하는 형식은 무엇인가요?**  
A: PDF, DOCX, PPTX, XLSX, 이미지(PNG, JPEG) 및 일반 텍스트를 포함해 **30개** 이상의 형식을 지원합니다.

**Q: 고압축이 검색 관련성에 어떤 영향을 줍니까?**  
A: 영향을 주지 않습니다. 텍스트 압축은 무손실이므로 관련성 점수는 압축되지 않은 인덱스와 동일합니다.

**Q: 인덱싱할 수 있는 문서 크기에 제한이 있나요?**  
A: GroupDocs.Search는 스트리밍을 통해 수 기가바이트 파일을 처리할 수 있지만, 압축 인덱스를 위한 충분한 디스크 공간(원본 크기의 약 10 %)을 확보해야 합니다.

## 리소스
- [문서](https://docs.groupdocs.com/search/net/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction for .NET 다운로드](https://releases.groupdocs.com/search/net/)
- [무료 지원 포럼](https://forum.groupdocs.com/c/search/10)
- [임시 라이선스 획득](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-06-07  
**테스트 환경:** GroupDocs.Search 23.12 및 GroupDocs.Redaction 23.12 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [.NET 문서 관리를 위한 GroupDocs.Search 및 Redaction 구현](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [.NET용 GroupDocs.Redaction 최적화 방법: 효율적인 인덱스 및 맞춤법 관리 가이드](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [.NET에서 GroupDocs Redaction 및 Search 마스터하기: 효율적인 문서 관리 및 보안 검색](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
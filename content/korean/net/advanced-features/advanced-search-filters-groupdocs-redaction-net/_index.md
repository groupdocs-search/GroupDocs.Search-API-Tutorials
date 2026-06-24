---
date: '2026-04-02'
description: GroupDocs.Redaction for .NET을 사용하여 파일 확장자로 필터링하고 txt 파일만 검색하는 방법을 배우고,
  문서 관리 효율성을 높이세요.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: .NET에서 GroupDocs.Redaction을 사용하여 파일 확장자로 필터링
type: docs
url: /ko/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# .NET에서 GroupDocs.Redaction을 사용한 파일 확장자별 필터링

대량의 파일 컬렉션을 검색하는 것은 특히 특정 파일 유형의 결과만 필요할 때 압도적으로 느껴질 수 있습니다. 이 튜토리얼에서는 GroupDocs.Redaction for .NET을 사용하여 **파일 확장자별 필터링** 방법을 알아보고, txt 파일이나 원하는 다른 확장자만 검색할 수 있습니다. 파일 유형 및 경로 기반 필터 설정 방법을 단계별로 안내하여 필요한 문서를 빠르게 찾을 수 있습니다.

## 빠른 답변
- **“filter by file extension”가 무엇을 하나요?** 지정된 파일 확장자(예: *.txt)와 일치하는 문서만 검색하도록 제한합니다.  
- **왜 GroupDocs.Redaction을 사용하나요?** 빠르고 쉽게 통합할 수 있는 내장 필터링 API를 제공합니다.  
- **라이선스가 필요합니까?** 테스트용으로는 무료 체험판을 사용할 수 있으며, 프로덕션에서는 유료 라이선스가 필요합니다.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **파일 유형 필터와 경로 필터를 결합할 수 있나요?** 예—정밀한 검색을 위해 여러 필터를 적용할 수 있습니다.

## 배우게 될 내용
- 텍스트 파일만 검색하도록 **파일 확장자별 필터링** 방법.  
- 특정 폴더나 이름 패턴으로 결과를 제한하는 **파일 경로 필터** 설정 방법.  
- 인덱스를 빠르고 메모리 효율적으로 유지하기 위한 팁.

## 전제 조건

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- **GroupDocs.Redaction Library**가 설치되어 있고 .NET 프로젝트와 호환되는지 확인하십시오.  
- Visual Studio 또는 VS Code와 같은 개발 환경.  
- 기본 C# 지식 및 .NET 프로젝트 구조에 대한 이해.

## .NET용 GroupDocs.Redaction 설정

먼저, 라이브러리를 프로젝트에 추가합니다.

**.NET CLI 사용:**  
```bash
dotnet add package GroupDocs.Redaction
```

**패키지 관리자 사용:**  
```bash
Install-Package GroupDocs.Redaction
```

또는 NuGet 패키지 관리자 UI에서 “GroupDocs.Redaction”을 찾아 최신 버전을 설치합니다.

### 라이선스 획득

무료 체험으로 시작하거나 임시 라이선스를 요청할 수 있습니다. 장기 프로젝트의 경우 공식 사이트에서 라이선스를 구매하십시오.

### 기본 초기화

패키지를 설치한 후, 문서에 대한 참조를 보관할 인덱스를 생성합니다:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## 구현 가이드

### 기능 1: 텍스트 문서(.txt) 필터 설정

#### 텍스트 문서에 대한 파일 확장자별 필터링 방법

1. **인덱스 및 문서 폴더 정의**  
   소스 파일이 위치한 경로를 설정합니다:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **인덱스 생성**  
   소스 폴더의 모든 파일을 인덱스로 로드합니다:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **파일 확장자 필터가 포함된 검색 옵션 구성**  
   엔진에 *.txt 파일만 고려하도록 지시합니다:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **검색 수행**  
   쿼리를 실행합니다; 필터가 비텍스트 파일을 무시하도록 보장합니다:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *설명*: `Search` 메서드는 필터를 만족하는 일치 항목을 반환하여 잡음을 크게 줄이고 성능을 향상시킵니다.

### 기능 2: 파일 경로 필터

#### 파일 경로 필터를 사용하는 이유는?

때때로 특정 부서 폴더나 동일한 명명 규칙을 공유하는 파일 집합으로 검색을 제한해야 할 때가 있습니다. 경로 필터를 사용하면 정확히 그렇게 할 수 있습니다.

1. **인덱스 및 문서 폴더 정의**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **인덱스 생성**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **경로 기반 정규식으로 검색 옵션 구성**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   이 정규식은 전체 경로에 “Lorem”이라는 단어가 포함된 모든 파일과 일치하여 특정 하위 폴더를 대상으로 할 수 있게 합니다.

4. **경로 기반 검색 실행**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## 실용적인 적용 사례
- **법률 문서 관리** – 일반 텍스트 파일로 저장된 관련 계약서를 빠르게 찾습니다.  
- **학술 연구** – 특정 프로젝트 폴더에 속한 *.txt 연구 노트만 가져옵니다.  
- **기업 보고** – 부서 경로(예: `/Finance/2025/`)별로 내부 보고서를 필터링합니다.

## 성능 고려 사항
- 실제로 필요한 문서 유형만 인덱싱하십시오; 불필요한 파일은 인덱스 크기와 검색 시간을 증가시킵니다.  
- 새로운 파일이나 변경된 파일에 대해 `index.Add()`를 호출하는 예약 작업으로 인덱스를 최신 상태로 유지하십시오.  
- 간단한 정규식을 사용하십시오; 과도하게 복잡한 패턴은 검색 엔진을 느리게 할 수 있습니다.  
- 더 이상 필요하지 않을 때 `Index` 객체를 해제하여 메모리를 확보하십시오.

## 결론
이제 GroupDocs.Redaction for .NET을 사용하여 **파일 확장자별 필터링** 및 **파일 경로 필터** 적용 방법을 알게 되었습니다. 이러한 기술은 대규모 문서 컬렉션에 대해 세밀한 제어를 제공하여 검색을 더 빠르고 관련성 있게 만듭니다. 다음으로 여러 필터를 결합하거나 검색을 더 큰 애플리케이션 워크플로에 통합해 보세요.

## FAQ 섹션

**Q1: 텍스트 파일 외의 문서도 필터링할 수 있나요?**  
A1: 예, GroupDocs.Redaction은 다양한 형식을 지원합니다. `CreateFileExtension`의 인수를 원하는 확장자(예: ".pdf")로 변경하십시오.

**Q2: 검색 인덱스를 정기적으로 어떻게 업데이트하나요?**  
A2: 백그라운드 서비스나 cron 작업을 예약하여 최신 상태를 유지하려는 디렉터리에서 `index.Add()`를 실행하십시오.

**Q3: 파일 경로 필터링 시 성능에 영향을 미치나요?**  
A3: 적절히 최적화된 정규식은 최소한의 영향을 미치지만, 항상 자체 데이터 세트로 벤치마크하십시오.

**Q4: 더 정교한 검색을 위해 여러 필터를 결합할 수 있나요?**  
A4: 물론입니다. 필터를 체인하거나 복합 필터를 만들어 파일 유형과 경로를 동시에 대상으로 할 수 있습니다.

**Q5: GroupDocs.Redaction에 대한 추가 자료는 어디서 찾을 수 있나요?**  
A5: 자세한 가이드와 API 참조는 공식 문서인 [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)를 방문하십시오.

## 자주 묻는 질문

**Q: `SearchDocumentFilter`가 암호화된 파일에서도 작동하나요?**  
A: 필터는 파일 메타데이터에 작동하므로 인덱싱 중에 필요한 복호화 자격 증명을 제공하면 암호화된 파일도 인덱싱됩니다.

**Q: 경로 필터링에 정규식 대신 와일드카드를 사용할 수 있나요?**  
A: 현재 API는 정규식을 요구하지만, 간단한 와일드카드(`.*` 등)를 시뮬레이션할 수 있습니다.

**Q: 샤딩을 고려하기 전에 인덱스 크기는 얼마나 커질 수 있나요?**  
A: 수백 기가바이트 규모의 인덱스는 여러 논리적 인덱스로 분할하는 것이 유리할 수 있으니, 컬렉션이 성장함에 따라 성능을 테스트하십시오.

**Q: 인덱스에서 문서를 제거하는 내장 메서드가 있나요?**  
A: 예—`index.Delete(documentId)` 또는 `index.DeleteAll()`을 호출하여 오래된 항목을 관리할 수 있습니다.

**Q: 전체 문서를 로드하기 전에 검색 결과를 미리 볼 수 있나요?**  
A: `SearchResult` 객체에는 스니펫 정보가 포함되어 있어 전체 파일을 열지 않고 UI에 표시할 수 있습니다.

## 리소스
- **문서**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **다운로드**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **무료 지원**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **임시 라이선스**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**마지막 업데이트:** 2026-04-02  
**테스트 환경:** GroupDocs.Redaction 23.12 for .NET  
**작성자:** GroupDocs
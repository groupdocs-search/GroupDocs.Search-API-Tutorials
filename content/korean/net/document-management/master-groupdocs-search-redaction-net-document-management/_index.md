---
date: '2026-07-16'
description: GroupDocs Search와 Redaction을 사용해 .NET에서 문서를 레드랙하고, 검색 결과를 강조 표시하여 문서
  관리를 보다 빠르게 하는 방법을 배웁니다.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: GroupDocs Search와 Redaction을 사용해 .NET에서 문서를 레드랙하고, 검색 결과를 강조 표시하여
  문서 관리를 보다 빠르게 하는 방법을 배웁니다.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: .NET에서 GroupDocs Search를 사용해 문서를 레드랙하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: .NET에서 GroupDocs Search를 사용해 문서를 레드랙하는 방법
type: docs
url: /ko/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# GroupDocs Search를 사용한 .NET 문서 가리기 방법

현대 기업에서는 **문서를 가리는 방법**을 빠르고 안전하게 처리하는 것이 일상적인 과제입니다. GroupDocs.Search와 GroupDocs.Redaction for .NET을 함께 사용하면 민감한 콘텐츠를 가릴 뿐만 아니라 퍼지 검색을 수행하고 HTML에서 **검색 결과를 강조**할 수 있는 강력한 즉시 사용 가능한 솔루션을 제공합니다. 이 튜토리얼에서는 라이브러리 설치, 인덱스 생성, 퍼지 쿼리 실행, 강조된 출력 생성 과정을 명확하고 프로덕션 수준의 코드 스니펫과 함께 안내합니다.

## 빠른 답변
- **첫 번째 단계는 무엇인가요?** GroupDocs.Search와 GroupDocs.Redaction NuGet 패키지를 설치합니다.  
- **PDF와 Word 파일을 가릴 수 있나요?** 예, 두 형식 모두 기본적으로 지원됩니다.  
- **퍼지 검색을 사용할 수 있나요?** 물론입니다 – 정확도를 0 %에서 100 %까지 조정할 수 있습니다.  
- **개발에 라이선스가 필요합니까?** 테스트용으로는 무료 체험 라이선스가 작동하며, 프로덕션에는 유료 라이선스가 필요합니다.  
- **솔루션이 .NET 6에서 작동합니까?** 예, 라이브러리는 .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+와 호환됩니다.

## GroupDocs.Search란?
GroupDocs.Search는 100개가 넘는 파일 형식에 대해 빠른 인덱싱 및 전체 텍스트 검색을 제공하는 .NET 라이브러리입니다. 전체 파일을 메모리에 로드하지 않고도 최대 2 GB 크기의 문서를 처리할 수 있어 대규모 저장소에 적합합니다. 증분 인덱싱, 다국어 분석을 지원하며 .NET 애플리케이션과 원활하게 통합되어 최소한의 코드로 강력한 검색 경험을 구축할 수 있습니다.

## 문서 가리기에 GroupDocs.Redaction을 사용하는 이유
GroupDocs.Redaction은 30개 이상의 내장 가리기 패턴을 제공하고 배치 처리를 지원하여 개인 데이터, 기밀 조항 또는 규제 표시를 영구적으로 제거합니다. 벤치마크 테스트에서 500페이지 PDF를 가리는 데 표준 서버에서 2 초 미만이 소요됩니다. 엔진은 문서의 콘텐츠 스트림에서 작동하므로 가린 영역을 복구할 수 없으며 원본 형식과 레이아웃을 유지합니다.

## 전제 조건
- **필수 라이브러리:** GroupDocs.Search, GroupDocs.Redaction  
- **지원 플랫폼:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 이상 (모든 에디션)  
- **기본 기술:** C#, 파일 I/O 및 OOP 개념에 익숙함  

## .NET 프로젝트에서 GroupDocs.Search와 GroupDocs.Redaction을 설정하는 방법
.NET CLI, Package Manager Console 또는 UI를 통해 NuGet 패키지를 설치하고 라이선스 파일을 프로젝트에 추가합니다. 이 두 단계 설정만으로 인덱싱이나 가리기 코드를 작성하기 전에 준비가 완료됩니다. 패키지를 추가한 후 라이선스 파일을 애플리케이션 루트에 배치하고 코드 파일에서 네임스페이스를 참조해야 합니다.

## .NET용 GroupDocs.Redaction 설정
GroupDocs.Search와 GroupDocs.Redaction을 .NET 애플리케이션에서 사용하려면 다음 설치 단계를 따르세요:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
"GroupDocs.Redaction"을 검색하고 최신 버전을 설치합니다.

### 라이선스 획득 단계
1. **무료 체험**: [GroupDocs](https://www.groupdocs.com) 에서 가입하여 임시 라이선스를 얻으세요.  
2. **구매**: 전체 접근을 위해 GroupDocs 웹사이트에서 라이선스를 구매하세요.  
3. **임시 라이선스**: 제공된 링크를 통해 평가용으로 얻으세요.

#### 기본 초기화 및 설정
`Index` 클래스는 디스크에 저장되는 검색 가능한 인덱스를 나타내며 문서 추가, 업데이트 및 쿼리를 위한 메서드를 제공합니다. 설치 후 필요한 구성으로 프로젝트를 초기화합니다:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## 구현 가이드

### 문서 생성 및 인덱싱
**Overview**  
이 기능은 여러 파일이 포함된 폴더에 대한 인덱스를 생성하여 문서를 효율적으로 구성하는 방법을 보여줍니다.

#### 단계 1: 경로 정의  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### 퍼지 검색 설정 및 실행
**Overview**  
퍼지 검색은 검색어에 약간의 차이가 있더라도 문서를 찾을 수 있게 해줍니다. 이 기능은 정확도를 조정할 수 있는 퍼지 검색 설정을 보여줍니다.

#### 단계 1: 퍼지 검색 활성화  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### HTML 형식으로 검색 결과 강조
**Overview**  
검색 결과를 시각적으로 강조하면 파일 내 관련 섹션을 빠르게 분석할 수 있습니다.

#### 단계 1: 고압축 설정  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### 단계 2: 강조 및 출력  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### 문제 해결 팁
- 경로가 올바르게 지정되어 파일을 찾을 수 없음 오류를 방지하십시오.  
- 디렉터리 읽기/쓰기 작업에 필요한 모든 권한이 설정되어 있는지 확인하십시오.  

## 실용적인 적용 사례
1. **법률 문서 검토** – 방대한 법률 자료에서 사건 관련 용어를 빠르게 찾습니다.  
2. **학술 연구** – 수천 개 논문에서 특정 방법론을 검색합니다.  
3. **비즈니스 인텔리전스** – 분기 보고서에서 주요 지표를 수동 탐색 없이 추출합니다.  
4. **고객 지원** – 지원 티켓에서 반복되는 문제를 스캔하고 분석 전에 개인 데이터를 가립니다.  
5. **콘텐츠 관리 시스템(CMS)** – 퍼지 검색과 민감한 스니펫 자동 가리기를 통해 콘텐츠 검색을 강화합니다.  

## 성능 고려 사항
- 인덱스 저장 설정을 최적화하여 속도와 디스크 사용량의 균형을 맞추세요.  
- 데이터를 최신 상태로 유지하기 위해 인덱스를 정기적으로 업데이트하여 불필요한 처리를 줄이세요.  
- 특히 대량 배치를 처리할 때 사용되지 않는 객체를 즉시 해제하여 메모리 누수를 방지하세요.  

## GroupDocs Redaction을 사용하여 PDF에서 민감한 정보를 가리는 방법?
`Redactor`는 지원되는 문서 형식에 가리기 패턴을 적용하는 주요 클래스입니다. `Redactor redactor = new Redactor("file.pdf")` 로 대상 PDF를 로드하고, `redactor.AddRedaction(new RedactionPhrase("confidential"))` 와 같이 가리기 패턴을 정의한 뒤 `redactor.Apply()` 를 호출하면 라이브러리가 레이아웃을 유지하면서 원본 파일을 가린 콘텐츠로 덮어씁니다. 이 한 단계 워크플로우는 보호된 구절이 완전히 사라지도록 보장합니다.

## 퍼지 쿼리 후 HTML에서 검색 결과를 강조하는 방법?
`SearchResultHighlighter`는 검색 매치에서 강조된 HTML 스니펫을 생성하는 유틸리티를 제공합니다. 퍼지 쿼리를 실행하고 매칭된 조각을 가져온 뒤 `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")` 에 전달합니다. 이 메서드는 각 발생을 지정된 태그로 감싸서 모든 관련 용어가 시각적으로 강조된 HTML 스니펫을 생성합니다. 강조된 HTML은 웹 페이지에 직접 삽입하거나 보고서로 저장할 수 있어 최종 사용자가 각 매치의 컨텍스트를 쉽게 확인할 수 있습니다.

## 자주 묻는 질문

**Q: 퍼지 검색이란?**  
A: 퍼지 검색은 근사 일치를 찾아내며, 철자 오류나 약간의 변형이 있는 경우에도 결과를 반환합니다.

**Q: 이러한 라이브러리를 상업 프로젝트에 사용할 수 있나요?**  
A: 예, 유효한 GroupDocs 라이선스가 있으면 상업적 사용 권한이 부여됩니다.

**Q: 대용량 문서 세트를 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: 증분 인덱싱을 사용하고 `IndexingOptions` 로 배치 크기를 조정하며 정기적인 인덱스 재구축을 스케줄링하여 성능을 최적화합니다.

**Q: GroupDocs.Search에서 지원하는 파일 형식은 무엇인가요?**  
A: PDF, DOCX, XLSX, PPTX, HTML, TXT 및 JPEG, PNG와 같은 이미지 형식을 포함해 100개가 넘는 형식을 지원합니다.

**Q: 검색 및 가리기에 다국어 지원이 있나요?**  
A: 예, 라이브러리에는 30개 이상의 언어에 대한 분석기가 포함되어 있어 전 세계 콘텐츠에 대해 정확한 검색 및 가리기를 수행할 수 있습니다.

## 리소스
- [문서](https://docs.groupdocs.com/search/net/)  
- [문서](https://docs.groupdocs.com/search/net/)  
- [지원 포럼](https://forum.groupdocs.com/c/search/10)  
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)  
- [다운로드](https://www.groupdocs.com/products/search-net)

---

**마지막 업데이트:** 2026-07-16  
**테스트 환경:** GroupDocs.Search 2.0.0 및 GroupDocs.Redaction 2.0.0 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Search와 Redaction을 사용한 .NET 문서에서 검색 결과 강조](/search/net/highlighting/highlight-search-results-net-groupdocs/)  
- [.NET에서 GroupDocs Redaction 및 Search 마스터하기: 효율적인 문서 관리와 안전한 검색](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)  
- [GroupDocs.Redaction .NET으로 문서 가리기 마스터: 인덱싱 및 별칭 관리로 안전한 문서 관리](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)
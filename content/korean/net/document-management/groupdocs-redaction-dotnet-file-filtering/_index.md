---
date: '2026-04-21'
description: GroupDocs.Redaction for .NET를 사용하여 파일을 필터링하는 방법을 배우세요. 여기에는 생성 날짜, 파일
  크기, 수정 날짜별 필터링 및 NOT 필터 적용 방법이 포함됩니다.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: .NET용 GroupDocs.Redaction으로 파일 필터링하는 방법
type: docs
url: /ko/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# GroupDocs.Redaction for .NET으로 파일 필터링하는 방법

오늘날 빠르게 변화하는 디지털 환경에서 **파일을 필터링하는 방법**은 생산성을 좌우할 수 있습니다. 확장자, 생성 날짜, 크기 또는 수정 날짜별로 문서를 분리해야 할 때, 견고한 필터링 전략은 시간을 절약하고 저장 비용을 줄이며 검색 인덱스를 깔끔하게 유지합니다. 이 튜토리얼에서는 GroupDocs.Redaction for .NET을 사용한 실제 예제를 통해 파일을 어떻게 필터링하여 일반적인 비즈니스 요구를 충족시키는지 단계별로 안내합니다.

## 빠른 답변
- **필요한 라이브러리는?** GroupDocs.Redaction for .NET (NuGet을 통해 설치).  
- **생성 날짜로 필터링할 수 있나요?** 예 – `CreateCreationTimeRange` 사용.  
- **특정 유형을 제외하려면 어떻게 하나요?** `DocumentFilter.CreateNot`으로 NOT 필터 적용.  
- **파일 크기 필터링이 지원되나요?** 물론이며, `CreateFileLengthRange` 또는 상/하한을 사용합니다.  
- **라이선스가 필요합니까?** 프로덕션 사용을 위해 체험판 또는 정식 라이선스가 필요합니다.

## GroupDocs.Redaction에서 파일 필터링이란?
파일 필터링은 확장자, 날짜, 경로 패턴 또는 크기와 같은 메타데이터를 기반으로 인덱싱 엔진에 포함하거나 무시할 문서를 지정할 수 있게 합니다. 정확한 `DocumentFilter` 규칙을 정의함으로써 인덱스를 가볍게 유지하고 검색 속도를 빠르게 할 수 있습니다.

## 왜 GroupDocs.Redaction for .NET을 사용하나요?
- **내장 필터 헬퍼** – 사용자 정의 파일 시스템 코드를 작성할 필요가 없습니다.  
- **논리 연산자** – AND, OR, NOT으로 여러 조건을 결합합니다.  
- **성능 최적화** – 필터는 인덱싱 중에 적용되며, 이후가 아닙니다.  
- **크로스 플랫폼** – .NET Framework, .NET Core, .NET 5/6+에서 작동합니다.

## 사전 요구 사항
- .NET Framework 4.6 이상 또는 .NET Core 3.1 이상이 설치되어 있어야 합니다.  
- Visual Studio 또는 선호하는 C# IDE.  
- 기본 C# 지식.  

### 필수 라이브러리 및 설정
Install the NuGet package using your preferred method:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **팁:** 설치 후 라이선스 파일을 프로젝트 루트에 추가하고, Redactor 또는 Index 객체를 만들기 전에 `License.SetLicense("license-file-path")`를 호출하십시오.

## GroupDocs.Redaction for .NET 설정

First, create a `Redactor` instance that points to the document you want to work with:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **왜 중요한가:** Redactor를 초기화하면 라이브러리가 워크플로우 후반에 필터와 가리기 규칙을 적용할 준비가 됩니다.

## 확장자로 파일 필터링하는 방법

파일 확장자로 필터링하는 것은 문서 집합을 좁히는 가장 일반적인 방법입니다. 아래 예제에서는 FB2, EPUB, TXT 파일만 유지합니다.

### 파일 확장자로 필터링

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 원하지 않는 유형을 제외하기 위해 NOT 필터 적용하기

NOT 필터 로직을 적용해야 할 경우—예를 들어 HTML 및 PDF 파일을 제외하려면—`CreateNot`을 사용합니다.

### HTM, HTML 및 PDF 파일 제외

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 생성 날짜로 파일 필터링하는 방법

생성 날짜로 필터링해야 할 경우, 시작 및 종료 `DateTime`을 지정합니다.

### 생성 날짜 범위로 필터링

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 수정 날짜로 파일 필터링하는 방법

생성 날짜와 유사하게, 특정 시점 이전에 수정된 파일로 결과를 제한할 수 있습니다.

### 수정 날짜로 필터링

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 정규식을 사용해 경로로 파일 필터링하는 방법

폴더 구조가 명명 규칙을 따르는 경우, 정규식을 사용해 특정 경로를 대상으로 할 수 있습니다.

### 파일 경로 패턴으로 필터링

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 파일 크기로 필터링하는 방법

대역폭이나 저장 용량 제한을 다룰 때 문서 크기 제어는 필수적입니다.

### 파일 크기로 필터링 (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## AND로 여러 조건 결합하기

여러 기준을 한 번에 사용해 파일을 **필터링하는 방법**이 필요할 때는 `CreateAnd`로 결합합니다.

### 논리 AND 예시

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## OR로 여러 조건 결합하기

여러 규칙 중 하나라도 통과하면 될 때는 `CreateOr`를 사용합니다.

### 논리 OR 예시

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## 일반적인 문제 및 해결책
- **필터가 적용되지 않음:** `Index` 인스턴스를 만들기 **앞에** `settings.DocumentFilter`를 할당했는지 확인하십시오.  
- **예상치 못한 파일이 나타남:** 파일 확장자에 앞점(`.txt`)이 포함되어 있는지 다시 확인하십시오.  
- **성능 저하:** AND로 필터를 결합해 인덱싱 파이프라인 초기에 스캔되는 파일 수를 줄이세요.  
- **정규식 오류:** 경로 패턴의 특수 문자를 이스케이프하거나 대소문자 구분 없이 매치하려면 `RegexOptions.IgnoreCase`를 사용하십시오.

## 자주 묻는 질문

**Q: NOT 필터를 AND 필터와 결합할 수 있나요?**  
A: 예. 먼저 NOT 필터를 만들고 (`DocumentFilter.CreateNot`) 이를 `DocumentFilter.CreateAnd`의 인수 중 하나로 포함합니다.

**Q: 10 MB보다 큰 파일을 어떻게 필터링하나요?**  
A: `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)`를 사용해 해당 크기 초과 파일만 포함합니다.

**Q: 생성 날짜와 수정 날짜를 동시에 필터링할 수 있나요?**  
A: 물론입니다. 각각의 필터를 별도로 만든 뒤 `CreateAnd`로 결합합니다.

**Q: 이러한 필터가 클라우드 스토리지 경로에서도 작동하나요?**  
A: 필터는 로컬 파일 시스템에서 작동합니다. 클라우드 소스의 경우 파일을 임시 폴더에 다운로드한 뒤 동일한 필터를 적용하십시오.

**Q: 필터를 변경하면 재인덱싱이 필요합니까?**  
A: 예. 필터는 `index.Add`를 호출할 때 평가됩니다. 필터를 변경하면 새로운 기준을 반영하기 위해 인덱스를 다시 구축해야 합니다.

## 결론

GroupDocs.Redaction for .NET을 사용해 **파일을 필터링하는 방법**을 마스터하면—확장자, 생성 날짜, 수정 날짜, 파일 크기 또는 NOT 로직을 사용하든—문서 관리를 효율화하고 인덱스 성능을 유지하며 실제로 중요한 콘텐츠에 집중할 수 있습니다. 논리 연산자를 실험해 비즈니스 규칙에 맞게 필터링을 맞춤 설정하면 속도와 저장 효율성에서 즉각적인 향상을 경험하게 될 것입니다.

---

**마지막 업데이트:** 2026-04-21  
**테스트 환경:** GroupDocs.Redaction 24.11 for .NET  
**작성자:** GroupDocs  

---
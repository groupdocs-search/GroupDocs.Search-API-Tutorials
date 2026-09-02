---
date: '2026-04-04'
description: GroupDocs.Search를 사용하여 법률 문서를 검색하고 인덱스를 관리하는 방법을 배우고, .NET에서 GroupDocs.Redaction을
  활용해 의료 기록에 레드액션을 통합하세요.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: GroupDocs Search & Redaction for .NET를 사용하여 법률 문서 검색
type: docs
url: /ko/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# GroupDocs Search 및 Redaction을 사용한 .NET에서 법률 문서 검색

오늘날 데이터‑중심 환경에서 **법률 문서 검색**을 빠르고 안전하게 수행하는 것은 모든 조직에 필수적인 요구 사항입니다. 계약서, 법원 제출 서류 또는 컴플라이언스 보고서를 다루든, GroupDocs.Search는 빠르고 확장 가능한 인덱스를 제공하고, GroupDocs.Redaction은 민감한 정보를 숨깁니다. 이 튜토리얼에서는 검색 가능한 인덱스를 설정하고, 여러 폴더에서 문서를 추가하며, 레드랙션을 구성하여 의료 기록 및 기타 기밀 파일을 안전하게 검색하는 방법을 안내합니다.

## 빠른 답변
- **GroupDocs.Search는 무엇을 하나요?** 다양한 문서 형식에 대한 전체 텍스트 검색 가능한 인덱스를 생성합니다.  
- **검색 전에 정보를 레드랙션할 수 있나요?** 예 – GroupDocs.Redaction을 사용하여 민감한 데이터를 가리거나 제거합니다.  
- **인덱스에 문서를 어떻게 추가하나요?** 포함하려는 각 폴더에 대해 `index.Add("folderPath")`를 호출합니다.  
- **지원되는 파일 유형은 무엇인가요?** PDF, DOCX, PPTX, TXT 등 다양한 형식.  
- **프로덕션에 라이선스가 필요합니까?** 임시 체험판을 사용할 수 있으며, 상업적 사용을 위해서는 영구 라이선스가 필요합니다.

## 전제 조건
이 튜토리얼을 따라하려면 다음이 필요합니다:
- .NET Core SDK (3.1 이상) 설치
- Visual Studio Code, Visual Studio 또는 .NET을 지원하는 다른 IDE
- C# 프로그래밍에 대한 기본 지식

### 라이선스 획득
두 라이브러리 모두 무료 체험판으로 시작할 수 있습니다. 장기 사용을 위해서는 임시 라이선스를 획득하거나 [GroupDocs 웹사이트](https://purchase.groupdocs.com/temporary-license/)에서 구매하는 것을 고려하십시오.

## 필요한 패키지 설치

**GroupDocs.Search 설치:**  
**.NET CLI**를 사용하여 실행합니다:
```bash
dotnet add package GroupDocs.Search
```
또는 Visual Studio의 패키지 관리자 콘솔을 사용합니다:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction 설치:**  
- .NET CLI 사용:
```bash
dotnet add package GroupDocs.Redaction
```
- 또는 패키지 관리자를 통해:
```powershell
Install-Package GroupDocs.Redaction
```

GUI를 선호한다면 NuGet 패키지 관리자 UI를 열어 "GroupDocs.Redaction"을 검색하여 설치하십시오.

## 레드랙터 설정 구성
레드랙션을 시작하기 전에 레드랙터 동작을 조정하고 싶을 수 있습니다(예: 레드랙션 색상 설정 또는 사용자 정의 패턴 정의). 다음 코드 조각은 기본 초기화를 보여줍니다:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **전문가 팁:** 조직의 컴플라이언스 정책에 맞게 `redactorSettings`를 조정하십시오(예: 텍스트를 검은 상자로 교체, 레드랙션 전에 OCR 적용 등).

## 구현 가이드

### 법률 문서를 검색하는 방법은?
검색 가능한 인덱스를 만드는 것은 법률 문서를 빠르게 검색하기 위한 기반입니다. GroupDocs.Search를 사용하면 任意의 폴더를 지정하고 인덱스를 구축한 뒤 수천 개의 파일에 대해 복잡한 쿼리를 실행할 수 있습니다.

### 인덱스에 문서를 추가하는 방법
문서 추가는 간단합니다—라이브러리를 파일이 저장된 디렉터리로 지정하면 됩니다. 여러 폴더를 추가할 수 있어 법률 문서가 서로 다른 위치에 분산되어 있을 때 유용합니다.

#### 인덱스 생성 및 관리
**개요:**  
인덱스를 생성하는 것은 효율적인 문서 검색 작업을 위한 첫 번째 단계입니다. GroupDocs.Search를 사용하면 원하는 디렉터리에 검색 가능한 인덱스를 만들 수 있어 문서를 빠르게 검색할 수 있습니다.

##### 단계 1: 인덱스 생성
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*설명:* `Index`는 지정된 디렉터리에 검색 인덱스를 초기화합니다. 경로가 프로젝트 폴더 구조를 반영하는지 확인하십시오.

##### 단계 2: 인덱스에 문서 추가
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*설명:* `Add` 메서드는 지정된 폴더를 스캔하고 지원되는 모든 문서를 인덱스에 포함합니다. 이를 사용하여 계약서, 사건 파일, 의료 기록 등 여러 소스에서 **인덱스에 문서 추가**를 수행하십시오.

### 인덱싱 보고서 검색 및 표시
**개요:**  
인덱싱 보고서는 처리된 문서 수, 전체 용어 수, 저장 용량 등 성능 튜닝에 필요한 핵심 지표를 제공합니다.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*설명:* `GetIndexingReports`는 인덱싱 과정을 상세히 나타내는 보고서 배열을 반환하여 성능을 모니터링하고 최적화하는 데 도움을 줍니다.

## 실용적인 적용 사례
1. **법률 문서 관리:** 사건 파일을 자동으로 인덱싱하여 법령, 브리프, 판결을 즉시 검색할 수 있습니다.  
2. **의료 기록 시스템:** GroupDocs.Redaction을 사용해 PHI를 가려 개인정보를 보호하면서 환자 기록을 검색합니다.  
3. **기업 HR 포털:** 검색 가능한 직원 파일에 레드랙션을 적용해 개인 데이터를 보호합니다.

## 성능 고려 사항
- **인덱스 크기 최적화:** 주기적으로 오래된 항목을 정리하고 인덱스를 재구축하여 경량화합니다.  
- **메모리 관리:** .NET의 가비지 컬렉터를 활용하고, 더 이상 필요하지 않은 `Index` 객체는 해제합니다.  
- **확장성 모범 사례:** 인덱스를 빠른 SSD에 저장하고 대규모 코퍼스를 여러 인덱스로 샤딩하는 것을 고려하십시오.

## 자주 묻는 질문

**Q: GroupDocs.Search의 주요 사용 사례는 무엇인가요?**  
A: 대용량 문서 컬렉션에서 검색 가능한 인덱스를 생성하여 법률 및 의료 파일을 빠르게 검색할 수 있습니다.

**Q: GroupDocs.Redaction은 어떻게 데이터 프라이버시를 보장하나요?**  
A: 문서가 인덱싱되거나 공유되기 전에 민감한 정보를 영구적으로 제거하거나 가리는 레드랙션 패턴을 정의할 수 있습니다.

**Q: 이러한 라이브러리를 클라우드 환경에서 사용할 수 있나요?**  
A: 예—두 라이브러리 모두 적절한 라이선스가 있으면 Azure, AWS 또는 컨테이너화된 .NET 배포 환경에서 작동합니다.

**Q: GroupDocs.Search가 지원하는 파일 형식은 무엇인가요?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML 등 다양한 엔터프라이즈 형식.

**Q: 인덱싱 오류를 어떻게 해결하나요?**  
A: 폴더 경로를 확인하고 파일 권한을 점검하며 `IndexingReport`의 콘솔 출력을 검토하여 특정 오류 코드를 확인하십시오.

## 리소스
- **문서:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API 레퍼런스:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **다운로드:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **무료 지원:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **임시 라이선스:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**마지막 업데이트:** 2026-04-04  
**테스트 환경:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**작성자:** GroupDocs
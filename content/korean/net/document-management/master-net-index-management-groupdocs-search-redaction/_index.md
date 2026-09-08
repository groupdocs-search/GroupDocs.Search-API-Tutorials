---
date: '2026-07-26'
description: .NET에서 GroupDocs.Search를 사용하여 index를 생성하고 GroupDocs.Redaction와 연동하여 fast
  document search 및 data handling을 가능하게 하는 방법을 배웁니다.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: .NET에서 GroupDocs.Search를 사용하여 index를 생성하고 GroupDocs.Redaction와 연동하여
  fast document search 및 data handling을 가능하게 하는 방법을 배웁니다.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: .NET에서 GroupDocs Search API로 index 생성 방법
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: .NET에서 GroupDocs Search API로 index 생성 방법
type: docs
url: /ko/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# .NET에서 GroupDocs Search API를 사용하여 인덱스 생성 방법

이 튜토리얼에서는 GroupDocs.Search를 사용하여 .NET 애플리케이션용 **인덱스를 생성하는 방법**을 배우고, 이후 GroupDocs.Redaction으로 민감한 콘텐츠를 보호하는 방법을 알아봅니다. 가이드를 마치면 검색 가능한 인덱스를 구축, 업데이트 및 정리할 수 있으며, 검색과 Redaction을 결합하는 것이 안전한 문서 관리에 최선의 방법임을 이해하게 됩니다.

## 빠른 답변
- **“인덱스 생성 방법”이 의미하는 바는?** 문서 내용을 빠른 조회 키에 매핑하는 검색 가능한 데이터 구조를 구축하는 것을 의미합니다.  
- **필요한 라이브러리는?** .NET용 GroupDocs.Search 및 GroupDocs.Redaction (NuGet 패키지).  
- **PDF, Word, 이미지 등을 인덱싱할 수 있나요?** 예—150개 이상의 형식을 기본적으로 지원합니다.  
- **인덱스에서 문서를 삭제하려면 어떻게 하나요?** 문서 경로나 ID와 함께 `Delete` 메서드를 호출합니다.  
- **Redaction은 인덱싱 전인가 후인가?** Redaction은 먼저 수행되어야 하며, 보호된 데이터가 인덱스에 들어가지 않도록 합니다.

## “인덱스 생성 방법”이란?
**how to create index**라는 문구는 빠른 검색을 위해 용어‑문서 매핑을 저장하는 검색 가능한 데이터 구조를 생성하는 과정을 의미합니다. GroupDocs에서는 이 구조가 디스크에 저장되며 전체 컬렉션을 재구성하지 않고도 점진적으로 업데이트할 수 있습니다.

## GroupDocs.Search와 GroupDocs.Redaction을 함께 사용하는 이유는?
GroupDocs.Search는 **150개 이상의 파일 형식**을 인덱싱하고 **10 GB** 이상의 인덱스도 메모리 사용량을 200 MB 이하로 유지하면서 처리할 수 있습니다. 이는 파일을 전체 로드하지 않고 스트리밍하기 때문입니다. GroupDocs.Redaction을 추가하면 기밀 텍스트, 이미지 또는 메타데이터가 콘텐츠가 인덱스에 도달하기 전에 제거되어 GDPR, HIPAA 등 규정을 준수할 수 있습니다.

## 사전 요구 사항

- **라이브러리 및 버전** – .NET 6 이상과 호환되는 최신 **GroupDocs.Search** 및 **GroupDocs.Redaction** NuGet 패키지를 설치합니다.  
- **IDE** – Visual Studio 2022(또는 .NET 6을 지원하는 IDE).  
- **지식** – 기본 C# 기술, 파일 I/O에 대한 친숙함, 인덱싱 개념에 대한 이해.

## .NET용 GroupDocs.Redaction 설정

### 설치

**.NET CLI 사용:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Visual Studio의 패키지 관리자 콘솔 사용:**  
```powershell
Install-Package GroupDocs.Redaction
```  

또한 NuGet 패키지 관리자 UI에서 “GroupDocs.Redaction”을 찾아 최신 안정 버전을 설치할 수 있습니다.

### 라이선스 획득

제한 없이 모든 기능을 탐색하려면 무료 체험을 받거나 임시 라이선스를 요청할 수 있습니다. 라이선스 획득에 대한 자세한 내용은 [GroupDocs 구매 페이지](https://purchase.groupdocs.com/temporary-license/)를 방문하세요.

### 기본 초기화

Redactor는 문서에 대한 Redaction 작업을 수행하는 주요 클래스입니다.  
다음 스니펫은 GroupDocs.Redaction을 시작하는 데 필요한 최소 코드를 보여줍니다:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

이 간단한 설정만으로 GroupDocs.Redaction 사용을 시작할 수 있습니다.

## 구현 가이드

### 인덱스 생성 방법은?

`Index`는 용어 사전과 문서 메타데이터를 보관하는 검색 가능한 컨테이너를 나타냅니다. `Index` 객체를 로드하거나 생성하고, 인덱스 파일이 저장될 폴더를 지정한 뒤 `Create`를 호출합니다. 이 작업은 필요한 메타데이터 파일을 작성하고 엔진을 문서 수집 준비 상태로 만듭니다.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### 단계 1: 인덱스 생성
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### 인덱스에 문서를 추가하는 방법은?

`Add`는 단일 문서를 인덱스에 삽입하고, `AddFolder`는 디렉터리의 모든 파일을 처리합니다. `Add` 또는 `AddFolder`를 호출하여 파일을 추가합니다. 엔진은 지원되는 각 파일을 읽고 텍스트를 추출한 뒤 용어 사전을 업데이트합니다.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### 단계 2: 문서 폴더 추가
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### 인덱싱된 경로를 검색하는 방법은?

`GetIndexedPaths`는 인덱스에 저장된 모든 문서 경로의 컬렉션을 반환합니다. 인덱싱된 파일 경로 목록을 가져오면 현재 검색 가능한 문서를 확인할 수 있습니다.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### 단계 3: 인덱싱된 경로 표시
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### 인덱스에서 문서를 삭제하는 방법은?

`Delete`는 경로나 식별자를 사용해 인덱스에서 문서를 제거합니다. 파일이 삭제되거나 더 이상 필요하지 않을 때 해당 항목을 삭제하여 검색 결과의 정확성을 유지해야 합니다.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### 단계 4: 특정 경로 삭제
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### 삭제 후 남은 인덱싱된 경로를 확인하는 방법은?

삭제 후에는 검색 메서드를 다시 실행하여 인덱스가 현재 상태를 반영하는지 확인할 수 있습니다.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### 단계 5: 남은 경로 확인
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## 실용적인 적용 사례

1. **문서 관리 시스템** – 수백만 파일 중에서 계약서, 청구서 또는 매뉴얼을 빠르게 찾을 수 있습니다.  
2. **법률 문서 검토** – 인덱싱 전에 특권 정보를 Redact하여 우발적인 노출을 방지합니다.  
3. **아카이브 솔루션** – 전체 아카이브를 메모리에 로드하지 않고도 역사적 기록에 대한 검색 가능한 메타데이터를 보존합니다.  
4. **콘텐츠 관리 플랫폼** – 블로그, 지식 베이스 및 멀티미디어 라이브러리 전역 검색을 지원합니다.  
5. **데이터 컴플라이언스 감사** – 정제된 콘텐츠만 검색 가능하도록 하여 규제 요구사항을 충족합니다.

## 성능 고려 사항

- **인덱싱 최적화** – 매일 밤 증분 인덱싱을 예약하고, I/O 급증을 줄이기 위해 배치 크기 100개의 파일로 `AddFolder`를 사용합니다.  
- **리소스 관리** – CPU와 RAM을 모니터링합니다; GroupDocs.Search는 파일을 스트리밍 방식으로 처리하여 10 GB 인덱스에서도 피크 메모리를 200 MB 이하로 유지합니다.  
- **모범 사례** – 서브 초 응답을 위해 SSD에 인덱스를 저장하고, 압축(`index.Compression = true`)을 활성화하여 디스크 사용량을 절반으로 줄입니다.

## 자주 묻는 질문

**Q: GroupDocs로 텍스트가 아닌 파일도 인덱싱할 수 있나요?**  
A: 예, GroupDocs.Search는 PDF, DOCX, PPTX, XLSX 및 이미지 유형을 포함해 150개 이상의 형식을 인덱싱할 수 있으며, 필요한 경우 OCR을 통해 내장 텍스트를 추출합니다.

**Q: 대량의 문서를 어떻게 처리하나요?**  
A: 구성 가능한 배치 크기로 `AddFolder`를 사용하고, 백그라운드 서비스에서 인덱싱을 실행하며, 정기적으로 `Optimize()`를 호출해 작은 인덱스 세그먼트를 병합합니다.

**Q: 인덱싱과 함께 Redaction을 사용하는 이점은 무엇인가요?**  
A: Redaction은 개인 식별 정보를 인덱스에 도달하기 전에 제거하므로 검색 결과가 보호된 데이터를 노출하지 않도록 보장합니다.

**Q: 검색 알고리즘을 맞춤 설정할 수 있나요?**  
A: GroupDocs.Search는 동의어 사전, 사용자 정의 토크나이저 및 정규식 필터를 제공하여 관련성 점수를 세밀하게 조정할 수 있습니다.

**Q: 일반적인 인덱싱 문제를 어떻게 해결하나요?**  
A: 폴더 권한을 확인하고, .NET 런타임이 라이브러리 대상과 일치하는지 확인하며, 인덱스 폴더에 생성된 로그 파일을 확인해 상세 오류 메시지를 검토합니다.

## 리소스

- **문서**: [GroupDocs Redaction .NET 문서](https://docs.groupdocs.com/search/net/)  
- **API 레퍼런스**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **다운로드**: [최신 GroupDocs 릴리스](https://releases.groupdocs.com/search/net/)  
- **무료 지원**: [GroupDocs 포럼](https://forum.groupdocs.com/c/search/10)  
- **임시 라이선스**: [임시 라이선스 요청](https://purchase.groupdocs.com/temporary-license/)  

이러한 리소스를 활용해 GroupDocs.Search와 Redaction을 .NET에 구현하는 방법을 심화하고 구현을 향상시키세요. 즐거운 코딩 되세요!

---

**Last Updated:** 2026-07-26  
**Tested With:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs

## 관련 튜토리얼

- [효율적인 문서 관리를 위한 GroupDocs.Redaction .NET 마스터 인덱스 생성 및 병합](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [고급 문서 검색을 위한 GroupDocs.Redaction .NET 마스터링: 효율적인 인덱스 생성 및 별칭 관리](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [.NET에서 GroupDocs Search와 Redaction 마스터하기: 문서 관리를 위한 포괄적인 가이드](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)
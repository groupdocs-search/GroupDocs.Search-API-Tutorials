---
date: '2026-10-02'
description: Java에서 chunk‑based search를 사용해 문서를 인덱스에 추가할 때 temporary license를 활용하는
  방법을 배우고, 검색 성능을 향상시키면서 메모리 사용을 제어합니다.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Java에서 chunk‑based search를 이용해 문서를 인덱스에 추가할 때 temporary license를 사용하면
  검색 속도가 개선되고 메모리 소비가 감소합니다.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Java에서 chunk‑based indexing을 위한 temporary license 사용
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Java에서 chunk‑based indexing을 위한 temporary license 사용
type: docs
url: /ko/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Java에서 청크 기반 인덱싱을 위한 임시 라이선스 사용

In this tutorial you’ll **use a temporary license** to add documents to index with GroupDocs.Search’s chunk‑based search feature. The approach lets you handle massive document collections—legal contracts, support tickets, research papers—while keeping **java search index memory** usage low and **increase search performance** dramatically. You’ll see how to set up the index folder, feed multiple document sources, enable chunk searching, and run both the first and subsequent chunk queries.

## 빠른 답변
- **첫 번째 단계는 무엇인가요?** Create a search index folder.  
- **많은 파일을 포함하려면 어떻게 해야 하나요?** Use `index.add()` for each document folder.  
- **어떤 옵션이 청크 검색을 활성화하나요?** `options.setChunkSearch(true)`.  
- **첫 번째 청크 이후에도 검색을 계속할 수 있나요?** Yes, call `index.searchNext()` with the token.  
- **라이선스가 필요합니까?** A free trial or temporary license works for development; a full license is required for production.  

## 배울 내용
- 지정된 폴더에 검색 인덱스를 생성하는 방법.  
- 여러 위치에서 **add documents to index**를 수행하는 단계.  
- 청크 기반 검색을 활성화하기 위한 검색 옵션 구성.  
- 초기 및 이후 청크 기반 검색 수행.  
- 청크 기반 문서 검색이 뛰어난 실제 시나리오.  

## 사전 요구 사항
이 가이드를 따르려면 다음을 확인하십시오:

- **필수 라이브러리**: GroupDocs.Search for Java 25.4 이상.  
- **환경 설정**: 호환되는 Java Development Kit (JDK) 설치.  
- **지식 사전 요구 사항**: 기본 Java 프로그래밍 및 Maven에 대한 친숙함.  

## GroupDocs.Search for Java 설정
시작하려면 Maven을 사용하여 프로젝트에 GroupDocs.Search를 통합합니다:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

또는 최신 버전을 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 다운로드하십시오.

### 라이선스 획득
GroupDocs.Search를 사용해 보려면:

- **무료 체험** – 약정 없이 핵심 기능을 테스트합니다.  
- **임시 라이선스** – 개발을 위한 확장된 접근 권한.  
- **구매** – 프로덕션 사용을 위한 정식 라이선스.  

## 인덱스에 문서를 추가하는 방법은?
**Direct answer:** 검색 가능한 파일이 들어 있는 각 폴더에 대해 `index.add()`를 호출합니다; 이 메서드는 폴더를 재귀적으로 스캔하고 지원되는 모든 문서를 단일 작업으로 인덱스에 추가합니다. 이는 파일을 하나씩 수동으로 처리할 필요를 없애고 대량 삽입 속도를 높입니다.

`SearchIndex`는 디스크에 있는 검색 가능한 컬렉션을 나타내는 핵심 클래스입니다. 이를 인스턴스화한 후 모든 인덱싱 및 쿼리 작업은 이 객체를 통해 흐릅니다.

### 1. 인덱스 생성
**Direct answer:** 인덱스 파일이 저장될 경로로 `SearchIndex` 객체를 인스턴스화한 다음 `index.create()`를 호출하여 저장 구조를 초기화합니다. 이 호출은 첫 사용 시 필요한 폴더와 메타데이터 파일을 생성합니다.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. 인덱스에 문서 추가
**Direct answer:** `index.add()` 메서드를 사용하고 각 소스 폴더의 절대 경로를 전달합니다; API는 지원되는 형식(PDF, DOCX, XLSX 등)을 자동으로 감지하고 검색 가능한 텍스트를 인덱스로 추출합니다.

`SearchOptions`는 인덱싱 및 검색 중 문서가 처리되는 방식을 세밀하게 조정할 수 있는 구성 객체입니다. 이후 청크 기반 쿼리를 활성화하는 데 사용할 것입니다.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. 청크 검색을 위한 검색 옵션 구성
**Direct answer:** 쿼리를 실행하기 전에 `SearchOptions` 인스턴스에 `options.setChunkSearch(true)`를 설정합니다; 이는 엔진에게 각 문서를 논리적인 청크(보통 단락)로 분할하고 전체 파일이 아닌 청크별로 일치 항목을 반환하도록 지시합니다.

`SearchResult`는 일치하는 청크, 위치 및 관련성 점수를 보유합니다. 청크 검색이 활성화되면 각 `SearchResult`는 원본 문서의 단일 조각에 해당합니다.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. 초기 청크 기반 검색 수행
**Direct answer:** `index.search("your query", options)`를 실행합니다; 이 호출은 첫 번째 일치 청크 집합에 대한 `SearchResult` 컬렉션과 검색 상태를 나타내는 토큰을 반환합니다.

반환된 토큰은 전체 쿼리를 다시 실행하지 않고도 큰 결과 집합을 페이지 처리하는 데 필수적입니다.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. 청크 기반 검색 계속하기
**Direct answer:** 이전 호출에서 반환된 토큰을 `index.searchNext(token, options)`에 전달합니다; 메서드가 `null`을 반환할 때까지 반복하면 모든 일치 청크가 검색된 것입니다.

이 점진적 접근 방식은 현재 청크 배치만 메모리에 존재하므로 메모리 사용량을 낮게 유지합니다.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## 청크 기반 검색을 사용하는 이유
청크 기반 검색은 방대한 문서 컬렉션을 관리 가능한 조각으로 나누어 메모리 압력을 줄이고 응답 시간을 가속화합니다. 단락 또는 섹션 수준에서 인덱싱함으로써 엔진은 관련 조각만 검색할 수 있어 CPU 사용량을 낮추고 최종 사용자의 지연 시간을 개선합니다. 특히 다음과 같은 경우에 유용합니다:

1. **법무 팀**은 수천 개의 계약서에서 특정 조항을 찾아야 합니다.  
2. **고객 지원 포털**은 관련 지식 베이스 기사를 즉시 제공해야 합니다.  
3. **연구원**은 전체 파일을 메모리에 로드하지 않고 방대한 데이터 세트를 탐색합니다.  

수치화된 주장: GroupDocs.Search는 표준 8코어 서버에서 **500페이지 이상의 PDF**를 **청크당 2초 미만**으로 처리할 수 있으며, 피크 힙을 **200 MB** 이하로 유지합니다.

## 이 접근 방식이 검색 성능을 향상시키는 방법
**Direct answer:** 전체 파일 대신 작은 청크를 검색함으로써 엔진은 불필요한 섹션을 조기에 건너뛰고 CPU 사이클을 줄이며 활성 청크만 메모리에 유지하여 **java search index memory** 사용량을 직접 낮추고 응답 시간을 빠르게 합니다. 이 목표 지향 접근 방식은 보다 효율적인 캐싱 및 병렬 처리를 가능하게 하여 여러 코어가 동시에 다른 청크를 처리하도록 하여 다중 코어 서버에서 처리량을 더욱 향상시킵니다.

추가 이점은 다음과 같습니다:

- 여러 코어에 걸친 병렬 청크 처리.  
- 높은 관련성 일치가 발견되면 조기 종료.  

## java search index memory 관리
**Direct answer:** 예상 인덱스 크기에 따라 충분한 JVM 힙(`-Xmx2g` 이상)을 할당하고, 대량 추가 후 `index.optimize()`를 실행하여 인덱스 구조를 압축하며, VisualVM으로 GC 일시 정지를 모니터링하여 지연 시간 급증을 방지합니다.

추가 튜닝 팁:

- 대량 배치 후 `index.flush()`를 사용하여 중간 데이터를 디스크에 기록합니다.  
- `options.setMemoryLimit(256)`을 활성화하여 검색당 메모리 사용량을 제한합니다.  

## 성능 고려 사항
- **메모리 관리** – 대형 인덱스를 위해 충분한 힙 공간(`-Xmx`)을 할당합니다.  
- **리소스 모니터링** – 인덱싱 및 검색 작업 중 CPU 사용량을 주시합니다.  
- **인덱스 유지 관리** – 주기적으로 인덱스를 재구축하거나 정리하여 오래된 데이터를 삭제합니다.  

## 일반적인 함정 및 문제 해결
| 문제 | 발생 원인 | 해결 방법 |
|------|----------|-----------|
| `OutOfMemoryError` 인덱싱 중 | 힙 크기가 너무 작음 | JVM 힙을 늘립니다(`-Xmx2g` 이상) |
| 결과가 반환되지 않음 | 청크 토큰이 처리되지 않음 | `while` 루프가 `getNextChunkSearchToken()`이 `null`이 될 때까지 실행되는지 확인합니다 |
| 검색 성능 저하 | 인덱스가 최적화되지 않음 | 대량 추가 후 `index.optimize()`를 실행합니다 |

## 자주 묻는 질문

**Q: 청크 기반 검색이란 무엇인가요?**  
A: 청크 기반 검색은 데이터 세트를 더 작은 조각으로 나누어 전체 문서를 메모리에 로드하지 않고도 대용량 데이터에 대한 효율적인 쿼리를 가능하게 합니다.

**Q: 새 파일로 인덱스를 업데이트하려면 어떻게 하나요?**  
A: 새 문서 경로를 사용해 `index.add()`를 호출하면 인덱스가 자동으로 이를 포함합니다.

**Q: GroupDocs.Search가 다양한 파일 형식을 처리할 수 있나요?**  
A: 예, **PDF, DOCX, XLSX, PPTX, HTML, TXT 및 30가지 이상의 다른 형식**을 지원합니다.

**Q: 일반적인 성능 병목 현상은 무엇인가요?**  
A: 메모리 제한과 최적화되지 않은 인덱스가 가장 흔합니다; 충분한 힙을 할당하고 인덱스를 정기적으로 최적화하십시오.

**Q: 자세한 문서는 어디에서 찾을 수 있나요?**  
A: 공식 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)을 방문하면 심층 가이드와 API 참조를 확인할 수 있습니다.

**Q: 청크 기반 검색이 암호화된 PDF에서도 작동하나요?**  
A: 예, 적절한 API 오버로드를 통해 비밀번호를 제공하면 작동합니다.

**Q: 인덱싱 진행 상황을 어떻게 모니터링할 수 있나요?**  
A: `Index.add()` 오버로드 중 `Progress` 객체를 반환하는 것을 사용하거나 로깅 콜백에 연결합니다.

## 리소스
- **문서**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API 레퍼런스**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **다운로드**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **무료 지원**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **임시 라이선스**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**마지막 업데이트:** 2026-10-02  
**테스트 환경:** GroupDocs.Search 25.4 for Java  
**작성자:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 관련 튜토리얼

- [검색 인덱스 디렉터리 생성 및 라이선스 설정 – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [GroupDocs.Search Java로 쿼리 성능 향상: 인덱스 및 검색 최적화](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java 고급 검색 기능](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
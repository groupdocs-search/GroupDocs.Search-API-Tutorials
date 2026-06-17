---
date: '2026-02-21'
description: GroupDocs.Search를 사용하여 Java에서 청크 기반 검색으로 문서를 인덱스에 추가하고 검색 성능을 향상시키는 방법을
  배우고, 대용량 문서 세트에 대한 Java 검색 인덱스 메모리를 최적화하세요.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Java에서 청크 기반 검색으로 문서를 인덱스에 추가하기
type: docs
url: /ko/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Java에서 청크 기반 검색으로 인덱스에 문서 추가

현대 애플리케이션에서 **인덱스에 문서를 빠르게 추가**하고 이후 빠른 청크‑기반 쿼리를 수행하려면 메모리를 과도하게 사용하지 않으면서 확장 가능한 솔루션이 필요합니다. 이 튜토리얼에서는 GroupDocs.Search for Java를 설정하고, 여러 문서 폴더를 추가하며, **검색 성능을 높이고** **java search index memory** 사용량을 제어하는 엔진을 구성하는 방법을 단계별로 안내합니다. 법률 계약서, 지원 티켓, 연구 논문 등 어떤 종류의 문서를 인덱싱하든 아래 단계들을 따라 하면 프로덕션에 바로 적용 가능한 구현을 만들 수 있습니다.

## Quick Answers
- **첫 번째 단계는 무엇인가요?** 검색 인덱스 폴더를 생성합니다.  
- **많은 파일을 포함하려면 어떻게 하나요?** 각 문서 폴더마다 `index.add()`를 사용합니다.  
- **청크 검색을 활성화하는 옵션은?** `options.setChunkSearch(true)`.  
- **첫 번째 청크 이후에도 검색을 계속할 수 있나요?** 예, 토큰과 함께 `index.searchNext()`를 호출하면 됩니다.  
- **라이선스가 필요한가요?** 개발 단계에서는 무료 체험 또는 임시 라이선스로 충분하지만, 프로덕션에서는 정식 라이선스가 필요합니다.  

## What You’ll Learn
- 지정된 폴더에 검색 인덱스를 만드는 방법.  
- 여러 위치에서 **인덱스에 문서를 추가**하는 단계.  
- 청크‑기반 검색을 활성화하도록 검색 옵션을 구성하는 방법.  
- 초기 및 이후 청크‑기반 검색 수행 방법.  
- 청크‑기반 문서 검색이 빛을 발하는 실제 시나리오.  

## Prerequisites
이 가이드를 따라 하려면 다음을 준비하세요:

- **필수 라이브러리**: GroupDocs.Search for Java 25.4 이상.  
- **환경 설정**: 호환되는 Java Development Kit (JDK) 설치.  
- **지식 전제조건**: 기본 Java 프로그래밍 및 Maven 사용 경험.  

## Setting Up GroupDocs.Search for Java
먼저 Maven을 사용해 프로젝트에 GroupDocs.Search를 통합합니다:

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

또는 최신 버전을 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 다운로드하세요.

### License Acquisition
GroupDocs.Search를 체험하려면:

- **Free Trial** – 핵심 기능을 무료로 테스트.  
- **Temporary License** – 개발용으로 연장된 접근 권한.  
- **Purchase** – 프로덕션 사용을 위한 정식 라이선스.  

### Basic Initialization and Setup
검색 가능한 데이터를 저장할 폴더에 인덱스를 생성합니다:

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

## How to add documents to index
인덱스가 생성되었으니, 이제 파일이 저장된 위치에서 **인덱스에 문서를 추가**하는 것이 다음 논리적 단계입니다.

### 1. Creating an Index
**개요**: 검색 인덱스를 위한 디렉터리를 설정합니다.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adding Documents to Index
**개요**: 여러 소스 폴더에서 파일을 가져옵니다.

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

### 3. Configuring Search Options for Chunk Search
옵션 객체를 조정해 청크‑기반 검색을 활성화합니다.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Performing Initial Chunk‑Based Search
청크가 활성화된 옵션을 사용해 첫 번째 쿼리를 실행합니다.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuing Chunk‑Based Search
검색이 완료될 때까지 남은 청크를 순차적으로 처리합니다.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Why use chunk‑based search?
청크‑기반 검색은 방대한 문서 컬렉션을 관리 가능한 조각으로 나누어 메모리 부담을 줄이고 응답 시간을 단축합니다. 특히 다음 상황에서 유용합니다:

1. **법무팀**이 수천 개 계약서에서 특정 조항을 찾아야 할 때.  
2. **고객 지원 포털**이 관련 지식‑베이스 문서를 즉시 제공해야 할 때.  
3. **연구원**이 전체 파일을 메모리에 로드하지 않고 방대한 데이터셋을 탐색해야 할 때.  

## How this approach **increases search performance**
전체 파일 대신 작은 청크를 검색함으로써 엔진은 다음을 수행할 수 있습니다:

- 관련 없는 섹션을 조기에 건너뛰어 CPU 사이클을 절감.  
- 활성 청크만 메모리에 유지해 **java search index memory** 사용량을 직접 감소.  
- 다중 코어 머신에서 청크 처리를 병렬화해 결과를 더 빠르게 반환.  

## Managing **java search index memory**
청크‑기반 검색만으로도 메모리 사용량이 감소하지만, JVM을 추가로 튜닝할 수 있습니다:

- 인덱스 크기에 맞춰 충분한 힙을 할당 (`-Xmx2g` 이상).  
- 대량 추가 후 `index.optimize()`를 호출해 인덱스 구조를 압축.  
- VisualVM 같은 도구로 GC 일시 정지를 모니터링해 지연 시간 급증을 방지.  

## Performance Considerations
- **Memory Management** – 대형 인덱스를 위해 충분한 힙 공간(`-Xmx`)을 할당합니다.  
- **Resource Monitoring** – 인덱싱 및 검색 작업 중 CPU 사용량을 지속적으로 확인합니다.  
- **Index Maintenance** – 오래된 데이터를 제거하기 위해 인덱스를 주기적으로 재구축하거나 정리합니다.  

## Common Pitfalls & Troubleshooting
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` during indexing | Heap size too low | Increase JVM heap (`-Xmx2g` or higher) |
| No results returned | Chunk token not processed | Ensure the `while` loop runs until `getNextChunkSearchToken()` is `null` |
| Slow search performance | Index not optimized | Run `index.optimize()` after bulk additions |

## Frequently Asked Questions

**Q: 청크‑기반 검색이란 무엇인가요?**  
A: 청크‑기반 검색은 데이터셋을 작은 조각으로 나누어 전체 문서를 메모리에 로드하지 않고도 대용량 데이터를 효율적으로 쿼리할 수 있게 합니다.

**Q: 새 파일이 추가되면 인덱스를 어떻게 업데이트하나요?**  
A: 새 문서 경로를 인자로 `index.add()`를 호출하면 인덱스가 자동으로 반영됩니다.

**Q: GroupDocs.Search가 다양한 파일 형식을 지원하나요?**  
A: 예, PDF, DOCX, XLSX, PPTX 등 여러 일반 형식을 지원합니다.

**Q: 일반적인 성능 병목 현상은 무엇인가요?**  
A: 메모리 제한과 최적화되지 않은 인덱스가 가장 흔합니다; 충분한 힙을 할당하고 인덱스를 정기적으로 최적화하세요.

**Q: 더 자세한 문서는 어디서 찾을 수 있나요?**  
A: 공식 [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)에서 심층 가이드와 API 레퍼런스를 확인하세요.

**Q: 암호화된 PDF에서도 청크‑기반 검색이 작동하나요?**  
A: 예, 해당 API 오버로드에 비밀번호를 제공하면 됩니다.

**Q: 인덱싱 진행 상황을 어떻게 모니터링하나요?**  
A: `Index.add()` 오버로드 중 `Progress` 객체를 반환하거나 로깅 콜백을 활용하면 됩니다.

## Resources
- **Documentation**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Reference**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs  

---
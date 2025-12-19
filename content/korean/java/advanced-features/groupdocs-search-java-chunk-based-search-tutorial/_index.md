---
date: '2025-12-19'
description: GroupDocs.Search를 사용하여 Java에서 문서를 인덱스에 추가하고 청크 기반 검색을 활성화하는 방법을 배우고,
  대용량 문서 세트의 성능을 향상시키세요.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Java에서 청크 기반 검색을 사용하여 문서를 인덱스에 추가
type: docs
url: /ko/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Java에서 청크 기반 검색으로 문서 인덱스에 추가하기

오늘날 데이터 중심의 세상에서 **문서를 인덱스에 추가**하고 빠르게 청크 기반 검색을 수행할 수 있는 능력은 대량 파일 컬렉션을 다루는 모든 애플리케이션에 필수적입니다. 법률 계약서, 고객 지원 아카이브, 방대한 연구 라이브러리를 다루든, 이 튜토리얼은 GroupDocs.Search for Java을 설정하여 문서를 효율적으로 인덱싱하고 필요한 정보를 작은 청크 단위로 검색하는 방법을 정확히 보여줍니다.

## 배울 내용
- 지정된 폴더에 검색 인덱스를 만드는 방법.  
- 여러 위치에서 **문서를 인덱스에 추가**하는 단계.  
- 청크 기반 검색을 활성화하기 위한 검색 옵션 구성.  
- 초기 및 이후 청크 기반 검색 수행 방법.  
- 청크 기반 문서 검색이 빛을 발하는 실제 시나리오.

## 빠른 답변
- **첫 번째 단계는 무엇인가요?** 검색 인덱스 폴더를 생성합니다.  
- **많은 파일을 포함하려면 어떻게 하나요?** 각 문서 폴더에 대해 `index.add()`를 사용합니다.  
- **청크 검색을 활성화하는 옵션은?** `options.setChunkSearch(true)`.  
- **첫 번째 청크 이후에도 검색을 계속할 수 있나요?** 예, 토큰과 함께 `index.searchNext()`를 호출하면 됩니다.  
- **라이선스가 필요하나요?** 개발용으로는 무료 체험 또는 임시 라이선스로 충분하지만, 프로덕션에서는 정식 라이선스가 필요합니다.

## 전제 조건
이 가이드를 따르려면 다음을 준비하십시오:

- **필수 라이브러리**: GroupDocs.Search for Java 25.4 이상.  
- **환경 설정**: 호환되는 Java Development Kit (JDK) 설치.  
- **지식 전제**: 기본 Java 프로그래밍 및 Maven 사용 경험.

## GroupDocs.Search for Java 설정
프로젝트에 Maven을 사용해 GroupDocs.Search를 통합합니다:

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

또는 최신 버전을 [GroupDocs.Search for Java 릴리스](https://releases.groupdocs.com/search/java/)에서 다운로드하십시오.

### 라이선스 획득
GroupDocs.Search를 사용해 보기:

- **무료 체험** – 핵심 기능을 제한 없이 테스트.  
- **임시 라이선스** – 개발을 위한 연장된 접근 권한.  
- **구매** – 프로덕션 사용을 위한 정식 라이선스.

### 기본 초기화 및 설정
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

## 문서를 인덱스에 추가하는 방법
인덱스가 생성되었으니, 이제 파일이 저장된 위치에서 **문서를 인덱스에 추가**하는 것이 다음 논리적 단계입니다.

### 1. 인덱스 생성
**개요**: 검색 인덱스를 위한 디렉터리를 설정합니다.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. 문서를 인덱스에 추가
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

### 3. 청크 검색을 위한 검색 옵션 구성
옵션 객체를 조정하여 청크 기반 검색을 활성화합니다.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. 초기 청크 기반 검색 수행
청크가 활성화된 옵션을 사용해 첫 번째 쿼리를 실행합니다.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. 청크 기반 검색 계속하기
검색이 완료될 때까지 남은 청크를 순차적으로 처리합니다.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## 청크 기반 검색을 사용하는 이유
청크 기반 검색은 방대한 문서 컬렉션을 관리 가능한 조각으로 나누어 메모리 부담을 줄이고 응답 시간을 가속화합니다. 특히 다음 상황에서 유용합니다:

1. **법무팀**이 수천 개 계약서에서 특정 조항을 찾아야 할 때.  
2. **고객 지원 포털**이 관련 지식베이스 기사를 즉시 제공해야 할 때.  
3. **연구원**이 전체 파일을 메모리에 로드하지 않고 방대한 데이터셋을 탐색해야 할 때.

## 성능 고려 사항
- **메모리 관리** – 대형 인덱스를 위해 충분한 힙 공간(`-Xmx`)을 할당합니다.  
- **리소스 모니터링** – 인덱싱 및 검색 작업 중 CPU 사용량을 주시합니다.  
- **인덱스 유지보수** – 오래된 데이터를 제거하기 위해 주기적으로 인덱스를 재구축하거나 정리합니다.

## 일반적인 함정 및 문제 해결
| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| `OutOfMemoryError` during indexing | 힙 크기가 너무 작음 | JVM 힙을 늘립니다 (`-Xmx2g` 이상) |
| No results returned | 청크 토큰이 처리되지 않음 | `while` 루프가 `getNextChunkSearchToken()`이 `null`이 될 때까지 실행되는지 확인 |
| Slow search performance | 인덱스가 최적화되지 않음 | 대량 추가 후 `index.optimize()`를 실행 |

## 자주 묻는 질문

**Q: 청크 기반 검색이란 무엇인가요?**  
A: 청크 기반 검색은 데이터셋을 작은 조각으로 나누어 전체 문서를 메모리에 로드하지 않고도 대용량 데이터에 대한 효율적인 쿼리를 가능하게 합니다.

**Q: 새로운 파일로 인덱스를 어떻게 업데이트하나요?**  
A: 새 문서 경로를 인수로 `index.add()`를 호출하면 인덱스가 자동으로 반영됩니다.

**Q: GroupDocs.Search가 다양한 파일 형식을 지원하나요?**  
A: 예, PDF, DOCX, XLSX, PPTX 등 많은 일반 형식을 지원합니다.

**Q: 일반적인 성능 병목 현상은 무엇인가요?**  
A: 메모리 제한과 최적화되지 않은 인덱스가 가장 흔합니다; 충분한 힙을 할당하고 정기적으로 인덱스를 최적화하십시오.

**Q: 더 자세한 문서는 어디서 찾을 수 있나요?**  
A: 공식 [GroupDocs.Search 문서](https://docs.groupdocs.com/search/java/)에서 심층 가이드와 API 레퍼런스를 확인하세요.

## 리소스
- **문서**: [GroupDocs.Search for Java 문서](https://docs.groupdocs.com/search/java/)  
- **API 레퍼런스**: [GroupDocs.Search API 레퍼런스](https://reference.groupdocs.com/search/java)  
- **다운로드**: [GroupDocs.Search 릴리스](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub 저장소](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **무료 지원**: [GroupDocs 포럼](https://forum.groupdocs.com/c/search/10)  
- **임시 라이선스**: [임시 라이선스 받기](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
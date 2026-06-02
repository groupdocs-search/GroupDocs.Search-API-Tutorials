---
date: '2026-02-06'
description: GroupDocs.Search를 사용하여 Java에서 문서를 인덱스에 추가하고 대소문자 구분 검색을 활성화하는 방법을 배우고,
  애플리케이션의 정확성을 높이세요.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: '문서를 인덱스에 추가: GroupDocs를 활용한 대소문자 구분 Java 검색'
type: docs
url: /ko/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# 인덱스에 문서 추가: Java와 GroupDocs를 활용한 대소문자 구분 검색 마스터하기

방대한 문서 컬렉션에서 올바른 정보를 찾아내는 것은 현대 애플리케이션의 핵심 요구 사항입니다. 이 가이드에서는 **인덱스에 문서를 추가하는 방법**과 GroupDocs.Search for Java를 사용한 **대소문자 구분 검색**을 수행하는 방법을 배웁니다. 법률 문서 저장소, 전자상거래 카탈로그, 콘텐츠 관리 시스템을 구축하든, 정확한 검색 결과는 사용자 만족도를 높이고 데이터의 신뢰성을 유지합니다.

## 빠른 답변
- **검색을 시작하기 위한 기본 단계는 무엇인가요?** `index.add(...)` 로 인덱스에 문서를 추가합니다.  
- **대소문자 구분 검색을 어떻게 활성화하나요?** `options.setUseCaseSensitiveSearch(true)` 를 설정합니다.  
- **여러 디렉터리를 동시에 검색할 수 있나요?** 예 – 포함하려는 각 폴더에 대해 `index.add()` 를 호출합니다.  
- **객체를 사용해 검색하려면 어떤 메서드를 사용하나요?** `SearchQuery.createWordQuery(...)` 를 사용합니다.  
- **테스트에 라이선스가 필요합니까?** 체험용으로 임시 라이선스를 사용할 수 있습니다.

## “인덱스에 문서 추가”가 의미하는 바는 무엇인가요?
인덱스에 문서를 추가한다는 것은 소스 파일(PDF, Word 문서, 일반 텍스트 등)을 GroupDocs.Search에 전달하여 검색 가능한 데이터 구조를 구축한다는 의미입니다. 인덱싱이 완료되면 엔진은 대소문자 구분 검색을 포함한 빠른 쿼리를 실행할 수 있습니다.

## Java에서 대소문자 구분 검색을 활성화하는 이유는?
- **정확한 용어 매칭** – “Apple”(회사)과 “apple”(과일)을 구분합니다.  
- **규제 준수** – 일부 산업에서는 정확한 구문 매칭이 요구됩니다.  
- **관련성 향상** – 기술 또는 법률 분야에서 사용자는 대소문자 구분 결과를 기대합니다.

## 사전 요구 사항
- JDK (Java 17 이상 권장)  
- Maven (의존성 관리)  
- IntelliJ IDEA 또는 Eclipse와 같은 IDE  
- Java 프로그래밍에 대한 기본 지식  

## GroupDocs.Search for Java 설정
First, add the GroupDocs repository and dependency to your `pom.xml`:

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

또는 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) 에서 최신 버전을 직접 다운로드할 수 있습니다.

### 라이선스
체험판을 시작하려면 GroupDocs 사이트에서 임시 라이선스를 획득하십시오. 이를 통해 모든 기능을 제한 없이 테스트할 수 있습니다.

## 인덱스에 문서 추가 – 텍스트 쿼리 검색

### 단계 1: 인덱스 생성 및 문서 추가
인덱스 파일이 저장될 폴더를 만든 뒤, 검색하려는 문서가 들어 있는 소스 디렉터리를 추가합니다.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **프로 팁:** `index.add()` 를 여러 번 호출하여 단일 인덱스에서 **여러 디렉터리를 검색**할 수 있습니다.

### 단계 2: 대소문자 구분 검색 활성화
검색 옵션을 설정하여 대소문자를 구분하도록 구성합니다.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 단계 3: 대소문자 구분 텍스트 쿼리 실행
“Advantages”와 “advantages”를 구분하는 쿼리를 실행합니다.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

루프는 정확히 대소문자가 일치하는 용어를 포함한 각 문서의 전체 경로를 출력합니다.

## 인덱스에 문서 추가 – 객체 쿼리 검색

객체 쿼리는 특히 여러 조건을 결합해야 할 때 더 큰 유연성을 제공합니다.

### 단계 1: 두 번째 인덱스 초기화 (선택 사항)
객체 기반 검색을 별도로 유지하고 싶다면 다른 인덱스 폴더를 생성합니다.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### 단계 2: 대소문자 구분 옵션 재사용
동일한 `SearchOptions` 인스턴스를 객체 쿼리에도 사용할 수 있습니다.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### 단계 3: 객체 쿼리 구축 및 실행
워드 쿼리 객체를 생성하고 이를 검색 엔진에 전달합니다.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

`createWordQuery` 를 사용하면 이후에 구문, 와일드카드 또는 Boolean 쿼리와 결합하여 더 복잡한 시나리오를 구현할 수 있습니다.

## 실용적인 적용 사례
- **법률 문서 관리:** 대소문자가 중요한 사례별 조항을 검색합니다.  
- **전자상거래 플랫폼:** “PRO‑X”와 “pro‑x”와 같은 제품 SKU를 구분합니다.  
- **콘텐츠 관리 시스템(CMS):** 작성자가 정확한 제목이나 태그를 찾을 수 있도록 합니다.

## 성능 고려 사항
- **인덱스를 최신 상태로 유지** – 새 파일이 추가되거나 기존 파일이 변경될 때 재인덱싱합니다.  
- **메모리 사용량 모니터링** – 대규모 코퍼스는 증분 인덱싱과 적절한 JVM 힙 크기 설정으로 이점을 얻습니다.  
- **Java 가비지 컬렉터 활용** – 더 이상 필요하지 않은 `Index` 객체를 해제합니다.

## 일반적인 문제 및 해결책
| Issue | Solution |
|-------|----------|
| `useCaseSensitiveSearch` appears ignored | 최신 GroupDocs.Search 버전을 사용하고 옵션 변경 후 인덱스를 재구축했는지 확인하십시오. |
| No results returned for a known term | 용어의 대소문자가 정확히 일치하는지, 그리고 문서가 인덱스에 성공적으로 추가되었는지 확인하십시오. |
| Searching many folders slows down | 각 폴더를 `index.add()` 로 개별 추가하고, 매우 큰 데이터셋의 경우 인덱스를 샤드로 분할하는 것을 고려하십시오. |

## 자주 묻는 질문

**Q:** GroupDocs.Search로 대용량 데이터셋을 어떻게 처리하나요?  
**A:** 인덱스 파티셔닝을 활용하고 JVM 메모리 설정을 조정하며, 성능을 최적화하기 위해 주기적으로 인덱스를 압축합니다.

**Q:** 여러 디렉터리를 동시에 검색할 수 있나요?  
**A:** 예 – 포함하려는 각 디렉터리에 대해 `index.add()` 를 호출한 뒤, 결합된 인덱스에 단일 쿼리를 실행합니다.

**Q:** 대소문자 구분 검색을 설정할 때 흔히 발생하는 실수는 무엇인가요?  
**A:** `useCaseSensitiveSearch` 를 활성화한 후 인덱스를 재구축하지 않거나, 쿼리 문자열에서 잘못된 대소문자를 사용하는 경우입니다.

**Q:** 검색 오류를 어떻게 해결하나요?  
**A:** GroupDocs.Search가 생성한 로그 파일에서 스택 트레이스를 확인하고, 모든 Maven 의존성이 올바르게 해결되었는지 확인하십시오.

**Q:** GroupDocs.Search가 실시간 애플리케이션에 적합한가요?  
**A:** 적절한 인덱싱 전략(증분 업데이트 및 인메모리 캐싱)을 사용하면 거의 실시간에 가까운 검색 결과를 제공할 수 있습니다.

## 리소스
- **문서:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API 레퍼런스:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **다운로드:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub 저장소:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **지원 포럼:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **임시 라이선스:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-02-06  
**테스트 환경:** GroupDocs.Search 25.4  
**작성자:** GroupDocs
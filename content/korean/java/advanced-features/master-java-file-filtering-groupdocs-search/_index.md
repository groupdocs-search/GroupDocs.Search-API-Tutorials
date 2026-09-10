---
date: '2026-09-06'
description: GroupDocs.Search for Java를 사용하여 java 파일 확장자를 필터링하는 방법을 배우고, 논리 연산자 AND,
  OR, NOT, 날짜 범위 필터 및 경로 필터에 대해 알아봅니다.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: GroupDocs.Search를 사용하여 java 파일 확장자를 필터링합니다. Java에서 논리 연산자를 사용해 확장자,
  날짜 범위 및 경로 필터를 결합하는 방법을 배웁니다.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: GroupDocs.Search로 java 파일 확장자 필터링 – 완전 가이드
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: GroupDocs.Search를 사용한 java 파일 확장자 필터링 방법
type: docs
url: /ko/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search를 사용한 Java 파일 확장자 필터링

이 포괄적인 튜토리얼에서는 GroupDocs.Search를 사용하여 문서를 인덱싱할 때 **filter file extensions java** 방법을 배웁니다. 가이드를 마치면 필요한 파일 유형만 포함하고, 원하지 않는 형식을 제외하며, 날짜 범위 및 경로 필터와 논리 연산자 AND, OR, NOT을 사용해 이러한 규칙을 결합할 수 있습니다. 이 접근 방식은 인덱스를 가볍게 유지하고 검색 속도를 높이며 데이터 처리 정책을 준수하는 데 도움이 됩니다.

## 빠른 답변
- **java file extension filter란 무엇인가요?** 이는 인덱싱 중에 포함하거나 제외할 파일 확장자를 GroupDocs.Search에 알려주는 규칙입니다.  
- **어떤 라이브러리가 이 기능을 제공하나요?** GroupDocs.Search for Java.  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험으로 충분하며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **필터를 결합할 수 있나요?** 예 – 확장자, 날짜, 크기 및 경로 필터를 AND, OR, NOT 논리와 함께 체인할 수 있습니다.  
- **Maven과 호환되나요?** 물론 – `pom.xml`에 GroupDocs.Search 의존성을 추가하면 됩니다.  

## java file extension filter란 무엇인가요?
**java file extension filter**는 파일이 인덱싱 엔진으로 전달되기 전에 각 파일의 확장자를 평가하는 규칙 집합입니다. `.txt`, `.pdf`, `.epub`와 같은 확장자를 지정하면 **include files by extension** 또는 **exclude files by extension**을 통해 인덱스를 집중시키고 검색 결과를 관련성 있게 유지할 수 있습니다.

## GroupDocs.Search와 함께 파일 확장자 필터링을 사용하는 이유는 무엇인가요?
파일 확장자 필터링은 관련 없는 형식을 제외함으로써 인덱싱 효율성을 높이고, 저장 요구량을 줄이며, 원치 않는 콘텐츠가 인덱스로 들어가는 것을 방지해 규정 준수를 돕습니다. 또한 검색 엔진이 더 작고 관련성 높은 데이터 세트를 처리하므로 쿼리 응답 속도가 빨라집니다.

- **Performance:** 원하지 않는 파일을 건너뛰면 I/O가 감소하고 대규모 저장소에서 인덱싱 속도가 최대 40 % 빨라집니다.  
- **Storage savings:** 관련 문서만 인덱스에 저장되어 평균 30 % 정도 디스크 사용량이 감소합니다.  
- **Compliance:** 기밀 또는 지원되지 않는 파일 유형이 실수로 인덱싱되는 것을 방지합니다.  
- **Flexibility:** **date range filter java** 기능과 결합해 특정 기간에 생성·수정된 파일을 대상으로 할 수 있습니다.  

## 전제 조건

시작하기 전에 다음 항목을 준비하십시오:

### 필요한 라이브러리 및 종속성
- **GroupDocs.Search for Java** – 버전 25.4 이상 (60개 이상의 입력 형식 지원).  
- **Java Development Kit (JDK)** – 호환 가능한 버전이면 모두 (8 버전 이상).

### 환경 설정
- 통합 개발 환경(IDE): IntelliJ IDEA, Eclipse 또는 Maven‑compatible IDE.

### 지식 전제 조건
- 기본 Java 프로그래밍.  
- Java 파일 I/O에 대한 친숙함.  
- 정규식 및 날짜‑시간 처리에 대한 이해.

## GroupDocs.Search for Java 설정

GroupDocs.Search를 사용하려면 프로젝트에 의존성으로 포함해야 합니다.

### Maven 구성
`pom.xml` 파일에 다음 저장소 및 의존성 구성을 추가하십시오:

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

### 직접 다운로드
또는 [GroupDocs.Search for Java 릴리스](https://releases.groupdocs.com/search/java/)에서 최신 버전을 직접 다운로드하십시오.

#### 라이선스 획득
1. **Free trial** – 비용 없이 기능을 탐색합니다.  
2. **Temporary license** – 제한된 기간 동안 전체 기능을 사용합니다.  
3. **Purchase** – 프로덕션 사용을 위한 영구 라이선스를 획득합니다.

### 기본 초기화 및 설정
라이브러리를 추가한 후 인덱싱 환경을 초기화합니다. `IndexSettings` 클래스는 필터를 포함한 모든 구성 옵션을 보유합니다.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 구현 가이드

아래에서는 각 필터 유형을 자세히 살펴보고 **왜 중요한지** 설명한 뒤, 프로젝트에 복사해 사용할 수 있는 단계별 지침을 제공합니다.

### 파일 확장자 필터링
인덱싱 중에 파일 확장자를 기준으로 파일을 필터링합니다. 전자책(`.fb2`, `.epub`)과 일반 텍스트 파일(`.txt`)만 처리하고 싶을 때 이상적입니다.

#### 개요
`DocumentFilter.createFileExtension`은 확장자 화이트리스트를 생성합니다.

#### 구현 단계
1. **Create filter** – 유지하려는 확장자를 정의합니다.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – `IndexSettings`를 구성할 때 필터를 적용합니다.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 논리 NOT 필터
검색 시나리오에 필요하지 않은 경우 웹 페이지나 PDF와 같은 특정 확장자를 제외합니다.

#### 구현 단계
1. **Create exclusion filter** – 제외할 확장자를 지정합니다.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – NOT 필터를 다른 규칙과 결합합니다.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – 결합된 필터를 통과한 파일만 인덱싱됩니다.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 논리 AND 필터
생성 날짜, 확장자, 파일 크기 등 여러 조건을 결합해 **모든 기준을 충족하는 파일**만 인덱싱합니다.

#### 개요
`DocumentFilter.createAnd`는 여러 필터를 하나의 규칙으로 병합합니다.

#### 구현 단계
1. **Define filters** – 각 조건에 대한 개별 필터를 생성합니다.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – 모든 조건을 요구하도록 AND 연산자를 사용합니다.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – 결합된 필터를 인덱싱 파이프라인에 전달합니다.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 논리 OR 필터
지정된 조건 중 **하나라도** 만족하는 파일을 포함합니다—작은 텍스트 파일과 큰 비텍스트 파일을 모두 포착하고 싶을 때 유용합니다.

#### 구현 단계
1. **Define filters** – 각 대안 조건에 대해 별도 필터를 생성합니다.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – OR 연산자를 사용합니다.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – 결합된 필터를 인덱스 구성에 연결합니다.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 생성 시간 필터
특정 기간 내에 생성된 파일을 대상으로 하는 전형적인 **date range filter java** 시나리오입니다.

#### 구현 단계
1. **Define date‑range filter** – 시작일과 종료일을 지정합니다.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – 생성 타임스탬프가 범위 내에 있는 파일만 인덱싱됩니다.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 수정 시간 필터
특정 기준일 이후에 수정된 파일을 제외합니다.

#### 구현 단계
1. **Define filter** – 최대 수정 타임스탬프를 설정합니다.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – 기준일 이후에 수정된 파일은 무시됩니다.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 파일 경로 필터링
특정 폴더에 있거나 패턴에 일치하는 파일만 인덱싱하도록 제한합니다—특정 디렉터리 구조 내에서 **include files by extension**에 이상적입니다.

#### 구현 단계
1. **Define file‑path filter** – glob 또는 regex 패턴을 사용해 디렉터리를 매칭합니다.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – 다른 규칙과 함께 경로 필터를 적용합니다.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## 일반적인 함정 및 팁

- **절대 경로와 상대 경로를 같은 필터 구성에 혼용하지 마십시오** – 예기치 않은 제외가 발생할 수 있습니다.  
- **필터 세트를 전환할 때 `IndexSettings`를 재설정**하십시오; 그렇지 않으면 이전 필터가 남아 있을 수 있습니다.  
- **대용량 컬렉션에서는 길이 상한선과 확장자 필터를 결합**해 메모리 사용량을 낮추십시오.  
- LoggingOptions는 GroupDocs.Search의 로깅 구성을 제어합니다.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`)을 활성화하면 파일이 거부된 이유를 확인할 수 있습니다.  

## 자주 묻는 질문

**Q: 인덱스를 만든 후에도 필터 기준을 변경할 수 있나요?**  
A: 예. 새 `DocumentFilter`로 인덱스를 재구축하거나 업데이트된 설정으로 증분 인덱싱을 수행하면 됩니다.

**Q: java file extension filter가 압축 아카이브(e.g., ZIP)에서도 작동하나요?**  
A: GroupDocs.Search는 지원되는 아카이브 형식을 인덱싱할 수 있지만, 확장자 필터는 아카이브 자체에 적용되며 내부 파일에는 적용되지 않습니다. 내부 파일을 제어하려면 중첩 필터를 사용하십시오.

**Q: 특정 파일이 제외된 이유를 어떻게 디버깅하나요?**  
A: 라이브러리 로깅을 (`LoggingOptions.setEnabled(true)`) 활성화하고 로그를 확인하면 어떤 필터가 파일을 거부했는지 보고할 수 있습니다.

**Q: java file extension filter를 사용자 정의 정규식 필터와 결합할 수 있나요?**  
A: 물론 가능합니다. 정규식 필터를 `DocumentFilter.createAnd()` 안에 래핑해 확장자 필터와 함께 사용하면 됩니다.

**Q: 많은 필터를 추가하면 성능에 어떤 영향을 미치나요?**  
A: 각 필터는 인덱싱 시 약간의 오버헤드를 추가하지만, 인덱싱되는 데이터가 감소함으로써 일반적으로 비용보다 이점이 큽니다. 대표 샘플로 테스트해 최적의 균형을 찾으세요.

---

**마지막 업데이트:** 2026-09-06  
**테스트 환경:** GroupDocs.Search 25.4 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [맞춤 날짜 형식 Java | GroupDocs와 날짜 범위 검색](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: GroupDocs.Search for Java로 부울 검색 마스터](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [GroupDocs.Search for Java의 고급 인덱싱 기술로 검색 성능 최적화](/search/java/indexing/groupdocs-search-java-advanced-indexing/)


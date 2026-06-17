---
date: '2026-02-21'
description: GroupDocs.Search for Java를 사용하여 자바 파일 확장자 필터를 구현하는 방법을 배우고, 논리 연산자, 생성·수정
  날짜 및 경로 필터를 다룹니다.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: GroupDocs.Search를 사용한 Java 파일 확장자 필터 – 가이드
type: docs
url: /ko/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

Also preserve bold formatting.

Let's craft final answer.# GroupDocs.Search와 함께 java 파일 확장자 필터 마스터하기

## 빠른 답변
- **java 파일 확장자 필터란?** 인덱싱 중에 포함하거나 제외할 파일 확장자를 GroupDocs.Search에 알려주는 구성입니다.  
- **어떤 라이브러리가 이 기능을 제공합니까?** GroupDocs.Search for Java.  
- **라이선스가 필요합니까?** 무료 체험으로 평가할 수 있으며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **필터를 결합할 수 있나요?** 예 – 확장자, 날짜, 크기 및 경로 필터를 AND, OR, NOT 논리와 함께 체인할 수 있습니다.  
- **Maven과 호환됩니까?** 물론입니다 – `pom.xml`에 GroupDocs.Search 의존성을 추가하면 됩니다.

## java 파일 확장자 필터란?
**java 파일 확장자 필터**는 파일이 인덱싱 엔진에 전달되기 전에 각 파일의 확장자를 평가하는 규칙 집합입니다. `.txt`, `.pdf`, `.epub`와 같은 확장자를 지정하여 **확장자로 파일을 포함**하거나 **확장자로 파일을 제외**함으로써 인덱스를 집중시키고 검색 결과를 관련성 있게 유지할 수 있습니다.

## GroupDocs.Search와 파일 확장자 필터링을 사용하는 이유
- **성능:** 원하지 않는 파일을 건너뛰면 I/O가 감소하고 인덱싱 속도가 빨라집니다.  
- **스토리지 절감:** 관련 문서만 인덱스에 저장되어 디스크 사용량이 줄어듭니다.  
- **컴플라이언스:** 기밀 파일이나 지원되지 않는 파일 유형이 실수로 인덱싱되는 것을 방지합니다.  
- **유연성:** **date range filter java** 기능과 결합해 특정 기간에 생성·수정된 파일을 대상으로 할 수 있습니다.

## 전제 조건

### 필수 라이브러리 및 종속성
- **GroupDocs.Search for Java**: 버전 25.4 이상  
- **Java Development Kit (JDK)**: 호환되는 버전 설치  

### 환경 설정
- 통합 개발 환경(IDE): IntelliJ IDEA, Eclipse 또는 Maven 호환 IDE  

### 지식 전제 조건
- 기본 Java 프로그래밍  
- Java의 파일 I/O에 대한 친숙함  
- 정규식 및 날짜·시간 처리에 대한 이해  

## GroupDocs.Search for Java 설정하기
GroupDocs.Search를 사용하려면 프로젝트에 의존성을 추가해야 합니다.

### Maven 구성
다음 저장소와 의존성 구성을 `pom.xml` 파일에 추가하십시오:

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
또는 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 최신 버전을 직접 다운로드하십시오.

#### 라이선스 획득
1. **Free Trial** – 비용 없이 기능을 탐색합니다.  
2. **Temporary License** – 제한된 기간 동안 전체 기능을 사용합니다.  
3. **Purchase** – 프로덕션 사용을 위한 영구 라이선스를 획득합니다.  

### 기본 초기화 및 설정
라이브러리를 추가한 후 인덱싱 환경을 초기화합니다:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 구현 가이드
아래에서는 각 필터 유형을 자세히 살펴보고 **왜 중요한지** 설명한 뒤, 프로젝트에 복사해 사용할 수 있는 단계별 코드를 제공합니다.

### 파일 확장자 필터링
인덱싱 중에 파일 확장자를 기준으로 파일을 필터링합니다. 전자책(`.fb2`, `.epub`)과 일반 텍스트 파일(`.txt`)만 처리하고 싶을 때 이상적입니다.

#### 개요
`DocumentFilter.createFileExtension`을 사용해 허용할 확장자를 화이트리스트에 추가합니다.

#### 구현 단계
1. **필터 생성**:

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **인덱스 초기화 및 문서 추가**:

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical NOT 필터
검색 시나리오에 필요하지 않은 경우, 웹 페이지나 PDF와 같은 특정 확장자를 제외합니다.

#### 구현 단계
1. **제외 필터 생성**:

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **인덱스 설정에 적용**:

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **문서 추가**:

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical AND 필터
생성 날짜, 확장자, 파일 크기 등 여러 조건을 결합해 **모든 기준을 만족하는 파일**만 인덱싱합니다.

#### 개요
`DocumentFilter.createAnd`는 여러 필터를 하나의 규칙으로 병합합니다.

#### 구현 단계
1. **필터 정의**:

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **필터 결합**:

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **문서 인덱싱**:

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logical OR 필터
지정된 조건 중 **하나라도** 만족하는 파일을 포함합니다. 작은 텍스트 파일과 큰 비텍스트 파일을 모두 포착하고 싶을 때 유용합니다.

#### 구현 단계
1. **필터 정의**:

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **논리 조건으로 필터 결합**:

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **OR 필터 최종화**:

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 생성 시간 필터
특정 기간 내에 생성된 파일을 대상으로 하는 고전적인 **date range filter java** 시나리오입니다.

#### 구현 단계
1. **날짜 범위 필터 정의**:

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **문서 인덱싱**:

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 수정 시간 필터
특정 기준일 이후에 수정된 파일을 제외합니다.

#### 구현 단계
1. **필터 정의**:

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **문서 인덱싱**:

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### 파일 경로 필터링
특정 폴더에 있거나 특정 패턴과 일치하는 파일만 인덱싱하도록 제한합니다. 특정 디렉터리 계층 내에서 **include files by extension**에 이상적입니다.

#### 구현 단계
1. **파일 경로 필터 정의**:

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **인덱스 초기화 및 문서 추가**:

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## 일반적인 함정 및 팁

- **절대 경로와 상대 경로를 같은 필터 구성에 혼용하지 마십시오** – 예기치 않은 제외가 발생할 수 있습니다.  
- **필터 세트를 전환할 때 `IndexSettings`를 재설정하십시오**; 그렇지 않으면 이전 필터가 지속될 수 있습니다.  
- **대용량 컬렉션에서는 확장자 필터와 함께 길이 상한을 결합**해 메모리 사용량을 낮게 유지하십시오.  
- **로깅 활성화** (`LoggingOptions.setEnabled(true)`)를 통해 파일이 왜 거부되었는지 확인할 수 있습니다.  

## 자주 묻는 질문

**Q: 인덱스를 만든 후에 필터 기준을 변경할 수 있나요?**  
A: 예. 새 `DocumentFilter`로 인덱스를 재구축하거나, 업데이트된 설정으로 증분 인덱싱을 수행하면 됩니다.

**Q: java 파일 확장자 필터가 압축 아카이브(e.g., ZIP)에서도 작동하나요?**  
A: GroupDocs.Search는 지원되는 아카이브 형식을 인덱싱할 수 있지만, 확장자 필터는 아카이브 자체에 적용되며 내부 파일에는 적용되지 않습니다. 내부 파일을 제어하려면 중첩 필터를 사용하십시오.

**Q: 특정 파일이 제외된 이유를 어떻게 디버깅하나요?**  
A: 라이브러리의 로깅을 활성화(`LoggingOptions.setEnabled(true)`)하고 로그를 확인하면 어떤 필터가 해당 파일을 거부했는지 보고됩니다.

**Q: java 파일 확장자 필터를 사용자 정의 정규식 필터와 결합할 수 있나요?**  
A: 물론입니다. 정규식 필터를 `DocumentFilter.createAnd()` 안에 확장자 필터와 함께 래핑하면 됩니다.

**Q: 많은 필터를 추가하면 성능에 어떤 영향을 미치나요?**  
A: 각 필터는 인덱싱 중에 약간의 오버헤드를 추가하지만, 인덱싱되는 데이터가 감소함으로써 일반적으로 비용을 상쇄합니다. 대표 샘플로 테스트해 최적의 균형을 찾으세요.

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
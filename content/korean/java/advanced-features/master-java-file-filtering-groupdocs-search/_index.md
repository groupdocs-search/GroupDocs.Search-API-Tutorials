---
date: '2025-12-19'
description: GroupDocs.Search for Java를 사용하여 Java 파일 확장자 필터를 구현하는 방법을 배우고, 논리 연산자,
  생성/수정 날짜 및 경로 필터를 다룹니다.
keywords:
- Java File Filtering
- GroupDocs.Search
- Logical AND OR NOT Filters
title: GroupDocs.Search와 함께하는 Java 파일 확장자 필터 – 가이드
type: docs
url: /ko/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# GroupDocs.Search와 함께 java 파일 확장자 필터 마스터하기

문서 저장소가 커지면 관리가 금방 버거워집니다. 특정 문서 유형만 인덱싱하거나 관련 없는 파일을 제외하고 싶을 때, **java 파일 확장자 필터**를 사용하면 처리 대상에 대한 세밀한 제어가 가능합니다. 이 가이드에서는 GroupDocs.Search for Java 설정 방법을 단계별로 안내하고, 파일‑확장자 필터를 논리 연산자 AND, OR, NOT과 함께 사용하며 날짜‑범위 및 경로 필터까지 결합하는 방법을 보여드립니다.

## 빠른 답변
- **java 파일 확장자 필터란?** 인덱싱 중 포함하거나 제외할 파일 확장자를 지정하는 설정입니다.  
- **어떤 라이브러리가 이 기능을 제공하나요?** GroupDocs.Search for Java.  
- **라이선스가 필요합니까?** 평가용 무료 체험이 가능하며, 운영 환경에서는 정식 라이선스가 필요합니다.  
- **필터를 결합할 수 있나요?** 예 – 확장자, 날짜, 크기, 경로 필터를 AND, OR, NOT 논리로 연결할 수 있습니다.  
- **Maven과 호환되나요?** 물론입니다 – `pom.xml`에 GroupDocs.Search 의존성을 추가하면 됩니다.  

## 소개

파일 저장소가 계속 늘어나면서 효율적으로 관리하기가 어려우신가요? 문서를 유형별로 정리하거나 인덱싱 시 불필요한 파일을 걸러내려면 적절한 도구가 필요합니다. **GroupDocs.Search for Java**는 강력한 파일 필터링 기능을 제공하는 고급 검색 라이브러리로, 이러한 문제를 손쉽게 해결해 줍니다. 이 튜토리얼에서는 GroupDocs.Search를 활용한 .NET 파일 필터링 기법을 Java에 적용하는 방법을 다루며, 논리 연산자 AND, OR, NOT 필터에 중점을 둡니다.

### 배울 내용
- Java 환경에 GroupDocs.Search 설정하기  
- 다양한 필터 구현: 파일 확장자, 논리 연산자(AND, OR, NOT), 생성 시간, 수정 시간, 파일 경로, 길이  
- 효율적인 문서 관리를 위한 실제 적용 사례  
- 대규모 인덱싱 작업을 위한 성능 최적화 팁  

Java에서 파일 필터링의 모든 잠재력을 활용하고 싶으신가요? 먼저 전제 조건을 확인해 보세요.

## 전제 조건

시작하기 전에 다음 항목을 준비하십시오.

### 필수 라이브러리 및 의존성
- **GroupDocs.Search for Java**: 버전 25.4 이상  
- **Java Development Kit (JDK)**: 시스템에 호환되는 버전이 설치되어 있어야 합니다  

### 환경 설정
- 통합 개발 환경(IDE): IntelliJ IDEA, Eclipse 또는 Maven 프로젝트를 지원하는 선호하는 IDE를 사용하세요.

### 지식 전제 조건
- Java 프로그래밍 기본 이해  
- Java 파일 I/O 작업에 대한 친숙함  
- 정규식 및 날짜‑시간 처리에 대한 이해  

## GroupDocs.Search for Java 설정하기
GroupDocs.Search를 사용하려면 프로젝트에 의존성을 추가해야 합니다. 방법은 다음과 같습니다.

### Maven 구성
`pom.xml` 파일에 다음 저장소와 의존성 설정을 추가하십시오:

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
또는 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 최신 버전을 직접 다운로드할 수 있습니다.

#### 라이선스 획득
1. **무료 체험**: GroupDocs.Search 기능을 탐색하기 위해 무료 체험을 시작합니다.  
2. **임시 라이선스**: 제한 없이 전체 기능을 사용하려면 임시 라이선스를 신청합니다.  
3. **구매**: 장기 사용을 위해 구독을 구매합니다.  

### 기본 초기화 및 설정
라이브러리를 추가한 후 인덱싱 환경을 초기화합니다:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## 구현 가이드
이제 GroupDocs.Search를 사용해 다양한 파일 필터링 기능을 구현하는 방법을 살펴보겠습니다.

### 파일 확장자 필터링
인덱싱 중 파일 확장자를 기준으로 파일을 걸러냅니다. 이 기능은 FB2, EPUB, TXT와 같이 특정 문서 유형만 처리하고자 할 때 유용합니다.

#### 개요
맞춤형 필터 구성을 통해 파일 확장자를 기준으로 문서를 필터링합니다.

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

### 논리 NOT 필터
HTM, HTML, PDF와 같이 특정 확장자를 인덱싱에서 제외합니다.

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

### 논리 AND 필터
여러 조건을 결합해 모든 조건을 만족하는 파일만 포함합니다.

#### 개요
생성 시간, 파일 확장자, 길이 등을 기준으로 논리 AND 연산을 사용해 파일을 필터링합니다.

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

### 논리 OR 필터
지정된 기준 중 하나라도 만족하면 파일을 포함합니다.

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
생성 시간을 기준으로 지정된 날짜 범위에 포함되는 파일만 인덱싱합니다.

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
특정 날짜 이후에 수정된 파일을 제외합니다.

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
파일 경로를 기준으로 특정 디렉터리에 위치한 파일만 포함합니다.

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

- **절대 경로와 상대 경로를 같은 필터 구성에 혼용하지 마세요** – 예기치 않은 제외가 발생할 수 있습니다.  
- **필터 세트를 전환할 때는 `IndexSettings`를 반드시 초기화**하십시오; 그렇지 않으면 이전 필터가 남아 있을 수 있습니다.  
- **대용량 파일 컬렉션**은 길이 상한선과 확장자 필터를 함께 사용하면 메모리 사용량을 낮출 수 있습니다.  

## 자주 묻는 질문

**Q: 인덱스를 만든 후에 필터 기준을 변경할 수 있나요?**  
A: 예. 새로운 `DocumentFilter`로 인덱스를 재구축하거나, 업데이트된 설정으로 증분 인덱싱을 수행하면 됩니다.

**Q: java 파일 확장자 필터가 압축 파일(ZIP 등)에도 적용되나요?**  
A: GroupDocs.Search는 지원되는 압축 형식을 인덱싱할 수 있지만, 확장자 필터는 압축 파일 자체에만 적용됩니다. 내부 파일을 필터링하려면 중첩 필터를 사용하세요.

**Q: 특정 파일이 제외된 이유를 어떻게 디버깅하나요?**  
A: 라이브러리 로깅을 활성화(`LoggingOptions.setEnabled(true)`)하고 생성된 로그를 확인하면, 어떤 필터가 파일을 거부했는지 확인할 수 있습니다.

**Q: java 파일 확장자 필터를 사용자 정의 정규식 필터와 결합할 수 있나요?**  
A: 물론입니다. `DocumentFilter.createAnd()` 안에 정규식 필터와 확장자 필터를 함께 래핑하면 됩니다.

**Q: 필터를 많이 추가하면 성능에 어떤 영향을 미치나요?**  
A: 각 필터는 인덱싱 시 약간의 오버헤드를 추가하지만, 인덱스 크기 감소 효과가 일반적으로 비용보다 큽니다. 샘플 데이터로 테스트해 최적의 균형을 찾으세요.

---

**마지막 업데이트:** 2025-12-19  
**테스트 환경:** GroupDocs.Search 25.4 for Java  
**작성자:** GroupDocs  

---
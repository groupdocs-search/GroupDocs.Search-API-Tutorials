---
date: '2026-07-31'
description: GroupDocs.Search를 사용해 인덱스에 문서를 추가하고, character replacement를 이용해 인덱싱 중
  텍스트를 normalize text함으로써 case insensitive search java를 구현하는 방법을 배웁니다.
keywords:
- case insensitive search java
- add documents to index
- character replacement indexing
lastmod: '2026-07-31'
og_description: Case insensitive search java를 사용하면 문서를 인덱스에 추가하고 대소문자를 신경 쓰지 않고 조회할
  수 있습니다. 이 가이드는 GroupDocs.Search가 인덱싱 중 텍스트를 normalize text하여 빠르고 신뢰할 수 있는 결과를 제공하는
  방법을 보여줍니다.
og_image_alt: 'Guide: Add documents to index for case insensitive search in Java using
  GroupDocs.Search'
og_title: Case Insensitive Search Java – GroupDocs와 함께 문서 인덱스
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  headline: Add Documents to Index for Case‑Insensitive Search in Java
  type: TechArticle
- description: Learn how to implement case insensitive search java by adding documents
    to an index with GroupDocs.Search, using character replacement to normalize text
    during indexing.
  name: Add Documents to Index for Case‑Insensitive Search in Java
  steps:
  - name: Configure `IndexSettings`
    text: '`IndexSettings` is the configuration object that controls how the index
      stores and processes text. By setting `useCharacterReplacements` to **true**,
      you turn on automatic lower‑casing (or any custom mapping you provide).'
  - name: Define and Add Replacement Pairs
    text: The replacement dictionary holds pairs such as `'A' → 'a'`, `'É' → 'e'`,
      etc. Adding these pairs before indexing ensures every token is normalized.
  - name: Add Documents for Indexing
    text: GroupDocs.Search scans the target directory, extracts text from each supported
      file type, applies the replacement map, and writes the tokens to the index storage.
  - name: Execute Case‑Sensitive Searches
    text: '`SearchOptions` configures query behavior, such as toggling case sensitivity,
      allowing fine‑grained control over how searches are performed. `SearchOptions.setUseCaseSensitiveSearch(true)`
      forces the engine to treat upper‑ and lower‑case characters as distinct during
      a specific query, overriding the'
  type: HowTo
- questions:
  - answer: Include those characters in your replacement map, mapping them to their
      ASCII equivalents or keeping them unchanged based on search requirements.
    question: How do I handle special characters (e.g., “é”, “ß”) during indexing?
  - answer: Yes. Build a custom replacement array that contains only the characters
      for the target language before adding it to the dictionary.
    question: Can I limit character replacement to a specific language?
  - answer: Optimize the folder structure, remove unnecessary files, and store the
      index on a high‑speed SSD. Incremental indexing also reduces load overhead.
    question: What should I do if the index takes a long time to load?
  - answer: No. Replacements are baked into the indexed data; you must rebuild the
      index with new settings to change them.
    question: Is it possible to revert the character replacements after indexing?
  - answer: The official docs and API reference provide exhaustive details (see Resources
      below).
    question: Where can I find more detailed API documentation?
  type: FAQPage
tags:
- case insensitive search
- GroupDocs.Search
- Java indexing
- document search
title: Java에서 Case‑Insensitive Search를 위한 인덱스에 문서 추가
type: docs
url: /ko/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

# 대소문자 구분 없는 검색을 위한 Java에서 인덱스에 문서 추가

When you need **case insensitive search java** that reliably finds information regardless of how users type it, the key is to add documents to an index while normalizing the text. In this tutorial we walk through configuring GroupDocs.Search for Java so that every document you index is automatically lower‑cased (or otherwise transformed) during indexing, guaranteeing case‑insensitive results without extra query‑time logic.

## 빠른 답변
- **“add documents to index”가 무엇을 의미하나요?** 소스 파일을 검색 가능한 데이터 구조에 로드하여 나중에 쿼리할 수 있게 하는 것을 의미합니다.  
- **문자 교체를 사용하는 이유는?** 모든 문자를 정규화(보통 소문자로)하여 검색 시 대소문자 차이를 자동으로 무시하도록 합니다.  
- **라이선스가 필요합니까?** 무료 체험판은 개발에 사용할 수 있으며, 프로덕션 배포에는 정식 라이선스가 필요합니다.  
- **필요한 Java 버전은?** Java 8 이상; 라이브러리는 최적 성능을 위해 Java 11+을 목표로 합니다.  
- **필요할 때 대소문자 구분 검색으로 전환할 수 있나요?** 예—검색 옵션을 통해 쿼리별로 대소문자 구분을 토글할 수 있습니다.

## GroupDocs.Search에서 “add documents to index”란 무엇인가요?
소스 파일(PDF, DOCX, TXT 등)을 검색 가능한 인덱스로 로드하여 엔진이 빠르게 검색할 수 있도록 합니다. 인덱스에 문서를 추가하면 각 파일을 파싱하고 순수 텍스트를 추출한 뒤, 빠른 조회를 가능하게 하는 최적화된 데이터 구조에 저장합니다.

## 인덱싱 중 문자 교체를 활성화하는 이유는?
문자 교체는 인덱스를 구축하는 동안 각 문자를 미리 정의된 동등 문자(대부분 소문자)로 변환합니다. 이를 통해 대소문자, 악센트, 로케일별 기호의 변형이 검색 결과에 영향을 주지 않도록 보장합니다. 인덱싱 시 텍스트를 정규화함으로써 엔진은 일관된 토큰 집합에 대해 쿼리를 매칭할 수 있어, 각 검색 시 추가 처리를 하지 않아도 빠르고 신뢰할 수 있는 대소문자 구분 없는 동작을 제공합니다.

## 사전 요구 사항
- **GroupDocs.Search for Java** 버전 25.4 이상(이 라이브러리는 30개 이상의 파일 형식을 지원하며 전체 파일을 메모리에 로드하지 않고 수백 페이지 문서를 인덱싱할 수 있습니다).  
- **Java Development Kit (JDK)** 8 이상 설치.  
- **Maven**에 대한 기본적인 이해(또는 JAR를 수동으로 추가할 수 있는 능력).

## GroupDocs.Search for Java 설정

### Maven 설정
`pom.xml`에 GroupDocs 저장소와 의존성을 추가합니다:

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
Maven을 사용하고 싶지 않다면 공식 사이트에서 최신 JAR를 다운로드하세요: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 라이선스 획득
- **Free Trial** – 체험 라이선스를 다운로드하여 실험을 시작합니다.  
- **Temporary License** – GroupDocs 포털에서 연장 테스트 라이선스를 요청합니다.  
- **Full License** – 실서비스를 시작할 준비가 되면 정식 라이선스를 구매합니다.

### 기본 초기화 (인덱스 생성)
다음 스니펫은 인덱스 폴더를 생성하고 문자 교체를 활성화합니다:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## 구현 가이드

### 인덱스 설정에서 문자 교체 활성화
이 기능을 활성화하면 엔진이 인덱싱 중에 문자를 교체하도록 하며, 이는 대소문자 구분 없는 동작을 위한 핵심 단계입니다.

#### 단계 1: `IndexSettings` 구성
`IndexSettings`는 인덱스가 텍스트를 저장하고 처리하는 방식을 제어하는 구성 객체입니다. `useCharacterReplacements`를 **true**로 설정하면 자동 소문자 변환(또는 제공하는 사용자 정의 매핑)을 활성화합니다.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";

// Create an instance of IndexSettings and enable character replacement.
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);

// Initialize the index with these settings.
Index index = new Index(indexFolder, settings);
```

### 문자 교체 구성
각 문자를 소문자 대응 문자(또는 필요한 사용자 정의 매핑)와 매핑합니다.

#### 단계 2: 교체 쌍 정의 및 추가
교체 사전은 `'A' → 'a'`, `'É' → 'e'`와 같은 쌍을 보관합니다. 인덱싱 전에 이러한 쌍을 추가하면 모든 토큰이 정규화됩니다.

```java
import com.groupdocs.search.dictionaries.CharacterReplacementPair;

// Access existing replacements and clear them.
index.getDictionaries().getCharacterReplacements().clear();

// Create an array for new replacements.
CharacterReplacementPair[] characterReplacements = new CharacterReplacementPair[Character.MAX_VALUE + 1];
for (int i = 0; i < characterReplacements.length; i++) {
    char originalChar = (char) i;
    char replacementChar = Character.toLowerCase(originalChar);
    characterReplacements[i] = new CharacterReplacementPair(originalChar, replacementChar);
}

// Add these replacements to the index's dictionary.
index.getDictionaries().getCharacterReplacements().addRange(characterReplacements);
```

### 문서 인덱싱
이제 인덱스가 준비되었으므로, 어떤 폴더에서든 **add documents to index**를 수행할 수 있습니다.

#### 단계 3: 인덱싱을 위한 문서 추가
GroupDocs.Search는 대상 디렉터리를 스캔하고, 지원되는 각 파일 유형에서 텍스트를 추출한 뒤, 교체 맵을 적용하고 토큰을 인덱스 저장소에 기록합니다.

```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### 대소문자 구분 검색 수행 (선택 사항)

#### 단계 4: 대소문자 구분 검색 실행
`SearchOptions`는 쿼리 동작을 구성하며, 예를 들어 대소문자 구분 토글을 통해 검색 수행 방식을 세밀하게 제어할 수 있습니다.  
`SearchOptions.setUseCaseSensitiveSearch(true)`는 특정 쿼리에서 엔진이 대문자와 소문자를 구분하도록 강제하여 기본 대소문자 구분 없는 동작을 무시합니다.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.SearchOptions;
import com.groupdocs.search.results.SearchResult;

String query = "Promotion";
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);

// Perform the search.
Index index = new Index(indexFolder, settings);
SearchResult result = index.search(query, options);
```

## 실용적인 적용 사례
1. **Marketing Campaigns** – 제품명을 정규화하여 영업팀이 대소문자에 구애받지 않고 자산을 찾을 수 있도록 합니다.  
2. **Customer Support** – 사용자가 “login” 또는 “Login”을 입력하더라도 올바른 문서를 반환하는 헬프데스크 검색 상자를 구현합니다.  
3. **E‑commerce Catalogs** – 고객이 제품명을 어떻게 입력하든 항목을 찾을 수 있게 하여 전환율을 향상시킵니다.

## 성능 고려 사항
- **소스 파일 정리** – 깔끔한 폴더 구조는 **add documents to index** 단계에서 스캔 시간을 줄여줍니다.  
- **메모리 모니터링** – 대규모 코퍼스를 인덱싱하면 많은 RAM을 사용할 수 있으므로, 파일을 500 – 1 000개씩 배치 처리하면 힙 사용량을 제어할 수 있습니다.  
- **비동기 인덱싱** – 지원되는 경우 백그라운드 스레드에서 인덱싱을 실행하여 UI 응답성을 유지하고 사용자 작업을 차단하지 않도록 합니다.

## 일반적인 문제 및 해결 방법
| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| 알려진 용어에 대해 결과가 반환되지 않음 | 문자 교체가 활성화되지 않음 | `settings.setUseCharacterReplacements(true)`를 확인하고 교체 맵에 필요한 문자가 포함되어 있는지 확인합니다. |
| 인덱싱 중 메모리 부족 오류 | 한 번에 너무 많은 대용량 파일을 인덱싱 | 작은 배치로 인덱싱하거나 JVM 힙을 늘립니다(`-Xmx4g`). |
| 검색이 예상치 않게 대소문자 구분 결과를 반환 | `SearchOptions.setUseCaseSensitiveSearch(true)`가 설정됨 | `false`로 변경하거나 제거하여 기본 대소문자 구분 없는 동작을 사용합니다. |
| 인덱스 로드 시간이 기대보다 김 | 비효율적인 폴더 구조 또는 SSD 미사용 | 파일을 재구성하고 사용하지 않는 문서를 정리하며 인덱스를 빠른 SSD에 저장합니다. |
| 특수 문자가 무시됨 | 교체 맵에 유니코드 항목이 누락됨 | “é”, “ß”, “ø”와 같은 문자에 대한 매핑을 추가합니다. |

## 자주 묻는 질문

**Q: 인덱싱 중 특수 문자(예: “é”, “ß”)를 어떻게 처리하나요?**  
A: 해당 문자를 교체 맵에 포함시켜 ASCII 동등 문자로 매핑하거나 검색 요구 사항에 따라 그대로 유지합니다.

**Q: 문자 교체를 특정 언어에만 제한할 수 있나요?**  
A: 예. 대상 언어에 해당하는 문자만 포함하는 사용자 정의 교체 배열을 만든 뒤 사전에 추가하면 됩니다.

**Q: 인덱스 로드에 오래 걸리면 어떻게 해야 하나요?**  
A: 폴더 구조를 최적화하고 불필요한 파일을 제거하며 인덱스를 고속 SSD에 저장합니다. 증분 인덱싱도 로드 오버헤드를 줄여줍니다.

**Q: 인덱싱 후에 문자 교체를 되돌릴 수 있나요?**  
A: 아니요. 교체는 인덱스된 데이터에 고정되므로 설정을 변경하려면 인덱스를 다시 구축해야 합니다.

**Q: 자세한 API 문서는 어디서 찾을 수 있나요?**  
A: 공식 문서와 API 레퍼런스에 상세한 내용이 모두 포함되어 있습니다(아래 리소스 참고).

## 리소스
- [문서](https://docs.groupdocs.com/search/java/)
- [API 레퍼런스](https://reference.groupdocs.com/search/java)
- [GroupDocs.Search 다운로드](https://releases.groupdocs.com/search/java/)
- [GitHub 저장소](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [무료 지원 포럼](https://forum.groupdocs.com/c/search/10)
- [임시 라이선스 정보](https://purchase.groupdocs.com/temporary-license/) 

---

**마지막 업데이트:** 2026-07-31  
**테스트 환경:** GroupDocs.Search 25.4 for Java  
**작성자:** GroupDocs  

## 관련 튜토리얼

- [GroupDocs.Search Java에서 문자 교체: 텍스트 검색 및 인덱싱 향상을 위한 종합 가이드](/search/java/text-extraction-processing/groupdocs-search-java-character-replacement-guide/)
- [인덱스에 문서 추가: GroupDocs와 함께하는 대소문자 구분 Java 검색](/search/java/searching/master-case-sensitive-searches-java-groupdocs/)
- [GroupDocs.Search for Java로 인덱스에 문서 추가하는 방법](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
---
date: '2026-02-03'
description: GroupDocs.Search를 사용하여 Java에서 문서를 인덱스에 추가하고 인덱싱 중 문자 교체를 활용해 효율적인 대소문자
  구분 없는 검색을 수행하는 방법을 배워보세요.
keywords:
- case-insensitive search in Java
- character replacement during indexing
- GroupDocs.Search setup
title: Java에서 대소문자 구분 없는 검색을 위해 문서를 인덱스에 추가하기
type: docs
url: /ko/java/searching/master-case-insensitive-search-java-groupdocs-search/
weight: 1
---

스에 정보를 for Java번 신뢰할 수 있는 대소문자 구분 없는 결과를 제공하는 방법을 단계별로 안내합니다.

## Quick Answers
- **“add documents to index”가 의미하는 것은?** 소스 파일을 검색 가능한 인덱스로 넣어 나중에 쿼리할 수 있게 하는 것을 의미합니다.  
- **문자 교체를 사용하는 이유는?** 텍스트를 정규화(예: 모두 소문자로 변환)하여 검색 시 대소문자 차이를 무시하게 합니다.  
- **라이선스가 필요합니까?** 개발 단계에서는 무료 체험판으로 충분하며, 운영 환경에서는 정식 라이선스가 필요합니다.  
- **필요한 Java 버전은?** Java 8 이상; 최적 호환성을 위해 라이브러리는 Java 11+을 권장합니다.  
- **필요에 따라 대소문자 구분 검색을 할 수 있나요?** 예—검색 옵션을 통해 쿼리별로 대소문자 구분 동작을 토글할 수 있습니다.

## GroupDocs.Search에서 “add documents to index”란?
문서를 인덱스에 추가한다는 것은 파일(PDF, Word 문서, 일반 텍스트 등)을 GroupDocs.Search가 조회할 수 있는 데이터 구조에 로드하는 것을 의미합니다. 라이브러리는 각 파일을 파싱하고 검색 가능한 텍스트를 추출한 뒤, 빠르고 효율적인 조회가 가능하도록 저장합니다.

## 인덱싱 중 문자 교체를 활성화하는 이유
문자 교체는 인덱스를 구축하는 동안 모든 문자를 미리 정의된 동등 문자(보통 소문자)로 변환합니다. 이를 통해 **“Promotion”** 같은 쿼리가 **“promotion”**, **“PROMOTION”**, 혹은 혼합 대소문자 형태와도 별도 작업 없이 매치됩니다.

## Prerequisites
- **GroupDocs.Search for Java** 버전 25.4 이상.  
- **Java Development Kit (JDK)** 8 이상 설치.  
- **Maven**에 대한 기본 지식(또는 JAR를 수동으로 추가할 수 있는 능력).

## Setting Up GroupDocs.Search for Java

### Maven Setup
pom.xml`에 GroupDocs 저장소와 의존성을 추가합니다:

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

### Direct Download
Maven을 사용하지 않으려면 공식 사이트에서 최신 JAR를 다운로드하세요: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
- **Free Trial** – 체험용 라이선스를 다운로드하여 실험을 시작합니다.  
- **Temporary License** – GroupDocs 포털에서 연장 테스트 라이선스를 요청합니다.  
- **Full License** – 운영 환경에 진입할 준비가 되면 정식 라이선스를 구매합니다.

### Basic Initialization (Create the index)
다음 스니펫은 인덱스 폴더를 생성하고 문자 교체를 활성화합니다:

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterReplacementDuringIndexing";
IndexSettings settings = new IndexSettings();
settings.setUseCharacterReplacements(true);
Index index = new Index(indexFolder, settings);
```

## Implementation Guide

### Enable Character Replacement in Index Settings
이 기능을 활성화하면 인며: Configure `IndexSettings`
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

### Configure Character Replacements
각 문자를 소문자 대응 문자(또는 필요에 따라 사용자 정의 매핑)로 매핑합니다.

#### Step 2: Define and Add Replacement Pairs
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

### Indexing Documents
인덱스가 준비되었으니 이제 **add documents to index**를 통해任意 폴더의 파일을 추가할 수 있습니다.

#### Step 3: Add Documents for Indexing
```java
import com.groupdocs.search.Index;

String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

// Initialize the index and add documents.
Index index = new Index(indexFolder, settings);
index.add(documentFolder);
```

### Perform Case‑Sensitive Search (Optional)
특정 쿼리에서 대소문자를 구분해야 할 경우, 요청별로 토글할 수 있습니다.

#### Step 4: Execute Case‑Sensitive Searches
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

## Practical Applications
1. **Marketing Campaigns** – 제품명을 정규화하여 영업팀이 대소문자에 신경 쓰지 않고 자산을 찾을 수 있게 합니다.  
2. **Customer Support** – 사용자가 “login”이나 “Login”을 입력해도 올바른 문서를 반환하는 헬프데스크 검색 박스를 구현합니다.  
3. **E‑commerce Catalogs** – 쇼핑객이 제품 제목을 어떻게 입력하든 원하는 아이템을 찾을 수 있도록 보장합니다.

## Performance Considerations
- **Organize Source Files** – 깔끔한 폴더 구조는 **add documents to index** 단계의 속도를 높입니다.  
- **Monitor Memory** – 대용량 데이터는 많은 RAM 배- **Asynchronous드| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| 알려진 용어에 대해 결과가 반환되지 않음 | 문자 교체가 활성화되지 않음 | `settings.setUseCharacterReplacements(true)`와 교체 항목이 추가‑memory싱덱싱하거나 JVM 힙(`-Xmx`)을 늘림 |
| 검색 결과가 예상치 않게 대 해당 Asked Questions

**Q: 인덱싱 중 특수 문자(예: “é”, “ß”)는 어떻게 처리하나요?**  
A: 교체 맵에 해당 문자를 포함시킵니다. 검색 요구사항에 따라 ASCII 등가 문자로 매핑하거나 그대로 유지할 수 있습니다.

**Q: 문자 교체를 특정 언어에만 제한할 수 있나요?**  
A: 예. 대상 언어에 해당하는 문자만 포함한 사용자 정의 교체 배열을 만든 뒤 사전에 추가하면 됩니다.

**Q: 인덱스 로드 시간이 오래 걸리면 어떻게 해야 하나요?**  
A: 폴더 구조를 최적화하고 불필요한 파일을 제거한 뒤, 빠른 SSD에 인덱스를 저장하는 것을 고려하세요.

**Q: 인덱싱 후에 문자 교체를 되돌릴 수 있나요?**  
A: 아니요. 교체는 인덱스 데이터에 영구적으로 적용되므로, 설정을 바꾸려면 인덱스를 새로 빌드해야 합니다.

**Q: 자세한 API 문서는 어디서 찾을 수 있나요?**  
A: 공식 문서와 API 레퍼런스에 상세히 나와 있습니다(아래 Resources 참고).

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java)
- [Download GroupDocs.Search](https://releases.groupdocs.com/search/java/)
- [GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/) 

---

**Last Updated:** 2026-02-03  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
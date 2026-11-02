---
date: '2026-11-02'
description: GroupDocs.Search를 사용하여 일반 및 혼합 문자를 처리하고, OCR 이미지 검색을 최적화하며, legal case
  number 검색을 개선하는 맞춤 검색 인덱스 Java를 생성합니다.
keywords:
- custom search index java
- GroupDocs.Search Java
- character recognition java
- OCR search Java
- search library Java
lastmod: '2026-11-02'
og_description: GroupDocs.Search를 사용하여 일반 및 혼합 문자를 처리하고, OCR 이미지 검색을 최적화하며, legal
  case number 검색을 개선하는 맞춤 검색 인덱스 Java를 생성합니다.
og_image_alt: Guide showing custom search index creation in Java with GroupDocs.Search
og_title: GroupDocs.Search와 함께 맞춤 검색 인덱스 Java 만들기
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Create a custom search index java using GroupDocs.Search to handle
    regular and blended characters, optimize OCR image search, and improve legal case
    number retrieval.
  headline: Create a custom search index java with GroupDocs.Search
  type: TechArticle
- questions:
  - answer: It means configuring an index to treat specific symbols as letters or
      blended characters, rather than ignoring them.
    question: What does “create custom search index” mean?
  - answer: GroupDocs.Search for Java (v25.4 at the time of writing).
    question: Which library is used?
  - answer: A free trial works for development; a paid license is required for production.
    question: Do I need a license?
  - answer: Yes—GroupDocs.Search supports OCR on images and PDFs when properly configured.
    question: Can I index both PDFs and images?
  - answer: Maven is the recommended way to manage dependencies, but you can also
      use Gradle or manual JARs.
    question: Is Maven required?
  type: FAQPage
tags:
- custom search index
- GroupDocs.Search
- Java OCR
- character recognition
- search library
title: GroupDocs.Search와 함께 맞춤 검색 인덱스 Java 만들기
type: docs
url: /ko/java/ocr-image-search/groupdocs-search-java-character-recognition/
weight: 1
---

# GroupDocs.Search로 사용자 정의 검색 인덱스 java 만들기

현대의 문서 중심 애플리케이션에서는 하이픈, 언더스코어, 언어별 기호와 같은 텍스트의 미묘한 차이를 고려한 **custom search index java**를 만드는 것이 빠르고 정확한 검색을 위해 필수적입니다. 이 튜토리얼에서는 **GroupDocs.Search for Java**에서 문자 인식을 구성하는 방법을 안내하며, 일반 문자(문자, 숫자, 언더스코어)와 혼합 문자(예: 하이픈)를 모두 다룹니다. 마지막까지 진행하면 OCR 또는 이미지 검색 시나리오에 정확히 맞는 인덱스를 맞춤 설정할 수 있으며, 법적 사건 번호, 소스 코드 저장소, 다국어 PDF 등을 인덱싱할 수 있습니다.

## 빠른 답변
- **“create custom search index”는 무엇을 의미합니까?** 이는 인덱스를 구성하여 특정 기호를 무시하지 않고 문자 또는 혼합 문자로 취급하도록 하는 것을 의미합니다.  
- **어떤 라이브러리를 사용합니까?** GroupDocs.Search for Java (작성 시점 v25.4).  
- **라이선스가 필요합니까?** 개발에는 무료 체험판을 사용할 수 있으며, 프로덕션에는 유료 라이선스가 필요합니다.  
- **PDF와 이미지를 모두 인덱싱할 수 있습니까?** 예—GroupDocs.Search는 적절히 구성하면 이미지와 PDF에 대한 OCR을 지원합니다.  
- **Maven이 필요합니까?** Maven은 의존성을 관리하는 권장 방법이지만, Gradle이나 수동 JAR도 사용할 수 있습니다.

## custom search index java란 무엇입니까?
**custom search index java**는 문자, 숫자 또는 혼합 기호로 취급되는 문자를 정의하여 형태를 지정할 수 있는 검색 가능한 데이터 구조입니다. 기본적으로 많은 기호가 무시되며, 이는 사건 번호(`2023-AB-456`)나 코드 스니펫(`my_variable`)과 같은 식별자 매칭 누락을 초래할 수 있습니다. 알파벳 사전을 조정하면 토큰화에 대한 완전한 제어가 가능해져 관련성이 높아지고 쿼리 실행 속도가 빨라집니다.

## 법적 사건 번호를 위해 일반 및 혼합 문자를 구성하는 이유는 무엇입니까?
하이픈과 슬래시를 혼합 문자로 처리하면 관련 토큰이 함께 유지되어 사건 번호, 제품 코드, 파일 경로와 같은 식별자가 원치 않게 분할되는 것을 방지합니다. 이 구성은 토큰 파편화를 줄여 **search index performance**를 최적화하고, 특히 구조화된 식별자에 크게 의존하는 법률 문서를 다룰 때 OCR 생성 콘텐츠의 관련성을 향상시킵니다.

## 전제 조건
- **JDK 8** 이상이 설치되어 있어야 합니다.  
- 의존성 관리를 위한 **Maven**.  
- **GroupDocs.Search for Java** 라이브러리에 접근할 수 있어야 합니다 (Maven 또는 공식 사이트를 통해 다운로드).

### 필요한 라이브러리 및 종속성
`pom.xml`에 저장소와 종속성 항목을 추가하십시오 (아래와 같이). XML 블록은 변경되지 않아야 합니다.

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

최신 JAR는 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 다운로드할 수 있습니다.

### 라이선스 획득
- **Free trial** – 초기 실험에 적합합니다.  
- **Temporary license** – 장기 개발 주기에 유용합니다.  
- **Production license** – 상업적 배포에 필요합니다.  

공식 포털에서 라이선스를 받으세요: [GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### 기본 초기화
아래 스니펫은 빈 인덱스를 시작하는 데 필요한 최소 코드를 보여줍니다. `Index` 클래스는 검색 가능한 데이터를 저장하고 관리하는 핵심 구성 요소입니다. 그대로 유지하십시오; 이후에 확장할 것입니다.

```java
import com.groupdocs.search.*;

public class GroupDocsSearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentFolder = "YOUR_DOCUMENT_DIRECTORY";

        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search setup completed!");
    }
}
```

## GroupDocs.Search for Java 설정

### Maven을 통한 설치
*Prerequisites* 섹션의 Maven 구성만 있으면 됩니다. 추가한 후 `mvn clean install`을 실행하여 바이너리를 가져오세요.

### 환경 설정 요구 사항
- **index folder**와 **document folder**가 디스크에 존재하는지 확인하십시오.  
- 절대 경로를 사용하거나 IDE가 상대 경로를 올바르게 해석하도록 구성하십시오.

## 구현 가이드

아래에서는 두 가지 별도 기능인 **regular characters**와 **blended characters**를 살펴봅니다. 각 기능은 동일한 패턴을 따릅니다—경로 정의, 인덱스 생성, 문자 사전 설정, 마지막으로 문서 인덱싱.

### 기능 1 – regular characters

#### 개요
regular characters는 독립 토큰으로 처리됩니다. 이는 숫자, 문자 및 언더스코어를 그대로 검색 가능하도록 할 때 이상적입니다.

#### 단계별 구현

**1️⃣ Set up paths**  
인덱스가 저장될 위치와 소스 문서가 위치한 경로를 정의합니다.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/RegularCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and configure index**  
인덱스를 인스턴스화하고 기존 알파벳 구성을 모두 초기화합니다.

```java
Index index = new Index(indexFolder);
index.getDictionaries().getAlphabet().clear();
```

**3️⃣ Define regular characters**  
숫자, 라틴 문자 및 언더스코어를 포함하는 문자 배열을 만듭니다.

```java
StringBuilder sb = new StringBuilder();
for (char i = 0x0030; i <= 0x0039; i++) { // Digits
    sb.append(i);
}
for (char i = 0x0041; i <= 0x005A; i++) { // Latin capital letters
    sb.append(i);
}
sb.append(0x005F); // Underscore
for (char i = 0x0061; i <= 0x007A; i++) { // Latin small letters
    sb.append(i);
}

// Convert to character array and set as alphabet range
char[] characters = new char[sb.length()];
sb.getChars(0, sb.length(), characters, 0);
index.getDictionaries().getAlphabet().setRange(characters, CharacterType.Letter);
```

**4️⃣ Index documents**  
소스 폴더의 모든 파일을 새로 구성된 인덱스에 추가합니다.

```java
index.add(documentFolder);
```

### 기능 2 – blended characters

#### 개요
blended characters(예: 하이픈)는 두 단어를 연결하는 경우가 많습니다. 이를 *blended*로 표시하면 인덱싱 시 엔진이 주변 토큰을 함께 유지합니다.

#### 단계별 구현

**1️⃣ Set up paths**  

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Indexing/CharacterTypes/BlendedCharacters";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

**2️⃣ Create and configure index**  

```java
Index index = new Index(indexFolder);
```

**3️⃣ Define blended characters**  
여기서는 하이픈을 blended character로 처리하도록 사전에 지정합니다.

```java
index.getDictionaries().getAlphabet().setRange(new char[] { '-' }, CharacterType.Blended);
```

**4️⃣ Index documents**  

```java
index.add(documentFolder);
```

## 실용적인 적용 사례

### 사용 사례 1 – 법률 문서 관리
법률 파일에는 종종 `2023-AB-456`와 같은 사건 번호가 포함됩니다. 언더스코어와 하이픈을 구성하면 식별자가 분할되지 않고 정확히 일치하는 검색 결과를 반환하여 **legal case numbers**를 효율적으로 검색할 수 있습니다.

### 사용 사례 2 – 소스 코드 저장소
개발자는 언더스코어(`my_variable`)와 하이픈(`my-function`)이 의미 있는 코드 스니펫을 검색해야 합니다. 맞춤 문자 인식은 검색 엔진이 이러한 기호를 존중하도록 보장합니다.

### 사용 사례 3 – 다국어 데이터셋
추가 알파벳을 사용하는 언어를 다룰 때, 해당 범위를 포함하도록 **Unicode 문자 집합을 확장**하면 정확한 다국어 검색 결과를 보장할 수 있습니다.

### 사용 사례 4 – PDF 이미지 인덱싱
스캔된 PDF나 이미지 파일을 인덱싱하는 경우 OCR 출력에 혼합 문자가 자주 포함됩니다. regular 및 blended characters를 적절히 구성하면 이미지 기반 콘텐츠에 대한 **search index** 성능이 최적화됩니다.

## 성능 고려 사항

- **Resource management** – 힙 사용량을 모니터링하십시오; 큰 인덱스는 증분 커밋으로 이점을 얻습니다.  
- **Garbage collection** – 작업이 끝나면 `Index` 객체를 해제하여 JVM이 메모리를 회수하도록 합니다.  
- **Index optimization** – 정기적으로 `index.optimize()`(가능한 경우)를 호출하여 인덱스를 압축하고 쿼리 속도를 향상시킵니다.  

## 결론

이제 GroupDocs.Search for Java를 사용하여 regular와 blended characters를 구분하는 **custom search index java**를 만드는 방법을 알게 되었습니다. 이러한 세밀한 제어를 통해 법률, 개발 또는 다국어 환경에 맞춘 OCR 인식 고성능 검색 솔루션을 구축할 수 있습니다.

### 다음 단계
- 비라틴 알파벳을 위한 추가 Unicode 범위를 실험해 보세요.  
- 문자 구성과 stemming 또는 synonyms와 같은 다른 GroupDocs.Search 기능을 결합하십시오.  
- REST API를 통해 인덱스를 노출하여 프런트엔드 애플리케이션이 HTTP를 통해 검색을 수행하도록 합니다.  

## 자주 묻는 질문

**Q:** *`CharacterType.Letter`의 목적은 무엇입니까?*  
**A:** 인덱스에 제공된 문자를 일반 문자로 취급하도록 알려 주어 인덱싱 시 별도로 토큰화됩니다.

**Q:** *동일한 인덱스에서 regular와 blended characters를 혼합할 수 있습니까?*  
**A:** 예—각 유형에 대해 `setRange`를 호출하면 사전이 두 구성을 동시에 처리합니다.

**Q:** *알파벳을 변경한 후 인덱스를 재구축해야 합니까?*  
**A:** 물론입니다. 문자 사전 변경은 토큰화에 영향을 미치므로 새로운 규칙을 적용하려면 문서를 다시 인덱싱해야 합니다.

**Q:** *정의할 수 있는 사용자 정의 문자 수에 제한이 있습니까?*  
**A:** 라이브러리는 전체 Unicode 범위를 지원하지만, 매우 큰 집합을 추가하면 성능이 저하될 수 있으므로 실제로 필요한 문자만 제한하십시오.

**Q:** *이것이 OCR 정확도에 어떤 영향을 줍니까?*  
**A:** 인덱스의 문자 집합을 OCR 엔진 출력과 맞추면 false negative을 줄이고 전체 검색 관련성을 향상시킵니다.

---

**마지막 업데이트:** 2026-11-02  
**Tested with:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## 관련 튜토리얼

- [Groupdocs Search Java 인덱스 생성 및 관리](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [검색 인덱스 디렉터리 생성 및 라이선스 설정 – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Java 전체 텍스트 검색 라이브러리 – GroupDocs.Search로 인덱스 최적화](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
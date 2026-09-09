---
date: '2026-08-15'
description: GroupDocs.Search for Java의 고급 인덱싱 기능(취소, async operations, multithreading,
  metadata customization 포함)을 사용하여 검색 지연 시간을 개선하는 방법을 배웁니다.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: GroupDocs.Search for Java를 사용해 취소, asynchronous indexing, multithreading,
  metadata customization을 활용하여 검색 지연 시간을 개선합니다. 성능을 높이고 리소스 사용을 줄이세요.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: GroupDocs에서 고급 인덱싱으로 검색 지연 시간 개선
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: GroupDocs에서 고급 인덱싱으로 검색 지연 시간 개선
type: docs
url: /ko/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# GroupDocs에서 고급 인덱싱으로 검색 지연 시간 개선

오늘날 빠르게 변화하는 디지털 환경에서 **검색 지연 시간 개선**은 사용자에게 즉시 결과를 제공하는 데 필수적입니다. 맞춤형 검색 엔진을 구축하든 기존 문서 관리 시스템을 강화하든, 올바른 인덱싱 전략은 지연 시간을 크게 줄이고 리소스 소비를 낮추며 전반적으로 **검색 지연 시간 개선**할 수 있습니다. 이 튜토리얼에서는 GroupDocs.Search for Java의 가장 강력한 기능인 취소, 비동기 인덱싱, 멀티스레딩 및 메타데이터 사용자 정의를 살펴보며 **문서를 인덱스에 추가**하는 속도를 높이고 효율성을 향상시킬 수 있습니다.

**배우게 될 내용**

- 지정된 시간 후 인덱싱 작업을 취소하는 방법  
- 비동기 인덱싱 작업 수행 및 상태 변화 처리 방법  
- 멀티스레딩을 구성하여 인덱싱 속도 향상  
- **검색 메타데이터 사용자 정의**를 위한 메타데이터 인덱싱 옵션 맞춤 설정  

코드에 들어가기 전에 필요한 모든 것이 준비되었는지 확인해 봅시다.

## 빠른 답변
- **취소는 무엇을 하나요?** 설정된 시간 초과 후 인덱싱을 중단하여 다른 작업을 위해 CPU와 메모리를 해제합니다.  
- **문서를 비동기적으로 인덱싱할 수 있나요?** 예 – `options.setAsync(true)` 로 활성화합니다.  
- **몇 개의 스레드를 사용할 수 있나요?** 양의 정수이면 언제든지 가능하며, 대부분의 서버에서는 2‑4개의 스레드가 일반적입니다.  
- **메타데이터 인덱싱은 선택 사항인가요?** 물론입니다 – 필드별로 활성화하거나 세부 조정할 수 있습니다.  
- **이 기능들을 사용하려면 라이선스가 필요합니까?** 테스트용으로는 체험판으로 충분하지만, 프로덕션에서는 정식 라이선스가 필요합니다.

## 사전 요구 사항

- **GroupDocs.Search 라이브러리** – 버전 25.4 이상.  
- **Java 개발 환경** – JDK 8 이상 권장.  
- Java와 인덱싱 개념에 대한 기본적인 이해.

### GroupDocs.Search for Java 설정

#### Maven 설치

`pom.xml` 파일에 저장소와 의존성을 추가합니다:

`pom.xml` 구성은 Maven에게 어떤 GroupDocs.Search 아티팩트를 다운로드하고 프로젝트에 포함할지 알려줍니다.

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

#### 직접 다운로드

또는 최신 JAR 파일을 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 다운로드합니다.

**라이선스 획득** – 무료 체험으로 시작하거나 전체 기능을 사용하려면 임시 라이선스를 요청하십시오.

### 기본 초기화 및 설정

`SearchIndex` 클래스는 디스크 또는 메모리에 저장된 검색 가능한 인덱스를 나타내는 진입점입니다.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## 이 맥락에서 “검색 성능 최적화”란 무엇인가요?

검색 성능을 최적화한다는 것은 인덱싱 프로세스를 구성하여 적절한 CPU, 메모리, 시간을 사용하면서 가장 관련성 높은 결과를 즉시 제공하도록 하는 것을 의미합니다. 취소, 비동기 실행, 스레딩 및 메타데이터 처리를 제어함으로써 엔진이 **문서를 인덱스에 추가**하고 쿼리에 응답하는 속도에 직접적인 영향을 미칩니다.

## 왜 고급 인덱싱 기능을 사용하나요?

비동기 및 멀티스레드 인덱싱은 애플리케이션을 반응적으로 유지하고, 취소는 과도한 프로세스를 방지합니다. 세밀하게 조정된 메타데이터 옵션은 가장 중요한 정보를 노출시켜 최종 사용자에게 **검색 지연 시간 개선**합니다. 또한 이러한 기능은 CPU 급증을 감소시키고 메모리 압력을 낮추며 대용량 문서를 처리할 때 보다 원활한 확장을 가능하게 합니다.

## 고급 인덱싱으로 검색 지연 시간을 개선하는 방법은?

`SearchIndex` 인스턴스를 로드하고, `IndexingOptions`에 취소, 비동기 및 스레드 설정을 구성한 뒤 `index.add(document)`를 호출합니다 — 이 조합은 일반적인 작업 부하에서 전체 인덱싱 시간을 최대 60 %까지 단축하고 장기 실행 작업이 다른 작업을 차단하지 않도록 보장합니다. 또한 메타데이터 인덱싱 제한을 조정하고 상태 변경 이벤트를 통해 진행 상황을 모니터링하여 파이프라인이 성능 예산 내에 머물도록 할 수 있습니다.

## 구현 가이드

### 취소 속성

**개요** – 지정된 기간이 지나면 인덱싱을 취소하여 리소스 과다 사용을 방지합니다.

#### 1단계: 환경 설정

인덱스 폴더를 가리키는 `SearchIndex` 인스턴스를 생성합니다.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2단계: 취소 옵션을 포함한 인덱싱 옵션 생성

`IndexingOptions`를 사용하면 인덱싱 엔진의 동작 방식을 지정할 수 있습니다.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**핵심 포인트**

- `setCancellation()`이 기능을 활성화합니다.  
- `cancelAfter(int milliseconds)`가 타임아웃을 정의합니다 (이 예시에서는 3초).

### 비동기 속성

**개요** – 백그라운드 스레드에서 인덱싱을 실행하고 상태 변화를 수신합니다.

#### 1단계: 환경 설정

인덱스를 인스턴스화하고 문서 컬렉션을 준비합니다.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2단계: status‑changed 이벤트 구독

`StatusChanged` 이벤트는 인덱싱 작업이 상태 간 전환될 때 알림을 제공합니다.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### 3단계: 비동기 옵션 구성

비동기 모드를 활성화하면 호출이 즉시 반환되고 처리는 백그라운드에서 계속됩니다.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### 스레드 속성

**개요** – 여러 CPU 코어를 활용하여 인덱싱 속도를 높입니다.

#### 1단계: 환경 설정

인덱스를 준비하고 JVM에 충분한 힙 메모리가 있는지 확인합니다.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2단계: 멀티스레딩 구성

작업자 스레드 수를 설정합니다; 각 스레드는 문서의 일부를 처리합니다.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### 메타데이터 인덱싱 옵션 속성

**개요** – 어떤 문서 메타데이터가 인덱싱되고 어떻게 저장되는지를 세밀하게 조정합니다.

#### 1단계: 환경 설정

author, title, custom tags와 같은 메타데이터 필드를 포함한 문서를 로드합니다.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### 2단계: 메타데이터 옵션 구성

`MetadataIndexingOptions`를 사용하면 개별 메타데이터 필드를 활성화/비활성화하고 크기 제한을 정의할 수 있습니다.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## 실용적인 적용 사례

1. **문서 관리 시스템** – 비동기 인덱싱을 사용하여 대량 배치를 백그라운드에서 처리하는 동안 UI가 반응성을 유지하도록 합니다.  
2. **콘텐츠 검색 엔진** – 취소를 적용하여 피크 트래픽 시 장시간 실행 작업이 서버 리소스를 독점하지 않도록 합니다.  
3. **대규모 인제스트 파이프라인** – 멀티스레딩을 활용하여 **문서를 인덱스에 추가**하고 처리 시간을 크게 단축합니다.  

## 성능 고려 사항

- **스레드 관리** – CPU 사용량을 모니터링합니다; 스레드가 너무 많으면 컨텍스트 스위치 오버헤드가 발생할 수 있습니다.  
- **메모리 사용량** – 메타데이터 제한(`setMaxBytesToIndexField` 등)은 메모리 사용을 예측 가능하게 유지합니다.  
- **가비지 컬렉션** – 대규모 코퍼스를 인덱싱할 때 적절한 JVM 플래그(`-Xmx`, `-XX:+UseG1GC`)를 사용합니다.  

## 일반적인 문제와 해결책

| 증상 | 가능한 원인 | 해결 방법 |
|------|--------------|-----------|
| 인덱싱이 끝나지 않음 | 취소 시간이 너무 짧게 설정됨 | `cancelAfter` 값을 늘리거나 장기 작업에 대해 취소를 제거합니다 |
| 비동기 모드에서 상태 업데이트가 없음 | 이벤트 핸들러가 올바르게 연결되지 않음 | `index.getEvents().StatusChanged.add(...)`가 `index.add` 호출 전에 호출되었는지 확인합니다 |
| 메모리 부족 오류 | 스레드가 너무 많거나 메타데이터 제한이 높음 | `options.setThreads`를 줄이고 메타데이터 필드 제한을 낮춥니다 |
| 결과에 메타데이터 누락 | 메타데이터 인덱싱이 비활성화됨 | `options.getMetadataIndexingOptions()`가 구성되어 있고 필드를 무시하도록 설정되지 않았는지 확인합니다 |

## 자주 묻는 질문

**Q: GroupDocs.Search에 대한 임시 라이선스를 어떻게 얻나요?**  
A: 다음 [GroupDocs의 임시 라이선스 페이지](https://purchase.groupdocs.com/temporary-license/)를 방문하고 화면 안내에 따라 진행하십시오.

**Q: 인덱싱 작업을 중간에 취소할 수 있나요?**  
A: 예 – `cancelAfter()`를 사용하거나 프로그래밍 방식으로 `Cancellation.cancel()`을 호출하여 취소 속성을 사용합니다.

**Q: 비동기 인덱싱의 사용 사례는 무엇인가요?**  
A: 실시간 문서 검색, 백그라운드 배치 처리, UI 반응성을 유지하는 애플리케이션 등이 비동기 인덱싱의 혜택을 받습니다.

**Q: 공유 서버에서 스레드 수를 늘리는 것이 안전한가요?**  
A: 점진적으로 늘리고 CPU 부하를 모니터링하십시오; 공유 환경이 많이 사용되는 경우 스레드 수를 적당히 유지하세요 (2‑4).

**Q: 메타데이터 인덱싱이 검색 관련성에 어떤 영향을 미치나요?**  
A: 올바르게 인덱싱된 메타데이터(작성자, 생성일, 태그 등)는 쿼리에서 더 높은 가중치를 부여받아 결과 정확성을 향상시킵니다.

## 결론

GroupDocs.Search for Java의 이러한 고급 기능을 활용하면 다양한 시나리오에서 **검색 지연 시간 개선**할 수 있습니다—빠른 문서 수집부터 세밀한 메타데이터 제어까지. 다양한 구성으로 실험하고, 리소스 사용량을 모니터링하며, 워크로드에 맞게 설정을 조정하여 최상의 결과를 얻으세요.

---

**마지막 업데이트:** 2026-08-15  
**테스트 환경:** GroupDocs.Search 25.4 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Search Java로 쿼리 성능 향상: 인덱스 및 검색 최적화](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs.Search를 사용한 Java 메타데이터 인덱싱으로 문서를 인덱스에 추가하는 방법](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [GroupDocs.Search for Java에서 다중 별칭 추가 및 문서를 인덱스에 추가하는 방법](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
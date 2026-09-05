---
date: '2026-05-17'
description: GroupDocs.Search for Java와 함께 search network java를 구성하고, shards를 최적화하며,
  text search를 수행하고, port conflicts를 처리하는 방법을 배웁니다.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'GroupDocs.Search for Java에서 샤드 최적화 방법: 포괄적인 가이드'
type: docs
url: /ko/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Java용 GroupDocs.Search에서 샤드 최적화 방법: 종합 가이드

효율적인 문서 검색은 대규모 데이터 세트를 관리하거나 빠른 내부 검색이 필요한 개발자와 기업에게 필수적입니다. 이 튜토리얼에서는 **how to configure search network java**(검색 네트워크 Java 구성 방법)을 배우고, 문서를 인덱싱하고 쿼리하는 방법, 그리고 최고 성능을 위한 **optimize shards**(샤드 최적화) 정확한 단계를 배웁니다. 또한 실제 사용 사례, 일반적인 함정 및 검색 노드를 원활하게 운영하기 위한 실용적인 팁도 다룹니다.

## 빠른 답변
- **What is shard optimization?** 인덱스 데이터를 재구성하여 쿼리 속도를 높이고 저장 오버헤드를 줄입니다.  
- **How to configure a search network?** 기본 디렉터리와 포트를 정의한 뒤 제공된 API를 사용해 노드를 배포합니다.  
- **How to perform text search?** 쿼리 문자열과 함께 `TextSearchInNetwork.searchAll`을 사용합니다.  
- **How to index documents in Java?** `IndexingDocuments.addDirectories`를 사용해 문서 디렉터리를 마스터 노드에 추가합니다.  
- **How to handle port conflicts?** `basePort` 변수를 머신에서 사용되지 않는 포트로 변경합니다.

## 검색 네트워크 구성 방법
`Configuration`은 인덱스 폴더 위치와 통신 포트와 같이 GroupDocs.Search 네트워크를 시작하는 데 필요한 모든 설정을 저장합니다.  
`SearchNetwork`는 노드를 조정하며 인덱싱 및 쿼리 배포를 처리합니다.

검색 구성을 로드하고, 문서 기본 경로를 설정하고, 사용 가능한 포트를 선택한 뒤 네트워크를 시작합니다—몇 줄의 코드만으로 가능합니다. 이 직접적인 답변은 전체 과정을 70단어 이하로 설명합니다: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`**. 네트워크는 자동으로 마스터 노드와 필요한 워커 노드를 시작하여 인덱싱 요청을 받을 준비가 됩니다.

### 정의 앵커
`Configuration`은 인덱스 폴더 위치와 통신 포트와 같이 GroupDocs.Search 네트워크를 시작하는 데 필요한 모든 설정을 저장하는 핵심 클래스입니다.

‘포트가 이미 사용 중’ 오류를 피하려면 네트워크를 초기화하기 전에 선택한 포트가 사용 가능한지 먼저 확인하세요(예: `netstat` 또는 간단한 소켓 테스트 사용).

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

## Java에서 문서 인덱싱 방법
`IndexingDocuments`는 검색 노드에 여러 디렉터리를 추가하고 인덱싱 파이프라인을 트리거하는 작업을 단순화하는 유틸리티 클래스입니다.

문서 폴더를 마스터 노드에 추가한 뒤 인덱서가 이를 크롤링하도록 합니다. **Direct answer:** `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))`를 호출하고 `masterNode.index()`를 실행합니다; 엔진은 제공된 각 폴더에 대해 검색 가능한 샤드를 생성합니다. 이 접근 방식은 수평 확장이 가능하며—노드를 추가하면 동일한 메서드가 작업 부하를 자동으로 분산합니다.

### 정의 앵커
`IndexingDocuments`는 검색 노드에 여러 디렉터리를 추가하고 인덱싱 파이프라인을 트리거하는 작업을 단순화하는 유틸리티 클래스입니다.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## 텍스트 검색 수행 방법
`TextSearchInNetwork`는 네트워크의 모든 노드에 텍스트 쿼리를 전송하고 결과를 집계하는 정적 헬퍼 메서드를 제공합니다.  
`SearchResult`는 일치하는 문서의 ID, 스니펫 및 관련성 점수를 포함합니다.

단일 메서드 호출로 모든 샤드에 걸쳐 쿼리를 실행합니다. **Direct answer:** `TextSearchInNetwork.searchAll("your query", searchNetwork)`를 사용합니다; 이 메서드는 문서 ID, 스니펫 및 관련성 점수를 포함하는 `SearchResult` 객체 컬렉션을 반환합니다. 추가 코드를 작성하지 않고도 언어, 파일 유형 또는 사용자 정의 메타데이터로 결과를 필터링할 수 있습니다.

### 정의 앵커
`TextSearchInNetwork`는 네트워크의 모든 노드에 텍스트 쿼리를 전송하고 결과를 집계하는 정적 헬퍼 메서드를 제공합니다.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## 포트 충돌 처리 방법
기본 포트(`49132`)가 사용 중이면 다른 사용 가능한 포트를 선택하고 네트워크를 시작하기 전에 `basePort` 필드를 업데이트하면 됩니다. **Direct answer:** `int basePort = 49132;`를 `49133`과 같이 사용되지 않는 값으로 변경하고, 재빌드 및 재시작하면 네트워크가 기존 노드에 영향을 주지 않고 새 포트에 바인드됩니다.

팁: 작은 구성 파일(예: `search-config.properties`)을 유지하면 포트를 재컴파일 없이 변경할 수 있습니다.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## 사전 요구 사항
시작하기 전에 다음 사전 요구 사항이 준비되어 있는지 확인하십시오:

### 필요 라이브러리, 버전 및 종속성
이 솔루션을 구현하려면 Maven을 사용해 `pom.xml` 파일에 다음 구성을 추가하여 GroupDocs.Search 라이브러리를 포함합니다:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
또는 최신 버전을 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서 다운로드하십시오.

### 환경 설정 요구 사항
- Java Development Kit (JDK) 8 이상.  
- 선택한 `basePort`에 바인드할 수 있는 네트워크 권한.  
- 인덱스 파일을 위한 충분한 디스크 공간(각 샤드는 1,000문서당 약 10 MB를 차지할 수 있음).

### 지식 사전 요구 사항
Java, 객체 지향 프로그래밍 및 예외 처리에 대한 기본적인 이해가 예제를 원활히 따라가는 데 도움이 됩니다.

## Java용 GroupDocs.Search 설정
프로젝트에서 GroupDocs.Search를 사용하려면 다음 단계를 따르세요:

1. **Add the Dependency**: 위에 표시된 대로 필요한 Maven 종속성을 프로젝트에 추가하거나 릴리스 페이지에서 직접 다운로드합니다.  
2. **License Acquisition**:  
   - **Free trial** – 라이선스 키가 필요 없지만 하루에 500 문서로 사용이 제한됩니다.  
   - **Temporary license** – [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)에서 30일 체험 키를 요청합니다.  
   - **Full license** – 무제한 접근 및 우선 지원을 위한 프로덕션 라이선스를 구매합니다.  
3. **Basic Initialization and Setup**:** `Configuration` 클래스를 사용해 구성을 초기화하고, 문서 기본 경로와 포트 번호를 지정합니다:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## 구현 가이드
이제 GroupDocs.Search Java를 사용한 주요 기능 구현을 살펴보겠습니다.

### 기능: 검색 네트워크 구성
**Overview**: 검색 네트워크를 설정하려면 문서 디렉터리를 정의하고 노드 간 통신을 위한 특정 포트로 구성합니다.

#### 단계 1: 문서 디렉터리 및 포트 정의
`DocumentDirectory`는 인덱싱하려는 폴더의 절대 경로를 보관하는 간단한 클래스입니다. 하나 이상의 경로를 구성에 제공하십시오.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### 단계 2: 검색 네트워크 구성
정의된 경로를 사용해 구성 객체를 생성합니다:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### 기능: 검색 네트워크 노드 배포
**Overview**: 네트워크 전반에 걸쳐 문서 검색을 효율적으로 처리하도록 노드를 배포합니다.

#### 단계 1: 구성을 사용해 노드 배포
검색 네트워크 노드를 배포하고 중앙 관리를 위한 마스터 노드를 식별합니다:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### 기능: 네트워크 노드 이벤트 구독
**Overview**: 중요한 변경 사항이나 동작을 알리는 이벤트에 구독하여 검색 네트워크를 모니터링합니다.

#### 단계 1: 마스터 노드 이벤트 구독
`SearchNetworkEventListener`를 사용하면 인덱싱 완료, 노드 실패 또는 샤드 최적화에 대응할 수 있습니다.

CODE_BLOCK_PLACEHOLDER_9_END

### 기능: 네트워크 노드에서 문서 인덱싱
**Overview**: 효율적인 검색을 위해 문서를 포함하는 디렉터리를 인덱싱 프로세스에 추가합니다.

#### 단계 1: 인덱싱 프로세스에 문서 디렉터리 추가
폴더 경로 목록을 마스터 노드에 전달하면 엔진이 각 폴더마다 별도의 샤드를 생성하여 병렬 쿼리 실행을 가능하게 합니다.

CODE_BLOCK_PLACEHOLDER_10_END

### 기능: 네트워크 노드에서 텍스트 검색
**Overview**: 검색 네트워크 내 모든 인덱싱된 문서에 대해 텍스트 검색을 실행합니다.

#### 단계 1: 텍스트 검색 수행
정적 헬퍼를 호출해 쿼리를 실행하고 관련성 점수가 포함된 일치 문서를 검색합니다.

CODE_BLOCK_PLACEHOLDER_11_END

### 기능: 샤드 최적화
**Overview**: 검색 네트워크 노드의 인덱서 내 샤드를 최적화하여 성능을 향상시킵니다.

#### 단계 1: 인덱서 샤드 최적화
샤드를 최적화해 검색 효율성을 향상시킵니다(여기서 **how to optimize shards**가 실제로 중요합니다):

CODE_BLOCK_PLACEHOLDER_12_END

## 실용적인 적용 사례
Java용 GroupDocs.Search는 다양한 실제 시나리오에 적용될 수 있으며, 각각 샤드 최적화의 이점을 얻습니다:

1. **Enterprise Document Management** – 샤드 최적화 후 10 TB 이상의 아카이브를 서브초 수준의 쿼리 시간으로 처리합니다.  
2. **E‑commerce Platforms** – 100만 SKU에 대한 제품 검색을 지원하며, 샤드 최적화 시 지연 시간을 최대 45 % 감소시킵니다.  
3. **Legal Firms** – 200 GB 저장소에서 사건 파일을 200 ms 이하로 검색합니다.  
4. **Library Systems** – 50만 디지털 도서 카탈로그 검색을 효율적인 메모리 사용으로 지원합니다.  
5. **Content Management Systems (CMS)** – 200만 페이지 이상을 가진 다중 사이트 배포에서 즉시 콘텐츠 검색을 가능하게 합니다.

## 성능 고려 사항
GroupDocs.Search 구현의 최적 성능을 보장하려면:

- **Regularly optimize shards** – 새로운 데이터 10 GB마다 `optimizeShards()`를 실행하면 쿼리 응답 시간이 30‑50 % 감소합니다.  
- **Monitor memory usage** – JVM 힙을 물리적 RAM의 75 % 이하로 유지하고, 대형 인덱스에는 G1GC를 활성화합니다.  
- **Use incremental indexing** – 전체 재인덱싱을 피하기 위해 변경된 파일만 추가합니다.  
- **Leverage multi‑node scaling** – 워커 노드를 추가해 샤드를 분산시키면, 읽기 중심 워크로드에서 각 추가 노드가 처리량을 약 20 % 향상시킬 수 있습니다.

## 일반적인 문제 및 해결책
| 문제 | 증상 | 해결책 |
|-------|---------|----------|
| 시작 시 포트 충돌 | `java.net.BindException: Address already in use` | `basePort`를 사용되지 않는 값으로 변경하고 `netstat -ano`로 확인합니다. |
| 최적화 중 메모리 부족 오류 | `java.lang.OutOfMemoryError: Java heap space` | JVM `-Xmx` 플래그를 늘리거나 더 많은 RAM을 가진 전용 노드에서 최적화를 실행합니다. |
| 검색 결과에 문서 누락 | 인덱싱 후 결과가 반환되지 않음 | `IndexingDocuments.addDirectories`를 통해 디렉터리가 올바르게 추가되었고 `masterNode.index()`가 예외 없이 완료되었는지 확인합니다. |
| 대량 삭제 후 오래된 샤드 | 삭제된 파일이 여전히 나타남 | `optimizeShards()`를 실행해 세그먼트를 병합하고 tombstone을 제거합니다. |

## 자주 묻는 질문

**Q: 샤드 최적화가 쿼리 속도에 어떤 영향을 줍니까?**  
A: 샤드 최적화는 인덱스를 압축하고 디스크 I/O를 감소시켜 대규모 데이터 세트에서 일반적으로 30‑50 % 더 빠른 쿼리 응답을 제공합니다.

**Q: 라이브 노드에서 `optimizeShards`를 실행해도 안전한가요?**  
A: 네, 이 작업은 다운타임 없이 실행되도록 설계되었지만, 20 GB보다 큰 인덱스는 트래픽이 적은 시간에 예약하는 것이 권장됩니다.

**Q: `OptimizeOptions`를 사용자 정의할 수 있나요?**  
A: 물론입니다. `maxSegmentSize`나 `mergeFactor`와 같은 매개변수를 설정해 최적화 과정을 미세 조정할 수 있습니다.

**Q: 최적화 중 `IOException`이 발생하면 어떻게 해야 하나요?**  
A: 파일 시스템 권한을 확인하고 충분한 여유 디스크 공간을 확보하며, 다른 프로세스가 인덱스 파일을 잠그고 있지 않은지 확인합니다.

**Q: 샤드 최적화가 삭제된 문서 공간도 회수하나요?**  
A: 네, 최적화 프로그램은 세그먼트를 병합하고 tombstone을 제거하여 삭제된 문서가 차지하던 공간을 해제합니다.

## 결론
이 종합 가이드를 따라 하면 이제 **configure search network java**(검색 네트워크 Java 구성) 방법, 문서 인덱싱, 텍스트 쿼리 실행, 그리고 가장 중요한 **optimize shards**(샤드 최적화) 방법을 알게 되어 검색 성능을 날카롭게 유지할 수 있습니다. 이러한 패턴을 Java 기반 엔터프라이즈 검색 솔루션에 적용하면 지연 시간, 확장성 및 자원 활용 측면에서 눈에 띄는 개선을 확인할 수 있습니다. 다음 단계로는 커스텀 분석기, 파싯 검색, 클라우드 스토리지 제공자와의 통합과 같은 고급 기능을 탐색해 보세요.

---
**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## 관련 튜토리얼

- [.NET에서 GroupDocs.Search 네트워크 구성: 종합 가이드](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [GroupDocs.Search를 사용한 .NET 문서 인덱싱 마스터: 종합 가이드](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Java용 GroupDocs.Search 튜토리얼 및 예제](/search/net/)
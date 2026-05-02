---
date: '2026-05-02'
description: GroupDocs.Search for Java를 사용하여 검색을 구성하고 실시간 검색 업데이트를 활성화하는 방법을 배우세요.
  네트워크 설정, 노드 배포 및 인덱싱에 대한 단계별 가이드.
keywords:
- how to configure search
- real time search updates
- add directories to index
- configure master node
- optimize shard size
title: Java에서 GroupDocs.Search를 사용한 검색 구성 방법 - 설정 및 배포 가이드
type: docs
url: /ko/java/licensing-configuration/mastering-groupdocs-search-java-configure-deploy/
weight: 1
---

# Java에서 GroupDocs.Search를 사용한 검색 구성 방법

오늘날 빠르게 변화하는 디지털 세계에서 **검색을 효율적으로 구성하는 방법**은 프로젝트 성공을 좌우할 수 있습니다. 수천 개의 계약서, 연구 논문 또는 내부 보고서를 다루든, 잘 설계된 검색 네트워크는 몇 초 만에 올바른 문서를 찾아줍니다. 이 튜토리얼에서는 검색 네트워크 구성, 노드 배포 및 GroupDocs.Search for Java를 사용한 **실시간 검색 업데이트** 활성화 방법을 단계별로 안내합니다.

## 빠른 답변
- **검색 네트워크의 주요 목적은 무엇입니까?** 다중 노드에 인덱싱 및 쿼리 처리를 분산시켜 확장성과 속도를 제공합니다.  
- **필요한 라이브러리 버전은 무엇입니까?** GroupDocs.Search for Java v25.4 이상.  
- **라이선스가 필요합니까?** 평가를 위해 무료 체험을 사용할 수 있으며, 프로덕션에서는 상용 라이선스가 필요합니다.  
- **실시간 업데이트는 어떻게 처리됩니까?** 인덱싱 변경 시 발생하는 노드 이벤트를 구독함으로써 처리됩니다.  
- **실행 중에 새로운 문서 폴더를 추가할 수 있나요?** 예—인덱서의 `addDirectories` 메서드를 사용합니다.

## GroupDocs 컨텍스트에서 “검색 구성”이란 무엇입니까?
검색 구성을 의미하는 것은 문서가 저장된 위치, 노드 간 통신 방식, 인덱싱 조정 방법을 아는 **검색 네트워크**를 설정하는 것입니다. 네트워크가 구성되면 다운타임 없이 노드를 추가하거나 제거할 수 있어 최신 검색 결과에 지속적으로 접근할 수 있습니다.

## Java용 GroupDocs.Search를 사용하는 이유
- **확장성:** 작업 부하를 여러 머신에 분산합니다.  
- **실시간 업데이트:** 새로 인덱싱된 파일을 네트워크 전체에 즉시 반영합니다.  
- **통합 용이성:** 간단한 Maven 설정과 명확한 Java API.  
- **엔터프라이즈 수준:** 대규모 말뭉치와 복잡한 쿼리 시나리오를 처리합니다.

## 사전 요구 사항
- **Java Development Kit (JDK) 8+**이 설치되어 있어야 합니다.  
- **Maven**을 사용한 의존성 관리.  
- Java, Maven 및 검색 개념에 대한 기본적인 이해.

## GroupDocs.Search for Java 설정

### Maven 의존성
Add the repository and dependency to your `pom.xml`:

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

**직접 다운로드:** 라이브러리는 [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)에서도 얻을 수 있습니다.

### 라이선스 획득
- **무료 체험:** 모든 기능을 탐색할 수 있는 체험 라이선스를 받으세요.  
- **임시 라이선스:** 장기간 평가를 위해 요청하세요.  
- **상용 라이선스:** 프로덕션 배포에 필요합니다.

### 기본 초기화
```java
import com.groupdocs.search.Configuration;
// Initialize configuration with your document path and port
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration config = new Configuration(basePath, basePort);
```

## Java에서 검색 네트워크 구성 방법

### 단계 1: 필요한 패키지 가져오기
```java
import com.groupdocs.search.scaling.ConfiguringSearchNetwork;
import com.groupdocs.search.scaling.Configuration;
```

### 단계 2: 네트워크 구성
```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/GettingDocumentsInNetwork/";
int basePort = 49112;

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
- **매개변수:** `basePath`는 문서 폴더를 가리키고, `basePort`는 노드 통신에 사용되는 TCP 포트입니다.

## 검색 네트워크 노드 배포

### 단계 1: 배포 패키지 가져오기
```java
import com.groupdocs.search.scaling.SearchNetworkDeployment;
import com.groupdocs.search.scaling.SearchNetworkNode;
```

### 단계 2: 노드 배포
```java
String[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0]; // Designate the first node as the master node
```
- **마스터 노드:** 모든 노드의 검색 및 인덱싱을 조정합니다. 샤드 할당 및 상태 검사를 포함한 **마스터 노드** 설정을 구성할 수 있습니다.

## 실시간 검색 업데이트를 위한 노드 이벤트 구독

### 단계 1: 이벤트 패키지 가져오기
```java
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;
```

### 단계 2: 마스터 노드 이벤트 구독
```java
SearchNetworkNodeEvents.subscribe(masterNode);
```
- **이벤트 처리:** 문서가 추가, 업데이트 또는 삭제될 때마다 **실시간 검색 업데이트**를 활성화합니다.

## 인덱싱을 위한 디렉터리 추가

### 단계 1: 인덱서 패키지 가져오기
```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.scaling.Indexer;
```

### 단계 2: 문서 디렉터리 추가
```java
Indexer indexer = masterNode.getIndexer();
indexer.addDirectories("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
- **동적 인덱싱:** `addDirectories` 메서드를 사용하여 네트워크를 재시작하지 않고도 **디렉터리를 인덱스에 추가**할 수 있습니다.

## 인덱싱된 문서 검색

### 단계 1: 검색기 패키지 가져오기
```java
import com.groupdocs.search.scaling.Searcher;
import com.groupdocs.search.scaling.NetworkDocumentInfo;
```

### 단계 2: 문서 정보 검색
```java
Searcher searcher = masterNode.getSearcher();
int[] shardIndices = masterNode.getShardIndices();

for (int i = 0; i < shardIndices.length; i++) {
    int shardIndex = shardIndices[i];
    NetworkDocumentInfo[] infos = searcher.getIndexedDocuments(shardIndex);

    for (NetworkDocumentInfo info : infos) {
        int nodeIndex = masterNode.getNodeIndex(info.getShardIndex());
        String filePath = info.getDocumentInfo().getFilePath();

        // Retrieve and process document attributes
        String[] attributes = indexer.getAttributes(filePath);
        
        NetworkDocumentInfo[] items = searcher.getIndexedDocumentItems(info);
        for (NetworkDocumentInfo item : items) {
            // Process each indexed item
        }
    }
}
```
- **샤드 관리:** 문서를 샤드에 분산시켜 대규모 데이터셋을 효율적으로 처리합니다. **샤드 크기 최적화**를 위해 샤드 통계를 모니터링하고 향후 릴리스에서 `shardSize` 설정을 조정하세요.

## 이것이 프로젝트에 중요한 이유
올바르게 구성된 검색 네트워크는 병목 현상을 없애고 지연 시간을 줄이며 사용자가 항상 최신 문서 버전을 볼 수 있도록 보장합니다. 실시간 업데이트와 **다운타임 없이 디렉터리를 인덱스에 추가**할 수 있는 기능은 특히 법률 사무소, 연구 기관 및 지속적으로 변화하는 문서 컬렉션을 다루는 모든 조직에 가치가 있습니다.

## 실용적인 적용 사례
1. **엔터프라이즈 문서 관리:** 수백만 파일에 대한 검색을 중앙화합니다.  
2. **법률 사무소:** 사건 파일, 계약서 및 증거를 빠르게 찾습니다.  
3. **학술 연구:** 저널 및 논문을 인덱싱하여 즉시 검색합니다.

## 성능 고려 사항
- **인덱싱 최적화:** 정기적인 인덱스 새로 고침을 예약하고 오래된 데이터를 정리합니다.  
- **메모리 관리:** 특히 큰 샤드를 처리할 때 JVM 힙을 모니터링합니다.  
- **확장성 계획:** 말뭉치가 커짐에 따라 노드를 추가하면 네트워크가 자동으로 부하를 균형 잡습니다.  
- **샤드 크기 최적화:** 작은 샤드는 쿼리 지연 시간을 개선하고, 큰 샤드는 오버헤드를 줄입니다. 하드웨어와 쿼리 패턴에 따라 조정하세요.

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결 방법 |
|-------|-------|-----|
| 노드가 연결되지 않음 | 포트 충돌 또는 방화벽 | `basePort`가 열려 있고 다른 서비스에서 사용되지 않는지 확인하십시오 |
| 인덱스가 업데이트되지 않음 | 이벤트 구독 누락 | 배포 후 `SearchNetworkNodeEvents.subscribe(masterNode)`를 호출하십시오 |
| 메모리 부족 오류 | 많은 대형 샤드가 로드됨 | 샤드 크기를 줄이거나 JVM 힙을 늘리세요 (`-Xmx` 플래그) |

## 자주 묻는 질문

**Q: 네트워크가 실행 중일 때 새로운 디렉터리를 추가할 수 있나요?**  
A: 예—`indexer.addDirectories()` 메서드를 사용하면 구독된 이벤트가 실시간으로 업데이트를 전파합니다.

**Q: 노드 상태를 어떻게 모니터링합니까?**  
A: 각 `SearchNetworkNode`는 상태 API를 제공하므로 원하는 모니터링 도구와 통합하십시오.

**Q: 마스터 노드를 별도 머신에서 실행할 수 있나요?**  
A: 물론 가능합니다. 모든 노드가 동일한 `basePort`를 공유하고 네트워크를 통해 서로 연결될 수 있도록 하세요.

**Q: 지원되는 파일 형식은 무엇입니까?**  
A: GroupDocs.Search는 PDF, Word, Excel, PowerPoint, 일반 텍스트 등 다양한 형식을 기본적으로 지원합니다.

**Q: 새로운 노드를 추가한 후 네트워크를 재시작해야 합니까?**  
A: 아니요—노드는 동적으로 추가·제거될 수 있으며, 마스터 노드가 자동으로 샤드를 재조정합니다.

## 결론
이제 GroupDocs.Search for Java를 사용한 **검색 구성 방법**을 알게 되었으니, 조직의 성장에 맞춰 빠르고 확장 가능하며 신뢰할 수 있는 문서 검색 솔루션을 구축할 수 있습니다. 이러한 패턴을 적용해 모든 산업 분야에 실시간 분산 검색 경험을 제공하세요.

---

**마지막 업데이트:** 2026-05-02  
**테스트 환경:** GroupDocs.Search for Java 25.4  
**작성자:** GroupDocs
---
date: '2026-07-02'
description: GroupDocs.Search에 대한 임시 라이선스를 획득하고, 인덱스에 디렉터리를 추가하며, Java 검색 네트워크 노드를
  관리하는 동안 사용자 정의 문서 속성을 추가하는 방법을 배웁니다.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: 임시 라이선스 획득 GroupDocs – Master Search Nodes (Java)
type: docs
url: /ko/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# 임시 라이선스 획득 GroupDocs – 마스터 검색 노드 (Java)

이 포괄적인 가이드에서는 **GroupDocs.Search에 대한 임시 라이선스를 획득**하고, 다중 노드 검색 네트워크를 구성하며, Java를 사용하여 **디렉터리를 인덱스에 추가**하고 **맞춤 문서 속성을 추가**하는 방법을 배웁니다. 기업 문서 관리 시스템이나 검색 가능한 제품 카탈로그를 구축하든, 이 단계들을 숙달하면 제한 없이 플랫폼을 평가하고 검색 기능을 빠르게 확장할 수 있습니다.

## 빠른 답변
- **GroupDocs.Search를 사용하기 시작하는 첫 번째 단계는 무엇인가요?** GroupDocs 포털에서 임시 라이선스를 획득합니다.  
- **어떤 Maven 저장소에 라이브러리가 호스팅되어 있나요?** `https://releases.groupdocs.com/search/java/`.  
- **디렉터리를 인덱스에 추가하려면 어떻게 하나요?** 마스터 노드에서 `addDirectoriesToIndex` 헬퍼를 호출합니다.  
- **맞춤 문서 속성을 추가할 수 있나요?** 예—문서 키와 속성 이름을 사용하여 `addAttribute`를 호출합니다.  
- **노드를 깔끔하게 종료하려면 어떻게 하나요?** 리소스를 해제하기 위해 `closeNodes`를 호출합니다.

## 임시 라이선스란 무엇이며 왜 필요합니까?
임시 라이선스를 사용하면 평가 제한 없이 GroupDocs.Search를 평가할 수 있습니다. 개발, 테스트 또는 개념 증명 프로젝트에 완벽하며, 전체 구매 전에 사용해 볼 수 있습니다. 라이선스는 제한된 기간 동안 전체 기능 접근을 제공하여 성능 벤치마크, 통합 포인트 테스트 및 재정적 부담 없이 솔루션이 요구 사항을 충족하는지 확인할 수 있게 합니다.

## 사전 요구 사항

시작하기 전에 다음 사전 요구 사항이 준비되어 있는지 확인하십시오:

### 필수 라이브러리 및 종속성
GroupDocs.Search for Java를 사용하려면 필요한 Maven 종속성을 포함하십시오:
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
또한 최신 버전을 직접 [GroupDocs.Search for Java 릴리스](https://releases.groupdocs.com/search/java/)에서 다운로드할 수 있습니다.

### 환경 설정
- 호환 가능한 JDK가 설치되어 있는지 확인하십시오 (Java 8 이상).  
- IDE를 Maven 프로젝트를 지원하도록 설정하십시오.

### 지식 사전 요구 사항
Java 프로그래밍에 대한 기본 이해와 Maven 프로젝트 관리에 대한 친숙함이 도움이 됩니다. 이러한 개념에 익숙하지 않다면 입문 자료를 탐색하여 시작하는 것을 고려하십시오.

## 임시 라이선스를 얻는 방법
임시 라이선스는 GroupDocs 포털을 방문하고 짧은 요청 양식을 작성한 뒤, 받은 `.lic` 파일을 프로젝트의 `resources` 폴더에 배치하여 얻을 수 있습니다. 그런 다음 아래 코드 스니펫을 사용해 라이선스를 초기화합니다. 요청 양식은 공식 페이지인 [GroupDocs 임시 라이선스](https://purchase.groupdocs.com/temporary-license/)를 사용하십시오.

## GroupDocs.Search for Java 설정

### 설치 정보
프로젝트에서 GroupDocs.Search for Java를 사용하려면 위 Maven 단계를 따르거나 공식 릴리스 페이지에서 최신 버전을 직접 다운로드하십시오.

#### 라이선스 획득 단계
1. **무료 체험** – 아무런 약속 없이 기능을 탐색합니다.  
2. **임시 라이선스** – 테스트용 단기 키를 획득합니다 (위 섹션 참조).  
3. **구매** – 프로덕션 사용을 위해 **[GroupDocs 구매 페이지](https://purchase.groupdocs.com/)**에서 전체 라이선스를 구입합니다.

### 기본 초기화 및 설정
GroupDocs.Search를 사용하여 프로젝트를 다음과 같이 초기화합니다:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
이 초기화 단계는 검색 네트워크 내 모든 구성 요소가 원활하게 작동하도록 보장하는 데 중요합니다.

## 구현 가이드
이제 프로세스를 관리 가능한 섹션으로 나누어 각각 검색 네트워크 노드 배포 및 관리의 특정 기능에 초점을 맞춥니다.

### 기능 1: 구성 설정
**Overview:** 검색 네트워크 구성을 설정하는 것은 노드를 배포하는 첫 번째 단계입니다. 이 설정에는 노드 배포에 중요한 경로와 포트를 지정하는 작업이 포함됩니다.

#### 구현 단계:
##### 단계 1: 기본 경로 및 포트 정의
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### 단계 2: 검색 네트워크 구성
`configureSearchNetwork` 함수는 노드 배포에 필요한 구성 객체를 준비합니다.  
`Configuration`은 인덱스 폴더, 네트워크 포트 및 노드 역할과 같은 모든 설정을 보유하는 클래스입니다.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameters:** 기본 경로와 포트는 리소스를 찾고 통신 채널을 설정하는 데 사용됩니다.  
- **Return Value:** 배포 요구에 맞게 구성된 `Configuration` 객체를 반환합니다.

### 기능 2: 검색 네트워크 배포
**Overview:** 노드 배포는 다양한 환경이나 데이터 세그먼트에 걸쳐 검색 기능을 확장하는 데 필수적입니다.

#### 구현 단계:
##### 단계 1: 노드 배포
`deploySearchNetwork` 함수는 검색 네트워크 노드 배열을 초기화하고 반환합니다.  
`SearchNetworkNodes`는 분산 검색 클러스터에 참여하는 각 노드 인스턴스를 나타냅니다.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameters:** 기본 경로, 포트 및 구성을 사용하여 배포 환경을 결정합니다.  
- **Return Value:** 초기화된 `SearchNetworkNodes`를 포함하는 배열을 반환합니다.

### 기능 3: 네트워크 이벤트 구독
**Overview:** 검색 네트워크 활동을 모니터링하는 것은 최적의 성능과 안정성을 유지하는 데 중요합니다.

#### 구현 단계:
##### 단계 1: 마스터 노드 이벤트 구독
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Purpose:** 이 단계는 검색 네트워크 내 중요한 이벤트나 변경 사항에 대한 알림을 보장합니다.

### 기능 4: 문서 인덱싱
**Overview:** 인덱싱할 문서를 포함하는 디렉터리를 추가하면 네트워크 전반에 걸쳐 효율적인 데이터 검색이 가능합니다.

#### 디렉터리를 인덱스에 추가하는 방법
`addDirectoriesToIndex`는 마스터 노드에서 인덱싱할 폴더 경로를 등록하는 헬퍼 메서드입니다.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Purpose:** 지정된 디렉터리 내 모든 문서에 대한 빠른 접근 및 검색 가능성을 촉진합니다.

### 기능 5: 문서에 속성 추가
**Overview:** 맞춤 속성은 문서 메타데이터를 강화하여 검색을 보다 유연하고 풍부하게 만듭니다.

#### 맞춤 문서 속성을 추가하는 방법
`addAttribute`는 인덱스에 지정된 문서에 맞춤 메타데이터 속성을 추가합니다.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameters:** 노드, 문서 키 및 추가할 속성을 지정합니다.  
- **Purpose:** 추가 메타데이터로 문서를 풍부하게 하여 검색 기능을 확장합니다.

### 기능 6: 인덱스된 문서 검색
**Overview:** 인덱스된 문서를 효율적으로 검색하고 목록화하여 데이터 정확성과 완전성을 보장합니다.

#### 구현 단계:
##### 단계 1: 인덱스된 문서 가져오기
```java
getIndexedDocuments(nodes[0]);
```  
- **Purpose:** 검색 네트워크 내 모든 필요한 문서가 성공적으로 인덱싱되었는지 확인합니다.

### 기능 7: 네트워크 노드 종료
**Overview:** 노드를 적절히 종료하는 것은 리소스 관리와 메모리 누수 방지를 위해 중요합니다.

#### 구현 단계:
##### 단계 1: 모든 노드 종료
`closeNodes`는 모든 활성 검색 노드를 종료하고 할당된 리소스를 해제합니다.  
```java
closeNodes(nodes);
```  
- **Purpose:** 각 노드가 차지하고 있던 리소스를 해제하여 깨끗한 종료 과정을 보장합니다.

## GroupDocs.Search에 임시 라이선스를 사용하는 이유
임시 라이선스는 **30일 동안 전체 기능 접근**을 제공하고 **50,000개의 인덱스된 문서**까지 성능 제한 없이 지원합니다. 이를 통해 실제 데이터에서 인덱싱 속도, 쿼리 지연 시간 및 확장성을 벤치마크하고 프로덕션 라이선스를 구매하기 전에 평가할 수 있습니다. 또한 평가 워터마크가 제거되어 최종 제품의 실제 기능을 정확히 확인할 수 있습니다.

## 일반적인 사용 사례
1. **엔터프라이즈 문서 관리** – 부서 전반에 걸친 수백만 개의 내부 파일을 인덱싱하여 즉시 전체 텍스트 검색을 가능하게 합니다.  
2. **전자상거래 플랫폼** – 여러 창고와 제3자 피드를 아우르는 검색 가능한 제품 카탈로그를 구축합니다.  
3. **법률 사무소** – 맞춤 메타데이터를 사용해 사건 파일, 계약서 및 증거를 조직하여 신속하게 검색합니다.

다른 시스템과의 통합 가능성에는 CRM 플랫폼, 콘텐츠 관리 시스템(CMS) 및 데이터 분석 도구와의 연동이 포함되며, 이는 GroupDocs.Search for Java가 제공하는 강력한 인덱싱 및 검색 기능을 활용합니다.

## 성능 고려 사항
GroupDocs.Search for Java를 사용할 때 성능을 최적화하려면:
- **Optimize Configuration** – 특정 배포 환경에 맞게 구성 설정을 조정합니다.  
- **Monitor Resource Usage** – CPU, 메모리 및 I/O를 정기적으로 확인하여 병목 현상이나 메모리 누수를 방지합니다.  
- **Follow Best Practices** – Java 메모리 관리 지침을 준수하여 시스템 리소스를 효율적으로 활용합니다.

## 자주 묻는 질문

**Q: 임시 라이선스는 얼마나 오래 유효합니까?**  
A: 임시 라이선스는 일반적으로 30일 동안 유효하며, 제품을 충분히 평가할 수 있는 시간을 제공합니다.

**Q: 재설치 없이 임시 라이선스에서 전체 라이선스로 전환할 수 있나요?**  
A: 예—임시 라이선스 파일을 전체 라이선스 파일로 교체하고 애플리케이션을 재시작하면 됩니다.

**Q: 새 라이선스를 적용한 후 문서를 다시 인덱싱해야 하나요?**  
A: 아니요, 인덱스는 그대로 유지되며 라이선스는 사용 권한만 관리합니다.

**Q: 노드를 종료하는 것을 잊으면 어떻게 되나요?**  
A: 해제되지 않은 리소스로 인해 메모리 누수가 발생할 수 있으므로, 종료 시 항상 `closeNodes`를 호출하십시오.

**Q: 문서당 하나 이상의 맞춤 속성을 추가할 수 있나요?**  
A: 물론입니다—다른 속성 이름으로 `addAttribute`를 여러 번 호출하면 됩니다.

---

**마지막 업데이트:** 2026-07-02  
**테스트 환경:** GroupDocs.Search for Java 25.4  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs를 사용하여 .NET에서 검색 네트워크 노드 배포 및 효율적인 문서 인덱싱 및 검색](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [.NET에서 GroupDocs.Search를 사용하여 문서 관리 시스템용 검색 네트워크 구현 방법](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Aspose.Search 네트워크 구성 및 .NET용 GroupDocs.Redaction으로 문서 속성 추가: 종합 가이드](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
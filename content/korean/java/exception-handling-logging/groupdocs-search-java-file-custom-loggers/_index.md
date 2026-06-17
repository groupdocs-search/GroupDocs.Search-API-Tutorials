---
date: '2026-02-24'
description: GroupDocs.Search for Java에서 사용자 정의 로거를 생성하고, 최대 로그 크기를 설정하며, 콘솔 또는 파일
  로거를 구성하는 방법을 배워보세요.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: GroupDocs.Search Java를 사용하여 사용자 지정 로거를 만들고 로그 파일 크기를 제한하는 방법
type: docs
url: /ko/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search Java 로거로 로그 파일 크기 제한하기

이 가이드에서는 **custom logger** 구현을 만들고 GroupDocs.Search for Java를 사용할 때 **log file size**를 **limit**하는 방법을 배웁니다. 로그 증가를 제어하는 것은 대규모 문서 인덱싱에 필수이며, 기본 제공 로거를 사용하면 **set max log size**, **roll over log file**, 또는 **use console logger** 로 전환하여 즉시 피드백을 받을 수 있습니다. Maven 설정부터 검색 쿼리 실행까지 전체 설정 과정을 살펴보고, 로거가 적용된 상태에서 **add documents index** 하는 방법을 확인해 보겠습니다.

## Quick Answers
- **“limit log file size”가 무엇을 의미하나요?** 로그 파일의 최대 크기를 제한하여 디스크에 무제한으로 커지는 것을 방지합니다.  
- **limit log file size를 지원하는 로거는 무엇인가요?** 기본 제공 `FileLogger`는 최대 크기 매개변수를 받습니다.  
- **console logger java를 어떻게 사용하나요?** `ConsoleLogger`를 인스턴스화하고 `IndexSettings`에 설정합니다.  
- **GroupDocs.Search에 라이선스가 필요합니까?** 평가용으로는 체험판을 사용할 수 있지만, 프로덕션에서는 상용 라이선스가 필요합니다.  
- **첫 번째 단계는 무엇인가요?** Maven 프로젝트에 GroupDocs.Search 의존성을 추가합니다.  

## What is limit log file size?
로그 파일 크기 제한은 로거를 설정하여 파일이 미리 정의된 임계값(예: 4 MB)에 도달하면 더 이상 커지지 않거나 롤오버하도록 하는 것을 의미합니다. 이를 통해 애플리케이션의 저장소 사용량을 예측 가능하게 유지하고 성능 저하를 방지할 수 있습니다.

## Why use file and custom loggers with GroupDocs.Search?
- **감사 가능성:** 인덱싱 및 검색 이벤트의 영구 기록을 유지합니다.  
- **디버깅:** 간결한 로그를 검토하여 문제를 신속히 파악합니다.  
- **유연성:** 영구 파일 로그와 즉시 콘솔 출력(`use console logger`) 중에서 선택합니다.  

## Prerequisites
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 이상, IDE(IntelliJ IDEA, Eclipse 등).  
- 기본 Java 및 Maven 지식.  

## Setting Up GroupDocs.Search for Java

아래 방법 중 하나를 사용하여 라이브러리를 프로젝트에 추가합니다.

**Maven Setup:**

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

**Direct Download:**  
공식 사이트에서 최신 JAR를 다운로드합니다: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
체험판을 받거나 [licensing page](https://purchase.groupdocs.com/temporary-license/)에서 라이선스를 구매합니다.

## How to create custom logger for GroupDocs.Search
GroupDocs.Search는 `ILogger` 인터페이스의 구현을 플러그인 형태로 사용할 수 있게 합니다. `FileLogger` 또는 `ConsoleLogger`를 확장하면 로그 파일 롤오버나 원격 모니터링 서비스로 메시지를 전달하는 등 추가 동작을 구현할 수 있습니다. 이러한 유연성 때문에 많은 팀이 운영 요구에 맞는 **custom logger** 솔루션을 **create**합니다.

## How to limit log file size with File Logger
다음은 로그 파일이 지정한 크기를 초과하지 않도록 **file logger**를 **configure**하는 단계별 가이드입니다.

### 1️⃣ 필요한 패키지 가져오기
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ File Logger를 사용한 Index Settings 설정
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ 인덱스 생성 또는 로드
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ 인덱스에 문서 추가
```java
index.add(documentsFolder);
```

### 5️⃣ 검색 쿼리 수행
```java
SearchResult result = index.search(query);
```

**핵심 포인트:** `FileLogger` 생성자의 두 번째 인수(`4.0`)는 메가바이트 단위의 **set max log size**를 정의하며, **limit log file size** 요구사항을 직접 해결합니다.

## How to use console logger java
터미널에서 즉시 피드백을 원한다면 파일 로거를 콘솔 로거로 교체합니다.

### 1️⃣ Console Logger 가져오기
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Console Logger를 사용한 Index Settings 설정
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ 인덱스 생성 또는 로드
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ 문서 추가 및 검색 수행
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**팁:** 콘솔 로거는 개발 중에 이상적이며, 각 로그 항목을 즉시 출력해 인덱싱 및 검색이 예상대로 동작하는지 확인하는 데 도움이 됩니다.

## Practical Applications
1. **문서 관리 시스템:** 인덱싱된 모든 문서의 감사 추적을 유지합니다.  
2. **엔터프라이즈 검색 엔진:** 실시간으로 쿼리 성능 및 오류 비율을 모니터링합니다.  
3. **법률 및 컴플라이언스 소프트웨어:** 규제 보고를 위해 검색어를 기록합니다.

## Performance Considerations
- **로그 크기:** **set max log size**를 사용하면 애플리케이션을 느려지게 할 수 있는 과도한 디스크 사용을 방지합니다.  
- **비동기 로깅:** 더 높은 처리량이 필요하면 로거를 비동기 큐로 감싸는 것을 고려하세요(이 가이드 범위 외).  
- **메모리 관리:** 필요 없어진 큰 `Index` 객체를 해제하여 JVM 메모리 사용량을 낮게 유지합니다.

## Common Issues & Solutions
- **Log path not accessible:** 디렉터리가 존재하고 애플리케이션에 쓰기 권한이 있는지 확인합니다.  
- **Logger not firing:** `Index` 객체를 생성하기 *앞에* `settings.setLogger(...)`를 호출했는지 확인합니다.  
- **Console output missing:** `System.out`을 표시하는 터미널에서 애플리케이션을 실행하고 있는지 확인합니다.

## Frequently Asked Questions

**Q: `FileLogger`의 두 번째 매개변수는 무엇을 제어하나요?**  
A: 로그 파일의 최대 크기를 메가바이트 단위로 설정하며, 이를 통해 **set max log size**를 할 수 있습니다.

**Q: 파일 로거와 콘솔 로거를 함께 사용할 수 있나요?**  
A: 예, 메시지를 두 목적지 모두에 전달하는 custom logger를 만들어 사용할 수 있습니다.

**Q: 초기 생성 후에 인덱스에 문서를 추가하려면 어떻게 해야 하나요?**  
A: 언제든지 `index.add(pathToNewDocs)`를 호출하면 로거가 해당 작업을 기록합니다.

**Q: `ConsoleLogger`는 스레드‑안전한가요?**  
A: `System.out`에 직접 쓰며, JVM이 동기화하므로 대부분의 사용 사례에서 안전합니다.

**Q: 로그 파일 크기 제한이 저장되는 정보량에 영향을 미치나요?**  
A: 크기 제한에 도달하면 로거 구현에 따라 새 항목이 버려지거나 파일이 **roll over log file**될 수 있습니다.

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**마지막 업데이트:** 2026-02-24  
**테스트 환경:** GroupDocs.Search for Java 25.4  
**작성자:** GroupDocs  

---
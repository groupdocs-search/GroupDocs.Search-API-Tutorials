---
date: '2026-09-21'
description: GroupDocs.Search for Java에서 logger를 생성하고, max log size를 설정하며, console
  logger를 사용하는 방법을 배웁니다.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: GroupDocs.Search for Java에서 logger를 생성하고, max log size를 설정하며, console
  logger를 사용하는 방법을 배웁니다. step‑by‑step instructions와 best‑practice tips를 따라 보세요.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: GroupDocs.Search에서 logger를 생성하고 log size를 제한하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  headline: How to create logger and limit log size in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to create logger, set max log size, and use console logger
    in GroupDocs.Search for Java.
  name: How to create logger and limit log size in GroupDocs.Search for Java
  steps:
  - name: Create a class that implements `ILogger`.
    text: Create a class that implements `ILogger`.
  - name: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
    text: Override the `log` method to write messages to your chosen destination (file,
      database, HTTP endpoint).
  - name: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
    text: In the index configuration, call `settings.setLogger(new YourCustomLogger())`.
  - name: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
    text: '**Document management systems:** Keep audit trails of every document indexed,
      satisfying compliance requirements.'
  - name: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
    text: '**Enterprise search engines:** Monitor query performance and error rates
      in real time, enabling rapid SLA compliance checks.'
  - name: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
    text: '**Legal & compliance software:** Record search terms and timestamps for
      regulatory reporting, with logs retained for the mandated retention period.'
  type: HowTo
- questions:
  - answer: It sets the maximum size of the log file in megabytes, allowing you to
      **set max log size** and prevent uncontrolled growth.
    question: What does the second parameter of `FileLogger` control?
  - answer: Yes. Create a custom logger that forwards each `log` call to both a `FileLogger`
      and a `ConsoleLogger`, then register that composite logger with `IndexSettings`.
    question: Can I combine file and console loggers?
  - answer: Call `index.add(pathToNewDocs)` at any time; the configured logger will
      automatically record the addition.
    question: How do I add documents to the index after the initial creation?
  - answer: It writes directly to `System.out`, which the JVM synchronizes internally,
      making it safe for typical multi‑threaded use cases.
    question: Is `ConsoleLogger` thread‑safe?
  - answer: Once the size limit is hit, new entries are either discarded or the logger
      rolls over to a new file, depending on the implementation you choose.
    question: Will limiting the log file size affect the amount of information stored?
  type: FAQPage
tags:
- GroupDocs.Search
- Java logging
- custom logger
- file logger
- console logger
title: GroupDocs.Search for Java에서 logger를 생성하고 log size를 제한하는 방법
type: docs
url: /ko/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# GroupDocs.Search for Java에서 로거 생성 및 로그 파일 크기 제한 방법

이 튜토리얼에서는 GroupDocs.Search용 **로거 생성 방법** 구현, 최대 로그 파일 크기 설정, 파일 기반 로거와 콘솔 로거 간 전환 방법을 다룹니다. 적절한 로그 관리로 대규모 인덱싱 작업 중 디스크가 가득 차는 것을 방지하고, 문제 해결을 개선하며, 개발 시 즉각적인 피드백을 제공합니다. Maven 설정부터 로거 구성 과정을 차례로 살펴보고, 로거가 작동하는 간단한 검색 쿼리로 마무리합니다.

## 빠른 답변
- **“limit log file size”가 의미하는 바는?** 로그 파일의 최대 크기를 제한하여 디스크에 무제한으로 커지는 것을 방지합니다.  
- **어떤 로거가 로그 파일 크기를 제한할 수 있나요?** 내장된 `FileLogger`는 최대 크기 매개변수를 받습니다.  
- **Java에서 콘솔 로거를 어떻게 사용하나요?** `ConsoleLogger`를 인스턴스화하고 `IndexSettings`에 설정합니다.  
- **GroupDocs.Search에 라이선스가 필요합니까?** 평가용 트라이얼은 사용할 수 있지만, 프로덕션에서는 상용 라이선스가 필요합니다.  
- **첫 번째 단계는 무엇인가요?** Maven 프로젝트에 GroupDocs.Search 의존성을 추가합니다.  

## 로그 파일 크기 제한이란?
**limit log file size** 설정은 파일이 정의된 임계값(예: 4 MB)에 도달하면 로거가 새로운 항목 작성을 중지하도록 지시합니다. 제한에 도달하면 로거는 추가 메시지를 버리거나 새 파일로 롤오버하여 디스크 사용량을 예측 가능하게 유지합니다.

## GroupDocs.Search에서 파일 및 커스텀 로거를 사용하는 이유는?
파일 및 커스텀 로거를 사용하면 감사 가능성, 디버깅 인사이트, 유연성을 얻을 수 있습니다. 프로덕션 환경에서는 파일 로그가 모든 인덱싱 및 검색 작업의 영구 기록을 제공하고, 개발 중에는 콘솔 로그가 즉각적인 피드백을 제공합니다. 이러한 로그는 팀이 성능을 모니터링하고, 오류를 추적하며, 상세한 활동 기록을 보존함으로써 규정 준수 요구사항을 만족하도록 돕습니다.

## 사전 요구 사항
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 이상, IntelliJ IDEA 또는 Eclipse와 같은 IDE.  
- Maven 및 Java 프로그래밍에 대한 기본 지식.  

## GroupDocs.Search for Java 설정

아래 방법 중 하나를 사용하여 라이브러리를 프로젝트에 추가합니다.

**Maven 설정:**  

```text
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
```

**직접 다운로드:**  
공식 사이트에서 최신 JAR를 다운로드하세요: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### 라이선스 획득
트라이얼을 받거나 [라이선스 페이지](https://purchase.groupdocs.com/temporary-license/)를 통해 라이선스를 구매하세요.

## GroupDocs.Search용 커스텀 로거 생성 방법
커스텀 로거를 만드는 것은 간단합니다. GroupDocs.Search는 `ILogger` 인터페이스에 의존하기 때문입니다. 이 인터페이스를 구현하거나 제공된 `FileLogger` 또는 `ConsoleLogger`를 확장함으로써 원격 포워딩이나 로그 회전과 같은 추가 동작을 주입할 수 있습니다. 네트워크 연결을 여는 초기화 로직을 추가하고, 로거의 종료 메서드에서 리소스를 닫도록 할 수도 있습니다. 이러한 접근 방식은 ELK 또는 Splunk와 같은 모니터링 플랫폼과 통합할 수 있게 해줍니다.

### 정의 앵커
`ILogger`는 GroupDocs.Search의 핵심 로깅 계약이며, `log(Level, String)` 메서드를 구현하는 모든 클래스는 로거가 될 수 있습니다.

### 예시 접근법 (코드 블록 없음)
1. `ILogger`를 구현하는 클래스를 생성합니다.  
2. `log` 메서드를 오버라이드하여 메시지를 원하는 대상(파일, 데이터베이스, HTTP 엔드포인트)으로 기록합니다.  
3. 인덱스 구성에서 `settings.setLogger(new YourCustomLogger())`를 호출합니다.  

## File Logger로 로그 파일 크기 제한하기
`FileLogger` 클래스는 로그 항목을 디스크 파일에 기록하며 최대 크기 인수를 받습니다. 크기 제한을 지정하면 로거는 임계값에 도달했을 때 자동으로 새로운 항목 추가를 중지하거나 새 파일을 생성하여 디스크 무제한 증가를 방지합니다. 이 동작은 로그가 인덱싱 성능에 영향을 주지 않으면서 이벤트 기록을 간결하게 유지하도록 보장합니다.

### 정의 앵커
`FileLogger`는 메시지를 텍스트 파일에 저장하고 구성 가능한 최대 파일 크기를 지원하는 내장 로거입니다.

### 단계별 가이드
1️⃣ **필요한 패키지 가져오기**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **File Logger와 함께 인덱스 설정 구성**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```
```

3️⃣ **인덱스 생성 또는 로드**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **인덱스에 문서 추가**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **검색 쿼리 수행**  
```text
```java
SearchResult result = index.search(query);
```
```

**핵심 포인트:** `FileLogger` 생성자의 두 번째 인수(`4.0`)는 메가바이트 단위의 **set max log size**를 정의하며, 이는 **limit log file size** 요구사항을 직접 해결합니다.

## Java에서 콘솔 로거 사용 방법
로그 이벤트를 즉시 확인해야 할 때 `ConsoleLogger`는 각 메시지를 `System.out`에 기록합니다. 이 로거는 가볍고 스레드‑안전하여 개발 및 디버깅 세션에 적합합니다. 파일 I/O 없이 인덱싱 진행 상황, 검색 쿼리 및 오류 상태에 대한 즉각적인 피드백을 제공하여 반복 테스트 속도를 높일 수 있습니다.

### 정의 앵커
`ConsoleLogger`는 로그 항목을 표준 콘솔 스트림에 출력하는 가벼운 로거로, 디버깅 세션에 이상적입니다.

### 구성 단계
1️⃣ **콘솔 로거 가져오기**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Console Logger와 함께 인덱스 설정 구성**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **인덱스 생성 또는 로드**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **문서를 추가하고 검색 수행**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**팁:** 콘솔 로거는 개발 중에 이상적이며, 각 로그 항목을 즉시 출력해 인덱싱 및 검색이 기대대로 동작하는지 확인하는 데 도움이 됩니다.

## 실용적인 적용 사례
1. 문서 관리 시스템: 인덱싱된 모든 문서의 감사 추적을 유지하여 규정 준수 요구사항을 충족합니다.  
2. 엔터프라이즈 검색 엔진: 실시간으로 쿼리 성능 및 오류율을 모니터링하여 빠른 SLA 준수 확인을 가능하게 합니다.  
3. 법률 및 컴플라이언스 소프트웨어: 규제 보고를 위해 검색어와 타임스탬프를 기록하고, 로그를 지정된 보존 기간 동안 유지합니다.

## 성능 고려 사항
- **로그 크기:** **set max log size**를 사용하면 JVM 가비지 컬렉터를 느리게 할 수 있는 과도한 디스크 사용을 방지합니다.  
- **비동기 로깅:** 고처리량 시나리오에서는 로거를 비동기 큐에 래핑하여 I/O를 인덱싱 스레드와 분리합니다(구현은 이 가이드 범위를 벗어납니다).  
- **메모리 관리:** 필요 없을 때 `index.close()`로 큰 `Index` 객체를 해제하여 JVM 메모리 사용량을 낮게 유지합니다.

## 일반적인 문제 및 해결책
- **로그 경로에 접근할 수 없음:** 디렉터리가 존재하고 JVM을 실행하는 사용자 계정에 쓰기 권한이 있는지 확인합니다.  
- **로거가 작동하지 않음:** `Index` 객체를 *앞에* `settings.setLogger(...)`를 호출했는지 확인합니다; 그렇지 않으면 기본 로거가 사용됩니다.  
- **콘솔 출력 누락:** `System.out`을 표시하는 터미널에서 애플리케이션을 실행하고 있는지, 그리고 로깅 프레임워크(e.g., SLF4J)가 출력을 가로채고 있지 않은지 확인합니다.

## 자주 묻는 질문

**Q: `FileLogger`의 두 번째 매개변수는 무엇을 제어하나요?**  
A: 로그 파일의 최대 크기를 메가바이트 단위로 설정하며, 이를 통해 **set max log size**를 지정하고 무제한 성장을 방지합니다.

**Q: 파일 로거와 콘솔 로거를 결합할 수 있나요?**  
A: 가능합니다. 각 `log` 호출을 `FileLogger`와 `ConsoleLogger` 모두에 전달하는 커스텀 로거를 만든 뒤, 해당 복합 로거를 `IndexSettings`에 등록합니다.

**Q: 초기 생성 후 인덱스에 문서를 추가하려면 어떻게 해야 하나요?**  
A: 언제든지 `index.add(pathToNewDocs)`를 호출하면 됩니다; 구성된 로거가 자동으로 추가를 기록합니다.

**Q: `ConsoleLogger`는 스레드‑안전한가요?**  
A: `System.out`에 직접 쓰며, JVM이 내부적으로 동기화하므로 일반적인 다중 스레드 사용 사례에 안전합니다.

**Q: 로그 파일 크기 제한이 저장되는 정보량에 영향을 미치나요?**  
A: 크기 제한에 도달하면 새로운 항목이 버려지거나(선택한 구현에 따라) 로거가 새 파일로 롤오버합니다.

## 리소스
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Last Updated:** 2026-09-21  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

---

## 관련 튜토리얼

- [로깅 구현 방법 - GroupDocs.Search Java 예외 처리 및 로깅 튜토리얼](/search/java/exception-handling-logging/)
- [GroupDocs.Search와 함께 Java에서 비동기 로깅 구현 – 커스텀 로거 가이드](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Java 검색 인덱스 생성 – GroupDocs.Search 튜토리얼](/search/java/indexing/)
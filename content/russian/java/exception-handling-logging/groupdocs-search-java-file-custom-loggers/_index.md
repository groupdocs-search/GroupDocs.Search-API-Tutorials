---
date: '2026-09-21'
description: Узнайте, как создать логгер, задать максимальный размер журнала и использовать
  консольный логгер в GroupDocs.Search для Java.
keywords:
- how to create logger
- set max log size
- create custom logger java
- use console logger
- java logger max size
lastmod: '2026-09-21'
og_description: Узнайте, как создать логгер, задать максимальный размер журнала и
  использовать консольный логгер в GroupDocs.Search для Java. Следуйте пошаговым инструкциям
  и советам по лучшим практикам.
og_image_alt: Guide showing how to create logger and manage log file size in GroupDocs.Search
  for Java
og_title: Как создать логгер и ограничить размер журнала в GroupDocs.Search
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
title: Как создать логгер и ограничить размер журнала в GroupDocs.Search для Java
type: docs
url: /ru/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

# Как создать логгер и ограничить размер файла журнала в GroupDocs.Search для Java

В этом руководстве вы узнаете, **как создать логгер** реализации для GroupDocs.Search, настроите максимальный размер файла журнала и переключитесь между файловым и консольным логированием. Правильное управление журналами предотвращает заполнение дисков во время больших задач индексации, улучшает отладку и предоставляет мгновенную обратную связь при разработке. Мы начнём с настройки Maven, пройдём через конфигурацию логгера и завершим простым поисковым запросом, демонстрирующим работу логгера в действии.

## Быстрые ответы
- **Что означает «ограничить размер файла журнала»?** Это ограничивает максимальный размер файла журнала, предотвращая неконтролируемый рост на диске.  
- **Какой логгер позволяет ограничить размер файла журнала?** Встроенный `FileLogger` принимает параметр максимального размера.  
- **Как использовать консольный логгер в Java?** Создайте экземпляр `ConsoleLogger` и установите его в `IndexSettings`.  
- **Нужна ли лицензия для GroupDocs.Search?** Пробная версия подходит для оценки; для продакшн требуется коммерческая лицензия.  
- **Какой первый шаг?** Добавьте зависимость GroupDocs.Search в ваш Maven‑проект.  

## Что такое ограничение размера файла журнала?
Параметр **limit log file size** указывает логгеру прекратить запись новых записей, как только файл достигнет определённого порога (например, 4 МБ). Когда лимит достигается, логгер либо отбрасывает дальнейшие сообщения, либо переходит к новому файлу, обеспечивая предсказуемое использование диска.

## Почему использовать файловые и пользовательские логгеры с GroupDocs.Search?
Файловые и пользовательские логгеры предоставляют возможность аудита, инсайты для отладки и гибкость. В производственных средах файловые журналы обеспечивают постоянную запись каждой операции индексации и поиска, тогда как консольные журналы дают мгновенную обратную связь во время разработки. Эти журналы помогают командам мониторить производительность, отслеживать ошибки и удовлетворять требования соответствия, сохраняя подробный след активности.

## Предварительные требования
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 или новее, с IDE, такой как IntelliJ IDEA или Eclipse.  
- Базовое знакомство с Maven и программированием на Java.  

## Настройка GroupDocs.Search для Java

Добавьте библиотеку в ваш проект, используя один из методов ниже.

**Настройка Maven:**  

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

**Прямое скачивание:**  
Скачайте последнюю JAR‑файл с официального сайта: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Приобретение лицензии
Получите пробную версию или приобретите лицензию через [страницу лицензирования](https://purchase.groupdocs.com/temporary-license/).

## Как создать пользовательский логгер для GroupDocs.Search
Создание пользовательского логгера простое, поскольку GroupDocs.Search опирается на интерфейс `ILogger`. Реализуя этот интерфейс — либо расширяя предоставленные `FileLogger` или `ConsoleLogger` — вы можете добавить дополнительное поведение, например удалённую пересылку или ротацию журналов. Вы также можете добавить логику инициализации, такую как открытие сетевых соединений, и обеспечить закрытие ресурсов в методе завершения работы логгера. Такой подход позволяет интегрировать с платформами мониторинга, такими как ELK или Splunk.

### Якорь определения
`ILogger` — основной контракт логирования в GroupDocs.Search; любой класс, реализующий его метод `log(Level, String)`, может стать логгером.

### Пример подхода (без блока кода)
1. Создайте класс, реализующий `ILogger`.  
2. Переопределите метод `log`, чтобы записывать сообщения в выбранное вами место назначения (файл, база данных, HTTP‑конечная точка).  
3. В конфигурации индекса вызовите `settings.setLogger(new YourCustomLogger())`.  

## Как ограничить размер файла журнала с помощью File Logger
`FileLogger` записывает записи журнала в файл на диске и принимает аргумент максимального размера. Указывая ограничение размера, логгер автоматически прекращает добавление новых записей или создаёт новый файл, когда достигается порог, предотвращая неконтролируемый рост диска. Такое поведение гарантирует, что журналирование не будет мешать производительности индексации, одновременно сохраняя лаконичную запись событий.

### Якорь определения
`FileLogger` — встроенный логгер, сохраняющий сообщения в текстовый файл и поддерживающий настраиваемый максимальный размер файла.

### Пошаговое руководство
1️⃣ **Импортировать необходимые пакеты**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```
```

2️⃣ **Настроить параметры индекса с File Logger**  
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

3️⃣ **Создать или загрузить индекс**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Добавить документы в индекс**  
```text
```java
index.add(documentsFolder);
```
```

5️⃣ **Выполнить поисковый запрос**  
```text
```java
SearchResult result = index.search(query);
```
```

**Ключевой момент:** Второй аргумент конструктора `FileLogger` (`4.0`) определяет **set max log size** в мегабайтах, непосредственно решая требование **limit log file size**.

## Как использовать консольный логгер в Java
Когда требуется мгновенная видимость событий журнала, `ConsoleLogger` записывает каждое сообщение в `System.out`. Этот логгер лёгкий и потокобезопасный, что делает его подходящим для разработки и отладки. Он предоставляет немедленную обратную связь о прогрессе индексации, поисковых запросах и ошибках без необходимости файлового ввода‑вывода, что может ускорить итеративное тестирование.

### Якорь определения
`ConsoleLogger` — лёгкий логгер, выводящий записи журнала в стандартный консольный поток, что делает его идеальным для сеансов отладки.

### Шаги конфигурации
1️⃣ **Импортировать консольный логгер**  
```text
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```
```

2️⃣ **Настроить параметры индекса с Console Logger**  
```text
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```
```

3️⃣ **Создать или загрузить индекс**  
```text
```java
Index index = new Index(indexFolder, settings);
```
```

4️⃣ **Добавить документы и выполнить поиск**  
```text
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```
```

**Совет:** Консольный логгер идеален в процессе разработки, поскольку он мгновенно выводит каждую запись журнала, помогая убедиться, что индексация и поиск работают как ожидается.

## Практические применения
1. **Системы управления документами:** Сохраняют аудиторские следы каждого проиндексированного документа, удовлетворяя требования соответствия.  
2. **Корпоративные поисковые движки:** Мониторят производительность запросов и уровень ошибок в реальном времени, позволяя быстро проверять соответствие SLA.  
3. **Юридическое и комплаенс‑ПО:** Записывают поисковые запросы и метки времени для регуляторной отчётности, при этом журналы хранятся в течение установленного периода.

## Соображения по производительности
- **Размер журнала:** С помощью **set max log size** вы избегаете избыточного использования диска, которое иначе могло бы замедлить сборщик мусора JVM.  
- **Асинхронное логирование:** Для сценариев с высокой пропускной способностью оберните ваш логгер в асинхронную очередь, чтобы отделить ввод‑вывод от потока индексации (реализация выходит за рамки данного руководства).  
- **Управление памятью:** Освобождайте большие объекты `Index` с помощью `index.close()`, когда они больше не нужны, чтобы снизить потребление памяти JVM.

## Распространённые проблемы и решения
- **Путь к журналу недоступен:** Убедитесь, что каталог существует и приложение имеет права записи для учётной записи пользователя, под которой запущена JVM.  
- **Логгер не срабатывает:** Убедитесь, что вы вызываете `settings.setLogger(...)` *до* создания объекта `Index`; иначе будет использован логгер по умолчанию.  
- **Отсутствует вывод в консоль:** Убедитесь, что приложение запущено в терминале, отображающем `System.out`, и что никакой фреймворк логирования (например, SLF4J) не перехватывает вывод.

## Часто задаваемые вопросы

**В: Что контролирует второй параметр `FileLogger`?**  
О: Он задаёт максимальный размер файла журнала в мегабайтах, позволяя вам **set max log size** и предотвращать неконтролируемый рост.

**В: Можно ли комбинировать файловый и консольный логгеры?**  
О: Да. Создайте пользовательский логгер, который перенаправляет каждый вызов `log` как в `FileLogger`, так и в `ConsoleLogger`, затем зарегистрируйте этот составной логгер в `IndexSettings`.

**В: Как добавить документы в индекс после первоначального создания?**  
О: Вызовите `index.add(pathToNewDocs)` в любой момент; настроенный логгер автоматически зафиксирует добавление.

**В: Является ли `ConsoleLogger` потокобезопасным?**  
О: Он пишет напрямую в `System.out`, который JVM синхронизирует внутренне, делая его безопасным для типичных многопоточных сценариев.

**В: Ограничит ли ограничение размера файла журнала количество сохраняемой информации?**  
О: После достижения лимита новые записи либо отбрасываются, либо логгер переходит к новому файлу, в зависимости от выбранной реализации.

## Ресурсы
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Последнее обновление:** 2026-09-21  
**Тестировано с:** GroupDocs.Search for Java 25.4  
**Автор:** GroupDocs  

## Связанные руководства

- [Как реализовать логирование - Руководства по обработке исключений и логированию для GroupDocs.Search Java](/search/java/exception-handling-logging/)
- [Реализация асинхронного логирования в Java с GroupDocs.Search – Руководство по пользовательскому логгеру](/search/java/exception-handling-logging/master-custom-logging-groupdocs-search-java/)
- [Создание поискового индекса Java – Руководства GroupDocs.Search](/search/java/indexing/)
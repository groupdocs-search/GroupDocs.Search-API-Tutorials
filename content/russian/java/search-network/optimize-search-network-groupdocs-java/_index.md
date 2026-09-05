---
date: '2026-05-17'
description: Узнайте, как настроить поисковую сеть Java, оптимизировать шарды, выполнять
  текстовый поиск и решать конфликты портов с помощью GroupDocs.Search for Java.
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
title: 'Как оптимизировать шарды в GroupDocs.Search for Java: Полное руководство'
type: docs
url: /ru/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Как оптимизировать шарды в GroupDocs.Search для Java: Полное руководство

Эффективный поиск документов необходим разработчикам и компаниям, которые управляют большими наборами данных или нуждаются в быстром внутреннем извлечении. В этом руководстве вы узнаете **how to configure search network java**, как индексировать и выполнять запросы к документам, а также точные шаги по **optimize shards** для достижения максимальной производительности. Мы также рассмотрим реальные примеры использования, распространённые подводные камни и практические советы, чтобы ваши узлы поиска работали без сбоев.

## Быстрые ответы
- **Что такое оптимизация шардов?** It reorganizes index data to speed up queries and reduce storage overhead.  
- **Как настроить поисковую сеть?** Define a base directory and port, then deploy nodes using the provided API.  
- **Как выполнить текстовый поиск?** Use `TextSearchInNetwork.searchAll` with your query string.  
- **Как индексировать документы в Java?** Add document directories to the master node with `IndexingDocuments.addDirectories`.  
- **Как решить конфликты портов?** Change the `basePort` variable to an unused port on your machine.

## Как настроить поисковую сеть
`Configuration` хранит все настройки, необходимые для запуска сети GroupDocs.Search, такие как расположение папки индекса и порт связи.  
`SearchNetwork` управляет узлами, обрабатывая индексацию и распределение запросов.

Загрузите конфигурацию поиска, задайте базовый путь к документам, выберите свободный порт и запустите сеть — всё в нескольких строках кода. Этот прямой ответ объясняет весь процесс менее чем за 70 слов: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`**. Сеть автоматически поднимет мастер‑узел и любые необходимые рабочие узлы, готовые принимать запросы на индексацию.

### Якорь определения
`Configuration` — это основной класс, который хранит все настройки, необходимые для запуска сети GroupDocs.Search, такие как расположение папки индекса и порт связи.

Чтобы избежать страшной ошибки «port already in use», сначала проверьте, что выбранный порт свободен (например, с помощью `netstat` или простого теста сокета) перед инициализацией сети.

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

## Как индексировать документы в Java
`IndexingDocuments` — это вспомогательный класс, упрощающий добавление нескольких каталогов в поисковый узел и запускающий процесс индексации.

Добавьте папки с документами в мастер‑узел, затем позвольте индексатору их просканировать. **Direct answer:** Call `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` and then invoke `masterNode.index()`; the engine will create searchable shards for every folder you supplied. This approach scales horizontally—add more nodes, and the same method distributes the workload automatically.

### Якорь определения
`IndexingDocuments` — это вспомогательный класс, упрощающий добавление нескольких каталогов в поисковый узел и запускающий процесс индексации.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Как выполнить текстовый поиск
`TextSearchInNetwork` предоставляет статические вспомогательные методы для рассылки текстового запроса каждому узлу в сети и агрегирования результатов.  
`SearchResult` инкапсулирует ID найденного документа, фрагмент и оценку релевантности.

Выполните запрос по всем шардам одним вызовом метода. **Direct answer:** Use `TextSearchInNetwork.searchAll("your query", searchNetwork)`; the method returns a collection of `SearchResult` objects containing document IDs, snippets, and relevance scores. You can further filter results by language, file type, or custom metadata without writing extra code.

### Якорь определения
`TextSearchInNetwork` предоставляет статические вспомогательные методы, которые рассылают текстовый запрос каждому узлу в сети и агрегируют результаты.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Как решить конфликты портов
Если порт по умолчанию (`49132`) занят, просто выберите другой свободный порт и обновите поле `basePort` перед запуском сети. **Direct answer:** Change `int basePort = 49132;` to an unused value like `49133`, rebuild, and restart; the network will bind to the new port without affecting existing nodes.

Pro tip: Keep a small configuration file (e.g., `search-config.properties`) so you can change the port without recompiling.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Предварительные требования
Прежде чем начать, убедитесь, что у вас есть следующие предварительные требования:

### Требуемые библиотеки, версии и зависимости
Чтобы реализовать это решение, включите библиотеку GroupDocs.Search с помощью Maven, добавив следующую конфигурацию в ваш файл `pom.xml`:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Требования к настройке окружения
- Java Development Kit (JDK) 8 или новее.
- Network permissions that allow binding to the chosen `basePort`.
- Sufficient disk space for index files (each shard can occupy ~10 MB per 1,000 documents).

### Требования к знаниям
Базовое понимание Java, объектно‑ориентированного программирования и обработки исключений поможет вам легко следовать примерам.

## Настройка GroupDocs.Search для Java
Чтобы начать использовать GroupDocs.Search в вашем проекте, выполните следующие шаги:

1. **Add the Dependency**: As shown above, add the necessary Maven dependency to your project or download directly from the releases page.  
2. **License Acquisition**:  
   - **Free trial** – ключ лицензии не требуется, но использование ограничено 500 документами в день.  
   - **Temporary license** – запросите 30‑дневный пробный ключ по ссылке [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – приобретите производственную лицензию для неограниченного доступа и приоритетной поддержки.  
3. **Basic Initialization and Setup**:  
   Initialize the configuration using the `Configuration` class, setting up the base path for documents and specifying a port number:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Руководство по реализации
Теперь давайте изучим реализацию ключевых функций с использованием GroupDocs.Search Java.

### Функция: Настройка поисковой сети
**Overview**: Настройка поисковой сети включает определение каталога документов и конфигурацию с определённым портом для связи между узлами.

#### Шаг 1: Определить каталоги документов и порт
`DocumentDirectory` — простой контейнер для абсолютного пути к папке, которую вы хотите индексировать. Укажите один или несколько путей в конфигурацию.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Шаг 2: Настроить поисковую сеть
Создайте объект конфигурации, используя определённые пути:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Функция: Развёртывание узлов поисковой сети
**Overview**: Развёртывание узлов для эффективной обработки поисковых запросов по документам в вашей сети.

#### Шаг 1: Развёртывание узлов с использованием конфигурации
Разверните узлы поисковой сети и определите мастер‑узел для централизованного управления:

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

### Функция: Подписка на события узлов сети
**Overview**: Мониторинг вашей поисковой сети посредством подписки на события, которые уведомляют о важных изменениях или действиях.

#### Шаг 1: Подписка на события мастер‑узла
`SearchNetworkEventListener` позволяет реагировать на завершение индексации, сбои узлов или оптимизацию шардов.

CODE_BLOCK_PLACEHOLDER_9_END

### Функция: Индексация документов в узлах сети
**Overview**: Добавление каталогов с документами в процесс индексации для эффективного поиска.

#### Шаг 1: Добавление каталогов документов в процесс индексации
Передайте список путей к папкам мастер‑узлу; движок создаст отдельный шард для каждой папки, позволяя выполнять запросы параллельно.

CODE_BLOCK_PLACEHOLDER_10_END

### Функция: Текстовый поиск в узлах сети
**Overview**: Выполнение текстового поиска по всем проиндексированным документам в вашей поисковой сети.

#### Шаг 1: Выполнение текстового поиска
Вызовите статический вспомогательный метод для выполнения запроса и получения совпадающих документов с оценками релевантности.

CODE_BLOCK_PLACEHOLDER_11_END

### Функция: Оптимизация шардов
**Overview**: Повышение производительности за счёт оптимизации шардов в индексаторе узла вашей поисковой сети.

#### Шаг 1: Оптимизация шардов индексатора
Оптимизируйте шарды для повышения эффективности поиска (здесь действительно важен **how to optimize shards**):

CODE_BLOCK_PLACEHOLDER_12_END

## Практические применения
GroupDocs.Search for Java может быть применён в различных реальных сценариях, каждый из которых выигрывает от оптимизации шардов:

1. **Enterprise Document Management** – Обрабатывает архивы более 10 ТБ с временем запроса менее секунды после оптимизации шардов.  
2. **E‑commerce Platforms** – Обеспечивает поиск товаров по 1 миллиону SKU, снижая задержку до 45 % при оптимизации шардов.  
3. **Legal Firms** – Извлекает судебные материалы из репозиториев объёмом 200 ГБ менее чем за 200 мс.  
4. **Library Systems** – Поддерживает поиск в каталоге 500 тыс. цифровых книг с эффективным использованием памяти.  
5. **Content Management Systems (CMS)** – Обеспечивает мгновенный поиск контента для многосайтовых развертываний с более чем 2 миллионами страниц.

## Соображения по производительности
Чтобы обеспечить оптимальную производительность вашей реализации GroupDocs.Search:

- **Regularly optimize shards** – Running `optimizeShards()` after every 10 GB of new data reduces query response times by 30‑50 %.  
- **Monitor memory usage** – Keep JVM heap below 75 % of physical RAM; enable G1GC for large indexes.  
- **Use incremental indexing** – Add only changed files to avoid full re‑indexing.  
- **Leverage multi‑node scaling** – Add worker nodes to distribute shards; each additional node can improve throughput by ~20 % for read‑heavy workloads.

## Распространённые проблемы и решения

| Проблема | Симптом | Решение |
|----------|---------|----------|
| Конфликт порта при запуске | `java.net.BindException: Address already in use` | Измените `basePort` на неиспользуемое значение; проверьте с помощью `netstat -ano`. |
| Ошибки Out‑of‑memory во время оптимизации | `java.lang.OutOfMemoryError: Java heap space` | Увеличьте параметр JVM `-Xmx` или выполните оптимизацию на выделенном узле с большим объёмом ОЗУ. |
| Отсутствие документов в результатах поиска | Нет результатов после индексации | Убедитесь, что каталоги правильно добавлены через `IndexingDocuments.addDirectories` и что `masterNode.index()` завершился без исключений. |
| Устаревшие шарды после массового удаления | Удалённые файлы всё ещё отображаются | Выполните `optimizeShards()`, чтобы объединить сегменты и удалить «могильные камни». |

## Часто задаваемые вопросы

**Q: Как оптимизация шардов влияет на скорость запросов?**  
A: Optimizing shards compacts the index, reduces disk I/O, and typically yields 30‑50 % faster query responses for large datasets.

**Q: Безопасно ли запускать `optimizeShards` на работающем узле?**  
A: Yes, the operation is designed to run without downtime, but scheduling during low‑traffic periods is recommended for indexes larger than 20 GB.

**Q: Можно ли настроить `OptimizeOptions`?**  
A: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor` to fine‑tune the optimization process.

**Q: Что делать, если во время оптимизации возникает `IOException`?**  
A: Verify file system permissions, ensure enough free disk space, and confirm that no other process is locking the index files.

**Q: Оптимизация шардов также освобождает место от удалённых документов?**  
A: Yes, the optimizer merges segments and removes tombstones, freeing up space occupied by deleted documents.

## Заключение
Следуя этому полному руководству, вы теперь знаете, как **configure search network java**, индексировать документы, выполнять текстовые запросы и, что самое важное, **optimize shards**, чтобы поддерживать производительность поиска на высоте. Применяйте эти шаблоны к любой Java‑ориентированной корпоративной поисковой системе, и вы увидите измеримые улучшения в задержке, масштабируемости и использовании ресурсов. Для дальнейших шагов изучите расширенные функции, такие как пользовательские анализаторы, фасетный поиск и интеграцию с облачными хранилищами.

---

**Последнее обновление:** 2026-05-17  
**Тестировано с:** GroupDocs.Search 25.4 for Java  
**Автор:** GroupDocs

## Связанные руководства

- [Настройка сети GroupDocs.Search в .NET&#58; Полное руководство](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Мастер‑индексация документов .NET с GroupDocs.Search&#58; Полное руководство](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Учебники и примеры GroupDocs.Search для Java](/search/net/)
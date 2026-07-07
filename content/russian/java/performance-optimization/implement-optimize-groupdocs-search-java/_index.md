---
date: '2026-07-07'
description: Узнайте, как удалить индекс, выполнить full text search Java и оптимизировать
  search performance с помощью GroupDocs.Search for Java. Пошаговое руководство с
  настройкой сети и индексацией.
keywords:
- how to delete index
- remove indexed files
- full text search java
- optimize search performance
- create searchable index
og_description: Как удалить индекс и выполнить full text search Java с помощью GroupDocs.Search.
  Следуйте этому руководству, чтобы настроить search network, создать searchable index
  и оптимизировать search performance.
og_title: Как удалить индекс и выполнить text search с GroupDocs.Search for Java
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to delete index, perform full text search Java, and optimize
    search performance using GroupDocs.Search for Java. Step‑by‑step guide with network
    setup and indexing.
  headline: How to Delete Index and Perform Text Search with GroupDocs.Search for
    Java
  type: TechArticle
- questions:
  - answer: It provides full‑text search across many document formats, allowing you
      to **perform text search** in large repositories.
    question: What is the primary use case for GroupDocs.Search for Java?
  - answer: Deploy additional nodes, tune the JVM heap, and schedule indexing during
      low‑traffic periods to **optimize search performance**.
    question: How can I improve search speed in a large network?
  - answer: Yes, use the **delete documents index** API as shown in the code example
      to remove specific files.
    question: Is it possible to delete a single document without re‑indexing the whole
      collection?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production deployments.
    question: Do I need a license for development?
  - answer: Absolutely—GroupDocs.Search supports a wide range of formats out of the
      box.
    question: Can I index PDFs, Word files, and emails together?
  type: FAQPage
title: Как удалить индекс и выполнить text search с GroupDocs.Search for Java
type: docs
url: /ru/java/performance-optimization/implement-optimize-groupdocs-search-java/
weight: 1
---

# Как удалить индекс и выполнить текстовый поиск с GroupDocs.Search для Java

В современном мире, управляемом данными, быстрое **how to delete index** при сохранении молниеносных возможностей полнотекстового поиска на Java является конкурентным преимуществом. Независимо от того, создаёте ли вы внутреннюю базу знаний, репозиторий юридических дел или каталог товаров для электронной коммерции, правильно настроенная поисковая сеть может значительно повысить удовлетворённость пользователей. В этом руководстве вы узнаете, как **set up a search network**, **create a searchable index**, **optimize search performance**, и **delete documents from the index** при необходимости — используя GroupDocs.Search для Java.

## Быстрые ответы
- **Какова основная цель GroupDocs.Search для Java?** It provides full‑text search across 50+ document formats, enabling rapid keyword retrieval.  
- **Как выполнить текстовый поиск в распределённой среде?** Deploy a search network, index documents on a master node, then query any node.  
- **Можно ли удалить документы из индекса без его перестроения?** Yes, use the Delete API to remove selected files, effectively *how to delete index* without full re‑indexing.  
- **Какая версия Java требуется?** JDK 8 or higher.  
- **Нужна ли лицензия для продакшн?** A valid GroupDocs.Search license is required; a free trial is available.

## Что такое «perform text search»?
Выполнение текстового поиска означает запрос к полнотекстовому индексу для получения документов, содержащих указанные ключевые слова или фразы. GroupDocs.Search создает обратный индекс, который делает такие запросы чрезвычайно быстрыми, даже при работе с тысячами файлов.

## Зачем настраивать поисковую сеть?
Поисковая сеть распределяет нагрузки индексации и запросов между несколькими узлами, позволяя **optimize search performance**, масштабироваться горизонтально и поддерживать высокую доступность. Эта архитектура идеальна для корпоративных репозиториев документов, где важны задержка и пропускная способность.

## Как реализовать и оптимизировать поисковую сеть с GroupDocs.Search для Java
Загрузите свою конфигурацию, запустите мастер‑узел, а затем добавьте рабочие узлы, которые используют тот же базовый путь и порт. Развёртывание сети таким образом позволяет любому узлу обрабатывать запросы индексации или поиска, обеспечивая стабильные времена отклика даже при росте количества документов до сотен тысяч.

### Поэтапный обзор
1. **Определите базовую конфигурацию**, включающую общую директорию и TCP‑порт.  
2. **Запустите мастер‑узел**, чтобы управлять индексом и координировать рабочие узлы.  
3. **Добавьте рабочие узлы**, которые подключаются к мастеру, обеспечивая параллельную индексацию и поиск.  
4. **Контролируйте использование ресурсов** и настраивайте параметры кучи JVM для снижения задержки.

## Как удалить индекс в GroupDocs.Search для Java
`SearchNode` представляет узел в сети GroupDocs.Search, который управляет операциями индексации и запросов. Метод `delete` удаляет указанные документы из индекса.

### Прямые шаги удаления
- Вызовите метод `delete` у экземпляра `SearchNode`.  
- Передайте массив относительных путей к файлам.  
- Зафиксируйте изменения; индекс мгновенно обновляется, и последующие поиски больше не возвращают удалённые файлы.

## Что такое поисковая сеть?
**search network** — это кластер взаимосвязанных узлов, которые используют общий репозиторий индекса, позволяя распределённую индексацию и выполнение запросов. Он обеспечивает горизонтальное масштабирование и отказоустойчивость для крупномасштабных коллекций документов.

## Как создать поисковый индекс (index documents java)
Метод `add` индексирует документ в поисковый индекс. Добавляйте документы в мастер‑узел с помощью метода `add`; сеть распространяет изменения на все рабочие узлы. Такой подход гарантирует, что каждый узел может обслуживать запросы к самому актуальному индексу без дополнительных шагов синхронизации.

### Ключевые действия
- Укажите мастер‑узлу папку, содержащую исходные файлы.  
- Вызовите процедуру индексации; сеть обрабатывает каждый файл и обновляет обратный индекс.  
- Убедитесь, что файлы индекса появились в указанной директории хранения.

## Как удалить проиндексированные файлы (remove indexed files)
Когда документ становится устаревшим, вызовите API `delete` с его путём. Система удаляет записи файла из обратного индекса, освобождая место и предотвращая появление устаревших результатов.

## Настройка GroupDocs.Search для Java
Для начала интегрируйте GroupDocs.Search в ваш Java‑проект, используя следующую настройку:

### Настройка Maven
Добавьте репозиторий и зависимость в ваш файл `pom.xml`:

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

### Прямое скачивание
В качестве альтернативы вы можете [скачать последнюю версию напрямую с GroupDocs](https://releases.groupdocs.com/search/java/).

### Приобретение лицензии
GroupDocs предлагает бесплатную пробную версию, которая позволяет оценить функции перед покупкой. Вы можете получить временную лицензию, следуя инструкциям на их [странице покупки](https://purchase.groupdocs.com/temporary-license/). Это активирует полную функциональность во время тестирования.

### Базовая инициализация и настройка
Инициализируйте GroupDocs.Search в вашем Java‑приложении с помощью:

```java
import com.groupdocs.search.*;

class SearchNetworkSetup {
    public static void main(String[] args) {
        Index index = new Index("path/to/index/directory");
        // Additional configuration can be set here.
    }
}
```

## Руководство по реализации

### Настройка поисковой сети
**Overview:** Установите базовый путь и порт для вашей поисковой сети, позволяя узлам эффективно взаимодействовать.

#### Шаг 1: Определить базовую конфигурацию
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104; // Change if necessary.
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **Parameters:**  
  - `basePath`: Путь к директории для операций сети.  
  - `basePort`: Номер порта, используемый поисковой сетью.

#### Шаг 2: Устранение неполадок
Убедитесь, что указанный порт не заблокирован настройками брандмауэра и не используется другим приложением. При необходимости измените его, чтобы избежать конфликтов.

### Развёртывание узлов поисковой сети
**Overview:** С помощью вашей конфигурации разверните узлы в сети для распределённой индексации и поиска.

```java
import com.groupdocs.search.scaling.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/output/AdvancedUsage/Scaling/DeletingDocuments/";
int basePort = 49104;
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);

// Nodes are now deployed and ready for further operations.
```

- **Key Configuration Options:**  
  - **Base Path & Port:** Эти значения должны совпадать с теми, что использовались в начальной конфигурации, чтобы обеспечить согласованность.

### Индексация документов (`create searchable index`)
**Overview:** Эффективно добавляйте документы в поисковый индекс с помощью мастер‑узла.

```java
import com.groupdocs.search.scaling.*;

String documentsPath = "YOUR_DOCUMENT_DIRECTORY/path/to/documents";
SearchNetworkNode masterNode = nodes[0];
IndexingDocuments.addDirectories(masterNode, documentsPath);
```

- **Purpose:**  
  - `masterNode`: Основной узел, управляющий индексацией документов.  
  - `documentsPath`: Путь к директории, содержащей документы.

#### Советы по устранению неполадок
Убедитесь, что пути к документам правильные и доступны. Проверьте, что разрешения позволяют чтение из этих директорий.

### Поиск текста в сети (`perform text search`)
**Overview:** Выполняйте комплексный текстовый поиск по вашей проиндексированной сети.

```java
import com.groupdocs.search.scaling.*;

String query = "nulla";
SearchNetworkNode masterNode = nodes[0];
TextSearchInNetwork.searchAll(masterNode, query, false);
```

- **Parameters:**  
  - `query`: Текст, который вы ищете.  
  - `masterNode`: Узел, выполняющий поиск.

### Удаление документов из индекса (`delete documents index`)
**Overview:** Удаляйте конкретные документы из индекса, используя их пути к файлам.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode node = nodes[0];
String[] filePaths = {
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.pdf",
    "YOUR_DOCUMENT_DIRECTORY/Lorem ipsum.docx"
};
deleteDocuments(node, filePaths);

void deleteDocuments(SearchNetworkNode node, String... filePaths) {
    Indexer indexer = node.getIndexer();
    DeleteOptions options = new DeleteOptions();
    indexer.delete(filePaths, options);
}
```

- **Method Purpose:**  
  - `node`: Целевой узел для операций удаления.  
  - `filePaths`: Пути к документам, которые нужно удалить из индекса.

#### Устранение неполадок
Убедитесь, что пути к файлам точны и файлы существуют в вашей директории. Если проблемы сохраняются, проверьте сетевые разрешения и соединение.

## Практические применения
1. **Enterprise Document Management:** Упрощение внутреннего поиска знаний.  
2. **Legal Case Analysis:** Быстрый поиск релевантных деловых файлов в нескольких репозиториях.  
3. **E‑commerce Platforms:** Увеличьте скорость поиска продуктов, индексируя описания и отзывы.  
4. **Academic Research:** Эффективный поиск в больших цифровых библиотеках статей и диссертаций.  
5. **Customer Support Systems:** Сократите время ответа, позволяя агентам мгновенно искать прошлые заявки.

## Соображения по производительности
- **Optimize Indexing Speed:** Пошагово добавляйте новые документы в непиковые часы, чтобы поддерживать низкую задержку.  
- **Resource Usage Guidelines:** Следите за использованием CPU и памяти, особенно при масштабировании количества узлов.  
- **Java Memory Management:** Настраивайте параметры кучи JVM в зависимости от нагрузки (например, `-Xmx2g` для индексов среднего размера).

## Заключение
Следуя этому руководству, вы узнали, как **set up a search network**, **create a searchable index**, **perform text search** и **delete documents index** с помощью GroupDocs.Search для Java. Эти возможности обеспечивают быстрый и надёжный поиск документов в распределённых средах.

**Следующие шаги**
- Экспериментируйте с различными конфигурациями узлов, чтобы найти оптимальный баланс для вашей нагрузки.  
- Углубитесь в расширенные параметры индексации, такие как пользовательские анализаторы и настройка релевантности.  
- Исследуйте интеграцию с другими продуктами GroupDocs для сквозной обработки документов.

## Часто задаваемые вопросы

**Q: Каков основной сценарий использования GroupDocs.Search для Java?**  
A: Он предоставляет полнотекстовый поиск по множеству форматов документов, позволяя вам **perform text search** в больших репозиториях.

**Q: Как улучшить скорость поиска в большой сети?**  
A: Разверните дополнительные узлы, настройте кучу JVM и планируйте индексацию в периоды низкой нагрузки, чтобы **optimize search performance**.

**Q: Можно ли удалить один документ без переиндексации всей коллекции?**  
A: Да, используйте API **delete documents index**, как показано в примере кода, чтобы удалить конкретные файлы.

**Q: Нужна ли лицензия для разработки?**  
A: Бесплатная пробная лицензия достаточна для тестирования; коммерческая лицензия требуется для продакшн‑развёртываний.

**Q: Можно ли индексировать PDF, Word и электронные письма вместе?**  
A: Конечно — GroupDocs.Search поддерживает широкий спектр форматов из коробки.

**Последнее обновление:** 2026-07-07  
**Тестировано с:** GroupDocs.Search for Java 25.4  
**Автор:** GroupDocs

## Связанные руководства
- [Как индексировать текст в Java с руководством GroupDocs.Search](/search/java/indexing/master-text-indexing-java-groupdocs-search-guide/)
- [Оптимизация производительности поиска с помощью продвинутых техник индексации в GroupDocs.Search для Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)
- [Повышение производительности запросов с GroupDocs.Search Java: оптимизация индекса и поиска](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
---
date: '2026-01-16'
description: Узнайте, как настроить сеть поиска GroupDocs в Java и добавить синонимы
  в индекс для повышения эффективности поиска.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Настройка GroupDocs.Search Network в Java – Boost Search
type: docs
url: /ru/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Настройка сети GroupDocs.Search в Java – Ускорение поиска

В современных приложениях, ориентированных на данные, **configure groupdocs search network** является ключевым шагом для предоставления быстрых и точных результатов по огромным коллекциям документов. Независимо от того, создаёте ли вы корпоративный поисковый портал или расширяете существующее решение, правильно настроенная сеть GroupDocs.Search позволяет масштабировать горизонтально, добавлять поддержку синонимов и поддерживать низкую задержку. В этом руководстве вы узнаете, как настроить, развернуть и оптимизировать сеть GroupDocs.Search с использованием Java, а также получите практические советы по добавлению синонимов в индекс и управлению жизненным циклом узлов.

## Быстрые ответы
- **What is the primary benefit of configuring a GroupDocs.Search network?** Это позволяет выполнять распределённое индексирование и запросы, улучшая производительность и масштабируемость.  
- **Do I need a license to run the examples?** Бесплатная пробная версия подходит для разработки; для продакшн‑развертываний требуется коммерческая лицензия.  
- **Can synonyms be added without rebuilding the index?** Да — используйте словарь синонимов во время выполнения, чтобы **add synonyms to index**.  
- **How many nodes can I deploy?** Вы можете развернуть столько узлов, сколько позволяет ваша инфраструктура; каждый узел работает на собственном порту.  

## Что такое настройка сети GroupDocs.Search?
Настройка сети GroupDocs.Search подразумевает определение структуры папок, портов и параметров узлов, позволяющих нескольким экземплярам JVM совместно выполнять индексацию и поиск. Эта конфигурация создаёт мастер‑узел, который координирует рабочие узлы (шарды) и гарантирует выполнение запросов по всему набору данных.

## Зачем настраивать сеть GroupDocs.Search?
- **Scalability** – Распределить нагрузку индексации между несколькими машинами.  
- **Reliability** – Узлы можно добавлять или удалять без простоя.  
- **Search relevance** – **add synonyms to index** для более богатых результатов.  
- **Performance** – Параллельное выполнение запросов сокращает время отклика.  

## Предварительные требования
- Java Development Kit (JDK) 8 или новее  
- Maven для сборки проекта  
- Базовое знакомство с синтаксисом Java  
- Доступ к библиотеке GroupDocs.Search for Java (скачивается через Maven или официальную страницу релизов)  

## Настройка GroupDocs.Search для Java
Добавьте репозиторий и зависимость в ваш Maven **pom.xml**:

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

В качестве альтернативы загрузите последнюю версию напрямую с [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Приобретение лицензии
- **Free Trial** – Исследуйте основные функции бесплатно.  
- **Temporary License** – Откройте полный набор возможностей для краткосрочного тестирования.  
- **Commercial License** – Требуется для продакшн‑развёртываний.  

### Базовая инициализация и настройка
Создайте простой Java‑класс, чтобы проверить корректную загрузку библиотеки:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Пошаговое руководство по настройке сети GroupDocs.Search

### 1. Настройка поисковой сети
Определите базовую папку документов и начальный порт для коммуникации узлов.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Путь, где находятся словари (например, файлы синонимов).  
- **basePort** – Первый порт; последующие узлы используют порты, увеличивая это значение.  

### 2. Развёртывание узлов поисковой сети
Запустите несколько рабочих узлов, использующих одну и ту же конфигурацию.

```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Каждый узел работает на собственном порту (basePort + index) и содержит часть общего индекса.

### 3. Подписка на события узлов
Отслеживайте состояние, прогресс индексации и ошибки, присоединив слушатель событий к мастер‑узлу.

```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Обратные вызовы событий позволяют реагировать на запуск/остановку узла, завершение индексации и непредвиденные сбои.

### 4. Добавление синонимов в индексатор узла  
Повышайте релевантность, используя **add synonyms to index** во время выполнения.

```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Массив терминов, которые должны рассматриваться как эквиваленты.  
- **clearBeforeAdding** – Установите `true`, если хотите заменить существующие записи.  

### 5. Добавление каталогов для индексации
Укажите мастер‑узлу, какие папки содержат документы, которые необходимо сделать доступными для поиска.

```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Метод рекурсивно сканирует каталог и распределяет файлы по шардам.

### 6. Выполнение текстового поиска в сети
Выполните запрос по всем узлам, при необходимости принудительно используя точное совпадение.

```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Установите `exactMatchOnly` в `true`, когда требуется строгое совпадение терминов без стемминга.

### 7. Закрытие узлов сети
Корректно освобождайте ресурсы после завершения обработки.

```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Правильное завершение предотвращает утечки памяти и поддерживает здоровье JVM.

## Практические применения
| Scenario | How the network helps |
|----------|-----------------------|
| **Enterprise Search** | Распределить индексацию по серверам дата‑центра для корпусов данных в масштабе петабайт. |
| **Document Management** | Добавить синонимы в индекс, чтобы пользователи находили документы даже при различной терминологии. |
| **E‑commerce Catalog** | Развернуть региональные узлы для быстрой локализованной поисковой выдачи товаров. |
| **Content Management** | Сохранять контент доступным для поиска, пока редакторы добавляют новые файлы в определённые каталоги. |

## Распространённые проблемы и решения
- **Port Conflicts** – Убедитесь, что порт каждого узла (basePort + index) свободен; при необходимости измените `basePort`.  
- **Synonym Not Applied** – Проверьте, что вы вызвали `indexer.setDictionary(dictionary)` после добавления терминов.  
- **Node Not Responding** – Подпишитесь на события; ищите обратные вызовы `NodeFailed` для диагностики проблем сети.  
- **Memory Leak on Close** – Всегда вызывайте `node.close()` для каждого развернутого узла.  

## Часто задаваемые вопросы

**Q: How does deploying multiple nodes improve search performance?**  
A: Каждый узел индексирует часть данных, позволяя выполнять параллельную обработку и снижая задержку запросов за счёт распределения нагрузки.

**Q: Can I add synonyms without re‑indexing existing documents?**  
A: Да, вы можете **add synonyms to index** во время выполнения через словарь синонимов; изменения вступают в силу сразу для новых запросов.

**Q: Is subscribing to node events mandatory?**  
A: Хотя это не требуется для базовой работы, подписка на события предоставляет информацию о состоянии узлов и помогает быстро реагировать на сбои.

**Q: What are best practices for managing node resources?**  
A: Регулярно закрывайте неиспользуемые узлы, контролируйте использование памяти JVM и перераспределяйте узлы в часы низкой нагрузки, чтобы поддерживать оптимальное потребление ресурсов.

**Q: Does GroupDocs.Search support non‑text formats like PDFs or images?**  
A: Конечно. Библиотека извлекает текст из PDF, файлов Office и даже выполняет OCR изображений, делая их доступными для поиска сразу после установки.

---

**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
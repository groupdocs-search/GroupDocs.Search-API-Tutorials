---
date: '2026-01-24'
description: Изучите, как настроить базовую группу PortDocs для масштабируемых поисковых
  сетей с помощью GroupDocs.Search Java, оптимизировать скорость извлечения и настроить
  многокомпонентные системы.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Настройка базового порта groupdocs в Java Search Network
type: docs
url: /ru/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Настройка базового порта GroupDocs в Java Search Network

В современных приложениях с большим объёмом данных **настройка базового порта GroupDocs** является фундаментальным шагом для построения быстрой и надёжной поисковой инфраструктуры. Независимо от того, обрабатываете ли вы тысячи PDF‑файлов или масштабируете решение на несколько серверов, правильная настройка портов и путей гарантирует, что каждый узел будет взаимодействовать с другими без конфликтов. Этот учебник проведёт вас через каждый шаг — от предварительных требований до полной многопользовательской конфигурации — чтобы вы уверенно запустили масштабируемую поисковую сеть с GroupDocs.Search for Java.

## Быстрые ответы
- **Какова основная цель?** Установить уникальные порты и каталоги для каждого поискового узла, предотвращая конфликты.
- **Нужна ли лицензия?** Да, для использования в продакшене требуется пробная или полная лицензия.
- **Какая версия Java поддерживается?** Java 8 или выше.
- **Можно ли запускать это на облачных серверах?** Конечно — только убедитесь, что порты открыты в группах безопасности.
- **Сколько узлов можно добавить?** Жёсткого ограничения нет; добавляйте столько, сколько позволяют ваше оборудование и сеть.

## Что такое «configure base port groupdocs»?
Когда вы **configure base port groupdocs**, вы задаёте начальный TCP‑порт, который будет использовать каждый узел (и будет увеличиваться для последующих узлов). Этот простой шаг устраняет ошибку «порт уже используется» и закладывает основу для чистого, горизонтально масштабируемого поискового кластера.

## Почему стоит использовать GroupDocs.Search для масштабируемой сети?
- **Высокая производительность** — оптимизированные алгоритмы индексации и поиска.
- **Гибкая архитектура** — вы можете комбинировать индексаторы, поисковики, шарды и экстракторы между узлами.
- **Лёгкая интеграция** — работает с любым Java‑приложением, как в локальном, так и в облачном окружении.
- **Надёжное лицензирование** — пробные варианты позволяют протестировать решение перед покупкой.

## Предварительные требования
- **Java Development Kit (JDK)** 8 или новее.
- **IDE** — например, IntelliJ IDEA или Eclipse.
- **GroupDocs.Search for Java** — библиотека версии 25.4 или новее, установленная через Maven или вручную.
- Базовые знания сетей (TCP‑порты, localhost vs. удалённые хосты).

## Установка GroupDocs.Search for Java

### Инструкции по установке

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

**Прямое скачивание:**

В качестве альтернативы скачайте последнюю версию по ссылке [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Приобретение лицензии

- **Бесплатная проба** — начните тестировать сразу.
- **Временная лицензия** — получите расширенную пробную версию на странице [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Полная покупка** — необходима для продакшн‑развёртываний.

### Базовая инициализация и настройка

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Руководство по реализации

### Как настроить базовый порт GroupDocs

#### Настройка базовых путей

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Зачем:** Последовательная структура каталогов позволяет каждому узлу находить свои файлы индекса, шарда или экстрактора без двусмысленностей.

#### Конфигурация базового порта

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Зачем:** Выбор высокого номера порта (например, 49100) уменьшает вероятность столкновения с обычными сервисами. Увеличивайте порт для каждого дополнительного узла.

#### Определение адреса хоста

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Зачем:** Использование `localhost` идеально для разработки; замените его на IP‑адрес или DNS‑имя вашего сервера в продакшене.

#### Создание сетевой конфигурации

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Зачем:** Эти параметры балансируют скорость и эффективность использования хранилища, предоставляя лёгкий, но мощный поисковый индекс.

#### Добавление узлов

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Зачем:** Распределение задач между узлами (индексация vs. поиск, шардинг vs. экстракция) повышает параллелизм и отказоустойчивость.

#### Завершение конфигурации

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Распространённые проблемы и решения

- **Конфликты портов** — Всегда увеличивайте `basePort` для каждого нового узла. Проверяйте с помощью `netstat` или мониторинга портов ОС.
- **Отсутствующие каталоги** — Убедитесь, что все указанные папки (`Indexer0`, `Searcher0` и т.д.) существуют и процесс Java имеет права чтения/записи.
- **Доступность сети** — При переходе к многомашинной конфигурации замените `127.0.0.1` на реальный IP хоста и откройте выбранные порты в брандмауэрах.

## Практические применения

| Сценарий | Преимущество настройки базового порта GroupDocs |
|----------|--------------------------------------------|
| Корпоративное управление документами | Бесшовное масштабирование между отделами без простоя |
| Большие CMS‑платформы | Быстрее извлечение контента благодаря распределённому индексу |
| Управление юридическими делами | Параллельная экстракция PDF‑файлов снижает задержку поиска |

## Соображения по производительности

- **Мониторинг CPU/Memory** — Используйте JMX Java или профилировщик для наблюдения за загрузкой потоков.
- **Настройка сжатия** — `Compression.High` экономит место на диске, но может увеличить нагрузку на CPU; протестируйте как `High`, так и `Normal`.
- **Регулярные обновления** — Новые версии GroupDocs.Search часто включают патчи производительности.

## Заключение

Теперь вы знаете, как **configure base port groupdocs** и настроить многопользовательскую поисковую сеть с помощью GroupDocs.Search for Java. Экспериментируйте с добавлением новых узлов, подстраивайте параметры индекса и интегрируйте сеть в существующие приложения для действительно масштабируемого поискового решения.

## Часто задаваемые вопросы

**В: Какова цель отключения стоп‑слов при индексации?**  
О: Отключение стоп‑слов может повысить точность поиска, сохраняя общие термины, которые могут быть критичны в специализированных областях.

**В: Как справиться с конфликтами портов при добавлении нескольких узлов?**  
О: Начните с высокого `basePort` (например, 49100) и увеличивайте его для каждого последующего узла, гарантируя уникальную TCP‑точку для каждого узла.

**В: Можно ли использовать эту настройку для облачных приложений?**  
О: Да — просто убедитесь, что выбранные порты открыты в группах безопасности вашего облака и замените `127.0.0.1` на соответствующий публичный или приватный IP.

**В: Чем отличается NormalIndex от других типов индексов?**  
О: `NormalIndex` предлагает сбалансированный компромисс между скоростью и использованием памяти, тогда как специализированные индексы (например, `FastIndex`) ориентированы на нишевые сценарии производительности.

**В: Есть ли ограничение на количество узлов, которые можно добавить?**  
О: Технически нет; ограничение определяется только вашими аппаратными ресурсами и пропускной способностью сети.

---

**Последнее обновление:** 2026-01-24  
**Тестировано с:** GroupDocs.Search Java 25.4  
**Автор:** GroupDocs
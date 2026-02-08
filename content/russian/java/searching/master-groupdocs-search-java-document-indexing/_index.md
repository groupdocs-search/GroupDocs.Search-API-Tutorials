---
date: '2026-02-08'
description: Узнайте, как подсвечивать результаты поиска в Java и как индексировать
  документы Java с помощью GroupDocs.Search for Java, используя синхронную и асинхронную
  индексацию.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: Подсветка результатов поиска Java – Синхронная и асинхронная индексация
type: docs
url: /ru/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Выделение результатов поиска Java – Синхронная и Асинхронная индексация

Улучшите свои Java‑приложения, **выделяя результаты поиска Java** с помощью мощной библиотеки GroupDocs.Search. Независимо от того, работаете ли вы с несколькими файлами или с огромным репозиторием, освоение как синхронной, так и асинхронной индексации позволяет предоставлять быстрые, точные результаты без блокировки потоков вашего приложения.

## Быстрые ответы
- **Что означает “highlight search results Java”?** Это отображение найденных терминов в результатах поиска с визуальными подсказками (например, HTML `<mark>` тегами), чтобы пользователи могли видеть, где запрос встречается в каждом документе.  
- **Когда следует использовать синхронную индексацию?** Для небольших и средних наборов данных, где требуется мгновенная доступность только что добавленных документов.  
- **Когда предпочтительна асинхронная индексация?** При обработке больших коллекций документов или работе в UI‑потоке, где необходимо сохранять отзывчивость приложения.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; полная лицензия открывает расширенные функции и снимает ограничения по использованию.  
- **Какая версия Java поддерживается?** Java 8 или новее.

## Что такое “highlight search results Java”?
Выделение результатов поиска в Java означает взятие необработанных совпадений, возвращаемых GroupDocs.Search, и оборачивание найденных терминов в HTML (или другую разметку), чтобы они выделялись при отображении в пользовательском интерфейсе или веб‑странице. Это улучшает пользовательский опыт, мгновенно показывая контекст каждого совпадения.

## Почему использовать GroupDocs.Search для Java?
GroupDocs.Search предоставляет высокопроизводительный, независимый от языка движок, который поддерживает:
- Индексацию и поиск в реальном времени
- Асинхронную обработку больших нагрузок
- Встроенное выделение результатов
- Поддержку многоязычных и пользовательских анализаторов  

## Предварительные требования
Перед началом убедитесь, что у вас есть:

- **Java Development Kit** (JDK 8 или новее) установлен.
- IDE, например **IntelliJ IDEA** или **Eclipse**.
- Папка, содержащая документы, которые вы хотите проиндексировать.
- Maven для управления зависимостями (или вы можете скачать JAR вручную).

### Требуемые библиотеки и зависимости
Добавьте GroupDocs.Search в ваш Maven‑проект:

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

Для прямой загрузки получите последнюю версию по ссылке [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Настройка окружения
- Проверьте, что переменная **JAVA_HOME** указывает на совместимый JDK.
- Создайте проект в вашей IDE и добавьте вышеуказанную конфигурацию Maven.
- Подготовьте каталог (например, `documents/`) с образцами текстовых, PDF‑ или Word‑файлов.

## Как настроить GroupDocs.Search для Java
1. **Установить библиотеку** – Используйте фрагмент Maven выше или скачайте JAR с [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Получить лицензию** – Начните с пробной лицензии, затем перейдите на полную при переходе в продакшн.  
3. **Инициализировать индекс** – Ниже приведён фрагмент, показывающий, как создать (или открыть) папку индекса:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Как выделять результаты поиска Java – Синхронная индексация
Синхронная индексация обрабатывает документы сразу, делая только что добавленные файлы доступными для поиска немедленно.

### Шаг 1: Создать индекс и добавить обработку ошибок
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Шаг 2: Добавить документы и выполнить поиск
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Шаг 3: Обработать результаты и **выделять результаты поиска Java**
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

`DocumentHighlighter` автоматически оборачивает найденные термины в теги `<mark>` (или любой другой формат, который вы настроите), предоставляя **выделенные результаты поиска**, готовые к отображению.

## Как выделять результаты поиска Java – Асинхронная индексация
При работе с тысячами файлов блокировка основного потока нежелательна. Асинхронная индексация позволяет движку работать в фоновом режиме.

### Шаг 1: Настроить индекс с обработчиками событий
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Шаг 2: Включить асинхронный режим и начать индексацию
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

Пока индекс строится, ваше приложение может продолжать обслуживать другие запросы. Как только событие `StatusChanged` сообщает `Ready`, вы можете безопасно выполнять поиск и получать **выделенные результаты поиска Java**.

## Как **индексировать документы java** – Практические советы
- **Размер пакета**: Для огромных коллекций разбивайте папку на более мелкие пакеты, чтобы избежать всплесков памяти.  
- **Фильтры файлов**: Используйте `IndexingOptions.setFileExtensions`, чтобы включать только необходимые форматы (например, `.pdf`, `.docx`).  
- **Переиндексация**: Когда документы меняются, вызывайте `index.update(documentPath)` вместо полной перестройки индекса.

## Соображения по производительности
- **Память**: Следите за использованием кучи; увеличьте `-Xmx`, если обрабатываете много больших файлов.  
- **CPU**: Асинхронная индексация распределяет нагрузку, но всё равно потребляет процессор — контролируйте её с помощью JVisualVM.  
- **Выделение результатов**: Выделение добавляет небольшие накладные расходы; кэшируйте сгенерированный HTML, если нужно многократно отображать результаты.

## Часто задаваемые вопросы

**В: Можно ли комбинировать синхронную и асинхронную индексацию в одном приложении?**  
О: Да. Используйте синхронную индексацию для небольших часто обновляемых наборов и асинхронную индексацию для массового импорта или фоновых задач.

**В: Как настроить стиль выделения?**  
О: Предоставьте собственную реализацию `DocumentHighlighter`, которая записывает нужные HTML, CSS или XML‑теги вокруг найденных терминов.

**В: Какие типы файлов поддерживает GroupDocs.Search из коробки?**  
О: Текстовые, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML и многие другие через встроенные парсеры.

**В: Можно ли выполнять поиск сразу по нескольким языкам?**  
О: Конечно. GroupDocs.Search включает многоязычные анализаторы; просто настройте соответствующий `Analyzer` при создании индекса.

**В: Как защитить папку индекса?**  
О: Храните индекс в защищённом каталоге, задайте правильные разрешения файловой системы и рассмотрите возможность шифрования индекса с помощью функций безопасности библиотеки.

---

**Последнее обновление:** 2026-02-08  
**Тестировано с:** GroupDocs.Search 25.4 for Java  
**Автор:** GroupDocs
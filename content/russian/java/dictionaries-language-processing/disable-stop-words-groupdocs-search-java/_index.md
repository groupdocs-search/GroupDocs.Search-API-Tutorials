---
date: '2026-02-19'
description: Узнайте, как отключить стоп‑слова в поиске и добавить документы в индекс
  с помощью GroupDocs.Search для Java, повышая точность запросов.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Стоп‑слова в поиске: добавление документов в индекс с помощью GroupDocs.Search
  Java'
type: docs
url: /ru/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Стоп-слова в поиске: Добавление документов в индекс с GroupDocs.Search Java

Если вам нужно **add documents to index**, при этом убедиться, что ни один важный термин — особенно часто встречающийся — не игнорируется, вы попали по адресу. В этом руководстве мы покажем, как **disable stop words in search** с помощью GroupDocs.Search for Java, чтобы каждый токен (даже «on», «by» или «the») стал доступен для поиска и ваши результаты стали гораздо точнее.

## Быстрые ответы
- **What does “add documents to index” mean?** Это означает загрузку ваших исходных файлов в поисковый индекс, чтобы их можно было эффективно запрашивать.  
- **Why would I disable stop words?** Чтобы включить общие слова (например, «on», «the») в поиск, когда эти термины имеют смысл в вашем домене.  
- **Which library version is required?** GroupDocs.Search for Java 25.4 или новее.  
- **Do I need a license?** Бесплатная пробная версия подходит для оценки; для продакшна требуется постоянная лицензия.  
- **Can I use this in a Maven project?** Да — просто добавьте репозиторий и зависимость, показанные ниже.

## Что такое стоп-слова в поиске и почему вы можете захотеть их отключить?
Стоп-слова — это часто встречающиеся термины, которые многие поисковые движки автоматически фильтруют, чтобы ускорить запросы. Хотя это повышает производительность при общих веб‑поисках, в специализированных областях — юридические контракты, каталоги e‑commerce или технические руководства — такие слова, как «on», «by» или «as», имеют реальное значение. Отключение стоп-слов позволяет рассматривать каждое слово как значимое, гарантируя, что ни один релевантный документ не будет упущен.

## Как работает добавление документов в индекс в GroupDocs.Search?
Когда вы add documents, библиотека читает каждый файл, токенизирует его содержимое и сохраняет токены в оптимизированную структуру данных (индекс). После индексации движок может извлекать соответствующие документы за миллисекунды, даже для больших коллекций.

## Предварительные требования

- **Required Libraries**: GroupDocs.Search for Java 25.4 (or newer).  
- **Development Environment**: IntelliJ IDEA, Eclipse или любой Java IDE, который вам нравится.  
- **Basic Knowledge**: Знакомство с синтаксисом Java и концепцией индексации.

## Настройка GroupDocs.Search for Java

### Установка через Maven

Если вы используете Maven, добавьте следующее в ваш `pom.xml`:

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

Либо скачайте последнюю версию с [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Шаги получения лицензии
- **Free Trial** – начните тестировать сразу.  
- **Temporary License** – получите ограниченный по времени ключ для полной функциональности.  
- **Purchase** – приобретите постоянную лицензию для использования в продакшене.

## Базовая инициализация и настройка

Создайте экземпляр `IndexSettings`, чтобы управлять поведением индекса:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Как отключить стоп-слова в поиске (Java)

Следующая строка отключает встроенный фильтр стоп-слов:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parameters*: `setUseStopWords` принимает булево значение.  
*Purpose*: Гарантирует, что каждое слово — включая обычные стоп-слова — будет проиндексировано и доступно для поиска.

## Как добавить документы в индекс

### Определение выходного каталога

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Указание каталога документов

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Теперь каждый файл в `YOUR_DOCUMENT_DIRECTORY` **added documents to index** и готов к запросам.

## Выполнение поискового запроса

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Поскольку стоп-слова отключены, термин `"on"` будет учитываться при поиске, возвращая совпадения, которые иначе были бы проигнорированы.

## Практические применения

1. **Enterprise Document Search** – Убедитесь, что критическая терминология не фильтруется.  
2. **E‑commerce Platforms** – Улучшите поиск продуктов, индексируя каждое слово в описаниях товаров.  
3. **Legal Research Tools** – Захватывайте каждый юридический термин, даже те, которые обычно считаются стоп-словами.

## Соображения по производительности

- **Optimization Tips**: Регулярно обновляйте и очищайте ваш индекс, чтобы поддерживать высокую скорость поиска.  
- **Resource Usage**: Следите за размером кучи JVM; большие индексы могут потребовать настройки сборки мусора.  
- **Java Memory Management**: Используйте эффективные структуры данных и рассматривайте хранение вне кучи (off‑heap) для очень больших корпусов.

## Распространённые проблемы и решения

| Симптом | Вероятная причина | Решение |
|---|---|---|
| Нет результатов для общих слов | `setUseStopWords(true)` (default) | Вызовите `setUseStopWords(false)`, как показано выше. |
| Ошибки out‑of‑memory при индексации | Индексация слишком большого количества больших файлов одновременно | Индексируйте файлы партиями; увеличьте параметр JVM `-Xmx`. |
| Поиск возвращает устаревшие данные | Индекс не обновлён после добавления новых файлов | Вызовите `index.update()` или повторно добавьте изменённые документы. |

## Часто задаваемые вопросы

**Q: What are stop words?**  
A: Стоп-слова — это общие термины (например, «the», «is», «on»), которые многие поисковые движки игнорируют для ускорения запросов. Отключение их позволяет рассматривать каждый токен как доступный для поиска.

**Q: Why disable stop words in search indexes?**  
A: Когда требуется точное совпадение фраз — например, в юридических или технических документах — каждое слово имеет значение, поэтому необходимо включать стоп-слова.

**Q: How does GroupDocs.Search handle large datasets?**  
A: Библиотека использует оптимизированные структуры данных и инкрементальную индексацию, чтобы поддерживать низкое потребление памяти даже при миллионах документов.

**Q: Can I integrate GroupDocs.Search with other Java applications?**  
A: Да, API разработан для простого встраивания в любую Java‑основанную систему, от веб‑служб до настольных приложений.

**Q: What should I do if my search results are not accurate?**  
A: Убедитесь, что индекс включает все необходимые документы (`add documents to index`), при необходимости отключите фильтрацию стоп-слов и рассмотрите возможность пересоздания индекса после крупных изменений.

## Дополнительные ресурсы

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Следуя этому руководству, вы теперь знаете, как **add documents to index** и **disable stop words in search**, чтобы предоставлять более точные результаты в ваших Java‑приложениях.

---

**Last Updated:** 2026-02-19  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs
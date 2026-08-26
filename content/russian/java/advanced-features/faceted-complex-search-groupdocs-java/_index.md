---
date: '2026-08-26'
description: Узнайте, как boolean operators Java позволяют создать быстрый search
  index, выполнить content search Java и запустить faceted queries с GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Узнайте, как boolean operators Java позволяют построить быстрый search
  index, выполнить content search Java и выполнить faceted queries с GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – построить search index и faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – создать search index и faceted search
type: docs
url: /ru/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Булевы операторы Java – создание поискового индекса и фасетный поиск

## Быстрые ответы
- **Что такое фасетный поиск?** Способ фильтрации результатов по предопределённым категориям, таким как тип файла или дата.  
- **Как создать поисковый индекс Java?** Инициализировать объект `Index`, указывающий на папку, и добавить документы.  
- **Можно ли комбинировать несколько критериев с помощью булевых операторов?** Да — используйте объектно‑ориентированные запросы или булевые операторы в текстовом запросе.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; коммерческая лицензия снимает ограничения.  
- **Какой IDE лучше всего подходит?** Любой Java IDE (IntelliJ IDEA, Eclipse, NetBeans) подходит.

## Что такое «create search index java»?
Создание поискового индекса Java означает построение дисковой структуры, которая хранит текст документов и метаданные, обеспечивая мгновенное получение совпадающих документов через запросы. Индекс сопоставляет термины с идентификаторами документов, поддерживает быстрый поиск и может инкрементно обновляться при изменении файлов, предоставляя основу для мощных функций поиска.

## Почему использовать GroupDocs.Search для фасетных и сложных запросов?
GroupDocs.Search для Java предоставляет встроенную фасетизацию, поддержку Boolean‑запросов и высокопроизводительное индексирование, способное обрабатывать до 10 миллионов документов, при этом задержка запросов остаётся ниже 200 мс на типичном серверном оборудовании. Он предлагает готовые к использованию фильтры полей, богатый язык запросов и чистую совместимость с Java, что делает его идеальным для корпоративных сценариев поиска.

## Предварительные требования
- **JDK 8 или новее** установлен и настроен в вашем IDE.  
- **Maven** (или Gradle) для управления зависимостями.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Базовое знакомство с концепциями ООП в Java и структурой Maven‑проекта.

## Настройка GroupDocs.Search для Java

### Настройка Maven
Add the repository and dependency to your `pom.xml` file:

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
Alternatively, download the latest JAR from the official release page:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Приобретение лицензии
To unlock full functionality:

1. **Бесплатная пробная версия** — идеально для разработки и тестирования.  
2. **Временная оценочная лицензия** — расширяет ограничения пробной версии.  
3. **Коммерческая лицензия** — снимает все ограничения для использования в продакшене.

### Базовая инициализация и настройка
The `Index` class is the core component that represents a searchable index stored on disk. The following snippet shows how to **create a search index Java** by instantiating the `Index` class:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

With the index ready, we can move on to real‑world faceted and complex queries.

## Как использовать boolean operators java – простой фасетный поиск

Load your index, add documents, and issue a field query; the two‑step pattern lets you retrieve facet counts and filtered results in a single call. This approach gives users an intuitive way to narrow results by categories such as file type, author, or custom metadata.

### Шаг 1: Создать индекс
First, point the `Index` to a folder where the index files will be stored.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Шаг 2: Добавить документы в индекс
Tell GroupDocs.Search where your source documents live. All supported file types (PDF, DOCX, TXT, etc.) will be indexed automatically.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Шаг 3: Выполнить поиск в поле content с текстовым запросом
A quick text query filters by the `content` field. The syntax `content: Pellentesque` limits results to documents containing the word *Pellentesque* in their body text.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Шаг 4: Выполнить поиск с использованием объектного запроса
Object‑based queries give you fine‑grained control. Here we build a word query, wrap it in a field query, and execute it.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Как использовать boolean operators java – сложный поисковый запрос

To execute a complex query, combine multiple field conditions with AND/OR/NOT operators, and optionally include phrase searches. You can specify each condition using field queries, nest them with Boolean operators, and control relevance with boosting, allowing you to retrieve only the most relevant documents that satisfy all required criteria.

### Шаг 1: Создать индекс для сложных запросов
Reuse the same folder structure; you can share the index across both simple and complex scenarios.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Шаг 2: Выполнить поиск с текстовым запросом
The following query looks for files named *lorem* **and** *ipsum* **or** content containing either of two exact phrases.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Шаг 3: Выполнить поиск с объектным запросом
Object‑based construction mirrors the textual query but offers type safety and IDE assistance.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Практические применения фасетных и сложных поисков

| Сценарий | Как фасетирование помогает | Пример запроса |
|----------|----------------------------|----------------|
| **Каталог электронной коммерции** | Фильтрация по категории, цене, бренду | `category: Electronics AND price:[100 TO 500]` |
| **Хранилище юридических документов** | Сужение по номеру дела, юрисдикции | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Исследовательские архивы** | Комбинация автора, года публикации, ключевых слов | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Корпоративный интранет** | Поиск по типу файла и отделу | `filetype: pdf AND department: HR` |

These examples illustrate why mastering **boolean operators java** and **filename search java** techniques is a game‑changer for any data‑intensive application.

## Распространённые ошибки и устранение неполадок

The `SearchResult` object contains the documents that match a query and provides access to their relevance scores and highlighted fragments.  
The `CommonFieldNames` class defines standard field names such as `Content` and `FileName` used throughout the API.

- **Пустые результаты** — Убедитесь, что документы успешно добавлены (`index.getDocumentCount()` может помочь).  
- **Устаревший индекс** — После добавления или удаления файлов вызовите `index.update()`, чтобы **update index java** и поддерживать индекс в актуальном состоянии.  
- **Неправильные имена полей** — Используйте константы `CommonFieldNames` (`Content`, `FileName` и т.д.), чтобы избежать опечаток.  
- **Узкие места в производительности** — Для больших коллекций рассмотрите возможность включения `index.setCacheSize()` или использования выделенного SSD для папки индекса.  
- **Отсутствие подсветки** — Чтобы **highlight search results java**, получите совпавшие фрагменты через `SearchResult.getFragments()` (не показано здесь, но доступно в API).  

## Часто задаваемые вопросы

**Q: Можно ли использовать GroupDocs.Search с Spring Boot?**  
A: Абсолютно. Добавьте Maven‑зависимость, настройте индекс как Spring‑bean и внедрите его там, где нужны возможности поиска.

**Q: Поддерживает ли библиотека пользовательские поля метаданных?**  
A: Да — вы можете добавить пользовательские поля во время индексации и затем выполнять фасетирование по ним.

**Q: Насколько большой может стать индекс?**  
A: Дисковый индекс может обрабатывать до 10 million документов; просто обеспечьте достаточное хранилище и следите за настройками кэша.

**Q: Есть ли способ ранжировать результаты по релевантности?**  
A: GroupDocs.Search автоматически оценивает совпадения; вы можете получить оценку через `SearchResult.getDocument(i).getScore()`.

**Q: Что происходит, если я индексирую зашифрованные PDF?**  
A: Укажите пароль при добавлении документа: `index.add(filePath, password)`.

## Заключение

By now you should feel comfortable **creating a search index Java** with GroupDocs.Search, adding documents, and crafting both simple faceted queries and sophisticated Boolean searches using **boolean operators java**. These capabilities empower you to deliver fast, accurate, and user‑friendly search experiences across a wide range of applications—from e‑commerce platforms to enterprise knowledge bases.

Ready for the next step? Explore **GroupDocs.Search’s** advanced features such as **highlighting**, **suggestions**, and **real‑time indexing** to further boost your application’s search power.

---

**Last Updated:** 2026-08-26  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Связанные руководства

- [Поиск по шаблону Java с GroupDocs.Search – Расширенные возможности](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Как обновить индекс Java с GroupDocs.Search – Полное руководство](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Как реализовать полнотекстовый поиск java: создать каталог индекса с GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
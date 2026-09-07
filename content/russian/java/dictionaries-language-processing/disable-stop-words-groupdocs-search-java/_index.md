---
date: '2026-07-07'
description: Узнайте, как отключить stop words Java и добавить документы в индекс
  с помощью GroupDocs.Search for Java, повышая точность поиска и производительность.
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: Отключить stop words Java и добавить документы в индекс с GroupDocs.Search
  for Java. Следуйте этому пошаговому руководству, чтобы улучшить точность запросов
  и производительность.
og_title: Отключить stop words Java – Add Docs to Index с GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: Отключить stop words Java – Add Docs to Index с GroupDocs
type: docs
url: /ru/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Отключить стоп-слова Java – Добавление документов в индекс с GroupDocs

В этом руководстве вы узнаете, как **disable stop words java**, добавляя ваши файлы в поисковый индекс с GroupDocs.Search for Java. Отключив встроенный фильтр стоп‑слов, каждый токен — включая обычные слова, такие как «on», «by» или «the» — становится доступным для поиска, что значительно повышает релевантность результатов для специализированных областей, таких как юридические контракты, каталоги электронной коммерции или технические руководства.

## Быстрые ответы
- **Что означает «add documents to index»?** Это загрузка ваших исходных файлов в поисковый индекс, чтобы их можно было эффективно запрашивать.  
- **Почему я могу отключить стоп‑слова?** Чтобы включить общие слова (например, «on», «the») в поиск, когда эти термины имеют смысл для вашего домена.  
- **Какая версия библиотеки требуется?** GroupDocs.Search for Java 25.4 или новее.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для оценки; для продакшн‑использования требуется постоянная лицензия.  
- **Можно ли использовать это в проекте Maven?** Да — просто добавьте репозиторий и зависимость, показанные ниже.

## Что такое стоп‑слова в поиске и почему их может потребоваться отключить?
Стоп‑слова — это часто встречающиеся термины, которые многие поисковые движки автоматически фильтруют, чтобы ускорить обработку запросов. Отключение их гарантирует, что **каждое слово** — включая традиционно игнорируемые — вносит вклад в поисковый индекс, что важно, когда эти слова несут доменно‑специфическое значение. Например, в юридическом контракте слово «by» может различать стороны, а в каталоге продуктов «on» может быть частью названия модели.

## Как работает добавление документов в индекс в GroupDocs.Search?
Когда вы добавляете документы, GroupDocs.Search читает каждый файл, токенизирует содержимое и сохраняет токены в оптимизированном обратном индексе. Эта структура обеспечивает поиск за доли секунды даже для коллекций, содержащих **сотни тысяч файлов**. Библиотека также поддерживает инкрементные обновления, позволяя поддерживать индекс актуальным без полной перестройки.

## Предварительные требования
- **Требуемые библиотеки**: GroupDocs.Search for Java 25.4 (или новее).  
- **Среда разработки**: IntelliJ IDEA, Eclipse или любой другой Java IDE по вашему выбору.  
- **Базовые знания**: Знакомство с синтаксисом Java и концепцией индексации.

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
Alternatively, download the latest version from [выпуски GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/).

#### Шаги получения лицензии
- **Бесплатная пробная версия** – начните тестировать сразу.  
- **Временная лицензия** – получите ограниченный по времени ключ для полной функциональности.  
- **Покупка** – приобретите постоянную лицензию для использования в продакшн.

## Базовая инициализация и настройка
IndexSettings — это класс конфигурации, определяющий, как создаётся и ищется индекс, а также какие функции включены.

Создайте экземпляр `IndexSettings`, чтобы управлять поведением индекса:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Как отключить стоп‑слова в поиске (Java)?
IndexSettings — это объект конфигурации, контролирующий поведение поискового индекса. По умолчанию он включает встроенный фильтр стоп‑слов. Чтобы отключить этот фильтр, вызовите метод `setUseStopWords(false)` у экземпляра `IndexSettings`. Этот единственный вызов отключает удаление стоп‑слов, гарантируя, что каждый токен — включая общие слова, такие как «on» или «the» — будет проиндексирован и доступен для запросов.

## Как добавить документы в индекс
Добавление документов в индекс осуществляется созданием объекта `Index` с нужными `IndexSettings` и последующим вызовом его метода `add` для каждого файла или папки. Библиотека читает каждый документ, токенизирует его содержимое и сохраняет полученные термы в обратный индекс, делая их мгновенно доступными для поиска. Вы можете указать индекс в конкретный каталог вывода и задать исходную папку, содержащую файлы для индексации.

### Определение каталога вывода

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### Указание каталога документов

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## Выполнение поискового запроса

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Поскольку `disable stop words java` активен, запрос, содержащий термин «"on"», будет обработан, возвращая совпадения, которые иначе были бы проигнорированы фильтром по умолчанию.

## Практические применения
1. **Поиск корпоративных документов** – Сохранить критически важную терминологию, которая была бы удалена списками стоп‑слов по умолчанию.  
2. **Платформы электронной коммерции** – Повысить обнаруживаемость продуктов, индексируя каждое слово в описаниях, номерах моделей и спецификациях.  
3. **Инструменты юридических исследований** – Захватывать каждый юридический термин, даже те, которые обычно считаются стоп‑словами, чтобы не пропустить важные положения.

## Соображения по производительности
- **Советы по оптимизации**: Регулярно обновляйте и очищайте ваш индекс, чтобы поддерживать высокую скорость поиска. GroupDocs.Search может обрабатывать **до 1 миллиона документов**, сохраняя время отклика менее секунды.  
- **Использование ресурсов**: Следите за размером кучи JVM; большие индексы могут требовать максимальную кучу (`-Xmx`) в 4 ГБ или более.  
- **Управление памятью Java**: Используйте варианты хранения вне кучи для очень больших корпусов, чтобы удерживать потребление кучи ниже 2 ГБ.

## Распространённые проблемы и решения

| Симптом | Вероятная причина | Решение |
|---|---|---|
| Нет результатов для общих слов | `setUseStopWords(true)` (по умолчанию) | Вызовите `setUseStopWords(false)`, как показано выше. |
| Ошибки Out‑of‑memory при индексации | Индексация слишком большого количества больших файлов одновременно | Индексируйте файлы пакетами; увеличьте параметр JVM `-Xmx`. |
| Поиск возвращает устаревшие данные | Индекс не обновлён после добавления новых файлов | Вызовите `index.update()` или повторно добавьте изменённые документы. |

## Часто задаваемые вопросы

**Q: Что такое стоп‑слова?**  
A: Стоп‑слова — это общие термины (например, «the», «is», «on»), которые многие поисковые движки игнорируют для ускорения запросов. Отключение их позволяет рассматривать каждый токен как доступный для поиска.

**Q: Почему отключать стоп‑слова в поисковых индексах?**  
A: Когда требуется точное совпадение фраз — например, в юридических или технических документах — каждое слово имеет значение, поэтому необходимо включать стоп‑слова.

**Q: Как GroupDocs.Search обрабатывает большие наборы данных?**  
A: Библиотека использует оптимизированные структуры данных и инкрементную индексацию, чтобы поддерживать низкое потребление памяти, даже при **миллионах документов**.

**Q: Могу ли я интегрировать GroupDocs.Search с другими Java‑приложениями?**  
A: Да, API разработан для простого встраивания в любую систему на Java, от веб‑сервисов до настольных приложений.

**Q: Что делать, если результаты поиска неточны?**  
A: Убедитесь, что индекс включает все необходимые файлы (`add documents to index`), проверьте, что фильтрация стоп‑слов отключена при необходимости, и рассмотрите возможность перестроения индекса после значительных изменений.

## Дополнительные ресурсы
- **Документация**: [Документация GroupDocs Search](https://docs.groupdocs.com/search/java/)
- **Справочник API**: [Справочник API GroupDocs](https://reference.groupdocs.com/search/java)
- **Скачать**: [Скачать последнюю версию GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **Репозиторий GitHub**: [Исследовать на GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Бесплатная поддержка**: [Присоединиться к форуму GroupDocs](https://forum.groupdocs.com/c/search/10)
- **Временная лицензия**: [Подать заявку на временную лицензию](https://purchase.groupdocs.com/temporary-license/)

Следуя этому руководству, вы теперь знаете, как **add documents to index** и **disable stop words java**, чтобы предоставлять более точные результаты поиска в ваших Java‑приложениях.

---

**Последнее обновление:** 2026-07-07  
**Тестировано с:** GroupDocs.Search for Java 25.4  
**Автор:** GroupDocs  

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## Связанные руководства
- [Обработка языка Java – Создание словаря синонимов с GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Как добавить документы в индекс с мета‑данными в Java с использованием GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Как добавить документы в индекс с GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
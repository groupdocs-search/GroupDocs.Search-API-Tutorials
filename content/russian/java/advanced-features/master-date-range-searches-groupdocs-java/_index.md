---
date: '2026-10-07'
description: Узнайте, как реализовать поиск с пользовательским форматом даты java
  в GroupDocs, охватывая запросы диапазона дат, пользовательские шаблоны и рекомендации
  по производительности.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Руководство по Custom date format java показывает, как настроить GroupDocs.Search
  для Java, выполнять запросы диапазона дат и повышать производительность. Следуйте
  пошаговым примерам.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Custom date format java – руководство по поиску диапазона дат с GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Custom date format java | поиск диапазона дат с GroupDocs
type: docs
url: /ru/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Пользовательский формат даты java | поиск диапазона дат с GroupDocs

Поиск документов по дате — частое требование, будь то создание архивной системы, инструмента финансовой отчетности или портала управления контентом. В этом руководстве вы изучите техники **custom date format java** с использованием GroupDocs.Search, охватывающие запросы диапазона дат, определения пользовательских шаблонов и советы по **optimize search performance**. К концу вы сможете позволить пользователям получать записи, попадающие в любой интервал дат, независимо от используемого формата.

## Быстрые ответы
- **Каков основной класс для индексации?** `Index` from the `com.groupdocs.search` package.  
- **Как определить пользовательский шаблон даты?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Можно ли выполнять поиск текстовым запросом?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Какие координаты Maven требуются?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Нужна ли лицензия для разработки?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## Что такое custom date format java?
Custom date format java сообщает GroupDocs.Search, как интерпретировать строки дат, которые не соответствуют шаблону ISO по умолчанию (YYYY‑MM‑DD). Определяя собственный шаблон — например `MM/dd/yyyy` или `dd‑MM‑yyyy` — вы позволяете движку распознавать даты, встроенные в документы, использующие региональные или устаревшие форматы. Эта возможность позволяет индексировать и выполнять запросы по датам последовательно в разных источниках, улучшая как полноту, так и точность поисков, ориентированных на даты.

## Почему использовать GroupDocs.Search для запросов диапазона дат?
GroupDocs.Search сочетает высокоскоростную индексацию с гибким построением запросов, делая его идеальным для сценариев с диапазонами дат. Движок может быстро находить документы, содержащие даты в указанном интервале, даже когда эти даты находятся в свободном тексте или полях метаданных. Встроенная поддержка множества форматов файлов и настраиваемых парсеров дат позволяет работать с разнородными коллекциями документов без написания кода, специфичного для формата, при этом достигая субсекундных откликов на больших индексах.

## Как искать документы по дате с GroupDocs.Search
Вы настроите библиотеку, проиндексируете примерную папку и затем выполните как простые текстовые запросы, так и более сложные объектные запросы. Процесс начинается с создания экземпляра `Index`, настройки необходимых пользовательских форматов дат и вызова API поиска либо строкой, либо структурированным `SearchQuery`. Такой подход позволяет выбрать уровень контроля, соответствующий требованиям вашего приложения.

### Требования
- Java 8 или новее установлен.  
- Maven для управления зависимостями.  
- Доступ к лицензии GroupDocs.Search (пробная или временная подходит для разработки).  

### Настройка GroupDocs.Search для Java

#### Установка с помощью Maven
Add the repository and dependency to your `pom.xml`:

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

#### Прямое скачивание
В качестве альтернативы вы можете скачать последнюю версию напрямую с [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Базовая инициализация и настройка
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** Класс `Index` является основным контейнером, который хранит поисковые метаданные для каждого добавляемого файла, обеспечивая быстрый поиск по большим коллекциям.

## Функция 1: создание запросов поиска диапазона дат

### Использование текстового запроса
The simplest way is to embed the date range directly in the query string:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** Загрузите ваш индекс, затем вызовите `search("daterange(2022-01-01 ~~ 2022-12-31)")`, чтобы получить каждый документ, у которого индексированная дата находится между 1 января 2022 года и 31 декабря 2022 года. Этот однострочный запрос работает сразу из коробки и возвращает результаты, отсортированные по релевантности.

**Explanation:** Синтаксис `daterange` ожидает даты в формате `YYYY‑MM‑DD`. Он возвращает все документы, у которых индексированные даты попадают в указанный интервал.

### Использование объектного запроса
For programmatic control and custom parsing, build a `SearchQuery` object. The `SearchQuery` class represents a structured query that can combine multiple criteria such as keywords, filters, and date ranges.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** Сконструируйте `SearchQuery` с помощью `createDateRangeQuery(startDate, endDate)`, где `startDate` и `endDate` — экземпляры `java.util.Date`; затем передайте запрос в `index.search(query)`, чтобы получить точные результаты с учётом смещений часовых поясов и локальных календарей.

**Definition anchor:** Класс `SearchQuery` инкапсулирует все критерии поиска, позволяя комбинировать диапазоны дат с фильтрами по ключевым словам, логическими операторами и правилами повышения релевантности.

**Explanation:** `createDateRangeQuery` позволяет передавать объекты `java.util.Date`, предоставляя полную гибкость в работе с часовыми поясами и локальными особенностями.

## Функция 2: указание шаблонов custom date format java

### Установка пользовательских форматов даты
The `DateFormat` class tells the engine how to split and interpret a date string based on element order and separator characters. Define a `DateFormat` that matches your document’s date representation:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Очистите стандартные форматы с помощью `dateFormat.clear()`, затем добавьте новый `DateFormat`, построенный из объектов `DateFormatElement` (month, day, year) и задайте разделитель `/`. После этого движок корректно будет разбирать даты, записанные как `MM/dd/yyyy`, как при индексации, так и при выполнении запросов.

**Definition anchor:** `DateFormat` — это объект конфигурации, который сообщает GroupDocs.Search, как разбивать и интерпретировать строку даты в зависимости от порядка элементов и символов‑разделителей.

**Explanation:** Очистив стандартные форматы и добавив `DateFormat`, использующий `/` в качестве разделителя, движок теперь понимает даты, записанные как `MM/dd/yyyy`. Это необходимо для **search documents by date** в регионах, где предпочтительна запись месяц‑день‑год.

## Советы по оптимизации производительности поиска
- **Индексировать инкрементально:** Добавляйте новые файлы в существующий индекс вместо полной перестройки; это снижает нагрузку на процессор до 70 % при ежедневных обновлениях.  
- **Удалять устаревшие данные:** Периодически удаляйте документы, которые больше не нужны; облегчённый индекс улучшает коэффициент попаданий в кэш и уменьшает задержку запросов.  
- **Настроить параметры памяти:** Увеличьте размер кучи JVM (`-Xmx4g` или выше), когда работаете с индексами более 5 GB, чтобы избежать ошибок out‑of‑memory.  
- **Включить многопоточную индексацию:** Используйте `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` для параллельной обработки документов и сокращения времени индексации примерно на количество ядер процессора.

## Распространённые проблемы и решения
- **Ошибки разбора дат:** Убедитесь, что строки дат в документе точно соответствуют определённому вами пользовательскому шаблону; несоответствие разделителей или отсутствие ведущих нулей приводит к сбоям.  
- **Отсутствие результатов:** Проверьте, что проиндексированные поля содержат метаданные даты; если документ имеет даты только в свободных текстовых абзацах, включите опцию `ExtractDateMetadata` при индексации.  
- **Исключения доступа к индексу:** Убедитесь, что путь `indexFolder` доступен для записи и не заблокирован другим процессом; используйте отдельную папку для каждой среды (dev, test, prod), чтобы избежать конфликтов.

## Практические применения
1. **Archival systems** – Получайте записи за определённый исторический период без ручной нормализации дат.  
2. **Content management** – Поддержка региональных форматов дат, таких как `dd/MM/yyyy`, для европейской аудитории, повышая удовлетворённость пользователей.  
3. **Financial software** – Быстрая фильтрация транзакций по финансовому кварталу или году, позволяя создавать панели реального времени.

## Почему это важно
Внедрение обработки **custom date format java** устраняет трения, связанные с несогласованными представлениями дат в разных документах. Это позволяет **handle multiple date formats** в одном индексе, гарантируя, что конечные пользователи получают точные результаты независимо от того, как изначально были записаны даты. Такая гибкость повышает релевантность поиска, снижает затраты на предварительную обработку и сокращает время получения ценности для приложений, ориентированных на даты.

## Следующие шаги
- Исследуйте более сложные комбинации запросов с использованием операторов `AND`, `OR` и `NOT`.  
- Поэкспериментируйте с пользовательскими анализаторами, если необходимо индексировать дополнительную временную метаинформацию, такую как метки времени, встроенные в XML‑теги.  
- Ознакомьтесь с руководством по настройке производительности в официальной документации, чтобы масштабировать решение до миллионов документов и многопользовательских сред.

## Часто задаваемые вопросы

**Q: What is the difference between text form and object‑based date queries?**  
A: Text form is quick and easy but limited to the default ISO format; object‑based queries let you supply `Date` objects and custom formats for greater flexibility.

**Q: Can I search for multiple date ranges in a single query?**  
A: Yes, combine `daterange` clauses with logical operators like `AND` or `OR` to build complex queries.

**Q: Will custom date formats slow down the search?**  
A: There is a minor overhead for additional parsing, but the impact is negligible for typical workloads and is outweighed by the accuracy gains.

**Q: Is GroupDocs.Search suitable for large‑scale deployments?**  
A: Absolutely. With proper indexing strategies and JVM tuning, it scales to millions of documents while maintaining sub‑second query response times.

**Q: Where can I find more Java examples?**  
A: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) for additional samples and use‑case implementations.

---

**Ресурсы**

- **Документация:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **Справочник API:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Скачать:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **Репозиторий GitHub:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Посмотреть на GitHub:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Форум бесплатной поддержки:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Временная лицензия:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-10-07  
**Тестировано с:** GroupDocs.Search Java 25.4  
**Автор:** GroupDocs  

## Связанные руководства

- [Groupdocs Search Java: Расширенные функции поиска](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Библиотека полнотекстового поиска Java – Оптимизация индекса с GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Как добавить документы в индекс с помощью индексирования метаданных в Java с использованием GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
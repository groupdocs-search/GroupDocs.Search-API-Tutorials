---
date: '2026-01-29'
description: Узнайте, как реализовать логические запросы И/ИЛИ в Java с помощью GroupDocs.Search,
  добавить документы в индекс и улучшить поиск документов.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean and or: Освойте булевые поиски с GroupDocs.Search для Java'
type: docs
url: /ru/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Освойте булевый поиск с GroupDocs.Search для Java

Поиск в огромных коллекциях документов может напоминать поиск иголки в стоге сена. С помощью запросов **java boolean and or** вы можете точно указать движку, что вам нужно — документы, содержащие *оба* термина, *любой* из терминов, или *исключающие* нежелательные слова. В этом руководстве мы пройдем настройку **GroupDocs.Search for Java**, добавление документов в индекс и создание мощных булевых запросов, которые ускорят ваши рабочие процессы **document retrieval java**.

## Быстрые ответы
- **Что такое запрос boolean AND?** Возвращает только документы, содержащие *все* указанные термины.  
- **Чем отличается OR от AND?** OR находит документы с *любым* из терминов, расширяя набор результатов.  
- **Когда следует использовать NOT?** Используйте NOT, чтобы отфильтровать документы, содержащие нежелательные слова.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для тестирования; для продакшна требуется коммерческая лицензия.  
- **Какая версия Java требуется?** Поддерживается Java 8+; рекомендуется JDK 11+.

## Что такое **java boolean and or**?
Запрос **java boolean and or** сочетает логические операторы (AND, OR, NOT) для уточнения результатов поиска. Формируя запросы, вы указываете GroupDocs.Search, как термины взаимосвязаны, получая точный контроль над процессом извлечения.

## Почему стоит использовать GroupDocs.Search для Java?
- **High performance** при работе с большими наборами документов.  
- **Rich API**, поддерживающий как текстовые, так и объектные запросы.  
- **Built‑in language support** для стемминга, стоп‑слов и нечеткого поиска.  
- **Easy integration** с Maven или прямой загрузкой JAR.

## Предварительные требования
Прежде чем приступать, убедитесь, что у вас есть:
- **GroupDocs.Search for Java** (v25.4 или новее) – ссылка для скачивания ниже.  
- JDK 8+ установлен и настроен в вашей IDE (IntelliJ IDEA, Eclipse и т.д.).  
- Базовые знания Java и Maven для управления зависимостями.

## Настройка GroupDocs.Search для Java

### Настройка Maven
Добавьте репозиторий и зависимость в ваш `pom.xml`:

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

### Прямая загрузка
Либо скачайте последнюю JAR‑файл с официального сайта: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Приобретение лицензии
Начните с бесплатной пробной лицензии, чтобы изучить все функции. Для продакшн‑использования приобретите коммерческую лицензию, чтобы открыть полный набор возможностей.

### Базовая инициализация и настройка
Создайте папку индекса и создайте объект `Index`:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: Реализация булевых поисков

Ниже мы рассмотрим запросы **AND**, **OR**, **NOT** и **complex**. Каждый раздел показывает как текстовый запрос, так и эквивалентный объектный запрос, чтобы вы могли выбрать стиль, подходящий вашему коду.

### Поиск с Boolean AND
Объединяйте термины с помощью **AND**, чтобы получить только документы, содержащие *все* ключевые слова.

#### Обзор
Запрос AND сужает результаты, повышая релевантность, когда нужны документы, соответствующие нескольким критериям.

#### Шаги реализации

1. **Initialize Index** – это также демонстрирует **add documents to index** для сценария AND.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – используя синтаксис обычной строки.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – полезно при программном построении запросов (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Поиск с Boolean OR
Используйте **OR**, чтобы расширить результаты, сопоставляя любой из указанных терминов.

#### Обзор
Запрос OR идеален для исследовательского поиска, когда нужно захватить документы, содержащие хотя бы одно из нескольких ключевых слов (**search with or java**).

#### Шаги реализации

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Поиск с Boolean NOT
Исключайте нежелательные термины с помощью **NOT**, чтобы отфильтровать шум в результатах.

#### Обзор
Запрос NOT помогает удалить нерелевантные документы, например, отфильтровать название бренда конкурента (**boolean search examples java**).

#### Шаги реализации

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Сложные булевые запросы
Комбинируйте **AND**, **OR** и **NOT**, чтобы создать сложную логику поиска для очень специфических задач извлечения.

#### Обзор
Сложные запросы позволяют моделировать реальные сценарии поиска, например, «найти спортивные статьи, которые положительные, но исключить любые упоминания конкретных спортсменов».

#### Шаги реализации

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Практические применения запросов java boolean and or
- **Document Management Systems** – находите контракты, содержащие одновременно “confidential” **AND** “renewal”.  
- **Legal Research** – фильтруйте судебные решения с помощью **AND**/**OR**, исключая устаревшие законы с помощью **NOT**.  
- **Customer Support** – получайте тикеты, где упоминаются “login” **AND** “error”, но не “resolved”.  
- **Content Curation** – собирайте блоги о “cloud” **OR** “serverless” для рассылки.

## Распространённые ошибки и устранение неполадок
- **Missing Index Refresh** – после добавления новых документов вызовите `index.update()`, чтобы они стали доступными для поиска.  
- **Incorrect Operator Spacing** – GroupDocs.Search требует пробелы вокруг операторов (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – запросы по умолчанию нечувствительны к регистру, но пользовательские анализаторы могут изменить это.  
- **Large Result Sets** – используйте пагинацию (`search(query, 0, 100)`), чтобы избежать перегрузки памяти.

## Часто задаваемые вопросы

**Q: Можно ли объединить более двух терминов в запросе AND?**  
A: Конечно. Вы можете соединять несколько объектов `createWordQuery` с помощью `createAndQuery`, либо просто написать `"term1 AND term2 AND term3"` в текстовом запросе.

**Q: Поддерживает ли GroupDocs.Search поиск с подстановочными знаками или нечеткий поиск?**  
A: Да. Добавьте `*` для подстановки (например, `promot*`) или используйте `~` для нечеткого совпадения (например, `comfort~`).

**Q: Как ограничить поиск определенными типами файлов?**  
A: Используйте класс `FileTypeQuery` для ограничения результатов PDF, DOCX и т.д., и комбинируйте его с вашим булевым запросом.

**Q: Как лучше всего контролировать производительность индексации?**  
A: Включите встроенный логгер (`index.getLogger().setLevel(Level.INFO)`) и просмотрите метрики времени после каждой операции `add`.

**Q: Есть ли способ повысить релевантность определенных терминов?**  
A: Да. Оберните важные слова в `BoostQuery`, чтобы увеличить их вес в алгоритме оценки.

---

**Последнее обновление:** 2026-01-29  
**Тестировано с:** GroupDocs.Search 25.4 (Java)  
**Автор:** GroupDocs
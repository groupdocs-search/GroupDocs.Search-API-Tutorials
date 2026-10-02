---
date: '2026-10-02'
description: Узнайте, как использовать temporary license для добавления documents
  в index с помощью chunk‑based search в Java, повышая производительность поиска и
  контролируя использование памяти.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Используйте temporary license для добавления documents в index с chunk‑based
  search в Java, улучшая скорость поиска и снижая потребление памяти.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Используйте temporary license для chunk‑based indexing в Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Используйте temporary license для chunk‑based indexing в Java
type: docs
url: /ru/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Используйте временную лицензию для индексирования по фрагментам в Java

В этом руководстве вы **используете временную лицензию** для добавления документов в индекс с помощью функции поиска по фрагментам GroupDocs.Search. Этот подход позволяет работать с огромными коллекциями документов — юридическими контрактами, заявками в службу поддержки, научными статьями — при низком потреблении **java search index memory** и значительном **повышении производительности поиска**. Вы увидите, как настроить папку индекса, загрузить несколько источников документов, включить поиск по фрагментам и выполнить как первый, так и последующие запросы по фрагментам.

## Быстрые ответы
- **Что является первым шагом?** Создайте папку поискового индекса.  
- **Как включить множество файлов?** Используйте `index.add()` для каждой папки с документами.  
- **Какая опция включает поиск по фрагментам?** `options.setChunkSearch(true)`.  
- **Можно ли продолжить поиск после первого фрагмента?** Да, вызовите `index.searchNext()` с токеном.  
- **Нужна ли лицензия?** Бесплатная пробная версия или временная лицензия подходят для разработки; полная лицензия требуется для продакшн.

## Что вы узнаете
- Как создать поисковый индекс в указанной папке.  
- Шаги для **добавления документов в индекс** из нескольких мест.  
- Настройка параметров поиска для включения поиска по фрагментам.  
- Выполнение начального и последующего поиска по фрагментам.  
- Реальные сценарии, где поиск по фрагментам документов проявляет себя.

## Предварительные требования
Чтобы следовать этому руководству, убедитесь, что у вас есть:

- **Необходимые библиотеки**: GroupDocs.Search для Java 25.4 или новее.  
- **Настройка окружения**: Установленный совместимый Java Development Kit (JDK).  
- **Требования к знаниям**: Базовое программирование на Java и знакомство с Maven.

## Настройка GroupDocs.Search для Java
Для начала интегрируйте GroupDocs.Search в ваш проект с помощью Maven:

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

В качестве альтернативы загрузите последнюю версию с [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Приобретение лицензии
Чтобы попробовать GroupDocs.Search:

- **Бесплатная пробная версия** – протестировать основные функции без обязательств.  
- **Временная лицензия** – расширенный доступ для разработки.  
- **Покупка** – полная лицензия для использования в продакшн.

## Как добавить документы в индекс?
**Прямой ответ:** Вызовите `index.add()` для каждой папки, содержащей файлы, которые вы хотите сделать доступными для поиска; метод рекурсивно сканирует папку и добавляет каждый поддерживаемый документ в индекс одной операцией. Это устраняет необходимость ручной обработки файлов по отдельности и ускоряет массовое импортирование.

`SearchIndex` — центральный класс, представляющий поисковую коллекцию на диске. После его создания все операции индексации и запросов проходят через этот объект.

### 1. Создание индекса
**Прямой ответ:** Создайте объект `SearchIndex` с путем, где должны храниться файлы индекса, затем вызовите `index.create()` для инициализации структуры хранилища. Этот вызов создаёт необходимые папки и файлы метаданных при первом использовании.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Добавление документов в индекс
**Прямой ответ:** Используйте метод `index.add()` и передайте абсолютный путь каждой исходной папки; API автоматически определяет поддерживаемые форматы (PDF, DOCX, XLSX и т.д.) и извлекает текст для поиска в индекс.

`SearchOptions` — объект конфигурации, позволяющий точно настроить обработку документов во время индексации и поиска. Позже вы будете использовать его для включения запросов по фрагментам.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Настройка параметров поиска для фрагментного поиска
**Прямой ответ:** Установите `options.setChunkSearch(true)` в экземпляре `SearchOptions` перед выполнением запроса; это указывает движку разбивать каждый документ на логические фрагменты (обычно абзацы) и возвращать совпадения по фрагменту, а не по всему файлу.

`SearchResult` содержит найденные фрагменты, их позиции и оценки релевантности. Когда включён поиск по фрагментам, каждый `SearchResult` соответствует отдельному фрагменту исходного документа.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Выполнение начального поиска по фрагментам
**Прямой ответ:** Выполните `index.search("your query", options)`; вызов возвращает коллекцию `SearchResult` для первого набора совпадающих фрагментов и токен, представляющий состояние поиска для продолжения.

Возвращённый токен необходим для постраничного обхода больших наборов результатов без повторного выполнения полного запроса.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Продолжение поиска по фрагментам
**Прямой ответ:** Передайте токен, полученный от предыдущего вызова, в `index.searchNext(token, options)`; повторяйте, пока метод не вернёт `null`, что указывает на то, что все совпадающие фрагменты получены.

Этот пошаговый подход сохраняет низкое потребление памяти, поскольку в памяти находится только текущая партия фрагментов.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Почему использовать поиск по фрагментам?
Поиск по фрагментам разбивает огромные коллекции документов на управляемые части, снижая нагрузку на память и ускоряя время отклика. Индексируя на уровне абзаца или раздела, движок может извлекать только релевантные фрагменты, что уменьшает использование CPU и улучшает задержку для конечных пользователей. Это особенно полезно, когда:

1. **Юридические команды** нужно находить конкретные пункты в тысячах контрактов.  
2. **Порталы поддержки клиентов** должны мгновенно показывать релевантные статьи базы знаний.  
3. **Исследователи** просеивают обширные наборы данных без загрузки целых файлов в память.  

Конкретное утверждение: GroupDocs.Search может обрабатывать **PDF‑файлы более 500 страниц** менее чем за **2 секунды на фрагмент** на стандартном 8‑ядерном сервере, при этом пиковый размер кучи остаётся ниже **200 МБ**.

## Как этот подход повышает производительность поиска
**Прямой ответ:** Ища небольшие фрагменты вместо целых файлов, движок может раннее пропускать нерелевантные части, уменьшать количество CPU‑циклов и держать в памяти только активный фрагмент, что напрямую снижает потребление **java search index memory** и обеспечивает более быстрые ответы. Такой целевой подход также позволяет более эффективно кэшировать и выполнять параллельную обработку, позволяя нескольким ядрам одновременно обрабатывать разные фрагменты, что дополнительно повышает пропускную способность на многопроцессорных серверах.

Дополнительные преимущества включают:

- Параллельная обработка фрагментов на нескольких ядрах.  
- Раннее завершение, когда найдено совпадение с высокой релевантностью.

## Управление памятью java search index
**Прямой ответ:** Выделите достаточный размер кучи JVM (например, `-Xmx2g` или больше) в зависимости от ожидаемого размера индекса, выполните `index.optimize()` после массового добавления для сжатия структуры индекса и контролируйте паузы сборки мусора с помощью VisualVM, чтобы избежать всплесков задержки.

Дополнительные рекомендации по настройке:

- Используйте `index.flush()` после больших пакетов, чтобы записать промежуточные данные на диск.  
- Включите `options.setMemoryLimit(256)`, чтобы ограничить потребление памяти на один поиск.

## Соображения по производительности
- **Управление памятью** – Выделите достаточное пространство кучи (`-Xmx`) для больших индексов.  
- **Мониторинг ресурсов** – Следите за использованием CPU во время индексации и поиска.  
- **Обслуживание индекса** – Периодически перестраивайте или очищайте индекс, чтобы удалить устаревшие данные.

## Распространённые ошибки и устранение неполадок
| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| `OutOfMemoryError` во время индексации | Размер кучи слишком мал | Увеличьте размер кучи JVM (`-Xmx2g` или больше) |
| Нет результатов | Токен фрагмента не обработан | Убедитесь, что цикл `while` выполняется до тех пор, пока `getNextChunkSearchToken()` не вернёт `null` |
| Низкая производительность поиска | Индекс не оптимизирован | Выполните `index.optimize()` после массового добавления |

## Часто задаваемые вопросы

**Q: Что такое поиск по фрагментам?**  
A: Поиск по фрагментам делит набор данных на более мелкие части, позволяя выполнять эффективные запросы к большим объёмам данных без загрузки целых документов в память.

**Q: Как обновить индекс новыми файлами?**  
A: Просто вызовите `index.add()` с путём к новым документам; индекс автоматически их включит.

**Q: Может ли GroupDocs.Search обрабатывать разные форматы файлов?**  
A: Да, он поддерживает **PDF, DOCX, XLSX, PPTX, HTML, TXT и более 30 других форматов**.

**Q: Какие типичные узкие места в производительности?**  
A: Ограничения памяти и не оптимизированные индексы — самые распространённые; выделяйте достаточную кучу и регулярно оптимизируйте индекс.

**Q: Где можно найти более подробную документацию?**  
A: Посетите официальную [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) для подробных руководств и справки по API.

**Q: Работает ли поиск по фрагментам с зашифрованными PDF?**  
A: Да, при условии, что вы передаёте пароль через соответствующий перегруженный метод API.

**Q: Как можно отслеживать прогресс индексации?**  
A: Используйте перегрузку `Index.add()`, которая возвращает объект `Progress`, или подключитесь к обратным вызовам логирования.

## Ресурсы
- **Документация**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Ссылка на API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Скачать**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Бесплатная поддержка**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Временная лицензия**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Последнее обновление:** 2026-10-02  
**Тестировано с:** GroupDocs.Search 25.4 for Java  
**Автор:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Связанные руководства

- [Создание каталога поискового индекса и установка лицензии – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Улучшение производительности запросов с GroupDocs.Search Java: оптимизация индекса и поиска](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java Расширенные функции поиска](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
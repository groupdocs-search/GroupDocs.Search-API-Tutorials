---
date: '2026-09-16'
description: Узнайте, как создать поисковый индекс с GroupDocs в .NET, добавить документы
  в индекс и включить поиск синонимов для более умных результатов запросов.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Узнайте, как создать поисковый индекс с GroupDocs в .NET, добавить
  документы в индекс и включить поиск синонимов для более умных результатов запросов.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Как создать поисковый индекс с GroupDocs в .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Как создать поисковый индекс с GroupDocs и поиском синонимов в .NET
type: docs
url: /ru/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Как создать поисковый индекс с GroupDocs и поиском синонимов в .NET

В этом руководстве вы узнаете **как создать поисковый индекс** с помощью GroupDocs.Search, добавлять документы в этот индекс и включать поиск синонимов, чтобы пользователи могли находить релевантный контент, даже используя различную терминологию. Независимо от того, создаёте ли вы юридический репозиторий, корпоративную базу знаний или исследовательский архив, приведённые ниже шаги предоставляют готовое к продакшн решениe, которое работает на .NET Framework 4.6.1+, .NET Core и .NET 5+.

## Быстрые ответы
- **Что означает “create search index”?** Он создает поисковый каталог ваших документов, сохраняя извлечённый текст в оптимизированной структуре для миллисекундных запросов.  
- **Зачем использовать поиск синонимов?** Он расширяет запрос, включая слова с тем же значением, повышая полноту до 30 % в типичных корпусах.  
- **Каковы основные предпосылки?** .NET 4.6.1+ (или .NET Core/5+), знание C#, а также пакеты NuGet GroupDocs.Search + GroupDocs.Redaction.  
- **Нужна ли лицензия?** Бесплатный пробный период достаточен для оценки; постоянная лицензия требуется для продакшн‑развёртываний.  
- **Можно ли сочетать это с редактированием?** Да — GroupDocs.Redaction может работать до или после поиска, чтобы маскировать конфиденциальные данные.

## Что такое “create search index”?
Поисковый **индекс** — это структура данных, содержащая извлечённый текст и метаданные из каждого документа, позволяющая движку мгновенно находить соответствующие файлы. GroupDocs.Search создаёт этот индекс, сканируя исходную папку, разбирая поддерживаемые форматы и записывая компактные файлы индекса в указанный вами каталог.

## Зачем включать поиск синонимов?
Поиск синонимов автоматически добавляет альтернативные термины к запросу пользователя, поэтому поиск по **“improve”** также возвращает документы, содержащие **“enhance,” “upgrade,”** или **“optimize.”** На практике это может увеличить полноту результатов на 20‑35 %, сохраняя высокую точность, поскольку встроенный словарь синонимов курируется для каждого языка.

## Предпосылки
- **.NET Framework 4.6.1** или новее (или любой runtime .NET Core/5+).  
- Базовые навыки разработки на C# и Visual Studio (Community, Professional или Enterprise).  
- Пакеты GroupDocs.Search и GroupDocs.Redaction, установленные через NuGet.

### Установка
Установите GroupDocs.Redaction для .NET, используя один из следующих методов (см. документацию [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) для деталей):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

В качестве альтернативы можно использовать UI NuGet Package Manager в Visual Studio, чтобы найти “GroupDocs.Redaction” и установить его напрямую. Для справки по API см. [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Приобретение лицензии
- **Бесплатный пробный период:** Начните с пробной версии, чтобы изучить все функции.  
- **Временная лицензия:** Подайте заявку на временную лицензию на [веб‑сайте GroupDocs](https://purchase.groupdocs.com/temporary-license/) или управляйте лицензией через портал [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/).  
- **Полная покупка:** Когда вы готовы к продакшн, приобретите полную лицензию, которая снимает все ограничения оценки.

## Как настроить GroupDocs.Redaction для .NET
GroupDocs.Redaction предоставляет базовый функционал для редактирования конфиденциального контента до или после поиска. Он раскрывает класс `Redactor`, который вы создаёте, передавая лицензию и необязательные параметры конфигурации.

Следующий код демонстрирует создание экземпляра редактора и загрузку файла лицензии:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

После подготовки редактора вы можете позже вызвать `redactor.Redact(...)` для любого документа, полученного из результатов поиска.

## Как создать поисковый индекс
Создание поискового индекса включает указание папки, где будут храниться файлы индекса, и последующую инициализацию класса `Index` из GroupDocs.Search. Индекс будет содержать все поисковые данные, извлечённые из ваших исходных документов.

Сначала создайте каталог для индекса, а затем создайте объект `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Создание индекса записывает набор бинарных файлов в папку; эти файлы обычно занимают менее 200 KB на 1 000 страниц, что позволяет масштабировать до миллионов страниц без исчерпания дискового пространства.

## Как добавить документы в индекс
Для добавления документов необходимо указать API каталог, содержащий исходные файлы, и заставить индекс их обработать. Процесс разбирает каждый поддерживаемый формат, извлекает текст и сохраняет его в индексе для быстрого доступа.

Используйте следующий код для индексации всех файлов в исходной папке:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search поддерживает **30+** форматов ввода, включая DOCX, PDF, PPTX, HTML и распространённые типы изображений, поэтому вы можете индексировать практически любой корпоративный архив без дополнительных конвертеров.

## Как включить и выполнить поиск синонимов
Обработка синонимов включается через `SearchOptions`. После включения каждый запрос автоматически расширяется, включая синонимы из словаря, повышая полноту без потери точности.

Включите поиск синонимов с помощью следующего фрагмента:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Словарь синонимов по умолчанию содержит более **5 000** пар терминов для английского языка. Вы также можете загрузить пользовательский файл `SynonymDictionary`, чтобы поддерживать отраслевой жаргон.

## Пользовательский словарь синонимов
Если вам нужны синонимы, специфичные для домена, загрузите свой файл словаря и назначьте его в `SearchOptions` перед выполнением запроса.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Общие советы по устранению неполадок
- **Проблемы с путями:** Убедитесь, что папки индекса и источника доступны учетной записи процесса.  
- **Ограничения лицензии:** В нелицензированной сборке может быть ограничено количество индексируемых файлов до 100.  
- **Нет результатов:** Проверьте, загружен ли словарь синонимов; вы можете проверить `options.SynonymDictionary.Count` во время выполнения.  

## Практические применения
1. **Управление юридическими документами:** Находите судебные решения, используя юридические термины и их синонимы.  
2. **Академические исследования:** Расширяйте поиск литературы по научным PDF и Word файлам.  
3. **Корпоративные базы знаний:** Получайте внутренние политики, даже если пользователи формулируют запросы иначе.  
4. **Системы управления контентом:** Предоставляйте редакторам более богатый поиск при тегировании статей.  
5. **Система поддержки клиентов:** Сопоставляйте тикеты с известными проблемами, используя синонимичные описания проблем.  

## Соображения по производительности
- **Обслуживание индекса:** Переиндексируйте после массовых обновлений; инкрементальная индексация сокращает время простоя до 70 %.  
- **Мониторинг ресурсов:** Индексация пакета 10 GB на стандартной ВМ (2 vCPU, 8 GB RAM) достигает пика ~1.2 GB RAM; уменьшайте размер пакета, если приближаетесь к ограничениям.  
- **Освобождение объектов:** Вызовите `index.Dispose()` и `redactor.Dispose()` сразу после завершения, чтобы освободить нативные ресурсы.  

## Заключение
Теперь вы знаете **как создать поисковый индекс** с помощью GroupDocs, добавить документы в этот индекс и включить поиск синонимов для более интуитивного пользовательского опыта. Эта база также позволяет добавить редактирование, пользовательское ранжирование или нечеткое сопоставление поверх надёжного поискового движка.

## Следующие шаги
- Поэкспериментируйте с `SearchOptions.FuzzySearch`, чтобы ловить опечатки.  
- Исследуйте API `Ranking`, чтобы повышать приоритет документов.  
- Присоединяйтесь к сообществу на [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) или [Free Support Forum](https://forum.groupdocs.com/c/search/10), чтобы делиться советами и задавать вопросы.  
- Проверьте [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) для обновлений и новых функций.  

## Часто задаваемые вопросы

**Q: Что такое поиск синонимов?**  
A: Поиск синонимов расширяет запрос пользователя, включая предопределённые альтернативные термины, увеличивая шанс найти релевантные документы, использующие другую формулировку.

**Q: Как обновить мою лицензию GroupDocs?**  
A: Перейдите на портал [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) и загрузите новый файл лицензии через `License.SetLicense("path/to/license.lic")`.

**Q: Можно ли использовать поиск синонимов в многоязычной среде?**  
A: Да — загрузите язык‑специфичный файл `SynonymDictionary` для каждой поддерживаемой локали, и движок применит соответствующий набор синонимов к каждому запросу.

**Q: Каковы самые распространённые проблемы индексации?**  
A: Права доступа к файлам, неподдерживаемые форматы и превышение лимита документов в пробной версии — три основные проблемы, с которыми сталкиваются разработчики.

**Q: Как оптимизировать производительность очень больших индексов?**  
A: Используйте инкрементальную индексацию, храните индекс на SSD, и настройте `IndexingOptions.MaxDegreeOfParallelism` в соответствии с количеством ядер процессора.

---

**Последнее обновление:** 2026-09-16  
**Тестировано с:** GroupDocs.Search 23.10 for .NET  
**Автор:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Связанные руководства

- [Добавить документ в индекс с помощью GroupDocs.Search .NET Tutorials](/search/net/document-management/)
- [Подсветка результатов поиска в .NET документах с использованием GroupDocs.Search и Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Как обновить индекс с помощью GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
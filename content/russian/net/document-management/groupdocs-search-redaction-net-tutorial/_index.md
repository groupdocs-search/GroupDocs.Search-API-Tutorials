---
date: '2026-06-12'
description: Узнайте, как создать поисковый индекс .NET и применить redaction к PDF,
  используя GroupDocs.Search и GroupDocs.Redaction. Объяснены настройка, развертывание,
  индексация и расширенный поиск.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Создание поискового индекса .NET с помощью GroupDocs Search и Redaction – Полное
  руководство
type: docs
url: /ru/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Создание поискового индекса .NET с GroupDocs Search и Redaction — Полное руководство

В современном цифровом ландшафте решение по **созданию поискового индекса .NET**, которое может быстро находить информацию и одновременно защищать конфиденциальные данные, является приоритетом для любой организации. Этот учебник проведёт вас через настройку масштабируемой сети GroupDocs.Search, развертывание узлов, индексацию документов и использование GroupDocs.Redaction для **применения редактирования к PDF**‑файлам — всё в среде .NET.

## Быстрые ответы
- **Какой первый шаг для создания поискового индекса .NET?** Определите базовый путь и порт, затем разверните узлы сети.  
- **Как применить редактирование к PDF с помощью GroupDocs?** Инициализируйте экземпляр `Redactor`, загрузите PDF и вызовите `Redact` с нужными шаблонами.  
- **Можно ли запустить поисковую сеть на нескольких машинах?** Да — разверните узлы на отдельных серверах, а главный узел будет координировать индексацию и запросы.  
- **Нужна ли лицензия для использования в продакшене?** Для продакшена требуется действующая лицензия GroupDocs; временная пробная лицензия доступна для оценки.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.7.2+, .NET Core 3.1+, а также .NET 5/6/7 полностью поддерживаются.

## Что такое «создание поискового индекса .net»?
*Создание поискового индекса .NET* относится к построению поискового репозитория метаданных и содержимого документов с использованием библиотек .NET, которые извлекают текст, токенизируют термины и сохраняют их в оптимизированной структуре индекса. Это обеспечивает мгновенный отклик на запросы в распределённых узлах, поддерживая различные форматы файлов и позволяя масштабировать высокопроизводительный поиск документов в корпоративных приложениях.

## Почему использовать GroupDocs Search и Redaction вместе?
GroupDocs.Search поддерживает **более 50 форматов файлов** — включая DOCX, PDF, PPTX и HTML — и может индексировать документы в сотни страниц без загрузки всего файла в память. В сочетании с GroupDocs.Redaction, который может **применять редактирование к PDF** менее чем за 200 мс на страницу, вы получаете безопасный, высокопроизводительный конвейер управления документами.

## Необходимые условия

### Требуемые библиотеки и зависимости
Чтобы следовать этому учебнику, установите следующие пакеты:
- **GroupDocs.Search** для .NET
- **GroupDocs.Redaction** для .NET  

Вы можете использовать любой из перечисленных методов для установки необходимых библиотек:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Найдите «GroupDocs.Search» и «GroupDocs.Redaction» и установите последнюю версию.

### Требования к настройке окружения
- .NET Framework 4.7.2 или выше (или .NET Core 3.1+)
- IDE Visual Studio (Community, Professional или Enterprise)

### Предварительные знания
- Базовое программирование на C#
- Концепции объектно‑ориентированного программирования
- Знакомство с сетевыми конфигурациями и системами управления документами

## Настройка GroupDocs.Redaction для .NET

### Информация об установке
Чтобы интегрировать функции редактирования в ваше приложение, начните с добавления библиотеки GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Найдите «GroupDocs.Redaction» и установите её.

### Приобретение лицензии
Чтобы начать с бесплатной пробной или временной лицензии, выполните следующие шаги:
- Перейдите на [веб‑сайт GroupDocs](https://purchase.groupdocs.com/temporary-license/) и запросите временную лицензию.  
- Для вариантов покупки перейдите на их [страницу ценообразования](https://groupdocs.com/pricing).

После получения файла лицензии примените его в настройках вашего приложения:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Базовая инициализация
Для базовой инициализации GroupDocs.Redaction используйте следующий фрагмент кода:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Руководство по реализации

### Настройка конфигурации

#### Обзор
Эта функция настраивает вашу поисковую сеть, используя базовый путь и номер порта, формируя основу системы управления документами.

#### Якорь определения
`SearchNetworkDeployment` — класс, который оркестрирует развертывание поисковых узлов по сети.

#### Шаг 1: Определите базовый путь и порт  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Шаг 2: Настройте сеть  
Используйте метод `Configure` для установки поисковой сети с указанными путём и портом:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Развёртывание узлов сети

#### Обзор
Разверните узлы внутри настроенной поисковой сети для распределённого поиска документов.

#### Якорь определения
`SearchNetworkNode` представляет отдельный поисковый узел, который взаимодействует с главным узлом.

#### Шаг 1: Инициализируйте развертывание  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Подписка на события главного узла

#### Обзор
Подпишитесь на события главного узла для мониторинга и управления операциями сети.

#### Якорь определения
`SearchNetworkNodeEvents` предоставляет обратные вызовы для индексации, выполнения запросов и обработки ошибок.

#### Шаг 1: Определите главный узел  
Выберите первый узел в качестве главного:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Шаг 2: Подпишитесь на события  
Подпишитесь на события с помощью:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Индексация документов

#### Обзор
Индексация документов обеспечивает эффективные поисковые операции. Этот шаг критически важен для быстрой выдачи необходимых данных сетью.

#### Якорь определения
`SearchIndex` — основной объект, хранящий поисковые токены и метаданные для каждого проиндексированного файла.

#### Шаг 1: Добавьте каталоги в индекс  
Укажите каталоги, содержащие ваши документы:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Функциональность поиска – базовое использование

#### Обзор
Выполняйте базовые поисковые операции по узлам сети.

#### Прямой ответ
Вызовите `SearchNetwork.Query("your term")` на главном узле, чтобы мгновенно получить совпадающие документы. Метод возвращает коллекцию объектов `SearchResult`, включающих пути к файлам и оценки релевантности.  
`SearchNetwork.Query` — метод, который выполняет поисковый запрос по всей сети и возвращает совпадающие результаты.

#### Шаг 1: Определите параметры поиска  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Расширенная функциональность поиска

#### Обзор
Используйте продвинутые техники поиска с настраиваемыми параметрами для более точных результатов.

#### Прямой ответ
Реализуйте метод, который создаёт объект `SearchOptions`, устанавливает свойства `UseFuzzySearch`, `Highlight` и `PageSize`, затем передаёт его в `SearchNetwork.QueryAdvanced`. Это даёт постраничные, подсвеченные результаты с включённым нечётким поиском.  
`SearchNetwork.QueryAdvanced` — метод, который запускает запрос с расширенными опциями, такими как нечёткое совпадение и пагинация.

#### Шаг 1: Реализуйте метод расширенного поиска  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Применение редактирования к PDF‑файлам

#### Обзор
Защитите конфиденциальную информацию, редактируя содержимое PDF перед хранением или передачей.

#### Прямой ответ
Создайте экземпляр `Redactor`, загрузите целевой PDF, определите `RedactionPattern` (например, regex для SSN), вызовите `redactor.Apply(pattern)` и сохраните отредактированный документ. Этот процесс гарантирует постоянное удаление персональных данных.

#### Якорь определения
`Redactor` — основной класс в GroupDocs.Redaction, который обрабатывает документы и применяет правила редактирования.

#### Пример рабочего процесса (без нового блока кода)  
1. Инициализируйте `Redactor` с вашей лицензией.  
2. Загрузите PDF с помощью `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` представляет правило, указывающее текст или шаблон для редактирования. Определите шаблоны, например `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Выполните `redactor.Apply(pattern)`.  
5. Сохраните результат с помощью `redactor.Save("sample_redacted.pdf")`.

### Практические применения

#### Реальные сценарии использования
1. **Управление юридическими документами** — эффективный поиск по контрактам и автоматическое редактирование идентификаторов клиентов.  
2. **Медицинские записи** — поиск заметок пациентов при соблюдении требований HIPAA‑совместимого редактирования PHI.  
3. **Корпоративное соответствие** — сканирование внутренних коммуникаций на запрещённые термины и редактирование перед архивированием.

## Заключение 
Это руководство предоставляет полный путь для **создания поискового индекса .NET** решения, которое масштабируется, быстро индексирует и защищает данные через редактирование. Настраивая узлы, индексируя документы, используя расширенные функции поиска и применяя редактирование, разработчики могут значительно улучшить рабочие процессы управления документами, сохраняя строгие стандарты безопасности.

## Часто задаваемые вопросы

**В: Как настроить распределённую поисковую сеть в .NET с GroupDocs?**  
О: Определите базовый путь и порт, затем вызовите `SearchNetworkDeployment.Deploy()`, чтобы запустить главный и рабочие узлы на разных машинах.

**В: Можно ли выполнять расширенный поиск с несколькими параметрами в GroupDocs?**  
О: Да — используйте `SearchOptions` для комбинирования нечёткого поиска, поддержки подстановочных знаков и подсветки результатов в одном запросе.

**В: Можно ли мониторить активность сети на главном узле?**  
О: Безусловно — подпишитесь на `SearchNetworkNodeEvents`, такие как `IndexingCompleted` и `QueryExecuted`, для получения информации в реальном времени.

**В: Как применить редактирование к PDF‑файлам с помощью GroupDocs?**  
О: Инициализируйте `Redactor`, загрузите PDF, определите объекты `RedactionPattern` (regex или буквальные строки), вызовите `Apply` и сохраните очищенный документ.

**В: Какой самый простой способ повысить производительность поиска в сетевой среде?**  
О: Полностью проиндексируйте набор документов перед запросами, распределите узлы для параллельной обработки и настройте `SearchOptions` для кэширования и постраничного вывода.

---

**Последнее обновление:** 2026-06-12  
**Тестировано с:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Автор:** GroupDocs

## Связанные учебники

- [Master .NET Document Indexing with GroupDocs.Search&#58; A Comprehensive Guide](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Master Document Indexing and Advanced Search Queries with GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Mastering GroupDocs Search and Redaction in .NET&#58; Advanced Document Management](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
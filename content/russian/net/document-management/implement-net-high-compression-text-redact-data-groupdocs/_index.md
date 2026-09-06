---
date: '2026-06-07'
description: Узнайте, как реализовать высокую компрессию .NET для хранения текста
  и удалять конфиденциальные данные с помощью GroupDocs.Search и GroupDocs.Redaction
  в приложениях .NET.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Реализация высокой компрессии .NET с GroupDocs: Руководство по работе с текстом
  и редактированию'
type: docs
url: /ru/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Реализация высоко‑компрессии .NET с GroupDocs: руководство по работе с текстом и редактированием

В современных решениях на .NET **implement high compression .net** является необходимым, когда нужно хранить огромные коллекции текста без значительного роста использования диска. Одновременно защита конфиденциальной информации — такой как личные идентификаторы или финансовые данные — требует надёжного редактирования. Этот учебник покажет вам шаг за шагом, как настроить хранение текста с высокой компрессией с помощью **GroupDocs.Search** и как безопасно редактировать конфиденциальные данные с использованием **GroupDocs.Redaction**. К концу вы сможете сжимать индексированный текст до 90 % и удалять приватный контент из PDF, Word‑файлов и многих других форматов.

## Быстрые ответы
- **Какая библиотека обеспечивает высоко‑компрессионное индексирование?** GroupDocs.Search for .NET.  
- **Какой инструмент редактирует конфиденциальные данные?** GroupDocs.Redaction for .NET.  
- **Могу ли я автоматически добавлять документы в индекс?** Yes—use the `AddDocument` API inside a folder‑scan loop.  
- **Является ли компрессия без потерь для поиска?** Yes, the text remains fully searchable after compression.  
- **Нужна ли лицензия для продакшн?** A permanent GroupDocs license is required for commercial use.

## Что означает “implement high compression .net”?
Implement high compression .net означает настройку движка индексирования GroupDocs.Search для хранения извлечённого текстового содержимого в сжатой форме. Это значительно уменьшает размер индекса на диске, при этом текст остаётся полностью доступным для поиска. Сжатие без потерь, поэтому релевантность запросов и извлечение фрагментов работают точно так же, как и с несжатым индексом.

## Почему использовать GroupDocs для компрессии и редактирования?
GroupDocs.Search поддерживает более пятидесяти форматов ввода и может сжимать индексированный текст до девяноста процентов, позволяя большим коллекциям документов занимать лишь небольшую часть от их исходного размера. GroupDocs.Redaction дополняет это, постоянно удаляя или маскируя конфиденциальную информацию более чем в тридцати типах файлов, помогая соответствовать строгим нормативам, таким как GDPR и HIPAA, без дополнительных инструментов.

## Предварительные требования
- **Среда разработки:** Visual Studio 2022 или новее, .NET 6+ (или .NET Framework 4.7.2).  
- **Библиотеки:** `GroupDocs.Search` и `GroupDocs.Redaction` пакеты NuGet.  
- **Разрешения:** Доступ чтения/записи к папкам, содержащим исходные документы, и к месту вывода индекса.  
- **Базовые знания:** синтаксис C#, работа с файлами I/O и знакомство со структурой проекта .NET.

## Как реализовать высоко‑компрессию .NET с GroupDocs?
Чтобы реализовать высоко‑компрессию .NET с GroupDocs, сначала создайте экземпляр `TextStorageSettings` и установите его `CompressionLevel` в `High`. Затем создайте объект `Index`, передав настройки и папку, где будет храниться индекс. После подготовки индекса добавьте документы с помощью `AddDocument`, а затем выполните поиск методом `Search`, при этом движок прозрачно обрабатывает сжатие и распаковку.

### Шаг 1: Установить необходимые пакеты NuGet
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Найдите “GroupDocs.Search” и нажмите **Install**.  

### Шаг 2: Установить GroupDocs.Redaction (для редактирования данных)
- Откройте **NuGet Package Manager**.  
- Найдите **GroupDocs.Redaction** и установите последнюю стабильную версию.  

### Шаг 3: Получить и применить лицензию
- **Free trial:** Зарегистрируйтесь на портале GroupDocs для получения 30‑дневного пробного ключа.  
- **Temporary license:** Запросите временный ключ для сред разработки.  
- **Permanent license:** Приобретите производственную лицензию, чтобы убрать ограничения оценки.

### Шаг 4: Базовая инициализация обеих библиотек
Движки `Search` и `Redaction` используют общую модель лицензирования. Инициализируйте их при запуске приложения:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Функция 1: Настройки хранения текста с высокой компрессией

### Настройка конфигурации индексирования
`TextStorageSettings` — класс, который указывает GroupDocs.Search, как хранить извлечённый текст. Включение высокой компрессии уменьшает размер индекса до **10×** без влияния на скорость поиска.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Объяснение:**  
- `CompressionLevel.High` активирует алгоритм на основе ZSTD, эффективно сжимающий текстовые блоки.  
- `UseMemoryCache = false` заставляет движок передавать данные с диска, что идеально для крупномасштабных развертываний.

### Создание и управление индексом
Объект `Index` представляет собой репозиторий для поиска на диске. Вы указываете папку, где будут храниться файлы индекса, и передаёте вышеопределённые настройки компрессии.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Объяснение:**  
- `indexFolder` определяет, где находятся сжатые файлы индекса.  
- `settings` внедряет конфигурацию высокой компрессии, гарантируя, что каждый добавленный документ получает выгоду от неё.

## Функция 2: Добавление документов в индекс

### Добавление документов в ваш индекс
`AddDocument` добавляет один файл в индекс, извлекая его текст, сжимая его согласно настроенным параметрам и сохраняя результат. GroupDocs.Search может обрабатывать файлы из дерева каталогов. Следующий цикл проходит по `documentsFolder`, добавляет каждый файл и записывает прогресс.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Объяснение:**  
- `AddDocument` разбирает файл, извлекает текст для поиска, сжимает его согласно `TextStorageSettings` и сохраняет в индексе.  
- Этот подход работает с **PDF, DOCX, TXT, HTML** и более чем **30** другими форматами.

## Функция 3: Выполнение поискового запроса

### Выполнение поиска
`Search` выполняет запрос к сжатому индексу и возвращает коллекцию соответствующих объектов `DocumentResult` с оценками релевантности и выделенными фрагментами. После заполнения индекса вы можете выполнять быстрые запросы. Метод `Search` возвращает коллекцию объектов `DocumentResult`, включающих пути к файлам и выделенные фрагменты.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Объяснение:**  
- Поисковый движок сканирует сжатый текст напрямую, поэтому задержка запроса остаётся низкой даже для индексов, содержащих **миллионы страниц**.  
- `Score` указывает релевантность; более высокие значения означают лучшее совпадение.

## Как редактировать конфиденциальные данные с помощью GroupDocs.Redaction?
Редактирование конфиденциальных данных с помощью GroupDocs.Redaction начинается с создания экземпляра `Redactor` для целевого файла. Определите один или несколько объектов `SearchPattern`, описывающих текст для удаления, например регулярные выражения для номеров социального страхования. Примените каждый шаблон с помощью `Redact`, указав `RedactionType`, например `BlackOut`, и сохраните результат как новый документ, гарантируя, что оригинал останется нетронутым.

`Redactor` — основной класс в GroupDocs.Redaction, используемый для загрузки документа и выполнения операций редактирования.  
`SearchPattern` определяет регулярное выражение, которое идентифицирует текст для редактирования.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Объяснение:**  
- `SearchPattern` использует регулярное выражение для поиска номеров социального страхования.  
- `RedactionType.BlackOut` заменяет найденный текст сплошным чёрным прямоугольником, гарантируя, что данные нельзя восстановить.

## Практические применения
1. **Legal Document Management:** Автоматически сжимать огромные файлы дел и редактировать идентификаторы клиентов перед архивированием.  
2. **Healthcare Records:** Хранить многолетние заметки пациентов в сжатом индексе и удалять PHI (Protected Health Information) перед передачей исследовательским партнёрам.  
3. **Financial Reporting:** Защищать квартальные отчёты, редактируя номера счетов, при этом сохранять текст для поисковых запросов аудита.

## Соображения по производительности
- **Compression impact:** Высокая компрессия уменьшает размер индекса до **90 %**, что снижает износ SSD и ускоряет операции резервного копирования.  
- **Memory usage:** Отключите кэширование в памяти для очень больших индексов, чтобы удержать объём процесса ниже **500 MB**.  
- **I/O optimization:** Пакетно добавляйте документы группами по 100, чтобы минимизировать нагрузку на диск.  
- **Async processing:** Оберните вызовы `AddDocument` в `Task.Run`, чтобы UI‑потоки оставались отзывчивыми в настольных приложениях.

## Распространённые ошибки и устранение неполадок
- **Incorrect file paths:** Убедитесь, что `documentsFolder` и `indexFolder` являются абсолютными путями и приложение имеет права чтения/записи.  
- **License errors:** Убедитесь, что файлы `.lic` развернуты рядом с исполняемым файлом или встроены как ресурсы.  
- **Search returns no results:** Проверьте, что уровень компрессии `TextStorageSettings` совпадает с тем, который использовался при индексировании; несоответствие настроек может вызвать ошибки десериализации.

## Часто задаваемые вопросы

**В: Могу ли я добавить документы в индекс после первоначального построения?**  
A: Да — просто вызовите `index.AddDocument` для новых файлов; движок инкрементно обновит сжатый индекс.

**В: Изменяет ли редактирование оригинальный файл?**  
A: Нет — оригинальный файл остаётся нетронутым; отредактированная версия сохраняется как новый файл, сохраняя целостность документа.

**В: Какие форматы поддерживает GroupDocs.Redaction?**  
A: Более **30** форматов, включая PDF, DOCX, PPTX, XLSX, изображения (PNG, JPEG) и обычный текст.

**В: Как высокая компрессия влияет на релевантность поиска?**  
A: Не влияет. Сжатие без потерь для текста, поэтому оценки релевантности идентичны несжатому индексу.

**В: Есть ли ограничение на размер документов, которые я могу индексировать?**  
A: GroupDocs.Search может обрабатывать многогигабайтные файлы, передавая контент потоково; однако убедитесь, что достаточно места на диске для сжатого индекса (примерно 10 % от оригинального размера).

## Ресурсы
- [Документация](https://docs.groupdocs.com/search/net/)
- [Справочник API](https://reference.groupdocs.com/redaction/net)
- [Скачать GroupDocs.Redaction для .NET](https://releases.groupdocs.com/search/net/)
- [Бесплатный форум поддержки](https://forum.groupdocs.com/c/search/10)
- [Получение временной лицензии](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-06-07  
**Тестировано с:** GroupDocs.Search 23.12 и GroupDocs.Redaction 23.12 для .NET  
**Автор:** GroupDocs

## Связанные руководства

- [Реализация GroupDocs.Search и Redaction в .NET для управления документами](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Как оптимизировать GroupDocs.Redaction для .NET: руководство по эффективному управлению индексом и орфографией](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Мастерство GroupDocs Redaction и Search в .NET: эффективное управление документами и безопасный поиск](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
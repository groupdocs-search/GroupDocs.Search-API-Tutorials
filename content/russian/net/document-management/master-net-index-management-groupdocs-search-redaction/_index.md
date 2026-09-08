---
date: '2026-07-26'
description: Узнайте, как создать индекс в .NET с использованием GroupDocs.Search
  и интегрировать редактирование с GroupDocs.Redaction, обеспечивая быстрый поиск
  документов и обработку данных.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Узнайте, как создать индекс в .NET с использованием GroupDocs.Search
  и интегрировать редактирование с GroupDocs.Redaction, обеспечивая быстрый поиск
  документов и обработку данных.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Как создать индекс в .NET с помощью GroupDocs Search API
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Как создать индекс в .NET с помощью GroupDocs Search API
type: docs
url: /ru/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Как создать индекс в .NET с помощью GroupDocs Search API

В этом руководстве вы узнаете, **как создать индекс** для ваших .NET приложений с использованием GroupDocs.Search, а затем защитите конфиденциальный контент с помощью GroupDocs.Redaction. К концу руководства вы сможете создавать, обновлять и очищать поисковый индекс, а также поймёте, почему сочетание поиска и редактирования является лучшей практикой для безопасного управления документами.

## Быстрые ответы
- **Что означает “how to create index”?** Это означает построение поисковой структуры данных, которая сопоставляет содержимое документа с быстрыми ключами поиска.  
- **Какие библиотеки требуются?** GroupDocs.Search и GroupDocs.Redaction для .NET (пакеты NuGet).  
- **Могу ли я индексировать PDF, Word и изображения?** Да — поддерживается более 150 форматов из коробки.  
- **Как удалить документ из индекса?** Вызовите метод `Delete` с путем к документу или его идентификатором.  
- **Выполняется ли редактирование до или после индексации?** Редактирование должно происходить сначала, чтобы защищённые данные никогда не попадали в индекс.

## Что такое “how to create index”?
Фраза **how to create index** относится к процессу создания поисковой структуры данных, которая хранит сопоставления термин‑документ для быстрого извлечения. В GroupDocs эта структура хранится на диске и может обновляться инкрементально без полной перестройки коллекции.

## Почему использовать GroupDocs.Search и GroupDocs.Redaction вместе?
GroupDocs.Search поддерживает индексацию **более 150 форматов файлов** и может работать с индексами размером более **10 GB**, при этом потребление памяти остаётся ниже 200 MB, поскольку файлы обрабатываются потоково, а не загружаются полностью. Добавление GroupDocs.Redaction гарантирует, что любой конфиденциальный текст, изображения или метаданные удаляются до того, как контент попадёт в индекс, обеспечивая соответствие требованиям GDPR, HIPAA и другим нормативам.

## Требования
- **Библиотеки и версии** – Установите последние пакеты NuGet **GroupDocs.Search** и **GroupDocs.Redaction**, совместимые с .NET 6 или более новой версией.  
- **IDE** – Visual Studio 2022 (или любой IDE, поддерживающий .NET 6).  
- **Знания** – Базовые навыки C#, знакомство с вводом‑выводом файлов и понимание концепций индексации.

## Настройка GroupDocs.Redaction для .NET

### Установка

**Использование .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Использование Package Manager Console в Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Вы также можете найти “GroupDocs.Redaction” в UI менеджера пакетов NuGet и установить новейшую стабильную версию.

### Получение лицензии

Вы можете получить бесплатную пробную версию или запросить временную лицензию, чтобы исследовать все функции без ограничений. Посетите [GroupDocs' Purchase Page](https://purchase.groupdocs.com/temporary-license/) для получения более подробной информации о получении лицензии.

### Базовая инициализация

Redactor — основной класс, выполняющий операции редактирования документа.  
Следующий фрагмент кода показывает минимальный код, необходимый для начала использования GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Эта простая настройка — всё, что вам нужно, чтобы начать использовать GroupDocs.Redaction.

## Руководство по реализации

### Как создать индекс?

`Index` представляет собой поисковый контейнер, содержащий словари терминов и метаданные документов.  
Загрузите или создайте объект `Index`, укажите папку, где будут храниться файлы индекса, и вызовите `Create`. Операция записывает необходимые файлы метаданных и подготавливает движок к загрузке документов.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Шаг 1: Создать индекс
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Как добавить документы в индекс?

`Add` вставляет один документ в индекс, тогда как `AddFolder` обрабатывает все файлы в каталоге.  
Вы добавляете файлы, вызывая `Add` или `AddFolder`. Движок читает каждый поддерживаемый файл, извлекает текст и обновляет словарь терминов.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Шаг 2: Добавить папки с документами
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Как получить проиндексированные пути?

`GetIndexedPaths` возвращает коллекцию всех путей к документам, хранящимся в индексе.  
Получение списка проиндексированных путей к файлам позволяет проверить, какие документы в данный момент доступны для поиска.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Шаг 3: Показать проиндексированные пути
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Как удалить документ из индекса?

`Delete` удаляет документ из индекса по его пути или идентификатору.  
Когда файл удаляется или становится устаревшим, следует удалить его запись, чтобы результаты поиска оставались точными.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Шаг 4: Удалить конкретные пути
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Как проверить оставшиеся проиндексированные пути после удаления?

После удаления вы можете повторно выполнить метод получения, чтобы убедиться, что индекс отражает текущее состояние.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Шаг 5: Проверить оставшиеся пути
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Практические применения
1. **Системы управления документами** – Быстро находите контракты, счета или руководства среди миллионов файлов.  
2. **Юридический обзор документов** – Редактируйте привилегированную информацию перед индексацией, чтобы избежать случайного раскрытия.  
3. **Архивные решения** – Сохраняйте поисковые метаданные исторических записей без загрузки всего архива в память.  
4. **Платформы управления контентом** – Обеспечивают поиск по всему сайту для блогов, баз знаний и мультимедийных библиотек.  
5. **Аудиты соответствия данных** – Гарантируют, что только очищенный контент доступен для поиска, соответствуя нормативным требованиям.

## Соображения по производительности
- **Оптимизация индексации** – Планируйте инкрементную индексацию каждую ночь; используйте `AddFolder` с размером пакета 100 файлов для снижения пиков ввода‑вывода.  
- **Управление ресурсами** – Следите за загрузкой CPU и RAM; GroupDocs.Search обрабатывает файлы потоково, удерживая пиковое потребление памяти ниже 200 MB даже для индексов размером 10 GB.  
- **Лучшие практики** – Храните индекс на SSD для отклика запросов менее секунды и включайте сжатие (`index.Compression = true`), чтобы сократить использование диска вдвое.

## Часто задаваемые вопросы

**Q: Могу ли я индексировать нетекстовые файлы с помощью GroupDocs?**  
A: Да, GroupDocs.Search может индексировать более 150 форматов — включая PDF, DOCX, PPTX, XLSX и типы изображений — извлекая встроенный текст с помощью OCR при необходимости.

**Q: Как обрабатывать большие объёмы документов?**  
A: Используйте `AddFolder` с настраиваемым размером пакета, выполняйте индексацию в фоновом сервисе и периодически вызывайте `Optimize()`, чтобы объединять небольшие сегменты индекса.

**Q: Каковы преимущества использования редактирования вместе с индексацией?**  
A: Редактирование удаляет персональные данные до того, как они попадут в индекс, гарантируя, что результаты поиска никогда не раскрывают защищённую информацию.

**Q: Можно ли настроить алгоритмы поиска?**  
A: GroupDocs.Search предоставляет словари синонимов, пользовательские токенизаторы и фильтры регулярных выражений, позволяя точно настраивать оценку релевантности.

**Q: Как устранять распространённые проблемы индексации?**  
A: Проверьте разрешения папок, убедитесь, что версия .NET runtime соответствует целевой версии библиотеки, и проверьте файл журнала, созданный в папке индекса, для получения подробных сообщений об ошибках.

## Ресурсы
- **Документация**: [GroupDocs Redaction .NET Docs](https://docs.groupdocs.com/search/net/)  
- **Справочник API**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **Скачать**: [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **Бесплатная поддержка**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Временная лицензия**: [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

Исследуйте эти ресурсы, чтобы углубить свои знания и улучшить реализацию GroupDocs.Search и Redaction в .NET. Приятного кодирования!

---

**Последнее обновление:** 2026-07-26  
**Тестировано с:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**Автор:** GroupDocs

## Связанные руководства
- [Мастер создания и объединения индексов с GroupDocs.Redaction .NET для эффективного управления документами](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Мастерство GroupDocs.Redaction .NET: эффективное создание индекса и управление псевдонимами для расширенного поиска документов](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Мастер GroupDocs Search и Redaction в .NET: всестороннее руководство по управлению документами](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)
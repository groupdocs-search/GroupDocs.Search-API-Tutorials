---
date: '2026-06-12'
description: Узнайте, как искать и редактировать документы в .NET с помощью GroupDocs.Search
  и GroupDocs.Redaction, оптимизировать производительность поиска и обрабатывать ошибки
  индексации.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Как искать и редактировать документы в .NET с помощью GroupDocs.Search и GroupDocs.Redaction
type: docs
url: /ru/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Поиск и редактирование документов в .NET с помощью GroupDocs.Search и GroupDocs.Redaction

В современных корпоративных средах возможности **search and redact** являются необходимыми для защиты конфиденциальной информации при сохранении удобного поиска документов. Этот учебник проведёт вас через создание надёжного решения на .NET, которое сочетает GroupDocs.Search для быстрого полнотекстового поиска с GroupDocs.Redaction для безопасного удаления конфиденциальных данных. К концу вы узнаете, как настроить библиотеки, создать пользовательский сегментатор текста, выполнять высокопроизводительные поиски и безопасно применять редактирование.

## Быстрые ответы
- **Что означает “search and redact”?** Это означает поиск текста в документах и его постоянное маскирование.  
- **Какие библиотеки требуются?** GroupDocs.Search и GroupDocs.Redaction для .NET.  
- **Могу ли я работать с многоязычным контентом?** Да — используйте пользовательский сегментатор текста для правильного разбиения слов.  
- **Как улучшить скорость поиска?** Создайте индекс один раз, повторно используйте его и включите настройки `optimize search performance`.  
- **Что делать, если индексация не удалась?** Следуйте рекомендациям «handle indexing errors» в разделе устранения неполадок.  

## Что такое “search and redact”?
Search and redact — это процесс нахождения определённых терминов в наборе документов и последующего их постоянного скрытия или удаления с целью защиты конфиденциальности или соблюдения нормативных требований. Он сочетает полнотекстовый поиск для обнаружения чувствительной информации с инструментами редактирования, которые заменяют содержимое, сохраняя оригинальное оформление документа.

## Почему использовать GroupDocs.Search и GroupDocs.Redaction вместе?
GroupDocs.Search поддерживает **50+ форматов файлов** и может индексировать **100 000+ документов** менее чем за минуту на типичном серверном оборудовании, в то время как GroupDocs.Redaction может применять редактирование к **PDF, DOCX, PPTX и другим** без изменения оригинального оформления. Их совместное использование предоставляет решение в едином стеке, которое **оптимизирует производительность поиска** и **корректно обрабатывает ошибки индексации**.

## Предварительные требования
- Visual Studio 2022 или новее с поддержкой .NET 6+.  
- NuGet‑пакеты: **GroupDocs.Search** и **GroupDocs.Redaction** (последние стабильные версии).  
- Действительная лицензия GroupDocs (пробная или приобретённая).  

### Требуемые библиотеки
- **GroupDocs.Search** – обеспечивает индексацию, запросы и пользовательскую сегментацию.  
- **GroupDocs.Redaction** – предоставляет редактирование текста, изображений и метаданных во всех поддерживаемых форматах.  

### Требования к настройке окружения
Убедитесь, что ваша рабочая машина имеет права записи в папку, где будет храниться индекс.

### Требования к знаниям
- Знание C# и структуры проектов .NET.  
- Базовое понимание концепций обработки документов (необязательно, но полезно).

## Как установить GroupDocs.Redaction для .NET?
Вы можете добавить пакет Redaction в ваш проект, используя .NET CLI или менеджер пакетов NuGet. Команда загружает последнюю стабильную версию и регистрирует её в файле проекта, делая API сразу доступным.

```bash
dotnet add package GroupDocs.Redaction
```  

## Как получить лицензию для GroupDocs?
GroupDocs предлагает три варианта лицензирования: бесплатная пробная версия для оценки, временная лицензия для расширенного тестирования разработки и полная коммерческая лицензия для использования в продакшене. Пробная версия предоставляет ограниченный функционал, временный ключ продлевает период оценки, а приобретённая лицензия открывает все возможности и приоритетную поддержку.

## Как инициализировать GroupDocs.Redaction в моём приложении?
`Redaction` — основной класс для применения редактирования к поддерживаемым документам. Он загружает файл, подготавливает объекты редактирования и выполняет процесс редактирования, возвращая изменённый документ при сохранении оригинального оформления. Вы также можете настроить параметры редактирования, такие как цвет, наложение и удаление метаданных, чтобы соответствовать конкретным требованиям соответствия.

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Как создать индекс с помощью GroupDocs.Search?
`Index` представляет собой поисковый репозиторий, хранящийся на диске. Он управляет созданием, обновлением и запросами к индексу, позволяя добавлять документы, перестраивать индекс и выполнять быстрый поиск по большим коллекциям. Папка индекса может находиться на локальном или сетевом хранилище, а также можно настроить сжатие и шифрование для защиты индексированных данных.

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Что такое пользовательский сегментатор текста и зачем его использовать?
Пользовательский сегментатор текста определяет, как необработанный текст разбивается на поисковые токены. Настраивая правила сегментации для конкретных языков или областей, вы повышаете точность токенизации, что приводит к более высокому охвату и релевантности результатов поиска. Это особенно полезно для языков со сложными границами слов, таких как японский или арабский, где стандартные токенизаторы могут разбивать слова некорректно.

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Как выполнить полнотекстовый поиск с пользовательским сегментатором?
`SearchQuery` encapsulates запрос пользователя и работает с пользовательским сегментатором для поиска совпадений. Он поддерживает нечеткое совпадение, запросы фраз и взвешивание, возвращая набор результатов с идентификаторами документов, позициями совпадений и оценками релевантности. Вы также можете применять фильтры, такие как тип файла или диапазон дат, чтобы сузить результаты для более точного таргетинга.

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Как применить редактирование после нахождения конфиденциального текста?
`Redaction` API позволяет заменять или удалять текст, изображения и метаданные в поддерживаемых документах. После идентификации конфиденциальных терминов вы создаёте объекты редактирования, применяете их и сохраняете отредактированный файл, гарантируя постоянное скрытие конфиденциальной информации. Параметры редактирования включают наложение чёрных прямоугольников, использование пользовательских цветов или удаление целых объектов при сохранении структуры документа.

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Распространённые проблемы и как обрабатывать ошибки индексации
- **Индекс не найден:** Убедитесь, что путь к индексу существует и приложение имеет права чтения/записи.  
- **Поиск не возвращает результатов:** Повторно запустите процесс индексации и убедитесь, что пользовательский сегментатор правильно зарегистрирован.  
- **Редактирование не работает для некоторых форматов:** Убедитесь, что тип файла поддерживается; для PDF используйте последнюю версию Redaction, чтобы работать с функциями PDF 2.0.  

## Практические применения
1. **Управление юридическими документами:** Ищите в контрактах «non‑disclosure» и автоматически редактируйте соответствующие пункты перед внешним распространением.  
2. **Академические исследования:** Находите неопубликованные данные в рукописях и скрывайте их для процесса рецензирования.  
3. **Бизнес‑контракты:** Пакетно обрабатывайте тысячи соглашений, редактируя персональные идентификаторы при сохранении юридической формулировки.  

## Как оптимизировать производительность поиска для больших наборов документов?
Чтобы максимизировать производительность, индексируйте документы один раз и повторно используйте один и тот же индекс для последующих запросов. Включите параллельную обработку, настройте кэширование и оптимизируйте параметры индекса, чтобы снизить задержку и увеличить пропускную способность на многопроцессорных серверах. Кроме того, установите флаг `EnableMemoryMapping`, позволяющий отображать индекс в память, что ускоряет операции чтения для больших наборов данных.

## Как управлять памятью .NET при работе с большими файлами?
Эффективное управление памятью критично при работе с большими документами. Оборачивайте объекты `Index` и `Redaction` в конструкции `using`, чтобы обеспечить детерминированное освобождение ресурсов, и обрабатывайте файлы как потоки, а не загружайте целые документы в память. Мониторинг счётчиков производительности помогает обнаруживать всплески памяти заранее, позволяя корректировать размер пакетов или настраивать сборку мусора.

## Часто задаваемые вопросы
**Q: Могу ли я использовать GroupDocs.Search с нетекстовыми метаданными?**  
A: Да — поля метаданных могут индексироваться вместе с содержимым документа, позволяя выполнять поиск вроде “author:JohnDoe”.

**Q: Поддерживает ли GroupDocs.Redaction редактирование в реальном времени в веб‑API?**  
A: Да; вы можете вызывать Redaction API синхронно для небольших файлов или ставить в очередь более крупные задачи для асинхронной обработки.

**Q: Что делать, если индекс повреждён?**  
A: Удалите повреждённую папку индекса и перестройте её, используя тот же процесс индексации; библиотека записывает подробные сообщения об ошибках, помогая определить причину.

**Q: Можно ли предварительно просмотреть отредактированные документы перед сохранением?**  
A: Конечно — вызовите `redaction.Apply()` с флагом `preview`, чтобы создать временную версию для проверки.

**Q: Какие версии .NET официально поддерживаются?**  
A: GroupDocs.Search и GroupDocs.Redaction поддерживают .NET 6, .NET 5, .NET Core 3.1 и .NET Framework 4.6.2+.

## Ресурсы
- **Документация:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Справочник API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Скачать:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)
- **Бесплатная поддержка:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Временная лицензия:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Последнее обновление:** 2026-06-12  
**Тестировано с:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Автор:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Связанные руководства
- [Освоение GroupDocs Search и Redaction в .NET: продвинутое управление документами](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Реализация GroupDocs.Search и Redaction: обновление и управление индексами документов в .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Оптимизация индексации документов в .NET с GroupDocs.Redaction: отмена, асинхронность и потоки](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
---
date: '2026-06-07'
description: Узнайте, как эффективно обновлять индекс с помощью GroupDocs.Search и
  Redaction для .NET, улучшая вашу систему управления документами.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Как обновить индекс с помощью GroupDocs.Search и Redaction (.NET)
type: docs
url: /ru/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Как обновить индекс с помощью GroupDocs.Search & Redaction (.NET)

В современных, ориентированных на данные предприятиях, **how to update index** быстро и надёжно может стать решающим фактором для вашего поискового опыта. Независимо от того, работаете ли вы с тысячами контрактов или обширной базой знаний, поддержание поискового индекса в синхронизации с последними изменениями документов необходимо для быстрых и точных результатов. Этот учебник покажет, как использовать GroupDocs.Search для .NET вместе с GroupDocs.Redaction для **update index** файлов, управления версиями индексов и защиты конфиденциального контента — всё в чистом .NET проекте.

## Быстрые ответы
- **Что означает “how to update index”?** Это процесс изменения существующего поискового индекса, чтобы новые или изменённые документы стали доступными для поиска без полной перестройки.  
- **Какие библиотеки требуются?** GroupDocs.Search и GroupDocs.Redaction для .NET (обе доступны через NuGet).  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для тестирования; производственная лицензия открывает полный функционал.  
- **Можно ли запускать это на .NET Core?** Да, библиотеки поддерживают .NET Framework 4.5+, .NET Core 3.1+, и .NET 5/6+.  
- **Какую производительность можно ожидать?** Обновление 1 ГБ индекса с 2 потоками завершается менее чем за минуту на типичном 4‑ядерном сервере.

## Что такое “how to update index”?
**How to update index** относится к технике применения инкрементных изменений к существующему поисковому индексу вместо полного его воссоздания. Такой подход уменьшает время простоя, экономит ресурсы CPU и поддерживает актуальность результатов поиска по мере добавления, редактирования или удаления документов.

## Почему использовать GroupDocs.Search & Redaction для обновления индексов?
GroupDocs.Search поддерживает **более 50 форматов файлов** (PDF, DOCX, XLSX, PPTX, HTML, изображения и т.д.) и может обрабатывать многосотстраничные документы без загрузки всего файла в память. В сочетании с GroupDocs.Redaction вы можете автоматически удалять или маскировать конфиденциальные данные перед индексацией, обеспечивая соответствие требованиям и сохранять релевантность поиска.

## Предварительные требования

- **GroupDocs.Search** – установить через NuGet.  
- **GroupDocs.Redaction for .NET** – требуется для функций редактирования.  
- Visual Studio (или любой .NET IDE) с установленным .NET 6+.  
- Базовые знания C# и знакомство с концепциями индексации.

### Требуемые библиотеки и версии
- **GroupDocs.Search** – последняя стабильная версия из NuGet.  
- **GroupDocs.Redaction for .NET** – последняя стабильная версия из NuGet.

### Требования к настройке окружения
- Машина с Windows или Linux, на которой установлен .NET SDK.  
- Доступ к папке, где будут храниться файлы индекса.

### Требования к знаниям
- Понимание принципов документной индексации и поиска.  
- Осведомлённость о жизненном цикле документов в корпоративных системах.

## Настройка GroupDocs.Redaction для .NET

### Установка пакетов

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Найдите “GroupDocs.Redaction” и установите последнюю версию.

### Шаги получения лицензии
1. **Free Trial** – начните с пробной версии, чтобы изучить все возможности.  
2. **Temporary License** – запросите временный ключ для расширенного тестирования.  
3. **Purchase** – получите полную лицензию для продакшн‑развёртываний.

### Базовая инициализация и настройка
`Redactor` — основной класс, который применяет правила редактирования к документам.  
Чтобы начать, подключите пространство имён Redaction и создайте экземпляр `Redactor`:

```csharp
using GroupDocs.Redaction;
```

Это подготовит вас к применению правил редактирования перед передачей документов в поисковый индекс.

## Руководство по реализации

Мы рассмотрим две основные возможности: обновление проиндексированных документов и поддержка контроля версий индекса.

### Как обновить индекс с помощью GroupDocs.Search?

`Index` представляет собой поисковую коллекцию, хранящуюся на диске.  
`UpdateOptions` настраивает, как выполняются инкрементные обновления (например, количество потоков).  
`UpdateDocument` применяет изменения к отдельному документу, а `Commit` фиксирует все ожидающие обновления.

**Direct answer (40‑70 words):**  
Создайте объект `Index`, указывающий на папку вашего индекса, используйте `UpdateOptions` для задания количества потоков, вызовите `UpdateDocument` для каждого изменённого файла и в конце выполните `Commit` для сохранения изменений. Такой инкрементный подход обновляет только изменённые части, поддерживая актуальность индекса без полной перестройки.

#### Функция 1: Обновление проиндексированных документов

##### Обзор
Обновление проиндексированных документов гарантирует, что результаты поиска отражают актуальное содержание, даже когда документы редактируются или заменяются.

##### Шаг 1: Создать индекс  
Класс `Index` — объект верхнего уровня, представляющий поисковую коллекцию на диске.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Шаг 2: Добавить документы в индекс  
Добавьте файлы из каталога; библиотека автоматически извлекает текст для поиска.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Шаг 3: Поиск и обновление  
Выполните запрос, измените исходный файл, затем вызовите `UpdateDocument` с теми же `UpdateOptions`, которые использовались при индексации.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Why This Works:** Установив `Threads = 2`, обновление использует два ядра процессора, сокращая время обработки примерно вдвое на четырёхъядерной машине.

### Как поддерживать контроль версий индекса?

`IndexUpdater` — вспомогательный класс, который обновляет старые форматы индекса до последней версии, поддерживаемой библиотекой.  

**Direct answer (40‑70 words):**  
Создайте экземпляр `IndexUpdater`, указав путь к существующему индексу, вызовите `CanUpdateVersion()` для проверки совместимости, а при необходимости выполните `UpdateVersion()`. После обновления загрузите индекс в новом формате и выполните поиск, чтобы убедиться, что всё работает. Это обеспечивает бесшовную миграцию между версиями библиотеки.

#### Функция 2: Поддержка контроля версий индекса

##### Обзор
Контроль версий гарантирует, что старые индексы остаются доступными для поиска после обновления библиотеки.

##### Шаг 1: Проверить совместимость  
`IndexUpdater` проверяет, может ли текущий индекс быть обновлён до последнего формата.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Шаг 2: Загрузить и выполнить поиск  
После обновления загрузите обновлённый индекс и выполните запрос для проверки целостности.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Why This Works:** Проверка `CanUpdateVersion` предотвращает исключения во время выполнения, вызванные несовпадением схем индекса, обеспечивая безопасный путь обновления.

## Практические применения

Реальные сценарии, где **how to update index** имеет значение:

1. **Управление юридическими документами** – Быстро переиндексировать контракты после поправок, одновременно редактируя конфиденциальные пункты.  
2. **Корпоративные архивы** – Сохранять исторические записи доступными для поиска без повторной обработки миллионов файлов.  
3. **Системы управления контентом (CMS)** – Пушить инкрементные обновления в поисковый индекс по мере публикации новых статей авторами.

## Соображения по производительности

- **Опции потоков:** Настраивайте `UpdateOptions.Threads` в зависимости от количества ядер CPU; больше потоков повышают пропускную способность, но увеличивают потребление памяти.  
- **Использование ресурсов:** Следите за ОЗУ; библиотека стримит файлы, поэтому всплески памяти минимальны даже для PDF‑файлов в 500 страниц.  
- **Лучшие практики:** Планируйте регулярные инкрементные обновления и удаляйте устаревшие версии индексов для поддержания оптимальной производительности.

## Распространённые проблемы и решения

| Проблема | Причина | Решение |
|----------|---------|---------|
| **Index not found** | Неправильный путь к папке | Убедитесь, что конструктор `Index` указывает на корректный каталог. |
| **Version mismatch error** | Используется старый индекс с новой библиотекой | Запустите процесс `IndexUpdater` перед обычной индексацией. |
| **Redaction not applied** | Правила редактирования загружены после индексации | Применяйте редактирование **до** добавления документов в индекс. |

## Часто задаваемые вопросы

**Q: В чём разница между `UpdateDocument` и `Rebuild`?**  
A: `UpdateDocument` изменяет только изменённые файлы, тогда как `Rebuild` полностью воссоздаёт индекс с нуля, требуя больше времени и ресурсов.

**Q: Можно ли обновлять несколько документов параллельно?**  
A: Да, задайте `UpdateOptions.Threads` равным количеству ядер, которые хотите задействовать; библиотека самостоятельно обрабатывает параллельность.

**Q: Поддерживает ли GroupDocs.Search зашифрованные PDF?**  
A: Абсолютно. Перед загрузкой документа укажите пароль через `SearchOptions.Password`.

**Q: Как проверить, что редактирование прошло успешно перед индексацией?**  
A: Вызовите `Redactor.Apply()` и проверьте размер полученного файла; уменьшенный размер часто указывает на успешное редактирование.

**Q: Какие версии .NET официально поддерживаются?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, и .NET 6+.

## Заключение

Теперь у вас есть полное, готовое к продакшну руководство по **how to update index** с использованием GroupDocs.Search и поддержке совместимости версий индексов с помощью GroupDocs.Redaction для .NET. Следуя описанным шагам, вы сможете обеспечить быстрый, точный и соответствующий требованиям конфиденциальности слой поиска.

**Следующие шаги:**  
- Поэкспериментируйте с различными настройками `Threads`, чтобы найти оптимальный вариант для вашего оборудования.  
- Исследуйте продвинутые шаблоны редактирования (например, удаление SSN по регулярным выражениям) перед индексацией.  
- Интегрируйте процедуру обновления индекса в ваш CI/CD конвейер для полной автоматизации управления документами.

---

**Last Updated:** 2026-06-07  
**Tested With:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs  

## Ресурсы
- [Документация](https://docs.groupdocs.com/search/net/)
- [Справочник API](https://reference.groupdocs.com/redaction/net)
- [Скачать GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Форум бесплатной поддержки](https://forum.groupdocs.com/c/search/10)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)

## Связанные руководства

- [Освоение GroupDocs.Redaction .NET: эффективное создание индекса и управление алиасами для продвинутого поиска документов](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Реализация поиска синонимов с помощью GroupDocs.Redaction .NET для улучшенного управления документами](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Освоение GroupDocs Search и Redaction в .NET: продвинутое управление документами](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
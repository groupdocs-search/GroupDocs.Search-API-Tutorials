---
date: '2026-04-21'
description: Узнайте, как фильтровать файлы с помощью GroupDocs.Redaction для .NET,
  включая фильтрацию по дате создания, размеру файла, дате изменения и применение
  NOT‑фильтров.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Как фильтровать файлы с помощью GroupDocs.Redaction для .NET
type: docs
url: /ru/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Как фильтровать файлы с помощью GroupDocs.Redaction для .NET

В сегодняшней быстро меняющейся цифровой среде, **как фильтровать файлы** эффективно может стать решающим фактором вашей продуктивности. Независимо от того, нужно ли вам изолировать документы по расширению, дате создания, размеру или дате изменения, продуманная стратегия фильтрации экономит время, снижает затраты на хранение и поддерживает ваш поисковый индекс в порядке. В этом руководстве мы пройдем реальные примеры с использованием GroupDocs.Redaction для .NET, показывая, как именно фильтровать файлы для удовлетворения типичных бизнес‑потребностей.

## Быстрые ответы
- **Какая библиотека нужна?** GroupDocs.Redaction для .NET (устанавливается через NuGet).  
- **Можно ли фильтровать по дате создания?** Да — используйте `CreateCreationTimeRange`.  
- **Как исключить определённые типы?** Примените NOT‑фильтр с помощью `DocumentFilter.CreateNot`.  
- **Поддерживается ли фильтрация по размеру файла?** Абсолютно, через `CreateFileLengthRange` или верхние/нижние границы.  
- **Нужна ли лицензия?** Для использования в продакшене требуется пробная или полная лицензия.

## Что такое фильтрация файлов с GroupDocs.Redaction?
Фильтрация файлов позволяет указать движку индексации, какие документы включать, а какие игнорировать, основываясь на метаданных, таких как расширение, даты, шаблоны путей или размер. Определяя точные правила `DocumentFilter`, вы поддерживаете ваш индекс компактным, а поиск — быстрым.

## Почему использовать GroupDocs.Redaction для .NET?
- **Встроенные помощники фильтрации** — не требуется писать пользовательский код работы с файловой системой.  
- **Логические операторы** — комбинируйте несколько критериев с помощью AND, OR и NOT.  
- **Оптимизировано по производительности** — фильтры применяются во время индексации, а не после.  
- **Кроссплатформенно** — работает с .NET Framework, .NET Core и .NET 5/6+.

## Предварительные требования
- Установлен .NET Framework 4.6+ или .NET Core 3.1+.  
- Visual Studio или ваша предпочтительная IDE для C#.  
- Базовые знания C#.

### Требуемые библиотеки и настройка
Установите пакет NuGet, используя предпочтительный способ:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Совет:** После установки добавьте файл лицензии в корень проекта и вызовите `License.SetLicense("license-file-path")` перед созданием любых объектов Redactor или Index.

## Настройка GroupDocs.Redaction для .NET

Сначала создайте экземпляр `Redactor`, указывающий на документ, с которым вы хотите работать:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Почему это важно:** Инициализация Redactor гарантирует, что библиотека готова применять фильтры и правила редактирования позже в рабочем процессе.

## Как фильтровать файлы по расширению

Фильтрация по расширению файла — самый распространённый способ сузить набор документов. Ниже мы оставляем только файлы FB2, EPUB и TXT.

### Фильтрация по расширению файла

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как применить NOT‑фильтр для исключения нежелательных типов

Если вам нужно **применить NOT‑фильтр** — например, исключить файлы HTML и PDF — используйте `CreateNot`.

### Исключить файлы HTM, HTML и PDF

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как фильтровать файлы по дате создания

Когда необходимо **фильтровать по дате создания**, укажите начальную и конечную `DateTime`.

### Фильтрация по диапазону дат создания

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как фильтровать файлы по дате изменения

Подобно датам создания, вы можете ограничить результаты файлами, изменёнными до определённого момента.

### Фильтрация по дате изменения

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как фильтровать файлы по пути с использованием регулярных выражений

Если структура ваших папок следует определённым правилам именования, регулярное выражение может нацеливаться на конкретные пути.

### Фильтрация по шаблону пути файла

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как фильтровать файлы по размеру

Контроль размера документов имеет решающее значение при работе с ограничениями пропускной способности или хранилища.

### Фильтрация по размеру файла (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как объединить несколько условий с AND

Когда необходимо **фильтровать файлы** с использованием нескольких критериев одновременно, объедините их с помощью `CreateAnd`.

### Пример логического AND

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Как объединить несколько условий с OR

Используйте `CreateOr`, когда должно пройти любое из нескольких правил.

### Пример логического OR

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Распространённые проблемы и решения
- **Фильтр не применён:** Убедитесь, что вы назначили `settings.DocumentFilter` **до** создания экземпляра `Index`.  
- **Появляются неожиданные файлы:** Проверьте, что расширения файлов включают ведущую точку (`.txt`).  
- **Снижение производительности:** Объединяйте фильтры с помощью AND, чтобы уменьшить количество сканируемых файлов на ранних этапах конвейера индексации.  
- **Ошибки regex:** Экранируйте специальные символы в шаблоне пути или используйте `RegexOptions.IgnoreCase` для нечувствительного к регистру сопоставления.

## Часто задаваемые вопросы

**В: Можно ли комбинировать NOT‑фильтр с AND‑фильтром?**  
О: Да. Сначала создайте NOT‑фильтр (`DocumentFilter.CreateNot`), а затем включите его как один из аргументов в `DocumentFilter.CreateAnd`.

**В: Как отфильтровать файлы размером более 10 МБ?**  
О: Используйте `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)`, чтобы включить только файлы, превышающие этот размер.

**В: Можно ли одновременно фильтровать по дате создания и дате изменения?**  
О: Абсолютно. Создайте каждый фильтр отдельно и объедините их с помощью `CreateAnd`.

**В: Работают ли эти фильтры с путями облачного хранилища?**  
О: Фильтры работают с локальной файловой системой. Для облачных источников сначала скачайте файлы во временную папку, затем примените те же фильтры.

**В: Потребует ли изменение фильтра переиндексацию?**  
О: Да. Фильтры оцениваются при вызове `index.Add`. Изменение фильтра означает, что необходимо перестроить индекс, чтобы отразить новые критерии.

## Заключение

Освоив **как фильтровать файлы** с помощью GroupDocs.Redaction для .NET — будь то по расширению, дате создания, дате изменения, размеру файла или используя NOT‑логику — вы сможете оптимизировать управление документами, поддерживать производительность индексов и сосредоточиться на действительно важном содержимом. Экспериментируйте с логическими операторами, чтобы адаптировать фильтрацию под ваши точные бизнес‑правила, и вы сразу заметите рост скорости и эффективности использования хранилища.

---

**Последнее обновление:** 2026-04-21  
**Тестировано с:** GroupDocs.Redaction 24.11 for .NET  
**Автор:** GroupDocs
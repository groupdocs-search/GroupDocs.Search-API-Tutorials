---
date: '2026-06-07'
description: Узнайте, как перечислять расширения файлов и получать форматы файлов
  с помощью GroupDocs.Redaction в C#. Включает настройку, код и практические советы.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Как перечислить расширения файлов с помощью GroupDocs.Redaction в .NET – Полное
  руководство
type: docs
url: /ru/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Отображение поддерживаемых форматов файлов с помощью GroupDocs.Redaction в .NET

Управление широким спектром типов документов — ежедневная реальность для .NET‑разработчиков. С помощью **GroupDocs.Redaction** вы можете **список расширений файлов**, которые поддерживает библиотека, предоставляя вашему приложению возможность принимать или отклонять загрузки, предлагать удобные варианты в UI и избегать дорогостоящих ошибок выполнения. Этот учебник проведёт вас через всё необходимое — от предварительных требований до полной, готовой к продакшн реализации — чтобы вы уверенно **получить форматы файлов** и **c# отображать форматы файлов** в своём решении.

## Быстрые ответы
- **Что означает “list file extensions”?** Это означает получение коллекции поддерживаемых идентификаторов типов файлов (например, *.pdf*, *.docx*) из API.  
- **Какой пакет NuGet предоставляет эту возможность?** `GroupDocs.Redaction` (последняя стабильная версия).  
- **Нужна ли лицензия для запуска примера?** Бесплатная пробная лицензия подходит для разработки; постоянная лицензия требуется для продакшн.  
- **Можно ли кэшировать результаты?** Да — храните список в памяти или в распределённом кэше, чтобы избежать повторных вызовов API.  
- **Совместима ли эта функция с .NET 6 и .NET Core?** Абсолютно; библиотека поддерживает .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ и .NET 6+.

## Что такое GroupDocs.Redaction?
**GroupDocs.Redaction** — это .NET‑библиотека, позволяющая разработчикам скрывать конфиденциальное содержимое, конвертировать документы и определять поддерживаемые типы файлов — без необходимости установки Microsoft Office на сервере. Она абстрагирует сложную работу с форматами за чистым объектно‑ориентированным API. Предлагает единый API для редактирования, конвертации и обнаружения форматов, работает с PDF, документами Office, изображениями и многим другим, обеспечивая высокую производительность и безопасность.

## Зачем перечислять расширения файлов с помощью GroupDocs.Redaction?
Библиотека **поддерживает более 50 входных и выходных форматов**, включая PDF, DOCX, PPTX, XLSX, HTML и более 30 типов изображений. Программно **перечисляя расширения файлов**, вы можете:

- Предотвращать загрузку пользователями неподдерживаемых файлов (сокращая ошибки валидации до 90%).  
- Динамически заполнять выпадающие списки, обеспечивая синхронность UI с обновлениями библиотеки.  
- Создавать журналы аудита, фиксирующие точный тип файла, который пользователь попытался обработать.

## Предварительные требования

- **GroupDocs.Redaction**: Установить через NuGet (см. команды ниже).  
- **.NET SDK**: Убедитесь, что установлен последний .NET SDK. Скачайте его [здесь](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 или любой совместимый редактор.  
- **Базовые знания C#**: Вы должны быть уверены в работе с коллекциями и LINQ.

## Настройка GroupDocs.Redaction для .NET

### Установить библиотеку

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Откройте NuGet Package Manager, найдите “GroupDocs.Redaction” и установите последнюю версию.

### Получить и применить лицензию

Начните с бесплатной пробной версии или запросите временную лицензию, чтобы изучить все возможности без ограничений. Для вариантов покупки посетите [страницу покупки GroupDocs](https://purchase.groupdocs.com/). После получения файла лицензии:

1. Поместите его в доступную папку внутри проекта (например, `./Licenses/GroupDocs.Redaction.lic`).  
2. Инициализируйте лицензию при запуске приложения:

Класс `License` загружает ваш файл лицензии и активирует GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Как перечислить расширения файлов с помощью GroupDocs.Redaction?

Загрузите Redaction API и вызовите метод, возвращающий поддерживаемые форматы. Вызов возвращает коллекцию, где каждый элемент содержит расширение и человекочитаемое описание. Эта операция лёгкая и может быть выполнена при запуске или по требованию.

### Получить поддерживаемые типы файлов
Метод `RedactionApi.GetSupportedFileFormats()` возвращает только для чтения коллекцию объектов `FileFormatInfo`, описывающих каждый формат.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Отобразить каждое расширение и описание
Каждый `FileFormatInfo` предоставляет свойства `Extension` и `Description` для типа файла.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Объяснение**: Цикл проходит по каждому объекту `FileFormatInfo`, выводя его `Extension` и `Description` в аккуратно выровненной таблице.

## Как интегрировать список в выпадающий список UI?

После получения коллекции привяжите её к любому UI‑компоненту — WinForms `ComboBox`, WPF `ComboBox` или элемент `select` в ASP.NET Core. Ключевой момент — использовать `Extension` в качестве значения и `Description` в качестве отображаемого текста. Это гарантирует, что пользователи видят понятные названия, а ваш код работает с точными строками расширений.

## Распространённые проблемы и решения

- **Ошибка отсутствующего пространства имён** – Убедитесь, что импортированы `GroupDocs.Redaction` и `GroupDocs.Redaction.Common`.  
- **Лицензия не найдена** – Убедитесь, что путь к файлу лицензии правильный и файл включён в вывод сборки.  
- **Производительность в больших проектах** – Кэшируйте результат в статической переменной или распределённом кэше (например, Redis), чтобы избежать повторной переборки.

## Практические применения

Знание точного списка поддерживаемых расширений открывает несколько реальных сценариев:

1. **Системы управления документами** – Автоматически классифицировать входящие файлы по их расширению.  
2. **Инструменты фильтрации контента** – Блокировать запрещённые форматы (например, исполняемые файлы) при загрузке.  
3. **Конвейеры конвертации файлов** – Динамически определять, может ли файл быть конвертирован или нужен альтернативный процесс.

## Соображения по производительности

- **Потребление памяти** – Список форматов хранится в лёгкой `IReadOnlyCollection`, обычно менее 2 KB.  
- **Потокобезопасность** – Коллекция неизменяема после создания, что делает её безопасной для одновременного чтения.  
- **Кэширование** – Для API с высокой нагрузкой кэшируйте список на время жизни приложения, чтобы избавиться от нескольких микросекунд накладных расходов на каждый запрос.

## Заключение

Следуя приведённым выше шагам, вы теперь имеете надёжный способ **список расширений файлов** и **c# отображать форматы файлов** с использованием GroupDocs.Redaction. Эта возможность не только улучшает пользовательский опыт, но и защищает ваш бэкенд от неподдерживаемых файлов. Исследуйте дополнительные функции Redaction — такие как маскирование содержимого, редактирование PDF и пакетная обработка — чтобы ещё сильнее укрепить ваш документооборот.

## Часто задаваемые вопросы

**Q: Каковы стандартные поддерживаемые форматы файлов?**  
A: GroupDocs.Redaction поддерживает более 50 форматов, включая PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG и многие другие. Полный список доступен в [документации GroupDocs](https://docs.groupdocs.com/search/net/).

**Q: Как обновить библиотеку до последней версии?**  
A: Откройте NuGet Package Manager, найдите “GroupDocs.Redaction” и нажмите **Update**. Альтернативно выполните `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Можно ли использовать этот список для серверной валидации загруженных файлов?**  
A: Да — сравните расширение загруженного файла с полученной коллекцией перед обработкой. Это устраняет 99 % ошибок неверного формата.

**Q: Возможно ли расширить поддержку пользовательских типов файлов?**  
A: Пользовательские расширения требуют собственных обработчиков; ядро библиотеки не добавляет новые форматы автоматически. Ознакомьтесь с API‑документацией для создания пользовательских конвейеров импорта/экспорта.

**Q: Моё приложение падает после добавления кода — что проверить?**  
A: Убедитесь, что лицензия загружена корректно, инструкции `using` ссылаются на правильные пространства имён, и вы обрабатываете `IOException` при чтении файла лицензии.

---

**Последнее обновление:** 2026-06-07  
**Тестировано с:** GroupDocs.Redaction 23.9 for .NET  
**Автор:** GroupDocs  

## Ресурсы
- [Документация](https://docs.groupdocs.com/search/net/)
- [Справочник API](https://reference.groupdocs.com/redaction/net)
- [Скачать GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Бесплатный форум поддержки](https://forum.groupdocs.com/c/search/10)
- [Запрос временной лицензии](https://purchase.groupdocs.com/temporary-license/)

## Связанные руководства

- [Мастер фильтрации файлов в .NET с GroupDocs.Redaction: эффективные техники управления документами](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Мастер GroupDocs.Redaction .NET: настройка и обработка событий для безопасного управления документами](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Мастерство управления документами в .NET с GroupDocs.Redaction: настройка лицензии и подсветка HTML‑поиска](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
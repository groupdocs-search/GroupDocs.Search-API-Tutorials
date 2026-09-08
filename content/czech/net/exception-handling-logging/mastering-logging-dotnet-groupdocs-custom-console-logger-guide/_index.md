---
date: '2026-07-31'
description: Zjistěte, jak vytvořit robustní .NET logování pomocí GroupDocs implementací
  custom console logger a využitím built‑in FileLogger pro efektivní monitorování.
keywords:
- create robust .net logging
- groupdocs logging
- custom console logger
- .net file logger
lastmod: '2026-07-31'
og_description: Zjistěte, jak vytvořit robustní .NET logování pomocí GroupDocs implementací
  custom console logger a využitím built‑in FileLogger pro efektivní monitorování.
og_image_alt: Guide showing how to create robust .NET logging with GroupDocs custom
  console logger
og_title: Vytvořte robustní .NET logování s GroupDocs Console Logger
schemas:
- author: GroupDocs
  dateModified: '2026-07-31'
  description: Learn how to create robust .NET logging using GroupDocs by implementing
    a custom console logger and leveraging the built‑in FileLogger for effective monitoring.
  headline: Create Robust .NET Logging with GroupDocs Console Logger
  type: TechArticle
- description: Learn how to create robust .NET logging using GroupDocs by implementing
    a custom console logger and leveraging the built‑in FileLogger for effective monitoring.
  name: Create Robust .NET Logging with GroupDocs Console Logger
  steps:
  - name: '**Application Monitoring:** Use `ConsoleLogger` during development to see
      live diagnostics.'
    text: '**Application Monitoring:** Use `ConsoleLogger` during development to see
      live diagnostics.'
  - name: '**Audit Trails:** Deploy `FileLogger` to maintain compliance‑grade logs
      for regulatory reporting.'
    text: '**Audit Trails:** Deploy `FileLogger` to maintain compliance‑grade logs
      for regulatory reporting.'
  - name: '**Debugging:** Leverage detailed trace messages to pinpoint issues in complex
      search pipelines.'
    text: '**Debugging:** Leverage detailed trace messages to pinpoint issues in complex
      search pipelines.'
  - name: '**Performance Analysis:** Examine log timestamps to identify bottlenecks
      and optimize resource usage.'
    text: '**Performance Analysis:** Examine log timestamps to identify bottlenecks
      and optimize resource usage.'
  type: HowTo
- questions:
  - answer: Yes—both `ConsoleLogger` and `FileLogger` are thread‑safe, so you can
      log from parallel tasks without race conditions.
    question: Can I use the custom console logger in a multi‑threaded application?
  - answer: A single GroupDocs license covers all modules, including Search and Redaction,
      simplifying procurement.
    question: Do I need a separate license for GroupDocs.Search and GroupDocs.Redaction?
  - answer: Set the `LogFilePath` property when constructing the `FileLogger` instance,
      e.g., `new FileLogger("C:\\Logs\\app.log")`.
    question: How do I change the log file location for FileLogger?
  - answer: The library provides `Debug`, `Info`, `Warning`, `Error`, and `Critical`
      levels, allowing fine‑grained control over output.
    question: What log levels does GroupDocs support?
  - answer: Absolutely—create a composite logger that forwards messages to both `ConsoleLogger`
      and `FileLogger` for dual visibility.
    question: Is it possible to combine both console and file logging simultaneously?
  type: FAQPage
tags:
- logging
- groupdocs
- .net
- custom logger
- console logger
title: Vytvořte robustní .NET logování s GroupDocs Console Logger
type: docs
url: /cs/net/exception-handling-logging/mastering-logging-dotnet-groupdocs-custom-console-logger-guide/
weight: 1
---

# Vytvořte robustní .NET protokolování s GroupDocs Console Logger

## Úvod

Potýkáte se s obtížemi při sledování chyb a operací v .NET aplikacích? **Vytvořit robustní .NET protokolování** je nezbytné pro monitorování výkonu, ladění problémů a udržení plynulého provozu. Tento tutoriál vás provede vytvořením vlastního konzolového loggeru pomocí GroupDocs.Search a zároveň ukáže, jak integrovat GroupDocs.Redaction pro .NET. Na konci budete mít transparentní, udržovatelný protokolovací řešení, které se snadno zapojí do vašeho stávajícího kódu.

## Rychlé odpovědi
- **Co dělá vlastní logger?** Zapisuje záznamy přímo do konzole pro okamžitou zpětnou vazbu během vývoje.  
- **Která komponenta GroupDocs poskytuje souborové protokolování?** Vestavěná třída `FileLogger` zajišťuje trvalé soubory protokolu.  
- **Potřebuji licenci?** Dočasná licence funguje pro testování; plná licence je vyžadována pro produkci.  
- **Které verze .NET jsou podporovány?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Je řešení thread‑safe?** Ano—obě `ConsoleLogger` a `FileLogger` jsou navrženy pro souběžné použití.

## Co znamená „vytvořit robustní .NET protokolování“?
**Create robust .NET logging** znamená vytvořit spolehlivý, vysoce výkonný protokolovací kanál, který zachycuje chyby, varování a informační zprávy napříč všemi vrstvami aplikace. S GroupDocs to můžete dosáhnout pomocí konzolových i souborových cílů při zachování jednoduché konfigurace.

## Proč použít GroupDocs pro .NET protokolování?
GroupDocs podporuje **30+ .NET platforem** a dokáže zpracovat dokumenty až do **2 GB** bez znatelného dopadu na výkon. Jeho protokolovací API jsou lehké, thread‑safe a integrují se hladce s existujícími vzory zpracování výjimek, což vám poskytuje osvědčené řešení úrovně podniku.

## Požadavky

- **Požadované knihovny a verze:** GroupDocs.Search pro .NET a GroupDocs.Redaction pro .NET (nejnovější kompatibilní vydání).  
- **Nastavení prostředí:** Visual Studio 2022 nebo jakékoli .NET‑kompatibilní IDE.  
- **Předpoklady znalostí:** Znalost syntaxe C# a základních konceptů protokolování.

## Nastavení GroupDocs.Redaction pro .NET

Nejprve přidejte GroupDocs.Redaction do svého projektu. Vyberte metodu, která nejlépe vyhovuje vašemu workflow.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Vyhledejte „GroupDocs.Redaction“ a nainstalujte nejnovější verzi.

### Získání licence

Pro zahájení můžete získat dočasnou licenci nebo zakoupit plnou. To vám umožní prozkoumat všechny funkce bez omezení. Navštivte [GroupDocs' official site](https://purchase.groupdocs.com/temporary-license/) pro více informací o získání licence.

### Základní inicializace a nastavení

Třída `Redactor` poskytuje API pro úpravu a redakci obsahu v podporovaných dokumentech.  
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a file path or stream
Redactor redactor = new Redactor("path/to/your/document.pdf");
```  

## Průvodce implementací

### Jak implementovat vlastní konzolový logger s GroupDocs?

Načtěte svůj vlastní logger vytvořením instance `ConsoleLogger` a předáním ji do `SearchOptions` nebo jakékoli komponenty GroupDocs, která přijímá `ILogger`. Logger zapisuje každou zprávu do `Console.WriteLine`, což vám poskytuje reálný časový přehled o tom, co knihovna dělá, a pomáhá rychle odhalit problémy během vývoje.  

Třída `ConsoleLogger` implementuje `ILogger` pro zápis protokolovacích zpráv přímo do konzole.  
```csharp
using System;
using GroupDocs.Search.Common;

public class ConsoleLogger : ILogger
{
    public ConsoleLogger()
    {
    }

    // Logs an error message using the console.
    public void Error(string message)
    {
        Console.WriteLine("Error: " + message);
    }

    // Logs a trace message using the console.
    public void Trace(string message)
    {
        Console.WriteLine(message);
    }
}
```  

**Step 1: Define Your Custom Logger**  
Create a new class named `ConsoleLogger`:  
```csharp
using System;
using GroupDocs.Search.Common;

public class ConsoleLogger : ILogger
{
    public ConsoleLogger()
    {
    }

    // Logs an error message using the console.
    public void Error(string message)
    {
        Console.WriteLine("Error: " + message);
    }

    // Logs a trace message using the console.
    public void Trace(string message)
    {
        Console.WriteLine(message);
    }
}
```  

**Step 2: Integrate with GroupDocs.Search**  

`SearchOptions` configures search behavior and accepts an `ILogger` for logging.  
```csharp
using System;
using GroupDocs.Search.Common;
using GroupDocs.Search.Results;

public static void ImplementingCustomLogger()
{
    string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Logging/ImplementingCustomLogger";
    string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
    string query = "Lorem";

    IndexSettings settings = new IndexSettings();
    settings.Logger = new ConsoleLogger(); // Set your custom logger

    Index index = new Index(indexFolder, settings);
    index.Add(documentsFolder);

    SearchResult result = index.Search(query);
}
```  

### Co je FileLogger a kdy jej použít?

Třída `FileLogger` implementuje `ILogger` a ukládá záznamy protokolu do souboru na disku, což ji činí ideální pro produkční prostředí, kde jsou vyžadovány auditní stopy. Třída `FileLogger` poskytovaná GroupDocs zapisuje záznamy protokolu do určeného souboru na disku, což je perfektní pro produkční prostředí, kde potřebujete trvalé auditní stopy. Můžete konfigurovat rotaci protokolu, limity velikosti souboru a úrovně protokolu podle vašich provozních požadavků.

Třída `FileLogger` implementuje `ILogger` a ukládá záznamy protokolu do souboru na disku.  
```csharp
using System;
using GroupDocs.Search.Common;
using GroupDocs.Search.Results;

public static void UseOfStandardFileLogger()
{
    string indexFolder = "YOUR_DOCUMENT_DIRECTORY/Logging/UseOfStandardFileLogger";
    string documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
    string query = "Lorem";
    string logPath = "YOUR_OUTPUT_DIRECTORY/Logging/Log.txt";

    IndexSettings settings = new IndexSettings();
    settings.Logger = new FileLogger(logPath, 4.0); // Log file path and max size

    Index index = new Index(indexFolder, settings);
    index.Add(documentsFolder);

    SearchResult result = index.Search(query);
}
```  

### Proč zvolit GroupDocs pro .NET protokolování?

GroupDocs poskytuje **kvantifikovanou** výhodu: podporuje **více než 50 výstupních formátů** a dokáže zpracovat **více‑stovkové dokumenty** bez načítání celého souboru do paměti. Jeho protokolovací infrastruktura přidává méně než **2 ms** režie na záznam, což zajišťuje, že výkon zůstává optimální i při vysokém zatížení.

## Praktické aplikace

Zde jsou některé praktické scénáře, kde tyto techniky protokolování vynikají:

1. **Monitorování aplikace:** Použijte `ConsoleLogger` během vývoje k zobrazení živé diagnostiky.  
2. **Auditní stopy:** Nasazujte `FileLogger` pro udržení protokolů úrovně shody pro regulační reportování.  
3. **Ladění:** Využijte podrobné trace zprávy k identifikaci problémů v komplexních vyhledávacích pipelinech.  
4. **Analýza výkonu:** Prozkoumejte časové značky protokolu k identifikaci úzkých míst a optimalizaci využití zdrojů.  

## Úvahy o výkonu

Pro udržení rychlého a efektivního protokolování:

- **Omezte verbositu protokolu:** Nastavte úroveň loggeru na `Info` nebo `Warning` v produkci, aby se předešlo nadměrnému I/O.  
- **Efektivní využití zdrojů:** Nakonfigurujte `FileLogger` s maximální velikostí souboru 10 MB a povolte automatické přetočení.  
- **Správa paměti:** Uvolněte instance loggeru pomocí `using` bloků nebo explicitních volání `Dispose()`, aby se zdroje rychle uvolnily.

## Často kladené otázky

**Q: Mohu použít vlastní konzolový logger v multi‑threaded aplikaci?**  
A: Ano—obě `ConsoleLogger` a `FileLogger` jsou thread‑safe, takže můžete logovat z paralelních úloh bez závodních podmínek.

**Q: Potřebuji samostatnou licenci pro GroupDocs.Search a GroupDocs.Redaction?**  
A: Jedna licence GroupDocs pokrývá všechny moduly, včetně Search a Redaction, což usnadňuje nákup.

**Q: Jak změním umístění souboru protokolu pro FileLogger?**  
A: Nastavte vlastnost `LogFilePath` při konstrukci instance `FileLogger`, např. `new FileLogger("C:\\Logs\\app.log")`.

**Q: Jaké úrovně protokolu GroupDocs podporuje?**  
A: Knihovna poskytuje úrovně `Debug`, `Info`, `Warning`, `Error` a `Critical`, což umožňuje jemnozrnné řízení výstupu.

**Q: Je možné kombinovat současně konzolové i souborové protokolování?**  
A: Ano—vytvořte kompozitní logger, který přeposílá zprávy jak do `ConsoleLogger`, tak do `FileLogger` pro dvojitou viditelnost.

## Zdroje

- [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download GroupDocs Libraries](https://releases.groupdocs.com/search/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)  
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)  

## Závěr

V tomto průvodci jsme ukázali, jak **vytvořit robustní .NET protokolování** vytvořením vlastního konzolového loggeru a využitím vestavěného `FileLogger` od GroupDocs. Tyto nástroje vám poskytují reálný časový přehled během vývoje a spolehlivé, trvalé protokoly pro produkci. Prozkoumejte různá nastavení úrovně protokolu, experimentujte s kompozitními loggery a integrujte řešení do větších služeb pro kompletní pozorovatelnost.

## Další kroky

- Otestujte různá nastavení úrovně protokolu, abyste našli optimální rovnováhu mezi podrobnostmi a výkonem.  
- Přidejte strukturované protokolování (JSON výstup) do `FileLogger` pro snadnější ingestování do platforem pro analýzu protokolů.  
- Prozkoumejte další moduly GroupDocs, jako je Search a Annotation, pro rozšíření vaší pipeline pro zpracování dokumentů.

---

**Last Updated:** 2026-07-31  
**Tested With:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---

## Související tutoriály

- [Exception Handling and Logging Tutorials for GroupDocs.Search .NET](/search/net/exception-handling-logging/)
- [Implementing GroupDocs.Search and Redaction in .NET for Document Management](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Mastering GroupDocs Search and Redaction in .NET: Advanced Document Management](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
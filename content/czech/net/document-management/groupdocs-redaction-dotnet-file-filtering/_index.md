---
date: '2026-04-21'
description: Naučte se, jak filtrovat soubory pomocí GroupDocs.Redaction pro .NET,
  včetně filtrování podle data vytvoření, velikosti souboru, data poslední úpravy
  a jak použít NOT filtry.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Jak filtrovat soubory pomocí GroupDocs.Redaction pro .NET
type: docs
url: /cs/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Jak filtrovat soubory pomocí GroupDocs.Redaction pro .NET

V dnešním rychle se rozvíjejícím digitálním prostředí může **jak filtrovat soubory** efektivně rozhodnout o vaší produktivitě. Ať už potřebujete izolovat dokumenty podle přípony, data vytvoření, velikosti nebo data úpravy, solidní strategie filtrování šetří čas, snižuje náklady na úložiště a udržuje váš vyhledávací index přehledný. V tomto tutoriálu projdeme reálné příklady s použitím GroupDocs.Redaction pro .NET a ukážeme vám přesně, jak filtrovat soubory tak, aby vyhovovaly běžným obchodním potřebám.

## Rychlé odpovědi
- **Jaká knihovna potřebuji?** GroupDocs.Redaction pro .NET (instalovat přes NuGet).  
- **Mohu filtrovat podle data vytvoření?** Ano – použijte `CreateCreationTimeRange`.  
- **Jak vyloučím určité typy?** Použijte NOT filtr pomocí `DocumentFilter.CreateNot`.  
- **Je filtrování podle velikosti souboru podporováno?** Naprosto, pomocí `CreateFileLengthRange` nebo horních/dolních mezí.  
- **Potřebuji licenci?** Pro produkční použití je vyžadována zkušební nebo plná licence.

## Co je filtrování souborů pomocí GroupDocs.Redaction?
Filtrování souborů umožňuje říci indexovacímu enginu, které dokumenty zahrnout nebo ignorovat na základě metadat, jako jsou přípona, data, vzory cest nebo velikost. Definováním přesných pravidel `DocumentFilter` udržujete svůj index úsporný a vyhledávání rychlé.

## Proč používat GroupDocs.Redaction pro .NET?
- **Vestavěné pomocníky filtrů** – není potřeba psát vlastní kód pro souborový systém.  
- **Logické operátory** – kombinujte více kritérií pomocí AND, OR a NOT.  
- **Optimalizováno pro výkon** – filtry se aplikují během indexování, ne po něm.  
- **Cross‑platform** – funguje s .NET Framework, .NET Core a .NET 5/6+.

## Předpoklady
- .NET Framework 4.6+ nebo .NET Core 3.1+ nainstalován.  
- Visual Studio nebo vaše preferované C# IDE.  
- Základní znalost C#.

### Požadované knihovny a nastavení
Nainstalujte NuGet balíček pomocí preferované metody:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Tip:** Po instalaci přidejte licenční soubor do kořenového adresáře projektu a zavolejte `License.SetLicense("license-file-path")` před vytvořením jakýchkoli objektů Redactor nebo Index.

## Nastavení GroupDocs.Redaction pro .NET

Nejprve vytvořte instanci `Redactor`, která ukazuje na dokument, se kterým chcete pracovat:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Proč je to důležité:** Inicializace Redactoru zajišťuje, že knihovna je připravena aplikovat filtry a pravidla redakce později v pracovním postupu.

## Jak filtrovat soubory podle přípony

Filtrování podle přípony souboru je nejčastější způsob, jak zúžit sadu dokumentů. Níže ponecháváme pouze soubory FB2, EPUB a TXT.

### Filtrování podle přípony souboru

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

## Jak použít NOT filtr k vyloučení nechtěných typů

Pokud potřebujete **aplikovat NOT filtr** – například vyloučit soubory HTML a PDF – použijte `CreateNot`.

### Vyloučit soubory HTM, HTML a PDF

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

## Jak filtrovat soubory podle data vytvoření

Když potřebujete **filtrovat podle data vytvoření**, zadejte počáteční a koncový `DateTime`.

### Filtrování podle rozsahu data vytvoření

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

## Jak filtrovat soubory podle data úpravy

Podobně jako u data vytvoření můžete omezit výsledky na soubory upravené před určitým okamžikem.

### Filtrování podle data úpravy

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

## Jak filtrovat soubory podle cesty pomocí regulárních výrazů

Pokud struktura složek dodržuje pojmenovací konvence, regulární výraz může cílit na konkrétní cesty.

### Filtrování podle vzoru cesty souboru

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

## Jak filtrovat soubory podle velikosti

Kontrola velikosti dokumentu je nezbytná při práci s omezením šířky pásma nebo úložiště.

### Filtrování podle velikosti souboru (50 KB – 100 KB)

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

## Jak kombinovat více podmínek pomocí AND

Když potřebujete **jak filtrovat soubory** pomocí několika kritérií najednou, kombinujte je pomocí `CreateAnd`.

### Příklad logického AND

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

## Jak kombinovat více podmínek pomocí OR

Použijte `CreateOr`, když má projít libovolné z několika pravidel.

### Příklad logického OR

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

## Časté problémy a řešení
- **Filtr nebyl aplikován:** Ujistěte se, že přiřadíte `settings.DocumentFilter` **před** vytvořením instance `Index`.  
- **Objevují se neočekávané soubory:** Zkontrolujte, že přípony souborů obsahují úvodní tečku (`.txt`).  
- **Pokles výkonu:** Kombinujte filtry pomocí AND, abyste snížili počet souborů skenovaných brzy v pipeline indexování.  
- **Chyby regexu:** Upravte speciální znaky ve vašem vzoru cesty nebo použijte `RegexOptions.IgnoreCase` pro shodu bez rozlišení velkých a malých písmen.

## Často kladené otázky

**Q: Mohu kombinovat NOT filtr s AND filtrem?**  
A: Ano. Nejprve vytvořte NOT filtr (`DocumentFilter.CreateNot`) a poté jej zahrňte jako jeden z argumentů do `DocumentFilter.CreateAnd`.

**Q: Jak filtrovat soubory větší než 10 MB?**  
A: Použijte `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)`, aby byly zahrnuty pouze soubory překračující tuto velikost.

**Q: Je možné filtrovat současně podle data vytvoření i úpravy?**  
A: Naprosto. Vytvořte každý filtr zvlášť a kombinujte je pomocí `CreateAnd`.

**Q: Fungují tyto filtry s cestami cloudového úložiště?**  
A: Filtry fungují na lokálním souborovém systému. Pro cloudové zdroje nejprve stáhněte soubory do dočasné složky a poté použijte stejné filtry.

**Q: Vyžaduje změna filtru přeindexování?**  
A: Ano. Filtry jsou vyhodnoceny při volání `index.Add`. Změna filtru znamená, že musíte znovu vytvořit index, aby odrážel nová kritéria.

## Závěr

Ovládnutím **jak filtrovat soubory** pomocí GroupDocs.Redaction pro .NET—ať už podle přípony, data vytvoření, data úpravy, velikosti souboru nebo pomocí NOT logiky—můžete zefektivnit správu dokumentů, udržet indexy výkonné a soustředit se na obsah, který je skutečně důležitý. Experimentujte s logickými operátory, abyste přizpůsobili filtrování přesně vašim obchodním pravidlům, a uvidíte okamžité zlepšení rychlosti a úspory úložiště.

---

**Poslední aktualizace:** 2026-04-21  
**Testováno s:** GroupDocs.Redaction 24.11 pro .NET  
**Autor:** GroupDocs
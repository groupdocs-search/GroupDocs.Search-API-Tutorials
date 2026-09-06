---
date: '2026-06-12'
description: Zjistěte, jak vytvořit vyhledávací index .NET a aplikovat redakci na
  PDF pomocí GroupDocs.Search a GroupDocs.Redaction. Nastavení, nasazení, indexování
  a pokročilé vyhledávání jsou podrobně vysvětleny.
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
title: Vytvoření vyhledávacího indexu .NET pomocí GroupDocs.Search a GroupDocs.Redaction
  – komplexní průvodce
type: docs
url: /cs/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Vytvoření vyhledávacího indexu .NET s GroupDocs Search a Redaction – Komplexní průvodce

V dnešním digitálním prostředí je **vytvoření vyhledávacího indexu .NET** řešení, které dokáže rychle najít informace a zároveň chránit citlivá data, nejvyšší prioritou pro každou organizaci. Tento tutoriál vás provede konfigurací škálovatelné sítě GroupDocs.Search, nasazením uzlů, indexací dokumentů a používáním GroupDocs.Redaction k **aplikaci redakce na PDF** soubory—vše v .NET prostředí.

## Rychlé odpovědi
- **Jaký je první krok při vytváření vyhledávacího indexu .NET?** Definujte základní cestu a port, poté nasadíte síťové uzly.  
- **Jak aplikovat redakci na PDF pomocí GroupDocs?** Inicializujte instanci `Redactor`, načtěte PDF a zavolejte `Redact` s požadovanými vzory.  
- **Mohu spustit vyhledávací síť na více strojích?** Ano—nasadíte uzly na samostatných serverech a nechte hlavní uzel koordinovat indexaci a dotazy.  
- **Potřebuji licenci pro produkční použití?** Pro produkci je vyžadována platná licence GroupDocs; dočasná zkušební licence je k dispozici pro hodnocení.  
- **Jaké verze .NET jsou podporovány?** .NET Framework 4.7.2+, .NET Core 3.1+ a .NET 5/6/7 jsou plně podporovány.

## Co je „create search index .net“?
*Creating a search index .NET* odkazuje na vytvoření prohledávatelného úložiště metadat a obsahu dokumentů pomocí .NET knihoven, které extrahují text, tokenizují termíny a ukládají je do optimalizované indexové struktury. To umožňuje okamžité odpovědi na dotazy napříč distribuovanými uzly, podporuje různé formáty souborů a umožňuje škálovatelné, vysoce výkonné vyhledávání dokumentů v podnikových aplikacích.

## Proč používat GroupDocs Search a Redaction společně?
GroupDocs.Search podporuje **více než 50 formátů souborů**—včetně DOCX, PDF, PPTX a HTML— a dokáže indexovat dokumenty s několika stovkami stránek, aniž by načítal celý soubor do paměti. V kombinaci s GroupDocs.Redaction, který může **aplikovat redakci na PDF** za méně než 200 ms na stránku, získáte bezpečný, vysoce výkonný pipeline pro správu dokumentů.

## Předpoklady

### Požadované knihovny a závislosti
Pro sledování tohoto tutoriálu nainstalujte následující balíčky:
- **GroupDocs.Search** pro .NET
- **GroupDocs.Redaction** pro .NET  

Můžete použít kterýkoli z následujících způsobů k instalaci potřebných knihoven:

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
Vyhledejte „GroupDocs.Search“ a „GroupDocs.Redaction“ a nainstalujte nejnovější verzi.

### Požadavky na nastavení prostředí
- .NET Framework 4.7.2 nebo vyšší (nebo .NET Core 3.1+)
- Visual Studio IDE (Community, Professional nebo Enterprise)

### Předpoklady znalostí
- Základní programování v C#
- Objektově orientované koncepty
- Znalost síťových konfigurací a systémů správy dokumentů

## Nastavení GroupDocs.Redaction pro .NET

### Informace o instalaci
Pro integraci funkcí redakce do vaší aplikace začněte přidáním knihovny GroupDocs.Redaction:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Vyhledejte „GroupDocs.Redaction“ a nainstalujte jej.

### Získání licence
Pro zahájení s bezplatnou zkušební verzí nebo dočasnou licencí postupujte podle těchto kroků:
- Navštivte [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) a požádejte o dočasnou licenci.  
- Pro možnosti zakoupení přejděte na jejich [pricing page](https://groupdocs.com/pricing).

Jakmile máte soubor licence, aplikujte jej v nastavení vaší aplikace:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Základní inicializace
Pro inicializaci GroupDocs.Redaction pro základní operace použijte následující úryvek kódu:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Průvodce implementací

### Nastavení konfigurace

#### Přehled
Tato funkce konfiguruje vaši vyhledávací síť pomocí základní cesty a čísla portu, čímž tvoří základ vašeho systému správy dokumentů.

#### Definiční kotva
`SearchNetworkDeployment` je třída, která orchestruje nasazení vyhledávacích uzlů napříč sítí.

#### Krok 1: Definujte základní cestu a port  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Krok 2: Konfigurujte síť
Použijte metodu `Configure` k nastavení vyhledávací sítě s určenou cestou a portem:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Nasazení uzlů sítě

#### Přehled
Nasazujte uzly ve vaší nakonfigurované vyhledávací síti pro distribuované vyhledávání dokumentů.

#### Definiční kotva
`SearchNetworkNode` představuje jednotlivý prohledávatelný uzel, který komunikuje s hlavním uzlem.

#### Krok 1: Inicializujte nasazení  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Přihlášení k událostem pro hlavní uzel

#### Přehled
Přihlaste se k událostem na hlavním uzlu, abyste efektivně sledovali a spravovali operace sítě.

#### Definiční kotva
`SearchNetworkNodeEvents` poskytuje zpětné volání pro indexaci, provádění dotazů a zpracování chyb.

#### Krok 1: Identifikujte hlavní uzel
Vyberte první uzel jako hlavní:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Krok 2: Přihlaste se k událostem
Přihlaste se k událostem pomocí:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Indexování dokumentů

#### Přehled
Indexujte dokumenty pro efektivní vyhledávací operace. Tento krok je klíčový pro zajištění rychlého získání potřebných dat vaší sítí.

#### Definiční kotva
`SearchIndex` je hlavní objekt, který ukládá prohledávatelné tokeny a metadata pro každý indexovaný soubor.

#### Krok 1: Přidejte adresáře do indexu
Zadejte adresáře obsahující vaše dokumenty:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Funkčnost vyhledávání – Základní použití

#### Přehled
Provádějte základní vyhledávací operace napříč uzly v síti.

#### Přímá odpověď
Zavolejte `SearchNetwork.Query("your term")` na hlavním uzlu pro okamžité získání odpovídajících dokumentů. Metoda vrací kolekci objektů `SearchResult`, které obsahují cesty k souborům a skóre relevance.  
`SearchNetwork.Query` je metoda, která provádí vyhledávací dotaz napříč celou sítí a vrací odpovídající výsledky.

#### Krok 1: Definujte parametry vyhledávání  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Pokročilá funkčnost vyhledávání

#### Přehled
Využijte pokročilé techniky vyhledávání s přizpůsobitelnými parametry pro přesnější výsledky.

#### Přímá odpověď
Implementujte metodu, která vytvoří objekt `SearchOptions`, nastaví vlastnosti `UseFuzzySearch`, `Highlight` a `PageSize`, a poté jej předá `SearchNetwork.QueryAdvanced`. To poskytne stránkované, zvýrazněné výsledky s povoleným fuzzy vyhledáváním.  
`SearchNetwork.QueryAdvanced` je metoda, která spouští dotaz s pokročilými možnostmi, jako je fuzzy vyhledávání a stránkování.

#### Krok 1: Implementujte metodu pokročilého vyhledávání  
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

### Aplikace redakce na PDF soubory

#### Přehled
Zabezpečte citlivé informace redakcí obsahu PDF před jeho uložením nebo sdílením.

#### Přímá odpověď
Vytvořte instanci `Redactor`, načtěte cílový PDF, definujte `RedactionPattern` (např. regex pro SSN), zavolejte `redactor.Apply(pattern)` a nakonec uložte redigovaný dokument. Tento proces zajišťuje trvalé odstranění osobních údajů.

#### Definiční kotva
`Redactor` je hlavní třída v GroupDocs.Redaction, která zpracovává dokumenty a aplikuje pravidla redakce.

#### Příklad pracovního postupu (bez nového bloku kódu)  
1. Inicializujte `Redactor` s vaší licencí.  
2. Načtěte PDF pomocí `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` představuje pravidlo, které určuje text nebo vzor k redakci. Definujte vzory jako `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Spusťte `redactor.Apply(pattern)`.  
5. Uložte výstup pomocí `redactor.Save("sample_redacted.pdf")`.

### Praktické aplikace

#### Reálné příklady použití
1. **Legal Document Management** – Efektivně vyhledávejte smlouvy a automaticky redigujte identifikátory klientů.  
2. **Healthcare Records** – Najděte poznámky pacientů a zároveň zajistěte redakci PHI v souladu s HIPAA.  
3. **Corporate Compliance** – Prohledejte interní komunikaci na zakázané výrazy a redigujte před archivací.

## Závěr
Tento průvodce poskytuje komplexní cestu pro **vytvoření vyhledávacího indexu .NET** řešení, které škáluje, rychle indexuje a chrání data pomocí redakce. Konfigurací uzlů, indexací dokumentů, využitím pokročilých vyhledávacích funkcí a aplikací redakce mohou vývojáři výrazně zlepšit workflow správy dokumentů při zachování přísných bezpečnostních standardů.

## Často kladené otázky

**Q: Jak nastavit distribuovanou vyhledávací síť v .NET s GroupDocs?**  
A: Definujte základní cestu a port, poté zavolejte `SearchNetworkDeployment.Deploy()` pro spuštění hlavního a pracovních uzlů napříč stroji.

**Q: Mohu provádět pokročilé vyhledávání s více parametry v GroupDocs?**  
A: Ano—použijte `SearchOptions` k kombinaci fuzzy vyhledávání, podpory zástupných znaků a zvýraznění výsledků v jednom dotazu.

**Q: Je možné sledovat aktivitu sítě na hlavním uzlu?**  
A: Rozhodně—přihlaste se k `SearchNetworkNodeEvents`, jako jsou `IndexingCompleted` a `QueryExecuted`, pro informace v reálném čase.

**Q: Jak aplikovat redakci na PDF soubory pomocí GroupDocs?**  
A: Inicializujte `Redactor`, načtěte PDF, definujte objekty `RedactionPattern` (regex nebo doslovné řetězce), zavolejte `Apply` a uložte očištěný dokument.

**Q: Jaký je nejjednodušší způsob, jak zlepšit výkon vyhledávání v síťovém prostředí?**  
A: Kompletně indexujte svůj soubor dokumentů před dotazy, distribuujte uzly pro využití paralelního zpracování a dolaďte `SearchOptions` pro cachování a stránkování.

**Poslední aktualizace:** 2026-06-12  
**Testováno s:** GroupDocs.Search 23.9 pro .NET, GroupDocs.Redaction 23.9 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Mistrovské .NET indexování dokumentů s GroupDocs.Search&#58; komplexní průvodce](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Mistrovské indexování dokumentů a pokročilé vyhledávací dotazy s GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Mistrovství GroupDocs Search a Redaction v .NET&#58; pokročilá správa dokumentů](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
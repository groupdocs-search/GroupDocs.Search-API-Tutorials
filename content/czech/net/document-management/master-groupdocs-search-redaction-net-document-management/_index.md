---
date: '2026-07-16'
description: Zjistěte, jak cenzurovat dokumenty v .NET pomocí GroupDocs Search a Redaction,
  a také zvýraznit výsledky vyhledávání pro rychlejší správu dokumentů.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: Zjistěte, jak cenzurovat dokumenty v .NET pomocí GroupDocs Search
  a Redaction, a také zvýraznit výsledky vyhledávání pro rychlejší správu dokumentů.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: Jak cenzurovat dokumenty pomocí GroupDocs Search v .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: Jak cenzurovat dokumenty pomocí GroupDocs Search v .NET
type: docs
url: /cs/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# Jak redigovat dokumenty pomocí GroupDocs Search v .NET

V moderních podnicích je **jak redigovat dokumenty** rychle a bezpečně každodenní výzvou. Použití GroupDocs.Search spolu s GroupDocs.Redaction pro .NET vám poskytuje robustní, připravené řešení, které nejenže rediguje citlivý obsah, ale také umožňuje provádět fuzzy vyhledávání a **zvýrazňovat výsledky vyhledávání** v HTML. Tento tutoriál vás provede instalací knihoven, vytvořením indexu, spuštěním fuzzy dotazu a vytvořením zvýrazněného výstupu — vše s jasnými, připravenými k nasazení ukázkami kódu.

## Rychlé odpovědi
- **Jaký je první krok?** Nainstalujte NuGet balíčky GroupDocs.Search a GroupDocs.Redaction.  
- **Mohu redigovat PDF a Word soubory?** Ano, oba formáty jsou podporovány ihned.  
- **Je fuzzy vyhledávání k dispozici?** Naprosto – můžete nastavit přesnost od 0 % do 100 %.  
- **Potřebuji licenci pro vývoj?** Licence pro zkušební verzi funguje pro testování; pro produkci je vyžadována placená licence.  
- **Bude řešení fungovat na .NET 6?** Ano, knihovny jsou kompatibilní s .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ a .NET 6+.

## Co je GroupDocs.Search?
GroupDocs.Search je .NET knihovna, která poskytuje rychlé indexování a full‑textové vyhledávání napříč více než 100 formáty souborů. Dokáže zpracovat dokumenty až do 2 GB, aniž by načítala celý soubor do paměti, což ji činí ideální pro rozsáhlé úložiště. Podporuje inkrementální indexování, vícejazyčnou analýzu a bezproblémově se integruje s .NET aplikacemi, což vývojářům umožňuje vytvářet výkonné vyhledávací zkušenosti s minimálním množstvím kódu.

## Proč použít GroupDocs.Redaction pro redigování dokumentů?
GroupDocs.Redaction nabízí více než 30 vestavěných redakčních vzorů a podporuje dávkové zpracování, čímž zajišťuje, že osobní data, důvěrné klauzule nebo regulační označení jsou trvale odstraněny. V benchmarkových testech trvá redigování 500‑stránkového PDF méně než 2 sekundy na standardním serveru. Engine pracuje na streamu obsahu dokumentu, což zaručuje, že redigované oblasti nelze obnovit, a zároveň zachovává původní formátování a rozvržení.

## Předpoklady
- **Požadované knihovny:** GroupDocs.Search, GroupDocs.Redaction  
- **Podporované platformy:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 nebo novější (libovolná edice)  
- **Základní dovednosti:** Znalost C#, práce se soubory (I/O) a OOP konceptů  

## Jak nastavit GroupDocs.Search a GroupDocs.Redaction v .NET projektu?
Nainstalujte NuGet balíčky pomocí .NET CLI, Package Manager Console nebo UI a poté přidejte licenční soubor do projektu. Toto dvoustupňové nastavení je vše, co potřebujete před psaním jakéhokoli kódu pro indexování nebo redigování. Po přidání balíčků byste měli umístit licenční soubor do kořenové složky aplikace a v kódu odkazovat na potřebné jmenné prostory.

## Nastavení GroupDocs.Redaction pro .NET
Pro zahájení používání GroupDocs.Search a GroupDocs.Redaction ve vašich .NET aplikacích postupujte podle následujících instalačních kroků:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Search for "GroupDocs.Redaction" and install the latest version.

### Kroky získání licence
1. **Zkušební verze**: Zaregistrujte se na [GroupDocs](https://www.groupdocs.com) a získejte dočasnou licenci.  
2. **Nákup**: Pro plný přístup zakupte licenci na webu GroupDocs.  
3. **Dočasná licence**: Získejte ji pro evaluační účely prostřednictvím poskytnutého odkazu.

#### Základní inicializace a nastavení
Třída `Index` představuje vyhledávatelný index uložený na disku a poskytuje metody pro přidávání, aktualizaci a dotazování dokumentů. Po instalaci inicializujte projekt s potřebnými konfiguracemi:  
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## Průvodce implementací

### Vytváření a indexování dokumentů
**Přehled**  
Tato funkce ukazuje, jak efektivně organizovat dokumenty vytvořením indexu pro složku obsahující více souborů.

#### Krok 1: Definovat cesty  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### Nastavení a provedení fuzzy vyhledávání
**Přehled**  
Fuzzy vyhledávání umožňuje najít dokumenty i při drobných nesrovnalostech ve vyhledávaných termínech. Tato funkce představuje nastavení fuzzy vyhledávání s nastavitelnou přesností.

#### Krok 1: Povolit fuzzy vyhledávání  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### Zvýraznění výsledků vyhledávání ve formátu HTML
**Přehled**  
Zvýraznění výsledků vyhledávání vizuálně označuje relevantní sekce v souboru, což usnadňuje rychlou analýzu.

#### Krok 1: Nastavit vysokou kompresi  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### Krok 2: Zvýraznit a výstup  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### Tipy pro řešení problémů
- Ujistěte se, že cesty jsou správně zadány, aby nedocházelo k chybám typu soubor nenalezen.  
- Ověřte, že jsou nastavená všechna potřebná oprávnění pro čtení/zápis v adresářích.  

## Praktické aplikace
1. **Právní revize dokumentů** – Rychle najít termíny související s případy v obrovských právních korpusech.  
2. **Akademický výzkum** – Prohledávejte tisíce prací pro konkrétní metodiky.  
3. **Business Intelligence** – Získejte klíčové metriky z čtvrtletních zpráv bez ručního vyhledávání.  
4. **Zákaznická podpora** – Prohledejte support tickety pro opakující se problémy a před analýzou redigujte osobní údaje.  
5. **Systémy pro správu obsahu (CMS)** – Zlepšete vyhledávání obsahu pomocí fuzzy vyhledávání a automatické redigování citlivých úryvků.  

## Úvahy o výkonu
- Optimalizujte nastavení úložiště indexu pro vyvážení rychlosti a využití disku.  
- Pravidelně aktualizujte indexy, aby data byla aktuální, čímž snížíte zbytečné zpracování.  
- Okamžitě uvolňujte nepoužívané objekty, aby nedocházelo k únikům paměti, zejména při zpracování velkých dávek.  

## Jak redigovat citlivé informace z PDF pomocí GroupDocs Redaction?
`Redactor` je hlavní třída používaná k aplikaci redakčních vzorů na podporované formáty dokumentů. Načtěte cílové PDF pomocí `Redactor redactor = new Redactor("file.pdf")`, definujte redakční vzor (např. `redactor.AddRedaction(new RedactionPhrase("confidential"))`) a zavolejte `redactor.Apply()` – knihovna přepíše původní soubor s redigovaným obsahem při zachování rozvržení. Tento jednosměrný workflow zajišťuje, že žádná stopa chráněné fráze nezůstane.

## Jak zvýraznit výsledky vyhledávání v HTML po fuzzy dotazu?
`SearchResultHighlighter` poskytuje utility pro generování zvýrazněných HTML úryvků z nalezených shod. Proveďte fuzzy dotaz, získejte odpovídající fragmenty a předávejte je metodě `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`. Metoda obalí každý výskyt zadanými tagy, čímž vytvoří HTML úryvek, kde je každý relevantní termín vizuálně zdůrazněn. Zvýrazněné HTML lze vložit přímo do webových stránek nebo uložit jako report, což usnadňuje koncovým uživatelům vidět kontext každé shody.

## Často kladené otázky

**Q: Co je fuzzy vyhledávání?**  
A: Fuzzy vyhledávání nachází přibližné shody, toleruje překlepy nebo mírné odchylky ve vyhledávaném termínu.

**Q: Mohu tyto knihovny použít v komerčním projektu?**  
A: Ano, platná licence GroupDocs poskytuje práva k obchodnímu využití.

**Q: Jak efektivně zvládnout velké sady dokumentů?**  
A: Použijte inkrementální indexování, dolaďte `IndexingOptions` pro velikost dávky a naplánujte pravidelné přestavby indexu, aby byl výkon optimální.

**Q: Jaké formáty souborů podporuje GroupDocs.Search?**  
A: Podporováno je více než 100 formátů, včetně PDF, DOCX, XLSX, PPTX, HTML, TXT a typů obrázků jako JPEG a PNG.

**Q: Existuje vícejazyčná podpora pro vyhledávání a redigování?**  
A: Ano, knihovny obsahují jazykové analyzátory pro více než 30 jazyků, což umožňuje přesné vyhledávání a redigování napříč globálním obsahem.

## Zdroje
- [dokumentace](https://docs.groupdocs.com/search/net/)  
- [Dokumentace](https://docs.groupdocs.com/search/net/)  
- [fórum podpory](https://forum.groupdocs.com/c/search/10)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Stáhnout](https://www.groupdocs.com/products/search-net)

---

**Poslední aktualizace:** 2026-07-16  
**Testováno s:** GroupDocs.Search 2.0.0 and GroupDocs.Redaction 2.0.0 for .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Zvýraznění výsledků vyhledávání v .NET dokumentech pomocí GroupDocs.Search a Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Mistrovství GroupDocs Redaction a Search v .NET: Efektivní správa dokumentů a bezpečné vyhledávání](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
- [Mistrovství redigování dokumentů s GroupDocs.Redaction .NET: Indexování a správa aliasů pro bezpečnou správu dokumentů](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)
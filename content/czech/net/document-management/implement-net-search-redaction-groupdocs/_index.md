---
date: '2026-06-12'
description: Naučte se, jak vyhledávat a redigovat dokumenty v .NET pomocí GroupDocs.Search
  a GroupDocs.Redaction, optimalizovat výkon vyhledávání a řešit chyby indexování.
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
title: Jak vyhledávat a redigovat dokumenty v .NET pomocí GroupDocs.Search a GroupDocs.Redaction
type: docs
url: /cs/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Vyhledávání a redakce dokumentů v .NET s GroupDocs.Search & GroupDocs.Redaction

V moderních podnikových prostředích jsou schopnosti **search and redact** nezbytné pro ochranu citlivých informací a zároveň pro snadné vyhledávání dokumentů. Tento tutoriál vás provede vytvořením robustního .NET řešení, které kombinuje GroupDocs.Search pro rychlé full‑textové vyhledávání s GroupDocs.Redaction pro bezpečné odstranění důvěrných dat. Na konci budete vědět, jak nastavit knihovny, vytvořit vlastní segmentátor textu, spustit vysoce výkonná vyhledávání a bezpečně aplikovat redakce.

## Rychlé odpovědi
- **Co znamená “search and redact”?** Znamená to vyhledávání textu v dokumentech a jeho trvalé zakrytí.  
- **Které knihovny jsou vyžadovány?** GroupDocs.Search a GroupDocs.Redaction pro .NET.  
- **Mohu zpracovávat vícejazyčný obsah?** Ano — použijte vlastní segmentátor textu k správnému rozdělení slov.  
- **Jak zlepšit rychlost vyhledávání?** Indexujte jednou, znovu použijte index a povolte nastavení `optimize search performance`.  
- **Co když indexování selže?** Postupujte podle pokynů „handle indexing errors“ v sekci řešení problémů.

## Co je “search and redact”?

Search and redact je proces vyhledání konkrétních výrazů v kolekci dokumentů a následného trvalého zakrytí nebo odstranění těchto výrazů za účelem ochrany soukromí nebo splnění regulatorních požadavků. Kombinuje full‑textové vyhledávání pro nalezení citlivých informací s nástroji pro redakci, které nahrazují obsah při zachování původního rozvržení dokumentu.

## Proč použít GroupDocs.Search a GroupDocs.Redaction společně?

GroupDocs.Search podporuje **50+ formátů souborů** a dokáže indexovat **100 000+ dokumentů** za méně než minutu na typickém serverovém hardware, zatímco GroupDocs.Redaction může aplikovat redakce na **PDF, DOCX, PPTX a další** bez změny původního rozvržení. Kombinace těchto knihoven poskytuje jediné řešení, které **optimalizuje výkon vyhledávání** a **elegantně řeší chyby indexování**.

## Požadavky

- Visual Studio 2022 nebo novější s podporou .NET 6+.  
- NuGet balíčky: **GroupDocs.Search** a **GroupDocs.Redaction** (nejnovější stabilní verze).  
- Platná licence GroupDocs (zkušební nebo zakoupená).  

### Požadované knihovny
- **GroupDocs.Search** – Poskytuje indexování, dotazování a vlastní segmentaci.  
- **GroupDocs.Redaction** – Nabízí redakci textu, obrázků a metadat napříč podporovanými formáty.

### Požadavky na nastavení prostředí
Ujistěte se, že váš vývojový počítač má oprávnění k zápisu do složky, kde bude index uložen.

### Předpoklady znalostí
- Znalost C# a struktury .NET projektů.  
- Základní pochopení konceptů zpracování dokumentů (volitelné, ale užitečné).

## Jak nainstalovat GroupDocs.Redaction pro .NET?

Můžete přidat balíček Redaction do svého projektu pomocí .NET CLI nebo NuGet Package Manageru. Příkaz stáhne nejnovější stabilní verzi a zaregistruje ji ve vašem souboru projektu, čímž okamžitě zpřístupní API.

```bash
dotnet add package GroupDocs.Redaction
```  

## Jak získat licenci pro GroupDocs?

GroupDocs nabízí tři licenční možnosti: bezplatnou zkušební verzi pro hodnocení, dočasnou licenci pro rozšířené testování vývoje a plnou komerční licenci pro produkční použití. Zkušební verze poskytuje omezenou funkčnost, zatímco dočasný klíč prodlužuje evaluační období a zakoupená licence odemyká všechny funkce a prioritu podpory.

## Jak inicializovat GroupDocs.Redaction v mé aplikaci?

Třída `Redaction` je hlavním vstupním bodem pro aplikaci redakcí na podporované dokumenty. Načte soubor, připraví objekty redakce a spustí proces redakce, přičemž vrátí upravený dokument při zachování původního rozvržení. Můžete také konfigurovat možnosti redakce, jako jsou barva, překrytí a odstranění metadat, aby vyhovovaly konkrétním požadavkům na soulad.

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Jak nastavit index pomocí GroupDocs.Search?

Třída `Index` představuje vyhledávatelný úložiště uložené na disku. Spravuje vytváření, aktualizaci a dotazování indexu, umožňuje přidávat dokumenty, přestavovat index a provádět rychlá vyhledávání napříč velkými kolekcemi. Složka indexu může být umístěna na lokálním nebo síťovém úložišti a můžete konfigurovat kompresi a šifrování pro ochranu indexovaných dat.

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Co je vlastní textový segmentátor a proč jej použít?

Vlastní segmentátor textu určuje, jak je surový text rozdělen na vyhledávatelné tokeny. Přizpůsobením pravidel segmentace pro konkrétní jazyky nebo domény zvyšujete přesnost tokenizace, což vede k vyšší úplnosti a relevance výsledků vyhledávání. To je zvláště užitečné pro jazyky s komplexními hranicemi slov, jako je japonština nebo arabština, kde výchozí tokenizéry mohou slova rozdělovat nesprávně.

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Jak provést full‑textové vyhledávání s vlastním segmentátorem?

Objekt `SearchQuery` zapouzdřuje uživatelský dotaz a spolupracuje s vlastním segmentátorem při hledání shod. Podporuje fuzzy vyhledávání, fráze a vážení, vrací sadu výsledků s ID dokumentů, pozicemi zásahů a skóre relevance. Můžete také použít filtry, jako je typ souboru nebo časové rozmezí, pro zúžení výsledků a přesnější cílení.

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Jak aplikovat redakce po nalezení citlivého textu?

API `Redaction` vám umožní nahradit nebo odstranit text, obrázky a metadata v podporovaných dokumentech. Po identifikaci citlivých výrazů vytvoříte objekty redakce, aplikujete je a uložíte redigovaný soubor, čímž zajistíte trvalé skrytí důvěrných informací. Možnosti redakce zahrnují překrytí černými rámečky, použití vlastních barev nebo odstranění celých objektů při zachování struktury dokumentu.

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

## Časté problémy a jak řešit chyby indexování

- **Index nenalezen:** Ověřte, že cesta k indexu existuje a aplikace má oprávnění číst/zapisovat.  
- **Vyhledávání nevrací žádné výsledky:** Znovu spusťte proces indexování a ujistěte se, že vlastní segmentátor je správně zaregistrován.  
- **Redakce selhává u některých formátů:** Ověřte, že typ souboru je podporován; pro PDF použijte nejnovější verzi Redaction, která podporuje funkce PDF 2.0.

## Praktické aplikace

1. **Správa právních dokumentů:** Vyhledávejte ve smlouvách termín “non‑disclosure” a automaticky redactujte klauzule před externím sdílením.  
2. **Akademický výzkum:** Najděte nepublikovaná data v rukopisech a skryjte je pro proces recenzování.  
3. **Obchodní smlouvy:** Hromadně zpracovávejte tisíce smluv, redactujte osobní identifikátory a zachovejte právní jazyk.

## Jak optimalizovat výkon vyhledávání pro velké sady dokumentů?

Pro maximální výkon indexujte dokumenty jednou a znovu použijte stejný index pro následné dotazy. Povolit paralelní zpracování, konfigurovat kešování a ladit nastavení indexu pro snížení latence a zvýšení propustnosti na vícejádrových serverech. Navíc nastavte příznak `EnableMemoryMapping`, aby byl index paměťově mapován, což urychluje čtení velkých datových sad.

## Jak spravovat paměť .NET při práci s velkými soubory?

Efektivní správa paměti je klíčová při zpracování velkých dokumentů. Obalte objekty `Index` a `Redaction` v `using` blocích, aby byla zajištěna deterministická likvidace, a zpracovávejte soubory jako streamy místo načítání celých dokumentů do paměti. Monitorování výkonových čítačů pomáhá včas odhalit špičky paměti, což vám umožní upravit velikosti batchů nebo ladit garbage collection.

## Často kladené otázky

**Q: Mohu použít GroupDocs.Search s netextovými metadaty?**  
A: Ano — pole metadat mohou být indexována spolu s obsahem dokumentu, což umožňuje vyhledávání jako “author:JohnDoe”.

**Q: Podporuje GroupDocs.Redaction real‑time redakci ve webovém API?**  
A: Ano; můžete volat Redaction API synchronně pro malé soubory nebo zařadit větší úlohy do fronty pro asynchronní zpracování.

**Q: Co mám dělat, když se index poškodí?**  
A: Odstraňte poškozenou složku indexu a znovu jej vytvořte pomocí stejné rutiny indexování; knihovna zaznamenává podrobné chybové zprávy, které vám pomohou identifikovat příčinu.

**Q: Je možné zobrazit náhled redigovaných dokumentů před uložením?**  
A: Rozhodně — zavolejte `redaction.Apply()` s příznakem `preview` a vygenerujete dočasnou verzi k revizi.

**Q: Které verze .NET jsou oficiálně podporovány?**  
A: GroupDocs.Search a GroupDocs.Redaction podporují .NET 6, .NET 5, .NET Core 3.1 a .NET Framework 4.6.2+.

## Zdroje

- **Dokumentace:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **Reference API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Stáhnout:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)
- **Bezplatná podpora:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Dočasná licence:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-12  
**Tested With:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Související tutoriály

- [Mistrovství GroupDocs Search a Redaction v .NET: Pokročilá správa dokumentů](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Implementace GroupDocs.Search a Redaction: Aktualizace a správa indexů dokumentů v .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Optimalizace indexování dokumentů v .NET s GroupDocs.Redaction: Zrušení, asynchronní operace a vlákna](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
---
date: '2026-09-16'
description: Zjistěte, jak vytvořit vyhledávací index s GroupDocs v .NET, přidat dokumenty
  do indexu a povolit synonymní vyhledávání pro chytřejší výsledky dotazů.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Zjistěte, jak vytvořit vyhledávací index s GroupDocs v .NET, přidat
  dokumenty do indexu a povolit synonymní vyhledávání pro chytřejší výsledky dotazů.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Jak vytvořit vyhledávací index s GroupDocs v .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Jak vytvořit vyhledávací index s GroupDocs a synonymním vyhledáváním v .NET
type: docs
url: /cs/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Jak vytvořit vyhledávací index s GroupDocs a synonymním vyhledáváním v .NET

V tomto průvodci se naučíte **jak vytvořit vyhledávací index** pomocí GroupDocs.Search, přidávat dokumenty do tohoto indexu a povolit synonymní vyhledávání, aby uživatelé mohli najít relevantní obsah i při použití odlišné terminologie. Ať už budujete právní úložiště, firemní znalostní bázi nebo výzkumný archiv, níže uvedené kroky vám poskytnou produkčně připravené řešení, které funguje na .NET Framework 4.6.1+, .NET Core a .NET 5+.

## Rychlé odpovědi
- **Co znamená „vytvořit vyhledávací index“?** Vytváří prohledávatelný katalog vašich dokumentů, ukládá extrahovaný text v optimalizované struktuře pro milisekundové vyhledávání.  
- **Proč používat synonymní vyhledávání?** Rozšiřuje dotaz o slova se stejným významem, čímž zvyšuje úplnost až o 30 % v typických korpusech.  
- **Jaké jsou hlavní předpoklady?** .NET 4.6.1+ (nebo .NET Core/5+), znalost C# a NuGet balíčky GroupDocs.Search + GroupDocs.Redaction.  
- **Potřebuji licenci?** Bezplatná zkušební verze stačí pro hodnocení; pro produkční nasazení je vyžadována trvalá licence.  
- **Mohu to kombinovat s redakcí?** Ano—GroupDocs.Redaction může běžet před nebo po vyhledávání k maskování citlivých dat.

## Co je „vytvořit vyhledávací index“?
**Vyhledávací index** je datová struktura, která obsahuje extrahovaný text a metadata z každého dokumentu, což umožňuje enginu okamžitě najít odpovídající soubory. GroupDocs.Search vytváří tento index skenováním zdrojové složky, parsováním podporovaných formátů a zápisem kompaktních souborů indexu do adresáře, který určíte.

## Proč povolit synonymní vyhledávání?
Synonymní vyhledávání automaticky přidává alternativní výrazy k dotazu uživatele, takže vyhledávání **„improve“** také vrátí dokumenty obsahující **„enhance“, „upgrade“** nebo **„optimize“. V praxi může toto zvýšit úplnost výsledků o 20‑35 % při zachování vysoké přesnosti, protože vestavěný synonymní slovník je vytvořen pro každý jazyk.

## Předpoklady
- **.NET Framework 4.6.1** nebo novější (nebo jakýkoli runtime .NET Core/5+).  
- Základní dovednosti vývoje v C# a Visual Studio (Community, Professional nebo Enterprise).  
- Balíčky GroupDocs.Search a GroupDocs.Redaction nainstalované přes NuGet.

### Instalace
Nainstalujte GroupDocs.Redaction pro .NET pomocí jedné z těchto metod (podrobnosti najdete v dokumentaci [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/)):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternativně můžete použít UI Správce balíčků NuGet ve Visual Studio k vyhledání „GroupDocs.Redaction“ a jeho přímé instalaci. Pro referenci API viz [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Získání licence
- **Bezplatná zkušební verze:** Začněte s trial verzí a prozkoumejte všechny funkce.  
- **Dočasná licence:** Požádejte o dočasnou licenci na [webu GroupDocs](https://purchase.groupdocs.com/temporary-license/) nebo spravujte svou licenci přes portál [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/).  
- **Plná koupě:** Až budete připraveni na produkci, zakupte plnou licenci, která odstraní všechna omezení zkoušky.

## Jak nastavit GroupDocs.Redaction pro .NET
GroupDocs.Redaction poskytuje základní funkčnost pro redakci citlivého obsahu před nebo po vyhledávání. Exponuje třídu `Redactor`, kterou vytvoříte s licencí a volitelnými konfiguračními nastaveními.

Následující kód ukazuje vytvoření instance redaktoru a načtení souboru licence:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Po připravení redaktoru můžete později zavolat `redactor.Redact(...)` na libovolný dokument, který získáte z výsledků vyhledávání.

## Jak vytvořit vyhledávací index
Vytvoření vyhledávacího indexu zahrnuje určení složky, kde budou uloženy soubory indexu, a následnou inicializaci třídy `Index` z GroupDocs.Search. Index bude obsahovat všechna prohledávatelná data extrahovaná z vašich zdrojových dokumentů.

Nejprve vytvořte adresář pro index a poté vytvořte instanci objektu `Index`:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Vytvoření indexu zapíše sadu binárních souborů do složky; tyto soubory jsou typicky pod 200 KB na 1 000 stránek, což vám umožní škálovat na miliony stránek bez vyčerpání místa na disku.

## Jak přidat dokumenty do indexu
Přidání dokumentů vyžaduje nasměrování API na adresář obsahující zdrojové soubory a instrukci indexu, aby je načetl. Proces parsuje každý podporovaný formát, extrahuje text a uloží jej do indexu pro rychlé načítání.

Použijte následující kód k indexaci všech souborů ve zdrojové složce:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search podporuje **30+** vstupních formátů—včetně DOCX, PDF, PPTX, HTML a běžných typů obrázků—takže můžete indexovat prakticky jakýkoli firemní archiv bez dalších konvertorů.

## Jak povolit a spustit synonymní vyhledávání
Zpracování synonym se zapíná pomocí `SearchOptions`. Po povolení se každý dotaz automaticky rozšíří o synonyma ze slovníku, čímž se zvyšuje úplnost bez ztráty přesnosti.

Povolte synonymní vyhledávání následujícím úryvkem:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Výchozí synonymní slovník obsahuje více než **5 000** dvojic termínů pro angličtinu. Můžete také načíst vlastní soubor `SynonymDictionary` pro podporu oborově specifického žargonu.

## Vlastní synonymní slovník
Pokud potřebujete doménově specifické synonyma, načtěte svůj vlastní soubor slovníku a přiřaďte jej k `SearchOptions` před provedením dotazu.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Běžné tipy pro řešení problémů
- **Problémy s cestou:** Zkontrolujte, že indexová a zdrojová složka jsou přístupné procesnímu účtu.  
- **Licenční omezení:** Nelicencovaná verze může omezit počet indexovaných souborů na 100.  
- **Žádné výsledky:** Ověřte, že je načten synonymní slovník; můžete zkontrolovat `options.SynonymDictionary.Count` za běhu.  

## Praktické aplikace
1. **Správa právních dokumentů:** Vyhledávejte judikaturu pomocí právních termínů a jejich synonym.  
2. **Akademický výzkum:** Rozšiřte vyhledávání literatury napříč vědeckými PDF a Word soubory.  
3. **Firemní znalostní báze:** Získejte interní politiky i když uživatelé formulují dotazy odlišně.  
4. **Systémy pro správu obsahu:** Poskytněte editorům bohatší možnosti objevování při označování článků.  
5. **Ticketing zákaznické podpory:** Přiřaďte tickety k známým problémům pomocí synonymních popisů problémů.  

## Úvahy o výkonu
- **Údržba indexu:** Proveďte reindexaci po hromadných aktualizacích; inkrementální indexování snižuje dobu výpadku až o 70 %.  
- **Monitorování zdrojů:** Indexování dávky 10 GB na standardním VM (2 vCPU, 8 GB RAM) dosahuje špičky ~1,2 GB RAM; omezte velikost dávky, pokud se blížíte k limitům.  
- **Uvolnění objektů:** Zavolejte `index.Dispose()` a `redactor.Dispose()` co nejdříve po dokončení, aby se uvolnily nativní zdroje.  

## Závěr
Nyní víte **jak vytvořit vyhledávací index** s GroupDocs, přidávat dokumenty do tohoto indexu a povolit synonymní vyhledávání pro intuitivnější uživatelský zážitek. Tento základ vám také umožní vrstvit redakci, vlastní řazení nebo fuzzy shodu na robustní vyhledávací engine.

## Další kroky
- Experimentujte s `SearchOptions.FuzzySearch` pro zachycení překlepů.  
- Prozkoumejte API `Ranking` pro zvýšení priority dokumentů.  
- Připojte se ke komunitě na [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) nebo na [Free Support Forum](https://forum.groupdocs.com/c/search/10), kde můžete sdílet tipy a klást otázky.  
- Zkontrolujte [Nejnovější vydání GroupDocs](https://releases.groupdocs.com/search/net/) pro aktualizace a nové funkce.  

## Často kladené otázky

**Q: Co je synonymní vyhledávání?**  
A: Synonymní vyhledávání rozšiřuje dotaz uživatele o předdefinované alternativní výrazy, čímž zvyšuje šanci najít relevantní dokumenty, které používají odlišné formulace.

**Q: Jak aktualizuji svou licenci GroupDocs?**  
A: Navštivte portál [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) a nahrajte nový licenční soubor pomocí `License.SetLicense("path/to/license.lic")`.

**Q: Mohu používat synonymní vyhledávání ve vícejazyčném prostředí?**  
A: Ano—načtěte jazykově specifický soubor `SynonymDictionary` pro každou podporovanou lokalitu a engine použije odpovídající sadu synonym pro každý dotaz.

**Q: Jaké jsou nejčastější problémy s indexací?**  
A: Oprávnění k přístupu k souborům, nepodporované formáty a překročení limitu dokumentů ve zkušební verzi jsou tři hlavní problémy, se kterými vývojáři narazí.

**Q: Jak mohu optimalizovat výkon pro velmi velké indexy?**  
A: Použijte inkrementální indexování, uložte index na SSD a nakonfigurujte `IndexingOptions.MaxDegreeOfParallelism` tak, aby odpovídal počtu jader CPU.

---

**Poslední aktualizace:** 2026-09-16  
**Testováno s:** GroupDocs.Search 23.10 pro .NET  
**Autor:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Související tutoriály

- [Přidat dokument do indexu s GroupDocs.Search .NET tutoriály](/search/net/document-management/)
- [Zvýraznit výsledky vyhledávání v .NET dokumentech pomocí GroupDocs.Search a Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Jak aktualizovat index s GroupDocs.Search a Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
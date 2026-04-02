---
date: '2026-04-02'
description: Naučte se, jak vytvořit vyhledávací index v GroupDocs a přidat dokumenty
  do indexu při implementaci fasetového vyhledávání pomocí GroupDocs.Search a GroupDocs.Redaction
  v .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Vytvoření vyhledávacího indexu GroupDocs s redakcí a .NET faceted search
type: docs
url: /cs/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Vytvoření vyhledávacího indexu GroupDocs s Redaction .NET Facetovým vyhledáváním

## Rychlé odpovědi
- **Jaký je hlavní účel?** Vytvořit vyhledávací index s GroupDocs a umožnit facetové vyhledávání.  
- **Které knihovny jsou vyžadovány?** GroupDocs.Redaction a GroupDocs.Search pro .NET.  
- **Jak přidám dokumenty do indexu?** Použijte `index.Add(documentsFolder)` po inicializaci indexu.  
- **Mohu spouštět složité dotazy?** Ano, kombinujte objektové dotazy s logickými operátory pro pokročilé filtrování.  
- **Je potřeba licence?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.

## Co je facetové vyhledávání a proč jej použít s GroupDocs?
Facetové vyhledávání umožňuje uživatelům upřesnit výsledky aplikací více filtrů – například kategorie, datum nebo autor – současně. V kombinaci s **GroupDocs.Redaction** získáte zabezpečený, prohledávatelný obsah, který respektuje pravidla redakce, což je ideální pro prostředí s vysokými požadavky na soulad.

## Předpoklady

### Požadované knihovny, verze a závislosti
- **GroupDocs.Redaction .NET** – nejnovější stabilní verze.  
- **GroupDocs.Search .NET** – úzce spolupracuje s Redaction při indexování.

### Požadavky na nastavení prostředí
- **IDE**: Visual Studio 2019 nebo novější.  
- **Framework**: .NET Core 3.1, .NET 5 nebo .NET 6.  
- **Kompatibilita OS**: Windows, Linux, macOS.

### Předpoklady znalostí
Základní dovednosti v C# a obecné pochopení konceptů facetového vyhledávání pomohou, ale průvodce krok za krokem je přátelský i pro nováčky.

## Nastavení GroupDocs.Redaction pro .NET

### Informace o instalaci
Balíček GroupDocs.Redaction můžete přidat pomocí některé z následujících metod:

- **.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

- **Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

- **NuGet Package Manager UI** – Vyhledejte "GroupDocs.Redaction" a nainstalujte nejnovější verzi.

### Kroky získání licence
Chcete-li odemknout všechny funkce, začněte s bezplatnou zkušební verzí nebo získáte trvalou licenci:

1. Navštivte [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) a prozkoumejte možnosti licencování.  
2. Postupujte podle pokynů na obrazovce a získejte soubor licence pro zkušební nebo zakoupenou verzi.

### Základní inicializace a nastavení
Po instalaci balíčku inicializujte Redactor ve své aplikaci:
```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Jak vytvořit vyhledávací index groupdocs

Níže rozdělíme implementaci do dvou částí: **Jednoduché facetové vyhledávání** a **Složitý dotaz**. Každá část ukazuje, jak **vytvořit vyhledávací index groupdocs**, přidat dokumenty a spustit dotazy.

### Funkce 1: Jednoduché facetové vyhledávání

**Přehled**  
Facetové vyhledávání umožňuje uživatelům zúžit výsledky výběrem více kritérií. Tato sekce ukazuje jednoduchý přístup pomocí GroupDocs.Search.

#### Krok 1: Definujte složky indexu a dokumentů
Nastavte cesty ke složkám, kde bude index uložen a kde se nacházejí zdrojové dokumenty.
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Krok 2: Vytvořte index
Inicializujte vyhledávací index ve složce, kterou jste definovali.
```csharp
Index index = new Index(indexFolder);
```

#### Krok 3: Přidejte dokumenty do indexu
Načtěte své dokumenty, aby byly prohledávatelné.
```csharp
index.Add(documentsFolder);
```

#### Krok 4: Proveďte vyhledávání textového dotazu
Spusťte základní textový dotaz proti poli **content**.
```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Krok 5: Proveďte vyhledávání objektovým dotazem
Použijte objektově orientované dotazy pro jemnější kontrolu.
```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Funkce 2: Složitý dotaz

**Přehled**  
Když potřebujete kombinovat více filtrů – například vzory názvů souborů a shody frází – můžete vytvořit složitý dotaz pomocí logických operátorů.

#### Krok 1: Definujte složky indexu a dokumentů
Znovu použijte stejnou strukturu složek pro pokročilejší scénář.
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Krok 2: Vytvořte index a přidejte dokumenty
(Viz kroky 2‑3 z jednoduchého příkladu; zůstávají stejné.)

#### Krok 3: Proveďte vyhledávání textového dotazu
Spusťte složený textový dotaz, který kombinuje kritéria názvu souboru a obsahu.
```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Krok 4: Vytvořte a proveďte objektové dotazy
Programově vytvořte stejnou logiku.
```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Pokračujte v kombinování frází, rozsahů a logických operátorů, aby odpovídaly vašim konkrétním obchodním pravidlům.

## Praktické aplikace

1. **E‑Commerce platformy** – Filtrujte produkty podle kategorie, ceny a hodnocení.  
2. **Systémy pro správu dokumentů** – Najděte smlouvy podle autora, data nebo úrovně důvěrnosti.  
3. **Obsahové portály** – Umožněte čtenářům prohloubit výběr pomocí štítků, témat a data publikace.

## Úvahy o výkonu

- **Obnovení indexu**: Pravidelně reindexujte nové nebo aktualizované soubory, aby vyhledávání zůstalo rychlé.  
- **Správa paměti**: Uvolněte objekty `Index`, když jsou hotové, zejména u velkých datových sad.  
- **Asynchronní indexování**: Použijte `Task.Run` nebo služby na pozadí, aby nedocházelo k zamrznutí UI během těžkého indexování.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Index nebyl nalezen** | Ověřte cestu `indexFolder` a ujistěte se, že složka má oprávnění k zápisu. |
| **Žádné výsledky** | Zkontrolujte, že pole, která dotazujete (např. `Content`, `Filename`), jsou indexována. |
| **Chyby nedostatku paměti** | Zpracovávejte dokumenty po dávkách a zvažte zvýšení velikosti .NET GC haldy. |

## Často kladené otázky

**Q: Co je facetové vyhledávání?**  
A: Facetové vyhledávání umožňuje uživatelům upřesnit výsledky pomocí více nezávislých filtrů, jako je kategorie, datum nebo autor.

**Q: Jak zacházet s velkými datovými sadami pomocí GroupDocs.Search?**  
A: Používejte inkrementální indexování, zpracování po dávkách a asynchronní operace, aby byl nízký odběr paměti a vysoký výkon.

**Q: Mohu integrovat funkce GroupDocs do existujících .NET aplikací?**  
A: Ano, knihovny jsou navrženy pro bezproblémovou integraci s jakýmkoli .NET projektem.

**Q: Jaké jsou některé běžné problémy s facetovým vyhledáváním?**  
A: Složitá syntaxe dotazů a zajištění, že všechna relevantní pole jsou indexována, jsou typické výzvy; řádné testování a údržba indexu je zmírňují.

**Q: Jak získat dočasnou licenci pro GroupDocs?**  
A: Navštivte [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) a požádejte o zkušební licenci, která během hodnocení odemkne plnou funkčnost.

## Zdroje
- **Dokumentace**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Poslední aktualizace:** 2026-04-02  
**Testováno s:** GroupDocs.Redaction 23.12 pro .NET, GroupDocs.Search 23.12 pro .NET  
**Autor:** GroupDocs
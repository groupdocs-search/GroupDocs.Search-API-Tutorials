---
date: '2026-10-07'
description: Zjistěte, jak implementovat vyhledávání s vlastním formátem data v Java
  pomocí GroupDocs, zahrnující dotazy v rozmezí dat, vlastní vzory a tipy na výkon.
keywords:
- custom date format java
- search documents by date
- date range query example
- optimize search performance
- configure custom date pattern
lastmod: '2026-10-07'
og_description: Tutoriál o vlastním formátu data v Java ukazuje, jak nakonfigurovat
  GroupDocs.Search pro Java, spustit dotazy v rozmezí dat a zvýšit výkon. Postupujte
  podle krok‑za‑krokem příkladů.
og_image_alt: Guide illustrating custom date format java usage in GroupDocs Search
og_title: Vlastní formát data java – průvodce vyhledáváním v rozmezí dat s GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-07'
  description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  headline: Custom date format java | date range search with GroupDocs
  type: TechArticle
- description: Learn how to implement custom date format java searches with GroupDocs,
    covering date range queries, custom patterns, and performance tips.
  name: Custom date format java | date range search with GroupDocs
  steps:
  - name: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
    text: '**Archival systems** – Retrieve records from a specific historical period
      without manually normalising dates.'
  - name: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
    text: '**Content management** – Support regional date formats like `dd/MM/yyyy`
      for European audiences, improving user satisfaction.'
  - name: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
    text: '**Financial software** – Filter transactions by fiscal quarter or year
      quickly, enabling real‑time reporting dashboards.'
  type: HowTo
- questions:
  - answer: Text form is quick and easy but limited to the default ISO format; object‑based
      queries let you supply `Date` objects and custom formats for greater flexibility.
    question: What is the difference between text form and object‑based date queries?
  - answer: Yes, combine `daterange` clauses with logical operators like `AND` or
      `OR` to build complex queries.
    question: Can I search for multiple date ranges in a single query?
  - answer: There is a minor overhead for additional parsing, but the impact is negligible
      for typical workloads and is outweighed by the accuracy gains.
    question: Will custom date formats slow down the search?
  - answer: Absolutely. With proper indexing strategies and JVM tuning, it scales
      to millions of documents while maintaining sub‑second query response times.
    question: Is GroupDocs.Search suitable for large‑scale deployments?
  - answer: Explore the [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
      for additional samples and use‑case implementations.
    question: Where can I find more Java examples?
  type: FAQPage
tags:
- custom date format
- GroupDocs.Search
- Java date handling
- document indexing
- search optimization
title: Vlastní formát data java | vyhledávání v rozmezí dat s GroupDocs
type: docs
url: /cs/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Vlastní formát data v Javě | vyhledávání v rozmezí dat pomocí GroupDocs

Hledání dokumentů podle data je častý požadavek — ať už vytváříte archivní systém, nástroj pro finanční výkaznictví nebo portál pro správu obsahu. V tomto tutoriálu se naučíte techniky **custom date format java** pomocí GroupDocs.Search, zahrnující dotazy na rozmezí dat, definice vlastních vzorů a tipy k **optimize search performance**. Na konci budete schopni umožnit uživatelům získat záznamy spadající do libovolného časového intervalu, bez ohledu na použité formátování.

## Rychlé odpovědi
- **Jaká je hlavní třída pro indexování?** `Index` from the `com.groupdocs.search` package.  
- **Jak definovat vlastní vzor data?** Use `DateFormat` with `DateFormatElement` objects and a separator.  
- **Mohu vyhledávat pomocí textového dotazu?** Yes, the `daterange(start ~~ end)` syntax works directly in the query string.  
- **Jaké Maven koordináty jsou vyžadovány?** `com.groupdocs:groupdocs-search:25.4` (or newer).  
- **Potřebuji licenci pro vývoj?** A free trial or temporary license is sufficient for testing; a commercial license is required for production.

## Co je vlastní formát data v Javě?
Custom date format java říká GroupDocs.Search, jak interpretovat řetězce dat, které neodpovídají výchozímu ISO vzoru (YYYY‑MM‑DD). Definováním vlastního vzoru — například `MM/dd/yyyy` nebo `dd‑MM‑yyyy` — umožníte enginu rozpoznat data vložená v dokumentech, které používají regionální nebo starší formáty. Tato schopnost vám umožní indexovat a dotazovat se na data konzistentně napříč heterogenními zdroji, což zlepšuje jak recall, tak precision pro vyhledávání zaměřené na data.

## Proč použít GroupDocs.Search pro dotazy na rozmezí dat?
GroupDocs.Search kombinuje vysokorychlostní indexování s flexibilní konstrukcí dotazů, což z něj činí ideální nástroj pro scénáře s rozmezím dat. Engine dokáže rychle najít dokumenty, které obsahují data v určeném intervalu, i když se data objevují ve volném textu nebo v polích metadat. Jeho vestavěná podpora pro více souborových formátů a přizpůsobitelné parsování dat znamená, že můžete zpracovávat rozmanité kolekce dokumentů bez psaní kódu specifického pro formát, a přitom dosahovat subsekundových odezvových časů u velkých indexů.

## Jak vyhledávat dokumenty podle data pomocí GroupDocs.Search
Nastavíte knihovnu, indexujete ukázkovou složku a poté spustíte jak jednoduché dotazy ve formě textu, tak i bohatší dotazy založené na objektech. Proces začíná vytvořením instance `Index`, konfigurací všech potřebných vlastních formátů data a následným voláním vyhledávacího API buď s prostým řetězcem, nebo se strukturovaným `SearchQuery`. Tento přístup vám umožní zvolit úroveň kontroly, která odpovídá požadavkům vaší aplikace.

### Požadavky
- Java 8 nebo novější nainstalována.  
- Maven pro správu závislostí.  
- Přístup k licenci GroupDocs.Search (zkušební nebo dočasná licence funguje pro vývoj).  

### Nastavení GroupDocs.Search pro Javu

#### Instalace pomocí Maven
Add the repository and dependency to your `pom.xml`:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

#### Přímé stažení
Alternativně můžete nejnovější verzi stáhnout přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Základní inicializace a nastavení
Vytvořte instanci `Index` a přidejte své dokumenty:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

**Definition anchor:** Třída `Index` je hlavní kontejner, který ukládá prohledávatelná metadata pro každý soubor, který přidáte, a umožňuje rychlé vyhledávání napříč velkými kolekcemi.

## Funkce 1: vytváření dotazů na vyhledávání v rozmezí dat

### Použití textového dotazu
Nejjednodušší způsob je vložit rozmezí dat přímo do řetězce dotazu:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a text-based query for the specified date range
String query1 = "daterange(2017-01-01 ~~ 2019-12-31)";
SearchResult result1 = index.search(query1);
```

**Direct answer:** Načtěte svůj index a poté zavolejte `search("daterange(2022-01-01 ~~ 2022-12-31)")`, aby se získaly všechny dokumenty, jejichž indexované datum spadá mezi 1. ledna 2022 a 31. prosince 2022. Tento jednorázový dotaz funguje ihned a vrací výsledky seřazené podle relevance.

**Explanation:** Syntax `daterange` očekává data ve formátu `YYYY‑MM‑DD`. Vrací všechny dokumenty, jejichž indexovaná data spadají do zadaného intervalu.

### Použití objektu dotazu
Pro programovou kontrolu a vlastní parsování vytvořte objekt `SearchQuery`. Třída `SearchQuery` představuje strukturovaný dotaz, který může kombinovat více kritérií, jako jsou klíčová slova, filtry a rozmezí dat.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Create a date range query using the Query API
SearchQuery query2 = SearchQuery.createDateRangeQuery(Utils.createDate(2017, 1, 1), Utils.createDate(2019, 12, 31));
SearchResult result2 = index.search(query2);
```

**Direct answer:** Vytvořte `SearchQuery` pomocí `createDateRangeQuery(startDate, endDate)`, kde `startDate` a `endDate` jsou instance `java.util.Date`; poté předáte dotaz metodě `index.search(query)`, abyste získali přesné výsledky, které respektují posuny časových pásem a kalendáře specifické pro locale.

**Definition anchor:** Třída `SearchQuery` zapouzdřuje všechna kritéria vyhledávání a umožňuje kombinovat rozmezí dat s filtry klíčových slov, Booleovými operátory a pravidly pro zvýšení relevance.

**Explanation:** `createDateRangeQuery` vám umožňuje předat objekty `java.util.Date`, což poskytuje plnou flexibilitu nad časovými pásmy a locale‑specifickým zpracováním.

## Funkce 2: specifikace vlastních vzorů formátu data v Javě

### Nastavení vlastních formátů data
Třída `DateFormat` říká enginu, jak rozdělit a interpretovat řetězec data na základě pořadí prvků a znaků oddělovače. Definujte `DateFormat`, který odpovídá reprezentaci data ve vašem dokumentu:

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;
import com.groupdocs.search.results.*;

// Define directories (as previously shown)

Index index = new Index(indexFolder);
index.add(documentsFolder);

// Configure search options with custom date formats
SearchOptions options = new SearchOptions();
options.getDateFormats().clear(); // Remove default formats

DateFormatElement[] elements = new DateFormatElement[]{
    DateFormatElement.getMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getDayOfMonthTwoDigits(),
    DateFormatElement.getDateSeparator(),
    DateFormatElement.getYearFourDigits()
};

// Create a custom date format pattern 'MM/dd/yyyy'
DateFormat dateFormat = new DateFormat(elements, "/");
options.getDateFormats().addItem(dateFormat);

String query = "daterange(01/01/2017 ~~ 12/31/2019)";
SearchResult result = index.search(query, options);
```

**Direct answer:** Vymažte výchozí formáty pomocí `dateFormat.clear()`, poté přidejte nový `DateFormat` vytvořený z objektů `DateFormatElement` (měsíc, den, rok) a nastavte oddělovač na `/`. Po tomto kroku engine správně parsuje data ve formátu `MM/dd/yyyy` během indexování i dotazování.

**Definition anchor:** `DateFormat` je konfigurační objekt, který říká GroupDocs.Search, jak rozdělit a interpretovat řetězec data na základě pořadí prvků a znaků oddělovače.

**Explanation:** Vymazáním výchozích formátů a přidáním `DateFormat`, který používá `/` jako oddělovač, engine nyní rozumí datům ve formátu `MM/dd/yyyy`. To je nezbytné pro **search documents by date** v regionech, které upřednostňují zápis měsíc‑den‑rok.

## Tipy pro optimalizaci výkonu vyhledávání
- **Indexovat inkrementálně:** Přidávejte nové soubory do existujícího indexu místo přestavování od nuly; tím se sníží využití CPU až o 70 % při denních aktualizacích.  
- **Odstraňovat zastaralá data:** Pravidelně odstraňujte dokumenty, které již nejsou potřeba; úsporný index zlepšuje míru zásahů do cache a snižuje latenci dotazů.  
- **Upravit nastavení paměti:** Zvyšte haldu JVM (`-Xmx4g` nebo vyšší) při práci s indexy většími než 5 GB, aby se předešlo chybám out‑of‑memory.  
- **Povolit vícevláknové indexování:** Použijte `IndexingOptions.setThreadCount(Runtime.getRuntime().availableProcessors())` k paralelizaci zpracování dokumentů a zkrácení času indexování přibližně o počet jader CPU.

## Časté problémy a řešení
- **Chyby při parsování data:** Ověřte, že řetězce data v dokumentu přesně odpovídají definovanému vlastnímu vzoru; nesoulad oddělovačů nebo chybějící úvodní nuly způsobují selhání.  
- **Chybějící výsledky:** Ujistěte se, že indexovaná pole obsahují metadata data; pokud dokument má data jen ve volných textových odstavcích, povolte možnost `ExtractDateMetadata` během indexování.  
- **Výjimky při přístupu k indexu:** Ověřte, že cesta `indexFolder` je zapisovatelná a není uzamčena jiným procesem; použijte dedikovanou složku pro každé prostředí (dev, test, prod), aby nedocházelo ke konfliktům.

## Praktické aplikace
1. **Archivační systémy** – Získávejte záznamy z konkrétního historického období bez ruční normalizace dat.  
2. **Správa obsahu** – Podporujte regionální formáty dat jako `dd/MM/yyyy` pro evropské uživatele, což zvyšuje spokojenost uživatelů.  
3. **Finanční software** – Rychle filtrujte transakce podle fiskálního čtvrtletí nebo roku, což umožňuje dashboardy s reportováním v reálném čase.

## Proč je to důležité
Implementace **custom date format java** odstraňuje překážky spojené s nejednotnými reprezentacemi dat v dokumentech. Umožňuje vám **handle multiple date formats** v jednom indexu, což zajišťuje, že koncoví uživatelé získají přesné výsledky bez ohledu na to, jak byla data původně zaznamenána. Tato flexibilita zlepšuje relevanci vyhledávání, snižuje úsilí při předzpracování a zkracuje čas k hodnotě pro aplikace zaměřené na data.

## Další kroky
- Prozkoumejte pokročilejší kombinace dotazů pomocí operátorů `AND`, `OR` a `NOT`.  
- Experimentujte s vlastními analyzátory, pokud potřebujete indexovat další časová metadata, jako jsou časové razítka vložená do XML tagů.  
- Projděte si průvodce laděním výkonu v oficiální dokumentaci, abyste mohli škálovat řešení na miliony dokumentů a multi‑tenantní prostředí.

## Často kladené otázky

**Q: Jaký je rozdíl mezi textovým dotazem a objektově‑založenými dotazy na datum?**  
A: Textový dotaz je rychlý a jednoduchý, ale omezený na výchozí ISO formát; objektově‑založené dotazy vám umožní předat objekty `Date` a vlastní formáty pro větší flexibilitu.

**Q: Mohu vyhledávat více rozmezí dat v jednom dotazu?**  
A: Ano, kombinujte klauzule `daterange` s logickými operátory jako `AND` nebo `OR` pro tvorbu složitých dotazů.

**Q: Zpomalí vlastní formáty data vyhledávání?**  
A: Existuje mírná režie navíc pro parsování, ale dopad je zanedbatelný pro typické pracovní zatížení a je vyvážen přesností, kterou přináší.

**Q: Je GroupDocs.Search vhodný pro rozsáhlá nasazení?**  
A: Rozhodně. S vhodnými strategiemi indexování a laděním JVM se škáluje na miliony dokumentů při zachování subsekundových odezvových časů dotazů.

**Q: Kde najdu více příkladů v Javě?**  
A: Prozkoumejte [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) pro další ukázky a implementace případů použití.

**Zdroje**
- **Dokumentace:** [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Stáhnout:** [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub repozitář:** [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Zobrazit na GitHubu:** [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Bezplatné fórum podpory:** [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Dočasná licence:** [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

**Poslední aktualizace:** 2026-10-07  
**Testováno s:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs  

## Související tutoriály

- [Groupdocs Search Java Pokročilé funkce vyhledávání](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Java knihovna pro full‑textové vyhledávání – optimalizace indexu pomocí GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Jak přidat dokumenty do indexu s indexováním metadat v Javě pomocí GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
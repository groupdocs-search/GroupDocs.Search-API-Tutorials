---
date: '2025-12-18'
description: Naučte se, jak implementovat vyhledávání v Javě s vlastním formátem data
  pomocí GroupDocs.Search, včetně dotazů na časové intervaly, vlastních vzorů a tipů
  na výkon.
keywords:
- GroupDocs.Search Java
- date range searches
- Java text search library
- custom date formats
- indexing documents
- search query optimization
title: 'Vlastní formát data v Javě: Vyhledávání v rozmezí dat pomocí GroupDocs'
type: docs
url: /cs/java/advanced-features/master-date-range-searches-groupdocs-java/
weight: 1
---

# Vlastní formát data Java: Vyhledávání v rozmezí dat s GroupDocs

Vyhledávání dokumentů podle data je častý požadavek — ať už vytváříte archivní systém, nástroj pro finanční výkaznictví nebo portál pro správu obsahu. V tomto tutoriálu se naučíte techniky **custom date format java** pomocí GroupDocs.Search, zahrnující dotazy na rozmezí dat, definice vlastních vzorů a tipy na **optimalizaci výkonu vyhledávání**. Na konci budete schopni umožnit uživatelům získat záznamy spadající do libovolného časového intervalu, bez ohledu na použité formátování.

## Rychlé odpovědi
- **Jaká je hlavní třída pro indexování?** `Index` from the `com.groupdocs.search` package.  
- **Jak definovat vlastní vzor data?** Použijte `DateFormat` s objekty `DateFormatElement` a oddělovačem.  
- **Mohu vyhledávat pomocí textového dotazu?** Ano, syntaxe `daterange(start ~~ end)` funguje přímo v řetězci dotazu.  
- **Jaké Maven koordináty jsou požadovány?** `com.groupdocs:groupdocs-search:25.4` (nebo novější).  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební nebo dočasná licence stačí pro testování; pro produkci je vyžadována komerční licence.

## Co je **custom date format java**?
A **custom date format java** říká GroupDocs.Search, jak interpretovat řetězce dat, které neodpovídají výchozímu ISO vzoru (YYYY‑MM‑DD). Definováním vlastního vzoru — například `MM/dd/yyyy` nebo `dd‑MM‑yyyy` — umožníte enginu rozpoznat data vložená v dokumentech, které používají regionální nebo starší formáty.

## Proč použít GroupDocs.Search pro dotazy na rozmezí dat?
- **Rychlost:** Vestavěné indexování umožňuje vyhledávání O(log n).  
- **Flexibilita:** Podporuje tvorbu dotazů jak na základě textu, tak na základě objektů.  
- **Podpora více formátů:** Zpracovává PDF, Word, Excel, prostý text a další bez extra kódu.  

## Jak **vyhledávat dokumenty podle data** s GroupDocs.Search
Níže najdete krok‑za‑krokem průvodce, který vás provede nastavením knihovny, indexováním souborů a prováděním jak jednoduchých, tak pokročilých vyhledávání v rozmezí dat.

### Předpoklady
- Java 8 nebo novější nainstalováno.  
- Maven pro správu závislostí.  
- Přístup k licenci GroupDocs.Search (zkušební nebo dočasná licence funguje pro vývoj).  

### Nastavení GroupDocs.Search pro Java

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
Alternativně můžete stáhnout nejnovější verzi přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Základní inicializace a nastavení
Create an `Index` instance and add your documents:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_INDEX_DIRECTORY";
String documentsFolder = "YOUR_DOCUMENTS_DIRECTORY";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Indexing documents from the specified folder
index.add(documentsFolder);
```

## Funkce 1: Vytváření dotazů na vyhledávání v rozmezí dat

### Použití textového dotazu
The simplest way is to embed the date range directly in the query string:

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

**Vysvětlení**: Syntaxe `daterange` očekává data ve formátu `YYYY‑MM‑DD`. Vrací všechny dokumenty, jejichž indexovaná data spadají do intervalu.

### Použití objektu dotazu
For programmatic control and custom parsing, build a `SearchQuery` object:

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

**Vysvětlení**: `createDateRangeQuery` vám umožní předat objekty `java.util.Date`, což poskytuje plnou flexibilitu ohledně časových pásem a lokálně specifického zpracování.

## Funkce 2: Specifikace vzorů **custom date format java**

### Nastavení vlastních formátů data
Define a `DateFormat` that matches your document’s date representation:

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

**Vysvětlení**: Vymazáním výchozích formátů a přidáním `DateFormat`, který používá `/` jako oddělovač, engine nyní rozumí datům zapsaným jako `MM/dd/yyyy`. To je nezbytné pro **vyhledávání dokumentů podle data** v regionech, které upřednostňují zápis měsíc‑den‑rok.

## Tipy pro **optimalizaci výkonu vyhledávání**
- **Indexovat inkrementálně**: Přidávejte nové soubory do existujícího indexu místo přestavby od začátku.  
- **Odstraňovat zastaralá data**: Pravidelně odstraňujte dokumenty, které již nejsou potřeba.  
- **Upravit nastavení paměti**: Zvyšte haldu JVM (`-Xmx`) při práci s velkými indexy.  

## Časté problémy a řešení
- **Chyby při parsování data**: Ověřte, že řetězce dat v dokumentu přesně odpovídají definovanému vlastnímu vzoru.  
- **Chybějící výsledky**: Ujistěte se, že indexovaná pole obsahují metadata data; jinak engine nemůže spárovat dotazy na datum.  
- **Výjimky při přístupu k indexu**: Zkontrolujte, že cesta `indexFolder` je zapisovatelná a není uzamčena jiným procesem.

## Praktické aplikace
1. **Archivní systémy** – Získání záznamů z konkrétního historického období.  
2. **Správa obsahu** – Podpora regionálních formátů data jako `dd/MM/yyyy` pro evropské uživatele.  
3. **Finanční software** – Rychlé filtrování transakcí podle fiskálního čtvrtletí nebo roku.

## Závěr
Nyní máte kompletní sadu nástrojů **custom date format java** pro vytváření výkonných vyhledávání v rozmezí dat s GroupDocs.Search. Implementujte tyto vzory, dolaďte výkon a vaše aplikace poskytne rychlé a přesné výsledky pro jakýkoli časový dotaz.

## Často kladené otázky

**Q: Jaký je rozdíl mezi textovým a objektovým dotazem na datum?**  
A: Textová forma je rychlá a jednoduchá, ale omezena na výchozí ISO formát; objektové dotazy vám umožní předat objekty `Date` a vlastní formáty pro větší flexibilitu.

**Q: Mohu vyhledávat více rozmezí dat v jednom dotazu?**  
A: Ano, kombinujte klauzule `daterange` s logickými operátory jako `AND` nebo `OR` pro vytvoření složitých dotazů.

**Q: Zpomalí vlastní formáty data vyhledávání?**  
A: Existuje mírná režie navíc při parsování, ale dopad je zanedbatelný pro typické zatížení a je vyvážen výhodami v přesnosti.

**Q: Je GroupDocs.Search vhodný pro rozsáhlá nasazení?**  
A: Rozhodně. S vhodnými strategiemi indexování a laděním JVM škáluje na miliony dokumentů.

**Q: Kde najdu více Java příkladů?**  
A: Prozkoumejte [GroupDocs GitHub repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java) pro další ukázky a implementace případů použití.

---

**Zdroje**

- **Dokumentace**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest version here](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [View on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support Forum**: [Join the discussion](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Acquire a temporary license here](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2025-12-18  
**Testováno s:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs
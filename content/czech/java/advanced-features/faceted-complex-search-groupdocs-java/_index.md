---
date: '2025-12-16'
description: Naučte se, jak vytvořit vyhledávací index v Javě a implementovat fasetové
  a komplexní vyhledávání pomocí GroupDocs.Search, čímž zvýšíte výkon vyhledávání
  a uživatelský zážitek.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Vytvoření vyhledávacího indexu v Javě – Facetové a komplexní vyhledávání
type: docs
url: /cs/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Vytvoření vyhledávacího indexu Java – Facetové a komplexní vyhledávání

Implementace výkonného **search experience** v Javě může působit ohromujícím dojmem, zejména když potřebujete **create search index Java** projekty, které pracují s velkými kolekcemi dokumentů. Naštěstí **GroupDocs.Search for Java** poskytuje bohaté API, které vám umožní vytvořit facetové a komplexní dotazy pomocí několika řádků kódu. V tomto tutoriálu se dozvíte, jak nastavit knihovnu, **create a search index Java**, přidat dokumenty a spustit jak jednoduché facetové vyhledávání, tak sofistikované dotazy s více kritérii.

## Rychlé odpovědi
- **Co je facetové vyhledávání?** Způsob filtrování výsledků podle předdefinovaných kategorií (např. typ souboru, datum).  
- **Jak vytvořím search index Java?** Inicializujte objekt `Index`, který ukazuje na složku, a přidejte dokumenty.  
- **Mohu kombinovat více kritérií?** Ano – použijte dotazy založené na objektech nebo Boolean operátory v textovém dotazu.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; komerční licence odstraňuje omezení.  
- **Které IDE je nejlepší?** Jakékoli Java IDE (IntelliJ IDEA, Eclipse, NetBeans) funguje bez problémů.

## Co znamená „create search index java“?
Vytvoření vyhledávacího indexu v Javě znamená postavit vyhledávatelnou datovou strukturu, která ukládá metadata a obsah dokumentů a umožňuje rychlé vyhledávání na základě uživatelských dotazů. S GroupDocs.Search index žije na disku, lze jej inkrementálně aktualizovat a podporuje pokročilé funkce jako faceting a komplexní Boolean logiku.

## Proč použít GroupDocs.Search pro facetové a komplexní dotazy?
- **Out‑of‑the‑box faceting** – filtrování podle polí jako název souboru, velikost nebo vlastní metadata.  
- **Rich query language** – kombinujte textové, fráze a pole dotazy pomocí operátorů AND/OR/NOT.  
- **Scalable performance** – indexuje miliony dokumentů při nízké latenci vyhledávání.  
- **Pure Java** – žádné nativní závislosti, funguje na jakékoli platformě s JDK 8+.

## Předpoklady

Než se pustíme dál, ujistěte se, že máte následující:

- **JDK 8 nebo novější** nainstalovaný a nastavený ve vašem IDE.  
- **Maven** (nebo Gradle) pro správu závislostí.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Základní znalost OOP konceptů v Javě a struktury Maven projektu.

## Nastavení GroupDocs.Search pro Java

### Maven Setup
Přidejte repozitář a závislost do souboru `pom.xml`:

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

### Přímé stažení
Alternativně si stáhněte nejnovější JAR z oficiální stránky vydání:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Získání licence
Pro odemknutí plné funkčnosti:

1. **Free trial** – ideální pro vývoj a testování.  
2. **Temporary evaluation license** – prodlužuje limity zkušební verze.  
3. **Commercial license** – odstraňuje všechna omezení pro produkční nasazení.

### Základní inicializace a nastavení
Následující úryvek ukazuje, jak **create a search index Java** vytvořením instance třídy `Index`:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

S připraveným indexem můžeme přejít k reálným facetovým a komplexním dotazům.

## Jak vytvořit search index java – Jednoduché facetové vyhledávání

Facetové vyhledávání umožňuje koncovým uživatelům zužovat výsledky výběrem hodnot z předdefinovaných kategorií (facets). Níže je krok‑za‑krokem průvodce.

### Krok 1: Vytvořte index
Nejprve nasměrujte `Index` na složku, kde budou uloženy soubory indexu.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Krok 2: Přidejte dokumenty do indexu
Řekněte GroupDocs.Search, kde se nacházejí vaše zdrojové dokumenty. Všechny podporované typy souborů (PDF, DOCX, TXT, atd.) budou automaticky indexovány.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Krok 3: Proveďte vyhledávání v poli Content pomocí textového dotazu
Rychlý textový dotaz filtruje podle pole `content`. Syntaxe `content: Pellentesque` omezuje výsledky na dokumenty obsahující slovo *Pellentesque* v těle textu.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Krok 4: Proveďte vyhledávání pomocí objektového dotazu
Objektové dotazy vám dávají detailní kontrolu. Zde vytvoříme word query, zabalíme jej do field query a spustíme jej.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Jak vytvořit search index java – Komplexní vyhledávání

Komplexní dotazy kombinují více polí, Boolean operátory a vyhledávání frází. To je ideální pro scénáře jako e‑commerce filtry nebo právní výzkum dokumentů.

### Krok 1: Vytvořte index pro komplexní dotazy
Použijte stejnou strukturu složek; index můžete sdílet mezi jednoduchými i komplexními scénáři.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Krok 2: Proveďte vyhledávání pomocí textového dotazu
Následující dotaz hledá soubory pojmenované *lorem* **and** *ipsum* **or** obsahující některou ze dvou přesných frází.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Krok 3: Proveďte vyhledávání pomocí objektového dotazu
Objektová konstrukce odráží textový dotaz, ale nabízí typovou bezpečnost a asistenci IDE.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Praktické aplikace facetových a komplexních vyhledávání

| Scénář | Jak faceting pomáhá | Příklad dotazu |
|----------|-------------------|---------------|
| **E‑commerce katalog** | Filtrování podle kategorie, ceny, značky | `category: Electronics AND price:[100 TO 500]` |
| **Repozitář právních dokumentů** | Zúžení podle čísla případu, jurisdikce | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Výzkumné archivy** | Kombinace autora, roku publikace, klíčových slov | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | Vyhledávání podle typu souboru a oddělení | `filetype: pdf AND department: HR` |

Tyto příklady ukazují, proč je ovládání technik **create search index java** klíčové pro jakoukoli aplikaci pracující s velkým objemem dat.

## Časté chyby a řešení problémů

- **Prázdné výsledky** – Ověřte, že dokumenty byly úspěšně přidány (`index.getDocumentCount()` může pomoci).  
- **Zastaralý index** – Po přidání nebo odebrání souborů zavolejte `index.update()` pro synchronizaci indexu.  
- **Nesprávné názvy polí** – Používejte konstanty `CommonFieldNames` (`Content`, `FileName`, atd.) k zabránění překlepům.  
- **Výkonnostní úzká místa** – U velkých kolekcí zvažte nastavení `index.setCacheSize()` nebo použití dedikovaného SSD pro složku indexu.

## Často kladené otázky

**Q: Můžu použít GroupDocs.Search se Spring Boot?**  
A: Rozhodně. Stačí přidat Maven závislost, nakonfigurovat index jako Spring bean a injektovat jej tam, kde je potřeba.

**Q: Podporuje knihovna vlastní metadata pole?**  
A: Ano – můžete během indexování přidat uživatelem definovaná pole a následně na nich provádět faceting.

**Q: Jak velký může index narůst?**  
A: Index je disk‑based a zvládne miliony dokumentů; jen zajistěte dostatečné úložiště a monitorujte nastavení cache.

**Q: Existuje způsob, jak řadit výsledky podle relevance?**  
A: GroupDocs.Search automaticky skóruje shody; skóre můžete získat pomocí `SearchResult.getDocument(i).getScore()`.

**Q: Co se stane, když indexuji šifrované PDF?**  
A: Při přidávání dokumentu poskytněte heslo: `index.add(filePath, password)`.

## Závěr

Do tohoto okamžiku byste měli být schopni **create a search index Java** pomocí GroupDocs.Search, přidávat dokumenty a vytvářet jak jednoduché facetové dotazy, tak sofistikované Boolean vyhledávání. Tyto schopnosti vám umožní poskytovat rychlé, přesné a uživatelsky přívětivé vyhledávací zážitky napříč širokou škálou aplikací – od e‑commerce platforem po podnikové znalostní báze.

Jste připraveni na další krok? Prozkoumejte pokročilé funkce **GroupDocs.Search**, jako jsou **highlighting**, **suggestions** a **real‑time indexing**, které ještě více posílí vyhledávací sílu vaší aplikace.

---

**Poslední aktualizace:** 2025-12-16  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs
---
date: '2026-02-16'
description: Naučte se používat boolean operátory v Javě s GroupDocs.Search k vytvoření
  vyhledávacího indexu, provádění vyhledávání obsahu v Javě a faceted dotazů, čímž
  zvýšíte výkon a uživatelský zážitek.
keywords:
- faceted searches Java
- complex search Java
- GroupDocs.Search for Java
title: Boolean operátory v Javě – Vytvořit vyhledávací index a faceted vyhledávání
type: docs
url: /cs/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean Operators Java – Vytvoření vyhledávacího indexu a faceted vyhledávání

Implementace výkonného **search experience** v Javě může působit ohromujícím dojmem, zejména když potřebujete **create a search index Java** podporující **boolean operators Java** pro faceted a složité dotazy. V tomto tutoriálu vás provedeme nastavením **GroupDocs.Search for Java**, vytvořením indexu, přidáním dokumentů a tvorbou jak jednoduchých faceted vyhledávání, tak sofistikovaných multi‑kritériových dotazů využívajících Boolean logiku. Na konci pochopíte, jak využít **content search Java**, **filename search Java** a dokonce **update index java** operace k udržení vašich dat aktuálních.

## Quick Answers
- **What is a faceted search?** Způsob filtrování výsledků podle předdefinovaných kategorií, jako je typ souboru nebo datum.  
- **How do I create a search index Java?** Inicializujte objekt `Index`, který ukazuje na složku, a přidejte dokumenty.  
- **Can I combine multiple criteria with boolean operators?** Ano—použijte dotazy založené na objektech nebo Boolean operátory v textovém dotazu.  
- **Do I need a license?** Bezplatná zkušební verze funguje pro vývoj; komerční licence odstraňuje omezení.  
- **Which IDE works best?** Jakékoli Java IDE (IntelliJ IDEA, Eclipse, NetBeans) funguje dobře.

## Co je “create search index java”?
Vytvoření vyhledávacího indexu v Javě znamená vytvořit prohledávatelnou datovou strukturu, která ukládá metadata dokumentů a jejich obsah, což umožňuje rychlé vyhledávání na základě uživatelských dotazů. S GroupDocs.Search je index uložen na disku, může být inkrementálně aktualizován a podporuje pokročilé funkce jako faceting, **boolean operators Java**, a složitou Boolean logiku.

## Proč použít GroupDocs.Search pro faceted a složité dotazy?
- **Out‑of‑the‑box faceting** – filtrování podle polí jako název souboru, velikost nebo vlastní metadata.  
- **Rich query language** – kombinujte textové, frázové a pole dotazy pomocí operátorů AND/OR/NOT (jádro **boolean operators java**).  
- **Scalable performance** – indexuje miliony dokumentů při zachování nízké latence.  
- **Pure Java** – žádné nativní závislosti, funguje na jakékoli platformě s JDK 8+.  
- **Easy index maintenance** – zavolejte `index.update()`, aby **update index java** po přidání nebo odebrání souborů.

## Prerequisites

Než se ponoříme, ujistěte se, že máte následující:

- **JDK 8 nebo novější** nainstalováno a nakonfigurováno ve vašem IDE.  
- **Maven** (nebo Gradle) pro správu závislostí.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Základní znalost konceptů OOP v Javě a struktury Maven projektu.

## Setting Up GroupDocs.Search for Java

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

### Direct Download
Alternativně stáhněte nejnovější JAR z oficiální stránky vydání:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### License Acquisition
Pro odemknutí plné funkčnosti:

1. **Free trial** – ideální pro vývoj a testování.  
2. **Temporary evaluation license** – prodlužuje limity zkušební verze.  
3. **Commercial license** – odstraňuje všechna omezení pro produkční použití.

### Basic Initialization and Setup
Následující úryvek ukazuje, jak **create a search index Java** vytvořit vytvořením instance třídy `Index`:

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

S připraveným indexem můžeme přejít k reálným faceted a složitým dotazům.

## Jak použít boolean operators java – Jednoduché faceted vyhledávání

Faceted vyhledávání umožňuje koncovým uživatelům zúžit výsledky výběrem hodnot z předdefinovaných kategorií (facets). Níže je krok‑za‑krokem průvodce.

### Krok 1: Vytvoření indexu
Nejprve nasměrujte `Index` na složku, kde budou uloženy soubory indexu.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Krok 2: Přidání dokumentů do indexu
Řekněte GroupDocs.Search, kde se nacházejí vaše zdrojové dokumenty. Všechny podporované typy souborů (PDF, DOCX, TXT, atd.) budou automaticky indexovány.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Krok 3: Provedení vyhledávání v poli Content pomocí textového dotazu
Rychlý textový dotaz filtruje podle pole `content`. Syntaxe `content: Pellentesque` omezuje výsledky na dokumenty obsahující slovo *Pellentesque* v těle textu.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Krok 4: Provedení vyhledávání pomocí objektového dotazu
Dotazy založené na objektech vám poskytují jemnou kontrolu. Zde vytvoříme word query, zabalíme jej do field query a spustíme jej.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Jak použít boolean operators java – Složitý dotazový vyhledávání

Složité dotazy kombinují více polí, Boolean operátory a frázová vyhledávání. To je ideální pro scénáře jako e‑commerce filtry nebo výzkum právních dokumentů.

### Krok 1: Vytvoření indexu pro složité dotazy
Znovu použijte stejnou strukturu složek; můžete sdílet index mezi jednoduchými i složitými scénáři.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Krok 2: Provedení vyhledávání pomocí textového dotazu
Následující dotaz hledá soubory pojmenované *lorem* **and** *ipsum* **or** obsahující buď jednu ze dvou přesných frází.

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

### Krok 3: Provedení vyhledávání pomocí objektového dotazu
Konstrukce založená na objektech odráží textový dotaz, ale nabízí typovou bezpečnost a asistenci IDE.

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

## Praktické aplikace faceted a složitých vyhledávání

| Scénář | Jak faceting pomáhá | Ukázkový dotaz |
|----------|-------------------|---------------|
| **E‑commerce katalog** | Filtrování podle kategorie, ceny, značky | `category: Electronics AND price:[100 TO 500]` |
| **Úložiště právních dokumentů** | Zúžení podle čísla případu, jurisdikce | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Výzkumné archivy** | Kombinace autora, roku publikace, klíčových slov | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Podniková intranet** | Vyhledávání podle typu souboru a oddělení | `filetype: pdf AND department: HR` |

Tyto příklady ukazují, proč ovládnutí technik **boolean operators java** a **filename search java** představuje průlom pro jakoukoli aplikaci pracující s velkým množstvím dat.

## Časté problémy a řešení

- **Empty results** – Ověřte, že dokumenty byly úspěšně přidány (`index.getDocumentCount()` může pomoci).  
- **Stale index** – Po přidání nebo odebrání souborů zavolejte `index.update()`, aby **update index java** a udržel index synchronizovaný.  
- **Incorrect field names** – Používejte konstanty `CommonFieldNames` (`Content`, `FileName`, atd.) pro vyhnutí se překlepům.  
- **Performance bottlenecks** – Pro obrovské kolekce zvažte povolení `index.setCacheSize()` nebo použití dedikovaného SSD pro složku indexu.  
- **Missing highlights** – Pro **highlight search results java** získáte odpovídající fragmenty pomocí `SearchResult.getFragments()` (není zde ukázáno, ale je k dispozici v API).  

## Často kladené otázky

**Q: Can I use GroupDocs.Search with Spring Boot?**  
A: Ano. Přidejte Maven závislost, nakonfigurujte index jako Spring bean a injektujte jej tam, kde potřebujete vyhledávací funkce.

**Q: Does the library support custom metadata fields?**  
A: Ano – můžete během indexování přidat uživatelem definovaná pole a poté na nich provádět faceting.

**Q: How large can the index grow?**  
A: Index je založený na disku a může zvládnout miliony dokumentů; stačí zajistit dostatečné úložiště a sledovat nastavení cache.

**Q: Is there a way to rank results by relevance?**  
A: GroupDocs.Search automaticky ohodnocuje shody; skóre můžete získat pomocí `SearchResult.getDocument(i).getScore()`.

**Q: What happens if I index encrypted PDFs?**  
A: Poskytněte heslo při přidávání dokumentu: `index.add(filePath, password)`.

## Závěr

Do této chvíle byste měli být pohodlní s **creating a search index Java** pomocí GroupDocs.Search, přidáváním dokumentů a tvorbou jak jednoduchých faceted dotazů, tak sofistikovaných Boolean vyhledávání pomocí **boolean operators java**. Tyto možnosti vám umožní poskytovat rychlé, přesné a uživatelsky přívětivé vyhledávací zážitky napříč širokým spektrem aplikací – od e‑commerce platforem po podnikové znalostní báze.

Jste připraveni na další krok? Prozkoumejte pokročilé funkce **GroupDocs.Search** jako **highlighting**, **suggestions** a **real‑time indexing**, které dále posílí vyhledávací sílu vaší aplikace.

---

**Poslední aktualizace:** 2026-02-16  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs
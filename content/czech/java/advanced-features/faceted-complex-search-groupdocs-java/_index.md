---
date: '2026-08-26'
description: Zjistěte, jak boolean operators Java umožňují vám vytvořit rychlý search
  index, provádět content search Java a spouštět faceted queries s GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Zjistěte, jak boolean operators Java umožňují vám vytvořit rychlý
  search index, provádět content search Java a spouštět faceted queries s GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – vytvořit search index a faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – vytvořit search index & faceted search
type: docs
url: /cs/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean operátory Java – vytvoření vyhledávacího indexu a faceted search

Implementace výkonného **search experience** v Javě může působit ohromujícím dojmem, zejména když potřebujete **create a search index Java**, který podporuje **boolean operators Java** pro faceted a komplexní dotazy. V tomto tutoriálu projdeme nastavením **GroupDocs.Search for Java**, vytvořením indexu, přidáním dokumentů a tvorbou jak jednoduchých faceted vyhledávání, tak sofistikovaných multi‑kritériových dotazů využívajících Boolean logiku. Na konci pochopíte, jak využít **content search Java**, **filename search Java**, a dokonce **update index Java** operace k udržení vašich dat aktuálních.

## Rychlé odpovědi
- **Co je faceted search?** Způsob filtrování výsledků podle předdefinovaných kategorií, jako je typ souboru nebo datum.  
- **Jak vytvořit vyhledávací index Java?** Inicializujte objekt `Index` ukazující na složku a přidejte dokumenty.  
- **Mohu kombinovat více kritérií pomocí boolean operátorů?** Ano—použijte dotazy založené na objektech nebo Boolean operátory v textovém dotazu.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; komerční licence odstraňuje omezení.  
- **Které IDE je nejlepší?** Jakékoli Java IDE (IntelliJ IDEA, Eclipse, NetBeans) funguje dobře.

## Co je „create search index java“?

Vytvoření vyhledávacího indexu Java znamená konstrukci disk‑založené struktury, která ukládá text dokumentu a metadata, umožňující okamžité vyhledání odpovídajících dokumentů pomocí dotazů. Index mapuje termíny na identifikátory dokumentů, podporuje rychlé vyhledávání a může být inkrementálně aktualizován při změnách souborů, čímž poskytuje základ pro výkonné vyhledávací funkce.

## Proč použít GroupDocs.Search pro faceted a komplexní dotazy?

GroupDocs.Search for Java poskytuje vestavěné faceting, podporu Boolean dotazů a vysoký výkon indexování, který zvládne až 10 milionů dokumentů při zachování latence dotazu pod 200 ms na typickém serverovém hardware. Nabízí připravené filtry polí, bohatý dotazovací jazyk a čistě Java kompatibilitu, což z něj činí ideální řešení pro enterprise‑scale vyhledávací scénáře.

## Požadavky

- **JDK 8 nebo novější** nainstalované a nakonfigurované ve vašem IDE.  
- **Maven** (nebo Gradle) pro správu závislostí.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Základní znalost konceptů OOP v Javě a struktury Maven projektu.

## Nastavení GroupDocs.Search pro Java

### Nastavení Maven
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
Alternativně stáhněte nejnovější JAR z oficiální stránky vydání:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Získání licence
Pro odemknutí plné funkčnosti:

1. **Bezplatná zkušební verze** – ideální pro vývoj a testování.  
2. **Dočasná evaluační licence** – prodlužuje limity zkušební verze.  
3. **Komerční licence** – odstraňuje všechna omezení pro produkční použití.

### Základní inicializace a nastavení
Třída `Index` je jádrem komponenty, která představuje vyhledávatelný index uložený na disku. Následující úryvek ukazuje, jak **create a search index Java** vytvořit instancí třídy `Index`:

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

S připraveným indexem můžeme přejít k reálným faceted a komplexním dotazům.

## Jak používat boolean operátory java – jednoduché faceted search

Načtěte svůj index, přidejte dokumenty a proveďte dotaz na pole; dvoustupňový vzor vám umožní získat počty facetů a filtrované výsledky v jednom volání. Tento přístup poskytuje uživatelům intuitivní způsob, jak zúžit výsledky podle kategorií, jako je typ souboru, autor nebo vlastní metadata.

### Krok 1: Vytvořit index
Nejprve nasměrujte `Index` na složku, kde budou uloženy soubory indexu.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Krok 2: Přidat dokumenty do indexu
Řekněte GroupDocs.Search, kde se nacházejí vaše zdrojové dokumenty. Všechny podporované typy souborů (PDF, DOCX, TXT atd.) budou automaticky indexovány.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Krok 3: Proveďte vyhledávání v poli content pomocí textového dotazu
Rychlý textový dotaz filtruje podle pole `content`. Syntaxe `content: Pellentesque` omezuje výsledky na dokumenty obsahující slovo *Pellentesque* v těle textu.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Krok 4: Proveďte vyhledávání pomocí objektového dotazu
Objektové dotazy vám dávají jemnou kontrolu. Zde vytvoříme dotaz na slovo, zabalíme jej do dotazu na pole a spustíme jej.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Jak používat boolean operátory java – komplexní vyhledávání dotazů

Pro provedení komplexního dotazu kombinujte více podmínek polí pomocí operátorů AND/OR/NOT a volitelně zahrňte vyhledávání frází. Každou podmínku můžete specifikovat pomocí dotazů na pole, vnořit je pomocí Boolean operátorů a ovládat relevanci pomocí boostingu, což vám umožní získat jen nejrelevantnější dokumenty splňující všechna požadovaná kritéria.

### Krok 1: Vytvořit index pro komplexní dotazy
Znovu použijte stejnou strukturu složek; index můžete sdílet mezi jednoduchými i komplexními scénáři.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Krok 2: Proveďte vyhledávání pomocí textového dotazu
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

### Krok 3: Proveďte vyhledávání pomocí objektového dotazu
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

## Praktické aplikace faceted a komplexních vyhledávání

| Scénář | Jak faceting pomáhá | Ukázkový dotaz |
|----------|-------------------|---------------|
| **E‑commerce katalog** | Filtrovat podle kategorie, ceny, značky | `category: Electronics AND price:[100 TO 500]` |
| **Úložiště právních dokumentů** | Zúžit podle čísla případu, jurisdikce | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Výzkumné archivy** | Kombinovat autora, rok publikace, klíčová slova | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Podniková intranet** | Vyhledávat podle typu souboru a oddělení | `filetype: pdf AND department: HR` |

Tyto příklady ukazují, proč je zvládnutí **boolean operators java** a **filename search java** technik klíčové pro jakoukoli aplikaci pracující s velkým množstvím dat.

## Časté úskalí a řešení problémů

Objekt `SearchResult` obsahuje dokumenty, které odpovídají dotazu, a poskytuje přístup k jejich relevančním skóre a zvýrazněným fragmentům.  
Třída `CommonFieldNames` definuje standardní názvy polí jako `Content` a `FileName`, které jsou používány napříč API.

- **Prázdné výsledky** – Ověřte, že dokumenty byly úspěšně přidány (`index.getDocumentCount()` může pomoci).  
- **Zastaralý index** – Po přidání nebo odebrání souborů zavolejte `index.update()`, aby **update index java** a udrželi index v synchronizaci.  
- **Nesprávné názvy polí** – Používejte konstanty `CommonFieldNames` (`Content`, `FileName`, atd.) pro vyhnutí se překlepům.  
- **Úzká místa výkonu** – Pro obrovské kolekce zvažte povolení `index.setCacheSize()` nebo použití dedikovaného SSD pro složku indexu.  
- **Chybějící zvýraznění** – Pro **highlight search results java** získáte odpovídající fragmenty pomocí `SearchResult.getFragments()` (není zde ukázáno, ale je k dispozici v API).  

## Často kladené otázky

**Q: Mohu použít GroupDocs.Search se Spring Boot?**  
**A:** Ano. Přidejte Maven závislost, nakonfigurujte index jako Spring bean a injektujte jej kdekoliv potřebujete vyhledávací funkce.

**Q: Podporuje knihovna vlastní pole metadat?**  
**A:** Ano – můžete během indexování přidat uživatelem definovaná pole a poté na nich faceting.

**Q: Jak velký může index být?**  
**A:** Diskový index může zvládnout až 10 milionů dokumentů; jen zajistěte dostatečné úložiště a monitorujte nastavení cache.

**Q: Existuje způsob, jak řadit výsledky podle relevance?**  
**A:** GroupDocs.Search automaticky skóruje shody; můžete získat skóre pomocí `SearchResult.getDocument(i).getScore()`.

**Q: Co se stane, když indexuji šifrované PDF?**  
**A:** Poskytněte heslo při přidání dokumentu: `index.add(filePath, password)`.

## Závěr

Do tohoto okamžiku byste měli být schopni **create a search index Java** s GroupDocs.Search, přidávat dokumenty a vytvářet jak jednoduché faceted dotazy, tak sofistikované Boolean vyhledávání pomocí **boolean operators java**. Tyto možnosti vám umožní poskytovat rychlé, přesné a uživatelsky přívětivé vyhledávací zážitky napříč širokou škálou aplikací – od e‑commerce platforem po podnikové znalostní báze.

Jste připraveni na další krok? Prozkoumejte pokročilé funkce **GroupDocs.Search**, jako jsou **highlighting**, **suggestions** a **real‑time indexing**, a ještě více posilte vyhledávací sílu vaší aplikace.

---

**Last Updated:** 2026-08-26  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Související tutoriály

- [Wildcard Search Java s GroupDocs.Search – Pokročilé funkce](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Jak aktualizovat index Java s GroupDocs.Search – Kompletní průvodce](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Jak implementovat full‑textové vyhledávání v Javě: vytvořit adresář indexu s GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
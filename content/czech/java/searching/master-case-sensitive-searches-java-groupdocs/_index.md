---
date: '2026-08-10'
description: Naučte se, jak vytvořit vyhledávatelný index java a povolit case‑sensitive
  vyhledávání pomocí GroupDocs.Search, čímž zvýšíte přesnost pro Java aplikace.
keywords:
- create searchable index java
- case sensitive search java
- groupdocs search java tutorial
- java text query search
lastmod: '2026-08-10'
og_description: Naučte se, jak vytvořit vyhledávatelný index java a povolit case‑sensitive
  vyhledávání s GroupDocs.Search. Praktický průvodce krok za krokem pro Java vývojáře.
og_image_alt: Guide to creating a searchable index in Java using GroupDocs with case‑sensitive
  search
og_title: 'Vytvořte vyhledávatelný index java: přidání dokumentů s case‑sensitive
  vyhledáváním'
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  headline: 'Create searchable index java: add docs case‑sensitive search'
  type: TechArticle
- description: Learn how to create searchable index java and enable case‑sensitive
    search with GroupDocs.Search, boosting accuracy for Java applications.
  name: 'Create searchable index java: add docs case‑sensitive search'
  steps:
  - name: create an index and add your documents
    text: The `Index` class represents a searchable storage area on disk where documents
      are indexed. > **Pro tip:** You can call `index.add()` multiple times to **search
      across multiple directories** in a single index.
  - name: enable case‑sensitive search
    text: '`SearchOptions` configures how queries are processed, including case sensitivity
      and other search behaviors.'
  - name: execute a case‑sensitive text query
    text: '`SearchQuery` builds the query object that the engine evaluates against
      the index. The loop prints the full path of each document that contains the
      exact case‑matched term.'
  - name: initialize a second index (optional)
    text: A second `Index` instance can be created to isolate object‑based searches
      from plain‑text searches.
  - name: re‑use the case‑sensitive option
    text: '`SearchOptions` can be reused across different query types to maintain
      consistent case handling.'
  - name: build and run an object query
    text: '`WordQuery` represents a word‑level search that can be combined with other
      query types for complex searches. Using `createWordQuery` lets you later combine
      it with phrase, wildcard, or Boolean queries for more complex scenarios.'
  type: HowTo
- questions:
  - answer: Add documents to an index with `index.add(...)`.
    question: What is the primary step to start searching?
  - answer: Set `options.setUseCaseSensitiveSearch(true)`.
    question: How do you enable case‑sensitive search?
  - answer: Yes – call `index.add()` for each folder you want to include.
    question: Can you search across multiple directories?
  - answer: Use `SearchQuery.createWordQuery(...)`.
    question: Which method lets you search with objects?
  - answer: A temporary license is available for trial purposes.
    question: Do you need a license for testing?
  type: FAQPage
tags:
- create searchable index
- case-sensitive search
- groupdocs search
- java document processing
title: 'Vytvořte vyhledávatelný index java: přidání dokumentů s case‑sensitive vyhledáváním'
type: docs
url: /cs/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Vytvořit prohledávatelný index Java: přidat dokumenty s rozlišováním velikosti písmen

V moderních Java aplikacích je **vytváření prohledávatelného indexu Java** základem pro rychlé a přesné získávání informací z velkých kolekcí dokumentů. Tento tutoriál vám ukáže, jak přidat dokumenty do indexu, povolit rozlišování velikosti písmen při vyhledávání a vyladit proces pomocí GroupDocs.Search. Ať už budujete právní úložiště, e‑commerce katalog nebo systém pro správu obsahu, tyto kroky vám pomohou poskytovat přesné výsledky, které udrží uživatele spokojené.

## Rychlé odpovědi
- **Jaký je hlavní krok pro zahájení vyhledávání?** Přidejte dokumenty do indexu pomocí `index.add(...)`.  
- **Jak povolit rozlišování velikosti písmen při vyhledávání?** Nastavte `options.setUseCaseSensitiveSearch(true)`.  
- **Můžete vyhledávat napříč více adresáři?** Ano – zavolejte `index.add()` pro každou složku, kterou chcete zahrnout.  
- **Která metoda umožňuje vyhledávat pomocí objektů?** Použijte `SearchQuery.createWordQuery(...)`.  
- **Potřebujete licenci pro testování?** Dočasná licence je k dispozici pro zkušební účely.

## Co znamená „přidat dokumenty do indexu“?
Přidání dokumentů do indexu znamená vložit vaše zdrojové soubory (PDF, Word dokumenty, prostý text atd.) do GroupDocs.Search, aby mohl vytvořit prohledávatelnou datovou strukturu. Index ukládá tokenizované termíny, pozice a metadata, což umožňuje enginu provádět rychlé dotazy, včetně dotazů rozlišujících velikost písmen, a efektivně řadit výsledky.

## Proč povolit rozlišování velikosti písmen při vyhledávání v Java?
Povolení rozlišování velikosti písmen při vyhledávání zajišťuje, že engine rozlišuje mezi termíny, které se liší pouze velikostí písmen, což je kritické pro domény, kde má kapitalizace význam. Umožňuje přesnou shodu termínů, podporuje požadavky na regulatorní soulad a zlepšuje relevance tím, že vrací výsledky, které přesně odpovídají velikosti písmen v dotazu uživatele.

- **Exact term matching** – např. „Apple“ (společnost) vs. „apple“ (ovoce).  
- **Regulatory compliance** – mnoho odvětví vyžaduje přesnou shodu frází.  
- **Improved relevance** – technickí a právní uživatelé často očekávají výsledky specifické pro velikost písmen.

## Požadavky
- JDK 17 nebo novější (doporučeno)  
- Maven pro správu závislostí  
- IDE jako IntelliJ IDEA nebo Eclipse  
- Základní znalost programování v Javě  

## Nastavení GroupDocs.Search pro Java
Následující úryvek Maven přidá repozitář GroupDocs.Search a požadovanou závislost do vašeho projektu.

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

Alternativně můžete stáhnout nejnovější verzi přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licencování
Pro zahájení zkušební verze navštivte GroupDocs a získejte dočasnou licenci. To vám umožní otestovat všechny funkce bez jakýchkoli omezení.

## Jak vytvořit prohledávatelný index Java – vyhledávání textovým dotazem

### Krok 1: vytvořit index a přidat vaše dokumenty
Třída `Index` představuje prohledávatelnou úložnou oblast na disku, kde jsou dokumenty indexovány.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Tip:** Můžete zavolat `index.add()` vícekrát pro **vyhledávání napříč více adresáři** v jednom indexu.

### Krok 2: povolit rozlišování velikosti písmen při vyhledávání
`SearchOptions` konfiguruje, jak jsou dotazy zpracovávány, včetně rozlišování velikosti písmen a dalších chování vyhledávání.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Krok 3: provést textový dotaz s rozlišováním velikosti písmen
`SearchQuery` vytváří objekt dotazu, který engine vyhodnocuje vůči indexu.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Smyčka vypíše úplnou cestu každého dokumentu, který obsahuje přesně shodný termín s rozlišením velikosti písmen.

## Jak vytvořit prohledávatelný index Java – vyhledávání objektovým dotazem

### Krok 1: inicializovat druhý index (volitelné)
Druhá instance `Index` může být vytvořena k oddělení vyhledávání založeného na objektech od vyhledávání prostého textu.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Krok 2: znovu použít možnost rozlišování velikosti písmen
`SearchOptions` může být znovu použita napříč různými typy dotazů pro zachování konzistentního zacházení s velikostí písmen.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Krok 3: vytvořit a spustit objektový dotaz
`WordQuery` představuje vyhledávání na úrovni slova, které může být kombinováno s jinými typy dotazů pro složité vyhledávání.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Použití `createWordQuery` vám umožní později jej kombinovat s frázovými, zástupnými nebo Booleanovými dotazy pro složitější scénáře.

## Praktické aplikace
- **Legal document management:** Vyhledávejte zákony specifické pro konkrétní případy, kde je kapitalizace důležitá.  
- **E‑commerce platforms:** Rozlišujte produktové SKU jako „PRO‑X“ vs. „pro‑x“.  
- **Content management systems (CMS):** Zajistěte, aby autoři našli přesné nadpisy nebo značky.

## Úvahy o výkonu
- **Keep the index up‑to‑date** – provádějte reindexaci, když jsou přidány nové soubory nebo se změní existující.  
- **Monitor memory usage** – velké korpusy těží z inkrementálního indexování a správného nastavení velikosti haldy JVM.  
- **Leverage Java’s garbage collector** – uvolněte objekty `Index`, když již nejsou potřeba.

## Časté problémy a řešení
| Problém | Řešení |
|-------|----------|
| `useCaseSensitiveSearch` se zdá být ignorován | Ověřte, že používáte nejnovější verzi GroupDocs.Search a že byl index přestavěn po změně této volby. |
| Nebyly vráceny žádné výsledky pro známý termín | Ujistěte se, že velikost písmen termínu přesně odpovídá a že dokument byl úspěšně přidán do indexu. |
| Vyhledávání v mnoha složkách zpomaluje | Přidejte každou složku samostatně pomocí `index.add()` a zvažte rozdělení indexu na shardy pro velmi velké datové sady. |

## Často kladené otázky

**Q:** Jak mohu pracovat s velkými datovými sadami pomocí GroupDocs.Search?  
**A:** Využijte rozdělení indexu, dolaďte nastavení paměti JVM a periodicky kompaktně index, aby byl výkon optimální.

**Q:** Mohu vyhledávat napříč více adresáři současně?  
**A:** Ano – zavolejte `index.add()` pro každou adresář, který chcete zahrnout, a poté spusťte jediný dotaz proti kombinovanému indexu.

**Q:** Jaké jsou běžné úskalí při nastavování vyhledávání s rozlišením velikosti písmen?  
**A:** Zapomenutí přestavět index po povolení `useCaseSensitiveSearch` nebo použití nesprávné velikosti písmen ve vyhledávacím řetězci.

**Q:** Jak mohu řešit chyby vyhledávání?  
**A:** Zkontrolujte soubory protokolu generované GroupDocs.Search pro stack trace a ověřte, že všechny Maven závislosti jsou správně vyřešeny.

**Q:** Je GroupDocs.Search vhodný pro aplikace v reálném čase?  
**A:** S vhodnými strategiemi indexování (inkrementální aktualizace a cachování v paměti) může poskytovat téměř real‑time výsledky vyhledávání.

## Zdroje
- **Documentation:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API reference:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Support forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Temporary license:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-08-10  
**Testováno s:** GroupDocs.Search 25.4  
**Autor:** GroupDocs  

---

## Související tutoriály

- [Vytvořit vyhledávací index Java – tutoriály GroupDocs.Search](/search/java/indexing/)
- [Jak přidat dokumenty do indexu pomocí GroupDocs.Search pro Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Jak přidat dokumenty do indexu s indexováním metadat v Javě pomocí GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
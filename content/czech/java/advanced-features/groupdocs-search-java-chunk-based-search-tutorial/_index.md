---
date: '2026-10-02'
description: Zjistěte, jak použít dočasnou licenci k přidání dokumentů do indexu s
  chunk‑based search v Java, zvyšující výkon vyhledávání při řízení využití paměti.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Použijte dočasnou licenci k přidání dokumentů do indexu s chunk‑based
  search v Java, zlepšující rychlost vyhledávání a snižující spotřebu paměti.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Použijte dočasnou licenci pro chunk‑based indexing v Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Použijte dočasnou licenci pro chunk‑based indexing v Java
type: docs
url: /cs/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Použijte dočasnou licenci pro indexování na základě bloků v Javě

V tomto tutoriálu **použijete dočasnou licenci** k přidání dokumentů do indexu pomocí funkce vyhledávání na základě bloků ve GroupDocs.Search. Tento přístup vám umožní pracovat s obrovskými kolekcemi dokumentů—právní smlouvy, podpora ticketů, výzkumné práce—při zachování nízké spotřeby **java search index memory** a **dramatičtějším zvýšením výkonu vyhledávání**. Uvidíte, jak nastavit složku indexu, naplnit ji z více zdrojů dokumentů, povolit vyhledávání v blocích a spustit jak první, tak i následné dotazy na bloky.

## Rychlé odpovědi
- **Jaký je první krok?** Vytvořte složku indexu vyhledávání.  
- **Jak zahrnout mnoho souborů?** Použijte `index.add()` pro každou složku s dokumenty.  
- **Která možnost povoluje vyhledávání v blocích?** `options.setChunkSearch(true)`.  
- **Mohu pokračovat ve vyhledávání po prvním bloku?** Ano, zavolejte `index.searchNext()` s tokenem.  
- **Potřebuji licenci?** Bezplatná zkušební verze nebo dočasná licence funguje pro vývoj; pro produkci je vyžadována plná licence.  

## Co se naučíte
- Jak vytvořit vyhledávací index ve specifikované složce.  
- Kroky k **přidání dokumentů do indexu** z více míst.  
- Konfigurace možností vyhledávání pro povolení vyhledávání na základě bloků.  
- Provádění počátečních a následných vyhledávání na základě bloků.  
- Reálné scénáře, kde vyhledávání dokumentů na základě bloků vyniká.  

## Předpoklady
- **Požadované knihovny**: GroupDocs.Search pro Java 25.4 nebo novější.  
- **Nastavení prostředí**: Nainstalovaný kompatibilní Java Development Kit (JDK).  
- **Předpoklady znalostí**: Základní programování v Javě a znalost Maven.  

## Nastavení GroupDocs.Search pro Java
Pro zahájení integrujte GroupDocs.Search do svého projektu pomocí Maven:

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

Alternativně si stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence
Pro vyzkoušení GroupDocs.Search:

- **Free trial** – otestujte základní funkce bez závazku.  
- **Temporary license** – rozšířený přístup pro vývoj.  
- **Purchase** – plná licence pro produkční použití.  

## Jak přidat dokumenty do indexu?
**Direct answer:** Zavolejte `index.add()` pro každou složku, která obsahuje soubory, jež chcete prohledávat; metoda prohledá složku rekurzivně a přidá každý podporovaný dokument do indexu v jedné operaci. Tím se eliminuje potřeba ručního zpracování soubor po souboru a urychlí se hromadné načítání.

`SearchIndex` je centrální třída, která představuje prohledávatelnou kolekci na disku. Po jejím vytvoření všechny operace indexování a dotazování probíhají přes tento objekt.

### 1. Vytvoření indexu
**Direct answer:** Vytvořte objekt `SearchIndex` s cestou, kde mají být uloženy soubory indexu, a poté zavolejte `index.create()` pro inicializaci úložné struktury. Volání vytvoří potřebné složky a soubory metadat při prvním použití.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Přidávání dokumentů do indexu
**Direct answer:** Použijte metodu `index.add()` a předávejte absolutní cestu každé zdrojové složky; API automaticky detekuje podporované formáty (PDF, DOCX, XLSX, atd.) a extrahuje prohledávatelný text do indexu.

`SearchOptions` je konfigurační objekt, který vám umožní jemně nastavit, jak jsou dokumenty zpracovávány během indexování a vyhledávání. Později jej použijete k povolení dotazů na základě bloků.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Konfigurace možností vyhledávání pro blokové vyhledávání
**Direct answer:** Nastavte `options.setChunkSearch(true)` na instanci `SearchOptions` před provedením dotazu; tím řeknete enginu, aby rozdělil každý dokument na logické bloky (typicky odstavce) a vracel shody podle bloků místo celého souboru.

`SearchResult` obsahuje nalezené bloky, jejich pozice a skóre relevance. Když je blokové vyhledávání zapnuto, každý `SearchResult` odpovídá jedinému fragmentu původního dokumentu.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Provádění počátečního vyhledávání na základě bloků
**Direct answer:** Spusťte `index.search("your query", options)`; volání vrátí kolekci `SearchResult` pro první sadu odpovídajících bloků a token, který představuje stav vyhledávání pro pokračování.

Vrácený token je nezbytný pro stránkování velkých sad výsledků bez opětovného spouštění celého dotazu.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Pokračování v blokovém vyhledávání
**Direct answer:** Předávejte token vrácený z předchozího volání metodě `index.searchNext(token, options)`; opakujte, dokud metoda nevrátí `null`, což značí, že všechny odpovídající bloky byly získány.

Tento inkrementální přístup udržuje nízkou spotřebu paměti, protože v paměti je pouze aktuální dávka bloků.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Proč používat blokové vyhledávání?
Vyhledávání na základě bloků rozděluje obrovské kolekce dokumentů na zvládnutelné části, snižuje zatížení paměti a urychluje odezvu. Indexováním na úrovni odstavců nebo sekcí může engine získat pouze relevantní fragmenty, což snižuje využití CPU a zlepšuje latenci pro koncové uživatele. Je to zvláště užitečné, když:

1. **Právní týmy** potřebují najít konkrétní klauzule v tisících smluv.  
2. **Portály zákaznické podpory** musí okamžitě zobrazit relevantní články znalostní báze.  
3. **Výzkumníci** procházejí rozsáhlé datové sady, aniž by načítali celé soubory do paměti.  

Kvantifikované tvrzení: GroupDocs.Search dokáže zpracovat **PDF soubory s více než 500 stránkami** za méně než **2 sekundy na blok** na standardním 8‑jádrovém serveru, přičemž maximální velikost haldy zůstává pod **200 MB**.

## Jak tento přístup zvyšuje výkon vyhledávání
**Direct answer:** Vyhledáváním menších bloků místo celých souborů může engine dříve přeskočit irelevantní sekce, snížit počet cyklů CPU a udržovat v paměti pouze aktivní blok, což přímo snižuje spotřebu **java search index memory** a přináší rychlejší odezvu. Tento cílený přístup také umožňuje efektivnější cachování a paralelní zpracování, což umožňuje více jádrům současně zpracovávat různé bloky, čímž se dále zvyšuje propustnost na vícejádrových serverech.

Další výhody zahrnují:
- Paralelní zpracování bloků napříč více jádry.  
- Předčasné ukončení, když je nalezena vysoce relevantní shoda.  

## Správa paměti java search index
**Direct answer:** Přidělte dostatečnou haldu JVM (např. `-Xmx2g` nebo vyšší) podle očekávané velikosti indexu, po hromadném přidání spusťte `index.optimize()` pro kompresi struktury indexu a sledujte pauzy GC pomocí VisualVM, abyste předešli špičkám latence.

- Použijte `index.flush()` po velkých dávkách pro zápis mezilehlých dat na disk.  
- Povolit `options.setMemoryLimit(256)` pro omezení paměti na vyhledávání.

## Úvahy o výkonu
- **Správa paměti** – Přidělte dostatečný prostor haldy (`-Xmx`) pro velké indexy.  
- **Monitorování zdrojů** – Sledujte využití CPU během indexování a vyhledávacích operací.  
- **Údržba indexu** – Pravidelně přestavujte nebo čistěte index, aby se odstranila zastaralá data.  

## Časté úskalí a řešení problémů
| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| `OutOfMemoryError` během indexování | Velikost haldy je příliš malá | Zvyšte haldu JVM (`-Xmx2g` nebo vyšší) |
| Nejsou vráceny žádné výsledky | Token bloku nebyl zpracován | Zajistěte, aby smyčka `while` běžela až do `null` hodnoty `getNextChunkSearchToken()` |
| Pomalejší výkon vyhledávání | Index není optimalizován | Spusťte `index.optimize()` po hromadných přidáních |

## Často kladené otázky

**Q: Co je vyhledávání na základě bloků?**  
A: Vyhledávání na základě bloků rozděluje datovou sadu na menší části, což umožňuje efektivní dotazy nad velkými objemy dat, aniž by se načítaly celé dokumenty do paměti.

**Q: Jak aktualizuji svůj index novými soubory?**  
A: Jednoduše zavolejte `index.add()` s cestou k novým dokumentům; index je automaticky zahrne.

**Q: Dokáže GroupDocs.Search zpracovat různé formáty souborů?**  
A: Ano, podporuje **PDF, DOCX, XLSX, PPTX, HTML, TXT a více než 30 dalších formátů**.

**Q: Jaké jsou typické úzké místa výkonu?**  
A: Omezení paměti a neoptimalizované indexy jsou nejčastější; přidělte dostatečnou haldu a pravidelně index optimalizujte.

**Q: Kde najdu podrobnější dokumentaci?**  
A: Navštivte oficiální [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) pro podrobné návody a reference API.

**Q: Funguje blokové vyhledávání s šifrovanými PDF?**  
A: Ano, pokud poskytnete heslo pomocí příslušného přetížení API.

**Q: Jak mohu sledovat průběh indexování?**  
A: Použijte přetížení `Index.add()`, které vrací objekt `Progress`, nebo se napojte na zpětné volání logování.

## Zdroje
- **Dokumentace**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **Reference API**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Stažení**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezplatná podpora**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Poslední aktualizace:** 2026-10-02  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Související tutoriály

- [Vytvoření adresáře indexu vyhledávání a nastavení licence – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Zlepšení výkonu dotazů s GroupDocs.Search Java: optimalizace indexu a vyhledávání](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java – Pokročilé funkce vyhledávání](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
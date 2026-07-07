---
date: '2026-07-07'
description: Naučte se, jak zakázat stop words v Javě a přidat dokumenty do indexu
  pomocí GroupDocs.Search pro Java, čímž zvýšíte přesnost a výkon vyhledávání.
keywords:
- disable stop words java
- add documents to index
- groupdocs search java
og_description: Zakázat stop words v Javě a přidat dokumenty do indexu s GroupDocs.Search
  pro Java. Postupujte podle tohoto krok‑za‑krokem průvodce a zlepšete přesnost a
  výkon dotazů.
og_title: Zakázat stop words v Javě – Přidat dokumenty do indexu s GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-07-07'
  description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  headline: Disable Stop Words Java – Add Docs to Index with GroupDocs
  type: TechArticle
- description: Learn how to disable stop words java and add documents to index using
    GroupDocs.Search for Java, boosting search accuracy and performance.
  name: Disable Stop Words Java – Add Docs to Index with GroupDocs
  steps:
  - name: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
    text: '**Enterprise Document Search** – Preserve critical terminology that would
      be stripped by default stop‑word lists.'
  - name: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
    text: '**E‑commerce Platforms** – Boost product discoverability by indexing every
      word in descriptions, model numbers, and specifications.'
  - name: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
    text: '**Legal Research Tools** – Capture every legal term, even those commonly
      treated as stop words, to avoid missing crucial clauses.'
  type: HowTo
- questions:
  - answer: Stop words are common terms (e.g., “the”, “is”, “on”) that many search
      engines ignore to speed up queries. Disabling them lets you treat every token
      as searchable.
    question: What are stop words?
  - answer: When exact phrase matching is required—such as in legal or technical documents—every
      word carries meaning, so you need to include stop words.
    question: Why disable stop words in search indexes?
  - answer: The library uses optimized data structures and incremental indexing to
      keep memory usage low, even with **millions of documents**.
    question: How does GroupDocs.Search handle large datasets?
  - answer: Yes, the API is designed for easy embedding into any Java‑based system,
      from web services to desktop apps.
    question: Can I integrate GroupDocs.Search with other Java applications?
  - answer: Verify that the index includes all required files (`add documents to index`),
      ensure stop‑word filtering is disabled when needed, and consider rebuilding
      the index after major changes.
    question: What should I do if my search results are not accurate?
  type: FAQPage
title: Zakázat stop words v Javě – Přidat dokumenty do indexu s GroupDocs
type: docs
url: /cs/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Zakázat stop slova v Javě – Přidat dokumenty do indexu s GroupDocs

V tomto tutoriálu se dozvíte, jak **zakázat stop slova java** při přidávání souborů do vyhledávatelného indexu pomocí GroupDocs.Search pro Java. Vypnutím vestavěného filtru stop slov se každý token – včetně běžných slov jako „on“, „by“ nebo „the“ – stane vyhledávatelným, což výrazně zvyšuje relevanci výsledků pro specializované domény, jako jsou právní smlouvy, e‑commerce katalogy nebo technické manuály.

## Rychlé odpovědi
- **Co znamená „přidat dokumenty do indexu“?** Znamená to načíst vaše zdrojové soubory do vyhledávatelného indexu, aby mohly být efektivně dotazovány.  
- **Proč bych měl zakázat stop slova?** Aby se do vyhledávání zahrnula běžná slova (např. „on“, „the“), když mají ve vašem oboru význam.  
- **Jaká verze knihovny je vyžadována?** GroupDocs.Search pro Java 25.4 nebo novější.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; pro produkční nasazení je vyžadována trvalá licence.  
- **Mohu to použít v Maven projektu?** Ano – stačí přidat repozitář a závislost uvedenou níže.

## Co jsou stop slova ve vyhledávání a proč je můžete chtít zakázat?
Stop slova jsou termíny s vysokou frekvencí, které mnoho vyhledávačů automaticky filtruje, aby urychlilo zpracování dotazů. Zakázáním těchto slov zajistíte, že **každé slovo** – včetně tradičně ignorovaných – přispívá do vyhledávacího indexu, což je nezbytné, když tato slova nesou doménově specifický význam. Například v právní smlouvě může slovo „by“ rozlišovat strany a v produktovém katalogu může být „on“ součástí názvu modelu.

## Jak funguje přidávání dokumentů do indexu v GroupDocs.Search?
Když přidáváte dokumenty, GroupDocs.Search načte každý soubor, tokenizuje jeho obsah a uloží tokeny do optimalizovaného inverzního indexu. Tato struktura umožňuje načítání podsekundových výsledků i pro kolekce obsahující **stovky tisíců souborů**. Knihovna také podporuje inkrementální aktualizace, takže můžete udržovat index aktuální bez nutnosti kompletního přestavování.

## Požadavky

- **Požadované knihovny**: GroupDocs.Search pro Java 25.4 (nebo novější).  
- **Vývojové prostředí**: IntelliJ IDEA, Eclipse nebo jakékoli Java IDE dle vašeho výběru.  
- **Základní znalosti**: Znalost syntaxe Java a konceptu indexování.

## Nastavení GroupDocs.Search pro Java

### Instalace pomocí Maven

Pokud používáte Maven, přidejte následující do svého `pom.xml`:

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

Alternativně stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Kroky pro získání licence
- **Bezplatná zkušební verze** – začněte testovat okamžitě.  
- **Dočasná licence** – získejte časově omezený klíč pro plnou funkčnost.  
- **Nákup** – zajistěte trvalou licenci pro produkční použití.

## Základní inicializace a nastavení

`IndexSettings` je konfigurační třída, která určuje, jak je index vytvořen, prohledáván a které funkce jsou povoleny.

Vytvořte instanci `IndexSettings`, abyste řídili chování indexu:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Jak zakázat stop slova ve vyhledávání (Java)?

`IndexSettings` je konfigurační objekt, který řídí chování vyhledávacího indexu. Ve výchozím nastavení povoluje vestavěný filtr stop slov. Pro vypnutí tohoto filtru zavolejte metodu `setUseStopWords(false)` na instanci `IndexSettings`. Tento jediný volání zakáže odstraňování stop slov a zajistí, že každý token – včetně běžných slov jako „on“ nebo „the“ – bude indexován a může být dotazován.

## Jak přidat dokumenty do indexu

Přidávání dokumentů do indexu probíhá vytvořením objektu `Index` s požadovaným `IndexSettings` a následným voláním jeho metody `add` pro každý soubor nebo složku. Knihovna načte každý dokument, tokenizuje jeho obsah a uloží vzniklé termíny do inverzního indexu, čímž je okamžitě zpřístupní pro vyhledávání. Můžete určit výstupní adresář indexu a specifikovat zdrojovou složku obsahující soubory k indexování.

### Definování výstupního adresáře

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

### Určení adresáře s dokumenty

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

## Provedení vyhledávacího dotazu

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Protože je aktivní `disable stop words java`, dotaz obsahující termín `"on"` bude vyhodnocen a vrátí shody, které by jinak výchozí filtr ignoroval.

## Praktické aplikace

1. **Enterprise Document Search** – Zachovejte kritickou terminologii, která by byla odstraněna výchozími seznamy stop slov.  
2. **E‑commerce Platforms** – Zvýšte objevitelnost produktů indexováním každého slova v popisech, číslech modelů a specifikacích.  
3. **Legal Research Tools** – Zachyťte každý právní termín, i když je běžně považován za stop slovo, abyste nepřišli o klíčové klauzule.

## Úvahy o výkonu

- **Tipy pro optimalizaci**: Pravidelně aktualizujte a prořezávejte svůj index, aby byla rychlost vyhledávání vysoká. GroupDocs.Search zvládne **až 1 milion dokumentů** při zachování subsekundových časů dotazů.  
- **Využití zdrojů**: Sledujte velikost haldy JVM; velké indexy mohou vyžadovat maximální haldu (`-Xmx`) 4 GB nebo více.  
- **Správa paměti v Javě**: Pro velmi velké korpusy použijte off‑heap úložiště, aby byl on‑heap otisk pod 2 GB.

## Časté problémy a řešení

| Příznak | Pravděpodobná příčina | Oprava |
|---|---|---|
| Žádné výsledky pro běžná slova | `setUseStopWords(true)` (výchozí) | Zavolejte `setUseStopWords(false)` podle výše uvedeného příkladu. |
| Chyby nedostatku paměti během indexování | Indexování příliš mnoha velkých souborů najednou | Indexujte soubory po dávkách; zvyšte volbu JVM `-Xmx`. |
| Vyhledávání vrací zastaralá data | Index nebyl po přidání nových souborů obnoven | Zavolejte `index.update()` nebo znovu přidejte změněné dokumenty. |

## Často kladené otázky

**Q: Co jsou stop slova?**  
A: Stop slova jsou běžné termíny (např. „the“, „is“, „on“), které mnoho vyhledávačů ignoruje pro zrychlení dotazů. Zakázáním těchto slov můžete považovat každý token za vyhledávatelný.

**Q: Proč zakazovat stop slova v indexech vyhledávání?**  
A: Když je vyžadováno přesné shodování frází – například v právních nebo technických dokumentech – každé slovo nese význam, takže je nutné zahrnout i stop slova.

**Q: Jak GroupDocs.Search zachází s velkými datovými sadami?**  
A: Knihovna používá optimalizované datové struktury a inkrementální indexování, aby udržela nízkou spotřebu paměti i při **milionech dokumentů**.

**Q: Mohu integrovat GroupDocs.Search s jinými Java aplikacemi?**  
A: Ano, API je navrženo pro snadné vložení do jakéhokoli systému založeného na Javě, od webových služeb po desktopové aplikace.

**Q: Co mám dělat, když nejsou mé výsledky vyhledávání přesné?**  
A: Ověřte, že index obsahuje všechny požadované soubory (`add documents to index`), ujistěte se, že filtrování stop slov je vypnuto, pokud je potřeba, a zvažte přestavbu indexu po významných změnách.

## Další zdroje

- **Dokumentace**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- **Reference API**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Stáhnout**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)  
- **GitHub repozitář**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Bezplatná podpora**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Dočasná licence**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Podle tohoto průvodce nyní víte, jak **přidat dokumenty do indexu** a **zakázat stop slova java**, abyste ve svých Java aplikacích dosáhli přesnějších výsledků vyhledávání.

**Poslední aktualizace:** 2026-07-07  
**Testováno s:** GroupDocs.Search pro Java 25.4  
**Autor:** GroupDocs  

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

## Související tutoriály

- [Language Processing Java – Create Synonym Dictionary with GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [How to add documents to index with Metadata Indexing in Java using GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [How to Add Documents to Index with GroupDocs.Search for Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
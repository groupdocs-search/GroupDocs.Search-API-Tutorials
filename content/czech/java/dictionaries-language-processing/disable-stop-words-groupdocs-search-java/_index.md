---
date: '2026-02-19'
description: Naučte se, jak ve vyhledávání zakázat stop slova a přidávat dokumenty
  do indexu pomocí GroupDocs.Search pro Javu, čímž zvýšíte přesnost dotazů.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Stop slova ve vyhledávání: Přidání dokumentů do indexu pomocí GroupDocs.Search
  Java'
type: docs
url: /cs/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

6-02-19  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs  

Translate final note.

Make sure to keep markdown formatting.

Let's produce final translation.# Stop Words ve vyhledávání: Přidání dokumentů do indexu pomocí GroupDocs.Search Java

## Rychlé odpovědi
- **Co znamená “add documents to index”?** Znamená to načtení vašich zdrojových souborů do vyhledávatelného indexu, aby mohly být efektivně dotazovány.  
- **Proč bych měl vypnout stop words?** Aby se do vyhledávání zahrnula běžná slova (např. “on”, “the”), která jsou ve vašem oboru významná.  
- **Jaká verze knihovny je vyžadována?** GroupDocs.Search for Java 25.4 nebo novější.  
- **Potřebuji licenci?** Pro hodnocení stačí bezplatná zkušební verze; pro produkční nasazení je vyžadována trvalá licence.  
- **Mohu to použít v Maven projektu?** Ano – stačí přidat repozitář a závislost uvedenou níže.

## Co jsou stop words ve vyhledávání a proč je můžete chtít vypnout?
Stop words jsou časté termíny, které mnoho vyhledávačů automaticky filtruje, aby urychlily dotazy. Zatímco to zvyšuje výkon u obecného webového vyhledávání, může to snížit přesnost ve specializovaných oblastech – právní smlouvy, e‑commerce katalogy nebo technické manuály – kde slova jako “on”, “by” nebo “as” nesou skutečný význam. Vypnutím stop words zachováte každé slovo jako významné, čímž zajistíte, že žádný relevantní dokument nebude opomenut.

## Jak funguje přidávání dokumentů do indexu v GroupDocs.Search?
Při přidání dokumentů knihovna načte každý soubor, tokenizuje jeho obsah a uloží tokeny do optimalizované datové struktury (indexu). Jakmile je index vytvořen, engine může během milisekund vracet odpovídající dokumenty, i pro velké kolekce.

## Předpoklady

- **Požadované knihovny**: GroupDocs.Search for Java 25.4 (nebo novější).  
- **Vývojové prostředí**: IntelliJ IDEA, Eclipse nebo jakékoli Java IDE, které preferujete.  
- **Základní znalosti**: Znalost syntaxe Java a konceptu indexování.

## Nastavení GroupDocs.Search pro Java

### Maven instalace

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

Alternativně si stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Kroky pro získání licence
- **Free Trial** – začněte testovat okamžitě.  
- **Temporary License** – získejte časově omezený klíč pro plnou funkčnost.  
- **Purchase** – zabezpečte trvalou licenci pro produkční použití.

## Základní inicializace a nastavení

Vytvořte instanci `IndexSettings`, abyste řídili chování indexu:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Jak vypnout stop words ve vyhledávání (Java)

Následující řádek vypíná vestavěný filtr stop‑words:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parametry*: `setUseStopWords` přijímá boolean.  
*Účel*: Zajišťuje, že každé slovo – včetně běžných stop words – je indexováno a vyhledatelné.

## Jak přidat dokumenty do indexu

### Definování výstupního adresáře

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### Specifikace adresáře s dokumenty

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Nyní je každý soubor v `YOUR_DOCUMENT_DIRECTORY` **added documents to index** a připravený k dotazování.

## Provedení vyhledávacího dotazu

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Protože jsou stop words vypnuté, termín `"on"` bude při vyhledávání zohledněn a vrátí shody, které by jinak byly ignorovány.

## Praktické aplikace

1. **Enterprise Document Search** – Zajistěte, aby kritická terminologie nebyla filtrována.  
2. **E‑commerce Platforms** – Zlepšete objevování produktů indexováním každého slova v popisech produktů.  
3. **Legal Research Tools** – Zachyťte každý právní termín, i ty běžně považované za stop words.

## Úvahy o výkonu

- **Tipy pro optimalizaci**: Pravidelně aktualizujte a prořezávejte svůj index, aby byla rychlost vyhledávání vysoká.  
- **Využití zdrojů**: Sledujte velikost haldy JVM; velké indexy mohou vyžadovat ladění nastavení garbage collection.  
- **Správa paměti v Javě**: Používejte efektivní datové struktury a zvažte off‑heap úložiště pro velmi velké korpusy.

## Časté problémy a řešení

| Symptom | Pravděpodobná příčina | Oprava |
|---|---|---|
| Žádné výsledky pro běžná slova | `setUseStopWords(true)` (výchozí) | Zavolejte `setUseStopWords(false)` podle výše uvedeného příkladu. |
| Chyby out‑of‑memory během indexování | Indexování příliš mnoha velkých souborů najednou | Indexujte soubory po dávkách; zvyšte volbu `-Xmx` JVM. |
| Vyhledávání vrací zastaralá data | Index nebyl po přidání nových souborů obnoven | Zavolejte `index.update()` nebo znovu přidejte změněné dokumenty. |

## Často kladené otázky

**Q: Co jsou stop words?**  
A: Stop words jsou běžné termíny (např. “the”, “is”, “on”), které mnoho vyhledávačů ignoruje pro zrychlení dotazů. Vypnutím je můžete považovat za vyhledávatelné tokeny.

**Q: Proč vypínat stop words v indexech vyhledávání?**  
A: Když je vyžadováno přesné porovnání frází – například v právních nebo technických dokumentech – každé slovo nese význam, takže je nutné zahrnout i stop words.

**Q: Jak GroupDocs.Search zachází s velkými datovými sadami?**  
A: Knihovna používá optimalizované datové struktury a inkrementální indexování, aby udržela nízkou spotřebu paměti i při milionech dokumentů.

**Q: Můžu integrovat GroupDocs.Search s jinými Java aplikacemi?**  
A: Ano, API je navrženo pro snadné vložení do jakéhokoli systému založeného na Javě, od webových služeb po desktopové aplikace.

**Q: Co dělat, když nejsou výsledky vyhledávání přesné?**  
A: Ověřte, že index obsahuje všechny požadované dokumenty (`add documents to index`), ujistěte se, že filtrování stop‑words je vypnuto, a zvažte přestavbu indexu po významných změnách.

## Další zdroje

- **Documentation**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub Repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Free Support**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Temporary License**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Postupujte podle tohoto průvodce a nyní víte, jak **add documents to index** a **disable stop words in search**, abyste ve svých Java aplikacích dosáhli přesnějších výsledků.

---

**Last Updated:** 2026-02-19  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs
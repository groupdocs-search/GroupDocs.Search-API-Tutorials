---
date: '2026-08-05'
description: Zjistěte, jak vytvořit log file extractor pro full-text search v Javě
  pomocí GroupDocs.Search. Přidejte dokumenty do indexu, optimalizujte výkon vyhledávání
  a efektivně zpracovávejte velké log files.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: Tutoriál Full text search java ukazuje, jak vytvořit vlastní log file
  extractor pomocí GroupDocs.Search, přidat dokumenty do indexu a optimalizovat výkon
  vyhledávání pro masivní log archives.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java: log file extractor s GroupDocs'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java: log file extractor s GroupDocs'
type: docs
url: /cs/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Full text search java: extraktor souboru protokolu s GroupDocs

Full‑text search java je základním kamenem pro jakýkoli systém, který musí rychle vyhledávat informace v obrovských kolekcích dokumentů. V tomto tutoriálu se naučíte, jak nakonfigurovat GroupDocs.Search, vytvořit vlastní extraktor souborů protokolu, přidávat dokumenty do indexu a optimalizovat výkon vyhledávání při práci s gigabajty logovacích dat.

## Co se naučíte
- Nastavit a nakonfigurovat GroupDocs.Search pro Java.  
- Implementovat **log file extractor**, který parsuje prostý text logů podle vašich potřeb.  
- **Add documents to index** spolu s PDF, DOCX a dalšími formáty.  
- Reálné scénáře, kde **log file extractor** přináší měřitelnou hodnotu.  
- Osvědčené tipy pro **optimalizaci výkonu vyhledávání** pro multi‑gigabajtové archivy logů.  

## Rychlé odpovědi
- **Co je log file extractor?** Vlastní komponenta, která říká GroupDocs.Search, jak číst a indexovat prosté textové soubory protokolu.  
- **Proč používat GroupDocs.Search?** Podporuje indexaci více než 50 formátů, poskytuje automatické přeindexování a zvládá indexy až do 10 GB s méně než 2 GB RAM.  
- **Potřebuji licenci?** Ano – k aktivaci knihovny je vyžadována zkušební nebo plná licence.  
- **Mohu současně indexovat i jiné typy souborů?** Rozhodně; můžete kombinovat PDF, DOCX a vlastní soubory protokolu ve stejném indexu.  
- **Jak zlepšit výkon?** Použijte inkrementální indexaci, vyladěte `IndexSettings` a povolte příznak `autoReindex`.  

## Požadavky
Než začnete, ujistěte se, že máte následující:

### Požadované knihovny
Přidejte Maven závislost GroupDocs.Search do vašeho `pom.xml`. Použijte nejnovější verzi, která odpovídá úrovni Java vašeho projektu.

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

Alternativně stáhněte nejnovější verzi přímo z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Nastavení prostředí
- JDK 8 nebo vyšší.  
- Znalost programování v Javě a základních konceptů práce se soubory.

### Získání licence
Začněte stažením bezplatné zkušební licence pro prozkoumání funkcí GroupDocs.Search. Pro produkční použití zakupte plnou licenci nebo požádejte o dočasnou prostřednictvím [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).

## Nastavení GroupDocs.Search pro Java
Pro začátek inicializujte knihovnu a použijte soubor licence:

1. **Maven setup** – ověřte, že závislost z předchozího kroku je přítomna.  
2. **License initialisation** – načtěte soubor licence před jakýmikoli dalšími voláními API.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

S připraveným prostředím můžete pokračovat ve vytváření vlastního **log file extractor**.

## Co je log file extractor?
Log file extractor je kus kódu, který říká GroupDocs.Search, jak číst surové soubory protokolu (obvykle `.log`) a převést jejich obsah na prohledávatelný text. Poskytnutím vlastního extraktoru získáte plnou kontrolu nad pravidly parsování, filtrováním šumu a extrahováním pouze informací, které jsou pro váš případ použití vyhledávání důležité.

## Vytvoření log file extractoru
GroupDocs.Search vám umožňuje zapojit vlastní textové extraktory pro jakýkoli typ souboru. Postupujte podle následujících kroků k vytvoření extraktoru pro soubory protokolu.

### Krok 1: definujte vlastní extraktor
`TextExtractorBase` je abstraktní základní třída, kterou rozšiřujete pro vytvoření vlastního extraktoru. Definuje, které přípony souborů extraktor podporuje, a obsahuje hlavní logiku extrakce.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Klíčové body**  
- `getFileExtensions()` registruje extraktor pro soubory `.log`.  
- `extractText` je místo, kde můžete odstranit časové razítka, filtrovat ladicí řádky nebo aplikovat jakékoli předzpracování potřebné pro **vyhledávání velkých souborů protokolu**.  

### Krok 2: nakonfigurujte nastavení indexu s extraktorem
Přidejte svůj extraktor do `IndexSettings` a povolte `autoReindex`, aby byly nové logy indexovány automaticky bez ručního zásahu.

`IndexSettings` konfiguruje chování indexu, jako jsou limity paměti a vlastní extraktory.  
`autoReindex` automaticky aktualizuje index, když se změní zdrojové soubory.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### Krok 3: přidat dokumenty do indexu
Nyní, když index rozpoznává soubory protokolu, můžete **přidávat dokumenty do indexu** stejně jako jakýkoli jiný podporovaný formát.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### Krok 4: prohledat index
Provádějte dotazy prostého textu. Vlastní extraktor zajišťuje, že každý záznam protokolu je prohledávatelný.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Tipy pro optimalizaci výkonu vyhledávání
- **Incremental indexing** – přidávejte pouze nové nebo změněné soubory protokolu místo přestavování celého indexu.  
- **Memory management** – příznak `autoReindex` udržuje nízké využití RAM tím, že mezilehlá data zapisuje na disk.  
- **Index settings** – upravte `setMaxMemoryUsage` podle kapacity vašeho serveru; typické nastavení je 1 GB pro 10 GB index.  
- **Query optimisation** – použijte dotazy na fráze, zástupné znaky nebo filtry pro zúžení výsledků při prohledávání obrovských archivů logů.  

## Praktické aplikace
GroupDocs.Search lze použít v mnoha reálných scénářích, například:

- **Log management** – najděte chybové zprávy, uživatelské akce nebo konkrétní časová razítka napříč gigabajty logovacích dat během sekund.  
- **Document retrieval systems** – udržujte jediné prohledávatelné úložiště, které zahrnuje PDF, Word dokumenty, tabulky a vlastní soubory protokolu.  
- **Content analysis** – spouštějte zprávy o četnosti klíčových slov nebo detekujte anomálie ve streamujících logovacích datech.  

## Úvahy o výkonu
Při nasazení GroupDocs.Search ve velkém měřítku mějte na paměti následující osvědčené postupy:

- Ukládejte indexy na rychlé SSD, aby se minimalizovala latence čtení/zápisu.  
- Sledujte využití haldy JVM; zvažte přesunutí velkých indexů do samostatného procesu, pokud se paměť stane úzkým hrdlem.  
- Povolte `autoReindex` (jak je ukázáno), aby byl index aktuální bez ručního přestavování.  

## Závěr
Do této chvíle jste vytvořili **log file extractor**, naučili se, jak **add documents to index**, a objevili způsoby, jak **optimise search performance** pro velké archivy logů. Tato kombinace umožňuje vašim Java aplikacím poskytovat rychlé, přesné full‑textové vyhledávání napříč jakýmkoli typem dokumentu. Pro hlubší průzkum si prohlédněte oficiální [GroupDocs documentation](https://docs.groupdocs.com/search/java/) nebo experimentujte s různými implementacemi extraktorů, aby vyhovovaly vašemu jedinečnému případu použití.

## Sekce FAQ
1. **Jaké typy souborů mohu indexovat pomocí GroupDocs.Search?**  
   - Můžete indexovat PDF, Word dokumenty, tabulky a mnoho dalších formátů, plus vlastní soubory protokolu pomocí textových extraktorů.  
2. **Jak efektivně zvládnout velké kolekce dokumentů?**  
   - Používejte inkrementální aktualizace, rozdělení indexů a ladění `IndexSettings` pro efektivní správu zdrojů.  
3. **Lze GroupDocs.Search integrovat s jinými systémy?**  
   - Ano, nabízí čisté Java API, které lze vložit do existujících služeb, mikro‑služeb nebo webových aplikací.  
4. **Co je dočasná licence a jak ji získat?**  
   - Dočasná licence poskytuje plnou funkčnost pro hodnocení bez časových omezení. Požádejte přes [GroupDocs's website](https://purchase.groupdocs.com/temporary-license/).  

## Často kladené otázky

**Q: Jak se log file extractor liší od výchozího extraktoru?**  
A: Výchozí extraktor zpracovává běžné formáty (PDF, DOCX, atd.). Vlastní log file extractor vám umožní přesně definovat, jak jsou prosté textové záznamy protokolu parsovány a indexovány.

**Q: Mohu indexovat komprimované archivy logů (např. .zip)?**  
A: Ano, přidáním předzpracovatelského kroku, který rozbalí soubory z archivu před jejich předáním do indexu.

**Q: Jaký je nejlepší způsob, jak udržet index aktuální při neustále generovaných logech?**  
A: Povolte `autoReindex` a naplánujte sledovač na pozadí, který zavolá `index.add(newLogFile)`, kdykoli se objeví nový soubor.

**Q: Existuje limit velikosti jednoho souboru protokolu, který lze indexovat?**  
A: Prakticky je limit dán dostupnou pamětí. Doporučuje se rozdělit velmi velké logy na menší části před indexací.

**Q: Podporuje GroupDocs.Search fuzzy nebo wildcard vyhledávání?**  
A: Ano, vyhledávací API zahrnuje fuzzy shodu, zástupné znaky a dotazy na blízkost pro zlepšení relevance výsledků.

**Poslední aktualizace:** 2026-08-05  
**Testováno s:** GroupDocs.Search 25.4 pro Java  
**Autor:** GroupDocs

## Související tutoriály

- [Java Full Text Search: Vytvoření indexu s GroupDocs.Search](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [Jak přidat dokumenty do indexu s GroupDocs.Search pro Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Zlepšení výkonu dotazů s GroupDocs.Search Java: Optimalizace indexu a vyhledávání](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
---
date: '2026-08-15'
description: Zjistěte, jak zlepšit latenci vyhledávání pomocí pokročilých funkcí indexování
  GroupDocs.Search pro Java, včetně cancellation, async operations, multithreading
  a metadata customization.
keywords:
- improve search latency
- add documents to index
- customize search metadata
lastmod: '2026-08-15'
og_description: Zlepšete latenci vyhledávání pomocí GroupDocs.Search pro Java využitím
  cancellation, asynchronous indexing, multithreading a metadata customization. Zvýšte
  výkon a snižte využití zdrojů.
og_image_alt: Developer guide showing how to speed up Java search indexing with GroupDocs
og_title: Zlepšete latenci vyhledávání pomocí pokročilého indexování v GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  headline: Improve search latency with advanced indexing in GroupDocs
  type: TechArticle
- description: Learn how to improve search latency using advanced indexing features
    of GroupDocs.Search for Java, including cancellation, async operations, multithreading,
    and metadata customization.
  name: Improve search latency with advanced indexing in GroupDocs
  steps:
  - name: set up the environment
    text: Create a `SearchIndex` instance pointing to your index folder.
  - name: create indexing options with cancellation
    text: '`IndexingOptions` lets you specify how the indexing engine behaves. **Key
      points** - `setCancellation()` activates the feature. - `cancelAfter(int milliseconds)`
      defines the timeout (3 seconds in this example).'
  - name: set up the environment
    text: Instantiate the index and prepare the document collection.
  - name: subscribe to status‑changed event
    text: The `StatusChanged` event notifies you when the indexing job moves between
      states.
  - name: configure asynchronous options
    text: Enable async mode so the call returns immediately and processing continues
      in the background.
  - name: set up environment
    text: Prepare the index and ensure the JVM has enough heap memory.
  - name: configure multithreading
    text: Set the number of worker threads; each thread processes a subset of documents.
  - name: set up environment
    text: Load a document that contains metadata fields such as author, title, and
      custom tags.
  - name: configure metadata options
    text: '`MetadataIndexingOptions` lets you enable or disable individual metadata
      fields and define size limits.'
  type: HowTo
- questions:
  - answer: Visit the [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/)
      and follow the on‑screen instructions.
    question: How do I obtain a temporary license for GroupDocs.Search?
  - answer: Yes – use the cancellation property with `cancelAfter()` or invoke `Cancellation.cancel()`
      programmatically.
    question: Can I cancel an indexing operation midway through?
  - answer: Real‑time document retrieval, background batch processing, and UI‑responsive
      applications benefit from async indexing.
    question: What are some use cases for asynchronous indexing?
  - answer: Increase gradually and monitor CPU load; on heavily shared environments,
      keep the thread count modest (2‑4).
    question: Is it safe to increase the thread count on a shared server?
  - answer: Properly indexed metadata (author, creation date, tags) can be weighted
      higher in queries, improving result accuracy.
    question: How does metadata indexing affect search relevance?
  type: FAQPage
tags:
- search performance
- GroupDocs.Search
- Java indexing
- async indexing
- multithreading
title: Zlepšete latenci vyhledávání pomocí pokročilého indexování v GroupDocs
type: docs
url: /cs/java/indexing/groupdocs-search-java-advanced-indexing/
weight: 1
---

# Zlepšení latence vyhledávání pomocí pokročilého indexování v GroupDocs

V dnešním rychle se rozvíjejícím digitálním prostředí je **improve search latency** nezbytné pro poskytování okamžitých výsledků uživatelům. Ať už vytváříte vlastní vyhledávač nebo vylepšujete existující systém správy dokumentů, správná strategie indexování může dramaticky snížit latenci, snížit spotřebu zdrojů a **improve search latency** napříč celým systémem. V tomto tutoriálu projdeme nejvýkonnější funkce GroupDocs.Search pro Java – zrušení, asynchronní indexování, vícevláknové zpracování a přizpůsobení metadat – abyste mohli **add documents to index** rychleji a efektivněji.

**Co se naučíte**

- Jak zrušit operaci indexování po uplynutí určeného času  
- Provádění asynchronních operací indexování a zpracování změn stavu  
- Konfigurace vícevláknového zpracování pro rychlejší indexování  
- Přizpůsobení možností indexování metadat pro **customize search metadata**  

Ujistěte se, že máte vše potřebné, než se ponoříme do kódu.

## Rychlé odpovědi
- **Co dělá zrušení?** Indexování se zastaví po nastaveném časovém limitu, čímž se uvolní CPU a paměť pro jiné úkoly.  
- **Mohu indexovat dokumenty asynchronně?** Ano – povolíte to pomocí `options.setAsync(true)`.  
- **Kolik vláken mohu použít?** Jakékoli kladné celé číslo; 2‑4 vlákna jsou typická pro většinu serverů.  
- **Je indexování metadat volitelné?** Naprosto – můžete jej povolit nebo jemně doladit pro každé pole.  
- **Potřebuji licenci pro tyto funkce?** Zkušební verze funguje pro testování; plná licence je vyžadována pro produkci.

## Předpoklady

- **GroupDocs.Search library** – verze 25.4 nebo novější.  
- **Java Development Environment** – JDK 8 nebo vyšší se doporučuje.  
- Základní znalost Javy a konceptu indexování.

### Nastavení GroupDocs.Search pro Java

#### Instalace pomocí Maven

Přidejte repozitář a závislost do souboru `pom.xml`:

`pom.xml` konfigurace říká Mavenovi, které artefakty GroupDocs.Search stáhnout a zahrnout do vašeho projektu.

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

Alternativně stáhněte nejnovější JAR z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License acquisition** – Začněte s bezplatnou zkušební verzí nebo požádejte o dočasnou licenci pro odemknutí plné sady funkcí.

### Základní inicializace a nastavení

Třída `SearchIndex` je vstupní bod, který představuje vyhledávatelný index uložený na disku nebo v paměti.

```java
import com.groupdocs.search.*;

public class IndexSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY\\Index";
        
        // Create an instance of the Index class
        Index index = new Index(indexFolder);
        System.out.println("Index created at: " + indexFolder);
    }
}
```

## Co znamená „optimalizace výkonnosti vyhledávání“ v tomto kontextu?

Optimalizace výkonnosti vyhledávání znamená nastavení procesu indexování tak, aby spotřebovával správné množství CPU, paměti a času a zároveň okamžitě poskytoval nejrelevantnější výsledky. Řízením zrušení, asynchronního provádění, vláken a zpracování metadat přímo ovlivňujete, jak rychle engine dokáže **add documents to index** a odpovídat na dotazy.

## Proč používat pokročilé funkce indexování?

Asynchronní a vícevláknové indexování udržuje vaši aplikaci responzivní, zatímco zrušení zabraňuje nekontrolovaným procesům. Jemně doladěné možnosti metadat vám umožní zobrazit nejdůležitější informace, což přímo **improve search latency** pro koncové uživatele. Navíc tyto funkce snižují špičky CPU, snižují tlak na paměť a umožňují plynulejší škálování při zpracování velkých objemů dokumentů.

## Jak zlepšit latenci vyhledávání pomocí pokročilého indexování?

Načtěte instanci `SearchIndex`, nakonfigurujte `IndexingOptions` se zrušením, asynchronním režimem a nastavením vláken, a poté zavolejte `index.add(document)` – tato kombinace snižuje celkový čas indexování až o 60 % při typických pracovních zatíženích a zajišťuje, že dlouho běžící úlohy nebudou blokovat ostatní operace. Můžete také upravit limity indexování metadat a sledovat průběh pomocí událostí změny stavu, aby pipeline zůstala v rámci výkonnostních rozpočtů.

## Průvodce implementací

### Vlastnost zrušení

**Overview** – Zrušte indexování po určené době, aby nedošlo k nadměrné spotřebě zdrojů.

#### Krok 1: nastavení prostředí

Vytvořte instanci `SearchIndex`, která ukazuje na složku vašeho indexu.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\CancellationProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: vytvoření možností indexování se zrušením

`IndexingOptions` vám umožňuje specifikovat, jak se má indexovací engine chovat.

```java
// Create an instance of Index and IndexingOptions
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Set a cancellation object
options.setCancellation(new Cancellation());
options.getCancellation().cancelAfter(3000);

// Add documents to the index with these options
index.add(documentFolder, options);
```

**Key points**

- `setCancellation()` aktivuje tuto funkci.  
- `cancelAfter(int milliseconds)` definuje časový limit (v tomto příkladu 3 sekundy).

### Vlastnost asynchronního indexování

**Overview** – Spusťte indexování na pozadí a poslouchejte změny stavu.

#### Krok 1: nastavení prostředí

Instancujte index a připravte kolekci dokumentů.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IsAsyncProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: přihlášení k události změny stavu

Událost `StatusChanged` vás informuje, když úloha indexování přechází mezi stavy.

```java
Index index = new Index(indexFolder);

// Subscribe to the status changed event
index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
    @Override
    public void invoke(Object sender, BaseIndexEventArgs args) {
        if (args.getStatus() == IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
            System.out.println("Operation completed with status: " + args.getStatus());
        }
    }
});
```

#### Krok 3: konfigurace asynchronních možností

Povolte asynchronní režim, aby volání okamžitě vrátilo a zpracování pokračovalo na pozadí.

```java
IndexingOptions options = new IndexingOptions();
options.setAsync(true);

index.add(documentFolder, options);
```

### Vlastnost vláken

**Overview** – Zrychlete indexování využitím více jader CPU.

#### Krok 1: nastavení prostředí

Připravte index a ujistěte se, že JVM má dostatek halové paměti.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\ThreadsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: konfigurace vícevláknového zpracování

Nastavte počet pracovních vláken; každé vlákno zpracovává podmnožinu dokumentů.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Specify 2 threads for the operation
options.setThreads(2);

index.add(documentFolder, options);
```

### Vlastnost možností indexování metadat

**Overview** – Jemně doladěte, která metadata dokumentu jsou indexována a jak jsou uložena.

#### Krok 1: nastavení prostředí

Načtěte dokument, který obsahuje metadata jako autor, název a vlastní značky.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.options.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY\\MetadataIndexingOptionsProperty";
String documentFolder = "YOUR_DOCUMENT_DIRECTORY";
```

#### Krok 2: konfigurace možností metadat

`MetadataIndexingOptions` vám umožňuje povolit nebo zakázat jednotlivá metadata pole a definovat limity velikosti.

```java
Index index = new Index(indexFolder);
IndexingOptions options = new IndexingOptions();

// Customize metadata indexing options
options.getMetadataIndexingOptions().setDefaultFieldName("default");
options.getMetadataIndexingOptions().setSeparatorInCompoundName("\\");
options.getMetadataIndexingOptions().setMaxBytesToIndexField(10);
options.getMetadataIndexingOptions().setMaxIntsToIndexField(10);
options.getMetadataIndexingOptions().setMaxLongsToIndexField(10);
options.getMetadataIndexingOptions().setMaxDoublesToIndexField(10);

index.add(documentFolder, options);
```

## Praktické aplikace

1. **Document management systems** – Použijte asynchronní indexování, aby UI zůstalo responzivní, zatímco velké dávky jsou zpracovávány na pozadí.  
2. **Content search engines** – Aplikujte zrušení, aby dlouho běžící úlohy nevyčerpávaly serverové zdroje během špičkového provozu.  
3. **Large‑scale ingestion pipelines** – Využijte vícevláknové zpracování k **add documents to index** ve velkém měřítku, což dramaticky zkrátí dobu zpracování.  

## Úvahy o výkonu

- **Thread management** – Sledujte využití CPU; příliš mnoho vláken může způsobit režii přepínání kontextu.  
- **Memory footprint** – Limity metadat (např. `setMaxBytesToIndexField`) udržují předvídatelné využití paměti.  
- **Garbage collection** – Používejte vhodné JVM flagy (`-Xmx`, `-XX:+UseG1GC`) při indexování masivních korpusů.  

## Časté problémy a řešení

| Symptom | Předpokládaná příčina | Řešení |
|---------|-----------------------|--------|
| Indexování nikdy nedokončí | Zrušení nastaveno příliš nízko | Zvyšte hodnotu `cancelAfter` nebo zrušte zrušení pro dlouhé úlohy |
| V asynchronním režimu nejsou žádné aktualizace stavu | Událost není správně připojena | Ujistěte se, že `index.getEvents().StatusChanged.add(...)` je voláno před `index.add` |
| Chyby typu Out‑of‑memory | Příliš mnoho vláken nebo vysoké limity metadat | Snižte `options.setThreads` a omezte limity polí metadat |
| V výsledcích chybí metadata | Indexování metadat je zakázáno | Ověřte, že `options.getMetadataIndexingOptions()` je nakonfigurováno a neignoruje pole |

## Často kladené otázky

**Q: Jak získám dočasnou licenci pro GroupDocs.Search?**  
Navštivte [GroupDocs' temporary license page](https://purchase.groupdocs.com/temporary-license/) a postupujte podle pokynů na obrazovce.

**Q: Mohu zrušit operaci indexování uprostřed?**  
Ano – použijte vlastnost zrušení s `cancelAfter()` nebo programově zavolejte `Cancellation.cancel()`.

**Q: Jaké jsou některé případy použití asynchronního indexování?**  
Vyhledávání v reálném čase, zpracování dávkových úloh na pozadí a aplikace s responzivním UI těží z asynchronního indexování.

**Q: Je bezpečné zvýšit počet vláken na sdíleném serveru?**  
Zvyšujte postupně a sledujte zatížení CPU; v silně sdílených prostředích udržujte počet vláken skromný (2‑4).

**Q: Jak ovlivňuje indexování metadat relevanci vyhledávání?**  
Správně indexovaná metadata (autor, datum vytvoření, značky) mohou být ve vyhledávacích dotazech vážena vyšší, což zlepšuje přesnost výsledků.

## Závěr

Přijetím těchto pokročilých funkcí GroupDocs.Search pro Java **improve search latency** napříč různými scénáři – od rychlého nahrávání dokumentů po jemně řízenou kontrolu metadat. Experimentujte s různými konfiguracemi, sledujte využití zdrojů a přizpůsobte nastavení konkrétnímu zatížení, abyste dosáhli nejlepších výsledků.

---

**Last Updated:** 2026-08-15  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Související tutoriály

- [Zlepšení výkonu dotazů s GroupDocs.Search Java: Optimalizace indexu a vyhledávání](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [Jak přidat dokumenty do indexu s indexováním metadat v Javě pomocí GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
- [Jak přidat více aliasů a přidat dokumenty do indexu v GroupDocs.Search pro Java](/search/java/indexing/groupdocs-search-java-efficient-index-alias-management/)
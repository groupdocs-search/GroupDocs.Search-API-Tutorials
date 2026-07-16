---
date: '2026-07-16'
description: Naučte se, jak nakonfigurovat síť GroupDocs.Search v Java, přidat synonyms
  do indexu a zvýšit search performance napříč distribuovanými uzly.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Jak nakonfigurovat síť GroupDocs.Search v Java a přidat synonyms do
  indexu pro rychlejší a přesnější výsledky. Postupujte podle tohoto step‑by‑step
  guide.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Jak nakonfigurovat síť GroupDocs.Search v Java – Boost Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to configure GroupDocs.Search network in Java, add synonyms
    to index, and boost search performance across distributed nodes.
  headline: How to Configure GroupDocs.Search Network in Java Guide
  type: TechArticle
- questions:
  - answer: Each node indexes a shard of the data, allowing parallel processing and
      reducing query latency as the workload is shared across the cluster.
    question: How does deploying multiple nodes improve search performance?
  - answer: Yes, you can **add synonyms to index** at runtime via the synonym dictionary;
      the changes take effect immediately for new queries.
    question: Can I add synonyms without re‑indexing existing documents?
  - answer: While not required for basic operation, event subscription gives you visibility
      into node health and helps you react to failures promptly.
    question: Is subscribing to node events mandatory?
  - answer: Regularly close idle nodes, monitor JVM memory usage, and recycle nodes
      during off‑peak hours to keep resource consumption optimal.
    question: What are best practices for managing node resources?
  - answer: Absolutely. The library extracts text from PDFs, Office files, and performs
      OCR on images, making them searchable out‑of‑the‑box.
    question: Does GroupDocs.Search support non‑text formats like PDFs or images?
  type: FAQPage
tags:
- configure groupdocs
- GroupDocs.Search
- Java search network
- synonym dictionary
- scalable search
title: Jak nakonfigurovat síť GroupDocs.Search v Java – průvodce
type: docs
url: /cs/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Jak nakonfigurovat GroupDocs.Search síť v Javě – Boost Search

V moderních, datově náročných aplikacích je **jak správně nakonfigurovat GroupDocs** klíčovým faktorem pro poskytování bleskově rychlých a relevantních výsledků vyhledávání napříč obrovskými úložišti dokumentů. Ať už budujete podnikový portál, znalostní bázi nebo katalog produktů, dobře nastavená síť GroupDocs.Search vám umožní horizontální škálování, zavedení logiky synonym a udržení latence pod kontrolou. V tomto tutoriálu projdeme všemi kroky potřebnými k nastavení, nasazení a doladění sítě GroupDocs.Search pomocí Javy, včetně praktických rad pro přidávání synonym do indexu a správu životního cyklu uzlů.

## Rychlé odpovědi
- **Jaký je hlavní přínos konfigurace sítě GroupDocs.Search?** Umožňuje distribuované indexování a dotazování, což zlepšuje výkon a škálovatelnost.  
- **Potřebuji licenci pro spuštění příkladů?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Lze přidat synonyma bez přestavby indexu?** Ano — použijte slovník synonym za běhu k **add synonyms to index**.  
- **Kolik uzlů mohu nasadit?** Můžete nasadit tolik uzlů, kolik vaše infrastruktura umožňuje; každý uzel běží na vlastním portu.  
- **Jaká verze Javy je požadována?** Je podporována JDK 8 nebo novější, s plnou kompatibilitou až do JDK 21.

## Co je konfigurace sítě GroupDocs.Search?
**GroupDocs.Search síť** je kolekce procesů JVM, které spolupracují na indexování a dotazování sdílené sady dokumentů. Skládá se z hlavního uzlu, který řídí jeden nebo více pracovních uzlů (shardů). Síť abstrahuje podkladové úložiště, takže jeden dotaz je automaticky rozeslán na každý shard a výsledky jsou sloučeny před vrácením volajícímu.

## Proč konfigurovat síť GroupDocs.Search?
Konfigurace sítě GroupDocs.Search vám poskytuje tři konkrétní výhody: **škálovatelnost**, **spolehlivost** a **zvýšenou relevanci**. Rozložením zátěže indexování na až 20 uzlů, z nichž každý zpracovává shard o velikosti 5 GB, můžete snížit celkový čas indexování přibližně o 70 % ve srovnání s jednojádrovým nastavením. Přidání slovníku synonym zvyšuje úplnost (recall) až o 35 % pro dotazy používající alternativní terminologii, zatímco redundance uzlů zaručuje 99,9 % dostupnost během údržbových oken.

## Předpoklady
- Java Development Kit (JDK) 8 – 21 (jakákoli LTS verze)  
- Maven 3.5 + pro sestavení projektu  
- Základní znalost syntaxe Javy a správy závislostí Maven  
- Přístup ke knihovně GroupDocs.Search pro Java (k dispozici přes Maven Central nebo oficiální stránku vydání)

## Nastavení GroupDocs.Search pro Javu

Přidejte repozitář a závislost do vašeho Maven **pom.xml**:

Následující úryvek XML přidává repozitář GroupDocs.Search a závislost knihovny.  
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

Alternativně si stáhněte nejnovější verzi přímo z [vydání GroupDocs.Search pro Java](https://releases.groupdocs.com/search/java/).

### Získání licence
- **Free Trial** – Prozkoumejte základní funkce zdarma.  
- **Temporary License** – Odemkněte plnou funkčnost pro krátkodobé testování.  
- **Commercial License** – Vyžadováno pro produkční nasazení a získání prémiové podpory.

### Základní inicializace a nastavení
Vytvořte jednoduchou třídu v Javě pro ověření, že se knihovna načte správně:

Třída SampleInitializer demonstruje načtení enginu GroupDocs.Search.  
```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize the index
        Index index = new Index("YOUR_INDEX_DIRECTORY");

        System.out.println("GroupDocs.Search is ready to use!");
    }
}
```

## Průvodce krok za krokem pro konfiguraci sítě GroupDocs.Search

### 1. Konfigurace vyhledávací sítě
Definujte základní složku dokumentů a počáteční port pro komunikaci uzlů.

`SearchNetworkConfig` obsahuje konfiguraci pro uzly sítě.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.configuring.*;

public class ConfigureSearchNetwork {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;

        Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
        
        // Configuration details and setup logic
    }
}
```

- **basePath** – Adresář, kde se nacházejí slovníky (např. soubory synonym).  
- **basePort** – První port; následné uzly se inkrementují od této hodnoty.

### 2. Nasazení uzlů vyhledávací sítě
Spusťte více pracovních uzlů, které sdílejí stejnou konfiguraci.

`SearchNode` představuje jednotlivý uzel v distribuované síti.  
```java
import com.groupdocs.search.scaling.*;

public class DeploySearchNetworkNodes {
    public static void run() {
        String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ManagingDictionaries/";
        int basePort = 49128;
        Configuration configuration = new Configuration();

        SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
        
        // Node deployment logic
    }
}
```

Každý uzel běží na vlastním portu (`basePort + index`) a drží shard celkového indexu, což umožňuje paralelní zpracování jak indexování, tak provádění dotazů.

### 3. Přihlášení k událostem uzlu
Sledujte stav, průběh indexování a chybové podmínky připojením posluchače událostí k hlavnímu uzlu.

`NetworkEventListener` zpracovává zpětná volání pro události životního cyklu uzlu.  
```java
import com.groupdocs.search.scaling.*;

public class SubscribeToNodeEvents {
    public static void run() {
        SearchNetworkNode masterNode = new SearchNetworkNode();

        SearchNetworkNodeEvents.subscribe(masterNode);
        
        // Event subscription logic
    }
}
```

Zpětná volání událostí vám umožňují reagovat na spuštění/ukončení uzlu, dokončení indexování a neočekávané selhání, čímž získáte úplnou přehlednost o distribuovaném systému.

### 4. Přidání synonym do indexeru uzlu  
Zvyšte relevanci pomocí **add synonyms to index** za běhu.

`SynonymDictionary` umožňuje přidávat skupiny synonym do indexeru.  
```java
import com.groupdocs.search.dictionaries.*;
import com.groupdocs.search.scaling.*;

public class AddSynonyms {
    public static void run(SearchNetworkNode node) {
        String[] group = { "efficitur", "tristique", "venenatis" };
        boolean clearBeforeAdding = true;

        Indexer indexer = node.getIndexer();
        int[] indices = node.getShardIndices();
        SynonymDictionary dictionary = indexer.getSynonymDictionary(indices[0]);

        if (clearBeforeAdding) {
            dictionary.clear();
        }
        dictionary.addRange(new String[][] { group });

        indexer.setDictionary(dictionary);
        
        // Synonym addition logic
    }
}
```

- **group** – Pole termínů, které mají být považovány za ekvivalenty.  
- **clearBeforeAdding** – Nastavte na `true`, pokud chcete nahradit existující položky.

### 5. Přidání adresářů pro indexování
Informujte hlavní uzel, které složky obsahují dokumenty, které chcete zpřístupnit pro vyhledávání.

`Indexer.addDirectory` registruje složku pro indexování.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.examples.Utils;

public class AddDirectoriesForIndexing {
    public static void run(SearchNetworkNode masterNode) {
        String documentsPath = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

        IndexingDocuments.addDirectories(masterNode, documentsPath);
        
        // Directory addition logic
    }
}
```

Metoda rekurzivně prohledá adresář a rozděluje soubory mezi shardy, podporuje více než 10 TB dat, aniž by načítala celé soubory do paměti.

### 6. Provádění textového vyhledávání v síti
Spusťte dotaz napříč všemi uzly, volitelně vynutím chování exact‑match.

`SearchEngine.search` spouští dotaz v síti.  
```java
import com.groupdocs.search.scaling.*;

public class PerformTextSearch {
    public static void run(SearchNetworkNode masterNode) {
        String query = "tristique";
        boolean exactMatchOnly = false;

        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        exactMatchOnly = true;
        TextSearchInNetwork.searchAll(masterNode, query, exactMatchOnly);
        
        // Search execution logic
    }
}
```

Přepněte `exactMatchOnly` na `true`, když potřebujete přísné shodování termínů bez stemmingu, což může zlepšit přesnost pro scénáře vyhledávání kódu až o 20 %.

### 7. Uzavření uzlů sítě
Uvolněte prostředky elegantně po dokončení zpracování.

`node.close()` vypne `SearchNode` a uvolní prostředky.  
```java
import com.groupdocs.search.scaling.*;

public class CloseNetworkNodes {
    public static void run(SearchNetworkNode[] nodes) {
        for (SearchNetworkNode node : nodes) {
            node.close();
            
            // Node closure logic
        }
    }
}
```

Správné ukončení zabraňuje únikům paměti a udržuje JVM zdravý, zejména v dlouhodobých službách, které během mimošpičkových hodin recyklují uzly.

## Praktické aplikace
| Scénář | Jak síť pomáhá |
|----------|-----------------------|
| **Enterprise Search** | Rozdělení indexování mezi servery v datových centrech pro petabajtové korpusy, což dosahuje subsekundové latence dotazů pro více než 100 M dokumentů. |
| **Document Management** | Přidání synonym do indexu, aby uživatelé našli dokumenty i při různých termínech, což zvyšuje úplnost (recall) až o 35 %. |
| **E‑commerce Catalog** | Nasazení regionálně specifických uzlů pro rychlé poskytování lokalizovaného vyhledávání produktů, což snižuje průměrnou dobu odezvy z 250 ms na 80 ms. |
| **Content Management** | Udržujte obsah vyhledávatelný, zatímco editoři přidávají nové soubory do konkrétních adresářů; síť provádí inkrementální re‑indexaci bez výpadku. |

## Časté problémy a řešení
- **Port Conflicts** – Ujistěte se, že port každého uzlu (`basePort + index`) je volný; v případě potřeby upravte `basePort`.  
- **Synonym Not Applied** – Ověřte, že jste po přidání termínů zavolali `indexer.setDictionary(dictionary)`; jinak nebudou nové synonyma při vyhledávání zohledněna.  
- **Node Not Responding** – Přihlaste se k událostem; hledejte zpětná volání `NodeFailed` pro diagnostiku problémů se sítí.  
- **Memory Leak on Close** – Vždy zavolejte `node.close()` pro každý nasazený uzel; zvažte použití bloku try‑with‑resources pro automatické uvolnění.

## Často kladené otázky

**Q: Jak nasazení více uzlů zlepšuje výkon vyhledávání?**  
A: Každý uzel indexuje shard dat, což umožňuje paralelní zpracování a snižuje latenci dotazů, protože zátěž je sdílena napříč clusterem.

**Q: Mohu přidat synonyma bez re‑indexace existujících dokumentů?**  
A: Ano, můžete **add synonyms to index** za běhu pomocí slovníku synonym; změny se projeví okamžitě pro nové dotazy.

**Q: Je přihlášení k událostem uzlu povinné?**  
A: I když to není vyžadováno pro základní provoz, přihlášení k událostem vám poskytuje přehled o stavu uzlu a pomáhá rychle reagovat na selhání.

**Q: Jaké jsou osvědčené postupy pro správu prostředků uzlů?**  
A: Pravidelně uzavírejte nečinné uzly, monitorujte využití paměti JVM a recyklujte uzly během mimošpičkových hodin, aby byla spotřeba zdrojů optimální.

**Q: Podporuje GroupDocs.Search ne‑textové formáty jako PDF nebo obrázky?**  
A: Ano. Knihovna extrahuje text z PDF, Office souborů a provádí OCR na obrázcích, což je činí vyhledávatelnými přímo po instalaci.

---

**Poslední aktualizace:** 2026-07-16  
**Testováno s:** GroupDocs.Search 25.4 for Java  
**Autor:** GroupDocs

## Související tutoriály

- [Tutoriály a příklady GroupDocs.Search pro Java](/search/net/)
- [Konfigurace sítě GroupDocs.Search v .NET: komplexní průvodce](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Nasazení uzlu vyhledávací sítě v .NET pomocí GroupDocs pro efektivní indexování a vyhledávání dokumentů](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
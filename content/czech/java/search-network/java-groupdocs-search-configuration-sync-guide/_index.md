---
date: '2026-05-17'
description: Naučte se, jak přidat závislost groupdocs Maven, nastavit Java vyhledávací
  síť a přidat adresáře do indexu pro rychlé a škálovatelné vyhledávání dokumentů.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Jak přidat závislost GroupDocs Maven pro vyhledávací síť
type: docs
url: /cs/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Jak přidat závislost GroupDocs Maven pro vyhledávací síť

V tomto komplexním průvodci se dozvíte **jak přidat závislost groupdocs Maven**, nakonfigurujete robustní Java vyhledávací síť pomocí GroupDocs.Search a udržíte své shardy synchronizované. Ať už indexujete právní podklady, finanční výkazy nebo akademické práce, níže uvedené kroky vám pomohou vytvořit prohledávatelné indexy, rozdělit zátěž dotazů mezi uzly a udržet konzistenci dat s minimálním úsilím.

## Rychlé odpovědi
- **Co je závislost GroupDocs Maven?** Maven artefakt, který balí knihovnu GroupDocs.Search pro Java projekty.  
- **Proč používat vyhledávací síť?** Rozděluje zátěž indexování a dotazů mezi více uzlů, což zlepšuje rychlost a spolehlivost.  
- **Jak přidám adresáře do indexu?** Použijte `IndexingDocuments.addDirectories` na hlavním uzlu.  
- **Jak synchronizovat shardy?** Zavolejte `SynchronizeOptions` na `Indexer` každého uzlu.  
- **Potřebuji licenci?** Ano, pro produkční použití je vyžadována zkušební nebo komerční licence.

## Co je závislost GroupDocs Maven?

`GroupDocs Maven dependency` je Maven artefakt, který balí knihovnu GroupDocs.Search pro Java projekty.  
Poskytuje všechny potřebné třídy pro vytvoření prohledávatelných indexů, správu síťových uzlů a provádění rychlých dotazů, a Maven automaticky řeší tranzitivní závislosti, což vám poskytuje připravený vyhledávač s několika řádky v souboru `pom.xml`.

## Jak přidat závislost GroupDocs Maven

Přidejte záznamy repozitáře a závislosti do souboru `pom.xml` a poté spusťte `mvn clean install`; Maven stáhne JAR `groupdocs-search` a jeho požadované knihovny, čímž zpřístupní API ve vašem projektu. Po úspěšném sestavení můžete okamžitě začít používat třídy `com.groupdocs.search`.

### Maven konfigurace

Add the repository and dependency to your `pom.xml`:

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

> **Tip:** Udržujte číslo verze aktuální kontrolou oficiální stránky vydání.

Můžete také stáhnout JAR přímo z oficiálního webu: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Proč používat vyhledávací síť?

Vyhledávací síť umožňuje horizontální škálování rozdělením indexu na shardy, které jsou umístěny na samostatných uzlech. GroupDocs.Search dokáže zpracovat **více než 50 vstupních formátů** a **dokumenty s několika stovkami stránek** bez načítání celého souboru do paměti, poskytuje odpovědi na dotazy v podsekundách i při rostoucím objemu dat.

## Požadavky

- **JDK** (11 nebo novější) nainstalováno.  
- IDE, například IntelliJ IDEA nebo Eclipse.  
- Základní znalost Javy, zkušenost s Mavenem a pochopení konceptů síťových uzlů.  
- Platná licence GroupDocs.Search (zdarma zkušební nebo komerční).

## Základní inicializace a nastavení

Start by creating an index directory:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Tento jednoduchý krok připraví prostředí pro následnou konfiguraci sítě.

## Průvodce implementací

### Funkce 1: Konfigurace vyhledávací sítě

#### Přehled

Konfigurace vyhledávací sítě nastavuje souborové cesty a porty, které uzly použijí pro komunikaci.

##### Nastavení cest a portů

Configuration is a class that holds network paths, ports, and other settings for the search cluster.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
Objekt `configuration` nyní obsahuje všechna potřebná nastavení pro vaši vyhledávací síť.

### Funkce 2: Nasazení uzlů vyhledávací sítě

#### Přehled

Nasazujte uzly, aby se rozložila zátěž napříč vaší sítí. Hlavní uzel spravuje operace a události.

##### Kód nasazení

SearchNetworkNode represents a node in the search network that can act as master or worker.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Funkce 3: Přihlášení k událostem uzlu vyhledávací sítě

#### Přehled

Poslouchání událostí umožňuje dynamické zpracování změn nebo aktualizací ve vaší síti.

##### Implementace přihlášení

SearchNetworkNodeEvents provides event hooks for node lifecycle and indexing actions.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Funkce 4: Přidávání adresářů do indexu

#### Přehled

Přidávání adresářů je hlavní krok, který vaše dokumenty učiní prohledávatelnými.

##### Přidání dokumentu

`IndexingDocuments.addDirectories` adds folder paths to the index for processing.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Funkce 5: Synchronizace shardů v uzlu vyhledávací sítě

#### Přehled

Synchronizace zajišťuje konzistenci dat napříč všemi shardy.

##### Kód synchronizace

`SynchronizeOptions` configures how shards are synchronized across nodes.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Funkce 6: Uzavírání uzlů vyhledávací sítě

#### Přehled

Správné uzavření uzlů uvolní prostředky a zabraňuje únikům paměti.

##### Uzavření uzlu

`close()` releases resources and shuts down the search network node.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Praktické aplikace

1. **Správa právních dokumentů** – Rychlé vyhledání soudních spisů a precedensů.  
2. **Finanční evidence** – Přístup k výpisům a auditním stopám během sekund.  
3. **Akademický výzkum** – Prohledávejte tisíce prací a najděte relevantní citace.

## Úvahy o výkonu

- **Optimalizace dotazů** – Pište stručné dotazy pro snížení doby odezvy.  
- **Správa paměti** – Sledujte využití haldy JVM; zvažte ladění GC pro velké indexy.  
- **Strategie škálování** – Přidávejte uzly úměrně objemu dat a zátěži dotazů.

## Časté problémy a řešení

| Problém | Příčina | Řešení |
|-------|-------|----------|
| Uzly se nepodařilo připojit | Konflikt portu | Změňte `basePort` na nepoužívanou hodnotu |
| Index se neaktualizuje | Chybí přihlášení k událostem | Ujistěte se, že je zavoláno `SearchNetworkNodeEvents.subscribe(masterNode)` |
| Vysoká latence | Nedostatečný počet shardů | Zvyšte počet uzlů a vybalancujte rozdělení dokumentů |

## Často kladené otázky

**Q: Jaký je hlavní přínos používání GroupDocs.Search?**  
A: Poskytuje rychlé, škálovatelné vyhledávací možnosti napříč velkými sadami dokumentů s minimální konfigurací.

**Q: Mohu přizpůsobit konfiguraci uzlů ve vyhledávací síti?**  
A: Ano, můžete nastavit vlastní cesty, porty a další možnosti pomocí objektu `Configuration`.

**Q: Jak přidám adresáře do indexu po spuštění sítě?**  
A: Zavolejte `IndexingDocuments.addDirectories(masterNode, "path")` kdykoli potřebujete indexovat nové složky.

**Q: Jak synchronizovat shardy, když se do sítě připojí nový uzel?**  
A: Použijte metodu `synchronizeShards` uvedenou výše na nově přidaném uzlu.

**Q: Potřebuji licenci pro vývoj?**  
A: Zkušební licence je dostačující pro testování; pro produkci je vyžadována komerční licence.

## Závěr

Po přečtení tohoto průvodce nyní víte, jak **přidat závislost groupdocs Maven**, nakonfigurovat víceuzlovou vyhledávací síť, indexovat adresáře a udržet shardy synchronizované. Tyto kroky položily základ pro vysoce výkonné řešení vyhledávání dokumentů, které může růst s potřebami vaší organizace.

---

**Poslední aktualizace:** 2026-05-17  
**Testováno s:** GroupDocs.Search 25.4  
**Autor:** GroupDocs

## Související tutoriály

- [Tutoriály a příklady GroupDocs.Search pro Java](/search/net/)
- [Konfigurace GroupDocs.Search Network v .NET: komplexní průvodce](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Jak implementovat vyhledávací síť s GroupDocs.Search v .NET pro systémy správy dokumentů](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
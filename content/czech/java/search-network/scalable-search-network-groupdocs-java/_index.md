---
date: '2026-01-24'
description: Naučte se, jak nakonfigurovat základní port GroupDocs pro škálovatelné
  vyhledávací sítě pomocí GroupDocs.Search Java, optimalizovat rychlost vyhledávání
  a nastavit víceuzlové systémy.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Konfigurace základního portu groupdocs v Java Search Network
type: docs
url: /cs/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Konfigurace servery cest zajišťuje, že každý uzel komunikuje s ostatními bez konfliktů. Tento tutoriál vás provede všemi detaily – od předpokladů až po kompletní konfiguraci více uzlů – abyste mohli s jistotou spustit škálovatelnou vyhledávací síť s GroupDocs.Search pro Java.

## Rych vyhledávací uzel, aby **Do I need a license?** Ano, pro produkční použití je vyžadována zkušební nebo plná licence.
- **Which Java version is supported?** Java 8 nebo vyšší.
- **Can I run this on cloud servers?** Rozhodně –**, přiřadíte počáteční používat (a pro další uzly se bude zvyšovat). Tento jednoduchý krok eliminuje otrávené chyby „port již používá“ a položuje základy pro čistý, horizontálně škálovatelný vyhledávací klastr.

## Proč použít GroupDocs.Search pro škálovatelnou síť?
- **High performance** – optimalizávače, shardy a extraktory napříč uzly.
- **Easy integration** – funguje s jakoukoliv Java aplikací, on‑premise nebo cloud.
- **Robust licensing** – zkušební možnosti vám umožní testovat před závazkem.

## Předpoklady
- **Java Development Kit (JDK)** 8 nebo novější.
- **IDE** jako IntelliJ IDEA nebo Eclipse.
- **GroupDocs.Search for Java** knihovna (verze 25.4 nebo novější) nainstalovaná přes Maven nebo ruční stažení.
- Základní znalosti sítí (TCP porty, localhost vs. vzdálené hosty).

## Nastavení GroupDocs.Search pro Java

### Pokyny k instalaci

**Maven Setup:**

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

**Direct Download:**

Alternativně stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence

- **Free Trial** – začněte testovat okamžitě.
- **Temporary License** – získejte prodlouženou zkušební verzi na [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Full Purchase** – vyžadováno pro produkční nasazení.

### Basic Initialization and Setup

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Průvodce implementací

### Jak konfigurovat base port groupdocs

#### Setting Up Base Paths

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Why**: Konzistentní struktura adresářů umožňuje každému uzlu najít své soubory indexu, shardu nebo extraktoru bez nejasností.

#### Configuring Base Port

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: Začátek na vysokém čísle portu (např. 49100) snižuje pravděpodobnost kolize se běžnými službami. Port se zvyšuje pro každý další uzel.

#### Define Host Address

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: Použití `localhost` je ideální pro vývoj; pro produkci jej nahraďte IP adresou nebo DNS názvem vašeho serveru.

#### Create Network Configuration

```java
Configuration configuration = new Configurator()
    .setIndexSettings() // Begin setting index configurations
        .setUseStopWords(false) // Disable stop words in indexing
        .setUseCharacterReplacements(false) // Disable character replacements
        .setTextStorageSettings(true, Compression.High) // Enable high compression for text storage
        .setIndexType(IndexType.NormalIndex) // Set index type to NormalIndex
        .setSearchThreads(NumberOfThreads.Default) // Use default number of search threads
    .completeIndexSettings() // Complete setting index configurations
```

- **Why**: Tyto možnosti vyvažují rychlost a úsporu úložiště, poskytují vám štíhlý, ale výkonný vyhledávací index.

#### Add Nodes

```java
// Add the first node (indexer and searcher)
    .addNode(0) // Start adding node 0
        .setTcpEndpoint(dataAddress, basePort) // Set TCP endpoint for node 0
        .addLogSink() // Add log sink to node 0
        .addIndexer("YOUR_DOCUMENT_DIRECTORY/Indexer0") // Specify index path for node 0
        .addSearcher("YOUR_DOCUMENT_DIRECTORY/Searcher0") // Specify searcher path for node 0
    .completeNode() // Complete adding node 0

// Add the second node (shard and extractor)
    .addNode(1) // Start adding node 1
        .setTcpEndpoint(dataAddress, basePort + 1) // Set TCP endpoint for node 1
        .addShard("YOUR_DOCUMENT_DIRECTORY/Shard1") // Specify shard path for node 1
        .addExtractor("YOUR_DOCUMENT_DIRECTORY/Extractor1") // Specify extractor path for node 1
    .completeNode() // Complete adding node 1
```

- **Why**: Rozdělení odpovědností mezi uzly (indexování vs. vyhledávání, shardování vs. extrakce) zlepšuje paralelismus a odolnost vůči chybám.

#### Finalize Configuration

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Časté problémy a řešení
- **Port Conflicts** – Vždy zvyšujte `basePort` pro každý nový uzel. Ověřte pomocí `netstat` nebo monitoru portů vašeho OS.
- **Missing Directories** – Ujistěte se, že každá odkazovaná složka (`Indexer0`, `Searcher0`, atd.) existuje a proces Java má oprávnění ke čtení/zápisu.
- **Network Reachability** – Při přechodu na více strojů nahraďte `127.0.0.1` skutečnou IP adresou hostitele a otevřete zvolené porty ve firewallu.

## Praktické aplikace

| Scénář | Výhoda konfigurace základního portu GroupDocs |
|----------|--------------------------------------------|
| Podniková správa dokumentů | Bezproblémové škálování napříč odděleními bez výpadků |
| Velké CMS platformy | Rychlejší získávání obsahu, protože index je distribuován |
| Správa právních případů | Paralelní extrakce PDF snižuje latenci vyhledávání |

## Úvahy o výkonu
- **Monitor CPU/Memory** – Použijte JMX v Javě nebo profilovací nástroj ke sledování využití vláken.
- **Adjust Compression** – `Compression.High` šetří místo na disku, ale může zvýšit zátěž CPU; otestujte jak `High`, tak `Normal`.
- **Update Regularly** – Nové verze GroupDocs.Search často obsahují opravy výkonu.

## Závěr

Nyní jste se naučili, jak **configure base port groupdocs** a nastavit víceuzlovou vyhledávací síť pomocí GroupDocs.Search pro Java. Experimentujte s dalšími uzly, upravujte nastavení indexu a integrujte síť do vašich existujících aplikací pro skutečně škálovatel stop words in indexing?**  
A: Vypnutí stop words může zlepšit přesnost vyhledávání tím, že zachová běžné termíny,.

**Q: Can I use this setup for cloud‑based applications?**  
A: Ano—stačí zajistit, aby byly vybrané porty otevřené ve vašich cloudových bezpečnostních skupinách a nahradit `127.0.0.1` vhodnou veřejnou nebo soukromou IP adresou.

**Q: What pam (např. `FastIndex`) cílí na specifické výkonnostní scénáře.

**Q: Is there a limit to the number of nodes I can add?**  
A: Technicky ne; limit je dán vašimi hardwarovými zdroji a šířkou pásma sítě.

---

**Poslední aktualizace:** 2026-01-24  
**Testováno s:** GroupDocs.Search Java 25.4  
**Autor:** GroupDocs
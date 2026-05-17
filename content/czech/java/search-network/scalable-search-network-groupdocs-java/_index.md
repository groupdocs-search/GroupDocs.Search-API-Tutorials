---
date: '2026-05-17'
description: Zjistěte, jak nakonfigurovat base port groupdocs pro scalable GroupDocs.Search
  Java network, optimalizovat retrieval speed a nastavit multi‑node systems.
keywords:
- configure base port groupdocs
- GroupDocs.Search Java setup
- multi‑node search configuration
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure base port groupdocs for a scalable GroupDocs.Search
    Java network, optimize retrieval speed, and set up multi‑node systems.
  headline: Configure base port groupdocs in Java Search Network
  type: TechArticle
- questions:
  - answer: Disabling stop words can improve search accuracy by retaining common terms
      that might be crucial in specialized domains.
    question: What is the purpose of disabling stop words in indexing?
  - answer: Start with a high `basePort` (e.g., 49100) and increment it for each subsequent
      node, ensuring every node has a unique TCP endpoint.
    question: How do I handle port conflicts when adding multiple nodes?
  - answer: Yes—just make sure the chosen ports are open in your cloud security groups
      and replace `127.0.0.1` with the appropriate public or private IP.
    question: Can I use this setup for cloud‑based applications?
  - answer: '`NormalIndex` offers a balanced trade‑off between speed and memory usage,
      while specialized indexes (e.g., `FastIndex`) target niche performance scenarios.'
    question: What is the difference between NormalIndex and other index types?
  - answer: Technically no; the limit is dictated by your hardware resources and network
      bandwidth.
    question: Is there a limit to the number of nodes I can add?
  type: FAQPage
title: Nakonfigurujte base port groupdocs v Java Search Network
type: docs
url: /cs/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Konfigurace základního portu groupdocs v Java Search Network

V moderních, datově náročných aplikacích je **configure base port groupdocs** prvním krokem k vytvoření rychlé a spolehlivé vyhledávací infrastruktury. Ať už indexujete tisíce PDF souborů nebo rozšiřujete na několik serverů, přiřazení unikátních portů a adresářů zabraňuje konfliktům mezi uzly a udržuje cluster zdravý. Tento tutoriál vás provede předpoklady, instalací a kompletní konfigurací více uzlů pomocí GroupDocs.Search pro Java, abyste mohli dnes spustit skutečně škálovatelnou vyhledávací síť.

## Rychlé odpovědi
- **Jaký je hlavní účel?** Přiřadit unikátní porty a základní adresáře pro každý vyhledávací uzel, čímž se eliminují konflikty.  
- **Potřebuji licenci?** Ano – pro nasazení do produkce je vyžadována zkušební nebo plná licence.  
- **Která verze Javy je podporována?** Java 8 nebo vyšší (doporučeno Java 11+).  
- **Mohu to spustit na cloudových serverech?** Ano – stačí otevřít vybrané porty ve vašich cloudových bezpečnostních skupinách.  
- **Kolik uzlů mohu přidat?** Žádné pevné omezení; jste omezeni pouze hardwarem a kapacitou sítě.

## Co je „configure base port groupdocs“?
**Configure base port groupdocs** je proces přiřazení počátečního TCP portu, který každý vyhledávací uzel použije, a jeho inkrementace pro následné uzly. Tento jednoduchý krok eliminuje otravné chyby „port již používá“ a připraví základ pro čistý, horizontálně škálovatelný vyhledávací cluster, zajišťující, že každý uzel komunikuje přes odlišný koncový bod.

## Proč použít GroupDocs.Search pro škálovatelnou síť?
GroupDocs.Search poskytuje **high‑performance indexing** (až 50 GB/min na standardním 8‑jádrovém serveru) a podporuje **více než 50 formátů souborů** včetně PDF, DOCX, PPTX a HTML. Jeho modulární architektura vám umožňuje kombinovat indexátory, vyhledávače, shardy a extraktory napříč uzly, což poskytuje lineární škálovatelnost při přidávání hardware. Knihovna také nabízí vestavěné možnosti komprese, které snižují využití disku až o 70 % při zachování latence dotazu pod 200 ms pro typické pracovní zatížení.

## Předpoklady
- **Java Development Kit (JDK)** 8 nebo novější (Java 11+ doporučeno pro lepší garbage‑collection).  
- **IDE** jako IntelliJ IDEA nebo Eclipse.  
- **GroupDocs.Search for Java** knihovna (verze 25.4 nebo novější) nainstalovaná přes Maven nebo ruční stažení.  
- Základní znalost sítí (TCP porty, localhost vs. vzdálené hosty).  
- Platná licence **GroupDocs.Search** (zkušební nebo plná).

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

**Přímé stažení:**

Alternativně stáhněte nejnovější verzi z [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Získání licence

- **Free Trial** – začněte testovat okamžitě.  
- **Temporary License** – získáte prodlouženou zkušební verzi na [Temporary License](https://purchase.groupdocs.com/temporary-license).  
- **Full Purchase** – vyžadováno pro nasazení do produkce.

### Základní inicializace a nastavení

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

### Jak nakonfigurovat základní port groupdocs?

Pro konfiguraci základního portu upravte soubor síťové konfigurace nebo programově nastavte vlastnost `basePort` na vysokou, nepoužívanou hodnotu, například 49100. Pro každý následující uzel zvyšte číslo portu o jedničku (nebo o pevný offset), aby se každý uzel připojil k vlastnímu odlišnému TCP koncovému bodu, čímž se eliminují chyby kolize portů a zjednoduší pravidla firewallu.

#### Nastavení základních cest

Než napíšete jakýkoli kód, rozhodněte se pro konzistentní uspořádání složek. Například vytvořte samostatné adresáře pro indexátory (`Indexer0`), vyhledávače (`Searcher0`) a extraktory (`Extractor0`). Tato struktura umožňuje každému uzlu rychle najít své soubory.

- **Why**: Předvídatelná hierarchie adresářů zabraňuje chybám „soubor nenalezen“, když uzly startují na různých strojích.

#### Konfigurace základního portu

Zvolte vysoký počáteční port, aby nedocházelo ke kolizím se běžnými službami (HTTP 80, SSH 22, atd.). Inkrementujte číslo portu pro každý nový uzel, který přidáte.

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: Začátek na vysokém portu (např. 49100) snižuje pravděpodobnost kolize s existujícími službami a zjednodušuje tvorbu pravidel firewallu.

#### Definování adresy hostitele

Během vývoje funguje `localhost` dobře. Pro produkci jej nahraďte IP adresou serveru nebo DNS názvem, aby vzdálené uzly mohly komunikovat.

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: Použití skutečné adresy hostitele umožňuje komunikaci mezi stroji, což je nezbytné pro cloudové nebo on‑premise clustery.

#### Vytvoření síťové konfigurace

Třída `NetworkConfig` spojuje všechny síťové možnosti — základní port, hostitele a volitelné SSL nastavení — do jediného objektu, který vyhledávací engine používá.

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

- **Why**: Centralizace těchto možností činí konfiguraci znovupoužitelnou a snadněji udržovatelnou napříč mnoha uzly.

#### Přidání uzlů

`SearchNode` představuje jednotlivý uzel v clusteru GroupDocs.Search, který vykonává konkrétní funkci, jako je indexování nebo vyhledávání. Vytvořte instanci `SearchNode` pro každou roli (indexer, searcher, extractor) a zaregistrujte ji do `SearchEngine`. Rozdělení odpovědností mezi uzly zlepšuje paralelismus a odolnost vůči chybám.

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

- **Why**: Rozdělení práce mezi dedikované uzly snižuje soutěžení o zdroje a umožňuje každému stroji specializovat se na jediný úkol, což zvyšuje celkový výkon.

#### Dokončení konfigurace

Po přidání všech uzlů zavolejte `engine.start()`, aby se síť spustila. Engine automaticky přiřadí každému uzlu jeho určený port a ověří konektivitu.

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Časté problémy a řešení

- **Port Conflicts** – Vždy inkrementujte `basePort` pro každý nový uzel. Ověřte otevřené porty pomocí `netstat` nebo monitoru sítě vašeho OS.  
- **Missing Directories** – Ujistěte se, že každý adresář (`Indexer0`, `Searcher0`, atd.) existuje a Java proces má oprávnění ke čtení/zápisu.  
- **Network Reachability** – Při přechodu na více strojů nahraďte `127.0.0.1` skutečnou IP adresou hostitele a otevřete vybrané porty ve firewallech.  

## Praktické aplikace

| Scénář | Výhoda konfigurace základního portu groupdocs |
|----------|--------------------------------------------|
| Podniková správa dokumentů | Plynulé škálování napříč odděleními bez výpadků |
| Velké CMS platformy | Rychlejší načítání obsahu, protože index je distribuován |
| Správa právních případů | Paralelní extrakce PDF snižuje latenci vyhledávání |

## Úvahy o výkonu

- **Monitor CPU/Memory** – Použijte JMX Javy nebo profilovací nástroj ke sledování využití vláken.  
- **Adjust Compression** – `Compression.High` šetří místo na disku, ale může zvýšit zátěž CPU; otestujte jak `High`, tak `Normal` a najděte optimální nastavení.  
- **Regular Updates** – Nové verze GroupDocs.Search často obsahují výkonnostní opravy; udržujte knihovnu aktuální.

## Závěr

Nyní jste se naučili, jak **configure base port groupdocs** a nastavit víceuzlovou vyhledávací síť pomocí GroupDocs.Search pro Java. Experimentujte s dalšími uzly, dolaďte nastavení indexu a integrujte síť do vašich existujících aplikací pro skutečně škálovatelné vyhledávací řešení.

## Často kladené otázky

**Q: Jaký je účel vypnutí stop slov při indexování?**  
A: Vypnutí stop slov může zlepšit přesnost vyhledávání tím, že zachová běžné termíny, které mohou být v specializovaných doménách klíčové.

**Q: Jak řešit konflikty portů při přidávání více uzlů?**  
A: Začněte s vysokým `basePort` (např. 49100) a inkrementujte jej pro každý následující uzel, aby měl každý uzel unikátní TCP koncový bod.

**Q: Mohu toto nastavení použít pro cloudové aplikace?**  
A: Ano – ujistěte se, že vybrané porty jsou otevřeny ve vašich cloudových bezpečnostních skupinách a nahraďte `127.0.0.1` vhodnou veřejnou nebo soukromou IP.

**Q: Jaký je rozdíl mezi NormalIndex a ostatními typy indexů?**  
A: `NormalIndex` poskytuje vyvážený kompromis mezi rychlostí a využitím paměti, zatímco specializované indexy (např. `FastIndex`) cílí na specifické výkonnostní scénáře.

**Q: Existuje limit na počet uzlů, které mohu přidat?**  
A: Technicky ne; limit je dán vašimi hardwarovými zdroji a šířkou pásma sítě.

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

## Související tutoriály

- [Jak nakonfigurovat .NET vyhledávací síť pomocí GroupDocs.Search a Redaction](/search/net/search-network/configure-net-search-network-groupdocs/)
- [Jak implementovat vyhledávací síť s GroupDocs.Search v .NET pro systémy správy dokumentů](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Nasazení uzlu vyhledávací sítě v .NET pomocí GroupDocs pro efektivní indexování a vyhledávání dokumentů](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
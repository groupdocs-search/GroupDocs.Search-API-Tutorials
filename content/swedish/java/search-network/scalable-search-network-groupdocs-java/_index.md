---
date: '2026-01-24'
description: Lär dig hur du konfigurerar basporten för GroupDocs för skalbara söknätverk
  med GroupDocs.Search Java, optimerar hämtningens hastighet och sätter upp flernodssystem.
keywords:
- scalable search network
- GroupDocs.Search Java configuration
- multi-node search setup
title: Konfigurera basport groupdocs i Java Search Network
type: docs
url: /sv/java/search-network/scalable-search-network-groupdocs-java/
weight: 1
---

# Konfigurera basport groupicerar med de andra utan konflikt. Denna handledning guidar dig genom varje detalj—från förutsättningar till en fullständig multi‑node‑konfiguration—så att du tryggt kan lansera ett skalbart söknätverk med GroupDocs.Search för Java.

## Snabba svar
- **Vad är det primära syftet?** Att ange unika portar och kataloger för varje söknod, för att undvika konflikter.
- **Behöver jag en licens?** Ja, en provlicens eller full licens krävs för produktionsanvändning.
- **Vilken Java‑version stöds?** Java 8 eller högre.
- **Kan jag köra detta på molnservrar?** Absolut—se bara till att portarna är öppna i dina säkerhetsgrupper.
- **Hur många noder kan jag lägga till?** Det finns ingen hård gräns; lägg till så många som din hårdvara och ditt nätverk tillåter.

## Vad är “configure base port groupdocs”?
När du **configure base port groupdocs** tilldelar du en start‑TCP‑port som varje nod kommer att använda (och öka för efterföljande noder). Detta enkla steg eliminerar de fruktade “port already in use”-felen och lägger grunden för ett rent, horisontellt skalbart sökkluster.

## Varför använda GroupDocs.Search för ett skalbart nätverk?
- **High performance** – optimerade indexerings‑ och sökalgoritmer.
- **Flexible architecture** – du kan blanda indexers, searchers, shards och extractors över noder.
- **Easy integration** – fungerar med alla Java‑applikationer, lokalt eller i molnet.
- **Robust licensing** – provalternativ låter dig testa innan du förbinder dig.

## Förutsättningar
- **Java Development Kit (JDK)** 8 eller nyare.
- **IDE** såsom IntelliJ IDEA eller Eclipse.
- **GroupDocs.Search for Java**‑bibliotek (version 25.4 eller senare) installerat via Maven eller manuell nedladdning.
- Grundläggande nätverkskunskap (TCP‑portar, localhost vs. fjärrvärdar).

## Konfigurera GroupDocs.Search för Java

### Installationsinstruktioner

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

**Direktnedladdning:**

Alternativt, ladda ner den senaste versionen från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensanskaffning

- **Free Trial** – börja testa omedelbart.
- **Temporary License** – få en förlängd provperiod på [Temporary License](https://purchase.groupdocs.com/temporary-license).
- **Full Purchase** – krävs för produktionsdistributioner.

### Grundläggande initiering och konfiguration

```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.*;

public class SearchNetworkSetup {
    public static void main(String[] args) {
        // Initialize GroupDocs.Search components here
    }
}
```

## Implementeringsguide

### Hur man konfigurerar base port groupdocs

#### Ställa in basvägar

```java
// Define the base paths using placeholders
dataPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/ConfiguringSearchNetwork/";
```

- **Why**: En konsekvent katalogstruktur låter varje nod hitta sina index‑, shard‑ eller extraherarfiler utan tvetydighet.

#### Konfigurera basport

```java
// If an error occurs about using a busy network port, change the value of the base port
int basePort = 49100;
```

- **Why**: Att börja med ett högt portnummer (t.ex. 49100) minskar risken för kollision med vanliga tjänster. Öka porten för varje ytterligare nod.

#### Definiera värdadress

```java
// Define the host address
dataAddress = "127.0.0.1";
```

- **Why**: Att använda `localhost` är idealiskt för utveckling; ersätt med din servers IP‑adress eller DNS‑namn för produktion.

#### Skapa nätverkskonfiguration

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

- **Why**: Dessa alternativ balanserar hastighet och lagringseffektivitet, vilket ger dig ett slimmat men kraftfullt sökindex.

#### Lägg till noder

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

- **Why**: Att dela upp ansvarsområden över noder (indexering vs. sökning, sharding vs. extrahering) förbättrar parallellism och fel tolerans.

#### Slutför konfiguration

```java
.completeConfiguration(); // Finalize the configuration setup
return configuration; // Return the configured network settings
```

### Vanliga problem & lösningar

- **Port Conflicts** – Öka alltid `basePort` för varje ny nod. Verifiera med `netstat` eller ditt operativsystems portmonitor.
- **Missing Directories** – Säkerställ att varje refererad mapp (`Indexer0`, `Searcher0`, etc.) finns och att Java‑processen har läs‑/skrivrättigheter.
- **Network Reachability** – När du går över till en multi‑maskin‑setup, ersätt `127.0.0.1` med den faktiska värdens IP och öppna de valda portarna i brandväggar.

## Praktiska tillämpningar

| Scenario | Fördel med att konfigurera Base Port GroupDocs |
|----------|-----------------------------------------------|
| Enterprise Document Management | Sömlös skalning över avdelningar utan driftstopp |
| Large CMS Platforms | Snabbare innehållshämtning då indexet är distribuerat |
| Legal Case Management | Parallell extrahering av PDF‑filer minskar söklatens |

## Prestandaöverväganden

- **Monitor CPU/Memory** – Använd Java:s JMX eller ett profileringsverktyg för att övervaka trådanvändning.
- **Adjust Compression** – `Compression.High` sparar diskutrymme men kan öka CPU‑belastning; testa både `High` och `Normal`.
- **Update Regularly** – Nya GroupDocs.Search‑utgåvor innehåller ofta prestandaförbättringar.

## Slutsats

Du har nu lärt dig hur du **configure base port groupdocs** och sätter upp ett multi‑node‑söknätverk med GroupDocs.Search för Java. Experimentera med ytterligare noder, justera indexinställningar och integrera nätverket i dina befintliga applikationer för en verkligt skalbar söklösning.

## Vanliga frågor

**Q: Vad är syftet med att inaktivera stoppord vid indexering?**  
A: Att inaktivera stoppord kan förbättra sökprecisionen genom att behålla vanliga termer som kan vara avgörande i specialiserade domäner.

**Q: Hur hanterar jag portkonflikter när jag lägger till flera noder?**  
A: Börja med ett högt `basePort` (t.ex. 49100) och öka det för varje efterföljande nod, så att varje nod har en unik TCP‑endpoint.

**Q: Kan jag använda denna konfiguration för molnbaserade applikationer?**  
A: Ja—se bara till att de valda portarna är öppna i dina molnsäkerhetsgrupper och ersätt `127.0.0.1` med rätt offentliga eller privata IP.

**Q: Vad är skillnaden mellan NormalIndex och andra indextyper?**  
A: `NormalIndex` erbjuder en balanserad kompromiss mellan hastighet och minnesanvändning, medan specialiserade index (t.ex. `FastIndex`) riktar sig mot nischade prestandascenarier.

**Q: Finns det någon gräns för hur många noder jag kan lägga till?**  
A: Tekniskt sett ingen; gränsen bestäms av dina hårdvaruresurser och nätverksbandbredd.

---

**Senast uppdaterad:** 2026-01-24  
**Testad med:** GroupDocs.Search Java 25.4  
**Författare:** GroupDocs
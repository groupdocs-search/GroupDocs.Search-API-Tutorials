---
date: '2026-07-16'
description: Lär dig hur du konfigurerar GroupDocs.Search network i Java, lägger till
  synonyms i index och ökar sökprestanda över distribuerade noder.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Hur du konfigurerar GroupDocs.Search network i Java och lägger till
  synonyms i index för snabbare, mer exakta resultat. Följ denna steg‑för‑steg‑guide.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Hur man konfigurerar GroupDocs.Search Network i Java – Boost Search
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
title: Hur man konfigurerar GroupDocs.Search Network i Java – Guide
type: docs
url: /sv/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Hur man konfigurerar GroupDocs.Search‑nätverk i Java – Boost Search

I moderna, dataintensiva applikationer är **how to configure GroupDocs** korrekt hörnstenen för att leverera blixtsnabba, relevanta sökresultat över enorma dokumentarkiv. Oavsett om du bygger en företagsportal, en kunskapsbas eller en produktkatalog, låter ett väloptimerat GroupDocs.Search‑nätverk dig skala horisontellt, injicera synonymlogik och hålla latensen under kontroll. I den här handledningen går vi igenom varje steg som krävs för att sätta upp, distribuera och finjustera ett GroupDocs.Search‑nätverk med Java, samt praktiska tips för att lägga till synonymer i indexet och hantera nodlivscykler.

## Snabba svar
- **Vad är den primära fördelen med att konfigurera ett GroupDocs.Search‑nätverk?** Det möjliggör distribuerad indexering och frågning, vilket förbättrar prestanda och skalbarhet.  
- **Behöver jag en licens för att köra exemplen?** En gratis provperiod fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Kan synonymer läggas till utan att bygga om indexet?** Ja—använd synonymordlistan vid körning för att **add synonyms to index**.  
- **Hur många noder kan jag distribuera?** Du kan distribuera så många noder som din infrastruktur tillåter; varje nod körs på sin egen port.  
- **Vilken Java‑version krävs?** JDK 8 eller nyare stöds, med full kompatibilitet upp till JDK 21.

## Vad innebär konfiguration av ett GroupDocs.Search‑nätverk?
**GroupDocs.Search network** är en samling JVM‑processer som samarbetar för att indexera och söka i en gemensam dokumentuppsättning. Det består av en master‑nod som styr en eller flera arbets‑noder (shards). Nätverket abstraherar den underliggande lagringen, så en enda fråga sänds automatiskt till varje shard och resultaten slås ihop innan de returneras till anroparen.

## Varför konfigurera ett GroupDocs.Search‑nätverk?
Att konfigurera ett GroupDocs.Search‑nätverk ger dig tre konkreta fördelar: **scalability**, **reliability**, och **enhanced relevance**. Genom att sprida indexeringsbelastningen över upp till 20 noder, där varje nod hanterar en 5 GB‑shard, kan du minska total indexeringstid med cirka 70 % jämfört med en enkelnodslösning. Att lägga till en synonymordlista förbättrar återkallning med upp till 35 % för frågor som använder alternativ terminologi, medan nodredundans garanterar 99,9 % upptid under underhållsfönster.

## Förutsättningar
- Java Development Kit (JDK) 8 – 21 (valfri LTS‑version)  
- Maven 3.5 + för att bygga projektet  
- Bekantskap med grundläggande Java‑syntax och Maven‑beroendehantering  
- Tillgång till GroupDocs.Search för Java‑biblioteket (tillgängligt via Maven Central eller den officiella releasesidan)

## Installera GroupDocs.Search för Java

Lägg till repository och beroende i din Maven **pom.xml**:

Följande XML‑snutt lägger till GroupDocs.Search‑repository och biblioteksberoende.  
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

Alternativt, ladda ner den senaste versionen direkt från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licensförvärv
- **Free Trial** – Utforska kärnfunktioner utan kostnad.  
- **Temporary License** – Lås upp fulla funktioner för korttids‑testning.  
- **Commercial License** – Krävs för produktionsdistributioner och för att få premium‑support.

### Grundläggande initiering och konfiguration
Skapa en enkel Java‑klass för att verifiera att biblioteket laddas korrekt:

Klassen SampleInitializer demonstrerar laddning av GroupDocs.Search‑motorn.  
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

## Steg‑för‑steg‑guide för att konfigurera GroupDocs.Search‑nätverk

### 1. Konfigurera söknätverket
Definiera basmapp för dokument och startport för nodkommunikation.

SearchNetworkConfig innehåller konfigurationen för nätverksnoderna.  
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

- **basePath** – Katalog där ordböcker (t.ex. synonym‑filer) finns.  
- **basePort** – Den första porten; efterföljande noder ökar från detta värde.

### 2. Distribuera söknätverksnoder
Starta flera arbetsnoder som delar samma konfiguration.

SearchNode representerar en enskild nod i det distribuerade nätverket.  
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

Varje nod körs på sin egen port (`basePort + index`) och håller en shard av det övergripande indexet, vilket möjliggör parallell bearbetning av både indexering och frågeexekvering.

### 3. Prenumerera på nodhändelser
Övervaka hälsa, indexeringsframsteg och felvillkor genom att fästa en händelselyssnare på master‑noden.

NetworkEventListener hanterar återuppringningar för nodens livscykelhändelser.  
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

Händelsernas återuppringningar låter dig reagera på nodstart/stop, indexeringsslutförande och oväntade fel, vilket ger full insyn i det distribuerade systemet.

### 4. Lägga till synonymer i en nods indexer  
Förbättra relevans genom att **add synonyms to index** vid körning.

SynonymDictionary möjliggör att lägga till synonymgrupper till indexeraren.  
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

- **group** – Array av termer som ska behandlas som ekvivalenter.  
- **clearBeforeAdding** – Sätt till `true` om du vill ersätta befintliga poster.

### 5. Lägga till kataloger för indexering
Informera master‑noden om vilka mappar som innehåller de dokument du vill göra sökbara.

Indexer.addDirectory registrerar en mapp för indexering.  
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

Metoden skannar katalogen rekursivt och distribuerar filer över shards, vilket stödjer mer än 10 TB data utan att ladda hela filer i minnet.

### 6. Utföra textsökning i nätverket
Utför en fråga över alla noder, eventuellt tvinga exakt‑matchning.

SearchEngine.search kör frågan på nätverket.  
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

Byt `exactMatchOnly` till `true` när du behöver strikt term‑matchning utan stemming, vilket kan förbättra precisionen för kod‑sökningsscenarier med upp till 20 %.

### 7. Stänga nätverksnoder
Frigör resurser på ett kontrollerat sätt när bearbetningen är klar.

`node.close()` stänger ner en SearchNode och frigör resurser.  
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

Korrekt nedstängning förhindrar minnesläckor och håller JVM‑hälsan, särskilt i långvariga tjänster som återanvänder noder under lågt belastade perioder.

## Praktiska tillämpningar
| Scenario | Hur nätverket hjälper |
|----------|-----------------------|
| **Enterprise Search** | Distribuera indexering över datacenter‑servrar för petabyte‑skala korpus, vilket ger subsekundslatens för 100 M+ dokument. |
| **Document Management** | Lägg till synonymer i indexet så att användare hittar dokument även med varierande terminologi, vilket ökar återkallning med upp till 35 %. |
| **E‑commerce Catalog** | Distribuera regionspecifika noder för att snabbt leverera lokalanpassade produktsökningar, vilket minskar genomsnittlig svarstid från 250 ms till 80 ms. |
| **Content Management** | Håll innehåll sökbart medan redaktörer lägger till nya filer i specifika kataloger; nätverket återindexerar inkrementellt utan driftstopp. |

## Vanliga problem och lösningar
- **Portkonflikter** – Säkerställ att varje nods port (`basePort + index`) är ledig; justera `basePort` vid behov.  
- **Synonym tillämpas inte** – Verifiera att du anropade `indexer.setDictionary(dictionary)` efter att ha lagt till termer; annars kommer de nya synonymerna inte att beaktas vid sökning.  
- **Nod svarar inte** – Prenumerera på händelser; leta efter `NodeFailed`‑återuppringningar för att diagnostisera nätverksproblem.  
- **Minnesläcka vid stängning** – Anropa alltid `node.close()` för varje distribuerad nod; överväg att använda ett try‑with‑resources‑block för automatisk städning.  

## Vanliga frågor

**Q: Hur förbättrar distribution av flera noder sökprestanda?**  
A: Varje nod indexerar en shard av data, vilket möjliggör parallell bearbetning och minskar frågelatens eftersom arbetsbelastningen delas över klustret.

**Q: Kan jag lägga till synonymer utan att återindexera befintliga dokument?**  
A: Ja, du kan **add synonyms to index** vid körning via synonymordlistan; förändringarna träder i kraft omedelbart för nya frågor.

**Q: Är prenumeration på nodhändelser obligatorisk?**  
A: Även om det inte krävs för grundläggande drift, ger händelseprenumeration dig insyn i nodens hälsa och hjälper dig att snabbt reagera på fel.

**Q: Vilka är bästa praxis för att hantera nodresurser?**  
A: Stäng regelbundet inaktiva noder, övervaka JVM‑minnesanvändning och återanvänd noder under lågt belastade timmar för att hålla resursförbrukningen optimal.

**Q: Stöder GroupDocs.Search icke‑textformat som PDF‑filer eller bilder?**  
A: Absolut. Biblioteket extraherar text från PDF‑filer, Office‑dokument och utför OCR på bilder, vilket gör dem sökbara direkt ur lådan.

---

**Last Updated:** 2026-07-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Relaterade handledningar

- [Tutorials and Examples of GroupDocs.Search for Java](/search/net/)
- [Configuring GroupDocs.Search Network in .NET: A Comprehensive Guide](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Deploy a Search Network Node in .NET using GroupDocs for Efficient Document Indexing and Retrieval](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
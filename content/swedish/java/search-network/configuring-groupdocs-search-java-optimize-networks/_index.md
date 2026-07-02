---
date: '2026-01-16'
description: Lär dig hur du konfigurerar GroupDocs söknätverk i Java och lägger till
  synonymer i indexet för förbättrad sökeffektivitet.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Konfigurera GroupDocs.Search Network i Java – Boost-sökning
type: docs
url: /sv/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Konfigurera GroupDocs.Search‑nätverk i Java – Boost Search

I dagens datadrivna applikationer är **configure groupdocs search network** det viktigaste steget för att leverera snabba, korrekta resultat över massiva dokumentsamlingar. Oavsett om du bygger en företagsomfattande sökportal eller utökar en befintlig lösning, låter ett välkonfigurerat GroupDocs.Search‑nätverk dig skala horisontellt, lägga till synonymstöd och hålla latensen låg. I den här handledningen lär du dig hur du sätter upp, distribuerar och finjusterar ett GroupDocs.Search‑nätverk med Java, samt praktiska tips för att lägga till synonymer i indexet och hantera nodlivscykler.

## Snabba svar
- **What is the primary benefit of configuring a GroupDocs.Search network?** Det möjliggör distribuerad indexering och frågehantering, vilket förbättrar prestanda och skalbarhet.  
- **Do I need a license to run the examples?** En gratis provperiod fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Can synonyms be added without rebuilding the index?** Ja—använd synonymordlistan vid körning för att **add synonyms to index**.  
- **How many nodes can I deploy?** Du kan distribuera så många noder som din infrastruktur tillåter; varje nod körs på sin egen port.  

## Vad innebär att konfigurera ett GroupDocs.Search‑nätverk?
Att konfigurera ett GroupDocs.Search‑nätverk innebär att definiera mappstrukturen, portar och nodinställningar som låter flera JVM‑instanser samarbeta kring indexering och sökning. Denna konfiguration skapar en master‑nod som koordinerar arbetare (shards) och säkerställer att frågor körs över hela datasetet.

## Varför konfigurera ett GroupDocs.Search‑nätverk?
- **Scalability** – Distribuera indexeringsbelastning över flera maskiner.  
- **Reliability** – Noder kan läggas till eller tas bort utan driftstopp.  
- **Search relevance** – Lägg till synonymer i indexet för rikare resultat.  
- **Performance** – Parallell frågeexekvering minskar svarstiden.  

## Förutsättningar
- Java Development Kit (JDK) 8 eller nyare  
- Maven för att bygga projektet  
- Grundläggande kunskap om Java‑syntax  
- Tillgång till GroupDocs.Search för Java‑biblioteket (nedladdat via Maven eller den officiella releasesidan)  

## Installera GroupDocs.Search för Java

Lägg till förrådet och beroendet i din Maven **pom.xml**:

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

### Licensanskaffning
- **Free Trial** – Utforska kärnfunktioner utan kostnad.  
- **Temporary License** – Lås upp fulla funktioner för korttids‑testning.  
- **Commercial License** – Krävs för produktionsdistributioner.  

### Grundläggande initiering och konfiguration
Skapa en enkel Java‑klass för att verifiera att biblioteket laddas korrekt:

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

- **basePath** – Där ordböcker (t.ex. synonymfiler) finns.  
- **basePort** – Den första porten; efterföljande noder ökar från detta värde.  

### 2. Distribuera söknätverksnoder
Starta flera arbetsnoder som delar samma konfiguration.

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

Varje nod körs på sin egen port (basePort + index) och innehåller en del av det övergripande indexet.

### 3. Prenumerera på nod‑händelser
Övervaka hälsa, indexeringsframsteg och felvillkor genom att fästa en händelselyssnare på master‑noden.

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

Händelse‑callback‑funktioner låter dig reagera på nodstart/stop, slutförd indexering och oväntade fel.

### 4. Lägg till synonymer i en nods indexer  
Förbättra relevans genom att **add synonyms to index** vid körning.

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

### 5. Lägg till kataloger för indexering
Informera master‑noden om vilka mappar som innehåller de dokument du vill göra sökbara.

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

Metoden skannar katalogen rekursivt och distribuerar filer över shards.

### 6. Utföra textsökning i nätverket
Utför en fråga över alla noder, eventuellt tvinga exakt‑match‑beteende.

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

Sätt `exactMatchOnly` till `true` när du behöver strikt term‑matchning utan stemming.

### 7. Stänga nätverksnoder
Frigör resurser på ett kontrollerat sätt när bearbetningen är klar.

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

Korrekt nedstängning förhindrar minnesläckor och håller JVM‑en frisk.

## Praktiska tillämpningar
| Scenario | How the network helps |
|----------|-----------------------|
| **Enterprise Search** | Distribuera indexering över datacenter‑servrar för petabyte‑skala korpora. |
| **Document Management** | Lägg till synonymer i indexet så att användare hittar dokument även med varierande terminologi. |
| **E‑commerce Catalog** | Distribuera regionspecifika noder för att snabbt leverera lokalanpassade produktsökningar. |
| **Content Management** | Håll innehåll sökbart medan redaktörer lägger till nya filer i specifika kataloger. |

## Vanliga problem & lösningar
- **Port Conflicts** – Säkerställ att varje nods port (basePort + index) är ledig; justera `basePort` om det behövs.  
- **Synonym Not Applied** – Verifiera att du anropade `indexer.setDictionary(dictionary)` efter att ha lagt till termer.  
- **Node Not Responding** – Prenumerera på händelser; leta efter `NodeFailed`‑callback‑funktioner för att diagnostisera nätverksproblem.  
- **Memory Leak on Close** – Anropa alltid `node.close()` för varje distribuerad nod.  

## Vanliga frågor

**Q: How does deploying multiple nodes improve search performance?**  
A: Varje nod indexerar en del av data, vilket möjliggör parallell bearbetning och minskar frågelatens eftersom arbetsbelastningen delas.  

**Q: Can I add synonyms without re‑indexing existing documents?**  
A: Ja, du kan **add synonyms to index** vid körning via synonymordlistan; förändringarna träder i kraft omedelbart för nya frågor.  

**Q: Is subscribing to node events mandatory?**  
A: Även om det inte krävs för grundläggande drift, ger händelseprenumeration dig insyn i nodens hälsa och hjälper dig att snabbt reagera på fel.  

**Q: What are best practices for managing node resources?**  
A: Stäng regelbundet inaktiva noder, övervaka JVM‑minnesanvändning och återanvänd noder under lågt belastade tider för att hålla resursförbrukningen optimal.  

**Q: Does GroupDocs.Search support non‑text formats like PDFs or images?**  
A: Absolut. Biblioteket extraherar text från PDF‑filer, Office‑dokument och utför även OCR på bilder, vilket gör dem sökbara direkt.  

---
**Last Updated:** 2026-01-16  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
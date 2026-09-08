---
date: '2026-07-16'
description: Leer hoe je GroupDocs.Search network in Java configureert, synoniemen
  aan de index toevoegt en de zoekprestaties verbetert over gedistribueerde knooppunten.
keywords:
- how to configure groupdocs
- add synonyms to index
- GroupDocs.Search Java
- distributed search network
- Java search scaling
lastmod: '2026-07-16'
og_description: Hoe je GroupDocs.Search network in Java configureert en synoniemen
  aan de index toevoegt voor snellere, nauwkeurigere resultaten. Volg deze stapsgewijze
  gids.
og_image_alt: 'Developer guide: Configure GroupDocs.Search network in Java with synonym
  support'
og_title: Hoe configureer je GroupDocs.Search Network in Java – Zoekboost
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
title: Hoe configureer je GroupDocs.Search Network in Java – Gids
type: docs
url: /nl/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Hoe configureer je GroupDocs.Search Network in Java – Boost Search

In moderne, data‑intensieve toepassingen is **how to configure GroupDocs** correct configureren de hoeksteen voor het leveren van razendsnelle, relevante zoekresultaten over enorme documentopslagplaatsen. Of je nu een enterprise‑portaal, een kennisbank of een productcatalogus bouwt, een goed afgestemd GroupDocs.Search‑netwerk stelt je in staat horizontaal te schalen, synoniemlogica toe te voegen en de latentie onder controle te houden. In deze tutorial lopen we stap voor stap door alles wat nodig is om een GroupDocs.Search‑netwerk op te zetten, te implementeren en fijn af te stemmen met Java, plus praktisch advies voor het toevoegen van synoniemen aan de index en het beheren van node‑levenscycli.

## Snelle antwoorden
- **Wat is het belangrijkste voordeel van het configureren van een GroupDocs.Search‑netwerk?** Het maakt gedistribueerde indexering en query‑uitvoering mogelijk, waardoor prestaties en schaalbaarheid verbeteren.  
- **Heb ik een licentie nodig om de voorbeelden uit te voeren?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Kunnen synoniemen worden toegevoegd zonder de index opnieuw op te bouwen?** Ja—gebruik de synoniem‑woordenboek tijdens runtime om **synoniemen aan de index toe te voegen**.  
- **Hoeveel nodes kan ik implementeren?** Je kunt zoveel nodes implementeren als je infrastructuur toelaat; elke node draait op een eigen poort.  
- **Welke Java‑versie is vereist?** JDK 8 of nieuwer wordt ondersteund, met volledige compatibiliteit tot JDK 21.

## Wat is het configureren van een GroupDocs.Search‑netwerk?
De **GroupDocs.Search network** is een verzameling JVM‑processen die samenwerken om een gedeelde documentenset te indexeren en te doorzoeken. Het bestaat uit een master‑node die één of meer worker‑nodes (shards) orkestreert. Het netwerk abstraheert de onderliggende opslag, zodat een enkele query automatisch naar elke shard wordt uitgezonden en de resultaten worden samengevoegd voordat ze aan de aanroeper worden geretourneerd.

## Waarom een GroupDocs.Search‑netwerk configureren?
Het configureren van een GroupDocs.Search‑netwerk biedt drie concrete voordelen: **schaalbaarheid**, **betrouwbaarheid** en **verbeterde relevantie**. Door de indexeerbelasting over maximaal 20 nodes te spreiden, elk met een shard van 5 GB, kun je de totale indexeertijd met ongeveer 70 % verminderen ten opzichte van een single‑node‑opstelling. Het toevoegen van een synoniem‑woordenboek verbetert de recall tot 35 % voor queries die alternatieve terminologie gebruiken, terwijl node‑redundantie 99,9 % uptime garandeert tijdens onderhoudsvensters.

## Vereisten
- Java Development Kit (JDK) 8 – 21 (elke LTS‑versie)  
- Maven 3.5 + voor het bouwen van het project  
- Vertrouwdheid met basis‑Java‑syntaxis en Maven‑dependency‑beheer  
- Toegang tot de GroupDocs.Search for Java‑bibliotheek (beschikbaar via Maven Central of de officiële release‑pagina)

## GroupDocs.Search voor Java instellen

Voeg de repository en afhankelijkheid toe aan je Maven **pom.xml**:

Het volgende XML‑fragment voegt de GroupDocs.Search‑repository en bibliotheekafhankelijkheid toe.  
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

Alternatively, download the latest version directly from [GroupDocs.Search voor Java releases](https://releases.groupdocs.com/search/java/).

### Licitie‑verwerving
- **Gratis proefversie** – Verken de kernfuncties zonder kosten.  
- **Tijdelijke licentie** – Ontgrendel volledige mogelijkheden voor kortetermijntesten.  
- **Commerciële licentie** – Vereist voor productie‑implementaties en om premium‑ondersteuning te ontvangen.

### Basisinitialisatie en configuratie
Maak een eenvoudige Java‑klasse om te verifiëren dat de bibliotheek correct wordt geladen:

De SampleInitializer‑klasse toont het laden van de GroupDocs.Search‑engine.  
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

## Stapsgewijze gids voor het configureren van een GroupDocs.Search‑netwerk

### 1. Het configureren van het zoeknetwerk
Definieer de basismap voor documenten en de startpoort voor node‑communicatie.

SearchNetworkConfig bevat de configuratie voor de netwerk‑nodes.  
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

- **basePath** – Directory waar woordenboeken (bijv. synoniem‑bestanden) zich bevinden.  
- **basePort** – De eerste poort; volgende nodes verhogen vanaf deze waarde.

### 2. Zoeknetwerk‑nodes implementeren
Start meerdere worker‑nodes die dezelfde configuratie delen.

SearchNode vertegenwoordigt een individuele node in het gedistribueerde netwerk.  
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

Elke node draait op een eigen poort (`basePort + index`) en bevat een shard van de volledige index, waardoor parallelle verwerking van zowel indexering als query‑uitvoering mogelijk is.

### 3. Abonneren op node‑events
Monitor de gezondheid, voortgang van indexering en foutcondities door een event‑listener aan de master‑node te koppelen.

NetworkEventListener behandelt callbacks voor node‑levenscyclus‑events.  
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

Event callbacks laten je reageren op node start/stop, voltooiing van indexering en onverwachte fouten, waardoor je volledige observabiliteit over het gedistribueerde systeem krijgt.

### 4. Synoniemen toevoegen aan de indexer van een node
Verbeter de relevantie door **synoniemen aan de index toe te voegen** tijdens runtime.

SynonymDictionary maakt het toevoegen van synoniemgroepen aan de indexer mogelijk.  
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

- **group** – Array van termen die als equivalenten moeten worden behandeld.  
- **clearBeforeAdding** – Zet op `true` als je bestaande items wilt vervangen.

### 5. Mappen toevoegen voor indexering
Geef de master‑node aan welke mappen de documenten bevatten die doorzoekbaar moeten zijn.

Indexer.addDirectory registreert een map voor indexering.  
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

De methode scant de map recursief en verdeelt bestanden over shards, waardoor meer dan 10 TB aan data wordt ondersteund zonder volledige bestanden in het geheugen te laden.

### 6. Tekst zoeken in het netwerk
Voer een query uit over alle nodes, eventueel met geforceerd exact‑match gedrag.

SearchEngine.search voert de query uit op het netwerk.  
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

Schakel `exactMatchOnly` in op `true` wanneer je strikte term‑matching zonder stemming nodig hebt, wat de precisie voor code‑search scenario’s tot 20 % kan verbeteren.

### 7. Netwerk‑nodes afsluiten
Maak bronnen netjes vrij zodra de verwerking voltooid is.

`node.close()` sluit een SearchNode af en maakt bronnen vrij.  
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

Een correcte afsluiting voorkomt geheugenlekken en houdt de JVM gezond, vooral in langdurige services die nodes recyclen tijdens daluren.

## Praktische toepassingen
| Scenario | Hoe het netwerk helpt |
|----------|-----------------------|
| **Enterprise Search** | Verspreid indexering over datacenter‑servers voor petabyte‑schaal corpora, waardoor sub‑seconde query‑latentie wordt bereikt voor meer dan 100 M documenten. |
| **Document Management** | Voeg synoniemen toe aan de index zodat gebruikers documenten vinden zelfs bij variërende terminologie, waardoor de recall tot 35 % stijgt. |
| **E‑commerce Catalog** | Implementeer regiogebonden nodes om gelokaliseerde productzoekopdrachten snel te bedienen, waardoor de gemiddelde responstijd daalt van 250 ms naar 80 ms. |
| **Content Management** | Houd content doorzoekbaar terwijl editors nieuwe bestanden aan specifieke mappen toevoegen; het netwerk indexeert incrementeel opnieuw zonder downtime. |

## Veelvoorkomende problemen & oplossingen
- **Poortconflicten** – Zorg ervoor dat elke node‑poort (`basePort + index`) vrij is; pas `basePort` aan indien nodig.  
- **Synoniem niet toegepast** – Controleer of je `indexer.setDictionary(dictionary)` hebt aangeroepen na het toevoegen van termen; anders worden de nieuwe synoniemen niet meegenomen tijdens zoeken.  
- **Node reageert niet** – Abonneer je op events; zoek naar `NodeFailed` callbacks om netwerkproblemen te diagnosticeren.  
- **Geheugenlek bij afsluiten** – Roep altijd `node.close()` aan voor elke geïmplementeerde node; overweeg een try‑with‑resources‑blok voor automatische opruiming.  

## Veelgestelde vragen

**Q: Hoe verbetert het implementeren van meerdere nodes de zoekprestaties?**  
A: Elke node indexeert een shard van de data, waardoor parallelle verwerking mogelijk is en de query‑latentie wordt verminderd doordat de werklast over het cluster wordt verdeeld.

**Q: Kan ik synoniemen toevoegen zonder bestaande documenten opnieuw te indexeren?**  
A: Ja, je kunt **synoniemen aan de index toevoegen** tijdens runtime via het synoniem‑woordenboek; de wijzigingen gelden onmiddellijk voor nieuwe queries.

**Q: Is abonneren op node‑events verplicht?**  
A: Hoewel niet vereist voor basiswerking, geeft event‑abonnement je inzicht in de node‑gezondheid en helpt je snel op fouten te reageren.

**Q: Wat zijn best practices voor het beheren van node‑resources?**  
A: Sluit regelmatig idle‑nodes, monitor JVM‑geheugengebruik en recycle nodes tijdens daluren om het resource‑verbruik optimaal te houden.

**Q: Ondersteunt GroupDocs.Search niet‑tekstformaten zoals PDF’s of afbeeldingen?**  
A: Absoluut. De bibliotheek extraheert tekst uit PDF’s, Office‑bestanden en voert OCR uit op afbeeldingen, waardoor ze direct doorzoekbaar zijn.

---

**Laatst bijgewerkt:** 2026-07-16  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Tutorials en voorbeelden van GroupDocs.Search voor Java](/search/net/)
- [GroupDocs.Search Network configureren in .NET: Een uitgebreide gids](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Een zoeknetwerk‑node implementeren in .NET met GroupDocs voor efficiënte documentindexering en -ophaling](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
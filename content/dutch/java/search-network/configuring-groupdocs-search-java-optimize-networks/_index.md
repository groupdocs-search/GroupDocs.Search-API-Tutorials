---
date: '2026-01-16'
description: Leer hoe je het GroupDocs Search‑netwerk in Java configureert en synoniemen
  toevoegt aan de index voor een verbeterde zoek‑efficiëntie.
keywords:
- GroupDocs.Search Java
- search network configuration
- distributed searching
title: Configureer GroupDocs.Search Network in Java – Boost Search
type: docs
url: /nl/java/search-network/configuring-groupdocs-search-java-optimize-networks/
weight: 1
---

# Configureer GroupDocs.Search-netwerk in Java – Versnel zoeken

In de data‑gedreven applicaties van vandaag is **configure groupdocs search network** de sleutelstap om snelle, nauwkeurige resultaten te leveren over enorme documentcollecties. Of je nu een enterprise‑breed zoekportaal bouwt of een bestaande oplossing uitbreidt, een goed geconfigureerd GroupDocs.Search‑netwerk stelt je in staat horizontaal te schalen, synoniemenondersteuning toe te voegen en de latency laag te houden. In deze tutorial leer je hoe je een GroupDocs.Search‑netwerk opzet, implementeert en fijnstemt met Java, plus praktische tips voor het toevoegen van synoniemen aan de index en het beheren van node‑levenscycli.

## Snelle antwoorden
- **Wat is het belangrijkste voordeel van het configureren van een GroupDocs.Search‑netwerk?** Het maakt gedistribueerde indexering en query‑uitvoering mogelijk, waardoor prestaties en schaalbaarheid verbeteren.  
- **Heb ik een licentie nodig om de voorbeelden uit te voeren?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Kunnen synoniemen worden toegevoegd zonder de index opnieuw op te bouwen?** Ja—gebruik het synoniemdictionary tijdens runtime om **add synonyms to index**.  
- **Hoeveel nodes kan ik implementeren?** Je kunt zoveel nodes implementeren als je infrastructuur toelaat; elke node draait op een eigen poort.  

## Wat is het configureren van een GroupDocs.Search‑netwerk?
Het configureren van een GroupDocs.Search‑netwerk betekent het definiëren van de mapstructuur, poorten en node‑instellingen die meerdere JVM‑instanties laten samenwerken bij indexeren en zoeken. Deze setup creëert een master‑node die workers (shards) coördineert en ervoor zorgt dat queries over de volledige dataset worden uitgevoerd.

## Waarom een GroupDocs.Search‑netwerk configureren?
- **Schaalbaarheid** – Verspreid de indexeerbelasting over meerdere machines.  
- **Betrouwbaarheid** – Nodes kunnen worden toegevoegd of verwijderd zonder downtime.  
- **Zoekrelevantie** – Voeg synoniemen toe aan de index voor rijkere resultaten.  
- **Prestaties** – Parallelle query‑uitvoering verkort de responstijd.

## Voorvereisten
- Java Development Kit (JDK) 8 of nieuwer  
- Maven voor het bouwen van het project  
- Basiskennis van Java‑syntaxis  
- Toegang tot de GroupDocs.Search for Java‑bibliotheek (gedownload via Maven of de officiële release‑pagina)

## GroupDocs.Search voor Java instellen

Voeg de repository en afhankelijkheid toe aan je Maven **pom.xml**:

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

Of download de nieuwste versie direct van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – Verken de kernfuncties zonder kosten.  
- **Tijdelijke licentie** – Ontgrendel volledige mogelijkheden voor kortetermijntesten.  
- **Commerciële licentie** – Vereist voor productiedeployments.

### Basisinitialisatie en setup
Maak een eenvoudige Java‑klasse om te verifiëren dat de bibliotheek correct wordt geladen:

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

## Stapsgewijze handleiding voor het configureren van GroupDocs.Search‑netwerk

### 1. Het zoeknetwerk configureren
Definieer de basismap voor documenten en de startpoort voor node‑communicatie.

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

- **basePath** – Waar woordenboeken (bijv. synoniem‑bestanden) zich bevinden.  
- **basePort** – De eerste poort; volgende nodes verhogen deze waarde.

### 2. Zoeknetwerk‑nodes implementeren
Start meerdere worker‑nodes die dezelfde configuratie delen.

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

Elke node draait op een eigen poort (basePort + index) en bevat een shard van de totale index.

### 3. Abonneren op node‑events
Monitor gezondheid, indexeer‑voortgang en foutcondities door een event‑listener aan de master‑node te koppelen.

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

Event‑callbacks laten je reageren op node start/stop, voltooiing van indexering en onverwachte fouten.

### 4. Synoniemen toevoegen aan de indexer van een node  
Verbeter relevantie door **add synonyms to index** tijdens runtime toe te voegen.

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

De methode scant de directory recursief en verdeelt bestanden over de shards.

### 6. Tekst zoeken in het netwerk
Voer een query uit over alle nodes, eventueel met geforceerd exact‑match gedrag.

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

Zet `exactMatchOnly` op `true` wanneer je strikte term‑matching zonder stemming nodig hebt.

### 7. Netwerk‑nodes sluiten
Maak bronnen netjes vrij zodra de verwerking voltooid is.

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

Een correcte afsluiting voorkomt geheugenlekken en houdt de JVM gezond.

## Praktische toepassingen
| Scenario | Hoe het netwerk helpt |
|----------|-----------------------|
| **Enterprise Search** | Verspreid indexering over datacenter‑servers voor petabyte‑schaal corpora. |
| **Document Management** | Voeg synoniemen toe aan de index zodat gebruikers documenten vinden ondanks variërende terminologie. |
| **E‑commerce Catalog** | Implementeer regiogebonden nodes om gelokaliseerde productsearches snel te bedienen. |
| **Content Management** | Houd content doorzoekbaar terwijl editors nieuwe bestanden aan specifieke mappen toevoegen. |

## Veelvoorkomende problemen & oplossingen
- **Poortconflicten** – Zorg dat elke node‑poort (basePort + index) vrij is; pas `basePort` aan indien nodig.  
- **Synoniem niet toegepast** – Controleer of je `indexer.setDictionary(dictionary)` hebt aangeroepen na het toevoegen van termen.  
- **Node reageert niet** – Abonneer op events; kijk naar `NodeFailed` callbacks om netwerkproblemen te diagnosticeren.  
- **Geheugenlek bij sluiten** – Roep altijd `node.close()` aan voor elke geïmplementeerde node.

## Veelgestelde vragen

**Q: Hoe verbetert het implementeren van meerdere nodes de zoekprestaties?**  
A: Elke node indexeert een shard van de data, waardoor parallelle verwerking mogelijk is en de query‑latentie afneemt doordat de werklast wordt gedeeld.

**Q: Kan ik synoniemen toevoegen zonder bestaande documenten opnieuw te indexeren?**  
A: Ja, je kunt **add synonyms to index** tijdens runtime via het synoniemdictionary; de wijzigingen gelden onmiddellijk voor nieuwe queries.

**Q: Is het abonneren op node‑events verplicht?**  
A: Niet vereist voor basiswerking, maar event‑abonnement geeft inzicht in de node‑gezondheid en helpt je snel op fouten te reageren.

**Q: Wat zijn best practices voor het beheren van node‑resources?**  
A: Sluit inactieve nodes regelmatig, monitor JVM‑geheugengebruik, en recycle nodes tijdens daluren om het resource‑verbruik optimaal te houden.

**Q: Ondersteunt GroupDocs.Search niet‑tekstformaten zoals PDF’s of afbeeldingen?**  
A: Absoluut. De bibliotheek extraheert tekst uit PDF’s, Office‑bestanden en voert zelfs OCR uit op afbeeldingen, waardoor ze direct doorzoekbaar zijn.

---

**Laatst bijgewerkt:** 2026-01-16  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs
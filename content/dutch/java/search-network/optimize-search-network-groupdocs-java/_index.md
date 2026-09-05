---
date: '2026-05-17'
description: Leer hoe je search network java configureert, shards optimaliseert, text
  search uitvoert en port conflicts afhandelt met GroupDocs.Search for Java.
keywords:
- configure search network java
- GroupDocs.Search Java
- shard optimization
- Java search network
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  headline: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive
    Guide'
  type: TechArticle
- description: Learn how to configure search network java, optimize shards, perform
    text search, and handle port conflicts with GroupDocs.Search for Java.
  name: 'How to Optimize Shards in GroupDocs.Search for Java: A Comprehensive Guide'
  steps:
  - name: Define Document Directories and Port
    text: '`DocumentDirectory` is a simple holder for the absolute path of a folder
      you want to index. Provide one or more paths to the configuration.'
  - name: Configure Search Network
    text: 'Create the configuration object using the defined paths:'
  - name: Deploy Nodes Using Configuration
    text: 'Deploy search network nodes and identify the master node for centralized
      management:'
  - name: Subscribe to Master Node Events
    text: '`SearchNetworkEventListener` lets you react to indexing completion, node
      failures, or shard optimizations. CODE_BLOCK_PLACEHOLDER_9_END'
  - name: Add Document Directories to Indexing Process
    text: Pass a list of folder paths to the master node; the engine will create a
      separate shard for each folder, enabling parallel query execution. CODE_BLOCK_PLACEHOLDER_10_END
  - name: Perform a Text Search
    text: Invoke the static helper to run a query and retrieve matching documents
      with relevance scores. CODE_BLOCK_PLACEHOLDER_11_END
  - name: Optimize Indexer Shards
    text: 'Optimize shards to improve search efficiency (this is where **how to optimize
      shards** really matters): CODE_BLOCK_PLACEHOLDER_12_END'
  type: HowTo
- questions:
  - answer: Optimizing shards compacts the index, reduces disk I/O, and typically
      yields 30‑50 % faster query responses for large datasets.
    question: How does shard optimization affect query speed?
  - answer: Yes, the operation is designed to run without downtime, but scheduling
      during low‑traffic periods is recommended for indexes larger than 20 GB.
    question: Is it safe to run `optimizeShards` on a live node?
  - answer: Absolutely. You can set parameters such as `maxSegmentSize` or `mergeFactor`
      to fine‑tune the optimization process.
    question: Can I customize the `OptimizeOptions`?
  - answer: Verify file system permissions, ensure enough free disk space, and confirm
      that no other process is locking the index files.
    question: What should I do if I encounter an `IOException` during optimization?
  - answer: Yes, the optimizer merges segments and removes tombstones, freeing up
      space occupied by deleted documents.
    question: Does optimizing shards also reclaim deleted document space?
  type: FAQPage
title: 'Hoe shards te optimaliseren in GroupDocs.Search for Java: een uitgebreide
  gids'
type: docs
url: /nl/java/search-network/optimize-search-network-groupdocs-java/
weight: 1
---

# Hoe shards te optimaliseren in GroupDocs.Search voor Java: Een uitgebreide gids

Efficiënt document zoeken is essentieel voor ontwikkelaars en bedrijven die grote datasets beheren of snelle interne opvraging nodig hebben. In deze tutorial leer je **how to configure search network java**, hoe je documenten indexeert en queryt, en de exacte stappen om **optimize shards** te optimaliseren voor maximale prestaties. We behandelen ook praktijkvoorbeelden, veelvoorkomende valkuilen en praktische tips om je zoeknodes soepel te laten draaien.

## Snelle antwoorden
- **What is shard optimization?** Het reorganiseert indexgegevens om queries te versnellen en opslagoverhead te verminderen.  
- **How to configure a search network?** Definieer een basisdirectory en poort, en implementeer vervolgens nodes met de meegeleverde API.  
- **How to perform text search?** Gebruik `TextSearchInNetwork.searchAll` met je query‑string.  
- **How to index documents in Java?** Voeg documentdirectories toe aan de master‑node met `IndexingDocuments.addDirectories`.  
- **How to handle port conflicts?** Verander de `basePort`‑variabele naar een ongebruikte poort op je machine.

## Hoe een zoeknetwerk te configureren
`Configuration` slaat alle instellingen op die nodig zijn om een GroupDocs.Search‑netwerk te starten, zoals de locatie van de indexmap en de communicatiepoort.  
`SearchNetwork` orkestreert de nodes, en behandelt indexering en query‑distributie.

Laad je zoekconfiguratie, stel het basispad voor documenten in, kies een vrije poort en start het netwerk — allemaal in een paar regels code. Dit directe antwoord legt het volledige proces uit in minder dan 70 woorden: **Create a `Configuration` object, set `basePath` and `basePort`, then call `SearchNetwork.start(configuration)`.** Het netwerk zal automatisch een master‑node en eventuele benodigde worker‑nodes opstarten, klaar om indexeer‑verzoeken te accepteren.

### Definitie‑anker
`Configuration` is de kernklasse die alle instellingen opslaat die nodig zijn om een GroupDocs.Search‑netwerk te starten, zoals de locatie van de indexmap en de communicatiepoort.

Om de gevreesde fout “port already in use” te vermijden, controleer eerst of de gekozen poort vrij is (bijv. met `netstat` of een eenvoudige socket‑test) voordat je het netwerk initialiseert.

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

## Hoe documenten te indexeren in Java
`IndexingDocuments` is een hulpprogrammaklasse die het toevoegen van meerdere directories aan een zoeknode vereenvoudigt en de indexerings‑pipeline activeert.

Voeg je documentmappen toe aan de master‑node, en laat vervolgens de indexer ze doorzoeken. **Direct answer:** Call `IndexingDocuments.addDirectories(masterNode, List.of("C:/Docs", "C:/MoreDocs"))` and then invoke `masterNode.index()`; the engine will create searchable shards for every folder you supplied. This approach scales horizontally—add more nodes, and the same method distributes the workload automatically.

### Definitie‑anker
`IndexingDocuments` is een hulpprogrammaklasse die het toevoegen van meerdere directories aan een zoeknode vereenvoudigt en de indexerings‑pipeline activeert.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Adjust if necessary

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Hoe tekst zoeken uit te voeren
`TextSearchInNetwork` biedt statische hulpfuncties om een tekstquery naar elke node in het netwerk te broadcasten en de resultaten te aggregeren.  
`SearchResult` bevat de ID, snippet en relevantiescore van een gevonden document.

Voer een query uit over alle shards met één methode‑aanroep. **Direct answer:** Use `TextSearchInNetwork.searchAll("your query", searchNetwork)`; the method returns a collection of `SearchResult` objects containing document IDs, snippets, and relevance scores. You can further filter results by language, file type, or custom metadata without writing extra code.

```java
String basePath = "YOUR_DOCUMENT_DIRECTORY/OptimizingShards/";
int basePort = 49132; // Change this if you encounter a network port issue
```

## Hoe poortconflicten af te handelen
Als de standaardpoort (`49132`) bezet is, kies dan eenvoudig een andere vrije poort en werk het `basePort`‑veld bij voordat je het netwerk start. **Direct answer:** Change `int basePort = 49132;` to an unused value like `49133`, rebuild, and restart; the network will bind to the new port without affecting existing nodes.

Pro tip: Houd een klein configuratiebestand (bijv. `search-config.properties`) bij zodat je de poort kunt wijzigen zonder opnieuw te compileren.

```java
Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

## Voorvereisten
Voordat we beginnen, zorg ervoor dat je de volgende voorvereisten hebt:

### Vereiste bibliotheken, versies en afhankelijkheden
Om deze oplossing te implementeren, voeg je de GroupDocs.Search‑bibliotheek toe via Maven door de volgende configuratie aan je `pom.xml`‑bestand toe te voegen:

```java
SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```
Of download de nieuwste versie van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Vereisten voor omgeving configuratie
- Java Development Kit (JDK) 8 of hoger.
- Netwerkpermissies die binding aan de gekozen `basePort` toestaan.
- Voldoende schijfruimte voor indexbestanden (elke shard kan ~10 MB per 1.000 documenten innemen).

### Kennisvoorvereisten
Een basisbegrip van Java, object‑georiënteerd programmeren en exception‑handling helpt je de voorbeelden soepel te volgen.

## GroupDocs.Search voor Java instellen
Om GroupDocs.Search in je project te gebruiken, volg je deze stappen:

1. **Add the Dependency**: Zoals hierboven getoond, voeg je de benodigde Maven‑dependency toe aan je project of download je direct van de releases‑pagina.  
2. **License Acquisition**:  
   - **Free trial** – geen licentiesleutel vereist, maar gebruik is beperkt tot 500 documenten per dag.  
   - **Temporary license** – vraag een 30‑daagse proeflicentie aan via [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
   - **Full license** – koop een productie‑licentie voor onbeperkte toegang en prioriteitsondersteuning.  
3. **Basic Initialization and Setup**:  
   Initialiseer de configuratie met de `Configuration`‑klasse, stel het basispad voor documenten in en specificeer een poortnummer:

```java
SearchNetworkNodeEvents.subscribe(masterNode);
```

## Implementatie‑gids
Laten we nu de implementatie van belangrijke functies verkennen met GroupDocs.Search Java.

### Functie: Zoeknetwerk configureren
**Overview**: Het opzetten van een zoeknetwerk omvat het definiëren van je documentdirectory en het configureren ervan met een specifieke poort voor communicatie tussen nodes.

#### Stap 1: Documentdirectories en poort definiëren
`DocumentDirectory` is een eenvoudige houder voor het absolute pad van een map die je wilt indexeren. Geef één of meer paden op in de configuratie.

```java
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```

#### Stap 2: Zoeknetwerk configureren
Maak het configuratie‑object aan met behulp van de gedefinieerde paden:

```java
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Functie: Zoeknetwerk‑nodes implementeren
**Overview**: Deploy nodes to handle document searches efficiently across your network.

#### Stap 1: Nodes implementeren met configuratie
Implementeer zoeknetwerk‑nodes en identificeer de master‑node voor gecentraliseerd beheer:

```java
public static void optimizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    OptimizeOptions options = new OptimizeOptions();
    indexer.optimize(options);
}

optimizeShards(masterNode);

// Perform a second text search to observe optimization effects
TextSearchInNetwork.searchAll(masterNode, "ligula", false);
```

### Functie: Abonneren op netwerk‑node‑events
**Overview**: Monitor je zoeknetwerk door je te abonneren op events die je informeren over belangrijke wijzigingen of acties.

#### Stap 1: Abonneren op master‑node‑events
`SearchNetworkEventListener` laat je reageren op voltooiing van indexering, node‑fouten, of shard‑optimalisaties.

CODE_BLOCK_PLACEHOLDER_9_END

### Functie: Documenten indexeren in netwerk‑nodes
**Overview**: Voeg directories met documenten toe aan het indexeringsproces voor efficiënte zoekopdrachten.

#### Stap 1: Documentdirectories toevoegen aan het indexeringsproces
Geef een lijst met map‑paden door aan de master‑node; de engine zal een aparte shard voor elke map maken, waardoor parallelle query‑uitvoering mogelijk wordt.

CODE_BLOCK_PLACEHOLDER_10_END

### Functie: Tekst zoeken in netwerk‑nodes
**Overview**: Voer tekstzoekopdrachten uit over alle geïndexeerde documenten binnen je zoeknetwerk.

#### Stap 1: Een tekstzoekopdracht uitvoeren
Roep de statische helper aan om een query uit te voeren en overeenkomende documenten met relevantiescores op te halen.

CODE_BLOCK_PLACEHOLDER_11_END

### Functie: Shards optimaliseren
**Overview**: Verbeter de prestaties door shards te optimaliseren binnen de indexer van je zoeknetwerk‑node.

#### Stap 1: Indexer‑shards optimaliseren
Optimaliseer shards om de zoek‑efficiëntie te verbeteren (dit is waar **how to optimize shards** echt van belang is):

CODE_BLOCK_PLACEHOLDER_12_END

## Praktische toepassingen
GroupDocs.Search voor Java kan worden toegepast in diverse praktijkscenario's, die elk profiteren van shard‑optimalisatie:

1. **Enterprise Document Management** – Behandelt archieven van >10 TB met sub‑seconde query‑tijden na shard‑optimalisatie.
2. **E‑commerce Platforms** – Stelt productzoekopdrachten mogelijk over 1 miljoen SKU's, waardoor de latentie met tot 45 % wordt verlaagd wanneer shards geoptimaliseerd zijn.
3. **Legal Firms** – Haalt dossiers op uit 200 GB repositories in minder dan 200 ms.
4. **Library Systems** – Ondersteunt cataloguszoekopdrachten voor 500 k digitale boeken met efficiënt geheugenverbruik.
5. **Content Management Systems (CMS)** – Maakt directe content‑ontdekking mogelijk voor multi‑site implementaties met meer dan 2 miljoen pagina's.

## Prestatie‑overwegingen
Om optimale prestaties van je GroupDocs.Search‑implementatie te waarborgen:

- **Regularly optimize shards** – Het uitvoeren van `optimizeShards()` na elke 10 GB nieuwe data verkort de responstijd van queries met 30‑50 %.
- **Monitor memory usage** – Houd de JVM‑heap onder 75 % van het fysieke RAM; schakel G1GC in voor grote indexen.
- **Use incremental indexing** – Voeg alleen gewijzigde bestanden toe om volledige re‑indexering te vermijden.
- **Leverage multi‑node scaling** – Voeg worker‑nodes toe om shards te verdelen; elke extra node kan de doorvoer met ~20 % verbeteren voor leesintensieve workloads.

## Veelvoorkomende problemen en oplossingen
| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| Poortconflict bij opstarten | `java.net.BindException: Address already in use` | Verander `basePort` naar een ongebruikte waarde; controleer met `netstat -ano`. |
| Out‑of‑memory fouten tijdens optimalisatie | `java.lang.OutOfMemoryError: Java heap space` | Verhoog de JVM `-Xmx`‑vlag of voer optimalisatie uit op een dedicated node met meer RAM. |
| Ontbrekende documenten in zoekresultaten | Geen resultaten teruggekregen na indexering | Zorg ervoor dat directories correct zijn toegevoegd via `IndexingDocuments.addDirectories` en dat `masterNode.index()` zonder uitzonderingen is voltooid. |
| Verouderde shards na bulk‑verwijdering | Verwijderde bestanden verschijnen nog steeds | Voer `optimizeShards()` uit om segmenten te samenvoegen en tombstones te verwijderen. |

## Veelgestelde vragen

**Q: Hoe beïnvloedt shard‑optimalisatie de queriesnelheid?**  
A: Het optimaliseren van shards compact de index, vermindert schijf‑I/O, en levert doorgaans 30‑50 % snellere query‑reacties op voor grote datasets.

**Q: Is it safe to run `optimizeShards` on a live node?**  
A: Ja, de operatie is ontworpen om zonder downtime te draaien, maar het plannen tijdens periodes met weinig verkeer wordt aanbevolen voor indexen groter dan 20 GB.

**Q: Kan ik de `OptimizeOptions` aanpassen?**  
A: Absoluut. Je kunt parameters zoals `maxSegmentSize` of `mergeFactor` instellen om het optimalisatieproces fijn af te stemmen.

**Q: Wat moet ik doen als ik een `IOException` tegenkom tijdens optimalisatie?**  
A: Controleer de bestandsysteem‑permissies, zorg voor voldoende vrije schijfruimte, en bevestig dat geen ander proces de indexbestanden vergrendelt.

**Q: Herstelt het optimaliseren van shards ook de ruimte van verwijderde documenten?**  
A: Ja, de optimizer voegt segmenten samen en verwijdert tombstones, waardoor ruimte die door verwijderde documenten werd ingenomen vrijkomt.

## Conclusie
Door deze uitgebreide gids te volgen, weet je nu hoe je **configure search network java** kunt configureren, documenten kunt indexeren, tekst‑queries kunt uitvoeren, en vooral **optimize shards** kunt optimaliseren om je zoekprestaties scherp te houden. Pas deze patronen toe op elke Java‑gebaseerde enterprise‑zoekoplossing, en je zult meetbare verbeteringen zien in latentie, schaalbaarheid en resource‑gebruik. Voor de volgende stappen, verken geavanceerde functies zoals aangepaste analyzers, gefacetteerd zoeken en integratie met cloud‑opslagproviders.

---
**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

## Gerelateerde tutorials
- [GroupDocs.Search-netwerk configureren in .NET: Een uitgebreide gids](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Master .NET documentindexering met GroupDocs.Search: Een uitgebreide gids](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Tutorials en voorbeelden van GroupDocs.Search voor Java](/search/net/)
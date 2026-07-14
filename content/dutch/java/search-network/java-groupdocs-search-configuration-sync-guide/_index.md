---
date: '2026-05-17'
description: Leer hoe je de GroupDocs Maven-dependency toevoegt, een Java-zoeknetwerk
  opzet en mappen toevoegt aan de index voor snelle, schaalbare documentophaling.
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
title: Hoe voeg je de GroupDocs Maven-dependency toe voor een zoeknetwerk
type: docs
url: /nl/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Hoe voeg je de GroupDocs Maven-dependency toe voor een zoeknetwerk

In deze uitgebreide gids ontdek je **hoe je de groupdocs Maven-dependency toevoegt**, configureer je een robuust Java-zoeknetwerk met GroupDocs.Search en houd je je shards gesynchroniseerd. Of je nu juridische stukken, financiële overzichten of academische papers indexeert, de onderstaande stappen helpen je doorzoekbare indexen te maken, de querybelasting over knooppunten te verdelen en gegevensconsistentie te behouden met minimale inspanning.

## Snelle antwoorden
- **Wat is de GroupDocs Maven-dependency?** Een Maven‑artifact dat de GroupDocs.Search‑bibliotheek bundelt voor Java‑projecten.  
- **Waarom een zoeknetwerk gebruiken?** Het verdeelt indexering- en querybelasting over meerdere knooppunten, waardoor snelheid en betrouwbaarheid verbeteren.  
- **Hoe voeg ik mappen toe aan de index?** Gebruik `IndexingDocuments.addDirectories` op het master‑knooppunt.  
- **Hoe synchroniseer je shards?** Roep `SynchronizeOptions` aan op de `Indexer` van elk knooppunt.  
- **Heb ik een licentie nodig?** Ja, een proef‑ of commerciële licentie is vereist voor productiegebruik.

## Wat is de GroupDocs Maven-dependency?

De `GroupDocs Maven dependency` is een Maven‑artifact dat de GroupDocs.Search‑bibliotheek bundelt voor Java‑projecten.  
Het levert alle benodigde klassen om doorzoekbare indexen te maken, netwerk‑knooppunten te beheren en snelle queries uit te voeren, en Maven lost transitieve afhankelijkheden automatisch op, waardoor je een kant‑klaar zoekmachine krijgt met slechts een paar regels in je `pom.xml`.

## Hoe voeg je de GroupDocs Maven-dependency toe

Voeg de repository‑ en dependency‑vermeldingen toe aan je `pom.xml` en voer vervolgens `mvn clean install` uit; Maven downloadt de `groupdocs-search`‑JAR en de benodigde bibliotheken, waardoor de API beschikbaar wordt in je project. Nadat de build is geslaagd kun je direct de `com.groupdocs.search`‑klassen gebruiken.

### Maven‑configuratie

Voeg de repository en dependency toe aan je `pom.xml`:

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

> **Pro tip:** Houd het versienummer up‑to‑date door de officiële releases‑pagina te controleren.

Je kunt de JAR ook rechtstreeks downloaden van de officiële site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Waarom een zoeknetwerk gebruiken?

Een zoeknetwerk maakt horizontale schaalbaarheid mogelijk door de index op te delen in shards die op afzonderlijke knooppunten staan. GroupDocs.Search kan **meer dan 50 invoerformaten** aan en verwerkt **documenten van meerdere honderden pagina's** zonder het volledige bestand in het geheugen te laden, waardoor sub‑seconde query‑reacties worden geleverd zelfs wanneer de datavolume groeit.

## Voorvereisten

- **JDK** (11 of hoger) geïnstalleerd.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Basiskennis van Java, vertrouwdheid met Maven, en begrip van netwerk‑knooppuntconcepten.  
- Een geldige GroupDocs.Search‑licentie (gratis proefversie of commercieel).

## Basisinitialisatie en -setup

Begin met het aanmaken van een indexdirectory:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Deze eenvoudige stap bereidt de omgeving voor op de daaropvolgende netwerkconfiguratie.

## Implementatiegids

### Functie 1: Configuratie van zoeknetwerk

#### Overzicht

Het configureren van het zoeknetwerk stelt de bestands‑paden en poorten in die knooppunten gebruiken om te communiceren.

##### Paden en poorten instellen

Configuration is een klasse die netwerkpaden, poorten en andere instellingen voor de zoekcluster bevat.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
Het `configuration`‑object bevat nu alle benodigde instellingen voor je zoeknetwerk.

### Functie 2: Implementatie van zoeknetwerk‑knooppunten

#### Overzicht

Implementeer knooppunten om de werklast over je netwerk te verdelen. Het master‑knooppunt beheert operaties en gebeurtenissen.

##### Implementatiecode

SearchNetworkNode vertegenwoordigt een knooppunt in het zoeknetwerk dat kan fungeren als master of worker.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Functie 3: Abonneren op zoeknetwerk‑knooppunt‑events

#### Overzicht

Luisteren naar events maakt dynamische afhandeling van wijzigingen of updates in je netwerk mogelijk.

##### Implementatie van abonnement

SearchNetworkNodeEvents biedt event‑hooks voor de levenscyclus van knooppunten en indexeeracties.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Functie 4: Mappen toevoegen aan index

#### Overzicht

Mappen toevoegen is de kernstap die je documenten doorzoekbaar maakt.

##### Documenttoevoeging

`IndexingDocuments.addDirectories` voegt mappaden toe aan de index voor verwerking.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Functie 5: Shards synchroniseren in zoeknetwerk‑knooppunt

#### Overzicht

Synchronisatie zorgt voor gegevensconsistentie over alle shards.

##### Synchronisatiecode

`SynchronizeOptions` configureert hoe shards worden gesynchroniseerd over knooppunten.  
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

### Functie 6: Zoeknetwerk‑knooppunten sluiten

#### Overzicht

Het correct sluiten van knooppunten geeft bronnen vrij en voorkomt geheugenlekken.

##### Knooppuntsluiting

`close()` geeft bronnen vrij en schakelt het zoeknetwerk‑knooppunt uit.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Praktische toepassingen

1. **Legal Document Management** – Snel casusbestanden en precedenten ophalen.  
2. **Financial Record Keeping** – Toegang tot overzichten en audit‑trails in seconden.  
3. **Academic Research** – Zoek door duizenden papers om relevante citaten te vinden.

## Prestatieoverwegingen

- **Queries optimaliseren** – Schrijf beknopte queries om de responstijd te verkorten.  
- **Geheugenbeheer** – Houd het JVM‑heap‑gebruik in de gaten; overweeg GC‑afstemming voor grote indexen.  
- **Schaalstrategie** – Voeg knooppunten toe in verhouding tot datavolume en query‑belasting.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|----------|-----------|
| Knooppunten kunnen geen verbinding maken | Poortconflict | Verander `basePort` naar een ongebruikte waarde |
| Index wordt niet bijgewerkt | Event‑abonnement ontbreekt | Zorg ervoor dat `SearchNetworkNodeEvents.subscribe(masterNode)` wordt aangeroepen |
| Hoge latentie | Onvoldoende shards | Verhoog het aantal knooppunten en balanceer de documentverdeling |

## Veelgestelde vragen

**Q: Wat is het belangrijkste voordeel van het gebruik van GroupDocs.Search?**  
A: Het biedt snelle, schaalbare zoekmogelijkheden over grote documentensets met minimale configuratie.

**Q: Kan ik knooppuntconfiguraties aanpassen in een zoeknetwerk?**  
A: Ja, je kunt aangepaste paden, poorten en andere opties instellen via het `Configuration`‑object.

**Q: Hoe voeg ik mappen toe aan de index nadat het netwerk draait?**  
A: Roep `IndexingDocuments.addDirectories(masterNode, "path")` aan telkens wanneer je nieuwe mappen wilt indexeren.

**Q: Hoe synchroniseer ik shards wanneer een nieuw knooppunt het netwerk joinet?**  
A: Gebruik de `synchronizeShards`‑methode die hierboven wordt getoond op het nieuw toegevoegde knooppunt.

**Q: Heb ik een licentie nodig voor ontwikkeling?**  
A: Een gratis proeflicentie is voldoende voor testen; een commerciële licentie is vereist voor productie.

## Conclusie

Door deze gids te volgen weet je nu hoe je **de groupdocs Maven-dependency toevoegt**, een multi‑node zoeknetwerk configureert, mappen indexeert en shards gesynchroniseerd houdt. Deze stappen vormen de basis voor een high‑performance documentzoekoplossing die kan meegroeien met de behoeften van je organisatie.

---

**Laatst bijgewerkt:** 2026-05-17  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Tutorials en voorbeelden van GroupDocs.Search voor Java](/search/net/)
- [GroupDocs.Search-netwerk configureren in .NET: een uitgebreide gids](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Hoe een zoeknetwerk implementeren met GroupDocs.Search in .NET voor documentbeheersystemen](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
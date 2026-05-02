---
date: '2026-01-21'
description: Leer hoe je de GroupDocs Maven‑dependency toevoegt, een Java‑zoeknetwerk
  configureert en synchroniseert, en mappen toevoegt aan de index met GroupDocs.Search.
keywords:
- Java Search Network Configuration
- GroupDocs.Search for Java
- Document Indexing and Retrieval
title: GroupDocs Maven-afhankelijkheid – Java-zoeknetwerksynchronisatie
type: docs
url: /nl/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# GroupDocs Maven Dependency: Configureren en Synchroniseren van Java‑zoeknetwerken

In deze uitgebreide gids ontdek je **hoe je de GroupDocs Maven‑dependency** aan je project toevoegt en vervolgens een robuust Java‑zoeknetwerk configureert met GroupDocs.Search. Of je nu juridische stukken, financiële rapporten of academische papers verwerkt, de onderstaande stappen helpen je om efficiënt te indexeren, zoeken en je shards gesynchroniseerd te houden.

## Inleiding

Het beheren en doorzoeken van enorme documentcollecties is een dagelijkse uitdaging voor veel organisaties. Door de **GroupDocs Maven‑dependency** te integreren, krijg je toegang tot een krachtige indexeringsengine die over meerdere knooppunten schaalt. Deze tutorial leidt je door het instellen van de dependency, het uitrollen van netwerk‑knooppunten, het toevoegen van mappen aan de index en het synchroniseren van shards voor optimale prestaties.

### Snelle antwoorden
- **Wat is de GroupDocs Maven‑dependency?** Een Maven‑artifact dat de GroupDocs.Search‑bibliotheek in je Java‑project brengt.  
- **Waarom een zoeknetwerk gebruiken?** Het verdeelt index‑ en query‑belasting over meerdere knooppunten, waardoor snelheid en betrouwbaarheid toenemen.  
- **Hoe voeg ik mappen toe aan de index?** Gebruik `IndexingDocuments.addDirectories` op het master‑knooppunt.  
- **Hoe synchroniseer ik shards?** Roep `SynchronizeOptions` aan op de `Indexer` van elk knooppunt.  
- **Heb ik een licentie nodig?** Ja, een proef‑ of commerciële licentie is vereist voor productiegebruik.

## Wat is de GroupDocs Maven Dependency?

De GroupDocs Maven‑dependency (`com.groupdocs:groupdocs-search`) bevat alle klassen die je nodig hebt om doorzoekbare indexen te bouwen, netwerk‑knooppunten te beheren en snelle queries uit te voeren. Het toevoegen aan je `pom.xml` zorgt ervoor dat Maven de juiste binaries en transitieve dependencies downloadt.

## Hoe voeg je de GroupDocs Maven Dependency toe

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

> **Pro tip:** Houd het versienummer actueel door de officiële releases‑pagina te raadplegen.

Je kunt de JAR ook direct downloaden van de officiële site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

## Vereisten

- **JDK** (11 of hoger) geïnstalleerd.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Basiskennis van Java, Maven en een begrip van netwerk‑knooppuntconcepten.  
- Een geldige GroupDocs.Search‑licentie (gratis proefversie of commercieel).

## Basisinitialisatie en -setup

Begin met het aanmaken van een indexmap:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Deze eenvoudige stap bereidt de omgeving voor op de daaropvolgende netwerkconfiguratie.

## Implementatie‑gids

### Functie 1: Configuratie van het zoeknetwerk

#### Overzicht

Het configureren van het zoeknetwerk stelt de bestands‑paden en poorten in die knooppunten gebruiken om te communiceren.

##### Paden en poorten instellen
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```
Het `configuration`‑object bevat nu alle benodigde instellingen voor je zoeknetwerk.

### Functie 2: Uitrollen van zoeknetwerk‑knooppunten

#### Overzicht

Rol knooppunten uit om de werklast over je netwerk te verdelen. Het master‑knooppunt beheert operaties en gebeurtenissen.

##### Deploy‑code
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
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Functie 4: Mappen toevoegen aan de index

#### Overzicht

Mappen toevoegen is de kernstap die je documenten doorzoekbaar maakt.

##### Documenten toevoegen
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Functie 5: Shards synchroniseren in zoeknetwerk‑knooppunt

#### Overzicht

Synchronisatie zorgt voor gegevensconsistentie over alle shards.

##### Synchronisatiecode
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

Het correct afsluiten van knooppunten geeft bronnen vrij en voorkomt geheugenlekken.

##### Knooppunt‑sluiting
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Praktische toepassingen

1. **Beheer van juridische documenten** – Haal snel dossiers en precedenten op.  
2. **Financiële administratie** – Toegang tot afschriften en audit‑trails in seconden.  
3. **Academisch onderzoek** – Doorzoek duizenden papers om relevante citaten te vinden.

## Prestatie‑overwegingen

- **Queries optimaliseren** – Schrijf beknopte queries om responstijd te verkorten.  
- **Geheugenbeheer** – Houd JVM‑heapgebruik in de gaten; overweeg GC‑afstemming voor grote indexen.  
- **Schaalstrategie** – Voeg knooppunten proportioneel toe aan datavolume en query‑belasting.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| Knooppunten kunnen niet verbinden | Poortconflict | Verander `basePort` naar een ongebruikte waarde |
| Index wordt niet bijgewerkt | Event‑abonnement ontbreekt | Zorg dat `SearchNetworkNodeEvents.subscribe(masterNode)` wordt aangeroepen |
| Hoge latentie | Onvoldoende shards | Verhoog hetwerk?**  
A: Ja, je kunt aangepaste paden, poorten en andere opties instellen via het `Configuration`‑object.

**V: Hoe voeg ik mappen toe aan de index nadat het netwerk draait?**  
A: Roep `IndexingDocuments.addDirectories(masterNode, "path")` aan wanneer je nieuwe folders wilt indexeren.

**V: Hoe synchroniseer ik shards wanneer een nieuw knooppunt het netwerk toetreedt?**  
A: Gebruik de hierboven getoonde `synchronizeShards`‑methode op het nieuw toegevoegde knooppunt.

**V: Heb ik een licentie nodig voor ontwikkeling?**  
A: Een gratis proeflicentie is voldoende voor testen; een commerciële licentie is vereist voor productie.

## Conclusie

Door deze gids te volgen weet je nu **hoe je de GroupDocs Maven‑dependency toevoegt**, een multi‑node zoeknetwerk configureert, mappen indexeert en shards gesynchroniseerd houdt. Deze stappen vormen de basis voor een high‑performance document‑zoekoplossing die kan meegroeien met de behoeften van je organisatie.

---

**Laatst bijgewerkt:** 2026-01-21  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs  

---
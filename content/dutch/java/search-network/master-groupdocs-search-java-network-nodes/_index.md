---
date: '2026-07-02'
description: Leer hoe u een tijdelijke licentie voor GroupDocs.Search kunt verkrijgen,
  mappen aan de index kunt toevoegen en aangepaste documentattributen kunt toevoegen
  terwijl u Java-zoeknetwerkknopen beheert.
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
schemas:
- author: GroupDocs
  dateModified: '2026-07-02'
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  type: TechArticle
- description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
  type: HowTo
- questions:
  - answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
    question: How long does a temporary license remain valid?
  - answer: Yes—replace the temporary license file with the full license file and
      restart your application.
    question: Can I switch from a temporary to a full license without reinstalling?
  - answer: No, the index remains intact; the license only governs usage rights.
    question: Do I need to re‑index documents after applying a new license?
  - answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
    question: What happens if I forget to close nodes?
  - answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
    question: Is it possible to add more than one custom attribute per document?
  type: FAQPage
title: Tijdelijke licentie verkrijgen voor GroupDocs – Master Search Nodes (Java)
type: docs
url: /nl/java/search-network/master-groupdocs-search-java-network-nodes/
weight: 1
---

# Verkrijg Tijdelijke Licentie GroupDocs – Master Search Nodes (Java)

In deze uitgebreide gids **verkrijgt u een tijdelijke licentie voor GroupDocs.Search**, configureert u een multi‑node zoeknetwerk, en leert u hoe u **mappen aan de index toevoegt** en **aangepaste documentattributen toevoegt** met Java. Of u nu een enterprise document‑managementsysteem of een doorzoekbare productcatalogus bouwt, het beheersen van deze stappen stelt u in staat het platform zonder beperkingen te evalueren en uw zoekmogelijkheden snel te schalen.

## Snelle Antwoorden
- **Wat is de eerste stap om GroupDocs.Search te gaan gebruiken?** Verkrijg een tijdelijke licentie via het GroupDocs‑portaal.  
- **Welke Maven-repository host de bibliotheek?** `https://releases.groupdocs.com/search/java/`.  
- **Hoe voeg ik mappen toe aan de index?** Roep de `addDirectoriesToIndex` helper aan op de master‑node.  
- **Kan ik aangepaste documentattributen toevoegen?** Ja—roep `addAttribute` aan met de document‑sleutel en attribuutnaam.  
- **Hoe sluit ik knooppunten netjes af?** Roep `closeNodes` aan om bronnen vrij te geven.

## Wat is een tijdelijke licentie en waarom heb ik die nodig?
Een tijdelijke licentie stelt u in staat GroupDocs.Search te evalueren zonder beperkingen. Het is perfect voor ontwikkeling, testen of proof‑of‑conceptprojecten voordat u een volledige aankoop doet. De licentie verleent volledige functionaliteit voor een beperkte periode, waardoor u de prestaties kunt benchmarken, integratiepunten kunt testen en kunt verzekeren dat de oplossing aan uw eisen voldoet zonder financiële verplichting.

## Voorvereisten

Voordat we beginnen, zorg ervoor dat u de volgende voorvereisten heeft:

### Vereiste Bibliotheken en Afhankelijkheden
Om met GroupDocs.Search voor Java te werken, neem de benodigde Maven‑afhankelijkheden op:
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
U kunt de nieuwste versie ook direct downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Omgevingsconfiguratie
- Zorg ervoor dat u een compatibele JDK geïnstalleerd heeft (Java 8 of later).  
- Stel uw IDE in om Maven‑projecten te ondersteunen.

### Kennisvoorvereisten
Een basisbegrip van Java‑programmeren en vertrouwdheid met Maven‑projectbeheer is nuttig. Als u nieuw bent met deze concepten, overweeg dan om introductiematerialen te verkennen om te beginnen.

## Hoe een tijdelijke licentie te verkrijgen
Een tijdelijke licentie verkrijgt u door de GroupDocs‑portal te bezoeken, een kort aanvraagformulier in te vullen en het ontvangen `.lic`‑bestand in de `resources`‑map van uw project te plaatsen. Initialiseert vervolgens de licentie met een paar regels code (zie de codefragment hieronder). Gebruik voor het aanvraagformulier de officiële pagina: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## GroupDocs.Search voor Java Instellen

### Installatie‑informatie
Om GroupDocs.Search voor Java in uw project te gebruiken, volgt u de bovenstaande Maven‑stappen of downloadt u de nieuwste versie direct van de officiële releases‑pagina.

#### Stappen voor Licentie‑verwerving
1. **Gratis proefversie** – Verken de functies zonder enige verplichting.  
2. **Tijdelijke licentie** – Verkrijg een kort‑lopende sleutel voor testen (zie de sectie hierboven).  
3. **Aankoop** – Voor productiegebruik koopt u een volledige licentie via de **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Basisinitialisatie en Configuratie
Initialiseer uw project met GroupDocs.Search als volgt:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
Deze initialisatiestap is cruciaal om te garanderen dat alle componenten naadloos functioneren binnen uw zoeknetwerk.

## Implementatiegids

Laten we nu het proces opdelen in beheersbare secties, elk gericht op een specifieke functie van het implementeren en beheren van zoeknetwerkknooppunten.

### Functie 1: Configuratie‑instelling
**Overzicht:** Het instellen van de configuratie voor uw zoeknetwerk is de eerste stap bij het implementeren van knooppunten. Deze instelling omvat het specificeren van paden en poorten die cruciaal zijn voor de implementatie van knooppunten.

#### Implementatiestappen:
##### Stap 1: Definieer Basispad en Poort
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Stap 2: Configureer Zoeknetwerk
De functie `configureSearchNetwork` bereidt het configuratie‑object voor dat nodig is voor het implementeren van knooppunten.  
`Configuration` is een klasse die alle instellingen bevat, zoals indexmap, netwerkpoorten en knooppuntrollen.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameters:** Het basispad en de poort worden gebruikt om bronnen te lokaliseren en communicatielijnen op te zetten.  
- **Returnwaarde:** Een geconfigureerd `Configuration`‑object dat is afgestemd op uw implementatiebehoeften.

### Functie 2: Implementatie van Zoeknetwerk
**Overzicht:** Het implementeren van knooppunten is essentieel om uw zoekmogelijkheden te schalen over verschillende omgevingen of datasegmenten.

#### Implementatiestappen:
##### Stap 1: Implementeer Knooppunten
De functie `deploySearchNetwork` initialiseert en retourneert een array van zoeknetwerkknooppunten.  
`SearchNetworkNodes` vertegenwoordigt elke knooppunt‑instantie die deelneemt aan de gedistribueerde zoekcluster.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameters:** Basispad, poort en configuratie worden gebruikt om de implementatie‑omgeving te bepalen.  
- **Returnwaarde:** Een array met geïnitialiseerde `SearchNetworkNodes`.

### Functie 3: Abonneren op Netwerkevenementen
**Overzicht:** Het monitoren van de activiteiten van uw zoeknetwerk is cruciaal voor het behouden van optimale prestaties en betrouwbaarheid.

#### Implementatiestappen:
##### Stap 1: Abonneer op Master‑Node‑Evenementen
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Doel:** Deze stap zorgt ervoor dat u op de hoogte wordt gesteld van belangrijke gebeurtenissen of wijzigingen binnen uw zoeknetwerk.

### Functie 4: Documenten Indexeren
**Overzicht:** Het toevoegen van mappen met documenten die geïndexeerd moeten worden, maakt efficiënte gegevensopvraging over uw netwerk mogelijk.

#### Hoe mappen aan de index toe te voegen
`addDirectoriesToIndex` is een helper‑methode die mappaden registreert voor indexering op de master‑node.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Doel:** Faciliteert snelle toegang en doorzoekbaarheid van alle documenten binnen de opgegeven mappen.

### Functie 5: Attributen aan Documenten Toevoegen
**Overzicht:** Aangepaste attributen verrijken de documentmetadata, waardoor zoekopdrachten flexibeler en informatiever worden.

#### Hoe aangepaste documentattributen toe te voegen
`addAttribute` voegt een aangepast metadata‑attribuut toe aan een opgegeven document in de index.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameters:** Specificeer de node, document‑sleutel en attribuut dat moet worden toegevoegd.  
- **Doel:** Breidt de zoekfunctionaliteit uit door documenten te verrijken met extra metadata.

### Functie 6: Ophalen van Geïndexeerde Documenten
**Overzicht:** Haal efficiënt geïndexeerde documenten op en lijst ze op om datanauwkeurigheid en volledigheid te waarborgen.

#### Implementatiestappen:
##### Stap 1: Haal Geïndexeerde Documenten Op
```java
getIndexedDocuments(nodes[0]);
```  
- **Doel:** Verifieert de succesvolle indexering van alle benodigde documenten binnen uw zoeknetwerk.

### Functie 7: Netwerkknooppunten Sluiten
**Overzicht:** Het correct afsluiten van knooppunten is cruciaal voor resource‑beheer en het voorkomen van geheugenlekken.

#### Implementatiestappen:
##### Stap 1: Sluit Alle Knooppunten
`closeNodes` sluit alle actieve zoekknooppunten af en geeft toegewezen resources vrij.  
```java
closeNodes(nodes);
```  
- **Doel:** Geeft de door elk knooppunt bezette resources vrij, waardoor een nette afsluitprocedure wordt gegarandeerd.

## Waarom een tijdelijke licentie gebruiken voor GroupDocs.Search?
Een tijdelijke licentie biedt **volledige functionaliteit voor 30 dagen** en ondersteunt tot **50.000 geïndexeerde documenten** zonder prestatiebeperking. Hiermee kunt u de indexeringssnelheid, query‑latentie en schaalbaarheid op real‑world data benchmarken voordat u een productielicentie aanschaft. Het verwijdert ook evaluatiewatermerken, waardoor u een echte weergave krijgt van de mogelijkheden van het eindproduct.

## Veelvoorkomende Gebruikssituaties
1. **Enterprise Document Management** – Index miljoenen interne bestanden over afdelingen heen, waardoor directe full‑text zoekopdrachten mogelijk zijn.  
2. **E‑commerce Platforms** – Bouw een doorzoekbare productcatalogus die zich uitstrekt over meerdere magazijnen en externe feeds.  
3. **Legal Firms** – Organiseer dossiers, contracten en bewijsmateriaal met aangepaste metadata voor snelle opvraging.

Integratiemogelijkheden met andere systemen omvatten CRM‑platformen, content‑managementsystemen (CMS) en data‑analytics‑tools, waarbij gebruik wordt gemaakt van de robuuste indexerings‑ en zoekfuncties die GroupDocs.Search voor Java biedt.

## Prestatie‑overwegingen
Om de prestaties te optimaliseren bij het gebruik van GroupDocs.Search voor Java:
- **Configureer Optimaliseren** – Pas uw configuratie‑instellingen aan op uw specifieke implementatie‑omgeving.  
- **Resourcegebruik Monitoren** – Controleer regelmatig CPU, geheugen en I/O om knelpunten of geheugenlekken te voorkomen.  
- **Beste Praktijken Volgen** – Houd u aan de Java‑geheugenbeheer‑richtlijnen, zodat systeemresources efficiënt worden benut.

## Veelgestelde Vragen

**Q: Hoe lang blijft een tijdelijke licentie geldig?**  
A: Tijdelijke licenties zijn doorgaans 30 dagen geldig, waardoor u voldoende tijd heeft om het product te evalueren.

**Q: Kan ik van een tijdelijke naar een volledige licentie overschakelen zonder opnieuw te installeren?**  
A: Ja—vervang het tijdelijke licentiebestand door het volledige licentiebestand en herstart uw applicatie.

**Q: Moet ik documenten opnieuw indexeren na het toepassen van een nieuwe licentie?**  
A: Nee, de index blijft intact; de licentie regelt alleen de gebruiksrechten.

**Q: Wat gebeurt er als ik vergeet knooppunten te sluiten?**  
A: Niet‑gerelease resources kunnen leiden tot geheugenlekken; roep altijd `closeNodes` aan tijdens het afsluiten.

**Q: Is het mogelijk om meer dan één aangepast attribuut per document toe te voegen?**  
A: Absoluut—roep `addAttribute` meerdere keren aan met verschillende attribuutnamen.

**Last Updated:** 2026-07-02  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs

## Gerelateerde Tutorials

- [Een Zoeknetwerk‑knooppunt implementeren in .NET met GroupDocs voor efficiënte documentindexering en -opvraging](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [Hoe een Zoeknetwerk te implementeren met GroupDocs.Search in .NET voor Document Management Systemen](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Aspose.Search Netwerk configureren & Documentattributen toevoegen met GroupDocs.Redaction voor .NET: Een uitgebreide gids](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
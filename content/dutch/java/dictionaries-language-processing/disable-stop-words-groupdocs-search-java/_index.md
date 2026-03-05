---
date: '2026-02-19'
description: Leer hoe u stopwoorden bij zoeken kunt uitschakelen en documenten aan
  de index kunt toevoegen met GroupDocs.Search voor Java, waardoor de nauwkeurigheid
  van zoekopdrachten wordt verhoogd.
keywords:
- add documents to index
- disable stop words java
- configure index settings
title: 'Stopwoorden in zoeken: documenten toevoegen aan index met GroupDocs.Search
  Java'
type: docs
url: /nl/java/dictionaries-language-processing/disable-stop-words-groupdocs-search-java/
weight: 1
---

# Stopwoorden in zoeken: documenten toevoegen aan index met GroupDocs.Search Java

Als je **documenten aan de index wilt toevoegen** terwijl je ervoor zorgt dat geen belangrijke term—vooral veelvoorkomende—wordt genegeerd, ben je op de juiste plek. In deze gids laten we je zien hoe je **stopwoorden in zoeken kunt uitschakelen** met GroupDocs.Search voor Java, zodat elk token (zelfs “on”, “by” of “the”) doorzoekbaar wordt en je resultaten veel nauwkeuriger zijn.

## Snelle antwoorden
- **Wat betekent “documenten aan de index toevoegen”?** Het betekent dat je je bronbestanden laadt in een doorzoekbare index zodat ze efficiënt kunnen worden bevraagd.  
- **Waarom zou ik stopwoorden uitschakelen?** Om veelvoorkomende woorden (bijv. “on”, “the”) op te nemen in zoekopdrachten wanneer die termen betekenisvol zijn voor jouw domein.  
- **Welke bibliotheekversie is vereist?** GroupDocs.Search voor Java 25.4 of later.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een permanente licentie is vereist voor productie.  
- **Kan ik dit gebruiken in een Maven‑project?** Ja – voeg gewoon de repository en afhankelijkheid toe zoals hieronder weergegeven.

## Wat zijn stopwoorden in zoeken en waarom zou je ze willen uitschakelen?
Stopwoorden zijn veelvoorkomende termen die veel zoekmachines automatisch filteren om query's te versnellen. Hoewel dit de prestaties verbetert voor algemene webzoekopdrachten, kan het de precisie schaden in gespecialiseerde domeinen—juridische contracten, e‑commerce catalogi of technische handleidingen—waar woorden zoals “on”, “by” of “as” een echte betekenis hebben. Het uitschakelen van stopwoorden laat je elk woord als significant behandelen, waardoor geen relevant document wordt gemist.

## Hoe werkt het toevoegen van documenten aan de index in GroupDocs.Search?
Wanneer je documenten toevoegt, leest de bibliotheek elk bestand, tokeniseert de inhoud en slaat de tokens op in een geoptimaliseerde datastructuur (de index). Eenmaal geïndexeerd kan de engine overeenkomende documenten in milliseconden ophalen, zelfs voor grote collecties.

## Voorwaarden

- **Vereiste bibliotheken**: GroupDocs.Search voor Java 25.4 (of nieuwer).  
- **Ontwikkelomgeving**: IntelliJ IDEA, Eclipse, of elke Java‑IDE die je verkiest.  
- **Basiskennis**: Vertrouwdheid met Java‑syntaxis en het concept van indexeren.

## GroupDocs.Search voor Java instellen

### Maven‑installatie

Als je Maven gebruikt, voeg dan het volgende toe aan je `pom.xml`:

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

### Directe download

Download anders de nieuwste versie van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Stappen voor licentie‑acquisitie
- **Gratis proefversie** – begin meteen met testen.  
- **Tijdelijke licentie** – verkrijg een tijdelijk sleutel voor volledige functionaliteit.  
- **Aankoop** – zorg voor een permanente licentie voor productiegebruik.

## Basisinitialisatie en -configuratie

Maak een instantie van `IndexSettings` aan om te bepalen hoe de index zich gedraagt:

```java
import com.groupdocs.search.IndexSettings;

// Create an instance of IndexSettings
IndexSettings settings = new IndexSettings();
```

## Hoe stopwoorden uitschakelen in zoeken (Java)

De volgende regel schakelt de ingebouwde stop‑woordfilter uit:

```java
// Disable the use of stop words
tsettings.setUseStopWords(false);
```

*Parameters*: `setUseStopWords` accepteert een boolean.  
*Doel*: Garandeert dat elk woord—incl. veelvoorkomende stopwoorden—geïndexeerd en doorzoekbaar is.

## Hoe documenten aan de index toevoegen

### De uitvoermap definiëren

```java
import com.groupdocs.search.Index;

// Define the path to the output directory for indexing
String indexFolder = "YOUR_OUTPUT_DIRECTORY\\IndexingWithStopWords";

// Create an index at the specified location with the configured settings
Index index = new Index(indexFolder, settings);
```

### De documentmap opgeven

```java
// Define the path to your document directory
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in the specified folder to the index
index.add(documentsFolder);
```

Nu wordt elk bestand in `YOUR_DOCUMENT_DIRECTORY` **documenten aan de index toegevoegd** en is klaar voor query's.

## Een zoekopdracht uitvoeren

```java
import com.groupdocs.search.results.SearchResult;

// Define your search query
tString query = "on";

// Perform the search operation using the index and the specified query
SearchResult result = index.search(query);
```

Omdat stopwoorden zijn uitgeschakeld, wordt de term "on" meegenomen tijdens de zoekopdracht, waardoor overeenkomsten worden geretourneerd die anders genegeerd zouden worden.

## Praktische toepassingen

1. **Enterprise Document Search** – Zorg ervoor dat kritieke terminologie niet wordt gefilterd.  
2. **E‑commerce Platforms** – Verbeter productontdekking door elk woord in productbeschrijvingen te indexeren.  
3. **Legal Research Tools** – Leg elk juridisch term vast, zelfs diegene die gewoonlijk als stopwoorden worden behandeld.

## Prestatieoverwegingen

- **Optimalisatietips**: Werk je index regelmatig bij en snoei deze om de zoekprestaties hoog te houden.  
- **Resourcegebruik**: Houd de JVM‑heapgrootte in de gaten; grote indexen kunnen afstemming van de garbage‑collection‑instellingen vereisen.  
- **Java‑geheugenbeheer**: Gebruik efficiënte datastructuren en overweeg off‑heap opslag voor zeer grote corpora.

## Veelvoorkomende problemen en oplossingen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|---|---|---|
| Geen resultaten voor veelvoorkomende woorden | `setUseStopWords(true)` (standaard) | Roep `setUseStopWords(false)` aan zoals hierboven getoond. |
| Out‑of‑memory‑fouten tijdens indexeren | Te veel grote bestanden tegelijk indexeren | Indexeer bestanden in batches; vergroot de `-Xmx` JVM‑optie. |
| Zoekopdracht geeft verouderde data terug | Index niet ververst na het toevoegen van nieuwe bestanden | Roep `index.update()` aan of voeg de gewijzigde documenten opnieuw toe. |

## Veelgestelde vragen

**Q: Wat zijn stopwoorden?**  
A: Stopwoorden zijn veelvoorkomende termen (bijv. “the”, “is”, “on”) die veel zoekmachines negeren om query's te versnellen. Het uitschakelen ervan laat je elk token als doorzoekbaar behandelen.

**Q: Waarom stopwoorden uitschakelen in zoekindexen?**  
A: Wanneer exacte zinsnede‑matching vereist is—zoals in juridische of technische documenten—draagt elk woord betekenis, dus moet je stopwoorden opnemen.

**Q: Hoe gaat GroupDocs.Search om met grote datasets?**  
A: De bibliotheek gebruikt geoptimaliseerde datastructuren en incrementeel indexeren om het geheugenverbruik laag te houden, zelfs bij miljoenen documenten.

**Q: Kan ik GroupDocs.Search integreren met andere Java‑applicaties?**  
A: Ja, de API is ontworpen voor eenvoudige integratie in elk Java‑gebaseerd systeem, van webservices tot desktop‑apps.

**Q: Wat moet ik doen als mijn zoekresultaten niet nauwkeurig zijn?**  
A: Controleer of de index alle benodigde documenten bevat (`documenten aan de index toevoegen`), zorg ervoor dat stop‑woordfiltering is uitgeschakeld indien nodig, en overweeg de index opnieuw op te bouwen na grote wijzigingen.

## Aanvullende bronnen

- **Documentatie**: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)
- **API‑referentie**: [GroupDocs API Reference](https://reference.groupdocs.com/search/java)
- **Download**: [Get the latest GroupDocs.Search for Java](https://releases.groupdocs.com/search/java/)
- **GitHub‑repository**: [Explore on GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Gratis ondersteuning**: [Join GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Tijdelijke licentie**: [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

Door deze gids te volgen, weet je nu hoe je **documenten aan de index toevoegt** en **stopwoorden in zoeken uitschakelt** om nauwkeurigere resultaten te leveren in je Java‑applicaties.

---

**Laatst bijgewerkt:** 2026-02-19  
**Getest met:** GroupDocs.Search voor Java 25.4  
**Auteur:** GroupDocs
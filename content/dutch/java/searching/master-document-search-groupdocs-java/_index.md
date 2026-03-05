---
date: '2026-02-06'
description: Leer hoe u documenten indexeert en documenten aan de index toevoegt met
  GroupDocs.Search voor Java. Bouw krachtige zoekapplicaties met tekst‑ en objectquery’s.
keywords:
- GroupDocs.Search Java
- document indexing in Java
- Java document search
title: Hoe documenten indexeren met GroupDocs.Search voor Java
type: docs
url: /nl/java/searching/master-document-search-groupdocs-java/
weight: 1
---

# Hoe documenten indexeren met GroupDocs.Search voor Java

In de hedendaagse data‑gedreven wereld is **hoe documenten te indexeren** efficiënt een cruciale vaardigheid voor elke Java‑ontwikkelaar die met grote collecties bestanden werkt. Of je nu juridische contracten, financiële overzichten of interne rapporten verwerkt, het kunnen snel vinden van de juiste informatie kan uren handmatig werk besparen. In deze tutorial leer je **hoe documenten te indexeren** met behulp van de GroupDocs.Search‑bibliotheek, en vervolgens zowel tekst‑gebaseerde als object‑gebaseerde queries op de aangemaakte index uit te voeren. Laten we beginnen!

## Snelle antwoorden
- **Wat is de eerste stap om documenten te indexeren?** Initialiseer een `Index`‑object dat naar een map wijst waar de index wordt opgeslagen.  
- **Welke methode voegt documenten toe aan een index?** Gebruik `index.add("PATH_TO_DOCUMENTS")`.  
- **Kan ik numerieke bereiken zoeken?** Ja, met een tekstquery zoals `"400 ~~ 4000"` of een objectquery via `SearchQuery.createNumericRangeQuery`.  
- **Heb ik een licentie nodig?** Een gratis proefversie is beschikbaar; een commerciële licentie ontgrendelt alle functies.  
- **Welke Java‑versie is vereist?** JDK 8 of hoger.

## Wat is “hoe documenten te indexeren” met GroupDocs.Search?
Documenten indexeren betekent het scannen van de inhoud van bestanden in een map en het opslaan van doorzoekbare tokens in een speciale indexmap. Deze pre‑processing stap maakt razendsnelle zoekopdrachten later mogelijk, omdat de bibliotheek de voorbereide index doorzoekt in plaats van elke keer de ruwe bestanden.

## Waarom GroupDocs.Search voor Java gebruiken?
- **Prestaties:** Zoekopdrachten worden uitgevoerd in milliseconden, zelfs bij duizenden bestanden.  
- **Formaatondersteuning:** Verwerkt PDF's, Word, Excel, PowerPoint en nog veel meer.  
- **Flexibiliteit:** Ondersteunt plain‑text queries, numerieke bereiken en complexe objectqueries.  
- **Schaalbaarheid:** Werk de index eenvoudig bij door nieuwe documenten toe te voegen zonder de index opnieuw te bouwen.

## Vereisten
- Maven geïnstalleerd voor dependency‑beheer.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Basiskennis van Java (OOP‑concepten, exception handling).  

## GroupDocs.Search voor Java instellen
### Maven‑configuratie
Voeg de repository en afhankelijkheid toe aan je `pom.xml`:

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
Je kunt ook de nieuwste JAR downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Stappen voor het verkrijgen van een licentie
1. **Gratis proefversie** – verken de bibliotheek zonder kosten.  
2. **Tijdelijke licentie** – vraag een kort‑lopende sleutel aan voor uitgebreide evaluatie.  
3. **Aankoop** – verkrijg een volledige licentie voor productiegebruik.

## Basisinitialisatie en configuratie
Om **documenten toe te voegen aan de index**, maak je eerst een `Index`‑object aan dat naar de map wijst waar de indexbestanden worden opgeslagen:

```java
import com.groupdocs.search.Index;

// Initialize the index by specifying a directory path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");
```

Deze regel maakt (of opent) een index die klaar is om documenten te ontvangen.

## Implementatie‑gids
### Documenten maken en indexeren
#### Hoe documenten toe te voegen aan de index
De `add`‑methode scant een map en slaat doorzoekbare gegevens op voor elk bestand.

```java
import com.groupdocs.search.Index;

// Initialize an index at the specified path
Index index = new Index("YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\NumericRangeSearch");

// Add documents from a directory for indexing
index.add("YOUR_DOCUMENT_DIRECTORY");
```

- **Parameters:** De pad‑string wijst naar de map die de bestanden bevat die je wilt indexeren.  
- **Doel:** Na deze stap bevat de index tokens van alle ondersteunde documenttypes, waardoor snelle zoekopdrachten mogelijk zijn.

### Tekst‑query zoeken
#### Hoe een tekst‑gebaseerde numerieke bereikzoekopdracht uit te voeren
Je kunt zoeken met een eenvoudige tekenreeks die een bereik definieert.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Define a query for numeric values within a specific range
String query1 = "400 ~~ 4000";

// Execute text-based search on indexed data
SearchResult result1 = index.search(query1);
```

- **Parameters:** De query‑string `"400 ~~ 4000"` vertelt de engine om nummers tussen 400 en 4000 te vinden.  
- **Returnwaarde:** `SearchResult` bevat de lijst met overeenkomende documenten en markeringen.

### Object‑query zoeken
#### Hoe een object‑query te gebruiken voor numerieke bereiken
Object‑gebaseerde queries geven je programmatische controle over zoekcriteria.

```java
import com.groupdocs.search.*;
import com.groupdocs.search.results.*;

// Create a numeric range query object
SearchQuery query2 = SearchQuery.createNumericRangeQuery(400, 4000);

// Perform search using the query object
SearchResult result2 = index.search(query2);
```

- **Parameters:** `createNumericRangeQuery` ontvangt de start‑ en eind‑integers.  
- **Doel:** Deze methode is ideaal wanneer je meerdere voorwaarden wilt combineren of queries dynamisch wilt opbouwen.

## Praktische toepassingen
Hier zijn enkele praktijkvoorbeelden waarbij **hoe documenten te indexeren** een doorslaggevende factor wordt:

1. **Beheer van juridische documenten** – vind clausules, zaaknummers of data in duizenden contracten.  
2. **Financiële rapportage** – haal transacties op die binnen een specifiek geldbedrag vallen.  
3. **Voorraadbeheer** – vind items op serienummers, batchcodes of SKU‑bereiken.  

Het integreren van GroupDocs.Search met databases, cloudopslag of berichtqueues kan documentworkflows verder automatiseren.

## Prestatie‑overwegingen
- **Regelmatige indexupdates:** Voer `index.add` opnieuw uit voor nieuwe bestanden om de index actueel te houden.  
- **Resource‑beheer:** Houd het heap‑gebruik in de gaten; grote indexen profiteren van geoptimaliseerde JVM‑garbage‑collection‑instellingen.  
- **Query‑optimalisatie:** Gebruik objectqueries voor complexe filters om onnodig scannen te verminderen.

## Veelvoorkomende problemen en oplossingen
| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Search returns no results** | Index niet gebouwd of mappad onjuist | Controleer of `index.add` is uitgevoerd op de juiste directory en of de indexmap schrijfbaar is. |
| **OutOfMemoryError during indexing** | Zeer grote bestanden of onvoldoende heap | Verhoog de JVM `-Xmx`‑waarde of indexeer bestanden in kleinere batches. |
| **Unsupported file format** | Bestandstype niet herkend door GroupDocs.Search | Zorg ervoor dat de bestandsextensie voorkomt in de ondersteunde lijst (PDF, DOCX, XLSX, etc.). |

## Veelgestelde vragen
**V: Hoe werk ik een bestaande index bij met nieuwe documenten?**  
A: Roep `index.add("NEW_DOCUMENT_PATH")` opnieuw aan; de bibliotheek voegt nieuwe items samen zonder de hele index opnieuw te maken.

**V: Kan GroupDocs.Search verschillende bestandsformaten aan?**  
A: Ja, het ondersteunt PDF's, Word, Excel, PowerPoint, platte tekst en vele andere gangbare formaten.

**V: Wat zijn de systeemvereisten voor het gebruik van GroupDocs.Search?**  
A: Java 8+ runtime, voldoende RAM (minimaal 2 GB voor middelgrote collecties) en lees‑/schrijftoegang tot de indexmap.

**V: Hoe kan ik zoek‑prestatieproblemen oplossen?**  
A: Zorg ervoor dat de index up‑to‑date is, profileer je queries en controleer de JVM‑geheugeninstellingen. Het verminderen van het aantal geïndexeerde velden kan de snelheid ook verbeteren.

**V: Is er een manier om te zoeken met synoniemen of fuzzy matching?**  
A: Ja, GroupDocs.Search biedt synoniemdictionaries en fuzzy‑zoekopties die via de `SearchOptions`‑klasse kunnen worden ingeschakeld.

## Conclusie
Je hebt nu een solide begrip van **hoe documenten te indexeren** met GroupDocs.Search voor Java, hoe **documenten toe te voegen aan de index**, en hoe zowel tekst‑gebaseerde als object‑gebaseerde queries uit te voeren. Door deze technieken te integreren, zullen je Java‑applicaties snelle, nauwkeurige zoekervaringen bieden over elke documentrepository.

Klaar voor de volgende stap? Verken gefacetteerd zoeken, synoniem‑verwerking, of integreer de index met een REST‑API om zoekfunctionaliteit beschikbaar te maken voor andere services.

---

**Laatst bijgewerkt:** 2026-02-06  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs
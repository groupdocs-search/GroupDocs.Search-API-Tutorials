---
date: '2026-02-24'
description: Leer hoe u een aangepaste logger maakt, de maximale loggrootte instelt
  en een console‑ of bestandslogger configureert in GroupDocs.Search voor Java.
keywords:
- GroupDocs.Search for Java
- file logger implementation
- custom loggers
title: Hoe een aangepaste logger te maken en de logbestandsgrootte te beperken met
  GroupDocs.Search Java
type: docs
url: /nl/java/exception-handling-logging/groupdocs-search-java-file-custom-loggers/
weight: 1
---

Let's translate.

Will produce final content.

# Beperk de grootte van logbestanden met GroupDocs.Search Java Loggers

In deze gids **maak je aangepaste logger**‑implementaties en leer je hoe je de **grootte van logbestanden kunt beperken** tijdens het gebruik van GroupDocs.Search voor Java. Het beheersen van loggroei is cruciaal voor grootschalige documentindexering, en de ingebouwde loggers laten je **maximale loggrootte instellen**, **logbestand roteren**, of overschakelen naar een **gebruik console logger** voor directe feedback. Laten we de volledige configuratie doorlopen, van Maven‑instelling tot het uitvoeren van een zoekquery, en zien hoe je **documenten aan de index toevoegt** met de logger in place.

## Snelle antwoorden
- **Wat betekent “grootte van logbestand beperken”?** Het stelt een maximale grootte van een logbestand in, waardoor ongecontroleerde groei op de schijf wordt voorkomen.  
- **Welke logger laat je de grootte van het logbestand beperken?** De ingebouwde `FileLogger` accepteert een max‑size‑parameter.  
- **Hoe gebruik ik console logger java?** Instantieer `ConsoleLogger` en stel deze in op `IndexSettings`.  
- **Heb ik een licentie nodig voor GroupDocs.Search?** Een proefversie werkt voor evaluatie; een commerciële licentie is vereist voor productie.  
- **Wat is de eerste stap?** Voeg de GroupDocs.Search‑dependency toe aan je Maven‑project.  

## Wat betekent het beperken van de grootte van een logbestand?
Het beperken van de grootte van een logbestand betekent dat je de logger zo configureert dat, zodra het bestand een vooraf gedefinieerde drempel bereikt (bijv. 4 MB), het niet meer groeit of rolt. Dit houdt de opslagvoetafdruk van je applicatie voorspelbaar en voorkomt prestatie‑degradatie.

## Waarom bestanden‑ en aangepaste loggers gebruiken met GroupDocs.Search?
- **Auditability:** Houd een permanent register bij van index‑ en zoekgebeurtenissen.  
- **Debugging:** Lokaliseer snel problemen door beknopte logs te bekijken.  
- **Flexibility:** Kies tussen persistente bestandslogs en directe console‑output (`gebruik console logger`).  

## Vereisten
- **GroupDocs.Search for Java** ≥ 25.4.  
- JDK 8 of nieuwer, IDE (IntelliJ IDEA, Eclipse, enz.).  
- Basiskennis van Java en Maven.  

## GroupDocs.Search voor Java instellen

Voeg de bibliotheek toe aan je project met een van de onderstaande methoden.

**Maven‑instelling:**

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

**Direct downloaden:**  
Download de nieuwste JAR van de officiële site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
Vraag een proeflicentie aan of koop een licentie via de [licentiepagina](https://purchase.groupdocs.com/temporary-license/).

## Hoe maak je een aangepaste logger voor GroupDocs.Search
GroupDocs.Search stelt je in staat om elke implementatie van de `ILogger`‑interface in te pluggen. Door `FileLogger` of `ConsoleLogger` uit te breiden, kun je extra gedrag toevoegen — zoals het roteren van het logbestand of het doorsturen van berichten naar een externe bewakingsservice. Deze flexibiliteit is de reden waarom veel teams **aangepaste logger**‑oplossingen creëren die passen bij hun operationele behoeften.

## Hoe de grootte van een logbestand beperken met File Logger
Hieronder vind je een stap‑voor‑stap‑gids die laat zien hoe je de **file logger** configureert zodat het logbestand nooit groter wordt dan de door jou opgegeven grootte.

### 1️⃣ Vereiste pakketten importeren
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.FileLogger;
```

### 2️⃣ Indexinstellingen configureren met File Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/IndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";
String logPath = "YOUR_OUTPUT_DIRECTORY/Log.txt";

IndexSettings settings = new IndexSettings();
settings.setLogger(new FileLogger(logPath, 4.0)); // 4 MB max size → limits log file size
```

### 3️⃣ De index maken of laden
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Documenten aan de index toevoegen
```java
index.add(documentsFolder);
```

### 5️⃣ Een zoekquery uitvoeren
```java
SearchResult result = index.search(query);
```

**Belangrijk punt:** Het tweede argument (`4.0`) van de `FileLogger`‑constructor definieert de **maximale loggrootte** in megabytes, waarmee direct wordt voldaan aan de eis om de **grootte van logbestand te beperken**.

## Hoe console logger java gebruiken
Als je directe feedback in de terminal wilt, vervang je de file logger door een console logger.

### 1️⃣ De Console Logger importeren
```java
import com.groupdocs.search.*;
import com.groupdocs.search.common.ConsoleLogger;
```

### 2️⃣ Indexinstellingen configureren met Console Logger
```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY/CustomLoggerIndexFolder";
String documentsFolder = Utils.DocumentsPath; // Directory containing documents
String query = "Lorem";

IndexSettings settings = new IndexSettings();
settings.setLogger(new ConsoleLogger()); // use console logger java
```

### 3️⃣ De index maken of laden
```java
Index index = new Index(indexFolder, settings);
```

### 4️⃣ Documenten toevoegen en een zoekopdracht uitvoeren
```java
index.add(documentsFolder);
SearchResult result = index.search(query);
```

**Tip:** De console logger is ideaal tijdens ontwikkeling omdat hij elke logvermelding onmiddellijk afdrukt, waardoor je kunt verifiëren dat indexeren en zoeken zich gedragen zoals verwacht.

## Praktische toepassingen
1. **Document Management Systems:** Houd audit‑trails bij van elk geïndexeerd document.  
2. **Enterprise Search Engines:** Monitor query‑prestaties en foutpercentages in realtime.  
3. **Legal & Compliance Software:** Registreer zoektermen voor wettelijke rapportage.

## Prestatie‑overwegingen
- **Loggrootte:** Door **maximale loggrootte in te stellen**, vermijd je overmatig schijfgebruik dat je applicatie kan vertragen.  
- **Asynchrone logging:** Als je een hogere doorvoersnelheid nodig hebt, overweeg dan de logger in een async‑queue te plaatsen (buiten de scope van deze gids).  
- **Geheugenbeheer:** Maak grote `Index`‑objecten vrij zodra ze niet meer nodig zijn om de JVM‑voetafdruk laag te houden.

## Veelvoorkomende problemen & oplossingen
- **Logpad niet toegankelijk:** Controleer of de map bestaat en of de applicatie schrijfrechten heeft.  
- **Logger wordt niet geactiveerd:** Zorg ervoor dat je `settings.setLogger(...)` *voordat* je het `Index`‑object maakt, aanroept.  
- **Console‑output ontbreekt:** Controleer of je de applicatie uitvoert in een terminal die `System.out` weergeeft.

## Veelgestelde vragen

**Q: Wat regelt de tweede parameter van `FileLogger`?**  
A: Hij stelt de maximale grootte van het logbestand in megabytes in, waardoor je de **maximale loggrootte kunt instellen**.

**Q: Kan ik file‑ en console‑loggers combineren?**  
A: Ja, door een aangepaste logger te maken die berichten naar beide bestemmingen doorstuurt.

**Q: Hoe voeg ik documenten toe aan de index na de initiële creatie?**  
A: Roep `index.add(pathToNewDocs)` op op elk moment; de logger registreert de bewerking.

**Q: Is `ConsoleLogger` thread‑safe?**  
A: Hij schrijft direct naar `System.out`, wat door de JVM gesynchroniseerd wordt, waardoor hij veilig is voor de meeste gebruikssituaties.

**Q: Heeft het beperken van de loggrootte invloed op de hoeveelheid opgeslagen informatie?**  
A: Zodra de limiet is bereikt, kunnen nieuwe vermeldingen worden weggegooid of kan het bestand **logbestand roteren**, afhankelijk van de logger‑implementatie.

## Resources
- [Documentation](https://docs.groupdocs.com/search/java/)
- [API Reference](https://reference.groupdocs.com/search/java/)

---

**Laatst bijgewerkt:** 2026-02-24  
**Getest met:** GroupDocs.Search for Java 25.4  
**Auteur:** GroupDocs  

---
---
date: '2026-09-11'
description: Leer hoe u zoekresultaten Java kunt markeren en documenten Java kunt
  indexeren met GroupDocs.Search voor Java met zowel synchronische als asynchrone
  indexering.
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: Markeer zoekresultaten Java met GroupDocs.Search. Leer synchronische
  en asynchrone indexering, real‑time-updates en het markeren van resultaten in Java-toepassingen.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: Markeer zoekresultaten Java – Snelle synchronische & async indexering
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: Markeer zoekresultaten Java – Synchronous & async indexering
type: docs
url: /nl/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Markeer zoekresultaten Java – Synchronous & async indexering

In deze gids ontdek je hoe je **highlight search results Java** gebruikt met de GroupDocs.Search‑bibliotheek, en zie je stap‑voor‑stap hoe je documenten Java zowel synchronisch als asynchroon indexeert. Of je nu een klein desktop‑hulpmiddel bouwt of een grootschalige enterprise‑zoekservice, deze technieken laten je instant, visueel duidelijke matches leveren zonder de toepassings‑threads te blokkeren.

## Snelle antwoorden
- **Wat betekent “highlight search results Java”?** Het betekent dat elke gevonden term in de geretourneerde fragmenten wordt omgeven met markup (bijv. `<mark>`) zodat gebruikers direct de context van de hit kunnen zien.  
- **Wanneer moet ik synchronische indexering gebruiken?** Gebruik het voor kleine‑tot‑middelgrote collecties waarbij je het document direct doorzoekbaar moet maken zodra het is toegevoegd.  
- **Wanneer is asynchrone indexering te verkiezen?** Kies dit voor grote batches of wanneer de UI‑thread responsief moet blijven terwijl de index op de achtergrond wordt opgebouwd.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een volledige licentie verwijdert limieten en ontgrendelt geavanceerde functies.  
- **Welke Java‑versie wordt ondersteund?** Java 8 of hoger.

## Wat is “highlight search results Java”?
`highlight search results java` is het proces waarbij ruwe match‑data van GroupDocs.Search worden genomen en visuele aanwijzingen—meestal HTML `<mark>`‑tags—rond elke gevonden term worden geplaatst. Dit maakt de resultaatsfragmenten direct leesbaar in een webpagina of Swing‑component, waardoor de gebruikerservaring verbetert doordat precies wordt getoond waar de query voorkomt.

## Waarom GroupDocs.Search voor Java gebruiken?
GroupDocs.Search levert een high‑performance, taal‑agnostische engine die **tot 5 000 documenten per seconde kan verwerken**, **meer dan 30 bestandsformaten ondersteunt**, en **collecties van 10 miljoen documenten kan indexeren** zonder het volledige corpus in het geheugen te laden. De ingebouwde markering, realtime indexering en meertalige analyzers maken het ideaal voor content‑managementsystemen, e‑commerce catalogi en enterprise document repositories.

## Vereisten
- **Java Development Kit** (JDK 8 of nieuwer) geïnstalleerd en `JAVA_HOME` correct ingesteld.  
- Een IDE zoals **IntelliJ IDEA** of **Eclipse**.  
- Een map (bijv. `documents/`) met de bestanden die je wilt indexeren — platte tekst, PDF, DOCX, enz.  
- Maven voor dependency‑beheer (of je kunt handmatig de JAR toevoegen).

### Vereiste bibliotheken en afhankelijkheden
Add GroupDocs.Search to your Maven `pom.xml`:

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

Voor directe downloads, haal de nieuwste versie op van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Omgevingsconfiguratie
- Controleer of `JAVA_HOME` naar een compatibele JDK wijst.  
- Maak een nieuw Maven‑project aan en plak de bovenstaande snippet in de `<dependencies>`‑sectie.  
- Plaats voorbeeldbestanden in een map zoals `src/main/resources/documents/`.

## Hoe GroupDocs.Search voor Java in te stellen
`Index` is de kernklasse die een doorzoekbare collectie op schijf vertegenwoordigt.

Maak een `Index`‑instantie die naar een map op schijf wijst, pas een licentie toe als je er een hebt, en configureer eventueel een analyzer voor taalspecifieke tokenisatie. Deze voorbereidingsstap zorgt ervoor dat de engine de index efficiënt kan lezen, schrijven en doorzoeken.

De `Index`‑klasse is de kerncomponent die een doorzoekbare collectie op schijf vertegenwoordigt. Nadat je deze hebt geïnstantieerd, verlopen alle index‑ en query‑operaties via dit object.

1. **Installeer de bibliotheek** – Gebruik de Maven‑snippet hierboven of download de JAR van [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Verkrijg een licentie** – Begin met een proeflicentie; vervang deze door een productiesleutel vóór de uitrol.  
3. **Initialiseer de index** – De volgende snippet toont hoe je een indexmap maakt (of opent):

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Hoe zoekresultaten markeren Java – synchronische indexering
`DocumentHighlighter` is een hulpprogrammaklasse die gemarkeerde fragmenten genereert uit zoekresultaten.

Laad de index, voeg documenten toe met `index.add(documentPath)`, voer een query uit, en roep vervolgens `DocumentHighlighter` aan om matches te omhullen met `<mark>`‑tags. Het volledige proces draait op de aanroepende thread, zodat het document direct doorzoekbaar wordt zodra `add` terugkeert voor eindgebruikers.

### Stap 1: maak de index aan en voeg foutafhandeling toe
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Stap 2: voeg documenten toe en voer een zoekopdracht uit
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Stap 3: verwerk resultaten en markeer zoekresultaten Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## Hoe zoekresultaten markeren Java – asynchrone indexering
`IndexingOptions` configureert hoe het indexeringsproces draait, inclusief synchronische of asynchrone modus.

Configureer de `IndexingOptions` om in achtergrondmodus te draaien, abonneer je op `StatusChanged`‑events, en laat de engine bestanden indexeren terwijl je UI andere verzoeken blijft afhandelen. Zodra de status verandert naar `Ready`, kun je zoekopdrachten uitvoeren en gemarkeerde fragmenten verkrijgen, net als in synchronische modus.

De `AsyncIndexingListener` ontvangt voortgangsupdates, waardoor je een voortgangsbalk kunt tonen of de status kunt loggen zonder de hoofdthread te blokkeren.

### Stap 1: configureer de index met event‑listeners
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Stap 2: schakel asynchrone modus in en start de indexering
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## Hoe documenten indexeren Java – praktische tips
`index.update(path)` werkt een bestaand document in de index bij met het bestand op het opgegeven pad.

Verdeel grote collecties in batches van 1 000–5 000 bestanden, filter op extensie om onnodige parsing te vermijden, en gebruik `index.update(path)` voor gewijzigde bestanden in plaats van de hele index opnieuw op te bouwen. Deze praktijken houden het geheugenverbruik laag en de indexeringstijd voorspelbaar om consistentie te behouden.

- **Batchgrootte**: Voor enorme collecties, splits de map in kleinere batches om geheugenspikes te voorkomen.  
- **Bestandsfilters**: Gebruik `IndexingOptions.setFileExtensions` om alleen de formaten op te nemen die je nodig hebt (bijv. `.pdf`, `.docx`).  
- **Her‑indexeren**: Wanneer een document verandert, roep `index.update(documentPath)` aan in plaats van de index vanaf nul opnieuw te maken.

## Prestatieoverwegingen
- **Geheugen**: Monitor heap‑gebruik; verhoog `-Xmx` als je veel grote bestanden gelijktijdig verwerkt.  
- **CPU**: Asynchrone indexering verdeelt de werklast over threads maar verbruikt nog steeds CPU — volg het gebruik met JVisualVM.  
- **Resultaatmarkering**: Markering voegt een bescheiden overhead toe (≈ 2–5 ms per resultaat). Cache de gegenereerde HTML als je dezelfde fragmenten herhaaldelijk moet weergeven.

## Veelgestelde vragen

**Q: Kan ik synchronische en asynchrone indexering combineren in dezelfde applicatie?**  
A: Ja. Gebruik synchronische indexering voor kleine, vaak bijgewerkte sets en asynchrone indexering voor bulk‑import of achtergrondtaken.

**Q: Hoe pas ik de markeerstijl aan?**  
A: Lever een aangepaste `DocumentHighlighter`‑implementatie die de gewenste HTML-, CSS- of XML‑tags rond de gevonden termen schrijft.

**Q: Welke bestandstypen ondersteunt GroupDocs.Search standaard?**  
A: Tekst, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, en nog veel meer via ingebouwde parsers — meer dan 30 formaten in totaal.

**Q: Is het mogelijk om gelijktijdig in meerdere talen te zoeken?**  
A: Absoluut. GroupDocs.Search bevat meertalige analyzers; configureer gewoon de juiste `Analyzer` bij het aanmaken van de index.

**Q: Hoe beveilig ik de indexmap?**  
A: Bewaar de index in een beveiligde directory, stel strikte besturingssysteem‑rechten in, en versleutel eventueel de index met de beveiligingsfuncties van de bibliotheek.

---

**Laatst bijgewerkt:** 2026-09-11  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Hoe een documentindex te maken en documenten toe te voegen met de GroupDocs.Search API voor Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Hoe een indexrepository te maken in Java met GroupDocs.Search: Efficiënte documentindexering & zoeken](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [Efficiënte documentindexering zoeken Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)
---
date: '2026-06-27'
description: Stapsgewijze handleiding over hoe je een index maakt, tekst uit documenten
  extraheert en tekst naar een bestand uitvoert met GroupDocs.Search voor Java – de
  snelle Java-zoekbibliotheek.
keywords:
- how to create index
- extract text from documents
- output text to file
- add documents to index
- extract text to string
schemas:
- author: GroupDocs
  dateModified: '2026-06-27'
  description: Step‑by‑step guide on how to create index, extract text from documents
    and output text to file using GroupDocs.Search for Java – the fast java search
    library.
  headline: How to create index java with GroupDocs.Search for Java
  type: TechArticle
- questions:
  - answer: Yes, the library is pure Java and works seamlessly with any JVM language.
    question: Can I use GroupDocs.Search with other JVM languages like Kotlin or Scala?
  - answer: High compression reduces disk usage by up to 70 % and adds only a minimal
      CPU overhead during indexing; query latency remains under 100 ms for typical
      workloads.
    question: How does compression affect search speed?
  - answer: Absolutely. Use `index.add()` for new files and `index.remove()` to delete
      outdated ones, allowing incremental updates.
    question: Is it possible to update an existing index without rebuilding it?
  - answer: The `PlainText` result from the **structured text extraction** adapter
      provides clean, language‑agnostic content ideal for NLP tasks.
    question: Which output format is best for natural‑language‑processing pipelines?
  - answer: A free trial license suffices for development and evaluation; production
      deployments require a purchased license.
    question: Do I need a license for development and testing?
  type: FAQPage
title: Hoe een index te maken in Java met GroupDocs.Search voor Java
type: docs
url: /nl/java/performance-optimization/groupdocs-search-java-efficient-indexing-document-text-output/
weight: 1
---

# Beheersen van efficiënte documentzoekopdrachten met GroupDocs.Search voor Java

Finding the right passage inside thousands of PDFs, Word files, or spreadsheets can feel like searching for a needle in a haystack. **How to create index** quickly and retrieve that needle is what makes a document‑search solution valuable. In this tutorial you’ll learn how to use **GroupDocs.Search for Java**, a high‑performance java search library, to **create index**, **add documents to index**, and **extract text from documents** in multiple formats such as files, streams, strings, and structured data. By the end you’ll have a production‑ready indexing pipeline that scales to large document collections while keeping memory usage low.

## Snelle antwoorden
- **Wat is het primaire doel?** Om **how to create index** en documentinhoud onmiddellijk op te halen.  
- **Welke bibliotheek moet ik gebruiken?** De **GroupDocs.Search for Java** **java search library**.  
- **Kan ik tekst naar een bestand exporteren?** Ja – de bibliotheek biedt **output text to file** adapters voor HTML, platte tekst, en meer.  
- **Wordt gestructureerde extractie ondersteund?** Absoluut – gebruik de **structured text extraction** adapter om veld‑niveau gegevens te verkrijgen.  
- **Heb ik een licentie nodig?** Een proeflicentie werkt voor ontwikkeling; een permanente licentie is vereist voor productie‑implementaties.

## Wat je zult leren
- Hoe **how to create index** en **add documents to index** te gebruiken met GroupDocs.Search voor Java.  
- Technieken voor **output text to file**, streams, strings en gestructureerde formaten.  
- Prestaties‑optimalisatietips die indexeren snel en geheugen‑efficiënt houden.  
- Praktijkvoorbeelden waarin deze functies schitteren, zoals juridische‑contract repositories en academische‑paper archieven.

## Waarom GroupDocs.Search voor Java gebruiken?
GroupDocs.Search ondersteunt **50+ input and output formats** – inclusief DOCX, XLSX, PPTX, PDF, HTML en gangbare afbeeldingsformaten – en kan multi‑gigabyte bestanden indexeren zonder het volledige bestand in het geheugen te laden. Benchmarks tonen aan dat een collectie van 1 GB documenten in minder dan 2 minuten kan worden geïndexeerd op een standaard 8‑core server, terwijl zoekopdrachten resultaten teruggeven in minder dan 100 ms.

## Voorvereisten
- **Java Development Kit (JDK)** 8 of nieuwer.  
- **GroupDocs.Search for Java** bibliotheek (trial of gelicentieerd).  
- **Maven** voor afhankelijkheidsbeheer.  
- Basiskennis van Java I/O.

## GroupDocs.Search voor Java instellen
Voeg eerst de GroupDocs.Search Maven-repository en afhankelijkheid toe aan de `pom.xml` van je project. Deze stap zorgt ervoor dat de bibliotheek beschikbaar is op het classpath.

**Maven Setup**  
Voeg de volgende repository‑ en afhankelijkheidsconfiguraties toe in je `pom.xml` bestand:

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

Voor wie de voorkeur geeft aan een directe download, kun je de nieuwste versie verkrijgen via [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

**License Acquisition**  
Om GroupDocs.Search in productie te gebruiken, verkrijg een proef‑ of permanente licentie van de officiële site. De proeflicentie is onbeperkt voor ontwikkeling en testen.

## Hoe een index te maken in Java met aangepaste instellingen
`Index` is de kernklasse die een doorzoekbare collectie documenten vertegenwoordigt.  
`IndexSettings` configureert opties zoals compressie voor de index.  
`CompressionLevel` definieert de mate van compressie die op opgeslagen tekst wordt toegepast.

Laad het `Index`‑object met compressie ingeschakeld, wijs het op een map en voeg alle ondersteunde bestanden toe. Deze directe‑antwoord alinea vertelt precies wat te doen: instantiate `Index` met `new Index("indexFolder", new IndexSettings().setCompressionLevel(CompressionLevel.High))`, roep vervolgens `index.add("documentsFolder", true)` aan om recursief elke ondersteunde file te indexeren. De high‑compression modus verkleint de schijfgrootte tot 70 % terwijl de zoek‑snelheid snel blijft.

Het creëren van de index is de basis voor elke zoek‑gedreven applicatie. Het voorbeeld hieronder leidt je door het proces, legt elke instelling uit en toont hoe je kunt verifiëren dat de index succesvol is opgebouwd.

### Indexcreatie en documentindexering

#### Overzicht
De `Index`‑klasse is het kerncomponent dat een doorzoekbare collectie documenten vertegenwoordigt. Het slaat omgekeerde indexen, term‑woordenboeken en metadata op die nodig zijn voor snelle opzoekingen.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureIndexCreation {
    public static void main(String[] args) {
        // Define the folder paths for indexing
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY + "/DocumentsPath";  // Adjust as needed

        // Creating an index settings instance with compression enabled
        IndexSettings settings = new IndexSettings();
        settings.setTextStorageSettings(new TextStorageSettings(Compression.High));

        // Creating the index in the specified folder
        Index index = new Index(indexFolder, settings);

        // Adding documents from the specified folder to the index
        index.add(documentsFolder);
    }
}
```

**Uitleg**  
- **Index Settings**: We schakelen **high compression** in voor tekstopslag, optimaliseren het schijfruimtegebruik zonder de query‑snelheid te compromitteren.  
- **Adding Documents**: De `index.add()` methode **adds documents to index**, scant de map recursief en verwerkt automatisch alle ondersteunde formaten.

## Hoe tekst naar bestand, stream, string en gestructureerde formaten te exporteren
Na het indexeren moet je vaak de ruwe of opgemaakte tekst van een document extraheren. GroupDocs.Search biedt vier adapters waarmee je de geëxtraheerde inhoud naar een bestand, een in‑memory stream, een Java `String`, of een gestructureerd objectmodel kunt schrijven.

### Documenttekstuitvoer naar bestand

`FileOutputAdapter` schrijft de geëxtraheerde documenttekst naar een bestand in het gekozen formaat.

#### Overzicht
De `FileOutputAdapter` schrijft de geëxtraheerde tekst in het gekozen formaat (HTML, platte tekst, enz.) direct naar een bestand op schijf. Dit is nuttig voor het genereren van mens‑leesbare rapporten of het voeden van downstream verwerkings‑pijplijnen.

```java
import com.groupdocs.search.*;

public class FeatureOutputToFile {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to an HTML file
            FileOutputAdapter fileOutputAdapter = new FileOutputAdapter(OutputFormat.Html, YOUR_OUTPUT_DIRECTORY + "/Text.html");
            index.getDocumentText(document, fileOutputAdapter);
        }
    }
}
```

**Uitleg**  
- **FileOutputAdapter**: Converteert de tekst van het geïndexeerde document naar HTML en schrijft deze naar het opgegeven bestandspad, waarbij basisopmaak zoals koppen en tabellen behouden blijft.

### Documenttekstuitvoer naar stream

`StreamOutputAdapter` streamt de geëxtraheerde documenttekst naar een `ByteArrayOutputStream` zonder een tijdelijk bestand te maken.

#### Overzicht
Wanneer je de inhoud slechts tijdelijk nodig hebt—bijv. om het via HTTP te verzenden of in een webrespons in te sluiten—gebruik dan de `StreamOutputAdapter`. Deze streamt de tekst naar een `ByteArrayOutputStream`, waardoor de overhead van het maken van een tijdelijk bestand wordt vermeden.

```java
import com.groupdocs.search.*;
import java.io.ByteArrayOutputStream;

public class FeatureOutputToStream {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a stream in HTML format
            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            StreamOutputAdapter streamOutputAdapter = new StreamOutputAdapter(OutputFormat.Html, stream);
            index.getDocumentText(document, streamOutputAdapter);
        }
    }
}
```

**Uitleg**  
- **StreamOutputAdapter**: Streamt de tekst van het document naar een `ByteArrayOutputStream`, waardoor flexibele verwerking mogelijk is zonder het bestandssysteem aan te raken.

### Documenttekstuitvoer naar string

`StringOutputAdapter` legt de volledige documenttekst vast in één `String`‑object.

#### Overzicht
Voor snelle logging, debugging of UI‑weergave legt de `StringOutputAdapter` de volledige documenttekst vast in één `String`‑object.

```java
import com.groupdocs.search.*;

public class FeatureOutputToString {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a string in HTML format
            StringOutputAdapter stringOutputAdapter = new StringOutputAdapter(OutputFormat.Html);
            index.getDocumentText(document, stringOutputAdapter);
            String result = stringOutputAdapter.getResult();
        }
    }
}
```

**Uitleg**  
- **StringOutputAdapter**: Legt de tekst van het document vast in een `String`, waardoor het eenvoudig kan worden ingebed in logs, console‑output of UI‑componenten.

### Documenttekstuitvoer naar gestructureerd formaat

`StructuredOutputAdapter` retourneert een rijk objectmodel dat alinea's, tabellen en aangepaste metadata bevat.

#### Overzicht
De `StructuredOutputAdapter` retourneert een rijk objectmodel dat alinea's, tabellen en aangepaste metadata bevat. Dit formaat is ideaal voor downstream natural‑language‑processing (NLP) of data‑extractieworkflows.

```java
import com.groupdocs.search.*;

public class FeatureOutputToStructure {
    public static void main(String[] args) {
        String indexFolder = YOUR_DOCUMENT_DIRECTORY + "/OutputAdapters/Index";
        Index index = new Index(indexFolder);

        // Assuming documents are already indexed, retrieve the first document
        DocumentInfo[] documents = index.getIndexedDocuments();
        if (documents.length > 0) {
            DocumentInfo document = documents[0];

            // Output document text to a structured format like PlainText
            StructuredOutputAdapter structuredOutputAdapter = new StructuredOutputAdapter(OutputFormat.PlainText);
            index.getDocumentText(document, structuredOutputAdapter);
        }
    }
}
```

**Uitleg**  
- **StructuredOutputAdapter**: Extraheert documenttekst naar een **structured text extraction** formaat, waardoor fijne‑granulaire analyse, veld‑extractie en integratie met machine‑learning pijplijnen mogelijk zijn.

## Veelvoorkomende problemen en oplossingen
| Issue | Cause | Fix |
|-------|-------|-----|
| **Index niet aangemaakt** | Onjuist mappad of ontbrekende schrijfrechten | Controleer of `indexFolder` bestaat en de applicatie schrijfrechten heeft |
| **Geen documenten geretourneerd** | `index.add()` niet aangeroepen of verkeerde bronmap | Zorg ervoor dat `documentsFolder` naar de juiste map wijst en ondersteunde bestandstypen bevat |
| **Uitvoerbestand leeg** | Uitvoer‑adapter pad ongeldig of ontbrekende mappen | Maak de doelmap (`YOUR_OUTPUT_DIRECTORY`) aan vóór uitvoering |
| **Geheugenspieken bij grote bestanden** | Het volledige bestand in het geheugen laden | Gebruik `StreamOutputAdapter` om data incrementeel te verwerken |

## Veelgestelde vragen

**Q: Kan ik GroupDocs.Search gebruiken met andere JVM‑talen zoals Kotlin of Scala?**  
A: Ja, de bibliotheek is pure Java en werkt naadloos met elke JVM‑taal.

**Q: Hoe beïnvloedt compressie de zoek‑snelheid?**  
A: Hoge compressie vermindert het schijfgebruik tot 70 % en voegt slechts een minimale CPU‑overhead toe tijdens het indexeren; de query‑latentie blijft onder 100 ms voor typische workloads.

**Q: Is het mogelijk een bestaande index bij te werken zonder deze opnieuw te bouwen?**  
A: Absoluut. Gebruik `index.add()` voor nieuwe bestanden en `index.remove()` om verouderde te verwijderen, waardoor incrementele updates mogelijk zijn.

**Q: Welk uitvoerformaat is het beste voor natural‑language‑processing pipelines?**  
A: Het `PlainText`‑resultaat van de **structured text extraction** adapter levert schone, taal‑agnostische inhoud die ideaal is voor NLP‑taken.

**Q: Heb ik een licentie nodig voor ontwikkeling en testen?**  
A: Een gratis proeflicentie is voldoende voor ontwikkeling en evaluatie; productie‑implementaties vereisen een aangeschafte licentie.

## Conclusie
Je hebt nu een volledige, productie‑klare workflow voor **how to create index**, documenten toevoegen en hun tekst extraheren in elk gewenst formaat. Begin met het configureren van de `Index` met compressie, voeg je documentcollectie toe, en kies de juiste output‑adapter voor je downstream‑scenario—of het nu gaat om het genereren van HTML‑rapporten, het voeden van een NLP‑model, of het streamen van inhoud naar een webclient. Experimenteer met de incrementele update‑API's om je index actueel te houden zonder dure herbouw, en je zult genieten van snelle, betrouwbare zoekopdrachten over elke documentrepository.

---

**Last Updated:** 2026-06-27  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## Gerelateerde tutorials

- [Documenten toevoegen aan index – GroupDocs.Search Java-gids](/search/java/advanced-features/)
- [Documentindex maken met GroupDocs.Search voor Java](/search/java/advanced-features/groupdocs-search-java-implementation-guide/)
- [Hoe documenten toevoegen aan index met metadata‑indexering in Java met GroupDocs.Search](/search/java/indexing/groupdocs-search-java-metadata-indexing/)
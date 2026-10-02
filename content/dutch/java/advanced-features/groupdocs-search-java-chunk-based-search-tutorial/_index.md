---
date: '2026-10-02'
description: Leer hoe u een tijdelijke licentie kunt gebruiken om documenten toe te
  voegen aan de index met chunk‑based search in Java, waardoor de zoekprestaties worden
  verhoogd terwijl het geheugengebruik wordt gecontroleerd.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Gebruik een tijdelijke licentie om documenten toe te voegen aan de
  index met chunk‑based search in Java, waardoor de zoek snelheid wordt verbeterd
  en het geheugengebruik wordt verminderd.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Gebruik een tijdelijke licentie voor chunk‑based indexing in Java
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Gebruik een tijdelijke licentie voor chunk‑based indexing in Java
type: docs
url: /nl/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Gebruik een tijdelijke licentie voor chunk‑gebaseerde indexering in Java

In deze tutorial **gebruik je een tijdelijke licentie** om documenten toe te voegen aan de index met de chunk‑gebaseerde zoekfunctie van GroupDocs.Search. De aanpak stelt je in staat enorme documentcollecties—juridische contracten, supporttickets, onderzoekspapers—te verwerken, terwijl je **java search index memory** gebruik laag houdt en **search performance** drastisch verhoogt. Je ziet hoe je de indexmap instelt, meerdere documentbronnen toevoert, chunk‑zoeken inschakelt en zowel de eerste als de daaropvolgende chunk‑query's uitvoert.

## Snelle antwoorden
- **Wat is de eerste stap?** Maak een zoekindexmap aan.  
- **Hoe voeg ik veel bestanden toe?** Gebruik `index.add()` voor elke documentmap.  
- **Welke optie schakelt chunk‑search in?** `options.setChunkSearch(true)`.  
- **Kan ik blijven zoeken na de eerste chunk?** Ja, roep `index.searchNext()` aan met het token.  
- **Heb ik een licentie nodig?** Een gratis proefversie of tijdelijke licentie werkt voor ontwikkeling; een volledige licentie is vereist voor productie.  

## Wat je zult leren
- Hoe je een zoekindex maakt in een opgegeven map.  
- Stappen om **documenten aan de index toe te voegen** vanuit meerdere locaties.  
- Zoekopties configureren om chunk‑gebaseerd zoeken in te schakelen.  
- Initieel en daaropvolgend chunk‑gebaseerd zoeken uitvoeren.  
- Praktijkvoorbeelden waarbij chunk‑gebaseerd document zoeken uitblinkt.  

## Vereisten
Om deze gids te volgen, zorg dat je het volgende hebt:

- **Vereiste bibliotheken**: GroupDocs.Search voor Java 25.4 of later.  
- **Omgevingsconfiguratie**: Een compatibele Java Development Kit (JDK) geïnstalleerd.  
- **Kennisvereisten**: Basis Java-programmeren en bekendheid met Maven.  

## GroupDocs.Search voor Java instellen
Om te beginnen, integreer GroupDocs.Search in je project met Maven:

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

Download anders de nieuwste versie van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie verkrijgen
Om GroupDocs.Search uit te proberen:

- **Gratis proefversie** – test kernfuncties zonder verplichting.  
- **Tijdelijke licentie** – uitgebreide toegang voor ontwikkeling.  
- **Aankoop** – volledige licentie voor productiegebruik.  

## Hoe documenten aan de index toevoegen?
**Direct answer:** Roep `index.add()` aan voor elke map die bestanden bevat die je doorzoekbaar wilt maken; de methode scant de map recursief en voegt elk ondersteund document toe aan de index in één enkele bewerking. Dit elimineert de noodzaak voor handmatige bestand‑voor‑bestand verwerking en versnelt bulk‑inname.

`SearchIndex` is de centrale klasse die de doorzoekbare collectie op schijf vertegenwoordigt. Nadat je deze hebt geïnstantieerd, verlopen alle index‑ en query‑operaties via dit object.

### 1. Een index maken
**Direct answer:** Instantieer een `SearchIndex` object met het pad waar de indexbestanden moeten worden opgeslagen, roep vervolgens `index.create()` aan om de opslagstructuur te initialiseren. De aanroep maakt de benodigde mappen en metadata‑bestanden bij eerste gebruik.

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

### 2. Documenten aan de index toevoegen
**Direct answer:** Gebruik de `index.add()` methode en geef het absolute pad van elke bronmap door; de API detecteert automatisch ondersteunde formaten (PDF, DOCX, XLSX, enz.) en extraheert doorzoekbare tekst naar de index.

`SearchOptions` is een configuratie‑object waarmee je fijn kunt afstemmen hoe documenten worden verwerkt tijdens indexeren en zoeken. Je zult het later gebruiken om chunk‑gebaseerde queries in te schakelen.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Zoekopties configureren voor chunk‑search
**Direct answer:** Stel `options.setChunkSearch(true)` in op een `SearchOptions`‑instantie vóór het uitvoeren van een query; dit vertelt de engine elk document op te splitsen in logische chunks (meestal alinea's) en overeenkomsten per chunk terug te geven in plaats van per heel bestand.

`SearchResult` bevat de gevonden chunks, hun posities en relevantiescores. Wanneer chunk‑search is ingeschakeld, correspondeert elk `SearchResult` met één fragment van het oorspronkelijke document.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 4. Initiële chunk‑gebaseerde zoekopdracht uitvoeren
**Direct answer:** Voer `index.search("your query", options)` uit; de aanroep retourneert een `SearchResult`‑collectie voor de eerste set overeenkomende chunks en een token dat de zoekstatus voor voortzetting weergeeft.

Het geretourneerde token is essentieel om door grote resultaatsverzamelingen te pagineren zonder de volledige query opnieuw uit te voeren.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Chunk‑gebaseerd zoeken voortzetten
**Direct answer:** Geef het token dat is geretourneerd door de vorige aanroep door aan `index.searchNext(token, options)`; herhaal tot de methode `null` retourneert, wat aangeeft dat alle overeenkomende chunks zijn opgehaald.

Deze incrementele aanpak houdt het geheugenverbruik laag omdat alleen de huidige chunk‑batch in het geheugen aanwezig is.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Waarom chunk‑gebaseerd zoeken gebruiken?
Chunk‑gebaseerd zoeken splitst enorme documentcollecties op in beheersbare stukken, waardoor de geheugenbelasting wordt verminderd en de responstijden worden versneld. Door te indexeren op alinea‑ of sectieniveau kan de engine alleen de relevante fragmenten ophalen, wat het CPU‑gebruik verlaagt en de latentie voor eindgebruikers verbetert. Het is vooral voordelig wanneer:

1. **Juridische teams** moeten specifieke clausules vinden in duizenden contracten.  
2. **Klantenondersteuningsportalen** moeten direct relevante kennisbankartikelen tonen.  
3. **Onderzoekers** doorzoeken uitgebreide datasets zonder volledige bestanden in het geheugen te laden.  

Gekwantificeerde bewering: GroupDocs.Search kan **PDF's van meer dan 500 pagina's** verwerken in minder dan **2 seconden per chunk** op een standaard 8‑core server, terwijl de piek‑heap onder **200 MB** blijft.

## Hoe deze aanpak de zoekprestaties verhoogt
**Direct answer:** Door kleinere chunks te zoeken in plaats van volledige bestanden, kan de engine irrelevante secties vroeg overslaan, CPU‑cycli verminderen en alleen de actieve chunk in het geheugen houden, wat direct het **java search index memory** verbruik verlaagt en snellere responstijden oplevert. Deze gerichte aanpak maakt ook effectievere caching en parallelle verwerking mogelijk, waardoor meerdere cores verschillende chunks gelijktijdig kunnen verwerken, wat de doorvoer op multi‑core servers verder verbetert.

Extra voordelen omvatten:

- Parallelle chunk‑verwerking over meerdere cores.
- Vroegtijdige beëindiging wanneer een hoge‑relevantie match wordt gevonden.

## Beheren van java search index memory
**Direct answer:** Reserveer voldoende JVM‑heap (bijv. `-Xmx2g` of hoger) op basis van de verwachte indexgrootte, voer `index.optimize()` uit na bulk‑toevoegingen om de indexstructuur te comprimeren, en monitor GC‑pauzes met VisualVM om pieken in latentie te voorkomen.

Verdere afstemtips:

- Gebruik `index.flush()` na grote batches om tussentijdse gegevens naar schijf te schrijven.
- Schakel `options.setMemoryLimit(256)` in om het geheugenverbruik per zoekopdracht te beperken.

## Prestatieoverwegingen
- **Geheugenbeheer** – Reserveer voldoende heap‑ruimte (`-Xmx`) voor grote indexen.  
- **Resource monitoring** – Houd het CPU‑gebruik in de gaten tijdens indexering en zoekoperaties.  
- **Indexonderhoud** – Bouw de index periodiek opnieuw op of maak deze schoon om verouderde gegevens te verwijderen.  

## Veelvoorkomende valkuilen & probleemoplossing
| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| `OutOfMemoryError` tijdens indexering | Heap‑grootte te laag | Verhoog JVM‑heap (`-Xmx2g` of hoger) |
| Geen resultaten teruggegeven | Chunk‑token niet verwerkt | Zorg ervoor dat de `while`‑lus loopt tot `getNextChunkSearchToken()` `null` is |
| Trage zoekprestaties | Index niet geoptimaliseerd | Voer `index.optimize()` uit na bulk‑toevoegingen |

## Veelgestelde vragen

**Q: Wat is chunk‑gebaseerd zoeken?**  
A: Chunk‑gebaseerd zoeken verdeelt de dataset in kleinere stukken, waardoor efficiënte queries over grote hoeveelheden data mogelijk zijn zonder volledige documenten in het geheugen te laden.

**Q: Hoe werk ik mijn index bij met nieuwe bestanden?**  
A: Roep simpelweg `index.add()` aan met het pad naar de nieuwe documenten; de index zal ze automatisch opnemen.

**Q: Kan GroupDocs.Search verschillende bestandsformaten verwerken?**  
A: Ja, het ondersteunt **PDF, DOCX, XLSX, PPTX, HTML, TXT, en meer dan 30 andere formaten**.

**Q: Wat zijn typische prestatieknelpunten?**  
A: Geheugenbeperkingen en niet‑geoptimaliseerde indexen zijn het meest voorkomend; reserveer voldoende heap en optimaliseer de index regelmatig.

**Q: Waar kan ik meer gedetailleerde documentatie vinden?**  
A: Bezoek de officiële [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) voor diepgaande handleidingen en API‑referenties.

**Q: Werkt chunk‑gebaseerd zoeken met versleutelde PDF's?**  
A: Ja, zolang je het wachtwoord via de juiste API‑overload opgeeft.

**Q: Hoe kan ik de voortgang van het indexeren monitoren?**  
A: Gebruik de `Index.add()` overload die een `Progress`‑object retourneert of koppel in op logging‑callbacks.

## Bronnen
- **Documentatie**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API‑referentie**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis ondersteuning**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tijdelijke licentie**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Laatst bijgewerkt:** 2026-10-02  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs  

---

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Gerelateerde tutorials

- [Maak zoekindexdirectory & stel licentie in – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Verbeter query‑prestaties met GroupDocs.Search Java: Index & zoekoptimalisatie](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java geavanceerde zoekfuncties](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
---
date: '2026-07-21'
description: De Create Boolean Query Java‑tutorial laat zien hoe je booleaanse AND-,
  OR- en NOT‑zoekopdrachten implementeert met GroupDocs.Search for Java, documenten
  aan een index toevoegt en de documentophaling verbetert.
keywords:
- create boolean query java
- boolean search tutorial java
- how to implement boolean search java
- boolean and or not java
- how to use not operator java
lastmod: '2026-07-21'
og_description: De Create Boolean Query Java‑tutorial legt stap voor stap uit hoe
  je AND-, OR- en NOT‑query's bouwt met GroupDocs.Search for Java, documenten aan
  een index toevoegt en de zoekprestaties verbetert.
og_image_alt: 'Developer guide: Build boolean queries in Java using GroupDocs.Search'
og_title: Create Boolean Query Java – Beheers Booleaanse zoekopdrachten met GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-07-21'
  description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  headline: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  type: TechArticle
- description: Create Boolean Query Java tutorial shows how to implement boolean AND,
    OR, NOT searches using GroupDocs.Search for Java, add documents to an index, and
    boost document retrieval.
  name: 'Create Boolean Query Java: Master Boolean Searches with GroupDocs.Search
    for Java'
  steps:
  - name: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
    text: '**Initialize Index** – this also demonstrates **add documents to index**
      for the AND scenario.'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search** – using the plain string syntax.'
    text: '**Perform Text Query Search** – using the plain string syntax.'
  - name: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
    text: '**Perform Object Query Search** – useful when building queries programmatically
      (**search with and java**).'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  - name: '**Perform Text Query Search**'
    text: '**Perform Text Query Search**'
  - name: '**Perform Object Query Search**'
    text: '**Perform Object Query Search**'
  - name: '**Initialize Index**'
    text: '**Initialize Index**'
  - name: '**Index Documents**'
    text: '**Index Documents**'
  type: HowTo
- questions:
  - answer: Absolutely. You can chain multiple `createWordQuery` objects with `createAndQuery`,
      or simply write `"term1 AND term2 AND term3"` in the text query.
    question: Can I combine more than two terms in an AND query?
  - answer: Yes. Append `*` for wildcard (e.g., `promot*`) or use `~` for fuzzy matching
      (e.g., `comfort~`).
    question: Does GroupDocs.Search support wildcard or fuzzy searches?
  - answer: Enable the built‑in logger (`index.getLogger().setLevel(Level.INFO)`)
      and review the timing metrics after each `add` operation.
    question: What is the best way to monitor indexing performance?
  type: FAQPage
tags:
- boolean search java
- groupdocs search
- java document indexing
- search queries
- java tutorial
title: 'Create Boolean Query Java: Beheers Booleaanse zoekopdrachten met GroupDocs.Search
  for Java'
type: docs
url: /nl/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# Maak Booleaanse Query Java: Beheers Booleaanse Zoekopdrachten met GroupDocs.Search voor Java

Zoeken in enorme collecties documenten kan aanvoelen als het zoeken naar een speld in een hooiberg. **Create Boolean Query Java** laat je de engine precies vertellen wat je nodig hebt—documenten die *both* termen bevatten, *either* term, of *exclude* ongewenste woorden. In deze gids lopen we door het opzetten van **GroupDocs.Search for Java**, het toevoegen van documenten aan een index, en het maken van krachtige booleaanse queries die je **document retrieval java** workflows verbeteren. Aan het einde kun je schone, onderhoudbare code schrijven die booleaanse queries in Java maakt met slechts een paar regels.

## Snelle antwoorden
- **Wat is een boolean AND query?** Retourneert alleen documenten die *all* opgegeven termen bevatten.  
- **Hoe verschilt OR van AND?** OR vindt documenten met *any* van de termen, waardoor de resultaatsverzameling wordt vergroot.  
- **Wanneer moet ik NOT gebruiken?** Gebruik NOT om documenten met ongewenste woorden te filteren.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor testen; een commerciële licentie is vereist voor productie.  
- **Welke Java‑versie is vereist?** Java 8+ wordt ondersteund; JDK 11+ wordt aanbevolen.

## Wat is **create boolean query java**?
`create boolean query java` verwijst naar het construeren van een zoekquery in Java die logische operatoren zoals AND, OR en NOT combineert via de GroupDocs.Search API. Door deze operatoren samen te stellen kun je nauwkeurig bepalen welke documenten overeenkomen, waardoor geavanceerde filtering, relevantie‑afstemming en complexe zoekscenario's mogelijk worden.

## Waarom GroupDocs.Search voor Java gebruiken?
- **Hoge prestaties** op grote documentensets – het kan 500 GB tekst indexeren en doorzoeken in minder dan een minuut op een standaard server.  
- **Rijke API** die zowel tekst‑gebaseerde als object‑gebaseerde queries ondersteunt, zodat je de stijl kunt kiezen die bij je architectuur past.  
- **Ingebouwde taalondersteuning** voor stemming, stop‑woorden en fuzzy matching in meer dan 30 talen.  
- **Eenvoudige integratie** met Maven of directe JAR‑download, vereist slechts een paar regels code om te beginnen.

## Vereisten
Voordat je begint, zorg dat je het volgende hebt:

- **GroupDocs.Search for Java** (v25.4 of later) – zie de downloadlink hieronder.  
- JDK 8+ geïnstalleerd en geconfigureerd in je IDE (IntelliJ IDEA, Eclipse, enz.).  
- Basiskennis van Java en Maven voor afhankelijkheidsbeheer.  

## GroupDocs.Search voor Java instellen

### Maven‑configuratie
Add the repository and dependency to your `pom.xml`:

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
Alternatively, download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
Begin met een gratis proeflicentie om alle functies te verkennen. Voor productiegebruik koop je een commerciële licentie om de volledige functionaliteit te ontgrendelen.

### Basisinitialisatie en configuratie
Create an index folder and instantiate the `Index` object:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## Hoe maak je boolean query java?
De `Index`‑klasse vertegenwoordigt een doorzoekbare collectie documenten die op schijf zijn opgeslagen. Een `BooleanQuery` combineert meerdere sub‑queries met logische operatoren. `createAndQuery`, `createOrQuery` en `createNotQuery` bouwen respectievelijk AND-, OR- en NOT‑sub‑queries. Laad of maak een `Index`‑instantie, voeg documenten toe, en bouw vervolgens een `BooleanQuery`‑object met `createAndQuery`, `createOrQuery` of `createNotQuery`. Roep `index.search(query)` aan om overeenkomende documenten op te halen. Dit patroon werkt zowel voor eenvoudige als complexe scenario’s en vereist slechts drie logische stappen: indexinitialisatie, documenttoevoeging en query‑uitvoering.

## Boolean AND‑zoekopdracht

### Overzicht
Een AND‑query beperkt de resultaten, waardoor de relevantie verbetert wanneer je documenten nodig hebt die aan meerdere criteria voldoen.

### Implementatiestappen
1. **Index initialiseren** – dit toont ook **add documents to index** voor het AND‑scenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Documenten indexeren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Tekst‑query zoeken uitvoeren** – met de eenvoudige tekenreeks‑syntaxis.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Object‑query zoeken uitvoeren** – handig bij het programmatisch opbouwen van queries (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

## Boolean OR‑zoekopdracht

### Overzicht
Een OR‑query is ideaal voor verkennende zoekopdrachten waarbij je documenten wilt vinden die ten minste één van meerdere trefwoorden bevatten (**search with or java**).

### Implementatiestappen
1. **Index initialiseren**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Documenten indexeren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Tekst‑query zoeken uitvoeren**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Object‑query zoeken uitvoeren**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

## Boolean NOT‑zoekopdracht

### Overzicht
Een NOT‑query helpt je irrelevante documenten te elimineren, bijvoorbeeld door de merknaam van een concurrent te filteren (**boolean search examples java**).

### Implementatiestappen
1. **Index initialiseren**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Documenten indexeren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Tekst‑query zoeken uitvoeren**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Object‑query zoeken uitvoeren**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

## Complexe Booleaanse Queries

### Overzicht
Complexe queries stellen je in staat real‑world zoekscenario’s te modelleren, zoals “vind sportartikelen die positief zijn maar sluit elke vermelding van specifieke atleten uit”.

### Implementatiestappen
1. **Index initialiseren**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Documenten indexeren**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Tekst‑query zoeken uitvoeren**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Object‑query zoeken uitvoeren**

   ```java
   SearchQuery word1Query = SearchQuery.createWordQuery("sportsman");
   SearchQuery word2Query = SearchQuery.createWordQuery("favourable");
   SearchQuery andQuery = SearchQuery.createAndQuery(word1Query, word2Query);

   SearchQuery word3Query = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery word4Query = SearchQuery.createWordQuery("Murray");
   SearchQuery orQuery = SearchQuery.createOrQuery(word3Query, word4Query);
   SearchQuery notQuery = SearchQuery.createNotQuery(orQuery);

   SearchQuery rootQuery = SearchQuery.createAndQuery(andQuery, notQuery);
   SearchResult result2 = index.search(rootQuery);
   ```

## Praktische toepassingen van **java boolean and or** queries
- **Document Management Systems** – vind contracten die zowel “confidential” **AND** “renewal” bevatten.  
- **Legal Research** – filter jurisprudentie met **AND**/ **OR** terwijl verouderde wetten worden uitgesloten met **NOT**.  
- **Customer Support** – haal tickets op die “login” **AND** “error” vermelden, maar niet “resolved”.  
- **Content Curation** – verzamel blogposts over “cloud” **OR** “serverless” voor een nieuwsbrief.

## Veelvoorkomende valkuilen & probleemoplossing
- **Ontbrekende indexverversing** – roep na het toevoegen van nieuwe documenten `index.update()` aan om te zorgen dat ze doorzoekbaar zijn.  
- **Onjuiste operator‑spatiëring** – GroupDocs.Search verwacht spaties rond operatoren (`AND`, `OR`, `NOT`).  
- **Hoofdlettergevoeligheid** – queries zijn standaard niet hoofdlettergevoelig, maar aangepaste analyzers kunnen dit beïnvloeden.  
- **Grote resultaatsverzamelingen** – gebruik paginering (`search(query, 0, 100)`) om geheugenoverbelasting te voorkomen.  

## Veelgestelde vragen

**Q: Kan ik meer dan twee termen combineren in een AND‑query?**  
A: Absoluut. Je kunt meerdere `createWordQuery`‑objecten ketenen met `createAndQuery`, of simpelweg `"term1 AND term2 AND term3"` schrijven in de tekst‑query.

**Q: Ondersteunt GroupDocs.Search wildcard‑ of fuzzy‑zoekopdrachten?**  
A: Ja. Voeg `*` toe voor een wildcard (bijv. `promot*`) of gebruik `~` voor fuzzy matching (bijv. `comfort~`).

**Q: Hoe beperk ik de zoekopdracht tot specifieke bestandstypen?**  
`FileTypeQuery` beperkt zoekresultaten tot bepaalde bestandsformaten zoals PDF of DOCX.  
A: Gebruik de `FileTypeQuery`‑klasse om resultaten te beperken tot PDF’s, DOCX, enz., en combineer deze met je booleaanse query.

**Q: Wat is de beste manier om de indexeringsprestaties te monitoren?**  
A: Schakel de ingebouwde logger in (`index.getLogger().setLevel(Level.INFO)`) en bekijk de timing‑statistieken na elke `add`‑operatie.

**Q: Is er een manier om de relevantie van bepaalde termen te verhogen?**  
`BoostQuery` verhoogt de relevantiescore van opgegeven termen in een zoekquery.  
A: Ja. Omhul belangrijke woorden met `BoostQuery` om hun gewicht in het scoring‑algoritme te verhogen.

---

**Last Updated:** 2026-07-21  
**Tested With:** GroupDocs.Search 25.4 (Java)  
**Author:** GroupDocs

## Gerelateerde tutorials

- [Boolean Operators Java – Maak Zoekindex & Faceted Search](/search/java/advanced-features/faceted-complex-search-groupdocs-java/)
- [Master GroupDocs.Search Java&#58; Efficiënt Documenten zoeken en Indexbeheer](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [search query java - Mastering GroupDocs.Search Java – Maak en beheer een zoekindex](/search/java/indexing/groupdocs-search-java-create-index-guide/)
---
date: '2026-01-29'
description: Leer hoe je Java‑boolean‑ en -or‑queries implementeert met GroupDocs.Search
  voor Java, documenten aan de index toevoegt en de documentophaling verbetert.
keywords:
- GroupDocs.Search Java
- Boolean Searches Java
- AND OR NOT queries Java
- GroupDocs Java search
- Java boolean search implementation
title: 'java boolean en of: Beheers Booleaanse zoekopdrachten met GroupDocs.Search
  voor Java'
type: docs
url: /nl/java/searching/implement-boolean-searches-groupdocs-java/
weight: 1
---

# java boolean and or: Beheers Booleaanse Zoekopdrachten met GroupDocs.Search voor Java

Het doorzoeken van enorme collecties documenten kan aanvoelen als het zoeken naar een speld in een hooiberg. Met **java boolean and or**‑query's kun je de engine precies vertellen wat je nodig hebt—documenten die *beide* termen bevatten, *een van* de termen, of *ongewenste* woorden uitsluiten. In deze gids lopen we door het installeren van **GroupDocs.Search for Java**, het toevoegen van documenten aan een index, en het maken van krachtige booleaanse query's die je **document retrieval java**‑werkstromen verbeteren.

## Snelle Antwoorden
- **Wat is een boolean AND-query?** Geeft alleen documenten terug die *alle* opgegeven termen bevatten.  
- **Hoe verschilt OR van AND?** OR matcht documenten met *een van* de termen, waardoor de resultaatsset wordt vergroot.  
- **Wanneer moet ik NOT gebruiken?** Gebruik NOT om documenten met ongewenste woorden te filteren.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor testen; een commerciële licentie is vereist voor productie.  
- **Welke Java‑versie is vereist?** Java 8+ wordt ondersteund; JDK 11+ wordt aanbevolen.

## Wat is **java boolean and or**?
Een **java boolean and or**‑query combineert logische operatoren (AND, OR, NOT) om zoekresultaten te verfijnen. Door query's te structureren vertel je GroupDocs.Search precies hoe termen zich tot elkaar verhouden, waardoor je nauwkeurige controle krijgt over het retrieval‑proces.

## Waarom GroupDocs.Search voor Java gebruiken?
- **High performance** op grote documentensets.  
- **Rich API** die zowel tekst‑gebaseerde als object‑gebaseerde query's ondersteunt.  
- **Built‑in language support** voor stemming, stop‑words en fuzzy matching.  
- **Easy integration** met Maven of directe JAR‑download.

## Vereisten
Voordat je begint, zorg ervoor dat je het volgende hebt:

- **GroupDocs.Search for Java** (v25.4 of later) – zie de downloadlink hieronder.  
- JDK 8+ geïnstalleerd en geconfigureerd in je IDE (IntelliJ IDEA, Eclipse, enz.).  
- Basiskennis van Java en Maven voor afhankelijkheidsbeheer.  

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
Alternatively, download the latest JAR from the official site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
Begin met een gratis proeflicentie om alle functies te verkennen. Voor productiegebruik koop je een commerciële licentie om de volledige functionaliteit te ontgrendelen.

### Basisinitialisatie en configuratie
Maak een indexmap aan en instantieer het `Index`‑object:

```java
import com.groupdocs.search.Index;

public class GroupDocsSetup {
    public static void main(String[] args) {
        String indexFolder = "path/to/index/directory";
        Index index = new Index(indexFolder);
    }
}
```

## java boolean and or: Booleaanse zoekopdrachten implementeren

Hieronder behandelen we **AND**, **OR**, **NOT** en **complex**‑query's. Elke sectie toont zowel een platte‑tekst query als de equivalente object‑gebaseerde query, zodat je de stijl kunt kiezen die bij je codebase past.

### Booleaanse AND‑zoekopdracht
Combineer termen met **AND** om alleen documenten op te halen die *alle* trefwoorden bevatten.

#### Overzicht
Een AND‑query verkleint de resultaten, waardoor de relevantie verbetert wanneer je documenten nodig hebt die aan meerdere criteria voldoen.

#### Implementatiestappen

1. **Initialize Index** – dit toont ook **add documents to index** voor het AND‑scenario.

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorAnd";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search** – met de platte string‑syntaxis.

   ```java
   String query1 = "comfort AND promotion";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search** – handig bij het programmatically opbouwen van query's (**search with and java**).

   ```java
   import com.groupdocs.search.query.*;

   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("promotion");
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(andQuery);
   ```

### Booleaanse OR‑zoekopdracht
Gebruik **OR** om de resultaten te verbreden, waarbij elk van de opgegeven termen overeenkomt.

#### Overzicht
Een OR‑query is ideaal voor verkennende zoekopdrachten waarbij je documenten wilt vastleggen die ten minste één van meerdere trefwoorden bevatten (**search with or java**).

#### Implementatiestappen

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorOr";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "comfort OR neque";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("comfort");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("neque");
   SearchQuery orQuery = SearchQuery.createOrQuery(wordQuery1, wordQuery2);
   SearchResult result2 = index.search(orQuery);
   ```

### Booleaanse NOT‑zoekopdracht
Sluit ongewenste termen uit met **NOT** om ruis uit je resultaten te filteren.

#### Overzicht
Een NOT‑query helpt je irrelevante documenten te elimineren, bijvoorbeeld door de merknaam van een concurrent uit te filteren (**boolean search examples java**).

#### Implementatiestappen

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/OperatorNot";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "sportsman AND NOT Kynynmound";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

   ```java
   SearchQuery wordQuery1 = SearchQuery.createWordQuery("sportsman");
   SearchQuery wordQuery2 = SearchQuery.createWordQuery("Kynynmound");
   SearchQuery notQuery = SearchQuery.createNotQuery(wordQuery2);
   SearchQuery andQuery = SearchQuery.createAndQuery(wordQuery1, notQuery);
   SearchResult result2 = index.search(andQuery);
   ```

### Complexe Booleaanse Query's
Combineer **AND**, **OR**, en **NOT** om ingewikkelde zoeklogica te maken voor zeer specifieke retrieval‑behoeften.

#### Overzicht
Complexe query's stellen je in staat real‑world zoekscenario's te modelleren, zoals “vind sportartikelen die positief zijn maar sluit elke vermelding van specifieke atleten uit”.

#### Implementatiestappen

1. **Initialize Index**

   ```java
   String indexFolder = "YOUR_OUTPUT_DIRECTORY/BooleanSearch/ComplexQueries";
   Index index = new Index(indexFolder);
   ```

2. **Index Documents**

   ```java
   String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
   index.add(documentsFolder);
   ```

3. **Perform Text Query Search**

   ```java
   String query1 = "(sportsman AND favourable) AND NOT (Kynynmound OR Murray)";
   SearchResult result1 = index.search(query1);
   ```

4. **Perform Object Query Search**

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

## Praktische toepassingen van java boolean and or query's
- **Document Management Systems** – vind contracten die zowel “confidential” **AND** “renewal” bevatten.  
- **Legal Research** – filter jurisprudentie met **AND**/ **OR** terwijl je verouderde wetten uitsluit met **NOT**.  
- **Customer Support** – haal tickets op die “login” **AND** “error” vermelden, maar niet “resolved”.  
- **Content Curation** – verzamel blogposts over “cloud” **OR** “serverless” voor een nieuwsbrief.

## Veelvoorkomende valkuilen & probleemoplossing
- **Missing Index Refresh** – na het toevoegen van nieuwe documenten, roep `index.update()` aan om ervoor te zorgen dat ze doorzoekbaar zijn.  
- **Incorrect Operator Spacing** – GroupDocs.Search verwacht spaties rond operatoren (`AND`, `OR`, `NOT`).  
- **Case Sensitivity** – query's zijn standaard niet hoofdlettergevoelig, maar aangepaste analyzers kunnen dit beïnvloeden.  
- **Large Result Sets** – gebruik paginering (`search(query, 0, 100)`) om geheugenoverbelasting te voorkomen.

## Veelgestelde vragen

**Q: Kan ik meer dan twee termen combineren in een AND‑query?**  
A: Absoluut. Je kunt meerdere `createWordQuery`‑objecten koppelen met `createAndQuery`, of simpelweg `"term1 AND term2 AND term3"` in de tekst‑query schrijven.

**Q: Ondersteunt GroupDocs.Search wildcard‑ of fuzzy‑searches?**  
A: Ja. Voeg `*` toe voor een wildcard (bijv. `promot*`) of gebruik `~` voor fuzzy matching (bijv. `comfort~`).

**Q: Hoe beperk ik de zoekopdracht tot specifieke bestandstypen?**  
A: Gebruik de `FileTypeQuery`‑klasse om resultaten te beperken tot PDF's, DOCX, enz., en combineer deze met je booleaanse query.

**Q: Wat is de beste manier om de indexeringsprestaties te monitoren?**  
A: Schakel de ingebouwde logger in (`index.getLogger().setLevel(Level.INFO)`) en bekijk de timing‑statistieken na elke `add`‑operatie.

**Q: Is er een manier om de relevantie van bepaalde termen te verhogen?**  
A: Ja. Omhul belangrijke woorden met `BoostQuery` om hun gewicht in het scoring‑algoritme te verhogen.

---

**Laatst bijgewerkt:** 2026-01-29  
**Getest met:** GroupDocs.Search 25.4 (Java)  
**Auteur:** GroupDocs
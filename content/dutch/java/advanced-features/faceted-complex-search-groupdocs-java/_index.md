---
date: '2026-08-26'
description: Leer hoe boolean operators Java je in staat stellen een snelle zoekindex
  te bouwen, content search Java uit te voeren en faceted queries uit te voeren met
  GroupDocs.Search.
keywords:
- boolean operators java
- update index java
- faceted search java
- content search java
lastmod: '2026-08-26'
og_description: Leer hoe boolean operators Java je in staat stellen een snelle zoekindex
  te bouwen, content search Java uit te voeren en faceted queries uit te voeren met
  GroupDocs.Search.
og_image_alt: Guide showing boolean operators Java for creating a search index and
  faceted search using GroupDocs.Search
og_title: Boolean operators Java – bouw een zoekindex en faceted search
schemas:
- author: GroupDocs
  dateModified: '2026-08-26'
  description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  headline: Boolean operators Java – create search index & faceted search
  type: TechArticle
- description: Learn how boolean operators Java enable you to build a fast search
    index, perform content search Java, and run faceted queries with GroupDocs.Search.
  name: Boolean operators Java – create search index & faceted search
  steps:
  - name: Create an index
    text: First, point the `Index` to a folder where the index files will be stored.
  - name: Add documents to the index
    text: Tell GroupDocs.Search where your source documents live. All supported file
      types (PDF, DOCX, TXT, etc.) will be indexed automatically.
  - name: Perform a search in the content field with a text query
    text: 'A quick text query filters by the `content` field. The syntax `content:
      Pellentesque` limits results to documents containing the word *Pellentesque*
      in their body text.'
  - name: Perform a search using an object query
    text: Object‑based queries give you fine‑grained control. Here we build a word
      query, wrap it in a field query, and execute it.
  - name: Create an index for complex queries
    text: Reuse the same folder structure; you can share the index across both simple
      and complex scenarios.
  - name: Perform a search with a text query
    text: The following query looks for files named *lorem* **and** *ipsum* **or**
      content containing either of two exact phrases.
  - name: Perform a search with an object query
    text: Object‑based construction mirrors the textual query but offers type safety
      and IDE assistance.
  type: HowTo
- questions:
  - answer: Absolutely. Add the Maven dependency, configure the index as a Spring
      bean, and inject it wherever you need search capabilities.
    question: Can I use GroupDocs.Search with Spring Boot?
  - answer: Yes – you can add user‑defined fields during indexing and then facet on
      them.
    question: Does the library support custom metadata fields?
  - answer: The disk‑based index can handle up to 10 million documents; just ensure
      sufficient storage and monitor cache settings.
    question: How large can the index grow?
  - answer: GroupDocs.Search automatically scores matches; you can retrieve the score
      via `SearchResult.getDocument(i).getScore()`.
    question: Is there a way to rank results by relevance?
  - answer: 'Provide the password when adding the document: `index.add(filePath, password)`.'
    question: What happens if I index encrypted PDFs?
  type: FAQPage
tags:
- boolean operators java
- faceted search java
- GroupDocs.Search
- Java search
- search index java
title: Boolean operators Java – maak een zoekindex & faceted search
type: docs
url: /nl/java/advanced-features/faceted-complex-search-groupdocs-java/
weight: 1
---

# Boolean operators Java – zoekindex maken & gefacetteerd zoeken

Implementing a powerful **search experience** in Java can feel overwhelming, especially when you need to **create a search index Java** that supports **boolean operators Java** for faceted and complex queries. In this tutorial we’ll walk through setting up **GroupDocs.Search for Java**, building an index, adding documents, and crafting both simple faceted searches and sophisticated multi‑criteria queries that use Boolean logic. By the end you’ll understand how to leverage **content search Java**, **filename search Java**, and even **update index Java** operations to keep your data fresh.

## Snelle antwoorden
- **Wat is een gefacetteerde zoekopdracht?** Een manier om resultaten te filteren op vooraf gedefinieerde categorieën zoals bestandstype of datum.  
- **Hoe maak ik een search index Java?** Initialiseer een `Index` object dat naar een map wijst en voeg documenten toe.  
- **Kan ik meerdere criteria combineren met boolean operators?** Ja—gebruik object‑gebaseerde queries of Boolean operators in een tekstquery.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie verwijdert limieten.  
- **Welke IDE werkt het beste?** Elke Java IDE (IntelliJ IDEA, Eclipse, NetBeans) werkt prima.

## Wat is “create search index java”?

Een search index Java maken betekent het construeren van een schijf‑gebaseerde structuur die documenttekst en metadata opslaat, waardoor directe ophalen van overeenkomende documenten via queries mogelijk is. De index map termen naar document‑identifiers, ondersteunt snelle opzoekacties, en kan incrementeel worden bijgewerkt wanneer bestanden veranderen, wat de basis biedt voor krachtige zoekfuncties.

## Waarom GroupDocs.Search gebruiken voor gefacetteerde en complexe queries?

GroupDocs.Search for Java biedt ingebouwde faceting, ondersteuning voor Boolean‑queries en high‑performance indexering die tot 10 miljoen documenten aankan terwijl de query‑latentie onder 200 ms blijft op typische serverhardware. Het biedt kant‑en‑klaar veldfilters, een rijke querytaal, en pure‑Java compatibiliteit, waardoor het ideaal is voor enterprise‑scale zoekscenario's.

## Vereisten

- **JDK 8 of nieuwer** geïnstalleerd en geconfigureerd in je IDE.  
- **Maven** (of Gradle) voor afhankelijkheidsbeheer.  
- **GroupDocs.Search for Java** ≥ 25.4.  
- Basiskennis van Java OOP-concepten en Maven‑projectstructuur.

## GroupDocs.Search voor Java instellen

### Maven-configuratie
Voeg de repository en afhankelijkheid toe aan je `pom.xml` bestand:

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
Alternatief kun je de nieuwste JAR downloaden van de officiële release‑pagina:  
[GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/)

### Licentie‑acquisitie
Om de volledige functionaliteit te ontgrendelen:

1. **Free trial** – perfect voor ontwikkeling en testen.  
2. **Temporary evaluation license** – verlengt proeflimieten.  
3. **Commercial license** – verwijdert alle beperkingen voor productiegebruik.

### Basisinitialisatie en -configuratie
De `Index`‑klasse is de kerncomponent die een doorzoekbare index op schijf vertegenwoordigt. De volgende snippet laat zien hoe je een **search index Java** maakt door de `Index`‑klasse te instantieren:

```java
import com.groupdocs.search.Index;

public class SearchSetup {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
        
        // Create an instance of Index – this creates the on‑disk index
        Index index = new Index(indexFolder);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

Met de index klaar, kunnen we doorgaan naar real‑world gefacetteerde en complexe queries.

## Hoe boolean operators java gebruiken – Eenvoudige gefacetteerde zoekopdracht

Laad je index, voeg documenten toe, en voer een veldquery uit; het twee‑stappenpatroon stelt je in staat om facet‑aantallen en gefilterde resultaten in één oproep op te halen. Deze aanpak biedt gebruikers een intuïtieve manier om resultaten te verfijnen op categorieën zoals bestandstype, auteur, of aangepaste metadata.

### Stap 1: Index maken
Eerst wijs je de `Index` naar een map waar de indexbestanden worden opgeslagen.

```java
import com.groupdocs.search.Index;

String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
Index index = new Index(indexFolder);
```

### Stap 2: Documenten toevoegen aan de index
Geef GroupDocs.Search aan waar je bron‑documenten zich bevinden. Alle ondersteunde bestandstypen (PDF, DOCX, TXT, enz.) worden automatisch geïndexeerd.

```java
import com.groupdocs.search.Index;

String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

// Adding documents to the index
index.add(documentsFolder);
```

### Stap 3: Een zoekopdracht uitvoeren in het content‑veld met een tekstquery
Een snelle tekstquery filtert op het `content`‑veld. De syntaxis `content: Pellentesque` beperkt resultaten tot documenten die het woord *Pellentesque* in hun hoofdtekst bevatten.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "content: Pellentesque";
SearchResult result1 = index.search(query1);

// Output search results
System.out.println("Documents found (query 1): " + result1.getDocumentCount());
```

### Stap 4: Een zoekopdracht uitvoeren met een object‑query
Object‑gebaseerde queries geven je fijnmazige controle. Hier bouwen we een woordquery, wikkelen die in een veldquery, en voeren die uit.

```java
import com.groupdocs.search.SearchQuery;
import com.groupdocs.search.options.CommonFieldNames;

SearchQuery wordQuery = SearchQuery.createWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.search(fieldQuery);

// Output search results
System.out.println("Documents found (query 2): " + result2.getDocumentCount());
```

## Hoe boolean operators java gebruiken – Complexe query‑zoekopdracht

Om een complexe query uit te voeren, combineer je meerdere veldcondities met AND/OR/NOT‑operators, en voeg je optioneel phrase‑searches toe. Je kunt elke conditie specificeren met veldqueries, deze nesten met Boolean‑operators, en de relevantie regelen met boosting, waardoor je alleen de meest relevante documenten ophaalt die aan alle vereiste criteria voldoen.

### Stap 1: Index maken voor complexe queries
Herbruik dezelfde mapstructuur; je kunt de index delen tussen zowel eenvoudige als complexe scenario's.

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
Index index = new Index(indexFolder);
index.add(documentsFolder);
```

### Stap 2: Een zoekopdracht uitvoeren met een tekstquery
De volgende query zoekt naar bestanden met de naam *lorem* **en** *ipsum* **of** content die een van twee exacte zinnen bevat.

```java
import com.groupdocs.search.results.SearchResult;

String query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.search(query1);

// Output search results
class SearchResult {
    public int getDocumentCount() {
        // Implementation here
        return 0; // Placeholder
    }
}
System.out.println("Documents found (complex text query): " + result1.getDocumentCount());
```

### Stap 3: Een zoekopdracht uitvoeren met een object‑query
Object‑gebaseerde constructie spiegelt de tekstuele query maar biedt type‑veiligheid en IDE‑ondersteuning.

```java
import com.groupdocs.search.SearchQuery;

SearchQuery word6Query = SearchQuery.createWordQuery("lorem");
SearchQuery word7Query = SearchQuery.createWordQuery("ipsum");

// Constructing AND, OR queries for filename field
SearchQuery andQuery = SearchQuery.createAndQuery(word6Query, word7Query);
SearchQuery filenameQuery = SearchQuery.createFieldQuery(CommonFieldNames.FileName, andQuery);

// Content search using OR query with phrases
SearchQuery phrase1Query = SearchQuery.createPhraseSearchQuery("lectus", "eu", "aliquam");
SearchQuery phrase2Query = SearchQuery.createPhraseSearchQuery("dignissim", "turpis");

SearchQuery contentQuery = SearchQuery.createFieldQuery(CommonFieldNames.Content, 
    SearchQuery.createOrQuery(phrase1Query, phrase2Query));

// Final root query combining filename and content queries
SearchQuery rootQuery = SearchQuery.createOrQuery(filenameQuery, contentQuery);
SearchResult result2 = index.search(rootQuery);

// Output search results
System.out.println("Documents found (complex object query): " + result2.getDocumentCount());
```

## Praktische toepassingen van gefacetteerde & complexe zoekopdrachten

| Scenario | Hoe faceting helpt | Voorbeeldquery |
|----------|-------------------|---------------|
| **E‑commerce catalogus** | Filter op categorie, prijs, merk | `category: Electronics AND price:[100 TO 500]` |
| **Juridische documentopslag** | Beperk op zaaknummer, jurisdictie | `caseNumber: 2023-045 AND jurisdiction: "California"` |
| **Onderzoeksarchieven** | Combineer auteur, publicatiejaar, trefwoorden | `(author: "Doe") AND (year: 2022) AND (keywords: "machine learning")` |
| **Enterprise intranet** | Zoeken op bestandstype en afdeling | `filetype: pdf AND department: HR` |

## Veelvoorkomende valkuilen & probleemoplossing

Het `SearchResult`‑object bevat de documenten die aan een query voldoen en biedt toegang tot hun relevantiescores en gemarkeerde fragmenten.  
De `CommonFieldNames`‑klasse definieert standaard veldnamen zoals `Content` en `FileName` die door de hele API worden gebruikt.

- **Lege resultaten** – Controleer of de documenten succesvol zijn toegevoegd (`index.getDocumentCount()` kan helpen).  
- **Verouderde index** – Na het toevoegen of verwijderen van bestanden, roep `index.update()` aan om **update index java** uit te voeren en de index gesynchroniseerd te houden.  
- **Onjuiste veldnamen** – Gebruik `CommonFieldNames`‑constants (`Content`, `FileName`, enz.) om typefouten te vermijden.  
- **Prestatieknelpunten** – Voor enorme collecties, overweeg `index.setCacheSize()` in te schakelen of een dedicated SSD te gebruiken voor de indexmap.  
- **Ontbrekende highlights** – Om **highlight search results java** te doen, haal de overeenkomende fragmenten op via `SearchResult.getFragments()` (niet getoond hier maar beschikbaar in de API).  

## Veelgestelde vragen

**Q: Kan ik GroupDocs.Search gebruiken met Spring Boot?**  
A: Absoluut. Voeg de Maven‑afhankelijkheid toe, configureer de index als een Spring‑bean, en injecteer deze waar je zoekfunctionaliteit nodig hebt.

**Q: Ondersteunt de bibliotheek aangepaste metadata‑velden?**  
A: Ja – je kunt gebruikers‑gedefinieerde velden toevoegen tijdens het indexeren en vervolgens er op facetten.

**Q: Hoe groot kan de index worden?**  
A: De schijf‑gebaseerde index kan tot 10 miljoen documenten aan; zorg gewoon voor voldoende opslag en monitor de cache‑instellingen.

**Q: Is er een manier om resultaten te rangschikken op relevantie?**  
A: GroupDocs.Search scoort automatisch overeenkomsten; je kunt de score ophalen via `SearchResult.getDocument(i).getScore()`.

**Q: Wat gebeurt er als ik versleutelde PDF's indexeer?**  
A: Geef het wachtwoord op bij het toevoegen van het document: `index.add(filePath, password)`.

## Conclusie

Tegenwoordig zou je je comfortabel moeten voelen met het **creëren van een search index Java** met GroupDocs.Search, het toevoegen van documenten, en het maken van zowel eenvoudige gefacetteerde queries als geavanceerde Boolean‑zoekopdrachten met **boolean operators java**. Deze mogelijkheden stellen je in staat om snelle, nauwkeurige en gebruiksvriendelijke zoekervaringen te leveren over een breed scala aan toepassingen — van e‑commerce platformen tot enterprise‑kennisbanken.

Klaar voor de volgende stap? Ontdek de geavanceerde functies van **GroupDocs.Search** zoals **highlighting**, **suggestions**, en **real‑time indexing** om de zoekkracht van je applicatie verder te vergroten.

---

**Laatst bijgewerkt:** 2026-08-26  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Wildcard Search Java met GroupDocs.Search – Geavanceerde functies](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
- [Hoe Index Java bijwerken met GroupDocs.Search – Een uitgebreide gids](/search/java/document-management/guide-updating-index-versions-groupdocs-search-java/)
- [Hoe java full‑text search implementeren: indexdirectory maken met GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
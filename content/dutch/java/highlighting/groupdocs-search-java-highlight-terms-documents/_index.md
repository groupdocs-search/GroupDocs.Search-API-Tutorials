---
date: '2026-09-27'
description: Leer hoe u tekst java kunt markeren met GroupDocs.Search voor Java, met
  inbegrip van search documents java, index documents java en fragment highlighting.
keywords:
- highlight text java
- search documents java
- index documents java
- java text highlighting library
- highlight terms pdf java
lastmod: '2026-09-27'
og_description: Leer hoe u tekst java kunt markeren met GroupDocs.Search voor Java.
  Ontvang stapsgewijze begeleiding bij indexeren, zoeken en fragment highlighting
  voor snelle resultaten.
og_image_alt: Screenshot of highlighted search terms in a Java application using GroupDocs.Search
og_title: Tekst markeren in Java met GroupDocs.Search – Snelle documentmarkering
schemas:
- author: GroupDocs
  dateModified: '2026-09-27'
  description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  headline: Highlight text java with GroupDocs.Search
  type: TechArticle
- description: Learn how to highlight text java using GroupDocs.Search for Java, covering
    search documents java, index documents java, and fragment highlighting.
  name: Highlight text java with GroupDocs.Search
  steps:
  - name: create and populate the index
    text: Create an index folder and add all source files you want to search. The
      `Index` class represents the searchable container.
  - name: perform search and apply highlighting
    text: Search for the term (e.g., `ipsum`) and generate an HTML file with highlighted
      matches. Use `HighlightOptions` to specify the highlight color and whether to
      use inline styles. `HighlightOptions` lets you define the foreground and background
      colors, as well as the CSS class that will be applied to ea
  - name: index and search (same as above)
    text: The same index and search steps apply; you reuse the `Index` and `SearchResult`
      objects.
  - name: define fragment context and highlight
    text: Specify how many terms before and after the match should appear in each
      fragment with `FragmentOptions`. `FragmentOptions` controls the number of surrounding
      words (`termsBefore` and `termsAfter`) that are included in each snippet, allowing
      you to balance context against snippet length.
  - name: retrieve and write highlighted fragments
    text: Collect the generated fragments and write them to an HTML file. Each fragment
      is already highlighted according to the `HighlightOptions` you configured. `fragmentHighlighter`
      is a utility that creates highlighted snippets from a `SearchResult` using the
      specified fragment and highlight options. **Di
  type: HowTo
- questions:
  - answer: It offers fast, scalable indexing, customizable highlighting, and support
      for 30+ document formats, processing 500‑page files in under 2 seconds on a
      typical server.
    question: What are the benefits of using GroupDocs.Search for Java?
  - answer: Expose the search and highlight methods via Spring Boot controllers, returning
      HTML snippets or JSON payloads that contain the highlighted fragments.
    question: How can I integrate GroupDocs.Search with a REST API?
  - answer: Yes—provide the password when adding the document to the index via `addDocument(filePath,
      password)`.
    question: Does the library handle password‑protected files?
  - answer: Absolutely; you can assign a CSS class with `options.setCssClass("myHighlight")`
      and style it globally, or modify the generated HTML after highlighting.
    question: Can I customize the highlight markup beyond color?
  - answer: The code was validated against GroupDocs.Search 25.4.
    question: What version was tested for this guide?
  type: FAQPage
tags:
- highlight text java
- GroupDocs.Search
- Java document processing
title: Tekst markeren in Java met GroupDocs.Search
type: docs
url: /nl/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Markeer tekst java met GroupDocs.Search

In moderne bedrijfsapplicaties is **tekst markeren in Java** essentieel om ruwe zoekresultaten om te zetten in direct leesbare inzichten. Of je nu een legal‑review portal, een academische zoekmachine of een klant‑support dashboard bouwt, het kunnen lokaliseren en visueel benadrukken van zoektermen bespaart gebruikers talloze seconden handmatig scannen. Deze tutorial laat zien hoe je **GroupDocs.Search for Java** gebruikt om **documenten zoeken in Java**, **documenten indexeren in Java**, en zowel volledige‑document‑ als fragment‑niveau markering toe te passen, alles met slechts een paar regels code.

## Snelle antwoorden
- **Wat betekent “search and highlight text”?** Het betekent het lokaliseren van zoektermen binnen een document en deze visueel benadrukken (bijvoorbeeld met een gekleurde achtergrond).  
- **Welke bibliotheek biedt deze functionaliteit?** GroupDocs.Search for Java.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een volledige licentie is vereist voor productiegebruik.  
- **Kan ik highlight‑kleuren aanpassen?** Ja—elke RGB‑kleur kan worden ingesteld via `HighlightOptions`.  
- **Wordt fragment‑highlighting ondersteund?** Absoluut; je kunt termen vóór/na de overeenkomst definiëren om beknopte fragmenten te maken.

## Hoe tekst in Java markeren in documenten

Om tekst in Java te markeren in documenten, bouw je eerst een index van de bronbestanden met geschikte compressie‑instellingen, voer je vervolgens een zoekopdracht uit om de gewenste termen te vinden, en exporteer je tenslotte de resultaten naar HTML, PDF of platte tekst waarbij elke overeenkomst wordt omgeven door een highlight‑tag. Dit drie‑stappenproces zorgt voor snelle, nauwkeurige markering in grote collecties.

1. **Maak een index** met compressie‑instellingen die de opslaggrootte laag houden.  
2. **Voer een zoekopdracht uit** met de query‑string die je wilt markeren.  
3. **Genereer output** (HTML, PDF of platte tekst) waarbij elke voorkoming van de zoekterm wordt omgeven door een highlight‑tag.

## Wat is zoeken en tekst markeren?

Zoeken en tekst markeren is het proces van het doorzoeken van een geïndexeerde collectie op een gegeven query, het ophalen van overeenkomende documenten, en vervolgens elke voorkoming van de zoekterm in de output (HTML, PDF, enz.) te markeren. Deze visuele aanwijzing helpt eindgebruikers direct relevante informatie te vinden.

## Waarom GroupDocs.Search for Java gebruiken?

GroupDocs.Search for Java levert **high‑performance indexering** (tot 50 GB per index met `Compression.High`), **uitgebreide markering** die werkt op volledige documenten en aangepaste fragmenten, en **cross‑format ondersteuning** voor meer dan 30 bestandstypen—waaronder DOCX, PDF, PPTX en TXT. De bibliotheek biedt ook **incrementele indexering**, waardoor je nieuwe bestanden kunt toevoegen zonder de volledige index opnieuw op te bouwen, wat de downtime in grootschalige implementaties met tot 80 % vermindert.

## Vereisten
- Java Development Kit (JDK) 8 of nieuwer.  
- Maven voor afhankelijkheidsbeheer.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Basiskennis van Java‑syntaxis.

## GroupDocs.Search for Java instellen

Add the GroupDocs repository and dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

Je kunt de nieuwste JAR ook direct downloaden van de officiële site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
Begin met een gratis proefversie of verkrijg een tijdelijke licentie voor evaluatie. Voor productie‑implementaties koop je een volledige licentie om alle functies te ontgrendelen.

## Implementatie‑gids

De implementatie is opgesplitst in twee praktische secties: **markeren in volledige documenten** en **markeren in fragmenten**. Beide secties bevatten de essentiële stappen voor **hoe Java‑documenten te markeren** met GroupDocs.Search.

### Indexinstellingen configureren

Configureer vóór het indexeren de opslag om hoge compressie te gebruiken—dit vermindert het schijfgebruik met tot 70 % terwijl de zoek‑snelheid behouden blijft.

`IndexSettings` is het configuratie‑object dat bepaalt hoe de index op schijf wordt opgeslagen. Stel `Compression` in op `Compression.High` om deze optimalisatie in te schakelen.  
`Compression` specificeert het niveau van datacompressie dat op de indexbestanden wordt toegepast, waarbij `Compression.High` de maximale grootte‑reductie biedt.

## Markeren in volledige documenten

### Stap 1: maak en vul de index

Maak een indexmap aan en voeg alle bronbestanden toe die je wilt doorzoeken. De `Index`‑klasse vertegenwoordigt de doorzoekbare container.

### Stap 2: voer zoekopdracht uit en pas markering toe

Zoek naar de term (bijv. `ipsum`) en genereer een HTML‑bestand met gemarkeerde overeenkomsten. Gebruik `HighlightOptions` om de highlight‑kleur en of inline‑stijlen moeten worden gebruikt, op te geven.

`HighlightOptions` stelt je in staat de voor‑ en achtergrondkleuren te definiëren, evenals de CSS‑klasse die op elke gemarkeerde term wordt toegepast.

`HtmlHighlighter` genereert HTML‑output met gemarkeerde termen op basis van de opgegeven opties.  
`SearchResult` bevat de lijst met overeenkomende documenten en de posities van elke gevonden term.

**Direct antwoord:** Laad je index, roep `search("ipsum")` aan, en geef het resulterende `SearchResult` samen met een geconfigureerde `HighlightOptions`‑instantie door aan de `HtmlHighlighter`. De highlighter retourneert HTML waarbij elke voorkoming van “ipsum” wordt omgeven door een `<span>` met de gekozen achtergrondkleur.

Belangrijke opties uitgelegd  
- **Compression** – hoge compressie bespaart opslag.  
- **HighlightColor** – stel elke RGB‑waarde in om bij je UI‑palet te passen.  
- **UseInlineStyles** – `false` genereert schone HTML die globaal met CSS gestyled kan worden.

## Markeren in fragmenten

### Stap 1: indexeren en zoeken (zelfde als hierboven)

Dezelfde index‑ en zoekstappen zijn van toepassing; je hergebruikt de `Index`‑ en `SearchResult`‑objecten.

### Stap 2: definieer fragment‑context en markering

Geef op hoeveel termen vóór en na de overeenkomst in elk fragment moeten verschijnen met `FragmentOptions`.

`FragmentOptions` regelt het aantal omringende woorden (`termsBefore` en `termsAfter`) dat in elk fragment wordt opgenomen, waardoor je context kunt balanceren ten opzichte van de fragmentlengte.

### Stap 3: haal gemarkeerde fragmenten op en schrijf ze weg

Verzamel de gegenereerde fragmenten en schrijf ze naar een HTML‑bestand. Elk fragment is al gemarkeerd volgens de `HighlightOptions` die je hebt geconfigureerd.

`fragmentHighlighter` is een hulpprogramma dat gemarkeerde fragmenten maakt uit een `SearchResult` met behulp van de opgegeven fragment‑ en highlight‑opties.

**Direct antwoord:** Nadat je het `SearchResult` hebt verkregen, roep je `fragmentHighlighter.highlight(searchResult, fragmentOptions, highlightOptions)` aan. De methode retourneert een lijst met HTML‑fragmenten, elk met de gevonden term omgeven door het geconfigureerde aantal contextwoorden en gemarkeerd met de gekozen kleur.

## Praktische toepassingen
1. **Juridische documentreview** – markeer onmiddellijk wetten, clausules of casusverwijzingen in duizenden contracten.  
2. **Academisch onderzoek** – breng sleutelterminologie naar voren in tientallen PDF‑ en Word‑bestanden, waardoor de literatuurreviewtijd met tot 60 % wordt verkort.  
3. **Klantenondersteuning** – lokaliseer ordernummers of foutcodes in ticketgeschiedenissen, waardoor agenten problemen sneller kunnen oplossen.

## Prestatie‑overwegingen
- **Indexgrootte** – hoge compressie (`Compression.High`) verkleint de schijfvoetafdruk met tot 70 % zonder merkbare latentie‑impact.  
- **Fragment‑context** – grotere `termsBefore/After`‑waarden verhogen de leesbaarheid van fragmenten maar kunnen 10–15 ms per query toevoegen.  
- **Geheugenbeheer** – houd de JVM‑heap in de gaten bij het indexeren van grote corpora; overweeg incrementele indexering voor datasets groter dan 2 GB om het geheugengebruik onder 1 GB te houden.

## Veelvoorkomende problemen en oplossingen
- **Indexeringsfouten** – controleer bestands‑paden en zorg ervoor dat de applicatie lees‑/schrijfrechten heeft op de indexmap.  
- **Geen markeringen zichtbaar** – bevestig dat `UseInlineStyles` overeenkomt met je output‑formaat (HTML vs. PDF).  
- **Kleur niet toegepast** – zorg ervoor dat de RGB‑waarden binnen het bereik 0‑255 liggen en dat de viewer inline‑CSS of de meegeleverde CSS‑klasse respecteert.

## Veelgestelde vragen

**Q: Wat zijn de voordelen van het gebruik van GroupDocs.Search for Java?**  
A: Het biedt snelle, schaalbare indexering, aanpasbare markering, en ondersteuning voor meer dan 30 documentformaten, waarbij 500‑pagina‑bestanden in minder dan 2 seconden op een typische server worden verwerkt.

**Q: Hoe kan ik GroupDocs.Search integreren met een REST‑API?**  
A: Maak de zoek‑ en highlight‑methoden beschikbaar via Spring Boot‑controllers, die HTML‑fragmenten of JSON‑payloads teruggeven die de gemarkeerde fragmenten bevatten.

**Q: Ondersteunt de bibliotheek wachtwoord‑beveiligde bestanden?**  
A: Ja—geef het wachtwoord op bij het toevoegen van het document aan de index via `addDocument(filePath, password)`.

**Q: Kan ik de highlight‑markup aanpassen naast kleur?**  
A: Absoluut; je kunt een CSS‑klasse toewijzen met `options.setCssClass("myHighlight")` en deze globaal stylen, of de gegenereerde HTML na het markeren aanpassen.

**Q: Welke versie is getest voor deze gids?**  
A: De code is gevalideerd tegen GroupDocs.Search 25.4.

**Q: Hoe stel ik highlight‑opties java in om een CSS‑klasse te gebruiken in plaats van inline‑stijlen?**  
A: Roep `options.setUseInlineStyles(false)` aan en definieer een CSS‑regel voor de klasse die je toewijst via `options.setCssClass("myHighlight")`.

**Q: Is er een manier om termen direct in PDF‑output te markeren?**  
A: Ja—GroupDocs.Search werkt met PDF‑invoer, en de highlighter levert HTML die kan worden ingebed in een PDF‑viewer of opnieuw kan worden geconverteerd naar PDF met behulp van GroupDocs.Conversion.

---

**Laatst bijgewerkt:** 2026-09-27  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs

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

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

```java
SearchResult result = index.search("ipsum");

if (result.getDocumentCount() > 0) {
    FoundDocument document = result.getFoundDocument(0);
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, "/path/to/your/output/directory/Highlighted.html");
    
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);
    HighlightOptions options = new HighlightOptions();
    options.setHighlightColor(new Color(150, 255, 150)); // Custom green shade
    options.setUseInlineStyles(false); // Prefer CSS for styling
    
    index.highlight(document, highlighter, options);
}
```

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

```java
HighlightOptions options = new HighlightOptions();
options.setTermsBefore(5); // Include 5 terms before the match
options.setTermsAfter(5);   // Include 5 terms after the match
options.setHighlightColor(new Color(127, 200, 255)); // Custom blue shade
options.setUseInlineStyles(true); // Use inline styles for emphasis

FoundDocument document = result.getFoundDocument(0);
FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.Html);

index.highlight(document, highlighter, options);
```

```java
StringBuilder stringBuilder = new StringBuilder();
FragmentContainer[] fragmentContainers = highlighter.getResult();

for (FragmentContainer container : fragmentContainers) {
    String[] fragments = container.getFragments();
    
    if (fragments.length > 0) {
        stringBuilder.append("\n<br>").append(container.getFieldName()).append("<br>\n");
        
        for (String fragment : fragments) {
            stringBuilder.append(fragment).append("\n");
        }
    }
}

try {
    Files.write(Paths.get("/path/to/your/output/directory/Fragments.html"), stringBuilder.toString().getBytes());
} catch (IOException ex) {
    // Handle exceptions
}
```

## Gerelateerde tutorials

- [Hoe java full‑text search te implementeren: indexdirectory maken met GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Leer om zoekindex te beheren met GroupDocs.Search for Java](/search/java/searching/groupdocs-search-java-efficient-document-search/)
- [Documenten toevoegen aan index met chunk‑gebaseerd zoeken in Java](/search/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/)
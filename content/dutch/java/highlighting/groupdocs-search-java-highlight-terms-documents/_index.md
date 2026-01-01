---
date: '2025-12-26'
description: Leer hoe u tekst in documenten kunt zoeken en markeren met GroupDocs.Search
  voor Java. Ontdek technieken voor het markeren van volledige documenten en fragmenten.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Zoek en markeer tekst met GroupDocs.Search voor Java
type: docs
url: /nl/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Zoeken en Tekst Markeren in Documenten met GroupDocs.Search voor Java

In het digitale tijdperk van vandaag is **search and highlight text** over enorme documentcollecties een veelvoorkomende eis. Of je nu een juridisch beoordelingsinstrument, een academisch onderzoeksportaal of een klantenondersteuningsdashboard bouwt, het kunnen vinden en benadrukken van sleuteltermen verbetert de bruikbaarheid aanzienlijk. In deze uitgebreide gids ontdek je hoe je **search and highlight text** implementeert met GroupDocs.Search voor Java—met zowel volledige documentmarkering als fragment‑niveau markering voor gerichte context.

## Snelle Antwoorden
- **Wat betekent “search and highlight text”?** Het verwijst naar het vinden van zoektermen in een document en ze visueel te benadrukken (bijv. met een achtergrondkleur).  
- **Welke bibliotheek biedt deze functionaliteit?** GroupDocs.Search for Java.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een volledige licentie is vereist voor productie.  
- **Kan ik highlight‑kleuren aanpassen?** Ja—elke RGB‑kleur kan worden ingesteld via `HighlightOptions`.  
- **Wordt fragment‑highlighting ondersteund?** Absoluut; je kunt termen vóór/na de overeenkomst definiëren om beknopte fragmenten te maken.

## Wat is Search and Highlight Text?
Search and highlight text is het proces van het doorzoeken van een documentindex voor een gegeven query, het ophalen van overeenkomende documenten, en vervolgens elke voorkoming van de zoekterm binnen de documentoutput (HTML, PDF, enz.) markeren. Deze visuele aanwijzing helpt eindgebruikers om relevante informatie onmiddellijk te vinden.

## Waarom GroupDocs.Search voor Java gebruiken?
- **High‑performance indexing** met configureerbare compressie.  
- **Rich highlighting API** die werkt op volledige documenten en op aangepaste fragmenten.  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT, en meer).  
- **Easy Maven integration** en duidelijke Java‑gerichte API.

## Vereisten
- Java Development Kit (JDK) 8 of nieuwer.  
- Maven voor afhankelijkheidsbeheer.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Basiskennis van Java‑syntaxis.

## GroupDocs.Search voor Java instellen

Voeg de GroupDocs-repository en afhankelijkheid toe aan je `pom.xml`:

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

Je kunt de nieuwste JAR ook direct downloaden van de officiële site: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
Begin met een gratis proefversie of verkrijg een tijdelijke licentie voor evaluatie. Voor productie‑implementaties moet je een volledige licentie aanschaffen om alle functies te ontgrendelen.

## Implementatie‑gids

De implementatie is opgesplitst in twee praktische secties: **highlighting in entire documents** en **highlighting in fragments**. Beide secties bevatten de essentiële stappen voor **how to highlight Java** documenten met behulp van GroupDocs.Search.

### Indexinstellingen configureren
Configureer vóór het indexeren de opslag om hoge compressie te gebruiken—dit vermindert het schijfgebruik terwijl de zoek‑snelheid behouden blijft.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Highlighting in Entire Documents

#### Stap 1: Index maken en vullen
Maak een indexmap aan en voeg alle bronbestanden toe die je wilt doorzoeken.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Stap 2: Zoekopdracht uitvoeren en Highlighting toepassen
Zoek naar de term (bijv. `ipsum`) en genereer een HTML‑bestand met gemarkeerde overeenkomsten.

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

**Belangrijke opties uitgelegd**
- **Compression** – hoge compressie bespaart opslag.  
- **HighlightColor** – stel elke RGB‑waarde in om overeen te komen met je UI‑palet.  
- **UseInlineStyles** – `false` genereert schone HTML die globaal gestyled kan worden met CSS.

### Highlighting in Fragments

#### Stap 1: Indexeren en zoeken (zelfde als hierboven)
```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Stap 2: Fragment‑context definiëren en highlighten
Geef op hoeveel termen vóór en na de overeenkomst in elk fragment moeten verschijnen.

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

#### Stap 3: Gemarkeerde fragmenten ophalen en schrijven
Verzamel de gegenereerde fragmenten en schrijf ze naar een HTML‑bestand.

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

## Praktische Toepassingen
1. **Legal Document Review** – markeer onmiddellijk wetten, clausules of casus‑referenties.  
2. **Academic Research** – breng sleutelterminologie naar voren over tientallen PDF‑ en Word‑bestanden.  
3. **Customer Support** – lokaliseer ordernummers of foutcodes binnen ticketgeschiedenissen.

## Prestatie‑overwegingen
- **Index Size** – hoge compressie (`Compression.High`) verkleint de schijfvoetafdruk.  
- **Fragment Context** – grotere `termsBefore/After`‑waarden verhogen de nauwkeurigheid maar kunnen de snelheid beïnvloeden.  
- **Memory Management** – houd de JVM‑heap in de gaten bij het indexeren van grote corpora; overweeg incrementeel indexeren voor zeer grote sets.

## Veelvoorkomende Problemen en Oplossingen
- **Indexing Errors** – controleer bestands‑paden en zorg dat de applicatie lees‑/schrijfrechten heeft.  
- **No Highlights Appear** – bevestig dat `UseInlineStyles` overeenkomt met je output‑formaat (HTML vs. PDF).  
- **Color Not Applied** – zorg dat de RGB‑waarden binnen het bereik 0‑255 liggen en dat de HTML‑viewer de stijl ondersteunt.

## Veelgestelde Vragen

**Q: Wat zijn de voordelen van het gebruik van GroupDocs.Search voor Java?**  
A: Het biedt snelle, schaalbare indexering, aanpasbare highlighting en ondersteuning voor vele documentformaten.

**Q: Hoe kan ik GroupDocs.Search integreren met een REST‑API?**  
A: Expose de zoek‑ en highlight‑methoden via Spring Boot‑controllers, die HTML‑ of JSON‑payloads retourneren.

**Q: Ondersteunt de bibliotheek wachtwoord‑beveiligde bestanden?**  
A: Ja—geef het wachtwoord op bij het toevoegen van het document aan de index.

**Q: Kan ik de highlight‑markup aanpassen naast kleur?**  
A: Absoluut; je kunt CSS‑klassen injecteren via `HighlightOptions` of de HTML na generatie aanpassen.

**Q: Welke versie is getest voor deze gids?**  
A: De code is gevalideerd tegen GroupDocs.Search 25.4.

---

**Laatst bijgewerkt:** 2025-12-26  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs
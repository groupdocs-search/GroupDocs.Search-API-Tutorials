---
date: '2026-02-27'
description: Leer hoe je tekst kunt markeren in Java met GroupDocs.Search voor Java,
  met aandacht voor het doorzoeken van documenten in Java, het indexeren van documenten
  in Java en fragmentmarkering.
keywords:
- GroupDocs.Search for Java
- highlight search terms in documents
- document highlighting
title: Tekst markeren in Java met GroupDocs.Search
type: docs
url: /nl/java/highlighting/groupdocs-search-java-highlight-terms-documents/
weight: 1
---

# Markeer Tekst Java met GroupDocs.Search

In de hedendaagse snel evoluerende digitale omgeving is het kunnen **highlight text java** over grote collecties bestanden een onmisbare functie. Of je nu een legal‑review platform, een academische zoekmachine of een klantenservice‑console bouwt, het direct vinden van de termen waar gebruikers naar zoeken maakt de ervaring veel efficiënter. Deze tutorial leidt je door het gebruik van **GroupDocs.Search for Java** om **search documents java**, **index documents java**, en rijke markeringen toe te passen — zowel voor volledige documenten als voor gerichte fragmenten.

## Snelle Antwoorden
- **What does “search and highlight text” mean?** Het verwijst naar het lokaliseren van zoektermen in een document en ze visueel te benadrukken (bijv. met een achtergrondkleur).  
- **Which library provides this capability?** GroupDocs.Search for Java.  
- **Do I need a license?** Een gratis proefversie werkt voor evaluatie; een volledige licentie is vereist voor productie.  
- **Can I customize highlight colors?** Ja — elke RGB‑kleur kan worden ingesteld via `HighlightOptions`.  
- **Is fragment highlighting supported?** Absoluut; je kunt termen vóór/na de overeenkomst definiëren om beknopte fragmenten te maken.

## Hoe Tekst Markeren Java in Documenten
Het markeren van tekst in Java omvat drie kernstappen:

1. **Index the source files** zodat ze snel doorzocht kunnen worden.  
2. **Run a query** tegen de index om overeenkomende documenten te vinden.  
3. **Render the results with visual cues** met behulp van de highlighter‑API.

Hieronder verkennen we elke stap in detail, eerst voor volledige documentoutput en vervolgens voor fragment‑niveau snippets.

## Wat is Search and Highlight Text?
Search and highlight text is het proces van het doorzoeken van een documentindex voor een gegeven query, het ophalen van overeenkomende documenten, en vervolgens elke voorkomen van de zoekterm binnen de documentoutput (HTML, PDF, enz.) markeren. Deze visuele aanwijzing helpt eindgebruikers direct relevante informatie te vinden.

## Waarom GroupDocs.Search for Java gebruiken?
- **High‑performance indexing** met configureerbare compressie (`index documents java`).  
- **Rich highlighting API** die werkt op volledige documenten en op aangepaste fragmenten (`highlight search terms java`).  
- **Cross‑format support** (DOCX, PDF, PPTX, TXT, en meer).  
- **Simple Maven integration** en een schoon Java‑gericht ontwerp.

## Voorwaarden
- Java Development Kit (JDK) 8 of nieuwer.  
- Maven voor afhankelijkheidsbeheer.  
- Een IDE zoals IntelliJ IDEA of Eclipse.  
- Basiskennis van Java‑syntaxis.

## GroupDocs.Search for Java Instellen

Voeg de GroupDocs‑repository en afhankelijkheid toe aan je `pom.xml`:

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

### Licentie‑verwerving
Begin met een gratis proefversie of verkrijg een tijdelijke licentie voor evaluatie. Voor productie‑implementaties moet je een volledige licentie aanschaffen om alle functies te ontgrendelen.

## Implementatie‑gids

De implementatie is opgesplitst in twee praktische secties: **highlighting in entire documents** en **highlighting in fragments**. Beide secties bevatten de essentiële stappen voor **how to highlight Java** documenten met behulp van GroupDocs.Search.

### Indexinstellingen Configureren
Voor het indexeren, configureer de opslag om hoge compressie te gebruiken — dit vermindert schijfruimte terwijl de zoek‑snelheid behouden blijft.

```java
IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Markeren in Volledige Documenten

#### Stap 1: Maak en Vul de Index
Maak een indexmap aan en voeg alle bronbestanden toe die je wilt doorzoeken.

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInEntireDocument";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");
```

#### Stap 2: Voer Zoekopdracht uit en Pas Markering toe
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
- **HighlightColor** – stel elke RGB‑waarde in om bij je UI‑palet te passen.  
- **UseInlineStyles** – `false` genereert schone HTML die globaal gestyled kan worden met CSS.  

### Markeren in Fragmenten

#### Stap 1: Indexeren en Zoeken (zelfde als hierboven)

```java
String indexFolder = "/path/to/your/document/directory/HighlightingInFragments";
Index index = new Index(indexFolder, settings);
index.add("/path/to/your/documents");

SearchResult result = index.search("ipsum");
```

#### Stap 2: Definieer Fragmentcontext en Markering
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

#### Stap 3: Haal Gemarkeerde Fragmenten op en Schrijf ze
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
1. **Legal Document Review** – markeer onmiddellijk statuten, clausules of casus‑referenties.  
2. **Academic Research** – breng sleutelterminologie naar voren in tientallen PDF‑ en Word‑bestanden.  
3. **Customer Support** – lokaliseer ordernummers of foutcodes binnen ticketgeschiedenissen.

## Prestatie‑overwegingen
- **Index Size** – hoge compressie (`Compression.High`) vermindert de schijfvoetafdruk.  
- **Fragment Context** – grotere `termsBefore/After`‑waarden verhogen de nauwkeurigheid maar kunnen de snelheid beïnvloeden.  
- **Memory Management** – houd de JVM‑heap in de gaten bij het indexeren van grote corpora; overweeg incrementeel indexeren voor zeer grote sets.

## Veelvoorkomende Problemen en Oplossingen
- **Indexing Errors** – controleer bestandspaden en zorg dat de applicatie lees‑/schrijfrechten heeft.  
- **No Highlights Appear** – bevestig dat `UseInlineStyles` overeenkomt met je output‑formaat (HTML vs. PDF).  
- **Color Not Applied** – zorg dat de RGB‑waarden binnen het bereik 0‑255 liggen en dat de HTML‑viewer de stijl ondersteunt.

## Veelgestelde Vragen

**Q: Wat zijn de voordelen van het gebruik van GroupDocs.Search for Java?**  
A: Het biedt snelle, schaalbare indexering, aanpasbare markering en ondersteuning voor vele documentformaten.

**Q: Hoe kan ik GroupDocs.Search integreren met een REST‑API?**  
A: Stel de zoek‑ en markeer‑methoden beschikbaar via Spring Boot‑controllers, die HTML‑ of JSON‑payloads retourneren.

**Q: Ondersteunt de bibliotheek wachtwoord‑beveiligde bestanden?**  
A: Ja — geef het wachtwoord op bij het toevoegen van het document aan de index.

**Q: Kan ik de markering‑markup aanpassen buiten kleur?**  
A: Absoluut; je kunt CSS‑klassen injecteren via `HighlightOptions` of de HTML na generatie aanpassen.

**Q: Welke versie is getest voor deze gids?**  
A: De code is gevalideerd tegen GroupDocs.Search 25.4.

**Q: Hoe stel ik highlight options java in om een CSS‑klasse te gebruiken in plaats van inline‑stijlen?**  
A: Stel `options.setUseInlineStyles(false)` in en voeg een CSS‑regel toe voor de klasse die je toewijst via `options.setCssClass("myHighlight")`.

**Q: Is er een manier om terms pdf java direct te markeren wanneer de bron een PDF is?**  
A: Ja — GroupDocs.Search werkt met PDF‑invoer, en de highlighter zal HTML outputten die je kunt embedden in een PDF‑viewer of terug kunt converteren naar PDF met behulp van GroupDocs.Conversion.

---

**Laatst bijgewerkt:** 2026-02-27  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs
---
date: '2026-05-28'
description: Leer hoe u een zin kunt zoeken met jokertekenpatronen met behulp van
  GroupDocs.Search voor Java. Inclusief het maken van een zoekindex, het toevoegen
  van documenten en het uitvoeren van exacte zin- en jokertekenquery's.
keywords:
- how to search phrase
- create search index
- java wildcard search
- exact phrase search
- wildcard pattern search
schemas:
- author: GroupDocs
  dateModified: '2026-05-28'
  description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  headline: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  type: TechArticle
- description: Learn how to search phrase with wildcard patterns using GroupDocs.Search
    for Java. Includes creating a search index, adding documents, and executing exact
    phrase and wildcard queries.
  name: How to Search Phrase with Wildcards in GroupDocs.Search for Java
  steps:
  - name: Create an Index
    text: '*(Same as Simple Phrase Search.)*'
  - name: Add Documents to Index
    text: '*(Same as above.)*'
  - name: Create an Index
    text: '*(Repeated for clarity.)*'
  - name: Add Documents to Index
    text: '*(Repeated.)*'
  type: HowTo
- questions:
  - answer: A phrase search requires the exact word order and spacing, while a wildcard
      allows you to replace or skip words within that order, offering flexible matching.
    question: What is the difference between a wildcard and a phrase search?
  - answer: Yes—wildcard range parameters (`*min~max`) work with numbers as well as
      words, enabling queries like `"version *1~3"`.
    question: Can I use wildcards with numeric data in searches?
  - answer: Keep the index optimized, perform incremental updates, and craft specific
      wildcard patterns to limit term expansion. GroupDocs.Search can index 1 million
      documents while keeping query latency under 200 ms on standard hardware.
    question: How should I handle very large document collections?
  - answer: Absolutely—once the index is built, queries execute in milliseconds, making
      it ideal for interactive search boxes and auto‑complete features.
    question: Is GroupDocs.Search suitable for real‑time search scenarios?
  - answer: Yes. Add the Maven dependency or JAR, instantiate the `Index` as shown,
      and you’re ready to query without altering existing code.
    question: Can I integrate this library into an existing Java project?
  type: FAQPage
title: Hoe een zin te zoeken met jokertekens in GroupDocs.Search voor Java
type: docs
url: /nl/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Zoek een zin met wildcards in GroupDocs.Search voor Java

In moderne document‑gerichte applicaties is **hoe een zin te zoeken** snel en nauwkeurig een doorslaggevende factor voor de gebruikerservaring. Of je nu een kennisbank, een e‑commercecatalogus of een compliance‑gedreven repository bouwt, het vermogen om een exacte zin—of een flexibele variatie daarvan—te vinden houdt gebruikers productief en vermindert de ondersteuningslast. Deze tutorial leidt je door het installeren van **GroupDocs.Search for Java**, het maken van een zoekindex, het laden van documenten en het uitvoeren van zowel exacte‑zin‑ als wildcard‑verrijkte query's, allemaal met duidelijke, productie‑klare code‑fragmenten.

## Snelle antwoorden
- **Wat is het belangrijkste voordeel van zinszoekopdrachten?** Precieze overeenstemming van woordvolgorde en nabijheid, waardoor alleen documenten die de exacte reeks bevatten worden geretourneerd.  
- **Kunnen wildcards binnen een zin worden gebruikt?** Ja—wildcards laten je woorden overslaan of vervangen terwijl de algemene volgorde behouden blijft.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een volledige licentie is vereist voor productie‑implementaties.  
- **Welke Maven‑versie moet ik gebruiken?** De nieuwste GroupDocs.Search for Java‑release (bijv. 25.4 op het moment van schrijven).  
- **Is deze aanpak geschikt voor grote documentensets?** Absoluut—GroupDocs.Search kan multi‑honderd‑duizend‑documentcollecties aan met sub‑seconde query‑latentie wanneer de index geoptimaliseerd is.

## Wat is “hoe een zin te zoeken”?
**Zoeken naar een zin betekent zoeken naar een specifieke reeks woorden in een document.**  
Wanneer je een zinsquery uitvoert, controleert de engine dat de woorden in de exacte volgorde en binnen de gedefinieerde nabijheid verschijnen, waardoor irrelevante hits die dezelfde woorden in een andere context bevatten, worden geëlimineerd. Dit maakt zinszoekopdrachten ideaal voor het vinden van juridische clausules, productcodes of elke tekst waarbij volgorde van belang is.

## Waarom GroupDocs.Search gebruiken voor zin‑ en wildcard‑query's?
GroupDocs.Search levert **hoge‑doorvoersnelheid bij het indexeren van tot 1 miljoen documenten terwijl sub‑seconde responstijden behouden blijven** op typische serverhardware. De querytaal ondersteunt exacte zinnen, eenvoudige `*`‑ en `?`‑wildcards, en geavanceerde patronen zoals numerieke bereiken (`*2~5`). De bibliotheek integreert met elke Java‑applicatie via Maven of een directe JAR‑download, en draait op Java 8+ zonder externe services.

## Vereisten
- Java 8 of nieuwer (Java 11 LTS aanbevolen).  
- Maven 3 of later (als je afhankelijkheidsbeheer verkiest).  
- Basiskennis van Java‑projectstructuur en object‑georiënteerde concepten.  

## GroupDocs.Search voor Java instellen

### Maven gebruiken
Voeg de officiële repository en de GroupDocs.Search‑dependency toe aan je `pom.xml`:

```xml
<!-- Maven repository -->
<repositories>
    <repository>
        <id>groupdocs-releases</id>
        <url>https://repository.groupdocs.com/release</url>
    </repository>
</repositories>

<!-- GroupDocs.Search dependency -->
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-search</artifactId>
    <version>25.4</version>
</dependency>
```

### Directe download
Download anders de nieuwste JAR van de officiële release‑pagina: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie:** Ideaal voor snelle experimenten; beperkt tot 100 MB geïndexeerde data.  
- **Tijdelijke licentie:** Vraag een 30‑daagse evaluatiesleutel aan via het GroupDocs‑portaal.  
- **Volledige licentie:** Vereist voor productiegebruik en onbeperkte indexeer‑capaciteit.

## Basisinitialisatie en configuratie
Maak een map die de indexbestanden zal bevatten en instantieer het `Index`‑object. De `Index`‑klasse vertegenwoordigt de doorzoekbare index op schijf en biedt methoden om documenten toe te voegen, bij te werken en te doorzoeken.

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

Voeg de documenten toe die je doorzoekbaar wilt maken:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

## Hoe een zin met wildcards zoeken in GroupDocs.Search
Deze sectie toont drie niveaus van zinszoeken—exacte match, eenvoudige wildcard en geavanceerde wildcard‑patronen—en laat zien hoe je een index maakt, documenten toevoegt en elk type query uitvoert met beknopte Java‑code. De voorbeelden illustreren zowel tekst‑gebaseerde query's als object‑gebaseerde query‑constructie, zodat ontwikkelaars flexibele zoekfunctionaliteit in hun applicaties kunnen integreren.

### Eenvoudige zinszoekopdracht

#### Overzicht
Gebruik deze aanpak wanneer je een **exacte match** van een woordreeks nodig hebt, zoals een juridische clausule of een productmodelnummer.

#### Direct antwoord
Laad de index, roep `search` aan met een geciteerde zin (bijv. `"quick brown fox"`), en de engine retourneert alleen documenten die die exacte reeks bevatten, waarbij woordvolgorde en spatiëring behouden blijven. De query wordt in milliseconden uitgevoerd, zelfs op indexen met honderden duizenden bestanden.

#### Stap 1: Maak een index
```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

#### Stap 2: Voeg documenten toe aan de index
```java
Index index = new Index(indexFolder);
```

#### Stap 3: Zoek naar een specifieke zin (tekstvorm)
```java
index.add(documentsFolder);
```

#### Stap 4: Object‑gebaseerde query's (exacte zin zoeken)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

### Zinszoekopdracht met wildcards

#### Overzicht
Wildcard‑plaatsaanduidingen (`*` voor een willekeurig aantal tekens, `?` voor één teken) laten je **variabele woorden overslaan** terwijl de omringende volgorde behouden blijft.

#### Direct antwoord
Plaats een wildcard‑token (`*`) binnen een geciteerde zin—bijv. `"quick * fox"`—om elk woord of woorden tussen *quick* en *fox* te matchen. De engine breidt de wildcard uit op het moment van de query en scant alleen de geïndexeerde termen die aan het patroon voldoen, waardoor de prestaties vergelijkbaar blijven met een gewone zinsquery.

#### Stap 1: Maak een index
*(Hetzelfde als Eenvoudige zinszoekopdracht.)*

#### Stap 2: Voeg documenten toe aan de index
*(Hetzelfde als hierboven.)*

#### Stap 3: Tekstvorm zoeken met wildcards
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Stap 4: Object‑gebaseerde query's met wildcards (Wildcard Search Java)
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

### Geavanceerde wildcard‑zoekopdracht

#### Overzicht
Combineer numerieke bereiken, optionele tekens en aangepaste regex‑achtige patronen voor **sophisticated matching**, zoals versienummers of productcodes.

#### Direct antwoord
Gebruik de uitgebreide wildcard‑syntaxis `*min~max` om een bereik van toegestane woordafstanden te definiëren, of `?` om één teken te matchen. Bijvoorbeeld, `"error *2~5 code"` vindt het woord *error* gevolgd door twee tot vijf woorden en daarna *code*. Deze precisie vermindert false positives terwijl flexibiliteit behouden blijft.

#### Stap 1: Maak een index
*(Herhaald voor duidelijkheid.)*

#### Stap 2: Voeg documenten toe aan de index
*(Herhaald.)*

#### Stap 3: Tekstvorm zoeken met complexe wildcard‑patronen
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

#### Stap 4: Object‑gebaseerde query's met geavanceerde wildcards
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

## Praktische toepassingen
- **Content Management Systemen:** Editors kunnen exacte clausules of flexibele fragmenten vinden zonder handmatig honderden pagina's te scannen.  
- **E‑commerce catalogi:** Kopers vinden producten zelfs als ze een beschrijving weglaten of synoniemen gebruiken, dankzij wildcard‑tolerantie.  
- **Juridisch & compliance:** Snel contractuele taal isoleren die met kleine variaties in verschillende overeenkomsten kan voorkomen.  

## Prestatie‑overwegingen
- **Maak zoekindex** slechts één keer per stabiele documentenset; hergebruik dezelfde `Index`‑instantie voor alle query's.  
- **Voeg documenten incrementeel toe** wanneer er nieuwe bestanden aankomen—vermijd het herbouwen van de volledige index om CPU‑gebruik laag te houden.  
- **Ontwerp precieze wildcard‑patronen**; bredere patronen (`*`) verhogen het aantal term‑expansies en kunnen de CPU‑belasting verhogen.  
- **Roep `index.optimize()`** periodiek aan (indien ondersteund) om de index te comprimeren en het geheugenverbruik onder controle te houden.  

## Veelvoorkomende problemen & oplossingen

| Probleem | Oplossing |
|----------|-----------|
| Geen resultaten teruggegeven voor een wildcard‑query | Controleer de wildcard‑syntaxis (`*min~max`) en zorg ervoor dat de doelwoorden bestaan binnen de gedefinieerde afstand. |
| Index wordt verouderd na bestandsupdates | Gebruik `index.add(updatedFolder)` of de incrementele update‑API om alleen gewijzigde bestanden te vernieuwen. |
| Hoge geheugengebruik bij grote datasets | Verhoog de JVM‑heap (`-Xmx4g` of hoger) en overweeg de index op te splitsen in meerdere shards voor parallelle verwerking. |

## Veelgestelde vragen

**V: Wat is het verschil tussen een wildcard en een zinszoekopdracht?**  
Een zinszoekopdracht vereist de exacte woordvolgorde en spatiëring, terwijl een wildcard je toestaat woorden binnen die volgorde te vervangen of over te slaan, waardoor flexibel zoeken mogelijk is.

**V: Kan ik wildcards gebruiken met numerieke data in zoekopdrachten?**  
Ja—wildcard‑bereikparameters (`*min~max`) werken zowel met cijfers als woorden, waardoor query's zoals "version *1~3" mogelijk zijn.

**V: Hoe moet ik omgaan met zeer grote documentcollecties?**  
Houd de index geoptimaliseerd, voer incrementele updates uit, en maak specifieke wildcard‑patronen om termexpansie te beperken. GroupDocs.Search kan 1 miljoen documenten indexeren terwijl de query‑latentie onder 200 ms blijft op standaard hardware.

**V: Is GroupDocs.Search geschikt voor realtime zoekscenario's?**  
Absoluut—zodra de index is opgebouwd, worden query's in milliseconden uitgevoerd, waardoor het ideaal is voor interactieve zoekvelden en auto‑complete‑functies.

**V: Kan ik deze bibliotheek integreren in een bestaand Java‑project?**  
Ja. Voeg de Maven‑dependency of JAR toe, instantieer de `Index` zoals getoond, en je bent klaar om te zoeken zonder bestaande code aan te passen.

---

**Last Updated:** 2026-05-28  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs

```java
double word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);

WordPattern pattern = new WordPattern();
pattern.appendWildcard(0, 4);
pattern.appendString("la");

SearchQuery wordPattern3 = SearchQuery.createWordPatternQuery(pattern);
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, wordPattern3);
SearchResult resultObject = index.search(queryObject);
```

## Gerelateerde tutorials

- [Zoekindex maken Java – GroupDocs.Search tutorials](/search/java/)
- [Documenten toevoegen aan index – GroupDocs.Search Java tutorials](/search/java/document-management/)
- [Zoekindex maken - GroupDocs.Search Java tutorials](/search/java/advanced-features/)
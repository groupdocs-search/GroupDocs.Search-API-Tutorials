---
date: '2026-01-26'
description: Leer hoe u een zin zoekt met behulp van wildcard‑patronen in GroupDocs.Search
  voor Java. Deze gids behandelt het maken van een zoekindex, het toevoegen van documenten
  aan de index en het uitvoeren van een wildcard‑zoekopdracht in Java.
keywords:
- GroupDocs.Search for Java
- phrase searches
- wildcard patterns
title: Zoek een zin met jokertekens in GroupDocs.Search Java
type: docs
url: /nl/java/searching/groupdocs-search-java-phrase-wildcard/
weight: 1
---

# Hoe een zin zoeken met wildcards in GroupDocs.Search voor Java

In de snel veranderende wereld van documentbeheer kan **hoe een zin zoeken** efficiënt zoeken het verschil maken voor de bruikbaarheid van een applicatie. Of je nu een contentmanagementsysteem, een e‑commercecatalogus of een juridisch documentarchief bouwt, het kunnen vinden van exacte zinnen—of flexibele variaties daarvan—is van belang. In deze tutorial lopen we door het opzetten van **GroupDocs.Search for Java**, het maken van een zoekindex, het toevoegen van documenten aan de index, en het beheersen van zowel eenvoudige zinszoekopdrachten als krachtige wildcard‑zoektechnieken in Java.

## Snelle antwoorden
- **Wat is het belangrijkste voordeel van zinszoekopdrachten?** Precieze overeenkomst van woordvolgorde en nabijheid.  
- **Kunnen wildcards binnen een zin worden gebruikt?** Ja, je kunt wildcards combineren met exacte woorden voor flexibele overeenkomsten.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een volledige licentie is vereist voor productie.  
- **Welke Maven‑versie moet ik gebruiken?** De nieuwste GroupDocs.Search for Java‑release (bijvoorbeeld 25.4 op het moment van schrijven).  
- **Is deze aanpak geschikt voor grote documentverzamelingen?** Absoluut—houd de index geoptimaliseerd en gebruik gerichte wildcard‑patronen.

## Wat is “how to search phrase”?
Een zin zoeken betekent zoeken naar een specifieke reeks woorden in een document. Wanneer je wildcards toevoegt, laat je de zoekmachine woorden overslaan of vervangen, waardoor je de flexibiliteit krijgt om variaties te matchen zonder relevantie op te offeren.

## Waarom GroupDocs.Search gebruiken voor zin‑ en wildcard‑query's?
- **Hoge prestaties** op grote collecties dankzij een geoptimaliseerde inverted index.  
- **Rijke query‑taal** die exacte zinnen, eenvoudige wildcards en geavanceerde patronen ondersteunt.  
- **Eenvoudige integratie** met elke Java‑gebaseerde applicatie via Maven of directe download.  

## Prerequisites
- Java 8 of nieuwer geïnstalleerd.  
- Maven 3 of later (als je Maven‑dependency‑beheer verkiest).  
- Basiskennis van Java‑syntaxis en projectstructuur.  

## Setting Up GroupDocs.Search for Java

### Maven gebruiken
Add the repository and dependency to your `pom.xml` file:

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
Download anders de nieuwste JAR van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie:** Ideaal voor snelle experimenten.  
- **Tijdelijke licentie:** Aanvragen via het GroupDocs‑portaal voor uitgebreid testen.  
- **Volledige aankoop:** Aanbevolen voor productie‑implementaties.

### Basisinitialisatie en -configuratie
Maak een map voor de index en initialiseert deze:

```java
String indexFolder = "YOUR_OUTPUT_DIRECTORY/PhraseSearch";
Index index = new Index(indexFolder);
```

Voeg de documenten toe die je doorzoekbaar wilt maken:

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
index.add(documentsFolder);
```

## Hoe een zin zoeken met wildcards in GroupDocs.Search
Hieronder splitsen we drie opeenvolgende scenario's: exacte zinszoekopdracht, eenvoudig wildcard‑gebruik en geavanceerde wildcard‑patronen.

### Eenvoudige zinszoekopdracht

#### Overzicht
Gebruik dit wanneer je een exacte overeenkomst van een woordreeks nodig hebt.

##### Stap 1: Maak een index
```java
Index index = new Index(indexFolder);
```

##### Stap 2: Voeg documenten toe aan de index
```java
index.add(documentsFolder);
```

##### Stap 3: Zoek naar een specifieke zin (tekstvorm)
```java
String queryText = "\"sollicitudin at ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Stap 4: Object‑gebaseerde query's (exacte zin zoeken)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery word2 = SearchQuery.createWordQuery("at");
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, word2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Zinszoekopdracht met wildcards

#### Overzicht
Wildcard‑plaatsaanduidingen laten je een variabel aantal woorden tussen exacte termen overslaan.

##### Stap 1: Maak een index
*(Hetzelfde als de stappen van de eenvoudige zinszoekopdracht.)*

##### Stap 2: Voeg documenten toe aan de index
*(Hetzelfde als hierboven.)*

##### Stap 3: Tekstvorm zoeken met wildcards
```java
String queryText = "\"sollicitudin *0~~3 ligula\"";
SearchResult resultText = index.search(queryText);
```

##### Stap 4: Object‑gebaseerde query's met wildcards (Wildcard Search Java)
```java
SearchQuery word1 = SearchQuery.createWordQuery("sollicitudin");
SearchQuery wildcard2 = SearchQuery.createWildcardQuery(0, 3);
SearchQuery word3 = SearchQuery.createWordQuery("ligula");
SearchQuery queryObject = SearchQuery.createPhraseSearchQuery(word1, wildcard2, word3);
SearchResult resultObject = index.search(queryObject);
```

### Geavanceerd wildcard‑zoek

#### Overzicht
Combineer numerieke bereiken, optionele tekens en aangepaste patronen voor geavanceerde overeenkomsten.

##### Stap 1: Maak een index
*(Herhaald voor duidelijkheid.)*

##### Stap 2: Voeg documenten toe aan de index
*(Herhaald.)*

##### Stap 3: Tekstvorm zoeken met complexe wildcard‑patronen
```java
String queryText = "\"sollicitudin *0~~3 ?(0~4)la\"";
SearchResult resultText = index.search(queryText);
```

##### Stap 4: Object‑gebaseerde query's met geavanceerde wildcards
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

## Praktische toepassingen
- **Content Management Systems:** Sta redacteuren toe exacte clausules of flexibele fragmenten te vinden.  
- **E‑commerce catalogi:** Laat shoppers producten vinden zelfs als ze een woord missen of synoniemen gebruiken.  
- **Juridisch & compliance:** Snel contractuele taal isoleren die met kleine variaties kan voorkomen.  

## Prestatie‑overwegingen
- **Create Search Index** slechts één keer per documentset, daarna hergebruiken.  
- **Add Documents to Index** incrementeel wanneer nieuwe bestanden arriveren—herbouw de volledige index niet elke keer.  
- Gebruik **precieze wildcard‑patronen** om onnodig scannen te vermijden; bredere patronen verhogen de CPU‑belasting.  
- Roep periodiek `index.optimize()` aan (indien beschikbaar) om het geheugenverbruik laag te houden.

## Veelvoorkomende problemen & oplossingen

| Probleem | Oplossing |
|----------|-----------|
| Geen resultaten teruggegeven voor een wildcard‑query | Controleer de wildcard‑syntaxis (`*min~~max`) en zorg dat de woorden bestaan binnen de opgegeven afstand. |
| Index wordt verouderd na bestandsupdates | Voer `index.add(updatedFolder)` opnieuw uit of gebruik de incrementele update‑API. |
| Hoge geheugengebruik bij grote datasets | Verhoog de JVM‑heap‑grootte en overweeg de index op te splitsen in meerdere shards. |

## Veelgestelde vragen

**Q: Wat is het verschil tussen een wildcard en een zinszoekopdracht?**  
A: Een zinszoekopdracht zoekt naar een exacte woordvolgorde, terwijl een wildcard je toestaat woorden binnen die volgorde te vervangen of over te slaan.

**Q: Kan ik wildcards gebruiken met numerieke gegevens in zoekopdrachten?**  
A: Ja, de wildcard‑bereikparameters werken zowel met cijfers als met woorden.

**Q: Hoe moet ik omgaan met zeer grote documentverzamelingen?**  
A: Houd de index geoptimaliseerd, gebruik incrementele updates, en ontwerp je wildcard‑patronen zo specifiek mogelijk.

**Q: Is GroupDocs.Search geschikt voor real‑time zoekscenario's?**  
A: Absoluut—zodra de index is gebouwd, worden query's uitgevoerd in milliseconden, waardoor het geschikt is voor interactieve toepassingen.

**Q: Kan ik deze bibliotheek integreren in een bestaand Java‑project?**  
A: Ja. Voeg de Maven‑dependency of JAR toe, initialiseert de index zoals getoond, en je bent klaar om te gaan.

---

**Last Updated:** 2026-01-26  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
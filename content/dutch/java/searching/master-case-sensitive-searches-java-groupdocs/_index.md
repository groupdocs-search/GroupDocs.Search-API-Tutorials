---
date: '2026-02-06'
description: Leer hoe u documenten aan de index kunt toevoegen en hoofdlettergevoelige
  zoekopdrachten in Java met GroupDocs.Search kunt inschakelen, waardoor de nauwkeurigheid
  van uw applicatie wordt verhoogd.
keywords:
- case-sensitive searches in Java
- GroupDocs.Search Java tutorial
- Java text query search
- object query search in Java
title: 'Documenten toevoegen aan index: hoofdlettergevoelige Java-zoekopdracht met
  GroupDocs'
type: docs
url: /nl/java/searching/master-case-sensitive-searches-java-groupdocs/
weight: 1
---

# Documenten toevoegen aan index: Case‑gevoelige zoekopdrachten in Java beheersen met GroupDocs

Het ophalen van het juiste stukje informatie uit een enorme verzameling documenten is een kernvereiste voor moderne applicaties. In deze gids leer je **hoe je documenten toevoegt aan een index** en **case‑gevoelige zoekopdrachten** uitvoert met GroupDocs.Search voor Java. Of je nu een juridisch documentarchief, een e‑commerce catalogus of een content‑managementsysteem bouwt, nauwkeurige zoekresultaten houden gebruikers tevreden en je data betrouwbaar.

## Snelle antwoorden
- **Wat is de eerste stap om te beginnen met zoeken?** Voeg documenten toe aan een index met `index.add(...)`.
- **Hoe schakel je case‑gevoelige zoekopdrachten in?** Stel `options.setUseCaseSensitiveSearch(true)` in.
- **Kan ik zoeken over meerdere mappen?** Ja – roep `index.add()` aan voor elke map die je wilt opnemen.
- **Welke methode laat me zoeken met objecten?** Gebruik `SearchQuery.createWordQuery(...)`.
- **Heb ik een licentie nodig voor testen?** Een tijdelijke licentie is beschikbaar voor proefdoeleinden.

## Wat betekent “documenten toevoegen aan index”?
Documenten toevoegen aan een index betekent dat je je bronbestanden (PDF's, Word‑documenten, platte tekst, enz.) in GroupDocs.Search laadt zodat het een doorzoekbare datastructuur kan opbouwen. Eenmaal geïndexeerd kan de engine snelle queries uitvoeren, inclusief case‑gevoelige.

## Waarom case‑gevoelige zoekopdrachten inschakelen in Java?
- **Exacte termovereenkomst** – onderscheid “Apple” (het bedrijf) van “apple” (de vrucht).  
- **Regelgeving naleving** – sommige sectoren vereisen exacte frase‑overeenstemming.  
- **Verbeterde relevantie** – gebruikers verwachten vaak case‑specifieke resultaten in technische of juridische contexten.

## Vereisten
- JDK (Java 17 of later aanbevolen)  
- Maven voor afhankelijkheidsbeheer  
- Een IDE zoals IntelliJ IDEA of Eclipse  
- Basiskennis van Java‑programmeren  

## GroupDocs.Search voor Java instellen
Voeg eerst de GroupDocs‑repository en afhankelijkheid toe aan je `pom.xml`:

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

Alternatief kun je de nieuwste versie direct downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenties
Om te beginnen met een proefversie, ga naar GroupDocs om een tijdelijke licentie aan te schaffen. Hiermee kun je alle functies testen zonder beperkingen.

## Hoe documenten toevoegen aan index – Tekst‑query zoeken

### Stap 1: Maak een index aan en voeg je documenten toe
Maak een map aan waar de indexbestanden worden opgeslagen, en voeg vervolgens de bronmap toe die de documenten bevat die je wilt doorzoeken.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInTextForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

> **Pro tip:** Je kunt `index.add()` meerdere keren aanroepen om **over meerdere mappen te zoeken** in één enkele index.

### Stap 2: Schakel case‑gevoelige zoekopdrachten in
Configureer de zoekopties zodat ze hoofdlettergebruik respecteren.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Stap 3: Voer een case‑gevoelige tekst‑query uit
Voer een query uit die “Advantages” onderscheidt van “advantages”.

```java
String query = "Advantages";
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

De lus print het volledige pad van elk document dat de exact case‑overeenkomende term bevat.

## Hoe documenten toevoegen aan index – Object‑query zoeken

Object‑queries geven je meer flexibiliteit, vooral wanneer je meerdere criteria moet combineren.

### Stap 1: Initialiseert een tweede index (optioneel)
Als je object‑gebaseerde zoekopdrachten gescheiden wilt houden, maak dan een andere indexmap aan.

```java
String indexFolder = YOUR_OUTPUT_DIRECTORY + "/CaseSensitiveSearch/QueryInObjectForm";
Index index = new Index(indexFolder);
index.add(YOUR_DOCUMENT_DIRECTORY); // Add documents to the index
```

### Stap 2: Hergebruik de case‑gevoelige optie
Dezelfde `SearchOptions`‑instantie werkt voor object‑queries.

```java
SearchOptions options = new SearchOptions();
options.setUseCaseSensitiveSearch(true);
```

### Stap 3: Bouw en voer een object‑query uit
Maak een woord‑query‑object aan en geef het door aan de zoekengine.

```java
SearchQuery query = SearchQuery.createWordQuery("Advantages");
SearchResult result = index.search(query, options);

// Output results
for (FoundDocument doc : result.getDocuments()) {
    System.out.println("Document: " + doc.getDocumentInfo().getFilePath());
}
```

Het gebruik van `createWordQuery` stelt je later in staat het te combineren met phrase-, wildcard- of Boolean‑queries voor complexere scenario's.

## Praktische toepassingen
- **Juridisch documentbeheer:** Haal case‑specifieke wetgevingen op waar hoofdlettergebruik van belang is.  
- **E‑commerce platforms:** Onderscheid product‑SKU's zoals “PRO‑X” versus “pro‑x”.  
- **Content Management Systems (CMS):** Zorg ervoor dat auteurs exacte koppen of tags vinden.

## Prestatie‑overwegingen
- **Houd de index up‑to‑date** – re‑indexeer wanneer nieuwe bestanden worden toegevoegd of bestaande wijzigen.  
- **Monitor geheugenverbruik** – grote corpora profiteren van incrementeel indexeren en juiste JVM‑heap‑grootte.  
- **Maak gebruik van Java’s garbage collector** – geef `Index`‑objecten vrij wanneer ze niet meer nodig zijn.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oplossing |
|----------|-----------|
| `useCaseSensitiveSearch` lijkt genegeerd te worden | Controleer of je de nieuwste GroupDocs.Search‑versie gebruikt en of de index opnieuw is opgebouwd na het wijzigen van de optie. |
| Geen resultaten teruggekregen voor een bekende term | Zorg ervoor dat de hoofdlettergebruik van de term exact overeenkomt en dat het document succesvol aan de index is toegevoegd. |
| Zoeken in veel mappen vertraagt | Voeg elke map afzonderlijk toe met `index.add()` en overweeg de index op te splitsen in shards voor zeer grote datasets. |

## Veelgestelde vragen

**Q:** Hoe ga ik om met grote datasets met GroupDocs.Search?  
**A:** Maak gebruik van index‑partitionering, stel JVM‑geheugeninstellingen af en compactteer periodiek de index om de prestaties optimaal te houden.

**Q:** Kan ik gelijktijdig zoeken over meerdere mappen?  
**A:** Ja – roep `index.add()` aan voor elke map die je wilt opnemen, en voer vervolgens één enkele query uit tegen de gecombineerde index.

**Q:** Wat zijn veelvoorkomende valkuilen bij het instellen van case‑gevoelige zoekopdrachten?  
**A:** Het vergeten opnieuw opbouwen van de index na het inschakelen van `useCaseSensitiveSearch`, of het gebruiken van de verkeerde hoofdlettercase in de query‑string.

**Q:** Hoe kan ik zoekfouten oplossen?  
**A:** Controleer de logbestanden die door GroupDocs.Search worden gegenereerd op stacktraces, en bevestig dat alle Maven‑afhankelijkheden correct zijn opgelost.

**Q:** Is GroupDocs.Search geschikt voor realtime‑applicaties?  
**A:** Met de juiste indexeringsstrategieën (incrementele updates en in‑memory caching) kan het bijna realtime zoekresultaten leveren.

## Bronnen
- **Documentatie:** [GroupDocs.Search Java Docs](https://docs.groupdocs.com/search/java/)
- **API‑referentie:** [Java API Reference](https://reference.groupdocs.com/search/java)
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)
- **GitHub‑repository:** [GroupDocs.Search for Java](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)
- **Supportforum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/search/10)
- **Tijdelijke licentie:** [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-02-06  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs
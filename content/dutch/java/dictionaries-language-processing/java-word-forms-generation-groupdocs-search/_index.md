---
date: '2026-09-02'
description: 'Hoe formulieren te genereren in Java met GroupDocs.Search: leer hoe
  je een aangepaste word‑forms provider maakt voor nauwkeurige zoekopdrachten en tekstanalyse.'
keywords:
- how to generate forms
- GroupDocs.Search Java
- word forms provider
- singular plural Java
lastmod: '2026-09-02'
og_description: 'Hoe formulieren te genereren in Java met GroupDocs.Search: leer hoe
  je een aangepaste word‑forms provider maakt voor nauwkeurige zoekopdrachten en tekstanalyse.'
og_image_alt: Guide showing how to generate forms in Java using GroupDocs.Search
og_title: Hoe formulieren te genereren in Java met GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-09-02'
  description: 'How to generate forms in Java with GroupDocs.Search: learn to create
    a custom word‑forms provider for accurate search and text analysis.'
  headline: How to generate forms in Java with GroupDocs.Search
  type: TechArticle
- description: 'How to generate forms in Java with GroupDocs.Search: learn to create
    a custom word‑forms provider for accurate search and text analysis.'
  name: How to generate forms in Java with GroupDocs.Search
  steps:
  - name: '**Free trial:** Sign up for a trial to explore core features.'
    text: '**Free trial:** Sign up for a trial to explore core features.'
  - name: '**Temporary license:** Request a temporary key for extended testing.'
    text: '**Temporary license:** Request a temporary key for extended testing.'
  - name: '**Purchase:** Obtain a commercial license for unrestricted production use.'
    text: '**Purchase:** Obtain a commercial license for unrestricted production use.'
  - name: '**Search engines:** Users typing “mouse” should also find documents containing
      “mice”. A provider can generate such irregular forms.'
    text: '**Search engines:** Users typing “mouse” should also find documents containing
      “mice”. A provider can generate such irregular forms.'
  - name: '**Text analysis tools:** Sentiment or entity extraction becomes more reliable
      when all word variants are recognised.'
    text: '**Text analysis tools:** Sentiment or entity extraction becomes more reliable
      when all word variants are recognised.'
  - name: '**Content management systems:** Automatic tag generation can include plural
      synonyms, improving SEO and internal linking.'
    text: '**Content management systems:** Automatic tag generation can include plural
      synonyms, improving SEO and internal linking.'
  type: HowTo
- questions:
  - answer: It’s a powerful library that offers full‑text search, indexing, and linguistic
      features—including the ability to plug in custom word‑form providers.
    question: What is GroupDocs.Search for Java?
  - answer: It generates alternative forms by applying simple suffix‑based rules (removing
      “s/es”, converting “y” to “is”, and appending “s/es”).
    question: How does the SimpleWordFormsProvider work?
  - answer: Absolutely. Modify the `getWordForms` method to include irregular forms,
      locale‑specific rules, or integration with external dictionaries.
    question: Can I customize the word form generation rules?
  - answer: Search engines, text‑analysis pipelines, and CMS platforms benefit from
      recognising singular/plural variants.
    question: What are some common applications for this feature?
  - answer: Yes—while a trial lets you explore the API, a purchased license removes
      usage limits and grants support.
    question: Do I need a commercial license for production use?
  type: FAQPage
tags:
- word forms
- GroupDocs.Search
- Java
- search indexing
- text analysis
title: Hoe formulieren te genereren in Java met GroupDocs.Search
type: docs
url: /nl/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Hoe formulieren genereren in Java met GroupDocs.Search

In deze gids leer je **hoe formulieren te genereren in Java** met behulp van de GroupDocs.Search API. Door een aangepaste word‑forms provider te maken, stel je je zoek‑ of tekstanalyse‑engine in staat elke variatie van een term te herkennen — of het nu “cat”, “cats”, “city” of “citis” is. Dit verbetert de recall aanzienlijk terwijl de precisie hoog blijft.

## Snelle antwoorden
- **Wat doet een word forms provider?** Het genereert alternatieve vormen (enkelvoud, meervoud, enz.) van een gegeven woord zodat zoekopdrachten alle varianten kunnen matchen.  
- **Welke bibliotheek is vereist?** GroupDocs.Search voor Java (versie 25.4 of nieuwer).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een permanente licentie is vereist voor productie.  
- **Welke Java‑versie wordt ondersteund?** JDK 8 of hoger.  
- **Hoeveel regels code zijn nodig?** Ongeveer 30 regels voor een eenvoudige provider‑implementatie.

## Wat is een “create word forms provider” functie?
Een **create word forms provider** is een aangepaste klasse die `IWordFormsProvider` implementeert. `IWordFormsProvider` is een interface die definieert hoe providers alternatieve woordvormen aan de zoekengine leveren. Het ontvangt een woord en retourneert een array van mogelijke vormen — enkelvoud, meervoud of andere linguïstische variaties — op basis van regels die je definieert. Dit stelt de zoekindex in staat “cat” en “cats” als equivalent te behandelen, waardoor de recall verbetert zonder precisie op te offeren.

## Waarom GroupDocs.Search gebruiken voor woord‑vorm generatie?
GroupDocs.Search biedt ingebouwde uitbreidbaarheid, waardoor je je eigen provider direct in de indexerings‑pipeline kunt pluggen. Het verwerkt indexen met tot **10 miljoen documenten** terwijl het geheugenverbruik onder **500 MB** blijft dankzij een streaming‑architectuur, en je kunt resultaten cachen om sub‑milliseconde zoektijden te behalen.

## Voorvereisten
- **Maven** geïnstalleerd en een JDK 8 of nieuwer ingesteld op je machine.  
- Basiskennis van Java‑ontwikkeling en de `pom.xml`‑configuratie van Maven.  
- Toegang tot de GroupDocs.Search Java‑bibliotheek (versie 25.4 of later).

## GroupDocs.Search voor Java instellen

### Maven‑configuratie
Voeg de repository en afhankelijkheid toe aan je `pom.xml`‑bestand precies zoals hieronder weergegeven:

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
Of download de nieuwste JAR van de officiële releases‑pagina: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Stappen voor licentie‑verwerving
1. **Gratis proefversie:** Meld je aan voor een proefversie om de kernfuncties te verkennen.  
2. **Tijdelijke licentie:** Vraag een tijdelijke sleutel aan voor uitgebreid testen.  
3. **Aankoop:** Verkrijg een commerciële licentie voor onbeperkt gebruik in productie.

### Basisinitialisatie en -configuratie
De volgende snippet laat zien hoe je een index maakt — je startpunt voor het toevoegen van documenten en woord‑vorm logica:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Initialize an index
        Index index = new Index("path/to/index");
        
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Implementatie‑gids

Hieronder lopen we de stappen door om een **word forms provider** te **creëren** die eenvoudige enkelvoud‑naar‑meervoud en meervoud‑naar‑enkelvoud transformaties afhandelt.

### Implementatie van SimpleWordFormsProvider

#### Overzicht
De `SimpleWordFormsProvider`‑klasse implementeert `IWordFormsProvider`. De definitie‑anker verduidelijkt het doel:

`SimpleWordFormsProvider` is een aangepaste implementatie van `IWordFormsProvider` die enkelvoud‑meervoud variaties levert voor de indexeringsengine.

#### Stap 1 – maak de klassenstructuur
Start met het definiëren van een klasse die `IWordFormsProvider` implementeert. Houd de import‑statements ongewijzigd:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Stap 2 – implementeer `getWordForms`
Voeg de methode toe die de lijst van mogelijke vormen opbouwt. Dit blok bevat de kernlogica; je kunt het later uitbreiden om meer complexe regels te dekken.

`getWordForms` ontvangt een term en retourneert een `String[]` met alle gegenereerde variaties.

```java
    @Override
    public final String[] getWordForms(String word) {
        // Initialize a list to store generated word forms
        ArrayList<String> result = new ArrayList<>();

        // Singular form for words ending in 'es'
        if (word.length() > 2 && word.toLowerCase().endsWith("es")) {
            result.add(word.substring(0, word.length() - 2));
        }

        // Singular form for words ending in 's'
        if (word.length() > 1 && word.toLowerCase().endsWith("s")) {
            result.add(word.substring(0, word.length() - 1));
        }

        // Plural form by replacing 'y' with 'is'
        if (word.length() > 1 && word.toLowerCase().endsWith("y")) {
            result.add(word.substring(0, word.length() - 1).concat("is"));
        }

        // Basic plural forms
        result.add(word.concat("s"));
        result.add(word.concat("es"));

        // Convert list to array and return
        return result.toArray(new String[0]);
    }
}
```

#### Uitleg van de logica
- **Singularisatie:** Detecteert veelvoorkomende meervoudsuffixen (`es`, `s`) en verwijdert ze om het basiswoord te benaderen.  
- **Pluralisatie:** Behandelt zelfstandige naamwoorden die eindigen op `y` door deze te vervangen door `is`, een eenvoudige regel die voor veel Engelse woorden werkt.  
- **Suffix toevoegen:** Voegt `s` en `es` toe om reguliere meervoudsvormen te dekken die mogelijk niet door de eerdere controles worden opgevangen.

#### Tips voor probleemoplossing
- **Hoofdlettergevoeligheid:** De methode gebruikt `toLowerCase()` voor vergelijking, waardoor “Cats” en “cats” hetzelfde gedrag vertonen.  
- **Randgevallen:** Woorden korter dan de suffixlengte worden genegeerd om het retourneren van lege strings te voorkomen.  
- **Prestaties:** Overweeg voor grote vocabularia om resultaten te cachen in een `ConcurrentHashMap`.

## Praktische toepassingen

Het implementeren van een **create word forms provider** kan verschillende real‑world scenario's verbeteren:

1. **Zoekmachines:** Gebruikers die “mouse” intypen moeten ook documenten vinden die “mice” bevatten. Een provider kan dergelijke onregelmatige vormen genereren.  
2. **Tekstanalyse‑tools:** Sentiment‑ of entiteitsextractie wordt betrouwbaarder wanneer alle woordvarianten worden herkend.  
3. **Content‑management‑systemen:** Automatische tag‑generatie kan meervoudige synoniemen bevatten, waardoor SEO en interne links verbeteren.

## Prestatie‑overwegingen

Wanneer je de provider in een productiesysteem integreert, houd dan deze tips in gedachten:

- **Cache vaak gebruikte vormen:** Sla resultaten op in het geheugen om herhaaldelijk berekenen van hetzelfde woord te vermijden.  
- **Monitor JVM‑heap:** Grote indexen kunnen de geheugenbelasting verhogen; stem `-Xmx` hierop af.  
- **Gebruik efficiënte collecties:** `ArrayList` werkt voor kleine sets, maar overweeg voor duizenden vormen `HashSet` om duplicaten snel te verwijderen.

**Beste praktijken**
- Houd de bibliotheek up‑to‑date om te profiteren van prestatie‑patches.  
- Profileer de provider met realistische query‑belastingen om knelpunten vroegtijdig te ontdekken.

## Conclusie

Je hebt nu geleerd **hoe formulieren te genereren in Java** met een aangepaste `SimpleWordFormsProvider` met GroupDocs.Search. Deze lichtgewicht component kan de relevantie van zoekresultaten en de nauwkeurigheid van linguïstische analyse in veel toepassingen drastisch verbeteren.

**Volgende stappen**  
- Experimenteer met meer geavanceerde linguïstische regels (onregelmatige meervouden, stemming).  
- Integreer de provider in een indexerings‑pipeline en meet recall‑verbeteringen.  
- Verken andere GroupDocs.Search‑functies zoals synoniemdictionaries en aangepaste analyzers.

**Oproep tot actie:** Probeer de `SimpleWordFormsProvider` vandaag aan je eigen project toe te voegen en zie hoe het je zoekervaring verrijkt!

## FAQ‑sectie

**Q: Wat is GroupDocs.Search voor Java?**  
A: Het is een krachtige bibliotheek die full‑text zoeken, indexering en linguïstische functies biedt — inclusief de mogelijkheid om aangepaste word‑form providers in te pluggen.

**Q: Hoe werkt de SimpleWordFormsProvider?**  
A: Het genereert alternatieve vormen door eenvoudige suffix‑gebaseerde regels toe te passen (verwijderen van “s/es”, omzetten van “y” naar “is”, en toevoegen van “s/es”).

**Q: Kan ik de regels voor woordvormgeneratie aanpassen?**  
A: Absoluut. Pas de `getWordForms`‑methode aan om onregelmatige vormen, locale‑specifieke regels, of integratie met externe woordenboeken op te nemen.

**Q: Wat zijn enkele veelvoorkomende toepassingen voor deze functie?**  
A: Zoekmachines, tekstanalyse‑pijplijnen en CMS‑platformen profiteren van het herkennen van enkelvoud‑/meervoud‑varianten.

**Q: Heb ik een commerciële licentie nodig voor productiegebruik?**  
A: Ja — hoewel een proefversie je de API laat verkennen, verwijdert een aangekochte licentie gebruikslimieten en biedt ondersteuning.

---

**Laatst bijgewerkt:** 2026-09-02  
**Getest met:** GroupDocs.Search 25.4 (Java)  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Taalverwerking Java – Synoniemdictionary maken met GroupDocs.Search](/search/java/dictionaries-language-processing/)
- [Hoe Java full‑text zoeken te implementeren: indexdirectory maken met GroupDocs.Search](/search/java/indexing/groupdocs-search-java-create-index/)
- [Hoe regex‑zoeken in Java: GroupDocs.Search beheersen voor tekstdocumentanalyse](/search/java/searching/groupdocs-search-java-regex-tutorial/)
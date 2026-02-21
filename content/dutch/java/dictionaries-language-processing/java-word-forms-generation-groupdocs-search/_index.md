---
date: '2026-02-21'
description: Leer hoe je enkelvoud‑ en meervoudsvormen kunt genereren in Java met
  de GroupDocs.Search‑API. Maak een aangepaste provider voor woordvormen voor nauwkeurig
  zoeken en tekstanalyse.
keywords:
- word forms generation
- GroupDocs.Search Java API
- linguistic transformation
title: Genereer enkelvoud‑ en meervoudsvormen in Java met GroupDocs.Search
type: docs
url: /nl/java/dictionaries-language-processing/java-word-forms-generation-groupdocs-search/
weight: 1
---

# Genereer enkelvoud‑meervoudsvormen in Java met GroupDocs.Search

Als u **singular‑meervoudsvormen in Java genereren** moet, is een aangepaste word‑forms provider de sleutel om uw zoek‑ of tekstanalyse‑engine elke variatie van een term te laten begrijpen. In deze tutorial laten we u stap voor stap zien hoe u zo’n provider bouwt met de GroupDocs.Search Java API, zodat uw applicatie automatisch “cat”, “cats”, “city” en “citis” kan matchen zonder extra inspanning.

## Snelle antwoorden
- **Wat doet een word forms provider?** Het genereert alternatieve vormen (enkelvoud, meervoud, enz.) van een gegeven woord zodat zoekopdrachten alle varianten kunnen matchen.  
- **Welke bibliotheek is vereist?** GroupDocs.Search for Java (versie 25.4 of nieuwer).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een permanente licentie is vereist voor productie.  
- **Welke Java‑versie wordt ondersteund?** JDK 8 of hoger.  
- **Hoeveel regels code zijn nodig?** Ongeveer 30 regels voor een eenvoudige provider‑implementatie.

## Wat is een “Create Word Forms Provider” functie?
Een **create word forms provider** component is een aangepaste klasse die `IWordFormsProvider` implementeert. Het ontvangt een woord en retourneert een array van mogelijke vormen — enkelvoud, meervoud of andere linguïstische variaties — op basis van regels die u definieert. Dit maakt het mogelijk dat de zoekindex “cat” en “cats” als equivalent behandelt, waardoor de recall verbetert zonder precisie op te offeren.

## Waarom GroupDocs.Search gebruiken voor woord‑vormgeneratie?
- **Ingebouwde uitbreidbaarheid:** Sluit uw eigen provider direct aan op de indexerings‑pipeline.  
- **Prestatie‑geoptimaliseerd:** Verwerkt grote indexen efficiënt, en u kunt resultaten cachen voor extra snelheid.  
- **Cross‑language ondersteuning:** Concepten zijn ook toepasbaar op .NET en andere platformen.

## Voorvereisten
Voordat u de **create word forms provider** implementeert, zorg ervoor dat u het volgende heeft:

- **Maven** geïnstalleerd en een JDK 8 of nieuwer ingesteld op uw machine.  
- Basiskennis van Java‑ontwikkeling en de `pom.xml`‑configuratie van Maven.  
- Toegang tot de GroupDocs.Search Java‑bibliotheek (versie 25.4 of later).  

## GroupDocs.Search voor Java instellen

### Maven‑configuratie

Voeg de repository en afhankelijkheid toe aan uw `pom.xml`‑bestand precies zoals hieronder weergegeven:

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

U kunt ook de nieuwste JAR downloaden van de officiële releases‑pagina: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Stappen voor het verkrijgen van een licentie

1. **Gratis proefversie:** Meld u aan voor een proefversie om de kernfuncties te verkennen.  
2. **Tijdelijke licentie:** Vraag een tijdelijke sleutel aan voor uitgebreid testen.  
3. **Aankoop:** Verkrijg een commerciële licentie voor onbeperkt gebruik in productie.

### Basisinitialisatie en -configuratie

De volgende code‑fragment toont hoe u een index maakt — uw startpunt voor het toevoegen van documenten en woord‑vormlogica:

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

Hieronder lopen we de stappen door om een **create word forms provider** te maken die eenvoudige enkelvoud‑naar‑meervoud‑ en meervoud‑naar‑enkelvoud‑transformaties afhandelt.

### Implementatie van SimpleWordFormsProvider

#### Overzicht
Onze aangepaste provider zal:

- Het achtervoegsel “es” of “s” verwijderen om een enkelvoudige vorm te raden.  
- Een achtervoegsel “y” wijzigen in “is” om een meervoudige vorm te produceren (bijv. “city” → “citis”).  
- “s” en “es” toevoegen om basis‑meervoudkandidaten te genereren.

#### Stap 1 – Maak de klassen‑skelet

Begin met het definiëren van een klasse die `IWordFormsProvider` implementeert. Houd de import‑verklaringen ongewijzigd:

```java
import com.groupdocs.search.dictionaries.IWordFormsProvider;
import java.util.ArrayList;

public class SimpleWordFormsProvider implements IWordFormsProvider {
```

#### Stap 2 – Implementeer `getWordForms`

Voeg de methode toe die de lijst met mogelijke vormen opbouwt. Dit blok bevat de kernlogica; u kunt het later uitbreiden om meer complexe regels te dekken.

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
- **Singularisatie:** Detecteert veelvoorkomende meervoudige achtervoegsels (`es`, `s`) en verwijdert ze om het basiswoord te benaderen.  
- **Meervoudsvorming:** Behandelt zelfstandige naamwoorden die eindigen op `y` door deze te vervangen door `is`, een eenvoudige regel die voor veel Engelse woorden werkt.  
- **Achtervoegsel toevoegen:** Voegt `s` en `es` toe om reguliere meervoudsvormen te dekken die mogelijk niet door de eerdere controles worden opgevangen.

#### Tips voor probleemoplossing
- **Hoofdlettergevoeligheid:** De methode gebruikt `toLowerCase()` voor vergelijking, waardoor “Cats” en “cats” hetzelfde gedrag vertonen.  
- **Randgevallen:** Woorden korter dan de lengte van het achtervoegsel worden genegeerd om te voorkomen dat lege strings worden geretourneerd.  
- **Prestaties:** Overweeg voor grote vocabularia om resultaten te cachen in een `ConcurrentHashMap`.

## Praktische toepassingen

Het implementeren van een **create word forms provider** kan verschillende real‑world scenario’s verbeteren:

1. **Zoekmachines:** Gebruikers die “mouse” typen, moeten ook documenten vinden die “mice” bevatten. Een provider kan dergelijke onregelmatige vormen genereren.  
2. **Tekstanalyse‑tools:** Sentiment‑ of entiteits‑extractie wordt betrouwbaarder wanneer alle woordvarianten worden herkend.  
3. **Content Management Systemen:** Automatische tag‑generatie kan meervoudige synoniemen omvatten, wat SEO en interne linking verbetert.

## Prestatie‑overwegingen

Wanneer u de provider in een productiesysteem integreert, houd dan deze tips in gedachten:

- **Cache vaak gebruikte vormen:** Sla resultaten op in het geheugen om te voorkomen dat hetzelfde woord herhaaldelijk wordt herberekend.  
- **Monitor JVM‑heap:** Grote indexen kunnen de geheugendruk verhogen; stem `-Xmx` hierop af.  
- **Gebruik efficiënte collecties:** `ArrayList` werkt voor kleine sets, maar overweeg voor duizenden vormen `HashSet` om duplicaten snel te elimineren.

**Best Practices**
- Houd de bibliotheek up‑to‑date om te profiteren van prestatie‑patches.  
- Profileer de provider met realistische query‑belastingen om knelpunten vroegtijdig te ontdekken.  

## Conclusie

U heeft nu geleerd hoe u **singular‑meervoudsvormen in Java** kunt **genereren** met een aangepaste `SimpleWordFormsProvider` via GroupDocs.Search. Deze lichtgewicht component kan de relevantie van zoekresultaten en de nauwkeurigheid van linguïstische analyse in veel toepassingen aanzienlijk verbeteren.

**Volgende stappen:**  
- Experimenteer met meer geavanceerde linguïstische regels (onregelmatige meervouden, stemming).  
- Integreer de provider in een indexerings‑pipeline en meet recall‑verbeteringen.  
- Verken andere GroupDocs.Search‑functies zoals synoniemdictionaries en aangepaste analyzers.

**Oproep tot actie:** Probeer de `SimpleWordFormsProvider` vandaag nog aan uw eigen project toe te voegen en zie hoe het uw zoekervaring verrijkt!

## FAQ‑sectie

**1. Wat is GroupDocs.Search voor Java?**  
Het is een krachtige bibliotheek die full‑text zoeken, indexering en linguïstische functies biedt — inclusief de mogelijkheid om aangepaste word‑form providers in te pluggen.

**2. Hoe werkt de SimpleWordFormsProvider?**  
Het genereert alternatieve vormen door eenvoudige suffix‑gebaseerde regels toe te passen (verwijderen van “s/es”, omzetten van “y” naar “is”, en toevoegen van “s/es”).

**3. Kan ik de regels voor woord‑vormgeneratie aanpassen?**  
Zeker. Pas de `getWordForms`‑methode aan om onregelmatige vormen, locale‑specifieke regels of integratie met externe woordenboeken op te nemen.

**4. Wat zijn enkele veelvoorkomende toepassingen voor deze functie?**  
Zoekmachines, tekstanalyse‑pipelines en CMS‑platformen profiteren van het herkennen van enkelvoud‑/meervoudvarianten.

**5. Heb ik een commerciële licentie nodig voor productiegebruik?**  
Ja — hoewel een proefversie u de API laat verkennen, verwijdert een aangeschafte licentie gebruikslimieten en biedt ondersteuning.

---

**Laatst bijgewerkt:** 2026-02-21  
**Getest met:** GroupDocs.Search 25.4 (Java)  
**Auteur:** GroupDocs
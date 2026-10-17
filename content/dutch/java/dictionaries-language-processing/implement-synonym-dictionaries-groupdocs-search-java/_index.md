---
date: '2026-10-17'
description: Leer hoe je synoniemen kunt gebruiken in Java met GroupDocs.Search, importeer
  synoniemdictionaries, beheer synoniemgroepen en optimaliseer je zoekindex voor betere
  relevantie.
keywords:
- how to use synonyms
- add synonym support
- manage synonym groups
- import synonym dictionary
- optimize search index
lastmod: '2026-10-17'
og_description: Leer hoe je synoniemen kunt gebruiken in Java met GroupDocs.Search,
  importeer synoniemdictionaries, beheer synoniemgroepen en optimaliseer je zoekindex
  voor betere relevantie.
og_image_alt: Developer guide showing synonym dictionary integration in GroupDocs.Search
  for Java
og_title: Hoe synoniemen te gebruiken in Java met GroupDocs.Search
schemas:
- author: GroupDocs
  dateModified: '2026-10-17'
  description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  headline: How to use synonyms in Java with GroupDocs.Search
  type: TechArticle
- description: Learn how to use synonyms in Java with GroupDocs.Search, import synonym
    dictionaries, manage synonym groups, and optimize your search index for better
    relevance.
  name: How to use synonyms in Java with GroupDocs.Search
  steps:
  - name: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
    text: '**Content management systems (CMS):** Users find articles even when they
      use alternative terminology.'
  - name: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
    text: '**E‑commerce platforms:** Product searches become tolerant to synonyms
      like “laptop” vs. “notebook”.'
  - name: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
    text: '**Document repositories:** Legal or medical archives benefit from domain‑specific
      synonym groups, improving discoverability for professionals.'
  type: HowTo
- questions:
  - answer: Any modern OS with a compatible JDK (Java 8 or newer) is sufficient.
    question: What is the minimum system requirement for using GroupDocs.Search?
  - answer: Update it whenever new terminology emerges—use `clear()` followed by `addRange()`
      for a clean refresh.
    question: How often should I refresh my synonym dictionary?
  - answer: A free trial works for evaluation, but a license is required for production
      deployments.
    question: Can I run GroupDocs.Search without purchasing a license?
  - answer: Split data into logical batches, monitor heap usage, and schedule regular
      index maintenance.
    question: What are best practices for indexing large data sets?
  - answer: Verify that the dictionary is correctly imported, that `setUseSynonymSearch(true)`
      is active, and that the terms are present in the synonym groups.
    question: I’m not seeing expected synonym matches—what should I check?
  type: FAQPage
tags:
- synonym search
- GroupDocs.Search
- Java search indexing
- document retrieval
title: Hoe synoniemen te gebruiken in Java met GroupDocs.Search
type: docs
url: /nl/java/dictionaries-language-processing/implement-synonym-dictionaries-groupdocs-search-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe synoniemen te gebruiken in Java met GroupDocs.Search

Als je wilt dat je gebruikers de juiste inhoud vinden, zelfs wanneer ze verschillende woorden typen, **search with synonyms** is het antwoord. In deze gids leer je hoe je een synoniemwoordenboek maakt, het importeert of exporteert, synoniemgroepen beheert en een zoekopdracht uitvoert die automatisch zoekopdrachten uitbreidt met die synoniemen. Of je nu een CMS, een e‑commercecatalogus of een juridisch documentarchief bouwt, het toevoegen van synoniemondersteuning kan de relevantie en conversieratio's drastisch verhogen.

## Snelle antwoorden
- **Wat is de eerste stap om synoniemen toe te voegen?** Maak een `Index`‑instantie aan en werk met de `SynonymDictionary` API.  
- **Kan ik een kant‑klaar synoniemwoordenboek importeren?** Ja – roep `importDictionary(path)` aan met de bestandslocatie.  
- **Hoe schakel ik synonym‑aware zoeken in?** Schakel `SearchOptions.setUseSynonymSearch(true)` in.  
- **Is het mogelijk om synoniemgroepen tijdens runtime te bewerken?** Absoluut – je kunt groepen wissen, toevoegen of ophalen via de dictionary‑API.  
- **Wat moet ik in de gaten houden bij het schalen van de index?** Verwijder regelmatig ongebruikte items en stem de JVM‑heap af voor grote synoniem‑bestanden.

## Wat is search with synonyms?
**Search with synonyms** betekent dat de engine een set woorden of zinnen als uitwisselbaar beschouwt. Wanneer een gebruiker **“better”** typt, zoekt de engine ook naar **“improve”**, **“enhance”**, of elke andere term die je in dezelfde synoniemgroep hebt gedefinieerd, en levert rijkere resultaten zonder de zoekopdracht van de gebruiker te wijzigen.

## Waarom synoniemondersteuning inschakelen in GroupDocs.Search?
Het inschakelen van synoniemondersteuning laat de engine automatisch zoekopdrachten uitbreiden met equivalente termen, wat de relevantie van resultaten verbetert, de gebruikerstevredenheid verhoogt en de conversieratio's voor e‑commerce- of content‑gedreven sites kan verhogen. Het centraliseert ook het beheer van terminologie, waardoor de onderhoudslast over meerdere applicaties wordt verminderd.

## Vereisten
- GroupDocs.Search voor Java versie **25.4** of nieuwer.  
- Een Java IDE (IntelliJ IDEA, Eclipse, enz.) met Maven‑ondersteuning.  
- Basiskennis van Java en vertrouwdheid met de Maven‑projectstructuur.

### Vereiste bibliotheken en versies
- GroupDocs.Search voor Java **25.4** of hoger.

### Omgevingsconfiguratie
- IDE naar keuze (IntelliJ IDEA, Eclipse, enz.).  
- Maven voor afhankelijkheidsbeheer.

### Kennisvereisten
- Object‑georiënteerd programmeren in Java.  
- Basis bestands‑I/O‑bewerkingen.

## GroupDocs.Search voor Java instellen

### Installatie‑informatie
Add the repository and dependency to your `pom.xml`:

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

**Direct download** – je kunt de nieuwste JAR ook downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie:** Test kernfuncties zonder licentie.  
- **Tijdelijke licentie:** Breid proefmogelijkheden uit tijdens evaluatie.  
- **Aankoop:** Vereist voor productiegebruik en de volledige functionaliteit.

#### Basisinitialisatie en -configuratie
Maak een `Index`‑instantie aan en voeg vervolgens documenten toe die doorzoekbaar zijn:

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Index";
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath2";

// Creating an index in the specified folder
Index index = new Index(indexFolder);

// Adding documents from a specific folder to the index
index.add(documentsFolder);
```

## Hoe synoniemen toe te voegen aan je zoekindex

### Functie 1: een index maken en indexeren
De `Index`‑klasse vertegenwoordigt een doorzoekbare verzameling documenten die op schijf of in het geheugen zijn opgeslagen.  

```java
// Create an index in the specified folder
Index index = new Index(indexFolder);

// Add documents from the given folder to the index
index.add(documentsFolder);
```

### Functie 2: synoniemen ophalen voor een woord
`SynonymDictionary` beheert synoniemgroepen en biedt methoden om synoniemen voor een term op te vragen.  

```java
String[] synonyms = index.getDictionaries().getSynonymDictionary().getSynonyms("make");
```

### Functie 3: synoniemgroepen ophalen
`SynonymDictionary.getGroups()` retourneert een lijst van alle gedefinieerde synoniemgroepen met hun identifiers.  

```java
String[][] synonymGroups = index.getDictionaries().getSynonymDictionary().getSynonymGroups("make");
```

### Functie 4: synoniemwoordenboek‑items beheren
`add(word, synonym)` voegt een nieuwe synoniemrelatie toe aan het woordenboek. `clear()` verwijdert alle items, en `remove(word)` verwijdert een specifieke term uit het woordenboek.  

```java
if (index.getDictionaries().getSynonymDictionary().getCount() > 0) {
    index.getDictionaries().getSynonymDictionary().clear();
}

String[][] newSynonymGroups = new String[][]{
    new String[] { "achieve", "accomplish", "attain", "reach" },
    new String[] { "accept", "take", "have" },
    new String[] { "improve", "better" }
};

index.getDictionaries().getSynonymDictionary().addRange(newSynonymGroups);
```

### Functie 5: synoniemen exporteren naar een bestand
`exportDictionary(path)` schrijft het huidige synoniemwoordenboek naar een binair .dat‑bestand op de opgegeven locatie.  

```java
String exportFilePath = "YOUR_OUTPUT_DIRECTORY/AdvancedUsage/ManagingDictionaries/SynonymDictionary/Synonyms.dat";
index.getDictionaries().getSynonymDictionary().exportDictionary(exportFilePath);
```

### Functie 6: synoniemen importeren uit een bestand
`importDictionary(path)` laadt een eerder geëxporteerd .dat‑bestand in het synoniemwoordenboek.  

```java
index.getDictionaries().getSynonymDictionary().importDictionary(exportFilePath);
```

### Functie 7: zoeken uitvoeren met synoniemondersteuning
`SearchOptions` configureert het gedrag van de query, inclusief of synoniemuitbreiding is ingeschakeld. `setUseSynonymSearch(true)` schakelt synonym‑aware zoeken in voor de komende query.  

```java
String query = "better";
SearchOptions options = new SearchOptions();
options.setUseSynonymSearch(true);

SearchResult result = index.search(query, options);
```

## Hoe te zoeken met synoniemen
Laad je `Index`, schakel synoniemzoeken in, en voer een query uit. De engine breidt de query automatisch uit met behulp van het synoniemwoordenboek dat je hebt gebouwd of geïmporteerd, en retourneert overeenkomsten voor alle gerelateerde termen.

## Hoe een synoniemwoordenboek te importeren
Als je al een `.dat`‑bestand hebt dat door een andere omgeving is voorbereid, roep dan simpelweg `importDictionary(path)` aan. Dit is ideaal voor het synchroniseren van woordenboeken tussen ontwikkelings-, test‑ en productie‑servers.

## Hoe synoniemgroepen te beheren
Synoniemgroepen laten je een set termen behandelen als één logische entiteit. Het toevoegen, wissen of ophalen van groepen gebeurt via de `SynonymDictionary`‑API, zoals getoond in de bovenstaande code‑fragmenten.

## Hoe de zoekindex te optimaliseren
- **Regelmatig ongebruikte items verwijderen:** Gebruik `clear()` vóór bulk‑updates.  
- **JVM‑heap aanpassen:** Grote woordenboeken kunnen meer geheugen vereisen; verhoog de `-Xmx`‑parameter dienovereenkomstig.  
- **Houd de bibliotheek up‑to‑date:** Nieuwe releases bevatten prestatieverbeteringen en bugfixes.

## Praktische toepassingen
1. **Content management systemen (CMS):** Gebruikers vinden artikelen zelfs wanneer ze alternatieve terminologie gebruiken.  
2. **E‑commerceplatforms:** Productzoekopdrachten worden tolerant voor synoniemen zoals “laptop” versus “notebook”.  
3. **Documentopslagplaatsen:** Juridische of medische archieven profiteren van domeinspecifieke synoniemgroepen, waardoor de vindbaarheid voor professionals verbetert.

## Prestatie‑overwegingen
- **Indexopslag optimaliseren:** Bouw de index periodiek opnieuw op om verouderde gegevens te verwijderen.  
- **Geheugengebruik beheren:** Houd het heap‑verbruik in de gaten bij het laden van grote synoniem‑bestanden; een woordenboek van 500 MB vereist doorgaans een 2 GB heap op een 64‑bit JVM.  
- **Regelmatige updates:** Blijf op de nieuwste GroupDocs.Search‑versie voor bugfixes en snelheidsverbeteringen.

## Veelvoorkomende problemen en oplossingen
| Probleem | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Geen synoniemmatches verschijnen | `setUseSynonymSearch(true)` niet ingesteld of woordenboek niet geïmporteerd | Controleer of de optie is ingeschakeld en of het woordenboekbestand bestaat. |
| Out‑of‑memory‑fouten tijdens import | Zeer groot `.dat`‑bestand overschrijdt JVM‑heap | Verhoog de `-Xmx`‑heap‑grootte of importeer in kleinere batches. |
| Dubbele items in resultaten | Dezelfde term verschijnt in meerdere synoniemgroepen | Consolideer overlappende groepen met `clear()` gevolgd door `addRange()`. |

## Veelgestelde vragen

**Q: Wat is de minimale systeemvereiste voor het gebruik van GroupDocs.Search?**  
A: Elk modern besturingssysteem met een compatibele JDK (Java 8 of nieuwer) is voldoende.

**Q: Hoe vaak moet ik mijn synoniemwoordenboek vernieuwen?**  
A: Werk het bij zodra er nieuwe terminologie ontstaat — gebruik `clear()` gevolgd door `addRange()` voor een schone vernieuwing.

**Q: Kan ik GroupDocs.Search gebruiken zonder een licentie aan te schaffen?**  
A: Een gratis proefversie werkt voor evaluatie, maar een licentie is vereist voor productie‑implementaties.

**Q: Wat zijn de beste praktijken voor het indexeren van grote datasets?**  
A: Splits data in logische batches, houd heap‑gebruik in de gaten, en plan regelmatige indexonderhoud.

**Q: Ik zie niet de verwachte synoniemmatches — wat moet ik controleren?**  
A: Controleer of het woordenboek correct is geïmporteerd, of `setUseSynonymSearch(true)` actief is, en of de termen aanwezig zijn in de synoniemgroepen.

## Bronnen
- [Documentatie](https://docs.groupdocs.com/search/java/)  
- [API‑referentie](https://reference.groupdocs.com/search/java)  
- [Download GroupDocs.Search voor Java](https://releases.groupdocs.com/search/java/)  
- [GitHub‑repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/search/10)  
- [Tijdelijke licentie‑acquisitie](https://purchase.groupdocs.com/temporary-license/) 

---

**Laatste update:** 2026-10-17  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Maak en beheer GroupDocs Search Java-index](/search/java/indexing/create-manage-groupdocs-search-java-index/)
- [Java Full Text Search Library – Index optimaliseren met GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
- [Java Fuzzy Search: Documenten toevoegen aan index met GroupDocs.Search](/search/java/searching/groupdocs-search-java-advanced-text-search-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
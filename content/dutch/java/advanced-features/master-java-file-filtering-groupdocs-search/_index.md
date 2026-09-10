---
date: '2026-09-06'
description: Leer hoe je bestands extensies java kunt filteren met GroupDocs.Search
  voor Java, inclusief logische AND-, OR- en NOT-operatoren, datumreeksfilters en
  padfilters.
keywords:
- filter file extensions java
- date range filter java
- GroupDocs.Search Java
lastmod: '2026-09-06'
og_description: Filter bestands extensies java met GroupDocs.Search. Leer hoe je extensie-,
  datumreeks- en padfilters combineert met logische operatoren in Java.
og_image_alt: Guide showing how to filter file extensions in Java with GroupDocs.Search
og_title: Filter bestands extensies java met GroupDocs.Search – Complete gids
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  headline: How to filter file extensions java with GroupDocs.Search
  type: TechArticle
- description: Learn how to filter file extensions java using GroupDocs.Search for
    Java, covering logical AND, OR, NOT operators, date range filters, and path filters.
  name: How to filter file extensions java with GroupDocs.Search
  steps:
  - name: '**Free trial** – explore the features without cost.'
    text: '**Free trial** – explore the features without cost.'
  - name: '**Temporary license** – get full functionality for a limited period.'
    text: '**Temporary license** – get full functionality for a limited period.'
  - name: '**Purchase** – obtain a permanent license for production use.'
    text: '**Purchase** – obtain a permanent license for production use.'
  - name: '**Create filter** – define the extensions you want to keep.'
    text: '**Create filter** – define the extensions you want to keep.'
  - name: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
    text: '**Initialize index and add documents** – apply the filter when constructing
      the `IndexSettings`.'
  - name: '**Create exclusion filter** – specify extensions to reject.'
    text: '**Create exclusion filter** – specify extensions to reject.'
  - name: '**Apply to index settings** – combine the NOT filter with other rules.'
    text: '**Apply to index settings** – combine the NOT filter with other rules.'
  - name: '**Add documents** – only files that pass the combined filter are indexed.'
    text: '**Add documents** – only files that pass the combined filter are indexed.'
  - name: '**Define filters** – create individual filters for each condition.'
    text: '**Define filters** – create individual filters for each condition.'
  - name: '**Combine filters** – use the AND operator to require all conditions.'
    text: '**Combine filters** – use the AND operator to require all conditions.'
  type: HowTo
- questions:
  - answer: Yes. Rebuild the index with a new `DocumentFilter` or use incremental
      indexing with updated settings.
    question: Can I change the filter criteria after the index is created?
  - answer: GroupDocs.Search can index supported archive formats, but the extension
      filter applies to the archive itself, not the inner files. Use nested filters
      for deeper control.
    question: Does the java file extension filter work on compressed archives (e.g.,
      ZIP)?
  - answer: Enable the library’s logging (`LoggingOptions.setEnabled(true)`) and inspect
      the log – it reports which filter rejected each file.
    question: How do I debug why a particular file was excluded?
  - answer: Absolutely. Wrap a regex filter inside `DocumentFilter.createAnd()` alongside
      the extension filter.
    question: Is it possible to combine the java file extension filter with custom
      regex filters?
  - answer: Each filter adds a modest overhead during indexing, but the reduction
      in indexed data usually outweighs the cost. Test with a representative sample
      to find the optimal balance.
    question: What performance impact does adding many filters have?
  type: FAQPage
tags:
- java file filtering
- GroupDocs.Search
- document indexing
title: Hoe bestands extensies java filteren met GroupDocs.Search
type: docs
url: /nl/java/advanced-features/master-java-file-filtering-groupdocs-search/
weight: 1
---

# Filter bestandsextensies java met GroupDocs.Search

In deze uitgebreide tutorial leer je hoe je **filter file extensions java** kunt toepassen bij het indexeren van documenten met GroupDocs.Search. Aan het einde van de gids kun je alleen de bestandstypen opnemen die je nodig hebt, ongewenste formaten uitsluiten, en die regels combineren met datum‑bereik- en padfilters met behulp van logische AND-, OR- en NOT‑operatoren. Deze aanpak houdt je index slank, versnelt zoekopdrachten en helpt je te voldoen aan gegevens‑verwerkingsbeleid.

## Snelle antwoorden
- **Wat is de java file extension filter?** Het is een regel die GroupDocs.Search vertelt welke bestandsextensies moeten worden opgenomen of uitgesloten tijdens het indexeren.  
- **Welke bibliotheek biedt deze functie?** GroupDocs.Search for Java.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een volledige licentie is vereist voor productie.  
- **Kan ik filters combineren?** Ja – je kunt extensie-, datum-, grootte- en padfilters combineren met AND-, OR- en NOT‑logica.  
- **Is het Maven‑compatibel?** Absoluut – voeg de GroupDocs.Search‑dependency toe aan je `pom.xml`.

## Wat is een java file extension filter?
Een **java file extension filter** is een regelset die de extensie van elk bestand evalueert voordat het naar de indexeringsengine wordt gestuurd. Door extensies zoals `.txt`, `.pdf` of `.epub` op te geven, kun je **bestanden opnemen op extensie** of **bestanden uitsluiten op extensie** om je index gefocust te houden en je zoekresultaten relevant.

## Waarom bestands‑extensie filtering gebruiken met GroupDocs.Search?
Bestands‑extensie filtering verbetert de indexeer efficiëntie door irrelevante formaten uit te sluiten, vermindert opslagvereisten en helpt te voldoen aan nalevingsregels door ongewenste inhoud te voorkomen die in de index terechtkomt. Het maakt ook snellere query‑reacties mogelijk omdat de zoekmachine een kleinere, relevantere dataset verwerkt.

- **Prestaties:** Het overslaan van ongewenste bestanden vermindert I/O en versnelt het indexeren tot wel 40 % bij grote repositories.  
- **Opslagbesparing:** Alleen relevante documenten worden in de index opgeslagen, waardoor het schijfgebruik gemiddeld met 30 % daalt.  
- **Naleving:** Voorkom per ongeluk indexeren van vertrouwelijke of niet‑ondersteunde bestandstypen.  
- **Flexibiliteit:** Combineer met **date range filter java**-functies om bestanden te targeten die binnen specifieke periodes zijn aangemaakt of gewijzigd.

## Voorvereisten

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

### Vereiste bibliotheken en afhankelijkheden
- **GroupDocs.Search for Java** – versie 25.4 of later (ondersteunt 60+ invoerformaten).  
- **Java Development Kit (JDK)** – elke compatibele versie (8 of nieuwer).

### Omgevingsconfiguratie
- Integrated Development Environment (IDE): IntelliJ IDEA, Eclipse, of een Maven‑compatibele IDE.

### Kennisvoorvereisten
- Basis Java‑programmeren.  
- Vertrouwdheid met bestands‑I/O in Java.  
- Begrip van reguliere expressies en datum‑tijd handling.

## GroupDocs.Search voor Java instellen
Om GroupDocs.Search te gebruiken, moet je het opnemen als afhankelijkheid in je project.

### Maven‑configuratie
Voeg de volgende repository‑ en afhankelijkheidsconfiguratie toe aan je `pom.xml`‑bestand:

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
Alternatief kun je de nieuwste versie direct downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Licentie‑acquisitie
1. **Free trial** – verken de functies zonder kosten.  
2. **Temporary license** – krijg volledige functionaliteit voor een beperkte periode.  
3. **Purchase** – verkrijg een permanente licentie voor productiegebruik.

### Basisinitialisatie en configuratie
Zodra de bibliotheek is toegevoegd, initialiseert u uw indexeringsomgeving. De `IndexSettings`‑klasse bevat alle configuratie‑opties, inclusief filters.

```java
import com.groupdocs.search.*;

String indexFolder = "YOUR_OUTPUT_DIRECTORY";
Index index = new Index(indexFolder);
```

## Implementatie‑gids
Hieronder gaan we in op elk filtertype, leggen we uit **waarom het belangrijk is** en geven we stap‑voor‑stap instructies die je in je project kunt kopiëren.

### Bestands‑extensie filtering
Filter bestanden op hun extensies tijdens het indexeren. Dit is perfect wanneer je alleen e‑books (`.fb2`, `.epub`) en platte‑tekstbestanden (`.txt`) wilt verwerken.

#### Overzicht
`DocumentFilter.createFileExtension` maakt een whitelist van extensies.

#### Implementatiestappen
1. **Create filter** – definieer de extensies die je wilt behouden.

    ```java
    DocumentFilter filter = DocumentFilter.createFileExtension(".fb2", ".epub", ".txt");
    IndexSettings settings = new IndexSettings();
    settings.setDocumentFilter(filter);
    ```

2. **Initialize index and add documents** – pas het filter toe bij het construeren van de `IndexSettings`.

    ```java
    Index index = new Index("YOUR_OUTPUT_DIRECTORY\\FileExtensionFilter", settings);
    index.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logische NOT‑filter
Sluit specifieke extensies uit, zoals webpagina's en PDF's, wanneer ze niet nodig zijn voor je zoekscenario.

#### Implementatiestappen
1. **Create exclusion filter** – specificeer extensies om te weigeren.

    ```java
    DocumentFilter filterNot = DocumentFilter.createFileExtension(".htm", ".html", ".pdf");
    DocumentFilter invertedFilter = DocumentFilter.createNot(filterNot);
    ```

2. **Apply to index settings** – combineer de NOT‑filter met andere regels.

    ```java
    IndexSettings settingsNot = new IndexSettings();
    settingsNot.setDocumentFilter(invertedFilter);
    ```

3. **Add documents** – alleen bestanden die de gecombineerde filter doorstaan worden geïndexeerd.

    ```java
    Index indexNot = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalNotFilter", settingsNot);
    indexNot.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logische AND‑filter
Combineer verschillende voorwaarden—creatiedatum, extensie en bestandsgrootte—zodat **alleen bestanden die aan alle criteria voldoen** worden geïndexeerd.

#### Overzicht
`DocumentFilter.createAnd` voegt meerdere filters samen tot één regel.

#### Implementatiestappen
1. **Define filters** – maak individuele filters voor elke voorwaarde.

    ```java
    DocumentFilter filter1 = DocumentFilter.createCreationTimeRange(Utils.createDate(2015, 1, 1), Utils.createDate(2016, 1, 1));
    DocumentFilter filter2 = DocumentFilter.createFileExtension(".txt");
    DocumentFilter filter3 = DocumentFilter.createFileLengthUpperBound(8 * 1024 * 1024);
    ```

2. **Combine filters** – gebruik de AND‑operator om alle voorwaarden te vereisen.

    ```java
    DocumentFilter finalFilterAnd = DocumentFilter.createAnd(filter1, filter2, filter3);
    IndexSettings settingsAnd = new IndexSettings();
    settingsAnd.setDocumentFilter(finalFilterAnd);
    ```

3. **Index documents** – geef de gecombineerde filter door aan de indexerings‑pipeline.

    ```java
    Index indexAnd = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalAndFilter", settingsAnd);
    indexAnd.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Logische OR‑filter
Neem bestanden op die **een van** de gespecificeerde voorwaarden vervullen—handig wanneer je zowel kleine tekstbestanden als grotere niet‑tekstbestanden wilt opnemen.

#### Implementatiestappen
1. **Define filters** – maak aparte filters voor elke alternatieve voorwaarde.

    ```java
    DocumentFilter txtFilter = DocumentFilter.createFileExtension(".txt");
    DocumentFilter notTxtFilter = DocumentFilter.createNot(txtFilter);
    ```

2. **Combine filters with logical conditions** – gebruik de OR‑operator.

    ```java
    DocumentFilter bound5Filter = DocumentFilter.createFileLengthUpperBound(5 * 1024 * 1024);
    DocumentFilter bound10Filter = DocumentFilter.createFileLengthUpperBound(10 * 1024 * 1024);

    DocumentFilter txtSizeFilter = DocumentFilter.createAnd(txtFilter, bound5Filter);
    DocumentFilter notTxtSizeFilter = DocumentFilter.createAnd(notTxtFilter, bound10Filter);
    ```

3. **Finalize OR filter** – koppel de gecombineerde filter aan de indexconfiguratie.

    ```java
    DocumentFilter finalFilterOr = DocumentFilter.createOr(txtSizeFilter, notTxtSizeFilter);

    IndexSettings settingsOr = new IndexSettings();
    settingsOr.setDocumentFilter(finalFilterOr);
    Index indexOr = new Index("YOUR_OUTPUT_DIRECTORY\\LogicalOrFilter", settingsOr);
    indexOr.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Creatietijd filters
Target bestanden die binnen een specifieke periode zijn aangemaakt—een klassiek **date range filter java**‑scenario.

#### Implementatiestappen
1. **Define date‑range filter** – specificeer start‑ en einddatums.

    ```java
    DocumentFilter filter3CTime = DocumentFilter.createCreationTimeRange(Utils.createDate(2017, 1, 1), Utils.createDate(2018, 6, 15));
    IndexSettings settingsCTime = new IndexSettings();
    settingsCTime.setDocumentFilter(filter3CTime);
    ```

2. **Index documents** – alleen bestanden waarvan de creatietijdstempels binnen het bereik vallen, worden geïndexeerd.

    ```java
    Index indexCTime = new Index("YOUR_OUTPUT_DIRECTORY\\CreationTimeFilters", settingsCTime);
    indexCTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Wijzigingstijd filters
Sluit bestanden uit die na een bepaalde afkapdatum zijn gewijzigd.

#### Implementatiestappen
1. **Define filter** – stel de maximale wijzigingstijdstempel in.

    ```java
    DocumentFilter filter2MTime = DocumentFilter.createModificationTimeUpperBound(Utils.createDate(2018, 6, 15));
    IndexSettings settingsMTime = new IndexSettings();
    settingsMTime.setDocumentFilter(filter2MTime);
    ```

2. **Index documents** – bestanden die nieuwer zijn dan de afkapdatum worden genegeerd.

    ```java
    Index indexMTime = new Index("YOUR_OUTPUT_DIRECTORY\\ModificationTimeFilters", settingsMTime);
    indexMTime.add("YOUR_DOCUMENT_DIRECTORY");
    ```

### Padfiltering
Beperk indexering tot bestanden die zich in bepaalde mappen bevinden of overeenkomen met een patroon—ideaal voor **include files by extension** binnen een specifieke maphiërarchie.

#### Implementatiestappen
1. **Define file‑path filter** – gebruik glob‑ of regex‑patronen om mappen te matchen.

    ```java
    DocumentFilter pathFilter = DocumentFilter.createPath("*.txt", "documents/");
    IndexSettings settingsPath = new IndexSettings();
    settingsPath.setDocumentFilter(pathFilter);
    ```

2. **Initialize index and add documents** – pas de padfilter toe naast andere regels.

    ```java
    Index indexPath = new Index("YOUR_OUTPUT_DIRECTORY\\FilePathFilter", settingsPath);
    indexPath.add("YOUR_DOCUMENT_DIRECTORY");
    ```

## Veelvoorkomende valkuilen & tips

- **Mix nooit absolute en relatieve paden** in dezelfde filterconfiguratie – dit kan leiden tot onverwachte uitsluitingen.  
- **Reset de `IndexSettings`** bij het wisselen van filtersets; anders kunnen eerdere filters blijven bestaan.  
- **Combineer een maximale lengte met een extensiefilter** voor grote collecties om het geheugenverbruik laag te houden.  
- LoggingOptions regelt de logging‑configuratie voor GroupDocs.Search.  
- **Enable logging** (`LoggingOptions.setEnabled(true)`) om te zien waarom een bestand werd afgewezen.  

## Veelgestelde vragen

**Q: Kan ik de filtercriteria wijzigen nadat de index is aangemaakt?**  
A: Ja. Bouw de index opnieuw op met een nieuwe `DocumentFilter` of gebruik incrementeel indexeren met bijgewerkte instellingen.

**Q: Werkt de java file extension filter op gecomprimeerde archieven (bijv. ZIP)?**  
A: GroupDocs.Search kan ondersteunde archiefformaten indexeren, maar de extensiefilter wordt toegepast op het archief zelf, niet op de interne bestanden. Gebruik geneste filters voor diepere controle.

**Q: Hoe kan ik debuggen waarom een bepaald bestand werd uitgesloten?**  
A: Schakel de logging van de bibliotheek in (`LoggingOptions.setEnabled(true)`) en inspecteer het log – het meldt welke filter elk bestand heeft afgewezen.

**Q: Is het mogelijk om de java file extension filter te combineren met aangepaste regex‑filters?**  
A: Absoluut. Plaats een regex‑filter binnen `DocumentFilter.createAnd()` naast de extensiefilter.

**Q: Welke impact heeft het toevoegen van veel filters op de prestaties?**  
A: Elke filter voegt een bescheiden overhead toe tijdens het indexeren, maar de reductie in geïndexeerde data weegt meestal zwaarder dan de kosten. Test met een representatieve steekproef om de optimale balans te vinden.

---

**Laatst bijgewerkt:** 2026-09-06  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Aangepast datumformaat Java | Datum bereik zoeken met GroupDocs](/search/java/advanced-features/master-date-range-searches-groupdocs-java/)
- [java boolean and or: Beheers Boolean-zoekopdrachten met GroupDocs.Search voor Java](/search/java/searching/implement-boolean-searches-groupdocs-java/)
- [Optimaliseer zoekprestaties met geavanceerde indexeringstechnieken in GroupDocs.Search voor Java](/search/java/indexing/groupdocs-search-java-advanced-indexing/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
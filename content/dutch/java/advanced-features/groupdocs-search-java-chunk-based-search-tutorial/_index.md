---
date: '2025-12-19'
description: Leer hoe je documenten aan de index toevoegt en chunk‑gebaseerd zoeken
  in Java inschakelt met GroupDocs.Search, waardoor de prestaties voor grote documentensets
  worden verbeterd.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Documenten toevoegen aan index met chunk‑gebaseerd zoeken in Java
type: docs
url: /nl/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Documenten toevoegen aan index met chunk‑gebaseerd zoeken in Java

In de data‑gedreven wereld van vandaag is het kunnen **documenten toevoegen aan index** snel en vervolgens chunk‑gebaseerde zoekopdrachten uitvoeren essentieel voor elke applicatie die grote verzamelingen bestanden verwerkt. Of je nu werkt met juridische contracten, archieven van klantenondersteuning of enorme onderzoeksbibliotheken, deze tutorial laat precies zien hoe je GroupDocs.Search voor Java instelt zodat je documenten efficiënt kunt indexeren en relevante informatie in hapklare stukken kunt ophalen.

## Wat je leert
- Hoe je een zoekindex maakt in een opgegeven map.  
- Stappen om **documenten toe te voegen aan index** vanuit meerdere locaties.  
- Zoekopties configureren om chunk‑gebaseerd zoeken in te schakelen.  
- Initiële en daaropvolgende chunk‑gebaseerde zoekopdrachten uitvoeren.  
- Praktijkvoorbeelden waarin chunk‑gebaseerd document zoeken uitblinkt.

## Snelle antwoorden
- **Wat is de eerste stap?** Maak een zoekindexmap.  
- **Hoe voeg ik veel bestanden toe?** Gebruik `index.add()` voor elke documentmap.  
- **Welke optie schakelt chunk‑zoeken in?** `options.setChunkSearch(true)`.  
- **Kan ik blijven zoeken na de eerste chunk?** Ja, roep `index.searchNext()` aan met het token.  
- **Heb ik een licentie nodig?** Een gratis proefversie of tijdelijke licentie werkt voor ontwikkeling; een volledige licentie is vereist voor productie.

## Voorwaarden
- **Vereiste bibliotheken**: GroupDocs.Search for Java 25.4 of later.  
- **Omgevingsinstelling**: Een compatibele Java Development Kit (JDK) geïnstalleerd.  
- **Kennisvereisten**: Basis Java-programmeren en bekendheid met Maven.

## GroupDocs.Search voor Java instellen
Om te beginnen, integreer GroupDocs.Search in je project met Maven:

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

Alternatively, download the latest version from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
- **Gratis proefversie** – test kernfuncties zonder verplichting.  
- **Tijdelijke licentie** – uitgebreide toegang voor ontwikkeling.  
- **Aankoop** – volledige licentie voor productiegebruik.

### Basisinitialisatie en -instelling
Maak een index aan in de map waar je de doorzoekbare gegevens wilt opslaan:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Hoe documenten toe te voegen aan index
Nu de index bestaat, is de volgende logische stap om **documenten toe te voegen aan index** vanuit de locaties waar je bestanden zijn opgeslagen.

### 1. Een index maken
**Overzicht**: Een map instellen voor de zoekindex.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Documenten toevoegen aan index
**Overzicht**: Haal bestanden binnen uit verschillende bronmappen.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Zoekopties configureren voor chunk‑zoeken
Chunk‑gebaseerd zoeken inschakelen door het opties‑object aan te passen.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Initiële chunk‑gebaseerde zoekopdracht uitvoeren
Voer de eerste query uit met de chunk‑ingeschakelde opties.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Chunk‑gebaseerd zoeken voortzetten
Doorloop de resterende chunks totdat het zoeken voltooid is.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Waarom chunk‑gebaseerd zoeken gebruiken?
Chunk‑gebaseerd zoeken splitst enorme documentcollecties op in beheersbare stukken, vermindert geheugenbelasting en versnelt responstijden. Het is vooral nuttig wanneer:

1. **Juridische teams** specifieke clausules moeten vinden in duizenden contracten.  
2. **Klantenondersteuningsportalen** direct relevante kennisbankartikelen moeten tonen.  
3. **Onderzoekers** door uitgebreide datasets moeten bladeren zonder volledige bestanden in het geheugen te laden.

## Prestatie‑overwegingen
- **Geheugenbeheer** – Reserveer voldoende heap‑ruimte (`-Xmx`) voor grote indexen.  
- **Resource‑monitoring** – Houd het CPU‑gebruik in de gaten tijdens indexeren en zoeken.  
- **Indexonderhoud** – Bouw de index periodiek opnieuw op of maak deze schoon om verouderde gegevens te verwijderen.

## Veelvoorkomende valkuilen & probleemoplossing
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` tijdens indexeren | Heap‑grootte te laag | Verhoog de JVM‑heap (`-Xmx2g` of hoger) |
| Geen resultaten teruggegeven | Chunk‑token niet verwerkt | Zorg ervoor dat de `while`‑lus loopt tot `getNextChunkSearchToken()` `null` is |
| Trage zoekprestaties | Index niet geoptimaliseerd | Voer `index.optimize()` uit na bulk‑toevoegingen |

## Veelgestelde vragen

**Q: Wat is chunk‑gebaseerd zoeken?**  
A: Chunk‑gebaseerd zoeken verdeelt de dataset in kleinere stukken, waardoor efficiënte query's over grote hoeveelheden data mogelijk zijn zonder volledige documenten in het geheugen te laden.

**Q: Hoe werk ik mijn index bij met nieuwe bestanden?**  
A: Roep simpelweg `index.add()` aan met het pad naar de nieuwe documenten; de index zal ze automatisch opnemen.

**Q: Kan GroupDocs.Search verschillende bestandsformaten aan?**  
A: Ja, het ondersteunt PDF’s, DOCX, XLSX, PPTX en vele andere gangbare formaten.

**Q: Wat zijn typische prestatie‑knelpunten?**  
A: Geheugenbeperkingen en niet‑geoptimaliseerde indexen zijn het vaakst; reserveer voldoende heap en optimaliseer de index regelmatig.

**Q: Waar vind ik meer gedetailleerde documentatie?**  
A: Bezoek de officiële [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) voor diepgaande handleidingen en API‑referenties.

## Bronnen
- **Documentatie**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API‑referentie**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis ondersteuning**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tijdelijke licentie**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Laatst bijgewerkt:** 2025-12-19  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs
---
date: '2026-02-21'
description: Leer hoe u documenten aan de index toevoegt en de zoekprestaties verbetert
  met chunk‑gebaseerd zoeken in Java met GroupDocs.Search, en optimaliseer het geheugen
  van de Java‑zoekindex voor grote documentensets.
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

In moderne toepassingen die snel **add documents to index** moeten uitvoeren en vervolgens snelle, chunk‑gebaseerde queries willen doen, wilt u een oplossing die schaalt zonder het geheugen te overbelasten. Deze tutorial leidt u door het instellen van GroupDocs.Search voor Java, het toevoegen van meerdere documentmappen, en het configureren van de engine om **increase search performance** te bereiken terwijl het gebruik van **java search index memory** onder controle blijft. Of u nu juridische contracten, supporttickets of onderzoeksartikelen indexeert, de onderstaande stappen bieden een productie‑klare implementatie.

## Quick Answers
- **Wat is de eerste stap?** Create a search index folder.  
- **Hoe voeg ik veel bestanden toe?** Use `index.add()` for each document folder.  
- **Welke optie schakelt chunk search in?** `options.setChunkSearch(true)`.  
- **Kan ik blijven zoeken na de eerste chunk?** Yes, call `index.searchNext()` with the token.  
- **Heb ik een licentie nodig?** A free trial or temporary license works for development; a full license is required for production.  

## What You’ll Learn
- Hoe een zoekindex te maken in een opgegeven map.  
- Stappen om **add documents to index** vanuit meerdere locaties.  
- Zoekopties configureren om chunk‑gebaseerd zoeken in te schakelen.  
- Initiële en daaropvolgende chunk‑gebaseerde zoekopdrachten uitvoeren.  
- Praktijkvoorbeelden waarin chunk‑gebaseerd document zoeken uitblinkt.  

## Prerequisites
Om deze gids te volgen, zorg dat u het volgende heeft:

- **Vereiste bibliotheken**: GroupDocs.Search for Java 25.4 of later.  
- **Omgevingsconfiguratie**: Een compatibele Java Development Kit (JDK) geïnstalleerd.  
- **Kennisvereisten**: Basis Java-programmeren en bekendheid met Maven.

## Setting Up GroupDocs.Search for Java
Om te beginnen, integreer GroupDocs.Search in uw project met Maven:

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

Alternatief kunt u de nieuwste versie downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### License Acquisition
Om GroupDocs.Search uit te proberen:

- **Free Trial** – test core features without commitment.  
- **Temporary License** – extended access for development.  
- **Purchase** – full license for production use.

### Basic Initialization and Setup
Maak een index aan in de map waar u de doorzoekbare gegevens wilt opslaan:

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

## How to add documents to index
Nu de index bestaat, is de volgende logische stap om **add documents to index** vanuit de locaties waar uw bestanden zijn opgeslagen.

### 1. Creating an Index
**Overzicht**: Set up a directory for the search index.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Adding Documents to Index
**Overzicht**: Pull in files from several source folders.

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

### 3. Configuring Search Options for Chunk Search
Chunk‑gebaseerd zoeken inschakelen door het opties‑object aan te passen.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Performing Initial Chunk‑Based Search
Voer de eerste query uit met de chunk‑ingeschakelde opties.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Continuing Chunk‑Based Search
Doorloop de resterende chunks totdat het zoeken voltooid is.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Why use chunk‑based search?
Chunk‑gebaseerd zoeken splitst enorme documentcollecties op in beheersbare stukken, waardoor de geheugenbelasting wordt verminderd en de responstijden worden versneld. Het is vooral nuttig wanneer:

1. **Legal teams** moeten specifieke clausules vinden in duizenden contracten.  
2. **Customer support portals** moeten direct relevante kennisbankartikelen tonen.  
3. **Researchers** doorzoeken uitgebreide datasets zonder volledige bestanden in het geheugen te laden.  

## How this approach **increases search performance**
Door kleinere chunks te zoeken in plaats van volledige bestanden, kan de engine:

- Irrelevante secties vroeg overslaan, waardoor CPU-cycli worden bespaard.  
- Alleen de actieve chunk in het geheugen houden, wat direct het **java search index memory** verbruik verlaagt.  
- Chunk‑verwerking paralleliseren op multi‑core machines voor snellere resultaten.  

## Managing **java search index memory**
Hoewel chunk‑gebaseerd zoeken al de geheugenvoetafdruk verkleint, kunt u de JVM verder afstemmen:

- Voldoende heap toewijzen (`-Xmx2g` of hoger) op basis van de indexgrootte.  
- `index.optimize()` gebruiken na bulk‑toevoegingen om de indexstructuur te comprimeren.  
- GC‑pauzes monitoren met tools zoals VisualVM om latency‑pieken te vermijden.  

## Performance Considerations
- **Geheugenbeheer** – Voldoende heap‑ruimte (`-Xmx`) toewijzen voor grote indexen.  
- **Resource monitoring** – Houd het CPU‑gebruik in de gaten tijdens indexering en zoekoperaties.  
- **Indexonderhoud** – Periodiek de index opnieuw opbouwen of opschonen om verouderde data te verwijderen.  

## Common Pitfalls & Troubleshooting
| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `OutOfMemoryError` tijdens indexering | Heap‑grootte te laag | Verhoog de JVM‑heap (`-Xmx2g` of hoger) |
| Geen resultaten teruggekregen | Chunk‑token niet verwerkt | Zorg dat de `while`‑lus loopt tot `getNextChunkSearchToken()` `null` is |
| Trage zoekprestaties | Index niet geoptimaliseerd | Voer `index.optimize()` uit na bulk‑toevoegingen |

## Frequently Asked Questions

**Q: Wat is chunk‑gebaseerd zoeken?**  
A: Chunk‑gebaseerd zoeken verdeelt de dataset in kleinere stukken, waardoor efficiënte queries over grote hoeveelheden data mogelijk zijn zonder volledige documenten in het geheugen te laden.

**Q: Hoe werk ik mijn index bij met nieuwe bestanden?**  
A: Roep simpelweg `index.add()` aan met het pad naar de nieuwe documenten; de index zal ze automatisch opnemen.

**Q: Kan GroupDocs.Search verschillende bestandsformaten verwerken?**  
A: Ja, het ondersteunt PDF’s, DOCX, XLSX, PPTX en vele andere gangbare formaten.

**Q: Wat zijn typische prestatieknelpunten?**  
A: Geheugenbeperkingen en niet‑geoptimaliseerde indexen zijn het meest voorkomend; wijs voldoende heap toe en optimaliseer de index regelmatig.

**Q: Waar kan ik meer gedetailleerde documentatie vinden?**  
A: Bezoek de officiële [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) voor uitgebreide handleidingen en API‑referenties.

**Q: Werkt chunk‑gebaseerd zoeken met versleutelde PDF’s?**  
A: Ja, zolang u het wachtwoord opgeeft via de juiste API‑overload.

**Q: Hoe kan ik de voortgang van het indexeren monitoren?**  
A: Gebruik de `Index.add()` overload die een `Progress`‑object retourneert of koppel in op logging‑callbacks.

## Resources
- **Documentatie**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API‑referentie**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Download**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis ondersteuning**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tijdelijke licentie**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Laatst bijgewerkt:** 2026-02-21  
**Getest met:** GroupDocs.Search 25.4 for Java  
**Auteur:** GroupDocs
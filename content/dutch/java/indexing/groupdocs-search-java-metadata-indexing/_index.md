---
date: '2026-03-17'
description: Leer hoe u documenten aan de index kunt toevoegen en documenten kunt
  zoeken op metadata met GroupDocs.Search Java. Beheers indexinstellingen, maak indexen,
  voeg documenten toe en voer nauwkeurige zoekopdrachten uit.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Hoe documenten aan de index toevoegen met metadata‑indexering in Java met GroupDocs.Search
type: docs
url: /nl/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Hoe documenten toevoegen aan index met Metadata-indexering in Java met GroupDocs.Search

Het toevoegen van documenten aan een index snel en betrouwbaar is de ruggengraat van elke moderne zoek‑gedreven applicatie. Of je nu een juridisch archief, een klantenondersteunings‑kennisbank of een intern documentportaal bouwt, **metadata-indexering** laat je *documenten zoeken op metadata* zoals auteur, titel of aangepaste tags. In deze tutorial leer je hoe je indexinstellingen configureert, een metadata‑gerichte index maakt, je bestanden toevoegt en nauwkeurige zoekopdrachten uitvoert — allemaal met GroupDocs.Search voor Java.

## Snelle antwoorden
- **Wat is het primaire doel van metadata-indexering?** Het maakt snelle zoekopdrachten mogelijk op basis van documenteigenschappen in plaats van volledige tekstinhoud.  
- **Welke methode voegt bestanden toe aan de index?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Kan ik zoeken op aangepaste metadata‑velden?** Ja, zodra de velden zijn geïndexeerd kun je ze direct queryen.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een tijdelijke proeflicentie is voldoende voor evaluatie; een volledige licentie is vereist voor productie.  
- **Welke Java‑versie is vereist?** JDK 8 of hoger wordt aanbevolen.

## Wat is metadata-indexering in GroupDocs.Search?
Metadata-indexering extraheert en slaat documentattributen op (bijv. auteur, aanmaakdatum, aangepaste tags) in een doorzoekbare structuur. Wanneer je **documenten toevoegt aan de index**, registreert de engine deze attributen, waardoor je nauwkeurige queries kunt uitvoeren zoals “vind alle PDF's geschreven door *John Doe*” of “search pdf by author”.

## Waarom GroupDocs.Search gebruiken voor metadata-indexering?
- **Performance:** Metadata‑zoekopdrachten zijn lichtgewicht en leveren resultaten in milliseconden.  
- **Flexibility:** Ondersteunt een breed scala aan bestandsformaten (PDF, DOCX, PPT, enz.).  
- **Scalability:** Verwerkt miljoenen documenten met een minimale geheugenvoetafdruk.

## Vereisten
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 of nieuwer geïnstalleerd en geconfigureerd.  
- Basiskennis van Java en Maven.

## GroupDocs.Search voor Java instellen

### Installatie‑instructies
Voeg de GroupDocs-repository en afhankelijkheid toe aan je `pom.xml`:

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

Je kunt de nieuwste binaries ook direct downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑verwerving
Om een tijdelijke licentie voor testen te verkrijgen:

1. Bezoek de GroupDocs-website en ga naar de sectie **Purchase**.  
2. Kies een **temporary license**‑plan dat past bij je evaluatiebehoeften.

## Stapsgewijze implementatie

### Functie 1: Configuratie van indexinstellingen
Configureer de index om zich te richten op metadata:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` vertelt de engine om metadata boven volledige‑tekstinhoud te prioriteren.

### Functie 2: Een index maken in een opgegeven map
Maak een fysieke indexmap aan waar alle metadata worden opgeslagen:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Vervang `YOUR_DOCUMENT_DIRECTORY` door het pad dat overeenkomt met je projectstructuur.

### Functie 3: Hoe documenten toevoegen aan de index
Nu de index bestaat, kun je **documenten toevoegen aan de index** zodat ze doorzoekbaar worden:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tips:**  
- Controleer of het mappad correct is en de applicatie leesrechten heeft.  
- GroupDocs.Search extraheert automatisch ondersteunde metadata uit elk bestand.

### Functie 4: Documenten zoeken op metadata
Voer een query uit die zich richt op metadata‑velden, bijvoorbeeld zoeken naar documenten waarbij de taal Engels is:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` doorzoekt de geïndexeerde metadata en retourneert overeenkomende documenten.  
- Je kunt ook **search pdf by author** gebruiken door de naam van de auteur als query‑string te gebruiken.

## Praktische toepassingen
1. **Enterprise Document Management:** Haal contracten op op contractdatum of ondertekenaarnaam.  
2. **Digital Library Catalogs:** Laat gebruikers boeken bladeren op genre, publicatiejaar of auteur.  
3. **CRM Systems:** Zoek snel klantbestanden op met aangepaste metadata zoals klant‑ID of regio.

## Tips en best practices
- **Incremental Updates:** Gebruik `index.addOrUpdate()` voor nieuwe of gewijzigde bestanden in plaats van de hele index opnieuw op te bouwen.  
- **Batch Processing:** Voeg bij duizenden bestanden ze in kleinere batches toe om het geheugenverbruik laag te houden.  
- **Metadata Validation:** Zorg ervoor dat bronbestanden daadwerkelijk de metadata bevatten die je wilt queryen (bijv. auteur‑velden in PDF's).

## Prestatie‑overwegingen
- **Memory Tuning:** Pas de JVM‑heap‑grootte (`-Xmx`) aan op basis van de hoeveelheid geïndexeerde metadata.  
- **Optimized Storage:** Roep periodiek `index.optimize()` aan om de index te comprimeren en de zoek‑snelheid te verbeteren.

## Veelvoorkomende problemen en oplossingen
| Probleem | Oplossing |
|----------|-----------|
| **No results returned** | Bevestig dat de metadata‑velden die je verwacht daadwerkelijk aanwezig zijn in de bronbestanden. |
| **Permission errors** | Zorg ervoor dat het Java‑proces leesrechten heeft voor zowel de documentmap als de indexdirectory. |
| **Out‑of‑memory errors** | Verhoog de JVM‑heap‑grootte of batch de `add`‑operatie om bestanden in kleinere groepen te verwerken. |

## Veelgestelde vragen

**Q: Wat is metadata-indexering?**  
A: Metadata-indexering slaat documentattributen (auteur, titel, aangepaste tags) op in een doorzoekbare structuur, waardoor snelle opzoekingen mogelijk zijn zonder de volledige tekst te scannen.

**Q: Hoe verkrijg ik een tijdelijke licentie?**  
A: Bezoek de GroupDocs‑aankooppagina en volg de stappen om een proeflicentie te verkrijgen.

**Q: Kan ik PDF's indexeren met deze configuratie?**  
A: Ja, GroupDocs.Search ondersteunt PDF, DOCX, PPT en vele andere formaten.

**Q: Wat zijn veelvoorkomende problemen bij het toevoegen van documenten?**  
A: Controleer correcte bestandspaden en zorg ervoor dat de applicatie leesrechten heeft voor de mappen.

**Q: Hoe optimaliseer ik de zoekprestaties?**  
A: Werk je index regelmatig bij, gebruik incrementele toevoegingen en stem de JVM‑geheugeninstellingen af.

## Bronnen
- **Documentatie:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API-referentie:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub-repository:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis ondersteuningsforum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Tijdelijke licentie:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-03-17  
**Getest met:** GroupDocs.Search Java 25.4  
**Auteur:** GroupDocs
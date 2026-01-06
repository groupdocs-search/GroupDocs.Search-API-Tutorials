---
date: '2026-01-06'
description: Leer hoe u documenten aan de index kunt toevoegen en documenten kunt
  zoeken op metadata met GroupDocs.Search Java. Beheers indexinstellingen, maak indexen
  aan, voeg documenten toe en voer nauwkeurige zoekopdrachten uit.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Hoe documenten toevoegen aan index met metadata‑indexering in Java met behulp
  van GroupDocs.Search
type: docs
url: /nl/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Hoe documenten toevoegen aan index met Metadata-indexering in Java met GroupDocs.Search

In moderne applicaties is **documenten toevoegen aan index** snel en betrouwbaar essentieel voor het leveren van snelle zoekervaringen. Of u nu een juridisch archief, een klanten‑support kennisbank of een intern documentportaal bouwt, het benutten van metadata maakt het mogelijk om **documenten zoeken op metadata** zoals auteur, titel of aangepaste tags. Deze gids leidt u door het volledige proces — het configureren van indexinstellingen, het maken van een metadata‑gerichte index, het toevoegen van uw bestanden en het uitvoeren van krachtige zoekopdrachten — allemaal met GroupDocs.Search voor Java.

## Snelle antwoorden
- **Wat is het primaire doel van metadata-indexering?** Het maakt snelle zoekopdrachten mogelijk op basis van documenteigenschappen in plaats van volledige tekstinhoud.  
- **Welke methode voegt bestanden toe aan de index?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Kan ik zoeken op aangepaste metadata‑velden?** Ja, zodra de velden zijn geïndexeerd kunt u ze direct query‑en.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een tijdelijke proeflicentie is voldoende voor evaluatie; een volledige licentie is vereist voor productie.  
- **Welke Java‑versie is vereist?** JDK 8 of hoger wordt aanbevolen.

## Wat is metadata-indexering in GroupDocs.Search?
Metadata-indexering extraheert en slaat documentattributen (bijv. auteur, aanmaakdatum, aangepaste tags) op in een doorzoekbare structuur. Wanneer u **documenten toevoegen aan index**, registreert de engine deze attributen, waardoor u precieze queries kunt uitvoeren zoals “alle PDF’s vinden die zijn geschreven door *John Doe*”.

## Waarom GroupDocs.Search gebruiken voor metadata-indexering?
- **Prestaties:** Metadata‑zoekopdrachten zijn lichtgewicht en leveren resultaten binnen milliseconden.  
- **Flexibiliteit:** Ondersteunt een breed scala aan bestandsformaten (PDF, DOCX, PPT, enz.).  
- **Schaalbaarheid:** Verwerkt miljoenen documenten met een minimale geheugenvoetafdruk.  

## Voorvereisten
- GroupDocs.Search voor Java ≥ 25.4.  
- JDK 8 of nieuwer geïnstalleerd en geconfigureerd.  
- Basiskennis van Java en Maven.  

## GroupDocs.Search voor Java instellen

### Installatie‑instructies
Voeg de GroupDocs‑repository en afhankelijkheid toe aan uw `pom.xml`:

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

U kunt ook de nieuwste binaries rechtstreeks downloaden van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licentie‑acquisitie
Om een tijdelijke licentie voor testen te verkrijgen:

1. Bezoek de GroupDocs‑website en ga naar de sectie **Purchase**.  
2. Kies een **temporary license**‑plan dat past bij uw evaluatiebehoeften.  

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

- `setIndexType(IndexType.MetadataIndex)` geeft de engine de opdracht om metadata boven volledige tekstinhoud te prioriteren.

### Functie 2: Een index maken in een opgegeven map
Maak een fysieke indexdirectory waar alle metadata wordt opgeslagen:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Vervang `YOUR_DOCUMENT_DIRECTORY` door het pad dat overeenkomt met uw projectstructuur.

### Functie 3: Hoe documenten toevoegen aan index
Nu de index bestaat, kunt u **documenten toevoegen aan index** zodat ze doorzoekbaar worden:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tips:**  
- Controleer of het mappad correct is en de applicatie leesrechten heeft.  
- GroupDocs.Search extraheert automatisch ondersteunde metadata uit elk bestand.

### Functie 4: Documenten zoeken op metadata
Voer een query uit die zich richt op metadata‑velden, bijvoorbeeld zoeken naar documenten waarvan de taal Engels is:

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

## Praktische toepassingen
1. **Enterprise Document Management:** Contracten ophalen op contractdatum of ondertekenaarnaam.  
2. **Digitale bibliotheekcatalogi:** Gebruikers laten bladeren op genre, publicatiejaar of auteur.  
3. **CRM‑systemen:** Snel klantbestanden vinden met aangepaste metadata zoals klant‑ID of regio.  

## Prestatie‑overwegingen
- **Incrementele updates:** Gebruik `index.addOrUpdate()` voor nieuwe of gewijzigde bestanden in plaats van de volledige index opnieuw op te bouwen.  
- **Geheugentuning:** Pas de JVM‑heap‑grootte (`-Xmx`) aan op basis van de hoeveelheid geïndexeerde metadata.  
- **Geoptimaliseerde opslag:** Roep periodiek `index.optimize()` aan om de index te comprimeren en de query‑snelheid te verbeteren.

## Veelvoorkomende problemen en oplossingen
| Probleem | Oplossing |
|----------|-----------|
| **Geen resultaten terug** | Controleer of de metadata‑velden die u verwacht daadwerkelijk aanwezig zijn in de bronbestanden. |
| **Toestemmingsfouten** | Zorg ervoor dat het Java‑proces leesrechten heeft voor zowel de documentmap als de indexdirectory. |
| **Out‑of‑memory‑fouten** | Verhoog de JVM‑heap‑grootte of batch de `add`‑operatie om bestanden in kleinere groepen te verwerken. |

## Veelgestelde vragen

**V: Wat is metadata-indexering?**  
A: Metadata-indexering slaat documentattributen (auteur, titel, aangepaste tags) op in een doorzoekbare structuur, waardoor snelle opzoekacties mogelijk zijn zonder de volledige tekst te scannen.

**V: Hoe verkrijg ik een tijdelijke licentie?**  
A: Bezoek de GroupDocs‑aankooppagina en volg de stappen om een proeflicentie aan te vragen.

**V: Kan ik PDF’s indexeren met deze configuratie?**  
A: Ja, GroupDocs.Search ondersteunt PDF, DOCX, PPT en vele andere formaten.

**V: Wat zijn veelvoorkomende problemen bij het toevoegen van documenten?**  
A: Controleer correcte bestands‑paden en zorg ervoor dat de applicatie leesrechten heeft voor de directories.

**V: Hoe optimaliseer ik de zoekprestaties?**  
A: Werk uw index regelmatig bij, gebruik incrementele toevoegingen en stem de JVM‑geheugeninstellingen af.

## Resources

- **Documentatie:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API‑referentie:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub‑repository:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Gratis supportforum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Tijdelijke licentie:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-01-06  
**Getest met:** GroupDocs.Search Java 25.4  
**Auteur:** GroupDocs
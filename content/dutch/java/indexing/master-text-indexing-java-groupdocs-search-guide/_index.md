---
date: '2026-11-02'
description: Leer hoe u een map toevoegt aan de index met GroupDocs.Search in Java,
  high compression configureert en snelle full-text queries uitvoert.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Leer hoe u een map toevoegt aan de index met GroupDocs.Search in Java,
  compression configureert en snelle full-text searches uitvoert. Ideaal voor grote
  documentensets.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Hoe een map toevoegen aan de index met GroupDocs.Search in Java
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  headline: How to add folder to index with GroupDocs.Search in Java
  type: TechArticle
- description: Learn how to add folder to index with GroupDocs.Search in Java, configure
    high compression, and run fast full‑text queries.
  name: How to add folder to index with GroupDocs.Search in Java
  steps:
  - name: define the index folder
    text: 'Choose a directory where the index files will reside:'
  - name: configure index settings
    text: '`TextStorageSettings` configures how text is stored in the index, including
      compression level. `Compression` is an enum that specifies the desired compression
      algorithm.'
  - name: create the index with custom settings
    text: 'Instantiate the index using the configuration defined above:'
  type: HowTo
- questions:
  - answer: It is a robust Java library that provides advanced full‑text search capabilities,
      including indexing, compression, and complex query support.
    question: What is GroupDocs.Search?
  - answer: Enable high compression (`Compression.High`) and periodically commit changes
      to keep the index lean. Also, allocate sufficient heap memory (e.g., 4 GB for
      indexes over 20 GB).
    question: How do I handle large datasets with GroupDocs.Search?
  - answer: Yes, the library can be embedded in any Java‑based backend, REST services,
      or micro‑services architecture.
    question: Can I integrate GroupDocs.Search with existing enterprise systems?
  - answer: Use the `index.add()` method to append new files and `index.delete()`
      to remove obsolete ones, then re‑run `index.optimize()` if needed.
    question: What if my index becomes outdated?
  - answer: Visit the community forum at [GroupDocs forums](https://forum.groupdocs.com/c/search/10)
      for troubleshooting and best‑practice tips.
    question: Where can I get help or support?
  type: FAQPage
tags:
- add folder to index
- groupdocs search
- java search indexing
title: Hoe een map toevoegen aan de index met GroupDocs.Search in Java
type: docs
url: /nl/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Hoe een map toevoegen aan de index met GroupDocs.Search in Java

Als je **java full text search** nodig hebt die kan opschalen tot miljoenen documenten, ben je op de juiste plek. In deze tutorial leer je hoe je **een map toevoegt aan de index** met GroupDocs.Search, high‑compression opslag configureert en razendsnelle queries uitvoert. Aan het einde heb je een productie‑klare oplossing die je in elk Java‑project kunt gebruiken.

## Snelle antwoorden
- **Wat is de primaire bibliotheek?** GroupDocs.Search for Java  
- **Hoe voeg je een map toe aan de index?** Gebruik `index.add(folderPath)`  
- **Kan ik tekstcompressie configureren?** Ja, via `TextStorageSettings(Compression.High)`  
- **Welke Java‑versie is vereist?** JDK 8 of hoger  
- **Waar kan ik een proeflicentie krijgen?** Van de GroupDocs‑website of de repository‑pagina  

## Wat is java full text search en waarom is het belangrijk?

Java full text search zet ruwe documenten om in een omgekeerde index, waardoor sub‑seconde‑opvraging van elke term over duizenden bestanden mogelijk is. Deze mogelijkheid is essentieel voor juridische archieven, onderzoeksbibliotheken en enterprise‑kennisbanken waar gebruikers onmiddellijke resultaten verwachten. Het verbetert ook de productiviteit in moderne applicaties.

## Waarom groupdocs.search gebruiken voor java full text search?

GroupDocs.Search levert hoge‑doorvoersnelheid bij indexeren en query‑uitvoering, terwijl het ingebouwde hoge compressie biedt. Het ondersteunt **50+ invoer‑ en uitvoerformaten**—inclusief PDF, DOCX, EML en HTML—en kan documenten van honderden pagina’s verwerken zonder het volledige bestand in het geheugen te laden, waardoor de geheugengebruik onder 200 MB blijft voor typische workloads.

## Vereisten

- **GroupDocs.Search for Java** (versie 25.4 of later) – de kernbibliotheek die indexeren en zoeken mogelijk maakt.  
- **JDK 8+** geïnstalleerd en geconfigureerd – de minimale runtime die nodig is voor de SDK.  
- **Maven** voor dependency‑beheer – vereenvoudigt het toevoegen van de bibliotheek aan je project.  
- Een IDE zoals **IntelliJ IDEA** of **Eclipse** – voor het schrijven en debuggen van Java‑code.

## GroupDocs.Search voor java instellen

### Maven‑configuratie
Voeg de repository en afhankelijkheid toe aan je `pom.xml`‑bestand:

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
Of download de nieuwste versie van [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Licentie‑acquisitie
- **Gratis proefversie** – verken alle functies zonder verplichting.  
- **Tijdelijke licentie** – verlengde testperiode.  
- **Aankoop** – ontgrendel volledige productie‑functionaliteit.

### Basisinitialisatie en -configuratie
`Index` is de kernklasse die wordt gebruikt om een zoek‑index te maken, te openen en te beheren.

```java
import com.groupdocs.search.Index;

public class InitializeSearch {
    public static void main(String[] args) {
        // Path to store index data
        String indexPath = "path/to/index";
        
        // Creating an index at specified location
        Index index = new Index(indexPath);
        
        System.out.println("GroupDocs.Search initialized successfully!");
    }
}
```

## Indextekst met aangepaste compressie

### Stap 1: definieer de indexmap
Kies een map waarin de indexbestanden worden opgeslagen:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Stap 2: configureer indexinstellingen
`TextStorageSettings` configureert hoe tekst wordt opgeslagen in de index, inclusief compressieniveau. `Compression` is een enum die het gewenste compressie‑algoritme specificeert.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Stap 3: maak de index met aangepaste instellingen
Instantieer de index met de hierboven gedefinieerde configuratie:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Hoe een map toevoegen aan de index

`Index` is de hoofdklasse die de doorzoekbare index vertegenwoordigt.

Laad de bestaande index (of maak een nieuwe) en roep vervolgens de `add`‑methode aan op het `Index`‑object. De `add`‑operatie scant de opgegeven map, extraheert tekst uit elk ondersteund bestand en slaat deze op in de gecomprimeerde index, klaar voor directe zoekopdrachten.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Hoe geïndexeerde documenten zoeken

`SearchResult` vertegenwoordigt een enkele overeenkomst met documentpad en relevantie.

Definieer een zoek‑query‑string die de term of frase die je wilt vinden representeert, en roep vervolgens de `search`‑methode aan op de `Index`‑instantie. De methode retourneert een collectie van `SearchResult`‑objecten, elk met het documentpad, een relevantiescore en een fragment dat de overeenkomst markeert.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Praktische toepassingen

1. **Legal document management** – onmiddellijke opvraging van dossiers.  
2. **Academic research libraries** – snelle opzoeking van papers en scripties.  
3. **Enterprise knowledge bases** – snelle toegang tot handleidingen en FAQ’s.  
4. **Content management systems** – efficiënte content‑ontdekking voor grote sites.  
5. **Customer service archives** – snelle zoekopdracht in eerdere tickets en chats.  

## Prestatie‑overwegingen

- **Compressie vs. snelheid**: Hoge compressie bespaart tot 70 % schijfruimte, maar voegt een bescheiden indexeer‑overhead toe; voer benchmark‑tests uit voor je datavolume.  
- **Geheugenbeheer**: Reserveer minimaal 2 GB heap voor indexen groter dan 10 GB om `OutOfMemoryError` te voorkomen.  
- **Index‑updates**: Voeg geleidelijk nieuwe documenten toe met `index.add()` en roep periodiek `index.optimize()` aan om de index compact te houden.  
- **Query‑optimalisatie**: Gebruik de geavanceerde query‑syntaxis (wildcards, nabijheid, fuzzy search) om resultaten te verfijnen en de responstijd te verkorten.

## Veelvoorkomende valkuilen & pro‑tips

- **Valkuil:** Vergeten `index.optimize()` aan te roepen na bulk‑toevoegingen.  
  **Pro‑tip:** Voer `index.optimize()` elke nacht uit om de index compact te houden.  

- **Valkuil:** De standaard (lage) compressie gebruiken op enorme datasets.  
  **Pro‑tip:** Schakel over naar `Compression.High` voor productie‑omgevingen om opslagkosten te verlagen.  

- **Valkuil:** Geen `IOException` afhandelen bij het toevoegen van bestanden vanaf een netwerkschijf.  
  **Pro‑tip:** Plaats `index.add()` in een try‑catch‑blok en log eventuele fouten voor later onderzoek.  

## Veelgestelde vragen

**Q: Wat is GroupDocs.Search?**  
A: Het is een robuuste Java‑bibliotheek die geavanceerde full‑text search‑functionaliteit biedt, inclusief indexering, compressie en ondersteuning voor complexe queries.

**Q: Hoe ga ik om met grote datasets met GroupDocs.Search?**  
A: Schakel hoge compressie in (`Compression.High`) en commit periodiek wijzigingen om de index slank te houden. Reserveer bovendien voldoende heap‑geheugen (bijv. 4 GB voor indexen groter dan 20 GB).

**Q: Kan ik GroupDocs.Search integreren met bestaande enterprise‑systemen?**  
A: Ja, de bibliotheek kan worden ingebed in elke Java‑gebaseerde backend, REST‑services of micro‑services‑architectuur.

**Q: Wat als mijn index verouderd raakt?**  
A: Gebruik de `index.add()`‑methode om nieuwe bestanden toe te voegen en `index.delete()` om verouderde te verwijderen, en voer vervolgens `index.optimize()` opnieuw uit indien nodig.

**Q: Waar kan ik hulp of ondersteuning krijgen?**  
A: Bezoek het community‑forum op [GroupDocs forums](https://forum.groupdocs.com/c/search/10) voor probleemoplossing en best‑practice tips.

## Aanvullende bronnen

- Gedetailleerde gebruiksgids: [GroupDocs Search Documentation](https://docs.groupdocs.com/search/java/)  
- Volledige API‑referentie: [API Reference Guide](https://reference.groupdocs.com/search/java)  
- Blijf up‑to‑date met nieuwe functies: [Latest Releases](https://releases.groupdocs.com/search/java/)  

---

**Laatst bijgewerkt:** 2026-11-02  
**Getest met:** GroupDocs.Search 25.4  
**Auteur:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Gerelateerde tutorials

- [Groupdocs Search Java Create Index Guide](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Mastering Groupdocs Search Java Index Management Guide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search Library – Optimize Index with GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
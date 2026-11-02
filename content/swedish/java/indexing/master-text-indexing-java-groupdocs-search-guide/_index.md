---
date: '2026-11-02'
description: Lär dig hur du lägger till en mapp i index med GroupDocs.Search i Java,
  konfigurerar hög kompression och kör snabba fulltextfrågor.
keywords:
- add folder to index
- java full text search
- groupdocs search compression
lastmod: '2026-11-02'
og_description: Lär dig hur du lägger till en mapp i index med GroupDocs.Search i
  Java, konfigurerar kompression och utför snabba fulltext‑sökningar. Perfekt för
  stora dokumentuppsättningar.
og_image_alt: Guide showing Java code for adding a folder to a GroupDocs.Search index
og_title: Hur man lägger till mapp i index med GroupDocs.Search i Java
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
title: Hur man lägger till mapp i index med GroupDocs.Search i Java
type: docs
url: /sv/java/indexing/master-text-indexing-java-groupdocs-search-guide/
weight: 1
---

# Hur man lägger till mapp i index med GroupDocs.Search i Java

Om du behöver **java full text search** som kan skalas till miljontals dokument, är du på rätt plats. I den här handledningen kommer du att lära dig hur du **lägga till mapp i index** med GroupDocs.Search, konfigurera lagring med hög kompression och köra blixtsnabba frågor. I slutet har du en produktionsklar lösning som du kan lägga in i vilket Java‑projekt som helst.

## Snabba svar
- **Vad är det primära biblioteket?** GroupDocs.Search for Java  
- **Hur lägger man till en mapp i index?** Använd `index.add(folderPath)`  
- **Kan jag konfigurera textkompression?** Ja, via `TextStorageSettings(Compression.High)`  
- **Vilken Java-version krävs?** JDK 8 eller högre  
- **Var kan man få en provlicens?** Från GroupDocs webbplats eller repositoriets sida  

## Vad är java full text search och varför är det viktigt?
Java full text search omvandlar råa dokument till ett inverterat index, vilket möjliggör undersekunders hämtning av vilken term som helst över tusentals filer. Denna funktion är avgörande för juridiska arkiv, forskningsbibliotek och företagskunskapsbaser där användare förväntar sig omedelbara resultat. Den förbättrar också produktiviteten i moderna applikationer.

## Varför använda groupdocs.search för java full text search?
GroupDocs.Search levererar hög genomströmning vid indexering och frågeexekvering samtidigt som den erbjuder inbyggd hög kompression. Den stöder **50+ input and output formats**—inklusive PDF, DOCX, EML och HTML—och kan bearbeta dokument med flera hundra sidor utan att ladda hela filen i minnet, vilket håller minnesavtrycket under 200 MB för typiska arbetsbelastningar.

## Förutsättningar
- **GroupDocs.Search for Java** (version 25.4 eller senare) – det kärnbibliotek som driver indexering och sökning.  
- **JDK 8+** installerad och konfigurerad – den minsta runtime som krävs för SDK:n.  
- **Maven** för beroendehantering – förenklar att lägga till biblioteket i ditt projekt.  
- En IDE såsom **IntelliJ IDEA** eller **Eclipse** – för att skriva och felsöka Java‑kod.

## Konfigurera GroupDocs.Search för java
### Maven‑konfiguration
Lägg till repositoriet och beroendet i din `pom.xml`‑fil:

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

### Direktnedladdning
Alternativt, ladda ner den senaste versionen från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

#### Licensförvärv
- **Free trial** – utforska alla funktioner utan förpliktelse.  
- **Temporary license** – förlängd testperiod.  
- **Purchase** – lås upp fulla produktionsfunktioner.

### Grundläggande initiering och konfiguration
`Index` är kärnklassen som används för att skapa, öppna och hantera ett sökindex.

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

## Indexera text med anpassad kompression
### Steg 1: definiera indexmappen
Välj en katalog där indexfilerna ska lagras:

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Indexing\\StoringTextOfIndexedDocuments";
```

### Steg 2: konfigurera indexinställningar
`TextStorageSettings` konfigurerar hur text lagras i indexet, inklusive komprimeringsnivå. `Compression` är en enum som specificerar den önskade komprimeringsalgoritmen.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.options.TextStorageSettings;
import com.groupdocs.search.compression.Compression;

IndexSettings settings = new IndexSettings();
settings.setTextStorageSettings(new TextStorageSettings(Compression.High));
```

### Steg 3: skapa indexet med anpassade inställningar
Instansiera indexet med konfigurationen som definierats ovan:

```java
Index index = new Index(indexFolder, settings);
System.out.println("Index created with high compression.");
```

## Hur man lägger till en mapp i index
`Index` är huvudklassen som representerar det sökbara indexet.

Läs in det befintliga indexet (eller skapa ett nytt) och anropa sedan `add`‑metoden på `Index`‑objektet. `add`‑operationen skannar den angivna katalogen, extraherar text från varje stödd fil och lagrar den i det komprimerade indexet, redo för omedelbar sökning.

```java
String documentsFolder = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual document path.
Index index = new Index(indexFolder);
```

## Hur man söker i indexerade dokument
`SearchResult` representerar en enskild matchning med dokumentväg och relevans.

Definiera en sökfrågesträng som representerar den term eller fras du vill hitta, och anropa sedan `search`‑metoden på `Index`‑instansen. Metoden returnerar en samling av `SearchResult`‑objekt, var och en innehåller dokumentvägen, relevanspoängen och ett utdrag som markerar matchen.

```java
index.add(documentsFolder);
System.out.println("Documents added successfully.");
```

## Praktiska tillämpningar
Verkliga scenarier där **java full text search** briljerar:

1. **Legal document management** – omedelbar hämtning av ärendefiler.  
2. **Academic research libraries** – snabb uppslagning av artiklar och avhandlingar.  
3. **Enterprise knowledge bases** – snabb åtkomst till manualer och FAQ.  
4. **Content management systems** – effektiv innehållsupptäckt för stora webbplatser.  
5. **Customer service archives** – snabb sökning i tidigare ärenden och chattar.  

## Prestandaöverväganden
- **Compression vs. speed**: Hög kompression sparar upp till 70 % diskutrymme men tillför en måttlig indexeringskostnad; kör benchmark‑tester för din datavolym.  
- **Memory management**: Tilldela minst 2 GB heap för index större än 10 GB för att undvika `OutOfMemoryError`.  
- **Index updates**: Lägg till nya dokument inkrementellt med `index.add()` och anropa periodiskt `index.optimize()` för att hålla indexet kompakt.  
- **Query optimization**: Använd den avancerade frågesyntaxen (jokertecken, närhet, fuzzy‑sökning) för att begränsa resultat och minska svarstiden.

## Vanliga fallgropar & proffstips
- **Pitfall:** Glömmer att anropa `index.optimize()` efter massiva tillägg.  
  **Pro tip:** Kör `index.optimize()` varje natt för att hålla indexet kompakt.  

- **Pitfall:** Använder standard (låg) kompression på massiva dataset.  
  **Pro tip:** Byt till `Compression.High` för produktionsmiljöer för att minska lagringskostnaderna.  

- **Pitfall:** Hanterar inte `IOException` när filer läggs till från en nätverksdelning.  
  **Pro tip:** Omge `index.add()` med ett try‑catch‑block och logga eventuella fel för senare granskning.  

## Vanliga frågor
**Q: Vad är GroupDocs.Search?**  
A: Det är ett robust Java‑bibliotek som tillhandahåller avancerade full‑text sökfunktioner, inklusive indexering, kompression och stöd för komplexa frågor.

**Q: Hur hanterar jag stora dataset med GroupDocs.Search?**  
A: Aktivera hög kompression (`Compression.High`) och begå förändringar periodiskt för att hålla indexet slimmat. Allokera också tillräckligt med heap‑minne (t.ex. 4 GB för index över 20 GB).

**Q: Kan jag integrera GroupDocs.Search med befintliga företagsystem?**  
A: Ja, biblioteket kan inbäddas i vilken Java‑baserad backend, REST‑tjänst eller mikrotjänstarkitektur som helst.

**Q: Vad händer om mitt index blir föråldrat?**  
A: Använd `index.add()`‑metoden för att lägga till nya filer och `index.delete()` för att ta bort föråldrade, kör sedan `index.optimize()` igen om det behövs.

**Q: Var kan jag få hjälp eller support?**  
A: Besök community‑forumet på [GroupDocs forums](https://forum.groupdocs.com/c/search/10) för felsökning och bästa praxis‑tips.

## Ytterligare resurser
- Detaljerad användarguide: [GroupDocs Search-dokumentation](https://docs.groupdocs.com/search/java/)  
- Fullständig API-referens: [API-referensguide](https://reference.groupdocs.com/search/java)  
- Håll dig uppdaterad med nya funktioner: [Senaste versionerna](https://releases.groupdocs.com/search/java/)  

---

**Senast uppdaterad:** 2026-11-02  
**Testad med:** GroupDocs.Search 25.4  
**Författare:** GroupDocs  

```java
String query = "sample";  
```

```java
import com.groupdocs.search.results.SearchResult;

SearchResult result = index.search(query);
System.out.println("Search completed. Results found: " + result.getDocumentCount());
```

## Relaterade handledningar
- [Groupdocs Search Java Skapa index‑guide](/search/java/indexing/groupdocs-search-java-create-index-guide/)
- [Mästra Groupdocs Search Java Indexhanteringsguide](/search/java/document-management/mastering-groupdocs-search-java-index-management-guide/)
- [Java Full Text Search‑bibliotek – Optimera index med GroupDocs.Search](/search/java/performance-optimization/groupdocs-search-java-index-optimization/)
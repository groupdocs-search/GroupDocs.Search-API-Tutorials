---
date: '2026-09-11'
description: Lär dig hur du markerar sökresultat i Java och indexerar dokument i Java
  med GroupDocs.Search för Java med både synchronous och asynchronous indexering.
keywords:
- highlight search results java
- index documents java
- real time indexing java
lastmod: '2026-09-11'
og_description: Markera sökresultat Java med GroupDocs.Search. Lär dig synchronous
  och asynchronous indexering, real‑time uppdateringar och resultatmarkering i Java‑applikationer.
og_image_alt: Developer guide showing Java code highlighting search results with GroupDocs.Search
og_title: Markera sökresultat Java – Snabb Synchronous & async indexering
schemas:
- author: GroupDocs
  dateModified: '2026-09-11'
  description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  headline: Highlight search results Java – Synchronous & async indexing
  type: TechArticle
- description: Learn how to highlight search results Java and index documents Java
    using GroupDocs.Search for Java with both synchronous and asynchronous indexing.
  name: Highlight search results Java – Synchronous & async indexing
  steps:
  - name: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
    text: '**Install the library** – Use the Maven snippet above or download the JAR
      from [GroupDocs](https://releases.groupdocs.com/search/java/).'
  - name: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
    text: '**Obtain a license** – Start with a trial license; replace it with a production
      key before deployment.'
  - name: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
    text: '**Initialize the index** – The following snippet shows how to create (or
      open) an index folder:'
  type: HowTo
- questions:
  - answer: Yes. Use synchronous indexing for small, frequently updated sets and asynchronous
      indexing for bulk imports or background jobs.
    question: Can I combine synchronous and asynchronous indexing in the same application?
  - answer: Provide a custom `DocumentHighlighter` implementation that writes the
      desired HTML, CSS, or XML tags around matched terms.
    question: How do I customize the highlight style?
  - answer: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML, and many more via built‑in
      parsers—over 30 formats in total.
    question: What file types does GroupDocs.Search support out of the box?
  - answer: Absolutely. GroupDocs.Search includes multi‑language analyzers; just configure
      the appropriate `Analyzer` when creating the index.
    question: Is it possible to search in multiple languages simultaneously?
  - answer: Store the index in a protected directory, set strict file‑system permissions,
      and optionally encrypt the index using the library’s security features.
    question: How do I secure the index folder?
  type: FAQPage
tags:
- highlight search
- groupdocs.search
- java indexing
title: Markera sökresultat Java – Synchronous & async indexering
type: docs
url: /sv/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Markera sökresultat Java – Synkron & async-indexering

I den här guiden kommer du att upptäcka hur du **highlight search results Java** med GroupDocs.Search‑biblioteket, och du kommer att se steg‑för‑steg hur du indexerar dokument Java både synkront och asynkront. Oavsett om du bygger ett litet skrivbordsverktyg eller en storskalig företagsökningstjänst, låter dessa tekniker dig leverera omedelbara, visuellt tydliga träffar utan att blockera dina applikationstrådar.

## Snabba svar
- **Vad betyder “highlight search results Java”?** Det betyder att omsluta varje matchande term i de returnerade snuttarna med markup (t.ex. `<mark>`) så att användarna omedelbart kan se kontexten för träffen.  
- **När bör jag använda synkron indexering?** Använd den för små‑till‑medelstora samlingar där du behöver att dokumentet är sökbart så snart det har lagts till.  
- **När är asynkron indexering att föredra?** Välj den för stora batcher eller när UI‑tråden måste förbli responsiv medan indexet byggs i bakgrunden.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en full licens tar bort begränsningar och låser upp avancerade funktioner.  
- **Vilken Java‑version stöds?** Java 8 eller senare.

## Vad är “highlight search results Java”?
`highlight search results java` är processen att ta råa matchningsdata från GroupDocs.Search och infoga visuella ledtrådar—vanligtvis HTML `<mark>`‑taggar—runt varje hittad term. Detta gör resultatsnuttarna omedelbart läsbara i en webbsida eller Swing‑komponent, vilket förbättrar användarupplevelsen genom att visa exakt var frågan förekommer.

## Varför använda GroupDocs.Search för Java?
GroupDocs.Search levererar en högpresterande, språkagnostisk motor som kan **processa upp till 5 000 dokument per sekund**, **stöda 30+ filformat**, och **indexera samlingar med 10 miljoner dokument** utan att ladda hela korpusen i minnet. Dess inbyggda markering, realtids‑indexering och flerspråkiga analysverktyg gör den idealisk för innehållshanteringssystem, e‑handelskataloger och företagsdokumentarkiv.

## Förutsättningar
- **Java Development Kit** (JDK 8 eller nyare) installerat och `JAVA_HOME` korrekt inställt.  
- En IDE såsom **IntelliJ IDEA** eller **Eclipse**.  
- En mapp (t.ex. `documents/`) som innehåller filerna du vill indexera—vanlig text, PDF, DOCX, etc.  
- Maven för beroendehantering (eller så kan du manuellt lägga till JAR‑filen).

### Nödvändiga bibliotek och beroenden
Lägg till GroupDocs.Search i din Maven `pom.xml`:

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

För direkta nedladdningar, hämta den senaste versionen från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Miljöinställning
- Verifiera att `JAVA_HOME` pekar på en kompatibel JDK.  
- Skapa ett nytt Maven‑projekt och klistra in kodsnutten ovan i `<dependencies>`‑sektionen.  
- Placera exempel filer i en katalog som `src/main/resources/documents/`.

## Hur du installerar GroupDocs.Search för Java
`Index` är kärnklassen som representerar en sökbar samling lagrad på disk.

Skapa en `Index`‑instans som pekar på en mapp på disken, applicera en licens om du har en, och konfigurera eventuellt en analysator för språk‑specifik tokenisering. Detta förberedande steg säkerställer att motorn kan läsa, skriva och söka i indexet effektivt.

`Index`‑klassen är den centrala komponenten som representerar en sökbar samling på disk. Efter att du har instansierat den flödar all indexering och frågeoperationer genom detta objekt.

1. **Install the library** – Use the Maven snippet above or download the JAR from [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Obtain a license** – Start with a trial license; replace it with a production key before deployment.  
3. **Initialize the index** – The following snippet shows how to create (or open) an index folder:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Hur du markerar sökresultat Java – synkron indexering
`DocumentHighlighter` är en verktygsklass som genererar markerade snuttar från sökresultat.

Läs in indexet, lägg till dokument med `index.add(documentPath)`, kör en fråga, och anropa sedan `DocumentHighlighter` för att omsluta matchningar i `<mark>`‑taggar. Hela processen körs på den anropande tråden, så dokumentet blir sökbart omedelbart efter att `add` returnerat för slutanvändarna.

### Steg 1: skapa indexet och bifoga felhantering
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;
import java.nio.file.Paths;

public class SynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/SynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });
```

### Steg 2: lägg till dokument och kör en sökning
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Steg 3: bearbeta resultat och markera sökresultat Java
```java
        for (int i = 0; i < result.getDocumentCount(); i++) {
            FoundDocument document = result.getFoundDocument(i);
            System.out.println(": Document: " + document.getDocumentInfo().getFilePath());
            System.out.println(": Occurrences: " + document.getOccurrenceCount());
        }

        // Highlight results
        if (result.getDocumentCount() > 0) {
            FoundDocument document = result.getFoundDocument(0);
            String path = YOUR_OUTPUT_DIRECTORY + "/Highlighted.html";
            OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
            DocumentHighlighter highlighter = new DocumentHighlighter(outputAdapter);
            index.highlight(document, highlighter);
        }
    }
}
```

## Hur du markerar sökresultat Java – asynkron indexering
`IndexingOptions` konfigurerar hur indexeringsprocessen körs, inklusive synkront eller asynkront läge.

Konfigurera `IndexingOptions` för att köra i bakgrundsläge, prenumerera på `StatusChanged`‑händelser, och låt motorn indexera filer medan ditt UI fortsätter att betjäna andra förfrågningar. När statusen ändras till `Ready` kan du utföra sökningar och få markerade snuttar precis som i synkront läge.

`AsyncIndexingListener` tar emot framstegsuppdateringar, vilket låter dig visa en förloppsindikator eller logga status utan att blockera huvudtråden.

### Steg 1: konfigurera indexet med händelselyssnare
```java
import com.groupdocs.search.*;
import com.groupdocs.search.events.*;

public class AsynchronousIndexingFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY/AsynchronousIndexing";
        String documentsFolder = YOUR_DOCUMENT_DIRECTORY; // Replace with actual directory path

        Index index = new Index(indexFolder);

        // Handle errors and status changes
        index.getEvents().ErrorOccurred.add(new EventHandler<IndexErrorEventArgs>() {
            @Override
            public void invoke(Object sender, IndexErrorEventArgs args) {
                System.out.println(args.getMessage());
            }
        });

        index.getEvents().StatusChanged.add(new EventHandler<BaseIndexEventArgs>() {
            @Override
            public void invoke(Object sender, BaseIndexEventArgs args) {
                if (args.getStatus() != IndexStatus.Ready || args.getStatus() == IndexStatus.Failed) {
                    System.out.println("Indexing completed.");
                }
            }
        });
```

### Steg 2: aktivera asynkront läge och starta indexering
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

## Hur du indexerar dokument Java – praktiska tips
`index.update(path)` uppdaterar ett befintligt dokument i indexet med filen på den angivna sökvägen.

Dela upp stora samlingar i batcher på 1 000–5 000 filer, filtrera efter filändelse för att undvika onödig parsning, och använd `index.update(path)` för ändrade filer istället för att bygga om hela indexet. Dessa metoder håller minnesanvändningen låg och indexeringstiden förutsägbar för att upprätthålla konsistens.

- **Batch size**: För enorma samlingar, dela upp mappen i mindre batcher för att undvika minnesspikar.  
- **File filters**: Använd `IndexingOptions.setFileExtensions` för att inkludera endast de format du behöver (t.ex. `.pdf`, `.docx`).  
- **Re‑indexing**: När ett dokument ändras, anropa `index.update(documentPath)` snarare än att återskapa indexet från grunden.

## Prestandaöverväganden
- **Memory**: Övervaka heap‑användning; öka `-Xmx` om du bearbetar många stora filer samtidigt.  
- **CPU**: Asynkron indexering sprider arbetsbelastningen över trådar men förbrukar fortfarande CPU—spåra användning med JVisualVM.  
- **Result highlighting**: Markering lägger till en måttlig overhead (≈ 2–5 ms per resultat). Cacha den genererade HTML‑koden om du behöver visa samma snuttar upprepade gånger.

## Vanliga frågor

**Q: Kan jag kombinera synkron och asynkron indexering i samma applikation?**  
A: Ja. Använd synkron indexering för små, ofta uppdaterade mängder och asynkron indexering för bulk‑import eller bakgrundsjobb.

**Q: Hur anpassar jag markeringsstilen?**  
A: Tillhandahåll en egen `DocumentHighlighter`‑implementation som skriver önskad HTML, CSS eller XML‑taggar runt matchade termer.

**Q: Vilka filtyper stöder GroupDocs.Search direkt?**  
A: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML och många fler via inbyggda parsers—över 30 format totalt.

**Q: Är det möjligt att söka i flera språk samtidigt?**  
A: Absolut. GroupDocs.Search inkluderar flerspråkiga analysatorer; konfigurera bara rätt `Analyzer` när du skapar indexet.

**Q: Hur skyddar jag indexmappen?**  
A: Förvara indexet i en skyddad katalog, sätt strikta filsystem‑behörigheter och kryptera eventuellt indexet med bibliotekets säkerhetsfunktioner.

---

**Senast uppdaterad:** 2026-09-11  
**Testat med:** GroupDocs.Search 25.4 för Java  
**Författare:** GroupDocs

## Relaterade handledningar

- [Hur man skapar dokumentindex och lägger till dokument med GroupDocs.Search API för Java](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Hur man skapar indexförråd java med GroupDocs.Search: Effektiv dokumentindexering & sökning](/search/java/searching/master-groupdocs-search-java-indexing-search/)
- [Effektiv dokumentindexering sökning Groupdocs Java](/search/java/indexing/efficient-document-indexing-search-groupdocs-java/)
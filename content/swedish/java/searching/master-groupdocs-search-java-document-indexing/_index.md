---
date: '2026-02-08'
description: Lär dig hur du markerar sökresultat i Java och hur du indexerar dokument
  i Java med GroupDocs.Search för Java med synkron och asynkron indexering.
keywords:
- document search
- synchronous indexing
- asynchronous indexing
title: Markera sökresultat Java – Synkron och asynkron indexering
type: docs
url: /sv/java/searching/master-groupdocs-search-java-document-indexing/
weight: 1
---

# Markera sökresultat Java – Synkron & Asynkron indexering

Boosta dina Java‑applikationer genom **highlighting search results Java** med det kraftfulla GroupDocs.Search‑biblioteket. Oavsett om du hanterar några få filer eller ett massivt arkiv, låter dig behärskning av både synkron och asynkron indexering leverera snabba, exakta resultat utan att blockera dina applikationstrådar.

## Snabba svar
- **Vad betyder “highlight search results Java”?** Det innebär att rendera matchande termer i sökresultaten med visuella ledtrådar (t.ex. HTML‑taggen `<mark>`) så att användarna kan se var frågan förekommer i varje dokument.  
- **När bör jag använda synkron indexering?** För små till medelstora datamängder där omedelbar tillgänglighet av nyinlagda dokument krävs.  
- **När är asynkron indexering att föredra?** När du bearbetar stora dokumentsamlingar eller kör på en UI‑tråd där du måste hålla applikationen responsiv.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en full licens låser upp avancerade funktioner och tar bort användningsgränser.  
- **Vilken Java‑version stöds?** Java 8 eller senare.

## Vad är “highlight search results Java”?
Att markera sökresultat i Java innebär att ta de råa matchningarna som returneras av GroupDocs.Search och omsluta de matchande termerna i HTML (eller annan markup) så att de framträder tydligt när de visas i ett UI eller på en webbsida. Detta förbättrar användarupplevelsen genom att omedelbart visa kontexten för varje träff.

## Varför använda GroupDocs.Search för Java?
GroupDocs.Search erbjuder en högpresterande, språk‑agnostisk motor som stödjer:
- Realtids‑indexering och sökning
- Asynkron bearbetning för stora arbetsbelastningar
- Inbyggd resultatmarkering
- Stöd för flera språk och anpassade analysatorer  

Dessa funktioner gör den idealisk för innehållshanteringssystem, e‑handelskataloger och företagsdokumentarkiv.

## Förutsättningar
Innan du börjar, se till att du har:

- **Java Development Kit** (JDK 8 eller nyare) installerat.  
- En IDE såsom **IntelliJ IDEA** eller **Eclipse**.  
- En mapp som innehåller de dokument du vill indexera.  
- Maven för beroendehantering (eller så kan du ladda ner JAR‑filen manuellt).

### Nödvändiga bibliotek och beroenden
Lägg till GroupDocs.Search i ditt Maven‑projekt:

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
- Verifiera att din **JAVA_HOME** pekar på en kompatibel JDK.  
- Skapa ett projekt i din IDE och lägg till Maven‑konfigurationen ovan.  
- Förbered en katalog (t.ex. `documents/`) med exempel på text‑, PDF‑ eller Word‑filer.

## Hur man konfigurerar GroupDocs.Search för Java
1. **Installera biblioteket** – Använd Maven‑snutten ovan eller ladda ner JAR‑filen från [GroupDocs](https://releases.groupdocs.com/search/java/).  
2. **Skaffa en licens** – Börja med en provlicens, uppgradera sedan när du går i produktion.  
3. **Initiera indexet** – Följande kodsnutt visar hur du skapar (eller öppnar) en indexmapp:

```java
import com.groupdocs.search.Index;

// Create an index in the specified folder
Index index = new Index("path/to/index/folder");
```

## Hur man markerar sökresultat Java – Synkron indexering
Synkron indexering bearbetar dokument omedelbart, så nyinlagda filer blir sökbara direkt.

### Steg 1: Skapa indexet och lägg till felhantering
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

### Steg 2: Lägg till dokument och kör en sökning
```java
        // Add documents
        index.add(documentsFolder);

        // Perform a search
        String query = "tincidunt";
        SearchResult result = index.search(query);
```

### Steg 3: Bearbeta resultat och **highlight search results Java**
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

`DocumentHighlighter` omsluter automatiskt matchande termer med `<mark>`‑taggar (eller vilket format du konfigurerar), vilket ger dig **highlighted search results** redo för visning.

## Hur man markerar sökresultat Java – Asynkron indexering
När du hanterar tusentals filer är det oönskat att blockera huvudtråden. Asynkron indexering låter motorn arbeta i bakgrunden.

### Steg 1: Konfigurera indexet med händelselyssnare
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

### Steg 2: Aktivera asynkront läge och starta indexering
```java
        // Set up async indexing options
        IndexingOptions options = new IndexingOptions();
        options.setAsync(true);

        // Add documents asynchronously
        index.add(documentsFolder, options);
    }
}
```

Medan indexet byggs kan din applikation fortsätta att hantera andra förfrågningar. När `StatusChanged`‑händelsen rapporterar `Ready` kan du säkert köra sökningar och erhålla **highlighted search results Java**.

## Hur man **indexerar dokument java** – Praktiska tips
- **Batch‑storlek**: För enorma samlingar, dela upp mappen i mindre batcher för att undvika minnesspikar.  
- **Filtrering**: Använd `IndexingOptions.setFileExtensions` för att inkludera endast de format du behöver (t.ex. `.pdf`, `.docx`).  
- **Re‑indexering**: När dokument ändras, anropa `index.update(documentPath)` istället för att bygga om hela indexet.

## Prestandaöverväganden
- **Minne**: Håll ett öga på heap‑användningen; öka `-Xmx` om du bearbetar många stora filer.  
- **CPU**: Asynkron indexering sprider arbetsbelastningen, men förbrukar fortfarande CPU—övervaka med JVisualVM.  
- **Resultatmarkering**: Markering lägger till en liten bearbetningskostnad; cacha den genererade HTML‑koden om du behöver visa resultat upprepade gånger.

## Vanliga frågor

**Q: Kan jag kombinera synkron och asynkron indexering i samma applikation?**  
A: Ja. Använd synkron indexering för små, ofta uppdaterade mängder och asynkron indexering för bulk‑import eller bakgrundsjobb.

**Q: Hur anpassar jag markeringsstilen?**  
A: Tillhandahåll en egen `DocumentHighlighter`‑implementation som skriver önskad HTML, CSS eller XML‑tagg runt matchande termer.

**Q: Vilka filtyper stöder GroupDocs.Search direkt?**  
A: Text, PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, HTML och många fler via dess inbyggda parsers.

**Q: Är det möjligt att söka i flera språk samtidigt?**  
A: Absolut. GroupDocs.Search innehåller flerspråkiga analysatorer; konfigurera bara rätt `Analyzer` när du skapar indexet.

**Q: Hur säkrar jag indexmappen?**  
A: Förvara indexet i en skyddad katalog, sätt korrekta filsystembehörigheter och överväg att kryptera indexet med bibliotekets säkerhetsfunktioner.

---

**Senast uppdaterad:** 2026-02-08  
**Testad med:** GroupDocs.Search 25.4 for Java  
**Författare:** GroupDocs
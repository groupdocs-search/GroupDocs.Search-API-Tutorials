---
date: '2026-03-17'
description: Lär dig hur du markerar sökresultat i Java med GroupDocs.Search, konfigurerar
  ett skalbart söknätverk, indexerar dokument, kör frågor och visar markerade utdrag.
keywords:
- GroupDocs.Search Java
- distributed searching Java
- highlight search results Java
title: Hur man markerar sökresultat i Java med GroupDocs.Search
type: docs
url: /sv/java/licensing-configuration/groupdocs-search-java-implementation/
weight: 1
---

**Författare:**". Keep values unchanged.

Now ensure all markdown formatting preserved.

Check for any shortcodes: none.

Check for images: none.

Check for code block placeholders: we kept them.

Now produce final content.# Markera sökresultat Java med GroupDocs.Search

Om du är trött på att manuellt gå igenom ändlösa dokument, **highlight search results java** erbjuder ett snabbt, pålitligt sätt att visa exakt det du behöver. I den här handledningen går vi igenom hur du konfigurerar ett distribuerat söknätverk, indexerar dina filer, kör frågor och slutligen markerar matchningarna direkt i dokumenten. I slutet har du en produktionsklar lösning som kan skalas över flera noder och får relevanta termer att framträda omedelbart.

## Snabba svar
- **Vad betyder “highlight search results java”?** Det hänvisar till att programatiskt markera hittade nyckelord i dokument när man använder Java‑bibliotek som GroupDocs.Search.  
- **Kan jag markera flera termer i samma dokument?** Ja – använd `HighlightOptions` för att definiera hur många termer före/efter varje matchning som visas.  
- **Behöver jag en licens för att köra detta exempel?** En gratis provperiod eller tillfällig licens fungerar för testning; en full licens krävs för produktion.  
- **Vilken Java‑version krävs?** Java 8 eller senare.  
- **Är detta tillvägagångssätt lämpligt för stora dokumentsamlingar?** Absolut – söknätverket distribuerar indexering och frågelast över noder.

## Vad är Highlight Search Results Java?
**Highlight search results java** är processen att ta en sökfråga, lokalisera matchande fragment i dina dokument och visuellt framhäva dessa fragment (t.ex. genom att omge dem med markörer eller returnera dem som markerade utdrag). Detta gör det enkelt för slutanvändare att se sammanhanget för varje matchning utan att öppna hela filen.

## Varför Highlight Search Results Java är viktigt
Att använda **highlight search results java** förbättrar användarupplevelsen genom att visa exakt var en term förekommer, minskar den tid som spenderas på att öppna irrelevanta filer och hjälper efterlevnadsteam att snabbt hitta känslig information. När det kombineras med ett distribuerat söknätverk förblir lösningen responsiv även när dokumentkorpuset växer till miljontals.

## Varför använda GroupDocs.Search för markering?
GroupDocs.Search erbjuder en färdig, högpresterande motor som stödjer dussintals filformat, distribuerad indexering och inbyggda fragment‑markeringar. Det eliminerar behovet av att skriva egna parsers eller hantera låg‑nivå sökinfrastruktur, så att du kan fokusera på att leverera en smidig användarupplevelse.

## Förutsättningar

- **Java Development Kit (JDK) 8+** – säkerställ att `java -version` rapporterar 1.8 eller högre.  
- **Maven** – för beroendehantering.  
- **GroupDocs.Search for Java 25.4** – versionen som används i hela guiden.  
- En IDE som **IntelliJ IDEA** eller **Eclipse** (valfritt men rekommenderat).  
- Grundläggande kunskap om Java och nätverkskoncept.

## Installera GroupDocs.Search för Java

Du kan lägga till biblioteket i ditt projekt antingen via Maven eller genom att ladda ner JAR‑filen direkt.

### Maven‑inställning
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

### Direkt nedladdning
Alternativt, ladda ner den senaste JAR‑filen från [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Steg för att skaffa licens
- **Free Trial:** Börja med en provperiod för att utforska kärnfunktionerna.  
- **Temporary License:** Skaffa en utökad testlicens från [this page](https://purchase.groupdocs.com/temporary-license/).  
- **Purchase:** Skaffa en full licens för produktionsdistributioner.

### Grundläggande initiering och konfiguration
Create an `Index` instance that points to a folder where the search index will be stored:

```java
import com.groupdocs.search.*;

public class SearchSetup {
    public static void main(String[] args) {
        // Create an instance of Index
        Index index = new Index("path/to/index/directory");
        System.out.println("GroupDocs.Search initialized successfully.");
    }
}
```

## Implementeringsguide

### Så markerar du Highlight Search Results Java i ett distribuerat nätverk

#### Konfigurering av söknätverket
First, define where your documents live and which port the network will use.

```java
import com.groupdocs.search.common.*;
import com.groupdocs.search.scaling.configuring.*;

String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/HighlightingResultsInNetwork/";
int basePort = 49116; // Change if port is busy

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```

- **`basePath`** – rotmappen som innehåller filerna du vill indexera.  
- **`basePort`** – TCP‑porten för nodkommunikation; välj en som inte används.

#### Distribuera söknätverksnoder
Deploy one or more nodes based on the configuration. The first node becomes the master.

```java
import com.groupdocs.search.scaling.*;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
SearchNetworkNode masterNode = nodes[0];
```

- **`nodes`** – en array med alla körande noder.  
- **`masterNode`** – koordinerar indexering och fråge‑distribution.

#### Prenumerera på händelser från söknätverksnoder
Attach listeners to the master node to receive real‑time notifications (e.g., when indexing completes).

```java
import com.groupdocs.search.scaling.events.*;

SearchNetworkNodeEvents.subscribe(masterNode);
```

#### Indexera kataloger i nätverksnod
Point the node to the folder(s) you want to index. The helper class `Utils.DocumentsPath` resolves to the sample data folder.

```java
import com.groupdocs.search.examples.Utils;
import com.groupdocs.search.options.*;

IndexingDocuments.addDirectories(masterNode, Utils.DocumentsPath);
```

#### Sök text över nätverksnoder
Run a query against **all** nodes and retrieve the matching documents.

```java
import java.util.ArrayList;
import com.groupdocs.search.scaling.results.*;

ArrayList<NetworkFoundDocument> documents = TextSearchInNetwork.searchAll(masterNode, "ipsum", false);
highlightInDocument(masterNode, documents.get(0), 3); // Highlight results from the first found document.
```

- Ersätt `"ipsum"` med någon term du behöver hitta.  
- Metoden `highlightInDocument` (visas härnäst) kommer att applicera markeringen.

#### Markera flera termer i dokument – Markering av sökresultat
Följande metod demonstrerar hur man markerar fragment runt varje matchning. Den visar också hur man styr antalet omgivande termer, vilket uppfyller det sekundära nyckelordet **highlight multiple terms document**.

```java
import com.groupdocs.search.highlighters.*;
import com.groupdocs.search.options.*;

public static void highlightInDocument(
    SearchNetworkNode node,
    NetworkFoundDocument document,
    int maxFragments) {
    
    Searcher searcher = node.getSearcher();
    FragmentHighlighter highlighter = new FragmentHighlighter(OutputFormat.PlainText);

    HighlightOptions options = new HighlightOptions();
    options.setTermsAfter(5);
    options.setTermsBefore(5);
    options.setTermsTotal(15);

    searcher.highlight(document, highlighter, options); // Perform highlighting on the document.

    FragmentContainer[] result = highlighter.getResult();
    for (FragmentContainer container : result) {
        if (container.getCount() == 0) continue;

        String[] fragments = container.getFragments();
        int count = Math.min(fragments.length, maxFragments);
        for (int j = 0; j < count; j++) {
            // Print each fragment within the specified limit.
        }
    }
}
```

- **`OutputFormat.PlainText`** – returnerar text‑snuttar; du kan byta till HTML för ett rikare UI.  
- **`HighlightOptions`** – styr hur många ord före/efter varje matchning som inkluderas (`setTermsBefore`, `setTermsAfter`).  
- **`maxFragments`** – begränsar antalet snuttar du visar per dokument.

#### Stänga nätverksnoder
When you’re done, shut down every node to free resources.

```java
for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Praktiska tillämpningar

- **Enterprise Document Management:** Centralisera företagsfiler och låt anställda omedelbart hitta relevanta kontrakt eller policyer.  
- **Legal Case Files:** Snabbt framhäva prejudikatdokument genom att markera viktiga juridiska termer.  
- **R&D Knowledge Bases:** Forskare kan söka i patent eller tekniska artiklar och se markerade utdrag.  
- **E‑commerce Catalogs:** Gör det möjligt för kunder att hitta produkter via nyckelord med markerade matchningar i beskrivningar.  
- **Library Systems:** Låntagare kan söka i tusentals böcker och se markerade passager utan att öppna varje fil.

## Prestandaöverväganden

- **Keep indexes fresh:** Indexera om ändrade filer varje natt eller använd inkrementella uppdateringar.  
- **Leverage multiple nodes:** Distribuera indexering och frågelast för att undvika flaskhalsar.  
- **Tune `HighlightOptions`:** Att minska `termsBefore/After` minskar minnesanvändningen för mycket stora dokument.

## Vanliga problem & felsökning

| Symtom | Trolig orsak | Åtgärd |
|--------|--------------|-------|
| Inga resultat returnerade | Index ej byggt eller pekar på fel mapp | Verifiera `Utils.DocumentsPath` och kör `IndexingDocuments.addDirectories` igen |
| Markeringens output är tom | `HighlightOptions`-gränser för låga eller dokumentkodningsproblem | Öka `termsTotal` eller säkerställ att dokumentets kodning stöds |
| Portkonfliktfel | `basePort` redan i bruk | Välj ett annat portnummer (t.ex. 49117) |
| Licensundantag | Saknad eller utgången licensfil | Placera en giltig `GroupDocs.Search.lic`-fil i applikationens rot |

## Vanliga frågor

**Q: Kan jag distribuera flera söknätverksnoder för lastbalansering?**  
A: Ja, genom att distribuera flera noder sprids indexering och frågearbete, vilket förbättrar skalbarhet och svarstid.

**Q: Hur markerar jag flera söktermer i samma dokument?**  
A: Skicka en lista med termer till `highlight`‑metoden och konfigurera `HighlightOptions` för att visa omgivande ord för varje matchning.

**Q: Är det möjligt att prenumerera på real‑tids sökhändelser?**  
A: Absolut. Använd `SearchNetworkNodeEvents.subscribe(masterNode)` för att få återuppringningar för indexeringsframsteg, frågeutförande och fel.

**Q: Vilka filformat stödjer GroupDocs.Search för indexering och markering?**  
A: Över 50 format, inklusive DOCX, PDF, HTML, TXT, PPTX och fler.

**Q: Hur kan jag förbättra sökhastigheten i mycket stora samlingar?**  
A: Uppdatera regelbundet indexen, distribuera dem över noder och finjustera `HighlightOptions` för att begränsa fragmentstorleken.

---

**Last Updated:** 2026-03-17  
**Testad med:** GroupDocs.Search for Java 25.4  
**Författare:** GroupDocs
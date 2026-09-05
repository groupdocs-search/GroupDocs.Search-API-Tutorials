---
date: '2026-05-17'
description: Lär dig hur du lägger till groupdocs Maven-beroende, sätter upp ett Java-söknätverk
  och lägger till kataloger i indexet för snabb, skalbar dokumenthämtning.
keywords:
- how to add groupdocs
- add directories to index
- set up search cluster
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  headline: How to Add GroupDocs Maven Dependency for Search Network
  type: TechArticle
- description: Learn how to add groupdocs Maven dependency, set up a Java search network,
    and add directories to index for fast, scalable document retrieval.
  name: How to Add GroupDocs Maven Dependency for Search Network
  steps:
  - name: '**Legal Document Management** – Quickly retrieve case files and precedents.'
    text: '**Legal Document Management** – Quickly retrieve case files and precedents.'
  - name: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
    text: '**Financial Record Keeping** – Access statements and audit trails in seconds.'
  - name: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
    text: '**Academic Research** – Search across thousands of papers to find relevant
      citations.'
  type: HowTo
- questions:
  - answer: It provides fast, scalable search capabilities across large document sets
      with minimal configuration.
    question: What is the primary benefit of using GroupDocs.Search?
  - answer: Yes, you can set custom paths, ports, and other options via the `Configuration`
      object.
    question: Can I customize node configurations in a search network?
  - answer: Call `IndexingDocuments.addDirectories(masterNode, "path")` whenever you
      need to index new folders.
    question: How do I add directories to index after the network is running?
  - answer: Use the `synchronizeShards` method shown above on the newly added node.
    question: How to sync shards when a new node joins the network?
  - answer: A free trial license is sufficient for testing; a commercial license is
      required for production.
    question: Do I need a license for development?
  type: FAQPage
title: Hur man lägger till GroupDocs Maven-beroende för söknätverk
type: docs
url: /sv/java/search-network/java-groupdocs-search-configuration-sync-guide/
weight: 1
---

# Hur man lägger till GroupDocs Maven‑beroende för söknätverk

I den här omfattande guiden kommer du att upptäcka **hur man lägger till groupdocs Maven‑beroende**, konfigurera ett robust Java‑söknätverk med GroupDocs.Search och hålla dina shards synkroniserade. Oavsett om du indexerar juridiska handlingar, finansiella rapporter eller akademiska artiklar, kommer stegen nedan att hjälpa dig att skapa sökbara index, distribuera frågelast över noder och upprätthålla datakonsistens med minimal ansträngning.

## Snabba svar
- **Vad är GroupDocs Maven‑beroendet?** Ett Maven‑artefakt som paketera GroupDocs.Search‑biblioteket för Java‑projekt.  
- **Varför använda ett söknätverk?** Det distribuerar indexering och frågelast över flera noder, vilket förbättrar hastighet och tillförlitlighet.  
- **Hur lägger jag till kataloger för indexering?** Använd `IndexingDocuments.addDirectories` på master‑noden.  
- **Hur synkroniserar man shards?** Anropa `SynchronizeOptions` på varje nods `Indexer`.  
- **Behöver jag en licens?** Ja, en prov- eller kommersiell licens krävs för produktionsanvändning.

## Vad är GroupDocs Maven‑beroendet?

`GroupDocs Maven dependency` är ett Maven‑artefakt som paketera GroupDocs.Search‑biblioteket för Java‑projekt.  
Det tillhandahåller alla nödvändiga klasser för att skapa sökbara index, hantera nätverksnoder och utföra snabba frågor, och Maven löser transitiva beroenden automatiskt, vilket ger dig en färdig‑till‑använd sökmotor med bara några rader i din `pom.xml`.

## Hur man lägger till GroupDocs Maven‑beroendet

Lägg till repository‑ och beroende‑poster i din `pom.xml`, kör sedan `mvn clean install`; Maven hämtar `groupdocs-search`‑JAR‑filen och dess nödvändiga bibliotek, vilket gör API‑et tillgängligt i ditt projekt. När bygget lyckas kan du omedelbart börja använda `com.groupdocs.search`‑klasserna.

### Maven‑konfiguration

Lägg till repository‑ och beroende‑posten i din `pom.xml`:

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

> **Pro tip:** Håll versionsnumret uppdaterat genom att kontrollera den officiella releases‑sidan.

Du kan också ladda ner JAR‑filen direkt från den officiella webbplatsen: [Handledningar och exempel på GroupDocs.Search för Java](https://releases.groupdocs.com/search/java/).

## Varför använda ett söknätverk?

Ett söknätverk möjliggör horisontell skalning genom att partitionera indexet i shards som ligger på separata noder. GroupDocs.Search kan hantera **50+ inmatningsformat** och bearbeta **dokument med flera hundra sidor** utan att ladda hela filen i minnet, vilket levererar svar på frågor på under en sekund även när datavolymen växer.

## Förutsättningar

- **JDK** (11 eller nyare) installerad.  
- En IDE såsom IntelliJ IDEA eller Eclipse.  
- Grundläggande Java‑kunskaper, Maven‑kunskap och förståelse för nätverksnodkoncept.  
- En giltig GroupDocs.Search‑licens (gratis prov eller kommersiell).

## Grundläggande initiering och konfiguration

Börja med att skapa en indexkatalog:

```java
import com.groupdocs.search.SearchIndex;
import com.groupdocs.search.options.IndexingOptions;

// Create an index in the specified directory
SearchIndex index = new SearchIndex("YOUR_INDEX_DIRECTORY");
```

Detta enkla steg förbereder miljön för den efterföljande nätverkskonfigurationen.

## Implementeringsguide

### Funktion 1: Konfiguration av söknätverk

#### Översikt

Att konfigurera söknätverket anger filvägar och portar som noderna kommer att använda för att kommunicera.

##### Ställ in vägar och portar

Configuration är en klass som innehåller nätverksvägar, portar och andra inställningar för sökklustret.  
```java
import com.groupdocs.search.options.*;
import com.groupdocs.search.scaling.configuring.ConfiguringSearchNetwork;

// Set custom paths for input/output directories
String basePath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/SynchronizingShards/";
int basePort = 49144; // Adjust if there's a port conflict

Configuration configuration = ConfiguringSearchNetwork.configure(basePath, basePort);
```  
`configuration`‑objektet innehåller nu alla nödvändiga inställningar för ditt söknätverk.

### Funktion 2: Distribuera söknätverksnoder

#### Översikt

Distribuera noder för att fördela arbetsbelastningen över ditt nätverk. Master‑noden hanterar operationer och händelser.

##### Distributionskod

`SearchNetworkNode` representerar en nod i söknätverket som kan fungera som master eller worker.  
```java
import com.groupdocs.search.scaling.*;
import com.groupdocs.search.options.Configuration;

SearchNetworkNode[] nodes = SearchNetworkDeployment.deploy(basePath, basePort, configuration);
// Retrieve the master node for further operations
SearchNetworkNode masterNode = nodes[0];
```

### Funktion 3: Prenumerera på söknätverksnod‑händelser

#### Översikt

Att lyssna på händelser möjliggör dynamisk hantering av förändringar eller uppdateringar i ditt nätverk.

##### Implementering av prenumeration

`SearchNetworkNodeEvents` tillhandahåller händelsekrokar för nodlivscykel och indexeringsåtgärder.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.scaling.SearchNetworkNodeEvents;

SearchNetworkNodeEvents.subscribe(masterNode);
```

### Funktion 4: Lägga till kataloger i index

#### Översikt

Att lägga till kataloger är huvudsteget som gör dina dokument sökbara.

##### Dokumenttillägg

`IndexingDocuments.addDirectories` lägger till mappvägar i indexet för bearbetning.  
```java
import com.groupdocs.search.indexing.IndexingDocuments;
import com.groupdocs.search.scaling.SearchNetworkNode;

IndexingDocuments.addDirectories(masterNode, "YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```

### Funktion 5: Synkronisera shards i söknätverksnod

#### Översikt

Synkronisering säkerställer datakonsistens över alla shards.

##### Synkroniseringskod

`SynchronizeOptions` konfigurerar hur shards synkroniseras över noder.  
```java
import com.groupdocs.search.indexing.Indexer;
import com.groupdocs.search.scaling.SearchNetworkNode;
import com.groupdocs.search.options.SynchronizeOptions;

SearchNetworkNode node = null; // Assume 'node' is initialized as a SearchNetworkNode

def synchronizeShards(SearchNetworkNode node) {
    Indexer indexer = node.getIndexer();
    SynchronizeOptions options = new SynchronizeOptions();
    indexer.synchronize(options);
}
```

### Funktion 6: Stänga söknätverksnoder

#### Översikt

Att stänga noder på rätt sätt frigör resurser och förhindrar minnesläckor.

##### Nodstängning

`close()` frigör resurser och stänger ner söknätverksnoden.  
```java
import com.groupdocs.search.scaling.SearchNetworkNode;

for (SearchNetworkNode node : nodes) {
    node.close();
}
```

## Praktiska tillämpningar

1. **Juridisk dokumenthantering** – Hämta snabbt ärendehandlingar och prejudikat.  
2. **Finansiell bokföring** – Få åtkomst till uttalanden och revisionsspår på sekunder.  
3. **Akademisk forskning** – Sök bland tusentals artiklar för att hitta relevanta citat.

## Prestandaöverväganden

- **Optimera frågor** – Skriv koncisa frågor för att minska svarstiden.  
- **Minneshantering** – Övervaka JVM‑heap‑användning; överväg GC‑optimering för stora index.  
- **Skaleringsstrategi** – Lägg till noder proportionellt mot datavolym och frågelast.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|----------|
| Noder kan inte ansluta | Portkonflikt | Ändra `basePort` till ett oanvänt värde |
| Index uppdateras inte | Händelseprenumeration saknas | Säkerställ att `SearchNetworkNodeEvents.subscribe(masterNode)` anropas |
| Hög latens | Otillräckliga shards | Öka antalet noder och balansera dokumentfördelning |

## Vanliga frågor

**Q: Vad är den främsta fördelen med att använda GroupDocs.Search?**  
A: Det ger snabba, skalbara sökfunktioner över stora dokumentuppsättningar med minimal konfiguration.

**Q: Kan jag anpassa nodkonfigurationer i ett söknätverk?**  
A: Ja, du kan ange anpassade vägar, portar och andra alternativ via `Configuration`‑objektet.

**Q: Hur lägger jag till kataloger i index efter att nätverket körs?**  
A: Anropa `IndexingDocuments.addDirectories(masterNode, "path")` när du behöver indexera nya mappar.

**Q: Hur synkroniserar man shards när en ny nod ansluter till nätverket?**  
A: Använd `synchronizeShards`‑metoden som visas ovan på den nyinlagda noden.

**Q: Behöver jag en licens för utveckling?**  
A: En gratis provlicens räcker för testning; en kommersiell licens krävs för produktion.

## Slutsats

Genom att följa den här guiden vet du nu hur man **lägger till groupdocs Maven‑beroende**, konfigurerar ett multi‑node‑söknätverk, indexerar kataloger och håller shards synkroniserade. Dessa steg lägger grunden för en högpresterande dokument‑sök‑lösning som kan växa med ditt företags behov.

---

**Senast uppdaterad:** 2026-05-17  
**Testat med:** GroupDocs.Search 25.4  
**Författare:** GroupDocs

## Relaterade handledningar

- [Handledningar och exempel på GroupDocs.Search för Java](/search/net/)
- [Konfigurering av GroupDocs.Search‑nätverk i .NET: En omfattande guide](/search/net/search-network/configuring-groupdocs-search-network-net-guide/)
- [Hur man implementerar ett söknätverk med GroupDocs.Search i .NET för dokumenthanteringssystem](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
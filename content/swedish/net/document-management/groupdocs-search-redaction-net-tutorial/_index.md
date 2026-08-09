---
date: '2026-06-12'
description: Lär dig hur du skapar sökindex .NET och tillämpar redaction på PDF med
  hjälp av GroupDocs.Search och GroupDocs.Redaction. Installation, distribution, indexering
  och avancerad sökning förklaras.
keywords:
- create search index .net
- apply redaction to pdf
- groupdocs search .net
- document redaction .net
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  headline: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to create search index .NET and apply redaction to PDF using
    GroupDocs.Search and GroupDocs.Redaction. Setup, deployment, indexing, and advanced
    search explained.
  name: Create Search Index .NET with GroupDocs Search and Redaction – A Comprehensive
    Guide
  steps:
  - name: Configure the Network
    text: 'Use the `Configure` method to set up the search network with the specified
      path and port:'
  - name: Identify the Master Node
    text: 'Select the first node as your master:'
  - name: Subscribe to Events
    text: 'Subscribe to events using:'
  - name: Add Directories to Index
    text: 'Specify directories containing your documents:'
  type: HowTo
- questions:
  - answer: Define a base path and port, then call `SearchNetworkDeployment.Deploy()`
      to launch master and worker nodes across machines.
    question: How do I set up a distributed search network in .NET with GroupDocs?
  - answer: Yes—use `SearchOptions` to combine fuzzy matching, wildcard support, and
      result highlighting in a single query.
    question: Can I perform advanced searches with multiple parameters in GroupDocs?
  - answer: Absolutely—subscribe to `SearchNetworkNodeEvents` such as `IndexingCompleted`
      and `QueryExecuted` for real‑time insights.
    question: Is it possible to monitor network activity on the master node?
  - answer: Initialize a `Redactor`, load the PDF, define `RedactionPattern` objects
      (regex or literal strings), call `Apply`, and save the sanitized document.
    question: How do I apply redaction to PDF files using GroupDocs?
  - answer: Fully index your document set before queries, distribute nodes to utilize
      parallel processing, and tune `SearchOptions` for caching and paging.
    question: What's the easiest way to improve search performance in a networked
      environment?
  type: FAQPage
title: Skapa sökindex .NET med GroupDocs Search och GroupDocs.Redaction – En omfattande
  guide
type: docs
url: /sv/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Skapa sökindex .NET med GroupDocs Search och Redaction – En omfattande guide

I dagens digitala landskap är **skapa ett sökindex .NET**‑lösning som både snabbt kan hitta information och skydda känsliga data en högsta prioritet för alla organisationer. Denna handledning guidar dig genom att konfigurera ett skalbart GroupDocs.Search‑nätverk, distribuera noder, indexera dokument och använda GroupDocs.Redaction för att **applicera redaction på PDF**‑filer – allt inom en .NET‑miljö.

## Snabba svar
- **Vad är det första steget för att skapa ett sökindex .NET?** Definiera en basväg och port, och distribuera sedan nätverksnoderna.  
- **Hur applicerar jag redaction på PDF med GroupDocs?** Initiera en `Redactor`‑instans, ladda PDF-filen och anropa `Redact` med de önskade mönstren.  
- **Kan jag köra söknätverket på flera maskiner?** Ja—distribuera noder på separata servrar och låt huvudnoden samordna indexering och frågor.  
- **Behöver jag en licens för produktionsbruk?** En giltig GroupDocs-licens krävs för produktion; en tillfällig provlicens finns tillgänglig för utvärdering.  
- **Vilka .NET‑versioner stöds?** .NET Framework 4.7.2+, .NET Core 3.1+, och .NET 5/6/7 stöds fullt ut.

## Vad är “create search index .net”?
*Creating a search index .NET* avser att bygga ett sökbart arkiv av dokumentmetadata och innehåll med .NET‑bibliotek, som extraherar text, tokeniserar termer och lagrar dem i en optimerad indexstruktur. Detta möjliggör omedelbara frågesvar över distribuerade noder, stödjer olika filformat och möjliggör skalbar, högpresterande dokumenthämtning i företagsapplikationer.

## Varför använda GroupDocs Search och Redaction tillsammans?
GroupDocs.Search stödjer **50+ filformat**—inklusive DOCX, PDF, PPTX och HTML—och kan indexera dokument med flera hundra sidor utan att ladda hela filen i minnet. Kombinerat med GroupDocs.Redaction, som kan **applicera redaction på PDF** på under 200 ms per sida, får du en säker, högpresterande dokumenthanteringspipeline.

## Förutsättningar

### Nödvändiga bibliotek & beroenden
För att följa den här handledningen, installera följande paket:
- **GroupDocs.Search** för .NET
- **GroupDocs.Redaction** för .NET  

Du kan använda någon av dessa metoder för att installera de nödvändiga biblioteken:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Sök efter "GroupDocs.Search" och "GroupDocs.Redaction" och installera den senaste versionen.

### Krav för miljöinställning
- .NET Framework 4.7.2 eller högre (eller .NET Core 3.1+)
- Visual Studio IDE (Community, Professional eller Enterprise)

### Förkunskaper
- Grundläggande C#‑programmering
- Objekt‑orienterade koncept
- Bekantskap med nätverkskonfigurationer och dokumenthanteringssystem

## Konfigurera GroupDocs.Redaction för .NET

### Installationsinformation
För att integrera redaction‑funktioner i din applikation, börja med att lägga till GroupDocs.Redaction‑biblioteket:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Sök efter "GroupDocs.Redaction" och installera det.

### Licensanskaffning
För att komma igång med en gratis provperiod eller en tillfällig licens, följ dessa steg:
- Besök [GroupDocs webbplats](https://purchase.groupdocs.com/temporary-license/) för att begära en tillfällig licens.  
- För köpalternativ, gå till deras [prissida](https://groupdocs.com/pricing).

När du har din licensfil, applicera den i din applikationsinställning:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Grundläggande initiering
För att initiera GroupDocs.Redaction för grundläggande operationer, använd följande kodsnutt:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Implementeringsguide

### Konfigurationsinställning

#### Översikt
Denna funktion konfigurerar ditt söknätverk med en basväg och portnummer, vilket bildar grunden för ditt dokumenthanteringssystem.

#### Definition Anchor
`SearchNetworkDeployment` är klassen som orkestrerar distribution av söknoder över nätverket.

#### Steg 1: Definiera basväg och port  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Steg 2: Konfigurera nätverket
Använd `Configure`‑metoden för att ställa in söknätverket med den angivna vägen och porten:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Distribution av nätverksnoder

#### Översikt
Distribuera noder inom ditt konfigurerade söknätverk för distribuerad dokumentsökning.

#### Definition Anchor
`SearchNetworkNode` representerar en individuell sökbar nod som kommunicerar med huvudnoden.

#### Steg 1: Initiera distribution  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Händelseprenumeration för huvudnod

#### Översikt
Prenumerera på händelser på huvudnoden för att övervaka och hantera nätverksoperationer effektivt.

#### Definition Anchor
`SearchNetworkNodeEvents` tillhandahåller återuppringningar för indexering, frågeutförande och felhantering.

#### Steg 1: Identifiera huvudnoden
Välj den första noden som din huvudnod:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Steg 2: Prenumerera på händelser
Prenumerera på händelser med:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Indexering av dokument

#### Översikt
Indexera dokument för effektiva sökoperationer. Detta steg är avgörande för att säkerställa att ditt nätverk snabbt kan hämta nödvändig data.

#### Definition Anchor
`SearchIndex` är kärnobjektet som lagrar sökbara token och metadata för varje indexerad fil.

#### Steg 1: Lägg till kataloger i indexet
Ange kataloger som innehåller dina dokument:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Sökfunktion – Grundläggande användning

#### Översikt
Utför grundläggande sökoperationer över noder i nätverket.

#### Direkt svar
Anropa `SearchNetwork.Query("your term")` på huvudnoden för att omedelbart hämta matchande dokument. Metoden returnerar en samling av `SearchResult`‑objekt som inkluderar filsökvägar och relevanspoäng.  
`SearchNetwork.Query` är en metod som utför en sökfråga över hela nätverket och returnerar matchande resultat.

#### Steg 1: Definiera sökparametrar  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Avancerad sökfunktion

#### Översikt
Använd avancerade söktekniker med anpassningsbara parametrar för mer precisa resultat.

#### Direkt svar
Implementera en metod som bygger ett `SearchOptions`‑objekt, sätter egenskaperna `UseFuzzySearch`, `Highlight` och `PageSize`, och sedan skickar det till `SearchNetwork.QueryAdvanced`. Detta ger paginerade, markerade resultat med fuzzy‑matchning aktiverad.  
`SearchNetwork.QueryAdvanced` är en metod som kör en fråga med avancerade alternativ såsom fuzzy‑matchning och paginering.

#### Steg 1: Implementera den avancerade sökmetoden  
```csharp
using GroupDocs.Search.Scaling.Results;
using System.Collections.Generic;

public static List<NetworkFoundDocument> SearchAll(
    SearchNetworkNode node,
    string word,
    bool useSynonymSearch,
    bool isObjectForm)
{
    // Initialize searcher and search options for the given node
    Searcher searcher = node.Searcher;
    SearchOptions options = new SearchOptions {
        IsChunkSearch = true, // Enable chunk-based search
        UseSynonymSearch = useSynonymSearch
    };

    int totalOccurrences = 0; // To count occurrences across all documents
    List<NetworkFoundDocument> documents = new List<NetworkFoundDocument>();

    NetworkSearchResult result;
    if (isObjectForm)
    {
        SearchQuery query = SearchQuery.CreateWordQuery(word);
        result = searcher.SearchFirst(query, options); // Perform initial chunk search
    }
    else
    {
        string queryText = word;
        result = searcher.SearchFirst(queryText, options); // Perform initial text-based search
    }

    AddDocsFromResult(documents, result);
    totalOccurrences += result.OccurrenceCount;

    while (result.NextChunkSearchToken != null)
    {
        result = searcher.SearchNext(result.NextChunkSearchToken);
        AddDocsFromResult(documents, result);
        totalOccurrences += result.OccurrenceCount;
    }

    return documents; // Return list of found documents
}

private static void AddDocsFromResult(List<NetworkFoundDocument> documents, NetworkSearchResult result)
{
    for (int i = 0; i < result.DocumentCount; i++)
    {
        documents.Add(result.GetFoundDocument(i)); // Collect each document from the search results
    }
}
```  

### Applicering av redaction på PDF‑filer

#### Översikt
Säkra känslig information genom att redigera PDF‑innehåll innan det lagras eller delas.

#### Direkt svar
Skapa en `Redactor`‑instans, ladda mål‑PDF‑filen, definiera ett `RedactionPattern` (t.ex. SSN‑regex), anropa `redactor.Apply(pattern)`, och slutligen spara det redigerade dokumentet. Denna process säkerställer att personuppgifter tas bort permanent.

#### Definition Anchor
`Redactor` är huvudklassen i GroupDocs.Redaction som bearbetar dokument och tillämpar redaction‑regler.

#### Exempelarbetsflöde (ingen ny kodblock)
1. Initiera `Redactor` med din licens.  
2. Ladda PDF‑filen med `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` representerar en regel som specificerar texten eller mönstret som ska redigeras. Definiera mönster såsom `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Utför `redactor.Apply(pattern)`.  
5. Spara resultatet med `redactor.Save("sample_redacted.pdf")`.

### Praktiska tillämpningar

#### Verkliga användningsfall
1. **Legal Document Management** – Sök effektivt i kontrakt och redigera automatiskt klientidentifierare.  
2. **Healthcare Records** – Lokalisera patientanteckningar samtidigt som du säkerställer HIPAA‑kompatibel redaction av PHI.  
3. **Corporate Compliance** – Skanna interna kommunikationer för förbjudna termer och redigera innan arkivering.

## Slutsats 
Denna guide ger en omfattande väg för **skapa ett sökindex .NET**‑lösning som skalar, indexerar snabbt och skyddar data genom redaction. Genom att konfigurera noder, indexera dokument, utnyttja avancerade sökfunktioner och applicera redaction kan utvecklare dramatiskt förbättra dokumenthanteringsarbetsflöden samtidigt som strikta säkerhetsstandarder upprätthålls.

## Vanliga frågor

**Q: Hur ställer jag in ett distribuerat söknätverk i .NET med GroupDocs?**  
A: Definiera en basväg och port, och anropa sedan `SearchNetworkDeployment.Deploy()` för att starta huvud‑ och arbetsnoder över maskiner.

**Q: Kan jag utföra avancerade sökningar med flera parametrar i GroupDocs?**  
A: Ja—använd `SearchOptions` för att kombinera fuzzy‑matchning, jokerteckenstöd och resultatmarkering i en enda fråga.

**Q: Är det möjligt att övervaka nätverksaktivitet på huvudnoden?**  
A: Absolut—prenumerera på `SearchNetworkNodeEvents` såsom `IndexingCompleted` och `QueryExecuted` för insikter i realtid.

**Q: Hur applicerar jag redaction på PDF‑filer med GroupDocs?**  
A: Initiera en `Redactor`, ladda PDF‑filen, definiera `RedactionPattern`‑objekt (regex eller bokstavliga strängar), anropa `Apply` och spara det sanerade dokumentet.

**Q: Vad är det enklaste sättet att förbättra sökprestanda i en nätverksmiljö?**  
A: Indexera hela ditt dokumentset fullt ut innan frågor, distribuera noder för att utnyttja parallell bearbetning och finjustera `SearchOptions` för cachning och paginering.

**Senast uppdaterad:** 2026-06-12  
**Testad med:** GroupDocs.Search 23.9 för .NET, GroupDocs.Redaction 23.9 för .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Master .NET Document Indexing with GroupDocs.Search: En omfattande guide](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Master Dokumentindexering och avancerade sökfrågor med GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [Mastering GroupDocs Search and Redaction in .NET: Avancerad dokumenthantering](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
---
date: '2026-06-12'
description: Leer hoe u een zoekindex .NET maakt en redaction toepast op PDF met behulp
  van GroupDocs.Search en GroupDocs.Redaction. Installatie, implementatie, indexering
  en geavanceerd zoeken uitgelegd.
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
title: Maak zoekindex .NET met GroupDocs Search en Redaction – Een uitgebreide gids
type: docs
url: /nl/net/document-management/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Maak zoekindex .NET met GroupDocs Search en Redaction – Een uitgebreide gids

In het digitale landschap van vandaag is **het maken van een zoekindex .NET** oplossing die zowel informatie snel kan vinden als gevoelige gegevens kan beschermen een topprioriteit voor elke organisatie. Deze tutorial leidt je door het configureren van een schaalbaar GroupDocs.Search‑netwerk, het implementeren van knooppunten, het indexeren van documenten en het gebruiken van GroupDocs.Redaction om **redactie toe te passen op PDF**‑bestanden — allemaal binnen een .NET‑omgeving.

## Snelle antwoorden
- **Wat is de eerste stap om een zoekindex .NET te maken?** Definieer een basispad en poort, en implementeer vervolgens de netwerk‑knooppunten.  
- **Hoe pas ik redactie toe op PDF met GroupDocs?** Initialiseert een `Redactor`‑instantie, laad de PDF, en roep `Redact` aan met de gewenste patronen.  
- **Kan ik het zoeknetwerk op meerdere machines draaien?** Ja — implementeer knooppunten op afzonderlijke servers en laat het master‑knooppunt de indexering en zoekopdrachten coördineren.  
- **Heb ik een licentie nodig voor productiegebruik?** Een geldige GroupDocs‑licentie is vereist voor productie; een tijdelijke proeflicentie is beschikbaar voor evaluatie.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.7.2+, .NET Core 3.1+ en .NET 5/6/7 worden volledig ondersteund.

## Wat is “create search index .net”?
*Creating a search index .NET* verwijst naar het bouwen van een doorzoekbare repository van documentmetadata en -inhoud met behulp van .NET‑bibliotheken, die tekst extraheren, termen tokeniseren en opslaan in een geoptimaliseerde indexstructuur. Dit maakt onmiddellijke zoekresponsen mogelijk over gedistribueerde knooppunten, ondersteunt verschillende bestandsformaten en maakt schaalbare, high‑performance document‑ophaling mogelijk in enterprise‑applicaties.

## Waarom GroupDocs Search en Redaction samen gebruiken?
GroupDocs.Search ondersteunt **meer dan 50 bestandsformaten** — waaronder DOCX, PDF, PPTX en HTML — en kan documenten van honderden pagina's indexeren zonder het volledige bestand in het geheugen te laden. In combinatie met GroupDocs.Redaction, dat **redactie kan toepassen op PDF** in minder dan 200 ms per pagina, krijg je een veilige, high‑performance document‑beheerpijplijn.

## Voorvereisten

### Vereiste bibliotheken & afhankelijkheden
Om deze tutorial te volgen, installeer de volgende pakketten:
- **GroupDocs.Search** voor .NET
- **GroupDocs.Redaction** voor .NET  

Je kunt een van deze methoden gebruiken om de benodigde bibliotheken te installeren:

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
Zoek naar "GroupDocs.Search" en "GroupDocs.Redaction" en installeer de nieuwste versie.

### Vereisten voor omgeving configuratie
- .NET Framework 4.7.2 of hoger (of .NET Core 3.1+)
- Visual Studio IDE (Community, Professional, of Enterprise)

### Kennisvereisten
- Basis C#‑programmeren
- Object‑georiënteerde concepten
- Vertrouwdheid met netwerkconfiguraties en documentbeheersystemen

## GroupDocs.Redaction voor .NET instellen

### Installatie‑informatie
Om redactie‑functies in je applicatie te integreren, begin je met het toevoegen van de GroupDocs.Redaction‑bibliotheek:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Zoek naar "GroupDocs.Redaction" en installeer deze.

### Licentie‑verwerving
Om te beginnen met een gratis proefversie of een tijdelijke licentie, volg deze stappen:
- Bezoek de [GroupDocs-website](https://purchase.groupdocs.com/temporary-license/) om een tijdelijke licentie aan te vragen.  
- Voor aankoopopties, ga naar hun [prijspagina](https://groupdocs.com/pricing).

Zodra je je licentiebestand hebt, pas je deze toe in de applicatie‑configuratie:

```csharp
RedactorSettings settings = new RedactorSettings("YOUR_LICENSE_PATH");
```  

### Basisinitialisatie
Om GroupDocs.Redaction te initialiseren voor basisbewerkingen, gebruik je de volgende code‑fragment:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

Redactor redactor = new Redactor("path/to/your/document.pdf", new LoadOptions(), settings);
```  

## Implementatie‑gids

### Configuratie‑instelling

#### Overzicht
Deze functie configureert je zoeknetwerk met een basispad en poortnummer, en vormt de basis van je documentbeheersysteem.

#### Definitie‑anker
`SearchNetworkDeployment` is de klasse die de implementatie van zoekknooppunten over het netwerk coördineert.

#### Stap 1: Definieer basispad en poort  
```csharp
string basePath = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Scaling/TextSearchInNetwork/";
int basePort = 49148; // Define your network's base port
```  

#### Stap 2: Configureer het netwerk  
Gebruik de `Configure`‑methode om het zoeknetwerk in te stellen met het opgegeven pad en poort:

```csharp
using GroupDocs.Search.Scaling.Configuring;

Configuration configuration = ConfiguringSearchNetwork.Configure(basePath, basePort);
```  

### Implementatie van netwerk‑knooppunten

#### Overzicht
Implementeer knooppunten binnen je geconfigureerde zoeknetwerk voor gedistribueerd document zoeken.

#### Definitie‑anker
`SearchNetworkNode` vertegenwoordigt een individueel doorzoekbaar knooppunt dat communiceert met het master‑knooppunt.

#### Stap 1: Initialiseer implementatie  
```csharp
using GroupDocs.Search.Scaling;
List<SearchNetworkNode> deployedNodes = new List<SearchNetworkNode>();
SearchNetworkNode[] nodes = SearchNetworkDeployment.Deploy(basePath, basePort, configuration);
deployedNodes.AddRange(nodes);
```  

### Evenement‑abonnement voor master‑knooppunt

#### Overzicht
Abonneer je op gebeurtenissen op het master‑knooppunt om netwerkactiviteiten effectief te monitoren en beheren.

#### Definitie‑anker
`SearchNetworkNodeEvents` biedt callbacks voor indexering, query‑uitvoering en foutafhandeling.

#### Stap 1: Identificeer het master‑knooppunt  
Selecteer het eerste knooppunt als je master:

```csharp
using GroupDocs.Search.Scaling.Results;

SearchNetworkNode masterNode = nodes[0];
```  

#### Stap 2: Abonneer op gebeurtenissen  
Abonneer op gebeurtenissen met:

```csharp
SearchNetworkNodeEvents.Subscibe(masterNode);
```  

### Documenten indexeren

#### Overzicht
Indexeer documenten voor efficiënte zoekbewerkingen. Deze stap is cruciaal om ervoor te zorgen dat je netwerk snel de benodigde gegevens kan ophalen.

#### Definitie‑anker
`SearchIndex` is het kernobject dat doorzoekbare tokens en metadata opslaat voor elk geïndexeerd bestand.

#### Stap 1: Voeg mappen toe aan de index  
Specificeer mappen die je documenten bevatten:

```csharp
using GroupDocs.Search.Options;

IndexingDocuments.AddDirectories(masterNode, @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```  

### Zoekfunctionaliteit – Basisgebruik

#### Overzicht
Voer basiszoekbewerkingen uit over knooppunten in het netwerk.

#### Direct antwoord
Roep `SearchNetwork.Query("your term")` aan op het master‑knooppunt om direct overeenkomende documenten op te halen. De methode retourneert een collectie van `SearchResult`‑objecten die bestands‑paden en relevantiescores bevatten.  
`SearchNetwork.Query` is een methode die een zoekquery uitvoert over het gehele netwerk en overeenkomende resultaten teruggeeft.

#### Stap 1: Definieer zoekparameters  
```csharp
string wordToSearch = "tempor";
bool useSynonymSearch = false;
bool isObjectForm = false;

List<NetworkFoundDocument> searchResults = SearchAll(masterNode, wordToSearch, useSynonymSearch, isObjectForm);
```  

### Geavanceerde zoekfunctionaliteit

#### Overzicht
Gebruik geavanceerde zoektechnieken met aanpasbare parameters voor nauwkeurigere resultaten.

#### Direct antwoord
Implementeer een methode die een `SearchOptions`‑object bouwt, de eigenschappen `UseFuzzySearch`, `Highlight` en `PageSize` instelt, en het vervolgens doorgeeft aan `SearchNetwork.QueryAdvanced`. Dit levert gepagineerde, gemarkeerde resultaten op met fuzzy‑matching ingeschakeld.  
`SearchNetwork.QueryAdvanced` is een methode die een query uitvoert met geavanceerde opties zoals fuzzy‑matching en paginering.

#### Stap 1: Implementeer de geavanceerde zoekmethode  
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

### Redactie toepassen op PDF‑bestanden

#### Overzicht
Beveilig gevoelige informatie door PDF‑inhoud te redigeren voordat deze wordt opgeslagen of gedeeld.

#### Direct antwoord
Maak een `Redactor`‑instantie, laad de doel‑PDF, definieer een `RedactionPattern` (bijv. SSN‑regex), roep `redactor.Apply(pattern)` aan, en sla tenslotte het geredigeerde document op. Dit proces zorgt ervoor dat persoonlijke gegevens permanent worden verwijderd.

#### Definitie‑anker
`Redactor` is de primaire klasse in GroupDocs.Redaction die documenten verwerkt en redactie‑regels toepast.

#### Example Workflow (no new code block)  
1. Initialiseert `Redactor` met je licentie.  
2. Laadt de PDF met `redactor.Load("sample.pdf")`.  
3. `RedactionPattern` vertegenwoordigt een regel die de te redigeren tekst of het patroon specificeert. Definieer patronen zoals `new RedactionPattern(@"\d{3}-\d{2}-\d{4}")`.  
4. Voer `redactor.Apply(pattern)` uit.  
5. Sla de output op met `redactor.Save("sample_redacted.pdf")`.

### Praktische toepassingen

#### Praktijkvoorbeelden
1. **Legal Document Management** – Zoek efficiënt contracten en redigeer automatisch klant‑identifiers.  
2. **Healthcare Records** – Lokaliseer patiëntnotities terwijl je HIPAA‑conforme redactie van PHI waarborgt.  
3. **Corporate Compliance** – Scan interne communicatie op verboden termen en redigeer vóór archivering.

## Conclusie 
Deze gids biedt een uitgebreide route voor **het maken van een zoekindex .NET** oplossing die schaalt, snel indexeert en gegevens beschermt via redactie. Door knooppunten te configureren, documenten te indexeren, geavanceerde zoekfuncties te benutten en redactie toe te passen, kunnen ontwikkelaars de documentbeheersprocessen aanzienlijk verbeteren terwijl ze strikte beveiligingsnormen handhaven.

## Veelgestelde vragen

**Q: Hoe stel ik een gedistribueerd zoeknetwerk in .NET met GroupDocs op?**  
A: Definieer een basispad en poort, en roep vervolgens `SearchNetworkDeployment.Deploy()` aan om master‑ en worker‑knooppunten over machines te starten.

**Q: Kan ik geavanceerde zoekopdrachten uitvoeren met meerdere parameters in GroupDocs?**  
A: Ja — gebruik `SearchOptions` om fuzzy‑matching, wildcard‑ondersteuning en resultaat‑highlighting te combineren in één query.

**Q: Is het mogelijk om netwerkactiviteit op het master‑knooppunt te monitoren?**  
A: Absoluut — abonneer je op `SearchNetworkNodeEvents` zoals `IndexingCompleted` en `QueryExecuted` voor realtime‑inzicht.

**Q: Hoe pas ik redactie toe op PDF‑bestanden met GroupDocs?**  
A: Initialiseert een `Redactor`, laad de PDF, definieer `RedactionPattern`‑objecten (regex of letterlijke strings), roep `Apply` aan, en sla het gesaniteerde document op.

**Q: Wat is de eenvoudigste manier om de zoekprestaties te verbeteren in een netwerk‑omgeving?**  
A: Indexeer je volledige documentset volledig vóór queries, verspreid knooppunten om parallel processing te benutten, en stem `SearchOptions` af voor caching en paginering.

---
**Last Updated:** 2026-06-12  
**Tested With:** GroupDocs.Search 23.9 for .NET, GroupDocs.Redaction 23.9 for .NET  
**Author:** GroupDocs

## Gerelateerde tutorials
- [Master .NET Document Indexering met GroupDocs.Search&#58; Een uitgebreide gids](/search/net/indexing/master-net-indexing-guide-groupdocs-search/)
- [Master Document Indexering en Geavanceerde Zoekquery's met GroupDocs.Redaction .NET](/search/net/indexing/groupdocs-redaction-net-indexing-advanced-search/)
- [GroupDocs Search en Redaction onder de knie krijgen in .NET&#58; Geavanceerd documentbeheer](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
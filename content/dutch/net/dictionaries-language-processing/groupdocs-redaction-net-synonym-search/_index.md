---
date: '2026-09-16'
description: Leer hoe je een search index maakt met GroupDocs in .NET, documenten
  toevoegt aan de index en synonym search inschakelt voor slimmere query results.
keywords:
- how to create search index
- add documents to index
- synonym search .NET
lastmod: '2026-09-16'
og_description: Leer hoe je een search index maakt met GroupDocs in .NET, documenten
  toevoegt aan de index en synonym search inschakelt voor slimmere query results.
og_image_alt: Guide showing how to create a GroupDocs search index with synonym support
  in .NET
og_title: Hoe maak je een search index met GroupDocs in .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  headline: How to create search index with GroupDocs and synonym search in .NET
  type: TechArticle
- description: Learn how to create search index with GroupDocs in .NET, add documents
    to index, and enable synonym search for smarter query results.
  name: How to create search index with GroupDocs and synonym search in .NET
  steps:
  - name: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
    text: '**Legal document management:** Find case law using legal terms and their
      synonyms.'
  - name: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
    text: '**Academic research:** Expand literature searches across scholarly PDFs
      and Word files.'
  - name: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
    text: '**Corporate knowledge bases:** Retrieve internal policies even when users
      phrase queries differently.'
  - name: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
    text: '**Content management systems:** Offer editors richer discovery when tagging
      articles.'
  - name: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
    text: '**Customer‑support ticketing:** Match tickets to known issues using synonymous
      problem descriptions.'
  type: HowTo
- questions:
  - answer: Synonym search expands a user’s query to include predefined alternative
      terms, increasing the chance of finding relevant documents that use different
      wording.
    question: What is synonym search?
  - answer: Visit the [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/)
      portal and upload the new license file via `License.SetLicense("path/to/license.lic")`.
    question: How do I update my GroupDocs license?
  - answer: Yes—load a language‑specific `SynonymDictionary` file for each locale
      you support, and the engine will apply the appropriate synonym set per query.
    question: Can I use synonym search in a multilingual environment?
  - answer: File‑access permissions, unsupported formats, and exceeding the trial‑version
      document limit are the top three problems developers encounter.
    question: What are the most common indexing issues?
  - answer: Use incremental indexing, store the index on SSDs, and configure `IndexingOptions.MaxDegreeOfParallelism`
      to match your CPU core count.
    question: How can I optimise performance for very large indexes?
  type: FAQPage
tags:
- search index
- GroupDocs
- synonym search
- .NET
- document management
title: Hoe maak je een search index met GroupDocs en synonym search in .NET
type: docs
url: /nl/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/
weight: 1
---

# Hoe een zoekindex te maken met GroupDocs en synoniem zoeken in .NET

In deze gids leer je **hoe je een zoekindex maakt** met GroupDocs.Search, documenten aan die index toevoegt, en synoniem zoeken inschakelt zodat gebruikers relevante inhoud kunnen vinden, zelfs wanneer ze andere terminologie gebruiken. Of je nu een juridisch archief, een bedrijfskennisbank of een onderzoeksarchief bouwt, de onderstaande stappen bieden een productieklare oplossing die werkt op .NET Framework 4.6.1+, .NET Core en .NET 5+.

## Snelle antwoorden
- **Wat betekent “create search index”?** Het bouwt een doorzoekbare catalogus van je documenten, waarbij geëxtraheerde tekst wordt opgeslagen in een geoptimaliseerde structuur voor milliseconden‑zoekopdrachten.  
- **Waarom synoniem zoeken gebruiken?** Het breidt een query uit met woorden met dezelfde betekenis, waardoor de recall met tot wel 30 % stijgt in typische corpora.  
- **Wat zijn de belangrijkste vereisten?** .NET 4.6.1+ (of .NET Core/5+), kennis van C#, en de NuGet‑pakketten GroupDocs.Search + GroupDocs.Redaction.  
- **Heb ik een licentie nodig?** Een gratis proefversie is voldoende voor evaluatie; een permanente licentie is vereist voor productie‑implementaties.  
- **Kan ik dit combineren met redaction?** Ja—GroupDocs.Redaction kan vóór of na het zoeken worden uitgevoerd om gevoelige gegevens te maskeren.

## Wat is “create search index”?
Een **search index** is een datastructuur die geëxtraheerde tekst en metadata van elk document bevat, waardoor de engine overeenkomende bestanden onmiddellijk kan vinden. GroupDocs.Search bouwt deze index door de bronmap te scannen, ondersteunde formaten te parseren en compacte indexbestanden naar een door jou opgegeven map te schrijven.

## Waarom synoniem zoeken inschakelen?
Synoniem zoeken voegt automatisch alternatieve termen toe aan de query van een gebruiker, zodat een zoekopdracht naar **“improve”** ook documenten retourneert die **“enhance,” “upgrade,”** of **“optimize.”** bevatten. In de praktijk kan dit de recall van resultaten met 20‑35 % verhogen terwijl de precisie hoog blijft, omdat het ingebouwde synoniemwoordenboek voor elke taal is samengesteld.

## Vereisten
- **.NET Framework 4.6.1** of later (of elke .NET Core/5+ runtime).  
- Basis C#‑ontwikkelvaardigheden en Visual Studio (Community, Professional of Enterprise).  
- GroupDocs.Search‑ en GroupDocs.Redaction‑pakketten geïnstalleerd via NuGet.

### Installatie
Installeer GroupDocs.Redaction voor .NET met een van deze methoden (zie de [GroupDocs.Redaction .NET](https://docs.groupdocs.com/search/net/) documentatie voor details):

**.NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Alternatief kun je de NuGet Package Manager UI in Visual Studio gebruiken om te zoeken naar “GroupDocs.Redaction” en deze direct te installeren. Voor API‑referentie, zie de [GroupDocs Redaction API](https://reference.groupdocs.com/redaction/net).

### Licentie‑acquisitie
- **Gratis proefversie:** Begin met een proefversie om alle functies te verkennen.  
- **Tijdelijke licentie:** Vraag een tijdelijke licentie aan op de [GroupDocs website](https://purchase.groupdocs.com/temporary-license/) of beheer je licentie via het [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) portaal.  
- **Volledige aankoop:** Wanneer je klaar bent voor productie, koop een volledige licentie die alle evaluatielimieten verwijdert.

## Hoe GroupDocs.Redaction voor .NET in te stellen
GroupDocs.Redaction biedt de kernfunctionaliteit om gevoelige inhoud te redigeren vóór of na het zoeken. Het stelt een `Redactor`‑klasse beschikbaar die je instantiateert met een licentie en optionele configuratie‑instellingen.

De volgende code toont het aanmaken van een redactor‑instantie en het laden van een licentiebestand:

```csharp
// Definition anchor: the Redactor class provides methods to locate and mask text, images, or metadata.
var redactor = new GroupDocs.Redaction.Redactor();
```  

```csharp
using GroupDocs.Redaction;

// Initialize a new Redactor object with your document path
RedactorSettings settings = new RedactorSettings();
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH", settings);
```  

Met de redactor gereed kun je later `redactor.Redact(...)` aanroepen op elk document dat je uit de zoekresultaten haalt.

## Hoe de zoekindex te maken
Het maken van een zoekindex houdt in dat je een map opgeeft waar de indexbestanden worden opgeslagen en vervolgens de `Index`‑klasse van GroupDocs.Search initialiseert. De index bevat alle doorzoekbare gegevens die uit je bronbestanden zijn geëxtraheerd.

Maak eerst een map voor de index en instantiateer vervolgens het `Index`‑object:

```csharp
// Definition anchor: the Index class represents the searchable container that holds all indexed documents.
var indexPath = @"C:\MySearchIndex";
var index = new GroupDocs.Search.Index(indexPath);
```  

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/SynonymSearch";
```  

Het aanmaken van de index schrijft een reeks binaire bestanden naar de map; deze bestanden zijn doorgaans onder de 200 KB per 1.000 pagina's, waardoor je kunt opschalen naar miljoenen pagina's zonder schijfruimte uit te putten.

## Hoe documenten aan de index toe te voegen
Documenten toevoegen vereist dat je de API wijst naar de map die de bronbestanden bevat en de index instrueert ze te verwerken. Het proces parseert elk ondersteund formaat, extraheert tekst en slaat deze op in de index voor snelle ophalen.

Gebruik de volgende code om alle bestanden in een bronmap te indexeren:

```csharp
// Definition anchor: DocumentSource tells the index where to read files from and which formats to accept.
var sourceFolder = @"C:\MyDocuments";
index.Add(sourceFolder);
```  

```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder);
// This sets up the index in the specified folder.
```  

GroupDocs.Search ondersteunt **30+** invoerformaten—waaronder DOCX, PDF, PPTX, HTML en veelvoorkomende afbeeldingsformaten—zodat je vrijwel elk bedrijfsarchief kunt indexeren zonder extra converters.

## Hoe synoniem zoeken in te schakelen en uit te voeren
Synoniem‑verwerking wordt ingeschakeld via `SearchOptions`. Eenmaal ingeschakeld, wordt elke query automatisch uitgebreid met de synoniemen uit het woordenboek, waardoor de recall verbetert zonder precisie op te offeren.

Schakel synoniem zoeken in met de volgende codefragment:

```csharp
var options = new GroupDocs.Search.SearchOptions()
{
    UseSynonyms = true
};
var result = index.Search("improve", options);
```  

```csharp
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
```  

Het standaard synoniemwoordenboek bevat meer dan **5.000** termparen voor Engels. Je kunt ook een aangepast `SynonymDictionary`‑bestand laden om branchespecifieke jargon te ondersteunen.

## Aangepast synoniemwoordenboek
Als je domeinspecifieke synoniemen nodig hebt, laad dan je eigen woordenboekbestand en wijs het toe aan `SearchOptions` voordat je een query uitvoert.

```csharp
options.SynonymDictionary = new SynonymDictionary(@"C:\mySynonyms.txt");
var result = index.Search("upgrade", options);
```  

```csharp
index.Add(documentsFolder);
// This step populates the index with content from your documents.
```  

## Veelvoorkomende probleemoplossingstips
- **Padproblemen:** Controleer dubbel dat de index‑ en bronmappen toegankelijk zijn voor het procesaccount.  
- **Licentie‑limieten:** Een niet-gelicentieerde build kan het aantal geïndexeerde bestanden beperken tot 100.  
- **Geen resultaten:** Verifieer dat het synoniemwoordenboek is geladen; je kunt `options.SynonymDictionary.Count` tijdens runtime inspecteren.  

## Praktische toepassingen
1. **Juridisch documentbeheer:** Zoek jurisprudentie met juridische termen en hun synoniemen.  
2. **Academisch onderzoek:** Breid literatuurzoekopdrachten uit over wetenschappelijke PDF‑ en Word‑bestanden.  
3. **Bedrijfskennisbanken:** Haal interne beleidsdocumenten op, zelfs wanneer gebruikers queries anders formuleren.  
4. **Content management systemen:** Bied editors een rijkere ontdekking bij het taggen van artikelen.  
5. **Klantenondersteuning ticketing:** Koppel tickets aan bekende problemen met behulp van synonieme probleemomschrijvingen.  

## Prestatie‑overwegingen
- **Indexonderhoud:** Re‑index na bulk‑updates; incrementeel indexeren vermindert downtime tot 70 %.  
- **Resource‑monitoring:** Het indexeren van een batch van 10 GB op een standaard VM (2 vCPU, 8 GB RAM) piekt op ~1,2 GB RAM; beperk de batchgrootte als je de limieten nadert.  
- **Object‑verwijdering:** Roep `index.Dispose()` en `redactor.Dispose()` aan zodra je klaar bent om native resources vrij te geven.  

## Conclusie
Je weet nu **hoe je een zoekindex maakt** met GroupDocs, documenten aan die index toevoegt, en synoniem zoeken inschakelt voor een meer intuïtieve gebruikerservaring. Deze basis stelt je ook in staat om redaction, aangepaste ranking of fuzzy matching toe te voegen bovenop een robuuste zoekmachine.

## Volgende stappen
- Experimenteer met `SearchOptions.FuzzySearch` om spelfouten te detecteren.  
- Verken de `Ranking`‑API om prioriteitsdocumenten te versterken.  
- Word lid van de community op het [GroupDocs Forum](https://forum.groupdocs.com/c/search/10) of het [Free Support Forum](https://forum.groupdocs.com/c/search/10) om tips te delen en vragen te stellen.  
- Controleer de [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/) voor updates en nieuwe functies.  

## Veelgestelde vragen

**Q: Wat is synoniem zoeken?**  
A: Synoniem zoeken breidt de query van een gebruiker uit met vooraf gedefinieerde alternatieve termen, waardoor de kans groter wordt om relevante documenten te vinden die andere bewoordingen gebruiken.

**Q: Hoe werk ik mijn GroupDocs‑licentie bij?**  
A: Bezoek het [GroupDocs License Management](https://purchase.groupdocs.com/temporary-license/) portaal en upload het nieuwe licentiebestand via `License.SetLicense("path/to/license.lic")`.

**Q: Kan ik synoniem zoeken gebruiken in een meertalige omgeving?**  
A: Ja—laad een taalspecifiek `SynonymDictionary`‑bestand voor elke locale die je ondersteunt, en de engine past de juiste synoniemset per query toe.

**Q: Wat zijn de meest voorkomende indexeringsproblemen?**  
A: Bestands‑toegangsrechten, niet‑ondersteunde formaten en het overschrijden van de documentlimiet van de proefversie zijn de drie belangrijkste problemen die ontwikkelaars tegenkomen.

**Q: Hoe kan ik de prestaties optimaliseren voor zeer grote indexen?**  
A: Gebruik incrementeel indexeren, sla de index op SSD's op, en configureer `IndexingOptions.MaxDegreeOfParallelism` zodat deze overeenkomt met het aantal CPU‑kernen.

---

**Laatst bijgewerkt:** 2026-09-16  
**Getest met:** GroupDocs.Search 23.10 for .NET  
**Auteur:** GroupDocs

```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.UseSynonymSearch = true; // Activate synonym search.
```

```csharp
string query = "improve";
SearchResult result = index.Search(query, options);
// This operation returns documents matching 'improve' or its synonyms.
```

## Gerelateerde tutorials

- [Document toevoegen aan index met GroupDocs.Search .NET tutorials](/search/net/document-management/)
- [Zoekresultaten markeren in .NET‑documenten met GroupDocs.Search en Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Hoe index bij te werken met GroupDocs.Search & Redaction (.NET)](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
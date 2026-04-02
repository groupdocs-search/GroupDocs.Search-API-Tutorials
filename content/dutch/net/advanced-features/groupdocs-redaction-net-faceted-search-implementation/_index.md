---
date: '2026-04-02'
description: Leer hoe je een zoekindex met GroupDocs maakt en documenten aan de index
  toevoegt, terwijl je gefacetteerd zoeken implementeert met GroupDocs.Search en GroupDocs.Redaction
  in .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Maak zoekindex GroupDocs met redactie .NET gefacetteerd zoeken
type: docs
url: /nl/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Maak zoekindex GroupDocs met Redaction .NET Faceted Search

## Snelle antwoorden
- **Wat is het primaire doel?** Om een zoekindex te maken met GroupDocs en gefacetteerd zoeken mogelijk te maken.  
- **Welke bibliotheken zijn vereist?** GroupDocs.Redaction en GroupDocs.Search voor .NET.  
- **Hoe voeg ik documenten toe aan de index?** Gebruik `index.Add(documentsFolder)` na het initialiseren van de index.  
- **Kan ik complexe queries uitvoeren?** Ja, combineer objectqueries met logische operatoren voor geavanceerde filtering.  
- **Is een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.

## Wat is gefacetteerd zoeken en waarom gebruiken met GroupDocs?
Gefacetteerd zoeken stelt gebruikers in staat resultaten te verfijnen door meerdere filters toe te passen—zoals categorie, datum of auteur—tegelijkertijd. In combinatie met **GroupDocs.Redaction** krijg je beveiligde, doorzoekbare inhoud die redactie‑regels respecteert, waardoor het ideaal is voor omgevingen met strenge naleving.

## Voorvereisten

### Vereiste bibliotheken, versies en afhankelijkheden
- **GroupDocs.Redaction .NET** – nieuwste stabiele release.  
- **GroupDocs.Search .NET** – werkt hand‑in‑hand met Redaction voor indexering.

### Vereisten voor omgeving configuratie
- **IDE**: Visual Studio 2019 of later.  
- **Framework**: .NET Core 3.1, .NET 5, of .NET 6.  
- **OS Compatibility**: Windows, Linux, macOS.

### Kennisvereisten
Basis C#-vaardigheden en een algemeen begrip van gefacetteerde zoekconcepten zijn nuttig, maar de stapsgewijze handleiding is ook vriendelijk voor nieuwkomers.

## Instellen van GroupDocs.Redaction voor .NET

### Installatie-informatie
Je kunt het GroupDocs.Redaction‑pakket toevoegen met een van de volgende methoden:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Zoek naar "GroupDocs.Redaction" en installeer de nieuwste versie.

### Stappen voor licentie‑acquisitie
Om alle functies te ontgrendelen, begin met een gratis proefversie of verkrijg een permanente licentie:

1. Bezoek [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) om licentieopties te verkennen.  
2. Volg de instructies op het scherm om uw proef‑ of gekochte licentiebestand te ontvangen.

### Basisinitialisatie en -configuratie
Zodra het pakket is geïnstalleerd, initialiseert u de Redactor in uw applicatie:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Hoe maak je een zoekindex groupdocs

Hieronder splitsen we de implementatie in twee delen: **Simple Faceted Search** en **Complex Query**. Elk deel toont hoe je **een zoekindex groupdocs maakt**, documenten toevoegt en queries uitvoert.

### Functie 1: Eenvoudig gefacetteerd zoeken

**Overzicht**  
Gefacetteerd zoeken stelt gebruikers in staat resultaten te beperken door meerdere criteria te selecteren. Deze sectie demonstreert een eenvoudige aanpak met GroupDocs.Search.

#### Stap 1: Definieer index- en documentenmappen
Stel de mappaden in waar de index wordt opgeslagen en waar uw bron documenten zich bevinden.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Stap 2: Maak een index
Initialiseer de zoekindex in de map die u hebt gedefinieerd.

```csharp
Index index = new Index(indexFolder);
```

#### Stap 3: Voeg documenten toe aan de index
Laad uw documenten zodat ze doorzoekbaar worden.

```csharp
index.Add(documentsFolder);
```

#### Stap 4: Voer een tekstquery-zoekopdracht uit
Voer een eenvoudige tekstquery uit op het **content**-veld.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Stap 5: Voer een objectquery-zoekopdracht uit
Gebruik objectgeoriënteerde queries voor fijnere controle.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Functie 2: Complexe query

**Overzicht**  
Wanneer u meerdere filters moet combineren—zoals bestandsnaampatronen en frase‑overeenkomsten—kunt u een complexe query bouwen met logische operatoren.

#### Stap 1: Definieer index- en documentenmappen
Herbruik dezelfde mapstructuur voor een geavanceerder scenario.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Stap 2: Maak een index en voeg documenten toe
( Zie stappen 2‑3 van het eenvoudige voorbeeld; ze blijven hetzelfde. )

#### Stap 3: Voer tekstquery-zoekopdracht uit
Voer een samengestelde tekstquery uit die bestandsnaam- en inhoudcriteria combineert.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Stap 4: Bouw en voer objectqueries uit
Construeer dezelfde logica programmatisch.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Blijf frasen, bereiken en Booleaanse operatoren combineren om aan uw exacte bedrijfsregels te voldoen.

## Praktische toepassingen

1. **E‑Commerce Platforms** – Filter producten op categorie, prijs en beoordeling.  
2. **Document Management Systems** – Zoek contracten op auteur, datum of vertrouwelijkheidsniveau.  
3. **Content Portals** – Laat lezers filteren op tags, onderwerpen en publicatiedata.

## Prestatieoverwegingen

- **Index Refresh**: Indexeer regelmatig nieuwe of bijgewerkte bestanden opnieuw om het zoeken snel te houden.  
- **Memory Management**: Vernietig `Index`-objecten wanneer ze niet meer nodig zijn, vooral bij grote datasets.  
- **Asynchronous Indexing**: Gebruik `Task.Run` of achtergrondservices om UI-bevriezingen tijdens zware indexering te voorkomen.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oplossing |
|----------|-----------|
| **Index niet gevonden** | Controleer het pad van `indexFolder` en zorg ervoor dat de map schrijfrechten heeft. |
| **Geen resultaten teruggekregen** | Controleer of de velden die u queryt (bijv. `Content`, `Filename`) geïndexeerd zijn. |
| **Out‑of‑memory fouten** | Verwerk documenten in batches en overweeg de .NET GC-heapgrootte te verhogen. |

## Veelgestelde vragen

**Q: Wat is gefacetteerd zoeken?**  
A: Gefacetteerd zoeken stelt gebruikers in staat resultaten te verfijnen met meerdere, onafhankelijke filters zoals categorie, datum of auteur.

**Q: Hoe ga ik om met grote datasets met GroupDocs.Search?**  
A: Gebruik incrementele indexering, batchverwerking en asynchrone operaties om het geheugenverbruik laag en de prestaties hoog te houden.

**Q: Kan ik GroupDocs-functionaliteiten integreren in bestaande .NET-toepassingen?**  
A: Ja, de bibliotheken zijn ontworpen voor naadloze integratie met elk .NET-project.

**Q: Wat zijn enkele veelvoorkomende problemen met gefacetteerd zoeken?**  
A: Complexe query‑syntaxis en het zorgen dat alle relevante velden geïndexeerd zijn, zijn typische uitdagingen; grondig testen en indexonderhoud beperken deze.

**Q: Hoe verkrijg ik een tijdelijke licentie voor GroupDocs?**  
A: Bezoek de [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) om een proeflicentie aan te vragen die volledige functionaliteit ontgrendelt tijdens evaluatie.

## Bronnen
- **Documentatie**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API-referentie**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Laatst bijgewerkt:** 2026-04-02  
**Getest met:** GroupDocs.Redaction 23.12 voor .NET, GroupDocs.Search 23.12 voor .NET  
**Auteur:** GroupDocs
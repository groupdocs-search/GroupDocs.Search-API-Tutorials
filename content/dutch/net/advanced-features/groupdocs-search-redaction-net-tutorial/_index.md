---
date: '2026-04-04'
description: Leer hoe u juridische documenten kunt doorzoeken en indexen kunt beheren
  met GroupDocs.Search, en hoe u redactie voor medische dossiers kunt integreren met
  GroupDocs.Redaction in .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Zoek juridische documenten met GroupDocs Search & Redaction voor .NET
type: docs
url: /nl/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Zoek juridische documenten met GroupDocs Search & Redaction in .NET

In de hedendaagse data‑gedreven omgeving is **het zoeken naar juridische documenten** snel en veilig een kritische eis voor elke organisatie. Of u nu contracten, gerechtelijke stukken of compliance‑rapporten verwerkt, GroupDocs.Search biedt u een snelle, schaalbare index, terwijl GroupDocs.Redaction ervoor zorgt dat gevoelige informatie verborgen blijft. Deze tutorial leidt u door het opzetten van een doorzoekbare index, het toevoegen van documenten uit meerdere mappen en het configureren van redaction zodat u veilig medische dossiers en andere vertrouwelijke bestanden kunt doorzoeken.

## Snelle antwoorden
- **Wat doet GroupDocs.Search?** Het maakt een full‑text doorzoekbare index voor een breed scala aan documentformaten.  
- **Kan ik informatie redigeren vóór het zoeken?** Ja – gebruik GroupDocs.Redaction om gevoelige gegevens te maskeren of te verwijderen.  
- **Hoe voeg ik documenten toe aan de index?** Roep `index.Add("folderPath")` aan voor elke map die u wilt opnemen.  
- **Welke bestandstypen worden ondersteund?** PDF’s, DOCX, PPTX, TXT en nog veel meer.  
- **Heb ik een licentie nodig voor productie?** Er is een tijdelijke proef beschikbaar; een permanente licentie is vereist voor commercieel gebruik.

## Vereisten
Om deze tutorial te volgen, zorg dat u het volgende heeft:
- .NET Core SDK (3.1 of later) geïnstalleerd.
- Visual Studio Code, Visual Studio, of een andere IDE die .NET ondersteunt.
- Basiskennis van C# programmeren.

### Licentie‑acquisitie
U kunt beginnen met een gratis proefversie van beide bibliotheken. Voor uitgebreid gebruik kunt u overwegen een tijdelijke licentie aan te schaffen of er een te kopen via de [GroupDocs-website](https://purchase.groupdocs.com/temporary-license/).

## Installeren van de vereiste pakketten

**GroupDocs.Search installatie:**  
Met **.NET CLI**, voer uit:
```bash
dotnet add package GroupDocs.Search
```
Alternatief, gebruik de Package Manager Console in Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction installatie:**  
- Gebruik .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Of, via Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Bezoek de NuGet Package Manager UI en zoek naar "GroupDocs.Redaction" om deze te installeren als u de voorkeur geeft aan een GUI.

## Configureer Redactor‑instellingen
Voordat u begint met redigeren, wilt u misschien het gedrag van de redactor aanpassen (bijv. de redactiekleur instellen of aangepaste patronen definiëren). Het volgende fragment toont de basisinitialisatie:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Pro tip:** Pas `redactorSettings` aan om te voldoen aan de compliance‑richtlijnen van uw organisatie (bijv. tekst vervangen door zwarte vakken, OCR toepassen vóór redactie, enz.).

## Implementatie‑gids

### Hoe juridische documenten zoeken?
Het creëren van een doorzoekbare index is de basis voor snelle vindbaarheid van juridische documenten. GroupDocs.Search stelt u in staat om naar elke map te wijzen, een index op te bouwen en vervolgens complexe queries uit te voeren over duizenden bestanden.

### Hoe documenten toevoegen aan de index
Documenten toevoegen is eenvoudig — wijs de bibliotheek simpelweg op de mappen die uw bestanden bevatten. U kunt meerdere mappen toevoegen, wat handig is wanneer uw juridische corpus verspreid is over verschillende locaties.

#### Een index maken en beheren
**Overzicht:**  
Het creëren van een index is de eerste stap naar efficiënte documentzoekoperaties. GroupDocs.Search maakt het mogelijk om een doorzoekbare index te maken in elke gewenste map, waardoor snelle vindbaarheid van documenten mogelijk wordt.

##### Stap 1: Maak de index
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Uitleg:* `Index` initialiseert een zoekindex in de opgegeven directory. Zorg ervoor dat het pad overeenkomt met de mapstructuur van uw project.

##### Stap 2: Documenten toevoegen aan een index
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Uitleg:* De `Add`‑methode scant de opgegeven map en neemt elk ondersteund document op in de index. Gebruik dit om **documenten toe te voegen aan de index** vanuit meerdere bronnen, zoals contracten, dossiers of medische dossiers.

### Rapporten over indexering ophalen en weergeven
**Overzicht:**  
Indexeringsrapporten geven inzicht in hoeveel documenten zijn verwerkt, het totale aantal termen en de opslaggrootte — essentiële statistieken voor prestatie‑afstemming.

```csharp
using System;

// Retrieve indexing reports
IndexingReport[] reports = index.GetIndexingReports();

foreach (IndexingReport report in reports)
{
    Console.WriteLine("Time: " + report.StartTime);
    Console.WriteLine("Duration: " + report.IndexingTime);
    Console.WriteLine("Documents total: " + report.TotalDocumentsInIndex);
    Console.WriteLine("Terms total: " + report.TotalTermCount);
    Console.WriteLine("Indexed documents size (MB): " + report.IndexedDocumentsSize);
    Console.WriteLine("Index size (MB): " + (report.TotalIndexSize / 1024.0 / 1024.0));
}
```
*Uitleg:* `GetIndexingReports` retourneert een array van rapporten die het indexeringsproces beschrijven, waardoor u de prestaties kunt monitoren en optimaliseren.

## Praktische toepassingen
1. **Juridisch documentbeheer:** Automatiseer het indexeren van dossiers voor directe vindbaarheid van wetten, memoranda en uitspraken.  
2. **Medisch dossiersysteem:** Zoek patiëntendossiers terwijl u de privacy behoudt door GroupDocs.Redaction te gebruiken om PHI te maskeren.  
3. **Corporate HR Portal:** Combineer doorzoekbare personeelsdossiers met redactie om persoonlijke gegevens te beschermen.

## Prestatie‑overwegingen
- **Optimaliseren van indexgrootte:** Verwijder periodiek verouderde items en bouw de index opnieuw om deze slank te houden.  
- **Geheugenbeheer:** Maak gebruik van de garbage collector van .NET; verwijder `Index`‑objecten wanneer ze niet meer nodig zijn.  
- **Schaalbaarheid best practices:** Sla de index op snelle SSD‑opslag op en overweeg het sharden van grote corpora over meerdere indexen.

## Veelgestelde vragen

**Q: Wat zijn de belangrijkste toepassingen van GroupDocs.Search?**  
A: Het is ideaal voor het creëren van doorzoekbare indexen uit grote documentcollecties, waardoor snelle vindbaarheid van juridische en medische bestanden mogelijk is.

**Q: Hoe zorgt GroupDocs.Redaction voor gegevensprivacy?**  
A: Het laat u redactiepatern definieren die gevoelige informatie permanent verwijderen of maskeren voordat het document wordt geïndexeerd of gedeeld.

**Q: Kan ik deze bibliotheken gebruiken in een cloud‑omgeving?**  
A: Ja — beide bibliotheken werken in Azure, AWS of elke gecontaineriseerde .NET‑implementatie met de juiste licentie.

**Q: Welke bestandsformaten ondersteunt GroupDocs.Search?**  
A: PDF’s, Word, Excel, PowerPoint, TXT, HTML en nog veel meer enterprise‑formaten.

**Q: Hoe los ik indexeringsfouten op?**  
A: Controleer map‑paden, controleer bestandsrechten en bekijk de console‑output van `IndexingReport` voor specifieke foutcodes.

## Bronnen
- **Documentatie:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API‑referentie:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Gratis ondersteuning:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tijdelijke licentie:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Laatst bijgewerkt:** 2026-04-04  
**Getest met:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Auteur:** GroupDocs
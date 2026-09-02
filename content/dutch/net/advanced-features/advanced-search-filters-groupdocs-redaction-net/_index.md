---
date: '2026-04-02'
description: Leer hoe u kunt filteren op bestandsextensie en alleen txt‑bestanden
  kunt zoeken met GroupDocs.Redaction voor .NET—verhoog de efficiëntie van documentbeheer.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filter op bestandsextensie in .NET met GroupDocs.Redaction
type: docs
url: /nl/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filter op bestandsextensie in .NET met GroupDocs.Redaction

Het doorzoeken van een enorme verzameling bestanden kan overweldigend aanvoelen, vooral wanneer je alleen resultaten nodig hebt van specifieke bestandstypen. In deze tutorial ontdek je **hoe je kunt filteren op bestandsextensie** met GroupDocs.Redaction voor .NET, waardoor je alleen txt‑bestanden of elke andere extensie die je kiest kunt doorzoeken. We lopen door het instellen van zowel bestandstype‑ als padgebaseerde filters, zodat je snel precies de documenten kunt vinden die je nodig hebt.

## Snelle antwoorden
- **Wat doet “filteren op bestandsextensie”?** Het beperkt een zoekopdracht tot documenten die overeenkomen met een gegeven bestandsextensie (bijv. *.txt).  
- **Waarom GroupDocs.Redaction hiervoor gebruiken?** Het biedt ingebouwde filter‑API's die snel en eenvoudig te integreren zijn.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor testen; een betaalde licentie is vereist voor productie.  
- **Welke .NET‑versies worden ondersteund?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Kan ik bestandstype‑ en padfilters combineren?** Ja—pas meerdere filters toe voor zeer precieze zoekopdrachten.

## Wat je zult leren
- Hoe je **filtert op bestandsextensie** zodat alleen tekstbestanden worden doorzocht.  
- Hoe je **bestandspad‑filters** instelt om resultaten te beperken tot specifieke mappen of naamgevingspatronen.  
- Tips om je index snel en geheugen‑efficiënt te houden.

## Voorvereisten

Voordat je begint, zorg ervoor dat je het volgende hebt:

- **GroupDocs.Redaction Library** geïnstalleerd en compatibel met je .NET‑project.  
- Een ontwikkelomgeving zoals Visual Studio of VS Code.  
- Basiskennis van C# en vertrouwdheid met de .NET‑projectstructuur.

## GroupDocs.Redaction voor .NET instellen

Eerst voeg je de bibliotheek toe aan je project.

**Gebruik .NET CLI:**
```bash
dotnet add package GroupDocs.Redaction
```

**Gebruik Package Manager:**
```bash
Install-Package GroupDocs.Redaction
```

Of zoek “GroupDocs.Redaction” in de NuGet Package Manager UI en installeer de nieuwste versie.

### Licentie‑acquisitie

Je kunt beginnen met een gratis proefversie of een tijdelijke licentie aanvragen. Voor langdurige projecten koop je een licentie via de officiële site.

### Basisinitialisatie

Nadat het pakket is geïnstalleerd, maak je een index aan die verwijzingen naar je documenten bevat:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Implementatie‑gids

### Functie 1: Een filter instellen voor tekstdocumenten (.txt)

#### Hoe filter je op bestandsextensie voor tekstdocumenten

1. **Definieer de index en documentmappen**  
   Stel de paden in waar je bronbestanden zich bevinden:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Maak een Index**  
   Laad alle bestanden uit de bronmap in de index:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Configureer Zoekopties met een bestandsextensie‑filter**  
   Geef de engine aan alleen *.txt‑bestanden te overwegen:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Voer de zoekopdracht uit**  
   Voer een query uit; het filter zorgt ervoor dat niet‑tekstbestanden worden genegeerd:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Uitleg*: De `Search`‑methode retourneert resultaten die voldoen aan het filter, waardoor ruis drastisch wordt verminderd en de prestaties verbeteren.

### Functie 2: Bestandspad‑filters

#### Waarom bestandspad‑filters gebruiken?

Soms moet je zoekopdrachten beperken tot een specifieke afdelingsmap of een reeks bestanden die een naamgevingsconventie delen. Padfilters maken dit mogelijk.

1. **Definieer de index en documentmappen**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Maak een Index**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Configureer Zoekopties met een pad‑gebaseerde reguliere expressie**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Deze reguliere expressie matcht elk bestand waarvan het volledige pad het woord “Lorem” bevat, waardoor je specifieke sub‑mappen kunt targeten.

4. **Voer de pad‑gebaseerde zoekopdracht uit**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Praktische toepassingen
- **Juridisch documentbeheer** – Snel relevante contracten vinden die als platte‑tekstbestanden zijn opgeslagen.  
- **Academisch onderzoek** – Alleen *.txt‑onderzoeksnotities ophalen die bij een specifieke projectmap horen.  
- **Bedrijfsrapportage** – Interne rapporten filteren op afdelingspad (bijv. `/Finance/2025/`).  

## Prestatie‑overwegingen
- Indexeer alleen de documenttypen die je daadwerkelijk nodig hebt; onnodige bestanden vergroten de indexgrootte en zoektijd.  
- Houd je index up‑to‑date met een geplande taak die `index.Add()` aanroept voor nieuwe of gewijzigde bestanden.  
- Gebruik eenvoudige reguliere expressies; te complexe patronen kunnen de zoekengine vertragen.  
- Vernietig `Index`‑objecten wanneer ze niet meer nodig zijn om geheugen vrij te maken.

## Conclusie
Je weet nu hoe je **filtert op bestandsextensie** en **bestandspad‑filters** toepast met GroupDocs.Redaction voor .NET. Deze technieken geven je fijnmazige controle over grote documentcollecties, waardoor zoekopdrachten sneller en relevanter worden. Probeer vervolgens meerdere filters te combineren of de zoekfunctie te integreren in een grotere applicatieworkflow.

## Veelgestelde vragen

**V1: Kan ik documenten filteren die geen tekstbestanden zijn?**  
A1: Ja, GroupDocs.Redaction ondersteunt veel formaten. Verander het argument in `CreateFileExtension` naar de gewenste extensie (bijv. ".pdf").

**V2: Hoe werk ik mijn zoekindex regelmatig bij?**  
A2: Plan een achtergrondservice of een cron‑taak die `index.Add()` uitvoert op de mappen die je up‑to‑date wilt houden.

**V3: Heeft filteren op bestandspad invloed op de prestaties?**  
A3: Goed geoptimaliseerde reguliere expressies hebben minimale impact, maar benchmark altijd met je eigen dataset.

**V4: Kan ik meerdere filters combineren voor verfijndere zoekopdrachten?**  
A4: Absoluut. Je kunt filters ketenen of samengestelde filters maken om zowel bestandstype als pad tegelijk te targeten.

**V5: Waar kan ik meer bronnen vinden over GroupDocs.Redaction?**  
A5: Bezoek de officiële documentatie op [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) voor gedetailleerde handleidingen en API‑referenties.

## Veelgestelde vragen

**V: Werkt de `SearchDocumentFilter` met versleutelde bestanden?**  
A: Het filter zelf werkt op bestandsmetadata, dus versleutelde bestanden worden nog steeds geïndexeerd als je de benodigde decryptie‑referenties tijdens het indexeren opgeeft.

**V: Kan ik jokertekens gebruiken in plaats van een reguliere expressie voor padfiltering?**  
A: De API vereist momenteel een reguliere expressie, maar je kunt eenvoudige jokertekens simuleren (bijv. `.*` voor willekeurige tekens).

**V: Hoe groot kan de index worden voordat ik moet overwegen te sharden?**  
A: Indexen van enkele honderden gigabytes kunnen profiteren van het splitsen in meerdere logische indexen; test de prestaties naarmate je collectie groeit.

**V: Zijn er ingebouwde methoden om documenten uit de index te verwijderen?**  
A: Ja—roep `index.Delete(documentId)` of `index.DeleteAll()` aan om verouderde items te beheren.

**V: Is er een manier om zoekresultaten te bekijken voordat het volledige document wordt geladen?**  
A: Het `SearchResult`‑object bevat snippet‑informatie die je in de UI kunt weergeven zonder het hele bestand te openen.

## Bronnen
- **Documentatie**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API‑referentie**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Gratis ondersteuning**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Tijdelijke licentie**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Laatst bijgewerkt:** 2026-04-02  
**Getest met:** GroupDocs.Redaction 23.12 for .NET  
**Auteur:** GroupDocs
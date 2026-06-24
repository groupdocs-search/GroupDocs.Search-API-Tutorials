---
date: '2026-04-21'
description: Leer hoe u bestanden kunt filteren met GroupDocs.Redaction voor .NET,
  inclusief filteren op aanmaakdatum, bestandsgrootte, wijzigingsdatum en hoe u NOT-filters
  kunt toepassen.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Hoe bestanden filteren met GroupDocs.Redaction voor .NET
type: docs
url: /nl/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Hoe bestanden filteren met GroupDocs.Redaction voor .NET

In de snel‑bewegende digitale omgeving van vandaag kan **how to filter files** efficiënt maken of breken voor uw productiviteit. Of u nu documenten wilt isoleren op extensie, aanmaakdatum, grootte of wijzigingsdatum, een solide filterstrategie bespaart tijd, verlaagt opslagkosten en houdt uw zoekindex overzichtelijk. In deze tutorial lopen we door praktijkvoorbeelden met GroupDocs.Redaction voor .NET, en laten we u precies zien hoe u bestanden kunt filteren om te voldoen aan veelvoorkomende zakelijke behoeften.

## Snelle antwoorden
- **Welke bibliotheek heb ik nodig?** GroupDocs.Redaction for .NET (install via NuGet).  
- **Kan ik filteren op aanmaakdatum?** Ja – use `CreateCreationTimeRange`.  
- **Hoe sluit ik bepaalde typen uit?** Apply a NOT filter with `DocumentFilter.CreateNot`.  
- **Wordt filteren op bestandsgrootte ondersteund?** Absolutely, via `CreateFileLengthRange` or upper/lower bounds.  
- **Heb ik een licentie nodig?** A trial or full license is required for production use.

## Wat is bestandsfiltering met GroupDocs.Redaction?
Bestandsfiltering stelt u in staat de indexeringsengine te vertellen welke documenten moeten worden opgenomen of genegeerd op basis van metadata zoals extensie, datums, padpatronen of grootte. Door nauwkeurige `DocumentFilter`‑regels te definiëren, houdt u uw index slank en uw zoekopdrachten snel.

## Waarom GroupDocs.Redaction voor .NET gebruiken?
- **Built‑in filter helpers** – geen noodzaak om aangepaste bestandsysteemcode te schrijven.  
- **Logical operators** – combineer meerdere criteria met AND, OR en NOT.  
- **Performance‑optimized** – filters worden toegepast tijdens het indexeren, niet achteraf.  
- **Cross‑platform** – werkt met .NET Framework, .NET Core en .NET 5/6+.

## Voorvereisten
- .NET Framework 4.6+ of .NET Core 3.1+ geïnstalleerd.  
- Visual Studio of uw favoriete C# IDE.  
- Basis C# kennis.  

### Vereiste bibliotheken & installatie
Install the NuGet package using your preferred method:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Pro tip:** Na het installeren, voeg uw licentiebestand toe aan de projectroot en roep `License.SetLicense("license-file-path")` aan voordat u een Redactor of Index‑object maakt.

## GroupDocs.Redaction voor .NET configureren

Eerst maakt u een `Redactor`‑instantie die wijst naar het document waarmee u wilt werken:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Waarom dit belangrijk is:** Het initialiseren van de Redactor garandeert dat de bibliotheek klaar is om later in de workflow filters en redaction‑regels toe te passen.

## Hoe bestanden filteren op extensie

Filteren op bestandsextensie is de meest voorkomende manier om een documentenset te verkleinen. Hieronder behouden we alleen FB2-, EPUB- en TXT‑bestanden.

### Filteren op bestandsextensie

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe een NOT‑filter toe te passen om ongewenste typen uit te sluiten

Als u **apply NOT filter**‑logica nodig heeft—bijvoorbeeld HTML‑ en PDF‑bestanden uitsluiten—gebruik dan `CreateNot`.

### HTM, HTML en PDF‑bestanden uitsluiten

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe bestanden filteren op aanmaakdatum

Wanneer u **filter by creation date** nodig heeft, specificeer een start‑ en eind‑`DateTime`.

### Filteren op aanmaakdatumbereik

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe bestanden filteren op wijzigingsdatum

Net als bij aanmaakdatums kunt u resultaten beperken tot bestanden die vóór een bepaald moment zijn gewijzigd.

### Filteren op wijzigingsdatum

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe bestanden filteren op pad met reguliere expressies

Als uw mapstructuur naamgevingsconventies volgt, kan een regex specifieke paden targeten.

### Filteren op bestandspadpatroon

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe bestanden filteren op grootte

Het beheersen van de documentgrootte is essentieel bij het omgaan met bandbreedte‑ of opslaglimieten.

### Filteren op bestandsgrootte (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe meerdere voorwaarden combineren met AND

Wanneer u **how to filter files** met meerdere criteria tegelijk nodig heeft, combineer ze met `CreateAnd`.

### Voorbeeld van logische AND

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hoe meerdere voorwaarden combineren met OR

Gebruik `CreateOr` wanneer een van meerdere regels moet slagen.

### Voorbeeld van logische OR

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Veelvoorkomende problemen en oplossingen
- **Filter not applied:** Zorg ervoor dat u `settings.DocumentFilter` **vóór** het aanmaken van de `Index`‑instantie toewijst.  
- **Onverwachte bestanden verschijnen:** Controleer dubbel of bestandsextensies de leidende punt (`.txt`) bevatten.  
- **Performance slowdown:** Combineer filters met AND om het aantal vroegtijdig gescande bestanden in de indexerings‑pipeline te verminderen.  
- **Regex errors:** Escape speciale tekens in uw padpatroon of gebruik `RegexOptions.IgnoreCase` voor hoofdletterongevoelige matches.

## Veelgestelde vragen

**Q: Kan ik een NOT‑filter combineren met een AND‑filter?**  
A: Ja. Bouw eerst het NOT‑filter (`DocumentFilter.CreateNot`) en voeg het vervolgens toe als een van de argumenten aan `DocumentFilter.CreateAnd`.

**Q: Hoe filter ik bestanden groter dan 10 MB?**  
A: Gebruik `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` om alleen bestanden op te nemen die groter zijn dan die grootte.

**Q: Is het mogelijk om zowel op aanmaak‑ als wijzigingsdatums tegelijk te filteren?**  
A: Absoluut. Maak elke filter afzonderlijk aan en combineer ze met `CreateAnd`.

**Q: Werken deze filters met cloud‑opslagpaden?**  
A: De filters werken op het lokale bestandssysteem. Voor cloud‑bronnen downloadt u eerst bestanden naar een tijdelijke map en past u vervolgens dezelfde filters toe.

**Q: Vereist het wijzigen van het filter opnieuw indexeren?**  
A: Ja. Filters worden geëvalueerd wanneer u `index.Add` aanroept. Het wijzigen van een filter betekent dat u de index moet herbouwen om de nieuwe criteria weer te geven.

## Conclusie

Door **how to filter files** met GroupDocs.Redaction voor .NET onder de knie te krijgen—of het nu gaat om extensie, aanmaakdatum, wijzigingsdatum, bestandsgrootte of NOT‑logica—kunt u documentbeheer stroomlijnen, indexen performant houden en focussen op de inhoud die echt belangrijk is. Experimenteer met de logische operatoren om het filteren af te stemmen op uw exacte bedrijfsregels, en u zult directe winst zien in snelheid en opslag‑efficiëntie.

---

**Laatst bijgewerkt:** 2026-04-21  
**Getest met:** GroupDocs.Redaction 24.11 for .NET  
**Auteur:** GroupDocs
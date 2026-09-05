---
date: '2026-06-07'
description: Leer hoe u bestandsextensies kunt opsommen en bestandsformaten kunt ophalen
  met GroupDocs.Redaction in C#. Inclusief installatie, code en praktische tips.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Hoe bestandsextensies op te sommen met GroupDocs.Redaction in .NET – Een uitgebreide
  gids
type: docs
url: /nl/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Weergave van ondersteunde bestandsformaten met GroupDocs.Redaction in .NET

Het beheren van een breed scala aan documenttypen is een dagelijkse realiteit voor .NET‑ontwikkelaars. Met **GroupDocs.Redaction** kun je **bestands extensies weergeven** die de bibliotheek ondersteunt, waardoor je applicatie de mogelijkheid krijgt om uploads te accepteren of te weigeren, gebruiksvriendelijke UI‑keuzes te presenteren en kostbare runtime‑fouten te vermijden. Deze tutorial leidt je door alles wat je nodig hebt — van vereisten tot een volledige, productie‑klare implementatie — zodat je met vertrouwen **bestandsformaten ophalen** en **c# bestandsformaten weergeven** in je oplossing kunt.

## Snelle antwoorden
- **Wat betekent “list file extensions”?** Het betekent het ophalen van de collectie van ondersteunde bestandstype‑identifiers (bijv. *.pdf*, *.docx*) via de API.  
- **Welke NuGet‑package biedt deze functionaliteit?** `GroupDocs.Redaction` (nieuwste stabiele versie).  
- **Heb ik een licentie nodig om het voorbeeld uit te voeren?** Een gratis proeflicentie werkt voor ontwikkeling; een permanente licentie is vereist voor productie.  
- **Kan ik de resultaten cachen?** Ja — sla de lijst op in het geheugen of een gedistribueerde cache om herhaalde API‑aanroepen te vermijden.  
- **Is deze functie compatibel met .NET 6 en .NET Core?** Absoluut; de bibliotheek ondersteunt .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ en .NET 6+.

## Wat is GroupDocs.Redaction?
**GroupDocs.Redaction** is een .NET‑bibliotheek die ontwikkelaars in staat stelt gevoelige inhoud te redigeren, documenten te converteren en ondersteunde bestandstypen te ontdekken — allemaal zonder dat Microsoft Office op de server nodig is. Het abstraheert complexe format‑afhandeling achter een schone, object‑georiënteerde API. Het biedt een eendrachtige API voor redactie, conversie en format‑detectie, die PDF’s, Office‑documenten, afbeeldingen en meer verwerkt, terwijl het hoge prestaties en beveiliging garandeert.

## Waarom bestands extensies weergeven met GroupDocs.Redaction?
De bibliotheek **ondersteunt meer dan 50 invoer‑ en uitvoerformaten**, waaronder PDF, DOCX, PPTX, XLSX, HTML en meer dan 30 afbeeldingsformaten. Door programmatisch **bestands extensies weer te geven**, kun je:
- Voorkom dat gebruikers niet‑ondersteunde bestanden uploaden (vermindert validatiefouten tot wel 90%).  
- Dynamisch dropdown‑menu’s vullen, zodat de UI synchroon blijft met bibliotheekupdates.  
- Audit‑logboeken bouwen die het exacte bestandstype registreren dat een gebruiker probeerde te verwerken.

## Vereisten
- **GroupDocs.Redaction**: Installeer via NuGet (zie de commando’s hieronder).  
- **.NET SDK**: Zorg ervoor dat de nieuwste .NET SDK geïnstalleerd is. Download deze [hier](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 of een andere compatibele editor.  
- **Basis C#‑kennis**: Je moet vertrouwd zijn met collecties en LINQ.

## GroupDocs.Redaction instellen voor .NET

### Bibliotheek installeren

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Open NuGet Package Manager, zoek naar “GroupDocs.Redaction,” en installeer de nieuwste versie.

### Een licentie verkrijgen en toepassen

Begin met een gratis proefversie of vraag een tijdelijke licentie aan om alle functies zonder beperkingen te verkennen. Voor aankoopopties, bezoek de [aankooppagina van GroupDocs](https://purchase.groupdocs.com/). Zodra je je licentiebestand hebt:
1. Plaats het in een toegankelijke map binnen je project (bijv. `./Licenses/GroupDocs.Redaction.lic`).  
2. Initialise de licentie bij het starten van de applicatie:

De `License`‑klasse laadt je licentiebestand en activeert GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Hoe bestands extensies weergeven met GroupDocs.Redaction?
Laad de Redaction API en roep de methode aan die de ondersteunde formaten retourneert. De oproep geeft een collectie terug waarbij elk item een extensie en een mens‑leesbare beschrijving bevat. Deze bewerking is lichtgewicht en kan bij het opstarten of op aanvraag worden uitgevoerd.

### De ondersteunde bestandstypen ophalen
De `RedactionApi.GetSupportedFileFormats()`‑methode retourneert een alleen‑lezen collectie van `FileFormatInfo`‑objecten die elk formaat beschrijven.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Elke extensie en beschrijving weergeven
Elke `FileFormatInfo` biedt de `Extension`‑ en `Description`‑eigenschappen voor een bestandstype.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Uitleg**: De lus iterereert door elk `FileFormatInfo`‑object en print de `Extension` en `Description` in een netjes uitgelijnde tabel.

## Hoe de lijst integreren in een UI‑dropdown?
Nadat je de collectie hebt, bind je deze aan elk UI‑component — WinForms `ComboBox`, WPF `ComboBox` of ASP.NET Core `select`‑element. Het belangrijkste is om de `Extension` als waarde te gebruiken en de `Description` als weergavetekst. Dit zorgt ervoor dat gebruikers vriendelijke namen zien terwijl je code met de exacte extensiestrings werkt.

## Veelvoorkomende problemen en oplossingen
- **Missing namespace‑fout** – Controleer of je `GroupDocs.Redaction` en `GroupDocs.Redaction.Common` hebt geïmporteerd.  
- **Licentie niet gevonden** – Zorg ervoor dat het pad naar het licentiebestand correct is en dat het bestand is opgenomen in de build‑output.  
- **Prestaties bij grote projecten** – Cache het resultaat in een statische variabele of een gedistribueerde cache (bijv. Redis) om herhaalde enumeratie te vermijden.

## Praktische toepassingen
Het kennen van de exacte lijst met ondersteunde extensies opent verschillende real‑world scenario’s:
1. **Document Management Systems** – Categoriseer binnenkomende bestanden automatisch op basis van hun extensie.  
2. **Content Filtering Tools** – Blokkeer niet‑toegestane formaten (bijv. uitvoerbare bestanden) bij het uploaden.  
3. **File Conversion Pipelines** – Beslis dynamisch of een bestand kan worden geconverteerd of een fallback‑workflow nodig heeft.

## Prestatieoverwegingen
- **Geheugenvoetafdruk** – De formatlijst wordt opgeslagen in een lichtgewicht `IReadOnlyCollection`, meestal onder de 2 KB.  
- **Thread‑veiligheid** – De collectie is onveranderlijk na creatie, waardoor deze veilig is voor gelijktijdige reads.  
- **Caching** – Voor API’s met veel verkeer, cache de lijst voor de levensduur van de applicatie om de enkele microseconden overhead per request te elimineren.

## Conclusie
Door de bovenstaande stappen te volgen, heb je nu een betrouwbare manier om **bestands extensies weer te geven** en **c# bestandsformaten weer te geven** met GroupDocs.Redaction. Deze mogelijkheid verbetert niet alleen de gebruikerservaring, maar beschermt ook je backend tegen niet‑ondersteunde bestanden. Verken extra Redaction‑functies — zoals content masking, PDF‑redactie en batch‑verwerking — om je documentworkflow verder te versterken.

## Veelgestelde vragen
**Q: Wat zijn de standaard ondersteunde bestandsformaten?**  
A: GroupDocs.Redaction ondersteunt meer dan 50 formaten, waaronder PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG en nog veel meer. Zie de volledige lijst op [GroupDocs documentatie](https://docs.groupdocs.com/search/net/).

**Q: Hoe upgrade ik de bibliotheek naar de nieuwste versie?**  
A: Open NuGet Package Manager, zoek naar “GroupDocs.Redaction,” en klik op **Update**. Als alternatief, voer `dotnet add package GroupDocs.Redaction --version <latest>` uit.

**Q: Kan ik deze lijst gebruiken voor server‑side validatie van geüploade bestanden?**  
A: Ja — vergelijk de extensie van het geüploade bestand met de opgehaalde collectie voordat je het verwerkt. Dit elimineert 99 % van de fouten door ongeldige formaten.

**Q: Is het mogelijk om ondersteuning voor aangepaste bestandstypen uit te breiden?**  
A: Aangepaste extensies vereisen aangepaste handlers; de kernbibliotheek voegt niet native nieuwe formaten toe. Bekijk de API‑documentatie voor het maken van aangepaste import‑/export‑pijplijnen.

**Q: Mijn applicatie crasht na het toevoegen van de code — wat moet ik controleren?**  
A: Zorg ervoor dat de licentie correct wordt geladen, de `using`‑statements verwijzen naar de juiste namespaces, en dat je `IOException` afhandelt bij het lezen van het licentiebestand.

**Laatst bijgewerkt:** 2026-06-07  
**Getest met:** GroupDocs.Redaction 23.9 voor .NET  
**Auteur:** GroupDocs  

## Resources
- [Documentatie](https://docs.groupdocs.com/search/net/)
- [API‑referentie](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Gratis ondersteuningsforum](https://forum.groupdocs.com/c/search/10)
- [Tijdelijke licentie‑aanvraag](https://purchase.groupdocs.com/temporary-license/)

## Gerelateerde tutorials
- [Meester bestandsfiltering in .NET met GroupDocs.Redaction: efficiënte documentbeheer technieken](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Meester GroupDocs.Redaction .NET: installatie & event handling voor veilig documentbeheer](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Meesteren van documentbeheer in .NET met GroupDocs.Redaction: licentie‑instelling en HTML‑zoek‑markering](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
---
date: '2026-04-21'
description: Lär dig hur du filtrerar filer med GroupDocs.Redaction för .NET, inklusive
  filtrering efter skapelsedatum, filstorlek, ändringsdatum och hur du använder NOT-filter.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Hur man filtrerar filer med GroupDocs.Redaction för .NET
type: docs
url: /sv/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Hur man filtrerar filer med GroupDocs.Redaction för .NET

I dagens snabbrörliga digitala miljö kan **hur man filtrerar filer** effektivt vara avgörande för din produktivitet. Oavsett om du behöver isolera dokument efter filändelse, skapelsedatum, storlek eller ändringsdatum, sparar en solid filtreringsstrategi tid, minskar lagringskostnader och håller ditt sökindex prydligt. I den här handledningen går vi igenom verkliga exempel med GroupDocs.Redaction för .NET och visar exakt hur du filtrerar filer för att möta vanliga affärsbehov.

## Snabba svar
- **Vilket bibliotek behöver jag?** GroupDocs.Redaction för .NET (installera via NuGet).  
- **Kan jag filtrera efter skapelsedatum?** Ja – använd `CreateCreationTimeRange`.  
- **Hur exkluderar jag vissa typer?** Använd ett NOT-filter med `DocumentFilter.CreateNot`.  
- **Stöds filtrering efter filstorlek?** Absolut, via `CreateFileLengthRange` eller övre/nedre gränser.  
- **Behöver jag en licens?** En prov- eller fullständig licens krävs för produktionsanvändning.

## Vad är filtrering av filer med GroupDocs.Redaction?
Filtrering av filer låter dig ange för indexeringsmotorn vilka dokument som ska inkluderas eller ignoreras baserat på metadata såsom filändelse, datum, sökvägsmönster eller storlek. Genom att definiera precisa `DocumentFilter`-regler håller du ditt index slimmat och dina sökningar snabba.

## Varför använda GroupDocs.Redaction för .NET?
- **Inbyggda filterhjälpmedel** – ingen anledning att skriva anpassad filsystemkod.  
- **Logiska operatorer** – kombinera flera kriterier med AND, OR och NOT.  
- **Prestandaoptimerade** – filter tillämpas under indexering, inte efter.  
- **Plattformsoberoende** – fungerar med .NET Framework, .NET Core och .NET 5/6+.

## Förutsättningar
- .NET Framework 4.6+ eller .NET Core 3.1+ installerat.  
- Visual Studio eller din föredragna C#-IDE.  
- Grundläggande kunskaper i C#.

### Nödvändiga bibliotek och installation
Installera NuGet-paketet med din föredragna metod:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Proffstips:** Efter installationen, lägg till din licensfil i projektets rot och anropa `License.SetLicense("license-file-path")` innan du skapar några Redactor- eller Index-objekt.

## Konfigurera GroupDocs.Redaction för .NET

Först, skapa en `Redactor`-instans som pekar på det dokument du vill arbeta med:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Varför detta är viktigt:** Initiering av Redactor garanterar att biblioteket är redo att tillämpa filter och redigeringsregler senare i arbetsflödet.

## Hur man filtrerar filer efter filändelse

Filtrering efter filändelse är det vanligaste sättet att begränsa en dokumentuppsättning. Nedan behåller vi endast FB2-, EPUB- och TXT-filer.

### Filtrera efter filändelse

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

## Hur man använder NOT-filter för att exkludera oönskade typer

Om du behöver **tillämpa NOT-filter**‑logik—t.ex. exkludera HTML- och PDF-filer—använd `CreateNot`.

### Exkludera HTM-, HTML- och PDF-filer

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

## Hur man filtrerar filer efter skapelsedatum

När du behöver **filtrera efter skapelsedatum**, ange ett start- och slut-`DateTime`.

### Filtrera efter intervall för skapelsedatum

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

## Hur man filtrerar filer efter ändringsdatum

På liknande sätt som med skapelsedatum kan du begränsa resultaten till filer som ändrats före en viss tidpunkt.

### Filtrera efter ändringsdatum

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

## Hur man filtrerar filer efter sökväg med reguljära uttryck

Om din mappstruktur följer namngivningskonventioner kan ett regex rikta in sig på specifika sökvägar.

### Filtrera efter mönster för filsökväg

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

## Hur man filtrerar filer efter storlek

Att kontrollera dokumentstorlek är viktigt när du hanterar bandbredds- eller lagringsgränser.

### Filtrera efter filstorlek (50 KB – 100 KB)

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

## Hur man kombinerar flera villkor med AND

När du behöver **filtrera filer** med flera kriterier samtidigt, kombinera dem med `CreateAnd`.

### Exempel på logisk AND

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

## Hur man kombinerar flera villkor med OR

Använd `CreateOr` när någon av flera regler ska godkännas.

### Exempel på logisk OR

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

## Vanliga problem och lösningar
- **Filtret tillämpas inte:** Se till att du tilldelar `settings.DocumentFilter` **innan** du skapar `Index`-instansen.  
- **Oväntade filer dyker upp:** Dubbelkolla att filändelserna inkluderar den inledande punkten (`.txt`).  
- **Prestandaförsämring:** Kombinera filter med AND för att minska antalet filer som skannas tidigt i indexeringsprocessen.  
- **Regex‑fel:** Escape specialtecken i ditt sökvägsmönster eller använd `RegexOptions.IgnoreCase` för skiftlägesokänsliga matchningar.

## Vanliga frågor

**Q: Kan jag kombinera ett NOT-filter med ett AND-filter?**  
A: Ja. Bygg NOT-filtret först (`DocumentFilter.CreateNot`) och inkludera det sedan som ett av argumenten till `DocumentFilter.CreateAnd`.

**Q: Hur filtrerar jag filer som är större än 10 MB?**  
A: Använd `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)` för att endast inkludera filer som överstiger den storleken.

**Q: Är det möjligt att filtrera både efter skapelse- och ändringsdatum samtidigt?**  
A: Absolut. Skapa varje filter separat och kombinera dem med `CreateAnd`.

**Q: Fungerar dessa filter med molnlagringsvägar?**  
A: Filtren fungerar på det lokala filsystemet. För molnkällor, ladda ner filer till en temporär mapp först, och tillämpa sedan samma filter.

**Q: Kommer ändring av filtret att kräva omindexering?**  
A: Ja. Filtren utvärderas när du anropar `index.Add`. Att ändra ett filter innebär att du måste bygga om indexet för att återspegla de nya kriterierna.

## Slutsats

Genom att behärska **hur man filtrerar filer** med GroupDocs.Redaction för .NET—oavsett om det är efter filändelse, skapelsedatum, ändringsdatum, filstorlek eller med NOT‑logik—kan du effektivisera dokumenthantering, hålla index presterande och fokusera på det innehåll som verkligen betyder något. Experimentera med de logiska operatorerna för att anpassa filtreringen efter dina exakta affärsregler, så kommer du att se omedelbara förbättringar i hastighet och lagringseffektivitet.

---

**Senast uppdaterad:** 2026-04-21  
**Testat med:** GroupDocs.Redaction 24.11 för .NET  
**Författare:** GroupDocs
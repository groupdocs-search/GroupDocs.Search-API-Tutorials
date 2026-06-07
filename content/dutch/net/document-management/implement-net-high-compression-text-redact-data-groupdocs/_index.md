---
date: '2026-06-07'
description: Leer hoe u hoge compressie .net implementeert voor tekstopslag en vertrouwelijke
  gegevens kunt redigeren met behulp van GroupDocs.Search en GroupDocs.Redaction in
  .NET-toepassingen.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implementeer Hoge Compressie .NET met GroupDocs: Tekst- en Redactiegids'
type: docs
url: /nl/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementeer Hoge Compressie .NET met GroupDocs: Tekst & Redactie Gids

In moderne .NET‑oplossingen is **implement high compression .net** essentieel wanneer u enorme tekstcollecties moet opslaan zonder de schijfruimte te overbelasten. Tegelijkertijd vereist het beschermen van gevoelige informatie—zoals persoonlijke identificatoren of financiële cijfers—betrouwbare redactie. Deze tutorial toont u stap‑voor‑stap hoe u hoog‑gecomprimeerde tekstopslag configureert met **GroupDocs.Search** en hoe u vertrouwelijke gegevens veilig redacteert met **GroupDocs.Redaction**. Aan het einde kunt u geïndexeerde tekst tot 90 % comprimeren en privé‑inhoud verwijderen uit PDF‑, Word‑bestanden en vele andere formaten.

## Snelle Antwoorden
- **Welke bibliotheek biedt hoge‑compressie indexering?** GroupDocs.Search voor .NET.  
- **Welke tool redacteert gevoelige gegevens?** GroupDocs.Redaction voor .NET.  
- **Kan ik documenten automatisch aan de index toevoegen?** Ja—gebruik de `AddDocument` API binnen een map‑scanlus.  
- **Is compressie verliesvrij voor zoeken?** Ja, de tekst blijft volledig doorzoekbaar na compressie.  
- **Heb ik een licentie nodig voor productie?** Een permanente GroupDocs‑licentie is vereist voor commercieel gebruik.

## Wat betekent “implement high compression .net”?
Implement high compression .net betekent het configureren van de GroupDocs.Search indexeringsengine om geëxtraheerde tekstinhoud in een gecomprimeerde vorm op te slaan. Dit verkleint de indexgrootte op schijf drastisch terwijl de tekst volledig doorzoekbaar blijft. De compressie is verliesvrij, zodat de relevantie van queries en het extraheren van fragmenten precies werkt als bij een ongecomprimeerde index.

## Waarom GroupDocs gebruiken voor compressie en redactie?
GroupDocs.Search ondersteunt meer dan vijftig invoerformaten en kan geïndexeerde tekst tot wel negentig procent comprimeren, waardoor grote documentcollecties slechts een fractie van hun oorspronkelijke grootte innemen. GroupDocs.Redaction vult dit aan door permanent gevoelige informatie in meer dan dertig bestandstypen te wissen of te maskeren, waardoor u aan strenge nalevingsvoorschriften zoals GDPR en HIPAA kunt voldoen zonder extra tools.

## Voorvereisten
- **Ontwikkelomgeving:** Visual Studio 2022 of later, .NET 6+ (of .NET Framework 4.7.2).  
- **Bibliotheken:** NuGet‑pakketten `GroupDocs.Search` en `GroupDocs.Redaction`.  
- **Machtigingen:** Lees‑/schrijftoegang tot de mappen die bron‑documenten en de index‑uitvoerlokatie bevatten.  
- **Basiskennis:** C#‑syntaxis, bestands‑I/O en vertrouwdheid met .NET‑projectstructuur.

## Hoe implementeer je hoge compressie .NET met GroupDocs?
Om hoge compressie .NET met GroupDocs te implementeren, maak eerst een `TextStorageSettings`‑instantie aan en stel de `CompressionLevel` in op `High`. Instantieer vervolgens een `Index`‑object, waarbij je de instellingen en de map doorgeeft waar de index wordt opgeslagen. Nadat de index klaar is, voeg je documenten toe met `AddDocument`, en voer je uiteindelijk zoekopdrachten uit met de `Search`‑methode, terwijl de engine transparant compressie en decompressie afhandelt.

### Stap 1: Installeer de vereiste NuGet‑pakketten
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Zoek naar “GroupDocs.Search” en klik op **Install**.  

### Stap 2: Installeer GroupDocs.Redaction (voor gegevensredactie)
- Open de **NuGet Package Manager**.  
- Zoek naar **GroupDocs.Redaction** en installeer de nieuwste stabiele versie.  

### Stap 3: Verkrijg en pas een licentie toe
- **Gratis proefversie:** Registreer op het GroupDocs‑portaal voor een 30‑daagse proef‑sleutel.  
- **Tijdelijke licentie:** Vraag een tijdelijke sleutel aan voor ontwikkelomgevingen.  
- **Permanente licentie:** Koop een productielicentie om evaluatiebeperkingen te verwijderen.

### Stap 4: Basisinitialisatie van beide bibliotheken
De `Search`‑ en `Redaction`‑engines delen een gemeenschappelijk licentiemodel. Initialiseert ze bij het opstarten van de applicatie:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Functie 1: Instellingen voor Hoge Compressie Tekstopslag

### Configuratie van Indexering Instellen
`TextStorageSettings` is de klasse die GroupDocs.Search vertelt hoe de geëxtraheerde tekst moet worden bewaard. Het inschakelen van hoge compressie verkleint de indexgrootte tot **10×** zonder de zoek‑snelheid te beïnvloeden.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Uitleg:**  
- `CompressionLevel.High` activeert een ZSTD‑gebaseerd algoritme dat tekstblokken efficiënt comprimeert.  
- `UseMemoryCache = false` dwingt de engine om gegevens van schijf te streamen, wat ideaal is voor grootschalige implementaties.

### Het Aanmaken en Beheren van de Index
Het `Index`‑object vertegenwoordigt de doorzoekbare repository op schijf. Je geeft de map op waar de indexbestanden worden opgeslagen en geeft de hierboven gedefinieerde compressie‑instellingen door.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Uitleg:**  
- `indexFolder` bepaalt waar de gecomprimeerde indexbestanden zich bevinden.  
- `settings` injecteert de hoge‑compressieconfiguratie, waardoor elk toegevoegd document hiervan profiteert.

## Functie 2: Documenten aan Index Toevoegen

### Voeg Documenten toe aan je Index
`AddDocument` voegt een enkel bestand toe aan de index, extraheert de tekst, comprimeert deze volgens de geconfigureerde instellingen en slaat het resultaat op. GroupDocs.Search kan bestanden uit een mapstructuur inlezen. De volgende lus doorloopt `documentsFolder`, voegt elk bestand toe en logt de voortgang.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Uitleg:**  
- `AddDocument` parseert het bestand, extraheert doorzoekbare tekst, comprimeert deze volgens `TextStorageSettings` en slaat het op in de index.  
- Deze aanpak werkt voor **PDF, DOCX, TXT, HTML**, en meer dan **30** andere formaten.

## Functie 3: Een Zoekopdracht Uitvoeren

### Voer een Zoekopdracht uit
`Search` voert een query uit op de gecomprimeerde index en retourneert een collectie van overeenkomende `DocumentResult`‑objecten met relevantiescores en gemarkeerde fragmenten. Zodra de index is gevuld, kun je snelle queries uitvoeren. De `Search`‑methode retourneert een collectie van `DocumentResult`‑objecten die bestands‑paden en gemarkeerde fragmenten bevatten.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Uitleg:**  
- De zoekengine scant de gecomprimeerde tekst direct, waardoor de query‑latentie laag blijft, zelfs voor indexen die **miljoenen pagina's** bevatten.  
- `Score` geeft de relevantie aan; hogere waarden betekenen een betere overeenkomst.

## Hoe vertrouwelijke gegevens te redigeren met GroupDocs.Redaction?
Het redigeren van vertrouwelijke gegevens met GroupDocs.Redaction begint met het aanmaken van een `Redactor`‑instantie voor het doelbestand. Definieer één of meer `SearchPattern`‑objecten die de te verwijderen tekst beschrijven, zoals reguliere expressies voor burgerservicenummers. Pas elk patroon toe met `Redact`, waarbij je een `RedactionType` zoals `BlackOut` opgeeft, en sla het resultaat op als een nieuw document, zodat het origineel onaangetast blijft.

`Redactor` is de primaire klasse in GroupDocs.Redaction die wordt gebruikt om een document te laden en redactie‑bewerkingen uit te voeren.  
`SearchPattern` definieert een reguliere expressie die de te redigeren tekst identificeert.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Uitleg:**  
- `SearchPattern` gebruikt een reguliere expressie om burgerservicenummers te vinden.  
- `RedactionType.BlackOut` vervangt de gevonden tekst door een volledig zwart rechthoek, waardoor de gegevens niet kunnen worden hersteld.

## Praktische Toepassingen
1. **Juridisch Documentbeheer:** Automatisch enorme dossiers comprimeren en klant‑identificatoren redigeren vóór archivering.  
2. **Gezondheidsdossiers:** Jaren aan patiëntnotities opslaan in een gecomprimeerde index en PHI (Protected Health Information) verwijderen vóór het delen met onderzoeks‑partners.  
3. **Financiële Rapportage:** Kwartaalrapporten beveiligen door rekeningnummers te redigeren, terwijl de doorzoekbare tekst behouden blijft voor audit‑queries.

## Prestatieoverwegingen
- **Impact van compressie:** Hoge compressie verkleint de indexgrootte tot **90 %**, wat SSD‑slijtage vermindert en back‑up‑operaties versnelt.  
- **Geheugengebruik:** Schakel in‑memory caching uit voor zeer grote indexen om de proces‑voetafdruk onder **500 MB** te houden.  
- **I/O‑optimalisatie:** Voeg documenten in batches van 100 toe om schijf‑thrashing te minimaliseren.  
- **Async verwerking:** Wikkel `AddDocument`‑aanroepen in `Task.Run` om UI‑threads responsief te houden in desktop‑apps.

## Veelvoorkomende Valkuilen & Probleemoplossing
- **Onjuiste bestandspaden:** Controleer of `documentsFolder` en `indexFolder` absolute paden zijn en of de applicatie lees‑/schrijftoegang heeft.  
- **Licentiefouten:** Zorg ervoor dat de `.lic`‑bestanden worden gedeployed naast het uitvoerbare bestand of ingebed als resources.  
- **Zoekopdracht geeft geen resultaten:** Controleer of het compressieniveau van `TextStorageSettings` overeenkomt met dat tijdens het indexeren; niet‑overeenkomende instellingen kunnen deserialisatiefouten veroorzaken.  

## Veelgestelde Vragen

**V: Kan ik documenten aan de index toevoegen na de initiële bouw?**  
A: Ja—roep simpelweg `index.AddDocument` aan voor nieuwe bestanden; de engine werkt de gecomprimeerde index incrementeel bij.

**V: Verandert redactie het originele bestand?**  
A: Nee—het originele bestand blijft onaangetast; de geredigeerde versie wordt opgeslagen als een nieuw bestand, waardoor de documentintegriteit behouden blijft.

**V: Welke formaten ondersteunt GroupDocs.Redaction?**  
A: Meer dan **30** formaten, waaronder PDF, DOCX, PPTX, XLSX, afbeeldingen (PNG, JPEG) en platte tekst.

**V: Hoe beïnvloedt hoge compressie de zoekrelevantie?**  
A: Niet. De compressie is verliesvrij voor tekst, dus relevantiescores zijn identiek aan een ongecomprimeerde index.

**V: Is er een limiet aan de grootte van documenten die ik kan indexeren?**  
A: GroupDocs.Search kan multi‑gigabyte bestanden verwerken door content te streamen; zorg echter voor voldoende schijfruimte voor de gecomprimeerde index (ongeveer 10 % van de originele grootte).

## Bronnen
- [Documentatie](https://docs.groupdocs.com/search/net/)
- [API‑referentie](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction voor .NET](https://releases.groupdocs.com/search/net/)
- [Gratis Supportforum](https://forum.groupdocs.com/c/search/10)
- [Tijdelijke Licentie‑acquisitie](https://purchase.groupdocs.com/temporary-license/)

---

**Laatst bijgewerkt:** 2026-06-07  
**Getest met:** GroupDocs.Search 23.12 en GroupDocs.Redaction 23.12 voor .NET  
**Auteur:** GroupDocs

## Gerelateerde Tutorials

- [Implementatie van GroupDocs.Search en Redaction in .NET voor Documentbeheer](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Hoe GroupDocs.Redaction voor .NET te optimaliseren: Gids voor efficiënte index‑ en spellingbeheer](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Beheers GroupDocs Redaction en Search in .NET: Efficiënt Documentbeheer en Veilige Zoeken](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
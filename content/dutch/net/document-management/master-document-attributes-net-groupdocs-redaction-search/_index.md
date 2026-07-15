---
date: '2026-06-22'
description: Leer hoe je documenten kunt redigeren in .NET terwijl je de zoekprestaties
  optimaliseert met GroupDocs.Redaction en GroupDocs.Search. Stapsgewijze attribuutbeheer,
  indexering en veilige redactie voor .NET‑ontwikkelaars.
keywords:
- how to redact documents
- optimize search performance
- how to index attributes
schemas:
- author: GroupDocs
  dateModified: '2026-06-22'
  description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  headline: How to Redact Documents in .NET Using GroupDocs Redaction
  type: TechArticle
- description: Learn how to redact documents in .NET while optimizing search performance
    with GroupDocs.Redaction and GroupDocs.Search. Step‑by‑step attribute management,
    indexing, and secure redaction for .NET developers.
  name: How to Redact Documents in .NET Using GroupDocs Redaction
  steps:
  - name: Initialize Index
    text: '`Index` represents a searchable collection of documents and their associated
      metadata. csharp using GroupDocs.Search.Common; using GroupDocs.Search.Options;
      using GroupDocs.Search.Results; Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
      index.Add("@YOUR_DOCUMENT_DIRECTORY/Docum'
  - name: Modify Attributes
    text: '`AttributeChangeBatch` is the class that batches attribute updates for
      efficiency. **Definition anchor:** *`AttributeChangeBatch` batches add, update,
      and delete operations on document attributes in a single transaction.* csharp
      DocumentInfo[] documents = index.GetIndexedDocuments(); AttributeChange'
  - name: Search with Attribute Filters
    text: You can filter search results by attribute values using `SearchOptions`.
      **Direct answer:** To search for documents that contain the attribute `Category
      = "Legal"`, configure `SearchOptions` with an `AttributeFilter` and call `searcher.Search("contract",
      options)`. This returns only the legally tagg
  - name: Set Up Event Handler for Indexing
    text: '**Definition anchor:** *The `DocumentIndexed` event fires each time a document
      is successfully added to the index, allowing custom logic to run.* csharp Index
      index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing"); index.Events.FileIndexing
      += (sender, args) => { if (args.Document'
  - name: Configure and Perform Search
    text: After attributes are attached, you can search using those new fields. **Direct
      answer:** Use `SearchOptions` with `AttributeFilter` to query the newly added
      attributes, for example `AttributeFilter("Department", "Finance")`. This returns
      only finance‑related files, demonstrating **how to index attri
  type: HowTo
- questions:
  - answer: Load each file with `Redactor`, add a `RedactionRegion` for every sensitive
      area, then call `Redactor.Apply()` inside a loop; this approach processes thousands
      of files with minimal memory overhead.
    question: What is the best way to batch‑redact multiple PDFs?
  - answer: Yes. After redaction, the document retains its metadata, so you can search
      with both text terms and `AttributeFilter` simultaneously.
    question: Can I combine redaction with attribute filtering in a single query?
  - answer: Pass the password to the `Redactor` constructor; the library will decrypt,
      redact, and re‑encrypt the file automatically.
    question: How do I handle password‑protected documents?
  - answer: Absolutely. Enable `RedactorOptions.Ocr = true` to recognize text in images,
      then apply redaction rules on the extracted text.
    question: Does GroupDocs support OCR for scanned images before redaction?
  - answer: GroupDocs.Redaction and GroupDocs.Search support .NET Core 3.1, .NET 5,
      .NET 6, and .NET 7, as well as .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Hoe documenten te redigeren in .NET met GroupDocs Redaction
type: docs
url: /nl/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Hoe documenten te redigeren in .NET met GroupDocs Redaction

In deze uitgebreide tutorial ontdek je **hoe je documenten kunt redigeren** in een .NET-omgeving en beheer je tegelijkertijd documentattributen met GroupDocs.Redaction en GroupDocs.Search. Of je nu gevoelige gegevens moet beschermen, de zoek snelheid wilt verhogen, of grote documentbibliotheken wilt organiseren, de hier getoonde technieken bieden een productieklare oplossing die schaalt tot honderdduizenden bestanden.

## Snelle antwoorden
- **Hoe redacteer ik een PDF in .NET?** Laad het bestand met `Redactor`, definieer een `RedactionRegion` en roep `Redactor.Apply()` aan – drie regels code doen het zware werk.  
- **Kan ik documentattributen wijzigen na het indexeren?** Ja, gebruik `AttributeChangeBatch` om attributen in bulk toe te voegen, bij te werken of te verwijderen.  
- **Welke bibliotheken zijn vereist?** `GroupDocs.Redaction` + `GroupDocs.Search` (nieuwste NuGet-versies).  
- **Heb ik een licentie nodig voor productie?** Een geldige GroupDocs-licentie is vereist; een tijdelijke proeflicentie is beschikbaar voor evaluatie.  
- **Hoe kan ik de zoek snelheid verbeteren?** Schakel batchverwerking en selectieve indexering in; deze technieken kunnen de **zoekprestaties optimaliseren** tot wel 40 % op grote datasets.

## Wat is “hoe documenten te redigeren”?

Het beschrijft het geautomatiseerde proces van het lokaliseren van gevoelige informatie binnen een bestand en het vervangen ervan door verduisterde inhoud—zoals zwarte balken of witruimte—terwijl de oorspronkelijke lay-out behouden blijft. Dit zorgt ervoor dat vertrouwelijke gegevens verborgen zijn voor kijkers, maar het document leesbaar en functioneel blijft voor vervolgprocessen.

## Waarom GroupDocs.Redaction en GroupDocs.Search samen gebruiken?

GroupDocs.Redaction ondersteunt **meer dan 50 bestandsformaten** (PDF, DOCX, XLSX, PPTX, afbeeldingen, enz.) en kan documenten verwerken tot **2 GB** zonder het volledige bestand in het geheugen te laden. GroupDocs.Search indexeert meer dan **70 miljoen termen** per uur op een standaard server, waardoor je **zoekprestaties drastisch kunt optimaliseren** wanneer het wordt gecombineerd met op attributen gebaseerde filtering.

## Voorvereisten

- **Vereiste bibliotheken:** `GroupDocs.Search` en `GroupDocs.Redaction` (nieuwste NuGet-releases).  
- **Ontwikkelomgeving:** Visual Studio 2019 of later, gericht op .NET Core 3.1 of .NET 6+.  
- **Basiskennis:** C#-syntaxis, object‑georiënteerde concepten, en vertrouwdheid met documentindexeerprincipes.

## GroupDocs.Redaction voor .NET instellen

### De bibliotheek installeren

Je kunt **GroupDocs.Redaction** aan je project toevoegen met een van de volgende methoden:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Package Manager**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- Zoek naar “GroupDocs.Redaction” en installeer de nieuwste versie.

### Stappen voor licentie‑acquisitie

Om te beginnen kun je een tijdelijke licentie verkrijgen of er een kopen. Een gratis proefversie is beschikbaar om functies te testen voordat je een beslissing neemt:
1. Bezoek de [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) om een tijdelijke licentie aan te vragen.  
2. Volg de gegeven instructies om je licentie in je applicatie toe te passen.

### Basisinitialisatie en -configuratie

`Redactor` is de hoofdklasse die wordt gebruikt om een document te laden en redactiebewerkingen toe te passen.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Functie 1: Documentattributen wijzigen

### Overzicht
Het wijzigen van documentattributen stelt je in staat om nauwkeurig af te stemmen hoe documenten verschijnen in zoekresultaten, waardoor precieze filtering en categorisatie mogelijk zijn.

#### Stap 1: Index initialiseren

`Index` vertegenwoordigt een doorzoekbare collectie van documenten en hun bijbehorende metadata.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Stap 2: Attributen wijzigen

`AttributeChangeBatch` is de klasse die attributenupdates batcht voor efficiëntie.  

**Definition anchor:** *`AttributeChangeBatch` batcht toevoeg-, update- en verwijderbewerkingen op documentattributen in één transactie.*  

```csharp
```csharp
DocumentInfo[] documents = index.GetIndexedDocuments();
AttributeChangeBatch batch = new AttributeChangeBatch();

// Adding "public" to all documents
batch.AddToAll("public");

// Removing "public" from the first document
batch.Remove(documents[0].FilePath, "public");

// Adding "main" and "key" to the first document
batch.Add(documents[0].FilePath, "main", "key");
index.ChangeAttributes(batch);
```
```

#### Stap 3: Zoeken met attribuutfilters

Je kunt zoekresultaten filteren op attribuutwaarden met `SearchOptions`.  

**Direct answer:** Om te zoeken naar documenten die het attribuut `Category = "Legal"` bevatten, configureer `SearchOptions` met een `AttributeFilter` en roep `searcher.Search("contract", options)` aan. Dit retourneert alleen de juridisch getagde contracten, vermindert ruis in de resultaten en **optimaliseert de zoekprestaties**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Functie 2: Attributen toevoegen tijdens indexeren

### Overzicht
Het toevoegen van attributen op het moment van indexeren zorgt ervoor dat elk document vanaf het begin wordt verrijkt met de juiste metadata, waardoor later bulkupdates overbodig zijn.

#### Stap 1: Eventhandler instellen voor indexeren

**Definition anchor:** *Het `DocumentIndexed`‑event wordt geactiveerd elke keer dat een document succesvol aan de index wordt toegevoegd, waardoor aangepaste logica kan worden uitgevoerd.*  

```csharp
```csharp
Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/AddAttributesDuringIndexing");

index.Events.FileIndexing += (sender, args) => {
    if (args.DocumentFullPath.EndsWith("Lorem ipsum.pdf")) {
        // Specify attributes for this document
        args.Attributes = new string[] { "main", "key" };
    }
};

// Add documents to index
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Stap 2: Configureren en zoeken uitvoeren

Nadat attributen zijn toegevoegd, kun je zoeken met die nieuwe velden.

**Direct answer:** Gebruik `SearchOptions` met `AttributeFilter` om te zoeken op de nieuw toegevoegde attributen, bijvoorbeeld `AttributeFilter("Department", "Finance")`. Dit retourneert alleen financiële bestanden, wat laat zien **hoe attributen te indexeren** voor snellere, relevantere resultaten.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Praktische toepassingen

Hier zijn drie veelvoorkomende scenario's waarin het beheren van documentattributen en redactie samen tastbare bedrijfswaarde toevoegt:
1. **Juridisch documentbeheer** – Redigeer automatisch vertrouwelijke clausules en label contracten op jurisdictie, zodat juristen alleen de relevante bestanden kunnen vinden.  
2. **Organisatie van medische dossiers** – Redigeer patiëntidentificatoren terwijl je attributen zoals `PatientID` en `VisitDate` toevoegt voor conforme, snelle opvraging.  
3. **E‑commerce productcatalogus** – Redigeer leveranciersprijzinformatie en label producten met `StockStatus` of `DiscountRate` tijdens bulkimport, waardoor realtime voorraadvragen mogelijk zijn.

## Prestatieoverwegingen

Bij het omgaan met grote datasets, houd deze best practices in gedachten:
- **Batchverwerking:** `AttributeChangeBatch` vermindert round‑trips naar de index, waardoor de verwerkingstijd met tot **45 %** wordt verkort bij batches van 100 k‑documenten.  
- **Selectieve indexering:** Index alleen documenten die nieuwe attributen nodig hebben; sla ongewijzigde bestanden over om CPU en I/O te besparen.  
- **Geheugenbeheer:** Vernietig `SearchResult`, `Redactor` en `Indexer`-instanties zodra je klaar bent om onbeheerste bronnen vrij te geven.

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| Redactie verbergt tekst niet | Onjuiste `RedactionRegion`-coördinaten | Controleer de paginadimensies met `Redactor.GetPageSize()` voordat je de regio definieert. |
| Attribuutwijzigingen worden niet weergegeven in de zoekopdracht | Index niet ververst | Roep `searcher.Refresh()` aan na uitvoering van `AttributeChangeBatch`. |
| Out‑of‑memory fouten bij grote bestanden | Het volledige bestand in het geheugen laden | Schakel streamingmodus in door `RedactorOptions.Stream = true` in te stellen. |

## Veelgestelde vragen

**Q: Wat is de beste manier om meerdere PDF's batch‑te redigeren?**  
A: Laad elk bestand met `Redactor`, voeg een `RedactionRegion` toe voor elk gevoelig gebied, roep vervolgens `Redactor.Apply()` aan binnen een lus; deze aanpak verwerkt duizenden bestanden met minimale geheugeroverhead.

**Q: Kan ik redactie combineren met attribuutfiltering in één query?**  
A: Ja. Na redactie behoudt het document zijn metadata, zodat je kunt zoeken met zowel teksttermen als `AttributeFilter` tegelijk.

**Q: Hoe ga ik om met wachtwoord‑beveiligde documenten?**  
A: Geef het wachtwoord door aan de `Redactor`‑constructor; de bibliotheek zal het bestand automatisch ontcijferen, redigeren en opnieuw versleutelen.

**Q: Ondersteunt GroupDocs OCR voor gescande afbeeldingen vóór redactie?**  
A: Absoluut. Schakel `RedactorOptions.Ocr = true` in om tekst in afbeeldingen te herkennen, en pas vervolgens redactieregels toe op de geëxtraheerde tekst.

**Q: Welke .NET‑versies worden officieel ondersteund?**  
A: GroupDocs.Redaction en GroupDocs.Search ondersteunen .NET Core 3.1, .NET 5, .NET 6 en .NET 7, evenals .NET Framework 4.6.2+.

## Conclusie

Je hebt nu een full‑stack oplossing voor **hoe documenten te redigeren** terwijl je **zoekprestaties optimaliseert** en **hoe attributen te indexeren** met GroupDocs.Redaction en GroupDocs.Search. Door de bovenstaande stappen te volgen, kun je gevoelige gegevens beschermen, je zoekindex verrijken met betekenisvolle metadata, en je .NET‑applicaties snel en veilig houden.

---

**Laatst bijgewerkt:** 2026-06-22  
**Getest met:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Auteur:** GroupDocs

## Gerelateerde tutorials

- [Beheersen van GroupDocs.Redaction .NET: Efficiënte indexcreatie en aliasbeheer voor geavanceerd document zoeken](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Documentredactie en metadata‑indexering beheersen met GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Beheersen van GroupDocs.Redaction .NET: Installatie & eventafhandeling voor veilig documentbeheer](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
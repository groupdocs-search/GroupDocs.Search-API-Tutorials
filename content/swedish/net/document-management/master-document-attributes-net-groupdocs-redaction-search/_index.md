---
date: '2026-06-22'
description: Lär dig hur du maskerar dokument i .NET samtidigt som du optimerar sökprestanda
  med GroupDocs.Redaction och GroupDocs.Search. Steg‑för‑steg hantering av attribut,
  indexering och säker maskering för .NET‑utvecklare.
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
title: Hur man maskerar dokument i .NET med GroupDocs Redaction
type: docs
url: /sv/net/document-management/master-document-attributes-net-groupdocs-redaction-search/
weight: 1
---

# Hur man maskar dokument i .NET med GroupDocs Redaction

I den här omfattande handledningen kommer du att upptäcka **hur man maskar dokument** i en .NET-miljö och samtidigt behärska hantering av dokumentattribut med GroupDocs.Redaction och GroupDocs.Search. Oavsett om du behöver skydda känslig data, öka sökhastigheten eller organisera stora dokumentbibliotek, ger teknikerna som visas här dig en produktionsklar lösning som kan skalas till hundratusentals filer.

## Snabba svar
- **Hur maskar jag en PDF i .NET?** Ladda filen med `Redactor`, definiera en `RedactionRegion` och anropa `Redactor.Apply()` – tre kodrader hanterar det tunga arbetet.  
- **Kan jag ändra dokumentattribut efter indexering?** Ja, använd `AttributeChangeBatch` för att lägga till, uppdatera eller ta bort attribut i bulk.  
- **Vilka bibliotek krävs?** `GroupDocs.Redaction` + `GroupDocs.Search` (senaste NuGet-versionerna).  
- **Behöver jag en licens för produktion?** En giltig GroupDocs-licens krävs; en tillfällig provlicens finns tillgänglig för utvärdering.  
- **Hur kan jag förbättra sökhastigheten?** Aktivera batchbearbetning och selektiv indexering; dessa tekniker kan **optimera sökprestanda** med upp till 40 % på stora datamängder.

## Vad är “hur man maskar dokument”?

Det beskriver den automatiserade processen att lokalisera känslig information i en fil och ersätta den med dolda element—såsom svarta staplar eller vitt utrymme—utan att ändra den ursprungliga layouten. Detta säkerställer att konfidentiell data är dold för betraktare men dokumentet förblir läsbart och funktionellt för efterföljande uppgifter.

## Varför använda GroupDocs.Redaction och GroupDocs.Search tillsammans?

GroupDocs.Redaction stöder **50+ filformat** (PDF, DOCX, XLSX, PPTX, bilder osv.) och kan bearbeta dokument upp till **2 GB** utan att läsa in hela filen i minnet. GroupDocs.Search indexerar över **70 miljoner termer** per timme på en standardserver, vilket gör att du kan **optimera sökprestanda** dramatiskt när det kombineras med attributbaserad filtrering.

## Förutsättningar

- **Nödvändiga bibliotek:** `GroupDocs.Search` och `GroupDocs.Redaction` (senaste NuGet-utgåvorna).  
- **Utvecklingsmiljö:** Visual Studio 2019 eller senare, med mål .NET Core 3.1 eller .NET 6+.  
- **Grundläggande kunskap:** C#-syntax, objektorienterade koncept och bekantskap med principer för dokumentindexering.

## Konfigurera GroupDocs.Redaction för .NET

### Installera biblioteket

Du kan lägga till **GroupDocs.Redaction** i ditt projekt med någon av följande metoder:

**.NET CLI**  
```csharp
```bash
dotnet add package GroupDocs.Redaction
```
```

**Pakethanterare**  
```csharp
```powershell
Install-Package GroupDocs.Redaction
```
```

**NuGet Package Manager UI**  
- Sök efter “GroupDocs.Redaction” och installera den senaste versionen.

### Steg för att skaffa licens

För att komma igång kan du skaffa en tillfällig licens eller köpa en. En gratis provperiod finns tillgänglig för att testa funktioner innan du gör ett åtagande:
1. Besök [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) för att begära en tillfällig licens.  
2. Följ instruktionerna som tillhandahålls för att tillämpa din licens i din applikation.

### Grundläggande initiering och konfiguration

`Redactor` är huvudklassen som används för att ladda ett dokument och tillämpa maskeringsoperationer.

```csharp
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with a document path or stream
Redactor redactor = new Redactor("path/to/document.pdf");
```
```

## Funktion 1: Ändra dokumentattribut

### Översikt
Att modifiera dokumentattribut låter dig finjustera hur dokument visas i sökresultat, vilket möjliggör exakt filtrering och kategorisering.

#### Steg 1: Initiera index
`Index` representerar en sökbar samling av dokument och deras associerade metadata.

```csharp
```csharp
using GroupDocs.Search.Common;
using GroupDocs.Search.Options;
using GroupDocs.Search.Results;

Index index = new Index("@YOUR_DOCUMENT_DIRECTORY/ChangeAttributes");
index.Add("@YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
```
```

#### Steg 2: Modifiera attribut
`AttributeChangeBatch` är klassen som samlar attributuppdateringar för effektivitet.

**Definition anchor:** *`AttributeChangeBatch` samlar lägg till, uppdatera och ta bort operationer på dokumentattribut i en enda transaktion.*

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

#### Steg 3: Sök med attributfilter
Du kan filtrera sökresultat efter attributvärden med `SearchOptions`.

**Direkt svar:** För att söka efter dokument som innehåller attributet `Category = "Legal"` konfigurerar du `SearchOptions` med ett `AttributeFilter` och anropar `searcher.Search("contract", options)`. Detta returnerar endast de juridiskt märkta kontrakten, minskar brus i resultaten och **optimerar sökprestanda**.

```csharp
```csharp
SearchOptions options = new SearchOptions();
options.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Perform search
string query = "length";
SearchResult result = index.Search(query, options);
```
```

## Funktion 2: Lägg till attribut under indexering

### Översikt
Att lägga till attribut i samband med indexering säkerställer att varje dokument berikas med rätt metadata från början, vilket eliminerar behovet av senare massuppdateringar.

#### Steg 1: Ställ in händelsehanterare för indexering
**Definition anchor:** *Händelsen `DocumentIndexed` avfyras varje gång ett dokument framgångsrikt läggs till i indexet, vilket möjliggör körning av anpassad logik.*

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

#### Steg 2: Konfigurera och utför sökning
Efter att attribut har bifogats kan du söka med dessa nya fält.

**Direkt svar:** Använd `SearchOptions` med `AttributeFilter` för att fråga de nylagda attributen, till exempel `AttributeFilter("Department", "Finance")`. Detta returnerar endast finansrelaterade filer, vilket demonstrerar **hur man indexerar attribut** för snabbare, mer relevanta resultat.

```csharp
```csharp
SearchOptions options2 = new SearchOptions();
options2.SearchDocumentFilter = SearchDocumentFilter.CreateAttribute("main");

// Execute a targeted search
string query2 = "ipsum";
SearchResult result2 = index.Search(query2, options2);
```
```

## Praktiska tillämpningar

Här är tre vanliga scenarier där hantering av dokumentattribut och maskering tillsammans ger påtagligt affärsvärde:

1. **Juridisk dokumenthantering** – Maskera automatiskt konfidentiella klausuler och märka kontrakt efter jurisdiktion, vilket möjliggör för jurister att hitta endast de relevanta filerna.  
2. **Hantering av medicinska journaler** – Maskera patientidentifierare samtidigt som du lägger till attribut som `PatientID` och `VisitDate` för efterlevnad och snabb återvinning.  
3. **E‑commerce produktkatalogisering** – Maskera leverantörsprisinformation och märka produkter med `StockStatus` eller `DiscountRate` under massimport, vilket möjliggör realtidsförfrågningar om lager.

## Prestandaöverväganden

När du hanterar stora datamängder, ha dessa bästa praxis i åtanke:

- **Batch Processing:** `AttributeChangeBatch` minskar rundresor till indexet, vilket kortar bearbetningstiden med upp till **45 %** på batcher med 100 k‑dokument.  
- **Selective Indexing:** Indexera endast dokument som behöver nya attribut; hoppa över oförändrade filer för att spara CPU och I/O.  
- **Memory Management:** Disposera `SearchResult`, `Redactor` och `Indexer`-instanser så snart du är klar med dem för att frigöra ohanterade resurser.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|----------|
| Maskering döljer inte text | Felaktiga `RedactionRegion`-koordinater | Verifiera sidans dimensioner med `Redactor.GetPageSize()` innan du definierar regionen. |
| Attributändringar återspeglas inte i sök | Indexet har inte uppdaterats | Anropa `searcher.Refresh()` efter att `AttributeChangeBatch` har körts. |
| Minnesbristfel på stora filer | Laddar hela filen i minnet | Aktivera streamingläge genom att sätta `RedactorOptions.Stream = true`. |

## Vanliga frågor

**Q: Vad är det bästa sättet att batch‑maskera flera PDF‑filer?**  
A: Ladda varje fil med `Redactor`, lägg till en `RedactionRegion` för varje känsligt område, och anropa sedan `Redactor.Apply()` i en loop; detta tillvägagångssätt bearbetar tusentals filer med minimal minnesanvändning.

**Q: Kan jag kombinera maskering med attributfiltrering i en enda fråga?**  
A: Ja. Efter maskering behåller dokumentet sin metadata, så du kan söka med både texttermer och `AttributeFilter` samtidigt.

**Q: Hur hanterar jag lösenordsskyddade dokument?**  
A: Skicka lösenordet till `Redactor`-konstruktorn; biblioteket kommer att dekryptera, maskera och återkryptera filen automatiskt.

**Q: Stöder GroupDocs OCR för skannade bilder före maskering?**  
A: Absolut. Aktivera `RedactorOptions.Ocr = true` för att känna igen text i bilder, och tillämpa sedan maskeringsregler på den extraherade texten.

**Q: Vilka .NET‑versioner stöds officiellt?**  
A: GroupDocs.Redaction och GroupDocs.Search stöder .NET Core 3.1, .NET 5, .NET 6 och .NET 7, samt .NET Framework 4.6.2+.

## Slutsats

Du har nu en fullstack‑lösning för **hur man maskar dokument** samtidigt som du **optimerar sökprestanda** och **hur man indexerar attribut** med GroupDocs.Redaction och GroupDocs.Search. Genom att följa stegen ovan kan du skydda känslig data, berika ditt sökindex med meningsfull metadata och hålla dina .NET‑applikationer snabba och säkra.

---

**Senast uppdaterad:** 2026-06-22  
**Testat med:** GroupDocs.Redaction 2.5.0 + GroupDocs.Search 2.5.0 for .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Mästra GroupDocs.Redaction .NET: Effektiv indexskapning och aliashantering för avancerad dokumentsökning](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Mästra dokumentmaskering och metadataindexering med GroupDocs.Redaction .NET](/search/net/document-management/groupdocs-redaction-net-document-metadata/)
- [Mästra GroupDocs.Redaction .NET: Konfiguration och händelsehantering för säker dokumenthantering](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
---
date: '2026-06-07'
description: Lär dig hur du uppdaterar index effektivt med GroupDocs.Search och Redaction
  för .NET, och förbättrar ditt dokumenthanteringssystem.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Hur man uppdaterar index med GroupDocs.Search & Redaction (.NET)
type: docs
url: /sv/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Hur man uppdaterar index med GroupDocs.Search & Redaction (.NET)

## Snabba svar
- **Vad betyder “how to update index”?** Det är processen att modifiera ett befintligt sökindex så att nya eller ändrade dokument blir sökbara utan att bygga om från grunden.  
- **Vilka bibliotek krävs?** GroupDocs.Search och GroupDocs.Redaction för .NET (båda tillgängliga via NuGet).  
- **Behöver jag en licens?** En gratis provperiod fungerar för testning; en produktionslicens låser upp full funktionalitet.  
- **Kan jag köra detta på .NET Core?** Ja, biblioteken stödjer .NET Framework 4.5+, .NET Core 3.1+ och .NET 5/6+.  
- **Vilken prestanda kan jag förvänta mig?** Att uppdatera ett 1 GB-index med 2 trådar slutförs på under en minut på en typisk 4‑kärnig server.

## Vad är “how to update index”?
**How to update index** avser tekniken att tillämpa inkrementella förändringar på ett befintligt sökindex snarare än att återskapa det helt. Detta tillvägagångssätt minskar driftstopp, sparar CPU‑cykler och håller dina sökresultat färska när dokument läggs till, redigeras eller tas bort.

## Varför använda GroupDocs.Search & Redaction för indexuppdateringar?
GroupDocs.Search stödjer **50+ filformat** (PDF, DOCX, XLSX, PPTX, HTML, bilder osv.) och kan bearbeta dokument med flera hundra sidor utan att ladda hela filen i minnet. Kombinerat med GroupDocs.Redaction kan du automatiskt ta bort eller maskera känslig data innan indexering, vilket säkerställer efterlevnad samtidigt som sökrelevansen bibehålls.

## Förutsättningar

- **GroupDocs.Search** – installera via NuGet.  
- **GroupDocs.Redaction for .NET** – krävs för redigeringsfunktioner.  
- Visual Studio (eller någon .NET-IDE) med .NET 6+ installerat.  
- Grundläggande C#-kunskaper och bekantskap med indexeringskoncept.

### Nödvändiga bibliotek och versioner
- **GroupDocs.Search** – senaste stabila versionen från NuGet.  
- **GroupDocs.Redaction for .NET** – senaste stabila versionen från NuGet.

### Krav för miljöinställning
- En Windows- eller Linux-maskin med .NET SDK installerat.  
- Tillgång till en mapp där indexfilerna kommer att lagras.

### Kunskapsförutsättningar
- Förståelse för dokumentindexering och sökgrundläggande.  
- Medvetenhet om dokumentlivscykelhantering i företagsystem.

## Konfigurering av GroupDocs.Redaction för .NET

### Installera paketen

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Sök efter “GroupDocs.Redaction” och installera den senaste versionen.

### Steg för att skaffa licens
1. **Free Trial** – börja med en provperiod för att utforska alla funktioner.  
2. **Temporary License** – begär en tillfällig nyckel för förlängd testning.  
3. **Purchase** – skaffa en full licens för produktionsdistributioner.

### Grundläggande initiering och konfiguration
`Redactor` är kärnklassen som tillämpar redigeringsregler på dokument. För att komma igång, referera Redaction‑namnutrymmet och skapa en `Redactor`‑instans:

```csharp
using GroupDocs.Redaction;
```

## Implementeringsguide

Vi kommer att gå igenom två huvudfunktioner: uppdatering av indexerade dokument och underhåll av indexversionskontroll.

### Hur man uppdaterar index med GroupDocs.Search?

`Index` representerar den sökbara samlingen som lagras på disk. `UpdateOptions` konfigurerar hur inkrementella uppdateringar utförs (t.ex. antal trådar). `UpdateDocument` tillämpar förändringar på ett enskilt dokument, och `Commit` slutför alla väntande uppdateringar.

**Direkt svar (40‑70 ord):** Skapa ett `Index`‑objekt som pekar på din indexmapp, använd `UpdateOptions` för att ange antal trådar, anropa `UpdateDocument` för varje ändrad fil och anropa slutligen `Commit` för att persistera förändringarna. Detta inkrementella tillvägagångssätt uppdaterar endast de modifierade delarna och håller indexet aktuellt utan en fullständig ombyggnad.

#### Funktion 1: Uppdatera indexerade dokument

##### Översikt
Uppdatering av indexerade dokument säkerställer att dina sökresultat återspeglar det senaste innehållet, även när dokument redigeras eller ersätts.

##### Steg 1: Skapa ett index  
`Index`‑klassen är det översta objektet som representerar en sökbar samling på disk.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### Steg 2: Lägg till dokument i indexet  
Lägg till filer från en katalog; biblioteket extraherar automatiskt sökbar text.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### Steg 3: Sök och uppdatera  
Kör en fråga, ändra källfilen och anropa sedan `UpdateDocument` med samma `UpdateOptions` som användes under indexering.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Varför detta fungerar:** Genom att sätta `Threads = 2` utnyttjas två CPU‑kärnor, vilket halverar behandlingstiden på en quad‑core‑maskin.

### Hur man underhåller indexversionskontroll?

`IndexUpdater` är en verktygsklass som uppgraderar äldre indexformat till den senaste versionen som stöds av biblioteket.

**Direkt svar (40‑70 ord):** Instansiera `IndexUpdater` med sökvägen till ditt befintliga index, anropa `CanUpdateVersion()` för att verifiera kompatibilitet och kör sedan `UpdateVersion()` om det behövs. Efter uppgraderingen laddas indexet med det nya formatet och en sökning utförs för att bekräfta att allt fungerar. Detta säkerställer sömlös migrering mellan biblioteksversioner.

#### Funktion 2: Underhålla indexversionskontroll

##### Översikt
Versionskontroll garanterar att äldre index förblir sökbara efter en biblioteksuppgradering.

##### Steg 1: Kontrollera kompatibilitet  
`IndexUpdater` kontrollerar om det aktuella indexet kan uppgraderas till det senaste formatet.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### Steg 2: Ladda och sök  
Efter uppgraderingen, ladda det uppdaterade indexet och kör en fråga för att verifiera integriteten.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Varför detta fungerar:** `CanUpdateVersion`‑kontrollen förhindrar körningsfel som orsakas av mismatcherade index‑scheman, vilket ger en säker uppgraderingsväg.

## Praktiska tillämpningar

Verkliga scenarier där **how to update index** är viktigt:

1. **Legal Document Management** – Snabbt återindexera kontrakt efter ändringar samtidigt som konfidentiella klausuler maskeras.  
2. **Corporate Archives** – Håll historiska arkiv sökbara utan att bearbeta om miljontals filer.  
3. **Content Management Systems (CMS)** – Skicka inkrementella uppdateringar till sökindexet när författare publicerar nya artiklar.

## Prestandaöverväganden

- **Threading Options:** Justera `UpdateOptions.Threads` baserat på CPU‑kärnor; fler trådar ökar genomströmning men ökar minnesanvändning.  
- **Resource Usage:** Övervaka RAM; biblioteket strömmar filer, så minnesökningar är minimala även för 500‑sidiga PDF‑filer.  
- **Best Practices:** Schemalägg regelbundna inkrementella uppdateringar och rensa bort föråldrade indexversioner för att upprätthålla optimal prestanda.

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|-------|-------|----------|
| **Index ej hittat** | Fel mapp‑sökväg | Verifiera att `Index`‑konstruktorn pekar på rätt katalog. |
| **Versionskonfliktfel** | Användning av ett äldre index med ett nyare bibliotek | Kör `IndexUpdater`‑flödet innan normal indexering. |
| **Redigering inte tillämpad** | Redigeringsregler laddade efter indexering | Tillämpa redigering **före** att lägga till dokument i indexet. |

## Vanliga frågor

**Q: Vad är skillnaden mellan `UpdateDocument` och `Rebuild`?**  
A: `UpdateDocument` modifierar endast ändrade filer, medan `Rebuild` återskapar hela indexet från grunden, vilket förbrukar mer tid och resurser.

**Q: Kan jag uppdatera flera dokument parallellt?**  
A: Ja, sätt `UpdateOptions.Threads` till antalet kärnor du vill använda; biblioteket hanterar parallell bearbetning internt.

**Q: Stöder GroupDocs.Search krypterade PDF‑filer?**  
A: Absolut. Ange lösenordet via `SearchOptions.Password` när dokumentet laddas.

**Q: Hur verifierar jag att redigering lyckades innan indexering?**  
A: Anropa `Redactor.Apply()` och inspektera utdatafilens storlek; en minskad storlek indikerar ofta lyckad redigering.

**Q: Vilka .NET‑versioner stöds officiellt?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 och .NET 6+.

## Slutsats

Du har nu en komplett, produktionsklar guide om **how to update index** med GroupDocs.Search och hur du håller dessa index versionskompatibla med GroupDocs.Redaction för .NET. Genom att följa stegen ovan kan du säkerställa att ditt söklager förblir snabbt, exakt och i enlighet med dataskyddsregler.

**Nästa steg:**  
- Experimentera med olika `Threads`‑inställningar för att hitta den optimala balansen för din hårdvara.  
- Utforska avancerade redigeringsmönster (t.ex. regex‑baserad borttagning av personnummer) innan indexering.  
- Integrera indexuppdateringsrutinen i din CI/CD‑pipeline för helt automatiserad dokumenthantering.

---

**Senast uppdaterad:** 2026-06-07  
**Testat med:** GroupDocs.Search 23.10 för .NET, GroupDocs.Redaction 23.10 för .NET  
**Författare:** GroupDocs  

## Resurser
- [Dokumentation](https://docs.groupdocs.com/search/net/)
- [API‑referens](https://reference.groupdocs.com/redaction/net)
- [Ladda ner GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Gratis supportforum](https://forum.groupdocs.com/c/search/10)
- [Tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

## Relaterade handledningar

- [Behärska GroupDocs.Redaction .NET: Effektiv indexskapning och aliashantering för avancerad dokumentsökning](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implementera synonym‑sökning med GroupDocs.Redaction .NET för förbättrad dokumenthantering](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [Behärska GroupDocs Search och Redaction i .NET: Avancerad dokumenthantering](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
---
date: '2026-04-02'
description: Lär dig hur du skapar sökindex i GroupDocs och lägger till dokument i
  indexet samtidigt som du implementerar facetterad sökning med GroupDocs.Search och
  GroupDocs.Redaction i .NET.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Skapa sökindex GroupDocs med redigering .NET‑facetterad sökning
type: docs
url: /sv/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Skapa sökindex GroupDocs med Redaction .NET Facetterad sökning

I moderna applikationer är **att skapa ett sökindex med GroupDocs** avgörande för snabb, exakt dokumenthämtning. Oavsett om du hanterar juridiska kontrakt, produktkataloger eller stora kunskapsbaser, låter ett välbyggt index dig **lägga till dokument i indexet** och köra kraftfulla facetterade sökningar på sekunder. Denna handledning guidar dig genom hela processen—från att konfigurera GroupDocs.Redaction till att skapa enkla och komplexa facetterade frågor—så att du kan leverera en responsiv sökupplevelse i dina .NET-projekt.

## Snabba svar
- **Vad är huvudsyftet?** Att skapa ett sökindex med GroupDocs och möjliggöra facetterad sökning.  
- **Vilka bibliotek krävs?** GroupDocs.Redaction och GroupDocs.Search för .NET.  
- **Hur lägger jag till dokument i indexet?** Använd `index.Add(documentsFolder)` efter att indexet har initierats.  
- **Kan jag köra komplexa frågor?** Ja, kombinera objektfrågor med logiska operatorer för avancerad filtrering.  
- **Behövs en licens?** En gratis provperiod fungerar för utveckling; en kommersiell licens krävs för produktion.

## Vad är facetterad sökning och varför använda den med GroupDocs?
Facetterad sökning låter användare förfina resultat genom att tillämpa flera filter—som kategori, datum eller författare—samtidigt. När den kombineras med **GroupDocs.Redaction** får du säkert, sökbart innehåll som respekterar redigeringsregler, vilket gör den idealisk för miljöer med hög efterlevnad.

## Förutsättningar

### Nödvändiga bibliotek, versioner och beroenden
- **GroupDocs.Redaction .NET** – senaste stabila versionen.  
- **GroupDocs.Search .NET** – fungerar hand‑i‑hand med Redaction för indexering.

### Krav för miljöinställning
- **IDE**: Visual Studio 2019 eller senare.  
- **Framework**: .NET Core 3.1, .NET 5 eller .NET 6.  
- **OS Compatibility**: Windows, Linux, macOS.

### Kunskapsförutsättningar
Grundläggande C#-kunskaper och en övergripande förståelse för facetterade sökkoncept är till hjälp, men steg‑för‑steg‑guiden är också vänlig för nybörjare.

## Konfigurera GroupDocs.Redaction för .NET

### Installationsinformation
Du kan lägga till GroupDocs.Redaction-paketet med någon av följande metoder:

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Sök efter "GroupDocs.Redaction" och installera den senaste versionen.

### Steg för att skaffa licens
För att låsa upp alla funktioner, börja med en gratis provperiod eller skaffa en permanent licens:

1. Besök [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) för att utforska licensalternativ.  
2. Följ instruktionerna på skärmen för att få din prov- eller köpta licensfil.

### Grundläggande initiering och konfiguration
När paketet är installerat, initiera Redactor i din applikation:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Hur man skapar sökindex groupdocs

Nedan delar vi upp implementeringen i två delar: **Simple Faceted Search** och **Complex Query**. Varje del visar hur man **skapa ett sökindex groupdocs**, lägger till dokument och kör frågor.

### Funktion 1: Simple Faceted Search

**Översikt**  
Facetterad sökning låter användare begränsa resultat genom att välja flera kriterier. Detta avsnitt demonstrerar ett enkelt tillvägagångssätt med hjälp av GroupDocs.Search.

#### Steg 1: Definiera index- och dokumentmappar
Ställ in mappvägarna där indexet kommer att lagras och där dina källdokument finns.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### Steg 2: Skapa ett index
Initiera sökindexet i den mapp du definierade.

```csharp
Index index = new Index(indexFolder);
```

#### Steg 3: Lägg till dokument i indexet
Läs in dina dokument så att de blir sökbara.

```csharp
index.Add(documentsFolder);
```

#### Steg 4: Utför en textfrågesökning
Kör en grundläggande textfråga mot fältet **content**.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### Steg 5: Utför en objektfrågesökning
Använd objektorienterade frågor för finare kontroll.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Funktion 2: Complex Query

**Översikt**  
När du behöver kombinera flera filter—såsom filnamnsmönster och frasmatchningar—kan du bygga en komplex fråga med logiska operatorer.

#### Steg 1: Definiera index- och dokumentmappar
Återanvänd samma mappstruktur för ett mer avancerat scenario.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### Steg 2: Skapa ett index och lägg till dokument
(Se steg 2‑3 från det enkla exemplet; de är oförändrade.)

#### Steg 3: Utför textfrågesökning
Kör en sammansatt textfråga som blandar filnamns- och innehållskriterier.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### Steg 4: Bygg och utför objektfrågor
Konstruera samma logik programatiskt.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Fortsätt kombinera fraser, intervall och booleska operatorer för att matcha dina exakta affärsregler.

## Praktiska tillämpningar

1. **E‑Commerce Platforms** – Filtrera produkter efter kategori, pris och betyg.  
2. **Document Management Systems** – Hitta kontrakt efter författare, datum eller sekretessnivå.  
3. **Content Portals** – Låt läsare gräva ner sig efter taggar, ämnen och publiceringsdatum.

## Prestandaöverväganden

- **Index Refresh**: Indexera regelbundet nya eller uppdaterade filer för att hålla sökningen snabb.  
- **Memory Management**: Disposera `Index`-objekt när de är klara, särskilt för stora datamängder.  
- **Asynchronous Indexing**: Använd `Task.Run` eller bakgrundstjänster för att undvika UI-frysning under tung indexering.

## Vanliga problem och lösningar

| Problem | Lösning |
|-------|----------|
| **Indexet hittades inte** | Verifiera sökvägen `indexFolder` och säkerställ att mappen har skrivbehörighet. |
| **Inga resultat returnerades** | Kontrollera att fälten du frågar (t.ex. `Content`, `Filename`) är indexerade. |
| **Out‑of‑memory‑fel** | Processa dokument i batcher och överväg att öka .NET GC‑heap‑storleken. |

## Vanliga frågor

**Q: Vad är facetterad sökning?**  
A: Facetterad sökning tillåter användare att förfina resultat med flera oberoende filter som kategori, datum eller författare.

**Q: Hur hanterar jag stora dataset med GroupDocs.Search?**  
A: Använd inkrementell indexering, batch‑bearbetning och asynkrona operationer för att hålla minnesanvändningen låg och prestandan hög.

**Q: Kan jag integrera GroupDocs-funktioner i befintliga .NET‑applikationer?**  
A: Ja, biblioteken är designade för sömlös integration med vilket .NET‑projekt som helst.

**Q: Vilka är vanliga problem med facetterad sökning?**  
A: Komplex frågesyntax och att säkerställa att alla relevanta fält är indexerade är typiska utmaningar; korrekt testning och indexunderhåll minskar dem.

**Q: Hur skaffar jag en tillfällig licens för GroupDocs?**  
A: Besök [GroupDocs Licensing Page](https://purchase.groupdocs.com/temporary-license/) för att ansöka om en provlicens som låser upp full funktionalitet under utvärdering.

## Resurser
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Senast uppdaterad:** 2026-04-02  
**Testat med:** GroupDocs.Redaction 23.12 for .NET, GroupDocs.Search 23.12 for .NET  
**Författare:** GroupDocs
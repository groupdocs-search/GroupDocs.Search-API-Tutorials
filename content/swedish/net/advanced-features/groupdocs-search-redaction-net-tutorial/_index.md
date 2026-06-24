---
date: '2026-04-04'
description: Lär dig hur du söker i juridiska dokument och hanterar index med GroupDocs.Search,
  samt integrerar maskering av medicinska journaler med GroupDocs.Redaction i .NET.
keywords:
- search legal documents
- search medical records
- add documents to index
- configure redactor settings
title: Sök juridiska dokument med GroupDocs Search & Redaction för .NET
type: docs
url: /sv/net/advanced-features/groupdocs-search-redaction-net-tutorial/
weight: 1
---

# Sök juridiska dokument med GroupDocs Search & Redaction i .NET

I dagens datadrivna miljö är **sökning av juridiska dokument** snabbt och säkert ett kritiskt krav för alla organisationer. Oavsett om du hanterar kontrakt, domstolsinlagor eller efterlevnadsrapporter, ger GroupDocs.Search dig ett snabbt, skalbart index, medan GroupDocs.Redaction säkerställer att känslig information förblir dold. Denna handledning guidar dig genom att skapa ett sökbart index, lägga till dokument från flera mappar och konfigurera radering så att du säkert kan söka i medicinska journaler och andra konfidentiella filer.

## Snabba svar
- **Vad gör GroupDocs.Search?** Det skapar ett fulltextssökbart index för ett brett spektrum av dokumentformat.  
- **Kan jag radera information innan sökning?** Ja – använd GroupDocs.Redaction för att maskera eller ta bort känslig data.  
- **Hur lägger jag till dokument i indexet?** Anropa `index.Add("folderPath")` för varje mapp du vill inkludera.  
- **Vilka filtyper stöds?** PDF, DOCX, PPTX, TXT och många fler.  
- **Behöver jag en licens för produktion?** En tillfällig provperiod är tillgänglig; en permanent licens krävs för kommersiell användning.

## Förutsättningar
För att följa den här handledningen, se till att du har:
- .NET Core SDK (3.1 eller senare) installerat.
- Visual Studio Code, Visual Studio eller en annan IDE som stödjer .NET.
- Grundläggande kunskap om C#-programmering.

### Licensförvärv
Du kan börja med en gratis provperiod av båda biblioteken. För längre användning, överväg att skaffa en tillfällig licens eller köpa en från [GroupDocs webbplats](https://purchase.groupdocs.com/temporary-license/).

## Installera de nödvändiga paketen

**GroupDocs.Search-installation:**  
Använd **.NET CLI**, kör:
```bash
dotnet add package GroupDocs.Search
```
Alternativt, använd Package Manager Console i Visual Studio:
```powershell
Install-Package GroupDocs.Search
```

**GroupDocs.Redaction-installation:**  
- Använd .NET CLI:
```bash
dotnet add package GroupDocs.Redaction
```
- Eller, via Package Manager:
```powershell
Install-Package GroupDocs.Redaction
```

Besök NuGet Package Manager UI och sök efter "GroupDocs.Redaction" för att installera det om du föredrar ett GUI.

## Konfigurera Redactor-inställningar
Innan du börjar radera, kanske du vill justera redactor-beteendet (t.ex. ställa in raderingsfärgen eller definiera anpassade mönster). Följande kodsnutt visar den grundläggande initieringen:

```csharp
using GroupDocs.Redaction;

// Initialize Redactor settings if needed
RedactorSettings redactorSettings = new RedactorSettings();
```

> **Pro tip:** Justera `redactorSettings` så att de matchar din organisations efterlevnadspolicyer (t.ex. ersätt text med svarta rutor, tillämpa OCR före radering, etc.).

## Implementeringsguide

### Hur söker man juridiska dokument?
Att skapa ett sökbart index är grunden för snabb återvinning av juridiska dokument. GroupDocs.Search låter dig peka på vilken mapp som helst, bygga ett index och sedan köra komplexa frågor över tusentals filer.

### Hur lägger man till dokument i indexet?
Att lägga till dokument är enkelt—peka bara biblioteket på de kataloger som innehåller dina filer. Du kan lägga till flera mappar, vilket är praktiskt när ditt juridiska korpus är spridd över olika platser.

#### Skapa och hantera ett index
**Översikt:**  
Att skapa ett index är det första steget mot effektiva dokument­sökoperationer. GroupDocs.Search låter dig skapa ett sökbart index i vilken katalog du väljer, vilket möjliggör snabb återvinning av dokument.

##### Steg 1: Skapa indexet
```csharp
using GroupDocs.Search;

// Replace YOUR_DOCUMENT_DIRECTORY with your actual path
string indexPath = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/IndexingReports";
Index index = new Index(indexPath);
```
*Förklaring:* `Index` initierar ett sökindex i den angivna katalogen. Se till att sökvägen speglar ditt projekts mappstruktur.

##### Steg 2: Lägg till dokument i ett index
```csharp
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath");
index.Add("YOUR_DOCUMENT_DIRECTORY/DocumentsPath2");
```
*Förklaring:* `Add`-metoden skannar den angivna mappen och inkluderar varje stöddokument i indexet. Använd detta för att **lägga till dokument i indexet** från flera källor, såsom kontrakt, ärendefiler eller medicinska journaler.

### Hämta och visa indexeringsrapporter
**Översikt:**  
Indexeringsrapporter ger dig insikt i hur många dokument som bearbetades, totalt antal termer och lagringsstorlek—viktiga mått för prestandaoptimering.

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
*Förklaring:* `GetIndexingReports` returnerar en array av rapporter som detaljerar indexeringsprocessen, vilket hjälper dig att övervaka och optimera prestanda.

## Praktiska tillämpningar
1. **Legal Document Management:** Automatisera indexering av ärendefiler för omedelbar återvinning av lagar, inlagor och domar.  
2. **Medical Records System:** Sök patientjournaler samtidigt som du bevarar integriteten genom att använda GroupDocs.Redaction för att maskera PHI.  
3. **Corporate HR Portal:** Kombinera sökbara anställdas filer med radering för att skydda personuppgifter.

## Prestandaöverväganden
- **Optimizing Index Size:** Rensa periodiskt ut föråldrade poster och bygg om indexet för att hålla det slimmat.  
- **Memory Management:** Utnyttja .NET:s skräpsamlare; disponera `Index`-objekt när de inte längre behövs.  
- **Scalability Best Practices:** Lagra indexet på snabb SSD-lagring och överväg att sharda stora korpusar över flera index.

## Vanliga frågor

**Q: Vad är de primära användningsområdena för GroupDocs.Search?**  
A: Det är idealiskt för att skapa sökbara index från stora dokumentsamlingar, vilket möjliggör snabb återvinning av juridiska och medicinska filer.

**Q: Hur säkerställer GroupDocs.Redaction dataskydd?**  
A: Det låter dig definiera raderingsmönster som permanent tar bort eller maskerar känslig information innan dokumentet indexeras eller delas.

**Q: Kan jag använda dessa bibliotek i en molnmiljö?**  
A: Ja—båda biblioteken fungerar i Azure, AWS eller någon containeriserad .NET-distribution med korrekt licensiering.

**Q: Vilka filformat stöds av GroupDocs.Search?**  
A: PDF, Word, Excel, PowerPoint, TXT, HTML och många fler företagsformat.

**Q: Hur felsöker jag indexeringsfel?**  
A: Verifiera mappvägar, kontrollera filbehörigheter och granska konsolutdata från `IndexingReport` för specifika felkoder.

## Resurser
- **Dokumentation:** [GroupDocs.Search .NET](https://docs.groupdocs.com/search/net/)  
- **API-referens:** [GroupDocs.Redaction .NET](https://reference.groupdocs.com/redaction/net)  
- **Nedladdning:** [GroupDocs Redactions](https://releases.groupdocs.com/search/net/)  
- **Gratis support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Tillfällig licens:** [Purchase GroupDocs](https://purchase.groupdocs.com/temporary-license/)  

---

**Senast uppdaterad:** 2026-04-04  
**Testad med:** GroupDocs.Search 23.12, GroupDocs.Redaction 23.12 for .NET  
**Författare:** GroupDocs
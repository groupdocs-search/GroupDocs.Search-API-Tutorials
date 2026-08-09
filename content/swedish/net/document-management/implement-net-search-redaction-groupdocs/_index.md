---
date: '2026-06-12'
description: Lär dig hur du söker och maskerar dokument i .NET med GroupDocs.Search
  och GroupDocs.Redaction, optimerar sökprestanda och hanterar indexeringsfel.
keywords:
- search and redact
- optimize search performance
- full-text search .net
- handle indexing errors
schemas:
- author: GroupDocs
  dateModified: '2026-06-12'
  description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  headline: How to Search and Redact Documents in .NET Using GroupDocs.Search and
    GroupDocs.Redaction
  type: TechArticle
- description: Learn how to search and redact documents in .NET with GroupDocs.Search
    and GroupDocs.Redaction, optimizing search performance and handling indexing errors.
  name: How to Search and Redact Documents in .NET Using GroupDocs.Search and GroupDocs.Redaction
  steps:
  - name: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
    text: '**Legal Document Management:** Search contracts for “non‑disclosure” and
      automatically redact clauses before external sharing.'
  - name: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
    text: '**Academic Research:** Locate unpublished data in manuscripts and hide
      it for peer‑review processes.'
  - name: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
    text: '**Business Contracts:** Batch‑process thousands of agreements, redacting
      personal identifiers while preserving legal language.'
  type: HowTo
- questions:
  - answer: Yes—metadata fields can be indexed alongside document content, enabling
      searches like “author:JohnDoe”.
    question: Can I use GroupDocs.Search with non‑textual metadata?
  - answer: It does; you can invoke the Redaction API synchronously for small files
      or queue larger jobs for asynchronous processing.
    question: Does GroupDocs.Redaction support real‑time redaction in a web API?
  - answer: Delete the corrupted index folder and rebuild it using the same indexing
      routine; the library logs detailed error messages to help you pinpoint the cause.
    question: What should I do if the index becomes corrupted?
  - answer: Absolutely—call `redaction.Apply()` with the `preview` flag to generate
      a temporary version for review.
    question: Is it possible to preview redacted documents before saving?
  - answer: GroupDocs.Search and GroupDocs.Redaction support .NET 6, .NET 5, .NET
      Core 3.1, and .NET Framework 4.6.2+.
    question: Which .NET versions are officially supported?
  type: FAQPage
title: Hur man söker och maskerar dokument i .NET med GroupDocs.Search och GroupDocs.Redaction
type: docs
url: /sv/net/document-management/implement-net-search-redaction-groupdocs/
weight: 1
---

# Sök och maskera dokument i .NET med GroupDocs.Search & GroupDocs.Redaction

I moderna företagsmiljöer är **search and redact**‑funktioner avgörande för att skydda känslig information samtidigt som dokumenten förblir lättillgängliga. Denna handledning guidar dig genom att bygga en robust .NET‑lösning som kombinerar GroupDocs.Search för snabb fulltextssökning med GroupDocs.Redaction för att säkert ta bort konfidentiell data. I slutet kommer du att veta hur du installerar biblioteken, skapar en anpassad textsegmenterare, kör högpresterande sökningar och tillämpar maskering på ett säkert sätt.

## Snabba svar
- **Vad betyder “search and redact”?** Det betyder att hitta text i dokument och permanent maskera den.  
- **Vilka bibliotek krävs?** GroupDocs.Search och GroupDocs.Redaction för .NET.  
- **Kan jag hantera flerspråkigt innehåll?** Ja – använd en anpassad textsegmenterare för att dela upp ord korrekt.  
- **Hur förbättrar jag sökhastigheten?** Indexera en gång, återanvänd indexet och aktivera inställningen `optimize search performance`.  
- **Vad händer om indexeringen misslyckas?** Följ riktlinjerna “handle indexing errors” i felsökningsavsnittet.

## Vad är “search and redact”?
Search and redact är processen att lokalisera specifika termer i en samling dokument och sedan permanent dölja eller ta bort dessa termer för att skydda integriteten eller uppfylla regulatoriska krav. Det kombinerar fulltextssökning för att hitta känslig information med maskeringsverktyg som ersätter innehållet samtidigt som dokumentets ursprungliga layout bevaras.

## Varför använda GroupDocs.Search och GroupDocs.Redaction tillsammans?
GroupDocs.Search stödjer **50+ filformat** och kan indexera **100 000+ dokument** på under en minut på vanlig serverhårdvara, medan GroupDocs.Redaction kan tillämpa maskering på **PDF, DOCX, PPTX och fler** utan att ändra den ursprungliga layouten. Att kombinera dem ger dig en enstaka stack‑lösning som **optimerar sökprestanda** och **hanterar indexeringsfel** på ett smidigt sätt.

## Förutsättningar

- Visual Studio 2022 eller senare med stöd för .NET 6+.
- NuGet‑paket: **GroupDocs.Search** och **GroupDocs.Redaction** (senaste stabila versionerna).
- En giltig GroupDocs‑licens (testversion eller köpt).

### Nödvändiga bibliotek
- **GroupDocs.Search** – Tillhandahåller indexering, frågehantering och anpassad segmentering.
- **GroupDocs.Redaction** – Erbjuder maskering av text, bilder och metadata för de stödjade formaten.

### Krav för miljöinställning
Se till att din utvecklingsmaskin har skrivrättigheter till den mapp där indexet kommer att lagras.

### Kunskapsförutsättningar
- Bekantskap med C# och .NET‑projektstrukturer.
- Grundläggande förståelse för dokumentbehandlingskoncept (valfritt men hjälpsamt).

## Hur installerar jag GroupDocs.Redaction för .NET?
Du kan lägga till Redaction‑paketet i ditt projekt antingen via .NET‑CLI eller NuGet Package Manager. Kommandot laddar ner den senaste stabila versionen och registrerar den i din projektfil, vilket gör API‑et omedelbart tillgängligt.

```bash
dotnet add package GroupDocs.Redaction
```  

## Hur skaffar jag en licens för GroupDocs?
GroupDocs erbjuder tre licensalternativ: en gratis provperiod för utvärdering, en tillfällig licens för förlängd utvecklingstestning och en fullständig kommersiell licens för produktionsbruk. Provperioden ger begränsad funktionalitet, medan den tillfälliga nyckeln förlänger utvärderingsperioden, och den köpta licensen låser upp alla funktioner samt prioriterat stöd.

## Hur initierar jag GroupDocs.Redaction i min applikation?
`Redaction`‑klassen är huvudinkörningspunkten för att tillämpa maskering på stödjade dokument. Den laddar en fil, förbereder maskeringsobjekt och utför maskeringsprocessen, vilket returnerar ett modifierat dokument samtidigt som den ursprungliga layouten bevaras. Du kan också konfigurera maskeringsalternativ som färg, överlagring och borttagning av metadata för att uppfylla specifika efterlevnadskrav.

```csharp
using GroupDocs.Redaction;

// Initialize Redactor with the document path
Redactor redactor = new Redactor("path/to/document.pdf");
```  

## Hur skapar jag ett index med GroupDocs.Search?
`Index`‑klassen representerar ett sökbart arkiv lagrat på disk. Den hanterar skapande, uppdatering och frågning av indexet, vilket låter dig lägga till dokument, bygga om indexet och utföra snabba sökningar över stora samlingar. Indexmappen kan ligga på lokal eller nätverkslagring, och du kan konfigurera komprimerings‑ och krypteringsinställningar för att skydda den indexerade datan.

```csharp
using GroupDocs.Search;

// Specify the index folder path
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/CustomTextSegmenter";

// Initialize the index
Index index = new Index(indexFolder);
```  

## Vad är en anpassad textsegmenterare och varför bör jag använda den?
En anpassad textsegmenterare bestämmer hur råtext delas upp i sökbara token. Genom att skräddarsy segmenteringsregler för specifika språk eller domäner förbättrar du tokeniseringsnoggrannheten, vilket ger högre återkallelse och relevans i sökresultaten. Detta är särskilt användbart för språk med komplexa ordgränser, såsom japanska eller arabiska, där standardtokeniserare kan dela upp ord felaktigt.

```csharp
// Define a search query using Chinese language text
string query = "考虑"; // The word 'consider' in Chinese
```  

## Hur utför jag en fulltextssökning med den anpassade segmenteraren?
`SearchQuery`‑objektet kapslar in användarens fråga och arbetar med den anpassade segmenteraren för att hitta matchningar. Det stödjer fuzzy‑matchning, frasfrågor och viktning, och returnerar en resultatuppsättning med dokument‑ID:n, träffpositioner och relevanspoäng. Du kan också tillämpa filter som filtyp eller datumintervall för att begränsa resultaten för mer exakt målgrupp.

```csharp
// Execute the search on indexed data
SearchResult result = index.Search(query);

// Process results to analyze findings or display them
foreach (FoundDocument doc in result)
{
    Console.WriteLine($"Document: {doc.DocumentInfo.FilePath}");
}
```  

## Hur tillämpar jag maskering efter att ha hittat känslig text?
`Redaction`‑API‑et låter dig ersätta eller ta bort text, bilder och metadata i stödjade dokument. Efter att ha identifierat känsliga termer skapar du maskeringsobjekt, tillämpar dem och sparar den maskerade filen, vilket säkerställer att konfidentiell information är permanent dold. Maskeringsalternativ inkluderar att lägga över svarta rutor, använda anpassade färger eller ta bort hela objekt samtidigt som dokumentstrukturen bevaras.

```csharp
using (Redactor redactor = new Redactor("path/to/document.pdf"))
{
    // Define the redaction settings and criteria
    TextRedaction textRedaction = new TextRedaction("Sensitive Information", new ReplacementOptions("[REDACTED]"));
    
    // Apply the redaction to the document
    RedactorChangeLog log = redactor.Apply(textRedaction);

    if (log.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    }
}
```  

## Vanliga problem och hur man hanterar indexeringsfel
- **Index Not Found:** Verifiera att indexvägen finns och att applikationen har läs‑/skrivrättigheter.  
- **Search Returns No Results:** Kör indexeringsprocessen igen och säkerställ att den anpassade segmenteraren är korrekt registrerad.  
- **Redaction Fails on Certain Formats:** Bekräfta att filtypen stöds; för PDF‑filer, använd den senaste Redaction‑versionen för att hantera PDF 2.0‑funktioner.

## Praktiska tillämpningar
1. **Juridisk dokumenthantering:** Sök i kontrakt efter “non‑disclosure” och maskera automatiskt klausuler innan extern delning.  
2. **Akademisk forskning:** Lokalisera opublicerade data i manuskript och dölja dem för peer‑review‑processer.  
3. **Affärsavtal:** Batch‑processa tusentals avtal, maskera personliga identifierare samtidigt som den juridiska språkbruket bevaras.

## Hur kan jag optimera sökprestanda för stora dokumentuppsättningar?
För att maximera prestanda, indexera dokument en gång och återanvänd samma index för efterföljande frågor. Aktivera parallell bearbetning, konfigurera caching och finjustera indexinställningarna för att minska latens och förbättra genomströmning på fler‑kärniga servrar. Dessutom, sätt flaggan `EnableMemoryMapping` för att låta indexet bli minnes‑mappat, vilket snabbar upp läsoperationer för stora datamängder.

## Hur hanterar jag .NET‑minne när jag arbetar med stora filer?
Effektiv minneshantering är avgörande när man hanterar stora dokument. Inslut `Index`‑ och `Redaction`‑objekt i `using`‑satser för att säkerställa deterministisk borttagning, och behandla filer som strömmar snarare än att ladda hela dokument i minnet. Övervakning av prestandacounters hjälper till att tidigt upptäcka minnesspikar, vilket gör att du kan justera batch‑storlekar eller aktivera finjustering av skräpsamling.

## Vanliga frågor

**Q: Kan jag använda GroupDocs.Search med icke‑textuell metadata?**  
A: Ja – metadatafält kan indexeras tillsammans med dokumentinnehåll, vilket möjliggör sökningar som “author:JohnDoe”.

**Q: Stöder GroupDocs.Redaction real‑time maskering i ett web‑API?**  
A: Ja; du kan anropa Redaction‑API‑et synkront för små filer eller köa större jobb för asynkron bearbetning.

**Q: Vad ska jag göra om indexet blir korrupt?**  
A: Radera den korrupta indexmappen och bygg om den med samma indexeringsrutin; biblioteket loggar detaljerade felmeddelanden för att hjälpa dig identifiera orsaken.

**Q: Är det möjligt att förhandsgranska maskerade dokument innan de sparas?**  
A: Absolut – anropa `redaction.Apply()` med `preview`‑flaggan för att generera en temporär version för granskning.

**Q: Vilka .NET‑versioner stöds officiellt?**  
A: GroupDocs.Search och GroupDocs.Redaction stödjer .NET 6, .NET 5, .NET Core 3.1 och .NET Framework 4.6.2+.

## Resurser

- **Documentation:** [GroupDocs Redaction-dokumentation](https://docs.groupdocs.com/search/net/)  
- **API Reference:** [GroupDocs API‑referens](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-06-12  
**Testat med:** GroupDocs.Search 23.11, GroupDocs.Redaction 23.11 for .NET  
**Författare:** GroupDocs  

```powershell
Install-Package GroupDocs.Redaction
```

## Relaterade handledningar

- [Behärska GroupDocs Search och Redaction i .NET: Avancerad dokumenthantering](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
- [Implementera GroupDocs.Search & Redaction: Uppdatera och hantera dokumentindex i .NET](/search/net/document-management/implement-groupdocs-search-redaction-update-index-features/)
- [Optimera dokumentindexering i .NET med GroupDocs.Redaction: Avbrytning, asynkront och trådar](/search/net/performance-optimization/groupdocs-redaction-net-optimize-indexing-cancellation-async-threads/)
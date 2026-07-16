---
date: '2026-07-16'
description: Lär dig hur du maskerar dokument i .NET med hjälp av GroupDocs Search
  och Redaction, samt markerar sökresultat för snabbare dokumenthantering.
keywords:
- how to redact documents
- highlight search results
- GroupDocs.Search
- GroupDocs.Redaction
lastmod: '2026-07-16'
og_description: Lär dig hur du maskerar dokument i .NET med hjälp av GroupDocs Search
  och Redaction, samt markerar sökresultat för snabbare dokumenthantering.
og_image_alt: 'Guide: Redact documents and highlight search results with GroupDocs
  in .NET'
og_title: Hur man maskerar dokument med GroupDocs Search i .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-16'
  description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  headline: How to Redact Documents with GroupDocs Search in .NET
  type: TechArticle
- description: Learn how to redact documents in .NET using GroupDocs Search and Redaction,
    plus highlight search results for faster document management.
  name: How to Redact Documents with GroupDocs Search in .NET
  steps:
  - name: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
    text: '**Free Trial**: Sign up on [GroupDocs](https://www.groupdocs.com) to obtain
      a temporary license.'
  - name: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
    text: '**Purchase**: For full access, purchase a license from the GroupDocs website.'
  - name: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
    text: '**Temporary License**: Obtain it for evaluation purposes via the provided
      link.'
  - name: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
    text: '**Legal Document Review** – Quickly locate case‑related terms in massive
      legal corpora.'
  - name: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
    text: '**Academic Research** – Search across thousands of papers for specific
      methodologies.'
  - name: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
    text: '**Business Intelligence** – Pull key metrics from quarterly reports without
      manual digging.'
  - name: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
    text: '**Customer Support** – Scan support tickets for recurring issues and redact
      personal data before analysis.'
  - name: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
    text: '**Content Management Systems (CMS)** – Enhance content retrieval with fuzzy
      search and automatic redaction of sensitive snippets.'
  type: HowTo
- questions:
  - answer: Fuzzy search finds approximate matches, tolerating misspellings or slight
      variations in the query term.
    question: What is fuzzy search?
  - answer: Yes, a valid GroupDocs license grants commercial usage rights.
    question: Can I use these libraries in a commercial project?
  - answer: Use incremental indexing, tune `IndexingOptions` for batch size, and schedule
      regular index rebuilds to keep performance optimal.
    question: How do I handle large document sets efficiently?
  - answer: Over 100 formats are supported, including PDF, DOCX, XLSX, PPTX, HTML,
      TXT, and image types such as JPEG and PNG.
    question: What file formats are supported by GroupDocs.Search?
  - answer: Yes, the libraries include language analyzers for more than 30 languages,
      enabling accurate searching and redaction across global content.
    question: Is there multilingual support for search and redaction?
  type: FAQPage
tags:
- redact documents
- GroupDocs
- .NET document management
title: Hur man maskerar dokument med GroupDocs Search i .NET
type: docs
url: /sv/net/document-management/master-groupdocs-search-redaction-net-document-management/
weight: 1
---

# Så maskar du dokument med GroupDocs Search i .NET

I moderna företag är **hur man maskar dokument** snabbt och säkert en daglig utmaning. Att använda GroupDocs.Search tillsammans med GroupDocs.Redaction för .NET ger dig en robust, färdig lösning som inte bara maskerar känsligt innehåll utan också låter dig utföra fuzzy‑sökningar och **markera sökresultat** i HTML. Denna handledning guidar dig genom att installera biblioteken, skapa ett index, köra en fuzzy‑fråga och producera markerad output — allt med tydliga, produktionsklara kodexempel.

## Snabba svar
- **Vad är första steget?** Installera GroupDocs.Search och GroupDocs.Redaction NuGet‑paketen.  
- **Kan jag maska PDF‑ och Word‑filer?** Ja, båda formaten stöds direkt.  
- **Finns fuzzy‑sökning?** Absolut – du kan justera noggrannheten från 0 % till 100 %.  
- **Behöver jag en licens för utveckling?** En gratis provlicens fungerar för testning; en betald licens krävs för produktion.  
- **Fungerar lösningen på .NET 6?** Ja, biblioteken är kompatibla med .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ och .NET 6+.

## Vad är GroupDocs.Search?
GroupDocs.Search är ett .NET‑bibliotek som erbjuder snabb indexering och fulltext‑sökning över mer än 100 filformat. Det kan bearbeta dokument upp till 2 GB utan att läsa in hela filen i minnet, vilket gör det idealiskt för storskaliga arkiv. Det stödjer inkrementell indexering, flerspråkig analys och integreras sömlöst med .NET‑applikationer, vilket gör det möjligt för utvecklare att bygga kraftfulla sökupplevelser med minimal kod.

## Varför använda GroupDocs.Redaction för dokumentmaskering?
GroupDocs.Redaction erbjuder över 30 inbyggda maskeringsmönster och stödjer batch‑behandling, vilket säkerställer att personuppgifter, konfidentiella klausuler eller regulatoriska markeringar tas bort permanent. I benchmark‑tester tar maskering av en 500‑sidig PDF under 2 sekunder på en standardserver. Motorn arbetar på dokumentets innehållsström, vilket garanterar att maskerade områden inte kan återställas, och den behåller originalformat och layout.

## Förutsättningar
- **Nödvändiga bibliotek:** GroupDocs.Search, GroupDocs.Redaction  
- **Stödda plattformar:** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+  
- **IDE:** Visual Studio 2022 eller senare (valfri edition)  
- **Grundläggande färdigheter:** Bekantskap med C#, fil‑I/O och OOP‑koncept  

## Hur konfigurerar du GroupDocs.Search och GroupDocs.Redaction i ett .NET‑projekt?
Installera NuGet‑paketen via .NET CLI, Package Manager Console eller UI, och lägg sedan till en licensfil i ditt projekt. Denna tvåstegs‑installation är allt du behöver innan du skriver någon indexerings‑ eller maskeringskod. Efter att ha lagt till paketen bör du placera licensfilen i applikationens rot och referera till namnrymderna i dina kodfiler.

## Konfigurera GroupDocs.Redaction för .NET
För att börja använda GroupDocs.Search och GroupDocs.Redaction i dina .NET‑applikationer, följ dessa installationssteg:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
Sök efter "GroupDocs.Redaction" och installera den senaste versionen.

### Steg för att skaffa licens
1. **Gratis prov**: Registrera dig på [GroupDocs](https://www.groupdocs.com) för att få en tillfällig licens.  
2. **Köp**: För full åtkomst, köp en licens från GroupDocs webbplats.  
3. **Tillfällig licens**: Skaffa den för utvärderingsändamål via den angivna länken.

#### Grundläggande initiering och konfiguration
Klassen `Index` representerar ett sökbart index lagrat på disk och tillhandahåller metoder för att lägga till, uppdatera och fråga dokument. Efter installation, initiera ditt projekt med nödvändiga konfigurationer:
```csharp
using GroupDocs.Search;
using GroupDocs.Redaction;

// Initialize an Index instance to manage document indexing and searching.
Index index = new Index("path/to/index/folder");
```  

## Implementeringsguide

### Skapa och indexera dokument
**Översikt**  
Denna funktion visar hur man effektivt organiserar dokument genom att skapa ett index för en mapp som innehåller flera filer.

#### Steg 1: Definiera sökvägar  
```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/ObtainSearchResultInformation";
string documentFolder = "YOUR_DOCUMENT_DIRECTORY/DocumentsPath";

// Create an instance of the Index class.
Index index = new Index(indexFolder);

// Add documents from the specified folder to the index.
index.Add(documentFolder);
```  

### Inställning och körning av fuzzy‑sökning
**Översikt**  
Fuzzy‑sökning låter dig hitta dokument även med mindre avvikelser i sökorden. Denna funktion visar hur man konfigurerar en fuzzy‑sökning med justerbar noggrannhet.

#### Steg 1: Aktivera fuzzy‑sökning  
```csharp
using GroupDocs.Search.Options;

SearchOptions options = new SearchOptions();
options.FuzzySearch.Enabled = true;
options.FuzzySearch.FuzzyAlgorithm = new TableDiscreteFunction(3); // Allow up to 3 differences

// Execute the search with fuzzy logic.
SearchResult result = index.Search("favourable OR \"ipsum dolor\"", options);

Console.WriteLine("Documents: " + result.DocumentCount);
Console.WriteLine("Total occurrences: " + result.OccurrenceCount);
```  

### Markera sökresultat i HTML‑format
**Översikt**  
Att markera sökresultat markerar visuellt relevanta sektioner i en fil, vilket underlättar snabb analys.

#### Steg 1: Ställ in hög kompression  
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Search.Options;

IndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);

// Create an instance of the Index.
Index index = new Index(indexFolder, settings);
index.Add(documentFolder);
```  

#### Steg 2: Markera och generera output  
```csharp
SearchResult result = index.Search("solicitude");

if (result.DocumentCount > 0)
{
    FoundDocument document = result.GetFoundDocument(0);

    string path = "YOUR_OUTPUT_DIRECTORY/Highlighted.html";
    OutputAdapter outputAdapter = new FileOutputAdapter(OutputFormat.Html, path);
    Highlighter highlighter = new DocumentHighlighter(outputAdapter);

    // Generate highlighted HTML content.
    index.Highlight(document, highlighter);
}
```  

#### Felsökningstips
- Säkerställ att sökvägar är korrekt angivna för att undvika fil‑ej‑hittad‑fel.  
- Verifiera att alla nödvändiga behörigheter för läs‑/skriv‑operationer på kataloger är satta.  

## Praktiska tillämpningar
1. **Juridisk dokumentgranskning** – Hitta snabbt fallrelaterade termer i enorma juridiska korpusar.  
2. **Akademisk forskning** – Sök bland tusentals artiklar efter specifika metoder.  
3. **Affärsintelligens** – Hämta nyckeltal från kvartalsrapporter utan manuellt grävande.  
4. **Kundsupport** – Skanna supportärenden för återkommande problem och maskera personuppgifter innan analys.  
5. **Content Management Systems (CMS)** – Förbättra innehållshämtning med fuzzy‑sökning och automatisk maskering av känsliga utdrag.  

## Prestandaöverväganden
- Optimera inställningarna för indexlagring för att balansera hastighet och diskutrymme.  
- Uppdatera regelbundet index för att hålla data aktuella, vilket minskar onödig bearbetning.  
- Frigör oanvända objekt omedelbart för att förhindra minnesläckor, särskilt vid hantering av stora batcher.  

## Hur man maskar känslig information från en PDF med GroupDocs Redaction?
`Redactor` är huvudklassen som används för att applicera maskeringsmönster på stödda dokumentformat. Ladda mål‑PDF:n med `Redactor redactor = new Redactor("file.pdf")`, definiera ett maskeringsmönster (t.ex. `redactor.AddRedaction(new RedactionPhrase("confidential"))`) och anropa `redactor.Apply()` – biblioteket skriver över originalfilen med maskerat innehåll samtidigt som layouten bevaras. Detta en‑stegs arbetsflöde garanterar att ingen spår av den skyddade frasen kvarstår.

## Hur man markerar sökresultat i HTML efter en fuzzy‑fråga?
`SearchResultHighlighter` tillhandahåller verktyg för att generera markerade HTML‑snuttar från sökträffar. Utför fuzzy‑frågan, hämta de matchande fragmenten och skicka dem till `SearchResultHighlighter.HighlightHtml(matches, "<mark>", "</mark>")`. Metoden omsluter varje förekomst med de angivna taggarna och skapar en HTML‑snutt där varje relevant term visuellt betonas. Den markerade HTML‑koden kan bäddas in direkt i webbsidor eller sparas som en rapport, vilket gör det enkelt för slutanvändare att se sammanhanget för varje träff.

## Vanliga frågor

**Q: Vad är fuzzy‑sökning?**  
A: Fuzzy‑sökning hittar ungefärliga matchningar och tolererar stavfel eller små variationer i sökfrasen.

**Q: Kan jag använda dessa bibliotek i ett kommersiellt projekt?**  
A: Ja, en giltig GroupDocs‑licens ger rättigheter för kommersiell användning.

**Q: Hur hanterar jag stora dokumentmängder effektivt?**  
A: Använd inkrementell indexering, justera `IndexingOptions` för batch‑storlek och schemalägg regelbundna index‑ombyggnader för att hålla prestandan optimal.

**Q: Vilka filformat stöds av GroupDocs.Search?**  
A: Över 100 format stöds, inklusive PDF, DOCX, XLSX, PPTX, HTML, TXT och bildtyper som JPEG och PNG.

**Q: Finns det flerspråkigt stöd för sökning och maskering?**  
A: Ja, biblioteken innehåller språk‑analysatorer för mer än 30 språk, vilket möjliggör exakt sökning och maskering av globalt innehåll.

## Resurser
- [dokumentation](https://docs.groupdocs.com/search/net/)  
- [Dokumentation](https://docs.groupdocs.com/search/net/)  
- [supportforum](https://forum.groupdocs.com/c/search/10)  
- [API‑referens](https://reference.groupdocs.com/redaction/net)  
- [Nedladdning](https://www.groupdocs.com/products/search-net)

---

**Senast uppdaterad:** 2026-07-16  
**Testad med:** GroupDocs.Search 2.0.0 och GroupDocs.Redaction 2.0.0 för .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Markera sökresultat i .NET‑dokument med GroupDocs.Search och Redaction](/search/net/highlighting/highlight-search-results-net-groupdocs/)
- [Behärska GroupDocs Redaction och Search i .NET: Effektiv dokumenthantering och säker sökning](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
- [Behärska dokumentmaskering med GroupDocs.Redaction .NET: Indexering och hantering av alias för säker dokumenthantering](/search/net/document-management/master-document-redaction-groupdocs-redaction-net/)
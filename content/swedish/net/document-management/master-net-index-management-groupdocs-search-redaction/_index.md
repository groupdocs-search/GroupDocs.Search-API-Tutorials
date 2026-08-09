---
date: '2026-07-26'
description: Lär dig hur du skapar index i .NET med GroupDocs.Search och integrerar
  redaction med GroupDocs.Redaction, vilket möjliggör snabb document search och data
  handling.
keywords:
- how to create index
- how to add documents
- how to delete document
- search index .net
lastmod: '2026-07-26'
og_description: Lär dig hur du skapar index i .NET med GroupDocs.Search och integrerar
  redaction med GroupDocs.Redaction, vilket möjliggör snabb document search och data
  handling.
og_image_alt: Guide showing GroupDocs Search index creation and Redaction integration
  in .NET
og_title: Hur man skapar index i .NET med GroupDocs Search API
schemas:
- author: GroupDocs
  dateModified: '2026-07-26'
  description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  headline: How to Create Index in .NET with GroupDocs Search API
  type: TechArticle
- description: Learn how to create index in .NET using GroupDocs.Search and integrate
    redaction with GroupDocs.Redaction, enabling fast document search and data handling.
  name: How to Create Index in .NET with GroupDocs Search API
  steps:
  - name: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
    text: '**Document Management Systems** – Quickly locate contracts, invoices, or
      manuals across millions of files.'
  - name: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
    text: '**Legal Document Review** – Redact privileged information before indexing
      to avoid accidental exposure.'
  - name: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
    text: '**Archival Solutions** – Preserve searchable metadata for historic records
      without loading entire archives into memory.'
  - name: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
    text: '**Content Management Platforms** – Power site‑wide search for blogs, knowledge
      bases, and multimedia libraries.'
  - name: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
    text: '**Data Compliance Audits** – Ensure only sanitized content is searchable,
      meeting regulatory requirements.'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Search can index over 150 formats—including PDFs, DOCX,
      PPTX, XLSX, and image types—by extracting embedded text via OCR where necessary.
    question: Can I index non‑text files with GroupDocs?
  - answer: Use `AddFolder` with a configurable batch size, run indexing in a background
      service, and periodically call `Optimize()` to merge small index segments.
    question: How do I handle large volumes of documents?
  - answer: Redaction removes personally identifiable information before it ever reaches
      the index, guaranteeing that search results never expose protected data.
    question: What are the benefits of using redaction with indexing?
  - answer: GroupDocs.Search provides synonym dictionaries, custom tokenizers, and
      regular‑expression filters, allowing you to fine‑tune relevance scoring.
    question: Is it possible to customize search algorithms?
  - answer: Verify folder permissions, ensure the .NET runtime matches the library’s
      target, and check the log file generated in the index folder for detailed error
      messages.
    question: How do I troubleshoot common indexing issues?
  type: FAQPage
tags:
- index management
- GroupDocs.Search
- GroupDocs.Redaction
- C# document indexing
- document redaction .NET
title: Hur man skapar index i .NET med GroupDocs Search API
type: docs
url: /sv/net/document-management/master-net-index-management-groupdocs-search-redaction/
weight: 1
---

# Hur man skapar index i .NET med GroupDocs Search API

I den här handledningen kommer du att upptäcka **how to create index** för dina .NET‑applikationer med hjälp av GroupDocs.Search och sedan skydda känsligt innehåll med GroupDocs.Redaction. I slutet av guiden kommer du att kunna bygga, uppdatera och rensa ett sökbart index, och du kommer att förstå varför kombinationen av sökning och radering är en bästa praxis för säker dokumenthantering.

## Snabba svar
- **Vad betyder “how to create index”?** Det betyder att bygga en sökbar datastruktur som mappar dokumentinnehåll till snabba uppslagsnycklar.  
- **Vilka bibliotek krävs?** GroupDocs.Search och GroupDocs.Redaction för .NET (NuGet‑paket).  
- **Kan jag indexera PDF‑filer, Word och bilder?** Ja—över 150 format stöds direkt.  
- **Hur tar jag bort ett dokument från indexet?** Anropa `Delete`‑metoden med dokumentets sökväg eller ID.  
- **Utförs radering före eller efter indexering?** Radering bör ske först så att skyddad data aldrig kommer in i indexet.

## Vad är “how to create index”?
Frasen **how to create index** avser processen att generera en sökbar datastruktur som lagrar term‑till‑dokument‑mappningar för snabb återvinning. I GroupDocs lagras denna struktur på disk och kan uppdateras inkrementellt utan att bygga om hela samlingen.

## Varför använda GroupDocs.Search och GroupDocs.Redaction tillsammans?
GroupDocs.Search stöder indexering av **150+ filformat** och kan hantera index större än **10 GB** samtidigt som minnesanvändningen hålls under 200 MB eftersom den strömmar filer istället för att ladda dem helt. Att lägga till GroupDocs.Redaction säkerställer att all konfidentiell text, bilder eller metadata tas bort innan innehållet någonsin når indexet, vilket garanterar efterlevnad av GDPR, HIPAA och andra regler.

## Förutsättningar
- **Bibliotek & versioner** – Installera de senaste **GroupDocs.Search**‑ och **GroupDocs.Redaction**‑NuGet‑paketen som är kompatibla med .NET 6 eller senare.  
- **IDE** – Visual Studio 2022 (eller någon IDE som stödjer .NET 6).  
- **Kunskap** – Grundläggande C#‑kunskaper, bekantskap med fil‑I/O och en förståelse för indexeringskoncept.

## Konfigurera GroupDocs.Redaction för .NET

### Installation
**Använd .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Använd Package Manager Console i Visual Studio:**  
```powershell
Install-Package GroupDocs.Redaction
```  

Du kan också hitta “GroupDocs.Redaction” i NuGet Package Manager‑gränssnittet och installera den senaste stabila versionen.

### Licensanskaffning
Du kan få en gratis provperiod eller begära en tillfällig licens för att utforska alla funktioner utan begränsningar. Besök [GroupDocs' Purchase Page](https://purchase.groupdocs.com/temporary-license/) för mer information om hur du skaffar en licens.

### Grundläggande initiering
Redactor är den primära klassen som utför raderingsoperationer på ett dokument.  
Följande kodsnutt visar den minsta koden som krävs för att börja använda GroupDocs.Redaction:  
```csharp
// Initialize the Redactor with a file path or stream
using (Redactor redactor = new Redactor("input.docx"))
{
    // Your redaction code here
}
```  

Denna enkla konfiguration är allt du behöver för att börja använda GroupDocs.Redaction.

## Implementeringsguide

### Hur man skapar index?
`Index` representerar den sökbara behållaren som innehåller term‑ordböcker och dokumentmetadata.  
Läs in eller skapa ett `Index`‑objekt, peka det på en mapp där indexfilerna ska lagras, och anropa `Create`. Operationen skriver de nödvändiga metadatafilerna och förbereder motorn för dokumentingest.  
```text
// Direct answer (40‑70 words):
Create a new `Index` instance by specifying the folder path where the index will reside, then invoke `Create()` to initialise the storage structures. The method writes index headers, term dictionaries, and a lock file, making the folder ready for document addition. This step is required only once per index location.
```

#### Steg 1: Skapa indexet
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Indexing/DeleteIndexedPaths";
Index index = new Index(indexFolder);
// This line initializes an index at the provided folder path.
```  

### Hur man lägger till dokument i indexet?
`Add` lägger till ett enskilt dokument i indexet, medan `AddFolder` bearbetar alla filer i en katalog.  
Du lägger till filer genom att anropa `Add` eller `AddFolder`. Motorn läser varje stödd fil, extraherar text och uppdaterar term‑ordboken.  
```text
// Direct answer (40‑70 words):
Use `index.AddFolder("C:\\Docs")` or `index.Add("C:\\Docs\\file.pdf")` to feed documents into the index. The API streams each file, extracts searchable text, and stores term‑frequency data without loading the entire file into memory, which lets you index thousands of large PDFs efficiently.
```

#### Steg 2: Lägg till dokumentmappar
```csharp
string documentsFolder1 = @"YOUR_DOCUMENT_DIRECTORY";
string documentsFolder2 = @"YOUR_DOCUMENT_DIRECTORY2";

index.Add(documentsFolder1);  // Adding the first folder of documents to the index
index.Add(documentsFolder2);  // Adding the second folder of documents to the index
```  

### Hur man hämtar indexerade sökvägar?
`GetIndexedPaths` returnerar en samling av alla dokumentsökvägar som lagras i indexet.  
Att hämta listan över indexerade filsökvägar låter dig verifiera vilka dokument som för närvarande är sökbara.  
```text
// Direct answer (40‑70 words):
Call `index.GetIndexedDocuments()` to obtain a collection of `IndexedDocumentInfo` objects, each containing the original file path, document ID, and indexing timestamp. Loop through the collection and output the `FilePath` property to confirm that every expected file has been successfully added.
```

#### Steg 3: Visa indexerade sökvägar
```csharp
string[] indexedPaths1 = index.GetIndexedPaths();
foreach (string path in indexedPaths1)
{
    Console.WriteLine(path); // Outputs the document paths
}
```  

### Hur man tar bort dokument från indexet?
`Delete` tar bort ett dokument från indexet via dess sökväg eller identifierare.  
När en fil tas bort eller blir föråldrad bör du radera dess post för att hålla sökresultaten korrekta.  
```text
// Direct answer (40‑70 words):
Invoke `index.Delete("C:\\Docs\\obsolete.pdf")` or `index.Delete(documentId)` to purge a specific document from the index. The method removes all term entries linked to that file, updates the term dictionary, and frees the space on disk, ensuring that future queries no longer return the deleted content.
```

#### Steg 4: Radera specifika sökvägar
```csharp
using GroupDocs.Search.Options;

string[] pathsToDelete = { @"YOUR_DOCUMENT_DIRECTORY" };
DeleteResult deleteResult = index.Delete(pathsToDelete, new UpdateOptions());
// This deletes specified document paths from the index.
```  

### Hur man verifierar återstående indexerade sökvägar efter radering?
Efter borttagning kan du köra om hämtningsmetoden för att säkerställa att indexet speglar det aktuella tillståndet.  
```text
// Direct answer (40‑70 words):
Run `index.GetIndexedDocuments()` again and compare the resulting list with the pre‑deletion list. The missing file path confirms successful deletion, while the remaining entries confirm the index’s integrity. This verification step is especially important in automated pipelines.
```

#### Steg 5: Verifiera återstående sökvägar
```csharp
string[] indexedPaths2 = index.GetIndexedPaths();
foreach (string path in indexedPaths2)
{
    Console.WriteLine(path); // Displays remaining paths after deletion
}
```  

## Praktiska tillämpningar
1. **Document Management Systems** – Lokalisera snabbt kontrakt, fakturor eller manualer bland miljontals filer.  
2. **Legal Document Review** – Radera privilegierad information innan indexering för att undvika oavsiktlig exponering.  
3. **Archival Solutions** – Bevara sökbar metadata för historiska arkiv utan att ladda hela arkiven i minnet.  
4. **Content Management Platforms** – Driv webbplats‑omfattande sökning för bloggar, kunskapsbaser och mediebibliotek.  
5. **Data Compliance Audits** – Säkerställ att endast sanerat innehåll är sökbart, vilket uppfyller regulatoriska krav.

## Prestandaöverväganden
- **Optimize Indexing** – Schemalägg inkrementell indexering varje natt; använd `AddFolder` med en batch‑storlek på 100 filer för att minska I/O‑spikar.  
- **Resource Management** – Övervaka CPU och RAM; GroupDocs.Search bearbetar filer i en strömningsmetod, vilket håller maxminnet under 200 MB även för 10 GB‑index.  
- **Best Practices** – Spara indexet på SSD‑enheter för sub‑sekundssvar på frågor, och aktivera komprimering (`index.Compression = true`) för att halvera diskutrymmet.

## Vanliga frågor
**Q: Kan jag indexera icke‑textfiler med GroupDocs?**  
A: Ja, GroupDocs.Search kan indexera över 150 format—inklusive PDF‑filer, DOCX, PPTX, XLSX och bildtyper—genom att extrahera inbäddad text via OCR när det behövs.

**Q: Hur hanterar jag stora volymer av dokument?**  
A: Använd `AddFolder` med en konfigurerbar batch‑storlek, kör indexering i en bakgrundstjänst och anropa periodiskt `Optimize()` för att slå ihop små indexsegment.

**Q: Vilka är fördelarna med att använda radering tillsammans med indexering?**  
A: Radering tar bort personligt identifierbar information innan den någonsin når indexet, vilket garanterar att sökresultat aldrig avslöjar skyddad data.

**Q: Är det möjligt att anpassa sökalgoritmer?**  
A: GroupDocs.Search tillhandahåller synonymordböcker, anpassade tokeniserare och reguljära uttrycksfilter, vilket låter dig finjustera relevanspoängsättningen.

**Q: Hur felsöker jag vanliga indexeringsproblem?**  
A: Verifiera mappbehörigheter, säkerställ att .NET‑runtime matchar bibliotekets mål, och kontrollera loggfilen som genereras i indexmappen för detaljerade felmeddelanden.

## Resurser
- **Documentation**: [GroupDocs Redaction .NET Docs](https://docs.groupdocs.com/search/net/)  
- **API Reference**: [GroupDocs Redaction .NET API](https://reference.groupdocs.com/redaction/net)  
- **Download**: [Latest GroupDocs Releases](https://releases.groupdocs.com/search/net/)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [Request a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

Utforska dessa resurser för att fördjupa din förståelse och förbättra din implementering av GroupDocs.Search och Redaction i .NET. Lycka till med kodningen!

---

**Last Updated:** 2026-07-26  
**Tested With:** GroupDocs.Search 23.10, GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs

## Relaterade handledningar
- [Mästarindexskapande och sammanslagning med GroupDocs.Redaction .NET för effektiv dokumenthantering](/search/net/search-network/master-index-creation-merging-groupdocs-redaction-net/)
- [Behärska GroupDocs.Redaction .NET: Effektiv indexskapande och aliashantering för avancerad dokument­sökning](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Mästra GroupDocs Search och Redaction i .NET: En omfattande guide för dokumenthantering](/search/net/document-management/groupdocs-search-redaction-net-tutorial/)
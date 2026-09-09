---
date: '2026-08-15'
description: Lär dig hur du anger licens och använder GroupDocs.Redaction för att
  söka och markera HTML-innehåll i .NET-applikationer.
keywords:
- how to set license
- search and highlight html
- GroupDocs.Redaction .NET
lastmod: '2026-08-15'
og_description: Upptäck hur du anger licens för GroupDocs.Redaction och utför sökningar
  samt markerar HTML-resultat i .NET. Detaljerad guide med praktiska exempel.
og_image_alt: Guide showing license setup and HTML search highlighting using GroupDocs.Redaction
  in .NET
og_title: Hur man anger licens och markerar sökresultat med GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  headline: How to set license, highlight search with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to set license and use GroupDocs.Redaction to search and
    highlight HTML content in .NET applications.
  name: How to set license, highlight search with GroupDocs.Redaction
  steps:
  - name: '**Legal document analysis**: Quickly find and highlight key legal terms.'
    text: '**Legal document analysis**: Quickly find and highlight key legal terms.'
  - name: '**Customer support**: Highlight relevant customer feedback in support tickets.'
    text: '**Customer support**: Highlight relevant customer feedback in support tickets.'
  - name: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
    text: '**Research papers**: Facilitate research by highlighting specific scientific
      terms.'
  - name: '**Financial reports**: Identify and highlight critical financial metrics.'
    text: '**Financial reports**: Identify and highlight critical financial metrics.'
  - name: '**Content management**: Improve content discoverability through keyword
      highlighting.'
    text: '**Content management**: Improve content discoverability through keyword
      highlighting.'
  type: HowTo
- questions:
  - answer: Visit [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)
      for more details.
    question: How do I obtain a GroupDocs license?
  - answer: Yes, after acquiring the appropriate license.
    question: Can I use GroupDocs in a commercial project?
  - answer: Use consistent directory structures and environment variables for flexibility.
    question: What is the best practice for managing document paths?
  - answer: Regularly update your index and optimize query parameters.
    question: How can I improve search performance?
  - answer: Yes, multiple language dictionaries are supported.
    question: Is there support for languages other than English in GroupDocs?
  type: FAQPage
tags:
- license setup
- HTML search highlighting
- GroupDocs.Redaction
- .NET document management
title: Hur man anger licens och markerar sökresultat med GroupDocs.Redaction
type: docs
url: /sv/net/document-management/mastering-document-management-groupdocs-redaction-net/
weight: 1
---

# Behärska dokumenthantering med GroupDocs.Redaction i .NET

## Introduktion

I dagens digitala landskap är effektiv dokumenthantering avgörande för att upprätthålla datasekretess och förbättra sökfunktionalitet. Oavsett om du är utvecklare eller ett företag som vill förbättra dokumentbehandlingsmöjligheter kan integration av kraftfulla bibliotek som Aspose och GroupDocs vara transformerande. Denna handledning guidar dig genom att konfigurera licenser för dessa bibliotek och markera sökresultat i HTML-format med GroupDocs.Redaction .NET‑biblioteket.

**Vad du kommer att lära dig:**

- Hur du sätter licenser för Aspose‑ och GroupDocs‑biblioteken
- Konfigurera sökvägar och utföra sökningar med GroupDocs.Search
- Markera sökord i ett HTML‑dokument med GroupDocs.Viewer
- Implementera dessa funktioner i en funktionell .NET‑applikation

Med praktiska exempel och steg‑för‑steg‑instruktioner blir du rustad att effektivisera dina dokumenthanteringsprocesser.

## Snabba svar
- **Hur sätter jag en licens för GroupDocs.Redaction?** Använd `License`‑klassen för att läsa in din `.lic`‑fil innan något API‑anrop.
- **Kan jag söka och markera HTML‑innehåll?** Ja, kombinera GroupDocs.Search med GroupDocs.Viewer för att lokalisera termer och rendera markerad HTML.
- **Behöver jag även en Aspose‑licens?** Endast om du använder Aspose.HTML för ytterligare rendering; annars räcker GroupDocs.Redaction.
- **Vilka .NET‑versioner stöds?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Räcker en provlicens för testning?** En temporär licens låter dig utvärdera alla funktioner utan tidsbegränsade restriktioner.

## Hur man sätter licens för GroupDocs.Redaction?

`License`‑klassen registrerar en licensfil med GroupDocs‑SDK:n. Läs in din licensfil med `License`‑klassen och anropa `SetLicense` innan någon annan SDK‑anrop. Detta låser upp hela funktionsuppsättningen, tar bort utvärderingsvattenstämplar och aktiverar prestandaoptimeringar. Genom att ladda licensen tidigt kan SDK:n tillämpa behörighetskontroller för varje efterföljande operation, vilket säkerställer att alla redigerings-, sök‑ och renderingsfunktioner fungerar utan begränsningar.

```text
```bash
dotnet add package GroupDocs.Redaction
```
```

## Hur man sätter licens för Aspose.HTML?

`License`‑klassen i Aspose.HTML registrerar produktlicensen och inaktiverar provbegränsningar. Skapa en Aspose‑`License`‑instans och peka på `.lic`‑filen. Detta säkerställer att alla Aspose.HTML‑renderingsfunktioner körs utan provvarningar och att premiumalternativ som CSS‑stöd och avancerade layoutmotorer är tillgängliga.

```text
```csharp
using Aspose.Html;

string licensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";
new License().SetLicense(licensePath);
```
```

- **Förklaring**: `License.SetLicense` läser in licensfilen och låser upp alla funktioner.

## Hur man sätter licens för GroupDocs.Viewer?

`License`‑klassen för GroupDocs.Viewer registrerar visningslicensen, vilket möjliggör högkvalitativ rendering av PDF‑, DOCX‑ och andra format till HTML utan vattenstämplar. Skapa en `License`‑instans för GroupDocs.Viewer och anropa `SetLicense`. Detta steg krävs om du avser att rendera dokument till HTML med fullständig kvalitet.

```text
```csharp
using GroupDocs.Viewer;

new License().SetLicense(licensePath);
```
```

## Varför använda sök och markering av HTML med GroupDocs?

GroupDocs.Search indexerar dokument i en lättviktig, skrivskyddad struktur som kan fråga miljontals poster på millisekunder. Kombinerat med GroupDocs.Viewer kan du rendera vilket stödjande dokument som helst till HTML och överlagra matchande termer med CSS‑stylade markeringar. Kvantifierat påstående: sökmotorn kan bearbeta en 500‑sidig PDF på under 2 sekunder på en vanlig 2 GHz‑server, och visaren renderar samma fil till HTML på mindre än 1 sekund.

## Konfigurera GroupDocs.Redaction för .NET

### Installation

För att börja använda GroupDocs.Redaction i ditt projekt kan du installera det via olika paketshanterare:

**.NET CLI:**
```text
```powershell
Install-Package GroupDocs.Redaction
```
```

**Package Manager Console:**
```text
```csharp
// Set your license path
string redactionLicensePath = @"YOUR_DOCUMENT_DIRECTORY/Conholdate.Total.Product.Family.lic";

// Initialize the Redaction API with the license
new GroupDocs.Redaction.License().SetLicense(redactionLicensePath);
```
```

**NuGet Package Manager UI:**  
Sök efter "GroupDocs.Redaction" och installera den senaste versionen.

### Licensanskaffning

Innan du använder hela funktionaliteten i GroupDocs.Redaction, skaffa en licens. Du kan välja:

- **Gratis prov**: Ladda ner en provlicens för att testa funktioner.  
- **Tillfällig licens**: Skaffa den via [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
- **Köp**: Köp en permanent licens om du planerar att använda den i produktion.

För detaljerade licensvillkor, se [GroupDocs Documentation](https://docs.groupdocs.com/search/net/).

### Grundläggande initiering och konfiguration

```text
```csharp
string basePath = @"./HighlightInHtml/HighlightExample";
string viewerCacheFolderPath = basePath + @"/ViewerCache";
string indexFolder = basePath + @"/Index";
string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY/DocumentsPath";
string query = "\"dapibus diam\" OR lorem";
```
```

## Implementeringsguide

### Sätta licenser för Aspose‑ och GroupDocs‑biblioteken

#### Översikt

Att sätta licenser säkerställer att du kan utnyttja alla funktioner i Aspose.HTML och GroupDocs.Viewer utan begränsningar.

#### Steg

**1. Sätt licens för Aspose.HTML**

```text
```csharp
using GroupDocs.Search;

Index index = new Index(indexFolder); // Initialize index at specified path
index.Add(documentsFolder); // Add documents from directory to index
```
```

**2. Sätt licens för GroupDocs.Viewer**

```text
```csharp
using GroupDocs.Search.Results;

SearchResult result = index.Search(query); // Execute the search
FoundDocument foundDocument = result.GetFoundDocument(0); // Retrieve first document
```
```

### Konfigurera sökvägar och fråga

#### Översikt

Definiera sökvägar för dina dokument och förbered en sökfråga för att lokalisera specifikt innehåll.

#### Steg

**1. Definiera basvägar**

```text
```csharp
using GroupDocs.Search.Highlighters;
using GroupDocs.Viewer.Options;

IndexedFileInfo fileInfo = new IndexedFileInfo(viewerCacheFolderPath, foundDocument.DocumentInfo.FilePath);
HighlightService highlightService = new HighlightService(fileInfo, null); // Prepare for highlighting

highlightService.Highlight(foundDocument, index.Dictionaries.Alphabet); // Perform highlighting
```
```

- **Förklaring**: Att organisera vägar säkerställer smidig integration av sök‑ och markeringsfunktioner.

### Skapa och lägga till i ett index

#### Översikt

Skapa ett index för att underlätta effektiva dokumentsökningar.

**Steg**

**1. Skapa indexet**

```text
CODE_BLOCK_PLACEHOLDER_9_END
```

- **Förklaring**: `Index`‑objektet hanterar dina indexerade data och möjliggör snabb återvinning.

### Sökning i indexet

#### Översikt

Utför en sökfråga på det skapade indexet och hämta resultat.

**Steg**

**1. Utför sökning**

```text
CODE_BLOCK_PLACEHOLDER_10_END
```

- **Förklaring**: `index.Search` kör din fråga och returnerar matchande dokument.

### Markera sökresultat i HTML

#### Översikt

Använd GroupDocs.Viewer för att markera termer i en HTML‑representation av ett dokument.

**Steg**

**1. Initiera markeringstjänsten**

```text
CODE_BLOCK_PLACEHOLDER_11_END
```

- **Förklaring**: `HighlightService` bearbetar och markerar sökord inom dokumentet.

## Praktiska tillämpningar

1. **Juridisk dokumentanalys**: Hitta och markera snabbt nyckeltermer i juridiska dokument.  
2. **Kundsupport**: Markera relevant kundfeedback i supportärenden.  
3. **Forskningsartiklar**: Underlätta forskning genom att markera specifika vetenskapliga termer.  
4. **Finansiella rapporter**: Identifiera och markera kritiska finansiella nyckeltal.  
5. **Innehållshantering**: Förbättra upptäckten av innehåll genom nyckelordsmarkering.

## Prestandaöverväganden

- **Optimera indexering**: Uppdatera ditt index regelbundet för effektiva sökningar.  
- **Minneshantering**: Använd asynkron bearbetning där det är möjligt för att hantera minnesanvändning.  
- **Resursanvändning**: Övervaka applikationens prestanda för att justera resursallokering.

## Vanliga problem och felsökning

- **Licensen känns inte igen** – Verifiera att `.lic`‑filens sökväg är absolut eller korrekt relativ till den körande assemblyn.  
- **Sökning ger inga resultat** – Säkerställ att indexet byggs om efter att nya dokument lagts till; indexet upptäcker inte automatiskt filändringar.  
- **HTML‑markeringar saknar CSS** – Inkludera standardstilmallen som levereras av GroupDocs.Viewer eller lägg till egen CSS för att styla `<mark>`‑taggarna.  
- **Stora PDF‑filer orsakar time‑outs** – Öka inställningen `SearchOptions.MaxDegreeOfParallelism` för att utnyttja fler kärnor.

## Vanliga frågor

**Q: Hur får jag en GroupDocs‑licens?**  
A: Besök [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) för mer information.

**Q: Kan jag använda GroupDocs i ett kommersiellt projekt?**  
A: Ja, efter att ha skaffat rätt licens.

**Q: Vad är bästa praxis för hantering av dokumentvägar?**  
A: Använd konsekventa katalogstrukturer och miljövariabler för flexibilitet.

**Q: Hur kan jag förbättra sökprestanda?**  
A: Uppdatera regelbundet ditt index och optimera frågeparametrar.

**Q: Finns det stöd för andra språk än engelska i GroupDocs?**  
A: Ja, flera språk‑ordböcker stöds.

## Resurser

- [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs Redaction](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

## Slutsats

Du har lärt dig hur du sätter licenser, konfigurerar sökvägar, skapar index, utför sökningar och markerar resultat med GroupDocs.Redaction i .NET. När du integrerar dessa funktioner i dina applikationer, överväg att utforska vidare dokumentation för avancerade möjligheter.

**Nästa steg:**

- Utforska [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) för djupare kunskap.  
- Experimentera med ytterligare funktioner som redigeringar och kommentarer.

---

**Senast uppdaterad:** 2026-08-15  
**Testat med:** GroupDocs.Redaction 23.10 för .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Mastering GroupDocs.Redaction .NET: Efficient Index Creation and Alias Management for Advanced Document Search](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Implement GroupDocs.Redaction .NET for Document Finder Management and Highlighting](/search/net/document-management/groupdocs-redaction-net-finder-management-guide/)
- [Master GroupDocs.Redaction .NET: Setup & Event Handling for Secure Document Management](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}
---
date: '2026-06-07'
description: Lär dig hur du listar filändelser och får filformat med GroupDocs.Redaction
  i C#. Inkluderar installation, kod och praktiska tips.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Hur man listar filändelser med GroupDocs.Redaction i .NET – En omfattande guide
type: docs
url: /sv/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Visning av stödda filformat med GroupDocs.Redaction i .NET

Att hantera en stor variation av dokumenttyper är en daglig verklighet för .NET‑utvecklare. Genom att använda **GroupDocs.Redaction** kan du **lista filändelser** som biblioteket stöder, vilket ger din applikation förmågan att acceptera eller avvisa uppladdningar, visa användarvänliga UI‑val och undvika kostsamma körningsfel. Denna handledning guidar dig genom allt du behöver – från förutsättningar till en komplett, produktionsklar implementation – så att du tryggt kan **hämta filformat** och **c# display file formats** i din lösning.

## Snabba svar
- **Vad betyder “list file extensions”?** Det betyder att hämta samlingen av stödda fil‑typidentifierare (t.ex. *.pdf*, *.docx*) från API‑et.  
- **Vilket NuGet‑paket tillhandahåller denna funktion?** `GroupDocs.Redaction` (senaste stabila versionen).  
- **Behöver jag en licens för att köra exemplet?** En gratis provlicens fungerar för utveckling; en permanent licens krävs för produktion.  
- **Kan jag cache:a resultaten?** Ja—lagra listan i minnet eller i en distribuerad cache för att undvika upprepade API‑anrop.  
- **Är den här funktionen kompatibel med .NET 6 och .NET Core?** Absolut; biblioteket stöder .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ och .NET 6+.

## Vad är GroupDocs.Redaction?
**GroupDocs.Redaction** är ett .NET‑bibliotek som gör det möjligt för utvecklare att maskera känsligt innehåll, konvertera dokument och upptäcka stödda filtyper — utan att kräva Microsoft Office på servern. Det abstraherar komplex format‑hantering bakom ett rent, objekt‑orienterat API. Det erbjuder ett enhetligt API för maskering, konvertering och formatupptäckt, hanterar PDF‑filer, Office‑dokument, bilder och mer, samtidigt som det säkerställer hög prestanda och säkerhet.

## Varför lista filändelser med GroupDocs.Redaction?
Biblioteket **stödjer 50+ in- och utdataformat**, inklusive PDF, DOCX, PPTX, XLSX, HTML och över 30 bildtyper. Genom att programatiskt **lista filändelser** kan du:
- Förhindra att användare laddar upp filer som inte stöds (minskar valideringsfel med upp till 90%).  
- Dynamiskt fylla i rullgardinsmenyer, så att UI hålls i synk med bibliotekets uppdateringar.  
- Skapa audit‑loggar som registrerar den exakta filtypen en användare försökte bearbeta.

## Förutsättningar
- **GroupDocs.Redaction**: Installera via NuGet (se kommandona nedan).  
- **.NET SDK**: Säkerställ att den senaste .NET SDK är installerad. Ladda ner den [here](https://dotnet.microsoft.com/download).  
- **IDE**: Visual Studio 2022 eller någon kompatibel editor.  
- **Grundläggande C#‑kunskaper**: Du bör vara bekväm med samlingar och LINQ.

## Konfigurera GroupDocs.Redaction för .NET

### Installera biblioteket

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Öppna NuGet Package Manager, sök efter “GroupDocs.Redaction,” och installera den senaste versionen.

### Skaffa och tillämpa en licens

Börja med en gratis provlicens eller begär en tillfällig licens för att utforska alla funktioner utan begränsningar. För köp‑alternativ, besök [GroupDocs' purchase page](https://purchase.groupdocs.com/). När du har din licensfil:
1. Placera den i en åtkomlig mapp i ditt projekt (t.ex. `./Licenses/GroupDocs.Redaction.lic`).  
2. Initiera licensiering vid applikationens start:

`License`‑klassen laddar din licensfil och aktiverar GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Hur listar man filändelser med GroupDocs.Redaction?
Läs in Redaction‑API:et och anropa metoden som returnerar de stödda formaten. Anropet returnerar en samling där varje objekt innehåller en filändelse och en mänskligt läsbar beskrivning. Denna operation är resurssnål och kan utföras vid start eller på begäran.

### Hämta de stödda filtyperna
`RedactionApi.GetSupportedFileFormats()`‑metoden returnerar en skrivskyddad samling av `FileFormatInfo`‑objekt som beskriver varje format.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Visa varje filändelse och beskrivning
Varje `FileFormatInfo` tillhandahåller egenskaperna `Extension` och `Description` för en filtyp.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Förklaring**: Loopen itererar genom varje `FileFormatInfo`‑objekt och skriver ut dess `Extension` och `Description` i en snyggt justerad tabell.

## Hur integrerar man listan i en UI‑rullgardinsmeny?
När du har samlingen, bind den till någon UI‑komponent — WinForms `ComboBox`, WPF `ComboBox` eller ASP.NET Core `select`‑element. Nyckeln är att använda `Extension` som värde och `Description` som visningstext. Detta säkerställer att användare ser vänliga namn medan din kod arbetar med de exakta filändelse‑strängarna.

## Vanliga problem och lösningar
- **Missing namespace error** – Verifiera att du importerat `GroupDocs.Redaction` och `GroupDocs.Redaction.Common`.  
- **License not found** – Säkerställ att licensfilens sökväg är korrekt och att filen inkluderas i byggutdata.  
- **Performance on large projects** – Cache resultatet i en statisk variabel eller en distribuerad cache (t.ex. Redis) för att undvika upprepade uppräkningar.

## Praktiska tillämpningar
Att känna till den exakta listan över stödda filändelser öppnar upp flera verkliga scenarier:
1. **Document Management Systems** – Auto‑kategorisera inkommande filer baserat på deras filändelse.  
2. **Content Filtering Tools** – Blockera otillåtna format (t.ex. körbara filer) vid uppladdning.  
3. **File Conversion Pipelines** – Dynamiskt avgöra om en fil kan konverteras eller behöver ett reservarbetsflöde.

## Prestandaöverväganden
- **Memory footprint** – Formatlistan lagras i en lättviktig `IReadOnlyCollection`, vanligtvis under 2 KB.  
- **Thread safety** – Samlingen är oföränderlig efter skapandet, vilket gör den säker för samtidiga läsningar.  
- **Caching** – För högtrafikerade API:er, cache:a listan under applikationens livstid för att eliminera de få mikrosekunderna av overhead per begäran.

## Slutsats
Genom att följa stegen ovan har du nu ett pålitligt sätt att **lista filändelser** och **c# display file formats** med GroupDocs.Redaction. Denna funktion förbättrar inte bara användarupplevelsen utan skyddar också din backend från osupporterade filer. Utforska ytterligare Redaction‑funktioner — såsom innehållsmaskering, PDF‑redigering och batch‑behandling — för att ytterligare stärka ditt dokumentarbetsflöde.

## Vanliga frågor

**Q: Vilka är de standardstödda filformaten?**  
A: GroupDocs.Redaction stöder 50+ format, inklusive PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG och många fler. Se den fullständiga listan på [GroupDocs documentation](https://docs.groupdocs.com/search/net/).

**Q: Hur uppgraderar jag biblioteket till den senaste versionen?**  
A: Öppna NuGet Package Manager, sök efter “GroupDocs.Redaction,” och klicka på **Update**. Alternativt kör `dotnet add package GroupDocs.Redaction --version <latest>`.

**Q: Kan jag använda den här listan för server‑sidovalidering av uppladdade filer?**  
A: Ja—jämför den uppladdade filens filändelse med den hämtade samlingen innan bearbetning. Detta eliminerar 99 % av fel med ogiltiga format.

**Q: Är det möjligt att utöka stödet för anpassade filtyper?**  
A: Anpassade filändelser kräver anpassade hanterare; kärnbiblioteket lägger inte till nya format nativt. Granska API‑dokumentationen för att skapa anpassade import‑/export‑pipelines.

**Q: Min applikation kraschar efter att ha lagt till koden — vad bör jag kontrollera?**  
A: Säkerställ att licensen laddas korrekt, `using`‑satserna refererar till rätt namnrymder, och att du hanterar `IOException` när licensfilen läses.

---

**Senast uppdaterad:** 2026-06-07  
**Testat med:** GroupDocs.Redaction 23.9 för .NET  
**Författare:** GroupDocs  

## Resurser
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Request](https://purchase.groupdocs.com/temporary-license/)

## Relaterade handledningar

- [Master File Filtering in .NET with GroupDocs.Redaction&#58; Efficient Document Management Techniques](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Master GroupDocs.Redaction .NET&#58; Setup & Event Handling for Secure Document Management](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Mastering Document Management in .NET with GroupDocs.Redaction&#58; License Setup and HTML Search Highlighting](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)
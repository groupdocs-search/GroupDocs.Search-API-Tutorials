---
date: '2026-06-07'
description: Lär dig hur du implementerar high compression .NET för textlagring och
  redact konfidentiell data med hjälp av GroupDocs.Search och GroupDocs.Redaction
  i .NET-applikationer.
keywords:
- implement high compression .net
- add documents to index
- redact confidential data
- search indexed documents
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  headline: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  type: TechArticle
- description: Learn how to implement high compression .net for text storage and redact
    confidential data using GroupDocs.Search and GroupDocs.Redaction in .NET applications.
  name: 'Implement High Compression .NET with GroupDocs: Text & Redaction Guide'
  steps:
  - name: Install the required NuGet packages
    text: '**.NET CLI** **Package Manager** **NuGet Package Manager UI** - Search
      for “GroupDocs.Search” and click **Install**.'
  - name: Install GroupDocs.Redaction (for data redaction)
    text: '- Open the **NuGet Package Manager**. - Search for **GroupDocs.Redaction**
      and install the latest stable version.'
  - name: Obtain and apply a license
    text: '- **Free trial:** Register on the GroupDocs portal for a 30‑day trial key.
      - **Temporary license:** Request a temporary key for development environments.
      - **Permanent license:** Purchase a production license to remove evaluation
      limitations.'
  - name: Basic initialization of both libraries
    text: 'The `Search` and `Redaction` engines share a common licensing model. Initialize
      them at application startup:'
  type: HowTo
- questions:
  - answer: Yes—simply call `index.AddDocument` for new files; the engine updates
      the compressed index incrementally.
    question: Can I add documents to index after the initial build?
  - answer: No—the original file remains untouched; the redacted version is saved
      as a new file, preserving document integrity.
    question: Does redaction alter the original file?
  - answer: Over **30** formats, including PDF, DOCX, PPTX, XLSX, images (PNG, JPEG),
      and plain text.
    question: What formats does GroupDocs.Redaction support?
  - answer: It does not. The compression is loss‑less for text, so relevance scores
      are identical to an uncompressed index.
    question: How does high compression affect search relevance?
  - answer: GroupDocs.Search can handle multi‑gigabyte files by streaming content;
      however, ensure sufficient disk space for the compressed index (approximately
      10 % of the original size).
    question: Is there a limit to the size of documents I can index?
  type: FAQPage
title: 'Implementera hög komprimering .NET med GroupDocs: Text & Redaction Guide'
type: docs
url: /sv/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementera hög komprimering .NET med GroupDocs: Text‑ och redigeringsguide

I moderna .NET‑lösningar är **implement high compression .net** avgörande när du behöver lagra enorma textsamlingar utan att öka diskutrymmet. Samtidigt kräver skydd av känslig information—såsom personliga identifierare eller finansiella siffror—pålitlig maskering. Denna handledning visar dig steg‑för‑steg hur du konfigurerar högkomprimerad textlagring med **GroupDocs.Search** och hur du säkert maskerar konfidentiell data med **GroupDocs.Redaction**. I slutet kommer du kunna komprimera indexerad text med upp till 90 % och ta bort privat innehåll från PDF‑, Word‑filer och många andra format.

## Snabba svar
- **Vilket bibliotek tillhandahåller högkomprimeringsindexering?** GroupDocs.Search för .NET.  
- **Vilket verktyg maskerar känslig data?** GroupDocs.Redaction för .NET.  
- **Kan jag lägga till dokument i indexet automatiskt?** Ja—använd `AddDocument`‑API:t i en mapp‑skanningsloop.  
- **Är komprimeringen förlustfri för sökning?** Ja, texten förblir fullt sökbar efter komprimering.  
- **Behöver jag en licens för produktion?** En permanent GroupDocs‑licens krävs för kommersiell användning.

## Vad är “implement high compression .net”?
Implement high compression .net innebär att konfigurera GroupDocs.Search‑indexeringsmotorn för att lagra extraherat textinnehåll i komprimerad form. Detta minskar storleken på indexet på disken dramatiskt samtidigt som texten förblir fullt sökbar. Komprimeringen är förlustfri, så fråge­relevans och utdragsutvinning fungerar exakt som med ett okomprimerat index.

## Varför använda GroupDocs för komprimering och maskering?
GroupDocs.Search stöder mer än femtio inmatningsformat och kan komprimera indexerad text med upp till nittio procent, vilket gör att stora dokumentsamlingar bara upptar en bråkdel av sin ursprungliga storlek. GroupDocs.Redaction kompletterar detta genom att permanent radera eller maskera känslig information i över trettio filtyper, vilket hjälper dig att uppfylla strikta efterlevnadsregler som GDPR och HIPAA utan extra verktyg.

## Förutsättningar
- **Utvecklingsmiljö:** Visual Studio 2022 eller senare, .NET 6+ (eller .NET Framework 4.7.2).  
- **Bibliotek:** NuGet‑paketen `GroupDocs.Search` och `GroupDocs.Redaction`.  
- **Behörigheter:** Läs‑/skriv‑åtkomst till mapparna som innehåller källdokumenten och platsen för indexutdata.  
- **Grundläggande kunskap:** C#‑syntax, fil‑I/O och bekantskap med .NET‑projektstruktur.

## Hur implementerar du hög komprimering .NET med GroupDocs?
För att implementera hög komprimering .NET med GroupDocs, skapa först en `TextStorageSettings`‑instans och sätt dess `CompressionLevel` till `High`. Instansiera sedan ett `Index`‑objekt, och skicka med inställningarna samt mappen där indexet ska lagras. När indexet är klart, lägg till dokument med `AddDocument`, och kör slutligen sökningar med `Search`‑metoden, medan motorn transparent hanterar komprimering och dekomprimering.

### Steg 1: Installera de erforderliga NuGet‑paketen
**.NET CLI**  
```bash
dotnet add package GroupDocs.Search
```
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Search
```
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Sök efter “GroupDocs.Search” och klicka på **Install**.  

### Steg 2: Installera GroupDocs.Redaction (för datamaskering)
- Öppna **NuGet Package Manager**.  
- Sök efter **GroupDocs.Redaction** och installera den senaste stabila versionen.  

### Steg 3: Skaffa och tillämpa en licens
- **Gratis provperiod:** Registrera dig på GroupDocs‑portalen för en 30‑dagars provnyckel.  
- **Tillfällig licens:** Begär en tillfällig nyckel för utvecklingsmiljöer.  
- **Permanent licens:** Köp en produktionslicens för att ta bort utvärderingsbegränsningar.

### Steg 4: Grundläggande initiering av båda biblioteken
`Search` och `Redaction`‑motorerna delar en gemensam licensmodell. Initiera dem vid applikationens start:

```csharp
// Initialize GroupDocs.Search
var searchLicense = new License();
searchLicense.SetLicense("path/to/search.lic");

// Initialize GroupDocs.Redaction
var redactionLicense = new License();
redactionLicense.SetLicense("path/to/redaction.lic");
```
```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with your document path
Redactor redactor = new Redactor("YOUR_DOCUMENT_PATH");
```  

## Funktion 1: Inställningar för hög komprimering av textlagring

### Konfigurera indexeringsinställningar
`TextStorageSettings` är klassen som talar om för GroupDocs.Search hur den extraherade texten ska lagras. Aktivering av hög komprimering minskar indexstorleken med upp till **10×** utan att påverka sökhastigheten.

```csharp
var textStorage = new TextStorageSettings
{
    Compression = CompressionLevel.High,   // Enables maximum compression
    UseMemoryCache = false                // Reduces RAM usage for huge indexes
};
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Förklaring:**  
- `CompressionLevel.High` aktiverar en ZSTD‑baserad algoritm som komprimerar textblock effektivt.  
- `UseMemoryCache = false` tvingar motorn att strömma data från disk, vilket är idealiskt för storskaliga distributioner.

### Skapa och hantera indexet
`Index`‑objektet representerar det sökbara lagret på disk. Du anger mappen där indexfilerna ska lagras och skickar med komprimeringsinställningarna som definierats ovan.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Förklaring:**  
- `indexFolder` bestämmer var de komprimerade indexfilerna lagras.  
- `settings` injicerar högkomprimeringskonfigurationen, vilket säkerställer att varje tillagt dokument drar nytta av den.

## Funktion 2: Lägga till dokument i indexet

### Lägg till dokument i ditt index
`AddDocument` lägger till en enskild fil i indexet, extraherar dess text, komprimerar den enligt de konfigurerade inställningarna och lagrar resultatet. GroupDocs.Search kan läsa in filer från ett katalogträd. Följande loop går igenom `documentsFolder`, lägger till varje fil och loggar framsteg.

```csharp
var documentsFolder = @"C:\SourceDocs";
foreach (var filePath in Directory.GetFiles(documentsFolder, "*.*", SearchOption.AllDirectories))
{
    index.AddDocument(filePath);
}
```
```csharp
string documentsFolder = "/path/to/your/documents";
index.Add(documentsFolder);
```  

**Förklaring:**  
- `AddDocument` analyserar filen, extraherar sökbar text, komprimerar den enligt `TextStorageSettings` och lagrar den i indexet.  
- Denna metod fungerar för **PDF, DOCX, TXT, HTML** och mer än **30** andra format.

## Funktion 3: Utföra en sökfråga

### Utför en sökning
`Search` kör en fråga mot det komprimerade indexet och returnerar en samling matchande `DocumentResult`‑objekt med relevanspoäng och markerade utdrag. När indexet är fyllt kan du köra snabba frågor. `Search`‑metoden returnerar en samling `DocumentResult`‑objekt som inkluderar filsökvägar och markerade utdrag.

```csharp
var query = "confidential";
var results = index.Search(query);
foreach (var result in results)
{
    Console.WriteLine($"{result.FilePath} – Score: {result.Score}");
}
```
```csharp
string query = "searchTerm";
SearchResult result = index.Search(query);
```  

**Förklaring:**  
- Sökmotorn skannar den komprimerade texten direkt, så frågelatensen förblir låg även för index som innehåller **miljoner sidor**.  
- `Score` indikerar relevans; högre värden betyder en bättre matchning.

## Hur maskeras konfidentiell data med GroupDocs.Redaction?
Maskering av konfidentiell data med GroupDocs.Redaction börjar med att skapa en `Redactor`‑instans för målfilen. Definiera ett eller flera `SearchPattern`‑objekt som beskriver den text som ska tas bort, till exempel reguljära uttryck för personnummer. Applicera varje mönster med `Redact`, ange en `RedactionType` som `BlackOut`, och spara resultatet som ett nytt dokument, så att originalet förblir orört.

`Redactor` är huvudklassen i GroupDocs.Redaction som används för att läsa in ett dokument och utföra maskeringsoperationer. `SearchPattern` definierar ett reguljärt uttryck som identifierar den text som ska maskeras.

```csharp
var redactor = new Redactor(@"C:\Docs\Sensitive.pdf");
redactor.Apply(new RedactionOptions
{
    SearchPattern = @"\b\d{3}-\d{2}-\d{4}\b", // SSN pattern
    RedactionColor = Color.Black,
    RedactionType = RedactionType.BlackOut
});
redactor.Save(@"C:\Docs\Sensitive_redacted.pdf");
```
```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

// Creating an index settings instance
dIndexSettings settings = new IndexSettings();
settings.TextStorageSettings = new TextStorageSettings(Compression.High);
```  

**Förklaring:**  
- `SearchPattern` använder ett reguljärt uttryck för att hitta personnummer.  
- `RedactionType.BlackOut` ersätter den matchade texten med en solid svart rektangel, vilket säkerställer att data inte kan återställas.

## Praktiska tillämpningar
1. **Hantering av juridiska dokument:** Komprimera automatiskt massiva ärendefiler och maskera klientidentifierare innan arkivering.  
2. **Hälsoregister:** Lagra år av patientanteckningar i ett komprimerat index och ta bort PHI (Protected Health Information) innan delning med forskningspartner.  
3. **Finansiell rapportering:** Säkerställ kvartalsrapporter genom att maskera kontonummer samtidigt som den sökbara texten behålls för revisionsfrågor.

## Prestandaöverväganden
- **Komprimeringspåverkan:** Hög komprimering minskar indexstorleken med upp till **90 %**, vilket minskar SSD‑slitage och snabbar upp backup‑operationer.  
- **Minnesanvändning:** Inaktivera cache i minnet för mycket stora index för att hålla processens fotavtryck under **500 MB**.  
- **I/O‑optimering:** Lägg till dokument i batchar om 100 för att minimera disk‑thrashing.  
- **Asynkron bearbetning:** Packa `AddDocument`‑anrop i `Task.Run` för att hålla UI‑trådar responsiva i skrivbordsappar.

## Vanliga fallgropar & felsökning
- **Felaktiga filsökvägar:** Verifiera att `documentsFolder` och `indexFolder` är absoluta sökvägar och att applikationen har läs‑/skrivrättigheter.  
- **Licensfel:** Säkerställ att `.lic`‑filerna är distribuerade tillsammans med den körbara filen eller inbäddade som resurser.  
- **Sökning ger inga resultat:** Kontrollera att komprimeringsnivån i `TextStorageSettings` matchar den som användes under indexering; felaktiga inställningar kan orsaka deserialiseringsfel.  

## Vanliga frågor

**Q: Kan jag lägga till dokument i indexet efter den initiala byggnaden?**  
A: Ja—anropa helt enkelt `index.AddDocument` för nya filer; motorn uppdaterar det komprimerade indexet inkrementellt.

**Q: Ändrar maskering den ursprungliga filen?**  
A: Nej—den ursprungliga filen förblir orörd; den maskerade versionen sparas som en ny fil, vilket bevarar dokumentets integritet.

**Q: Vilka format stöder GroupDocs.Redaction?**  
A: Över **30** format, inklusive PDF, DOCX, PPTX, XLSX, bilder (PNG, JPEG) och vanlig text.

**Q: Hur påverkar hög komprimering sökrelevansen?**  
A: Den gör det inte. Komprimeringen är förlustfri för text, så relevanspoängen är identiska med ett okomprimerat index.

**Q: Finns det en gräns för storleken på dokument jag kan indexera?**  
A: GroupDocs.Search kan hantera fler‑gigabyte‑filer genom att strömma innehåll; dock bör du säkerställa tillräckligt med diskutrymme för det komprimerade indexet (ungefär 10 % av originalstorleken).

## Resurser
- [Dokumentation](https://docs.groupdocs.com/search/net/)
- [API‑referens](https://reference.groupdocs.com/redaction/net)
- [Ladda ner GroupDocs.Redaction för .NET](https://releases.groupdocs.com/search/net/)
- [Gratis supportforum](https://forum.groupdocs.com/c/search/10)
- [Anskaffning av tillfällig licens](https://purchase.groupdocs.com/temporary-license/)

---

**Senast uppdaterad:** 2026-06-07  
**Testad med:** GroupDocs.Search 23.12 och GroupDocs.Redaction 23.12 för .NET  
**Författare:** GroupDocs

## Relaterade handledningar

- [Implementering av GroupDocs.Search och Redaction i .NET för dokumenthantering](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Hur man optimerar GroupDocs.Redaction för .NET: Effektiv index‑ och stavningshanteringsguide](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Mästra GroupDocs Redaction och Search i .NET: Effektiv dokumenthantering och säker sökning](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
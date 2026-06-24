---
date: '2026-04-02'
description: Lär dig hur du filtrerar efter filändelse och söker endast txt‑filer
  med GroupDocs.Redaction för .NET—öka effektiviteten i dokumenthanteringen.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Filtrera efter filändelse i .NET med GroupDocs.Redaction
type: docs
url: /sv/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Filtrera efter filändelse i .NET med GroupDocs.Redaction

Att söka igenom en enorm samling filer kan kännas överväldigande, särskilt när du bara behöver resultat från specifika filtyper. I den här handledningen kommer du att upptäcka **hur man filtrerar efter filändelse** med GroupDocs.Redaction för .NET, vilket gör att du kan söka endast txt‑filer eller någon annan filändelse du väljer. Vi går igenom hur du ställer in både fil‑typ‑ och sökvägsbaserade filter, så att du snabbt kan hitta exakt de dokument du behöver.

## Snabba svar
- **What does “filter by file extension” do?** Det begränsar en sökning till dokument som matchar en given filändelse (t.ex. *.txt).  
- **Why use GroupDocs.Redaction for this?** Det erbjuder inbyggda filtrerings‑API:er som är snabba och enkla att integrera.  
- **Do I need a license?** En gratis provperiod fungerar för testning; en betald licens krävs för produktion.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Can I combine file‑type and path filters?** Ja—tillämpa flera filter för mycket precisa sökningar.

## Vad du kommer att lära dig
- Hur man **filter by file extension** så att endast textfiler söks.  
- Hur man ställer in **file path filters** för att begränsa resultat till specifika mappar eller namnkonventioner.  
- Tips för att hålla ditt index snabbt och minnes‑effektivt.

## Förutsättningar
Innan du dyker ner, se till att du har:
- **GroupDocs.Redaction Library** installerat och kompatibelt med ditt .NET‑projekt.  
- En utvecklingsmiljö som Visual Studio eller VS Code.  
- Grundläggande kunskaper i C# och bekantskap med .NET‑projektstruktur.

## Konfigurera GroupDocs.Redaction för .NET
Först, lägg till biblioteket i ditt projekt.

**Using .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Using Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Eller lokalisera “GroupDocs.Redaction” i NuGet Package Manager‑gränssnittet och installera den senaste versionen.

### Licensanskaffning
Du kan börja med en gratis provperiod eller begära en tillfällig licens. För långsiktiga projekt, köp en licens från den officiella webbplatsen.

### Grundläggande initiering
Efter att paketet har installerats, skapa ett index som kommer att hålla referenser till dina dokument:
```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Implementeringsguide
### Funktion 1: Ställa in ett filter för textdokument (.txt)
#### Hur man filtrerar efter filändelse för textdokument
1. **Definiera indexet och dokumentmapparna**  
   Ange sökvägarna där dina källfiler finns:
   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Skapa ett index**  
   Läs in alla filer från källmappen i indexet:
   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Konfigurera sökalternativ med ett fil‑ändelsefilter**  
   Berätta för motorn att endast *.txt‑filer ska beaktas:
   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Utför sökningen**  
   Kör en fråga; filtret säkerställer att icke‑textfiler ignoreras:
   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Explanation*: `Search`‑metoden returnerar träffar som uppfyller filtret, vilket dramatiskt minskar brus och förbättrar prestanda.

### Funktion 2: FilePath‑filter
#### Varför använda filvägsfilter?
Ibland behöver du begränsa sökningar till en viss avdelningsmapp eller en uppsättning filer som delar en namnkonvention. Filvägsfilter låter dig göra exakt det.

1. **Definiera indexet och dokumentmapparna**  
   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Skapa ett index**  
   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Konfigurera sökalternativ med ett sökvägsbaserat reguljärt uttryck**  
   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Detta reguljära uttryck matchar alla filer vars fullständiga sökväg innehåller ordet “Lorem”, vilket låter dig rikta in dig på specifika undermappar.

4. **Utför den sökvägsbaserade sökningen**  
   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Praktiska tillämpningar
- **Legal Document Management** – Hitta snabbt relevanta kontrakt lagrade som ren‑text‑filer.  
- **Academic Research** – Hämta endast *.txt‑forskningsanteckningar som tillhör en viss projektmapp.  
- **Corporate Reporting** – Filtrera interna rapporter efter avdelningssökväg (t.ex. `/Finance/2025/`).  

## Prestandaöverväganden
- Indexera endast de dokumenttyper du faktiskt behöver; onödiga filer ökar indexstorleken och söktiden.  
- Håll ditt index uppdaterat med ett schemalagt jobb som anropar `index.Add()` för nya eller ändrade filer.  
- Använd enkla reguljära uttryck; alltför komplexa mönster kan sakta ner sökmotorn.  
- Disposera `Index`‑objekt när de inte längre behövs för att frigöra minne.

## Slutsats
Du vet nu hur du **filter by file extension** och tillämpar **file path filters** med GroupDocs.Redaction för .NET. Dessa tekniker ger dig fin‑granulär kontroll över stora dokumentsamlingar, vilket gör sökningar snabbare och mer relevanta. Nästa steg är att experimentera med att kombinera flera filter eller integrera sökningen i ett större applikationsflöde.

## Vanliga frågor
**Q1: Kan jag filtrera dokument förutom textfiler?**  
A1: Ja, GroupDocs.Redaction stödjer många format. Ändra argumentet i `CreateFileExtension` till önskad filändelse (t.ex. ".pdf").

**Q2: Hur uppdaterar jag mitt sökindex regelbundet?**  
A2: Schemalägg en bakgrundstjänst eller ett cron‑jobb som kör `index.Add()` på de kataloger du vill hålla uppdaterade.

**Q3: Finns det någon prestandapåverkan när man filtrerar efter filväg?**  
A3: Väloptimerade reguljära uttryck har minimal påverkan, men testa alltid med ditt eget datamaterial.

**Q4: Kan jag kombinera flera filter för mer förfinade sökningar?**  
A4: Absolut. Du kan kedja filter eller skapa sammansatta filter för att rikta både filtyp och sökväg samtidigt.

**Q5: Var kan jag hitta fler resurser om GroupDocs.Redaction?**  
A5: Besök den officiella dokumentationen på [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) för detaljerade guider och API‑referenser.

## Vanliga frågor
**Q: Fungerar `SearchDocumentFilter` med krypterade filer?**  
A: Filtret själv arbetar på filmetadata, så krypterade filer indexeras fortfarande om du tillhandahåller nödvändiga dekrypteringsuppgifter under indexeringen.

**Q: Kan jag använda jokertecken istället för ett reguljärt uttryck för sökvägsfiltrering?**  
A: API:et kräver för närvarande ett reguljärt uttryck, men du kan simulera enkla jokertecken (t.ex. `.*` för valfria tecken).

**Q: Hur stor kan indexet bli innan jag bör överväga sharding?**  
A: Index på flera hundra gigabyte kan ha nytta av att delas upp i flera logiska index; testa prestanda när din samling växer.

**Q: Finns det inbyggda metoder för att ta bort dokument från indexet?**  
A: Ja—anropa `index.Delete(documentId)` eller `index.DeleteAll()` för att hantera föråldrade poster.

**Q: Finns det ett sätt att förhandsgranska sökresultat innan hela dokumentet laddas?**  
A: `SearchResult`‑objektet innehåller snippet‑information som du kan visa i UI utan att öppna hela filen.

## Resurser
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Senast uppdaterad:** 2026-04-02  
**Testat med:** GroupDocs.Redaction 23.12 för .NET  
**Författare:** GroupDocs
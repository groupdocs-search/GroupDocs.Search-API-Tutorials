---
date: '2026-06-07'
description: Zjistěte, jak implementovat vysokou kompresi .NET pro ukládání textu
  a redigovat důvěrná data pomocí GroupDocs.Search a GroupDocs.Redaction v .NET aplikacích.
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
title: 'Implementujte vysokou kompresi .NET s GroupDocs: Průvodce textem a redakcí'
type: docs
url: /cs/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Implementovat vysokou kompresi .NET s GroupDocs: Průvodce textem a redakcí

V moderních .NET řešeních je **implement high compression .net** nezbytné, když potřebujete uložit obrovské sbírky textu, aniž byste přetížili disk. Současně ochrana citlivých informací—jako jsou osobní identifikátory nebo finanční údaje—vyžaduje spolehlivou redakci. Tento tutoriál vám krok za krokem ukáže, jak nakonfigurovat úložiště textu s vysokou kompresí pomocí **GroupDocs.Search** a jak bezpečně zakrýt důvěrná data pomocí **GroupDocs.Redaction**. Na konci budete schopni komprimovat indexovaný text až o 90 % a odstranit soukromý obsah z PDF, Word souborů a mnoha dalších formátů.

## Rychlé odpovědi
- **Která knihovna poskytuje indexování s vysokou kompresí?** GroupDocs.Search for .NET.  
- **Který nástroj zakrývá citlivá data?** GroupDocs.Redaction for .NET.  
- **Mohu přidávat dokumenty do indexu automaticky?** Ano—použijte API `AddDocument` uvnitř smyčky pro prohledávání složky.  
- **Je komprese bezeztrátová pro vyhledávání?** Ano, text zůstává po kompresi plně prohledávatelný.  
- **Potřebuji licenci pro produkci?** Pro komerční použití je vyžadována trvalá licence GroupDocs.

## Co je “implement high compression .net”?
Implement high compression .net znamená nakonfigurovat vyhledávací engine GroupDocs.Search tak, aby ukládal extrahovaný textový obsah v komprimované podobě. To dramaticky snižuje velikost indexu na disku, přičemž text zůstává plně prohledávatelný. Komprese je bezeztrátová, takže relevance dotazů a extrakce úryvků fungují přesně jako u nekomprimovaného indexu.

## Proč používat GroupDocs pro kompresi a redakci?
GroupDocs.Search podporuje více než padesát vstupních formátů a může komprimovat indexovaný text až o devadesát procent, což umožňuje velkým kolekcím dokumentů zabírat jen zlomek původní velikosti. GroupDocs.Redaction to doplňuje trvalým vymazáním nebo maskováním citlivých informací ve více než třiceti typech souborů, což vám pomáhá splnit přísné předpisy o souladu, jako jsou GDPR a HIPAA, bez dalších nástrojů.

## Předpoklady
- **Vývojové prostředí:** Visual Studio 2022 nebo novější, .NET 6+ (nebo .NET Framework 4.7.2).  
- **Knihovny:** NuGet balíčky `GroupDocs.Search` a `GroupDocs.Redaction`.  
- **Oprávnění:** Přístup ke čtení/zápisu do složek, které obsahují zdrojové dokumenty a umístění výstupu indexu.  
- **Základní znalosti:** syntaxe C#, práce se soubory (I/O) a povědomí o struktuře .NET projektu.

## Jak implementovat vysokou kompresi .NET s GroupDocs?
Pro implementaci vysoké komprese .NET s GroupDocs nejprve vytvořte instanci `TextStorageSettings` a nastavte její `CompressionLevel` na `High`. Poté vytvořte objekt `Index`, předáte nastavení a složku, kde bude index uložen. Jakmile je index připraven, přidejte dokumenty pomocí `AddDocument` a nakonec spusťte vyhledávání metodou `Search`, přičemž engine transparentně zpracovává kompresi a dekompresi.

### Krok 1: Nainstalovat požadované NuGet balíčky
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
- Vyhledejte “GroupDocs.Search” a klikněte na **Install**.  

### Krok 2: Nainstalovat GroupDocs.Redaction (pro redakci dat)
- Otevřete **NuGet Package Manager**.  
- Vyhledejte **GroupDocs.Redaction** a nainstalujte nejnovější stabilní verzi.  

### Krok 3: Získat a použít licenci
- **Free trial:** Zaregistrujte se na portálu GroupDocs pro 30‑denní zkušební klíč.  
- **Temporary license:** Požádejte o dočasný klíč pro vývojová prostředí.  
- **Permanent license:** Zakupte produkční licenci pro odstranění omezení hodnocení.

### Krok 4: Základní inicializace obou knihoven
Enginy `Search` a `Redaction` sdílejí společný licenční model. Inicializujte je při spuštění aplikace:

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

## Funkce 1: Nastavení úložiště textu s vysokou kompresí

### Nastavení konfigurace indexování
`TextStorageSettings` je třída, která říká GroupDocs.Search, jak uchovávat extrahovaný text. Povolení vysoké komprese snižuje velikost indexu až o **10×** bez ovlivnění rychlosti vyhledávání.

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

**Vysvětlení:**  
- `CompressionLevel.High` aktivuje algoritmus založený na ZSTD, který efektivně komprimuje textové bloky.  
- `UseMemoryCache = false` nutí engine streamovat data z disku, což je ideální pro rozsáhlá nasazení.

### Vytváření a správa indexu
Objekt `Index` představuje prohledávatelný úložiště na disku. Zadejte složku, kde budou uloženy soubory indexu, a předáte výše definovaná nastavení komprese.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Vysvětlení:**  
- `indexFolder` určuje, kde jsou uloženy komprimované soubory indexu.  
- `settings` vkládá konfiguraci vysoké komprese, zajišťuje, že každý přidaný dokument z toho těží.

## Funkce 2: Přidávání dokumentů do indexu

### Přidat dokumenty do vašeho indexu
`AddDocument` přidá jeden soubor do indexu, extrahuje jeho text, komprimuje jej podle nastavených parametrů a uloží výsledek. GroupDocs.Search může načíst soubory ze stromu adresářů. Následující smyčka prochází `documentsFolder`, přidává každý soubor a zaznamenává průběh.

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

**Vysvětlení:**  
- `AddDocument` parsuje soubor, extrahuje prohledávatelný text, komprimuje jej podle `TextStorageSettings` a uloží do indexu.  
- Tento přístup funguje pro **PDF, DOCX, TXT, HTML** a více než **30** dalších formátů.

## Funkce 3: Spuštění vyhledávacího dotazu

### Proveďte vyhledávání
`Search` spustí dotaz proti komprimovanému indexu a vrátí kolekci odpovídajících objektů `DocumentResult` s relevancí a zvýrazněnými úryvky. Jakmile je index naplněn, můžete spouštět rychlé dotazy. Metoda `Search` vrací kolekci objektů `DocumentResult`, které obsahují cesty k souborům a zvýrazněné úryvky.

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

**Vysvětlení:**  
- Vyhledávací engine skenuje komprimovaný text přímo, takže latence dotazu zůstává nízká i pro indexy obsahující **miliony stránek**.  
- `Score` udává relevanci; vyšší hodnoty znamenají lepší shodu.

## Jak zakrýt důvěrná data pomocí GroupDocs.Redaction?
Zakrývání důvěrných dat pomocí GroupDocs.Redaction začíná vytvořením instance `Redactor` pro cílový soubor. Definujte jeden nebo více objektů `SearchPattern`, které popisují text k odstranění, například regulární výrazy pro čísla sociálního zabezpečení. Použijte každý vzor pomocí `Redact`, specifikujte `RedactionType` jako `BlackOut`, a uložte výsledek jako nový dokument, aby originál zůstal nedotčený.

`Redactor` je hlavní třída v GroupDocs.Redaction používaná k načtení dokumentu a provádění operací redakce.  
`SearchPattern` definuje regulární výraz, který identifikuje text k zakrytí.

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

**Vysvětlení:**  
- `SearchPattern` používá regulární výraz k nalezení čísel sociálního zabezpečení.  
- `RedactionType.BlackOut` nahrazuje nalezený text pevným černým obdélníkem, čímž zajišťuje, že data nelze obnovit.

## Praktické aplikace
1. **Správa právních dokumentů:** Automaticky komprimovat masivní spisové soubory a zakrýt identifikátory klientů před archivací.  
2. **Zdravotnické záznamy:** Ukládat roky poznámek pacientů v komprimovaném indexu a odstranit PHI (chráněné zdravotní informace) před sdílením s výzkumnými partnery.  
3. **Finanční výkaznictví:** Zabezpečit čtvrtletní zprávy zakrytím čísel účtů, přičemž zachovat prohledávatelný text pro auditní dotazy.

## Úvahy o výkonu
- **Vliv komprese:** Vysoká komprese snižuje velikost indexu až o **90 %**, což snižuje opotřebení SSD a urychluje zálohovací operace.  
- **Využití paměti:** Vypněte cache v paměti pro velmi velké indexy, aby stopa procesu zůstala pod **500 MB**.  
- **Optimalizace I/O:** Přidávejte dokumenty ve skupinách po 100, aby se minimalizovalo přetěžování disku.  
- **Asynchronní zpracování:** Zabalte volání `AddDocument` do `Task.Run`, aby UI vlákna zůstala responsivní v desktopových aplikacích.

## Časté problémy a řešení
- **Nesprávné cesty k souborům:** Ověřte, že `documentsFolder` a `indexFolder` jsou absolutní cesty a že aplikace má oprávnění ke čtení/zápisu.  
- **Chyby licence:** Ujistěte se, že soubory `.lic` jsou nasazeny vedle spustitelného souboru nebo vloženy jako zdroje.  
- **Vyhledávání nevrací výsledky:** Zkontrolujte, že úroveň komprese `TextStorageSettings` odpovídá té použité při indexování; nesoulad nastavení může způsobit selhání deserializace.

## Často kladené otázky

**Q: Mohu po počátečním vytvoření přidávat dokumenty do indexu?**  
A: Ano—jednoduše zavolejte `index.AddDocument` pro nové soubory; engine aktualizuje komprimovaný index inkrementálně.

**Q: Změní redakce původní soubor?**  
A: Ne—originální soubor zůstává nedotčen; redigovaná verze je uložena jako nový soubor, zachovává integritu dokumentu.

**Q: Jaké formáty GroupDocs.Redaction podporuje?**  
A: Více než **30** formátů, včetně PDF, DOCX, PPTX, XLSX, obrázků (PNG, JPEG) a prostého textu.

**Q: Jak vysoká komprese ovlivňuje relevanci vyhledávání?**  
A: Neovlivňuje. Komprese je bezeztrátová pro text, takže skóre relevance jsou identická s nekomprimovaným indexem.

**Q: Existuje limit velikosti dokumentů, které mohu indexovat?**  
A: GroupDocs.Search dokáže zpracovat soubory o velikosti několika gigabajtů streamováním obsahu; však zajistěte dostatek místa na disku pro komprimovaný index (přibližně 10 % původní velikosti).

## Zdroje
- [Dokumentace](https://docs.groupdocs.com/search/net/)
- [Reference API](https://reference.groupdocs.com/redaction/net)
- [Stáhnout GroupDocs.Redaction pro .NET](https://releases.groupdocs.com/search/net/)
- [Bezplatné fórum podpory](https://forum.groupdocs.com/c/search/10)
- [Získání dočasné licence](https://purchase.groupdocs.com/temporary-license/)

---

**Poslední aktualizace:** 2026-06-07  
**Testováno s:** GroupDocs.Search 23.12 a GroupDocs.Redaction 23.12 pro .NET  
**Autor:** GroupDocs

## Související tutoriály

- [Implementace GroupDocs.Search a Redaction v .NET pro správu dokumentů](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Jak optimalizovat GroupDocs.Redaction pro .NET: Průvodce efektivní správou indexu a pravopisu](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [Mistrovství GroupDocs Redaction a Search v .NET: Efektivní správa dokumentů a bezpečné vyhledávání](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
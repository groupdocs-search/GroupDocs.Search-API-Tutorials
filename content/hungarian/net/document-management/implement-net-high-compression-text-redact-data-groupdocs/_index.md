---
date: '2026-06-07'
description: Ismerje meg, hogyan valósítható meg a magas tömörítésű .NET szövegtárolás,
  és hogyan lehet a bizalmas adatokat redakcióval eltávolítani a GroupDocs.Search
  és a GroupDocs.Redaction használatával .NET alkalmazásokban.
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
title: 'Magas tömörítésű .NET megvalósítása a GroupDocs segítségével: Szöveg- és redakciós
  útmutató'
type: docs
url: /hu/net/document-management/implement-net-high-compression-text-redact-data-groupdocs/
weight: 1
---

# Magas tömörítésű .NET megvalósítása a GroupDocs-szal: Szöveg- és Redakciós útmutató

A modern .NET megoldásokban a **implement high compression .net** elengedhetetlen, ha hatalmas szöveggyűjteményeket kell tárolni anélkül, hogy a lemezhasználat felrobbanna. Ugyanakkor az érzékeny információk – például személyes azonosítók vagy pénzügyi adatok – védelme megbízható redakciót igényel. Ez az útmutató lépésről‑lépésre bemutatja, hogyan konfiguráljuk a magas tömörítésű szövegtárolást a **GroupDocs.Search** segítségével, és hogyan redakcióval távolítsuk el a bizalmas adatokat a **GroupDocs.Redaction** használatával. A végére képes lesz akár 90 %-kal tömöríteni az indexelt szöveget, és privát tartalmakat eltávolítani PDF‑ekből, Word‑fájlokból és számos más formátumból.

## Gyors válaszok
- **Melyik könyvtár biztosít magas tömörítésű indexelést?** GroupDocs.Search for .NET.  
- **Melyik eszköz redakcióval távolítja el az érzékeny adatokat?** GroupDocs.Redaction for .NET.  
- **Hozzáadhatok dokumentumokat az indexhez automatikusan?** Igen – használja az `AddDocument` API-t egy mappavizsgálati ciklusban.  
- **A tömörítés veszteségmentes a kereséshez?** Igen, a szöveg a tömörítés után is teljesen kereshető marad.  
- **Szükség van licencre a termeléshez?** Egy állandó GroupDocs licenc szükséges a kereskedelmi használathoz.

## Mi az a “implement high compression .net”?
A “implement high compression .net” azt jelenti, hogy a GroupDocs.Search indexelő motorját úgy konfiguráljuk, hogy a kinyert szövegtartalmat tömörített formában tárolja. Ez drámai módon csökkenti a lemezen lévő index méretét, miközben a szöveg teljesen kereshető marad. A tömörítés veszteségmentes, így a lekérdezés relevanciája és a szövegrészlet‑kivonás pontosan úgy működik, mint egy nem tömörített index esetén.

## Miért használja a GroupDocs-t tömörítéshez és redakcióhoz?
A GroupDocs.Search több mint ötven bemeneti formátumot támogat, és akár kilencven százalékos tömörítést is elér a indexelt szövegnél, lehetővé téve, hogy nagy dokumentumgyűjtemények csak töredékét foglalják el az eredeti méretnek. A GroupDocs.Redaction ezt kiegészíti azzal, hogy véglegesen törli vagy maszkolja az érzékeny információkat több mint harminc fájltípusban, segítve a szigorú megfelelőségi szabályok, például a GDPR és a HIPAA betartását további eszközök nélkül.

## Előfeltételek
- **Fejlesztési környezet:** Visual Studio 2022 vagy újabb, .NET 6+ (vagy .NET Framework 4.7.2).  
- **Könyvtárak:** `GroupDocs.Search` és `GroupDocs.Redaction` NuGet csomagok.  
- **Jogosultságok:** Olvasási/írási hozzáférés a forrásdokumentumokat és az index kimeneti helyét tartalmazó mappákhoz.  
- **Alapvető tudás:** C# szintaxis, fájl I/O, és a .NET projektstruktúra ismerete.

## Hogyan valósítsuk meg a magas tömörítésű .NET-et a GroupDocs-szal?
A magas tömörítésű .NET megvalósításához a GroupDocs-szal először hozzunk létre egy `TextStorageSettings` példányt, és állítsuk be a `CompressionLevel`‑t `High`‑ra. Ezután példányosítsunk egy `Index` objektumot, megadva a beállításokat és azt a mappát, ahol az index tárolódik. Az index elkészülte után adjuk hozzá a dokumentumokat az `AddDocument`‑dal, végül futtassunk kereséseket a `Search` metódussal, miközben a motor átlátszóan kezeli a tömörítést és a kitömörítést.

### 1. lépés: A szükséges NuGet csomagok telepítése
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
- Keresse meg a “GroupDocs.Search” elemet, és kattintson a **Install** gombra.  

### 2. lépés: A GroupDocs.Redaction telepítése (az adatredakcióhoz)
- Nyissa meg a **NuGet Package Manager**-t.  
- Keresse meg a **GroupDocs.Redaction**-t, és telepítse a legújabb stabil verziót.  

### 3. lépés: Licenc beszerzése és alkalmazása
- **Ingyenes próba:** Regisztráljon a GroupDocs portálon egy 30 napos próba kulcsért.  
- **Ideiglenes licenc:** Kérjen ideiglenes kulcsot fejlesztői környezetekhez.  
- **Állandó licenc:** Vásároljon termelési licencet az értékelési korlátozások eltávolításához.

### 4. lépés: Mindkét könyvtár alapvető inicializálása
A `Search` és `Redaction` motorok közös licencmodellt használnak. Inicializálja őket az alkalmazás indításakor:

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

## 1. funkció: Magas tömörítésű szövegtárolási beállítások

### Indexelési konfiguráció beállítása
A `TextStorageSettings` határozza meg, hogyan tárolja a GroupDocs.Search a kinyert szöveget. A magas tömörítés engedélyezése akár **10×**‑es indexméret‑csökkenést eredményez a keresési sebesség befolyásolása nélkül.

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

**Magyarázat:**  
- `CompressionLevel.High` egy ZSTD‑alapú algoritmust aktivál, amely hatékonyan tömöríti a szövegrétegeket.  
- `UseMemoryCache = false` arra kényszeríti a motorot, hogy lemezről streamelje az adatokat, ami nagy léptékű telepítésekhez ideális.

### Az index létrehozása és kezelése
Az `Index` objektum a lemezen tárolt kereshető adattárat képviseli. Meg kell adni a mappát, ahol az indexfájlok tárolódnak, és átadni a fent definiált tömörítési beállításokat.

```csharp
var indexFolder = @"C:\Indexes\HighCompression";
var settings = new IndexSettings { TextStorage = textStorage };
var index = new Index(indexFolder, settings);
```
```csharp
string indexFolder = "/path/to/your/index/directory";
Index index = new Index(indexFolder, settings);
```  

**Magyarázat:**  
- `indexFolder` meghatározza, hogy hol tárolódnak a tömörített indexfájlok.  
- `settings` beilleszti a magas tömörítésű konfigurációt, biztosítva, hogy minden hozzáadott dokumentum ebből profitáljon.

## 2. funkció: Dokumentumok hozzáadása az indexhez

### Dokumentumok hozzáadása az indexhez
Az `AddDocument` egyetlen fájlt ad az indexhez, kinyeri a szöveget, a beállított `TextStorageSettings` szerint tömöríti, és elmenti az eredményt. A GroupDocs.Search képes fájlok beolvasására egy könyvtárfában. Az alábbi ciklus bejárja a `documentsFolder`‑t, minden fájlt hozzáad, és naplózza a folyamatot.

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

**Magyarázat:**  
- `AddDocument` feldolgozza a fájlt, kinyeri a kereshető szöveget, a `TextStorageSettings` szerint tömöríti, és az indexben tárolja.  
- Ez a megközelítés működik **PDF**, **DOCX**, **TXT**, **HTML** és több mint **30** egyéb formátum esetén.

## 3. funkció: Keresési lekérdezés végrehajtása

### Keresés végrehajtása
A `Search` egy lekérdezést futtat a tömörített indexen, és visszaadja a megfelelő `DocumentResult` objektumok gyűjteményét relevancia‑pontszámokkal és kiemelt szövegrészletekkel. Miután az index fel van töltve, gyors lekérdezéseket hajthat végre. A `Search` metódus visszaadja a `DocumentResult` objektumok gyűjteményét, amelyek fájlutakat és kiemelt szövegrészleteket tartalmaznak.

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

**Magyarázat:**  
- A keresőmotor közvetlenül a tömörített szöveget vizsgálja, így a lekérdezés késleltetése alacsony marad még **milliók oldalát** tartalmazó indexek esetén is.  
- `Score` a relevanciát jelzi; a magasabb érték jobb egyezést jelent.

## Hogyan redakcióval távolítsuk el a bizalmas adatokat a GroupDocs.Redaction segítségével?
A bizalmas adatok redakciója a GroupDocs.Redaction-nél egy `Redactor` példány létrehozásával kezdődik a célfájlhoz. Definiáljon egy vagy több `SearchPattern` objektumot, amely leírja a törlendő szöveget, például a társadalombiztosítási számok reguláris kifejezéseit. Alkalmazza minden mintát a `Redact`‑tal, megadva egy `RedactionType`‑ot, például `BlackOut`, majd mentse az eredményt új dokumentumként, biztosítva, hogy az eredeti változat érintetlen maradjon.

`Redactor` a fő osztály a GroupDocs.Redaction‑ban, amely betölti a dokumentumot és végrehajtja a redakciós műveleteket.  
`SearchPattern` egy reguláris kifejezést definiál, amely az eltávolítandó szöveget azonosítja.

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

**Magyarázat:**  
- `SearchPattern` reguláris kifejezést használ a társadalombiztosítási számok megtalálásához.  
- `RedactionType.BlackOut` egy szilárd fekete téglalappal helyettesíti a megtalált szöveget, biztosítva, hogy az adat ne legyen visszaállítható.

## Gyakorlati alkalmazások
1. **Jogi dokumentumkezelés:** Automatikusan tömörítse a hatalmas ügyiratokat, és archiválás előtt redakcióval távolítsa el az ügyfélazonosítókat.  
2. **Egészségügyi nyilvántartások:** Tárolja évek óta a betegjegyzeteket egy tömörített indexben, és a kutatási partnerekkel való megosztás előtt távolítsa el a PHI (védett egészségügyi információ) adatokat.  
3. **Pénzügyi jelentés:** Biztosítsa a negyedéves jelentéseket azáltal, hogy redakcióval eltávolítja a számlaszámokat, miközben a kereshető szöveget megőrzi az audit lekérdezésekhez.

## Teljesítménybeli megfontolások
- **Tömörítés hatása:** A magas tömörítés akár **90 %**‑kal csökkenti az index méretét, ami csökkenti az SSD kopását és felgyorsítja a biztonsági mentéseket.  
- **Memóriahasználat:** Kapcsolja ki a memóriában történő gyorsítótárazást nagyon nagy indexek esetén, hogy a folyamat lábnyoma **500 MB** alatt maradjon.  
- **I/O optimalizálás:** Csoportosítsa a dokumentumok hozzáadását 100‑as adagokban a lemezterhelés csökkentése érdekében.  
- **Aszinkron feldolgozás:** Csomagolja az `AddDocument` hívásokat `Task.Run`‑ba, hogy a felhasználói felület szálai reagálóképesek maradjanak asztali alkalmazásokban.

## Gyakori hibák és hibaelhárítás
- **Helytelen fájlutak:** Ellenőrizze, hogy a `documentsFolder` és az `indexFolder` abszolút útvonalak‑e, és hogy az alkalmazásnak van‑e olvasási/írási jogosultsága.  
- **Licenc hibák:** Győződjön meg róla, hogy a `.lic` fájlok az exe mellé vannak telepítve vagy erőforrásként beágyazottak.  
- **A keresés nem ad eredményt:** Ellenőrizze, hogy a `TextStorageSettings` tömörítési szintje megegyezik‑e az indexelés során használtal; a nem egyező beállítások deszerializációs hibákat okozhatnak.

## Gyakran feltett kérdések

**K: Hozzáadhatok dokumentumokat az indexhez az első építés után?**  
Igen – egyszerűen hívja meg az `index.AddDocument`‑ot új fájlokhoz; a motor fokozatosan frissíti a tömörített indexet.

**K: A redakció módosítja az eredeti fájlt?**  
Nem – az eredeti fájl érintetlen marad; a redakcióval ellátott verzió új fájlként kerül mentésre, megőrizve a dokumentum integritását.

**K: Milyen formátumokat támogat a GroupDocs.Redaction?**  
Több mint **30** formátum, beleértve a PDF, DOCX, PPTX, XLSX, képek (PNG, JPEG) és egyszerű szöveg.

**K: Hogyan befolyásolja a magas tömörítés a keresési relevanciát?**  
Nem befolyásolja. A tömörítés szövegre vonatkozóan veszteségmentes, így a relevancia pontszámok megegyeznek egy nem tömörített indexével.

**K: Van korlátja a dokumentumok méretének, amelyeket indexelni tudok?**  
A GroupDocs.Search több gigabájtos fájlok kezelésére képes streaming tartalommal; azonban biztosítsa a megfelelő lemezterületet a tömörített indexhez (kb. az eredeti méret 10 %-a).

## Források
- [Documentation](https://docs.groupdocs.com/search/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction for .NET](https://releases.groupdocs.com/search/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/search/10)
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license/)

---

**Legutóbb frissítve:** 2026-06-07  
**Tesztelve:** GroupDocs.Search 23.12 and GroupDocs.Redaction 23.12 for .NET  
**Szerző:** GroupDocs

## Kapcsolódó útmutatók

- [GroupDocs.Search és Redaction megvalósítása .NET-ben dokumentumkezeléshez](/search/net/document-management/groupdocs-search-redaction-net-guide/)
- [Hogyan optimalizáljuk a GroupDocs.Redaction-t .NET-hez: Hatékony index és helyesírás-kezelési útmutató](/search/net/performance-optimization/optimize-groupdocs-redaction-index-spelling-management/)
- [A GroupDocs Redaction és Search mesterfogásai .NET-ben: Hatékony dokumentumkezelés és biztonságos keresés](/search/net/advanced-features/mastering-groupdocs-redaction-search-dotnet/)
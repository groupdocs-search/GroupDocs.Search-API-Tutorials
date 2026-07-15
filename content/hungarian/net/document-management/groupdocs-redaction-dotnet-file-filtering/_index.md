---
date: '2026-04-21'
description: Ismerje meg, hogyan szűrhet fájlokat a GroupDocs.Redaction for .NET segítségével,
  beleértve a létrehozás dátuma, a fájlméret, a módosítás dátuma szerinti szűrést,
  valamint a NOT szűrők alkalmazását.
keywords:
- how to filter files
- filter by creation date
- filter by file size
- filter by modification date
- apply not filter
title: Hogyan szűrjünk fájlokat a GroupDocs.Redaction .NET-hez
type: docs
url: /hu/net/document-management/groupdocs-redaction-dotnet-file-filtering/
weight: 1
---

# Hogyan szűrjünk fájlokat a GroupDocs.Redaction for .NET segítségével

A mai gyorsan változó digitális környezetben a **fájlok hatékony szűrése** döntő lehet a termelékenység szempontjából. Akár kiterjesztés, létrehozási dátum, méret vagy módosítási dátum alapján szeretne dokumentumokat elkülöníteni, egy jól átgondolt szűrési stratégia időt takarít meg, csökkenti a tárolási költségeket, és rendezetten tartja a keresési indexet. Ebben az útmutatóban valós példákon keresztül mutatjuk be a GroupDocs.Redaction for .NET használatát, és pontosan bemutatjuk, hogyan szűrhet fájlokat a gyakori üzleti igényekhez.

## Gyors válaszok
- **Milyen könyvtárra van szükségem?** GroupDocs.Redaction for .NET (telepítés NuGet-en keresztül).  
- **Szűrhetek létrehozási dátum szerint?** Igen – használja a `CreateCreationTimeRange`-t.  
- **Hogyan zárhatok ki bizonyos típusokat?** Alkalmazzon NOT szűrőt a `DocumentFilter.CreateNot` segítségével.  
- **Támogatott a fájlméret szűrése?** Teljes mértékben, a `CreateFileLengthRange` vagy felső/alsó határok használatával.  
- **Szükségem van licencre?** Próbaverzió vagy teljes licenc szükséges a termelési használathoz.

## Mi az a fájlszűrés a GroupDocs.Redaction segítségével?
A fájlszűrés lehetővé teszi, hogy az indexelő motor számára megadja, mely dokumentumokat vegye fel vagy hagyja figyelmen kívül a metaadatok, például kiterjesztés, dátumok, útvonalminták vagy méret alapján. Pontos `DocumentFilter` szabályok definiálásával karcsú indexet és gyors keresést biztosít.

## Miért használjuk a GroupDocs.Redaction for .NET-et?
- **Beépített szűrősegédletek** – nincs szükség egyedi fájlrendszer-kód írására.  
- **Logikai operátorok** – több feltétel kombinálása AND, OR és NOT segítségével.  
- **Teljesítmény‑optimalizált** – a szűrőket az indexelés során alkalmazzák, nem utólag.  
- **Keresztplatformos** – működik .NET Framework, .NET Core és .NET 5/6+ környezetekkel.

## Előfeltételek
- .NET Framework 4.6+ vagy .NET Core 3.1+ telepítve.  
- Visual Studio vagy a kedvenc C# IDE-je.  
- Alap C# ismeretek.  

### Szükséges könyvtárak és beállítás
Telepítse a NuGet csomagot a kedvenc módszerével:

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

> **Pro tipp:** A telepítés után adja hozzá a licencfájlt a projekt gyökeréhez, és hívja meg a `License.SetLicense("license-file-path")`-t, mielőtt bármilyen Redactor vagy Index objektumot létrehozná.

## A GroupDocs.Redaction for .NET beállítása

Először hozzon létre egy `Redactor` példányt, amely a feldolgozni kívánt dokumentumra mutat:

```csharp
using GroupDocs.Redaction;
// Initialize Redactor with the path to your document.
Redactor redactor = new Redactor("your-document-path");
```

> **Miért fontos:** A Redactor inicializálása garantálja, hogy a könyvtár készen áll a szűrők és redakciós szabályok későbbi alkalmazására a munkafolyamat során.

## Hogyan szűrjünk fájlokat kiterjesztés szerint

A fájlok kiterjesztés szerinti szűrése a leggyakoribb módja egy dokumentumkészlet szűkítésének. Az alábbiakban csak az FB2, EPUB és TXT fájlokat tartjuk meg.

### Szűrés kiterjesztés szerint

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
// Allow only FB2, EPUB, and TXT files.
DocumentFilter filter = DocumentFilter.CreateFileExtension(".fb2", ".epub", ".txt");
settings.DocumentFilter = filter;

// Create an index with applied filters.
Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan alkalmazzunk NOT szűrőt a nem kívánt típusok kizárásához

Ha **NOT szűrőt** kell alkalmaznia – például HTML és PDF fájlok kizárásához – használja a `CreateNot`-et.

### HTM, HTML és PDF fájlok kizárása

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter excludeFilter = DocumentFilter.CreateFileExtension(".htm", ".html", ".pdf");
DocumentFilter invertedFilter = DocumentFilter.CreateNot(excludeFilter);
settings.DocumentFilter = invertedFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan szűrjünk fájlokat létrehozási dátum szerint

Amikor **létrehozási dátum szerint** kell szűrnie, adjon meg egy kezdő és egy befejező `DateTime` értéket.

### Szűrés létrehozási dátumtartomány szerint

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateCreationTimeRange(new DateTime(2017, 1, 1), new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan szűrjünk fájlokat módosítási dátum szerint

A létrehozási dátumokhoz hasonlóan korlátozhatja az eredményeket olyan fájlokra, amelyeket egy adott időpont előtt módosítottak.

### Szűrés módosítási dátum szerint

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateModificationTimeUpperBound(new DateTime(2018, 6, 15));
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan szűrjünk fájlokat útvonal alapján reguláris kifejezésekkel

Ha a mappaszerkezet megfelel elnevezési konvencióknak, egy reguláris kifejezés célozhat meg konkrét útvonalakat.

### Szűrés fájlútvonal-mintára

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System.Text.RegularExpressions;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFilePathRegularExpression("Ipsum", RegexOptions.IgnoreCase);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan szűrjünk fájlokat méret szerint

A dokumentumméret szabályozása elengedhetetlen, ha sávszélesség- vagy tárolási korlátokkal dolgozik.

### Szűrés fájlméret szerint (50 KB – 100 KB)

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter = DocumentFilter.CreateFileLengthRange(50 * 1024, 100 * 1024);
settings.DocumentFilter = filter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan kombináljunk több feltételt AND operátorral

Amikor **több feltétel alapján** kell egyszerre szűrnie a fájlokat, kombinálja őket a `CreateAnd` segítségével.

### Logikai AND példa

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;
using System;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter filter1 = DocumentFilter.CreateCreationTimeRange(new DateTime(2015, 1, 1), new DateTime(2016, 1, 1));
DocumentFilter filter2 = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter filter3 = DocumentFilter.CreateFileLengthUpperBound(8 * 1024 * 1024);
DocumentFilter finalFilter = DocumentFilter.CreateAnd(filter1, filter2, filter3);
settings.DocumentFilter = finalFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Hogyan kombináljunk több feltételt OR operátorral

Használja a `CreateOr`-t, ha több szabály közül bármelyiknek át kell mennie.

### Logikai OR példa

```csharp
using GroupDocs.Search;
using GroupDocs.Search.Options;

string indexFolder = "YOUR_OUTPUT_DIRECTORY";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY";

IndexSettings settings = new IndexSettings();
DocumentFilter txtFilter = DocumentFilter.CreateFileExtension(".txt");
DocumentFilter notTxtFilter = DocumentFilter.CreateNot(txtFilter);
DocumentFilter bound5Filter = DocumentFilter.CreateFileLengthUpperBound(5 * 1024 * 1024);
DocumentFilter bound10Filter = DocumentFilter.CreateFileLengthUpperBound(10 * 1024 * 1024);
DocumentFilter txtSizeFilter = DocumentFilter.CreateOr(txtFilter, notTxtFilter, bound5Filter, bound10Filter);
settings.DocumentFilter = txtSizeFilter;

Index index = new Index(indexFolder, settings);
index.Add(documentsFolder);
```

## Gyakori problémák és megoldások
- **A szűrő nem alkalmazódik:** Győződjön meg róla, hogy a `settings.DocumentFilter`-t **a** `Index` példány létrehozása **előtt** állítja be.  
- **Váratlan fájlok jelennek meg:** Ellenőrizze, hogy a fájlkiterjesztések tartalmazzák-e a vezető pontot (`.txt`).  
- **Teljesítménycsökkenés:** Kombinálja a szűrőket AND operátorral, hogy csökkentse a szkennelendő fájlok számát az indexelési folyamat korai szakaszában.  
- **Regex hibák:** Szökje meg a speciális karaktereket az útvonalmintában, vagy használja a `RegexOptions.IgnoreCase`-t a kis- és nagybetűket figyelmen kívül hagyó egyezésekhez.

## Gyakran feltett kérdések

**Q: Kombinálhatok NOT szűrőt AND szűrővel?**  
A: Igen. Először építse fel a NOT szűrőt (`DocumentFilter.CreateNot`), majd adja hozzá a `DocumentFilter.CreateAnd` argumentumai közé.

**Q: Hogyan szűrhetek 10 MB-nál nagyobb fájlokat?**  
A: Használja a `DocumentFilter.CreateFileLengthLowerBound(10 * 1024 * 1024)`-t, hogy csak a méretét meghaladó fájlokat vegye fel.

**Q: Lehetséges egyszerre szűrni létrehozási és módosítási dátum szerint?**  
A: Teljes mértékben. Készítse el mindkét szűrőt külön-külön, majd kombinálja őket a `CreateAnd` segítségével.

**Q: Működnek ezek a szűrők felhőalapú tárolási útvonalakkal?**  
A: A szűrők a helyi fájlrendszeren működnek. Felhőforrások esetén először töltse le a fájlokat egy ideiglenes mappába, majd alkalmazza ugyanazokat a szűrőket.

**Q: A szűrő módosítása újraindexelést igényel?**  
A: Igen. A szűrőket akkor értékelik ki, amikor meghívja a `index.Add`-et. A szűrő módosítása azt jelenti, hogy újra kell építeni az indexet az új kritériumok tükrözéséhez.

## Következtetés

A **fájlok szűrésének** elsajátításával a GroupDocs.Redaction for .NET segítségével – legyen szó kiterjesztésről, létrehozási dátumról, módosítási dátumról, fájlméretről vagy NOT logikáról – egyszerűsítheti a dokumentumkezelést, karbantarthatja az indexek teljesítményét, és a valóban fontos tartalomra koncentrálhat. Kísérletezzen a logikai operátorokkal, hogy a szűrést pontosan az üzleti szabályaihoz igazítsa, és azonnali javulást fog tapasztalni a sebességben és a tárolási hatékonyságban.

---

**Utoljára frissítve:** 2026-04-21  
**Tesztelve a következővel:** GroupDocs.Redaction 24.11 for .NET  
**Szerző:** GroupDocs  

---
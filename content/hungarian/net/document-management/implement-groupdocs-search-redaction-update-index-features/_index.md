---
date: '2026-06-07'
description: Ismerje meg, hogyan frissítheti hatékonyan az indexet a GroupDocs.Search
  és a Redaction for .NET segítségével, javítva dokumentumkezelő rendszerét.
keywords:
- how to update index
- GroupDocs.Search for .NET
- document index versioning
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  headline: How to Update Index with GroupDocs.Search & Redaction (.NET)
  type: TechArticle
- description: Learn how to update index efficiently with GroupDocs.Search and Redaction
    for .NET, enhancing your document management system.
  name: How to Update Index with GroupDocs.Search & Redaction (.NET)
  steps:
  - name: Create an Index
    text: The `Index` class is the top‑level object that represents a searchable collection
      on disk.
  - name: Add Documents to the Index
    text: Add files from a directory; the library automatically extracts searchable
      text.
  - name: Search and Update
    text: Run a query, modify the source file, then call `UpdateDocument` with the
      same `UpdateOptions` used during indexing. **Why This Works:** By setting `Threads
      = 2`, the update leverages two CPU cores, cutting processing time roughly in
      half on a quad‑core machine.
  - name: Check Compatibility
    text: '`IndexUpdater` checks whether the current index can be upgraded to the
      latest format.'
  - name: Load and Search
    text: After upgrading, load the refreshed index and execute a query to verify
      integrity. **Why This Works:** The `CanUpdateVersion` guard prevents runtime
      exceptions caused by mismatched index schemas, providing a safe upgrade path.
  type: HowTo
- questions:
  - answer: '`UpdateDocument` modifies only changed files, whereas `Rebuild` recreates
      the entire index from scratch, consuming more time and resources.'
    question: What is the difference between `UpdateDocument` and `Rebuild`?
  - answer: Yes, set `UpdateOptions.Threads` to the number of cores you wish to utilize;
      the library handles parallel processing internally.
    question: Can I update multiple documents in parallel?
  - answer: Absolutely. Provide the password via `SearchOptions.Password` when loading
      the document.
    question: Does GroupDocs.Search support encrypted PDFs?
  - answer: Call `Redactor.Apply()` and inspect the output file size; a reduced size
      often indicates successful redaction.
    question: How do I verify that redaction was successful before indexing?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5, and .NET 6+.
    question: What .NET versions are officially supported?
  type: FAQPage
title: Hogyan frissítsük az indexet a GroupDocs.Search & Redaction (.NET) segítségével
type: docs
url: /hu/net/document-management/implement-groupdocs-search-redaction-update-index-features/
weight: 1
---

# Hogyan frissítsük az indexet a GroupDocs.Search és Redaction segítségével (.NET)

A modern, adat‑központú vállalkozásokban az **index frissítése** gyorsan és megbízhatóan döntő lehet a keresési élmény szempontjából. Akár több ezer szerződést, akár egy kiterjedt tudásbázist kezel, a keresési index naprakészen tartása a legújabb dokumentumváltozásokkal elengedhetetlen a gyors és pontos eredményekhez. Ez a bemutató végigvezet a GroupDocs.Search for .NET és a GroupDocs.Redaction használatán a **index frissítése** fájlokhoz, a verziózott indexek kezeléséhez, és az érzékeny tartalom védelméhez – mind egy tiszta .NET projekt keretében.

## Gyors válaszok
- **Mi jelent a “how to update index” kifejezés?** Ez a folyamat, amely során egy meglévő keresési indexet módosítanak, hogy az új vagy módosított dokumentumok újra kereshetők legyenek az újraépítés nélkül.  
- **Mely könyvtárak szükségesek?** GroupDocs.Search és GroupDocs.Redaction for .NET (mindkettő elérhető a NuGet-en keresztül).  
- **Szükségem van licencre?** Egy ingyenes próba a teszteléshez működik; egy éles licenc a teljes funkcionalitást biztosítja.  
- **Futtatható .NET Core-on?** Igen, a könyvtárak támogatják a .NET Framework 4.5+, a .NET Core 3.1+, valamint a .NET 5/6+ verziókat.  
- **Milyen teljesítményre számíthatok?** Egy 1 GB méretű index 2 szállal történő frissítése egy tipikus 4‑magos szerveren kevesebb, mint egy perc alatt befejeződik.

## Mi az a “how to update index”?
**Index frissítése** arra a technikára utal, amely során egy meglévő keresési indexhez inkrementális változtatásokat alkalmaznak a teljes újraalkotás helyett. Ez a megközelítés csökkenti a leállási időt, CPU-erőforrásokat takarít meg, és frissíti a keresési eredményeket, ahogy a dokumentumok hozzáadódnak, módosulnak vagy eltávolításra kerülnek.

## Miért használjuk a GroupDocs.Search és Redaction-t az index frissítésekhez?
A GroupDocs.Search **50+ fájlformátumot** támogat (PDF, DOCX, XLSX, PPTX, HTML, képek stb.) és több száz oldalas dokumentumokat képes feldolgozni anélkül, hogy az egész fájlt a memóriába töltené. A GroupDocs.Redaction-nal kombinálva automatikusan eltávolíthat vagy maszkolhat érzékeny adatokat az indexelés előtt, biztosítva a megfelelőséget, miközben megőrzi a keresés relevanciáját.

## Előkövetelmények

- **GroupDocs.Search** – telepítés NuGet-en keresztül.  
- **GroupDocs.Redaction for .NET** – szükséges a redakciós funkciókhoz.  
- Visual Studio (vagy bármely .NET IDE) .NET 6+ telepítéssel.  
- Alap C# ismeretek és az indexelési koncepciók ismerete.

### Szükséges könyvtárak és verziók
- **GroupDocs.Search** – a legújabb stabil kiadás a NuGet-ről.  
- **GroupDocs.Redaction for .NET** – a legújabb stabil kiadás a NuGet-ről.

### Környezet beállítási követelmények
- Windows vagy Linux gép .NET SDK-val telepítve.  
- Hozzáférés egy mappához, ahol az index fájlok tárolva lesznek.

### Tudás előkövetelmények
- A dokumentum indexelés és a keresés alapjainak megértése.  
- Tudatosság a dokumentum életciklus-kezelésről vállalati rendszerekben.

## A GroupDocs.Redaction beállítása .NET-hez

### A csomagok telepítése

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Keresse meg a “GroupDocs.Redaction” csomagot, és telepítse a legújabb verziót.

### Licenc beszerzési lépések
1. **Free Trial** – kezdje egy próbaidőszakkal, hogy felfedezze az összes funkciót.  
2. **Temporary License** – kérjen ideiglenes kulcsot a kiterjesztett teszteléshez.  
3. **Purchase** – szerezzen be egy teljes licencet a termelési telepítésekhez.

### Alap inicializálás és beállítás
`Redactor` a központi osztály, amely redakciós szabályokat alkalmaz a dokumentumokra.  
A kezdéshez hivatkozzon a Redaction névtérre, és hozza létre a `Redactor` példányt:

```csharp
using GroupDocs.Redaction;
```

## Implementációs útmutató

Két fő képességet fogunk bemutatni: az indexelt dokumentumok frissítését és az index verziókezelésének fenntartását.

### Hogyan frissítsük az indexet a GroupDocs.Search használatával?

`Index` a lemezen tárolt kereshető gyűjteményt jelenti.  
`UpdateOptions` konfigurálja, hogyan történnek az inkrementális frissítések (pl. szálak száma).  
`UpdateDocument` egyetlen dokumentum változtatásait alkalmazza, a `Commit` pedig véglegesíti az összes függőben lévő frissítést.

**Közvetlen válasz (40‑70 szó):**  
Hozzon létre egy `Index` objektumot, amely az index mappájára mutat, használja a `UpdateOptions`-t a szálak számának megadásához, hívja meg a `UpdateDocument`-et minden módosított fájlra, és végül hívja meg a `Commit`-et a változások mentéséhez. Ez az inkrementális megközelítés csak a módosított részeket frissíti, így az index naprakész marad teljes újraépítés nélkül.

#### 1. funkció: Indexelt dokumentumok frissítése

##### Áttekintés
Az indexelt dokumentumok frissítése biztosítja, hogy a keresési eredmények a legújabb tartalmat tükrözzék, még akkor is, ha a dokumentumokat szerkesztik vagy cserélik.

##### 1. lépés: Index létrehozása  
`Index` osztály a legfelső szintű objektum, amely egy kereshető gyűjteményt képvisel a lemezen.

```csharp
string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexedDocuments/Index";
Index index = new Index(indexFolder);
```

##### 2. lépés: Dokumentumok hozzáadása az indexhez  
Adjon hozzá fájlokat egy könyvtárból; a könyvtár automatikusan kinyeri a kereshető szöveget.

```csharp
string documentFolder = @"YOUR_DOCUMENT_DIRECTORY/Documents";
index.Add(documentFolder);
```

##### 3. lépés: Keresés és frissítés  
Futtasson egy lekérdezést, módosítsa a forrásfájlt, majd hívja meg a `UpdateDocument`-et ugyanazzal a `UpdateOptions`-sal, amelyet az indexelés során használt.

```csharp
string query = "son";
SearchResult searchResult = index.Search(query);

UpdateOptions options = new UpdateOptions { Threads = 2 };
index.Update(options);

SearchResult searchResult2 = index.Search(query);
```

**Miért működik:** A `Threads = 2` beállítással a frissítés két CPU magot használ, így a feldolgozási idő körülbelül felére csökken egy négymagos gépen.

### Hogyan tartsuk karban az index verziókezelését?

`IndexUpdater` egy segédosztály, amely a régebbi indexformátumokat a könyvtár által támogatott legújabb verzióra frissíti.

**Közvetlen válasz (40‑70 szó):**  
Hozzon létre egy `IndexUpdater` példányt a meglévő index útvonalával, hívja meg a `CanUpdateVersion()`-t a kompatibilitás ellenőrzéséhez, majd szükség esetén futtassa a `UpdateVersion()`-t. A frissítés után töltse be újra az indexet az új formátummal, és végezzen keresést a működés ellenőrzéséhez. Ez biztosítja a zökkenőmentes migrációt a könyvtár kiadások között.

#### 2. funkció: Index verziókezelés fenntartása

##### Áttekintés
A verziókezelés garantálja, hogy a régi indexek is kereshetők maradjanak egy könyvtár frissítés után.

##### 1. lépés: Kompatibilitás ellenőrzése  
`IndexUpdater` ellenőrzi, hogy a jelenlegi index frissíthető‑e a legújabb formátumra.

```csharp
string oldIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/OldIndex";
string sourceIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexS";
string targetIndexFolder = @"YOUR_DOCUMENT_DIRECTORY/UpdateIndexVersion/IndexT";

IndexUpdater updater = new IndexUpdater();
if (updater.CanUpdateVersion(sourceIndexFolder))
{
    VersionUpdateResult result = updater.UpdateVersion(sourceIndexFolder, targetIndexFolder);
}
```

##### 2. lépés: Betöltés és keresés  
A frissítés után töltse be a megújult indexet, és hajtson végre egy lekérdezést az integritás ellenőrzéséhez.

```csharp
Index index = new Index(targetIndexFolder);
string query = "eagerness";
SearchResult searchResult = index.Search(query);
```

**Miért működik:** A `CanUpdateVersion` ellenőrzés megakadályozza a futásidejű kivételeket, amelyeket a nem egyező index sémák okoznak, így biztonságos frissítési útvonalat biztosít.

## Gyakorlati alkalmazások

Valós életbeli forgatókönyvek, ahol a **index frissítése** fontos:

1. **Jogi dokumentumkezelés** – Gyorsan újraindexelje a szerződéseket módosítások után, miközben a bizalmas záradékokat redakcióval eltávolítja.  
2. **Vállalati archívumok** – Tartsák a történelmi feljegyzéseket kereshetően anélkül, hogy millió fájlt újra feldolgoznának.  
3. **Tartalomkezelő rendszerek (CMS)** – Közvetítsen inkrementális frissítéseket a keresési indexbe, ahogy a szerzők új cikkeket publikálnak.

## Teljesítményfontosságú szempontok

- **Szálbeállítások:** Állítsa a `UpdateOptions.Threads` értékét a CPU magok számához; több szál növeli a teljesítményt, de a memóriahasználatot is.  
- **Erőforrás-használat:** Figyelje a RAM-ot; a könyvtár folyamatosan streameli a fájlokat, így a memóriacsúcsok is minimálisak még 500 oldalas PDF-eknél is.  
- **Legjobb gyakorlatok:** Ütemezzen rendszeres inkrementális frissítéseket, és tisztítsa meg a régi index verziókat a legoptimálisabb teljesítmény érdekében.

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| **Index nem található** | Helytelen mappautasítás | Ellenőrizze, hogy az `Index` konstruktor a megfelelő könyvtárra mutat. |
| **Verzióeltérés hiba** | Régebbi index használata egy újabb könyvtárral | Futtassa az `IndexUpdater` folyamatot a normál indexelés előtt. |
| **Redakció nem alkalmazott** | Redakciós szabályok betöltve az indexelés után | Alkalmazza a redakciót **előtt**, mielőtt a dokumentumokat az indexhez adná. |

## Gyakran ismételt kérdések

**Q: Mi a különbség az `UpdateDocument` és a `Rebuild` között?**  
A: `UpdateDocument` csak a módosított fájlokat változtatja, míg a `Rebuild` a teljes indexet újraépíti a semmiből, több időt és erőforrást igényelve.

**Q: Frissíthetek több dokumentumot párhuzamosan?**  
A: Igen, állítsa be a `UpdateOptions.Threads` értékét a kívánt magok számára; a könyvtár belsőleg kezeli a párhuzamos feldolgozást.

**Q: Támogatja a GroupDocs.Search a titkosított PDF-eket?**  
A: Teljes mértékben. Adja meg a jelszót a `SearchOptions.Password` segítségével a dokumentum betöltésekor.

**Q: Hogyan ellenőrizhetem, hogy a redakció sikeres volt-e az indexelés előtt?**  
A: Hívja meg a `Redactor.Apply()`-t, és ellenőrizze a kimeneti fájl méretét; a csökkent méret gyakran jelzi a sikeres redakciót.

**Q: Mely .NET verziók támogatottak hivatalosan?**  
A: .NET Framework 4.5+, .NET Core 3.1+, .NET 5 és .NET 6+.

## Következtetés

Most már rendelkezik egy teljes, termelésre kész útmutatóval az **index frissítéséről** a GroupDocs.Search használatával, valamint arról, hogyan tartsa ezeket az indexeket verziókompatibilis állapotban a GroupDocs.Redaction for .NET segítségével. A fenti lépések követésével biztosíthatja, hogy a keresési réteg gyors, pontos és az adatvédelmi előírásoknak megfelelő marad.

**Következő lépések:**  
- Kísérletezzen különböző `Threads` beállításokkal, hogy megtalálja a legoptimálisabb értéket a hardveréhez.  
- Fedezze fel a fejlett redakciós mintákat (pl. regex‑alapú TAJ szám eltávolítás) az indexelés előtt.  
- Integrálja az index frissítési rutinját a CI/CD folyamatba a teljesen automatizált dokumentumkezelés érdekében.

---

**Legutóbb frissítve:** 2026-06-07  
**Tesztelve a következőkkel:** GroupDocs.Search 23.10 for .NET, GroupDocs.Redaction 23.10 for .NET  
**Szerző:** GroupDocs  

## Erőforrások
- [Dokumentáció](https://docs.groupdocs.com/search/net/)
- [API referencia](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction letöltése](https://releases.groupdocs.com/search/net/)
- [Ingyenes támogatási fórum](https://forum.groupdocs.com/c/search/10)
- [Ideiglenes licenc](https://purchase.groupdocs.com/temporary-license/)

## Kapcsolódó oktatóanyagok
- [A GroupDocs.Redaction .NET elsajátítása: Hatékony index létrehozás és alias kezelés a fejlett dokumentumkereséshez](/search/net/indexing/groupdocs-redaction-net-index-alias-management/)
- [Szinonima keresés implementálása a GroupDocs.Redaction .NET segítségével a fejlett dokumentumkezeléshez](/search/net/dictionaries-language-processing/groupdocs-redaction-net-synonym-search/)
- [A GroupDocs Search és Redaction .NET-ben: Fejlett dokumentumkezelés](/search/net/advanced-features/groupdocs-search-redaction-net-tutorial/)
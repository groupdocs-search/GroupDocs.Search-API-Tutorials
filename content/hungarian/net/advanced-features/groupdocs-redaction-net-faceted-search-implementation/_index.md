---
date: '2026-04-02'
description: Tanulja meg, hogyan hozhat létre keresési indexet a GroupDocs segítségével,
  és hogyan adhat dokumentumokat az indexhez, miközben a facettált keresést valósítja
  meg a GroupDocs.Search és a GroupDocs.Redaction .NET környezetben.
keywords:
- create search index groupdocs
- add documents to index
- faceted search .NET
- GroupDocs.Redaction
title: Keresési index létrehozása a GroupDocs-ban redakcióval .NET facettált keresés
type: docs
url: /hu/net/advanced-features/groupdocs-redaction-net-faceted-search-implementation/
weight: 1
---

# Keresési index létrehozása GroupDocs Redaction .NET facettált kereséssel

## Gyors válaszok
- **Mi a fő cél?** A keresési index létrehozása a GroupDocs-szal és a facettált keresés engedélyezése.  
- **Mely könyvtárak szükségesek?** GroupDocs.Redaction és GroupDocs.Search .NET-hez.  
- **Hogyan adhatok dokumentumokat az indexhez?** Használja az `index.Add(documentsFolder)`-t az index inicializálása után.  
- **Futtathatok összetett lekérdezéseket?** Igen, kombinálja az objektumlekérdezéseket logikai operátorokkal a fejlett szűréshez.  
- **Szükséges licenc?** A fejlesztéshez egy ingyenes próba verzió elegendő; a termeléshez kereskedelmi licenc szükséges.

## Mi az a facettált keresés, és miért használjuk a GroupDocs-szal?
A facettált keresés lehetővé teszi a felhasználók számára, hogy több szűrőt—például kategória, dátum vagy szerző—alkalmazva egyszerre szűkítsék a találatokat. A **GroupDocs.Redaction**-nal kombinálva biztonságos, kereshető tartalmat kap, amely tiszteletben tartja a redakciós szabályokat, így ideális a szigorú megfelelőségi környezetekben.

## Előkövetelmények

### Szükséges könyvtárak, verziók és függőségek
- **GroupDocs.Redaction .NET** – legújabb stabil kiadás.  
- **GroupDocs.Search .NET** – kéz a kézben működik a Redaction-nal az indexeléshez.

### Környezet beállítási követelmények
- **IDE**: Visual Studio 2019 vagy újabb.  
- **Framework**: .NET Core 3.1, .NET 5 vagy .NET 6.  
- **OS kompatibilitás**: Windows, Linux, macOS.

### Tudás előkövetelmények
Az alapvető C# ismeretek és a facettált keresés koncepcióinak magas szintű megértése segíthet, de a lépésről‑lépésre útmutató kezdők számára is barátságos.

## A GroupDocs.Redaction beállítása .NET-hez

### Telepítési információk
A GroupDocs.Redaction csomagot az alábbi módszerek egyikével adhatja hozzá:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**
- Keresés a "GroupDocs.Redaction"‑ra, és telepítse a legújabb verziót.

### Licenc beszerzési lépések
Az összes funkció feloldásához kezdjen egy ingyenes próba verzióval, vagy szerezzen be egy állandó licencet:

1. Látogasson el a [GroupDocs Purchase](https://purchase.groupdocs.com/temporary-license/) oldalra, hogy megismerje a licencelési lehetőségeket.  
2. Kövesse a képernyőn megjelenő utasításokat a próba vagy megvásárolt licencfájl megkapásához.

### Alap inicializálás és beállítás
Miután a csomag telepítve van, inicializálja a Redactor-t az alkalmazásában:

```csharp
using GroupDocs.Redaction;
RedactorSettings settings = new RedactorSettings();
// Load a document for redaction using the Redactor class.
```

## Hogyan hozhatunk létre keresési indexet groupdocs-szal

Az alábbiakban a megvalósítást két részre bontjuk: **Egyszerű facettált keresés** és **Összetett lekérdezés**. Minden rész bemutatja, hogyan **hozzunk létre keresési indexet groupdocs-szal**, adjunk hozzá dokumentumokat, és futtassunk lekérdezéseket.

### Funkció 1: Egyszerű facettált keresés

**Áttekintés**  
A facettált keresés lehetővé teszi a felhasználók számára, hogy több kritérium kiválasztásával szűkítsék a találatokat. Ez a szakasz egy egyszerű megközelítést mutat be a GroupDocs.Search használatával.

#### 1. lépés: Az index és a dokumentumok mappáinak meghatározása
Állítsa be a mappák útvonalait, ahol az index tárolódik, és ahol a forrásdokumentumok találhatók.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/SimpleFacetedSearch";
string documentsFolder = "YOUR_DOCUMENT_DIRECTORY\\";
```

#### 2. lépés: Index létrehozása
```csharp
Index index = new Index(indexFolder);
```

#### 3. lépés: Dokumentumok hozzáadása az indexhez
```csharp
index.Add(documentsFolder);
```

#### 4. lépés: Szöveges lekérdezés keresés végrehajtása
Futtasson egy egyszerű szöveges lekérdezést a **content** mezőn.

```csharp
string query1 = "content: Pellentesque";
SearchResult result1 = index.Search(query1);
```

#### 5. lépés: Objektum lekérdezés keresés végrehajtása
Használjon objektum‑orientált lekérdezéseket a finomabb vezérléshez.

```csharp
SearchQuery wordQuery = SearchQuery.CreateWordQuery("Pellentesque");
SearchQuery fieldQuery = SearchQuery.CreateFieldQuery(CommonFieldNames.Content, wordQuery);
SearchResult result2 = index.Search(fieldQuery);
```

### Funkció 2: Összetett lekérdezés

**Áttekintés**  
Ha több szűrőt—például fájlnév mintákat és kifejezés egyezéseket—kell kombinálni, összetett lekérdezést építhet fel logikai operátorok használatával.

#### 1. lépés: Az index és a dokumentumok mappáinak meghatározása
Használja újra ugyanazt a mappaszerkezetet egy fejlettebb szcenárióhoz.

```csharp
string indexFolder = "YOUR_DOCUMENT_DIRECTORY/AdvancedUsage/Searching/FacetedSearch/ComplexQuery";
```

#### 2. lépés: Index létrehozása és dokumentumok hozzáadása
(Lásd a 2‑3 lépéseket az egyszerű példában; változatlanok.)

#### 3. lépés: Szöveges lekérdezés keresés végrehajtása
Futtasson egy összetett szöveges lekérdezést, amely keveri a fájlnév és a tartalom kritériumait.

```csharp
string query1 = "(filename: (lorem AND ipsum)) OR (content: (\"lectus eu aliquam\" OR \"dignissim turpis\"))";
SearchResult result1 = index.Search(query1);
```

#### 4. lépés: Objektum lekérdezések felépítése és végrehajtása
Programozottan építse fel ugyanazt a logikát.

```csharp
// Building components of the complex query.
SearchQuery word6Query = SearchQuery.CreateWordQuery("lorem");
SearchQuery word7Query ontext="ipsum";
SearchQuery andQuery = SearchQuery.CreateAndQuery(word6Query, word7Query);
```

Folytassa a kifejezések, tartományok és logikai operátorok kombinálását, hogy pontosan megfeleljen az üzleti szabályainak.

## Gyakorlati alkalmazások

1. **E‑kereskedelmi platformok** – Termékek szűrése kategória, ár és értékelés szerint.  
2. **Dokumentumkezelő rendszerek** – Szerző, dátum vagy titoktartási szint alapján szerződések megtalálása.  
3. **Tartalmi portálok** – Olvasók számára lehetővé teszi a címkék, témák és közzétételi dátumok szerinti szűrést.

## Teljesítmény szempontok

- **Index frissítése**: Rendszeresen indexeljen új vagy frissített fájlokat a gyors keresés érdekében.  
- **Memória kezelés**: Szabadítsa fel az `Index` objektumokat a használat után, különösen nagy adathalmazok esetén.  
- **Aszinkron indexelés**: Használja a `Task.Run`‑t vagy háttérszolgáltatásokat a UI fagyásának elkerülésére a nehéz indexelés során.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **Index nem található** | Ellenőrizze az `indexFolder` útvonalat, és győződjön meg arról, hogy a mappának írási jogosultsága van. |
| **Nincs találat** | Ellenőrizze, hogy a lekérdezett mezők (pl. `Content`, `Filename`) indexelve vannak-e. |
| **Memóriahiány hibák** | Feldolgozza a dokumentumokat kötegekben, és fontolja meg a .NET GC heap méretének növelését. |

## Gyakran feltett kérdések

**K: Mi az a facettált keresés?**  
V: A facettált keresés lehetővé teszi a felhasználók számára, hogy több, egymástól független szűrőt—például kategória, dátum vagy szerző—alkalmazva szűkítsék a találatokat.

**K: Hogyan kezeljem a nagy adathalmazokat a GroupDocs.Search-szel?**  
V: Használjon inkrementális indexelést, kötegelt feldolgozást és aszinkron műveleteket a memóriahasználat alacsonyan és a teljesítmény magas szinten tartásához.

**K: Integrálhatom a GroupDocs funkciókat meglévő .NET alkalmazásokba?**  
V: Igen, a könyvtárak úgy vannak tervezve, hogy zökkenőmentesen integrálhatók legyenek bármely .NET projektbe.

**K: Milyen gyakori problémák merülnek fel a facettált keresésnél?**  
V: Az összetett lekérdezési szintaxis és annak biztosítása, hogy minden releváns mező indexelve legyen, tipikus kihívások; a megfelelő tesztelés és az index karbantartása enyhíti ezeket.

**K: Hogyan szerezzek ideiglenes licencet a GroupDocs-hoz?**  
V: Látogasson el a [GroupDocs licencoldalra](https://purchase.groupdocs.com/temporary-license/), hogy kérjen egy próba licencet, amely a kiértékelés során teljes funkcionalitást biztosít.

## Források
- **Dokumentáció**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/search/net/)
- **API referencia**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction)

---

**Utolsó frissítés:** 2026-04-02  
**Tesztelve a következőkkel:** GroupDocs.Redaction 23.12 .NET-hez, GroupDocs.Search 23.12 .NET-hez  
**Szerző:** GroupDocs
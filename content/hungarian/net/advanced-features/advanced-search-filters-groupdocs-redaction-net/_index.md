---
date: '2026-04-02'
description: Ismerje meg, hogyan szűrhet fájlkiterjesztés szerint, és kereshet csak
  txt fájlok között a GroupDocs.Redaction for .NET segítségével—növelje a dokumentumkezelés
  hatékonyságát.
keywords:
- filter by file extension
- how to filter documents
- search only txt files
title: Fájl kiterjesztés szerinti szűrés .NET-ben a GroupDocs.Redaction használatával
type: docs
url: /hu/net/advanced-features/advanced-search-filters-groupdocs-redaction-net/
weight: 1
---

# Fájl kiterjesztés szerinti szűrés .NET-ben a GroupDocs.Redaction használatával

A hatalmas fájlgazdák átvizsgálása nyomasztó lehet, különösen akkor, ha csak bizonyos fájltípusok eredményeire van szükség. Ebben az útmutatóban megtudja, **hogyan szűrjünk fájl kiterjesztés szerint** a GroupDocs.Redaction for .NET segítségével, így csak txt fájlokat vagy bármely más általad választott kiterjesztést kereshet. Bemutatjuk a fájltípus‑ és útvonal‑alapú szűrők beállítását, így gyorsan megtalálhatja a szükséges dokumentumokat.

## Gyors válaszok
- **Mi a “fájl kiterjesztés szerinti szűrés” funkciója?** Korlátozza a keresést olyan dokumentumokra, amelyek megfelelnek egy adott fájl kiterjesztésnek (pl. *.txt).  
- **Miért használjuk ehhez a GroupDocs.Redaction-t?** Beépített szűrési API-kat biztosít, amelyek gyorsak és könnyen integrálhatók.  
- **Szükségem van licencre?** Egy ingyenes próba a teszteléshez működik; a termeléshez fizetett licenc szükséges.  
- **Mely .NET verziók támogatottak?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Kombinálhatom a fájltípus és útvonal szűrőket?** Igen – több szűrőt is alkalmazhat a nagyon pontos keresésekhez.

## Amit meg fog tanulni
- Hogyan **szűrjünk fájl kiterjesztés szerint**, hogy csak szövegfájlok legyenek keresve.  
- Hogyan állítsunk be **fájl útvonal szűrőket**, hogy a találatok egy adott mappára vagy elnevezési mintára korlátozódjanak.  
- Tippek az index gyors és memóriahatékony megtartásához.

## Előfeltételek

- **GroupDocs.Redaction könyvtár** telepítve és kompatibilis a .NET projektjével.  
- Fejlesztői környezet, például Visual Studio vagy VS Code.  
- Alap C# ismeretek és a .NET projekt struktúrájának ismerete.

## A GroupDocs.Redaction beállítása .NET-hez

Először adja hozzá a könyvtárat a projektjéhez.

**Using .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Using Package Manager:**  
```bash
Install-Package GroupDocs.Redaction
```

Vagy keresse meg a “GroupDocs.Redaction” elemet a NuGet Package Manager felületen, és telepítse a legújabb verziót.

### Licenc megszerzése

Kezdhet ingyenes próba verzióval vagy kérhet ideiglenes licencet. Hosszú távú projektekhez vásároljon licencet a hivatalos weboldalról.

### Alap inicializálás

A csomag telepítése után hozzon létre egy indexet, amely a dokumentumokra mutató hivatkozásokat tárolja:

```csharp
using GroupDocs.Search;

string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
Index index = new Index(indexFolder);
```

## Implementációs útmutató

### 1. funkció: Szűrő beállítása szöveges dokumentumokhoz (.txt)

#### Hogyan szűrjünk fájl kiterjesztés szerint szöveges dokumentumok esetén

1. **Határozza meg az indexet és a dokumentum mappákat**  
   Állítsa be az útvonalakat, ahol a forrásfájlok találhatók:

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/SettingAFilter";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Hozzon létre egy Indexet**  
   Töltsön be minden fájlt a forrásmappából az indexbe:

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder); // Add all files from this directory to the index
   ```

3. **Állítsa be a keresési opciókat fájl kiterjesztés szűrővel**  
   Adja meg a motor számára, hogy csak *.txt fájlokat vegyen figyelembe:

   ```csharp
   SearchOptions options = new SearchOptions();
   options.SearchDocumentFilter = SearchDocumentFilter.CreateFileExtension(".txt");
   ```

4. **Végezze el a keresést**  
   Futtasson egy lekérdezést; a szűrő biztosítja, hogy a nem szöveges fájlok figyelmen kívül maradjanak:

   ```csharp
   string query = "education";
   SearchResult result = index.Search(query, options);
   ```

   *Magyarázat*: A `Search` metódus olyan találatokat ad vissza, amelyek megfelelnek a szűrőnek, jelentősen csökkentve a zajt és javítva a teljesítményt.

### 2. funkció: Fájl útvonal szűrők

#### Miért használjunk fájl útvonal szűrőket?

Néha szükség van a keresés korlátozására egy adott részleg mappájára vagy olyan fájlokra, amelyek közös elnevezési szabályt követnek. Az útvonal szűrők pontosan ezt teszik lehetővé.

1. **Határozza meg az indexet és a dokumentum mappákat**  

   ```csharp
   string indexFolder = @"YOUR_DOCUMENT_DIRECTORY/FilePathFilters";
   string documentsFolder = @"YOUR_DOCUMENT_DIRECTORY";
   ```

2. **Hozzon létre egy Indexet**  

   ```csharp
   Index index = new Index(indexFolder);
   index.Add(documentsFolder);
   ```

3. **Állítsa be a keresési opciókat útvonal alapú reguláris kifejezéssel**  

   ```csharp
   SearchOptions options = new SearchOptions();
   ISearchDocumentFilter filter = SearchDocumentFilter.CreateFilePathRegularExpression("Lorem");
   options.SearchDocumentFilter = filter;
   ```

   Ez a reguláris kifejezés minden olyan fájlt egyeztesz, amelynek teljes útvonala tartalmazza a “Lorem” szót, lehetővé téve, hogy konkrét almappákat célozzon meg.

4. **Hajtsa végre az útvonal alapú keresést**  

   ```csharp
   SearchResult result = index.Search(query, options);
   ```

## Gyakorlati alkalmazások
- **Jogi dokumentumkezelés** – Gyorsan megtalálja a releváns szerződéseket, amelyek egyszerű szövegfájlokként vannak tárolva.  
- **Akademiai kutatás** – Csak a *.txt kutatási jegyzeteket húzza ki, amelyek egy adott projektmappához tartoznak.  
- **Vállalati jelentéskészítés** – Szűrje a belső jelentéseket részleg útvonala szerint (pl. `/Finance/2025/`).  

## Teljesítmény szempontok
- Csak azokat a dokumentumtípusokat indexelje, amelyekre valóban szüksége van; a felesleges fájlok növelik az index méretét és a keresési időt.  
- Tartsa az indexet naprakészen egy ütemezett feladattal, amely új vagy módosított fájlok esetén meghívja az `index.Add()` metódust.  
- Használjon egyszerű reguláris kifejezéseket; a túl komplex minták lelassíthatják a keresőmotort.  
- Szabadítsa fel a memóriát az `Index` objektumok eldobásával, amikor már nincs rájuk szükség.

## Következtetés
Most már tudja, hogyan **szűrhet fájl kiterjesztés szerint** és hogyan alkalmazhat **fájl útvonal szűrőket** a GroupDocs.Redaction .NET verziójával. Ezek a technikák finomhangolt irányítást biztosítanak a nagy dokumentumgyűjtemények felett, így a keresések gyorsabbak és relevánsabbak lesznek. Következő lépésként kísérletezzen több szűrő kombinálásával vagy a keresés integrálásával egy nagyobb alkalmazás munkafolyamatába.

## GyIK szekció

**Q1: Szűrhetek más, mint szövegfájlokat?**  
A1: Igen, a GroupDocs.Redaction számos formátumot támogat. Módosítsa a `CreateFileExtension` argumentumát a kívánt kiterjesztésre (pl. ".pdf").

**Q2: Hogyan frissíthetem rendszeresen a keresési indexet?**  
A2: Ütemezzen egy háttérszolgáltatást vagy cron feladatot, amely a frissíteni kívánt könyvtárakon futtatja az `index.Add()` metódust.

**Q3: Van teljesítménybeli hatása a fájl útvonal szerinti szűrésnek?**  
A3: A megfelelően optimalizált reguláris kifejezések minimális hatással vannak, de mindig mérje a teljesítményt a saját adatkészletével.

**Q4: Kombinálhatok több szűrőt a finomabb keresésekhez?**  
A4: Természetesen. Láncolhat szűrőket vagy létrehozhat összetett szűrőket, hogy egyszerre a fájltípusra és az útvonalra is célozzon.

**Q5: Hol találok további forrásokat a GroupDocs.Redaction-hoz?**  
A5: Látogassa meg a hivatalos dokumentációt a [GroupDocs Documentation](https://docs.groupdocs.com/search/net/) oldalon a részletes útmutatók és API hivatkozásokért.

## Gyakran Ismételt Kérdések

**Q: A `SearchDocumentFilter` működik titkosított fájlokkal?**  
A: A szűrő maga a fájl metaadatait használja, így a titkosított fájlok is indexelve lesznek, ha a indexelés során megadja a szükséges dekódolási hitelesítő adatokat.

**Q: Használhatok helyettesítő karaktereket reguláris kifejezés helyett az útvonal szűréshez?**  
A: Az API jelenleg reguláris kifejezést igényel, de szimulálhat egyszerű helyettesítő karaktereket (pl. `.*` bármilyen karakterhez).

**Q: Mekkora lehet az index, mielőtt a sharding-et kellene fontolni?**  
A: A több száz gigabájtos indexek előnyös lehet, ha több logikai indexre bontják; tesztelje a teljesítményt, ahogy a gyűjtemény nő.

**Q: Van beépített módszer a dokumentumok eltávolítására az indexből?**  
A: Igen – hívja meg az `index.Delete(documentId)` vagy `index.DeleteAll()` metódust a régi bejegyzések kezeléséhez.

**Q: Van mód a keresési eredmények előnézetére a teljes dokumentum betöltése előtt?**  
A: A `SearchResult` objektum tartalmaz snippet információt, amelyet a felhasználói felületen megjeleníthet a teljes fájl megnyitása nélkül.

## Források
- **Dokumentáció**: [GroupDocs Documentation](https://docs.groupdocs.com/search/net/)
- **API referencia**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Letöltés**: [GroupDocs Downloads](https://releases.groupdocs.com/search/net/)
- **Ingyenes támogatás**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)
- **Ideiglenes licenc**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Utolsó frissítés:** 2026-04-02  
**Tesztelve ezzel:** GroupDocs.Redaction 23.12 for .NET  
**Szerző:** GroupDocs
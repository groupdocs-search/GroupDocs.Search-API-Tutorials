---
date: '2025-12-19'
description: Ismerje meg, hogyan adhat dokumentumokat az indexhez, és engedélyezheti
  a darab-alapú keresést Java-ban a GroupDocs.Search használatával, ezáltal növelve
  a nagy dokumentumkészletek teljesítményét.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Dokumentumok hozzáadása az indexhez tömbalapú kereséssel Java-ban
type: docs
url: /hu/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Dokumentumok hozzáadása az indexhez tömb‑alapú kereséssel Java‑ban

A mai adat‑központú világban elengedhetetlen, hogy **gyorsan dokumentumokat adjunk az indexhez**, majd tömb‑alapú kereséseket végezzünk bármely olyan alkalmazásban, amely nagy fájlgáborokat kezel. Legyen szó jogi szerződésekről, ügyfélszolgálati archívumokról vagy hatalmas kutatási könyvtárakról, ez a bemutató pontosan megmutatja, hogyan állítsuk be a GroupDocs.Search for Java‑t, hogy hatékonyan indexeljünk dokumentumokat, és releváns információkat kapjunk kis darabokban.

## Mit fogsz megtanulni
- Hogyan hozzunk létre keresési indexet egy megadott mappában.  
- Lépések a **dokumentumok indexhez adásához** több helyről.  
- A keresési beállítások konfigurálása a tömb‑alapú keresés engedélyezéséhez.  
- Kezdeti és későbbi tömb‑alapú keresések végrehajtása.  
- Valós példák, ahol a tömb‑alapú dokumentumkeresés kiemelkedik.

## Gyors válaszok
- **Mi az első lépés?** Hozz létre egy keresési index mappát.  
- **Hogyan adhatok hozzá sok fájlt?** Használd az `index.add()` metódust minden dokumentummappához.  
- **Melyik opció engedélyezi a tömb keresést?** `options.setChunkSearch(true)`.  
- **Folytathatom a keresést az első tömb után?** Igen, hívd a `index.searchNext()`‑t a tokennel.  
- **Szükségem van licencre?** Fejlesztéshez egy ingyenes próba vagy ideiglenes licenc is elegendő; a termeléshez teljes licenc szükséges.

## Előfeltételek
A útmutató követéséhez biztosítsd, hogy:

- **Szükséges könyvtárak**: GroupDocs.Search for Java 25.4 vagy újabb.  
- **Környezet beállítása**: Telepített kompatibilis Java Development Kit (JDK).  
- **Ismeretek**: Alap Java programozás és Maven ismerete.

## A GroupDocs.Search beállítása Java‑hoz
Kezdjük a GroupDocs.Search integrálásával a projektedbe Maven‑en keresztül:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```

Alternatívaként töltsd le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
A GroupDocs.Search kipróbálásához:

- **Ingyenes próba** – teszteld a fő funkciókat kötelezettség nélkül.  
- **Ideiglenes licenc** – meghosszabbított hozzáférés fejlesztéshez.  
- **Vásárlás** – teljes licenc a termeléshez.

### Alap inicializálás és beállítás
Hozz létre egy indexet abban a mappában, ahol a kereshető adatot tárolni szeretnéd:

```java
import com.groupdocs.search.*;

public class CreateIndex {
    public static void main(String[] args) {
        String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
        // Creating an index in the specified folder
        Index index = new Index(indexFolder);
    }
}
```

## Hogyan adjunk dokumentumokat az indexhez
Most, hogy az index létezik, a következő logikus lépés a **dokumentumok indexhez adása** a fájlok tárolási helyéről.

### 1. Index létrehozása
**Áttekintés**: Hozz létre egy könyvtárat a keresési indexhez.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Dokumentumok hozzáadása az indexhez
**Áttekintés**: Hozz be fájlokat több forrásmappából.

```java
String documentsFolder1 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder2 = "YOUR_DOCUMENT_DIRECTORY";
String documentsFolder3 = "YOUR_DOCUMENT_DIRECTORY";
```

```java
index.add(documentsFolder1);
index.add(documentsFolder2);
index.add(documentsFolder3);
```

### 3. Keresési beállítások konfigurálása tömb kereséshez
Engedélyezd a tömb‑alapú keresést a beállítási objektum módosításával.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Kezdeti tömb‑alapú keresés végrehajtása
Futtasd az első lekérdezést a tömb‑engedélyezett beállításokkal.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Tömb‑alapú keresés folytatása
Iterálj a maradék tömbökön, amíg a keresés be nem fejeződik.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Miért használjunk tömb‑alapú keresést?
A tömb‑alapú keresés hatalmas dokumentumgyűjteményeket bont kisebb, kezelhető darabokra, csökkentve a memória terhelését és felgyorsítva a válaszidőt. Különösen előnyös, ha:

1. **Jogi csapatok**nak kell konkrét kikötéseket megtalálni több ezer szerződésben.  
2. **Ügyfélszolgálati portálok**nak kell azonnal releváns tudásbázis‑cikkeket megjeleníteni.  
3. **Kutatók**nak kell átfésülni nagy adatállományokat anélkül, hogy az egész fájlokat betöltenék a memóriába.

## Teljesítmény szempontok
- **Memória kezelés** – Biztosíts elegendő heap méretet (`-Xmx`) a nagy indexekhez.  
- **Erőforrás‑figyelés** – Figyeld a CPU‑használatot az indexelés és keresés során.  
- **Index karbantartás** – Időnként építsd újra vagy tisztítsd meg az indexet a régi adatok elhagyásához.

## Gyakori hibák és hibaelhárítás
| Probléma | Miért fordul elő | Megoldás |
|----------|-------------------|----------|
| `OutOfMemoryError` indexelés közben | A heap méret túl alacsony | Növeld a JVM heap‑et (`-Xmx2g` vagy nagyobb) |
| Nincs eredmény | A tömb token nincs feldolgozva | Győződj meg róla, hogy a `while` ciklus addig fut, amíg a `getNextChunkSearchToken()` `null`‑ra nem áll |
| Lassú keresési teljesítmény | Az index nincs optimalizálva | Hívd meg az `index.optimize()`‑t a tömeges hozzáadások után |

## Gyakran Ismételt Kérdések

**Q: Mi az a tömb‑alapú keresés?**  
A: A tömb‑alapú keresés a adatbázist kisebb darabokra bontja, lehetővé téve hatékony lekérdezéseket nagy mennyiségű adat felett anélkül, hogy az egész dokumentumokat betöltené a memóriába.

**Q: Hogyan frissíthetem az indexet új fájlokkal?**  
A: Egyszerűen hívd meg az `index.add()`‑t az új dokumentumok elérési útjával; az index automatikusan beépíti őket.

**Q: Kezelhet-e a GroupDocs.Search különböző fájlformátumokat?**  
A: Igen, támogatja a PDF‑eket, DOCX‑et, XLSX‑et, PPTX‑et és számos más gyakori formátumot.

**Q: Mik a tipikus teljesítmény‑szűk keresztmetszetek?**  
A: A memória korlátok és a nem optimalizált indexek a leggyakoribbak; biztosíts elegendő heap‑et és rendszeresen optimalizáld az indexet.

**Q: Hol találok részletesebb dokumentációt?**  
A: Látogasd meg a hivatalos [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) oldalt a mélyreható útmutatókért és API‑referenciákért.

## Erőforrások
- **Dokumentáció**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Referencia**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Letöltés**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ingyenes támogatás**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Ideiglenes licenc**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Utoljára frissítve:** 2025-12-19  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs
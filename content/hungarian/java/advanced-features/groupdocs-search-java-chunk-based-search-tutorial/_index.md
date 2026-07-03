---
date: '2026-02-21'
description: Tanulja meg, hogyan adhat dokumentumokat az indexhez, és növelheti a
  keresési teljesítményt a chunk‑alapú kereséssel Java‑ban a GroupDocs.Search használatával,
  optimalizálva a Java keresési index memóriahasználatát nagy dokumentumkészletek
  esetén.
keywords:
- chunk-based search
- GroupDocs.Search Java
- document search implementation
title: Dokumentumok hozzáadása az indexhez chunk‑alapú kereséssel Java‑ban
type: docs
url: /hu/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Dokumentumok hozzáadása az indexhez tömbalapú kereséssel Java-ban

A modern alkalmazásokban, amelyeknek gyorsan kell **dokumentumokat hozzáadni az indexhez**, majd gyors, tömb‑alapú lekérdezéseket kell végrehajtaniuk, egy olyan megoldásra van szükség, amely méretezhető anélkül, hogy a memória túlterhelődne. Ez az útmutató végigvezet a GroupDocs.Search for Java beállításán, több dokumentummappa hozzáadásán, és a motor konfigurálásán, hogy **növelje a keresési teljesítményt**, miközben a **java search index memory** használatát kontroll alatt tartja. Akár jogi szerződéseket, ügyféltámogatási jegyeket vagy kutatási anyagokat indexel, az alábbi lépések egy termelés‑kész megvalósítást biztosítanak.

## Gyors válaszok
- **Mi az első lépés?** Hozzon létre egy keresési index mappát.  
- **Hogyan adhatok hozzá sok fájlt?** Használja a `index.add()` metódust minden dokumentummappához.  
- **Melyik opció engedélyezi a tömbkeresést?** `options.setChunkSearch(true)`.  
- **Folytathatom a keresést az első tömb után?** Igen, hívja a `index.searchNext()` metódust a tokennel.  
- **Szükségem van licencre?** Egy ingyenes próba vagy ideiglenes licenc elegendő fejlesztéshez; a teljes licenc a termeléshez kötelező.  

## Amit megtanul
- Hogyan hozhat létre keresési indexet egy megadott mappában.  
- Lépések a **dokumentumok hozzáadásához az indexhez** több helyről.  
- A keresési beállítások konfigurálása a tömb‑alapú keresés engedélyezéséhez.  
- Kezdeti és későbbi tömb‑alapú keresések végrehajtása.  
- Valós példák, ahol a tömb‑alapú dokumentumkeresés kiemelkedik.  

## Előfeltételek
A útmutató követéséhez legyenek a következők:

- **Szükséges könyvtárak**: GroupDocs.Search for Java 25.4 vagy újabb.  
- **Környezet beállítása**: Telepített, kompatibilis Java Development Kit (JDK).  
- **Ismeretek**: Alapvető Java programozás és Maven ismerete.  

## A GroupDocs.Search beállítása Java-hoz
Kezdésként integrálja a GroupDocs.Search‑t a projektjébe Maven segítségével:

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

Alternatívaként töltse le a legújabb verziót a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc megszerzése
A GroupDocs.Search kipróbálásához:

- **Ingyenes próba** – a fő funkciók tesztelése kötelezettség nélkül.  
- **Ideiglenes licenc** – meghosszabbított hozzáférés fejlesztéshez.  
- **Megvásárlás** – teljes licenc termelési környezethez.  

### Alapvető inicializálás és beállítás
Hozzon létre egy indexet abban a mappában, ahol a kereshető adatokat tárolni szeretné:

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
Most, hogy az index létezik, a következő logikus lépés a **dokumentumok hozzáadása az indexhez** azokból a helyekből, ahol a fájljai tárolva vannak.

### 1. Index létrehozása
**Áttekintés**: Hozzon létre egy könyvtárat a keresési index számára.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 2. Dokumentumok hozzáadása az indexhez
**Áttekintés**: Hozza be a fájlokat több forrásmappából.

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

### 3. Keresési beállítások konfigurálása tömbkereséshez
Engedélyezze a tömb‑alapú keresést az opciós objektum finomhangolásával.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 4. Kezdeti tömbalapú keresés végrehajtása
Futtassa az első lekérdezést a tömb‑engedélyezett beállításokkal.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

### 5. Tömbalapú keresés folytatása
Iteráljon a maradék tömbökön, amíg a keresés be nem fejeződik.

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Miért használjunk tömbalapú keresést?
A tömb‑alapú keresés hatalmas dokumentumgyűjteményeket bont kisebb, kezelhető darabokra, csökkentve a memória nyomást és felgyorsítva a válaszidőket. Különösen előnyös, ha:

1. **Jogi csapatok**nak kell konkrét záradékokat megtalálniuk több ezer szerződésben.  
2. **Ügyféltámogatási portálok**nak kell azonnal releváns tudásbázis‑cikkeket megjeleníteniük.  
3. **Kutatók**nak kell átfésülniük kiterjedt adatbázisokat anélkül, hogy az egész fájlokat betöltenék a memóriába.  

## Hogyan **növeli a keresési teljesítményt** ez a megközelítés
Kisebb darabok keresésével a teljes fájlok helyett a motor:

- Korán kihagyja a nem releváns szakaszokat, csökkentve a CPU‑ciklusokat.  
- Csak az aktív tömböt tartja memóriában, ami közvetlenül csökkenti a **java search index memory** fogyasztást.  
- Többmagos gépeken párhuzamosan dolgozik a tömbök feldolgozásán, gyorsabb eredményeket érve el.  

## **java search index memory** kezelése
Miközben a tömb‑alapú keresés már csökkenti a memória lábnyomát, a JVM további finomhangolása is lehetséges:

- Allokáljon elegendő halmot (`-Xmx2g` vagy nagyobb) az index mérete alapján.  
- Hívja meg az `index.optimize()` metódust tömeges hozzáadások után az index struktúra tömörítéséhez.  
- Figyelje a GC‑szüneteket olyan eszközökkel, mint a VisualVM, hogy elkerülje a késleltetési csúcsokat.  

## Teljesítményfontosságú megfontolások
- **Memóriakezelés** – Allokáljon elegendő heap‑területet (`-Xmx`) nagy indexekhez.  
- **Erőforrás‑monitorozás** – Tartsa szemmel a CPU‑használatot az indexelés és keresés során.  
- **Index karbantartás** – Időnként építse újra vagy tisztítsa meg az indexet, hogy elhagyott adatokat eltávolítsa.  

## Gyakori buktatók és hibaelhárítás
| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| `OutOfMemoryError` indexelés közben | A heap mérete túl alacsony | Növelje a JVM heap‑et (`-Xmx2g` vagy nagyobb) |
| Nincs eredmény | A tömb token nem lett feldolgozva | Győződjön meg róla, hogy a `while` ciklus addig fut, amíg a `getNextChunkSearchToken()` `null` értéket ad |
| Lassú keresési teljesítmény | Az index nincs optimalizálva | Futtassa az `index.optimize()` metódust tömeges hozzáadások után |

## Gyakran Ismételt Kérdések

**Q: Mi az a tömb‑alapú keresés?**  
A: A tömb‑alapú keresés a teljes adatállományt kisebb darabokra bontja, lehetővé téve a hatékony lekérdezéseket nagy mennyiségű adat esetén anélkül, hogy az egész dokumentumokat betöltené a memóriába.

**Q: Hogyan frissíthetem az indexet új fájlokkal?**  
A: Egyszerűen hívja meg az `index.add()` metódust az új dokumentumok elérési útjával; az index automatikusan beépíti őket.

**Q: Kezelni tudja a GroupDocs.Search a különböző fájlformátumokat?**  
A: Igen, támogatja a PDF‑eket, DOCX‑et, XLSX‑et, PPTX‑et és számos más gyakori formátumot.

**Q: Mik a tipikus teljesítménybottleneckek?**  
A: A memória korlátok és a nem optimalizált indexek a leggyakoribbak; biztosítson elegendő heap‑et és rendszeresen optimalizálja az indexet.

**Q: Hol találok részletesebb dokumentációt?**  
A: Látogasson el a hivatalos [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) oldalra, ahol alapos útmutatók és API‑referenciák állnak rendelkezésre.

**Q: Működik a tömb‑alapú keresés titkosított PDF‑ekkel?**  
A: Igen, amennyiben a megfelelő API‑overload segítségével megadja a jelszót.

**Q: Hogyan figyelhetem az indexelés előrehaladását?**  
A: Használja az `Index.add()` overload‑ját, amely egy `Progress` objektumot ad vissza, vagy kapcsoljon be naplózási visszahívásokat.

## Erőforrások
- **Dokumentáció**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API Referencia**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Letöltés**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ingyenes támogatás**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Ideiglenes licenc**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-02-21  
**Tested With:** GroupDocs.Search 25.4 for Java  
**Author:** GroupDocs
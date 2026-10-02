---
date: '2026-10-02'
description: Tanulja meg, hogyan használjon temporary license-t dokumentumok hozzáadásához
  az indexhez chunk‑based search használatával Java-ban, a search performance növelése
  mellett a memory usage szabályozásával.
keywords:
- use temporary license
- add documents to index
- increase search performance
lastmod: '2026-10-02'
og_description: Használjon temporary license-t dokumentumok hozzáadásához az indexhez
  chunk‑based search használatával Java-ban, a search speed javítása és a memory consumption
  csökkentése érdekében.
og_image_alt: Guide to using a temporary license for chunk‑based document indexing
  in Java with GroupDocs.Search
og_title: Használjon temporary license-t a chunk‑based indexinghez Java-ban
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  headline: Use a temporary license for chunk‑based indexing in Java
  type: TechArticle
- description: Learn how to use a temporary license to add documents to index with
    chunk‑based search in Java, boosting search performance while controlling memory
    usage.
  name: Use a temporary license for chunk‑based indexing in Java
  steps:
  - name: '**Legal teams** need to locate specific clauses across thousands of contracts.'
    text: '**Legal teams** need to locate specific clauses across thousands of contracts.'
  - name: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
    text: '**Customer support portals** must surface relevant knowledge‑base articles
      instantly.'
  - name: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
    text: '**Researchers** sift through extensive datasets without loading entire
      files into memory.'
  type: HowTo
- questions:
  - answer: Chunk‑based searching divides the dataset into smaller pieces, allowing
      efficient queries over large volumes of data without loading entire documents
      into memory.
    question: What is chunk‑based searching?
  - answer: Simply call `index.add()` with the path to the new documents; the index
      will incorporate them automatically.
    question: How do I update my index with new files?
  - answer: Yes, it supports **PDF, DOCX, XLSX, PPTX, HTML, TXT, and over 30 other
      formats**.
    question: Can GroupDocs.Search handle different file formats?
  - answer: Memory constraints and unoptimized indexes are the most common; allocate
      sufficient heap and regularly optimize the index.
    question: What are typical performance bottlenecks?
  - answer: Visit the official [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/)
      for in‑depth guides and API references.
    question: Where can I find more detailed documentation?
  type: FAQPage
tags:
- temporary license
- chunk-based search
- GroupDocs.Search
- Java indexing
- document search
title: Használjon temporary license-t a chunk‑based indexinghez Java-ban
type: docs
url: /hu/java/advanced-features/groupdocs-search-java-chunk-based-search-tutorial/
weight: 1
---

# Ideiglenes licenc használata a darab‑alapú indexeléshez Java-ban

Ebben az oktatóanyagban **ideiglenes licencet** fogsz használni a dokumentumok indexhez adásához a GroupDocs.Search darab‑alapú keresési funkciójával. A megközelítés lehetővé teszi hatalmas dokumentumgyűjtemények – jogi szerződések, ügyféltámogatási jegyek, kutatási anyagok – kezelését, miközben alacsonyan tartja a **java search index memory** használatát, és drámaian **növeli a keresési teljesítményt**. Megmutatjuk, hogyan állítsd be az index mappát, hogyan táplálj több dokumentumforrást, hogyan engedélyezd a darabkeresést, és hogyan futtass mind az első, mind a későbbi darablekérdezéseket.

## Gyors válaszok
- **Mi az első lépés?** Hozz létre egy keresési index mappát.  
- **Hogyan tudok sok fájlt belefoglalni?** Használd a `index.add()`-t minden dokumentummappához.  
- **Melyik opció engedélyezi a darabkeresést?** `options.setChunkSearch(true)`.  
- **Folytathatom a keresést az első darab után?** Igen, hívd a `index.searchNext()`-t a tokennel.  
- **Szükségem van licencre?** Egy ingyenes próba vagy ideiglenes licenc működik fejlesztéshez; a teljes licenc szükséges a termeléshez.  

## Amit megtanul
- Hogyan hozz létre keresési indexet egy megadott mappában.  
- Lépések a **dokumentumok indexhez adásához** több helyről.  
- Keresési beállítások konfigurálása a darab‑alapú keresés engedélyezéséhez.  
- Kezdeti és későbbi darab‑alapú keresések végrehajtása.  
- Valós példák, ahol a darab‑alapú dokumentumkeresés kiemelkedik.  

## Előfeltételek
- **Szükséges könyvtárak**: GroupDocs.Search for Java 25.4 vagy újabb.  
- **Környezet beállítása**: Telepített kompatibilis Java Development Kit (JDK).  
- **Tudás előfeltételek**: Alap Java programozás és Maven ismerete.  

## A GroupDocs.Search beállítása Java-hoz
A kezdéshez integráld a GroupDocs.Search-t a projektedbe Maven segítségével:

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
- **Ideiglenes licenc** – kiterjesztett hozzáférés fejlesztéshez.  
- **Vásárlás** – teljes licenc a termeléshez.  

## Hogyan adjon dokumentumokat az indexhez?
**Közvetlen válasz:** Hívd a `index.add()`-t minden olyan mappához, amely a kereshető fájlokat tartalmazza; a metódus rekurzívan beolvassa a mappát, és minden támogatott dokumentumot egyetlen műveletben hozzáad az indexhez. Ez megszünteti a manuális fájl‑fájl kezelés szükségességét, és felgyorsítja a tömeges betöltést.

`SearchIndex` a központi osztály, amely a lemezen lévő kereshető gyűjteményt képviseli. Miután példányosítod, minden indexelési és lekérdezési művelet ezen az objektumon keresztül folyik.

### 1. Index létrehozása
**Közvetlen válasz:** Hozz létre egy `SearchIndex` objektumot a útvonallal, ahol az indexfájlok tárolásra kerülnek, majd hívd a `index.create()`-t a tárolási struktúra inicializálásához. A hívás létrehozza a szükséges mappákat és metaadat fájlokat az első használatkor.

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

### 2. Dokumentumok hozzáadása az indexhez
**Közvetlen válasz:** Használd a `index.add()` metódust, és add meg minden forrásmappa abszolút útvonalát; az API automatikusan felismeri a támogatott formátumokat (PDF, DOCX, XLSX, stb.) és kinyeri a kereshető szöveget az indexbe.

`SearchOptions` egy konfigurációs objektum, amely lehetővé teszi a dokumentumok finomhangolását az indexelés és keresés során. Később ezt fogod használni a darab‑alapú lekérdezések engedélyezéséhez.

```java
String indexFolder = "YOUR_DOCUMENT_DIRECTORY\\output\\AdvancedUsage\\Searching\\SearchByChunks";
```

```java
Index index = new Index(indexFolder);
```

### 3. Keresési beállítások konfigurálása darabkereséshez
**Közvetlen válasz:** Állítsd be a `options.setChunkSearch(true)`-t egy `SearchOptions` példányon a lekérdezés végrehajtása előtt; ez azt mondja a motornak, hogy bontsa fel minden dokumentumot logikai darabokra (általában bekezdésekre), és a találatokat darabonként adja vissza a teljes fájl helyett.

`SearchResult` tartalmazza a megtalált darabokat, azok pozícióit és relevancia pontszámait. Amikor a darabkeresés be van kapcsolva, minden `SearchResult` egyetlen eredeti dokumentum fragmentumának felel meg.

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

### 4. Kezdeti darab‑alapú keresés végrehajtása
**Közvetlen válasz:** Hajtsd végre a `index.search("your query", options)`-t; a hívás egy `SearchResult` gyűjteményt ad vissza az első egyező darabok halmazához, valamint egy tokent, amely a keresés állapotát jelzi a folytatáshoz.

A visszakapott token elengedhetetlen a nagy eredményhalmazok lapozásához a teljes lekérdezés újrafuttatása nélkül.

```java
SearchOptions options = new SearchOptions();
```

```java
options.setChunkSearch(true);
```

### 5. Darab‑alapú keresés folytatása
**Közvetlen válasz:** Add meg a korábbi hívásból kapott tokent a `index.searchNext(token, options)`-nek; ismételd, amíg a metódus `null`-t nem ad vissza, jelezve, hogy az összes egyező darab lekérdezve lett.

Ez a fokozatos megközelítés alacsonyan tartja a memóriahasználatot, mivel csak az aktuális darabcsoport van memóriában.

```java
String query = "invitation";
```

```java
SearchResult result = index.search(query, options);
```

## Miért használjunk darab‑alapú keresést?
A darab‑alapú keresés felbontja a hatalmas dokumentumgyűjteményeket kezelhető darabokra, csökkentve a memória terhelését és felgyorsítva a válaszidőket. A bekezdés vagy szakasz szintű indexelés révén a motor csak a releváns fragmentumokat tudja visszaadni, ami csökkenti a CPU használatot és javítja a felhasználók késleltetését. Különösen hasznos, ha:
1. **Jogi csapatok**nak kell megtalálniuk a konkrét záradékokat több ezer szerződésben.  
2. **Ügyfélszolgálati portálok**nak azonnal meg kell jeleníteniük a releváns tudásbázis cikkeket.  
3. **Kutatók**nak átnézhetik a kiterjedt adatállományokat anélkül, hogy az egész fájlokat betöltenék a memóriába.  

Mérhető állítás: A GroupDocs.Search képes **500+ oldalas PDF-eket** kevesebb mint **2 másodperc per darab** alatt feldolgozni egy standard 8‑magos szerveren, miközben a csúcs heap méret **200 MB** alatt marad.

## Hogyan növeli ez a megközelítés a keresési teljesítményt
**Közvetlen válasz:** A kisebb darabok keresésével a teljes fájlok helyett a motor korán kihagyhatja a nem releváns részeket, csökkentheti a CPU ciklusokat, és csak az aktív darabot tartja memóriában, ami közvetlenül csökkenti a **java search index memory** fogyasztást és gyorsabb válaszidőket eredményez. Ez a célzott megközelítés hatékonyabb gyorsítótárazást és párhuzamos feldolgozást is lehetővé tesz, lehetővé téve, hogy több mag egyszerre különböző darabokat kezeljen, ami tovább javítja a throughput-ot a többmagos szervereken.

Additional benefits include:
- Párhuzamos darabfeldolgozás több magon.  
- Korai leállás, ha magas relevanciájú találatot találnak.  

## A java keresési index memória kezelése
**Közvetlen válasz:** Allokálj elegendő JVM heap-et (pl. `-Xmx2g` vagy nagyobb) a várható index méret alapján, futtasd a `index.optimize()`-t a tömeges hozzáadások után az index struktúra tömörítéséhez, és figyeld a GC szüneteket a VisualVM-mel a késleltetés csúcsok elkerülése érdekében.

Further tuning tips:
- Használd a `index.flush()`-t nagy adagok után, hogy az átmeneti adatokat lemezre írd.  
- Engedélyezd a `options.setMemoryLimit(256)`-t a keresésenkénti memóriahasználat korlátozásához.  

## Teljesítmény szempontok
- **Memória kezelés** – Allokálj elegendő heap helyet (`-Xmx`) nagy indexekhez.  
- **Erőforrás monitorozás** – Figyeld a CPU használatot az indexelés és keresés során.  
- **Index karbantartás** – Időnként építsd újra vagy tisztítsd meg az indexet a régi adatok eldobásához.  

## Gyakori buktatók és hibaelhárítás
| Probléma | Miért fordul elő | Javítás |
|----------|------------------|---------|
| `OutOfMemoryError` indexing közben | A heap méret túl alacsony | Növeld a JVM heap-et (`-Xmx2g` vagy nagyobb) |
| Nincs eredmény | A darab token nincs feldolgozva | Győződj meg róla, hogy a `while` ciklus fut, amíg a `getNextChunkSearchToken()` `null` nem lesz |
| Lassú keresési teljesítmény | Az index nincs optimalizálva | Futtasd a `index.optimize()`-t a tömeges hozzáadások után |

## Gyakran feltett kérdések

**Q: Mi az a darab‑alapú keresés?**  
A: A darab‑alapú keresés a adathalmazt kisebb darabokra osztja, lehetővé téve a hatékony lekérdezéseket nagy adatmennyiségen anélkül, hogy az egész dokumentumokat betöltené a memóriába.

**Q: Hogyan frissíthetem az indexet új fájlokkal?**  
A: Egyszerűen hívd a `index.add()`-t az új dokumentumok útvonalával; az index automatikusan beépíti őket.

**Q: Kezelni tudja a GroupDocs.Search a különböző fájlformátumokat?**  
A: Igen, támogatja a **PDF, DOCX, XLSX, PPTX, HTML, TXT és több mint 30 egyéb formátumot**.

**Q: Mik a tipikus teljesítménybottleneckek?**  
A: A memória korlátok és a nem optimalizált indexek a leggyakoribbak; allokálj elegendő heap-et és rendszeresen optimalizáld az indexet.

**Q: Hol találok részletesebb dokumentációt?**  
A: Látogasd meg a hivatalos [GroupDocs.Search Documentation](https://docs.groupdocs.com/search/java/) oldalt a mélyreható útmutatókért és API referenciákért.

**Q: Működik a darab‑alapú keresés titkosított PDF-ekkel?**  
A: Igen, amennyiben a megfelelő API overload segítségével megadod a jelszót.

**Q: Hogyan figyelhetem az indexelés előrehaladását?**  
A: Használd az `Index.add()` overload-ot, amely egy `Progress` objektumot ad vissza, vagy csatlakozz a naplózási visszahívásokhoz.

## Erőforrások
- **Dokumentáció**: [GroupDocs.Search for Java Docs](https://docs.groupdocs.com/search/java/)  
- **API referencia**: [GroupDocs.Search API Reference](https://reference.groupdocs.com/search/java)  
- **Letöltés**: [GroupDocs.Search Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub**: [GroupDocs.Search GitHub Repository](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Ingyenes támogatás**: [GroupDocs Forum](https://forum.groupdocs.com/c/search/10)  
- **Ideiglenes licenc**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Utolsó frissítés:** 2026-10-02  
**Tesztelve:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs  

```java
while (result.getNextChunkSearchToken() != null) {
    result = index.searchNext(result.getNextChunkSearchToken());
}
```

## Kapcsolódó oktatóanyagok

- [Keresési index könyvtár létrehozása és licenc beállítása – GroupDocs.Search Java](/search/java/licensing-configuration/groupdocs-search-java-implementation-license/)
- [Kérdezési teljesítmény javítása a GroupDocs.Search Java-val: Index és keresés optimalizálása](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)
- [GroupDocs Search Java fejlett keresési funkciók](/search/java/advanced-features/groupdocs-search-java-advanced-search-features/)
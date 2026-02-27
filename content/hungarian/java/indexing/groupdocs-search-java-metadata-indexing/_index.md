---
date: '2026-01-06'
description: Ismerje meg, hogyan adhat hozzá dokumentumokat az indexhez, és hogyan
  kereshet dokumentumokat metaadatok alapján a GroupDocs.Search Java segítségével.
  Tanulja meg az indexbeállításokat, hozza létre az indexeket, adjon hozzá dokumentumokat,
  és hajtson végre pontos kereséseket.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Hogyan adhatunk dokumentumokat az indexhez metaadat-indexeléssel Java-ban a
  GroupDocs.Search segítségével
type: docs
url: /hu/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Hogyan adjunk dokumentumokat az indexhez metaadat-indexeléssel Java-ban a GroupDocs.Search használatával

A modern alkalmazásokban a **dokumentumok hozzáadása az indexhez** gyors és megbízható végrehajtása elengedhetetlen a gyors keresési élmény biztosításához. Akár jogi adattárat, ügyfélszolgálati tudásbázist vagy belső dokumentumportált építesz, a metaadatok kihasználása lehetővé teszi a **dokumentumok keresése metaadatok alapján** például szerző, cím vagy egyéni címkék szerint. Ez az útmutató végigvezet a teljes folyamaton – az index beállításainak konfigurálásán, egy metaadat‑központú index létrehozásán, a fájlok hozzáadásán és a hatékony keresések futtatásán – mindezt a GroupDocs.Search for Java segítségével.

## Gyors válaszok
- **Mi a metaadat-indexelés elsődleges célja?** Lehetővé teszi a gyors kereséseket a dokumentum tulajdonságai alapján, a teljes szöveges tartalom helyett.  
- **Melyik metódus adja hozzá a fájlokat az indexhez?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Kereshetek egyéni metaadatmezők szerint?** Igen, miután a mezők indexelve vannak, közvetlenül lekérdezhetők.  
- **Szükségem van licencre a fejlesztéshez?** Egy ideiglenes próbaverzió licenc elegendő az értékeléshez; a teljes licenc a termeléshez kötelező.  
- **Milyen Java verzió szükséges?** JDK 8 vagy újabb ajánlott.

## Mi a metaadat-indexelés a GroupDocs.Search-ben?
A metaadat-indexelés kinyeri és tárolja a dokumentum attribútumait (pl. szerző, létrehozás dátuma, egyéni címkék) egy kereshető struktúrában. Amikor **dokumentumok hozzáadása az indexhez**, a motor rögzíti ezeket az attribútumokat, lehetővé téve pontos lekérdezések futtatását, például „keresd meg az összes PDF-et, amelyet *John Doe* írt”.

## Miért használjuk a GroupDocs.Search-t metaadat-indexeléshez?
- **Teljesítmény:** A metaadat keresések könnyűek és ezredmásodpercek alatt visszaadják az eredményeket.  
- **Rugalmasság:** Széles körű fájlformátumot támogat (PDF, DOCX, PPT stb.).  
- **Skálázhatóság:** Millió dokumentumot kezel minimális memóriahasználattal.

## Előfeltételek
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 vagy újabb telepítve és konfigurálva.  
- Alapvető ismeretek a Java és Maven használatában.

## A GroupDocs.Search for Java beállítása

### Telepítési útmutató
Add the GroupDocs repository and dependency to your `pom.xml`:

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

A legújabb binárisokat közvetlenül letöltheted innen: [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Licenc beszerzése
Ideiglenes licenc beszerzéséhez teszteléshez:

1. Látogasd meg a GroupDocs weboldalát, és menj a **Purchase** szekcióba.  
2. Válassz egy **temporary license** csomagot, amely megfelel az értékelési igényeidnek.

## Lépésről‑lépésre megvalósítás

### 1. funkció: Index beállítások konfigurálása
Állítsd be az indexet, hogy a metaadatokra fókuszáljon:

```java
import com.groupdocs.search.IndexSettings;
import com.groupdocs.search.IndexType;

// Initialize index settings
IndexSettings settings = new IndexSettings();
settings.setIndexType(IndexType.MetadataIndex);  // Focus on metadata indexing
```

- `setIndexType(IndexType.MetadataIndex)` azt mondja a motornak, hogy a metaadatokat részesítse előnyben a teljes szöveges tartalom helyett.

### 2. funkció: Index létrehozása megadott mappában
Hozz létre egy fizikai index könyvtárat, ahol az összes metaadat tárolódik:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Cseréld le a `YOUR_DOCUMENT_DIRECTORY`-t arra az útvonalra, amely megfelel a projekt felépítésének.

### 3. funkció: Hogyan adjunk dokumentumokat az indexhez
Most, hogy az index létezik, **dokumentumok hozzáadása az indexhez** lehetővé teszi, hogy kereshetővé váljanak:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tippek:**  
- Ellenőrizd, hogy a mappa útvonala helyes-e, és az alkalmazásnak van olvasási jogosultsága.  
- A GroupDocs.Search automatikusan kinyeri a támogatott metaadatokat minden egyes fájlból.

### 4. funkció: Dokumentumok keresése metaadatok alapján
Futtass egy lekérdezést, amely a metaadatmezőket célozza, például keresd a dokumentumokat, ahol a nyelv angol:

```java
import com.groupdocs.search.results.SearchResult;

String query = "English";  // Define search query
SearchResult result = index.search(query);  // Perform the search

// Process results (example)
for (int i = 0; i < result.getDocumentCount(); i++) {
    System.out.println("Found document: " + result.getFoundDocument(i).getFilePath());
}
```

- `search(query)` átnézi az indexelt metaadatokat és visszaadja a megfelelő dokumentumokat.

## Gyakorlati alkalmazások
1. **Vállalati dokumentumkezelés:** Szerződések lekérdezése szerződés dátuma vagy aláíró neve alapján.  
2. **Digitális könyvtári katalógusok:** A felhasználók böngészhetnek könyveket műfaj, kiadási év vagy szerző szerint.  
3. **CRM rendszerek:** Gyorsan megtalálhatók az ügyfél fájlok egyéni metaadatok, például ügyfél‑azonosító vagy régió alapján.

## Teljesítményfontosságú szempontok
- **Inkrementális frissítések:** Használd a `index.addOrUpdate()`-t új vagy módosított fájlokhoz a teljes index újraépítése helyett.  
- **Memóriahangolás:** Állítsd be a JVM heap méretét (`-Xmx`) az indexelt metaadat mennyisége alapján.  
- **Optimalizált tárolás:** Időnként hívd meg a `index.optimize()`-t az index tömörítéséhez és a lekérdezési sebesség javításához.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **No results returned** | Erősítsd meg, hogy a várt metaadatmezők valóban jelen vannak a forrásfájlokban. |
| **Permission errors** | Győződj meg arról, hogy a Java folyamatnak olvasási hozzáférése van a dokumentum mappához és az index könyvtárhoz egyaránt. |
| **Out‑of‑memory errors** | Növeld a JVM heap méretét, vagy kötegeld a `add` műveletet, hogy a fájlokat kisebb csoportokban dolgozd fel. |

## Gyakran Ismételt Kérdések

**Q: Mi a metaadat-indexelés?**  
A: A metaadat-indexelés a dokumentum attribútumait (szerző, cím, egyéni címkék) egy kereshető struktúrában tárolja, lehetővé téve a gyors keresést a teljes szöveg beolvasása nélkül.

**Q: Hogyan szerezhetek ideiglenes licencet?**  
A: Látogasd meg a GroupDocs vásárlási oldalt, és kövesd a lépéseket a próbaverzió licenc beszerzéséhez.

**Q: Indexelhetek PDF-eket ezzel a beállítással?**  
A: Igen, a GroupDocs.Search támogatja a PDF, DOCX, PPT és sok más formátumot.

**Q: Milyen gyakori problémák merülnek fel dokumentumok hozzáadása során?**  
A: Ellenőrizd a helyes fájlútvonalakat, és győződj meg arról, hogy az alkalmazásnak olvasási jogosultsága van a könyvtárakhoz.

**Q: Hogyan optimalizálhatom a keresési teljesítményt?**  
A: Rendszeresen frissítsd az indexet, használj inkrementális hozzáadásokat, és hangold a JVM memória beállításait.

## Források

- **Documentation:** [GroupDocs.Search Java Documentation](https://docs.groupdocs.com/search/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/search/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/search/java/)  
- **GitHub Repository:** [GroupDocs.Search GitHub](https://github.com/groupdocs-search/GroupDocs.Search-for-Java)  
- **Free Support Forum:** [GroupDocs Community Forum](https://forum.groupdocs.com/c/search/10)  
- **Temporary License:** [Obtain Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-01-06  
**Tested With:** GroupDocs.Search Java 25.4  
**Author:** GroupDocs
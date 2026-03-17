---
date: '2026-03-17'
description: Tanulja meg, hogyan adjon dokumentumokat az indexhez, és kereshet dokumentumokat
  metaadatok alapján a GroupDocs.Search Java segítségével. Ismerje meg az indexbeállításokat,
  hozza létre az indexeket, adjon hozzá dokumentumokat, és hajtson végre pontos kereséseket.
keywords:
- metadata indexing java
- GroupDocs Search Java
- document management with metadata
title: Hogyan adhatunk dokumentumokat az indexhez metaadat-indexeléssel Java-ban a
  GroupDocs.Search használatával
type: docs
url: /hu/java/indexing/groupdocs-search-java-metadata-indexing/
weight: 1
---

# Hogyan adjunk dokumentumokat az indexhez metaadat-indexeléssel Java-ban a GroupDocs.Search használatával

A dokumentumok gyors és megbízható indexelése bármely modern keresés‑alapú alkalmazás gerince. Akár jogi adattárat, ügyfélszolgálati tudásbázist vagy belső dokumentumportált építesz, a **metadata indexing** lehetővé teszi, hogy *metaadatok alapján keress dokumentumokat*, például szerző, cím vagy egyedi címkék szerint. Ebben az útmutatóban megtanulod, hogyan konfiguráld az index beállításait, hozz létre egy metaadat‑központú indexet, add hozzá a fájljaidat, és futtass pontos kereséseket – mindezt a GroupDocs.Search for Java segítségével.

## Gyors válaszok
- **Mi a metaadat-indexelés elsődleges célja?** Lehetővé teszi a gyors keresést a dokumentum tulajdonságai alapján, a teljes szöveges tartalom helyett.  
- **Melyik metódus adja hozzá a fájlokat az indexhez?** `index.add(YOUR_DOCUMENTS_FOLDER);`  
- **Kereshetek egyedi metaadatmezőkkel?** Igen, miután a mezők indexelve lettek, közvetlenül lekérdezhetők.  
- **Szükségem van licencre a fejlesztéshez?** Egy ideiglenes próba licenc elegendő az értékeléshez; a teljes licenc a termeléshez szükséges.  
- **Milyen Java verzió szükséges?** JDK 8 vagy újabb ajánlott.

## Mi a metaadat-indexelés a GroupDocs.Search-ben?
A metaadat-indexelés kinyeri és tárolja a dokumentum attribútumait (pl. szerző, létrehozás dátuma, egyedi címkék) egy kereshető struktúrában. Amikor **dokumentumokat adsz hozzá az indexhez**, a motor rögzíti ezeket az attribútumokat, lehetővé téve pontos lekérdezések futtatását, mint például „keresd meg az összes PDF-et, amelyet *John Doe* írt” vagy „keresd a pdf-et szerző szerint”.

## Miért használjuk a GroupDocs.Search-t metaadat-indexeléshez?
- **Teljesítmény:** A metaadat-keresések könnyűek és milliszekundumok alatt visszaadják az eredményeket.  
- **Rugalmasság:** Széles körű fájlformátumot támogat (PDF, DOCX, PPT, stb.).  
- **Skálázhatóság:** Millió dokumentumot kezel minimális memóriahasználattal.

## Előfeltételek
- GroupDocs.Search for Java ≥ 25.4.  
- JDK 8 vagy újabb telepítve és konfigurálva.  
- Alapvető ismeretek a Java és Maven használatáról.  

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

A legújabb binárisokat közvetlenül letöltheted a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Licenc beszerzése
Ideiglenes licenc beszerzéséhez a teszteléshez:

1. Látogasd meg a GroupDocs weboldalát, és menj a **Purchase** szekcióba.  
2. Válassz egy **temporary license** tervet, amely megfelel az értékelési igényeidnek.  

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

### 2. funkció: Index létrehozása egy megadott mappában
Hozz létre egy fizikai indexkönyvtárat, ahol minden metaadat tárolva lesz:

```java
import com.groupdocs.search.Index;

String YOUR_INDEX_DIRECTORY = "YOUR_DOCUMENT_DIRECTORY\\\\output\\\\AdvancedUsage\\\\Indexing\\\\IndexingMetadataOfDocuments";

// Create index in specified directory using settings
Index index = new Index(YOUR_INDEX_DIRECTORY, settings);
```

Cseréld le a `YOUR_DOCUMENT_DIRECTORY`-t arra az útra, amely megfelel a projekt felépítésének.

### 3. funkció: Dokumentumok hozzáadása az indexhez
Most, hogy az index létezik, **add documents to index**-et használhatod, hogy kereshetővé tedd őket:

```java
String YOUR_DOCUMENTS_FOLDER = "YOUR_DOCUMENT_DIRECTORY";

// Add all documents in directory to the index
index.add(YOUR_DOCUMENTS_FOLDER);
```

**Tippek:**  
- Ellenőrizd, hogy a mappa útvonala helyes, és az alkalmazásnak olvasási jogosultsága van.  
- A GroupDocs.Search automatikusan kinyeri a támogatott metaadatokat minden fájlból.

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

- `search(query)` átnézi az indexelt metaadatokat, és visszaadja a megfelelő dokumentumokat.  
- **search pdf by author** is also possible by using the author's name as the query string.

## Gyakorlati alkalmazások
1. **Enterprise Document Management:** Szerződések lekérdezése szerződés dátuma vagy aláíró neve alapján.  
2. **Digital Library Catalogs:** Lehetővé teszi a felhasználók számára, hogy könyveket műfaj, kiadási év vagy szerző szerint böngésszenek.  
3. **CRM Systems:** Gyorsan megtalálja az ügyfél fájlokat egyedi metaadatok, például ügyfél‑azonosító vagy régió alapján.  

## Tippek és bevált gyakorlatok
- **Inkrementális frissítések:** Használd a `index.addOrUpdate()`-t új vagy módosított fájlokhoz a teljes index újraépítése helyett.  
- **Kötegelt feldolgozás:** Több ezer fájl esetén add hozzá őket kisebb kötegekben a memóriahasználat alacsonyan tartása érdekében.  
- **Metaadat ellenőrzés:** Győződj meg arról, hogy a forrásdokumentumok valóban tartalmazzák a lekérdezni kívánt metaadatokat (pl. szerző mezők a PDF-ekben).  

## Teljesítmény szempontok
- **Memória hangolás:** Állítsd be a JVM heap méretét (`-Xmx`) az indexelt metaadat mennyisége alapján.  
- **Optimalizált tárolás:** Időnként hívd meg a `index.optimize()`-t az index tömörítéséhez és a lekérdezési sebesség javításához.  

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **Nincs eredmény** | Ellenőrizd, hogy a várt metaadatmezők valóban jelen vannak-e a forrásfájlokban. |
| **Jogosultsági hibák** | Győződj meg arról, hogy a Java folyamatnak olvasási hozzáférése van mind a dokumentummappához, mind az indexkönyvtárhoz. |
| **Memóriahiány hibák** | Növeld a JVM heap méretét, vagy kötegeld a `add` műveletet, hogy a fájlokat kisebb csoportokban dolgozd fel. |

## Gyakran feltett kérdések

**Q: Mi a metaadat-indexelés?**  
A: A metaadat-indexelés a dokumentum attribútumait (szerző, cím, egyedi címkék) egy kereshető struktúrában tárolja, lehetővé téve a gyors lekérdezéseket a teljes szöveg átvizsgálása nélkül.

**Q: Hogyan szerezhetek ideiglenes licencet?**  
A: Látogasd meg a GroupDocs vásárlási oldalt, és kövesd a lépéseket a próba licenc megszerzéséhez.

**Q: Indexelhetek PDF-eket ezzel a beállítással?**  
A: Igen, a GroupDocs.Search támogatja a PDF, DOCX, PPT és sok más formátumot.

**Q: Mik a gyakori problémák dokumentumok hozzáadása közben?**  
A: Ellenőrizd a helyes fájlutakat, és győződj meg arról, hogy az alkalmazásnak olvasási jogosultsága van a könyvtárakhoz.

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

**Legutóbb frissítve:** 2026-03-17  
**Tesztelve ezzel:** GroupDocs.Search Java 25.4  
**Szerző:** GroupDocs
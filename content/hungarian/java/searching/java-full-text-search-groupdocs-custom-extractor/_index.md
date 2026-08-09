---
date: '2026-08-05'
description: Ismerje meg, hogyan építhet log file extractor-t a Java-ban a GroupDocs.Search
  segítségével a full-text search-hez. Dokumentumokat adhat az indexhez, optimalizálhatja
  a keresési teljesítményt, és nagy log file-okat kezelhet hatékonyan.
keywords:
- full text search java
- optimize search performance
- add documents to index
- java full text search
lastmod: '2026-08-05'
og_description: A Full text search java oktatóanyag bemutatja, hogyan építhet egy
  egyedi log file extractor-t a GroupDocs.Search használatával, hogyan adhat dokumentumokat
  az indexhez, és hogyan optimalizálhatja a keresési teljesítményt hatalmas log archívumok
  esetén.
og_image_alt: Diagram of log file extractor workflow in Java using GroupDocs.Search
og_title: 'Full text search java: log file extractor a GroupDocs-szal'
schemas:
- author: GroupDocs
  dateModified: '2026-08-05'
  description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  headline: 'Full text search java: log file extractor with GroupDocs'
  type: TechArticle
- description: Learn how to build a log file extractor for full-text search in Java
    using GroupDocs.Search. Add documents to index, optimize search performance, and
    handle large log files efficiently.
  name: 'Full text search java: log file extractor with GroupDocs'
  steps:
  - name: define the custom extractor
    text: '`TextExtractorBase` is the abstract base class you extend to create a custom
      extractor. It declares which file extensions the extractor supports and contains
      the core extraction logic. **Key points** - `getFileExtensions()` registers
      the extractor for `.log` files. - `extractText` is where you can s'
  - name: configure index settings with the extractor
    text: Add your extractor to the `IndexSettings` and enable `autoReindex` so new
      logs are indexed automatically without manual intervention. `IndexSettings`
      configures index behavior such as memory limits and custom extractors. `autoReindex`
      automatically updates the index when source files change.
  - name: add documents to the index
    text: Now that the index recognises log files, you can **add documents to index**
      just like any other supported format.
  - name: search the index
    text: Perform plain‑text queries. The custom extractor guarantees that every log
      entry is searchable.
  type: HowTo
- questions:
  - answer: The default extractor handles common formats (PDF, DOCX, etc.). A custom
      log file extractor lets you define exactly how plain‑text log entries are parsed
      and indexed.
    question: How does a log file extractor differ from the default extractor?
  - answer: Yes, by adding a pre‑processing step that extracts files from the archive
      before feeding them to the index.
    question: Can I index compressed log archives (e.g., .zip)?
  - answer: Enable `autoReindex` and schedule a background watcher that calls `index.add(newLogFile)`
      whenever a new file appears.
    question: What’s the best way to keep the index up‑to‑date with continuously generated
      logs?
  - answer: Practically, the limit is bound by available memory. Splitting very large
      logs into smaller chunks before indexing is recommended.
    question: Is there a limit to the size of a single log file that can be indexed?
  - answer: Yes, the search API includes fuzzy matching, wildcards, and proximity
      queries to improve result relevance.
    question: Does GroupDocs.Search support fuzzy or wildcard searches?
  type: FAQPage
tags:
- full text search
- GroupDocs
- Java search
- log file extractor
- indexing
title: 'Full text search java: log file extractor a GroupDocs-szal'
type: docs
url: /hu/java/searching/java-full-text-search-groupdocs-custom-extractor/
weight: 1
---

# Java teljes szöveges keresés: naplófájl kinyerő a GroupDocs-szal

A Java teljes‑szöveges keresés alapvető minden olyan rendszer számára, amelynek gyorsan kell információt megtalálnia hatalmas dokumentumgyűjteményekben. Ebben az útmutatóban megtanulja, hogyan konfigurálja a GroupDocs.Search‑t, hogyan hoz létre egy egyedi naplófájl kinyerőt, hogyan ad dokumentumokat az indexhez, és hogyan optimalizálja a keresési teljesítményt gigabájtoknyi naplóadatok kezelésekor.

## Mit fogsz megtanulni
- A GroupDocs.Search Java-hoz történő beállítása és konfigurálása.  
- Egy **log file extractor** megvalósítása, amely a nyers szöveges naplókat a kívánt módon elemzi.  
- **Add documents to index** PDF-ek, DOCX-ek és egyéb formátumok mellett.  
- Valós példák, ahol egy **log file extractor** mérhető értéket ad.  
- Bizonyított tippek a **optimise search performance** több gigabájtos naplóarchívumok esetén.

## Gyors válaszok
- **What is a log file extractor?** Egy egyedi komponens, amely megmondja a GroupDocs.Search‑nek, hogyan olvassa és indexelje a nyers szöveges naplófájlokat.  
- **Why use GroupDocs.Search?** Támogatja az 50+ formátum indexelését, automatikus újraindexelést biztosít, és akár 10 GB‑os indexeket is kezel kevesebb, mint 2 GB RAM-mal.  
- **Do I need a license?** Igen – egy próba vagy teljes licenc szükséges a könyvtár engedélyezéséhez.  
- **Can I index other file types simultaneously?** Természetesen; keverhet PDF-eket, DOCX-eket és egyedi naplófájlokat ugyanabban az indexben.  
- **How to improve performance?** Használjon inkrementális indexelést, finomhangolja az `IndexSettings`‑et, és engedélyezze az `autoReindex` zászlót.

## Előfeltételek

Mielőtt elkezdené, győződjön meg róla, hogy a következőkkel rendelkezik:

### Szükséges könyvtárak
Add the GroupDocs.Search Maven dependency to your `pom.xml`. Use the latest version that matches your project’s Java level.

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

Alternatív megoldásként töltse le a legújabb verziót közvetlenül a [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/) oldalról.

### Környezet beállítása
- JDK 8 vagy újabb.  
- Java programozás és alapvető fájlkezelési fogalmak ismerete.

### Licenc beszerzése
Kezdje egy ingyenes próbalicenc letöltésével a GroupDocs.Search funkcióinak felfedezéséhez. Termelésben való használathoz vásároljon teljes licencet, vagy kérjen ideiglenes licencet a [GroupDocs weboldalán](https://purchase.groupdocs.com/temporary-license/).

## A GroupDocs.Search Java-hoz történő beállítása

A kezdéshez inicializálja a könyvtárat, és alkalmazza a licencfájlt:

1. **Maven setup** – ellenőrizze, hogy az előző lépésben megadott függőség jelen van.  
2. **License initialisation** – töltse be a licencfájlt minden egyéb API hívás előtt.

```java
   License license = new License();
   license.setLicense("path/to/license");
   ```

A környezet készen áll, folytathatja az egyedi **log file extractor** felépítésével.

## Mi az a log file extractor?

A log file extractor egy kódrészlet, amely megmondja a GroupDocs.Search‑nek, hogyan olvassa a nyers naplófájlokat (általában `.log`) és alakítsa azok tartalmát kereshető szöveggé. Saját kinyerő biztosításával teljes irányítást kap a feldolgozási szabályok, a zajszűrés és csak a keresési esethez releváns információk kinyerése felett.

## Log file extractor létrehozása

A GroupDocs.Search lehetővé teszi egyedi szövegkinyerők csatlakoztatását bármely fájltípushoz. Kövesse ezeket a lépéseket egy naplófájlokhoz való kinyerő felépítéséhez.

### 1. lépés: egyedi kinyerő definiálása
`TextExtractorBase` az absztrakt alaposztály, amelyet kiterjesztve hozhat létre egy egyedi kinyerőt. Meghatározza, mely fájlkiterjesztéseket támogatja a kinyerő, és tartalmazza a fő kinyerési logikát.

```java
import com.groupdocs.search.extractors.TextExtractorBase;

public class LogExtractor extends TextExtractorBase {
    @Override
    public String[] getFileExtensions() {
        return new String[]{"log"};
    }

    @Override
    public String extractText(String documentContent) {
        // Custom logic for extracting text from log files.
        return documentContent; // Implement your custom extraction here.
    }
}
```

**Key points**  
- `getFileExtensions()` regisztrálja a kinyerőt a `.log` fájlokhoz.  
- `extractText` az a hely, ahol eltávolíthatja az időbélyegeket, kiszűrheti a hibakeresési sorokat, vagy bármilyen előfeldolgozást alkalmazhat a **search large log files** (nagy naplófájlok kereséséhez) esetén.

### 2. lépés: indexbeállítások konfigurálása a kinyerővel
Adja hozzá a kinyerőt az `IndexSettings`‑hez, és engedélyezze az `autoReindex`‑et, hogy az új naplókat automatikusan indexelje manuális beavatkozás nélkül.

`IndexSettings` konfigurálja az index viselkedését, például a memóriahatárokat és az egyedi kinyerőket.  
`autoReindex` automatikusan frissíti az indexet, amikor a forrásfájlok változnak.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.IndexSettings;

public class CustomTextExtractorFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        IndexSettings settings = new IndexSettings();
        
        // Adding the custom text extractor to the settings.
        settings.getCustomExtractors().addItem(new LogExtractor());
        
        // Creating or loading an index with specified settings and enabling auto-reindexing.
        Index index = new Index(indexFolder, settings, true);
    }
}
```

### 3. lépés: dokumentumok hozzáadása az indexhez
Most, hogy az index felismeri a naplófájlokat, **add documents to index**-et használhat, mint bármely más támogatott formátumot.

```java
import com.groupdocs.search.Index;

public class AddDocumentsToIndexFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        String documentsFolder = "YOUR_DOCUMENT_DIRECTORY";
        
        // Loading or creating an index in the specified directory.
        Index index = new Index(indexFolder);
        
        // Adding documents from the folder to the index.
        index.add(documentsFolder);
    }
}
```

### 4. lépés: az index keresése
Végezzen egyszerű szöveges lekérdezéseket. Az egyedi kinyerő garantálja, hogy minden naplóbejegyzés kereshető legyen.

```java
import com.groupdocs.search.Index;
import com.groupdocs.search.results.SearchResult;

public class SearchDocumentsFeature {
    public static void main(String[] args) {
        String indexFolder = "YOUR_OUTPUT_DIRECTORY";
        
        // Loading the existing index.
        Index index = new Index(indexFolder);
        
        // Define search queries
        String query1 = "objection";
        String query2 = "log";
        
        // Performing searches and retrieving results.
        SearchResult result1 = index.search(query1);
        SearchResult result2 = index.search(query2);
    }
}
```

## Tippek a keresési teljesítmény optimalizálásához
- **Incremental indexing** – csak az új vagy módosított naplófájlokat adja hozzá, a teljes index újraépítése helyett.  
- **Memory management** – az `autoReindex` zászló alacsony RAM használatot biztosít, az köztes adatokat lemezre írva.  
- **Index settings** – állítsa be a `setMaxMemoryUsage`‑t a szerver kapacitása alapján; egy tipikus beállítás 1 GB egy 10 GB-os indexhez.  
- **Query optimisation** – használjon kifejezés lekérdezéseket, helyettesítő karaktereket vagy szűrőket a találatok szűkítéséhez hatalmas naplóarchívumok keresésekor.

## Gyakorlati alkalmazások

A GroupDocs.Search számos valós példában alkalmazható, például:

- **Log management** – hibajelzések, felhasználói tevékenységek vagy konkrét időbélyegek megtalálása gigabájtoknyi naplóadatok között másodpercek alatt.  
- **Document retrieval systems** – egyetlen kereshető tároló fenntartása, amely PDF-eket, Word dokumentumokat, táblázatokat és egyedi naplófájlokat tartalmaz.  
- **Content analysis** – kulcsszó‑gyakorisági jelentések futtatása vagy anomáliák észlelése a folyamatos naplóadatokban.

## Teljesítménybeli megfontolások

A GroupDocs.Search nagy léptékű telepítésekor tartsa szem előtt ezeket a bevált gyakorlatokat:

- Tárolja az indexeket gyors SSD-ken a beolvasási/írási késleltetés minimalizálása érdekében.  
- Figyelje a JVM heap használatát; fontolja meg a nagy indexek külön folyamatba való áthelyezését, ha a memória szűk keresztmetszet lesz.  
- Engedélyezze az `autoReindex`‑et (ahogyan látható), hogy az index friss maradjon manuális újraépítés nélkül.

## Összegzés

Eddig elkészítette a **log file extractor**-t, megtanulta, hogyan **add documents to index**, és felfedezte a **optimise search performance** módjait nagy naplóarchívumok esetén. Ez a kombináció lehetővé teszi, hogy Java alkalmazásai gyors, pontos teljes‑szöveges keresést biztosítsanak bármilyen dokumentumtípuson.

A mélyebb felfedezéshez tekintse meg a hivatalos [GroupDocs documentation](https://docs.groupdocs.com/search/java/) oldalt, vagy kísérletezzen különböző kinyerő megvalósításokkal, hogy megfeleljen egyedi felhasználási esetének.

## GYIK szekció
1. **Milyen fájltípusokat indexelhetek a GroupDocs.Search segítségével?**  
   - PDF-eket, Word dokumentumokat, táblázatokat és sok más formátumot indexelhet, valamint egyedi naplófájlokat szövegkinyerők segítségével.  
2. **Hogyan kezeljem hatékonyan a nagy dokumentumgyűjteményeket?**  
   - Inkrementális frissítéseket használjon, partícionálja az indexeket, és finomhangolja az `IndexSettings`‑et a erőforrások hatékony kezelése érdekében.  
3. **Integrálható a GroupDocs.Search más rendszerekkel?**  
   - Igen, tiszta Java API-t kínál, amely beágyazható meglévő szolgáltatásokba, mikro‑szolgáltatásokba vagy webalkalmazásokba.  
4. **Mi az ideiglenes licenc, és hogyan szerezhetek egyet?**  
   - Az ideiglenes licenc teljes funkcionalitást biztosít a korlátlan időtartamú értékeléshez. Jelentkezzen a [GroupDocs weboldalán](https://purchase.groupdocs.com/temporary-license/).

## Gyakran ismételt kérdések

**Q: Miben különbözik a log file extractor az alapértelmezett kinyerőtől?**  
A: Az alapértelmezett kinyerő a gyakori formátumokat kezeli (PDF, DOCX, stb.). Egy egyedi log file extractor lehetővé teszi, hogy pontosan meghatározza, hogyan kerülnek feldolgozásra és indexelésre a nyers szöveges naplóbejegyzések.

**Q: Indexelhetek tömörített naplóarchívumokat (pl. .zip)?**  
A: Igen, egy előfeldolgozó lépés hozzáadásával, amely kicsomagolja a fájlokat az archívumból, mielőtt az indexnek átadná őket.

**Q: Mi a legjobb módja annak, hogy az index naprakész maradjon a folyamatosan generált naplókkal?**  
A: Engedélyezze az `autoReindex`‑et, és ütemezzen egy háttérfigyelőt, amely minden új fájl megjelenésekor meghívja az `index.add(newLogFile)`‑t.

**Q: Van korlátja egyetlen indexelhető naplófájl méretének?**  
A: Gyakorlatilag a korlát a rendelkezésre álló memória függvénye. Ajánlott a nagyon nagy naplókat kisebb darabokra bontani az indexelés előtt.

**Q: Támogatja a GroupDocs.Search a homályos vagy helyettesítő karakteres kereséseket?**  
A: Igen, a keresési API tartalmaz homályos egyezést, helyettesítő karaktereket és közelségi lekérdezéseket a találati relevancia javítása érdekében.

---

**Utolsó frissítés:** 2026-08-05  
**Tesztelve a következővel:** GroupDocs.Search 25.4 for Java  
**Szerző:** GroupDocs

## Kapcsolódó oktatóanyagok

- [Java teljes szöveges keresés: index felépítése a GroupDocs.Search segítségével](/search/java/dictionaries-language-processing/master-alphabet-dictionary-indexing-groupdocs-search-java/)
- [Hogyan adjunk dokumentumokat az indexhez a GroupDocs.Search for Java segítségével](/search/java/indexing/implement-document-indexing-groupdocs-search-java/)
- [Kérdezési teljesítmény javítása a GroupDocs.Search Java-val: index és keresés optimalizálása](/search/java/performance-optimization/master-groupdocs-search-java-index-query-optimization/)